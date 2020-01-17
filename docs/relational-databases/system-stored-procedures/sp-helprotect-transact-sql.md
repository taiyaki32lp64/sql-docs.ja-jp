---
title: sp_helprotect (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helprotect
- sp_helprotect_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helprotect
ms.assetid: faaa3e40-1c95-43c2-9fdc-c61a1d3cc0c3
author: stevestein
ms.author: sstein
ms.openlocfilehash: 7db43df5d500e56e58e3e8465ac03158fe7e4d21
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67997473"
---
# <a name="sphelprotect-transact-sql"></a>sp_helprotect (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  現在のデータベース内のオブジェクトは、ユーザーのアクセス許可またはステートメントの権限に関する情報を含むレポートを返します。  
  
> [!IMPORTANT]  
>  **sp_helprotect**で導入されたセキュリティ保護可能な情報は返されません[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]します。 使用[sys.database_permissions](../../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md)と[fn_builtin_permissions](../../relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql.md)代わりにします。  
  
 固定サーバー ロールまたは固定データベース ロールに常に割り当てられる権限は表示されません。 ログインまたはロールのメンバーシップに基づいて権限が与えられるユーザーは含まれません。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_helprotect [ [ @name = ] 'object_statement' ]   
     [ , [ @username = ] 'security_account' ]   
     [ , [ @grantorname = ] 'grantor' ]   
     [ , [ @permissionarea = ] 'type' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @name = ] 'object_statement'` 現在のデータベースまたはレポートへのアクセス許可のあるステートメント内のオブジェクトの名前です。 *object_statement*は**nvarchar (776)** の既定値は NULL には、すべてのオブジェクトとステートメントの権限が返されます。 値がオブジェクト (テーブル、ビュー、ストアド プロシージャ、または拡張ストアド プロシージャ) の場合、現在のデータベースで有効なオブジェクトがあります。 オブジェクト名は、フォームで、所有者の修飾子を含めることができます_所有者_ **.** _オブジェクト_します。  
  
 場合*object_statement*ステートメント、CREATE ステートメントであることができます。  
  
`[ @username = ] 'security_account'` アクセス許可を返す基になるプリンシパルの名前です。 *これ*は**sysname**の既定値は NULL には、現在のデータベースにすべてのプリンシパルが返されます。 *これ*現在のデータベースに存在する必要があります。  
  
`[ @grantorname = ] 'grantor'` アクセス許可を付与するプリンシパルの名前です。 *権限の許可者*は**sysname**の既定値は NULL には、データベース内のすべてのプリンシパルにより許可された権限のすべての情報が返されます。  
  
`[ @permissionarea = ] 'type'` オブジェクトのアクセス許可を表示するかどうかを示す文字の文字列 (文字の文字列**o**)、ステートメント権限 (文字の文字列**s**)、またはその両方 (**os**)。 *型*は**varchar (10)** 、既定値は**os**します。 *型*の任意の組み合わせは、 **o**と**s**、または間の空白またはコンマなし**o**と**s**します。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**[所有者]**|**sysname**|オブジェクトの所有者の名前です。|  
|**Object**|**sysname**|オブジェクト名。|  
|**権限付与対象ユーザー**|**sysname**|権限が許可されたプリンシパルの名前。|  
|**Grantor**|**sysname**|指定した権限付与対象ユーザーに権限を許可したプリンシパルの名前。|  
|**ProtectType**|**nvarchar(10)**|保護の種類の名前。<br /><br /> 許可の付与取り消し|  
|**操作**|**nvarchar(60)**|アクセス許可の名前。 有効な権限ステートメントは、オブジェクトの種類によって異なります。|  
|**列**|**sysname**|権限の種類:<br /><br /> All = オブジェクトの現在の列すべてに対する権限<br /><br /> 新しい変更する (を ALTER ステートメントを使用)、オブジェクトに対する今後すべての新しい列のに対する権限を = です。<br /><br /> All+New = All と New を組み合わせた権限<br /><br /> 権限の種類が列に適用されない場合は、ピリオドを返します。|  
  
## <a name="remarks"></a>コメント  
 次のプロシージャでは、すべてのパラメーターが省略可能です。 パラメーターなしで実行される場合`sp_helprotect`現在のデータベースで許可または拒否されているすべての権限を表示します。  
  
 すべてではなく一部のパラメーターだけを指定する場合は、特定のパラメーターを示す名前付きのパラメーターを使用するか、プレースホルダーとして `NULL` を使用します。 たとえば、データベース所有者のすべての権限をレポートする (`dbo`)、次を実行します。  
  
```  
EXEC sp_helprotect NULL, NULL, dbo;  
```  
  
 または  
  
```  
EXEC sp_helprotect @grantorname = 'dbo';  
```  
  
 権限カテゴリ、所有者、オブジェクト、権限付与対象ユーザー、権限の許可者、保護の種類のカテゴリ、保護の種類、アクション、および列順序 ID で並べ替えがレポートされます。  
  
## <a name="permissions"></a>アクセス許可  
 ロール **public** のメンバーシップが必要です。  
  
 返される情報は、メタデータへのアクセスの制限が適用されます。 これで、権限がプリンシパルにないエンティティは表示されません。 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-listing-the-permissions-for-a-table"></a>A. テーブルの権限を一覧表示  
 次の例では、テーブル `titles` の権限に関するレポートを一覧表示します。  
  
```  
EXEC sp_helprotect 'titles';  
```  
  
### <a name="b-listing-the-permissions-for-a-user"></a>B. ユーザーに対する権限を一覧表示する  
 次の例はそのユーザーのすべての権限を一覧表示`Judy`現在のデータベースにします。  
  
```  
EXEC sp_helprotect NULL, 'Judy';  
```  
  
### <a name="c-listing-the-permissions-granted-by-a-specific-user"></a>C. 特定のユーザーに与えられた権限を一覧表示  
 次の例では、現在のデータベース内でユーザー `Judy` に許可されたすべての権限を一覧表示します。指定しないパラメーターについては、プレースホルダーとして `NULL` を使用します。  
  
```  
EXEC sp_helprotect NULL, NULL, 'Judy';  
```  
  
### <a name="d-listing-the-statement-permissions-only"></a>D. ステートメント権限のみを一覧表示  
 次の例では、現在のデータベース内のすべてのステートメント権限を表示します。指定しないパラメーターについては、プレースホルダーとして `NULL` を使用します。  
  
```  
EXEC sp_helprotect NULL, NULL, NULL, 's';   
```  
  
### <a name="e-listing-the-permissions-for-a-create-statement"></a>e. CREATE ステートメントの権限だけを一覧表示する  
 次の例では、CREATE TABLE 権限が与えられているすべてのユーザーが一覧表示します。  
  
```  
EXEC sp_helprotect @name = 'CREATE TABLE';  
```  
  
## <a name="see-also"></a>関連項目  
 [セキュリティ ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [DENY &#40;Transact-SQL&#41;](../../t-sql/statements/deny-transact-sql.md)   
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [REVOKE &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
