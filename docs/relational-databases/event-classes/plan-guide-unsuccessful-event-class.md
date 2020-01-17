---
title: Plan Guide Unsuccessful イベント クラス | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- Plan Guide Unsuccessful event class
ms.assetid: ef9759f8-5613-4884-9257-86b609313f69
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: eb11261f8ff099874ebadbdaffb02b5c8706aa02
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67940708"
---
# <a name="plan-guide-unsuccessful-event-class"></a>Plan Guide Unsuccessful イベント クラス
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Plan Guide Unsuccessful イベント クラスは、プラン ガイドを含むクエリまたはバッチに対する実行プランを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が生成できなかったことを示します。 この場合、プラン ガイドは使用されずにプランがコンパイルされています。 このイベントは、次の条件に該当する場合に発生します。  
  
-   プラン ガイド定義のバッチまたはモジュールが、実行されているバッチと一致する。  
  
-   プラン ガイド定義のクエリが、実行されているクエリと一致する。  
  
-   USE PLAN を含めプラン ガイド定義のヒントがクエリまたはバッチに正常に適用されていない。 つまり、コンパイルされたクエリ プランには指定されたヒントが適用されず、プラン ガイドは使用されずにプランがコンパイルされている。  
  
 無効なプラン ガイドが原因でこのイベントが発生する場合があります。 クエリまたはバッチで使用されるプラン ガイドを [sys.fn_validate_plan_guide](../../relational-databases/system-functions/sys-fn-validate-plan-guide-transact-sql.md) 関数を使用して検証し、この関数で報告されたエラーを修正します。  
  
 このイベントは、 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] の Tuning テンプレートに含まれています。  
  
## <a name="plan-guide-unsuccessful-event-class-data-columns"></a>Plan Guide Unsuccessful イベント クラスのデータ列  
  
|データ列名|データ型|[説明]|列 ID|フィルターの適用|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|**nvarchar**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスへの接続を作成したクライアント アプリケーションの名前。 この列には、プログラムの表示名ではなく、アプリケーションによって渡された値が格納されます。|10|はい|  
|ClientProcessID|**int**|クライアント アプリケーションが実行されているプロセスに対し、ホスト コンピューターが割り当てた ID。 クライアントによりクライアント プロセス ID が指定されると、このデータ列に値が格納されます。|9|はい|  
|DatabaseID|**int**|USE *database* ステートメントで指定されたデータベースの ID、または特定のインスタンスについて USE *database* ステートメントが実行されていない場合は既定のデータベースの ID となります。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] では、ServerName データ列がトレースにキャプチャされ、そのサーバーが利用可能な場合、データベースの名前が表示されます。 データベースに対応する値は、DB_ID 関数を使用して特定します。|3|はい|  
|DatabaseName|**nvarchar**|ユーザーのステートメントが実行されているデータベースの名前。|35|はい|  
|EventClass|**int**|イベントの種類 = 218。|27|いいえ|  
|EventSequence|**int**|要求内の特定のイベントのシーケンス。|51|いいえ|  
|HostName|**nvarchar**|クライアントが実行されているコンピューターの名前。 このデータ列にはクライアントからホスト名が提供されている場合に値が格納されます。 ホスト名を指定するには、HOST_NAME 関数を使用します。|8|はい|  
|IsSystem|**int**|システム プロセスまたはユーザー プロセスのどちらでイベントが発生したのかを示します。1 はシステム、0 はユーザーです。|60|はい|  
|LoginName|**nvarchar**|ユーザーのログイン名 (DOMAIN [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] username [!INCLUDE[msCoName](../../includes/msconame-md.md)] の形式で表された\\*セキュリティ ログインまたは*Windows ログイン資格情報)。|11|はい|  
|LoginSid|**image**|ログイン ユーザーのセキュリティ ID 番号 (SID)。 この情報は、 [sys.server_principals](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md) カタログ ビューまたは [sys.sql_logins](../../relational-databases/system-catalog-views/sys-sql-logins-transact-sql.md) カタログ ビューで参照できます。 各 SID はサーバーのログインごとに一意です。|41|はい|  
|NTDomainName|**nvarchar**|ユーザーが所属する Windows ドメイン。|7|はい|  
|NTUserName|**nvarchar**|Windows のユーザー名。|6|はい|  
|ObjectID|**int**|プラン ガイドが適用されたときにコンパイルされていたモジュールのオブジェクト ID。 プラン ガイドがモジュールに適用されなかった場合、この列は NULL に設定されます。|22|はい|  
|RequestID|**int**|ステートメントが含まれている要求の ID。|49|はい|  
|ServerName|**nvarchar**|トレースされている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスの名前。|26|いいえ|  
|SessionLoginName|**nvarchar**|セッションを開始したユーザーのログイン名。 たとえば、Login1 を使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続し、Login2 でステートメントを実行すると、SessionLoginName には Login1 が表示され、LoginName には Login2 が表示されます。 この列には、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインと Windows ログインの両方が表示されます。|64|はい|  
|SPID|**int**|イベントが発生したセッションの ID。|12|はい|  
|StartTime|**datetime**|イベントの開始時刻 (取得できた場合)。|14|はい|  
|TextData|**ntext**|プラン ガイドの名前です。|1|はい|  
|TransactionID|**bigint**|システムによって割り当てられたトランザクション ID。|4|はい|  
|XactSequence|**bigint**|現在のトランザクションを説明するトークン。|50|はい|  
  
## <a name="see-also"></a>参照  
 [Plan Guide Successful イベント クラス](../../relational-databases/event-classes/plan-guide-successful-event-class.md)   
 [拡張イベント](../../relational-databases/extended-events/extended-events.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [sys.fn_validate_plan_guide &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-validate-plan-guide-transact-sql.md)   
 [sp_create_plan_guide &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)   
 [sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
  
