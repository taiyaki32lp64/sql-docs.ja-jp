---
title: "データベース メールと電子メール アラートは、Linux 上の SQL エージェントの |Microsoft ドキュメント"
description: "このトピックの内容が Linux に SQL Server でデータベース メールと電子メール アラートを使用する方法について説明します"
author: meet-bhagdev
ms.author: meetb
manager: jhubbard
ms.date: 07/17/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: tbd
ms.translationtype: MT
ms.sourcegitcommit: ea75391663eb4d509c10fb785fcf321558ff0b6e
ms.openlocfilehash: 838a7d492f9826d966da205fc4727eae48ff6e42
ms.contentlocale: ja-jp
ms.lasthandoff: 08/02/2017

---
# <a name="db-mail-and-email-alerts-with-sql-agent-on-linux"></a>データベース メールと Linux 上の SQL エージェントによる電子メールのアラート

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

次の手順は、データベース メールをセットアップし、SQL Server エージェントで使用する方法を示します (**mssql server エージェント**) on Linux です。 

> [!NOTE]
> SQL Server on Linux では、データベース メールを使用するには、SQL Server 2017 RC2 を使用する必要がありますまたはそれ以降。

## <a name="prerequisites"></a>前提条件
-   SQL Server 2017 RC2 以降
-   SQL Server エージェント v14.0.800.90 2 以上 (アラートの電子メールを使用する場合)

## <a name="1-enable-db-mail"></a>1.データベース メールを有効にします。

```sql
USE master 
GO 
sp_configure 'show advanced options',1 
GO 
RECONFIGURE WITH OVERRIDE 
GO 
sp_configure 'Database Mail XPs', 1 
GO 
RECONFIGURE  
GO  
```

## <a name="2-create-a-new-account"></a>2.[新しいアカウントを作成する]
```sql
EXECUTE msdb.dbo.sysmail_add_account_sp 
@account_name = 'SQLAlerts', 
@description = 'Account for Automated DBA Notifications', 
@email_address = 'sqlagenttest@gmail.com', 
@replyto_address = 'sqlagenttest@gmail.com', 
@display_name = 'SQL Agent', 
@mailserver_name = 'smtp.gmail.com', 
@port = 587, 
@enable_ssl = 1, 
@username = 'sqlagenttest@gmail.com', 
@password = '<password>' 
GO
```

## <a name="3-create-a-default-profile"></a>3.既定のプロファイルを作成します。

```sql
EXECUTE msdb.dbo.sysmail_add_profile_sp 
@profile_name = 'default', 
@description = 'Profile for sending Automated DBA Notifications' 
GO
```

## <a name="4-add-the-database-mail-account-to-a-database-mail-profile"></a>4.データベース メール プロファイルへのデータベース メール アカウントを追加します。
```sql
EXECUTE msdb.dbo.sysmail_add_principalprofile_sp 
@profile_name = 'default', 
@principal_name = 'public', 
@is_default = 1 ; 
 ```
 
## <a name="5-add-account-to-profile"></a>5.アカウントをプロファイルに追加します。 
```sql
EXECUTE msdb.dbo.sysmail_add_profileaccount_sp   
@profile_name = 'default',   
@account_name = 'SQLAlerts',   
@sequence_number = 1;  
 ```
 
## <a name="6-send-test-email"></a>6.テスト電子メールを送信します。
> [!NOTE]
> 電子メール クライアントに移動し、「クライアントを許可安全性の低いメールを送信する」を有効にする必要があります。 すべてのクライアントは、データベース メールを電子メール デーモンとして認識します。

```
EXECUTE msdb.dbo.sp_send_dbmail 
@profile_name = 'default', 
@recipients = 'recipient-email@gmail.com', 
@Subject = 'Testing DBMail', 
@Body = 'This message is a test for DBMail' 
GO
```

## <a name="7-set-db-mail-profile-using-mssql-conf-or-environment-variable"></a>7.Mssql conf または環境変数を使用してデータベース メール プロファイルの設定
Mssql conf ユーティリティまたは環境変数を使用すると、データベース メール プロファイルを登録します。 この場合、既定のプロファイルをとしましょう。

```bash
# via mssql-conf
sudo /opt/mssq/bin/mssql-conf set sqlagent.databasemailprofile default
# via environment variable
MSSQL_AGENT_EMAIL_PROFILE=default
```

## <a name="8-set-up-an-operator-for-sqlagent-job-notifications"></a>8.SQLAgent ジョブの通知をオペレーターを設定します。 

```sql
EXEC msdb.dbo.sp_add_operator 
@name=N'JobAdmins',  
@enabled=1, 
@email_address=N'recipient-email@gmail.com',  
@category_name=N'[Uncategorized]' 
GO 
```

## <a name="9-send-email-when-agent-test-job-succeeds"></a>9.'エージェントのテスト ジョブ' が成功したときに電子メールを送信します。 

```
EXEC msdb.dbo.sp_update_job 
@job_name='Agent Test Job', 
@notify_level_email=1, 
@notify_email_operator_name=N'JobAdmins' 
GO
```

## <a name="next-steps"></a>次の手順
SQL Server エージェントを使用して、作成、スケジュール、およびジョブを実行する方法の詳細については、次を参照してください。 [Linux に SQL Server エージェント ジョブを実行](sql-server-linux-run-sql-server-agent-job.md)です。
