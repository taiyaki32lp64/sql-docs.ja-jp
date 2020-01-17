---
title: WMI イベント警告の作成 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- WMI event alerts [SQL Server Management Studio]
ms.assetid: b8c46db6-408b-484e-98f0-a8af3e7ec763
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: f1f092ba4facfe166c8be67a21e6f20d414466e5
ms.sourcegitcommit: cbbb210c0315f9e2be2b9cd68db888ac53429814
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/21/2019
ms.locfileid: "69890929"
---
# <a name="create-a-wmi-event-alert"></a>Create a WMI Event Alert
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL Database Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) では現在、すべてではありませんがほとんどの SQL Server エージェントの機能がサポートされています。 詳細については、「[Azure SQL Database Managed Instance と SQL Server の T-SQL の相違点](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)」を参照してください。

このトピックでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] を使用して、WMI Provider for Server Events によって監視されている特定の [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] イベントが発生したときに通知される [!INCLUDE[tsql](../../includes/tsql-md.md)]エージェントの警告を作成する方法について説明します。  
  
WMI Provider を使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] イベントを監視する方法の詳細については、「 [WMI Provider for Server Events のクラスとプロパティ](../../relational-databases/wmi-provider-server-events/wmi-provider-for-server-events-concepts.md)」を参照してください。 WMI イベント警告の通知を受信するために必要な権限の詳細については、「 [SQL Server エージェント サービスのアカウントの選択](../../ssms/agent/select-an-account-for-the-sql-server-agent-service.md)」を参照してください。 WQL の詳細については、「 [WMI Provider for Server Events と WQL の使用](../../relational-databases/wmi-provider-server-events/using-wql-with-the-wmi-provider-for-server-events.md)」を参照してください。  
## <a name="BeforeYouBegin"></a>はじめに  
  
### <a name="Restrictions"></a>制限事項と制約事項  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] は、警告システム全体を簡単に管理できるグラフィカルなツールです。警告の基本構成を設定するには、SQL Server Management Studio を使用することをお勧めします。  
  
-   **xp_logevent** で生成されたイベントは master データベースで発生します。 このため、**xp_logevent** では、警告の **\@database_name** が **'master'** または NULL になっていないと、警告はトリガーされません。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントが実行されているコンピューター上の WMI 名前空間だけがサポートされます。  
  
### <a name="Security"></a>セキュリティ  
  
#### <a name="Permissions"></a>アクセス許可  
既定では、 **sp_add_alert** を実行できるのは、 **sysadmin**固定サーバー ロールのメンバーだけです。  
  
## <a name="SSMSProcedure"></a>SQL Server Management Studio の使用  
  
#### <a name="to-create-a-wmi-event-alert"></a>WMI イベント警告を作成するには  
  
1.  **オブジェクト エクスプローラー** で、プラス記号をクリックして、WMI イベントの警告を作成するサーバーを展開します。  
  
2.  プラス記号をクリックして **[SQL Server エージェント]** を展開します。  
  
3.  **[警告]** を右クリックし、 **[新しい警告]** をクリックします。  
  
4.  **[新しい警告]** ダイアログ ボックスで、 **[名前]** ボックスに新しい警告の名前を入力します。  
  
5.  **[有効化]** チェック ボックスをオンにして、実行する警告を有効にします。 既定では、 **[有効化]** チェック ボックスはオンになっています。  
  
6.  **[種類]** ボックスの一覧の **[WMI イベント警告]** をクリックします。  
  
7.  **[WMI イベント警告定義]** の **[名前空間]** ボックスで、この警告を発生させる WMI イベントを識別する WQL (WMI Query Language) ステートメントの WMI 名前空間を指定します。  
  
8.  **[クエリ]** ボックスで、警告が応答するイベントを識別する WQL ステートメントを指定します。  
  
9. **[OK]** をクリックします。  
  
## <a name="TsqlProcedure"></a>Transact-SQL の使用  
  
#### <a name="to-create-a-wmi-event-alert"></a>WMI イベント警告を作成するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde_md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```  
    -- creates a WMI event alert that retrieves all event properties for any ALTER_TABLE event that occurs on table AdventureWorks2012.Sales.SalesOrderDetail  
    -- This example assumes that the message 54001 already exists.  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_add_alert  
        @name = N'Test Alert 2',  
        @message_id = 54001  
        @notification_message = N'Error 54001 has occurred on the Sales.SalesOrderDetail table on the AdventureWorks2012 database.',  
        @wmi_namespace = '\\.\root\Microsoft\SqlServer\ServerEvents\,  
        @wmi_query = N'SELECT * FROM ALTER_TABLE   
    WHERE DatabaseName = 'AdventureWorks2012' AND SchemaName = 'Sales'   
        AND ObjectType='Table' AND ObjectName = 'SalesOrderDetail'';  
    GO  
    ```  
  
詳細については、「 [sp_add_alert (Transact-SQL)](https://msdn.microsoft.com/d9b41853-e22d-4813-a79f-57efb4511f09)」を参照してください。  
  
