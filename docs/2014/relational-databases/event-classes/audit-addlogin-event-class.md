---
title: Audit Addlogin イベント クラス | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Audit Addlogin event class
ms.assetid: 6e0633dc-889e-49ef-bace-3c50958db2dd
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9b40ec59f8d0f845528bb644631142ee89af03dc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62912166"
---
# <a name="audit-addlogin-event-class"></a>Audit Addlogin イベント クラス
  **Audit Addlogin** イベント クラスは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインが追加または削除されたときに発生します。  
  
 このログインを追加するときに、既定のデータベースなど別のプロパティを設定すると、そのプロパティに関する情報がこのイベントの **TextData** 列に表示されます。 ログインの追加中にこれらのプロパティを設定した場合、 **Audit Login Change Property Event** は発生しません。  
  
 この監査イベントは、 **sp_addlogin** ストアド プロシージャおよび **sp_droplogin** ストアド プロシージャで使用します。  
  
 このイベント クラスは、今後のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]で廃止される可能性があります。 代わりに、 **Audit Server Principal Management** イベント クラスを使用することを推奨します。  
  
## <a name="audit-addlogin-event-class-data-columns"></a>Audit Addlogin イベント クラスのデータ列  
  
|データ列名|データ型|説明|列 ID|フィルターの適用|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**ApplicationName**|**nvarchar**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスへの接続を作成したクライアント アプリケーションの名前。 この列には、プログラムの表示名ではなく、アプリケーションによって渡された値が格納されます。|10|はい|  
|**ClientProcessID**|**int**|クライアント アプリケーションが実行されているプロセスに対し、ホスト コンピューターが割り当てた ID。 クライアントによりクライアント プロセス ID が指定されると、このデータ列に値が格納されます。|9|はい|  
|**DatabaseID**|**int**|USE *database* ステートメントで指定されたデータベースの ID、または特定のインスタンスについて USE *database* ステートメントが実行されていない場合は既定のデータベースの ID となります。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] では、 **ServerName** データ列がトレースにキャプチャされ、そのサーバーが利用可能な場合、データベースの名前が表示されます。 データベースに対応する値は、DB_ID 関数を使用して特定します。|3|はい|  
|**DatabaseName**|**nvarchar**|ユーザーのステートメントが実行されているデータベースの名前。|35|[はい]|  
|**EventClass**|**int**|イベントの種類 = 104。|27|いいえ|  
|**EventSequence**|**int**|要求内の特定のイベントのシーケンス。|51|いいえ|  
|**EventSubClass**|**int**|イベント サブクラスの種類。<br /><br /> 1 = 追加<br /><br /> 2 = 削除|21|[はい]|  
|**HostName**|**nvarchar**|クライアントが実行されているコンピューターの名前。 このデータ列にはクライアントからホスト名が提供されている場合に値が格納されます。 ホスト名を指定するには、HOST_NAME 関数を使用します。|8|はい|  
|**IsSystem**|**int**|イベントがシステム プロセスとユーザー プロセスのどちらで発生したか。 1 はシステム、0 はユーザーです。|60|はい|  
|**LoginName**|**nvarchar**|ユーザーのログイン名 ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セキュリティ ログイン、または DOMAIN\username の形式で表された [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows ログイン資格情報)。|11|はい|  
|**LoginSid**|**image**|ログイン ユーザーのセキュリティ ID 番号 (SID)。 この情報は、 **sys.server_principals** カタログ ビューで参照できます。 各 SID はサーバーのログインごとに一意です。|41|はい|  
|**NTDomainName**|**nvarchar**|ユーザーが所属する Windows ドメイン。|7|はい|  
|**NTUserName**|**nvarchar**|Windows のユーザー名。|6|はい|  
|**RequestID**|**int**|ステートメントが含まれている要求の ID。|49|はい|  
|**ServerName**|**nvarchar**|トレースされている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスの名前。|26|いいえ|  
|**SessionLoginName**|**Nvarchar**|セッションを開始したユーザーのログイン名。 たとえば、Login1 を使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続し、Login2 でステートメントを実行すると、 **SessionLoginName** には Login1 が表示され、 **LoginName** には Login2 が表示されます。 この列には、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインと Windows ログインの両方が表示されます。|64|はい|  
|**SPID**|**int**|イベントが発生したセッションの ID。|12|はい|  
|**StartTime**|**datetime**|イベントの開始時刻 (取得できた場合)。|14|はい|  
|**成功**|**int**|1 = 成功。 0 = 失敗。 たとえば、値 1 は権限チェックの成功を示し、値 0 は失敗を示します。|23|はい|  
|**TargetLoginName**|**nvarchar**|追加または削除するログイン名。|42|はい|  
|**TargetLoginSid**|**image**|(パラメーターとして渡された場合) 対象ログインのセキュリティ ID 番号 (SID)。|43|はい|  
|**TransactionID**|**bigint**|システムによって割り当てられたトランザクション ID。|4|はい|  
|**XactSequence**|**bigint**|現在のトランザクションを説明するトークン。|50|はい|  
  
## <a name="see-also"></a>関連項目  
 [拡張イベント](../extended-events/extended-events.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)   
 [Audit Login Change Property イベント クラス](audit-login-change-property-event-class.md)   
 [sp_addlogin &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addlogin-transact-sql)   
 [sp_droplogin &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-droplogin-transact-sql)   
 [Audit Server Principal Management イベント クラス](audit-server-principal-management-event-class.md)  
  
  
