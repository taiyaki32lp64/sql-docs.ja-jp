---
title: Exchange Spill イベント クラス | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Exchange Spill event class
ms.assetid: fb876cec-f88d-4975-b3fd-0fb85dc0a7ff
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0220e81325345e84524ec0218dbaff7d6143bdd8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62663680"
---
# <a name="exchange-spill-event-class"></a>Exchange Spill イベント クラス
  **Exchange Spill** イベント クラスは、並列クエリ プランの通信バッファーが一時的に **tempdb** データベースに書き込まれたことを示します。 これは、クエリ プランに複数の範囲スキャンがある場合に限り、まれに発生します。  
  
 通常、そのような範囲スキャンを生成する [!INCLUDE[tsql](../../includes/tsql-md.md)] クエリには、多くの BETWEEN 操作が含まれています。各 BETWEEN 操作では、テーブルまたはインデックスから行の範囲を選択します。 または、式を使用して複数の範囲を取得できます (T.a > 10 AND T.a \< 20) または (T.a > 100 AND T.a \< 120)。 さらに、クエリ プランでは、このような範囲を順番にスキャンする必要があります。これは T.a に ORDER BY 句があり、プラン内の反復子で並べ替え順に組を使用することが必要なためです。  
  
 このようなクエリのクエリ プランに複数の **Parallelism** 操作が含まれているときは、 **Parallelism** 操作によって使用されるメモリ通信バッファーがいっぱいになり、その結果クエリの実行の進行が停止するという状況が起こります。 このような状況では、 **Parallelism** 操作のいずれかにより、入力バッファーの行を使用できるように、出力バッファーが **tempdb** に書き込まれます (この操作を *Exchange Spill*と呼びます)。 最終的には、書き込まれた行は、コンシューマーでその行を使用する準備が整ったときにコンシューマーに返されます。  
  
 同じ実行プラン内で複数の Exchange Spill を行うことができますが、これによって非常にまれにクエリの実行速度が低下する場合があります。 同じクエリ プランの実行内に 5 つを超える書き込みがある場合は、サポート担当者に問い合わせてください。  
  
 Exchange Spill は一時的なもので、データの分布が変更されると解消されることがあります。  
  
 Exchange Spill イベントを回避するには、いくつかの方法があります。  
  
-   結果セットを並べ替える必要がない場合は、ORDER BY 句を省略します。  
  
-   ORDER BY が必要な場合は、複数の範囲スキャンに参加する列 (上記の例の T.a) を ORDER BY 句から削除します。  
  
-   インデックス ヒントを使用して、オプティマイザーが当該のテーブルの別のアクセス パスを使用するようにします。  
  
-   別のクエリ実行プランを生成するようにクエリを書き直します。  
  
-   クエリの末尾またはインデックス操作に MAXDOP = 1 オプションを追加することにより、クエリを連続して実行させます。 詳細については、「 [max degree of parallelism サーバー構成オプションの構成](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md) 」および「 [並列インデックス操作の構成](../indexes/configure-parallel-index-operations.md)」を参照してください。  
  
> [!IMPORTANT]  
>  クエリ オプティマイザーが実行プランを生成するときに **Exchange Spill** イベントが発生している場所を特定するには、トレースで Showplan イベント クラスも収集する必要があります。 ノード ID を返さない **Showplan Text** イベント クラスと **Showplan Text (Unencoded)** イベント クラスを除く、任意の Showplan イベント クラスを選択できます。 Showplans のノード ID で、クエリ オプティマイザーがクエリ実行プランの生成時に実行する各操作が特定されます。 これらの操作はオペレーターと呼ばれ、Showplan の各オペレーターにはノード ID があります。 **Exchange Spill** イベントの **ObjectID** 列は Showplan のノード ID に対応するので、エラーの原因であるオペレーターつまり操作を判別できます。  
  
## <a name="exchange-spill-event-class-data-columns"></a>Exchange Spill イベント クラスのデータ列  
  
|データ列名|データ型|説明|列 ID|フィルターの適用|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**ApplicationName**|**nvarchar**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスへの接続を作成したクライアント アプリケーションの名前。 この列には、プログラムの表示名ではなく、アプリケーションによって渡された値が格納されます。|10|はい|  
|**ClientProcessID**|**int**|クライアント アプリケーションが実行されているプロセスに対し、ホスト コンピューターが割り当てた ID。 クライアントによりクライアント プロセス ID が指定されると、このデータ列に値が格納されます。|9|はい|  
|**DatabaseID**|**int**|USE *database* ステートメントで指定されたデータベースの ID、または特定のインスタンスについて USE *database* ステートメントが実行されていない場合は既定のデータベースの ID となります。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] では、 **ServerName** データ列がトレースにキャプチャされ、そのサーバーが利用可能な場合、データベースの名前が表示されます。 データベースに対応する値は、DB_ID 関数を使用して特定します。|3|[はい]|  
|**DatabaseName**|**nvarchar**|ユーザーのステートメントが実行されているデータベースの名前。|35|はい|  
|**EventClass**|**int**|イベントの種類 = 127。|27|いいえ|  
|**EventSequence**|**int**|要求内の特定のイベントのシーケンス。|51|いいえ|  
|**EventSubClass**|**int**|イベント サブクラスの種類。<br /><br /> 1 = 書き込み開始<br /><br /> 2 = 書き込み終了|21|はい|  
|**GroupID**|**int**|SQL トレース イベントが発生したワークロード グループの ID。|66|[はい]|  
|**HostName**|**nvarchar**|クライアントが実行されているコンピューターの名前。 このデータ列にはクライアントからホスト名が提供されている場合に値が格納されます。 ホスト名を指定するには、HOST_NAME 関数を使用します。|8|はい|  
|**IsSystem**|**int**|イベントがシステム プロセスとユーザー プロセスのどちらで発生したか。 1 はシステム、0 はユーザーです。|60|はい|  
|**LoginName**|**nvarchar**|ユーザーのログイン名 ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セキュリティ ログインまたは *\<DOMAIN>\\<username\>* という形式の Windows ログイン資格情報)。|11|はい|  
|**LoginSid**|**image**|ログイン ユーザーのセキュリティ ID 番号 (SID)。 この情報は、 **master** データベースの **syslogins** テーブルにあります。 各 SID はサーバーのログインごとに一意です。|41|はい|  
|**NTDomainName**|**nvarchar**|ユーザーが所属する Windows ドメイン。|7|はい|  
|**NTUserName**|**nvarchar**|Windows のユーザー名。|6|はい|  
|**Exchange Spill**|**int**|システムによって割り当てられたオブジェクト ID。 Showplan のノード ID と一致します。|22|はい|  
|**RequestID**|**int**|ステートメントが含まれている要求の ID。|49|はい|  
|**ServerName**|**nvarchar**|トレースされている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスの名前。|26|いいえ|  
|**SessionLoginName**|**nvarchar**|セッションを開始したユーザーのログイン名。 たとえば、Login1 を使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続し、Login2 でステートメントを実行すると、 **SessionLoginName** には Login1 が表示され、 **LoginName** には Login2 が表示されます。 この列には、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインと Windows ログインの両方が表示されます。|64|[はい]|  
|**SPID**|**int**|イベントが発生したセッションの ID。|12|はい|  
|**StartTime**|**datetime**|イベントの開始時刻 (取得できた場合)。|14|[はい]|  
|**TransactionID**|**bigint**|システムによって割り当てられたトランザクション ID。|4|[はい]|  
|**XactSequence**|**bigint**|現在のトランザクションを説明するトークン。|50|[はい]|  
  
## <a name="see-also"></a>参照  
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)   
 [インデックス オプションの設定](../indexes/set-index-options.md)   
 [ALTER INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql)  
  
  
