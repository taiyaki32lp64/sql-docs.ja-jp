---
title: Showplan All for Query Compile イベント クラス | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- Showplan All for Query Compile event class
ms.assetid: bb1dc446-5e6c-43d6-9db8-78c76cc2e01f
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 480d2d238a82039fd04c1c960e74b0c9da57449e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67911102"
---
# <a name="showplan-all-for-query-compile-event-class"></a>Showplan All for Query Compile イベント クラス
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Showplan All for Query Compile イベント クラスは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で SQL ステートメントがコンパイルされるときに発生します。 Showplan 操作を識別するには、このイベント クラスを含めます。 含まれる情報は、Showplan XML For Query Compile イベント クラスで使用できる情報のサブセットです。  
  
 Showplan All for Query Compile イベント クラスにより、コンパイル時の完全なデータが表示されるので、Showplan All for Query Compile を含むトレースでは、パフォーマンスのオーバーヘッドが大幅に増加することがあります。 このパフォーマンスの低下を最小限に抑えるには、このイベント クラスの使用を、短期間だけ特定の問題を監視するトレースに制限します。  
  
 Showplan All for Query Compile イベント クラスをトレースに含めるときは、BinaryData データ列を選択する必要があります。 このデータ列を選択しないと、このイベント クラスの情報がトレースに表示されません。  
  
## <a name="showplan-all-for-query-compile-event-class-data-columns"></a>Showplan All for Query Compile イベント クラスのデータ列  
  
|データ列名|データ型|[説明]|列 ID|フィルターの適用|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|**nvarchar**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスへの接続を作成したクライアント アプリケーションの名前。 この列には、プログラムの表示名ではなく、アプリケーションによって渡された値が格納されます。|10|はい|  
|BinaryData|**image**|クエリのコストの推定値。|2|いいえ|  
|ClientProcessID|**int**|クライアント アプリケーションが実行されているプロセスに対し、ホスト コンピューターが割り当てた ID。 クライアントでクライアント プロセス ID が指定されると、このデータ列が作成されます。|9|はい|  
|DatabaseID|**int**|USE *database* ステートメントで指定されたデータベースの ID、または特定のインスタンスについて USE *database* ステートメントが実行されていない場合は既定のデータベースの ID となります。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] では、ServerName データ列がトレースにキャプチャされ、そのサーバーが利用可能な場合、データベースの名前が表示されます。 データベースに対応する値は、DB_ID 関数を使用して特定します。|3|はい|  
|DatabaseName|**nvarchar**|ユーザーのステートメントが実行されているデータベースの名前。|35|はい|  
|EventClass|**int**|イベントの種類 = 169。|27|いいえ|  
|EventSequence|**int**|要求内の特定のイベントのシーケンス。|51|いいえ|  
|GroupID|**int**|SQL トレース イベントが発生したワークロード グループの ID。|66|はい|  
|HostName|**nvarchar**|クライアントが実行されているコンピューターの名前。 このデータ列には、クライアントがホスト名を指定している場合にデータが格納されます。 ホスト名を指定するには、HOST_NAME 関数を使用します。|8|はい|  
|IntegerData|**int**|返される行数の推定値。|25|はい|  
|IsSystem|**int**|イベントがシステム プロセスとユーザー プロセスのどちらで発生したか。 1 はシステム、0 はユーザーです。|60|はい|  
|LineNumber|**int**|エラーを含む行番号を表示します。|5|はい|  
|LoginName|**nvarchar**|ユーザーのログイン名 ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セキュリティ ログイン、または DOMAIN\username の形式で表された [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows ログイン資格情報)。|11|はい|  
|LoginSID|**image**|ログイン ユーザーのセキュリティ ID 番号 (SID)。 この情報は、sys.server_principals カタログ ビューで参照できます。 各 SID はサーバーのログインごとに一意です。|41|いいえ|  
|NestLevel|**int**|@@NESTLEVEL から返されるデータを表す整数。|29|はい|  
|NTDomainName|**nvarchar**|ユーザーが所属する Windows ドメイン。|7|はい|  
|NTUserName|**nvarchar**|Windows のユーザー名。|6|はい|  
|ObjectID|**int**|システムによって割り当てられたオブジェクト ID。|22|はい|  
|ObjectName|**nvarchar**|参照されているオブジェクトの名前。|34|はい|  
|ObjectType|**int**|イベントに関係するオブジェクトの種類を表す値。 この値は sys.objects の type 列に対応します。 値については、「 [ObjectType トレース イベント列](../../relational-databases/event-classes/objecttype-trace-event-column.md)」を参照してください。|28|はい|  
|RequestID|**int**|ステートメントが含まれている要求の ID。|49|はい|  
|ServerName|**nvarchar**|トレースされている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスの名前。|26|いいえ|  
|SessionLoginName|**nvarchar**|セッションを開始したユーザーのログイン名。 たとえば、Login1 を使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続し、Login2 でステートメントを実行すると、SessionLoginName には Login1 が表示され、LoginName には Login2 が表示されます。 この列には、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインと Windows ログインの両方が表示されます。|64|はい|  
|SPID|**int**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によってクライアントに関連付けられたプロセスに割り当てられたサーバー プロセス ID。|12|はい|  
|StartTime|**datetime**|イベントの開始時刻 (取得できた場合)。|14|はい|  
|TransactionID|**bigint**|システムによって割り当てられたトランザクション ID。|4|はい|  
|XactSequence|**bigint**|現在のトランザクションを説明するトークン。|50|はい|  
  
## <a name="see-also"></a>参照  
 [拡張イベント](../../relational-databases/extended-events/extended-events.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [プラン表示の論理操作と物理操作のリファレンス](../../relational-databases/showplan-logical-and-physical-operators-reference.md)  
  
  
