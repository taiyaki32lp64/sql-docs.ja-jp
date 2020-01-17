---
title: CmdExec ジョブ ステップの作成 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- CmdExec jobs
ms.assetid: b48da5b4-6fe7-4eb7-bade-dc7d697c6d5c
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 0767ce109e6278f4fa4852f650ac347a562958a0
ms.sourcegitcommit: 57e20b7d02853ec9af46b648106578aed133fb45
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/16/2019
ms.locfileid: "69553170"
---
# <a name="create-a-cmdexec-job-step"></a>CmdExec ジョブ ステップの作成
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL Database Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) では現在、すべてではありませんがほとんどの SQL Server エージェントの機能がサポートされています。 詳細については、「[Azure SQL Database Managed Instance と SQL Server の T-SQL の相違点](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)」を参照してください。

このトピックでは、 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 、または SQL Server 管理オブジェクトを使用して、実行可能なプログラムまたはオペレーティング システム コマンドを使用する [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)] エージェント ジョブ ステップを作成および定義する方法について説明します。  
  
## <a name="BeforeYouBegin"></a>はじめに  
  
### <a name="Security"></a>セキュリティ  
既定では、 **sysadmin** 固定サーバー ロールのメンバーだけが CmdExec ジョブ ステップを作成できます。 これらのジョブ ステップは、 **sysadmin** ユーザーがプロキシ アカウントを作成しない限り、SQL Server エージェント サービス アカウントのコンテキストで実行されます。 **sysadmin** ロールのメンバーではないユーザーでも、CmdExec プロキシ アカウントにアクセスできる場合は CmdExec ジョブ ステップを作成できます。  
  
#### <a name="Permissions"></a>アクセス許可  
詳細については、「 [SQL Server エージェントのセキュリティの実装](../../ssms/agent/implement-sql-server-agent-security.md)」をご覧ください。  
  
## <a name="SSMS"></a>SQL Server Management Studio の使用  
  
#### <a name="to-create-a-cmdexec-job-step"></a>CmdExec ジョブ ステップを作成するには  
  
1.  **オブジェクト エクスプローラー** で、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]のインスタンスに接続し、そのインスタンスを展開します。  
  
2.  **[SQL Server エージェント]** を展開し、新しいジョブを作成するか、既存のジョブを右クリックして **[プロパティ]** をクリックします。  
  
3.  **[ジョブのプロパティ]** ダイアログで **[ステップ]** ページをクリックし、 **[新規作成]** をクリックします。  
  
4.  **[新しいジョブ ステップ]** ダイアログの **[ステップ名]** ボックスにジョブ ステップ名を入力します。  
  
5.  **[種類]** ボックスの一覧の **[オペレーティング システム (CmdExec)]** をクリックします。  
  
6.  **[実行するアカウント名]** ボックスの一覧で、ジョブで使用する資格情報を備えたプロキシ アカウントをクリックします。 既定では、CmdExec ジョブ ステップは SQL Server エージェント サービス アカウントのコンテキストで実行されます。  
  
7.  **[コマンド成功時のプロセス終了コード]** ボックスに、0 ～ 999999 の値を入力します。  
  
8.  **[コマンド]** ボックスに、オペレーティング システム コマンドまたは実行可能プログラムを入力します。 例については、「Transact T-SQL の使用」を参照してください。  
  
9. **[詳細設定]** ページをクリックして、ジョブが成功または失敗した場合の操作、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントによるジョブ ステップ実行の試行回数、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントでジョブ ステップの出力を書き込むファイルなど、ジョブ ステップのオプションを設定します。 **sysadmin** 固定サーバー ロールのメンバーだけが、オペレーティング システム ファイルにジョブ ステップの出力を書き込むことができます。  
  
## <a name="TSQL"></a>Transact-SQL の使用  
  
#### <a name="to-create-a-cmdexec-job-step"></a>CmdExec ジョブ ステップを作成するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde_md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```  
    -- creates a job step that uses CmdExec  
    USE msdb;  
    GO  
    EXEC sp_add_jobstep  
        @job_name = N'Weekly Sales Data Backup',  
        @step_name = N'Set database to read only',  
        @subsystem = N'CMDEXEC',  
        @command = 'C:\clickme_scripts\SQL11\PostBOLReorg GetHsX.exe',   
        @retry_attempts = 5,  
        @retry_interval = 5 ;  
    GO  
    ```  
  
詳細については、「 [sp_add_jobstep (Transact-SQL)](https://msdn.microsoft.com/97900032-523d-49d6-9865-2734fba1c755)」を参照してください。  
  
## <a name="SMO"></a>SQL Server 管理オブジェクトの使用  
**CmdExec ジョブ ステップを作成するには**  
  
Visual Basic、Visual C#、PowerShell などの選択したプログラミング言語で **JobStep** クラスを使用します。  
  
