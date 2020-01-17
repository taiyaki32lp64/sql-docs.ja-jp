---
title: ASP.NET アプリケーションでの SqlDependency
description: ASP.NET アプリケーションからクエリ通知を使用する方法を示します。
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: ff226ce3-f6b5-47a1-8d22-dc78b67e07f5
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 2115d087d837118b99ee3ffded9cae0003b6d4e0
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 10/16/2019
ms.locfileid: "72451964"
---
# <a name="sqldependency-in-an-aspnet-application"></a>ASP.NET アプリケーションでの SqlDependency

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[ADO.NET をダウンロードする](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

このセクションの例では、ASP.NET <xref:System.Web.Caching.SqlCacheDependency> オブジェクトを利用して <xref:Microsoft.Data.SqlClient.SqlDependency> を間接的に使用する方法を示します。 <xref:System.Web.Caching.SqlCacheDependency> オブジェクトは、<xref:Microsoft.Data.SqlClient.SqlDependency> を使用して通知をリッスンし、キャッシュを正しく更新します。  
  
> [!NOTE]
>  このサンプルコードでは、クエリ[通知](enable-query-notifications.md)を有効にするスクリプトを実行して、クエリ通知を有効にしていることを前提としています。  
  
## <a name="about-the-sample-application"></a>サンプルアプリケーションについて  
このサンプル アプリケーションでは、1 つの ASP.NET Web ページを使用して、SQL Server データベースである **AdventureWorks** に格納されている製品情報を <xref:System.Web.UI.WebControls.GridView> コントロールに表示します。 ページが読み込まれると、コードは現在の時刻を <xref:System.Web.UI.WebControls.Label> コントロールに書き込みます。 次に、<xref:System.Web.Caching.SqlCacheDependency> オブジェクトを定義し、キャッシュデータを格納するためのプロパティを <xref:System.Web.Caching.Cache> オブジェクトに最大3分間設定します。 次に、データベースに接続し、データを取得します。 ページが読み込まれ、アプリケーションが実行されると、ASP.NET はキャッシュからデータを取得します。これは、ページ上の時刻が変更されないことを確認できます。 監視対象のデータが変更された場合、ASP.NET はキャッシュを無効にして、`GridView` コントロールに新しいデータを再作成し、`Label` コントロールに表示される時間を更新します。  
  
## <a name="creating-the-sample-application"></a>サンプル アプリケーションの作成  
サンプルアプリケーションを作成して実行するには、次の手順に従います。  
  
1. 新しい ASP.NET Web サイトの作成  
  
2. <xref:System.Web.UI.WebControls.Label> と <xref:System.Web.UI.WebControls.GridView> コントロールを default.aspx ページに追加します。  
  
3. ページのクラスモジュールを開き、次のディレクティブを追加します。  
  
    ```csharp  
    using Microsoft.Data.SqlClient;  
    using System.Web.Caching;  
    ```  
  
4. ページの `Page_Load` イベントに次のコードを追加します。  
  
    [!code-csharp[DataWorks SqlDependency_Start#1](~/../sqlclient/doc/samples/SqlDependency_Start.cs#1)]
  
5. `GetConnectionString` と `GetSQL` の2つのヘルパーメソッドを追加します。 定義される接続文字列では、統合セキュリティが使用されます。 使用しているアカウントが、必要とされるデータベースへのアクセス許可を持っており、サンプル データベースの **AdventureWorks** で通知が有効になっていることを確認する必要があります。
  
    [!code-csharp[DataWorks SqlDependency_Start#2](~/../sqlclient/doc/samples/SqlDependency_Start.cs#2)]
  
### <a name="testing-the-application"></a>アプリケーションのテスト  
アプリケーションは Web フォームに表示されているデータをキャッシュし、アクティビティがない場合は3分ごとに更新します。 データベースに変更が発生した場合、キャッシュは直ちに更新されます。 ブラウザーにページを読み込む Visual Studio からアプリケーションを実行します。 キャッシュ更新時間は、キャッシュが最後に更新された日時を示します。 3分待ってからページを更新すると、ポストバックイベントが発生します。 ページに表示される時刻が変更されていることに注意してください。 ページを3分以内に更新すると、ページに表示される時刻は変わりません。  
  
次に、Transact-sql の UPDATE コマンドを使用してデータベース内のデータを更新し、ページを更新します。 表示された時刻は、キャッシュがデータベースの新しいデータで更新されたことを示します。 キャッシュは更新されますが、ページに表示される時間はポストバックイベントが発生するまで変更されないことに注意してください。  
  
## <a name="next-steps"></a>次の手順
- [SQL Server でのクエリ通知](query-notifications-sql-server.md)
