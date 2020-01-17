---
title: クエリ通知の操作 |Microsoft Docs
description: OLE DB Driver for SQL Server でのクエリ通知の操作
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- data access [OLE DB Driver for SQL Server], query notifications
- rowsets [SQL Server], notifications
- OLE DB Driver for SQL Server, query notifications
- notifications [OLE DB Driver for SQL Server]
- query notifications [SQL Server], OLE DB Driver for SQL Server
- canceling rowset changes
- IRowsetNotify interface
- MSOLEDBSQL, query notifications
- OLE DB Driver for SQL Server, query notifications
- consumer notification for rowset changes [OLE DB Driver for SQL Server]
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 29aaab523b3a754c65b1b7a0312ceb5ea122f2d3
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419319"
---
# <a name="working-with-query-notifications"></a>クエリ通知の操作

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

クエリ通知は、および[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] OLE DB Driver for SQL Server で導入されました。 クエリ通知は SQL Server 2005 (9.x) に導入された SQL Service Broker インフラストラクチャに基づいて構築されており、データが変更されたときにアプリケーションに通知できます。 Web アプリケーションのように、データベースから情報のキャッシュを提供し、ソース データが変更されたときに通知を受ける必要があるアプリケーションでは、この機能が特に有用です。

クエリ通知を使用すると、クエリの基になるデータが変更されたときに、指定したタイムアウト期間内に通知を要求できます。 要求する際は、サービス名、メッセージ テキスト、サーバーのタイムアウト値などの通知オプションを指定します。 通知は Service Broker キューを使用して配信されます。アプリケーションではこのキューにポーリングして、使用可能な通知を確認できます。

クエリ通知オプションの構文を次に示します。

`service=<service-name>[;(local database=<database> | broker instance=<broker instance>)]`

 例:

`service=mySSBService;local database=mydb`

通知配信登録は、それらを開始するプロセスを直後します。 これは、アプリケーションが通知配信登録を作成して終了する可能性があるためです。 サブスクリプションが有効なままなので、サブスクリプションの作成時に指定したタイムアウト期間内にデータが変更されると、通知が行われます。 通知は、実行されたクエリ、通知オプション、およびメッセージテキストによって識別されます。 タイムアウト値を0に設定して取り消すことができます。

通知は、一度だけ送信されます。 データの変更を継続的に通知するには、各通知が処理された後でクエリを再実行して、新しいサブスクリプションを作成します。

SQL Server アプリケーションの OLE DB ドライバーは、通常、 [!INCLUDE[tsql](../../../includes/tsql-md.md)] [RECEIVE](../../../t-sql/statements/receive-transact-sql.md)コマンドを使用して通知を受信します。 このコマンドを使用して、通知オプションで指定されたサービスに関連付けられているキューから通知を読み取ります。

> [!NOTE]
> 通知を必要とするクエリ内のテーブル名は、修飾された名前にする必要があります。 たとえば、`dbo.myTable` のようになります。 テーブル名は、2 つの部分を持つ修飾名にする必要があります。 3 つまたは 4 つの部分を持つ名前を使用すると、サブスクリプションが無効になります。

この通知インフラストラクチャは、[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] で導入されたキュー処理機能に基づいて構築されています。 一般的に、サーバーで生成された通知は、後で処理するためにキュー経由で送信されます。

クエリ通知を使用するには、クエリとサービスがサーバー上に存在する必要があります。 これらは、次のような[!INCLUDE[tsql](../../../includes/tsql-md.md)]コマンドを使用して作成できます。

```sql
CREATE QUEUE myQueue
CREATE SERVICE myService ON QUEUE myQueue
([https://schemas.microsoft.com/SQL/Notifications/PostQueryNotification])
```

> [!NOTE]
> 上記のように、サービスでは定義済みのコントラクトを使用する必要があります。

## <a name="ole-db-driver-for-sql-server"></a>OLE DB Driver for SQL Server

OLE DB Driver for SQL Server は、行セットの変更時のコンシューマー通知をサポートしています。 コンシューマーは、行セットの変更のすべてのフェーズと、変更が試行されたときに通知を受け取ります。

> [!NOTE]
> OLE DB Driver for SQL Server を使用してクエリ通知をサブスクライブする場合、唯一の有効な方法は、**ICommand::Execute** を使用してサーバーに通知クエリを渡す方法です。

### <a name="dbpropsetsqlserverrowset-property-set"></a>DBPROPSET_SQLSERVERROWSET プロパティ セット

OLE DB によるクエリ通知をサポートするために、次の新しいプロパティが OLE DB Driver for SQL Server の `DBPROPSET_SQLSERVERROWSET` プロパティ セットに追加されました。

|[オブジェクト名]|型|[説明]|
|----------|----------|-----------------|
|SSPROP_QP_NOTIFICATION_TIMEOUT|VT_UI4|クエリ通知をアクティブのままにしておく秒数。<br /><br /> 既定値は 432,000 秒 (5 日) です。 最小値は 1 秒であり、最大値は 2^31-1 秒です。|
|SSPROP_QP_NOTIFICATION_MSGTEXT|VT_BSTR|通知のメッセージ テキスト。 このテキストはユーザーが定義するため、定義済みの書式はありません。<br /><br /> 既定では、文字列は空です。 1 ~ 2000 文字のメッセージを指定してください。|
|SSPROP_QP_NOTIFICATION_OPTIONS|VT_BSTR|クエリ通知オプション。 これらは *name*=*value* 構文を使用した文字列で指定されます。 ユーザーがサービスを作成して、キューから通知を読み取る必要があります。<br /><br /> 既定値は空の文字列です。|

通知サブスクリプションは常にコミットされます。 これは、ステートメントがユーザートランザクションで実行されたか、自動コミットで実行されたか、またはステートメントが実行されたトランザクションがコミットまたはロールバックされたかに関係なく発生します。 サーバー通知は、次の無効通知条件のいずれかが最初に発生したときに起動します。通知条件は、基になるデータまたはスキーマが変更されるか、タイムアウト期間に到達するかです。 

通知登録は、起動直後に削除されます。 したがって、通知を受け取った後も引き続き更新するには、アプリケーションで再度サブスクライブする必要があります。

他の接続またはスレッドは、接続先キューに通知があるかどうかを確認できます。 例:

```sql
WAITFOR (RECEIVE * FROM MyQueue); -- Where MyQueue is the queue name.
```

> [!NOTE]
> `SELECT *`キューからエントリを削除しません。 ただし、 `RECEIVE * FROM`はです。 このため、キューが空の場合は、サーバー スレッドが保留されます。 呼び出し時にキューエントリがある場合は、直ちに返されます。 それ以外の場合、呼び出しはキューエントリが作成されるまで待機します。

```sql
RECEIVE * FROM MyQueue
```

このステートメントは、キューが空の場合、すぐに空の結果セットを返します。 それ以外の場合は、すべてのキュー通知を返します。

`SSPROP_QP_NOTIFICATION_MSGTEXT` と`SSPROP_QP_NOTIFICATION_OPTIONS`が null 以外で空でない場合は、上記で定義された3つのプロパティを含むクエリ通知 TDS ヘッダーがサーバーに送信されます。 これは、コマンドの実行のたびに発生します。 これらのいずれかが null (または空) の場合、ヘッダーは`DB_E_ERRORSOCCURRED`送信されず`DB_S_ERRORSOCCURRED`に発生します (または、プロパティが両方とも省略可能としてマークされている場合は、発生します)。 次に、状態の値を`DBPROPSTATUS_BADVALUE`に設定します。 検証は、実行と準備の際に行われます。 同様に、クエリ通知プロパティが [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] より前のバージョンの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] への接続に対して設定されている場合は、`DB_S_ERRORSOCCURED` が発生します。 この場合の状態値は`DBPROPSTATUS_NOTSUPPORTED`です。

サブスクリプションが開始されても、後続のメッセージが正常に配信されるかどうかは保証されません。 指定されたサーバー名の妥当性に関するチェックも行われません。

> [!NOTE]
> ステートメントを準備しても、サブスクリプションが開始されることはありません。 ステートメントの実行のみが開始されます。 OLE DB コアサービスを使用しても、クエリ通知は影響を受けません。

プロパティセットの`DBPROPSET_SQLSERVERROWSET`詳細については、「[行セットのプロパティと動作](../../oledb/ole-db-rowsets/rowset-properties-and-behaviors.md)」を参照してください。

## <a name="see-also"></a>参照

[OLE DB Driver for SQL Server の機能](../../oledb/features/oledb-driver-for-sql-server-features.md)
