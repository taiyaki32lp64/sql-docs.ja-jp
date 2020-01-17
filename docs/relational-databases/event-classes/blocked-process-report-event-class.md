---
title: Blocked Process Report イベント クラス | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- Blocked Process Report event class
ms.assetid: e8acb408-938d-4b36-81dd-04f087410cc5
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 57bd71b3f066b8b392371af0e49693f9f19e6b7a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67999826"
---
# <a name="blocked-process-report-event-class"></a>Blocked Process Report イベント クラス
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  **Blocked Process Report** イベント クラスは、指定された時間より長い間タスクがブロックされていることを示します。 このイベント クラスには、システム タスクやデッドロックを検出できないリソースを待機しているタスクは含まれません。  
  
 レポートが生成されるしきい値と頻度を構成するには、 **sp_configure** コマンドを使用して、 **blocked process threshold** オプションを構成します。これは秒単位で設定できます。 既定では、ブロックされているプロセスのレポートは生成されません。 **blocked process threshold** オプションの設定に関する詳細については、「[blocked process threshold サーバー構成オプション](../../database-engine/configure-windows/blocked-process-threshold-server-configuration-option.md)」を参照してください します。  
  
 **Blocked Process Report** イベント クラスによって返されるデータのフィルター処理については、「[トレース内のイベントへのフィルターの適用 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/filter-events-in-a-trace-sql-server-profiler.md)」、「[トレース フィルターの設定 &#40;Transact-SQL&#41;](../../relational-databases/sql-trace/set-a-trace-filter-transact-sql.md)」、または「[sp_trace_setfilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql.md)」を参照してください。  
  
## <a name="blocked-process-report-event-class-data-columns"></a>Blocked Process Report イベント クラスのデータ列  
  
|データ列名|データ型|[説明]|列 ID|フィルターの適用|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**DatabaseID**|**int**|ロックが取得されたデータベースの ID です。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] では、 **ServerName** データ列がトレースにキャプチャされ、そのサーバーが利用可能な場合、データベースの名前が表示されます。 データベースに対応する値は、DB_ID 関数を使用して特定します。|3|はい|  
|**Duration**|**bigint**|プロセスがブロックされていた時間 (ミリ秒)。|13|はい|  
|**EndTime**|**datetime**|イベントの終了時刻。 **SQL:BatchStarting** や **SP:Starting**などの開始イベント クラスについては、この列に値が格納されません。|15|はい|  
|**EventClass**|**int**|イベントの種類 = 137。|27|いいえ|  
|**EventSequence**|**int**|要求内の特定のイベントのシーケンス。|51|いいえ|  
|**IndexID**|**int**|イベントの影響を受けるオブジェクトに付けられたインデックス用の ID。 オブジェクトのインデックス ID を調べるには、 **sysindexes** システム テーブルの **indid** 列を使用します。|24|はい|  
|**IsSystem**|**int**|イベントがシステム プロセスとユーザー プロセスのどちらで発生したか。 1 はシステム、0 はユーザーです。|60|はい|  
|**LoginSid**|**image**|ログインしたユーザーのセキュリティ識別子 (SID)。 このイベントは必ずシステム スレッドから報告されます。 IsSystem は 1、SID は sa です。|41|はい|  
|**モード**|**int**|イベントが受け取った状態またはイベントが要求している状態。<br /><br /> 0 = NULL<br /><br /> 1 = Sch-S<br /><br /> 2 = Sch-M<br /><br /> 3 = S<br /><br /> 4 = U<br /><br /> 5 = X<br /><br /> 6 = IS<br /><br /> 7 = IU<br /><br /> 8 = IX<br /><br /> 9 = SIU<br /><br /> 10 = SIX<br /><br /> 11 = UIX<br /><br /> 12 = BU<br /><br /> 13 = RangeS-S<br /><br /> 14 = RangeS-U<br /><br /> 15 = RangeI-N<br /><br /> 16 = RangeI-S<br /><br /> 17 = RangeI-U<br /><br /> 18 = RangeI-X<br /><br /> 19 = RangeX-S<br /><br /> 20 = RangeX-U<br /><br /> 21 = RangeX-X|32|はい|  
|**Exchange Spill**|**int**|ロックを取得したオブジェクトのシステム割り当て ID (使用可能かつ適用可能な場合)。|22|はい|  
|**ServerName**|**nvarchar**|トレースされている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスの名前。|26||  
|**SessionLoginName**|**nvarchar**|セッションを開始したユーザーのログイン名。 たとえば、Login1 を使用して SQL Server に接続し、Login2 でステートメントを実行すると、 **SessionLoginName** には Login1 が表示され、 **LoginName** には Login2 が表示されます。 この列には、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインと Windows ログインの両方が表示されます。|64|はい|  
|**TextData**|**ntext**|トレースでキャプチャされたイベント クラスに依存するテキスト値。|1|はい|  
|**TransactionID**|**bigint**|システムによって割り当てられたトランザクション ID。|4|はい|  
  
## <a name="see-also"></a>参照  
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
