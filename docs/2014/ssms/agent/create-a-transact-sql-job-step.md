---
title: Transact-SQL ジョブ ステップの作成 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- Transact-SQL job step
- job steps [Transact-SQL]
- SQL Server Agent jobs, Transact-SQL step
ms.assetid: 69c571a7-debe-4063-9d38-e4b6a1e8e84c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 488e07e86ba5a7febcb0675611136a1e0d792007
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/23/2019
ms.locfileid: "72798261"
---
# <a name="create-a-transact-sql-job-step"></a>Create a Transact-SQL Job Step
  このトピックでは、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、[!INCLUDE[tsql](../../includes/tsql-md.md)]、または SQL Server 管理オブジェクトを使用して、[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で [!INCLUDE[tsql](../../includes/tsql-md.md)] スクリプトを実行する [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブ ステップを作成する方法について説明します。  
  
 ここで作成するジョブ ステップ スクリプトは、ストアド プロシージャおよび拡張ストアド プロシージャを呼び出すことができます。 1 つの [!INCLUDE[tsql](../../includes/tsql-md.md)] ジョブ ステップに、複数のバッチおよび埋め込み GO コマンドを含めることができます。 ジョブの作成の詳細については、「 [ジョブの作成](create-jobs.md)」を参照してください。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [Security](#Security)  
  
-   **Transact-SQL ジョブ ステップを作成する方法:**  
  
     [SQL Server Management Studio](#SSMS)  
  
     [Transact-SQL](#TSQL)  
  
     [SQL Server 管理オブジェクト](#SMO)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Security"></a> Security  
 詳細については、「 [SQL Server エージェントのセキュリティの実装](implement-sql-server-agent-security.md)」をご覧ください。  
  
##  <a name="SSMS"></a> SQL Server Management Studio の使用  
  
#### <a name="to-create-a-transact-sql-job-step"></a>Transact-SQL ジョブ テップを作成するには  
  
1.  **オブジェクト エクスプローラー** で、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]のインスタンスに接続し、そのインスタンスを展開します。  
  
2.  **[SQL Server エージェント]** を展開し、新しいジョブを作成するか、既存のジョブを右クリックして **[プロパティ]** をクリックします。  
  
3.  **[ジョブのプロパティ]** ダイアログで **[ステップ]** ページをクリックし、 **[新規作成]** をクリックします。  
  
4.  **[新しいジョブ ステップ]** ダイアログの **[ステップ名]** ボックスにジョブ ステップ名を入力します。  
  
5.  **[種類]** ボックスの **[Transact-SQL スクリプト (T-SQL)]** をクリックします。  
  
6.  **[コマンド]** ボックスに、 [!INCLUDE[tsql](../../includes/tsql-md.md)] コマンド バッチを入力するか、または **[開く]** をクリックしてコマンドとして使用する [!INCLUDE[tsql](../../includes/tsql-md.md)] ファイルを選択します。  
  
7.  **[解析]** をクリックして構文をチェックします。  
  
8.  構文が正しい場合は、成功を示すメッセージが表示されます。 エラーが見つかった場合は、構文を訂正しないと先に進めません。  
  
9. **[詳細設定]** ページをクリックして、ジョブ ステップが成功または失敗した場合の操作、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントによるジョブ ステップ実行の試行回数、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントでジョブ ステップの出力を書き込むファイルまたはテーブルなど、ジョブ ステップのオプションを設定します。 **sysadmin** 固定サーバー ロールのメンバーだけが、オペレーティング システム ファイルにジョブ ステップの出力を書き込むことができます。 SQL Server エージェントのすべてのユーザーがテーブルにログを書き込むことができます。  
  
10. **sysadmin** 固定サーバー ロールのメンバーで、このジョブ ステップを別の SQL ログインで実行する場合は、 **[実行時のユーザー]** ボックスで SQL ログインを選択します。  
  
##  <a name="TSQL"></a> Transact-SQL の使用  
  
#### <a name="to-create-a-transact-sql-job-step"></a>Transact-SQL ジョブ テップを作成するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、**[実行]** をクリックします。  
  
    ```sql
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
  
 詳細については、「 [sp_add_jobstep &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql)」を参照してください。  
  
##  <a name="SMO"></a>SQL Server 管理オブジェクトの使用  
 **Transact-SQL ジョブ テップを作成するには**  
  
 Visual Basic、ビジュアルC#、PowerShell などのプログラミング言語で `JobStep` クラスを使用します。  
