---
title: sp_addremotelogin (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_addremotelogin_TSQL
- sp_addremotelogin
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addremotelogin
ms.assetid: 71b7cd36-a17d-4b12-b102-10aeb0f9268b
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: eb45ce1c3e1786eb5a9a3cd630741dd4df773c40
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68030962"
---
# <a name="spaddremotelogin-transact-sql"></a>sp_addremotelogin (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  ローカル サーバー上の新しいリモート ログイン ID を追加します。 これにより、リモート サーバーに接続し、リモート プロシージャ コールを実行できます。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextDontUse](../../includes/ssnotedepnextdontuse-md.md)]代わりに、リンク サーバーとリンク サーバー ストアド プロシージャを使用してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_addremotelogin [ @remoteserver = ] 'remoteserver'   
     [ , [ @loginame = ] 'login' ]   
     [ , [ @remotename = ] 'remote_name' ]  
```  
  
## <a name="arguments"></a>引数  
 [ @remoteserver **=** ] **'** _remoteserver_ **'**  
 リモート ログインが適用されるリモート サーバーの名前です。 *remoteserver*は**sysname**、既定値はありません。 だけの場合*remoteserver*が指定されているすべてのユーザーに*remoteserver*ローカル サーバーに同じ名前の既存のログインにマップされます。 このサーバーは、ローカル サーバーが認識している必要があります。 Sp_addserver を使用して追加されます。 ときにユーザーに*remoteserver*を実行しているローカル サーバーに接続[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]で自分のログインと一致するローカル ログインとして接続するリモート ストアド プロシージャを実行する*remoteserver*. *remoteserver*はリモート プロシージャ呼び出しを開始するサーバーです。  
  
 [ @loginame **=** ] **'** _ログイン_ **'**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のローカル インスタンス上のユーザーのログイン ID を指定します。 *login* のデータ型は **sysname** で、既定値は NULL です。 *ログイン*のローカル インスタンスに既に存在する必要があります[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 場合*ログイン*が指定されているすべてのユーザーに*remoteserver*特定ローカル ログインにマップされます。 ときにユーザーに*remoteserver*のローカル インスタンスに接続[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]として接続するリモート ストアド プロシージャを実行する*ログイン*します。  
  
 [ @remotename **=** ] **'** _remote_name_ **'**  
 リモート サーバー上のユーザーのログイン ID です。 *remote_name*は**sysname**、既定値は NULL です。 *remote_name*上に存在する必要があります*remoteserver*します。 場合*remote_name*が指定されている特定のユーザー *remote_name*にマップされて*ログイン*ローカル サーバーにします。 ときに*remote_name*で*remoteserver*のローカル インスタンスに接続する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]としてリモート ストアド プロシージャを実行する接続*ログイン*します。 ログイン ID *remote_name* 、リモート サーバー上のログイン ID と異なっていてもかまいません*ログイン*します。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="remarks"></a>コメント  
 分散クエリを実行するには、sp_addlinkedsrvlogin を使用します。  
  
 sp_addremotelogin は、ユーザー定義のトランザクション内で使用できません。  
  
## <a name="permissions"></a>アクセス許可  
 Sp_addremotelogin を実行できるは、sysadmin、securityadmin 固定サーバー ロールのメンバーだけです。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-mapping-one-to-one"></a>A. 一対一のマッピング  
 次の例では、リモート名をマップするローカル名の場合に、リモート サーバー`ACCOUNTS`と同じユーザー ログインを持つローカルのサーバー。  
  
```  
EXEC sp_addremotelogin 'ACCOUNTS';  
```  
  
### <a name="b-mapping-many-to-one"></a>B. 多対一のマッピング  
 次の例では、リモート サーバー `ACCOUNTS` のすべてのユーザーを、ローカル ID `Albert` にマップするエントリを作成します。  
  
```  
EXEC sp_addremotelogin 'ACCOUNTS', 'Albert';  
```  
  
### <a name="c-using-explicit-one-to-one-mapping"></a>C. 明示的に一対一でマップする  
 次の例は、リモート ユーザーからのリモート ログインをマップ`Chris`、リモート サーバーで`ACCOUNTS`がローカル ユーザーに`salesmgr`します。  
  
```  
EXEC sp_addremotelogin 'ACCOUNTS', 'salesmgr', 'Chris';  
```  
  
## <a name="see-also"></a>関連項目  
 [sp_addlinkedsrvlogin &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedsrvlogin-transact-sql.md)   
 [sp_addlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogin-transact-sql.md)   
 [sp_addserver &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md)   
 [sp_dropremotelogin &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropremotelogin-transact-sql.md)   
 [sp_grantlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [sp_helpremotelogin &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpremotelogin-transact-sql.md)   
 [sp_helpserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md)   
 [sp_remoteoption &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-remoteoption-transact-sql.md)   
 [sp_revokelogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revokelogin-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
