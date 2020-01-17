---
title: sp_addrolemember (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/30/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_addrolemember_TSQL
- sp_addrolemember
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addrolemember
ms.assetid: a583c087-bdb3-46d2-b9e5-3921b3e6d10b
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c9e0d3152c6d60faff4c1c42410374287bd7d111
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68030900"
---
# <a name="spaddrolemember-transact-sql"></a>sp_addrolemember (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  データベース ユーザー、データベース ロール、Windows ログイン、または Windows グループを、現在のデータベースのデータベース ロールに追加します。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 使用[ALTER ROLE](../../t-sql/statements/alter-role-transact-sql.md)代わりにします。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```
sp_addrolemember [ @rolename = ] 'role', [ @membername = ] 'security_account'  

```    
  
## <a name="arguments"></a>引数  
 [ @rolename=] '*ロール*'  
 現在のデータベース内のデータベース ロールの名前です。 *ロール*は、 **sysname**、既定値はありません。  
  
 [ @membername=] '*これ*'  
 セキュリティ アカウントは、ロールに追加されているされます。 *これ*は、 **sysname**、既定値はありません。 *これ*データベース ユーザー、データベース ロール、Windows ログイン、または Windows グループにすることができます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="remarks"></a>コメント  
 Sp_addrolemember を使用してロールに追加されたメンバーは、ロールの権限を継承します。 新しいメンバーが対応するデータベース ユーザー Windows レベルのプリンシパルである場合は、データベース ユーザーが作成されますが、ログインに完全にマップされません。 ログインが存在し、そのログインがデータベースへのアクセス権を持っていることを必ず確認してください。  
  
 ロールには、ロール自体をメンバーとして含めることはできません。 このような "循環" 定義は、1 つ以上の中間メンバーシップを介して間接的にメンバーシップが与えられる場合でも無効です。  
  
 sp_addrolemember では、固定データベース ロール、固定サーバー ロール、または dbo をロールに追加できません。
  
 Sp_addrolemember を使用してデータベース ロールにメンバーを追加するだけです。 サーバー ロールにメンバーを追加するには使用[sp_addsrvrolemember &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsrvrolemember-transact-sql.md)します。  
  
## <a name="permissions"></a>アクセス許可  
 可変データベース ロールにメンバーを追加するには、次のいずれかが必要です。  
  
-   Db_securityadmin ロールまたは db_owner 固定データベース ロールのメンバーシップ。  
  
-   ロールを所有するロールのメンバーシップ  
  
-   **ALTER ANY ROLE**権限または**ALTER**ロールに対する権限。  
  
 固定データベース ロールにメンバーを追加するには、db_owner 固定データベース ロールのメンバーシップが必要です。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-adding-a-windows-login"></a>A. Windows ログインの追加  
 次の例では、Windows ログイン`Contoso\Mary5`を`AdventureWorks2012`ユーザーとしてデータベース`Mary5`します。 ユーザー`Mary5`に追加し、`Production`ロール。  
  
> [!NOTE]  
>  `Contoso\Mary5` はデータベース [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] のデータベース ユーザー `Mary5` として設定されているので、ユーザー名 `Mary5` を指定する必要があります。 `Contoso\Mary5` のログインが存在しない場合、このステートメントは失敗します。 ドメインからログインを使用してテストします。  
  
```  
USE AdventureWorks2012;  
GO  
CREATE USER Mary5 FOR LOGIN [Contoso\Mary5] ;  
GO  
```  
  
### <a name="b-adding-a-database-user"></a>B. データベース ユーザーを追加します。  
 次の例は、データベース ユーザーを追加します。`Mary5`を、 `Production` 、現在のデータベースのデータベース ロール。  
  
```  
EXEC sp_addrolemember 'Production', 'Mary5';  
```  
  
## <a name="examples-includesspdwincludessspdw-mdmd"></a>例: [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-adding-a-windows-login"></a>C. Windows ログインの追加  
 次の例では、ログイン`LoginMary`を`AdventureWorks2008R2`ユーザーとしてデータベース`UserMary`します。 ユーザー`UserMary`に追加し、`Production`ロール。  
  
> [!NOTE]  
>  ログイン`LoginMary`はデータベース ユーザーと呼ばれます`UserMary`で、[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]データベース、ユーザー名`UserMary`指定する必要があります。 `Mary5` のログインが存在しない場合、このステートメントは失敗します。 ログインとユーザーは、通常同じ名前を指定します。 この例では、ユーザーとログインに影響を与えるアクションを区別するために別の名前を使用します。  
  
```  
-- Uses AdventureWorks  
  
CREATE USER UserMary FOR LOGIN LoginMary ;  
GO  
EXEC sp_addrolemember 'Production', 'UserMary'  
```  
  
### <a name="d-adding-a-database-user"></a>D. データベース ユーザーを追加します。  
 次の例は、データベース ユーザーを追加します。`UserMary`を、 `Production` 、現在のデータベースのデータベース ロール。  
  
```  
EXEC sp_addrolemember 'Production', 'UserMary'  
```  
  
## <a name="see-also"></a>関連項目  
 [セキュリティ ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addsrvrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsrvrolemember-transact-sql.md)   
 [sp_droprolemember の各&#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droprolemember-transact-sql.md)   
 [sp_grantdbaccess &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantdbaccess-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [データベース レベルのロール](../../relational-databases/security/authentication-access/database-level-roles.md)  
  
  
