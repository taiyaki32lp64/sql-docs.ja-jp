---
title: CursorExecute イベント クラス | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- CursorExecute event class
ms.assetid: 83399fd8-cc25-4d3c-8985-7a824ef08e08
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f9cc17fb916bad5879c4f55737b72f9a1013de51
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62663508"
---
# <a name="cursorexecute-event-class"></a>CursorExecute イベント クラス
  **CursorExecute** イベント クラスは、API (アプリケーション プログラミング インターフェイス) のカーソルで発生する、カーソル実行イベントを記述しています。 カーソル実行イベントは、カーソル準備イベントで作成された実行プランから、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] によってカーソルの作成およびデータ設定が行われたときに発生します。  
  
 **CursorExecute** イベント クラスは、カーソルのパフォーマンスを記録しているトレース内で使用します。 **CursorExecute** イベント クラスをトレースに含めた場合、発生するオーバーヘッドの量は、トレース中にデータベースに対してカーソルを使用する頻度によって異なります。 カーソルの使用頻度が高い場合は、トレースによってパフォーマンスが大幅に低下する可能性があります。  
  
## <a name="cursorexecute-event-class-data-columns"></a>CursorExecute イベント クラスのデータ列  
  
|データ列名|データ型|説明|列 ID|フィルターの適用|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**ApplicationName**|**nvarchar**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスへの接続を作成したクライアント アプリケーションの名前。 この列には、プログラムの表示名ではなく、アプリケーションによって渡された値が格納されます。|10|はい|  
|**ClientProcessID**|**int**|クライアント アプリケーションが実行されているプロセスに対し、ホスト コンピューターが割り当てた ID。 クライアントによりクライアント プロセス ID が指定されると、このデータ列に値が格納されます。|9|はい|  
|**DatabaseID**|**int**|USE *database* ステートメントで指定されたデータベースの ID、または特定のインスタンスについて USE *database*ステートメントが実行されていない場合は既定のデータベースの ID となります。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] では、 **ServerName** データ列がトレースにキャプチャされ、そのサーバーが利用可能な場合、データベースの名前が表示されます。 データベースに対応する値は、DB_ID 関数を使用して特定します。|3|はい|  
|**DatabaseName**|**nvarchar**|ユーザーのステートメントが実行されているデータベースの名前。|35|はい|  
|**EventClass**|**int**|記録されるイベントの種類 = 74。|27|いいえ|  
|**EventSequence**|**int**|バッチ内の **CursorExecute** イベント クラスのシーケンス。|51|いいえ|  
|**GroupID**|**int**|SQL トレース イベントが発生したワークロード グループの ID。|66|はい|  
|**Handle**|**int**|サーバーとの間で実行を調整するときに ODBC、OLE DB、または DB-Library によって使用される整数。|33|はい|  
|**HostName**|**nvarchar**|クライアントが実行されているコンピューターの名前。 このデータ列にはクライアントからホスト名が提供されている場合に値が格納されます。 ホスト名を指定するには、HOST_NAME 関数を使用します。|8|はい|  
|**IntegerData**|**int**|カーソルの種類。 値は次のとおりです。<br /><br /> 1 = キー セット<br /><br /> 2 = 動的<br /><br /> 4 = 順方向専用<br /><br /> 8 = 静的<br /><br /> 16 = 高速順方向|25|いいえ|  
|**IsSystem**|**int**|イベントがシステム プロセスとユーザー プロセスのどちらで発生したか。 1 はシステム、0 はユーザーです。|60|はい|  
|**LoginName**|**nvarchar**|ユーザーのログイン名 ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セキュリティ ログインまたは DOMAIN\username という形式の Windows ログイン資格情報)。|11|はい|  
|**LoginSid**|**image**|ログインしたユーザーのセキュリティ識別子 (SID)。 この情報は、 **sys.server_principals** カタログ ビューで参照できます。 各 SID はサーバーのログインごとに一意です。|41|はい|  
|**NTDomainName**|**nvarchar**|ユーザーが所属する Windows ドメイン。|7|はい|  
|**NTUserName**|**nvarchar**|Windows のユーザー名。|6|はい|  
|**RequestID**|**int**|カーソルを実行した要求 ID。|49|はい|  
|**ServerName**|**nvarchar**|トレースされている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスの名前。|26|いいえ|  
|**SessionLoginName**|**nvarchar**|セッションを開始したユーザーのログイン名。 たとえば、Login1 を使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続し、Login2 でステートメントを実行すると、 **SessionLoginName** には Login1 が表示され、 **LoginName** には Login2 が表示されます。 この列には、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインと Windows ログインの両方が表示されます。|64|はい|  
|**SPID**|**int**|イベントが発生したセッションの ID。|12|はい|  
|**StartTime**|**datetime**|イベントの開始時刻 (取得できた場合)。|14|はい|  
|**TransactionID**|**bigint**|システムによって割り当てられたトランザクション ID。|4|はい|  
|**XactSequence**|**bigint**|現在のトランザクションを説明するトークン。|50|はい|  
  
## <a name="see-also"></a>参照  
 [拡張イベント](../extended-events/extended-events.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)   
 [カーソル](../cursors.md)  
  
  
