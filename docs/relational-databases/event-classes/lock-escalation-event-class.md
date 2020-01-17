---
title: Lock:Escalation イベント クラス | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- Escalation event class
- lock escalation [SQL Server], event class
ms.assetid: d253b44c-7600-4afa-a3a7-03cc937c6a4b
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: faad3614a308efc8dfa8994b176cec148520522a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68118283"
---
# <a name="lockescalation-event-class"></a>Lock:Escalation イベント クラス
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **Lock:Escalation** イベント クラスは、細かい単位のロックが大きな単位のロックに変換されたことを示します。たとえば、行ロックがオブジェクト ロックに変換された場合です。 Escalation イベント クラスは、イベント ID 60 です。  
  
## <a name="lockescalation-event-class-data-columns"></a>Lock:Escalation イベント クラスのデータ列  
  
|データ列名|データ型|[説明]|列 ID|フィルターの適用|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**ApplicationName**|**nvarchar**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスへの接続を作成したクライアント アプリケーションの名前。 この列には、プログラムの表示名ではなく、アプリケーションによって渡された値が格納されます。|10|はい|  
|**ClientProcessID**|**int**|クライアント アプリケーションが実行されているプロセスに対し、ホスト コンピューターが割り当てた ID。 クライアントによりクライアント プロセス ID が指定されると、このデータ列に値が格納されます。|9|はい|  
|**DatabaseID**|**int**|ロックが取得されたデータベースの ID です。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] では、 **ServerName** データ列がトレースにキャプチャされ、そのサーバーが利用可能な場合、データベースの名前が表示されます。 データベースに対応する値は、DB_ID 関数を使用して特定します。|3|はい|  
|**DatabaseName**|**nvarchar**|エスカレーションが発生したデータベースの名前。|35|はい|  
|**EventClass**|**int**|イベントの種類 = 60。|27|いいえ|  
|**EventSubClass**|**int**|ロックのエスカレーションの原因。<br /><br /> **0 - LOCK_THRESHOLD** は、ステートメントがロックのしきい値を超えたことを示します。<br /><br /> **1 - MEMORY_THRESHOLD** は、ステートメントがメモリしきい値を超えたことを示します。|21|はい|  
|**EventSequence**|**int**|要求内の特定のイベントのシーケンス。|51|いいえ|  
|**GroupID**|**int**|SQL トレース イベントが発生したワークロード グループの ID。|66|はい|  
|**HostName**|**nvarchar**|クライアントが実行されているコンピューターの名前。 このデータ列にはクライアントからホスト名が提供されている場合に値が格納されます。 ホスト名を指定するには、HOST_NAME 関数を使用します。|8|はい|  
|**IntegerData**|**int**|HoBT ロック数。 ロックのエスカレーション時の HoBT に対するロックの数。|25|はい|  
|**IntegerData2**|**int**|エスカレートされたロック数。 変換されたロックの合計数。 これらのロック構造は、エスカレートされたロックによって既に対応されているため、割り当て解除されます。|55|はい|  
|**IsSystem**|**int**|イベントがシステム プロセスとユーザー プロセスのどちらで発生したか。 1 はシステム、0 はユーザーです。|60|はい|  
|**LineNumber**|**int**|[!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントの行番号。|5|はい|  
|**LoginName**|**nvarchar**|ユーザーのログイン名 ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セキュリティ ログインまたは DOMAIN\username という形式の [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows ログイン資格情報)。|11|はい|  
|**LoginSid**|**image**|ログイン ユーザーのセキュリティ ID 番号 (SID)。 この情報は、 **sys.server_principals** カタログ ビューで参照できます。 各 SID はサーバーのログインごとに一意です。|41|はい|  
|**モード**|**int**|エスカレーション後のロック モード。<br /><br /> 0 = NULL - 他のすべてのロック モードと互換性あり (LCK_M_NL)<br /><br /> 1 = スキーマ安定度ロック (LCK_M_SCH_S)<br /><br /> 2 = スキーマ変更ロック (LCK_M_SCH_M)<br /><br /> 3 = 共有ロック (LCK_M_S)<br /><br /> 4 = 更新ロック (LCK_M_U)<br /><br /> 5 = 排他ロック (LCK_M_X)<br /><br /> 6 = インテント共有ロック (LCK_M_IS)<br /><br /> 7 = インテント更新ロック (LCK_M_IU)<br /><br /> 8 = インテント排他ロック (LCK_M_IX)<br /><br /> 9 = 更新のためのインテント付き共有 (LCK_M_SIU)<br /><br /> 10 = インテント排他付き共有 (LCK_M_SIX)<br /><br /> 11 = インテント排他付き更新 (LCK_M_UIX)<br /><br /> 12 = 一括更新ロック (LCK_M_BU)<br /><br /> 13 = 共有キー範囲/共有 (LCK_M_RS_S)<br /><br /> 14 = 共有キー範囲/更新 (LCK_M_RS_U)<br /><br /> 15 = キー範囲挿入/NULL (LCK_M_RI_NL)<br /><br /> 16 = 挿入キー範囲/共有 (LCK_M_RI_S)<br /><br /> 17 = 挿入キー範囲/更新 (LCK_M_RI_U)<br /><br /> 18 = 挿入キー範囲/排他 (LCK_M_RI_X)<br /><br /> 19 = 排他キー範囲/共有 (LCK_M_RX_S)<br /><br /> 20 = 排他キー範囲/更新 (LCK_M_RX_U)<br /><br /> 21 = 排他キー範囲/排他 (LCK_M_RX_X)|32|はい|  
|**NTDomainName**|**nvarchar**|ユーザーが所属する Windows ドメイン。|7|はい|  
|**NTUserName**|**nvarchar**|Windows のユーザー名。|6|はい|  
|**Exchange Spill**|**int**|ロックのエスカレーションがトリガーされたテーブルにシステムが割り当てた ID。|22|はい|  
|**ObjectID2**|**bigint**|関連するオブジェクトまたはエンティティの ID (ロックのエスカレーションがトリガーされた HoBT ID)。|56|はい|  
|**Offset**|**int**|[!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントの開始オフセット。|61|はい|  
|**OwnerID**|**int**|1 = TRANSACTION<br /><br /> 2 = CURSOR<br /><br /> 3 = SESSION<br /><br /> 4 = SHARED_TRANSACTION_WORKSPACE<br /><br /> 5 = EXCLUSIVE_TRANSACTION_WORKSPACE<br /><br /> 6 = WAITFOR_QUERY|58|はい|  
|**RequestID**|**int**|ステートメントが含まれている要求の ID。|49|はい|  
|**ServerName**|**nvarchar**|トレースされている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスの名前。|26|いいえ|  
|**SessionLoginName**|**nvarchar**|セッションを開始したユーザーのログイン名。 たとえば、Login1 を使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続し、Login2 でステートメントを実行すると、 **SessionLoginName** には Login1 が表示され、 **LoginName** には Login2 が表示されます。 この列には、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインと Windows ログインの両方が表示されます。|64|はい|  
|**SPID**|**int**|イベントが発生したセッションの ID。|12|はい|  
|**StartTime**|**datetime**|イベントの開始時刻 (取得できた場合)。|14|はい|  
|**TextData**|**ntext**|ロックのエスカレーションの原因となった [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントのテキスト。|1|はい|  
|**TransactionID**|**bigint**|システムによって割り当てられたトランザクション ID。|4|はい|  
|**型**|**int**|ロックのエスカレーション粒度。<br /><br /> 1 = NULL_RESOURCE<br /><br /> 2 = DATABASE<br /><br /> 3 = FILE<br /><br /> 5 = OBJECT (テーブル レベル)<br /><br /> 6 = PAGE<br /><br /> 7 = KEY<br /><br /> 8 = EXTENT<br /><br /> 9 = RID<br /><br /> 10 = APPLICATION<br /><br /> 11 = METADATA<br /><br /> 12 = HOBT<br /><br /> 13=ALLOCATION_UNIT|57|はい|  
  
## <a name="examples"></a>使用例  
 次の例では、 `sp_trace_create` プロシージャを使用してトレースを作成し、 `sp_trace_setevent` を使用してロックのエスカレーション列をそのトレースに追加してから、 `sp_trace_setstatus` を使用してトレースを開始します。 `EXEC sp_trace_setevent @TraceID, 60, 22, 1`などのステートメントでは、番号 `60` は Escalation イベント クラスを示し、番号 `22` は **ObjectID** 列を示し、 `1` はトレース イベントを ON に設定します。  
  
```  
DECLARE @RC int, @TraceID int;  
EXEC @rc = sp_trace_create @TraceID output, 0, N'C:\TraceResults';  
-- Set the events and data columns you need to capture.  
EXEC sp_trace_setevent @TraceID, 60,  1, 1; --  1 = TextData  
EXEC sp_trace_setevent @TraceID, 60, 12, 1; -- 12 = SPID  
EXEC sp_trace_setevent @TraceID, 60, 21, 1; -- 21 = EventSubClass  
EXEC sp_trace_setevent @TraceID, 60, 22, 1; -- 22 = ObjectID  
EXEC sp_trace_setevent @TraceID, 60, 25, 1; -- 25 = IntegerData  
EXEC sp_trace_setevent @TraceID, 60, 55, 1; -- 25 = IntegerData2  
EXEC sp_trace_setevent @TraceID, 60, 57, 1; -- 57 = Type  
-- Set any filter  by using sp_trace_setfilter.  
-- Start the trace.  
EXEC sp_trace_setstatus @TraceID, 1;  
GO  
```  
  
 トレースが実行中であるため、トレースの必要があるステートメントを実行します。 完了したら、次のコードを実行してトレースを停止し、閉じます。 この例では、 `fn_trace_getinfo` 関数を使用して、 `traceid` ステートメントで使用される `sp_trace_setstatus` を取得します。  
  
```  
-- After the trace is complete.  
DECLARE @TraceID int;  
-- Find the traceid of the current trace.  
SELECT @TraceID = traceid   
FROM ::fn_trace_getinfo(default)   
WHERE value = N'C:\TraceResults.trc';  
  
-- First stop the trace.   
EXEC sp_trace_setstatus @TraceID, 0;  
  
-- Close and then delete its definition from SQL Server.   
EXEC sp_trace_setstatus @TraceID, 2;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [sys.dm_tran_locks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md)  
  
  
