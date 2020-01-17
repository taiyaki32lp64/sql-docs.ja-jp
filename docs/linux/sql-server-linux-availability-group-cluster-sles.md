---
title: SUSE:SQL Server on Linux の可用性グループを構成する
titleSuffix: SQL Server
description: SUSE Linux Enterprise Server (SLES) 用の可用性グループ クラスターを作成する方法について説明します。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 04/30/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 85180155-6726-4f42-ba57-200bf1e15f4d
ms.openlocfilehash: 89f8616b13f80642a62922d9a1e1023f153b23cb
ms.sourcegitcommit: 035ad9197cb9799852ed705432740ad52e0a256d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/31/2019
ms.locfileid: "75558447"
---
# <a name="configure-sles-cluster-for-sql-server-availability-group"></a>SQL Server 可用性グループ用の SLES クラスターを構成する

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

このガイドでは、SUSE Linux Enterprise Server (SLES) 12 SP2 の SQL Server 用に 3 ノード クラスターを作成する手順について説明します。 高可用性を実現するため、Linux 上の可用性グループには 3 つのノードが必要です。[可用性グループ構成の高可用性とデータ保護](sql-server-linux-availability-group-ha.md)に関するページを参照してください。 クラスタリング レイヤーは、[Pacemaker](https://clusterlabs.org/) の上に構築された SUSE [High Availability Extension (HAE)](https://www.suse.com/products/highavailability) に基づいています。 

クラスター構成、リソース エージェントのオプション、管理、ベスト プラクティス、推奨事項の詳細については、「[SUSE Linux Enterprise High Availability Extension 12 SP2](https://www.suse.com/documentation/sle-ha-12/index.html)」を参照してください。

>[!NOTE]
>現時点では、Linux 上の SQL Server と Pacemaker の統合では、Windows 上の WSFC のような連携は行われていません。 Linux の SQL Server サービスはクラスターに対応していません。 Pacemaker は、可用性グループ リソースを含む、クラスター リソースのすべてのオーケストレーションを制御します。 Linux では、sys.dm_hadr_cluster などのクラスター情報を提供する Always On 可用性グループの動的管理ビュー (DMV) に依存しないようにする必要があります。 さらに、仮想ネットワーク名は WSFC に固有のものであり、Pacemaker にはそれに該当するものはありません。 フェールオーバー後に透過的な再接続に使用するリスナーを引き続き作成できますが、仮想 IP リソースの作成に使用する IP で、DNS サーバーにリスナー名を手動で登録する必要があります (以下のセクションで説明します)。


## <a name="roadmap"></a>ロードマップ

高可用性のための可用性グループを作成する手順は、Linux サーバーと Windows Server フェールオーバー クラスターで異なります。 以下に、おおまかな手順を説明します。 

1. [クラスター ノードで SQL Server を構成します](sql-server-linux-setup.md)。

2. [可用性グループを作成します](sql-server-linux-availability-group-failover-ha.md)。 

3. Pacemaker などのクラスター リソース マネージャーを構成します。 これらの手順についてはこのドキュメントで説明します。
   
   クラスター リソース マネージャーを構成する方法は、特定の Linux ディストリビューションによって異なります。 

   >[!IMPORTANT]
   >運用環境では、高可用性のために STONITH のようなフェンス エージェントが必要です。 この記事の例では、フェンス エージェントは使用しません。 これらはテストと検証専用です。 
   
   >Pacemaker クラスターは、フェンスを使用してクラスターを既知の状態に戻します。 フェンスを構成する方法は、ディストリビューションと環境によって異なります。 現時点では、一部のクラウド環境ではフェンスを利用できません。 「[SUSE Linux Enterprise High Availability Extension](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#cha.ha.fencing)」を参照してください。

5. [可用性グループをクラスターのリソースとして追加します](sql-server-linux-availability-group-cluster-sles.md#configure-the-cluster-resources-for-sql-server)。 

## <a name="prerequisites"></a>前提条件

次のエンドツーエンドのシナリオを完了するには、3 つのノード クラスターをデプロイするために 3 台のマシンが必要です。 次の手順では、これらのサーバーを構成する方法を示します。

## <a name="setup-and-configure-the-operating-system-on-each-cluster-node"></a>各クラスター ノードにオペレーティング システムをセットアップして構成する 

最初の手順は、クラスター ノード上のオペレーティング システムを構成することです。 このチュートリアルでは、HA アドオンの有効なサブスクリプションで SLES 12 SP2 を使用します。

### <a name="install-and-configure-sql-server-service-on-each-cluster-node"></a>各クラスター ノードに SQL Server サービスをインストールして構成する

1. すべてのノードに SQL Server サービスをインストールしてセットアップします。 詳細については、[SQL Server on Linux のインストール](sql-server-linux-setup.md)に関するページを参照してください。

1. 1 つのノードをプライマリ ノードとして指定し、その他のノードをセカンダリとして指定します。 このガイド全体でこれらの用語を使用します。

1. クラスターの一部となるノードが相互に通信できることを確認します。

   次の例は `/etc/hosts` を示しています。SLES1、SLES2、および SLES3 という 3 つのノードに対して追加があります。

   ```
   127.0.0.1   localhost
   10.128.16.33 SLES1
   10.128.16.77 SLES2
   10.128.16.22 SLES3
   ```

   すべてのクラスター ノードは、SSH を使用して相互にアクセスできる必要があります。 `hb_report` または `crm_report` (トラブルシューティング用) などのツールや Hawk の History Explorer では、ノード間でパスワードなしの SSH アクセスが必要です。それ以外の場合は、現在のノード以外のデータは収集できません。 非標準の SSH ポートを使用する場合は、-X オプションを使用します (`man` ページを参照)。 たとえば、SSH ポートが 3479 の場合は、次のコマンドを実行して `crm_report` を呼び出します。

   ```bash
   sudo crm_report -X "-p 3479" [...]
   ```

   詳細については、[SLES 管理ガイドの「その他」のセクション](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#sec.ha.troubleshooting.misc)を参照してください。


## <a name="create-a-sql-server-login-for-pacemaker"></a>Pacemaker 用の SQL Server ログインを作成する

[!INCLUDE [SLES-Create-SQL-Login](../includes/ss-linux-cluster-pacemaker-create-login.md)]

## <a name="configure-an-always-on-availability-group"></a>Always On 可用性グループを構成する

Linux サーバーで、可用性グループを構成してから、クラスター リソースを構成します。 可用性グループを構成する場合は、[SQL Server on Linux の Always On 可用性グループの構成](sql-server-linux-availability-group-configure-ha.md)に関するページを参照してください

## <a name="install-and-configure-pacemaker-on-each-cluster-node"></a>各クラスター ノードに Pacemaker をインストールして構成する

1. High Availability Extension をインストールする

   リファレンスについては、「[Installing SUSE Linux Enterprise Server and High Availability Extension](https://www.suse.com/documentation/sle-ha-12/singlehtml/install-quick/install-quick.html#sec.ha.inst.quick.installation)」(SUSE Linux Enterprise Server と High Availability Extension のインストール) を参照してください

1. 両方のノードに SQL Server リソース エージェント パッケージをインストールします。

   ```bash
   sudo zypper install mssql-server-ha
   ```

## <a name="set-up-the-first-node"></a>最初のノードを設定する

   [SLES のインストール手順](https://www.suse.com/documentation/sle-ha-12/singlehtml/install-quick/install-quick.html#sec.ha.inst.quick.setup.1st-node)を参照してください

1. クラスター ノードとして使用する物理マシンまたは仮想マシンに、`root` としてログインします。
2. 次のように実行して、ブートストラップ スクリプトを起動します。
   ```bash
   sudo ha-cluster-init
   ```

   NTP が起動時に開始するように構成されていない場合は、メッセージが表示されます。 

   このまま続行する場合は、スクリプトによって SSH アクセス用と Csync2 同期ツール用のキーが自動的に生成され、両方に必要なサービスが開始されます。 

3. クラスター通信レイヤー (Corosync) を構成するには、次のようにします。 

   a. バインド先のネットワーク アドレスを入力します。 既定では、このスクリプトは eth0 のネットワーク アドレスを提示します。 別の方法としては、bond0 のアドレスなどの別のネットワーク アドレスを入力します。 

   b. マルチキャスト アドレスを入力します。 このスクリプトは、既定として使用できるランダムなアドレスを提示します。 

   c. マルチキャスト ポートを入力します。 このスクリプトは、既定として 5405 を提示します。 

   d. `SBD ()` を構成するには、SBD に使用するブロック デバイスのパーティションへの永続的なパスを入力します。 このパスは、クラスター内のすべてのノードで一貫している必要があります。 
   最後に、このスクリプトによって Pacemaker サービスが開始され、1 ノードのクラスターがオンラインになり、Web 管理インターフェイス Hawk2 が有効になります。 Hawk2 に使用する URL が画面に表示されます。 

4. セットアップ プロセスの詳細については、`/var/log/sleha-bootstrap.log` を確認してください。 これで、実行中の 1 ノード クラスターができました。 crm status を使用してクラスターの状態を確認します。

   ```bash
   sudo crm status
   ```

   また、`crm configure show xml` または `crm configure show` でクラスター構成を確認することもできます。

5. ブートストラップ プロシージャで、パスワード linux を使用して hacluster という名前の Linux ユーザーを作成します。 既定のパスワードは、できるだけ早くセキュリティで保護されたものに置き換えてください。 

   ```bash
   sudo passwd hacluster
   ```

## <a name="add-nodes-to-the-existing-cluster"></a>既存のクラスターにノードを追加する

クラスターが 1 つ以上のノードで実行されている場合は、ha-cluster-join ブートストラップ スクリプトを使用してクラスター ノードを追加します。 このスクリプトでは、既存のクラスター ノードへのアクセスが必要になるだけで、現在のマシンの基本的なセットアップが自動的に完了します。 次の手順に従います。

`YaST` クラスター モジュールを使用して既存のクラスター ノードを構成した場合は、`ha-cluster-join` を実行する前に、次の前提条件が満たされていることを確認してください。
- 既存のノードのルート ユーザーに、パスワードなしログイン用の SSH キーがある。 
- `Csync2` が既存のノードに構成されている。 詳細については、YaST による Csync2 の設定に関するページを参照してください。 

1. クラスターに参加することが想定された物理マシンまたは仮想マシンにルートとしてログインします。 
2. 次のように実行して、ブートストラップ スクリプトを起動します。 

   ```bash
   sudo ha-cluster-join
   ```

   NTP が起動時に開始するように構成されていない場合は、メッセージが表示されます。 

3. 続行する場合は、既存のノードの IP アドレスを入力するように求められます。 IP アドレスを入力します。 

4. 両方のマシン間でパスワードなしの SSH アクセスをまだ構成していない場合にも、既存のノードのルート パスワードを入力するように求められます。 

   指定されたノードにログインすると、スクリプトによって Corosync 構成がコピーされ、SSH と `Csync2` が構成され、現在のマシンが新しいクラスター ノードとしてオンラインになります。 それとは別に、Hawk に必要なサービスが開始されます。 共有ストレージを `OCFS2` で構成した場合は、`OCFS2` ファイル システムのマウントポイント ディレクトリも自動的に作成されます。 

5. クラスターに追加するすべてのマシンについて、前の手順を繰り返します。 

6. プロセスの詳細については、`/var/log/ha-cluster-bootstrap.log` を確認してください。 

1. `sudo crm status` を使用してクラスターの状態を確認します。 2 番目のノードが正常に追加されると、次のような出力が表示されます。

   ```bash
   sudo crm status
   
   3 nodes configured
   1 resource configured
   Online: [ SLES1 SLES2 SLES3]
   Full list of resources:   
   admin_addr     (ocf::heartbeat:IPaddr2):       Started node1
   ```

   >[!NOTE]
   >`admin_addr` は、最初の 1 ノード クラスターのセットアップ時に構成された仮想 IP クラスターのリソースです。

すべてのノードを追加した後、グローバル クラスター オプションで no-quorum-policy を調整する必要があるかどうかを確認します。 これは、2 ノード クラスターの場合に特に重要です。 詳細については、セクション 4.1.2 の、オプション no-quorum-policy を参照してください。 

## <a name="set-cluster-property-cluster-recheck-interval"></a>クラスター プロパティ cluster-recheck-interval を設定する

`cluster-recheck-interval` は、クラスターによってリソース パラメーター、制約、またはその他のクラスター オプションの変更が確認されるポーリング間隔を示します。 レプリカがダウンした場合、クラスターでは、`failure-timeout` 値と `cluster-recheck-interval` 値によってバインドされた間隔でレプリカの再起動が試みられます。 たとえば、`failure-timeout` が 60 秒に設定されていて、`cluster-recheck-interval` が 120 秒に設定されている場合、再起動は 60 秒より大きく 120 秒未満の間隔で試行されます。 failure-timeout は 60 秒、cluster-recheck-interval は 60 秒より大きい値に設定することをお勧めします。 cluster-recheck-interval を小さい値に設定することは推奨されません。

プロパティ値を `2 minutes` に更新するには、次を実行します。

```bash
crm configure property cluster-recheck-interval=2min
```

> [!IMPORTANT] 
> 既に Pacemaker クラスターによって管理されている可用性グループ リソースがある場合、使用可能な最新の Pacemaker パッケージ 1.1.18-11.el7 を使用しているすべてのディストリビューションでは、値が false の場合に start-failure-is-fatal クラスター設定の動作が変更されることに注意してください。 この変更は、フェールオーバー ワークフローに影響します。 プライマリ レプリカで障害が発生した場合、クラスターは使用可能なセカンダリ レプリカのいずれかにフェールオーバーする必要があります。 代わりに、クラスターが失敗したプライマリ レプリカを起動しようとしていることがユーザーに通知されます。 そのプライマリが永久に停止したためにオンラインにならない場合は、クラスターが別の使用可能なセカンダリ レプリカにフェールオーバーすることはありません。 この変更により、以前に start-failure-is-fatal を設定するために推奨されていた構成が有効ではなくなったため、この設定を既定値の `true` に戻す必要があります。 さらに、`failover-timeout` プロパティを含めるには、AG リソースを更新する必要があります。 
>
>プロパティ値を `true` に更新するには、次を実行します。
>
>```bash
>crm configure property start-failure-is-fatal=true
>```
>
>既存の AG リソース プロパティ `failure-timeout` を `60s` に更新して、次を実行します (`ag1` は可用性グループ リソースの名前に置き換えてください)。 
>
>```bash
>crm configure edit ag1
># In the text editor, add `meta failure-timeout=60s` after any `param`s and before any `op`s
>```

Pacemaker クラスター プロパティの詳細については、[クラスター リソースの構成](https://www.suse.com/documentation/sle_ha/book_sleha/data/sec_ha_config_crm_resources.html)に関するページを参照してください。

## <a name="configure-fencing-stonith"></a>フェンスを構成する (STONITH)
Pacemaker クラスターのベンダーは、STONITH を有効にして、サポートされているクラスター セットアップ用にフェンス デバイスを構成する必要があります。 クラスター リソース マネージャーでノードまたはノード上のリソースの状態を判断できない場合は、フェンスを使用してクラスターが既知の状態に戻されます。

リソース レベルのフェンスは、主に、リソースを構成することによって障害が発生したときにデータが破損しないことを保証します。 たとえば DRBD (分散レプリケートされたブロックデバイス) でリソース レベルのフェンスを使用して、通信リンクがダウンしたときにノード上のディスクを期限切れとしてマークすることができます。

ノード レベルのフェンスでは、ノードによってリソースが実行されないことが保証されます。 これはノードをリセットすることによって行われ、Pacemaker の実装は "STONITH" ("Shoot the Other Node in the Head") と呼ばれます。 Pacemaker は、サーバーの無停電電源装置や管理インターフェイス カードなど、さまざまな種類のフェンス デバイスをサポートしています。

詳細については、次を参照してください。

- [ゼロから始める Pacemaker クラスター](https://clusterlabs.org/pacemaker/doc/en-US/Pacemaker/1.1/html/Clusters_from_Scratch/)
- [フェンスと STONITH](https://clusterlabs.org/doc/crm_fencing.html)
- [SUSE HA ドキュメント:フェンスと STONITH](https://www.suse.com/documentation/sle_ha/book_sleha/data/cha_ha_fencing.html)

クラスターの初期化時に構成が検出されない場合、STONITH は無効になります。 後で次のコマンドを実行して有効にすることができます。

```bash
sudo crm configure property stonith-enabled=true
```
  
>[!IMPORTANT]
>STONITH を無効にするのは、テスト目的の場合だけです。 運用環境で Pacemaker を使用する予定がある場合は、環境に応じて STONITH の実装を計画し、有効にしておく必要があります。 SUSE では、どのクラウド環境 (Azure を含む) のフェンス エージェントも提供していません。 そのため、クラスター ベンダーでは、これらの環境で運用クラスターを実行するためのサポートは提供されていません。 Microsoft では、このギャップのための、今後のリリースで利用できるようになるソリューションに取り組んでいます。

## <a name="configure-the-cluster-resources-for-sql-server"></a>SQL Server 用にクラスター リソースを構成する

[SLES 管理ガイド](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#cha.ha.manual_config)を参照してください

## <a name="enable-pacemaker"></a>Pacemaker を有効にする

自動的に開始されるように Pacemaker を有効にします。

クラスターの各ノードで次のコマンドを実行します。

```bash
systemctl enable pacemaker
```

### <a name="create-availability-group-resource"></a>可用性グループのリソースを作成する

次のコマンドは、可用性グループ [ag1] の 3 つのレプリカの可用性グループ リソースを作成し、構成します。 モニター操作とタイムアウトは、タイムアウトがワークロードに大きく依存しており、デプロイごとに慎重に調整する必要があるという事実に基づいて、SLES で明示的に指定する必要があります。
クラスター内のいずれかのノードでコマンドを実行します。

1. `crm configure` を実行して crm プロンプトを開きます。

   ```bash
   sudo crm configure 
   ```

1. crm プロンプトで、次のコマンドを実行してリソース プロパティを構成します。

   ```bash
   primitive ag_cluster \
      ocf:mssql:ag \
      params ag_name="ag1" \
      meta failure-timeout=60s \
      op start timeout=60s \
      op stop timeout=60s \
      op promote timeout=60s \
      op demote timeout=10s \
      op monitor timeout=60s interval=10s \
      op monitor timeout=60s interval=11s role="Master" \
      op monitor timeout=60s interval=12s role="Slave" \
      op notify timeout=60s
   ms ms-ag_cluster ag_cluster \
      meta master-max="1" master-node-max="1" clone-max="3" \
     clone-node-max="1" notify="true" \
   commit
      ```

[!INCLUDE [required-synchronized-secondaries-default](../includes/ss-linux-cluster-required-synchronized-secondaries-default.md)]

### <a name="create-virtual-ip-resource"></a>仮想 IP リソースを作成する

`ha-cluster-init` を実行したときに仮想 IP リソースを作成しなかった場合は、ここでこのリソースを作成できます。 次のコマンドは、仮想 IP リソースを作成します。 `<**0.0.0.0**>` をネットワークの使用可能なアドレスに置き換え、`<**24**>` を CIDR サブネット マスクのビット数に置き換えます。 1 つのノードで実行します。

```bash
crm configure \
primitive admin_addr \
   ocf:heartbeat:IPaddr2 \
   params ip=<**0.0.0.0**> \
      cidr_netmask=<**24**>
```

### <a name="add-colocation-constraint"></a>コロケーション制約を追加する
リソースを実行する場所の選択など、Pacemaker クラスターでのほぼすべての決定は、スコアを比較することによって行われます。 スコアはリソースごとに計算され、クラスター リソース マネージャーでは、特定のリソースのスコアが最も高いノードが選択されます。 (ノードにリソースの負のスコアがある場合、そのノードではリソースを実行できません。)制約を使用してクラスターの決定を操作できます。 制約にはスコアがあります。 制約のスコアが INFINITY より低い場合、これは単なる推奨設定です。 INFINITY のスコアは、それが必要であることを意味します。 可用性グループと仮想 IP リソースのプライマリが同じホスト上で実行されるようにするため、INFINITY のスコアを持つコロケーション制約を定義します。 

マスターと同じノードで実行されるように仮想 IP のコロケーション制約を設定するには、1 つのノードで次のコマンドを実行します。

```bash
crm configure
colocation vip_on_master inf: \
    admin_addr ms-ag_cluster:Master
commit
```

### <a name="add-ordering-constraint"></a>順序制約を追加する
コロケーション制約には、暗黙的な順序制約があります。 これにより、可用性グループ リソースが移動する前に、仮想 IP リソースが移動します。 既定では、イベントの順序は次のとおりです。 

1. ユーザーが、ノード 1 からノード 2 の可用性グループ マスターに resource migrate を発行します。
2. 仮想 IP リソースがノード 1 で停止します。
3. 仮想 IP リソースがノード 2 で開始します。 この時点で、IP アドレスは一時的にノード 2 を指しますが、ノード 2 はフェールオーバー前のセカンダリのままです。 
4. ノード 1 の可用性グループ マスターは、スレーブに降格されます。
5. ノード 2 の可用性グループ スレーブは、マスターに昇格されます。 

IP アドレスが事前フェールオーバー セカンダリのノードを一時的に指さないようにするには、順序制約を追加します。 順序制約を追加するには、1 つのノードで次のコマンドを実行します。 

```bash
crm crm configure \
   order ag_first inf: ms-ag_cluster:promote admin_addr:start
```


>[!IMPORTANT]
>クラスターを構成し、可用性グループをクラスター リソースとして追加した後は、Transact-SQL を使用して可用性グループ リソースをフェールオーバーすることはできません。 Linux 上の SQL Server クラスター リソースは、Windows Server フェールオーバー クラスター (WSFC) ほど、オペレーティング システムと緊密に結合されていません。 SQL Server サービスでは、クラスターの存在は認識されません。 すべてのオーケストレーションは、クラスター管理ツールを使用して実行されます。 SLES では `crm` を使います。 

`crm` を使用して可用性グループの手動フェールオーバーを行います。 Transact-SQL を使用してフェールオーバーを開始しないでください。 詳細については、[フェールオーバー](sql-server-linux-availability-group-failover-ha.md#failover)に関するページを参照してください。


詳細については、次を参照してください。
- [クラスター リソースの管理](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#sec.ha.config.crm)。   
- [HA の概念](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#cha.ha.concepts)
- [Pacemaker クイック リファレンス](https://github.com/ClusterLabs/pacemaker/blob/master/doc/pcs-crmsh-quick-ref.md) 

<!---[!INCLUDE [Pacemaker Concepts](..\includes\ss-linux-cluster-pacemaker-concepts.md)]--->

## <a name="next-steps"></a>次のステップ

[HA 可用性グループの操作](sql-server-linux-availability-group-failover-ha.md)
