---
title: イベント ペアリング ターゲット |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- pairing target [SQL Server extended events]
- event pairing target
- targets [SQL Server extended events], pairing target
ms.assetid: 3c87dcfb-543a-4bd8-a73d-1390bdf4ffa3
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 39e444077c3dbe27ae243e4292b7a047e21de2b9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66064846"
---
# <a name="event-pairing-target"></a>イベント ペアリング ターゲット
  イベント ペアリング ターゲットは、各イベントに存在する単一列または複数列のデータを使って 2 つのイベントを照合します。 ロックの取得とロックの解放など、対で発生するイベントが数多く存在します。 イベント シーケンスが対で発生した後は、両方のイベントが破棄されます。 一対のイベントを破棄することによって、取得されたまま解放されていないロックを容易に検出できます。  
  
 イベント レベルのフィルターを使用すると、設定済みの条件に合致しないイベントだけを、ペアリング ターゲットを使ってキャプチャできます。  
  
 イベント ペアリング ターゲットを使用する場合は、照合に使用する列のシーケンスのほか、照合する 2 つのイベントを選択できます。 このシーケンス内のすべての列は、同じ型であることが必要です。  
  
 次の表では、イベント ペアリングの構成に使用できるオプションについて説明します。  
  
|オプション|指定できる値|説明|  
|------------|--------------------|-----------------|  
|begin_event|現在のセッションに存在する任意のイベント名。|対で発生するイベントのうち最初に発生するイベントの名前です。|  
|end_event|現在のセッションに存在する任意のイベント名。|対で発生するイベントのうち最後に発生するイベントの名前です。|  
|begin_matching_columns|コンマ区切りで順に指定された列名。|照合に使用する列です。|  
|end_matching_columns|コンマ区切りで順に指定された列名。|照合に使用する列です。|  
|begin_matching_actions|コンマ区切りで順に指定されたアクション。|照合に使用するアクションです。|  
|end_matching_actions|コンマ区切りで順に指定されたアクション。|照合に使用するアクションです。|  
|respond_to_memory_pressure|次のいずれかの値です。<br /><br /> 0 = 応答しません。<br /><br /> 1 = メモリが不足している場合、対になっていないイベントを新たに追加することはしません。|ターゲットは、メモリ イベントに応答します。 1 に設定した場合、サーバーのメモリが不足すると、それまで保持されていた、対になっていない情報は削除されます。|  
|max_orphans||ターゲットで収集される、対になっていないイベントの合計数を指定します。 制限に達すると、対になっていないイベントは先入れ先出し (FIFO) 順で削除されます。 既定値は 10,000 です。|  
  
 イベントに関連付けられているすべてのデータはキャプチャされて、その後のペアリングに備えて保存されます。 また、アクションによって追加されたデータも収集されます。 収集されたイベント データはメモリに格納されるため、格納できるサイズには上限があります。 この制限は、システムの容量とアクティビティに依存します。 使用メモリ量は利用可能なシステム リソースに基づくため、使用可能な最大メモリ量をパラメーターとして指定することはありません。 システム リソースが不足した場合、それまで保持されていた、対になっていないイベントは破棄されます。 イベントが対になっておらず破棄された場合、照合イベントは、対になっていないイベントとして発生します。  
  
 対になっていないイベントは、ペアリング ターゲットによって XML 形式にシリアル化されます。 この形式は、いずれのスキーマにも準拠しません。 この形式に含まれる要素は 2 種類だけです。 **\<対になっていない >** 要素は 1 が続く、ルートになります。 **\<イベント >** 現在追跡されている各ペアになっていないイベントの要素。 **\<イベント >** 要素には、対になっていないイベントの名前を含む 1 つの属性が含まれています。  
  
## <a name="adding-the-target-to-a-session"></a>セッションへのターゲットの追加  
 ペア照合ターゲットを拡張イベント セッションに追加するには、イベント セッションの作成時または変更時に次のステートメントを含める必要があります。  
  
```  
ADD TARGET package0.pair_matching   
```  
  
 この後に、最初と最後のイベント、および照合するアクションまたは列を定義する SET ステートメントを続けます。 以下は、sqlserver.lock_acquired イベントと sqlserver.lock_released イベントのペア照合のサンプル構文です。  
  
```  
   ( SET begin_event = 'sqlserver.lock_acquired',  
      begin_matching_columns = 'database_id, resource_0, resource_1, resource_2, transaction_id, mode',  
      end_event = 'sqlserver.lock_released',  
      end_matching_columns = 'database_id, resource_0, resource_1, resource_2, transaction_id, mode',  
   respond_to_memory_pressure = 1)  
```  
  
 詳細については、「 [ロックを保持しているクエリの特定](../relational-databases/extended-events/determine-which-queries-are-holding-locks.md)」を参照してください。  
  
## <a name="reviewing-the-target-output"></a>ターゲット出力の確認  
 ペア照合ターゲットの出力を確認するには、次のクエリを使用します。 *session_name* をイベント セッションの名前に置き換えてください。  
  
```  
SELECT name, target_name, CAST(xet.target_data AS xml)  
FROM sys.dm_xe_session_targets AS xet  
JOIN sys.dm_xe_sessions AS xe  
   ON (xe.address = xet.event_session_address)  
WHERE xe.name = 'session_name'  
```  
  
 次の例は、ペアリング ターゲットの出力形式を示しています。  
  
```  
<unpaired truncated = "0" matchedCount = "[matched count]" memoryPressureDroppedCount = " [lost count]">  
    <event name  = "[event name]" package = "[package]" id= "[event ID value]" version = "[event version]">  
    <data name = "[column name]">   
    <type name = "[column type]" package = "[type package]" />   
    <value>[column value]</value>  
    <text value>[text value]</text>>  
        </data>  
    </event>  
</unpaired>  
```  
  
## <a name="see-also"></a>関連項目  
 [SQL Server 拡張イベント ターゲット](../../2014/database-engine/sql-server-extended-events-targets.md)   
 [sys.dm_xe_session_targets &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-session-targets-transact-sql)   
 [CREATE EVENT SESSION &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-event-session-transact-sql)   
 [ALTER EVENT SESSION &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-event-session-transact-sql)  
  
  
