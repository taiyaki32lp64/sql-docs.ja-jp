---
title: SQL:StmtCompleted イベント クラス | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- SQL:StmtCompleted event class
ms.assetid: a55f005d-e020-423c-8940-c24ea1b20104
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 62dc29f8143f92fc9674ed10c092dc6ad08570fa
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63060370"
---
# <a name="sqlstmtcompleted-event-class"></a>SQL:StmtCompleted イベント クラス
  SQL:StmtCompleted イベント クラスは、 [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントが完了したことを示します。  
  
## <a name="sqlstmtcompleted-event-class-data-columns"></a>SQL:StmtCompleted イベント クラスのデータ列  
  
|データ列名|データ型|説明|列 ID|フィルターの適用|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|`nvarchar`|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスへの接続を作成したクライアント アプリケーションの名前。 この列には、プログラムの表示名ではなく、アプリケーションによって渡された値が格納されます。|10|はい|  
|ClientProcessID|`int`|クライアント アプリケーションが実行されているプロセスに対し、ホスト コンピューターが割り当てた ID。 クライアントによりクライアント プロセス ID が指定されると、このデータ列に値が格納されます。|9|はい|  
|CPU|`int`|イベントに使用された CPU 時間 (ミリ秒単位)。|18|[はい]|  
|DatabaseID|`int`|USE *database* ステートメントで指定されたデータベースの ID、または特定のインスタンスについて USE *database* ステートメントが実行されていない場合は既定のデータベースの ID となります。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] では、ServerName データ列がトレースにキャプチャされ、そのサーバーが利用可能な場合、データベースの名前が表示されます。 データベースに対応する値は、DB_ID 関数を使用して特定します。|3|[はい]|  
|DatabaseName|`nvarchar`|ユーザーのステートメントが実行されているデータベースの名前。|35|はい|  
|Duration|`bigint`|イベントにかかった時間 (マイクロ秒)。|13|はい|  
|EndTime|`datetime`|イベントの終了時刻。|15|[はい]|  
|EventClass|`int`|イベントの種類 = 41。|27|いいえ|  
|EventSequence|`int`|要求内の特定のイベントのシーケンス。|51|いいえ|  
|GroupID|`int`|SQL トレース イベントが発生したワークロード グループの ID。|66|はい|  
|HostName|`nvarchar`|クライアントが実行されているコンピューターの名前。 このデータ列にはクライアントからホスト名が提供されている場合に値が格納されます。 ホスト名を指定するには、HOST_NAME 関数を使用します。|8|はい|  
|IntegerData|`int`|ステートメントによって返された行数。|25|はい|  
|IntegerData2|`int`|実行中のステートメントの終了オフセット (バイト単位)。|55|はい|  
|IsSystem|`int`|イベントがシステム プロセスとユーザー プロセスのどちらで発生したか。 1 はシステム、0 はユーザーです。|60|はい|  
|LineNumber|`int`|実行されるステートメントの行番号。|5|はい|  
|LoginName|`nvarchar`|ユーザーのログイン名 ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セキュリティ ログインまたは DOMAIN\username という形式の [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows ログイン資格情報)。|11|はい|  
|LoginSid|`image`|ログイン ユーザーのセキュリティ ID 番号 (SID)。 この情報は、sys.server_principals カタログ ビューで参照できます。 各 SID はサーバーのログインごとに一意です。|41|はい|  
|NestLevel|`int`|ステートメントがストアド プロシージャ内で実行された場合のストアド プロシージャの入れ子レベル。|29|はい|  
|NTDomainName|`nvarchar`|ユーザーが所属する Windows ドメイン。|7|[はい]|  
|NTUserName|`nvarchar`|Windows のユーザー名。|6|はい|  
|Offset|`int`|ストアド プロシージャ内またはバッチ内のステートメントの開始オフセット。|61|はい|  
|Reads|`bigint`|SQL ステートメントによるページの読み取り回数。|16|はい|  
|RequestID|`int`|ステートメントが含まれている要求の ID。|49|はい|  
|RowCounts|`bigint`|イベントの影響を受けた行数。|48|はい|  
|ServerName|`nvarchar`|トレースされている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスの名前。|26|いいえ|  
|SessionLoginName|`nvarchar`|セッションを開始したユーザーのログイン名。 たとえば、Login1 を使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続し、Login2 でステートメントを実行すると、SessionLoginName には Login1 が表示され、LoginName には Login2 が表示されます。 この列には、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインと Windows ログインの両方が表示されます。|64|はい|  
|SPID|`int`|イベントが発生したセッションの ID。|12|[はい]|  
|StartTime|`datetime`|イベントの開始時刻 (取得できた場合)。|14|はい|  
|TextData|`ntext`|実行されたステートメントのテキスト。|1|[はい]|  
|TransactionID|`bigint`|ステートメントがトランザクション内で実行された場合のトランザクションの ID。|4|はい|  
|Writes|`bigint`|SQL ステートメントによるページの書き込み回数。|17|はい|  
|XactSequence|`bigint`|現在のトランザクションを説明するトークン。|50|はい|  
  
## <a name="see-also"></a>関連項目  
 [拡張イベント](../extended-events/extended-events.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)  
  
  
