---
title: SQL Server エージェントのマスター ジョブの作成 | Microsoft Docs
ms.custom: ''
ms.date: 04/26/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], master jobs
- jobs [SQL Server Agent], creating
- master SQL Server Agent job [SQL Server]
ms.assetid: c12ab23f-d7ee-43a5-8cd2-0a9121292bcd
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e80d5790f78c83a8a1ff3059e12e0946e206c060
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68211455"
---
# <a name="create-a-sql-server-agent-master-job"></a>SQL Server エージェントのマスター ジョブの作成
  このトピックでは、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../includes/tsql-md.md)] を使用して、[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントのマスター ジョブを作成する方法について説明します。  
  
 
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントのマスター ジョブの変更は、関係するすべての対象サーバーに伝達する必要があります。 これらのターゲットが指定されるまでターゲット サーバーはジョブをダウンロードしないので、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] では、ターゲット サーバーを指定する前に、特定のジョブのすべてのジョブ ステップとジョブ スケジュールを完了しておくことをお勧めしています。 この順序に従わなかった場合は、 **sp_post_msx_operation** ストアド プロシージャを実行するか、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]を使用してジョブを変更することによって、変更されたジョブをターゲット サーバーが再びダウンロードするように手動で要求する必要があります。 詳細については、次を参照してください。 [sp_post_msx_operation &#40;TRANSACT-SQL&#41; ](/sql/relational-databases/system-stored-procedures/sp-post-msx-operation-transact-sql)または[ジョブの変更](modify-a-job.md)します。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 プロキシに関連付けられているステップがある分散ジョブは、ターゲット サーバーのプロキシ アカウントのコンテキストで実行されます。 次の条件を満たしていることを確認してください。満たしていないと、プロキシに関連付けられているジョブ ステップがマスター サーバーから対象サーバーにダウンロードされません。  
  
-   レジストリ サブキー **\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\\<*instance_name*> \SQL Server Agent\AllowDownloadedJobsToMatchProxyName**(REG_DWORD) が 1 (true) に設定します。 既定では、この値は 0 (false) に設定されます。  
  
-   ジョブ ステップを実行するマスター サーバー プロキシ アカウントと同じ名前を持つターゲット サーバーにプロキシ アカウントが存在すること。  
  
 マスター サーバーからターゲット サーバーにプロキシ アカウントをダウンロード中に、これらのアカウントを使用するジョブ ステップが失敗した場合は、**msdb** データベースの **sysdownloadlist** テーブルの **error_message** 列を参照して、以下のエラー メッセージの有無を確認します。  
  
-   "ジョブ ステップではプロキシ アカウントが必要ですが、ターゲット サーバーで一致するプロキシが無効です。" このエラーを解決するには、 **AllowDownloadedJobsToMatchProxyName** レジストリ サブキーを 1 に設定します。  
  
-   "プロキシ アカウントが見つかりませんでした。" このエラーを解決するには、ターゲット サーバー上にプロキシ アカウントが存在し、ジョブ ステップを実行するマスター サーバー プロキシ アカウントと同じ名前が付けられているかどうかを確認します。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-create-a-master-sql-server-agent-job"></a>SQL Server エージェントのマスター ジョブを作成するには  
  
1.  **オブジェクト エクスプローラー**で、SQL Server エージェント ジョブを作成するサーバーをプラス記号をクリックして展開します。  
  
2.  プラス記号をクリックして **[SQL Server エージェント]** を展開します。  
  
3.  **[ジョブ]** フォルダーを右クリックし、 **[新しいジョブ]** を選択します。  
  
4.  **[新しいジョブ]** ダイアログ ボックスの **[全般]** ページで、ジョブの全般的なプロパティを変更します。 このページで使用可能なオプションの詳細については、次を参照してください[ジョブのプロパティと新しいジョブ&#40;[全般] ページ。&#41;](../../integration-services/general-page-of-integration-services-designers-options.md)  
  
5.  **[ステップ]** ページで、ジョブ ステップを編成します。 このページで使用可能なオプションの詳細については、次を参照してください[ジョブのプロパティ: 新しいジョブ&#40;[ステップ] ページ。&#41;](job-properties-new-job-steps-page.md)  
  
6.  **[スケジュール** ] ページで、ジョブのスケジュールを編成します。 このページで使用可能なオプションの詳細については、次を参照してください。[ジョブのプロパティ。新しいジョブ&#40;[スケジュール] ページ&#41;](job-properties-new-job-schedules-page.md)  
  
7.  **[警告]** ページで、ジョブの警告を編成します。 このページで使用可能なオプションの詳細については、次を参照してください。[ジョブのプロパティ。新しいジョブ&#40;警告 ページ&#41;](job-properties-new-job-alerts-page.md)  
  
8.  **[通知]** ページで、ジョブの完了時に [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントが実行するアクションを設定します。 このページで使用可能なオプションの詳細については、次を参照してください。[ジョブのプロパティ。新しいジョブ&#40;通知ページ&#41;](job-properties-new-job-notifications-page.md)します。  
  
9. **[ターゲット]** ページで、ジョブの対象サーバーを管理します。 このページで使用可能なオプションの詳細については、次を参照してください。[ジョブのプロパティ。新しいジョブ&#40;ページを対象と&#41;](job-properties-new-job-targets-page.md)します。  
  
10. 完了したら、 **[OK]** をクリックします。  
  

  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-create-a-master-sql-server-agent-job"></a>SQL Server エージェントのマスター ジョブを作成するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```  
    USE msdb ;  
    GO  
    -- Adds a new job executed by the SQLServerAgent service called 'Weekly Sales Data Backup'  
    EXEC dbo.sp_add_job  
        @job_name = N'Weekly Sales Data Backup' ;  
    GO  
    -- Adds a step (operation) to the 'Weekly Sales Data Backup' job.  
    EXEC sp_add_jobstep  
        @job_name = N'Weekly Sales Data Backup',  
        @step_name = N'Set database to read only',  
        @subsystem = N'TSQL',  
        @command = N'ALTER DATABASE SALES SET READ_ONLY',   
        @retry_attempts = 5,  
        @retry_interval = 5 ;  
    GO  
    -- Creates a schedule called RunOnce  
    EXEC dbo.sp_add_schedule  
        @schedule_name = N'RunOnce',  
        @freq_type = 1,  
        @active_start_time = 233000 ;  
    USE msdb ;  
    GO  
    -- Sets the 'RunOnce' schedule to the "Weekly Sales Data Backup' Job  
    EXEC sp_attach_schedule  
       @job_name = N'Weekly Sales Data Backup',  
       @schedule_name = N'RunOnce';  
    GO  
    -- assigns the multiserver job Weekly Sales Backups to the server SEATTLE2  
    -- assumes that SEATTLE2 is registered as a target server for the current instance.  
    EXEC dbo.sp_add_jobserver  
        @job_name = N'Weekly Sales Data Backups',  
        @server_name = N'SEATTLE2' ;  
    GO  
    ```  
  
 詳細については、以下をご覧ください。  
  
-   [sp_add_job &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-add-job-transact-sql)  
  
-   [sp_add_jobstep &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql)  
  
-   [sp_add_schedule &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-add-schedule-transact-sql)  
  
-   [sp_attach_schedule &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql)  
  
-   [sp_add_jobserver &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql)  
  

  
  
