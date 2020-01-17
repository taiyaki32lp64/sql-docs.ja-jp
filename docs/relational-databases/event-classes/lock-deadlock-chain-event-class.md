---
title: Lock:Deadlock Chain イベント クラス | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- Deadlock Chain event class
ms.assetid: 9883127b-aa34-4235-88cc-c161cd2112cc
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 1f9677502f863f63f26cc2e922d14663cd1c3878
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68062598"
---
# <a name="lockdeadlock-chain-event-class"></a>Lock:Deadlock Chain イベント クラス
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Lock:Deadlock Chain イベント クラスは、デッドロックに関係するオブジェクトごとに生成されます。  
  
 Lock:Deadlock Chain イベント クラスを使用すると、いつデッドロックの状態が発生したかを監視できます。 この情報は、デッドロックがアプリケーションのパフォーマンスに重大な影響を与えているかどうかや、デッドロックに関係しているオブジェクトを特定する際に役立ちます。 これらのオブジェクトを変更するアプリケーション コードを調べて、デッドロックを最小限に抑える変更を行うことができるかどうかを判断できます。  
  
## <a name="lockdeadlock-chain-event-class-data-columns"></a>Lock:Deadlock Chain イベント クラスのデータ列  
  
|データ列名|データ型|[説明]|列 ID|フィルターの適用|  
|----------------------|---------------|-----------------|---------------|----------------|  
|BinaryData|**image**|ロック リソース ID。|2|はい|  
|DatabaseID|**int**|このリソースが所属するデータベースの ID。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] では、ServerName データ列がトレースにキャプチャされ、そのサーバーが利用可能な場合、データベースの名前が表示されます。 データベースに対応する値は、DB_ID 関数を使用して特定します。|3|はい|  
|DatabaseName|**nvarchar**|リソースが所属するデータベースの名前。|35|はい|  
|EventClass|**int**|イベントの種類 = 59。|27|いいえ|  
|EventSequence|**int**|要求内の特定のイベントのシーケンス。|51|いいえ|  
|EventSubClass|**int**|イベント サブクラスの種類。<br /><br /> 101 = リソースの種類のロック<br /><br /> 102 = リソースの種類の交換|21|はい|  
|IntegerData|**int**|デッドロック番号。 サーバーを起動すると、0 から始まる番号が割り当てられ、デッドロックが発生するたびに 1 ずつ加算されます。|25|はい|  
|IntegerData2|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|55|はい|  
|IsSystem|**int**|イベントがシステム プロセスとユーザー プロセスのどちらで発生したか。 1 はシステム、0 はユーザーです。|60|はい|  
|LoginSid|**image**|ログイン ユーザーのセキュリティ ID 番号 (SID)。 この情報は、sys.server_principals カタログ ビューで参照できます。 各 SID はサーバーのログインごとに一意です。|41|はい|  
|モード|**int**|0 = NULL - 他のすべてのロック モードと互換性あり (LCK_M_NL)<br /><br /> 1 = スキーマ安定度ロック (LCK_M_SCH_S)<br /><br /> 2 = スキーマ変更ロック (LCK_M_SCH_M)<br /><br /> 3 = 共有ロック (LCK_M_S)<br /><br /> 4 = 更新ロック (LCK_M_U)<br /><br /> 5 = 排他ロック (LCK_M_X)<br /><br /> 6 = インテント共有ロック (LCK_M_IS)<br /><br /> 7 = インテント更新ロック (LCK_M_IU)<br /><br /> 8 = インテント排他ロック (LCK_M_IX)<br /><br /> 9 = 更新のためのインテント付き共有 (LCK_M_SIU)<br /><br /> 10 = インテント排他付き共有 (LCK_M_SIX)<br /><br /> 11 = インテント排他付き更新 (LCK_M_UIX)<br /><br /> 12 = 一括更新ロック (LCK_M_BU)<br /><br /> 13 = 共有キー範囲/共有 (LCK_M_RS_S)<br /><br /> 14 = 共有キー範囲/更新 (LCK_M_RS_U)<br /><br /> 15 = キー範囲挿入/NULL (LCK_M_RI_NL)<br /><br /> 16 = 挿入キー範囲/共有 (LCK_M_RI_S)<br /><br /> 17 = 挿入キー範囲/更新 (LCK_M_RI_U)<br /><br /> 18 = 挿入キー範囲/排他 (LCK_M_RI_X)<br /><br /> 19 = 排他キー範囲/共有 (LCK_M_RX_S)<br /><br /> 20 = 排他キー範囲/更新 (LCK_M_RX_U)<br /><br /> 21 = 排他キー範囲/排他 (LCK_M_RX_X)|32|はい|  
|ObjectID|**int**|ロックされたオブジェクトの ID (使用可能かつ適用可能な場合)。|22|はい|  
|ObjectID2|**bigint**|関連するオブジェクトまたはエンティティの ID (使用可能かつ適用可能な場合)。|56|はい|  
|OwnerID|**int**|1 = TRANSACTION<br /><br /> 2 = CURSOR<br /><br /> 3 = SESSION<br /><br /> 4 = SHARED_TRANSACTION_WORKSPACE<br /><br /> 5 = EXCLUSIVE_TRANSACTION_WORKSPACE|58|はい|  
|RequestID|**int**|ステートメントが含まれている要求の ID。|49|はい|  
|ServerName|**nvarchar**|トレースされている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスの名前。|26|いいえ|  
|SessionLoginName|**nvarchar**|セッションを開始したユーザーのログイン名。 たとえば、Login1 を使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続し、Login2 でステートメントを実行すると、SessionLoginName には Login1 が表示され、LoginName には Login2 が表示されます。 この列には、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインと [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows ログインの両方が表示されます。|64|はい|  
|SPID|**int**|イベントが発生したセッションの ID。|12|はい|  
|StartTime|**datetime**|イベントの開始時刻 (取得できた場合)。|14|はい|  
|TextData|**ntext**|リソースの種類に依存するテキスト値。|1|はい|  
|TransactionID|**bigint**|システムによって割り当てられたトランザクション ID。|4|はい|  
|型|**int**|1 = NULL_RESOURCE<br /><br /> 2 = DATABASE<br /><br /> 3 = FILE<br /><br /> 5 = OBJECT<br /><br /> 6 = PAGE<br /><br /> 7 = KEY<br /><br /> 8 = EXTENT<br /><br /> 9 = RID<br /><br /> 10 = APPLICATION<br /><br /> 11 = METADATA<br /><br /> 12 = AUTONAMEDB<br /><br /> 13 = HOBT<br /><br /> 14 = ALLOCATION_UNIT|57|はい|  
  
## <a name="see-also"></a>参照  
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [sys.dm_tran_locks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md)  
  
  
