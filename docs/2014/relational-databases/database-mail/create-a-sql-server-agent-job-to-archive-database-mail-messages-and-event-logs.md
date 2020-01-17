---
title: データベース メール メッセージやイベント ログをアーカイブする SQL Server エージェント ジョブの作成 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- archiving mail messages and attachments [SQL Server]
- removing mail messages and attachements
- Database Mail [SQL Server], archiving
- saving mail messages and attachments
ms.assetid: 8f8f0fba-f750-4533-9b76-a9cdbcdc3b14
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a1fa03dbb8803c27ba917e662db1958361900b15
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62917594"
---
# <a name="create-a-sql-server-agent-job-to-archive-database-mail-messages-and-event-logs"></a>データベース メール メッセージやイベント ログをアーカイブする SQL Server エージェント ジョブの作成
  データベース メール メッセージと添付ファイルのコピーは、データベース メール イベント ログに記録されると同時に、 **msdb** のテーブルに保持されます。 このテーブルのサイズを縮小するためには、不要になったメッセージやイベントを定期的にアーカイブする必要があります。 次の手順では、この処理を自動化する SQL Server エージェント ジョブを作成します。  
  
-   **作業を開始する準備:**  、 [前提条件](#Prerequisites)、 [推奨事項](#Recommendations)、 [権限](#Permissions)  
  
-   **データベース メール メッセージおよびログをアーカイブする方法:** [SQL Server エージェント](#Process_Overview)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Prerequisites"></a> 前提条件  
 アーカイブ データを格納する新しいテーブルが、特別なアーカイブ データベース内にある場合があります。 代わりに、行をテキスト ファイルにエクスポートすることができます。  
 
  
###  <a name="Recommendations"></a> 推奨事項  
 運用環境では、詳細なエラー チェックを追加したり、ジョブが失敗した場合には電子メール メッセージをオペレーターに送信したりする必要があるでしょう。  
  
  
###  <a name="Permissions"></a> Permissions  
 このトピックで説明したストアド プロシージャを実行するには、 **sysadmin** 固定サーバー ロールのメンバーである必要があります。  
  
  
###  <a name="Process_Overview"></a> プロセスの概要  
  
-   まず、次のステップから構成される "データベース メールのアーカイブ" という名前のジョブを作成します。  
  
    1.  すべてのメッセージをデータベース メールのテーブルから新しいテーブルにコピーします。新しいテーブルには、**DBMailArchive_**_<年_月>_ の形式で、前の月を表す文字列を付加した名前を付けます。  
  
    2.  最初のステップでコピーしたメッセージに関連する添付ファイルをデータベース メールのテーブルから新しいテーブルにコピーします。新しいテーブルには、**DBMailArchive_Attachments_**_<年_月>_ の形式で、前の月を表す文字列を付加した名前を付けます。  
  
    3.  最初のステップでコピーしたメッセージに関連するデータベース メール イベント ログからのイベントを、データベース メールのテーブルから新しいテーブルにコピーします。新しいテーブルには、**DBMailArchive_Log_**_<年_月>_ の形式で、前の月を表す文字列を付加した名前を付けます。  
  
    4.  移し変えたメール アイテムのレコードをデータベース メールのテーブルから削除します。  
  
    5.  移し変えたメール アイテムに関連するイベントをデータベース メールのイベント ログから削除します。  
  
-   ジョブが定期的に実行されるようにスケジュールを設定します。  
 
  
## <a name="to-create-a-sql-server-agent-job"></a>SQL Server エージェントのジョブを作成するには  
  
1.  オブジェクト エクスプローラーで [ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント] を展開し、 **[ジョブ]** を右クリックして、 **[新しいジョブ]** をクリックします。  
  
2.  **[新しいジョブ]** ダイアログ ボックスで、 **[名前]** ボックスに「 **データベース メールのアーカイブ**」と入力します。  
  
3.  **[所有者]** ボックスで、所有者が **sysadmin** 固定サーバー ロールのメンバーであることを確認します。  
  
4.  **[カテゴリ]** ボックスで **[データベースのメンテナンス]** をクリックします。  
  
5.  **[説明]** ボックスに「 **データベース メール メッセージのアーカイブ**」と入力し、 **[ステップ]** をクリックします。  
  
  
  
## <a name="to-create-a-step-to-archive-the-database-mail-messages"></a>データベース メールのメッセージをアーカイブするステップを作成するには  
  
1.  **[ステップ]** ページで **[新規作成]** をクリックします。  
  
2.  **[ステップ名]** ボックスに「 **データベース メール アイテムのコピー**」と入力します。  
  
3.  **[種類]** ボックスで **[Transact-SQL スクリプト (T-SQL)]** をクリックします。  
  
4.  **[データベース]** ボックスで **[msdb]** をクリックします。  
  
5.  **[コマンド]** ボックスに次のステートメントを入力します。このステートメントでは、前の月を表す文字列を付加した名前のテーブルが作成されます。このテーブルには、今月の開始日以前の行が格納されます。  
  
    ```  
    DECLARE @LastMonth nvarchar(12);  
    DECLARE @CopyDate nvarchar(20) ;  
    DECLARE @CreateTable nvarchar(250) ;  
    SET @LastMonth = (SELECT CAST(DATEPART(yyyy,GETDATE()) AS CHAR(4)) + '_' + CAST(DATEPART(mm,GETDATE())-1 AS varchar(2))) ;  
    SET @CopyDate = (SELECT CAST(CONVERT(char(8), CURRENT_TIMESTAMP- DATEPART(dd,GETDATE()-1), 112) AS datetime))  
    SET @CreateTable = 'SELECT * INTO msdb.dbo.[DBMailArchive_' + @LastMonth + '] FROM sysmail_allitems WHERE send_request_date < ''' + @CopyDate +'''';  
    EXEC sp_executesql @CreateTable ;  
    ```  
  
6.  **[OK]** をクリックしてステップを保存します。  
  
  
  
## <a name="to-create-a-step-to-archive-the-database-mail-attachments"></a>データベース メールの添付ファイルをアーカイブするステップを作成するには  
  
1.  **[ステップ]** ページで **[新規作成]** をクリックします。  
  
2.  **[ステップ名]** ボックスに「 **データベース メール添付ファイルのコピー**」と入力します。  
  
3.  **[種類]** ボックスで **[Transact-SQL スクリプト (T-SQL)]** をクリックします。  
  
4.  **[データベース]** ボックスで **[msdb]** をクリックします。  
  
5.  **[コマンド]** ボックスに次のステートメントを入力します。このステートメントでは、前の月を表す文字列を付加した名前の添付ファイル テーブルが作成されます。このテーブルには、前のステップでコピーされたメッセージに対応する添付ファイルが格納されます。  
  
    ```  
    DECLARE @LastMonth nvarchar(12);  
    DECLARE @CopyDate nvarchar(20) ;  
    DECLARE @CreateTable nvarchar(250) ;  
    SET @LastMonth = (SELECT CAST(DATEPART(yyyy,GETDATE()) AS CHAR(4)) + '_' + CAST(DATEPART(mm,GETDATE())-1 AS varchar(2))) ;  
    SET @CopyDate = (SELECT CAST(CONVERT(char(8), CURRENT_TIMESTAMP- DATEPART(dd,GETDATE()-1), 112) AS datetime))  
    SET @CreateTable = 'SELECT * INTO msdb.dbo.[DBMailArchive_Attachments_' + @LastMonth + '] FROM sysmail_attachments   
     WHERE mailitem_id in (SELECT DISTINCT mailitem_id FROM [DBMailArchive_' + @LastMonth + '] )';  
    EXEC sp_executesql @CreateTable ;  
    ```  
  
6.  **[OK]** をクリックしてステップを保存します。  
  
  
  
## <a name="to-create-a-step-to-archive-the-database-mail-log"></a>データベース メールのログをアーカイブするステップを作成するには  
  
1.  **[ステップ]** ページで **[新規作成]** をクリックします。  
  
2.  **[ステップ名]** ボックスに「 **データベース メール ログのコピー**」と入力します。  
  
3.  **[種類]** ボックスで **[Transact-SQL スクリプト (T-SQL)]** をクリックします。  
  
4.  **[データベース]** ボックスで **[msdb]** をクリックします。  
  
5.  **[コマンド]** ボックスに次のステートメントを入力します。このステートメントでは、前の月を表す文字列を付加した名前のログ テーブルが作成されます。このテーブルには、前半のステップでコピーされたメッセージに対応するログ エントリが格納されます。  
  
    ```  
    DECLARE @LastMonth nvarchar(12);  
    DECLARE @CopyDate nvarchar(20) ;  
    DECLARE @CreateTable nvarchar(250) ;  
    SET @LastMonth = (SELECT CAST(DATEPART(yyyy,GETDATE()) AS CHAR(4)) + '_' + CAST(DATEPART(mm,GETDATE())-1 AS varchar(2))) ;  
    SET @CopyDate = (SELECT CAST(CONVERT(char(8), CURRENT_TIMESTAMP- DATEPART(dd,GETDATE()-1), 112) AS datetime))  
    SET @CreateTable = 'SELECT * INTO msdb.dbo.[DBMailArchive_Log_' + @LastMonth + '] FROM sysmail_Event_Log   
     WHERE mailitem_id in (SELECT DISTINCT mailitem_id FROM [DBMailArchive_' + @LastMonth + '] )';  
    EXEC sp_executesql @CreateTable ;  
    ```  
  
6.  **[OK]** をクリックしてステップを保存します。  
  
  
  
## <a name="to-create-a-step-to-remove-the-archived-rows-from-database-mail"></a>データベース メールからアーカイブされた行を削除するステップを作成するには  
  
1.  **[ステップ]** ページで **[新規作成]** をクリックします。  
  
2.  **[ステップ名]** ボックスに「 **データベース メールからの行の削除**」と入力します。  
  
3.  **[種類]** ボックスで **[Transact-SQL スクリプト (T-SQL)]** をクリックします。  
  
4.  **[データベース]** ボックスで **[msdb]** をクリックします。  
  
5.  **[コマンド]** ボックスに次のステートメントを入力します。このステートメントでは、データベース メールのテーブルから今月よりも古い行が削除されます。  
  
    ```  
    DECLARE @CopyDate nvarchar(20) ;  
    SET @CopyDate = (SELECT CAST(CONVERT(char(8), CURRENT_TIMESTAMP- DATEPART(dd,GETDATE()-1), 112) AS datetime)) ;  
    EXECUTE msdb.dbo.sysmail_delete_mailitems_sp @sent_before = @CopyDate ;  
    ```  
  
6.  **[OK]** をクリックしてステップを保存します。  
  
  
  
## <a name="to-create-a-step-to-remove-the-archived-items-from-database-mail-event-log"></a>データベース メール イベント ログからアーカイブされたアイテムを削除するステップを作成するには  
  
1.  **[ステップ]** ページで **[新規作成]** をクリックします。  
  
2.  **[ステップ名]** ボックスに「 **データベース メール イベント ログからの行の削除**」と入力します。  
  
3.  **[種類]** ボックスで **[Transact-SQL スクリプト (T-SQL)]** をクリックします。  
  
4.  **[コマンド]** ボックスに次のステートメントを入力します。このステートメントでは、データベース メールのイベント ログから今月よりも古い行が削除されます。  
  
    ```  
    DECLARE @CopyDate nvarchar(20) ;  
    SET @CopyDate = (SELECT CAST(CONVERT(char(8), CURRENT_TIMESTAMP- DATEPART(dd,GETDATE()-1), 112) AS datetime)) ;  
    EXECUTE msdb.dbo.sysmail_delete_log_sp @logged_before = @CopyDate ;  
    ```  
  
5.  **[OK]** をクリックしてステップを保存します。  
  
  
  
## <a name="to-schedule-the-job-to-run-periodically"></a>ジョブが定期的に実行されるようにスケジュールを設定するには  
  
1.  **[新しいジョブ]** ダイアログ ボックスで **[スケジュール]** をクリックします。  
  
2.  **[スケジュール]** ページで **[新規作成]** をクリックします。  
  
3.  **[名前]** ボックスに「 **データベース メールのアーカイブ**」と入力します。  
  
4.  **[スケジュールの種類]** ボックスで **[定期的]** をクリックします。  
  
5.  **[頻度]** 領域で、たとえば毎月 1 回など、定期的にジョブを実行するオプションを選択します。  
  
6.  **[一日のうちの頻度]** 領域で、**[Occurs once at <time\<]** (<時刻> に 1 度実行) を選びます。  
  
7.  その他のオプションが目的どおりに構成されていることを確認し、 **[OK]** をクリックしてスケジュールを保存します。  
  
8.  **[OK]** をクリックしてジョブを保存します。  
  
  
  
  
