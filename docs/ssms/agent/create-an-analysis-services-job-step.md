---
title: Analysis Services ジョブ ステップの作成 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- job steps [Analysis Services]
ms.assetid: 03d4bb86-514b-4a55-97b9-c2c0fa08b428
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: e27f429820039b7d804f52776e9cf5dd33bf27dd
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68267279"
---
# <a name="create-an-analysis-services-job-step"></a>Create an Analysis Services Job Step

[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL Database Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) では現在、すべてではありませんがほとんどの SQL Server エージェントの機能がサポートされています。 詳細については、「[Azure SQL Database Managed Instance と SQL Server の T-SQL の相違点](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)」を参照してください。

このトピックでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 、または SQL Server 管理オブジェクトを使用して、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]Analysis Services のコマンドとクエリを実行する [!INCLUDE[tsql](../../includes/tsql-md.md)] エージェント ジョブ ステップの作成と定義方法について説明します。  
  
-   **作業を開始する準備:**  
  
    [制限事項と制約事項](#Restrictions)  
  
    [セキュリティ](#Security)  
  
-   **Analysis Services コマンドまたはクエリを使用する SQL Server ジョブ ステップを作成する方法:**  
  
    [SQL Server Management Studio](#SSMS)  
  
    [Transact-SQL](#TSQL)  
  
    [SQL Server 管理オブジェクト](#SMO)  
  
## <a name="BeforeYouBegin"></a>はじめに  
  
### <a name="Restrictions"></a>制限事項と制約事項  
  
-   ジョブ ステップで Analysis Services コマンドを使用する場合、コマンド ステートメントは XML for Analysis Services の **Execute** メソッドである必要があります。 ステートメントには、完全な SOAP (Simple Object Access Protocol) エンベロープまたは XML for Analysis の **Discover** メソッドを含めることはできません。 完全な SOAP エンベロープと [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] Discover **メソッドは、** ではサポートされていますが、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブ ステップではサポートされていません。 XML for Analysis Services の詳細については、「 [XML for Analysis の概要 (XMLA)](https://msdn.microsoft.com/library/ms187190.aspx)」を参照してください。  
  
-   ジョブ ステップで Analysis Services クエリを使用する場合、クエリ ステートメントは多次元式 (MDX) クエリである必要があります。 MDX の詳細については、「 [MDX ステートメントの基礎 (MDX)](https://msdn.microsoft.com/a560383b-bb58-472e-95f5-65d03d8ea08b)」を参照してください。  
  
### <a name="Security"></a>セキュリティ  
  
#### <a name="Permissions"></a>アクセス許可  
  
-   Analysis Services サブシステムを使用するジョブ ステップを実行できるのは、 **sysadmin** 固定サーバー ロールのメンバーであるか、このサブシステム用に定義された有効なプロキシ アカウントへアクセスできるユーザーだけです。 さらに、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービス アカウントまたはプロキシは、Analysis Services 管理者であり、かつ有効な Windows ドメイン アカウントである必要があります。  
  
-   **sysadmin** 固定サーバー ロールのメンバーのみがジョブ ステップ出力をファイルに書き込むことができます。 **msdb** データベースで **SQLAgentUserRole** データベース ロールのメンバーであるユーザーによってジョブ ステップが実行される場合、出力はテーブルのみに書き込むことができます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントによって **SQLAgentUserRole** データベースの **SQLAgentUserRole** テーブルに書き込まれます。  
  
-   詳細については、「 [SQL Server エージェントのセキュリティの実装](../../ssms/agent/implement-sql-server-agent-security.md)」をご覧ください。  
  
## <a name="SSMS"></a>SQL Server Management Studio の使用  
  
#### <a name="to-create-an-analysis-services-command-job-step"></a>Analysis Services コマンド ジョブ ステップを作成するには  
  
1.  **オブジェクト エクスプローラー** で、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]のインスタンスに接続し、そのインスタンスを展開します。  
  
2.  **[SQL Server エージェント]** を展開し、新しいジョブを作成するか、既存のジョブを右クリックして **[プロパティ]** をクリックします。 ジョブの作成の詳細については、「 [ジョブの作成](../../ssms/agent/create-jobs.md)」を参照してください。  
  
3.  **[ジョブのプロパティ]** ダイアログ ボックスで **[ステップ]** タブをクリックし、 **[新規作成]** をクリックします。  
  
4.  **[新しいジョブ ステップ]** ダイアログ ボックスで、ジョブの **[ステップ名]** を入力します。  
  
5.  **[種類]** ボックスの一覧で、 **[SQL Server Analysis Services コマンド]** をクリックします。  
  
6.  **[実行するアカウント名]** ボックスの一覧で、その Analysis Services コマンド サブシステムを使用するように定義済みのプロキシを選択します。 ユーザーが **sysadmin** 固定サーバー ロールのメンバーである場合は、 **[SQL エージェント サービスのアカウント]** を使用してこのジョブ ステップを実行することもできます。  
  
7.  **[サーバー]** でジョブ ステップを実行するサーバーを選択するか、サーバー名を入力します。  
  
8.  実行するステートメントを **[コマンド]** ボックスに入力します。または、 **[開く]** をクリックしてステートメントを選択します。  
  
9. **[詳細設定]** ページをクリックして、ジョブ ステップが成功または失敗した場合に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントが実行するアクション、ジョブ ステップの試行回数、ジョブ ステップ出力の出力先など、このジョブ ステップに関するさまざまなオプションを定義します。  
  
#### <a name="to-create-an-analysis-services-query-job-step"></a>Analysis Services クエリ ジョブ ステップを作成するには  
  
1.  **オブジェクト エクスプローラー** で、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]のインスタンスに接続し、そのインスタンスを展開します。  
  
2.  **[SQL Server エージェント]** を展開し、新しいジョブを作成するか、既存のジョブを右クリックして **[プロパティ]** をクリックします。 ジョブの作成の詳細については、「 [ジョブの作成](../../ssms/agent/create-jobs.md)」を参照してください。  
  
3.  **[ジョブのプロパティ]** ダイアログで **[ステップ]** ページをクリックし、 **[新規作成]** をクリックします。  
  
4.  **[新しいジョブ ステップ]** ダイアログの **[ステップ名]** ボックスにジョブ ステップ名を入力します。  
  
5.  **[種類]** ボックスの一覧で、 **[SQL Server Analysis Services クエリ]** をクリックします。  
  
6.  **[実行するアカウント名]** ボックスの一覧で、その Analysis Services クエリ サブシステムを使用するように定義済みのプロキシを選択します。 ユーザーが **sysadmin** 固定サーバー ロールのメンバーである場合は、 **[SQL エージェント サービスのアカウント]** を使用してこのジョブ ステップを実行することもできます。  
  
7.  **[サーバー]** および **[データベース]** で、ジョブ ステップを実行するサーバーとデータベースを選択するか、サーバー名またはデータベース名を直接入力します。  
  
8.  実行するステートメントを **[コマンド]** ボックスに入力します。または、 **[開く]** をクリックしてステートメントを選択します。  
  
9. **[詳細設定]** ページをクリックして、ジョブ ステップが成功または失敗した場合に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントが実行するアクション、ジョブ ステップの試行回数、ジョブ ステップ出力の出力先など、このジョブ ステップに関するさまざまなオプションを定義します。  
  
## <a name="TSQL"></a>Transact-SQL の使用  
  
#### <a name="to-create-an-analysis-services-command-job-step"></a>Analysis Services コマンド ジョブ ステップを作成するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde_md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```  
    -- Creates a job step that uses XMLA to create a relational data source that
    -- references the AdventureWorks2012 Microsoft SQL Server database.  
    USE msdb;  
    GO  
    EXEC sp_add_jobstep  
        @job_name = N'Weekly Sales Data Backup',  
        @step_name =
            N'Create a relational data source that references the AdventureWorks2012 Microsoft SQL Server database',  
        @subsystem = N'ANALYSISCOMMAND',  
        @command =
            N' <Create xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">  
        <ParentObject>  
            <DatabaseID>AdventureWorks2012</DatabaseID>  
        </ParentObject>  
        <ObjectDefinition>  
            <DataSource xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
                xsi:type="RelationalDataSource">  
                <ID>AdventureWorks2012</ID>  
                <Name>Adventure Works 2012</Name>  
                <ConnectionString>Data Source=localhost;Initial Catalog=AdventureWorks2012;Integrated Security=True</ConnectionString>  
                <ImpersonationInfo>  
                    <ImpersonationMode>ImpersonateServiceAccount</ImpersonationMode>  
                </ImpersonationInfo>  
                <ManagedProvider>System.Data.SqlClient</ManagedProvider>  
                <Timeout>PT0S</Timeout>  
            </DataSource>  
        </ObjectDefinition>  
    </Create>', ;  
    GO  
    ```  
  
詳細については、「 [sp_add_jobstep (Transact-SQL)](https://msdn.microsoft.com/97900032-523d-49d6-9865-2734fba1c755)」を参照してください。  
  
#### <a name="to-create-an-analysis-services-query-job-step"></a>Analysis Services クエリ ジョブ ステップを作成するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde_md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```  
    -- Creates a job step that uses MDX to return data  
    USE msdb;  
    GO  
    EXEC sp_add_jobstep  
        @job_name = N'Weekly Sales Data Backup',  
        @step_name = N'Returns the Internet sales amount by state',  
        @subsystem = N'ANALYSISQUERY',  
        @command = N' SELECT  
       [Measures].[Internet Sales Amount] ON COLUMNS,  
       [Customer].[State-Province].Members ON ROWS  
    FROM [AdventureWorks2012]',   
        @retry_attempts = 5,  
        @retry_interval = 5 ;  
    GO  
    ```  
  
詳細については、「 [sp_add_jobstep (Transact-SQL)](https://msdn.microsoft.com/97900032-523d-49d6-9865-2734fba1c755)」を参照してください。  
  
## <a name="SMO"></a>SQL Server 管理オブジェクトの使用  
**PowerShell スクリプト ジョブ ステップを作成するには**  
  
XMLA や MDX などのプログラミング言語で、 **JobStep** クラスを使用します。 詳細については、「 [SQL Server 管理オブジェクト (SMO) プログラミング ガイド](https://msdn.microsoft.com/library/ms162169.aspx)」を参照してください。  
  
