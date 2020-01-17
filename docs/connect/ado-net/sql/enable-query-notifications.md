---
title: クエリ通知の有効化
description: クエリ通知の使用方法について説明します。これには、クエリ通知の有効化と使用に関する要件も含まれます。
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: a5333e19-8e55-4aa9-82dc-ca8745e516ed
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 94b472a1fe040aa3a684d9f7b523ba09c82a651e
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452236"
---
# <a name="enabling-query-notifications"></a>クエリ通知の有効化

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[ADO.NET をダウンロードする](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

クエリ通知を使用するアプリケーションには、一般的な一連の要件があります。 SQL クエリ通知をサポートするには、データ ソースが正しく設定され、ユーザーがクライアント側およびサーバー側の正しい権限を所有している必要があります。  
  
クエリ通知を使用するには、次のことを行う必要があります。  
  
- データベースのクエリ通知を有効にします。  
  
- データベースへの接続に使用するユーザー ID に必要な権限があることを確認します。  
  
- <xref:Microsoft.Data.SqlClient.SqlCommand> オブジェクトを使用して、通知オブジェクト (<xref:Microsoft.Data.SqlClient.SqlDependency> または <xref:Microsoft.Data.Sql.SqlNotificationRequest> のいずれか) を持つ有効な SELECT ステートメントを実行します。  
  
- 監視対象のデータが変更された場合に通知を処理するコードを提供します。  
  
## <a name="query-notifications-requirements"></a>クエリ通知の要件  
クエリ通知は、特定の要件の一覧を満たす SELECT ステートメントでのみサポートされます。 次の表に、SQL Server オンラインブックの Service Broker およびクエリ通知に関するドキュメントへのリンクを示します。  
  
**SQL Server のドキュメント**  
  
- [通知のためのクエリの作成](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/ms181122(v=sql.105))  
  
- [Service Broker のセキュリティに関する注意点](https://docs.microsoft.com/previous-versions/sql/sql-server-2005/ms166059(v=sql.90))  
  
- [セキュリティと保護 (Service Broker)](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/bb522911(v=sql.105))  
  
- [Notification Services のセキュリティに関する注意点](https://docs.microsoft.com/previous-versions/sql/sql-server-2005/ms172604(v=sql.90))  
  
- [クエリ通知の権限](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/ms188311(v=sql.105))  
  
- [Service Broker の国際化に関する注意点](https://docs.microsoft.com/previous-versions/sql/sql-server-2005/ms166028(v=sql.90))  
  
- [ソリューション設計に関する考慮事項 (Service Broker)](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/bb522899(v=sql.105))  
  
- [Service Broker 開発者向けの情報](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/ms166100(v=sql.105))  
  
- [開発者ガイド (Service Broker)](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/bb522908(v=sql.105))  
  
## <a name="enabling-query-notifications-to-run-sample-code"></a>クエリ通知を有効にしてサンプルコードを実行する  
**AdventureWorks** データベースで Service Broker を有効にするには、SQL Server Management Studio を通じて、次の Transact-SQL ステートメントを実行します。  
  
`ALTER DATABASE AdventureWorks SET ENABLE_BROKER;`  
  
クエリ通知サンプルを正しく実行するには、データベースサーバーで次の Transact-sql ステートメントを実行する必要があります。  
  
```sql
CREATE QUEUE ContactChangeMessages;  
  
CREATE SERVICE ContactChangeNotifications  
  ON QUEUE ContactChangeMessages  
([http://schemas.microsoft.com/SQL/Notifications/PostQueryNotification]);  
```  
  
## <a name="query-notifications-permissions"></a>クエリ通知のアクセス許可  
通知を要求するコマンドを実行するユーザーは、サーバーに対するサブスクライブクエリ通知データベース権限を持っている必要があります。  
  
部分信頼の状況で実行されるクライアント側のコードには、<xref:Microsoft.Data.SqlClient.SqlClientPermission> が必要です。  
  
次のコードでは、<xref:Microsoft.Data.SqlClient.SqlClientPermission> オブジェクトを作成し、<xref:System.Security.Permissions.PermissionState> を <xref:System.Security.Permissions.PermissionState.Unrestricted> に設定しています。 呼び出し履歴の上位にあるすべての呼び出し元にアクセス許可が付与されていない場合、<xref:System.Security.CodeAccessPermission.Demand%2A> は実行時に <xref:System.Security.SecurityException> を強制します。  
  
[!code-csharp[DataWorks SqlClientPermission_Demand#1](~/../sqlclient/doc/samples/SqlClientPermission_Demand.cs#1)]
  
## <a name="choosing-a-notification-object"></a>通知オブジェクトの選択  
クエリ通知 API には、通知を処理するための2つのオブジェクトが用意されています。 <xref:Microsoft.Data.SqlClient.SqlDependency> と <xref:Microsoft.Data.Sql.SqlNotificationRequest> です。
  
### <a name="using-sqldependency"></a>SqlDependency の使用  
<xref:Microsoft.Data.SqlClient.SqlDependency> を使用するには、使用している SQL Server データベースに対して Service Broker を有効にし、通知を受け取るためのアクセス許可をユーザーに与える必要があります。 通知キューなどの Service Broker オブジェクトは事前に定義されています。  
  
さらに、<xref:Microsoft.Data.SqlClient.SqlDependency> は、キューにポストされるときに、通知を処理するためにワーカースレッドを自動的に起動します。また、Service Broker メッセージを解析して、情報をイベント引数データとして公開します。 <xref:Microsoft.Data.SqlClient.SqlDependency> は、データベースに対する依存関係を確立するために、`Start` メソッドを呼び出すことによって初期化する必要があります。 これは、必要なデータベース接続ごとに、アプリケーションの初期化中に1回だけ呼び出す必要がある静的メソッドです。 `Stop` メソッドは、実行された依存関係接続ごとに、アプリケーションの終了時に呼び出す必要があります。  
  
### <a name="using-sqlnotificationrequest"></a>SqlNotificationRequest の使用  
これに対し、<xref:Microsoft.Data.Sql.SqlNotificationRequest> では、リッスンしているインフラストラクチャ全体を自分で実装する必要があります。 さらに、キュー、サービス、キューでサポートされているメッセージの種類など、サポートされているすべての Service Broker オブジェクトが定義されている必要があります。 この手動によるアプローチは、アプリケーションが特別な通知メッセージや通知動作を必要とする場合や、アプリケーションが大規模な Service Broker アプリケーションの一部である場合に便利です。  
  
## <a name="next-steps"></a>次の手順
- [SQL Server でのクエリ通知](query-notifications-sql-server.md)
