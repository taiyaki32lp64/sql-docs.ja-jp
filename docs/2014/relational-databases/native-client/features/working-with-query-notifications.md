---
title: クエリ通知の操作 |マイクロソフトのドキュメント
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- data access [SQL Server Native Client], query notifications
- rowsets [SQL Server], notifications
- SQL Server Native Client, query notifications
- notifications [SQL Server Native Client]
- query notifications [SQL Server], SQL Server Native Client
- canceling rowset changes
- IRowsetNotify interface
- SQLNCLI, query notifications
- SQL Server Native Client OLE DB provider, query notifications
- consumer notification for rowset changes [SQL Server Native Client]
ms.assetid: 2f906fff-5ed9-4527-9fd3-9c0d27c3dff7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7a149e8940896210a408b36c7cb06814646fd322
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68206600"
---
# <a name="working-with-query-notifications"></a>クエリ通知の操作
  クエリ通知は、[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] および [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client で導入されました。 クエリ通知は [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] に導入された Service Broker インフラストラクチャに基づいて構築されており、データが変更されたときにクエリ通知を使用してアプリケーションに通知できます。 Web アプリケーションのように、データベースからの情報のキャッシュを用意し、データベースのデータが変更されたときに通知する必要があるアプリケーションでは、この機能が特に有用です。  
  
 クエリ通知を使用すると、クエリの基になるデータが変更された場合に、指定されたタイムアウト期間内に通知を要求することができます。 通知を要求する際は、サービス名、メッセージ テキスト、サーバーのタイムアウト値などの通知オプションを指定します。 通知は Service Broker キューを使用して配信されます。アプリケーションではこのキューにポーリングして、使用可能な通知を確認できます。  
  
 クエリ通知オプションの構文を次に示します。  
  
 `service=<service-name>[;(local database=<database> | broker instance=<broker instance>)]`  
  
 以下に例を示します。  
  
 `service=mySSBService;local database=mydb`  
  
 アプリケーションで通知サブスクリプションが作成された直後にそのアプリケーションが終了した場合、通知サブスクリプションを開始するプロセスが終了しても、通知サブスクリプションは有効です。 通知サブスクリプションが有効なままなので、通知サブスクリプションの作成時に指定したタイムアウト期間内にデータが変更されると、通知が行われます。 通知は、実行されるクエリ、通知オプション、およびメッセージ テキストによって識別されます。また、通知のタイムアウト値を 0 に設定して通知をキャンセルできます。  
  
 通知は、一度だけ送信されます。 データ変更の通知を連続して行う場合は、各通知が処理された後にクエリを再実行して、新しいサブスクリプションを作成する必要があります。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ネイティブ クライアント アプリケーションは通常を使用して通知を受信、 [!INCLUDE[tsql](../../../includes/tsql-md.md)] [受信](/sql/t-sql/statements/receive-transact-sql)コマンド通知オプションで指定されたサービスに関連付けられたキューから通知を読み取ります。  
  
> [!NOTE]  
>  通知を必要とするクエリ内のテーブル名は、`dbo.myTable` のように、修飾された名前にする必要があります。 テーブル名は、2 つの部分を持つ修飾名にする必要があります。 3 つまたは 4 つの部分を持つ名前を使用すると、サブスクリプションが無効になります。  
  
 この通知インフラストラクチャは、[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] で導入されたキュー処理機能に基づいて構築されています。 一般的に、サーバーで生成された通知は、後で処理するためにキュー経由で送信されます。  
  
 クエリ通知を使用するには、クエリとサービスがサーバー上に存在する必要があります。 次のような [!INCLUDE[tsql](../../../includes/tsql-md.md)] ステートメントを使用して、クエリやサービスを作成できます。  
  
```  
CREATE QUEUE myQueue  
CREATE SERVICE myService ON QUEUE myQueue   
  
([https://schemas.microsoft.com/SQL/Notifications/PostQueryNotification])  
```  
  
> [!NOTE]  
>  上記のように、サービスでは定義済みのコントラクト `https://schemas.microsoft.com/SQL/Notifications/PostQueryNotification` を使用する必要があります。  
  
## <a name="sql-server-native-client-ole-db-provider"></a>SQL Server Native Client OLE DB プロバイダー  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダー行セットの変更をコンシューマーに通知をサポートしています。 コンシューマーは、行セットの変更のすべてのフェーズで、任意の変更が試行されたときに通知を受け取ります。  
  
> [!NOTE]  
>  通知クエリを使用して、サーバーに渡す**icommand::execute**唯一の有効な方法でクエリ通知をサブスクライブするには、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダー。  
  
### <a name="the-dbpropsetsqlserverrowset-property-set"></a>DBPROPSET_SQLSERVERROWSET プロパティ セット  
 OLE DB により、クエリ通知をサポートするために[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client は、DBPROPSET_SQLSERVERROWSET プロパティ セットに、次の新しいプロパティを追加します。  
  
|名前|型|説明|  
|----------|----------|-----------------|  
|SSPROP_QP_NOTIFICATION_TIMEOUT|VT_UI4|クエリ通知をアクティブのままにしておく秒数。<br /><br /> 既定値は 432,000 秒 (5 日) です。 最小値は 1 秒であり、最大値は 2^31-1 秒です。|  
|SSPROP_QP_NOTIFICATION_MSGTEXT|VT_BSTR|通知のメッセージ テキスト。 これはユーザーが定義するため、あらかじめ定義済みの書式はありません。<br /><br /> 既定では、文字列が空です。 1 ～ 2,000 文字を使用してメッセージを指定できます。|  
|SSPROP_QP_NOTIFICATION_OPTIONS|VT_BSTR|クエリ通知オプション。 これらは *name*=*value* 構文を使用した文字列で指定されます。 ユーザーがサービスを作成して、キューから通知を読み取る必要があります。<br /><br /> 既定値は空の文字列です。|  
  
 ステートメントがユーザー トランザクションで実行されたか自動コミットで実行されたか、また、ステートメントが実行されたトランザクションがコミットされたかロールバックされたかに関係なく、通知サブスクリプションは必ずコミットされます。 サーバー通知は、次の無効通知条件のいずれかが最初に発生したときに起動します。通知条件は、基になるデータまたはスキーマが変更されるか、タイムアウト期間に到達するかです。 通知登録は、起動直後に削除されます。 したがって、通知を受け取った後も引き続き更新するには、アプリケーションで再度サブスクライブする必要があります。  
  
 他の接続またはスレッドは、接続先キューに通知があるかどうかを確認できます。 以下に例を示します。  
  
```  
WAITFOR (RECEIVE * FROM MyQueue);   // Where MyQueue is the queue name.   
```  
  
 SELECT * を指定してもキューのエントリは削除されませんが、RECEIVE \* FROM を指定すると削除されます。 このため、キューが空の場合は、サーバー スレッドが保留されます。 呼び出し時にキュー エントリがあれば、それらがすぐに返されます。それ以外の場合、呼び出しは、キュー エントリが作成されるまで待機します。  
  
```  
RECEIVE * FROM MyQueue  
```  
  
 キューが空の場合、このステートメントは空の結果セットを直ちに返します。それ以外の場合、すべてのキュー通知を返します。  
  
 SSPROP_QP_NOTIFICATION_MSGTEXT と SSPROP_QP_NOTIFICATION_OPTIONS が NULL 以外で、かつ空ではない場合、上記で定義された 3 つのプロパティを含んでいるクエリ通知 TDS ヘッダーが、コマンドが実行されるたびにサーバーに送信されます。 どちらかが NULL (または空) の場合、クエリ通知 TDS ヘッダーは送信されず、DB_E_ERRORSOCCURED (または、プロパティが両方とも省略可能に設定されている場合は DB_S_ERRORSOCCURED) が発生し、状態値が DBPROPSTATUS_BADVALUE に設定されます。 実行または準備の時点で検証が行われます。 同様に、クエリ通知プロパティが [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] より前のバージョンの [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] への接続に対して設定されている場合は、DB_S_ERRORSOCCURED が発生します。 この場合の状態値は DBPROPSTATUS_NOTSUPPORTED です。  
  
 サブスクリプションが開始されても、後続のメッセージが正常に配信されるかどうかは保証されません。 また、指定されたサーバー名の妥当性に関するチェックは行われません。  
  
> [!NOTE]  
>  ステートメントの準備フェーズではサブスクリプションが開始されることはありません。サブスクリプションは、ステートメントを実行したときにのみ開始されます。また、OLE DB Core Services を使用してもクエリ通知は影響を受けません。  
  
 DBPROPSET_SQLSERVERROWSET プロパティ セットの詳細については、次を参照してください。[行セット プロパティと動作](../../native-client-ole-db-rowsets/rowset-properties-and-behaviors.md)します。  
  
## <a name="sql-server-native-client-odbc-driver"></a>SQL Server Native Client ODBC ドライバー  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーに 3 つの新しい属性の追加により、クエリ通知をサポートしている、 [SQLGetStmtAttr](../../native-client-odbc-api/sqlgetstmtattr.md)と[SQLSetStmtAttr](../../native-client-odbc-api/sqlsetstmtattr.md)関数。  
  
-   SQL_SOPT_SS_QUERYNOTIFICATION_MSGTEXT  
  
-   SQL_SOPT_SS_QUERYNOTIFICATION_OPTIONS  
  
-   SQL_SOPT_SS_QUERYNOTIFICATION_TIMEOUT  
  
 SQL_SOPT_SS_QUERYNOTIFICATION_MSGTEXT と SQL_SOPT_SS_QUERYNOTIFICATION_OPTIONS が NULL 以外の場合、上記で定義された 3 つの属性を含むクエリ通知 TDS ヘッダーが、コマンドを実行するたびにサーバーに送信されます。 どちらかが NULL の場合、クエリ通知 TDS ヘッダーは送信されず、SQL_SUCCESS_WITH_INFO が返されます。 検証が行われます。 [SQLPrepare 関数](https://go.microsoft.com/fwlink/?LinkId=59360)、 **SqlExecDirect**、および**SqlExecute**、すべての属性が有効でない場合に失敗します。 同様に、これらのクエリ通知属性が [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] より前のバージョンの [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] に対して設定されている場合、SQL_SUCCESS_WITH_INFO によって実行が失敗します。  
  
> [!NOTE]  
>  ステートメントの準備段階では、サブスクリプションが開始されることはありません。サブスクリプションを開始できるのは、ステートメントを実行したときのみです。  
  
## <a name="special-cases-and-restrictions"></a>特別なケースおよび制限  
 通知では、次のデータ型がサポートされていません。  
  
-   `text`  
  
-   `ntext`  
  
-   `image`  
  
 これらのいずれかのデータ型を返すクエリに対して通知要求を作成すると、通知サブスクリプションが不可能であるという通知が、すぐに発行されます。  
  
 バッチまたはストアド プロシージャに対するサブスクリプション要求を作成すると、そのバッチまたはストアド プロシージャ内で実行される各ステートメントに対して、別個のサブスクリプション要求が作成されます。 EXECUTE ステートメントは通知を登録せず、実行されるコマンドへ通知要求を送信します。 バッチの場合、実行されるステートメントに対してコンテキストが適用され、さらに同様のルールが適用されます。  
  
 既存のアクティブなサブスクリプションと同じテンプレート、パラメーター値、通知 ID、および配信場所を持つ通知のクエリを、同じユーザーが同じデータベース コンテキストで送信すると、既存のサブスクリプションが更新され、新しく指定されたタイムアウトが再設定されます。つまり、同一内容の複数のクエリに対して通知を要求した場合、通知は 1 つだけ送信されます。 バッチ内で重複するクエリや、ストアド プロシージャ内で複数回呼び出されたクエリにも、これが当てはまります。  
  
## <a name="see-also"></a>参照  
 [SQL Server Native Client の機能](sql-server-native-client-features.md)  
  
  
