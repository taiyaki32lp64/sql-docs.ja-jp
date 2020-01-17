---
title: sp_releaseapplock (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_releaseapplock_TSQL
- sp_releaseapplock
dev_langs:
- TSQL
helpviewer_keywords:
- sp_releaseapplock
ms.assetid: 51b03c2f-0d54-40f5-9172-e747942d4a46
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 7b75962019d9b39728ceff0b151e770dd0f51a25
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68075628"
---
# <a name="spreleaseapplock-transact-sql"></a>sp_releaseapplock (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  アプリケーション リソースのロックを解放します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_releaseapplock [ @Resource = ] 'resource_name'   
     [ , [ @LockOwner = ] 'lock_owner' ]  
     [ , [ @DbPrincipal = ] 'database_principal' ]  
[ ; ]  
```  
  
## <a name="arguments"></a>引数  
 [ @Resource=] '*resource_name*'  
 ロック リソース名は、クライアント アプリケーションによって指定されます。 アプリケーションは、リソースが一意であることを確認する必要があります。 指定した名前は内部的にハッシュされ、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ロック マネージャーに格納できる値に変換されます。 *resource_name*は**nvarchar (255)** 既定値はありません。 *resource_name*はバイナリ比較、したがっては現在のデータベースの照合順序の設定に関係なく大文字小文字を区別します。  
  
 [ @LockOwner=] '*lock_owner*'  
 ロックの所有者を指定します。これはロックが要求されたときの *lock_owner* 値です。 *lock_owner* は **nvarchar (32)** です。 この値は **Transaction** (既定値) または **Session** のいずれかです。 ときに、 *lock_owner*値は**トランザクション**により、既定または明示的に指定すると、sp_getapplock 必要がありますから実行するトランザクション内で。  
  
 [ @DbPrincipal=] '*database_principal*'  
 ユーザー、ロール、またはデータベース内のオブジェクトへのアクセス許可を持つアプリケーション ロールです。 関数を呼び出すには、*database_principal*、dbo、または固定データベース ロール db_owner のメンバーであることが必要です。 既定値はパブリックです。  
  
## <a name="return-code-values"></a>リターン コードの値  
 \>= 0 (成功) または < 0 (失敗)  
  
|値|結果|  
|-----------|------------|  
|0|ロックが正常に解放されました。|  
|-999 =|パラメーターの検証エラーまたはその他の呼び出しエラーです。|  
  
## <a name="remarks"></a>コメント  
 アプリケーションで、同じロック リソースに対して sp_getapplock が複数回呼び出される場合は、同じ回数だけ sp_releaseapplock を呼び出して、ロックを解放する必要があります。  
  
 サーバーが何らかの理由でシャット ダウンすると、ロックが解放されます。  
  
## <a name="permissions"></a>アクセス許可  
 public ロールのメンバーシップが必要です。  
  
## <a name="examples"></a>使用例  
 次の例では、リソースの現在のトランザクションに関連付けられているロックを解放する`Form1`で、`AdventureWorks2012`データベース。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_getapplock @DbPrincipal = 'dbo', @Resource = 'Form1',   
     @LockMode = 'Shared';  
EXEC sp_releaseapplock @DbPrincipal = 'dbo', @Resource = 'Form1';  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [APPLOCK_MODE &#40;TRANSACT-SQL&#41;](../../t-sql/functions/applock-mode-transact-sql.md)   
 [APPLOCK_TEST &#40;TRANSACT-SQL&#41;](../../t-sql/functions/applock-test-transact-sql.md)   
 [sp_getapplock &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-getapplock-transact-sql.md)  
  
  
