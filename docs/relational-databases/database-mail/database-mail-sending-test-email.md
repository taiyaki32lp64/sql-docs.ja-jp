---
title: データベース メールでテスト メールを送信する | Microsoft Docs
ms.custom: ''
ms.date: 04/22/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- architecture [SQL Server], Database Mail
- Database Mail [SQL Server], architecture
- Database Mail [SQL Server], components
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: ce8a48b7e8315a564eaa1338df35a04226e705d4
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72906069"
---
# <a name="send-a-test-email-with-database-mail"></a>データベース メールでテスト メールを送信する  
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

[テスト電子メールの送信] ダイアログ ボックスを使用して、特定のプロファイルからメールを送信する機能をテストできます。

## <a name="permissions"></a>アクセス許可

[テスト電子メールの送信] ダイアログ ボックスを使用するには、sysadmin 固定サーバー ロールのメンバーである必要があります。 sysadmin 固定サーバー ロールのメンバーではないユーザーは、[sp_send_dbmail](../system-stored-procedures/sp-send-dbmail-transact-sql.md) プロシージャを使用してデータベース メールをテストできます。

## <a name="procedure"></a>手順

1. [SQL Server Management Studio](../../ssms/download-sql-server-management-studio-ssms.md) のオブジェクト エクスプローラーを使用して、データベース メールが構成されている SQL Server Database Engine のインスタンスに接続します。次に、[管理] を展開し、[データベース メール] を右クリックし、[テスト電子メールの送信] を選択します。 データベース メールのプロファイルが存在しない場合は、表示されるダイアログ ボックスにより、プロファイルを作成し、データベース メール構成ウィザードを起動するように求められます。
1. **[<instance name> からテスト電子メールを送信]** ダイアログ ボックスの [データベース メール プロファイル] ボックスで、テストするプロファイルを選択します。
1. **[宛先]** ボックスに、テスト電子メールの受信者の電子メール名を入力します。
1. **[件名]** ボックスに、テスト電子メールの件名を入力します。 既定の本文を変更し、トラブルシューティング用の電子メールであるとわかりやすい内容にします。
1. **[本文]** ボックスに、テスト電子メールの本文を入力します。 既定の本文を変更し、トラブルシューティング用の電子メールであるとわかりやすい内容にします。
1. **[テスト電子メールの送信]** を選択し、データベース メールのキューにテスト電子メールを送信します。
1. テスト電子メールを送信すると、[データベース メールのテスト電子メール] ダイアログ ボックスが開きます。 [送信された電子メール] ボックスに表示される数字をメモします。 この数字はテスト メッセージの mailitem_id です。 [OK] を選択します。
1. ツール バーの [新しいクエリ] を選択してクエリ エディター ウィンドウを開きます。 次の T-SQL ステートメントを実行して、テスト電子メール メッセージの状態を判断します。

    ```sql
    SELECT * FROM msdb.dbo.sysmail_allitems 
    WHERE mailitem_id = <the mailitem_id from the previous step> ;
    ```

    sent_status 列に、テスト電子メール メッセージが送信されたかどうかが示されます。

1. エラーが発生した場合は、次のステートメントを実行してエラー メッセージを表示します。

    ```sql
    SELECT * FROM msdb.dbo.sysmail_event_log 
    WHERE mailitem_id = <the mailitem_id from the previous step> ;
    ```


##  <a name="RelatedContent"></a> 参照 
  
-   [データベース メール構成オブジェクト](../../relational-databases/database-mail/database-mail-configuration-objects.md)
-   [データベース メール メッセージング オブジェクト](../../relational-databases/database-mail/database-mail-messaging-objects.md)
-   [データベース メール外部プログラム](../../relational-databases/database-mail/database-mail-external-program.md)
-   [データベース メールのログ記録と監査](../../relational-databases/database-mail/database-mail-log-and-audits.md)
-   [データベース メールを使用するように SQL Server エージェント メールを構成する](../../relational-databases/database-mail/configure-sql-server-agent-mail-to-use-database-mail.md)
  
  
