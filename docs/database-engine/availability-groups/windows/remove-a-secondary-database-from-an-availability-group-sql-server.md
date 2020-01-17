---
title: セカンダリ データベースの可用性グループからの削除
description: Transact-SQL (T-SQL)、PowerShell、または SQL Server Management Studio のいずれかを使用して Always On 可用性グループからセカンダリ データベースを削除する手順について説明します。
ms.custom: seodec18
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.availabilitygroup.unjoindb.f1
helpviewer_keywords:
- secondary databases [SQL Server], in availability group
- Availability Groups [SQL Server], removing
- Availability Groups [SQL Server], databases
ms.assetid: 4e51a570-58d7-4f01-9390-4198f3602576
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 94b495bf507dcbe67c305dbb69454bad943d2003
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68014443"
---
# <a name="remove-a-secondary-database-from-an-availability-group-sql-server"></a>可用性グループからのセカンダリ データベースの削除 (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このトピックでは、 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]で [!INCLUDE[tsql](../../../includes/tsql-md.md)]、 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]、または PowerShell を使用して、AlwaysOn 可用性グループからセカンダリ データベースを削除する方法について説明します。  
   
  
##  <a name="Prerequisites"></a> 前提条件と制限  
  
-   このタスクは、セカンダリ レプリカ上でのみサポートされます。 データベースを削除するセカンダリ レプリカをホストするサーバー インスタンスに接続している必要があります。  
  
 
##  <a name="Permissions"></a> Permissions  
 データベースに対する ALTER 権限が必要です。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
 **セカンダリ データベースを可用性グループから削除するには**  
  
1.  オブジェクト エクスプローラーで、1 つ以上のセカンダリ データベースを削除するセカンダリ レプリカをホストするサーバー インスタンスに接続し、サーバー ツリーを展開します。  
  
2.  **[AlwaysOn 高可用性]** ノードと **[可用性グループ]** ノードを展開します。  
  
3.  可用性グループを選択し、 **[可用性データベース]** ノードを展開します。  
  
4.  削除するデータベースが複数であるか 1 つのみであるかによって、次のように実行する手順が異なります。  
  
    -   複数のデータベースを削除するには、 **[オブジェクト エクスプローラーの詳細]** ペインを使用して削除するデータベースを表示し、すべてを選択します。 詳細については、「[[オブジェクト エクスプローラーの詳細] を使用した可用性グループの監視 &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-object-explorer-details-to-monitor-availability-groups.md)」を参照してください。  
  
    -   1 つのデータベースを削除するには、 **[オブジェクト エクスプローラー]** ペインまたは **[オブジェクト エクスプローラーの詳細]** ペインでそれを選択します。  
  
5.  選択したデータベースを右クリックし、コマンド メニューの **[セカンダリ データベースの削除]** を選択します。  
  
6.  **[可用性グループからのデータベースの削除]** ダイアログ ボックスで、表示されたすべてのデータベースを削除するには、 **[OK]** をクリックします。 表示されたデータベースをすべて削除しない場合は、 **[キャンセル]** をクリックします。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
 **セカンダリ データベースを可用性グループから削除するには**  
  
1.  セカンダリ レプリカをホストするサーバー インスタンスに接続します。  
  
2.  [ALTER DATABASE ステートメントの SET HADR 句](../../../t-sql/statements/alter-database-transact-sql-set-hadr.md) を使用します。次にその例を示します。  
  
     ALTER DATABASE *database_name* SET HADR OFF  
  
     *database_name* の部分には、可用性グループから削除するセカンダリ データベース名を指定します。  
  
     次の例では、ローカル セカンダリ データベース *MyDb2* を、可用性グループから削除します。  
  
    ```  
    ALTER DATABASE MyDb2 SET HADR OFF;  
    GO  
    ```  
  
##  <a name="PowerShellProcedure"></a> PowerShell の使用  
 **セカンダリ データベースを可用性グループから削除するには**  
  
1.  ディレクトリ変更コマンド (**cd**) を使用して、セカンダリ レプリカがホストされているサーバー インスタンスに移動します。  
  
2.  可用性グループから削除する可用性データベース名を指定して、 **Remove-SqlAvailabilityDatabase** コマンドレットを使用します。 セカンダリ レプリカをホストするサーバー インスタンスに接続している場合は、ローカル セカンダリ データベースのみが可用性グループから削除されます。  
  
     たとえば、次のコマンドは、 `MyDb8` という名前のサーバー インスタンスにホストされたセカンダリ レプリカから、セカンダリ データベース `SecondaryComputer\Instance`を削除します。 削除されたセカンダリ データベースへのデータ同期は行われなくなります。 このコマンドは、プライマリ データベースまたはその他のセカンダリ データベースには影響しません。  
  
    ```  
    Remove-SqlAvailabilityDatabase `  
    -Path SQLSERVER:\Sql\SecondaryComputer\InstanceName\AvailabilityGroups\MyAg\Databases\MyDb8  
    ```  
  
    > [!NOTE]  
    >  コマンドレットの構文を表示するには、 **PowerShell 環境で** Get-Help [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] コマンドレットを使用します。 詳細については、「 [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md)」を参照してください。  
  
 **SQL Server PowerShell プロバイダーを設定して使用するには**  
  
-   [SQL Server PowerShell プロバイダー](../../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
##  <a name="FollowUp"></a> 補足情報:セカンダリ データベースを可用性グループから削除した後  
 セカンダリ データベースを削除すると、可用性グループに参加しなくなり、削除されたセカンダリ データベースに関するすべての情報が可用性グループによって破棄されます。 削除されたセカンダリ データベースは RESTORING 状態になります。  
  
> [!TIP]  
>  セカンダリ データベースを削除してしばらくの間は、そのデータベースを可用性グループに再度参加させて、データベース上で AlwaysOn データ同期を再開できることがあります。 詳細については、「 [可用性グループへのセカンダリ データベースの参加 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-database-to-an-availability-group-sql-server.md)のインスタンスに AlwaysOn 可用性グループを作成する方法について説明します。  
  
 この時点で、削除されたセカンダリ データベースを処理する別の方法は次のとおりです。  
  
-   セカンダリ データベースが不要の場合は、削除できます。  
  
     詳細については、「[DROP DATABASE &#40;Transact-SQL&#41;](../../../t-sql/statements/drop-database-transact-sql.md)」または「[データベースの削除](../../../relational-databases/databases/delete-a-database.md)」を参照してください。  
  
-   可用性グループから削除された後に、削除されたセカンダリ データベースにアクセスする必要がある場合は、データベースを復元できます。 ただし、削除されたセカンダリ データベースを復元すると、異なる 2 つのデータベースが同じ名前でオンラインになります。 クライアントが現在のプライマリ データベースのみにアクセスできるようにする必要があります。  
  
     詳細については、「[データを復元しないデータベースの復旧 &#40;Transact-SQL&#41;](../../../relational-databases/backup-restore/recover-a-database-without-restoring-data-transact-sql.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [AlwaysOn 可用性グループの概要 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [可用性グループからのプライマリ データベースの削除 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remove-a-primary-database-from-an-availability-group-sql-server.md)  
  
  
