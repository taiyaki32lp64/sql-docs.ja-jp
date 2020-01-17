---
title: sp_helpmergearticleconflicts (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpmergearticleconflicts
- sp_helpmergearticleconflicts_TSQL
helpviewer_keywords:
- sp_helpmergearticleconflicts
ms.assetid: 4678a2b9-9a5f-4193-a20d-2e11fc896c3a
author: stevestein
ms.author: sstein
ms.openlocfilehash: 85e75e1ce52866eb04b3c410f021db8de392239a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68122327"
---
# <a name="sphelpmergearticleconflicts-transact-sql"></a>sp_helpmergearticleconflicts (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  競合しているパブリケーションでアーティクルを返します。 このストアド プロシージャは、パブリッシャー側でパブリケーション データベースについて実行されます。または、サブスクライバー側でマージ サブスクリプション データベースについて実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_helpmergearticleconflicts [ [ @publication = ] 'publication' ]  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @publisher_db = ] 'publsher_db' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'` マージ パブリケーションの名前です。*パブリケーション*は**sysname**、既定値は **%** 、競合するデータベース内のすべてのアーティクルが返されます。  
  
`[ @publisher = ] 'publisher'` パブリッシャーの名前です。*パブリッシャー*は**sysname**、既定値は NULL です。  
  
`[ @publisher_db = ] 'publisher_db'` パブリッシャー データベースの名前です。*publisher_db*は**sysname**、既定値は NULL です。  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**article**|**sysname**|アーティクルの名前。|  
|**source_owner**|**sysname**|ソース オブジェクトの所有者です。|  
|**source_object**|**nvarchar(386)**|ソース オブジェクトの名前です。|  
|**conflict_table**|**nvarchar(258)**|挿入または更新の競合を記録するテーブルの名前。|  
|**guidcolname**|**sysname**|ソース オブジェクトの RowGuidCol の名前。|  
|**centralized_conflicts**|**int**|かどうかの競合レコードは、指定されたパブリッシャーに格納されます。|  
  
 場合、アーティクルは削除競合と no のみ**conflict_table**行の名前、 **conflict_table**結果セットが NULL です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_helpmergearticleconflicts**はマージ レプリケーションで使用します。  
  
## <a name="permissions"></a>アクセス許可  
 メンバーのみ、 **sysadmin**固定サーバー ロールおよび**db_owner**固定データベース ロールが実行できる**sp_helpmergearticleconflicts**します。  
  
## <a name="see-also"></a>関連項目  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
