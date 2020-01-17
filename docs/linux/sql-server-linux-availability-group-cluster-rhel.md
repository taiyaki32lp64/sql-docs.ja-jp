---
title: RHEL:Linux で SQL Server の可用性グループを構成する
description: SQL Server 用の Red Hat Enterprise Linux (RHEL) の実行時、可用性グループを構成する方法について説明します。
ms.custom: seo-lt-2019
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 03/12/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: b7102919-878b-4c08-a8c3-8500b7b42397
ms.openlocfilehash: 6976d81994dbc8db154b285da03bed2397e9fee1
ms.sourcegitcommit: 035ad9197cb9799852ed705432740ad52e0a256d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/31/2019
ms.locfileid: "75558498"
---
# <a name="configure-rhel-cluster-for-sql-server-availability-group"></a>SQL Server 可用性グループ用の RHEL クラスターを構成する

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

このドキュメントでは、Red Hat Enterprise Linux 上の SQL Server 用に 3 ノードの可用性グループ クラスターを作成する方法について説明します。 高可用性を実現するため、Linux 上の可用性グループには 3 つのノードが必要です。[可用性グループ構成の高可用性とデータ保護](sql-server-linux-availability-group-ha.md)に関するページを参照してください。 クラスタリング レイヤーは、[Pacemaker](https://clusterlabs.org/) の上に構築された Red Hat Enterprise Linux (RHEL) [HA アドオン](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/pdf/High_Availability_Add-On_Overview/Red_Hat_Enterprise_Linux-6-High_Availability_Add-On_Overview-en-US.pdf)に基づいています。 

> [!NOTE] 
> Red Hat の完全なドキュメントにアクセスするには、有効なサブスクリプションが必要です。 

クラスター構成、リソース エージェント オプション、および管理の詳細については、[RHEL リファレンス ドキュメント](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/7/html/High_Availability_Add-On_Reference/index.html)を参照してください。

> [!NOTE] 
> SQL Server は、Windows Server フェールオーバー クラスタリングと同じように、Linux 上の Pacemaker と密接に統合されていません。 SQL Server インスタンスはクラスターを認識しません。 Pacemaker は、クラスター リソース オーケストレーションを提供します。 また、仮想ネットワーク名は Windows Server フェールオーバー クラスタリングに固有のものであり、Pacemaker には対応するものがありません。 クラスター情報のクエリを実行する可用性グループの動的管理ビュー (DMV) では、Pacemaker クラスター上の空の行が返されます。 フェールオーバー後に透過的な再接続用のリスナーを作成するには、仮想 IP リソースの作成に使用される IP を使用して、リスナー名を DNS に手動で登録します。 

以下のセクションでは、Pacemaker クラスターを設定し、高可用性のためにクラスターのリソースとして可用性グループを追加する手順について説明します。

## <a name="roadmap"></a>ロードマップ

高可用性のために Linux サーバー上に可用性グループを作成する手順は、Windows Server フェールオーバー クラスターでの手順とは異なります。 以下に、おおまかな手順を説明します。 

1. [クラスター ノードで SQL Server を構成します](sql-server-linux-setup.md)。

2. [可用性グループを作成します](sql-server-linux-availability-group-configure-ha.md)。 

3. Pacemaker などのクラスター リソース マネージャーを構成します。 これらの手順についてはこのドキュメントで説明します。
   
   クラスター リソース マネージャーを構成する方法は、特定の Linux ディストリビューションによって異なります。 

   >[!IMPORTANT]
   >運用環境では、高可用性のために STONITH のようなフェンス エージェントが必要です。 このドキュメントに含まれているデモでは、フェンス エージェントは使用しません。 このデモはテストと検証専用です。
   
   >Linux クラスターでは、フェンスを使用して、クラスターが既知の状態に戻されます。 フェンスを構成する方法は、ディストリビューションと環境によって異なります。 現時点では、一部のクラウド環境ではフェンスを利用できません。 詳細については、[RHEL 高可用性クラスターのサポート ポリシー (仮想化プラットフォーム)](https://access.redhat.com/articles/29440) に関するページをご覧ください。

5. [可用性グループをクラスターのリソースとして追加します](sql-server-linux-availability-group-cluster-rhel.md#create-availability-group-resource)。  

## <a name="configure-high-availability-for-rhel"></a>RHEL の高可用性を構成する

RHEL の高可用性を構成するには、高可用性サブスクリプションを有効にしてから、Pacemaker を構成します。

### <a name="enable-the-high-availability-subscription-for-rhel"></a>RHEL の高可用性サブスクリプションを有効にする

クラスター内の各ノードには、RHEL の適切なサブスクリプションと高可用性アドオンが必要です。 [Red Hat Enterprise Linux に高可用性クラスター パッケージをインストールする方法](https://access.redhat.com/solutions/45930)に関するページで要件を確認してください。 サブスクリプションとリポジトリを構成するには、次の手順を実行します。

1. システムを登録します。

   ```bash
   sudo subscription-manager register
   ```

   ユーザー名とパスワードを入力します。   

1. 登録に使用できるプールを一覧表示します。

   ```bash
   sudo subscription-manager list --available
   ```

   使用可能なプールの一覧から、高可用性サブスクリプションのプール ID を書き留めます。

1. 次のスクリプトを更新します。 `<pool id>` を、前の手順の高可用性のプール ID に置き換えます。 スクリプトを実行してサブスクリプションをアタッチします。

   ```bash
   sudo subscription-manager attach --pool=<pool id>
   ```

1. リポジトリを有効にします。

   ```bash
   sudo subscription-manager repos --enable=rhel-ha-for-rhel-7-server-rpms
   ```

詳細については、「[Pacemaker - The Open Source, High Availability Cluster](https://clusterlabs.org/pacemaker/)」を参照してください。 

サブスクリプションを構成したら、次の手順を実行して Pacemaker を構成します。

### <a name="configure-pacemaker"></a>Pacemaker を構成する

サブスクリプションを登録したら、次の手順を実行して Pacemaker を構成します。
   
[!INCLUDE [RHEL-Configure-Pacemaker](../includes/ss-linux-cluster-pacemaker-configure-rhel.md)]

Pacemaker を構成した後、`pcs` を使用してクラスターを操作します。 クラスターから 1 つのノードですべてのコマンドを実行します。 

## <a name="configure-fencing-stonith"></a>フェンスを構成する (STONITH)

Pacemaker クラスターのベンダーは、STONITH を有効にして、サポートされているクラスター セットアップ用にフェンス デバイスを構成する必要があります。 STONITH は "Shoot the Other Node in The Head" の略です。 クラスター リソース マネージャーがノードまたはノード上のリソースの状態を判断できない場合は、フェンスによりクラスターが既知の状態に戻ります。

STONITH デバイスでは、フェンス エージェントが提供されます。 「[Azure の Red Hat Enterprise Linux に Pacemaker をセットアップする](/azure/virtual-machines/workloads/sap/high-availability-guide-rhel-pacemaker/#1-create-the-stonith-devices)」では、Azure でこのクラスター用の STONITH デバイスを作成する方法の例が示されています。 環境の手順を変更します。

リソース レベルのフェンスは、リソースを構成することによって障害が発生した場合にデータが破損しないことを保証します。 たとえば、リソース レベルのフェンスを使用して、通信リンクがダウンしたときにノード上のディスクを期限切れとしてマークすることができます。 

ノード レベルのフェンスでは、ノードによってリソースが実行されないことが保証されます。 これを行うには、ノードをリセットします。 Pacemaker は、さまざまなフェンス デバイスをサポートしています。 例として、無停電電源装置やサーバーの管理インターフェイスカードなどがあります。

STONITH、およびフェンスの詳細については、次の記事を参照してください。

* [ゼロから始める Pacemaker クラスター](https://clusterlabs.org/pacemaker/doc/en-US/Pacemaker/1.1/html/Clusters_from_Scratch/index.html)
* [フェンスと STONITH](https://clusterlabs.org/doc/crm_fencing.html)
* [Pacemaker を使用した Red Hat High Availability Add-On:フェンス](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/6/html/Configuring_the_Red_Hat_High_Availability_Add-On_with_Pacemaker/ch-fencing-HAAR.html)

>[!NOTE]
>ノード レベルのフェンス構成は環境に大きく依存しているため、このチュートリアルでは無効にします (後で構成できます)。 次のスクリプトは、ノード レベルのフェンスを無効にします。
>
>```bash
>sudo pcs property set stonith-enabled=false
>``` 
>
>STONITH を無効にするのは、テスト目的の場合だけです。 運用環境で Pacemaker を使用する予定がある場合は、環境に応じて STONITH の実装を計画し、有効にしておく必要があります。

## <a name="set-cluster-property-cluster-recheck-interval"></a>クラスター プロパティ cluster-recheck-interval を設定する

`cluster-recheck-interval` は、クラスターによってリソース パラメーター、制約、またはその他のクラスター オプションの変更が確認されるポーリング間隔を示します。 レプリカがダウンした場合、クラスターでは、`failure-timeout` 値と `cluster-recheck-interval` 値によってバインドされた間隔でレプリカの再起動が試みられます。 たとえば、`failure-timeout` が 60 秒に設定されていて、`cluster-recheck-interval` が 120 秒に設定されている場合、再起動は 60 秒より大きく 120 秒未満の間隔で試行されます。 failure-timeout は 60 秒、cluster-recheck-interval は 60 秒より大きい値に設定することをお勧めします。 cluster-recheck-interval を小さい値に設定することは推奨されません。

プロパティ値を `2 minutes` に更新するには、次を実行します。

```bash
sudo pcs property set cluster-recheck-interval=2min
```

> [!IMPORTANT] 
> 使用可能な最新の Pacemaker パッケージ 1.1.18-11.el7 を使用しているすべてのディストリビューション (RHEL 7.3 および 7.4 を含む) では、値が false の場合は start-failure-is-fatal クラスター設定の動作が変更されることに注意してください。 この変更は、フェールオーバー ワークフローに影響します。 プライマリ レプリカで障害が発生した場合、クラスターは使用可能なセカンダリ レプリカのいずれかにフェールオーバーする必要があります。 代わりに、クラスターが失敗したプライマリ レプリカを起動しようとしていることがユーザーに通知されます。 そのプライマリが永久に停止したためにオンラインにならない場合は、クラスターが別の使用可能なセカンダリ レプリカにフェールオーバーすることはありません。 この変更により、以前に start-failure-is-fatal を設定するために推奨されていた構成が有効ではなくなったため、この設定を既定値の `true` に戻す必要があります。 さらに、`failover-timeout` プロパティを含めるには、AG リソースを更新する必要があります。 

プロパティ値を `true` に更新するには、次を実行します。

```bash
sudo pcs property set start-failure-is-fatal=true
```

`ag_cluster` リソース プロパティ `failure-timeout` を `60s` に更新するには、次を実行します。

```bash
pcs resource update ag_cluster meta failure-timeout=60s
```


Pacemaker クラスターのプロパティの詳細については、「[Pacemaker クラスターのプロパティ](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/High_Availability_Add-On_Reference/ch-clusteropts-HAAR.html)」を参照してください。

## <a name="create-a-sql-server-login-for-pacemaker"></a>Pacemaker 用の SQL Server ログインを作成する

[!INCLUDE [SQL-Create-SQL-Login](../includes/ss-linux-cluster-pacemaker-create-login.md)]

## <a name="create-availability-group-resource"></a>可用性グループのリソースを作成する

可用性グループ リソースを作成するには、`pcs resource create` コマンドを使用し、リソースのプロパティを設定します。 次のコマンドは、`ag1` という名前の可用性グループの `ocf:mssql:ag` マスター/スレーブ タイプのリソースを作成します。

```bash
sudo pcs resource create ag_cluster ocf:mssql:ag ag_name=ag1 meta failure-timeout=60s master notify=true
``` 

[!INCLUDE [required-synchronized-secondaries-default](../includes/ss-linux-cluster-required-synchronized-secondaries-default.md)]

<a name="createIP"></a>

## <a name="create-virtual-ip-resource"></a>仮想 IP リソースを作成する

仮想 IP アドレス リソースを作成するには、1 つのノードで次のコマンドを実行します。 ネットワークから使用可能な静的 IP アドレスを使用します。 `<10.128.16.240>` 間の IP アドレスは有効な IP アドレスに置き換えてください。

```bash
sudo pcs resource create virtualip ocf:heartbeat:IPaddr2 ip=<10.128.16.240>
```

Pacemaker では、仮想サーバー名に相当するものはありません。 IP アドレスではなく文字列サーバー名を指す接続文字列を使用するには、DNS の仮想 IP リソース アドレスと必要な仮想サーバー名を登録します。 DR 構成の場合は、必要な仮想サーバー名と IP アドレスを、プライマリ サイトと DR サイトの両方の DNS サーバーに登録します。

## <a name="add-colocation-constraint"></a>コロケーション制約を追加する

リソースを実行する場所の選択など、Pacemaker クラスターでのほぼすべての決定は、スコアを比較することによって行われます。 スコアはリソースごとに計算されます。 クラスター リソース マネージャーは、特定のリソースのスコアが最も高いノードを選択します。 ノードにリソースの負のスコアがある場合、そのノードではリソースを実行できません。

Pacemaker クラスターでは、制約を使用してクラスターの決定を操作できます。 制約にはスコアがあります。 制約のスコアが `INFINITY` より低い場合、Pacemaker は推奨設定とみなします。 `INFINITY` のスコアは必須です。

プライマリ レプリカと仮想 IP リソースが同じホスト上で実行されるようにするには、INFINITY のスコアを持つコロケーション制約を定義します。 コロケーション制約を追加するには、1 つのノードで次のコマンドを実行します。

```bash
sudo pcs constraint colocation add virtualip ag_cluster-master INFINITY with-rsc-role=Master
```

## <a name="add-ordering-constraint"></a>順序制約を追加する

コロケーション制約には、暗黙的な順序制約があります。 これにより、可用性グループ リソースが移動する前に、仮想 IP リソースが移動します。 既定では、イベントの順序は次のとおりです。

1. ユーザーは、ノード 1 からノード 2 の可用性グループのプライマリに `pcs resource move` を発行します。
1. 仮想 IP リソースがノード 1 で停止します。
1. 仮想 IP リソースがノード 2 で開始します。
  
   >[!NOTE]
   >この時点で、IP アドレスは一時的にノード 2 を指しますが、ノード 2 はフェールオーバー前のセカンダリのままです。 
   
1. ノード 1 の可用性グループのプライマリは、セカンダリに降格されます。
1. ノード 2 の可用性グループのセカンダリは、プライマリに昇格されます。 

IP アドレスが事前フェールオーバー セカンダリのノードを一時的に指さないようにするには、順序制約を追加します。 

順序制約を追加するには、1 つのノードで次のコマンドを実行します。

```bash
sudo pcs constraint order promote ag_cluster-master then start virtualip
```

>[!IMPORTANT]
>クラスターを構成し、可用性グループをクラスター リソースとして追加した後は、Transact-SQL を使用して可用性グループ リソースをフェールオーバーすることはできません。 Linux 上の SQL Server クラスター リソースは、Windows Server フェールオーバー クラスター (WSFC) ほど、オペレーティング システムと緊密に結合されていません。 SQL Server サービスでは、クラスターの存在は認識されません。 すべてのオーケストレーションは、クラスター管理ツールを使用して実行されます。 RHEL または Ubuntu では `pcs` を使用し、SLES では `crm` ツールを使用します。 

`pcs` を使用して可用性グループの手動フェールオーバーを行います。 Transact-SQL を使用してフェールオーバーを開始しないでください。 手順については、[フェールオーバー](sql-server-linux-availability-group-failover-ha.md#failover)に関するページを参照してください。

## <a name="next-steps"></a>次のステップ

[HA 可用性グループの操作](sql-server-linux-availability-group-failover-ha.md)
