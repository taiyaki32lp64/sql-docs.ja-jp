---
title: SQL Server エージェントのマスター ジョブに関連付けられている対象サーバーの変更 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
ms.assetid: 176e73b6-08aa-48ec-b349-e84b431e65cc
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 61173f4b9ef6c8f836b3654bdc5b7366a8a54461
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62654063"
---
# <a name="modify-the-target-servers-associated-with-a-sql-server-agent-master-job"></a>SQL Server エージェントのマスター ジョブに関連付けられているターゲット サーバーの変更
  このトピックでは、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../includes/tsql-md.md)] を使用して、[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で SQL Server エージェントのマスター ジョブに関連付けられているターゲット サーバーを変更する方法について説明します。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [Security](#Security)  
  
-   **以下を使用して SQL Server エージェントのマスター ジョブに関連付けられている対象サーバーを変更するには:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントのマスター ジョブの対象サーバーを、ローカル サーバーとリモート サーバーの両方に設定することはできません。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 **sysadmin** 固定サーバー ロールのメンバー以外は、所有しているジョブしか変更できません。 詳細については、「 [SQL Server エージェントのセキュリティの実装](implement-sql-server-agent-security.md)」をご覧ください。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-modify-the-target-servers-associated-with-a-sql-server-agent-master-job"></a>SQL Server エージェントのマスター ジョブに関連付けられているターゲット サーバーを変更するには  
  
1.  **オブジェクト エクスプローラー** で、対象サーバーを変更するジョブを含むサーバーをプラス記号をクリックして展開します。  
  
2.  プラス記号をクリックして **[SQL Server エージェント]** を展開します。  
  
3.  プラス記号をクリックして **[ジョブ]** フォルダーを展開します。  
  
4.  ターゲット サーバーを変更するジョブを右クリックし、 **[プロパティ]** を選択します。  
  
5.  **[ジョブのプロパティ - <_ジョブ名_>]** ダイアログ ボックスで、 **[ページの選択]** の **[対象サーバー]** を選択します。 このページで使用可能なオプションの詳細については、次を参照してください。[ジョブのプロパティ。新しいジョブ&#40;ページを対象と&#41;](job-properties-new-job-targets-page.md)します。  
  
6.  完了したら、 **[OK]** をクリックします。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-delete-a-target-server-currently-associated-with-a-sql-server-agent-master-job"></a>SQL Server エージェントのマスター ジョブに現在関連付けられているターゲット サーバーを削除するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```  
    -- removes the server SEATTLE2 from processing the Weekly Sales Backupsjob   
    -- assumes that the Weekly Sales Backups job exists  
    USE msdb ;  
    GO  
  
    EXEC sp_delete_jobserver  
        @job_name = N'Weekly Sales Backups',  
        @server_name = N'SEATTLE2' ;  
    GO  
    ```  
  
 詳細については、次を参照してください。 [sp_delete_jobserver &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-delete-jobserver-transact-sql)します。  
  
#### <a name="to-associate-a-target-server-with-the-current-sql-server-agent-master-job"></a>現在の SQL Server エージェントのマスター ジョブにターゲット サーバーを関連付けるには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```  
    -- assigns the multiserver job Weekly Sales Backups to the server SEATTLE2   
    -- assumes that the Weekly Sales Backups job already exists and that   
    -- SEATTLE2 is registered as a target server for the current instance  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_add_jobserver  
        @job_name = N'Weekly Sales Backups',  
        @server_name = N'SEATTLE2' ;  
    GO  
    ```  
  
 詳細については、次を参照してください。 [sp_add_jobserver &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql)します。  
  
  
