---
title: 可用性グループ用の Ubuntu クラスターを構成する
titleSuffix: SQL Server on Linux
description: Ubuntu で 3 ノードのクラスターを作成し、以前に作成した可用性グループ リソースをクラスターに追加する方法について説明します。
ms.custom: seo-lt-2019
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 04/30/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: dd0d6fb9-df0a-41b9-9f22-9b558b2b2233
ms.openlocfilehash: 8dd55f8cb9546c7ec91632d40d2eb6b46ffd4d90
ms.sourcegitcommit: 035ad9197cb9799852ed705432740ad52e0a256d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/31/2019
ms.locfileid: "75558488"
---
# <a name="configure-ubuntu-cluster-and-availability-group-resource"></a>Ubuntu クラスターと可用性グループ リソースを構成する

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

このドキュメントでは、Ubuntu で 3 ノードのクラスターを作成し、以前に作成した可用性グループをクラスター内のリソースとして追加する方法について説明します。 高可用性を実現するため、Linux 上の可用性グループには 3 つのノードが必要です。[可用性グループ構成の高可用性とデータ保護](sql-server-linux-availability-group-ha.md)に関するページを参照してください。

> [!NOTE] 
> 現時点では、Linux 上の SQL Server と Pacemaker の統合では、Windows 上の WSFC のような連携は行われていません。 SQL の内部にはクラスターの存在に関する情報はなく、すべての調整は外部で実行され、サービスはスタンドアロン インスタンスとして Pacemaker によって制御されます。 さらに、仮想ネットワーク名は WSFC に固有のものであり、Pacemaker にはそれに該当するものはありません。 クラスターの情報を照会する Always On の動的管理ビューでは、空の行が返されます。 フェールオーバー後に透過的な再接続に使用するリスナーを引き続き作成できますが、仮想 IP リソースの作成に使用する IP で、DNS サーバーにリスナー名を手動で登録する必要があります (以下のセクションで説明します)。

次のセクションでは、フェールオーバー クラスター ソリューションを設定する手順について説明します。 

## <a name="roadmap"></a>ロードマップ

高可用性のために Linux サーバー上に可用性グループを作成する手順は、Windows Server フェールオーバー クラスターでの手順とは異なります。 以下に、おおまかな手順を説明します。 

1. [クラスター ノードで SQL Server を構成します](sql-server-linux-setup.md)。

2. [可用性グループを作成します](sql-server-linux-availability-group-configure-ha.md)。 

3. Pacemaker などのクラスター リソース マネージャーを構成します。 これらの手順についてはこのドキュメントで説明します。
   
   クラスター リソース マネージャーを構成する方法は、特定の Linux ディストリビューションによって異なります。 

   >[!IMPORTANT]
   >運用環境では、高可用性のために STONITH のようなフェンス エージェントが必要です。 このドキュメントに含まれているデモでは、フェンス エージェントは使用しません。 このデモはテストと検証専用です。 
   >
   >Linux クラスターでは、フェンスを使用して、クラスターが既知の状態に戻されます。 フェンスを構成する方法は、ディストリビューションと環境によって異なります。 現時点では、一部のクラウド環境ではフェンスを利用できません。 詳細については、「[RHEL 高可用性クラスターのサポート ポリシー - 仮想化プラットフォーム](https://access.redhat.com/articles/29440)」をご覧ください。
   >
   >フェンスは通常、オペレーティング システムで実装され、環境に依存します。 フェンスの取扱説明はオペレーティング システムのディストリビューターが提供するドキュメントにあります。

5.  [可用性グループをクラスターのリソースとして追加します](sql-server-linux-availability-group-cluster-ubuntu.md#create-availability-group-resource)。 

## <a name="install-and-configure-pacemaker-on-each-cluster-node"></a>各クラスター ノードに Pacemaker をインストールして構成する

1. すべてのノードで、ファイアウォールのポートを開きます。 Pacemaker 高可用性サービス、SQL Server インスタンス、および可用性グループ エンドポイント用にポートを開きます。 SQL Server が実行されているサーバーの既定の TCP ポートは 1433 です。  

   ```bash
   sudo ufw allow 2224/tcp
   sudo ufw allow 3121/tcp
   sudo ufw allow 21064/tcp
   sudo ufw allow 5405/udp
        
   sudo ufw allow 1433/tcp # Replace with TDS endpoint
   sudo ufw allow 5022/tcp # Replace with DATA_MIRRORING endpoint
        
   sudo ufw reload
   ```
   
   または、単にファイアウォールを無効にしてもかまいません。
        
   ```bash
   sudo ufw disable
   ```

1. Pacemaker パッケージをインストールします。 すべてのノードで、次のコマンドを実行します。

   ```bash
   sudo apt-get install pacemaker pcs fence-agents resource-agents
   ```

2. Pacemaker と Corosync のパッケージをインストールしたときに作成された既定のユーザー用のパスワードを設定します。 すべてのノードで同じパスワードを使います。 

   ```bash
   sudo passwd hacluster
   ```

## <a name="enable-and-start-pcsd-service-and-pacemaker"></a>pcsd サービスと Pacemaker を有効にして開始する

次のコマンドを実行すると、pcsd サービスと Pacemaker が有効になり、開始されます。 すべてのノードで実行します。 これにより、再起動後にノードはクラスターに再度参加できます。 

```bash
sudo systemctl enable pcsd
sudo systemctl start pcsd
sudo systemctl enable pacemaker
```
>[!NOTE]
>Pacemaker のコマンド enable は、エラー "pacemaker Default-Start contains no runlevels, aborting" (Pacemaker Default-Start に実行レベルが含まれていません、中止します) で完了する場合があります。 これは害がないため、クラスターの構成を続行できます。 

## <a name="create-the-cluster"></a>クラスターを作成する

1. すべてのノードから既存のクラスター構成を削除します。 

   "sudo apt-get install pcs" を実行すると、Pacemaker、corosync、pcs が同時にインストールされ、3 つのサービスすべての実行が開始されます。  corosync を開始すると、テンプレート "/etc/cluster/corosync.conf" ファイルが生成されます。  次の手順を成功させるには、このファイルが存在していてはなりません。そのため、回避策として、pacemaker/corosync を停止して "/etc/cluster/corosync.conf" を削除します。そうすれば、次の手順は正常に完了します。 "pcs cluster destroy" では同じことが行われ、1 回の初期クラスター セットアップ ステップとして使用できます。
   
   次のコマンドでは、既存のクラスター構成ファイルが削除されて、すべてのクラスター サービスが停止されます。 これにより、クラスターが完全に破棄されます。 運用前環境での最初のステップとしてそれを実行します。 "pcs cluster destroy" によって pacemaker サービスが無効にされているので、再度有効にする必要があることに注意してください。 すべてのノードで次のコマンドを実行します。
   
   >[!WARNING]
   >そのコマンドでは、既存のすべてのクラスター リソースが破棄されます。

   ```bash
   sudo pcs cluster destroy 
   sudo systemctl enable pacemaker
   ```

1. クラスターを作成します。 

   >[!WARNING]
   >クラスタリング ベンダーが調査している既知の問題のため、クラスターの開始 ("pcs cluster start") は、次のエラーで失敗します。 これは、クラスターのセットアップ コマンドの実行時に作成される /etc/corosync/corosync.conf で構成されるログ ファイルが間違っているためです。 この問題を回避するには、ログ ファイルを次のように変更します: /var/log/corosync/corosync.log。 または、/var/log/cluster/corosync.log ファイルを作成するのでもかまいません。
 
   ```Error
   Job for corosync.service failed because the control process exited with error code. 
   See "systemctl status corosync.service" and "journalctl -xe" for details.
   ```
  
次のコマンドでは、3 ノードのクラスターが作成されます。 スクリプトを実行する前に、`< ... >` の間の値を置き換えます。 プライマリ ノードで次のコマンドを実行します。 

   ```bash
   sudo pcs cluster auth <node1> <node2> <node3> -u hacluster -p <password for hacluster>
   sudo pcs cluster setup --name <clusterName> <node1> <node2...> <node3>
   sudo pcs cluster start --all
   sudo pcs cluster enable --all
   ```
   
   >[!NOTE]
   >前に同じノードでクラスターを構成した場合は、"pcs cluster setup" を実行するときに "--force" オプションを使用する必要があります。 これは、"pcs cluster destroy" を実行するのと同じあり、"sudo systemctl enable pacemaker" を使用して、Pacemaker のサービスを再度有効にする必要がある点に注意してください。


## <a name="configure-fencing-stonith"></a>フェンスを構成する (STONITH)

Pacemaker クラスターのベンダーは、STONITH を有効にして、サポートされているクラスター セットアップ用にフェンス デバイスを構成する必要があります。 クラスター リソース マネージャーでノードまたはノード上のリソースの状態を判断できない場合は、フェンスを使用してクラスターが既知の状態に戻されます。 リソース レベルのフェンスにより主に、リソースを構成することによって障害が発生した場合にデータが破損しないことが保証されます。 たとえば DRBD (分散レプリケートされたブロックデバイス) でリソース レベルのフェンスを使用して、通信リンクがダウンしたときにノード上のディスクを期限切れとしてマークすることができます。 ノード レベルのフェンスでは、ノードによってリソースが実行されないことが保証されます。 これはノードをリセットすることによって行われ、Pacemaker の実装は "STONITH" ("Shoot the Other Node in the Head") と呼ばれます。 Pacemaker では、サーバーの無停電電源装置や管理インターフェイス カードなど、さまざまな種類のフェンス デバイスがサポートされています。 詳細については、「[ゼロから始める Pacemaker クラスター](https://clusterlabs.org/pacemaker/doc/en-US/Pacemaker/1.1/html/Clusters_from_Scratch/)」および「[フェンスと STONITH](https://clusterlabs.org/doc/crm_fencing.html)」をご覧ください 

ノード レベルのフェンス構成は環境に大きく依存しているため、このチュートリアルでは無効にします (後で構成できます)。 プライマリ ノードで次のスクリプトを実行します。 

```bash
sudo pcs property set stonith-enabled=false
```

>[!IMPORTANT]
>STONITH を無効にするのは、テスト目的の場合だけです。 運用環境で Pacemaker を使用する予定がある場合は、環境に応じて STONITH の実装を計画し、有効にしておく必要があります。 特定のディストリビューションのフェンス エージェントに関する詳細は、オペレーティング システム ベンダーにお問い合わせください。 

## <a name="set-cluster-property-cluster-recheck-interval"></a>クラスター プロパティ cluster-recheck-interval を設定する

`cluster-recheck-interval` は、クラスターによってリソース パラメーター、制約、またはその他のクラスター オプションの変更が確認されるポーリング間隔を示します。 レプリカがダウンした場合、クラスターでは、`failure-timeout` 値と `cluster-recheck-interval` 値によってバインドされた間隔でレプリカの再起動が試みられます。 たとえば、`failure-timeout` が 60 秒に設定されていて、`cluster-recheck-interval` が 120 秒に設定されている場合、再起動は 60 秒より大きく 120 秒未満の間隔で試行されます。 failure-timeout は 60 秒、cluster-recheck-interval は 60 秒より大きい値に設定することをお勧めします。 cluster-recheck-interval を小さい値に設定することは推奨されません。

プロパティ値を `2 minutes` に更新するには、次を実行します。

```bash
sudo pcs property set cluster-recheck-interval=2min
```

> [!IMPORTANT] 
> 既に Pacemaker クラスターによって管理されている可用性グループ リソースがある場合、使用可能な最新の Pacemaker パッケージ 1.1.18-11.el7 を使用しているすべてのディストリビューションでは、値が false の場合に start-failure-is-fatal クラスター設定の動作が変更されることに注意してください。 この変更は、フェールオーバー ワークフローに影響します。 プライマリ レプリカで障害が発生した場合、クラスターは使用可能なセカンダリ レプリカのいずれかにフェールオーバーする必要があります。 代わりに、クラスターが失敗したプライマリ レプリカを起動しようとしていることがユーザーに通知されます。 そのプライマリが永久に停止したためにオンラインにならない場合は、クラスターが別の使用可能なセカンダリ レプリカにフェールオーバーすることはありません。 この変更により、以前に start-failure-is-fatal を設定するために推奨されていた構成が有効ではなくなったため、この設定を既定値の `true` に戻す必要があります。 さらに、`failover-timeout` プロパティを含めるには、AG リソースを更新する必要があります。 
>
>プロパティ値を `true` に更新するには、次を実行します。
>
>```bash
>sudo pcs property set start-failure-is-fatal=true
>```
>
>既存の AG リソース プロパティ `failure-timeout` を `60s` に更新して、次を実行します (`ag1` は可用性グループ リソースの名前に置き換えてください)。
>
>```bash
>pcs resource update ag1 meta failure-timeout=60s
>```

## <a name="install-sql-server-resource-agent-for-integration-with-pacemaker"></a>Pacemaker との統合のために SQL Server リソース エージェントをインストールする

すべてのノードで次のコマンドを実行します。 

```bash
sudo apt-get install mssql-server-ha
```

## <a name="create-a-sql-server-login-for-pacemaker"></a>Pacemaker 用の SQL Server ログインを作成する

[!INCLUDE [SLES-Create-SQL-Login](../includes/ss-linux-cluster-pacemaker-create-login.md)]

## <a name="create-availability-group-resource"></a>可用性グループのリソースを作成する

可用性グループ リソースを作成するには、`pcs resource create` コマンドを使用し、リソースのプロパティを設定します。 次のコマンドでは、`ag1` という名前の可用性グループに対して、`ocf:mssql:ag` というマスター/スレーブ タイプのリソースが作成されます。 

```bash
sudo pcs resource create ag_cluster ocf:mssql:ag ag_name=ag1 meta failure-timeout=30s --master meta notify=true

```

[!INCLUDE [required-synchronized-secondaries-default](../includes/ss-linux-cluster-required-synchronized-secondaries-default.md)]

## <a name="create-virtual-ip-resource"></a>仮想 IP リソースを作成する

仮想 IP アドレス リソースを作成するには、1 つのノードで次のコマンドを実行します。 ネットワークから使用可能な静的 IP アドレスを使用します。 スクリプトを実行する前に、`< ... >` の間の値を有効な IP アドレスに置き換えます。

```bash
sudo pcs resource create virtualip ocf:heartbeat:IPaddr2 ip=<10.128.16.240>
```

Pacemaker では、仮想サーバー名に相当するものはありません。 IP アドレスを使用せず、文字列のサーバー名を指す接続文字列を使用するには、IP リソース アドレスと必要な仮想サーバー名を DNS に登録します。 DR 構成の場合は、必要な仮想サーバー名と IP アドレスを、プライマリ サイトと DR サイトの両方の DNS サーバーに登録します。

## <a name="add-colocation-constraint"></a>コロケーション制約を追加する

リソースを実行する場所の選択など、Pacemaker クラスターでのほぼすべての決定は、スコアを比較することによって行われます。 スコアはリソースごとに計算され、クラスター リソース マネージャーでは、特定のリソースのスコアが最も高いノードが選択されます。 (ノードにリソースの負のスコアがある場合、そのノードではリソースを実行できません。)制約を使用して、クラスターの決定を構成します。 制約にはスコアがあります。 制約のスコアが INFINITY より低い場合、これは単なる推奨設定です。 INFINITY のスコアは、それが必須であることを意味します。 プライマリ レプリカと仮想 IP リソースを同じホスト上に配置するには、INFINITY のスコアを持つコロケーション制約を定義します。 コロケーション制約を追加するには、1 つのノードで次のコマンドを実行します。 

```bash
sudo pcs constraint colocation add virtualip ag_cluster-master INFINITY with-rsc-role=Master
```

## <a name="add-ordering-constraint"></a>順序制約を追加する

コロケーション制約には、暗黙的な順序制約があります。 これにより、可用性グループ リソースが移動する前に、仮想 IP リソースが移動します。 既定では、イベントの順序は次のとおりです。

1. ユーザーは、ノード 1 からノード 2 の可用性グループのプライマリに `pcs resource move` を発行します。
1. 仮想 IP リソースが node1 で停止します。
1. 仮想 IP リソースが node2 で開始します。

   >[!NOTE]
   >この時点で、IP アドレスは一時的に node2 を指しますが、node2 はフェールオーバー前のセカンダリのままです。 
   
1. node1 の可用性グループのプライマリは、セカンダリに降格されます。
1. node2 の可用性グループのセカンダリは、プライマリに昇格されます。 

IP アドレスが事前フェールオーバー セカンダリのノードを一時的に指さないようにするには、順序制約を追加します。 

順序制約を追加するには、1 つのノードで次のコマンドを実行します。

```bash
sudo pcs constraint order promote ag_cluster-master then start virtualip
```

>[!IMPORTANT]
>クラスターを構成し、可用性グループをクラスター リソースとして追加した後は、Transact-SQL を使用して可用性グループ リソースをフェールオーバーすることはできません。 Linux 上の SQL Server クラスター リソースは、Windows Server フェールオーバー クラスター (WSFC) ほど、オペレーティング システムと緊密に結合されていません。 SQL Server サービスでは、クラスターの存在は認識されません。 すべてのオーケストレーションは、クラスター管理ツールを使用して実行されます。 RHEL または Ubuntu では、`pcs` を使います。 

<!---[!INCLUDE [Pacemaker Concepts](..\includes\ss-linux-cluster-pacemaker-concepts.md)]--->

## <a name="next-steps"></a>次のステップ

[HA 可用性グループの操作](sql-server-linux-availability-group-failover-ha.md)

