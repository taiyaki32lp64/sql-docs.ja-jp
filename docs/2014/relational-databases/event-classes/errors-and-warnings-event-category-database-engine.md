---
title: Errors and Warnings イベント カテゴリ (データベース エンジン) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Errors and Warnings event category [SQL Server]
- SQL Server event classes, Errors and Warnings event category
- event classes [SQL Server], Errors and Warnings event category
ms.assetid: 249c19b5-af68-4433-80f6-337395176641
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b86b68b0e7273a275c8dd1bd00fe99a7c462a27d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62662628"
---
# <a name="errors-and-warnings-event-category-database-engine"></a>Errors and Warnings イベント カテゴリ (データベース エンジン)
  **Errors and Warnings** イベント カテゴリには、一般的なエラーおよび警告のイベントが含まれています。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
|トピック|説明|  
|-----------|-----------------|  
|[Attention イベント クラス](attention-event-class.md)|**Attention** イベントが発生したことを示します。|  
|[Background Job Error イベント クラス](background-job-error-event-class.md)|バックグラウンド ジョブが異常終了したことを示します。|  
|[Bitmap Warning イベント クラス](bitmap-warning-event-class.md)|クエリでビットマップ フィルターが無効になっていることを示します。|  
|[Blocked Process Report イベント クラス](blocked-process-report-event-class.md)|指定した時間より長い間タスクがブロックされていることを示します。|  
|[CPU Threshold Exceeded イベント クラス](cpu-threshold-exceeded-event-class.md)|指定された CPU しきい値を超えるクエリがリソース ガバナーによって検出されたことを示します。|  
|[ErrorLog イベント クラス](errorlog-event-class.md)|エラー イベントが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラー ログに記録されたことを示します。|  
|[EventLog イベント クラス](eventlog-event-class.md)|イベントが Windows イベント ログに記録されたことを示します。|  
|[Exception イベント クラス](exception-event-class.md)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]で例外が発生したことを示します。|  
|[Exchange Spill イベント クラス](exchange-spill-event-class.md)|並列クエリ プランの通信バッファーが tempdb データベースに書き込まれたことを示します。|  
|[Execution Warnings イベント クラス](execution-warnings-event-class.md)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ステートメントまたはストアド プロシージャの実行中にメモリ許可警告が発生したことを示します。|  
|[Hash Warning イベント クラス](hash-warning-event-class.md)|ハッシュ処理中にハッシュの再帰またはハッシュの保留が発生したことを示します。|  
|[Missing Column Statistics イベント クラス](missing-column-statistics-event-class.md)|オプティマイザーに役立つ列統計が使用できないことを示します。|  
|[Missing Join Predicate イベント クラス](missing-join-predicate-event-class.md)|結合述語がないクエリが実行されていることを示します。|  
|[Sort Warnings イベント クラス](sort-warnings-event-class.md)|並べ替え操作をメモリ内で処理できないことを示します。|  
|[User Error Message イベント クラス](user-error-message-event-class.md)|ユーザーに対して表示されるエラー メッセージを表示します。|  
  
## <a name="see-also"></a>参照  
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)  
  
  
