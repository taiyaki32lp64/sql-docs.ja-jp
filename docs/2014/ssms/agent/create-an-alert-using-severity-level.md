---
title: 重大度レベルを使用して警告を作成する | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- alerts [SQL Server], creating
- SQL Server Agent, alerts
- severity levels [SQL Server]
- alerts [SQL Server], severity levels
ms.assetid: a1fd71bf-5bf9-4ce2-9a1d-032576a4a6e9
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8e94b24634eedf68afcb25c8c1ef957ce063cdc4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63136739"
---
# <a name="create-an-alert-using-severity-level"></a>Create an Alert Using Severity Level
  このトピックでは、[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../includes/tsql-md.md)] を使用して、特定の重大度レベルのイベントが発生したときに生成される [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントの警告を作成する方法について説明します。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [Security](#Security)  
  
-   **重大度レベルを使用して警告を作成する方法:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] は、警告システム全体を簡単に管理できるグラフィカルなツールです。警告の基本構成を設定するには、SQL Server Management Studio を使用することをお勧めします。  
  
-   **xp_logevent** で生成されたイベントは master データベースで発生します。 このため、 **xp_logevent** では、警告の **@database_name** が **'master'** または NULL になっていないと、警告が起動されません。  
  
-   重大度レベル 19 ～ 25 では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Windows アプリケーション ログに [!INCLUDE[msCoName](../../includes/msconame-md.md)] メッセージが送信され、警告が起動されます。 重大度レベルが 19 未満のイベントでは、 **sp_altermessage**、RAISERROR WITH LOG、 **xp_logevent** のいずれかを使用して Windows アプリケーション ログへの書き込みを強制した場合にのみ、警告が起動されます。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 既定では、 **sp_add_alert** を実行できるのは、 **sysadmin**固定サーバー ロールのメンバーだけです。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-create-an-alert-using-severity-level"></a>重大度レベルを使用して警告を作成するには  
  
1.  **オブジェクト エクスプローラー** で、プラス記号をクリックして、重大度レベルを使用した警告を作成するサーバーを展開します。  
  
2.  プラス記号をクリックして **[SQL Server エージェント]** を展開します。  
  
3.  **[警告]** を右クリックし、 **[新しい警告]** をクリックします。  
  
4.  **[新しい警告]** ダイアログ ボックスで、 **[名前]** ボックスに新しい警告の名前を入力します。  
  
5.  **[種類]** ボックスの一覧の **[SQL Server イベント警告]** をクリックします。  
  
6.  **[イベント警告定義]** で、 **[データベース名]** ボックスの一覧からデータベースを選択して、警告を特定のデータベースに限定します。  
  
7.  **[警告が発生する条件]** の **[重大度]** をクリックし、警告を発生させる重大度を選択します。  
  
8.  特定の文字列が含まれている場合のみ警告を生成するには、 **[メッセージに次の内容が含まれている場合に警告する]** チェック ボックスをオンにし、 **[メッセージ テキスト]** ボックスにキーワードまたは文字列を入力します。 最大文字数は 100 文字です。  
  
9. **[OK]** をクリックします。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-create-an-alert-using-severity-level"></a>重大度レベルを使用して警告を作成するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```  
    -- adds an alert (Test Alert) that runs the Back up the AdventureWorks2012 Database job when fired   
    -- assumes that the message 55001 and the Back up the AdventureWorks2012 Database job already exist.  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_add_alert  
        @name = N'Test Alert',  
        @message_id = 55001,   
       @severity = 0,   
       @notification_message = N'Error 55001 has occurred. The database will be backed up...',   
       @job_name = N'Back up the AdventureWorks2012 Database' ;  
    GO  
    ```  
  
 詳細については、次を参照してください。 [sp_add_alert &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-add-alert-transact-sql)します。  
  
  
