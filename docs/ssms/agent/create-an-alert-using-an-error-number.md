---
title: エラー番号を使用して警告を作成する | Microsoft Docs
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
- alerts [SQL Server], error numbers
ms.assetid: 03dd7fac-5073-4f86-babd-37e45a86023c
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: d1a701712ef879e17aaf2a91ff8d81b6c91e8b96
ms.sourcegitcommit: dc8697bdd950babf419b4f1e93b26bb789d39f4a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70846809"
---
# <a name="create-an-alert-using-an-error-number"></a>エラー番号を使用して警告を作成する
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL Database Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) では現在、すべてではありませんがほとんどの SQL Server エージェントの機能がサポートされています。 詳細については、「[Azure SQL Database Managed Instance と SQL Server の T-SQL の相違点](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)」を参照してください。

このトピックでは、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../includes/tsql-md.md)] を使用して、特定の番号のエラーが発生したときに [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で発生する [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント警告の作成方法について説明します。  
  
## <a name="BeforeYouBegin"></a>はじめに  
  
### <a name="Restrictions"></a>制限事項と制約事項  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] は、警告システム全体を簡単に管理できるグラフィカルなツールです。警告の基本構成を設定するには、SQL Server Management Studio を使用することをお勧めします。  
  
-   **xp_logevent** で生成されたイベントは master データベースで発生します。 このため、**xp_logevent** では、警告の **\@database_name** が **'master'** または NULL になっていないと、警告はトリガーされません。  
  
### <a name="Security"></a>セキュリティ  
  
#### <a name="Permissions"></a>アクセス許可  
既定では、 **sp_add_alert** を実行できるのは、 **sysadmin**固定サーバー ロールのメンバーだけです。  
  
## <a name="SSMSProcedure"></a>SQL Server Management Studio の使用  
  
#### <a name="to-create-an-alert-using-an-error-number"></a>エラー番号を使用して警告を作成するには  
  
1.  **オブジェクト エクスプローラー** で、プラス記号をクリックして、エラー番号を使用する警告を作成するサーバーを展開します。  
  
2.  プラス記号をクリックして **[SQL Server エージェント]** を展開します。  
  
3.  **[警告]** を右クリックし、 **[新しい警告]** をクリックします。  
  
4.  **[新しい警告]** ダイアログ ボックスで、 **[名前]** ボックスに新しい警告の名前を入力します。  
  
5.  **[有効化]** チェック ボックスをオンにして、実行する警告を有効にします。 既定では、 **[有効化]** チェック ボックスはオンになっています。  
  
6.  **[種類]** ボックスの一覧の **[SQL Server イベント警告]** をクリックします。  
  
7.  **[イベント警告定義]** で、 **[データベース名]** ボックスの一覧からデータベースを選択して、警告を特定のデータベースに限定します。  
  
8.  **[警告が発生する条件]** の **[エラー番号]** をクリックし、その警告の有効なエラー番号を入力します。 または、 **[重大度]** をクリックし、警告を発生させる重大度を選択します。  
  
9. 特定の文字列が含まれている場合のみ警告を生成するには、 **[メッセージに次の内容が含まれている場合に警告する]** チェック ボックスをオンにし、 **[メッセージ テキスト]** ボックスにキーワードまたは文字列を入力します。 最大文字数は 100 文字です。  
  
10. **[OK]** をクリックします。  
  
## <a name="TsqlProcedure"></a>Transact-SQL の使用  
  
#### <a name="to-create-an-alert-using-an-error-number"></a>エラー番号を使用して警告を作成するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde_md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```  
    -- adds an alert (Test Alert) that runs the Back up
    -- the AdventureWorks2012 Database job when fired   
    -- assumes that the message 55001 and the Back up
    -- the AdventureWorks2012 Database job already exist.  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_add_alert  
        @name = N'Test Alert',  
        @message_id = 55001,   
       @severity = 0,   
       @notification_message = N'Error 55001 has occurred. The DB will be backed up...',   
       @job_name = N'Back up the AdventureWorks2012 Database' ;  
    GO  
    ```  
  
詳細については、「 [sp_add_alert (Transact-SQL)](https://msdn.microsoft.com/d9b41853-e22d-4813-a79f-57efb4511f09)」を参照してください。  
  
