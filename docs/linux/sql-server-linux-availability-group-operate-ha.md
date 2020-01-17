---
title: 可用性グループ SQL Server on Linux を操作する
description: ''
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 03/01/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: ''
ms.openlocfilehash: 24a9d3d9ee0fd65b08e30f40a0597eadf47c6b76
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/25/2019
ms.locfileid: "67916041"
---
# <a name="operate-always-on-availability-groups-on-linux"></a>Linux で Always On 可用性グループを操作する

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

## <a name="upgrade-availability-group"></a>可用性グループのアップグレード

可用性グループをアップグレードする前に、[可用性グループ レプリカ インスタンスのアップグレード](../database-engine/availability-groups/windows/upgrading-always-on-availability-group-replica-instances.md)に関するページにあるパターンとプラクティスを見直してください。

以降のセクションでは、可用性グループを使用し、Linux 上の SQL Server インスタンスでローリング アップグレードを実行する方法について説明します。 

### <a name="upgrade-steps-on-linux"></a>Linux でのアップグレード手順

可用性グループのレプリカが SQL Server in Linux のインスタンスにある場合、可用性グループのクラスター タイプは `EXTERNAL` または `NONE` です。 Windows Server Failover Cluster (WSFC) 以外のクラスター マネージャーで管理される可用性グループは `EXTERNAL` です。 Pacemaker with Corosync は外部クラスター マネージャーの一例です。 クラスター マネージャーのない可用性グループのクラスターの種類は `NONE` です。ここで説明するアップグレード手順は、クラスターの種類が `EXTERNAL` か `NONE` に固有の手順です。

インスタンスをアップグレードする順序は、ロールがセカンダリであるかどうかと、ホストするレプリカが同期か非同期かに依存します。 非同期セカンダリ レプリカをホストする SQL Server のインスタンスを最初にアップグレードします。 次に、同期セカンダリ レプリカをホストするインスタンスをアップグレードします。 

   >[!NOTE]
   >可用性グループに非同期レプリカのみが含まれる場合、データ損失を回避する目的で、1 つのレプリカを同期に変更し、同期されるまで待ちます。 その後、このレプリカをアップグレードします。
   
始める前に、各データベースをバックアップします。

1. アップグレードの対象になっているセカンダリ レプリカをホストしているノードでリソースを停止します。
   
   アップグレード コマンドを実行する前に、リソースを停止します。そうすることで、クラスターはリソースを監視せず、不必要に不合格にすることがありません。 次の例では、場所の制約がノードに追加され、その結果、リソースが停止します。 `ag_cluster-master` をリソース名で、`nodeName1` をアップグレードの対象になっているレプリカをホストしているノードで更新します。

   ```bash
   pcs constraint location ag_cluster-master avoids nodeName1
   ```

1. セカンダリ レプリカで SQL Server をアップグレードします。

   次の例では、`mssql-server` パッケージと `mssql-server-ha` パッケージがアップグレードされます。

   ```bash
   sudo yum update mssql-server
   sudo yum update mssql-server-ha
   ```
1. 場所の制約を削除します。

   アップグレード コマンドを実行する前に、リソースを停止します。そうすることで、クラスターはリソースを監視せず、不必要に不合格にすることがありません。 次の例では、場所の制約がノードに追加され、その結果、リソースが停止します。 `ag_cluster-master` をリソース名で、`nodeName1` をアップグレードの対象になっているレプリカをホストしているノードで更新します。

   ```bash
   pcs constraint remove location-ag_cluster-master-rhel1--INFINITY
   ```
   ベスト プラクティスとしては、アップグレード後に (`pcs status` コマンドを使用して) リソースが確実に起動され、セカンダリ レプリカが接続され、状態が同期されるようにします。

1. セカンダリ レプリカがすべてアップグレードされたら、同期セカンダリ レプリカの 1 つに手動でフェールオーバーします。

   クラスターの種類が `EXTERNAL` の可用性グループについては、クラスター管理ツールを使用してフェールオーバーします。クラスターの種類が `NONE` の可用性グループでは、Transact-SQL を使用してフェールオーバーします。 
   次の例では、クラスター管理ツールを利用し、可用性グループがフェールオーバーされます。 `<targetReplicaName>` を、プライマリになる同期セカンダリ レプリカの名前に置換します。

   ```bash
   sudo pcs resource move ag_cluster-master <targetReplicaName> --master  
   ``` 
   
   >[!IMPORTANT]
   >次の手順は、クラスター マネージャーがない可用性グループにのみ適用されます。

   可用性グループのクラスターの種類が `NONE` の場合、手動でフェールオーバーします。 次の手順を実行します。

      A. 次のコマンドでは、プライマリ レプリカがセカンダリに設定されます。 `AG1` を実際の可用性グループの名前に置換します。 プライマリ レプリカをホストする SQL Server のインスタンスで Transact-SQL コマンドを実行します。

      ```transact-sql
      ALTER AVAILABILITY GROUP [ag1] SET (ROLE = SECONDARY);
      ```

      B. 次のコマンドでは、同期セカンダリ レプリカがプライマリに設定されます。 SQL Server のターゲット インスタンス (同期セカンダリ レプリカをホストするインスタンス) で次の Transact-SQL コマンドを実行します。

      ```transact-sql
      ALTER AVAILABILITY GROUP [ag1] FAILOVER;
      ```

1. フェールオーバー後、前の手順を繰り返すことで、古いプライマリ レプリカで SQL Server をアップグレードします。

   次の例では、`mssql-server` パッケージと `mssql-server-ha` パッケージがアップグレードされます。

   ```bash
   # add constraint for the resource to stop on the upgraded node
   # replace 'nodename2' with the name of the cluster node targeted for upgrade
   pcs constraint location ag_cluster-master avoids nodeName2
   sudo yum update mssql-server
   sudo yum update mssql-server-ha
   ```
   
   ```bash
   # upgrade mssql-server and mssql-server-ha packages
   sudo yum update mssql-server
   sudo yum update mssql-server-ha
   ```

   ```bash
   # remove the constraint; make sure the resource is started and replica is connected and synchronized
   pcs constraint remove location-ag_cluster-master-rhel1--INFINITY
   ```

1. 外部クラスター マネージャーのある可用性グループの場合、クラスターの種類が EXTERNAL ですが、手動のフェールオーバーによって引き起こされる場所の制約を消去します。 

   ```bash
   sudo pcs constraint remove cli-prefer-ag_cluster-master  
   ```

1. 新しくアップグレードされたセカンダリ レプリカ (前のプライマリ レプリカ) のデータ移動を再開します。 この手順は、SQL Server の上位インスタンスにより、可用性グループにおいて下位インスタンスにログ ブロックが転送されるときに必要です。 新しいセカンダリ レプリカ (前のプライマリ レプリカ) で次のコマンドを実行します。

   ```transact-sql
   ALTER DATABASE database_name SET HADR RESUME;
   ```

すべてのサーバーをアップグレードしたら、フェールバックできます。 必要に応じて、元のプライマリにフェールバックします。 

## <a name="drop-an-availability-group"></a>可用性グループを削除する

可用性グループを削除するには、[DROP AVAILABILITY GROUP](../t-sql/statements/drop-availability-group-transact-sql.md) を実行します。 クラスターの種類が `EXTERNAL` か `NONE` の場合、レプリカをホストする SQL Server の各インスタンスでコマンドを実行します。 たとえば、`group_name` という名前の可用性グループを削除するには、次のコマンドを実行します。

   ```transact-sql
   DROP AVAILABILITY GROUP group_name
   ```
 

## <a name="next-steps"></a>次の手順

[SQL Server 可用性グループ クラスター リソースに対して Red Hat Enterprise Linux クラスターを構成する](sql-server-linux-availability-group-cluster-rhel.md)

[SQL Server 可用性グループ クラスター リソースに対して SUSE Linux Enterprise Server クラスターを構成する](sql-server-linux-availability-group-cluster-sles.md)

[SQL Server 可用性グループ クラスター リソースに対して Ubuntu クラスターを構成する](sql-server-linux-availability-group-cluster-ubuntu.md)
