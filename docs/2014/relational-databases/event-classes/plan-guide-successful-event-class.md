---
title: Plan Guide Successful イベント クラス | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Plan Guide Successful event class
ms.assetid: fecfbb6c-56c9-4db4-84d3-00d6e338355a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 56157ce2c29a95d35198ab44835b50e45d7831a4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62827205"
---
# <a name="plan-guide-successful-event-class"></a>Plan Guide Successful イベント クラス
  Plan Guide Successful イベント クラスは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がプラン ガイドを含むクエリまたはバッチに対する実行プラン ガイドを正常に生成したことを示します。 このイベントは、次の条件に該当する場合に発生します。  
  
-   プラン ガイド定義のバッチまたはモジュールが、実行されているバッチまたはモジュールと一致する。  
  
-   プラン ガイド定義のクエリが、実行されているクエリと一致する。  
  
-   USE PLAN を含めプラン ガイド定義のヒントが正常にクエリに適用されている。 つまり、コンパイルされたクエリ プランには指定されたヒントが適用されている。  
  
## <a name="plan-guide-successful-event-class-data-columns"></a>Plan Guide Successful イベント クラスのデータ列  
  
|データ列名|データ型|説明|列 ID|フィルターの適用|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|`nvarchar`|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスへの接続を作成したクライアント アプリケーションの名前。 この列には、プログラムの表示名ではなく、アプリケーションによって渡された値が格納されます。|10|はい|  
|ClientProcessID|`int`|クライアント アプリケーションが実行されているプロセスに対し、ホスト コンピューターが割り当てた ID。 クライアントによりクライアント プロセス ID が指定されると、このデータ列に値が格納されます。|9|はい|  
|DatabaseID|`int`|USE *database* ステートメントで指定されたデータベースの ID、または特定のインスタンスについて USE *database* ステートメントが実行されていない場合は既定のデータベースの ID となります。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] では、ServerName データ列がトレースにキャプチャされ、そのサーバーが利用可能な場合、データベースの名前が表示されます。 データベースに対応する値は、DB_ID 関数を使用して特定します。|3|はい|  
|DatabaseName|`nvarchar`|ユーザーのステートメントが実行されているデータベースの名前。|35|はい|  
|EventClass|`int`|イベントの種類 = 214。|27|いいえ|  
|EventSequence|`int`|要求内の特定のイベントのシーケンス。|51|いいえ|  
|HostName|`nvarchar`|クライアントが実行されているコンピューターの名前。 このデータ列にはクライアントからホスト名が提供されている場合に値が格納されます。 ホスト名を指定するには、HOST_NAME 関数を使用します。|8|はい|  
|IsSystem|`int`|システム プロセスまたはユーザー プロセスのどちらでイベントが発生したのかを示します。1 はシステム、0 はユーザーです。|60|はい|  
|LoginName|`nvarchar`|ユーザーのログイン名 (DOMAIN [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] username [!INCLUDE[msCoName](../../includes/msconame-md.md)] の形式で表された\\*セキュリティ ログインまたは*Windows ログイン資格情報)。|11|はい|  
|LoginSid|`image`|ログイン ユーザーのセキュリティ ID 番号 (SID)。 この情報は、 [sys.server_principals](/sql/relational-databases/system-catalog-views/sys-server-principals-transact-sql) カタログ ビューまたは [sys.sql_logins](/sql/relational-databases/system-catalog-views/sys-sql-logins-transact-sql) カタログ ビューで参照できます。 各 SID はサーバーのログインごとに一意です。|41|[はい]|  
|NTDomainName|`nvarchar`|ユーザーが所属する Windows ドメイン。|7|はい|  
|NTUserName|`nvarchar`|Windows のユーザー名。|6|はい|  
|ObjectID|`int`|プラン ガイドが適用されたときにコンパイルされていたモジュールのオブジェクト ID。 プラン ガイドがモジュールに適用されなかった場合、この列は NULL に設定されます。|22|はい|  
|RequestID|`int`|ステートメントを含んでいる要求の ID。|49|はい|  
|ServerName|`nvarchar`|トレースされている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスの名前。|26|いいえ|  
|SessionLoginName|`nvarchar`|セッションを開始したユーザーのログイン名。 たとえば、Login1 を使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続し、Login2 でステートメントを実行すると、SessionLoginName には Login1 が表示され、LoginName には Login2 が表示されます。 この列には、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインと Windows ログインの両方が表示されます。|64|はい|  
|SPID|`int`|イベントが発生したセッションの ID。|12|はい|  
|StartTime|`datetime`|イベントの開始時刻 (取得できた場合)。|14|はい|  
|TextData|`ntext`|プラン ガイドの名前です。|1|はい|  
|TransactionID|`bigint`|システムによって割り当てられたトランザクション ID。|4|はい|  
|XactSequence|`bigint`|現在のトランザクションを説明するトークン。|50|はい|  
  
## <a name="see-also"></a>関連項目  
 [Plan Guide Unsuccessful イベント クラス](plan-guide-unsuccessful-event-class.md)   
 [拡張イベント](../extended-events/extended-events.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)  
  
  
