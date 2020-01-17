---
title: Performance イベント カテゴリ | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- SQL Server event classes, Performance event category
- Performance event category [SQL Server]
- event classes [SQL Server], Performance event category
ms.assetid: 708f3585-d8be-4980-bbff-672d7c59397e
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b7f387145077e5a562279b6c72bc0f7eefadde36
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63023299"
---
# <a name="performance-event-category"></a>Performance イベント カテゴリ
  **Performance** イベント カテゴリを使用すると、 **Showplan** イベント クラス、および SQL DML (データ操作言語) の操作を実行したときに作成されるイベント クラスを監視できます。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
|トピック|説明|  
|-----------|-----------------|  
|[Auto Stats イベント クラス](auto-stats-event-class.md)|インデックス統計および列統計の自動更新が実行されたことを示します。|  
|[Degree of Parallelism &#40;7.0 Insert&#41; イベント クラス](degree-of-parallelism-7-0-insert-event-class.md)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で、直列プランまたは並列プランのいずれかを使用して SELECT、INSERT、UPDATE、または DELETE ステートメントが実行されたことを示します。 操作の実行に使用された CPU の数もレポートされます。|  
|[Performance Statistics イベント クラス](performance-statistics-event-class.md)|実行中のクエリのパフォーマンスを監視します。|  
|[Showplan All イベント クラス](showplan-all-event-class.md)|SQL ステートメント内の **Showplan** 操作を識別します。|  
|[Showplan All for Query Compile イベント クラス](showplan-all-for-query-compile-event-class.md)|**Showplan** 操作のコンパイル時間データを表示します。|  
|[Showplan Statistics Profile イベント クラス](showplan-statistics-profile-event-class.md)|クエリの推定コストを表示します。|  
|[Showplan XML イベント クラス](showplan-xml-event-class.md)|SQL ステートメント内の **Showplan** 操作を識別します。 このイベント クラスには、各イベントが整形式の XML ドキュメントとして格納されます。|  
|[Showplan XML for Query Compile イベント クラス](showplan-xml-for-query-compile-event-class.md)|**Showplan** 操作のコンパイル時間データを XML 形式で表示します。|  
|[Showplan XML Statistics Profile イベント クラス](showplan-xml-statistics-profile-event-class.md)|SQL ステートメントに関連付けられた **Showplan** 操作を識別します。 出力は XML ドキュメントです。|  
|[SQL:FullTextQuery イベント クラス](sql-fulltextquery-event-class.md)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でフルテキスト クエリが実行されたことを示します。|  
|[Plan Guide Successful イベント クラス](plan-guide-successful-event-class.md)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でプラン ガイドを含むクエリまたはバッチの実行プランが正常に生成されたことを示します。|  
|[Plan Guide Unsuccessful イベント クラス](plan-guide-unsuccessful-event-class.md)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でプラン ガイドを含むクエリまたはバッチの実行プランを生成できなかったことを示します。|  
  
## <a name="see-also"></a>参照  
 [拡張イベント](../extended-events/extended-events.md)  
  
  
