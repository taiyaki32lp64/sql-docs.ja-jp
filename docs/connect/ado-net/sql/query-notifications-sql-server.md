---
title: SQL Server でのクエリ通知
description: .NET アプリケーションが、データが変更されたときに SQL Server から通知を要求する方法について説明します。
ms.date: 08/15/2019
ms.assetid: 0f0ba1a1-3180-4af8-87f7-c795dc8f8f55
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: d47241e3656e3ca7b4f5ea0eebe9f2cc8b571bf6
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452074"
---
# <a name="query-notifications-in-sql-server"></a>SQL Server でのクエリ通知

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[ADO.NET をダウンロードする](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

クエリ通知は Service Broker インフラストラクチャに基づいて構築されており、データが変更されたときにクエリ通知を使用してアプリケーションに通知できます。 Web アプリケーションのように、データベースからの情報のキャッシュを用意し、データベースのデータが変更されたときに通知する必要があるアプリケーションでは、この機能が特に有用です。  
  
ADO.NET を使用してクエリ通知を実装するには、次の3つの方法があります。  
  
- 低レベルの実装は、サーバー側の機能を公開する `SqlNotificationRequest` クラスによって提供されます。これにより、通知要求でコマンドを実行できるようになります。  
  
- 高レベルの実装は、`SqlDependency` クラスによって提供されます。このクラスは、ソースアプリケーションと SQL Server の間で通知機能の高度な抽象化を提供し、依存関係を使用してサーバーの変更を検出できるようにします。 マネージド クライアント アプリケーションが Microsoft SqlClient Data Provider for SQL Server を使用して SQL Server の通知機能を活用するには、ほとんどの場合、これが最も簡単かつ効果的な方法です。  
  
- さらに、ASP.NET 2.0 以降を使用して構築された Web アプリケーションは、`SqlCacheDependency` ヘルパー クラスを使用できます。  
  
クエリ通知は、基になるデータの変更に応じて表示またはキャッシュを更新する必要があるアプリケーションに使用されます。 Microsoft SQL Server では、最初に取得したものと異なる結果セットが同じコマンドで得られた場合には、.NET アプリケーションから SQL Server にコマンドを送信して通知を要求することができます。 サーバーで生成された通知は、後で処理するためにキュー経由で送信されます。  
  
SELECT ステートメントと EXECUTE ステートメントの通知を設定できます。 EXECUTE ステートメントを使用する場合、SQL Server EXECUTE ステートメント自体ではなく、実行されたコマンドの通知を登録します。 コマンドは、SELECT ステートメントの要件と制限を満たしている必要があります。 通知を登録するコマンドに複数のステートメントが含まれている場合、Database Engine によりバッチ内のステートメントごとに通知が作成されます。  
  
データ変更時に、信頼できる即時の通知が必要なアプリケーションを開発している場合は、SQL Server オンライン ブックの「[通知の計画](https://go.microsoft.com/fwlink/?LinkId=211984)」の「**効率的なクエリ通知方法の計画**」および「**クエリ通知に代わる方法**」を参照してください。 クエリ通知と SQL Server Service Broker の詳細については、SQL Server オンラインブックのトピックへの次のリンクを参照してください。  
  
**SQL Server のドキュメント**  
  
- [クエリ通知の使用](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/ms175110(v=sql.105))  
  
- [通知のためのクエリの作成](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/ms181122(v=sql.105))  
  
- [開発 (Service Broker)](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/bb522889(v=sql.105))  
  
- [Service Broker 開発者向けの情報](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/ms166100(v=sql.105))  
  
- [開発者ガイド (Service Broker)](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/bb522908(v=sql.105))  
  
## <a name="in-this-section"></a>このセクションの内容  
[クエリ通知の有効化](enable-query-notifications.md)  
クエリ通知の使用方法について説明します。これには、クエリ通知の有効化と使用に関する要件も含まれます。  
  
[ASP.NET アプリケーションでの SqlDependency](sqldependency-aspnet-app.md)  
ASP.NET アプリケーションからクエリ通知を使用する方法を示します。  
  
[SqlDependency を使用した変更の検出](detect-changes-sqldependency.md)  
クエリの結果が最初に受信したものと異なる場合を検出する方法を示します。  
  
[SqlCommand の実行と SqlNotificationRequest](sqlcommand-execution-sqlnotificationrequest.md)  
クエリ通知を使用するように <xref:Microsoft.Data.SqlClient.SqlCommand> オブジェクトを構成する方法を示します。  
  
## <a name="reference"></a>リファレンス  
<xref:Microsoft.Data.Sql.SqlNotificationRequest>  
<xref:Microsoft.Data.Sql.SqlNotificationRequest> クラスとそのすべてのメンバーについて説明します。  
  
<xref:Microsoft.Data.SqlClient.SqlDependency>  
<xref:Microsoft.Data.SqlClient.SqlDependency> クラスとそのすべてのメンバーについて説明します。  
  
<xref:System.Web.Caching.SqlCacheDependency>  
<xref:System.Web.Caching.SqlCacheDependency> クラスとそのすべてのメンバーについて説明します。  
  
## <a name="next-steps"></a>次の手順
- [SQL Server と ADO.NET](index.md)
