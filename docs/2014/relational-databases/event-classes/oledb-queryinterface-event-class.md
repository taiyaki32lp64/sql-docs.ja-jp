---
title: OLEDB QueryInterface イベント クラス | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- OLEDB QueryInterface event class
ms.assetid: f54c9ef9-3add-497c-a09b-42c4ce3c623d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b420e0b4b9c9531209f3d3227f534116e26dd206
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63032423"
---
# <a name="oledb-queryinterface-event-class"></a>OLEDB QueryInterface イベント クラス
  **OLEDB QueryInterface** イベント クラスは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] から分散クエリやリモート ストアド プロシージャの **OLE DB QueryInterface** 呼び出しが行われるときに発生します。 このイベント クラスは、分散クエリやリモート ストアド プロシージャに関連する問題を監視するトレースに含めます。  
  
 **OLEDB QueryInterface** イベント クラスを含めると、オーバーヘッドが大きくなります。 このようなイベントが頻繁に発生すると、トレースによってパフォーマンスが大きく低下することがあります。 発生するオーバーヘッドを最小限に抑えるには、短期間だけ特定の問題を監視するトレースに限定してこのイベント クラスを使用するようにします。  
  
## <a name="oledb-queryinterface-event-class-data-columns"></a>OLEDB QueryInterface イベント クラスのデータ列  
  
|データ列名|データ型|説明|列 ID|フィルターの適用|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|`nvarchar`|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスへの接続を作成したクライアント アプリケーションの名前。 この列には、プログラムの表示名ではなく、アプリケーションによって渡された値が格納されます。|10|はい|  
|ClientProcessID|`int`|クライアント アプリケーションが実行されているプロセスに対し、ホスト コンピューターが割り当てた ID。 クライアントによりクライアント プロセス ID が指定されると、このデータ列に値が格納されます。|9|はい|  
|DatabaseID|`int`|USE *database* ステートメントで指定されたデータベースの ID、または特定のインスタンスについて USE *database* ステートメントが実行されていない場合は既定のデータベースの ID となります。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] では、 **ServerName** データ列がトレースにキャプチャされ、そのサーバーが利用可能な場合、データベースの名前が表示されます。 データベースに対応する値は、DB_ID 関数を使用して特定します。|3|はい|  
|DatabaseName|`nvarchar`|ユーザーのステートメントが実行されているデータベースの名前。|35|はい|  
|Duration|`bigint`|OLE DB QueryInterface イベントを完了する時間長。|13|いいえ|  
|EndTime|`datetime`|イベントが終了した時刻。|15|はい|  
|[エラー]|`int`|特定のイベントのエラー番号。 多くの場合、 **sys.messages** カタログ ビューに保存されているエラー番号です。|31|はい|  
|EventClass|`int`|イベントの種類 = 120。|27|いいえ|  
|EventSequence|`int`|バッチ内の OLE DB イベント クラスのシーケンス。|51|いいえ|  
|EventSubClass|`int`|0 = 開始<br /><br /> 1 = 完了|21|いいえ|  
|GroupID|`int`|SQL トレース イベントが発生したワークロード グループの ID。|66|はい|  
|HostName|`nvarchar`|クライアントが実行されているコンピューターの名前。 このデータ列にはクライアントからホスト名が提供されている場合に値が格納されます。 ホスト名を指定するには、HOST_NAME 関数を使用します。|8|はい|  
|IsSystem|`int`|イベントがシステム プロセスとユーザー プロセスのどちらで発生したか。 1 はシステム、0 はユーザーです。|60|はい|  
|LinkedServerName|`nvarchar`|リンク サーバーの名前|45|はい|  
|LoginName|`nvarchar`|ユーザーのログイン名 ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セキュリティ ログインまたは DOMAIN\username という形式の [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows ログイン資格情報)。|11|はい|  
|LoginSid|`image`|ログインしたユーザーのセキュリティ識別子 (SID)。 この情報は、sys.server_principals カタログ ビューで参照できます。 各 SID はサーバーのログインごとに一意です。|41|はい|  
|MethodName|`nvarchar`|呼び出し側メソッドの名前。|47|いいえ|  
|NTDomainName|`nvarchar`|ユーザーが所属する Windows ドメイン。|7|はい|  
|NTUserName|`nvarchar`|Windows のユーザー名。|6|はい|  
|ProviderName|`nvarchar`|OLE DB プロバイダーの名前です。|46|はい|  
|RequestID|`int`|ステートメントが含まれている要求の ID。|49|はい|  
|SessionLoginName|`nvarchar`|セッションを開始したユーザーのログイン名。 たとえば、Login1 を使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続し、Login2 でステートメントを実行すると、`SessionLoginName` には Login1 が表示され、`LoginName` には Login2 が表示されます。 この列には、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインと Windows ログインの両方が表示されます。|64|はい|  
|SPID|`int`|イベントが発生したセッションの ID。|12|はい|  
|StartTime|`datetime`|イベントの開始時刻 (取得できた場合)。|14|はい|  
|TextData|`nvarchar`|OLE DB 呼び出しで送受信されるパラメーター。|1|いいえ|  
|TransactionID|`bigint`|システムによって割り当てられたトランザクション ID。|4|[はい]|  
  
## <a name="see-also"></a>参照  
 [拡張イベント](../extended-events/extended-events.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)   
 [Transact-SQL での OLE オートメーション オブジェクト](../stored-procedures/ole-automation-objects-in-transact-sql.md)  
  
  
