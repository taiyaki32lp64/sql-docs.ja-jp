---
title: Degree of Parallelism (7.0 Insert) イベント クラス | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Degree of Parallelism event class
ms.assetid: 6753ef30-890f-47a3-b0b6-8abb184e1d83
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 56a87741b104a49f98a3cba05dc65d911774774d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62662901"
---
# <a name="degree-of-parallelism-70-insert-event-class"></a>Degree of Parallelism (7.0 Insert) イベント クラス
  **Degree of Parallelism (7.0 Insert)** イベント クラスは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で SELECT、INSERT、UPDATE、または DELETE ステートメントが実行されるたびに発生します。  
  
 このイベント クラスをトレースに含めた場合、このイベントが頻繁に発生すると、発生したオーバーヘッドの量によってパフォーマンスが大幅に低下することがあります。 オーバーヘッドの発生を最小限に抑えるには、このイベント クラスの使用を、特定の問題を短時間監視するトレースに制限します。  
  
## <a name="degree-of-parallelism-70-insert-event-class-data-columns"></a>Degree of Parallelism (7.0 Insert) イベント クラスのデータ列  
  
|データ列名|データ型|説明|列 ID|フィルターの適用|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**ApplicationName**|**nvarchar**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスへの接続を作成したクライアント アプリケーションの名前。 この列には、プログラムの表示名ではなく、アプリケーションによって渡された値が格納されます。|10|はい|  
|**BinaryData**|**image**|次の値に基づいた、処理を完了するために使用される CPU の数。<br /><br /> 0x00000000:直列で実行される直列プランを示します。<br /><br /> 0x01000000 では、直列で実行される並列プランを示します。<br /><br /> >= 0x02000000:並列で実行されている並列プランを示します。|2|いいえ|  
|**ClientProcessID**|**int**|クライアント アプリケーションが実行されているプロセスに対し、ホスト コンピューターが割り当てた ID。 クライアントでクライアント プロセス ID が指定されると、このデータ列が作成されます。|9|はい|  
|**DatabaseID**|**int**|USE database ステートメントで指定されたデータベースの ID、または特定のインスタンスについて USE database ステートメントが実行されていない場合は既定のデータベースの ID となります。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] では、 **ServerName** データ列がトレースにキャプチャされ、そのサーバーが利用可能な場合、データベースの名前が表示されます。 データベースに対応する値は、DB_ID 関数を使用して特定します。|3|[はい]|  
|**DatabaseName**|**nvarchar**|ユーザーのステートメントが実行されているデータベースの名前。|35|はい|  
|**Event Class**|**int**|イベントの種類 = 28。|27|いいえ|  
|**EventSequence**|**int**|要求内の特定のイベントのシーケンス。|51|いいえ|  
|**EventSubClass**|**int**|次の値に基づいて、実行されるステートメントを示します。<br /><br /> 1 = Select<br /><br /> 2 = Insert<br /><br /> 3 = Update<br /><br /> 4 = Delete|21|いいえ|  
|**GroupID**|**int**|SQL トレース イベントが発生したワークロード グループの ID。|66|はい|  
|**HostName**|**nvarchar**|クライアントが実行されているコンピューターの名前。 このデータ列には、クライアントがホスト名を指定している場合にデータが格納されます。 ホスト名を指定するには、HOST_NAME 関数を使用します。|8|はい|  
|**Integer Data**|**int**|ハッシュ、並べ替え、インデックス作成などの操作を実行するためにクエリに与えられた "ワークスペース メモリ" の量 (KB 単位)。 このメモリは、実行中に必要に応じて取得されます。|25|はい|  
|**IsSystem**|**int**|イベントがシステム プロセスとユーザー プロセスのどちらで発生したか。 1 はシステム、0 はユーザーです。|60|[はい]|  
|**LoginName**|**nvarchar**|ユーザーのログイン名 ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セキュリティ ログインまたは DOMAIN\\ *\username*という形式の Windows ログイン資格情報)。|11|はい|  
|**LoginSid**|**image**|ログイン ユーザーのセキュリティ ID 番号 (SID)。 この情報は、sys.server_principals カタログ ビューで参照できます。 各 SID はサーバーのログインごとに一意です。|41|はい|  
|**NTDomainName**|**nvarchar**|ユーザーが所属する Windows ドメイン。|7|はい|  
|**NTUserName**|**nvarchar**|Windows のユーザー名。|6|はい|  
|**RequestID**|**int**|フルテキスト クエリを開始した要求 ID。|49|[はい]|  
|**ServerName**|**nvarchar**|トレースされている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスの名前。|26|いいえ|  
|**SessionLoginName**|**nvarchar**|セッションを開始したユーザーのログイン名。 たとえば、Login1 を使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続し、Login2 でステートメントを実行すると、 **SessionLoginName** には Login1 が表示され、 **LoginName** には Login2 が表示されます。 この列には、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインと Windows ログインの両方が表示されます。|64|はい|  
|**SPID**|**int**|イベントが発生したセッションの ID。|12|はい|  
|**StartTime**|**datetime**|イベントの開始時刻 (取得できた場合)。|14|はい|  
|**TransactionID**|**bigint**|システムによって割り当てられたトランザクション ID。|4|はい|  
  
## <a name="see-also"></a>参照  
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)   
 [INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/insert-transact-sql)  
  
  
