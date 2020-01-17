---
title: 読み取りスケール可用性グループを構成する (SQL Server on Linux)
description: Linux で読み取りスケールのワークロード用に SQL Server Always On 可用性グループ (AG) を構成する方法について説明します。
ms.custom: seo-lt-2019
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 01/09/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 1ce63521989edfccc1fc9fc085b0a9c476cde2ee
ms.sourcegitcommit: 035ad9197cb9799852ed705432740ad52e0a256d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/31/2019
ms.locfileid: "75558408"
---
# <a name="configure-a-sql-server-availability-group-for-read-scale-on-linux"></a>Linux で読み取りスケールの SQL Server 可用性グループを構成する

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Linux で読み取りスケールのワークロード用に SQL Server Always On 可用性グループ (AG) を構成できます。 AG には 2 種類のアーキテクチャがあります。 高可用性向けのアーキテクチャでは、クラスター マネージャーを使用して、向上した事業継続性が提供されます。 また、このアーキテクチャには、読み取りスケールのレプリカを含めることもできます。 高可用性アーキテクチャを作成するには、「[Linux で高可用性を実現するために SQL Server の Always On 可用性グループを構成する](sql-server-linux-availability-group-configure-ha.md)」をご覧ください。 その他のアーキテクチャでは、読み取りスケール ワークロードのみをサポートします。 この記事では、読み取りスケール ワークロードの場合で、クラスター マネージャーがない AG を作成する方法について説明します。 このアーキテクチャは、読み取りスケールのみを提供します。 高可用性は提供されません。

> [!NOTE]
> `CLUSTER_TYPE = NONE` による可用性グループには、さまざまなオペレーティング システム プラットフォームでホストされているレプリカを含めることができます。 高可用性はサポートできません。 

[!INCLUDE [Create prerequisites](../includes/ss-linux-cluster-availability-group-create-prereq.md)]

## <a name="create-the-ag"></a>AG を作成する

AG を作成します。 `CLUSTER_TYPE = NONE` を設定します。 さらに、`FAILOVER_MODE = MANUAL` で各レプリカを設定します。 分析やレポートのワークロードを実行するクライアント アプリケーションは、セカンダリ データベースに直接接続できます。 また、読み取り専用ルーティング リストを作成できます。 プライマリ レプリカへの接続によって、ルーティング リストに基づき、ラウンドロビン方式で各セカンダリ レプリカに読み取り接続要求を転送します。

次の Transact-SQL スクリプトによって `ag1` という名前の AG が作成されます。 このスクリプトでは、`SEEDING_MODE = AUTOMATIC` で AG レプリカが構成されます。 この設定によって、SQL Server は AG にセカンダリ サーバーが追加されるたびに、そのセカンダリ サーバーでデータベースを自動作成します。 ご利用の環境に合わせて次のスクリプトを変更してください。 `<node1>` 値と `<node2>` 値を、レプリカをホストする SQL Server インスタンスの名前に置き換えます。 `<5022>` 値を、エンドポイントに設定したポートに置き換えます。 プライマリ SQL Server レプリカで次の Transact-SQL スクリプトを実行します。

```SQL
CREATE AVAILABILITY GROUP [ag1]
    WITH (CLUSTER_TYPE = NONE)
    FOR REPLICA ON
        N'<node1>' WITH (
            ENDPOINT_URL = N'tcp://<node1>:<5022>',
            AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,
            FAILOVER_MODE = MANUAL,
            SEEDING_MODE = AUTOMATIC,
                    SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL)
            ),
        N'<node2>' WITH ( 
            ENDPOINT_URL = N'tcp://<node2>:<5022>', 
            AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,
            FAILOVER_MODE = MANUAL,
            SEEDING_MODE = AUTOMATIC,
            SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL)
            );
        
ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
```

### <a name="join-secondary-sql-servers-to-the-ag"></a>セカンダリ SQL Server を AG に参加させる

次の Transact-SQL スクリプトにより、`ag1` という名前の AG にサーバーが参加します。 ご利用の環境に合わせてスクリプトを変更してください。 各セカンダリ SQL Server レプリカで次の Transact-SQL スクリプトを実行し、AG に参加させます。

```SQL
ALTER AVAILABILITY GROUP [ag1] JOIN WITH (CLUSTER_TYPE = NONE);
         
ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
```

[!INCLUDE [Create post](../includes/ss-linux-cluster-availability-group-create-post.md)]

この AG は高可用性構成ではありません。 高可用性が必要な場合は、[Linux で SQL Server の Always On 可用性グループを構成する](sql-server-linux-availability-group-configure-ha.md)方法に関するページの手順に従ってください。 具体的には、`CLUSTER_TYPE=WSFC` (Windows) または `CLUSTER_TYPE=EXTERNAL` (Linux) で AG を作成します。 その後、Windows Server フェールオーバー クラスタリング (Windows) または Pacemaker (Linux) を使って、クラスター マネージャーと統合します。

## <a name="connect-to-read-only-secondary-replicas"></a>読み取り専用セカンダリ レプリカに接続する

読み取り専用セカンダリ レプリカには 2 つの方法で接続できます。 アプリケーションは、セカンダリ レプリカをホストする SQL Server インスタンスに直接接続し、データベースにクエリを実行できます。 リスナーを要求する読み取り専用ルーティングも利用できます。

* [読み取り可能なセカンダリ レプリカ](../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)
* [読み取り専用ルーティング](../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md#ConnectToSecondary)

## <a name="fail-over-the-primary-replica-on-a-read-scale-availability-group"></a>読み取りスケール可用性グループのプライマリ レプリカをフェールオーバーする

[!INCLUDE[Force failover](../includes/ss-force-failover-read-scale-out.md)]

## <a name="next-steps"></a>次のステップ

* [分散型可用性グループを構成する](../database-engine/availability-groups/windows/distributed-availability-groups-always-on-availability-groups.md)
* [可用性グループの詳細](../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)
* [強制手動フェールオーバーの実行](../database-engine/availability-groups/windows/perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)
