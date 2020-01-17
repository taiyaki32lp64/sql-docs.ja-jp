---
title: 一般的データベース メール トラブルシューティング
ms.custom: seo-dt-2019
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
ms.openlocfilehash: fb063b3af008ad7e734197a0d4360c9d83535cd3
ms.sourcegitcommit: 15fe0bbba963d011472cfbbc06d954d9dbf2d655
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/14/2019
ms.locfileid: "74094554"
---
# <a name="general-database-mail-troubleshooting-steps"></a>一般的データベース メール トラブルシューティング手順 
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

データベース メールのトラブルシューティングを行うには、データベース メール システムに関して次の点を確認する必要があります。 以下の手順は論理的な順序で示していますが、どのような順序で行ってもかまいません。

## <a name="permissions"></a>アクセス許可

データベース メールのどの領域の問題を解決するにしても、sysadmin 固定サーバー ロールのメンバーである必要があります。 sysadmin 固定サーバー ロールのメンバーでないユーザーは、自身が送信した電子メールに関する情報しか入手できず、他のユーザーが送信した電子メールに関する情報は入手できません。

## <a name="is-database-mail-enabled"></a>データベース メールが有効になっているか

1. SQL Server Management Studio のクエリ エディター ウィンドウを使用して SQL Server のインスタンスに接続し、次のコードを実行します。

    ```sql
    sp_configure 'show advanced', 1; 
    GO
    RECONFIGURE;
    GO
    sp_configure;
    GO
    ```

   結果ウィンドウで、[Database Mail XPs](../../database-engine/configure-windows/database-mail-xps-server-configuration-option.md) の run_value が 1 に設定されていることを確認します。
   run_value が 1 でない場合、データベース メールは無効です。 悪意のあるユーザーから攻撃を受ける機能の数を少なくするため、データベース メールは自動的には有効になりません。 詳細については、[セキュリティ構成を理解する](../security/surface-area-configuration.md)方法に関するページを参照してください。

1. データベース メールを有効にすることが適切であると判断した場合は、次のコードを実行します。

    ```sql
    sp_configure 'Database Mail XPs', 1; 
    GO
    RECONFIGURE;
    GO
    ```

1. sp_configure プロシージャを既定の状態に戻して、詳細設定オプションが表示されないようにするには、次のコードを実行します。

    ```sql 
    sp_configure 'show advanced', 0; 
    GO
    RECONFIGURE;
    GO
    ```

## <a name="are-users-properly-configured-to-send-mail"></a>ユーザーにメール送信が正しく設定されているか

1. データベース メールを送信するには、msdb データベースの DatabaseMailUserRole データベース ロールのメンバーにユーザーがなる必要があります。 sysadmin 固定サーバー ロールと msdbdb_owner ロールのメンバーは、自動的に DatabaseMailUserRole ロールのメンバーになります。 DatabaseMailUserRole の他のすべてのメンバーを一覧するには、次のステートメントを実行します。

    ```sql
    EXEC msdb.sys.sp_helprolemember 'DatabaseMailUserRole';
    ```

1. DatabaseMailUserRole ロールにユーザーを追加するには、次のステートメントを使用します。

    ```sql
    USE msdb;
    GO
    
    sp_addrolemember @rolename = 'DatabaseMailUserRole'
    ,@membername = '<database user>';
    ```

1. データベース メールを送信するユーザーは、少なくとも 1 つのデータベース メール プロファイルにアクセスできる必要があります。 ユーザー (プリンシパル) とそのユーザーがアクセスできるプロファイルを一覧するには、次のステートメントを実行します。

    ```sql
    EXEC msdb.dbo.sysmail_help_principalprofile_sp;
    ```

1. データベース メール構成ウィザードを使用してプロファイルを作成し、ユーザーにそのプロファイルへのアクセス許可を与えます。
 
## <a name="is-database-mail-started"></a>データベース メールが起動しているか

1. 処理する電子メール メッセージがあると、[データベース メール外部プログラム](database-mail-external-program.md)がアクティブになります。 指定されたタイムアウト期間内に送信するメッセージがなくなると、プログラムが終了します。 データベース メールのアクティブ化が開始されことを確認するには、次のステートメントを実行します。

    ```sql
    EXEC msdb.dbo.sysmail_help_status_sp;
    ```
1. データベース メールのアクティブ化が開始されていない場合は、次のステートメントを実行して開始します。

    ```sql
    EXEC msdb.dbo.sysmail_start_sp;
    ```

1. データベース メール外部プログラムが開始されている場合は、次のステートメントを使用してメール キューの状態を確認します。

    ```sql
    EXEC msdb.dbo.sysmail_help_queue_sp @queue_type = 'mail';
    ```
  
   メール キューの状態は RECEIVES_OCCURRING になっている必要があります。 キューの状態は刻一刻と変化します。 メールキューの状態が RECEIVES_OCCURRING ではない場合、キューの再起動をお試しください。 次のステートメントでキューを停止します。
   
```sql
EXEC msdb.dbo.sysmail_stop_sp;
```

停止後、次のステートメントでキューを開始します。

```sql
EXEC msdb.dbo.sysmail_start_sp;
```

  > [!NOTE]
  >  メール キュー内の電子メールの数を判断するには、sysmail_help_queue_sp の結果セットの length 列を使用します。

## <a name="do-problems-affect-some-or-all-accounts"></a>問題は一部のアカウントに影響を与えるのか、全部のアカウントに影響を与えるのか

1. すべてのプロファイルではなく、一部のプロファイルしかメールを送信できていない場合は、メールを送信できないプロファイルで使用されているデータベース メール アカウントに問題があると考えられます。 メールを正しく送信できるアカウントを確認するには、次のステートメントを実行します。

    ```sql
    SELECT sent_account_id, sent_date FROM msdb.dbo.sysmail_sentitems;
    ```

1. 一覧表示されたアカウントのいずれも、メールを送信できないプロファイルで使用されていない場合、そのプロファイルで使用可能なアカウントがすべて正しく機能していない可能性があります。 個々のアカウントをテストするには、データベース メール構成ウィザードを使用して、アカウントを 1 つだけ含む新しいプロファイルを作成します。次に、[テスト電子メールの送信] ダイアログ ボックスを使用し、このアカウントでメールを送信します。 
1. データベース メールから返されたエラー メッセージを表示するには、次のステートメントを実行します。

    ```sql
    SELECT * FROM msdb.dbo.sysmail_event_log;
    ```

   > [!NOTE]
   > データベース メールでは、メールが SMTP メール サーバーに正常に配信されると、メールが送信されたと見なします。 その後、受信者の電子メール アドレスが無効であるなどのエラーが発生しメールが配信されなくても、データベース メールのログにはそのことが記録されません。

## <a name="retry-mail-delivery"></a>メール配信を再試行する

1. SMTP サーバーに確実に到達できないことが原因でデータベース メールが失敗していると思われる場合は、データベース メールからの各メッセージの送信試行回数を増加することで、正常なメール配信率を向上できることがあります。 データベース メール構成ウィザードを起動して、[システム パラメーターを表示または変更する] オプションを選択します。 または、プロファイルに関連付けるアカウント数を増やすこともできます。これにより、プライマリ アカウントからのフェールオーバー時には、フェールオーバー アカウントを使用して電子メールが送信されるようになります。
1. [システム パラメーターの構成] ページの [アカウントの再試行回数] の 5 回、[アカウントの再試行間隔] の 60 秒という既定値は、SMTP サーバーに 5 分間到達できないと、メッセージの配信に失敗することを意味しています。 この 2 つのパラメーター値を増加することで、メッセージの配信に失敗するまでの時間を長くすることができます。

    > [!NOTE]
    > 送信されるメッセージが多い場合、この既定値を大きくすると確実性は高くなりますが、大量のメッセージの配信が何度も試行されるので、リソースの使用量も大幅に増加することになります。 ネットワークや SMTP サーバーに、データベース メールから SMTP サーバーへの即時アクセスを妨害するような問題があれば、それを解決することで、根本的な問題点に対処してください。



##  <a name="RelatedContent"></a> 参照
  
-   [データベース メール構成オブジェクト](../../relational-databases/database-mail/database-mail-configuration-objects.md)  
  
-   [データベース メール メッセージング オブジェクト](../../relational-databases/database-mail/database-mail-messaging-objects.md)  
  
-   [データベース メール外部プログラム](../../relational-databases/database-mail/database-mail-external-program.md)  
  
-   [データベース メールのログ記録と監査](../../relational-databases/database-mail/database-mail-log-and-audits.md)  
  
-   [データベース メールを使用するように SQL Server エージェント メールを構成する](../../relational-databases/database-mail/configure-sql-server-agent-mail-to-use-database-mail.md)  
  
  
  
