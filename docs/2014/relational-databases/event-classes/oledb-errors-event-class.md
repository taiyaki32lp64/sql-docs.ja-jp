---
title: OLEDB Errors イベント クラス | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- OLEDB Errors event class
ms.assetid: 0ce1e906-5d92-42f2-ab38-8771ad5ca008
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9a0f4e99247fe1a4a80734e56d8db1e05b961e43
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62961072"
---
# <a name="oledb-errors-event-class"></a>OLEDB Errors イベント クラス
  OLEDB Errors イベント クラスは、OLE DB プロバイダーの呼び出しによってエラーが返された場合に [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で発生します。 OLE DB プロバイダーから報告された HRESULT エラーを表示する場合に、このイベント クラスをトレースに追加します。  
  
 OLEDB Errors イベント クラスをトレースに追加した場合、それに伴うオーバーヘッドは、トレース中、データベースに関する OLE DB プロバイダー エラーがどの程度の頻度で発生するかによって異なります。 OLE DB プロバイダー エラーが頻繁に発生する場合は、トレースを実行することによってパフォーマンスが著しく低下する可能性があります。  
  
## <a name="oledb-errors-event-class-data-columns"></a>OLEDB Errors イベント クラスのデータ列  
  
|データ列名|データ型|説明|列 ID|フィルターの適用|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|`nvarchar`|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスへの接続を作成したクライアント アプリケーションの名前。 この列には、プログラムの表示名ではなく、アプリケーションによって渡された値が格納されます。|10|はい|  
|ClientProcessID|`int`|クライアント アプリケーションが実行されているプロセスに対し、ホスト コンピューターが割り当てた ID。 クライアントによりクライアント プロセス ID が指定されると、このデータ列に値が格納されます。|9|はい|  
|DatabaseID|`int`|USE *database* ステートメントで指定されたデータベースの ID、または特定のインスタンスについて USE database ステートメントが実行されていない場合は既定の *database* となります。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] では、ServerName データ列がトレースにキャプチャされ、そのサーバーが利用可能な場合、データベースの名前が表示されます。 データベースに対応する値は、DB_ID 関数を使用して特定します。|3|はい|  
|DatabaseName|`nvarchar`|ユーザーのステートメントが実行されているデータベースの名前。|35|はい|  
|[エラー]|`int`|プロバイダーによって返される HRESULT。|31|はい|  
|EventClass|`int`|イベントの種類 = 61。|27|いいえ|  
|EventSequence|`int`|バッチ内の OLE DB イベント クラスのシーケンス。|51|いいえ|  
|GroupID|`int`|SQL トレース イベントが発生したワークロード グループの ID。|66|はい|  
|HostName|`nvarchar`|クライアントが実行されているコンピューターの名前。 このデータ列にはクライアントからホスト名が提供されている場合に値が格納されます。 ホスト名を指定するには、HOST_NAME 関数を使用します。|8|[はい]|  
|IsSystem|`int`|イベントがシステム プロセスとユーザー プロセスのどちらで発生したか。 1 はシステム、0 はユーザーです。|60|はい|  
|LinkedServerName|`nvarchar`|リンク サーバーの名前|45|はい|  
|LoginName|`nvarchar`|ユーザーのログイン名 ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セキュリティ ログインまたは DOMAIN\username という形式の [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows ログイン資格情報)。|11|はい|  
|LoginSid|`image`|ログイン ユーザーのセキュリティ ID 番号 (SID)。 この情報は、sys.server_principals カタログ ビューで参照できます。 各 SID はサーバーのログインごとに一意です。|41|[はい]|  
|MethodName|`nvarchar`|OLE DB メソッドの名前。|47|はい|  
|NTDomainName|`nvarchar`|ユーザーが所属する Windows ドメイン。|7|はい|  
|NTUserName|`nvarchar`|Windows のユーザー名。|6|はい|  
|ProviderName|`nvarchar`|OLE DB プロバイダーの名前です。|46|はい|  
|RequestID|`int`|ステートメントが含まれている要求の ID。|49|はい|  
|SessionLoginName|`nvarchar`|セッションを開始したユーザーのログイン名。 たとえば、Login1 を使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続し、Login2 でステートメントを実行すると、SessionLoginName には Login1 が表示され、LoginName には Login2 が表示されます。 この列には、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインと Windows ログインの両方が表示されます。|64|はい|  
|SPID|`int`|イベントが発生したセッションの ID。|12|はい|  
|StartTime|`datetime`|イベントの開始時刻 (取得できた場合)。|14|はい|  
|TextData|`nvarchar`|OLE DB 呼び出しで送受信されるパラメーター。|1|いいえ|  
|TransactionID|`bigint`|システムによって割り当てられたトランザクション ID。|4|はい|  
  
## <a name="see-also"></a>参照  
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)   
 [Transact-SQL での OLE オートメーション オブジェクト](../stored-procedures/ole-automation-objects-in-transact-sql.md)  
  
  
