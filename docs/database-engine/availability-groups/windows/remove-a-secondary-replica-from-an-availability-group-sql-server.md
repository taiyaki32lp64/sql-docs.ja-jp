---
title: 可用性グループからセカンダリ レプリカを削除する
description: 'Transact-SQL (T-SQL)、PowerShell、または SQL Server Management Studio のいずれかを使用して Always On 可用性グループからセカンダリ レプリカを削除する手順。 '
ms.custom: seodec18
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.availabilitygroup.removesecondaryar.f1
helpviewer_keywords:
- Availability Groups [SQL Server], availability replicas
- Availability Groups [SQL Server], configuring
ms.assetid: 35ddc8b6-3e7c-4417-9a0a-d4987a09ddf7
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: f0b73bf44f4990b94ad44e450214099760901134
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68014385"
---
# <a name="remove-a-secondary-replica-from-an-availability-group-sql-server"></a>可用性グループからのセカンダリ レプリカの削除 (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このトピックでは、 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]で [!INCLUDE[tsql](../../../includes/tsql-md.md)]、 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]、または PowerShell を使用して、AlwaysOn 可用性グループからセカンダリ レプリカを削除する方法について説明します。  
 
   
##  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   このタスクは、プライマリ レプリカ上でのみサポートされます。    
-   セカンダリ レプリカのみを可用性グループから削除できます。  
  
## <a name="Prerequisites"></a> 前提条件  
  
-   可用性グループのプライマリ レプリカをホストするサーバー インスタンスに接続している。  
  
##  <a name="Permissions"></a> Permissions  
 可用性グループの ALTER AVAILABILITY GROUP 権限、CONTROL AVAILABILITY GROUP 権限、ALTER ANY AVAILABILITY GROUP 権限、または CONTROL SERVER 権限が必要です。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
 **セカンダリ レプリカを削除するには**  
  
1.  オブジェクト エクスプローラーで、プライマリ レプリカをホストするサーバー インスタンスに接続し、サーバー ツリーを展開します。  
  
2.  **[AlwaysOn 高可用性]** ノードと **[可用性グループ]** ノードを展開します。  
  
3.  可用性グループを選択し、 **[可用性レプリカ]** ノードを展開します。  
  
4.  削除するレプリカが複数であるか単独であるかによって、次のように実行する手順が異なります。  
  
    -   複数のレプリカを削除するには、 **[オブジェクト エクスプローラーの詳細]** ペインを使用して、削除するレプリカを表示してすべて選択します。 詳細については、「[[オブジェクト エクスプローラーの詳細] を使用した可用性グループの監視 &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-object-explorer-details-to-monitor-availability-groups.md) を参照してください。  
  
    -   単独のレプリカを削除するには、 **[オブジェクト エクスプローラー]** ペインまたは **[オブジェクト エクスプローラーの詳細]** ペインで選択します。  
  
5.  選択したセカンダリ レプリカを右クリックし、コマンド メニューの **[可用性グループからの削除]** をクリックします。  
  
6.  **[可用性グループからのセカンダリ レプリカの削除]** ダイアログ ボックスで、表示されたすべてのデータベースを削除するには、 **[OK]** をクリックします。 表示されたレプリカをすべて削除しない場合は、 **[キャンセル]** をクリックします。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
 **セカンダリ レプリカを削除するには**  
  
1.  プライマリ レプリカをホストするサーバー インスタンスに接続します。  
  
2.  [ALTER AVAILABILITY GROUP](../../../t-sql/statements/alter-availability-group-transact-sql.md) ステートメントを使用します。次にその例を示します。  
  
     ALTER AVAILABILITY GROUP *group_name* REMOVE REPLICA ON '*instance_name*' [,...*n*]  
  
     *group_name* は可用性グループの名前、 *instance_name* はセカンダリ レプリカがあるサーバー インスタンスです。  
  
     次の例では、セカンダリ レプリカを *MyAG* 可用性グループから削除しています。 対象のセカンダリ レプリカは、 *COMPUTER02* という名前のコンピューターの *HADR_INSTANCE*という名前のサーバー インスタンスにあります。  
  
    ```  
    ALTER AVAILABILITY GROUP MyAG REMOVE REPLICA ON 'COMPUTER02\HADR_INSTANCE';  
    ```  
  
##  <a name="PowerShellProcedure"></a> PowerShell の使用  
 **セカンダリ レプリカを削除するには**  
  
1.  プライマリ レプリカをホストするサーバー インスタンスにディレクトリを変更 (**cd**) します 。  
  
2.  **Remove-SqlAvailabilityReplica** コマンドレットを使用します。  
  
     たとえば、次のコマンドは、サーバー `MyReplica` 上の可用性レプリカを、 `MyAg`という名前の可用性グループから削除します。  このコマンドは、可用性グループのプライマリ レプリカをホストするサーバー インスタンスで実行する必要があります。  
  
    ```  
    Remove-SqlAvailabilityReplica `   
    -Path SQLSERVER:\SQL\PrimaryServer\InstanceName\AvailabilityGroups\MyAg\AvailabilityReplicas\MyReplica  
    ```  
  
    > [!NOTE]  
    >  コマンドレットの構文を表示するには、 **PowerShell 環境で** Get-Help [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] コマンドレットを使用します。 詳細については、「 [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md)」を参照してください。  
  
 **SQL Server PowerShell プロバイダーを設定して使用するには**  
  
-   [SQL Server PowerShell プロバイダー](../../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
##  <a name="PostBestPractices"></a> 補足情報:セカンダリ レプリカの削除後  
 現在使用できないレプリカを指定した場合、そのレプリカがオンラインに戻ったとき、可用性グループに属していないことが検出されます。  
  
 レプリカの削除により、データの受信が停止します。 セカンダリ レプリカがグローバル ストアから削除されたことが確認されると、RECOVERING 状態でローカル サーバー インスタンスに残っている可用性グループ設定がデータベースから削除されます。  
  
## <a name="see-also"></a>参照  
 [AlwaysOn 可用性グループの概要 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [可用性グループへのセカンダリ レプリカの追加 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server.md)   
 [可用性グループの削除 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remove-an-availability-group-sql-server.md)  
  
  
