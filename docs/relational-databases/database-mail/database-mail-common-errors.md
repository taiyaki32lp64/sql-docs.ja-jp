---
title: データベース メールの一般的なエラー | Microsoft Docs
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
ms.openlocfilehash: ee5e7fd6511a624b05b4d6c7d03c1f2dcd288054
ms.sourcegitcommit: 2da98f924ef34516f6ebf382aeb93dab9fee26c1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/03/2019
ms.locfileid: "70228434"
---
# <a name="common-errors-with-database-mail"></a>データベース メールの一般的なエラー 
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

この記事では、データベース メールでよく見られるエラーとその解決策について説明します。

## <a name="could-not-find-stored-procedure-sp_send_dbmail"></a>ストアド プロシージャ 'sp_send_dbmail' が見つかりませんでした
[sp_send_dbmail](../system-stored-procedures/sp-send-dbmail-transact-sql.md) ストアド プロシージャは msdb データベースにインストールされています。 msdb データベースから **sp_send_dbmail** を実行するか、3 部構成の名前をこのストアド プロシージャに指定する必要があります。

例:
```sql
EXEC msdb.dbo.sp_send_dbmail ...
```

または:

```sql
USE msdb;
GO
EXEC dbo.sp_send_dbmail ...
```

データベース メールの作成および構成には、[データベース メール構成ウィザード](configure-database-mail.md)を使用します。

## <a name="profile-not-valid"></a>プロファイルが無効です
このメッセージには 2 つの原因が考えられます。 指定されたプロファイルが存在しないか、[sp_send_dbmail (Transact-SQL)](../system-stored-procedures/sp-send-dbmail-transact-sql.md) を実行しているユーザーがプロファイルにアクセスする権限を持っていません。

プロファイルのアクセス許可を確認するには、ストアド プロシージャ [sysmail_help_principalprofile_sp (Transact-SQL)](../system-stored-procedures/sysmail-help-principalprofile-sp-transact-sql.md) をプロファイルの名前で実行します。 ストアド プロシージャ [sysmail_add_principalprofile_sp (Transact-SQL)](../system-stored-procedures/sysmail-help-principalprofile-sp-transact-sql.md) または[データベース メール構成ウィザード](configure-database-mail.md)を使用し、msdb ユーザーまたはグループがプロファイルにアクセスするための権限を与えます。

## <a name="permission-denied-on-sp_send_dbmail"></a>sp_send_dbmail でアクセスが拒否される

このトピックでは、データベース メールの送信を試みたユーザーには sp_send_dbmail を実行する権限がないというエラー メッセージに対してトラブルシューティングを行う方法について説明します。

このエラー メッセージのテキストは次のとおりです。

```
EXECUTE permission denied on object 'sp_send_dbmail', 
database 'msdb', schema 'dbo'.
```

データベース メールを送信するには、ユーザーが msdb データベースに存在し、msdb データベースの DatabaseMailUserRole データベース ロールのメンバーである必要があります。 msdb のユーザーやグループをこのロールに追加するには、SQL Server Management Studio を使用するか、データベース メールを送信する必要のあるユーザーまたはロールに対して次のステートメントを実行します。

```sql
EXEC msdb.dbo.sp_addrolemember @rolename = 'DatabaseMailUserRole'
    ,@membername = '<user or role name>';
GO
```
詳細については、「[sp_addrolemember](../system-stored-procedures/sp-addrolemember-transact-sql.md)」と「[sp_droprolemember](../system-stored-procedures/sp-droprolemember-transact-sql.md)」を参照してください。

## <a name="database-mail-queued-no-entries-in-sysmail_event_log-or-windows-application-event-log"></a>キューに登録されたデータベース メールのエントリが sysmail_event_log または Windows アプリケーション イベント ログにない 

データベース メールは、電子メール メッセージをキューに登録するために Service Broker に依存します。 データベース メールが停止している場合、または Service Broker のメッセージ配信が **msdb** データベースでアクティブになっていない場合は、データベース メールによってメッセージがデータベースのキューに登録されますが、そのメッセージは配信できません。 この場合、Service Broker メッセージは Service Broker のメール キューに残ります。 Service Broker では外部プログラムがアクティブ化されないので、**sysmail_event_log** にはログ エントリが存在せず、**sysmail_allitems** および関連するビューのアイテムの状態は更新されません。

次のステートメントを実行し、Service Broker が **msdb** データベースで有効になっているかどうかを確認します。

```sql
SELECT is_broker_enabled FROM sys.databases WHERE name = 'msdb';
```

値 0 は、Service Broker のメッセージ配信が msdb データベースでアクティブになっていないことを示します。 問題を解決するには、次の Transact-SQL コマンドを実行し、データベースで Service Broker を有効にします。

```sql
USE master ;
GO

ALTER DATABASE msdb SET ENABLE_BROKER ;
GO
``` 

データベース メールは、多数の内部ストアド プロシージャに依存しています。 外部からのアクセスを制限するには、これらのストアド プロシージャを新しくインストールした SQL Server で無効にします。 これらのストアド プロシージャを有効にするには、次の例のように、**sp_configure** システム ストアド プロシージャの [Database Mail XPs オプション](../../database-engine/configure-windows/database-mail-xps-server-configuration-option.md)を使用します。

```sql
EXEC sp_configure 'show advanced options', 1;  
RECONFIGURE;
EXEC sp_configure 'Database Mail XPs', 1;  
RECONFIGURE  
GO  

Database Mail may be stopped in the **msdb** database. To check status of Database Mail, execute the following statement:

```sql
EXECUTE dbo.sysmail_help_status_sp;
```

メール ホスト データベースでデータベース メールを開始するには、msdb データベースで次のコマンドを実行します。

```sql
EXECUTE dbo.sysmail_start_sp;
```

Service Broker がアクティブになっている場合、メッセージのダイアログの有効期間が確認されます。したがって、構成されたダイアログの有効期間よりも長く Service Broker 転送キューに登録されているすべてのメッセージがすぐに失敗します。 データベース メールにより、失敗したメッセージの状態が [sysmail_allitems](../system-catalog-views/sysmail-allitems-transact-sql.md) および関連するビューで更新されます。 電子メール メッセージを再び送信するかどうかを決定する必要があります。 データベース メールで使用するダイアログの有効期間の設定の詳細については、「[sysmail_configure_sp (Transact-SQL)](../system-stored-procedures/sysmail-configure-sp-transact-sql.md)」を参照してください。



##  <a name="RelatedContent"></a> 参照
  
-  [データベース メールの概要](database-mail.md)
-  [データベース メール プロファイルの作成](create-a-database-mail-profile.md)
  
  
