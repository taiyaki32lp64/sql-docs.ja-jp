---
title: ジョブ ステップのログの削除 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- job steps [SQL Server Agent]
- deleting job step logs
- logs [SQL Server], jobs
- removing job step logs
ms.assetid: ee20c6cd-0258-4550-bdb0-71e86a0fb330
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cd6cefd41ea223b91445042ff3cee9090074feeb
ms.sourcegitcommit: a165052c789a327a3a7202872669ce039bd9e495
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72783193"
---
# <a name="delete-a-job-step-log"></a>Delete a Job Step Log
  このトピックでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントのジョブ ステップのログを削除する方法について説明します。  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [Security](#Security)  
  
-   **SQL Server エージェントのジョブ ステップのログを削除する方法:**  
  
     [SQL Server Management Studio](#SSMS)  
  
     [Transact-SQL](#TSQL)  
  
     [SQL Server 管理オブジェクト](#SMO)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
 ジョブ ステップが削除されるときに、そのジョブ ステップの出力ログは自動的に削除されます。  
  
###  <a name="Security"></a> Security  
  
####  <a name="Permissions"></a> アクセス許可  
 **sysadmin** 固定サーバー ロールのメンバー以外は、所有しているジョブしか変更できません。  
  
##  <a name="SSMS"></a> SQL Server Management Studio の使用  
  
#### <a name="to-delete-a-sql-server-agent-job-step-log"></a>SQL Server エージェントのジョブ ステップのログを削除するには  
  
1.  **オブジェクト エクスプローラー** で、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]のインスタンスに接続し、そのインスタンスを展開します。  
  
2.  **[SQL Server エージェント]** 、 **[ジョブ]** の順に展開し、変更するジョブを右クリックします。次に、 **[プロパティ]** をクリックします。  
  
3.  **[ジョブのプロパティ]** ダイアログ ボックスで、選択したジョブ ステップを削除します。  
  
##  <a name="TSQL"></a> Transact-SQL の使用  
  
#### <a name="to-delete-a-sql-server-agent-job-step-log"></a>SQL Server エージェントのジョブ ステップのログを削除するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```sql
    -- removes the job step log for step 2 in the job Weekly Sales Data Backup  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_delete_jobsteplog  
        @job_name = N'Weekly Sales Data Backup',  
        @step_id = 2;  
    GO  
    ```  
  
 詳細については、「 [sp_delete_jobsteplog &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-delete-jobsteplog-transact-sql)」を参照してください。  
  
##  <a name="SMO"></a>SQL Server 管理オブジェクトの使用  
 Visual Basic、Visual C#、PowerShell などのプログラミング言語で `DeleteJobStepLogs` クラスの `Job` メソッドを使用します。 詳細については、「[SQL Server 管理オブジェクト (SMO) プログラミング ガイド](https://msdn.microsoft.com/library/ms162169.aspx)」を参照してください。  
  
```powershell
# Delete all job step log files that have ID values larger than 5.  
$srv = New-Object Microsoft.SqlServer.Management.Smo.Server("(local)")  
$jb = $srv.JobServer.Jobs["Test Job"]  
$jb.DeleteJobStepLogs(5)  
```
