---
title: データベース メール:メールがキューされました、配信されません | Microsoft Docs
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
ms.openlocfilehash: 92ff867d98b83f1934972a576df8295c3f9ca79d
ms.sourcegitcommit: 2da98f924ef34516f6ebf382aeb93dab9fee26c1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/03/2019
ms.locfileid: "70228414"
---
# <a name="database-mail-mail-queued-not-delivered"></a>データベース メール:メールがキューされました、配信されません 
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

このトピックでは、電子メール メッセージが正常にキューに登録されても、そのメッセージが配信されない問題のトラブルシューティングを行う方法について説明します。

## <a name="diagnose-the-problem"></a>問題を診断する 

電子メールの利用状況は、データベース メール外部プログラムにより **msdb** データベースに記録されます。

まず、データベース メールが有効になっていることを確認するために、次の例のように、**sp_configure** システム ストアド プロシージャの [Database Mail XPs オプション](../../database-engine/configure-windows/database-mail-xps-server-configuration-option.md)を使用します。

```sql 
EXEC sp_configure 'show advanced', 1;  
RECONFIGURE; 
EXEC sp_configure; 
GO
```

次に、**msdb** データベースで次のステートメントを実行し、メール キューの状態を確認します。

```sql
sysmail_help_queue_sp @queue_type = 'Mail' ;
```

列の詳細については、「[sysmail_help_queue_sp (Transact-SQL)](../system-stored-procedures/sysmail-help-queue-sp-transact-sql.md#result-set)」を参照してください。

**sysmail_event_log** ビューで利用状況を確認します。 このビューには、データベース メール外部プログラムが開始されていることを示すエントリが含まれています。 **sysmail_event_log** ビューにエントリが存在しない場合は、**sysmail_event_log** で [Messages Queued, No Entries](database-mail-common-errors.md#database-mail-queued-no-entries-in-sysmail_event_log-or-windows-application-event-log) という症状を確認してください。 **sysmail_event_log** ビューでエラーが発生している場合は、そのエラーのトラブルシューティングを行います。

**sysmail_event_log** ビューにエントリが含まれている場合は、**sysmail_allitems** ビューでメッセージの状態を確認します。

## <a name="message-status-unsent"></a>メッセージの状態 - unsent 

状態 **unsent** は、電子メール メッセージが[データベース メール外部プログラム](database-mail-external-program.md)でまだ処理されていないことを表します。 データベース メール外部プログラムによるメッセージの処理は遅れることがあります。この外部プログラムのメッセージ処理速度は、ネットワークの状態、再試行タイムアウト、メッセージの量、SMTP サーバーの処理能力によって異なります。 問題が解決しない場合は、複数のプロファイルを使用して、複数の SMTP サーバーにメッセージを分散させることを検討します。

正常に配信されたメッセージを対象に、最終更新日をチェックします。 最後に正常な配信が行われてからしばらく経過している場合は、sysmail_event_log ビューで、この外部プログラムが Service Broker によって正常に開始されたことを確認します。 最後の試行で外部プログラムが開始されなかった場合は、データベース メール外部プログラムが適切なディレクトリにあり、SQL Server のサービス アカウントにこの実行可能ファイルの実行権限があるかどうかを確認します。

   > [!NOTE]
   > 古い未送信のメッセージを削除するには、配信できないメッセージがキュー内で最も古いメッセージになるまで待ち、[sysmail_delete_mailitems_sp](../system-stored-procedures/sysmail-delete-mailitems-sp-transact-sql.md) を使用して、これらのメッセージを削除します。

## <a name="message-status-retrying"></a>メッセージの状態 - retrying

状態 retrying は、データベース メールが SMTP サーバーに電子メール メッセージを配信しようとしたが、配信できなかったことを表します。 通常、この現象は、ネットワークの中断、SMTP サーバーの障害、または正しく構成されていないデータベース メール アカウントによって発生します。 メッセージは最終的には成功または失敗し、イベント ログに記録されます。

## <a name="message-status-sent"></a>メッセージの状態 - sent

状態 **sent** は、電子メール メッセージがデータベース メール外部プログラムから SMTP サーバーに正常に配信されたことを表します。 そのメッセージが配信先に到達しなかった場合は、データベース メールから送信されたメッセージは SMTP サーバーで受信されていますが、最終的な受信者には配信されていません。 SMTP サーバーのログを確認するか、SMTP サーバーの管理者に問い合わせてください。 Outlook Express などの別のクライアントを使用して、SMTP メール サーバーをテストすることもできます。

## <a name="message-status-failed"></a>メッセージの状態 - failed

状態 failed は、電子メール メッセージをデータベース メール外部プログラムから SMTP サーバーに配信できなかったことを表します。 この場合、**sysmail_event_log** ビューにデータベース メールからの詳細情報が含まれています。 **sysmail_faileditems** と **sysmail_event_log** を結合して詳細なエラー メッセージを入手するサンプル クエリについては、「[データベース メールから送信された電子メール メッセージの状態の確認](check-the-status-of-e-mail-messages-sent-with-database-mail.md)」を参照してください。 このような問題では、宛先のアドレスが間違っているか、ネットワーク上で問題が発生したためにデータベース メールが 1 つ以上のフェールオーバー アカウントにアクセスできないことが最も一般的な原因です。 SMTP サーバーで問題が発生すると、その SMTP サーバーでメールが拒否されることがあります。 データベース メール構成ウィザードを使用して、**[ログ記録レベル]** を **[詳細]** に変更し、テスト メールを送信して障害発生時点を調べます。



##  <a name="RelatedContent"></a> 参照
  
-  [データベース メールの概要](database-mail.md)

  
  
