---
title: Stored Procedures イベント カテゴリ | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Stored Procedures event category [SQL Server]
- SQL Server event classes, Stored Procedures event category
- event classes [SQL Server], Stored Procedures event category
ms.assetid: 71bebaa3-a05a-4695-b349-078cecd0949a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 47dc8180fd6c8f59050520477724ff8adbc46a6a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63061015"
---
# <a name="stored-procedures-event-category"></a>Stored Procedures イベント カテゴリ
  **Stored Procedures** イベント カテゴリには、一般的なストアド プロシージャ イベントが含まれています。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
|トピック|説明|  
|-----------|-----------------|  
|[RPC:Completed イベント クラス](rpc-completed-event-class.md)|リモート プロシージャ コール (RPC) が完了したことを示します。|  
|[PreConnect:Completed イベント クラス](preconnect-completed-event-class.md)|リソース ガバナー分類子関数の実行が終了したことを示します。|  
|[PreConnect:Starting イベント クラス](preconnect-starting-event-class.md)|リソース ガバナー分類子関数の実行が開始されたことを示します。|  
|[RPC Output Parameter イベント クラス](rpc-output-parameter-event-class.md)|リモート プロシージャ コールの実行後に、その出力パラメーターの値をトレースします。|  
|[RPC:Starting イベント クラス](rpc-starting-event-class.md)|リモート プロシージャ コールが開始されたことを示します。|  
|[SP:CacheHit イベント クラス](sp-cachehit-event-class.md)|ストアド プロシージャがキャッシュに存在することを示します。|  
|[SP:CacheInsert イベント クラス](sp-cacheinsert-event-class.md)|ストアド プロシージャがキャッシュに挿入されたことを示します。|  
|[SP:CacheMiss イベント クラス](sp-cachemiss-event-class.md)|ストアド プロシージャがキャッシュで見つからなかったことを示します。|  
|[SP:CacheRemove イベント クラス](sp-cacheremove-event-class.md)|ストアド プロシージャがキャッシュから削除されていることを示します。|  
|[SP:Completed イベント クラス](sp-completed-event-class.md)|ストアド プロシージャの実行が完了したことを示します。|  
|[SP:Recompile イベント クラス](sp-recompile-event-class.md)|ストアド プロシージャが再コンパイルされたことを示します。|  
|[SP:Starting イベント クラス](sp-starting-event-class.md)|ストアド プロシージャの実行が開始されたことを示します。|  
|[SP:StmtCompleted イベント クラス](sp-stmtcompleted-event-class.md)|ストアド プロシージャ内の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントが完了したことを示します。|  
|[SP:StmtStarting イベント クラス](sp-stmtstarting-event-class.md)|ストアド プロシージャ内の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントが開始されたことを示します。|  
  
## <a name="see-also"></a>関連項目  
 [拡張イベント](../extended-events/extended-events.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)  
  
  
