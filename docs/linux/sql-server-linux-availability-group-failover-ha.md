---
title: 可用性グループのフェールオーバーを管理する - SQL Server on Linux
description: ''
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 03/01/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: ''
ms.openlocfilehash: e887c718c76563a7fcd8388c46a3e9e684faf6d5
ms.sourcegitcommit: 0c6c1555543daff23da9c395865dafd5bb996948
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2019
ms.locfileid: "70304850"
---
# <a name="always-on-availability-group-failover-on-linux"></a>Linux での Always On 可用性グループのフェールオーバー

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

可用性グループ (AG) のコンテキストでは、可用性レプリカのプライマリ ロールとセカンダリ ロールは、通常、フェールオーバーと呼ばれるプロセスで入れ替えることができます。 フェールオーバーには、自動フェールオーバー (データ損失なし)、計画的な手動フェールオーバー (データ損失なし)、および " *強制フェールオーバー*" と通常呼ばれる強制手動フェールオーバー (データ損失の可能性あり) の 3 つの形式があります。 自動フェールオーバーと計画的な手動フェールオーバーでは、すべてのデータが保持されます。 AG は、可用性レプリカのレベルでフェールオーバーされます。 つまり、AG はセカンダリ レプリカのいずれか (現在のフェールオーバー ターゲット) にフェールオーバーされます。 

フェールオーバーの背景情報については、「[フェールオーバーとフェールオーバー モード](../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md)」をご覧ください。

## <a name="failover"></a>手動フェールオーバー

外部のクラスター マネージャーによって管理されている AG をフェールオーバーするには、クラスター管理ツールを使います。 たとえば、ソリューションで Pacemaker を使って Linux クラスターが管理されている場合、RHEL または Ubuntu で手動フェールオーバーを実行するには、`pcs` を使います。 SLES では `crm` を使います。 

> [!IMPORTANT]
> 通常の動作では、SSMS や PowerShell などの Transact-SQL または SQL Server の管理ツールを使って、フェールオーバーを行わないでください。 `CLUSTER_TYPE = EXTERNAL` の場合、`FAILOVER_MODE` に対して指定できる値は `EXTERNAL` だけです。 これらの設定では、手動または自動のフェールオーバー操作はすべて、外部クラスター マネージャーによって実行されます。 データ損失の可能性がある強制的なフェールオーバーを実行する手順については、「[フェールオーバーを強制的に実行する](#forceFailover)」をご覧ください。

### <a name="a-namemanualfailovermanual-failover-steps"></a><a name="manualFailover">手動フェールオーバーの手順

フェールオーバーを行うには、プライマリ レプリカになるセカンダリ レプリカが同期されている必要があります。 セカンダリ レプリカが非同期の場合は、[可用性モードを変更](../database-engine/availability-groups/windows/change-the-availability-mode-of-an-availability-replica-sql-server.md)します。

手動フェールオーバーは 2 つのステップで行います。

   最初に、リソースを所有しているクラスター ノードから新しいノードに [AG リソースを移動することによって手動でフェールオーバー](#manualMove)を行います。

   クラスターによって AG リソースがフェールオーバーされ、場所の制約が追加されます。 この制約により、新しいノードで実行されるようにリソースが構成されます。 後で正常にフェールオーバーを行うには、この制約を削除します。

   次に、[場所の制約を削除](#removeLocConstraint)します。

#### <a name="manualMove"></a> 手順 1. 可用性グループ リソースを移動することにより手動でフェールオーバーを行う

*ag_cluster* という名前の AG リソースを *nodeName2* という名前のクラスター ノードに手動でフェールオーバーするには、ディストリビューションに適したコマンドを実行します。

- **RHEL/Ubuntu の例**

   ```bash
   sudo pcs resource move ag_cluster-master nodeName2 --master
   ```

- **SLES の例**

   ```bash
   crm resource migrate ag_cluster nodeName2
   ```

>[!IMPORTANT]
>手動でリソースをフェールオーバーした後、自動的に追加される場所の制約を削除する必要があります。

#### <a name="removeLocConstraint"> </a> 手順 2. 場所の制約の削除

手動フェールオーバーの間に、`pcs` のコマンド `move` または `crm` のコマンド `migrate` によって、新しいターゲット ノードに配置されるリソースに対する場所の制約が追加されます。 新しい制約を表示するには、リソースを手動で移動した後に次のコマンドを実行します。

- **RHEL/Ubuntu の例**

   ```bash
   sudo pcs constraint list --full
   ```

- **SLES の例**

   ```bash
   crm config show
   ```

手動フェールオーバーによって作成される制約の例。 
 `Enabled on: Node1 (score:INFINITY) (role: Master) (id:cli-prefer-ag_cluster-master)`

- **RHEL/Ubuntu の例**

   次のコマンドで、`cli-prefer-ag_cluster-master` は削除が必要な制約の ID です。 `sudo pcs constraint list --full` によってこの ID が返されます。 
   
   ```bash
   sudo pcs constraint remove cli-prefer-ag_cluster-master  
   ```
   
- **SLES の例**

   次のコマンドで、`cli-prefer-ms-ag_cluster` は制約の ID です。 `crm config show` によってこの ID が返されます。 
   
   ```bash
   crm configure
   delete cli-prefer-ms-ag_cluster 
   commit
   ```

>[!NOTE]
>自動フェールオーバーでは場所の制約が追加されないため、削除は不要です。 

詳細:
- [Red Hat - クラスター リソースの管理](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/6/html/Configuring_the_Red_Hat_High_Availability_Add-On_with_Pacemaker/ch-manageresource-HAAR.html)
- [Pacemaker - リソースを手動で移動する](https://clusterlabs.org/pacemaker/doc/en-US/Pacemaker/1.1/html/Clusters_from_Scratch/_manually_moving_resources_around_the_cluster.html)
 [SLES 管理ガイド - リソース](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#sec.ha.troubleshooting.resource) 
 
## <a name="forceFailover"></a> フェールオーバーを強制的に実行する 

強制フェールオーバーは、厳密にディザスター リカバリーを目的としたものです。 この場合、プライマリ データセンターがダウンしているため、クラスター管理ツールでフェールオーバーを行うことはできません。 非同期のセカンダリ レプリカに対して強制フェールオーバーを実行した場合、データ損失の可能性があります。 強制フェールオーバーは、AG にサービスをすぐに復元する必要があり、データが失われてもかまわない場合に限り、実行してください。

たとえばプライマリ データ センターでの障害のためにクラスターが応答しないときなど、クラスター管理ツールを使ってクラスターを操作できない場合は、フェールオーバーを強制的に行って、外部クラスター マネージャーをバイパスすることが必要になる場合があります。 この手順は、データ損失のリスクがあるため、通常の操作にはお勧めしません。 クラスター管理ツールでフェールオーバー アクションを実行できないときに使用してください。 機能的には、この手順は、Windows の AG で[強制手動フェールオーバーを実行する](../database-engine/availability-groups/windows/perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)ことと似ています。
 
この強制フェールオーバーのプロセスは、SQL Server on Linux に固有のものです。

1. AG リソースがクラスターによって管理されなくなっていることを確認します。 

      - ターゲット クラスター ノードで、リソースをアンマネージド モードに設定します。 このコマンドでは、リソースの監視と管理を停止するように、リソース エージェントに通知されます。 例: 
      
      ```bash
      sudo pcs resource unmanage <resourceName>
      ```

      - リソース モードをアンマネージド モードに設定しようとして失敗する場合は、リソースを削除します。 例:

      ```bash
      sudo pcs resource delete <resourceName>
      ```

      >[!NOTE]
      >リソースを削除すると、関連付けられているすべての制約も削除されます。 

1. セカンダリ レプリカがホストされている SQL Server のインスタンスで、セッション コンテキスト変数 `external_cluster` を設定します。

   ```Transact-SQL
   EXEC sp_set_session_context @key = N'external_cluster', @value = N'yes';
   ```

1. Transact-SQL で AG をフェールオーバーします。 次の例では、`<MyAg>` を実際の AG の名前に置き換えます。 ターゲット セカンダリ レプリカがホストされている SQL Server のインスタンスに接続し、次のコマンドを実行します。

   ```Transact-SQL
   ALTER AVAILABILITY GROUP <MyAg> FORCE_FAILOVER_ALLOW_DATA_LOSS;
   ```

1.  強制フェールオーバーの後、クラスター リソースの監視と管理を再開する前、または AG リソースを再作成する前に、AG を正常な状態にします。 「[強制フェールオーバー後の必須タスク](../database-engine/availability-groups/windows/perform-a-forced-manual-failover-of-an-availability-group-sql-server.md#FollowUp)」を確認してください。

1.  クラスター リソースの監視と管理を再開します。

   クラスター リソースの監視と管理を再開するには、次のコマンドを実行します。

   ```bash
   sudo pcs resource manage <resourceName>
   sudo pcs resource cleanup <resourceName>
   ```

   クラスター リソースを削除した場合は、作成し直します。 クラスター リソースを再作成するには、「[可用性グループのリソースを作成する](sql-server-linux-availability-group-cluster-rhel.md#create-availability-group-resource)」の手順に従います。

>[!Important]
>データが失われる可能性があるため、ディザスター リカバリー訓練に対する前の手順は使用しないでください。 代わりに、非同期レプリカを同期に変更し、[通常の手動フェールオーバー](#manualFailover)の手順に従います。

## <a name="database-level-monitoring-and-failover-trigger"></a>データベース レベルの監視とフェールオーバーのトリガー

`CLUSTER_TYPE=EXTERNAL` の場合、フェールオーバー トリガーのセマンティクスは WSFC の場合と異なります。 AG が WSFC 内の SQL Server のインスタンス上にある場合、状態がデータベースに対する `ONLINE` から変わると、AG の正常性でエラーが報告されます。 それに対して、クラスター マネージャーでフェールオーバー アクションがトリガーされます。 Linux では、SQL Server のインスタンスはクラスターと通信できません。 データベースの正常性の監視は、"*アウトサイドイン*" で行われます。 ユーザーが (AG の作成時にオプション `DB_FAILOVER=ON` を設定することにより) データベース レベルのフェールオーバー監視とフェールオーバーにオプトインしている場合、クラスターでは監視アクションが実行されるたびにデータベースの状態が `ONLINE` であるかどうかがチェックされます。 クラスターでは、`sys.databases` で状態のクエリが実行されます。 `ONLINE` 以外の状態の場合は、フェールオーバーが自動的にトリガーされます (自動フェールオーバーの条件が満たされている場合)。 フェールオーバーの実際の時間は、監視アクションの頻度と、sys.databases で更新されているデータベースの状態によって異なります。

自動フェールオーバーには、少なくとも 1 つの同期レプリカが必要です。

## <a name="next-steps"></a>次の手順

[SQL Server 可用性グループ クラスター リソースに対して Red Hat Enterprise Linux クラスターを構成する](sql-server-linux-availability-group-cluster-rhel.md)

[SQL Server 可用性グループ クラスター リソースに対して SUSE Linux Enterprise Server クラスターを構成する](sql-server-linux-availability-group-cluster-sles.md)

[SQL Server 可用性グループ クラスター リソースに対して Ubuntu クラスターを構成する](sql-server-linux-availability-group-cluster-ubuntu.md)
