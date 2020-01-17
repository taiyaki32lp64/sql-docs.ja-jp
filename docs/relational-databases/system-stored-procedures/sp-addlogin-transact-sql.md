---
title: sp_addlogin (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_addlogin
- sp_addlogin_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addlogin
ms.assetid: 030f19c3-a5e3-4b53-bfc4-de4bfca0fddc
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 5868120af1e98c4b2f3be78f2cf7927df53b42d1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68072665"
---
# <a name="spaddlogin-transact-sql"></a>sp_addlogin (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  新たに作成[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスに接続するユーザーを許可するログイン[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を使用して[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]認証します。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 使用[CREATE LOGIN](../../t-sql/statements/create-login-transact-sql.md)代わりにします。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_addlogin [ @loginame = ] 'login'   
    [ , [ @passwd = ] 'password' ]   
    [ , [ @defdb = ] 'database' ]   
    [ , [ @deflanguage = ] 'language' ]   
    [ , [ @sid = ] sid ]   
    [ , [ @encryptopt = ] 'encryption_option' ]   
[;]  
```  
  
## <a name="arguments"></a>引数  
 [ @loginame= ] '*login*'  
 ログインの名前を指定します。 *ログイン*は**sysname**、既定値はありません。  
  
 [ @passwd= ] '*password*'  
 ログインのパスワードです。 *パスワード*は**sysname**、既定値は NULL です。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]  
  
 [ @defdb=] '*データベース*'  
 ログインの既定のデータベースを指定します (そのログインがログインした後に最初に接続されるデータベース)。 *データベース*は**sysname**、既定値は**マスター**します。  
  
 [ @deflanguage=] '*言語*'  
 ログインの既定の言語です。 *言語*は**sysname**、既定値は NULL です。 場合*言語*が指定されていない既定*言語*新しいログインのサーバーの現在の既定の言語に設定されています。  
  
 [ @sid=] '*sid*'  
 セキュリティ ID 番号 (SID) を指定します。 *sid*は**varbinary (16)** 、既定値は NULL です。 場合*sid*が null の場合、システムには、新しいログインの SID が生成されます。 使用に関係なく、 **varbinary**データ型、NULL 以外の値は 16 バイトの長さにする必要があり、既に存在する必要があります。 指定する*sid*役に立ちます、たとえば、スクリプトをまたは移動するときに[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を別に 1 つのサーバーからログインする同じ SID を別のサーバー上にログインします。  
  
 [ @encryptopt=] '*encryption_option*'  
 パスワードを、クリア テキストとして渡すか、またはクリア テキスト パスワードのハッシュとして渡すかを指定します。 暗号化は行われないことに注意してください。 ここでは、"暗号化" という用語を旧バージョンとの互換性のために使用しています。 クリア テキスト パスワードが渡された場合はハッシュされています。 ハッシュは保存されます。 *encryption_option*は**varchar (20)** 値は次のいずれかを指定できます。  
  
|[値]|説明|  
|-----------|-----------------|  
|NULL|パスワードがクリア テキストで渡されます。 既定値です。|  
|**skip_encryption**|パスワードは既にハッシュされています。 [!INCLUDE[ssDE](../../includes/ssde-md.md)]再ハッシュせず、値を格納する必要があります。|  
|**skip_encryption_old**|指定されたパスワードは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の以前のバージョンでハッシュされています。 [!INCLUDE[ssDE](../../includes/ssde-md.md)]再ハッシュせず、値を格納する必要があります。 このオプションは、アップグレードのために提供されます。|  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="remarks"></a>コメント  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインの長さは 1 ～ 128 文字で、英字、記号、および数字を含めることができます。 ログインは、円記号を含めることはできません (\\); sa や public などの予約済みログイン名を指定するまたは既に存在; か、NULL または空の文字列にする (`''`)。  
  
 既定のデータベースの名前は、指定した場合、USE ステートメントを実行することがなく、指定されたデータベースに接続できます。 データベース所有者がそのデータベースへのアクセス権を付与はまでに、既定のデータベースを使用することはできませんただし、(を使用して[sp_adduser](../../relational-databases/system-stored-procedures/sp-adduser-transact-sql.md)または[sp_addrolemember](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)) または[sp_addrole](../../relational-databases/system-stored-procedures/sp-addrole-transact-sql.md).  
  
 SID 番号は、サーバーのログインが一意に識別する GUID です。  
  
 サーバーの既定の言語を変更しても、既存のログインに関する既定の言語は変更されません。 サーバーの既定の言語を変更する[sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)します。  
  
 使用して**skip_encryption**パスワードを抑制するのにログインが追加されると、パスワードは既にハッシュされている場合に便利ですがハッシュ[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 以前のバージョンで、パスワードがハッシュかどうか[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を使用して、 **skip_encryption_old**します。  
  
 ユーザー定義のトランザクション内では、sp_addlogin を実行できません。  
  
 次の表は、sp_addlogin と共に使用されるストアド プロシージャを示しています。  
  
|ストアド プロシージャ|説明|  
|----------------------|-----------------|  
|[sp_grantlogin](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)|Windows のユーザーまたはグループを追加します。|  
|[sp_password](../../relational-databases/system-stored-procedures/sp-password-transact-sql.md)|ユーザーのパスワードを変更します。|  
|[sp_defaultdb](../../relational-databases/system-stored-procedures/sp-defaultdb-transact-sql.md)|ユーザーの既定のデータベースを変更します。|  
|[sp_defaultlanguage](../../relational-databases/system-stored-procedures/sp-defaultlanguage-transact-sql.md)|ユーザーの既定の言語を変更します。|  
  
## <a name="permissions"></a>アクセス許可  
 ALTER ANY LOGIN 権限が必要です。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-creating-a-sql-server-login"></a>A. SQL Server ログインを作成する  
 次の例では、作成、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ユーザーのログイン`Victoria`、パスワードを使用して`B1r12-36`既定のデータベースを指定せずします。  
  
```  
EXEC sp_addlogin 'Victoria', 'B1r12-36';  
GO  
```  
  
### <a name="b-creating-a-sql-server-login-that-has-a-default-database"></a>B. 既定のデータベースを持つ SQL Server ログインを作成します。  
 次の例では、作成、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ユーザーのログイン`Albert`、パスワードを使用して`B5432-3M6`と、既定のデータベース`corporate`します。  
  
```  
EXEC sp_addlogin 'Albert', 'B5432-3M6', 'corporate';  
GO  
```  
  
### <a name="c-creating-a-sql-server-login-that-has-a-different-default-language"></a>C. 別の既定の言語には、SQL Server ログインを作成します。  
 次の例では、パスワード `TzTodorov`、既定のデータベース `709hLKH7chjfwv`、および既定の言語 `AdventureWorks2012` を指定して、ユーザー `Bulgarian` の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインを作成します。  
  
```  
EXEC sp_addlogin 'TzTodorov', '709hLKH7chjfwv', 'AdventureWorks2012', N'български'  
```  
  
### <a name="d-creating-a-sql-server-login-that-has-a-specific-sid"></a>D. 特定の SID を持つ SQL Server ログインを作成する  
 次の例では、パスワード `Michael`、既定のデータベース `B548bmM%f6`、既定の言語 `AdventureWorks2012`、および SID `us_english` を指定して、ユーザー `0x0123456789ABCDEF0123456789ABCDEF` の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインを作成します。  
  
```  
EXEC sp_addlogin 'Michael', 'B548bmM%f6', 'AdventureWorks2012', 'us_english', 0x0123456789ABCDEF0123456789ABCDEF  
```  
  
## <a name="see-also"></a>関連項目  
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [sp_droplogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droplogin-transact-sql.md)   
 [sp_helpuser &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpuser-transact-sql.md)   
 [sp_revokelogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revokelogin-transact-sql.md)   
 [xp_logininfo &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/xp-logininfo-transact-sql.md)  
  
  
