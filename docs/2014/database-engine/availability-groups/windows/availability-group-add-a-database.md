---
title: 可用性グループへのデータベースの追加 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- primary databases [SQL Server], in availability group
- Availability Groups [SQL Server], configuring
- Availability Groups [SQL Server], databases
ms.assetid: 2a54eef8-9e8e-4e04-909c-6970112d55cc
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: dda5ac5b2f569c8438439ec77da33fde3a385fa0
ms.sourcegitcommit: a165052c789a327a3a7202872669ce039bd9e495
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72782898"
---
# <a name="add-a-database-to-an-availability-group-sql-server"></a>可用性グループへのデータベースの追加 (SQL Server)
  このトピックでは、 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]で [!INCLUDE[tsql](../../../includes/tsql-md.md)]、 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]、または PowerShell を使用して、AlwaysOn 可用性グループにデータベースを追加する方法について説明します。  
  
-   **作業を開始する準備:**  
  
     [前提条件と制限](#Prerequisites)  
  
     [Permissions](#Permissions)  
  
-   **可用性グループにデータベースを追加する方法:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Prerequisites"></a> 前提条件と制限  
  
-   プライマリ レプリカをホストするサーバー インスタンスに接続されている必要があります。  
  
-   プライマリ レプリカがホストされるサーバー インスタンスにデータベースが存在し、データベースが可用性データベースの前提条件と制限に準拠している必要があります。 詳細については、「[AlwaysOn 可用性グループの前提条件、制限事項、および推奨事項 &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md)」を参照してください。  
  
###  <a name="Security"></a> セキュリティ  
  
###  <a name="Permissions"></a> アクセス許可  
 可用性グループの ALTER AVAILABILITY GROUP 権限、CONTROL AVAILABILITY GROUP 権限、ALTER ANY AVAILABILITY GROUP 権限、または CONTROL SERVER 権限が必要です。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
 **可用性グループにデータベースを追加するには**  
  
1.  オブジェクト エクスプローラーで、プライマリ レプリカをホストするサーバー インスタンスに接続し、サーバー ツリーを展開します。  
  
2.  **[AlwaysOn 高可用性]** ノードと **[可用性グループ]** ノードを展開します。  
  
3.  可用性グループを右クリックし、次のコマンドのどちらかを選択します。  
  
    -   可用性グループへのデータベース追加ウィザードを起動するには、 **[データベースの追加]** をクリックします。 詳細については、[可用性グループへのデータベース追加ウィザードの使用 &#40;SQL Server Management Studio&#41;](availability-group-add-database-to-group-wizard.md) を参照してください。  
  
    -   1 つまたは複数のデータベースを追加するには、 **[可用性グループのプロパティ]** ダイアログ ボックスでそれらを指定し、 **[プロパティ]** をクリックします。 データベースを追加する手順は以下のとおりです。  
  
        1.  **[可用性データベース]** ペインで、 **[追加]** ボタンをクリックします。 これにより、空のデータベース フィールドが作成され、選択されます。  
  
        2.  可用性データベースの前提条件を満たしているデータベースの名前を入力します。  
  
         別のデータベースを追加するには、上記の手順を繰り返します。 データベースの指定を完了したら、 **[OK]** をクリックして操作を完了します。  
  
         **[可用性グループのプロパティ]** ダイアログ ボックスを使用して可用性グループにデータベースを追加した後、セカンダリ レプリカをホストする各サーバー インスタンスで、対応するセカンダリ データベースを構成する必要があります。 詳細については、「[AlwaysOn セカンダリ データベース上のデータ移動の開始 &#40;SQL Server&#41;](start-data-movement-on-an-always-on-secondary-database-sql-server.md)」を参照してください。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
 **可用性グループにデータベースを追加するには**  
  
1.  プライマリ レプリカをホストするサーバー インスタンスをホストするセカンダリ インスタンスに接続します。  
  
2.  [ALTER AVAILABILITY GROUP](/sql/t-sql/statements/alter-availability-group-transact-sql) ステートメントを使用します。次にその例を示します。  
  
     ALTER AVAILABILITY GROUP *group_name* ADD DATABASE *database_name* [,...*n*]  
  
     *group_name* は可用性グループの名前、 *database_name* はグループに追加するデータベースの名前です。  
  
     次の例では、 *MyDb3* データベースを *MyAG* 可用性グループに追加します。  
  
    ```  
    -- Connect to the server instance that hosts the primary replica.  
    -- Add an existing database to the availability group.  
    ALTER AVAILABILITY GROUP MyAG ADD DATABASE MyDb3;  
    GO  
    ```  
  
3.  可用性グループにデータベースを追加した後、セカンダリ データベースをホストする各サーバー インスタンスで、対応するセカンダリ データベースを構成する必要があります。 詳細については、「[AlwaysOn セカンダリ データベース上のデータ移動の開始 &#40;SQL Server&#41;](start-data-movement-on-an-always-on-secondary-database-sql-server.md)」を参照してください。  
  
##  <a name="PowerShellProcedure"></a> PowerShell の使用  
 **可用性グループにデータベースを追加するには**  
  
1.  プライマリ レプリカをホストするサーバー インスタンスにディレクトリを変更 (`cd`) します。  
  
2.  `Add-SqlAvailabilityDatabase` コマンドレットを使用します。  
  
     たとえば、次のコマンドは、そのプライマリ レプリカが `MyDd` によってホストされるセカンダリ データベース `MyAG` を `PrimaryServer\InstanceName`可用性グループに追加します。  
  
    ```powershell
    Add-SqlAvailabilityDatabase `   
     -Path SQLSERVER:\SQL\PrimaryServer\InstanceName\AvailabilityGroups\MyAG `   
     -Database "MyDb"  
    ```  
  
    > [!NOTE]  
    >  コマンドレットの構文を表示するには、`Get-Help` PowerShell 環境で [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] コマンドレットを使用します。 詳細については、「 [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md)」を参照してください。  
  
3.  可用性グループにデータベースを追加した後、セカンダリ データベースをホストする各サーバー インスタンスで、対応するセカンダリ データベースを構成する必要があります。 詳細については、「[AlwaysOn セカンダリ データベース上のデータ移動の開始 &#40;SQL Server&#41;](start-data-movement-on-an-always-on-secondary-database-sql-server.md)」を参照してください。  
  
 SQL Server PowerShell プロバイダーを設定して使用する方法については、「 [SQL Server PowerShell プロバイダー](../../../powershell/sql-server-powershell-provider.md)」を参照してください。

 次の例では、可用性グループのプライマリ レプリカをホストするサーバー インスタンス上のデータベースからセカンダリ データベースを準備し、そのデータベースを (プライマリ データベースとして) 可用性グループに追加した後、セカンダリ データベースを可用性グループに参加させるすべての処理を示しています。 最初に、データベースとトランザクション ログをバックアップします。 次に、セカンダリ レプリカをホストするサーバー インスタンスにデータベースとログのバックアップを復元します。  
  
 この例では、`Add-SqlAvailabilityDatabase` を 2 回呼び出します。1 回目はデータベースを可用性グループに追加するためにプライマリ レプリカで呼び出し、2 回目はセカンダリ レプリカ上のセカンダリ データベースを可用性グループに参加させるためにセカンダリ レプリカで呼び出します。 セカンダリ レプリカが複数ある場合は、それぞれのセカンダリ データベースを復元して参加させます。  
  
```powershell
$DatabaseBackupFile = "\\share\backups\MyDatabase.bak"  
$LogBackupFile = "\\share\backups\MyDatabase.trn"  
$MyAgPrimaryPath = "SQLSERVER:\SQL\PrimaryServer\InstanceName\AvailabilityGroups\MyAg"  
$MyAgSecondaryPath = "SQLSERVER:\SQL\SecondaryServer\InstanceName\AvailabilityGroups\MyAg"  
  
Backup-SqlDatabase -Database "MyDatabase" -BackupFile $DatabaseBackupFile -ServerInstance "PrimaryServer\InstanceName"  
Backup-SqlDatabase -Database "MyDatabase" -BackupFile $LogBackupFile -ServerInstance "PrimaryServer\InstanceName" -BackupAction 'Log'  
  
Restore-SqlDatabase -Database "MyDatabase" -BackupFile $DatabaseBackupFile -ServerInstance "SecondaryServer\InstanceName" -NoRecovery  
Restore-SqlDatabase -Database "MyDatabase" -BackupFile $LogBackupFile -ServerInstance "SecondaryServer\InstanceName" -RestoreAction 'Log' -NoRecovery  
  
Add-SqlAvailabilityDatabase -Path $MyAgPrimaryPath -Database "MyDatabase"  
Add-SqlAvailabilityDatabase -Path $MyAgSecondaryPath -Database "MyDatabase"
```  
  
## <a name="see-also"></a>参照  
 [AlwaysOn 可用性グループ&#40;SQL Server&#41;の概要](overview-of-always-on-availability-groups-sql-server.md)   
 [可用性グループの作成と構成 &#40;SQL Server&#41;](creation-and-configuration-of-availability-groups-sql-server.md)   
 [AlwaysOn ダッシュボード&#40;SQL Server Management Studio&#41;を使用する](use-the-always-on-dashboard-sql-server-management-studio.md)   
 [可用性グループの監視 &#40;Transact-SQL&#41;](monitor-availability-groups-transact-sql.md)  
