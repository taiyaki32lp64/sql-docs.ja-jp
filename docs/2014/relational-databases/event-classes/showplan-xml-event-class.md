---
title: Showplan XML イベント クラス | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Showplan XML event class
ms.assetid: 8e22de84-8890-414a-93e4-aebfaa057d7f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6c025a899b426de714fb522218467e8d4cf805b6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62691870"
---
# <a name="showplan-xml-event-class"></a>Showplan XML イベント クラス
  Showplan XML イベント クラスは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で SQL ステートメントを実行したときに発生します。 プラン表示操作を特定する場合は、Showplan XML イベント クラスを含めます。 このイベント クラスには、各イベントが正しく定義された XML ドキュメントとして格納されます。  
  
 トレースに Showplan XML  イベント クラスを含めると、オーバーヘッドの量によって、パフォーマンスが著しく低下します。 Showplan XML は、クエリの最適化時に作成されるクエリ プランを格納します。 発生するオーバーヘッドを最小限に抑えるには、短期間だけ特定の問題を監視するトレースに限定してこのイベント クラスを使用するようにします。  
  
 Showplan XML ドキュメントには、スキーマが関連付けられています。 このスキーマは、 [Microsoft Web サイト](https://go.microsoft.com/fwlink/?LinkId=41740)で提供されています。また、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインストールの一部として提供されています。  
  
## <a name="showplan-xml-event-class-data-columns"></a>Showplan XML イベント クラスのデータ列  
  
|データ列名|データ型|説明|列 ID|フィルターの適用|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|`nvarchar`|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスへの接続を作成したクライアント アプリケーションの名前。 この列には、プログラムの表示名ではなく、アプリケーションによって渡された値が格納されます。|10|はい|  
|BinaryData|`image`|クエリのコストの推定値。|2|いいえ|  
|ClientProcessID|`int`|クライアント アプリケーションが実行されているプロセスに対し、ホスト コンピューターが割り当てた ID。 クライアントでクライアント プロセス ID が指定されると、このデータ列が作成されます。|9|はい|  
|DatabaseID|`int`|USE *database* ステートメントで指定されたデータベースの ID、または特定のインスタンスについて USE *database*ステートメントが実行されていない場合は既定のデータベースの ID となります。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] では、ServerName データ列がトレースにキャプチャされ、そのサーバーが利用可能な場合、データベースの名前が表示されます。 データベースに対応する値は、DB_ID 関数を使用して特定します。|3|はい|  
|DatabaseName|`nvarchar`|データベースの名前です。|35|いいえ|  
|Event Class|`int`|イベントの種類 = 122。|27|いいえ|  
|EventSequence|`int`|要求内の特定のイベントのシーケンス。|51|いいえ|  
|GroupID|`int`|SQL トレース イベントが発生したワークロード グループの ID。|66|はい|  
|HostName|`nvarchar`|クライアントが実行されているコンピューターの名前。 このデータ列には、クライアントがホスト名を指定している場合にデータが格納されます。 ホスト名を指定するには、HOST_NAME 関数を使用します。|8|はい|  
|Integer Data|`integer`|返される行数の推定値。|25|はい|  
|IsSystem|`int`|イベントがシステム プロセスとユーザー プロセスのどちらで発生したか。 1 はシステム、0 はユーザーです。|60|はい|  
|LineNumber|`int`|エラーを含む行番号を表示します。|5|はい|  
|LoginName|`nvarchar`|ユーザーのログイン名 ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セキュリティ ログインまたは DOMAIN\username という形式の [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows ログイン資格情報)。|11|はい|  
|LoginSID|`image`|ログイン ユーザーのセキュリティ ID 番号 (SID)。 この情報は、sys.server_principals カタログ ビューで参照できます。 各 SID はサーバーのログインごとに一意です。|41|いいえ|  
|NestLevel|`int`|@@NESTLEVEL から返されるデータを表す整数。|29|はい|  
|NTDomainName|`nvarchar`|ユーザーが所属する Windows ドメイン。|7|はい|  
|ObjectID|`int`|システムによって割り当てられたオブジェクト ID。|22|はい|  
|ObjectName|`nvarchar`|参照されているオブジェクトの名前。|34|はい|  
|ObjectType|`int`|イベントに関係するオブジェクトの種類を表す値。 この値は sys.objects カタログ ビューの type 列に対応します。 値については、「 [ObjectType トレース イベント列](objecttype-trace-event-column.md)」を参照してください。|28|はい|  
|RequestID|`int`|ステートメントが含まれている要求の ID。|49|はい|  
|ServerName|`nvarchar`|トレースされている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスの名前。|26|いいえ|  
|SessionLoginName|`nvarchar`|セッションを開始したユーザーのログイン名。 たとえば、Login1 を使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続し、Login2 でステートメントを実行すると、SessionLoginName には Login1 が表示され、LoginName には Login2 が表示されます。 この列には、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインと Windows ログインの両方が表示されます。|64|[はい]|  
|SPID|`int`|イベントが発生したセッションの ID。|12|はい|  
|StartTime|`datetime`|イベントの開始時刻 (取得できた場合)。|14|[はい]|  
|TextData|`ntext`|トレースでキャプチャされたイベント クラスに依存するテキスト値。|1|はい|  
|TransactionID|`bigint`|システムによって割り当てられたトランザクション ID。|4|はい|  
|XactSequence|`bigint`|現在のトランザクションを説明するトークン。|50|はい|  
  
## <a name="see-also"></a>参照  
 [拡張イベント](../extended-events/extended-events.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)   
 [プラン表示の論理操作と物理操作のリファレンス](../showplan-logical-and-physical-operators-reference.md)  
  
  
