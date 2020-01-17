---
title: エラーと警告イベント カテゴリ
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- Errors and Warnings event category [SQL Server]
- SQL Server event classes, Errors and Warnings event category
- event classes [SQL Server], Errors and Warnings event category
ms.assetid: 249c19b5-af68-4433-80f6-337395176641
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4832910f00322875c334e16df77975a33106d214
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056426"
---
# <a name="errors-and-warnings-event-category-database-engine"></a>Errors and Warnings イベント カテゴリ (データベース エンジン)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  **Errors and Warnings** イベント カテゴリには、一般的なエラーおよび警告のイベントが含まれています。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
|トピック|[説明]|  
|-----------|-----------------|  
|[Attention イベント クラス](../../relational-databases/event-classes/attention-event-class.md)|**Attention** イベントが発生したことを示します。|  
|[Background Job Error イベント クラス](../../relational-databases/event-classes/background-job-error-event-class.md)|バックグラウンド ジョブが異常終了したことを示します。|  
|[Bitmap Warning イベント クラス](../../relational-databases/event-classes/bitmap-warning-event-class.md)|クエリでビットマップ フィルターが無効になっていることを示します。|  
|[Blocked Process Report イベント クラス](../../relational-databases/event-classes/blocked-process-report-event-class.md)|指定した時間より長い間タスクがブロックされていることを示します。|  
|[CPU Threshold Exceeded イベント クラス](../../relational-databases/event-classes/cpu-threshold-exceeded-event-class.md)|指定された CPU しきい値を超えるクエリがリソース ガバナーによって検出されたことを示します。|  
|[ErrorLog イベント クラス](../../relational-databases/event-classes/errorlog-event-class.md)|エラー イベントが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラー ログに記録されたことを示します。|  
|[EventLog イベント クラス](../../relational-databases/event-classes/eventlog-event-class.md)|イベントが Windows イベント ログに記録されたことを示します。|  
|[Exception イベント クラス](../../relational-databases/event-classes/exception-event-class.md)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]で例外が発生したことを示します。|  
|[Exchange Spill イベント クラス](../../relational-databases/event-classes/exchange-spill-event-class.md)|並列クエリ プランの通信バッファーが tempdb データベースに書き込まれたことを示します。|  
|[Execution Warnings イベント クラス](../../relational-databases/event-classes/execution-warnings-event-class.md)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ステートメントまたはストアド プロシージャの実行中にメモリ許可警告が発生したことを示します。|  
|[Hash Warning イベント クラス](../../relational-databases/event-classes/hash-warning-event-class.md)|ハッシュ処理中にハッシュの再帰またはハッシュの保留が発生したことを示します。|  
|[Missing Column Statistics イベント クラス](../../relational-databases/event-classes/missing-column-statistics-event-class.md)|オプティマイザーに役立つ列統計が使用できないことを示します。|  
|[Missing Join Predicate イベント クラス](../../relational-databases/event-classes/missing-join-predicate-event-class.md)|結合述語がないクエリが実行されていることを示します。|  
|[Sort Warnings イベント クラス](../../relational-databases/event-classes/sort-warnings-event-class.md)|並べ替え操作をメモリ内で処理できないことを示します。|  
|[User Error Message イベント クラス](../../relational-databases/event-classes/user-error-message-event-class.md)|ユーザーに対して表示されるエラー メッセージを表示します。|  
  
## <a name="see-also"></a>参照  
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)  
  
  
