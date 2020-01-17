---
title: 重大度レベルを使用して警告を作成する | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- alerts [SQL Server], creating
- SQL Server Agent, alerts
- severity levels [SQL Server]
- alerts [SQL Server], severity levels
ms.assetid: a1fd71bf-5bf9-4ce2-9a1d-032576a4a6e9
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 696527b77cba555ad5c70a8ee65c8409295d18e4
ms.sourcegitcommit: dc8697bdd950babf419b4f1e93b26bb789d39f4a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70846800"
---
# <a name="create-an-alert-using-severity-level"></a>Create an Alert Using Severity Level
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL Database Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) では現在、すべてではありませんがほとんどの SQL Server エージェントの機能がサポートされています。 詳細については、「[Azure SQL Database Managed Instance と SQL Server の T-SQL の相違点](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)」を参照してください。

このトピックでは、[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../includes/tsql-md.md)] を使用して、特定の重大度レベルのイベントが発生したときに生成される [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントの警告を作成する方法について説明します。  
  
## <a name="BeforeYouBegin"></a>はじめに  
  
### <a name="Restrictions"></a>制限事項と制約事項  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] は、警告システム全体を簡単に管理できるグラフィカルなツールです。警告の基本構成を設定するには、SQL Server Management Studio を使用することをお勧めします。  
  
-   **xp_logevent** で生成されたイベントは master データベースで発生します。 このため、**xp_logevent** では、警告の **\@database_name** が **'master'** または NULL になっていないと、警告はトリガーされません。  
  
-   重大度レベル 19 ～ 25 では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Windows アプリケーション ログに [!INCLUDE[msCoName](../../includes/msconame_md.md)] メッセージが送信され、警告が起動されます。 重大度レベルが 19 未満のイベントでは、 **sp_altermessage**、RAISERROR WITH LOG、 **xp_logevent** のいずれかを使用して Windows アプリケーション ログへの書き込みを強制した場合にのみ、警告が起動されます。  
  
### <a name="Security"></a>セキュリティ  
  
#### <a name="Permissions"></a>アクセス許可  
既定では、 **sp_add_alert** を実行できるのは、 **sysadmin**固定サーバー ロールのメンバーだけです。  
  
## <a name="SSMSProcedure"></a>SQL Server Management Studio の使用  
  
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
  
## <a name="TsqlProcedure"></a>Transact-SQL の使用  
  
#### <a name="to-create-an-alert-using-severity-level"></a>重大度レベルを使用して警告を作成するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde_md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```  
    -- Adds an alert (Test Alert) that notifies the
    -- Alert Operator via email when an error with a 
    -- severity of 23 is detected.
    
    -- Assumes that the Alert Operator already exists 
    -- and that database mail is configured.
    
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_add_alert @name=N'Test Alert', 
      @message_id = 0, 
      @severity = 23, 
      @enabled = 1, 
      @include_event_description_in = 1
    ;
    GO
    
    EXEC dbo.sp_add_notification @alert_name=N'Test Alert',
      @operator_name=N'Alert Operator',
      @notification_method=1
    ;
    GO

    ```  
  
詳細については、「 [sp_add_alert (Transact-SQL)](https://msdn.microsoft.com/d9b41853-e22d-4813-a79f-57efb4511f09)」を参照してください。  
  
