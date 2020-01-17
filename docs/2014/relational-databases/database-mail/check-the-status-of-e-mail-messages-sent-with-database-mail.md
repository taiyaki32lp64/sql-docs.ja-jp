---
title: データベース メールから送信された電子メール メッセージの状態の確認 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- e-mail [SQL Server], status information
- mail [SQL Server], status information
- Database Mail [SQL Server], message status
- status information [Database Mail]
ms.assetid: eb290f24-b52f-46bc-84eb-595afee6a5f3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 73d0cf3a374a7f3dda7797238d2c1702360aa955
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62872331"
---
# <a name="check-the-status-of-e-mail-messages-sent-with-database-mail"></a>データベース メールから送信された電子メール メッセージの状態の確認
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] を使用して、 [!INCLUDE[tsql](../../includes/tsql-md.md)]のデータベース メール経由で送信された電子メール メッセージの状態を確認する方法について説明します。  
  
-   **作業を開始する準備:**  
  
-   **データベース メールを使用して、使用して送信される電子メールの状態を表示するには。** [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
 データベース メールは、送信する電子メール メッセージのコピーを保持し、 **msdb**データベースの **sysmail_allitems**、 **sysmail_sentitems**、 **sysmail_unsentitems** 、および **sysmail_faileditems** の各ビューに表示します。 データベース メール外部プログラムは、利用状況をログに記録し、Windows アプリケーション イベント ログや **msdb** データベースの **sysmail_event_log** ビューでそのログを表示します。 電子メール メッセージの状態を確認するには、このビューに対してクエリを実行します。 電子メール メッセージの状態は、 **sent**、 **unsent**、 **retrying**、および **failed**のいずれかになります。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
 **データベース メールを使用して送信された電子メールの状態を表示するには**  
  
> [!NOTE]  
>  この手順の例については、このセクションの後半の「 [例 (Transact-SQL)](#TsqlExample)」を参照してください。  
  
1.  **sysmail_allitems** テーブルから選択して、**mailitem_id** または **sent_status** で対象のメッセージを指定します。  
  
2.  その電子メール メッセージについてデータベース メール外部プログラムから返される状態を確認するには、次のセクションに示すように、 **mailitem_id** 列で **sysmail_allitems** と **sysmail_event_log** ビューを結合します。  
  
     データベース メール外部プログラムの既定では、正常に送信されたメッセージについての情報がログに記録されません。 すべてのメッセージをログに記録するには、 **データベース メール構成ウィザード** の **[システム パラメーターの構成]** ページを使用して、ログのレベルを詳細に設定します。  
  
###  <a name="TsqlExample"></a> 例 (Transact-SQL)  
 次の例では、外部プログラムが正常に送信できなかった、 `danw` への電子メール メッセージに関する情報を表示します。 このステートメントは、件名、外部プログラムでメッセージの送信に失敗した日時、およびデータベース メール ログに記録されているエラー メッセージの一覧を表示します。  
  
```  
USE msdb ;  
GO  
  
-- Show the subject, the time that the mail item row was last  
-- modified, and the log information.  
-- Join sysmail_faileditems to sysmail_event_log   
-- on the mailitem_id column.  
-- In the WHERE clause list items where danw was in the recipients,  
-- copy_recipients, or blind_copy_recipients.  
-- These are the items that would have been sent  
-- to danw.  
  
SELECT items.subject,  
    items.last_mod_date  
    ,l.description FROM dbo.sysmail_faileditems as items  
INNER JOIN dbo.sysmail_event_log AS l  
    ON items.mailitem_id = l.mailitem_id  
WHERE items.recipients LIKE '%danw%'    
    OR items.copy_recipients LIKE '%danw%'   
    OR items.blind_copy_recipients LIKE '%danw%'  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [データベース メールのログ記録と監査](database-mail-log-and-audits.md)  
  
  
