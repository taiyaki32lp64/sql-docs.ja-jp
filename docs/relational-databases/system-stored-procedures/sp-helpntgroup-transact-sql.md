---
title: sp_helpntgroup (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helpntgroup
- sp_helpntgroup_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpntgroup
ms.assetid: 02b4f7c1-480a-436c-8bae-7a2488be45d2
author: stevestein
ms.author: sstein
ms.openlocfilehash: fcc4a42307ccb11923460bb9c01c5cf7bdd8f8df
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68133675"
---
# <a name="sphelpntgroup-transact-sql"></a>sp_helpntgroup (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  現在のデータベース内のアカウントを持つ Windows グループに関する情報を報告します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_helpntgroup [ [ @ntname= ] 'name' ]   
```  
  
## <a name="arguments"></a>引数  
`[ @ntname = ] 'name'` Windows グループの名前です。 *名前* は **sysname** 、既定値は NULL です。 *名前*現在のデータベースにアクセスできる有効な Windows グループである必要があります。 場合*名前*が指定されていない、現在のデータベースへのアクセス権を持つすべての Windows グループは、出力に含めます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**Nt グループ名**|**sysname**|Windows グループの名前。|  
|**NTGroupId**|**smallint**|グループの識別子 (ID)。|  
|**SID**|**varbinary(85)**|セキュリティ識別子 (SID) **NTGroupName**します。|  
|**HasDbAccess**|**int**|1 = Windows グループには、データベースにアクセスします。|  
  
## <a name="remarks"></a>コメント  
 一覧を表示する、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]現在のデータベース内のロールを使用して、 **sp_helprole**します。  
  
## <a name="permissions"></a>アクセス許可  
 ロール **public** のメンバーシップが必要です。  
  
## <a name="examples"></a>使用例  
 次の例では、現在のデータベースへのアクセス権を持つ Windows グループの一覧を出力します。  
  
```  
EXEC sp_helpntgroup;  
```  
  
## <a name="see-also"></a>関連項目  
 [セキュリティ ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_grantdbaccess &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantdbaccess-transact-sql.md)   
 [sp_helprole &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helprole-transact-sql.md)   
 [sp_revokedbaccess &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revokedbaccess-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
