---
title: MSmerge_genhistory (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_genhistory_TSQL
- MSmerge_genhistory
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_genhistory system table
ms.assetid: 475d08ae-eb8b-49de-afd6-33c96ab8004d
author: stevestein
ms.author: sstein
ms.openlocfilehash: bf9c38fe71c1282b19b947fc1771714dd138c45a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68017702"
---
# <a name="msmerge_genhistory-transact-sql"></a>MSmerge_genhistory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSmerge_genhistory**テーブルには、サブスクライバーが保有期間) 以内について認識している各ジェネレーションの 1 つの行が含まれます。 交換中に共通する generation が送信されないようにして、バックアップから復元するサブスクライバーを再同期に使用されます。 このテーブルは、パブリケーション データベースとサブスクリプション データベースに保存されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**guidsrc**|**uniqueidentifier**|サブスクライバーの generation 値によって識別される変更のグローバル識別子です。|  
|**pubid**|**uniqueidentifier**|パブリケーションの識別子です。|  
|**generation**|**bigint**|Generation 値です。|  
|**art_nick**|**int**|アーティクルのニックネームです。|  
|**nicknames**|**varbinary(1001)**|この generation 値を持っていることが既に認識されている他のサブスクライバーのニックネームの一覧です。 その変更を既に認識しているサブスクライバーに、generation 値を送信することを防ぐために使用します。 ニックネーム一覧内のニックネームは、検索をより効率的に並べ替えられた順序で保持されます。 このフィールドに収まるを超えるニックネームがある場合は、この最適化からいない活用します。|  
|**coldate**|**datetime**|現在の generation 値がテーブルに追加された日付です。|  
|**genstatus**|**tinyint**|次のように、世代の状態:<br /><br /> **0**開くを = です。<br /><br /> **1** = 終了します。<br /><br /> **2** = クローズし、別のサブスクライバーで発生します。|  
|**changecount**|**int**|特定のジェネレーションに反映される変更の数|  
  
## <a name="see-also"></a>関連項目  
 [レプリケーション テーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
