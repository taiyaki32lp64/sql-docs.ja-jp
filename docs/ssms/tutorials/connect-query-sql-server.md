---
title: SQL Server Management Studio (SSMS) を使用して SQL Server インスタンスに接続し、クエリを行う
description: SQL Server Management Studio を使用し、基本的な T-SQL クエリを実行して SQL Server インスタンスに接続するためのチュートリアルです。
keywords: SQL Server, SSMS, SQL Server Management Studio
author: MashaMSFT
ms.author: mathoma
ms.reviewer: sstein
ms.topic: quickstart
ms.prod_service: sql-tools
ms.prod: sql
ms.technology: ssms
ms.custom: ''
ms.date: 03/13/2018
ms.openlocfilehash: eaf544085bfe6040bdf9f54300eb733ee4fd92f0
ms.sourcegitcommit: 8732161f26a93de3aa1fb13495e8a6a71519c155
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/01/2019
ms.locfileid: "71708330"
---
# <a name="tutorial-connect-to-and-query-a-sql-server-instance-by-using-sql-server-management-studio-ssms"></a>チュートリアル:SQL Server Management Studio (SSMS) を使用して SQL Server インスタンスに接続し、クエリを行う

このチュートリアルでは、SQL Server Management Studio (SSMS) を使って SQL Server インスタンスに接続し、いくつかの基本的な Transact-SQL (T-SQL) コマンドを実行する方法を説明します。 この記事では、以下の手順を行う方法を示します。

> [!div class="checklist"]
> * SQL Server インスタンスに接続する
> * データベース ("TutorialDB") を作成する
> * 新しいデータベースにテーブル ("Customers") を作成する
> * 新しいテーブルに行を挿入する
> * 新しいテーブルにクエリを行って結果を表示する
> * クエリ ウィンドウのテーブルを使用して接続のプロパティを確認する
> * クエリ ウィンドウが接続するサーバーを変更する

## <a name="prerequisites"></a>Prerequisites

このチュートリアルを実行するには、SQL Server Management Studio と SQL Server インスタンスへのアクセスが必要です。 

* [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) をインストールする。

SQL Server インスタンスへのアクセス権を持っていない場合は、次のリンクからプラットフォームを選択します。 SQL 認証を選択する場合は、SQL Server のログイン資格情報を使用します。

* **Windows**:[SQL Server 2017 Developer Edition をダウンロードする](https://www.microsoft.com/sql-server/sql-server-downloads)。
* **macOS**:[Docker で SQL Server 2017 をダウンロードする](https://docs.microsoft.com/sql/linux/quickstart-install-connect-docker)。

## <a name="connect-to-a-sql-server-instance"></a>SQL Server インスタンスに接続する

1. [SQL Server Management Studio] を起動します。 SSMS を初めて実行すると、 **[サーバーへの接続]** ウィンドウが開きます。 開かない場合は、 **[オブジェクト エクスプローラー]**  >  **[接続]**  >  **[データベース エンジン]** の順に選択して、手動で開くことができます。

    ![オブジェクト エクスプローラーの接続リンク](media/connect-query-sql-server/connectobjexp.png)

2. **[サーバーへの接続]** ウィンドウで、下の一覧どおりに進めます。

    * **[サーバーの種類]** に、 **[データベース エンジン]** (通常は既定のオプションです) を選択します。
    * **[サーバー名]** に、SQL Server インスタンスの名前を入力します。 (この記事では、ホスト名 NODE5 でインスタンス名 SQL2016ST を使用します [NODE5\SQL2016ST]。)SQL Server インスタンス名を確認する方法がわからない場合は、「[SSMS を使用するためのヒントとテクニック](ssms-tricks.md#determine-sql-server-name)」を参照してください。

    * **[認証]** に、 **[Windows 認証]** を選択します。 この記事では Windows 認証を使用しますが、SQL Server ログインもサポートされています。 **[SQL ログイン]** を選択した場合は、ユーザー名とパスワードが求められます。 認証の種類の詳細については、「[サーバーへの接続 (データベース エンジン)](https://docs.microsoft.com/sql/ssms/f1-help/connect-to-server-database-engine)」を参照してください。

    ![SQL Server インスタンスの使用のオプションが表示された "サーバー名" フィールド](media/connect-query-sql-server/connection2.png)

    **[オプション]** を選択して追加の接続オプションを変更することもできます。 接続オプションの例には、接続しているデータベース、接続のタイムアウト値、ネットワーク プロトコルなどがあります。 この記事では、すべてのオプションについて既定値を使用します。

3. すべてのフィールドを入力したら、 **[接続]** を選択します。

### <a name="examples-of-successful-connections"></a>接続の成功例

SQL Server 接続の成功を確認するには、**オブジェクト エクスプローラー**内でオブジェクトを展開し、調べます。 これらのオブジェクトは、接続先のサーバーの種類によって異なります。 

* オンプレミス SQL Server に接続 - この場合、NODE5\SQL2016ST:![オンプレミス サーバーに接続](media/connect-query-sql-server/connect-on-prem.png)

* SQL Azure DB に接続 - この場合、msftestserver.database.windows.net:![SQL Azure DB に接続](media/connect-query-sql-server/connect-sql-azure.png)

  >[!NOTE]
  > このチュートリアルでは、以前、"*Windows 認証*" を使用してオンプレミス SQL Server に接続しましたが、この方法は SQL Azure DB ではサポートされていません。 そのため、この画像では、SQL 認証を使用して SQL Azure DB に接続しています。 詳細については、[SQL オンプレミス認証](../../relational-databases/security/choose-an-authentication-mode.md)に関するページと [SQL Azure 認証](https://docs.microsoft.com/azure/sql-database/sql-database-security-overview#access-management)に関するページを参照してください。 

## <a name="create-a-database"></a>データベースの作成

次の手順で、TutorialDB という名前のデータベースを作成します。

1. オブジェクト エクスプローラーでサーバー インスタンスを右クリックして、 **[新しいクエリ]** を選択します。

   ![[新しいクエリ] のリンク](media/connect-query-sql-server/newquery.png)

2. クエリ ウィンドウに次の T-SQL コード スニペットを貼り付けます。 

   ```sql
   USE master
   GO
   IF NOT EXISTS (
      SELECT name
      FROM sys.databases
      WHERE name = N'TutorialDB'
   )
   CREATE DATABASE [TutorialDB]
   GO
   ```

3. クエリを実行するには、 **[実行]** を選択します (または、キーボードの F5 キーを押します)。

   ![[実行] コマンド](media/connect-query-sql-server/execute.png)
  
    クエリが完了すると、オブジェクト エクスプローラーのデータベースの一覧に新しい TutorialDB データベースが表示されます。 表示されない場合は、 **[データベース]** ノードを右クリックして **[更新]** を選択します。  

## <a name="create-a-table-in-the-new-database"></a>新しいデータベースにテーブルを作成する

このセクションでは、新しく作成した TutorialDB データベースにテーブルを作成します。 クエリ エディターがまだ*マスター* データベースのコンテキストにあるため、次の手順で接続コンテキストを *TutorialDB* データベースに切り替えます。

1. 次に示すように、[データベース] ドロップダウン リストで、目的のデータベースを選択します。 

   ![データベースの変更](media/connect-query-sql-server/changedb.png)

2. 次の T-SQL コード スニペットをクエリ ウィンドウに貼り付けて選択し、 **[実行]** を選択します (または、キーボードの F5 キーを押します)。  
   クエリ ウィンドウの既存のテキストを置き換えても、末尾に追加してもかまいません。 クエリ ウィンドウ内のすべてを実行する場合は、 **[実行]** を選択します。 テキストを追加した場合は、テキストの一部だけを実行したいので、その部分を強調表示にしてから、 **[実行]** を選択します。  
  
   ```sql
   USE [TutorialDB]
   -- Create a new table called 'Customers' in schema 'dbo'
   -- Drop the table if it already exists
   IF OBJECT_ID('dbo.Customers', 'U') IS NOT NULL
   DROP TABLE dbo.Customers
   GO
   -- Create the table in the specified schema
   CREATE TABLE dbo.Customers
   (
      CustomerId        INT    NOT NULL   PRIMARY KEY, -- primary key column
      Name      [NVARCHAR](50)  NOT NULL,
      Location  [NVARCHAR](50)  NOT NULL,
      Email     [NVARCHAR](50)  NOT NULL
   );
   GO
   ```

クエリが完了すると、オブジェクト エクスプローラーのテーブルの一覧に新しい Customers テーブルが表示されます。 テーブルが表示されない場合は、オブジェクト エクスプローラーで **[TutorialDB]**  >  **[テーブル]** ノードを右クリックした後、 **[更新]** を選択します。

## <a name="insert-rows-into-the-new-table"></a>新しいテーブルに行を挿入する

一部の行を先に作成した Customers テーブルに挿入します。 これを行うには、クエリ ウィンドウに次の T-SQL コード スニペットを貼り付けて、 **[実行]** を選択します。

   ```sql
   -- Insert rows into table 'Customers'
   INSERT INTO dbo.Customers
      ([CustomerId],[Name],[Location],[Email])
   VALUES
      ( 1, N'Orlando', N'Australia', N''),
      ( 2, N'Keith', N'India', N'keith0@adventure-works.com'),
      ( 3, N'Donna', N'Germany', N'donna0@adventure-works.com'),
      ( 4, N'Janet', N'United States', N'janet1@adventure-works.com')
   GO
   ```

## <a name="query-the-table-and-view-the-results"></a>テーブルのクエリを行って結果を表示する

クエリの結果は、クエリ テキスト ウィンドウの下に表示されます。 Customers テーブルのクエリを行い、前に挿入した行を表示するには、次の操作を行います。

1. クエリ ウィンドウに次の T-SQL コード スニペットを貼り付けて、 **[実行]** を選択します。

   ```sql
   -- Select rows from table 'Customers'
   SELECT * FROM dbo.Customers;
   ```

    クエリの結果は、テキストを入力した領域の下に表示されます。 

   ![[結果] 一覧](media/connect-query-sql-server/queryresults.png)

2. 以下のオプションのいずれかを選択して、結果の表示方法を変更します。

     ![クエリの結果を表示するための 3 つのオプション](media/connect-query-sql-server/results.png)

    * 中央のボタンを選ぶと、結果は**グリッド ビュー**で表示されます。これが、既定のオプションです。 
    * 1 番目のボタンを選ぶと、結果は**テキスト ビュー**で表示されます。次のセクションの図はこの表示方法です。
    * 3 番目のボタンでは、結果がファイルに保存されます。ファイルの既定の拡張子は .rpt です。

## <a name="verify-your-connection-properties-by-using-the-query-window-table"></a>クエリ ウィンドウのテーブルを使用して接続のプロパティを確認する

接続プロパティに関する情報は、クエリの結果の下で確認できます。 前の手順で示したクエリを実行した後、クエリ ウィンドウの下端にある接続のプロパティを確認します。

* 接続先のサーバーとデータベースと使用しているユーザー名がわかります。
* クエリの実行時間と、前に実行したクエリによって返された行数も確認できます。

    ![接続のプロパティ](media/connect-query-sql-server/connectionproperties.png)

    > [!Note]
    > この画像では、結果は**テキスト ビュー**で表示されています。

## <a name="change-the-server-based-on-the-query-window"></a>クエリ ウィンドウに基づいてサーバーを変更する

次の手順で、現在のクエリ ウィンドウが接続しているサーバーを変更できます。

1. クエリ ウィンドウを右クリックして、 **[接続]**  >  **[接続の変更]** を選択します。 **[サーバーへの接続]** ウィンドウがもう一度開きます。

2. クエリで使用されるサーバーを変更します。

   ![[接続の変更] コマンド](media/connect-query-sql-server/changeconnection.png)

    > [!NOTE]
    > この操作では、クエリ ウィンドウが接続しているサーバーのみが変更され、オブジェクト エクスプローラーで使用されるサーバーは変更されません。

## <a name="next-steps"></a>次の手順

SSMS に慣れ親しむには、実践的な経験を積むのが最も効果的です。 以下の記事は、SSMS 内で使用できるさまざまな機能を使用するのに役立ちます。  以下の記事では、SSMS のコンポーネントを管理する方法と、頻繁に使用する機能にアクセスする方法が説明されています。

* [スクリプトの作成](scripting-ssms.md)
* [SSMS でテンプレートを使用する](../template/templates-ssms.md)
* [SSMS を構成する](ssms-configuration.md)
* [SSMS を使用するための追加のヒントとテクニック](ssms-tricks.md)
