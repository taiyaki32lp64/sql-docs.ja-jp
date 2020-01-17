---
title: sp_helprolemember (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helprolemember_TSQL
- sp_helprolemember
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helprolemember
ms.assetid: 42797510-aa5d-4564-85ac-27418419af9c
author: stevestein
ms.author: sstein
ms.openlocfilehash: 2ac7ec92a47f56982300e81395d24fc5b197ed64
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67997492"
---
# <a name="sphelprolemember-transact-sql"></a>sp_helprolemember (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  現在のデータベースに含まれるロールの直接的なメンバーに関する情報を返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_helprolemember [ [ @rolename = ] 'role' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @rolename = ] ' role '` 現在のデータベース内のロールの名前です。 *ロール*は**sysname**、既定値は NULL です。 *ロール*現在のデータベースに存在する必要があります。 場合*ロール*が指定されていない、現在のデータベースから少なくとも 1 つのメンバーが含まれているすべてのロールが返されます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**DbRole**|**sysname**|現在のデータベース ロールの名前。|  
|**メンバー名**|**sysname**|メンバーの名前**DbRole します。**|  
|**MemberSID**|**varbinary(85)**|セキュリティ識別子**MemberName します。**|  
  
## <a name="remarks"></a>コメント  
 データベースには、入れ子になったロールが含まれている場合**MemberName**ロールの名前があります。 **sp_helprolemember**入れ子になったロールを介して取得されたメンバーシップは表示されません。 たとえば、Role1 のメンバーである User1 Role1、Role2 のメンバーである場合`EXEC sp_helprolemember 'Role2'`; は、Role1 が Role1 のメンバーではなくを返します (この例では、User1)。 入れ子になったメンバーシップを返すを実行する必要があります**sp_helprolemember**入れ子になった各ロールの繰り返しです。  
  
 使用**sp_helpsrvrolemember**固定サーバー ロールのメンバーを表示します。  
  
 使用[IS_ROLEMEMBER &#40;TRANSACT-SQL&#41; ](../../t-sql/functions/is-rolemember-transact-sql.md)指定されたユーザー ロールのメンバーシップを確認します。  
  
## <a name="permissions"></a>アクセス許可  
 ロール **public** のメンバーシップが必要です。  
  
## <a name="examples"></a>使用例  
 次の例では、ロール `Sales` のメンバーを表示します。  
  
```  
EXEC sp_helprolemember 'Sales';  
```  
  
## <a name="see-also"></a>関連項目  
 [セキュリティ ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)   
 [sp_droprolemember の各&#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droprolemember-transact-sql.md)   
 [sp_helprole &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helprole-transact-sql.md)   
 [sp_helpsrvrolemember &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsrvrolemember-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
