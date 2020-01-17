---
title: sp_password (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_password
- sp_password_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_password
ms.assetid: 0ecbec81-e637-44a9-a61e-11bf060ef084
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: c02b9327dbff75e3c0816bb3eec19e3cb3135d50
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68008922"
---
# <a name="sppassword-transact-sql"></a>sp_password (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  追加または変更するためのパスワードを[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ログインします。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 使用[ALTER LOGIN](../../t-sql/statements/alter-login-transact-sql.md)代わりにします。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_password [ [ @old = ] 'old_password' , ]  
     { [ @new =] 'new_password' }  
     [ , [ @loginame = ] 'login' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @old = ] 'old_password'` 古いパスワードです。 *old_password*は**sysname**、既定値は NULL です。  
  
`[ @new = ] 'new_password'` 新しいパスワードです。 *新しい _ パスワード*は**sysname**、既定値はありません。 *old_password*名前付きパラメーターを使用しないかどうかは指定する必要があります。  
  
> [!IMPORTANT]  
>  パスワードは NULL を使用しないでください。 強力なパスワードを使用してください。 詳細については、「 [Strong Passwords](../../relational-databases/security/strong-passwords.md)」を参照してください。  
  
`[ @loginame = ] 'login'` パスワードの変更により影響を受けるログインの名前です。 *login* のデータ型は **sysname** で、既定値は NULL です。 *ログイン*が既に存在しのメンバーでのみ指定できます、 **sysadmin**または**securityadmin**固定サーバー ロール。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_password**は ALTER LOGIN を呼び出します。 このステートメントは、追加のオプションをサポートします。 パスワードを変更する方法の詳細については、次を参照してください。 [ALTER LOGIN &#40;TRANSACT-SQL&#41;](../../t-sql/statements/alter-login-transact-sql.md)します。  
  
 **sp_password**ユーザー定義のトランザクション内で実行することはできません。  
  
## <a name="permissions"></a>アクセス許可  
 ALTER ANY LOGIN 権限が必要です。 古いパスワードを指定しないでパスワードをリセットする場合、または変更されるログインに CONTROL SERVER 権限がある場合は、CONTROL SERVER 権限も必要です。  
  
 プリンシパルは、独自のパスワードを変更できます。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-changing-the-password-of-a-login-without-knowing-the-old-password"></a>A. 古いパスワードがわからない場合、ログインのパスワードを変更します。  
 次の例では、`ALTER LOGIN` を使って、`Victoria` ログイン用のパスワードを `B3r1000d#2-36` に変更します。 これは推奨される方法です。 このコマンドを実行しているユーザーは、CONTROL SERVER 権限が必要です。  
  
```  
ALTER LOGIN Victoria WITH PASSWORD = 'B3r1000d#2-36';  
GO  
```  
  
### <a name="b-changing-a-password"></a>B. パスワードの変更  
 次の例は、使用する方法を示します`ALTER LOGIN`ログインのパスワードを変更する`Victoria`から`B3r1000d#2-36`に`V1cteAmanti55imE`します。 これは推奨される方法です。 ユーザー `Victoria` は、追加の権限を取得しなくてもこのコマンドを実行できます。 他のユーザーには ALTER ANY LOGIN 権限が必要です。  
  
```  
ALTER LOGIN Victoria WITH   
     PASSWORD = 'V1cteAmanti55imE'   
     OLD_PASSWORD = 'B3r1000d#2-36';  
GO  
```  
  
## <a name="see-also"></a>参照  
 [セキュリティ ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [ALTER LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/alter-login-transact-sql.md)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [sp_addlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogin-transact-sql.md)   
 [sp_adduser &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adduser-transact-sql.md)   
 [sp_grantlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [sp_revokelogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revokelogin-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
