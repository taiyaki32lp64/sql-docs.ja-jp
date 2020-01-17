---
title: 可用性グループの計画的な手動フェールオーバーの実行
description: このトピックでは、Always On 可用性グループの計画的な手動ールオーバーを実行する方法について説明します。
ms.custom: seodec18
ms.date: 10/25/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.availabilitygroup.manualfailover.f1
helpviewer_keywords:
- Availability Groups [SQL Server], failover
- failover [SQL Server], AlwaysOn Availability Groups
ms.assetid: 419f655d-3f9a-4e7d-90b9-f0bab47b3178
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 2346c770c5fec742d7c5805f028bd87bebaf71b1
ms.sourcegitcommit: f8cf8cc6650a22e0b61779c20ca7428cdb23c850
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/04/2019
ms.locfileid: "74822496"
---
# <a name="perform-a-planned-manual-failover-of-an-always-on-availability-group-sql-server"></a>Always On 可用性グループの計画的な手動フェールオーバーの実行 (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
このトピックでは、[!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] の [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]、[!INCLUDE[tsql](../../../includes/tsql-md.md)]、または PowerShell を使用して、AlwaysOn 可用性グループ上でデータを失わずに手動フェールオーバー (*計画的な手動フェールオーバー*) を実行する方法について説明します。 可用性グループは、可用性レプリカのレベルでフェールオーバーします。 AlwaysOn 可用性グループのフェールオーバーのように、計画的な手動フェールオーバーではセカンダリ レプリカがプライマリ ロールに移行します。 同時に、フェールオーバーによって元のプライマリ レプリカがセカンダリ ロールに移行します。  
  
計画的な手動フェールオーバーは、プライマリ レプリカおよびターゲット セカンダリ レプリカが同期コミット モードで動作していて、現在同期されている場合にのみサポートされます。 計画的な手動フェールオーバーでは、ターゲット セカンダリ レプリカの可用性グループに参加しているセカンダリ データベース内のすべてのデータが維持されます。 プライマリ レプリカがセカンダリ ロールに移行すると、そのデータベースがセカンダリ データベースになります。 次に、新しいプライマリ データベースとの同期が開始されます。 すべてが SYNCHRONIZED 状態に移行した後は、新しいセカンダリ レプリカが、将来の計画的な手動フェールオーバーのターゲットとして機能できるようになります。  
  
> [!NOTE]  
>  セカンダリ レプリカとプライマリ レプリカの両方に対して自動フェールオーバー モードを構成し、セカンダリ レプリカを同期すると、自動フェールオーバーのターゲットとしても機能できるようになります。 詳細については、「[可用性モード &#40;AlwaysOn 可用性グループ&#41;](../../../database-engine/availability-groups/windows/availability-modes-always-on-availability-groups.md)」を参照してください。  
   
##  <a name="BeforeYouBegin"></a> はじめる前に 

>[!IMPORTANT]
>クラスター マネージャーを使わないで読み取りスケール可用性グループをフェールオーバーするには、固有の手順があります。 可用性グループで CLUSTER_TYPE = NONE が設定されている場合は、「[読み取りスケール可用性グループのプライマリ レプリカをフェールオーバーする](#fail-over-the-primary-replica-on-a-read-scale-availability-group)」の手順に従ってください。

###  <a name="Restrictions"></a> 制限事項と制約事項 
  
- フェールオーバー コマンドは、ターゲットのセカンダリ レプリカがコマンドを受け入れた直後に戻ります。 ただし、データベースの復旧は、可用性グループがフェールオーバーを完了した後に非同期で行われます。 
- フェールオーバー時に、可用性グループ内のデータベース間の一貫性が維持されない場合があります。 
  
    > [!NOTE] 
    >  複数のデータベースにまたがるトランザクションと分散トランザクションのサポートは、SQL Server とオペレーティング システムのバージョンによって異なります。 詳細については、「[Always On 可用性グループとデータベース ミラーリングでの複数データベースにまたがるトランザクションと分散トランザクション &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/transactions-always-on-availability-and-database-mirroring.md)」を参照してください。 
  
###  <a name="Prerequisites"></a> 前提条件と制限 
  
-   ターゲットのセカンダリ レプリカとプライマリ レプリカは、両方とも同期コミット可用性モードで実行されている必要があります。 
-   現在、ターゲットのセカンダリ レプリカはプライマリ レプリカと同期されている必要があります。 このセカンダリ レプリカのすべてのセカンダリ データベースが可用性グループに参加している必要があります。 これらは対応するプライマリ データベースとも同期されている必要があります (つまり、ローカルのセカンダリ データベースが同期されている必要があります)。 
  
    > [!TIP] 
    >  セカンダリ レプリカのフェールオーバーの準備状態を調べるには、[sys.dm_hadr_database_replica_cluster_states](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-cluster-states-transact-sql.md) 動的管理ビューで **is_failover_ready** 列をクエリします。 または、[AlwaysOn グループ ダッシュボード](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)の **[フェールオーバーの準備]** 列を確認します。 
-   このタスクは、ターゲット セカンダリ レプリカ上でのみサポートされます。 ターゲット セカンダリ レプリカをホストするサーバー インスタンスに接続されている必要があります。 
  
###  <a name="Security"></a> セキュリティ 
  
####  <a name="Permissions"></a> Permissions 
 可用性グループに ALTER AVAILABILITY GROUP のアクセス許可が必要です。 CONTROL AVAILABILITY GROUP アクセス許可、ALTER ANY AVAILABILITY GROUP アクセス許可、または CONTROL SERVER アクセス許可も必要です。 
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用 
 可用性グループで手動フェールオーバーを行うには: 
  
1. オブジェクト エクスプローラーで、フェールオーバーを行う必要がある可用性グループのセカンダリ レプリカをホストするサーバー インスタンスに接続します。 サーバー ツリーを展開します。 
  
2. **[AlwaysOn 高可用性]** ノードと **[可用性グループ]** ノードを展開します。 
  
3. フェールオーバーする [可用性グループ] ノードを右クリックし、 **[フェールオーバー]** を選択します。 
  
4. 可用性グループのフェールオーバー ウィザードが開始されます。 詳細については、「[可用性グループのフェールオーバー ウィザードの使用 &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-fail-over-availability-group-wizard-sql-server-management-studio.md)」を参照してください。 
  
##  <a name="TsqlProcedure"></a> Transact-SQL を使用する 
 可用性グループで手動フェールオーバーを行うには: 
  
1. ターゲット セカンダリ レプリカをホストするサーバー インスタンスに接続します。 
  
2. [ALTER AVAILABILITY GROUP](../../../t-sql/statements/alter-availability-group-transact-sql.md) ステートメントを使用します。次にその例を示します。 
  
     ALTER AVAILABILITY GROUP *group_name* FAILOVER 
  
     ステートメントの *group_name* は可用性グループの名前です。 
  
     次の例では、接続されているセカンダリ レプリカに *MyAg* 可用性グループを手動でフェールオーバーします。 
  
    ```  
    ALTER AVAILABILITY GROUP MyAg FAILOVER;  
    ```  
  
##  <a name="PowerShellProcedure"></a> PowerShell を使用する 
 可用性グループで手動フェールオーバーを行うには: 
  
1. ディレクトリ変更コマンド (**cd**) を使用して、ターゲット セカンダリ レプリカをホストするサーバー インスタンスに移動します。 
  
2. **Switch-SqlAvailabilityGroup** コマンドレットを使用します。 
  
    > [!NOTE] 
    >  コマンドレットの構文を表示するには、 **PowerShell 環境で** Get-Help [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] コマンドレットを使用します。 詳細については、「[SQL Server PowerShell のヘルプの参照](../../../relational-databases/scripting/get-help-sql-server-powershell.md)」を参照してください。 
  
     次の例では、指定したパスのセカンダリ レプリカに *MyAg* 可用性グループを手動でフェールオーバーします。 
  
    ```  
    Switch-SqlAvailabilityGroup -Path SQLSERVER:\Sql\SecondaryServer\InstanceName\AvailabilityGroups\MyAg  
    ```  
  
    SQL Server PowerShell プロバイダーを設定して使用するには: 
  
    -   [SQL Server PowerShell プロバイダー](../../../relational-databases/scripting/sql-server-powershell-provider.md) 
    -   [SQL Server PowerShell のヘルプの参照](../../../relational-databases/scripting/get-help-sql-server-powershell.md) 

##  <a name="FollowUp"></a> 補足情報:可用性グループの手動フェールオーバーを実行した後 
 可用性グループの [!INCLUDE[ssFosAuto](../../../includes/ssfosauto-md.md)] の外側でフェールオーバーした場合、Windows Server フェールオーバー クラスタリング ノードのクォーラム投票を調整して新しい可用性グループの構成を反映します。 詳細については、「[Windows Server フェールオーバー クラスタリング &#40;WSFC&#41; と SQL Server](../../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md)」を参照してください。 

<a name = "ReadScaleOutOnly"><a/>

## <a name="fail-over-the-primary-replica-on-a-read-scale-availability-group"></a>読み取りスケール可用性グループのプライマリ レプリカをフェールオーバーする

[!INCLUDE[Force failover](../../../includes/ss-force-failover-read-scale-out.md)]

## <a name="see-also"></a>参照 

 * [AlwaysOn 可用性グループの概要 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md) 
 * [フェールオーバーとフェールオーバー モード &#40;AlwaysOn 可用性グループ&#41;](../../../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md) 
 * [可用性グループの強制手動フェールオーバーの実行 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/perform-a-forced-manual-failover-of-an-availability-group-sql-server.md) 
  
  
