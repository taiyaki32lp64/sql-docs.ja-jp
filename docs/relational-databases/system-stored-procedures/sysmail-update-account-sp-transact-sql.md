---
title: sysmail_update_account_sp (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 11/17/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_update_account_sp
- sysmail_update_account_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_update_account_sp
ms.assetid: ba2fdccc-5ed4-40ef-a479-79497b4d61aa
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 68bd628eb791e7af102c6689e22b30ebd5bad73c
ms.sourcegitcommit: 43c3d8939f6f7b0ddc493d8e7a643eb7db634535
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2019
ms.locfileid: "72305113"
---
# <a name="sysmail_update_account_sp-transact-sql"></a>sysmail_update_account_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  既存のデータベース メール アカウントの情報を変更します。  
 
 
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sysmail_update_account_sp [ [ @account_id = ] account_id ] [ , ] [ [ @account_name = ] 'account_name' ] ,  
    [ @email_address = ] 'email_address' ,   
    [ @display_name = ] 'display_name' ,   
    [ @replyto_address = ] 'replyto_address' ,  
    [ @description = ] 'description' ,   
    [ @mailserver_name = ] 'server_name' ,   
    [ @mailserver_type = ] 'server_type' ,   
    [ @port = ] port_number ,   
    [ @timeout = ] 'timeout' ,  
    [ @username = ] 'username' ,  
    [ @password = ] 'password' ,  
    [ @use_default_credentials = ] use_default_credentials ,  
    [ @enable_ssl = ] enable_ssl   
```  
  
## <a name="arguments"></a>引数  
更新するアカウント ID を `[ @account_id = ] account_id` します。 *account_id*は**int**,、既定値は NULL です。 少なくとも1つの*account_id*または*account_name*を指定する必要があります。 両方が指定されている場合、プロシージャはアカウントの名前を変更します。  
  
更新するアカウントの名前 `[ @account_name = ] 'account_name'` ます。 *account_name*は**sysname**,、既定値は NULL です。 少なくとも1つの*account_id*または*account_name*を指定する必要があります。 両方が指定されている場合、プロシージャはアカウントの名前を変更します。  
  
メッセージの送信元の新しい電子メールアドレスを `[ @email_address = ] 'email_address'` します。 このアドレスは、インターネット電子メールアドレスである必要があります。 アドレスのサーバー名は、このアカウントからメールを送信するためにデータベースメール使用するサーバーです。 *email_address*は**nvarchar (128)** ,、既定値は NULL です。  
  
このアカウントからの電子メールメッセージに使用する新しい表示名を `[ @display_name = ] 'display_name'` します。 *display_name*は**nvarchar (128)** ,、既定値はありません。  
  
このアカウントからの電子メールメッセージの返信先ヘッダーで使用する新しいアドレスを `[ @replyto_address = ] 'replyto_address'` します。 *replyto_address*は**nvarchar (128)** ,、既定値はありません。  
  
アカウントの新しい説明を `[ @description = ] 'description'` します。 *説明*は**nvarchar (256)** ,、既定値は NULL です。  
  
このアカウントに使用する SMTP メールサーバーの新しい名前を `[ @mailserver_name = ] 'server_name'` します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を実行するコンピューターは、 *server_name*を IP アドレスに解決できる必要があります。 *server_name*は**sysname**であり、既定値はありません。  
  
メールサーバーの新しい種類を `[ @mailserver_type = ] 'server_type'` します。 *server_type*は**sysname**であり、既定値はありません。 **' SMTP '** の値のみがサポートされています。  
  
メールサーバーの新しいポート番号を `[ @port = ] port_number` します。 *port_number*は**int**,、既定値はありません。  
  
SmtpClient の `[ @timeout = ] 'timeout'` タイムアウトパラメーター。1つの電子メールメッセージを送信します。 *タイムアウト*は秒単位の**int**で、既定値はありません。  
  
メールサーバーへのログオンに使用する新しいユーザー名を `[ @username = ] 'username'` します。 *ユーザー名*は**sysname**で、既定値はありません。  
  
メールサーバーへのログオンに使用する新しいパスワードを `[ @password = ] 'password'` します。 *パスワード*は**sysname**,、既定値はありません。  
  
`[ @use_default_credentials = ] use_default_credentials` [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] サービスの資格情報を使用して SMTP サーバーにメールを送信するかどうかを指定します。 **use_default_credentials**はビット,、既定値はありません。 このパラメーターが1の場合、データベースメールは [!INCLUDE[ssDE](../../includes/ssde-md.md)]の資格情報を使用します。 このパラメーターが0の場合、データベースメールは **\@ユーザー名**と **\@パスワード**を使用して、SMTP サーバーの認証を行います。 **\@ユーザー名**と **\@パスワード**が NULL の場合、匿名認証が使用されます。 このパラメーターを指定する前に、SMTP 管理者に相談してください。  
  
`[ @enable_ssl = ] enable_ssl` は、データベースメールが Secure Sockets Layer (SSL) を使用して通信を暗号化するかどうかを指定します。 SMTP サーバーで SSL が必要な場合はこのオプションを使用します。 **enable_ssl**はビット,、既定値はありません。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>Remarks  
 アカウント名とアカウント id の両方を指定すると、アカウントの情報を更新するだけでなく、アカウント名も変更されます。 アカウント名の変更は、アカウント名のエラーを修正する場合に利用できます。  
  
 ストアドプロシージャ**sysmail_update_account_sp**は**msdb**データベースにあり、 **dbo**スキーマが所有しています。 現在のデータベースが**msdb**でない場合は、3つの部分で構成される名前を使用してプロシージャを実行する必要があります。  
  
## <a name="permissions"></a>アクセス許可  
 **sysadmin** 固定サーバー ロールのメンバーシップが必要です。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-changing-the-information-for-an-account"></a>A. アカウントの情報を変更する  
 次の例では、 **msdb**データベースの `AdventureWorks Administrator` アカウントを更新します。 アカウントの情報は、指定された値に設定されます。  
  
```  
EXECUTE msdb.dbo.sysmail_update_account_sp  
     @account_name = 'AdventureWorks Administrator'  
    ,@description = 'Mail account for administrative e-mail.'  
    ,@email_address = 'dba@Adventure-Works.com'  
    ,@display_name = 'AdventureWorks Automated Mailer'  
    ,@replyto_address = NULL  
    ,@mailserver_name = 'smtp.Adventure-Works.com'  
    ,@mailserver_type = 'SMTP'  
    ,@port = 25  
    ,@timeout = 60  
    ,@username = NULL  
    ,@password = NULL  
    ,@use_default_credentials = 0  
    ,@enable_ssl = 0;  
```  
  
### <a name="b-changing-the-name-of-an-account-and-the-information-for-an-account"></a>b. アカウントの名前とアカウントの情報を変更する  
 次の例では、アカウント ID `125` の名前を変更し、アカウント情報を更新します。 アカウントの新しい名前が `Backup Mail Server`ます。  
  
```  
EXECUTE msdb.dbo.sysmail_update_account_sp  
     @account_id = 125  
    ,@account_name = 'Backup Mail Server'  
    ,@description = 'Mail account for administrative e-mail.'  
    ,@email_address = 'dba@Adventure-Works.com'  
    ,@display_name = 'AdventureWorks Automated Mailer'  
    ,@replyto_address = NULL  
    ,@mailserver_name = 'smtp-backup.Adventure-Works.com'  
    ,@mailserver_type = 'SMTP'  
    ,@port = 25  
    ,@timeout = 60  
    ,@username = NULL  
    ,@password = NULL  
    ,@use_default_credentials = 0  
    ,@enable_ssl = 0;  
```  
  
## <a name="see-also"></a>参照  
 [データベース メール](../../relational-databases/database-mail/database-mail.md)   
 [データベースメールアカウントの作成](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [ストアドプロシージャ&#40;のデータベースメール transact-sql&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
