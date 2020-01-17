---
title: Showplan Text (Unencoded) イベント クラス | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Showplan Text (Unencoded) event class
ms.assetid: 0aad4563-8caf-4971-92af-55992bc5ff2c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: bd9f8c6ca62fdd9f9a856a19f3d27c2144073b52
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62650376"
---
# <a name="showplan-text-unencoded-event-class"></a>Showplan Text (Unencoded) イベント クラス
  Showplan Text (Unencoded) イベント クラスは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で SQL ステートメントが実行されたときに発生します。 このイベント クラスは、Showplan Text イベント クラスと同じです。ただし、イベント情報がバイナリ データとしてではなく、文字列としてフォーマットされます。  
  
 含まれる情報は、Showplan All、Showplan XML、Showplan XML Statistics Profile イベント クラスで利用できる情報のサブセットです。  
  
 Showplan Text (Unencoded) イベント クラスをトレースに含めると、オーバーヘッドの量によっては、パフォーマンスが大幅に低下する可能性があります。 Showplan Text (Unencoded) では、他の Showplan イベント クラスほどはオーバーヘッドが発生しません。 オーバーヘッドの発生を最小限に抑えるには、このイベント クラスの使用を、短時間に特定の問題を監視するトレースに制限します。  
  
## <a name="showplan-text-unencoded-event-class-data-columns"></a>Showplan Text (Unencoded) イベント クラスのデータ列  
  
|データ列名|データ型|説明|列 ID|フィルターの適用|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|`nvarchar`|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスへの接続を作成したクライアント アプリケーションの名前。 この列には、プログラムの表示名ではなく、アプリケーションによって渡された値が格納されます。|10|[はい]|  
|BinaryData|`image`|トレースでキャプチャされたイベント クラスに依存するバイナリ値。|2|はい|  
|ClientProcessID|`int`|クライアント アプリケーションが実行されているプロセスに対し、ホスト コンピューターが割り当てた ID。 クライアントによりクライアント プロセス ID が指定されると、このデータ列に値が格納されます。|9|はい|  
|DatabaseID|`int`|USE *database* ステートメントで指定されたデータベースの ID、または特定のインスタンスについて USE *database* ステートメントが実行されていない場合は既定のデータベースの ID となります。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] では、ServerName データ列がトレースにキャプチャされ、そのサーバーが利用可能な場合、データベースの名前が表示されます。 データベースに対応する値は、DB_ID 関数を使用して特定します。|3|はい|  
|DatabaseName|`nvarchar`|ユーザーのステートメントが実行されているデータベースの名前。|35|はい|  
|EventClass|`int`|イベントの種類 = 68。|27|いいえ|  
|EventSequence|`int`|要求内の特定のイベントのシーケンス。|51|いいえ|  
|GroupID|`int`|SQL トレース イベントが発生したワークロード グループの ID。|66|はい|  
|HostName|`nvarchar`|クライアントが実行されているコンピューターの名前。 このデータ列にはクライアントからホスト名が提供されている場合に値が格納されます。 ホスト名を指定するには、HOST_NAME 関数を使用します。|8|はい|  
|IntegerData|`int`|トレースでキャプチャされたイベント クラスに依存する整数値。|25|はい|  
|IsSystem|`int`|イベントがシステム プロセスとユーザー プロセスのどちらで発生したか。 1 はシステム、0 はユーザーです。|60|はい|  
|LineNumber|`int`|エラーを含む行番号を表示します。|5|[はい]|  
|LoginName|`nvarchar`|ユーザーのログイン名 ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セキュリティ ログインまたは DOMAIN\username という形式の [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows ログイン資格情報)。|11|はい|  
|LoginSid|`image`|ログイン ユーザーのセキュリティ ID 番号 (SID)。 この情報は、sys.server_principals カタログ ビューで参照できます。 各 SID はサーバーのログインごとに一意です。|41|はい|  
|NestLevel|`int`|@@NESTLEVEL から返されるデータを表す整数。|29|はい|  
|NTDomainName|`nvarchar`|ユーザーが所属する Windows ドメイン。|7|はい|  
|NTUserName|`nvarchar`|Windows のユーザー名。|6|はい|  
|ObjectID|`int`|システムによって割り当てられたオブジェクト ID。|22|はい|  
|ObjectName|`nvarchar`|参照されているオブジェクトの名前。|34|はい|  
|ObjectType|`int`|イベントに関係するオブジェクトの種類を表す値。 この値は sys.objects カタログ ビューの type 列に対応します。 値については、「 [ObjectType トレース イベント列](objecttype-trace-event-column.md)」を参照してください。|28|はい|  
|RequestID|`int`|ステートメントが含まれている要求の ID。|49|はい|  
|ServerName|`nvarchar`|トレースされている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスの名前。|26|いいえ|  
|SessionLoginName|`nvarchar`|セッションを開始したユーザーのログイン名。 たとえば、Login1 を使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続し、Login2 でステートメントを実行すると、SessionLoginName には Login1 が表示され、LoginName には Login2 が表示されます。 この列には、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインと Windows ログインの両方が表示されます。|64|はい|  
|SPID|`int`|イベントが発生したセッションの ID。|12|はい|  
|StartTime|`datetime`|イベントの開始時刻 (取得できた場合)。|14|はい|  
|TextData|`ntext`|トレースでキャプチャされたイベント クラスに依存するテキスト値。|1|はい|  
|TransactionID|`bigint`|システムによって割り当てられたトランザクション ID。|4|はい|  
|XactSequence|`bigint`|現在のトランザクションを説明するトークン。|50|はい|  
  
## <a name="see-also"></a>参照  
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)   
 [プラン表示の論理操作と物理操作のリファレンス](../showplan-logical-and-physical-operators-reference.md)   
 [Showplan All イベント クラス](showplan-all-event-class.md)   
 [Showplan XML イベント クラス](showplan-xml-event-class.md)   
 [Showplan XML Statistics Profile イベント クラス](showplan-xml-statistics-profile-event-class.md)  
  
  
