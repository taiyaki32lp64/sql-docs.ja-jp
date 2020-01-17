---
title: sp_defaultlanguage (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_defaultlanguage
- sp_defaultlanguage_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_defaultlanguage
ms.assetid: 908d01cc-e704-45d9-9e85-d2df6da3e6f5
author: stevestein
ms.author: sstein
ms.openlocfilehash: af2402ce4f1e49ee572a9d271497c2798d679070
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68120091"
---
# <a name="spdefaultlanguage-transact-sql"></a>sp_defaultlanguage (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインの既定の言語を変更します。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 使用[ALTER LOGIN](../../t-sql/statements/alter-login-transact-sql.md)代わりにします。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_defaultlanguage [ @loginame = ] 'login'   
     [ , [ @language = ] 'language' ]   
```  
  
## <a name="arguments"></a>引数  
`[ @loginame = ] 'login'` ログイン名です。 *ログイン*は**sysname**、既定値はありません。 *ログイン*既存できる[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ログインまたは Windows ユーザーまたはグループ。  
  
`[ @language = ] 'language'` ログインの既定の言語です。 *言語*は**sysname**、既定値は NULL です。 *言語*サーバー上で有効な言語である必要があります。 場合*言語*が指定されていない*言語*、サーバーの既定言語に設定されている既定の言語がによって定義されている、 **sp_configure**構成変数**既定の言語**します。 サーバーの既定の言語を変更しても、既存のログインの既定の言語は変わりません。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_defaultlanguage**は追加のオプションをサポートする ALTER LOGIN を呼び出します。 その他のログインの既定値を変更する方法の詳細については、次を参照してください。 [ALTER LOGIN &#40;TRANSACT-SQL&#41;](../../t-sql/statements/alter-login-transact-sql.md)します。  
  
 現在のセッションの言語を変更するのにには、SET LANGUAGE ステートメントを使用します。 使用して、@@LANGUAGE関数を現在の言語設定を表示します。  
  
 サーバーからログインの既定の言語を削除すると、ログインは、サーバーの既定の言語を取得します。 **sp_defaultlanguage**ユーザー定義のトランザクション内で実行することはできません。  
  
 サーバーにインストールされている言語に関する情報は、 **sys.syslanguages**カタログ ビューです。  
  
## <a name="permissions"></a>アクセス許可  
 ALTER ANY LOGIN 権限が必要です。  
  
## <a name="examples"></a>使用例  
 次の例では、`ALTER LOGIN` を使用して、ログイン `Fathima` の既定の言語をアラビア語に変更します。 これは推奨される方法です。  
  
```  
ALTER LOGIN Fathima WITH DEFAULT_LANGUAGE = Arabic;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [セキュリティ ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [ALTER LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/alter-login-transact-sql.md)   
 [@@LANGUAGE &#40;Transact-SQL&#41;](../../t-sql/functions/language-transact-sql.md)   
 [SET ステートメント &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [sys.syslanguages &#40;TRANSACT-SQL&#41;](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
