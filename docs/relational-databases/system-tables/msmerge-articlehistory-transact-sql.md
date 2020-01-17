---
title: MSmerge_articlehistory (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_articlehistory
- MSmerge_articlehistory_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_articlehistory system table
ms.assetid: 2870e7ea-dbec-4636-9171-c2cee96018ac
author: stevestein
ms.author: sstein
ms.openlocfilehash: 96b6c2599920c8d251b6d421cc18dc43c82fe521
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67907253"
---
# <a name="msmerge_articlehistory-transact-sql"></a>MSmerge_articlehistory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSmerge_articlehistory**テーブル アーティクルに変更が行われる各アーティクルに対して 1 つの行と、マージ エージェントの同期セッション中に加えられた変更を追跡します。 このテーブルは、ディストリビューション データベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**session_id**|**int**|マージ エージェント ジョブ セッションの ID、 [MSmerge_sessions](../../relational-databases/system-tables/msmerge-sessions-transact-sql.md)システム テーブル。|  
|**phase_id**|**int**|次のいずれかの同期セッションのフェーズ:<br /><br /> **1** = アップロードします。<br /><br /> **2** = ダウンロードします。<br /><br /> **4**クリーンアップを = です。<br /><br /> **5** = シャット ダウンします。<br /><br /> **6**スキーマの変更を = です。<br /><br /> **7** BCP を = です。|  
|**article_name**|**sysname**|変更が行われるアーティクルの名前。|  
|**start_time**|**datetime**|エージェントがアーティクルの処理を開始したときの時刻。|  
|**duration**|**int**|エージェントが秒単位で、アーティクルを処理する時間の長さ。|  
|**inserts**|**int**|同期中に特定のアーティクルに適用されている挿入の数。 この値は、同期処理中に 1 ずつ増分され、終了値が合計数を表します。|  
|**updates**|**int**|同期中に特定のアーティクルに適用された更新数です。 この値は、同期処理中に 1 ずつ増分され、終了値が合計数を表します。|  
|**deletes**|**int**|同期中に特定のアーティクルに適用されている削除の数。 この値は、同期処理中に 1 ずつ増分され、終了値が合計数を表します。|  
|**conflicts**|**int**|同期中に発生した競合の数。 この値は、同期処理中に 1 ずつ増分され、終了値が合計数を表します。|  
|**conflicts_resolved**|**int**|解決された同期中に発生した競合の数。 この値は、同期処理中に 1 ずつ増分され、終了値が合計数を表します。|  
|**rows_retried**|**int**|同期中に再試行が失敗した行の数。 この値は、同期処理中に 1 ずつ増分され、終了値が合計数を表します。|  
|**percent_complete**|**decimal**|マージ エージェントがアーティクルで、セッション中に費やした総同期時間の割合。 セッションが完了するまで、この値は NULL です。|  
|**estimated_changes**|**int**|アーティクルに適用する必要がある行の変更数の見積もり。|  
|**relative_cost**|**decimal**|セッション全体の時間の合計このアーティクルの変更を適用するに費やされた時間。|  
  
## <a name="see-also"></a>関連項目  
 [レプリケーション テーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
