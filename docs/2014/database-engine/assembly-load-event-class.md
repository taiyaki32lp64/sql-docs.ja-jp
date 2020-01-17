---
title: Assembly Load イベント クラス |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Assembly Load event class
ms.assetid: cfb0b69d-4ce0-4067-a3df-d82775e57886
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 17a2c847e906616c4555d37e641f76eeb73391ab
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66065258"
---
# <a name="assembly-load-event-class"></a>Assembly Load イベント クラス
  **Assembly Load** イベント クラスは、アセンブリの読み込み要求が実行されるときに発生します。  
  
 アセンブリの読み込みを監視するトレースに **Assembly Load** イベント クラスを含めます。 これは、共通言語ランタイム (CLR) を使用するクエリのトラブルシューティングを行う場合、CLR クエリが実行されているサーバーの実行速度の低下のトラブルシューティングを行う場合、アセンブリの読み込みに関してユーザー、データベース、成功、またはその他の情報を収集するためにサーバーを監視する場合に役に立ちます。  
  
## <a name="assembly-load-event-class-data-columns"></a>Assembly Load イベント クラスのデータ列  
  
|データ列名|データ型|説明|列 ID|フィルターの適用|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**ApplicationName**|**nvarchar**|読み込みを要求したアプリケーションの名前。|10|はい|  
|**ClientProcessID**|**int**|クライアント アプリケーションが実行されているプロセスに対し、ホスト コンピューターが割り当てた ID。 クライアントによりクライアント プロセス ID が指定されると、このデータ列に値が格納されます。|9|はい|  
|**DatabaseID**|**int**|USE database ステートメントで指定されたデータベースの ID、または特定のインスタンスについて USE database ステートメントが実行されていない場合は既定のデータベースの ID となります。 [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] では、 **ServerName** データ列がトレースにキャプチャされ、そのサーバーが利用可能な場合、データベースの名前が表示されます。 データベースに対応する値は、DB_ID 関数を使用して特定します。|3|はい|  
|**DatabaseName**|**nvarchar**|ユーザーのステートメントが実行されているデータベースの名前。|35|はい|  
|**EventSequence**|**int**|要求内の特定のイベントのシーケンス。|51|いいえ|  
|**GroupID**|**int**|SQL トレース イベントが発生したワークロード グループの ID。|66|はい|  
|**HostName**|**nvarchar**|クライアントが実行されているコンピューターの名前。 このデータ列にはクライアントからホスト名が提供されている場合に値が格納されます。 ホスト名を指定するには、HOST_NAME 関数を使用します。|8|はい|  
|**LoginName**|**nvarchar**|ユーザーのログイン名 ( [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] セキュリティ ログインまたは DOMAIN\username という形式の [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows ログイン資格情報)。|11|はい|  
|**LoginSID**|**image**|ログインしたユーザーのセキュリティ識別子 (SID)。 この情報は、 **sys.server_principals** カタログ ビューで参照できます。 各 SID はサーバーのログインごとに一意です。|41|はい|  
|**NTDomainName**|**nvarchar**|ユーザーが所属する Windows ドメイン。|7|はい|  
|**NTUserName**|**nvarchar**|Windows のユーザー名。|6|はい|  
|**Exchange Spill**|**int**|アセンブリ ID。|22|はい|  
|**ObjectName**|**nvarchar**|アセンブリの完全修飾名。|34|はい|  
|**RequestID**|**int**|ステートメントが含まれている要求の ID。|49|[はい]|  
|**ServerName**|**nvarchar**|トレースされている [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のインスタンスの名前。|26|いいえ|  
|**SessionLoginName**|**nvarchar**|セッションを開始したユーザーのログイン名。 たとえば、Login1 を使用して [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] に接続し、Login2 でステートメントを実行すると、 **SessionLoginName** には Login1 が表示され、 **LoginName** には Login2 が表示されます。 この列には、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ログインと Windows ログインの両方が表示されます。|64|はい|  
|**SPID**|**int**|イベントが発生したセッションの ID。|12|はい|  
|**StartTime**|**datetime**|イベントの開始時刻 (取得できた場合)。|14|はい|  
|**成功**|**int**|アセンブリの読み込みの成功 (1) または失敗 (0) を示します。|23|はい|  
|**TextData**|**ntext**|読み込みが成功した場合は "アセンブリの読み込み成功" が、それ以外の場合は "アセンブリの読み込み失敗"。|1|はい|  
  
## <a name="see-also"></a>参照  
 [拡張イベント](../relational-databases/extended-events/extended-events.md)   
 [アセンブリ &#40;データベース エンジン&#41;](../relational-databases/clr-integration/assemblies-database-engine.md)  
  
  
