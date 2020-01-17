---
title: Missing Column Statistics イベント クラス | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Missing Column Statistics event class
ms.assetid: b9321143-3f29-4a19-8471-7085669282ef
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 43a83d0b20bbcdb0b95dd727a51d59353f7675bc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63023416"
---
# <a name="missing-column-statistics-event-class"></a>Missing Column Statistics イベント クラス
  Missing Column Statistics イベント クラスは、オプティマイザーにとって役立つ列統計が使用できないことを示します。  
  
 Missing Column Statistics イベント クラスを監視することにより、クエリに使用する列の統計が存在するかどうかを判断できます。 列統計が存在しないと、オプティマイザーは通常よりも効率の低いクエリ プランを選択することがあります。  
  
## <a name="missing-column-statistics-event-class-data-columns"></a>Missing Column Statistics イベント クラスのデータ列  
  
|データ列名|データ型|説明|列 ID|フィルターの適用|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|`nvarchar`|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスへの接続を作成したクライアント アプリケーションの名前。 この列には、プログラムの表示名ではなく、アプリケーションによって渡された値が格納されます。|10|はい|  
|ClientProcessID|`int`|クライアント アプリケーションが実行されているプロセスに対し、ホスト コンピューターが割り当てた ID。 クライアントによりクライアント プロセス ID が指定されると、このデータ列に値が格納されます。|9|はい|  
|DatabaseID|`int`|USE *database* ステートメントで指定されたデータベースの ID、または特定のインスタンスについて USE *database* ステートメントが実行されていない場合は既定のデータベースの ID となります。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] では、ServerName データ列がトレースにキャプチャされ、そのサーバーが利用可能な場合、データベースの名前が表示されます。 データベースに対応する値は、DB_ID 関数を使用して特定します。|3|はい|  
|DatabaseName|`nvarchar`|ユーザーのステートメントが実行されているデータベースの名前。|35|はい|  
|EventClass|`int`|イベントの種類 = 79。|27|いいえ|  
|EventSequence|`int`|要求内の特定のイベントのシーケンス。|51|いいえ|  
|GroupID|`int`|SQL トレース イベントが発生したワークロード グループの ID。|66|はい|  
|HostName|`nvarchar`|クライアントが実行されているコンピューターの名前。 このデータ列にはクライアントからホスト名が提供されている場合に値が格納されます。 ホスト名を指定するには、HOST_NAME 関数を使用します。|8|はい|  
|IsSystem|`int`|イベントがシステム プロセスとユーザー プロセスのどちらで発生したか。 1 はシステム、0 はユーザーです。|60|はい|  
|LoginName|`nvarchar`|ユーザーのログイン名 ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セキュリティ ログインまたは DOMAIN\username という形式の [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows ログイン資格情報)。|11|はい|  
|LoginSid|`image`|ログイン ユーザーのセキュリティ ID 番号 (SID)。 この情報は、sys.server_principals カタログ ビューで参照できます。 各 SID はサーバーのログインごとに一意です。|41|はい|  
|NTDomainName|`nvarchar`|ユーザーが所属する Windows ドメイン。|7|はい|  
|NTUserName|`nvarchar`|Windows のユーザー名。|6|はい|  
|RequestID|`int`|ステートメントが含まれている要求の ID。|49|はい|  
|ServerName|`nvarchar`|トレースされている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスの名前。|26|いいえ|  
|SessionLoginName|`nvarchar`|セッションを開始したユーザーのログイン名。 たとえば、Login1 を使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続し、Login2 でステートメントを実行すると、SessionLoginName には Login1 が表示され、LoginName には Login2 が表示されます。 この列には、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインと Windows ログインの両方が表示されます。|64|[はい]|  
|SPID|`int`|イベントが発生したセッションの ID。|12|はい|  
|StartTime|`datetime`|イベントの開始時刻 (取得できた場合)。|14|はい|  
|TextData|`ntext`|統計のない列の一覧。|1|はい|  
|TransactionID|`bigint`|システムによって割り当てられたトランザクション ID。|4|はい|  
|XactSequence|`bigint`|現在のトランザクションを説明するトークン。|50|はい|  
  
## <a name="see-also"></a>参照  
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)   
 [CREATE STATISTICS &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-statistics-transact-sql)   
 [イベントの監視と応答](../../ssms/agent/monitor-and-respond-to-events.md)  
  
  
