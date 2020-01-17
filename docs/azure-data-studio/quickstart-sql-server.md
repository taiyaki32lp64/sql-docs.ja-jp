---
title: 'クイック スタート: SQL Server に対する接続およびクエリ'
titleSuffix: Azure Data Studio
description: このクイック スタートでは、Azure Data Studio を使用して SQL Server に接続し、クエリを実行する方法を示します
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: quickstart
author: yualan
ms.author: alayu
ms.reviewer: alayu; sstein
ms.custom: seodec18, sqlfreshmay19
ms.date: 08/02/2019
ms.openlocfilehash: a218c2afa89c8798c46b305e80e677693509e7ab
ms.sourcegitcommit: 495913aff230b504acd7477a1a07488338e779c6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2019
ms.locfileid: "68810805"
---
# <a name="quickstart-connect-and-query-sql-server-using-includename-sosincludesname-sos-shortmd"></a>クイック スタート: [!INCLUDE[name-sos](../includes/name-sos-short.md)] を使用した SQL Server に対する接続およびクエリ

このクイック スタートでは、[!INCLUDE[name-sos](../includes/name-sos-short.md)] を使用して SQL Server に接続し、Transact-SQL (T-SQL) ステートメントを使用して、[!INCLUDE[name-sos](../includes/name-sos-short.md)] チュートリアルで使用する *TutorialDB* を作成する方法を示します。

## <a name="prerequisites"></a>Prerequisites

このクイックスタートを完了するには、[!INCLUDE[name-sos](../includes/name-sos-short.md)] と、SQL Server へのアクセス権が必要です。

- [[!INCLUDE[name-sos](../includes/name-sos-short.md)] をインストールする](download.md)。

SQL Server へのアクセス権がない場合は、次のリンクからご利用のプラットフォームを選択してください (SQL ログインとパスワードを忘れないでください)。

- [Windows - SQL Server 2017 Developer Edition をダウンロードする](https://www.microsoft.com/sql-server/sql-server-downloads)
- [macOS - Docker で SQL Server 2017 をダウンロードする](https://docs.microsoft.com/sql/linux/quickstart-install-connect-docker)
- [Linux - SQL Server 2017 Developer Edition をダウンロードする](https://docs.microsoft.com/sql/linux/sql-server-linux-overview#install) - 手順に従うだけで、*データを作成してクエリを実行する*ことができます。

## <a name="connect-to-a-sql-server"></a>SQL Server に接続する

1. **[!INCLUDE[name-sos](../includes/name-sos-short.md)]** を起動します。

2. 最初に [!INCLUDE[name-sos](../includes/name-sos-short.md)] を実行すると、**ウェルカム** ページが開きます。 **ウェルカム** ページが表示されない場合は、 **[ヘルプ]**  >  **[ようこそ]** を選択します。 **[新しい接続]** を選択して、 **[接続]** ウィンドウを開きます。

   ![新しい接続アイコン](media/quickstart-sql-server/new-connection-icon.png)

3. この記事では、*SQL ログイン*を使用しますが、*Windows 認証*はサポートされています。 次のようにフィールドに入力します。

- **サーバー名:** - ここにサーバー名を入力します。 たとえば、localhost です。
- **認証の種類:** SQL ログイン
- **ユーザー名:** SQL Server のユーザー名
- **パスワード:** SQL Server のパスワード
- **データベース名:** このフィールドは空白のままにします
- **サーバー グループ:** \<既定値\>

   ![新しい接続画面](media/quickstart-sql-server/new-connection-screen.png)

## <a name="create-a-database"></a>データベースの作成

次の手順では、**TutorialDB** という名前のデータベースを作成します。

1. ご利用のサーバー (**localhost**) を右クリックし、 **[新しいクエリ]** を選択します。

2. クエリ ウィンドウに次のスニペットを貼り付けてから、 **[実行]** を選択します。

 ```sql
 USE master
 GO
 IF NOT EXISTS (
  SELECT name
  FROM sys.databases
  WHERE name = N'TutorialDB'
 )
  CREATE DATABASE [TutorialDB];
 GO
 IF SERVERPROPERTY('ProductVersion') > '12'
  ALTER DATABASE [TutorialDB] SET QUERY_STORE=ON;
 GO
 ```

クエリが完了すると、新しい **TutorialDB** がデータベースの一覧に表示されます。 表示されない場合は、 **[データベース]** ノードを右クリックして **[最新の情報に更新]** を選択します。

   ![データベースの作成](media/quickstart-sql-server/create-database.png)

## <a name="create-a-table"></a>テーブルの作成

クエリ エディターはまだ *master* データベースに接続されていますが、*TutorialDB* データベースにテーブルを作成する必要があります。

1. 接続コンテキストを **TutorialDB** に変更します。

   ![変更コンテキスト](media/quickstart-sql-server/change-context.png)

2. クエリ ウィンドウに次のスニペットを貼り付けて、 **[実行]** をクリックします。

   > [!NOTE]
   > これを付け加えても、またはエディターで前のクエリを上書きしてもかまいません。 **[実行]** をクリックすると、選択されているクエリのみが実行されることに注意してください。 何も選択されていない場合、 **[実行]** をクリックすると、エディター内のすべてのクエリが実行されます。

 ```sql
 -- Create a new table called 'Customers' in schema 'dbo'
 -- Drop the table if it already exists
 IF OBJECT_ID('dbo.Customers', 'U') IS NOT NULL
  DROP TABLE dbo.Customers;
 GO
 -- Create the table in the specified schema
 CREATE TABLE dbo.Customers
 (
  CustomerId int NOT NULL PRIMARY KEY, -- primary key column
  Name nvarchar(50) NOT NULL,
  Location nvarchar(50) NOT NULL,
  Email nvarchar(50) NOT NULL
 );
 GO
 ```

クエリが完了すると、テーブルの一覧に新しい **Customers** テーブルが表示されます。 場合によっては、 **[TutorialDB] > [Tables]** ノードを右クリックして、 **[最新の情報に更新]** を選択します。

## <a name="insert-rows"></a>行を挿入する

- クエリ ウィンドウに次のスニペットを貼り付けて、 **[実行]** をクリックします。

 ```sql
 -- Insert rows into table 'Customers'
 INSERT INTO dbo.Customers
  ([CustomerId], [Name], [Location], [Email])
 VALUES
  ( 1, N'Orlando', N'Australia', N''),
  ( 2, N'Keith', N'India', N'keith0@adventure-works.com'),
  ( 3, N'Donna', N'Germany', N'donna0@adventure-works.com'),
  ( 4, N'Janet', N'United States', N'janet1@adventure-works.com')
 GO
 ```

## <a name="view-the-data-returned-by-a-query"></a>クエリによって返されるデータを表示する

1. クエリ ウィンドウに次のスニペットを貼り付けて、 **[実行]** をクリックします。

 ```sql
 -- Select rows from table 'Customers'
 SELECT * FROM dbo.Customers;
 ```

   ![結果の選択](media/quickstart-sql-server/select-results.png)

## <a name="next-steps"></a>次の手順

正常に SQL Server に接続し、クエリを実行することができたので、[コード エディターのチュートリアル](tutorial-sql-editor.md)をお試しいただけます。