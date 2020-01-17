---
title: Data File Auto Shrink イベント クラス | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Data File Auto Shrink event class
ms.assetid: ea02b01e-9f87-47ca-9117-afadc382fb45
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b65f0200dd91c3813be405d9186543732eea6741
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62663174"
---
# <a name="data-file-auto-shrink-event-class"></a>Data File Auto Shrink イベント クラス
  **Data File Auto Shrink** イベント クラスは、データ ファイルが自動的に圧縮されたことを示します。 このイベントは、ALTER DATABASE ステートメントを明示的に使用してデータ ファイルを圧縮した場合には発生しません。 データ ファイルのサイズ変更を監視するトレースに、 **Data File Auto Shrink** イベント クラスを含めます。  
  
 **Data File Auto Shrink** イベント クラスをトレースに含めても、データ ファイルが頻繁に圧縮されない限り、オーバーヘッドはそれほど発生しません。  
  
## <a name="data-file-auto-shrink-event-class-data-columns"></a>Data File Auto Shrink イベント クラスのデータ列  
  
|データ列名|データ型|説明|列 ID|フィルターの適用|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**ApplicationName**|**nvarchar**|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスへの接続を作成したクライアント アプリケーションの名前。 この列には、プログラムの表示名ではなく、アプリケーションによって渡された値が格納されます。|10|はい|  
|**ClientProcessID**|**Int**|クライアント アプリケーションが実行されているプロセスに対し、ホスト コンピューターが割り当てた ID。 クライアントでクライアント プロセス ID が指定されると、このデータ列が作成されます。|9|はい|  
|**DatabaseID**|**int**|USE *database* ステートメントで指定されたデータベースの ID、または特定のインスタンスについて USE *database* ステートメントが実行されていない場合は既定のデータベースの ID となります。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] では、 **ServerName** データ列がトレースにキャプチャされ、そのサーバーが利用可能な場合、データベースの名前が表示されます。 データベースに対応する値は、DB_ID 関数を使用して特定します。|3|[はい]|  
|**DatabaseName**|**nvarchar**|ユーザーのステートメントが実行されているデータベースの名前。|35|はい|  
|**Duration**|**bigint**|ファイルを圧縮するのに必要な時間 (ミリ秒)。|13|はい|  
|**EndTime**|**datetime**|自動圧縮の終了した時刻。|18|はい|  
|**EventClass**|**int**|記録されるイベントの種類 = 94。|27|いいえ|  
|**EventSequence**|**int**|バッチ内のイベント クラスのシーケンス。|51|いいえ|  
|**Filename**|**nvarchar**|圧縮されているファイルの論理名。|36|はい|  
|**HostName**|**nvarchar**|クライアントが実行されているコンピューターの名前。 このデータ列には、クライアントからホスト名が提供されている場合に値が格納されます。 ホスト名を指定するには、HOST_NAME 関数を使用します。|8|はい|  
|**IntegerData**|**int**|ファイルを圧縮する単位で、8 KB ページの倍数です。|25|[はい]|  
|**IsSystem**|**int**|イベントがシステム プロセスとユーザー プロセスのどちらで発生したか。 1 はシステム、0 はユーザーです。|60|はい|  
|**LoginName**|**nvarchar**|ユーザーのログイン名 ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セキュリティ ログインまたは DOMAIN\username という形式の [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows ログイン資格情報)。|11|[はい]|  
|**LoginSid**|**image**|ログイン ユーザーのセキュリティ ID 番号 (SID)。 この情報は、 **sys.server_principals** カタログ ビューで参照できます。 各 SID はサーバーのログインごとに一意です。|41|[はい]|  
|**NTDomainName**|**nvarchar**|ユーザーが所属する Windows ドメイン。|7|はい|  
|**ServerName**|**nvarchar**|トレースされている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスの名前。|26|いいえ|  
|**SessionLoginName**|**nvarchar**|セッションを開始したユーザーのログイン名。 たとえば、Login1 を使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続し、Login2 でステートメントを実行すると、 **SessionLoginName** には Login1 が表示され、 **LoginName** には Login2 が表示されます。 この列には、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインと Windows ログインの両方が表示されます。|64|はい|  
|**SPID**|**int**|イベントが発生したセッションの ID。|12|はい|  
|**StartTime**|**datetime**|イベントの開始時刻 (取得できた場合)。|14|はい|  
  
## <a name="see-also"></a>参照  
 [拡張イベント](../extended-events/extended-events.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)  
  
  
