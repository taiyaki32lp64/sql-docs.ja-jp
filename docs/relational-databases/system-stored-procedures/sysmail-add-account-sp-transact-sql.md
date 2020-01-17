---
title: sysmail_add_account_sp (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_add_account_sp
- sysmail_add_account_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_add_account_sp
ms.assetid: 65e15e2e-107c-49c3-b12c-f4edf0eb1617
author: stevestein
ms.author: sstein
ms.openlocfilehash: d382d8ee7a871244213467b7a46bdc5b864c55cb
ms.sourcegitcommit: 4c75b49599018124f05f91c1df3271d473827e4d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/16/2019
ms.locfileid: "72381898"
---
# <a name="sysmail_add_account_sp-transact-sql"></a>sysmail_add_account_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  SMTP アカウントに関する情報を保持する新しいデータベースメールアカウントを作成します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sysmail_add_account_sp  [ @account_name = ] 'account_name',  
    [ @email_address = ] 'email_address' ,  
    [ [ @display_name = ] 'display_name' , ]  
    [ [ @replyto_address = ] 'replyto_address' , ]  
    [ [ @description = ] 'description' , ]  
    [ @mailserver_name = ] 'server_name'   
    [ , [ @mailserver_type = ] 'server_type' ]  
    [ , [ @port = ] port_number ]  
    [ , [ @username = ] 'username' ]  
    [ , [ @password = ] 'password' ]  
    [ , [ @use_default_credentials = ] use_default_credentials ]  
    [ , [ @enable_ssl = ] enable_ssl ]  
    [ , [ @account_id = ] account_id OUTPUT ]  
```  
  
## <a name="arguments"></a>引数  
追加するアカウントの名前 `[ @account_name = ] 'account_name'` ます。 *account_name*は**sysname**であり、既定値はありません。  
  
メッセージの送信元の電子メールアドレスを `[ @email_address = ] 'email_address'` します。 このアドレスは、インターネット電子メールアドレスである必要があります。 *email_address*は**nvarchar (128)** ,、既定値はありません。 たとえば、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントのアカウントは、 **SqlAgent\@Adventure-Works.com**のアドレスから電子メールを送信する場合があります。  
  
このアカウントからの電子メールメッセージで使用する表示名を `[ @display_name = ] 'display_name'` します。 *display_name*は**nvarchar (128)** ,、既定値は NULL です。 たとえば、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントのアカウントには、電子メールメッセージに**自動メーラー SQL Server エージェント**名前が表示される場合があります。  
  
このアカウントからのメッセージに対する応答の送信先アドレスを `[ @replyto_address = ] 'replyto_address'` します。 *replyto_address*は**nvarchar (128)** ,、既定値は NULL です。 たとえば、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントのアカウントへの返信は、データベース管理者**danw\@Adventure-Works.com**に送られます。  
  
`[ @description = ] 'description'` は、アカウントの説明です。 *説明*は**nvarchar (256)** ,、既定値は NULL です。  
  
このアカウントに使用する SMTP メールサーバーの名前または IP アドレスを `[ @mailserver_name = ] 'server_name'` します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を実行するコンピューターは、 *server_name*を IP アドレスに解決できる必要があります。 *server_name*は**sysname**であり、既定値はありません。  
  
電子メールサーバーの種類 `[ @mailserver_type = ] 'server_type'` ます。 *server_type*は**sysname**で、既定値は **' SMTP '** です。  
  
電子メールサーバーのポート番号を `[ @port = ] port_number` します。 *port_number*は**int**,、既定値は25です。  
  
電子メールサーバーへのログオンに使用するユーザー名を `[ @username = ] 'username'` します。 *username*は**nvarchar (128)** ,、既定値は NULL です。 このパラメーターが NULL の場合、データベースメールはこのアカウントに対して認証を使用しません。 メールサーバーで認証を必要としない場合は、ユーザー名に NULL を使用します。  
  
電子メールサーバーへのログオンに使用するパスワードを `[ @password = ] 'password'` します。 *パスワード*は**nvarchar (128)** ,、既定値は NULL です。 ユーザー名を指定しない限り、パスワードを入力する必要はありません。  
  
`[ @use_default_credentials = ] use_default_credentials` [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]の資格情報を使用して SMTP サーバーにメールを送信するかどうかを指定します。 **use_default_credentials**はビット,、既定値は0です。 このパラメーターが1の場合、データベースメールは [!INCLUDE[ssDE](../../includes/ssde-md.md)]の資格情報を使用します。 このパラメーターが0の場合、 **\@ユーザー名**と **\@パスワード**パラメーターが存在する場合はデータベースメール送信されます。それ以外の場合は、 **\@ユーザー名**と **\@パスワード**パラメーターを指定せずにメールを送信します。  
  
`[ @enable_ssl = ] enable_ssl` は、データベースメールが Secure Sockets Layer を使用して通信を暗号化するかどうかを指定します。 **Enable_ssl**はビット,、既定値は0です。  
  
`[ @account_id = ] account_id OUTPUT` は、新しいアカウントのアカウント id を返します。 *account_id*は**int**,、既定値は NULL です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>Remarks  
 データベースメールには、 **\@email_address**、 **\@display_name**、および **\@** replyto_address に個別のパラメーターが用意されています。 **\@email_address**パラメーターは、メッセージの送信元のアドレスです。 **\@display_name**パラメーターは、電子メールメッセージの **[差出人]** フィールドに表示される名前です。 **\@replyto_address**パラメーターは、電子メールメッセージへの返信が送信されるアドレスです。 たとえば、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントで使用するアカウントでは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントでのみ使用される電子メール アドレスから電子メール メッセージを送信できます。 そのアドレスからのメッセージにはフレンドリ名が表示されるので、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントがメッセージを送信したことを受信者が簡単に判断できるようになります。 受信者がメッセージに返信した場合、その返信は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントで使用されるアドレスではなくデータベース管理者に送られます。 このシナリオでは、アカウントは電子メールアドレスとして **SqlAgent@Adventure-Works.com** を使用します。 表示名は**SQL Server エージェント自動メーラ**に設定されます。 アカウントは **danw@Adventure-Works.com** を返信先として使用するので、このアカウントから送信されたメッセージへの返信は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントの電子メールアドレスではなく、データベース管理者に送られます。 これら3つのパラメーターに個別の設定を指定することにより、データベースメールによって、必要に応じてメッセージを構成できます。  
  
 **\@mailserver_type**パラメーターでは、値 **' SMTP '** がサポートされています。  
  
 **\@use_default_credentials**は、[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]の資格情報を使用して SMTP サーバーに1つのメールが送信されます。 **\@use_default_credentials**が0で、 **\@ユーザー名**と **\@パスワード**がアカウントに指定されている場合、そのアカウントは SMTP 認証を使用します。 **\@ユーザー名**と **\@パスワード**は、SMTP サーバーに対してアカウントが使用する資格情報であり、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] またはコンピューターがあるネットワークの資格情報ではありません。  
  
 ストアドプロシージャ**sysmail_add_account_sp**は**msdb**データベースにあり、 **dbo**スキーマが所有しています。 現在のデータベースが**msdb**でない場合は、3つの部分で構成される名前を使用してプロシージャを実行する必要があります。  
  
## <a name="permissions"></a>アクセス許可  
 このプロシージャの実行権限は、既定では**sysadmin**固定サーバーロールのメンバーに与えています。  
  
## <a name="examples"></a>使用例  
 次の例では、`AdventureWorks Administrator`という名前のアカウントを作成します。 このアカウントは、電子メールアドレス `dba@Adventure-Works.com` を使用し、SMTP メールサーバー `smtp.Adventure-Works.com`にメールを送信します。 このアカウントから送信された電子メールメッセージでは、メッセージの **[差出人]** 行に `AdventureWorks Automated Mailer` が表示されます。 メッセージへの返信は `danw@Adventure-Works.com` に転送されます。  
  
```  
EXECUTE msdb.dbo.sysmail_add_account_sp  
    @account_name = 'AdventureWorks Administrator',  
    @description = 'Mail account for administrative e-mail.',  
    @email_address = 'dba@Adventure-Works.com',  
    @display_name = 'AdventureWorks Automated Mailer',  
    @mailserver_name = 'smtp.Adventure-Works.com' ;  
```  
  
## <a name="see-also"></a>参照  
 [データベース メール](../../relational-databases/database-mail/database-mail.md)   
 [データベースメールアカウントの作成](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [ストアドプロシージャ&#40;のデータベースメール transact-sql&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
