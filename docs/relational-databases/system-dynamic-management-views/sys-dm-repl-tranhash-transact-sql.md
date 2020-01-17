---
title: sys.dm_repl_tranhash (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_repl_tranhash
- sys.dm_repl_tranhash_TSQL
- dm_repl_tranhash_TSQL
- dm_repl_tranhash
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_repl_tranhash dynamic management view
ms.assetid: 0cc52338-e805-4ed4-9835-b19bbf72448e
author: stevestein
ms.author: sstein
ms.openlocfilehash: 0c44c5c08dc46da5a0f2f3dfd2c53ab6cb20f27d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68067874"
---
# <a name="sysdmrepltranhash-transact-sql"></a>sys.dm_repl_tranhash (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  トランザクション パブリケーションでレプリケートされるトランザクションに関する情報を返します。  
  
|column_name|data_type|description|  
|------------------|----------------|-----------------|  
|**buckets**|**bigint**|ハッシュ テーブル内のバケットの数。|  
|**hashed_trans**|**bigint**|現在のバッチでレプリケートされるコミットされたトランザクションの数。|  
|**completed_trans**|**bigint**|トランザクションの数は、これまでに完了します。|  
|**compensated_trans**|**bigint**|部分ロールバックを含むトランザクションの数。|  
|**first_begin_lsn**|**nvarchar(64)**|現在のバッチ内のログ シーケンス番号 (LSN) が最も早い開始します。|  
|**last_commit_lsn**|**nvarchar(64)**|現在のバッチでコミットした lsn 最後です。|  
  
## <a name="permissions"></a>アクセス許可  
 呼び出すパブリケーション データベースに対する VIEW DATABASE STATE 権限が必要**dm_repl_tranhash**します。  
  
## <a name="remarks"></a>コメント  
 情報は、レプリケーション アーティクル キャッシュに現在読み込まれているレプリケートされたデータベース オブジェクトに対してのみ返されます。  
  
## <a name="see-also"></a>関連項目  
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [レプリケーション関連の動的管理ビュー &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/replication-related-dynamic-management-views-transact-sql.md)  
  
  
