---
title: Transact-SQL ジョブ ステップの作成 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- Transact-SQL job step
- job steps [Transact-SQL]
- SQL Server Agent jobs, Transact-SQL step
ms.assetid: 69c571a7-debe-4063-9d38-e4b6a1e8e84c
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 19f830b39b6c981f47106e772980d883b6a6d821
ms.sourcegitcommit: 57e20b7d02853ec9af46b648106578aed133fb45
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/16/2019
ms.locfileid: "69553091"
---
# <a name="create-a-transact-sql-job-step"></a>Create a Transact-SQL Job Step
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL Database Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) では現在、すべてではありませんがほとんどの SQL Server エージェントの機能がサポートされています。 詳細については、「[Azure SQL Database Managed Instance と SQL Server の T-SQL の相違点](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)」を参照してください。

このトピックでは、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、[!INCLUDE[tsql](../../includes/tsql-md.md)]、または SQL Server 管理オブジェクトを使用して、[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で [!INCLUDE[tsql](../../includes/tsql-md.md)] スクリプトを実行する [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブ ステップを作成する方法について説明します。  
  
ここで作成するジョブ ステップ スクリプトは、ストアド プロシージャおよび拡張ストアド プロシージャを呼び出すことができます。 1 つの [!INCLUDE[tsql](../../includes/tsql-md.md)] ジョブ ステップに、複数のバッチおよび埋め込み GO コマンドを含めることができます。 ジョブの作成の詳細については、「 [ジョブの作成](../../ssms/agent/create-jobs.md)」を参照してください。  
  
## <a name="BeforeYouBegin"></a>はじめに  
  
### <a name="Security"></a>セキュリティ  
詳細については、「 [SQL Server エージェントのセキュリティの実装](../../ssms/agent/implement-sql-server-agent-security.md)」をご覧ください。  
  
## <a name="SSMS"></a>SQL Server Management Studio の使用  
  
#### <a name="to-create-a-transact-sql-job-step"></a>Transact-SQL ジョブ テップを作成するには  
  
1.  **オブジェクト エクスプローラー** で、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]のインスタンスに接続し、そのインスタンスを展開します。  
  
2.  **[SQL Server エージェント]** を展開し、新しいジョブを作成するか、既存のジョブを右クリックして **[プロパティ]** をクリックします。  
  
3.  **[ジョブのプロパティ]** ダイアログで **[ステップ]** ページをクリックし、 **[新規作成]** をクリックします。  
  
4.  **[新しいジョブ ステップ]** ダイアログの **[ステップ名]** ボックスにジョブ ステップ名を入力します。  
  
5.  **[種類]** ボックスの **[Transact-SQL スクリプト (T-SQL)]** をクリックします。  
  
6.  **[コマンド]** ボックスに、 [!INCLUDE[tsql](../../includes/tsql-md.md)] コマンド バッチを入力するか、または **[開く]** をクリックしてコマンドとして使用する [!INCLUDE[tsql](../../includes/tsql-md.md)] ファイルを選択します。  
  
7.  **[解析]** をクリックして構文をチェックします。  
  
8.  構文が正しい場合は、成功を示すメッセージが表示されます。 エラーが見つかった場合は、構文を訂正しないと先に進めません。  
  
9. **[詳細設定]** ページをクリックして、ジョブ ステップが成功または失敗した場合の操作、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントによるジョブ ステップ実行の試行回数、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントでジョブ ステップの出力を書き込むファイルまたはテーブルなど、ジョブ ステップのオプションを設定します。 **sysadmin** 固定サーバー ロールのメンバーだけが、オペレーティング システム ファイルにジョブ ステップの出力を書き込むことができます。 SQL Server エージェントのすべてのユーザーがテーブルにログを書き込むことができます。  
  
10. **sysadmin** 固定サーバー ロールのメンバーで、このジョブ ステップを別の SQL ログインで実行する場合は、 **[実行時のユーザー]** ボックスで SQL ログインを選択します。  
  
## <a name="TSQL"></a>Transact-SQL の使用  
  
#### <a name="to-create-a-transact-sql-job-step"></a>Transact-SQL ジョブ テップを作成するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde_md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```  
    -- creates a job step that uses Transact-SQL  
    USE msdb;  
    GO  
    EXEC sp_add_jobstep  
        @job_name = N'Weekly Sales Data Backup',  
        @step_name = N'Set database to read only',  
        @subsystem = N'TSQL',  
        @command = N'ALTER DATABASE SALES SET READ_ONLY',   
        @retry_attempts = 5,  
        @retry_interval = 5 ;  
    GO  
    ```  
  
詳細については、「 [sp_add_jobstep (Transact-SQL)](https://msdn.microsoft.com/97900032-523d-49d6-9865-2734fba1c755)」を参照してください。  
  
## <a name="SMO"></a>SQL Server 管理オブジェクトの使用  
**Transact-SQL ジョブ テップを作成するには**  
  
Visual Basic、Visual C#、PowerShell などの選択したプログラミング言語で **JobStep** クラスを使用します。  
  
