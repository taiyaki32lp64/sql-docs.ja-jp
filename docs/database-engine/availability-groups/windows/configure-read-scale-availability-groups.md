---
title: 可用性グループの読み取りスケールを構成する
description: Windows で読み取りスケール ワークロードの Always On 可用性グループを構成します。
ms.custom: seodec18
author: MashaMSFT
ms.author: mathoma
ms.reviewer: ''
ms.date: 05/24/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: high-availability
ms.openlocfilehash: 3ff0064a228cb756614dec2ff54a91f4f03d374c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67991157"
---
# <a name="configure-read-scale-for-an-always-on-availability-group"></a>Always On 可用性グループの読み取りスケールを構成する

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Windows で読み取りスケール ワークロードの SQL Server Always On 可用性グループを構成できます。 可用性グループには、2 種類のアーキテクチャがあります。
* 高可用性のアーキテクチャでは、クラスター マネージャーを利用し、ビジネス継続性を改善します。また、読み取り可能なセカンダリ レプリカを含めることもできます。 この高可用性アーキテクチャを作成するには、「[可用性グループの作成と構成 (SQL Server)](creation-and-configuration-of-availability-groups-sql-server.md)」を参照してください。 
* アーキテクチャでは、読み取りスケール ワークロードのみをサポートします。 

この記事では、読み取りスケール ワークロードの場合で、クラスター マネージャーがない可用性グループを作成する方法について説明します。 このアーキテクチャは、読み取りスケールのみを提供します。 高可用性は提供されません。

>[!NOTE]
>`CLUSTER_TYPE = NONE` による可用性グループには、さまざまなオペレーティング システム プラットフォームでホストされているレプリカを含めることができます。 高可用性はサポートできません。 Linux オペレーティング システムについては、[Linux で読み取りスケールの SQL Server 可用性グループを構成する](../../../linux/sql-server-linux-availability-group-configure-rs.md)方法に関するページを参照してください。

[!INCLUDE [Create prerequisites](../../../includes/ss-availability-group-rs-prereq.md)]

## <a name="create-an-availability-group"></a>可用性グループを作成する

可用性グループを作成します。 `CLUSTER_TYPE = NONE` を設定します。 さらに、`FAILOVER_MODE = NONE` で各レプリカを設定します。 分析やレポートのワークロードを実行するクライアント アプリケーションは、セカンダリ データベースに直接接続できます。 また、読み取り専用ルーティング リストも作成できます。 プライマリ レプリカへの接続によって、ルーティング リストに基づき、ラウンドロビン方式で各セカンダリ レプリカに読み取り接続要求を転送します。

次の Transact-SQL スクリプトでは、`ag1` という名前の可用性グループを作成します。 このスクリプトでは、`SEEDING_MODE = AUTOMATIC` で可用性グループのレプリカが構成されます。 この設定によって、SQL Server で可用性グループにセカンダリ サーバーが追加されるたびに、そのセカンダリ サーバーでデータベースが自動作成されます。 

ご利用の環境に合わせて次のスクリプトを変更してください。 `<node1>` 値と `<node2>` 値を、レプリカをホストする SQL Server インスタンスの名前に置き換えます。 `<5022>` 値を、エンドポイントに設定したポートに置き換えます。 プライマリ SQL Server レプリカで次の Transact-SQL スクリプトを実行します。

```sql
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

### <a name="join-secondary-sql-server-instances-to-the-availability-group"></a>セカンダリ SQL Server インスタンスを可用性グループに参加させる

次の Transact-SQL スクリプトにより、`ag1` という名前の可用性グループにサーバーを参加させます。 ご利用の環境に合わせてスクリプトを変更してください。 可用性グループに参加させるには、各セカンダリ SQL Server レプリカで次の Transact-SQL スクリプトを実行します。

```sql
ALTER AVAILABILITY GROUP [ag1] JOIN WITH (CLUSTER_TYPE = NONE);

ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
```

[!INCLUDE [Create post](../../../includes/ss-availability-group-rs-postactivity.md)]

この可用性グループは高可用性構成ではありません。 高可用性が必要な場合、[Linux で SQL Server の Always On 可用性グループを構成する](../../../linux/sql-server-linux-availability-group-configure-ha.md)方法に関するページか、「[可用性グループの作成と構成 (SQL Server)](creation-and-configuration-of-availability-groups-sql-server.md)」の手順に従ってください。

## <a name="connect-to-read-only-secondary-replicas"></a>読み取り専用セカンダリ レプリカに接続する

読み取り専用セカンダリ レプリカには、次の 2 つの方法で接続できます。
* アプリケーションは、セカンダリ レプリカをホストする SQL Server インスタンスに直接接続し、データベースにクエリを実行できます。 詳細については、「[アクティブなセカンダリ: 読み取り可能なセカンダリ レプリカ (Always On 可用性グループ)](active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)」を参照してください。
* アプリケーションでは、リスナーを要求する読み取り専用ルーティングも利用できます。 詳細については、「[リスナーを使用した読み取り専用セカンダリ レプリカ (読み取り専用ルーティング) への接続](listeners-client-connectivity-application-failover.md#ConnectToSecondary)」を参照してください。

## <a name="fail-over-the-primary-replica-on-a-read-scale-availability-group"></a>読み取りスケール可用性グループのプライマリ レプリカをフェールオーバーする

[!INCLUDE[Force failover](../../../includes/ss-force-failover-read-scale-out.md)]

## <a name="next-steps"></a>次の手順

* [分散型可用性グループの構成](distributed-availability-groups-always-on-availability-groups.md)
* [可用性グループの詳細](overview-of-always-on-availability-groups-sql-server.md)
* [強制手動フェールオーバーの実行](perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)
