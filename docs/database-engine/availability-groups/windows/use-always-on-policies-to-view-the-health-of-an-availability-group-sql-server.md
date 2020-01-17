---
title: 可用性グループの正常性を確認するポリシー
description: Always On ポリシーまたは PowerShell を使用して、Always On 可用性グループの運用状態の正常性を確認します。
ms.custom: seo-lt-2019
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 6f1bcbc3-1220-4071-8e53-4b957f5d3089
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 13f43e5f66ca7700e9dd4732e9cf45ee1921548d
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75244741"
---
# <a name="use-always-on-policies-to-view-the-health-of-an-availability-group-sql-server"></a>AlwaysOn ポリシーを使用した可用性グループの正常性の確認 (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  このトピックでは、 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] の AlwaysOn ポリシーまたは [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]の PowerShell を使用して、AlwaysOn 可用性グループの運用状態の正常性を確認する方法について説明します。 AlwaysOn ポリシー ベースの管理の詳細については、「 [AlwaysOn 可用性グループでの運用上の問題のポリシー ベースの管理 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-policies-for-operational-issues-always-on-availability.md)の PowerShell を使用して、AlwaysOn 可用性グループの運用状態の正常性を確認する方法について説明します。  
  
> [!IMPORTANT]  
>  AlwaysOn ポリシーでは、カテゴリの名前が ID として使用されます。 AlwaysOn カテゴリの名前を変更すると、正常性評価の機能を使用できなくなります。 このため、AlwaysOn カテゴリの名前は変更しないでください。  
  
  
  
##  <a name="Permissions"></a> Permissions  
 CONNECT、VIEW SERVER STATE、および VIEW ANY DEFINITION 権限が必要です。  
  
##  <a name="SSMSProcedure"></a> AlwaysOn ダッシュボードの使用  
 **AlwaysOn ダッシュボードを開くには**  
  
1.  オブジェクト エクスプローラーで、可用性レプリカの 1 つをホストするサーバー インスタンスに接続します。 可用性グループ内のすべての可用性レプリカについての情報を表示するには、プライマリ レプリカをホストするサーバー インスタンスを使用してください。  
  
2.  サーバー名をクリックし、サーバー ツリーを展開します。  
  
3.  **[AlwaysOn 高可用性]** ノードを展開します。  
  
     **[可用性グループ]** ノードを右クリックするか、このノードを展開し、特定の可用性グループを右クリックします。  
  
4.  **[ダッシュボードの表示]** をクリックします。  
  
 AlwaysOn ダッシュボードの使用方法の詳細については、「[AlwaysOn ダッシュボードの使用 &#40;SQL Server Management Studio&#41;](~/database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)」を参照してください。  
  
##  <a name="PowerShellProcedure"></a> PowerShell の使用  
 **Use Always On policies to view the health of an availability group**  
  
1.  可用性レプリカの 1 つをホストするサーバー インスタンスを既定の操作対象に設定 (**cd**) します。 可用性グループ内のすべての可用性レプリカについての情報を表示するには、プライマリ レプリカをホストするサーバー インスタンスを使用してください。  
  
2.  次のコマンドレットを使用します。  
  
     **Test-SqlAvailabilityGroup**  
     SQL Server のポリシー ベースの管理 (PBM) のポリシーを評価することによって、可用性グループの正常性を査定します。 このコマンドレットを実行するには、CONNECT、VIEW SERVER STATE、および VIEW ANY DEFINITION 権限が必要です。  
  
     たとえば、次のコマンドでは、サーバー インスタンス `Computer\Instance`上で正常性状態が "Error" の可用性グループすべてを表示します。  
  
    ```  
    Get-ChildItem SQLSERVER:\Sql\Computer\Instance\AvailabilityGroups `   
    | Test-SqlAvailabilityGroup | Where-Object { $_.HealthState -eq "Error" }  
    ```  
  
     **Test-SqlAvailabilityReplica**  
     SQL Server のポリシー ベースの管理 (PBM) のポリシーを評価することによって、可用性レプリカの正常性を査定します。 このコマンドレットを実行するには、CONNECT、VIEW SERVER STATE、および VIEW ANY DEFINITION 権限が必要です。  
  
     たとえば、次のコマンドは、可用性グループ `MyReplica` 内の `MyAg` という名前の可用性レプリカの正常性を評価し、概要を出力します。  
  
    ```  
    Test-SqlAvailabilityReplica `   
    -Path SQLSERVER:\Sql\Computer\Instance\AvailabilityGroups\MyAg\AvailabilityReplicas\MyReplica  
    ```  
  
     **Test-SqlDatabaseReplicaState**  
     SQL Server のポリシー ベースの管理 (PBM) のポリシーを評価することによって、参加しているすべての可用性レプリカ上の可用性データベースの正常性を査定します。  
  
     たとえば、次のコマンドは、可用性グループ `MyAg` 内のすべての可用性データベースの正常性を評価し、各データベースの概要を出力します。  
  
    ```  
    Get-ChildItem SQLSERVER:\Sql\Computer\Instance\AvailabilityGroups\MyAg\DatabaseReplicaStates `   
     | Test-SqlDatabaseReplicaState  
    ```  
  
     これらのコマンドレットでは、次のオプションを使用できます。  
  
    |オプション|[説明]|  
    |------------|-----------------|  
    |**AllowUserPolicies**|AlwaysOn ポリシーのカテゴリにあるユーザー ポリシーを実行します。|  
    |**InputObject**|可用性グループ、可用性レプリカ、または可用性データベースの状態 (使用するコマンドレットに応じて異なります) を表すオブジェクトのコレクションです。 コマンドレットを実行すると、指定されたオブジェクトの正常性が計算されます。|  
    |**NoRefresh**|このパラメーターを設定した場合、コマンドレットを実行すると、 **-Path** パラメーターまたは **-InputObject** パラメーターで指定されたオブジェクトが手動で最新の情報に更新されません。|  
    |**[パス]**|可用性グループ、1 つ以上の可用性レプリカ、または可用性データベースのデータベース レプリカ クラスターの状態へのパス (使用するコマンドレットに応じて異なります) です。 これは省略可能なパラメーターです。 このパラメーターの値を指定しない場合、既定では、現在の場所に設定されます。|  
    |**ShowPolicyDetails**|このコマンドレットで実行された各ポリシー評価の結果を表示します。 コマンドレットを実行すると、ポリシー評価ごとに 1 つのオブジェクトが出力されます。このオブジェクトには評価の結果を表すフィールド (ポリシーが渡されるかどうかに関係なく、ポリシー名、カテゴリなど) があります。|  
  
     たとえば、次の **Test-SqlAvailabilityGroup** コマンドは、 **-ShowPolicyDetails** パラメーターを指定して、可用性グループ `MyAg`上で実行されたポリシー ベースの管理 (PBM) のポリシーごとに、このコマンドレットによって実行されたそれぞれのポリシー評価の結果を表示します。  
  
    ```  
    Test-SqlAvailabilityGroup `   
    -Path SQLSERVER:\Sql\Computer\Instance\AvailabilityGroups\AgName `  
    -ShowPolicyDetails  
  
    ```  
  
    > [!NOTE]  
    >  コマンドレットの構文を表示するには、 **PowerShell 環境で** Get-Help [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] コマンドレットを使用します。 詳細については、「 [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md)」を参照してください。  
  
 **SQL Server PowerShell プロバイダーを設定して使用するには**  
  
-   [SQL Server PowerShell プロバイダー](../../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
-   [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md)  
  
##  <a name="RelatedContent"></a> 関連コンテンツ  
 **SQL Server Alway On チームのブログ: PowerShell を使用した AlwaysOn 正常性状態の監視:**  
  
-   [パート 1: 基本的なコマンドレットの概要](https://blogs.msdn.microsoft.com/sqlalwayson/2012/02/13/monitoring-alwayson-health-with-powershell-part-1-basic-cmdlet-overview/)  
  
-   [パート 2: 高度なコマンドレットの使用方法](https://blogs.msdn.microsoft.com/sqlalwayson/2012/02/13/monitoring-alwayson-health-with-powershell-part-2-advanced-cmdlet-usage/)  
  
-   [パート 3: シンプルな監視アプリケーション](https://blogs.msdn.microsoft.com/sqlalwayson/2012/02/14/monitoring-alwayson-health-with-powershell-part-3-a-simple-monitoring-application/)  
  
-   [パート 4: SQL Server エージェントとの統合](https://blogs.msdn.microsoft.com/sqlalwayson/2012/02/15/monitoring-alwayson-health-with-powershell-part-4-integration-with-sql-server-agent/)  
  
## <a name="see-also"></a>参照  
 [AlwaysOn 可用性グループの概要 &#40;SQL Server&#41;](~/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [可用性グループの管理 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/administration-of-an-availability-group-sql-server.md)   
 [可用性グループの監視 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/monitoring-of-availability-groups-sql-server.md)   
 [AlwaysOn 可用性グループでの運用上の問題のポリシー ベースの管理 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-policies-for-operational-issues-always-on-availability.md)  
  
  


