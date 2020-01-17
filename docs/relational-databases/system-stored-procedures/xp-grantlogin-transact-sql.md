---
title: xp_grantlogin (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- xp_grantlogin
- xp_grantlogin_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- xp_grantlogin
ms.assetid: c851c1ab-3b29-4b99-9902-78c2665a844b
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 957bbdc43c0f0adf3a545fee76e9f69df130d8f9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68116669"
---
# <a name="xpgrantlogin-transact-sql"></a>xp_grantlogin (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Windows グループまたはユーザー アクセス権を付与する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 使用[CREATE LOGIN](../../t-sql/statements/create-login-transact-sql.md)代わりにします。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
xp_grantlogin {[@loginame = ] 'login'} [,[@logintype = ] 'logintype']  
```  
  
## <a name="arguments"></a>引数  
`[ @loginame = ] 'login'` 追加するには、Windows ユーザーまたはグループの名前です。 Windows ユーザーまたはグループは、フォームでの Windows ドメイン名で修飾する必要があります*ドメイン*\\*ユーザー*します。 *ログイン*は**sysname**、既定値はありません。  
  
`[ @logintype = ] 'logintype'` ログインのセキュリティ レベルは、アクセスを許可されています。 *logintype*は**varchar (5)** 、既定値は NULL です。 のみ**管理者**を指定できます。 場合**管理者**が指定されている*ログイン*へのアクセスを許可するが[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のメンバーとして追加して、 **sysadmin**固定サーバー ロール。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="remarks"></a>コメント  
 **xp_grantlogin**は、システム ストアド プロシージャ、拡張ストアド プロシージャではなく。 **xp_grantlogin**呼び出し**sp_grantlogin**と**sp_addsrvrolemember**します。  
  
## <a name="permissions"></a>アクセス許可  
 メンバーシップが必要です、 **securityadmin**固定サーバー ロール。 変更するときに、 *logintype*、メンバーシップが必要です、 **sysadmin**固定サーバー ロール。  
  
## <a name="see-also"></a>関連項目  
 [sp_denylogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-denylogin-transact-sql.md)   
 [sp_grantlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [汎用拡張ストアド プロシージャ&#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)   
 [xp_enumgroups &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/xp-enumgroups-transact-sql.md)   
 [xp_loginconfig &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/xp-loginconfig-transact-sql.md)   
 [xp_logininfo &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/xp-logininfo-transact-sql.md)   
 [sp_revokelogin &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revokelogin-transact-sql.md)  
  
  
