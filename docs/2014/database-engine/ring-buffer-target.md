---
title: リング バッファー ターゲット |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- targets [SQL Server extended events], ring buffer target
- ring buffer target [SQL Server extended events]
ms.assetid: 54494e11-b56b-43b7-aa5e-c8724e56b251
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 920cc72a9d99da61575249559661c01826b0e89b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66088957"
---
# <a name="ring-buffer-target"></a>リング バッファー ターゲット
  リング バッファー ターゲットは、メモリにイベント データを一時的に保持します。 このターゲットでは、2 種類のモードのいずれかでイベントを管理できます。  
  
-   1 つ目のモードは厳密な先入れ先出し (FIFO) です。このモードでは、ターゲットに割り当てられたメモリがすべて使用されると、最も古いイベントが破棄されます。 このモード (既定値) では、occurrence_number オプションは 0 に設定されます。  
  
-   2 つ目のモードはイベントごとの FIFO です。このモードでは、各種イベントが指定した数だけ保持されます。 このモードで、ターゲットに割り当てられたすべてのメモリを使用すると、各型の最も古いイベントは破棄されます。 occurrence_number オプションを構成して、種類ごとに保持するイベントの数を指定できます。  
  
 次の表では、リング バッファー ターゲットの構成に使用できるオプションについて説明します。  
  
|オプション|指定できる値|説明|  
|------------|--------------------|-----------------|  
|max_memory|任意の 32 ビット整数。 この値は省略可能です。|使用するメモリの最大量 (KB)。 max_event_limit と max_memory のうち先に制限に達した方に基づいて、既存のイベントが削除されます。 最大の値は、4,194, 303 KB です。 SQL Server では、その他のメモリ コンシューマーの影響を与える可能性があります。、リング バッファーのサイズを GB の範囲の制限に設定する前に、慎重に検討を行う必要があります。|  
|max_event_limit|任意の 32 ビット整数。 この値は省略可能です。|ring_buffer に保持されるイベントの最大数。 max_event_limit と max_memory のうち先に制限に達した方に基づいて、既存のイベントが削除されます。 既定値は 1000 です。|  
|occurrence_number|次のいずれかの値です。<br /><br /> 0 (既定値) = ターゲットに割り当てられたメモリがすべて使用されると、最も古いイベントが破棄されます。<br /><br /> 任意の 32 ビット整数の種類ごとにイベントごとの FIFO に基づいて破棄されるまで保持するイベントの数を = です。<br /><br /> <br /><br /> この値は省略可能です。|使用する FIFO モード。0 を超える値に設定した場合は、種類ごとにバッファーに保持するイベントの数を表します。|
| &nbsp; | &nbsp; | &nbsp; |
  
## <a name="adding-the-target-to-a-session"></a>セッションへのターゲットの追加  
 リング バッファー ターゲットを拡張イベント セッションに追加するには、イベント セッションの作成時または変更時に次のステートメントを含める必要があります。  
  
```sql
ADD TARGET package0.ring_buffer  
```  
  
## <a name="reviewing-the-target-output"></a>ターゲット出力の確認  
 リング バッファー ターゲットの出力を確認するには、次のクエリを使用します。 *session_name* をイベント セッションの名前に置き換えてください。  
  
```sql
SELECT name, target_name, CAST(xet.target_data AS xml)  
FROM sys.dm_xe_session_targets AS xet  
JOIN sys.dm_xe_sessions AS xe  
   ON (xe.address = xet.event_session_address)  
WHERE xe.name = 'session_name'  
```  
  
 次の例は、リング バッファー ターゲットの出力形式を示しています。  
  
```  
<RingBufferTarget eventsPerSec="" processingTime="" totalEventsProcessed="" eventCount="" droppedCount="" memoryUsed="">  
 <event name="" package="" id="" version="" timestamp="">  
    <data name="">  
      <type name="" package="" />  
      <value></value>  
      <text></text>  
    </data>  
    <action name="" package="">  
      <type name="" package="" />  
      <value></value>  
      <text></text>  
    </action>  
  </event>  
</RingBufferTarget>  
```


## <a name="see-also"></a>関連項目

- [SQL Server 拡張イベント ターゲット](../../2014/database-engine/sql-server-extended-events-targets.md)
- [sys.dm_xe_session_targets &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-session-targets-transact-sql?view=sql-server-2016)
- [CREATE EVENT SESSION &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-event-session-transact-sql?view=sql-server-2016)
- [ALTER EVENT SESSION &#40;Transact-SQL&#41;](https://docs.microsoft.com/sql/t-sql/statements/alter-event-session-transact-sql?view=sql-server-2016)

