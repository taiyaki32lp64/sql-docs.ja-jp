---
title: sp_dropremotelogin (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_dropremotelogin
- sp_dropremotelogin_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dropremotelogin
ms.assetid: 9f097652-a286-40b2-be73-568d77ada698
ms.author: vanto
author: VanMSFT
ms.openlocfilehash: c316f48f3e590fcba419e125f8e327b25ee1ede6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67933823"
---
# <a name="spdropremotelogin-transact-sql"></a>sp_dropremotelogin (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を実行中のローカル サーバーに対してリモート ストアド プロシージャを実行する場合に使用される、ローカル ログインにマップされているリモート ログインを削除します。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextDontUse](../../includes/ssnotedepnextdontuse-md.md)] 代わりに、リンク サーバーとリンク サーバー ストアド プロシージャを使用します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
sp_dropremotelogin [ @remoteserver = ] 'remoteserver'   
     [ , [ @loginame = ] 'login' ]   
     [ , [ @remotename = ] 'remote_name' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @remoteserver = ] 'remoteserver'` 削除するリモート ログインにマップされているリモート サーバーの名前です。 *remoteserver*は**sysname**、既定値はありません。 *remoteserver*既に存在する必要があります。  
  
`[ @loginame = ] 'login'` リモート サーバーに関連付けられているローカル サーバー上の省略可能なログイン名です。 *login* のデータ型は **sysname** で、既定値は NULL です。 *ログイン*指定されている場合に既に存在する必要があります。  
  
`[ @remotename = ] 'remote_name'` マップされているリモート ログインの名前を省略可能な*ログイン*リモート サーバーからにログインします。 *remote_name*は**sysname**、既定値は NULL です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="remarks"></a>コメント  
 もしも*remoteserver*を指定すると、そのリモート サーバーのすべてのリモート ログインは、ローカル サーバーから削除されます。 場合*ログイン*から指定すると、すべてのリモート ログインも*remoteserver*その特定の場所にマップされたローカル ログインは、ローカル サーバーから削除されます。 場合*remote_name*が指定されても、そのリモート ユーザーからのリモート ログインだけ*remoteserver*ローカル サーバーから削除されます。  
  
 ローカル サーバー ユーザーを追加する**sp_addlogin**します。 ローカル サーバー ユーザーを削除する使用**sp_droplogin**します。  
  
 リモート ログインは、以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を使用する場合にのみ必要です。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Version 7.0 以降では、代わりにリンク サーバー ログインを使用します。 使用**sp_addlinkedsrvlogin**と**sp_droplinkedsrvlogin**を追加およびリンク サーバー ログインを削除します。  
  
 **sp_dropremotelogin**ユーザー定義のトランザクション内で実行することはできません。  
  
## <a name="permissions"></a>アクセス許可  
 メンバーシップが必要です、 **sysadmin**または**securityadmin**固定サーバー ロール。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-dropping-all-remote-logins-for-a-remote-server"></a>A. リモート サーバーのリモート ログインをすべて削除します。  
 次の例は、リモート サーバー エントリを削除します。 `ACCOUNTS`、し、そのため、ローカル サーバー上のログインとリモート サーバー上のリモート ログイン マッピングをすべて削除します。  
  
```sql
EXEC sp_dropremotelogin 'ACCOUNTS';  
```  
  
### <a name="b-dropping-a-login-mapping"></a>B. ログインのマッピングを削除します。  
 次の例では、リモート サーバー `ACCOUNTS` からのリモート ログインとローカル ログイン `Albert` をマップしているエントリを削除します。  
  
```sql
EXEC sp_dropremotelogin 'ACCOUNTS', 'Albert';  
```  
  
### <a name="c-dropping-a-remote-user"></a>C. リモート ユーザーを削除  
 次の例では、リモート ログインのログインを削除する`Chris`、リモート サーバーで`ACCOUNTS`ローカル ログインにマップされている`salesmgr`します。  
  
```sql
EXEC sp_dropremotelogin 'ACCOUNTS', 'salesmgr', 'Chris';  
```  
  
## <a name="see-also"></a>関連項目  
 [セキュリティ ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addlinkedsrvlogin &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedsrvlogin-transact-sql.md)   
 [sp_addlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogin-transact-sql.md)   
 [sp_addremotelogin &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addremotelogin-transact-sql.md)   
 [sp_addserver &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md)   
 [sp_droplinkedsrvlogin &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droplinkedsrvlogin-transact-sql.md)   
 [sp_droplogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droplogin-transact-sql.md)   
 [sp_helpremotelogin &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpremotelogin-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
