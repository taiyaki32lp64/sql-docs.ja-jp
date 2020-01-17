---
title: Lock:Deadlock イベント クラス | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- Deadlock event class
ms.assetid: 3e0394bc-6ea8-4533-845c-76782bec73c2
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 9ba1146dfe62067ba6371eec6a2b621eb2897852
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68118302"
---
# <a name="lockdeadlock-event-class"></a>Lock:Deadlock イベント クラス
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Lock:Deadlock イベント クラスは、ロックの取得を試行したときに、その試行がデッドロックの一部になり、デッドロックの対象として選択されたために取り消す場合に生成されます。  
  
 Lock:Deadlock イベント クラスを使用して、デッドロックがいつ発生し、どのオブジェクトが関係しているかを監視します。 この情報を使用すると、デッドロックがアプリケーションのパフォーマンスに重大な影響を及ぼしているかどうかを判断できます。 次に、アプリケーション コードを調べ、デッドロックが最小になるように変更できるかどうかを判断できます。  
  
## <a name="lockdeadlock-event-class-data-columns"></a>Lock:Deadlock イベント クラスのデータ列  
  
|データ列名|データ型|[説明]|列 ID|フィルターの適用|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|**nvarchar**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスへの接続を作成したクライアント アプリケーションの名前。 この列には、プログラムの表示名ではなく、アプリケーションによって渡された値が格納されます。|10|はい|  
|BinaryData|**image**|ロック リソース ID。|2|はい|  
|ClientProcessID|**int**|クライアント アプリケーションが実行されているプロセスに対し、ホスト コンピューターが割り当てた ID。 クライアントでクライアント プロセス ID が指定されると、このデータ列が作成されます。|9|はい|  
|DatabaseID|**int**|ロックが取得されていたデータベースの ID です。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] では、ServerName データ列がトレースにキャプチャされ、そのサーバーが利用可能な場合、データベースの名前が表示されます。 データベースに対応する値は、DB_ID 関数を使用して特定します。|3|はい|  
|DatabaseName|**nvarchar**|ロックが取得されていたデータベースの名前です。|35|はい|  
|Duration|**bigint**|ロック要求が発行されてからデッドロックが発生するまでに経過した時間 (ミリ秒) です。|13|はい|  
|EndTime|**datetime**|デッドロックが終了した時刻です。|15|はい|  
|EventClass|**int**|イベントの種類 = 25。|27|いいえ|  
|EventSequence|**int**|要求内の特定のイベントのシーケンス。|51|いいえ|  
|GroupID|**int**|SQL トレース イベントが発生したワークロード グループの ID。|66|はい|  
|HostName|**nvarchar**|クライアントが実行されているコンピューターの名前。 このデータ列にはクライアントからホスト名が提供されている場合に値が格納されます。 ホスト名を指定するには、HOST_NAME 関数を使用します。|8|はい|  
|IntegerData|**int**|デッドロック番号。 サーバーを起動すると番号が 0 から割り当てられ、デッドロックごとに増加します。|25|はい|  
|IntegerData2|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|55|はい|  
|IsSystem|**int**|イベントがシステム プロセスとユーザー プロセスのどちらで発生したか。 1 はシステム、0 はユーザーです。|60|はい|  
|LoginName|**nvarchar**|ユーザーのログイン名 ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セキュリティ ログインまたは DOMAIN\username という形式の [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows ログイン資格情報)。|11|はい|  
|LoginSid|**image**|ログイン ユーザーのセキュリティ ID 番号 (SID)。 この情報は、sys.server_principals カタログ ビューで参照できます。 各 SID はサーバーのログインごとに一意です。|41|はい|  
|モード|**int**|デッドロックの後に結果として発生するモード。<br /><br /> 0 = NULL - 他のすべてのロック モードと互換性あり (LCK_M_NL)<br /><br /> 1 = スキーマ安定度ロック (LCK_M_SCH_S)<br /><br /> 2 = スキーマ変更ロック (LCK_M_SCH_M)<br /><br /> 3 = 共有ロック (LCK_M_S)<br /><br /> 4 = 更新ロック (LCK_M_U)<br /><br /> 5 = 排他ロック (LCK_M_X)<br /><br /> 6 = インテント共有ロック (LCK_M_IS)<br /><br /> 7 = インテント更新ロック (LCK_M_IU)<br /><br /> 8 = インテント排他ロック (LCK_M_IX)<br /><br /> 9 = 更新のためのインテント付き共有 (LCK_M_SIU)<br /><br /> 10 = インテント排他付き共有 (LCK_M_SIX)<br /><br /> 11 = インテント排他付き更新 (LCK_M_UIX)<br /><br /> 12 = 一括更新ロック (LCK_M_BU)<br /><br /> 13 = 共有キー範囲/共有 (LCK_M_RS_S)<br /><br /> 14 = 共有キー範囲/更新 (LCK_M_RS_U)<br /><br /> 15 = キー範囲挿入/NULL (LCK_M_RI_NL)<br /><br /> 16 = 挿入キー範囲/共有 (LCK_M_RI_S)<br /><br /> 17 = 挿入キー範囲/更新 (LCK_M_RI_U)<br /><br /> 18 = 挿入キー範囲/排他 (LCK_M_RI_X)<br /><br /> 19 = 排他キー範囲/共有 (LCK_M_RX_S)<br /><br /> 20 = 排他キー範囲/更新 (LCK_M_RX_U)<br /><br /> 21 = 排他キー範囲/排他 (LCK_M_RX_X)|32|はい|  
|NTDomainName|**nvarchar**|ユーザーが所属する Windows ドメイン。|7|はい|  
|NTUserName|**nvarchar**|Windows のユーザー名。|6|はい|  
|ObjectID|**int**|競合するオブジェクトの ID です (存在する場合)。|22|はい|  
|ObjectID2|**bigint**|関連するオブジェクトまたはエンティティの ID (使用可能かつ適用可能な場合)。|56|はい|  
|OwnerID|**int**|1 = TRANSACTION<br /><br /> 2 = CURSOR<br /><br /> 3 = SESSION<br /><br /> 4 = SHARED_TRANSACTION_WORKSPACE<br /><br /> 5 = EXCLUSIVE_TRANSACTION_WORKSPACE|58|はい|  
|RequestID|**int**|ステートメントが含まれている要求の ID。|49|はい|  
|ServerName|**nvarchar**|トレースされている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスの名前。|26|いいえ|  
|SessionLoginName|**nvarchar**|セッションを開始したユーザーのログイン名。 たとえば、Login1 を使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続し、Login2 でステートメントを実行すると、SessionLoginName には Login1 が表示され、LoginName には Login2 が表示されます。 この列には、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインと Windows ログインの両方が表示されます。|64|はい|  
|SPID|**int**|イベントが発生したセッションの ID。|12|はい|  
|StartTime|**datetime**|イベントの開始時刻 (取得できた場合)。|14|はい|  
|TextData|**ntext**|取得されていたロックの種類に依存するテキスト値です。|1|はい|  
|TransactionID|**bigint**|システムによって割り当てられたトランザクション ID。|4|はい|  
|型|**int**|1 = NULL_RESOURCE<br /><br /> 2 = DATABASE<br /><br /> 3 = FILE<br /><br /> 5 = OBJECT<br /><br /> 6 = PAGE<br /><br /> 7 = KEY<br /><br /> 8 = EXTENT<br /><br /> 9 = RID<br /><br /> 10 = APPLICATION<br /><br /> 11 = METADATA<br /><br /> 12 = AUTONAMEDB<br /><br /> 13 = HOBT<br /><br /> 14 = ALLOCATION_UNIT|57|はい|  
  
## <a name="see-also"></a>参照  
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [sys.dm_tran_locks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md)  
  
  
