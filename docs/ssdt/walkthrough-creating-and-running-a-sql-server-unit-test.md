---
title: チュートリアル:SQL Server の単体テストの作成と実行 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 992c1d8e-3729-438b-9ef4-cd103e28f145
author: markingmyname
ms.author: maghan
ms.openlocfilehash: d8ed1dbfa5ffcb61200f7838753dc1681f8c6509
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68141206"
---
# <a name="walkthrough-creating-and-running-a-sql-server-unit-test"></a>チュートリアル:SQL Server の単体テストの作成と実行
このチュートリアルでは、複数のストアド プロシージャの動作を検証する SQL Server の単体テストを作成します。 SQL Server の単体テストを作成すると、アプリケーションの不適切な動作の原因となる可能性があるコードの欠陥を特定するのに役立ちます。 SQL Server の単体テストとアプリケーション テストは、自動テスト スイートの一部として実行できます。  
  
このチュートリアルでは、次のタスクを実行します。  
  
-   [データベース スキーマを含むスクリプトを作成する](#CreateScript)  
  
-   [データベース プロジェクトを作成してそのスキーマをインポートする](#CreateProjectAndImport)  
  
-   [データベース プロジェクトを分離開発環境に配置する](#DeployDBProj)  
  
-   [SQL Server の単体テストを作成する](#CreateDBUnitTests)  
  
-   [テスト ロジックを定義する](#DefineTestLogic)  
  
-   [SQL Server の単体テストを実行する](#RunTests)  
  
-   [ネガティブ単体テストを追加する](#NegativeTest)  
  
単体テストのいずれかによってストアド プロシージャ内のエラーが検出されたら、そのエラーを修正してテストを再実行します。  
  
## <a name="prerequisites"></a>Prerequisites  
このチュートリアルを完了するには、データベースを作成および配置するための権限があるデータベース サーバー (LocalDB データベース) に接続できる必要があります。 詳しくは、「[Visual Studio のデータベース機能に必要なアクセス許可](https://msdn.microsoft.com/library/aa833413(VS.100).aspx)」をご覧ください。  
  
## <a name="CreateScript"></a>データベース スキーマを含むスクリプトを作成する  
  
#### <a name="to-create-a-script-from-which-you-can-import-a-schema"></a>スキーマのインポート元となるスクリプトを作成するには  
  
1.  **[ファイル]** メニューの **[新規作成]** をポイントし、 **[ファイル]** をクリックします。  
  
    **[新しいファイル]** ダイアログ ボックスが表示されます。  
  
2.  **[カテゴリ]** ボックスの一覧で、 **[全般]** が強調表示されていない場合はクリックします。  
  
3.  **[テンプレート]** ボックスの一覧の **[SQL ファイル]** をクリックし、 **[開く]** をクリックします。  
  
    Transact\-SQL エディターが開きます。  
  
4.  次の Transact\-SQL コードをコピーし、 Transact\-SQL エディターに貼り付けます。  
  
    ```  
    PRINT N'Creating Sales...';  
    GO  
    CREATE SCHEMA [Sales]  
        AUTHORIZATION [dbo];  
    GO  
    PRINT N'Creating Sales.Customer...';  
    GO  
    CREATE TABLE [Sales].[Customer] (  
        [CustomerID]   INT           IDENTITY (1, 1) NOT NULL,  
        [CustomerName] NVARCHAR (40) NOT NULL,  
        [YTDOrders]    INT           NOT NULL,  
        [YTDSales]     INT           NOT NULL  
    );  
    GO  
    PRINT N'Creating Sales.Orders...';  
    GO  
    CREATE TABLE [Sales].[Orders] (  
        [CustomerID] INT      NOT NULL,  
        [OrderID]    INT      IDENTITY (1, 1) NOT NULL,  
        [OrderDate]  DATETIME NOT NULL,  
        [FilledDate] DATETIME NULL,  
        [Status]     CHAR (1) NOT NULL,  
        [Amount]     INT      NOT NULL  
    );  
    GO  
    PRINT N'Creating Sales.Def_Customer_YTDOrders...';  
    GO  
    ALTER TABLE [Sales].[Customer]  
        ADD CONSTRAINT [Def_Customer_YTDOrders] DEFAULT 0 FOR [YTDOrders];  
    GO  
    PRINT N'Creating Sales.Def_Customer_YTDSales...';  
    GO  
    ALTER TABLE [Sales].[Customer]  
        ADD CONSTRAINT [Def_Customer_YTDSales] DEFAULT 0 FOR [YTDSales];  
    GO  
    PRINT N'Creating Sales.Def_Orders_OrderDate...';  
    GO  
    ALTER TABLE [Sales].[Orders]  
        ADD CONSTRAINT [Def_Orders_OrderDate] DEFAULT GetDate() FOR [OrderDate];  
    GO  
    PRINT N'Creating Sales.Def_Orders_Status...';  
    GO  
    ALTER TABLE [Sales].[Orders]  
        ADD CONSTRAINT [Def_Orders_Status] DEFAULT 'O' FOR [Status];  
    GO  
    PRINT N'Creating Sales.PK_Customer_CustID...';  
    GO  
    ALTER TABLE [Sales].[Customer]  
        ADD CONSTRAINT [PK_Customer_CustID] PRIMARY KEY CLUSTERED ([CustomerID] ASC) WITH (ALLOW_PAGE_LOCKS = ON, ALLOW_ROW_LOCKS = ON, PAD_INDEX = OFF, IGNORE_DUP_KEY = OFF, STATISTICS_NORECOMPUTE = OFF);  
    GO  
    PRINT N'Creating Sales.PK_Orders_OrderID...';  
    GO  
    ALTER TABLE [Sales].[Orders]  
        ADD CONSTRAINT [PK_Orders_OrderID] PRIMARY KEY CLUSTERED ([OrderID] ASC) WITH (ALLOW_PAGE_LOCKS = ON, ALLOW_ROW_LOCKS = ON, PAD_INDEX = OFF, IGNORE_DUP_KEY = OFF, STATISTICS_NORECOMPUTE = OFF);  
    GO  
    PRINT N'Creating Sales.FK_Orders_Customer_CustID...';  
    GO  
    ALTER TABLE [Sales].[Orders]  
        ADD CONSTRAINT [FK_Orders_Customer_CustID] FOREIGN KEY ([CustomerID]) REFERENCES [Sales].[Customer] ([CustomerID]) ON DELETE NO ACTION ON UPDATE NO ACTION;  
    GO  
    PRINT N'Creating Sales.CK_Orders_FilledDate...';  
    GO  
    ALTER TABLE [Sales].[Orders]  
        ADD CONSTRAINT [CK_Orders_FilledDate] CHECK ((FilledDate >= OrderDate) AND (FilledDate < '01/01/2020'));  
    GO  
    PRINT N'Creating Sales.CK_Orders_OrderDate...';  
    GO  
    ALTER TABLE [Sales].[Orders]  
        ADD CONSTRAINT [CK_Orders_OrderDate] CHECK ((OrderDate > '01/01/2005') and (OrderDate < '01/01/2020'));  
    GO  
    PRINT N'Creating Sales.uspCancelOrder...';  
    GO  
    CREATE PROCEDURE [Sales].[uspCancelOrder]  
    @OrderID INT  
    AS  
    BEGIN  
    DECLARE @Delta INT, @CustomerID INT  
    BEGIN TRANSACTION  
        SELECT @Delta = [Amount], @CustomerID = [CustomerID]  
         FROM [Sales].[Orders] WHERE [OrderID] = @OrderID;  
  
    UPDATE [Sales].[Orders]  
       SET [Status] = 'X'  
    WHERE [OrderID] = @OrderID;  
  
    UPDATE [Sales].[Customer]  
       SET  
       YTDOrders = YTDOrders - @Delta  
        WHERE [CustomerID] = @CustomerID  
    COMMIT TRANSACTION  
    END  
    GO  
    PRINT N'Creating Sales.uspFillOrder...';  
    GO  
    CREATE PROCEDURE [Sales].[uspFillOrder]  
    @OrderID INT, @FilledDate DATETIME  
    AS  
    BEGIN  
    DECLARE @Delta INT, @CustomerID INT  
    BEGIN TRANSACTION  
        SELECT @Delta = [Amount], @CustomerID = [CustomerID]  
         FROM [Sales].[Orders] WHERE [OrderID] = @OrderID;  
  
    UPDATE [Sales].[Orders]  
       SET [Status] = 'F',  
           [FilledDate] = @FilledDate  
    WHERE [OrderID] = @OrderID;  
  
    UPDATE [Sales].[Customer]  
       SET  
       YTDSales = YTDSales - @Delta  
        WHERE [CustomerID] = @CustomerID  
    COMMIT TRANSACTION  
    END  
    GO  
    PRINT N'Creating Sales.uspNewCustomer...';  
    GO  
    CREATE PROCEDURE [Sales].[uspNewCustomer]  
    @CustomerName NVARCHAR (40)  
    AS  
    BEGIN  
    INSERT INTO [Sales].[Customer] (CustomerName) VALUES (@CustomerName);  
    SELECT SCOPE_IDENTITY()  
    END  
    GO  
    PRINT N'Creating Sales.uspPlaceNewOrder...';  
    GO  
    CREATE PROCEDURE [Sales].[uspPlaceNewOrder]  
    @CustomerID INT, @Amount INT, @OrderDate DATETIME, @Status CHAR (1)='O'  
    AS  
    BEGIN  
    DECLARE @RC INT  
    BEGIN TRANSACTION  
    INSERT INTO [Sales].[Orders] (CustomerID, OrderDate, FilledDate, Status, Amount)   
         VALUES (@CustomerID, @OrderDate, NULL, @Status, @Amount)  
    SELECT @RC = SCOPE_IDENTITY();  
    UPDATE [Sales].[Customer]  
       SET  
       YTDOrders = YTDOrders + @Amount  
        WHERE [CustomerID] = @CustomerID  
    COMMIT TRANSACTION  
    RETURN @RC  
    END  
    GO  
    CREATE PROCEDURE [Sales].[uspShowOrderDetails]  
    @CustomerID INT=0  
    AS  
    BEGIN  
    SELECT [C].[CustomerName], CONVERT(date, [O].[OrderDate]), CONVERT(date, [O].[FilledDate]), [O].[Status], [O].[Amount]  
      FROM [Sales].[Customer] AS C  
      INNER JOIN [Sales].[Orders] AS O  
         ON [O].[CustomerID] = [C].[CustomerID]  
      WHERE [C].[CustomerID] = @CustomerID  
    END  
    GO  
    ```  
  
5.  ファイルを保存します。 次の手順でこのスクリプトを使用する必要があるため、この場所をメモしておきます。  
  
6.  **[ファイル]** メニューの **[ソリューションを閉じる]** をクリックします。  
  
    次に、データベース プロジェクトを作成し、作成したスクリプトからスキーマをインポートします。  
  
## <a name="CreateProjectAndImport"></a>データベース プロジェクトを作成してスキーマをインポートする  
  
#### <a name="to-create-a-database-project"></a>データベース プロジェクトを作成するには  
  
1.  **[ファイル]** メニューの **[新規作成]** をポイントし、 **[プロジェクト]** をクリックします。  
  
    **[新しいプロジェクト]** ダイアログ ボックスが表示されます。  
  
2.  **[インストールされたテンプレート]** で、 **[SQL Server]** ノードを選択し、 **[SQL Server データベース プロジェクト]** を選択します。  
  
3.  **[名前]** に「 **SimpleUnitTestDB**」と入力します。  
  
4.  **[ソリューションのディレクトリを作成]** チェック ボックスがまだオンになっていない場合はオンにします。  
  
5.  **[ソース管理に追加]** チェック ボックスがまだオフになっていない場合はオフにし、 **[OK]** をクリックします。  
  
    データベース プロジェクトが作成され、 **ソリューション エクスプローラー**に表示されます。 次に、スクリプトからデータベース スキーマをインポートします。  
  
#### <a name="to-import-a-database-schema-from-a-script"></a>スクリプトからデータベース スキーマをインポートするには  
  
1.  **[プロジェクト]** メニューの **[インポート]** をクリックし、 **[スクリプト (\*.sql)]** をクリックします。  
  
2.  [ようこそ] ページを読んだ後、 **[次へ]** をクリックします。  
  
3.  **[参照]** をクリックし、.sql ファイルを保存したディレクトリに移動します。  
  
4.  .sql ファイルをダブルクリックし、 **[完了]** をクリックします。  
  
    スクリプトがインポートされ、そのスクリプトで定義されているオブジェクトがデータベース プロジェクトに追加されます。  
  
5.  概要を確認し、 **[完了]** をクリックして操作を完了します。  
  
    > [!NOTE]  
    > Sales.uspFillOrder プロシージャには、意図的なコード エラーが含まれています。このエラーは、この後の手順で検出して修正します。  
  
#### <a name="to-examine-the-resulting-project"></a>作成されたプロジェクトを確認するには  
  
1.  **ソリューション エクスプローラー**で、プロジェクトにインポートされたスクリプト ファイルを確認します。  
  
2.  **SQL Server オブジェクト エクスプローラー**で、[プロジェクト] ノード内のデータベースを確認します。  
  
## <a name="DeployDBProj"></a>LocalDB への配置  
既定では、F5 キーを押すと、データベースが LocalDB データベースに配置 (発行) されます。 プロジェクトのプロパティ ページで、[デバッグ] タブに移動して接続文字列を変更すると、データベースの場所を変更できます。  
  
## <a name="CreateDBUnitTests"></a>SQL Server の単体テストを作成する  
  
#### <a name="to-create-a-sql-server-unit-test-for-the-stored-procedures"></a>ストアド プロシージャに対して SQL Server の単体テストを作成するには  
  
1.  **SQL Server オブジェクト エクスプローラー**で、 **SimpleUnitTestDB** の [プロジェクト] ノード、 **[プログラミング]** ノード、 **[ストアド プロシージャ]** ノードの順に展開します。  
  
2.  ストアド プロシージャの 1 つを右クリックし、 **[単体テストの作成]** をクリックして **[単体テストの作成]** ダイアログ ボックスを表示します。  
  
3.  ストアド プロシージャのチェック ボックスの 5 つすべてを選択します。**Sales.uspCancelOrder**、**Sales.uspFillOrder**、**Sales.uspNewCustomer**、**Sales.uspPlaceNewOrder**、**Sales.uspShowOrderDetails**。  
  
4.  **[プロジェクト]** ボックスの一覧で、 **[新しい Visual C# テスト プロジェクトの作成]** を選択します。  
  
5.  プロジェクト名とクラス名の既定の名前をそのまま使用し、 **[OK]** をクリックします。  
  
6.  テストを構成するダイアログ ボックスの **[次のデータ接続を使用して単体テストを実行]** で、このチュートリアルで既に配置したデータベースへの接続を指定します。 たとえば、既定の配置場所 (LocalDB) を使用した場合は、 **[新しい接続]** をクリックして **(LocalDB)\Projects** を指定します。 次に、データベース名を選択します。 その後、[OK] をクリックして、 **[接続のプロパティ]** ダイアログ ボックスを閉じます。  
  
    > [!NOTE]  
    > 権限が制限されているビューまたはストアド プロシージャをテストする必要がある場合は、通常、この手順でその接続を指定します。 次に、テストを検証するために、権限の幅が広いセカンダリ接続を指定します。 セカンダリ接続がある場合は、そのユーザーをデータベース プロジェクトに追加し、配置前スクリプトにそのユーザーのログインを作成します。  
  
7.  テストを構成するダイアログ ボックスの **[配置]** セクションの **[単体テストの実行前に自動的にデータベース プロジェクトを配置]** チェック ボックスをオンにします。  
  
8.  **[データベース プロジェクト]** の **[SimpleUnitTestDB.sqlproj]** をクリックします。  
  
9. **[配置構成]** の **[デバッグ]** をクリックします。  
  
    テスト データは、SQL Server の単体テストの一部として生成することもできます。 このチュートリアルでは、テストによってテスト自体のデータが作成されるため、この手順は省略します。  
  
10. **[OK]** をクリックします。  
  
    テスト プロジェクトがビルドされ、SQL Server 単体テスト デザイナーが表示されます。 次に、単体テストの Transact\-SQL スクリプトのテスト ロジックを更新します。  
  
## <a name="DefineTestLogic"></a>テスト ロジックを定義する  
この単純なデータベースには、Customer と Order という 2 つのテーブルがあります。 データベースを更新するには、次のストアド プロシージャを使用します。  
  
-   uspNewCustomer - このストアド プロシージャは、Customer テーブルにレコードを追加します。この場合は、顧客の YTDOrders 列と YTDSales 列が 0 に設定されます。  
  
-   uspPlaceNewOrder - このストアド プロシージャは、指定した顧客のレコードを Orders テーブルに追加し、Customer テーブル内の対応するレコードの YTDOrders の値を更新します。  
  
-   uspFillOrder - このストアド プロシージャは、ステータスを 'O' から 'F' に変更することで Orders テーブル内のレコードを更新し、Customer テーブル内の対応するレコードの YTDSales の金額を加算します。  
  
-   uspCancelOrder - このストアド プロシージャは、ステータスを 'O' から 'X' に変更することで Orders テーブル内のレコードを更新し、Customer テーブル内の対応するレコードの YTDOrders の金額を減算します。  
  
-   uspShowOrderDetails - このストアド プロシージャは、Orders テーブルと Custom テーブルを結合し、特定の顧客のレコードを表示します。  
  
> [!NOTE]  
> この例では、単純な SQL Server の単体テストの作成方法を説明します。 実際のデータベースでは、特定の顧客のステータスが 'O' または 'F' のすべての注文の総額を合計する場合があります。 また、このチュートリアルの手順には、エラー処理も含まれていません。 たとえば、既に入力された注文に対する uspFillOrder の呼び出しを防ぐ処理はしていません。  
  
テストでは、データベースが空の状態で開始されることを前提としています。 次の条件を検証するテストを作成します。  
  
-   uspNewCustomer - このストアド プロシージャを実行した後、Customer テーブルに 1 行のレコードが含まれていることを確認します。  
  
-   uspPlaceNewOrder - CustomerID が 1 の顧客の場合は、100 ドルの注文を行います。 その顧客の YTDOrders の金額が 100 で、YTDSales の金額が 0 であることを確認します。  
  
-   uspFillOrder - CustomerID が 1 の顧客の場合は、50 ドルの注文を行います。 その注文を入力します。 YTDOrders と YTDSales の両方の金額が 50 であることを確認します。  
  
-   uspShowOrderDetails - CustomerID が 1 の顧客の場合は、100 ドル、50 ドル、および 5 ドルの注文を行います。 uspShowOrderDetails によって正しい列数が返され、結果セットに予期されるチェックサムがあることを確認します。  
  
> [!NOTE]  
> SQL Server の単体テスト全体のセットでは、通常、その他の列が正しく設定されたことを確認します。 このチュートリアルが長くなり過ぎないように、uspCancelOrder の動作を検証する方法については説明しません。  
  
#### <a name="to-write-the-sql-server-unit-test-for-uspnewcustomer"></a>uspNewCustomer に対して SQL Server の単体テストを作成するには  
  
1.  SQL Server 単体テスト デザイナーのナビゲーション バーで、 **[Sales_uspNewCustomerTest]** をクリックし、 **[テスト]** が隣接する一覧で強調表示されていることを確認します。  
  
    前の手順を実行したら、単体テスト内のテスト アクション用のテスト スクリプトを作成できます。  
  
2.  Transact\-SQL エディターで、次のステートメントに一致するように Transact\-SQL ステートメントを更新します。  
  
    ```  
    -- ssNoVersion unit test for Sales.uspNewCustomer  
    DECLARE @RC AS INT, @CustomerName AS NVARCHAR (40);  
  
    SELECT @RC = 0,  
           @CustomerName = 'Fictitious Customer';  
  
    EXECUTE @RC = [Sales].[uspNewCustomer] @CustomerName;  
  
    SELECT * FROM [Sales].[Customer];  
    ```  
  
3.  **[テスト条件]** ウィンドウで、[結果不確定] テスト条件をクリックし、 **[テスト条件を削除します]** アイコン (赤色の X) をクリックします。  
  
4.  **[テスト条件]** ウィンドウの一覧で、 **[行数]** をクリックし、 **[テスト条件を追加します]** アイコン (緑色の +) をクリックします。  
  
5.  **[プロパティ]** ウィンドウを開いて (テスト条件を選択して F4 キーを押します)、 **[行数]** プロパティを 1 に設定します。  
  
6.  **[ファイル]** メニューの **[すべてを保存]** をクリックします。  
  
    次に、uspPlaceNewOrder の単体テストのロジックを定義します。  
  
#### <a name="to-write-the-sql-server-unit-test-for-uspplaceneworder"></a>uspPlaceNewOrder に対して SQL Server の単体テストを作成するには  
  
1.  SQL Server 単体テスト デザイナーのナビゲーション バーで、 **[Sales_uspPlaceNewOrderTest]** をクリックし、 **[テスト]** が隣接する一覧で強調表示されていることを確認します。  
  
    この手順を実行したら、単体テスト内のテスト アクション用のテスト スクリプトを作成できます。  
  
2.  Transact\-SQL エディターで、次のステートメントに一致するように Transact\-SQL ステートメントを更新します。  
  
    ```  
    -- ssNoVersion unit test for Sales.uspPlaceNewOrder  
    DECLARE @RC AS INT, @CustomerID AS INT, @Amount AS INT, @OrderDate AS DATETIME, @Status AS CHAR (1);  
    DECLARE @CustomerName AS NVARCHAR(40);  
  
    SELECT @RC = 0,  
           @CustomerID = 0,  
           @CustomerName = N'Fictitious Customer',  
           @Amount = 100,  
           @OrderDate = getdate(),  
           @Status = 'O';  
  
    -- NOTE: Assumes that you inserted a Customer record with CustomerName='Fictitious Customer' in the pre-test script.  
    SELECT @CustomerID = [CustomerID] FROM [Sales].[Customer] WHERE [CustomerName] = @CustomerName;  
  
    -- place an order for that customer  
    EXECUTE @RC = [Sales].[uspPlaceNewOrder] @CustomerID, @Amount, @OrderDate, @Status;  
  
    -- verify that the YTDOrders value is correct.  
    SELECT @RC = [YTDOrders] FROM [Sales].[Customer] WHERE [CustomerID] = @CustomerID  
  
    SELECT @RC AS RC  
    ```  
  
3.  **[テスト条件]** ウィンドウで、[結果不確定] テスト条件をクリックし、 **[テスト条件を削除します]** をクリックします。  
  
4.  **[テスト条件]** ウィンドウの一覧で、 **[スカラー値]** をクリックし、 **[テスト条件を追加します]** をクリックします。  
  
5.  **[プロパティ]** ウィンドウで、 **[予期される値]** プロパティを 100 に設定します。  
  
6.  SQL Server 単体テスト デザイナーのナビゲーション バーで、 **[Sales_uspPlaceNewOrderTest]** をクリックし、 **[事前テスト]** が隣接する一覧で強調表示されていることを確認します。  
  
    この手順の実行後に、テストの実行に必要な状態にデータを変更するステートメントを指定できます。 この例では、注文を行う前に Customer レコードを作成する必要があります。  
  
7.  **[作成するにはここをクリックしてください]** をクリックし、事前テスト スクリプトを作成します。  
  
8.  Transact\-SQL エディターで、次のステートメントに一致するように Transact\-SQL ステートメントを更新します。  
  
    ```  
    /*  
    Add Transact-SQL statements here that you want to run before  
    the test script is run.  
    */  
    -- Add a customer for this test with the name 'Fictitious Customer'  
    DECLARE @NewCustomerID AS INT, @CustomerID AS INT, @RC AS INT, @CustomerName AS NVARCHAR (40);  
  
    SELECT @RC = 0,  
           @NewCustomerID = 0,  
       @CustomerID = 0,  
           @CustomerName = N'Fictitious Customer';  
  
    IF NOT EXISTS(SELECT * FROM [Sales].[Customer] WHERE CustomerName = @CustomerName)  
    BEGIN  
    EXECUTE @NewCustomerID = [Sales].[uspNewCustomer] @CustomerName;  
    END  
  
    -- NOTE: Assumes that you inserted a Customer record with CustomerName='Fictitious Customer' in the pre-test script.  
    SELECT @CustomerID = [CustomerID] FROM [Sales].[Customer] WHERE [CustomerName] = @CustomerName;  
  
    -- delete any old records in the Orders table and clear out the YTD Sales/Orders fields  
    DELETE from [Sales].[Orders] WHERE [CustomerID] = @CustomerID;  
    UPDATE [Sales].[Customer] SET YTDOrders = 0, YTDSales = 0 WHERE [CustomerID] = @CustomerID;  
    ```  
  
9. **[ファイル]** メニューの **[すべてを保存]** をクリックします。  
  
    次に、uspFillOrder の単体テストを作成します。  
  
#### <a name="to-write-the-sql-server-unit-test-for-uspfillorder"></a>uspFillOrder に対して SQL Server の単体テストを作成するには  
  
1.  SQL Server 単体テスト デザイナーのナビゲーション バーで、 **[Sales_uspFillOrderTest]** をクリックし、 **[テスト]** が隣接する一覧で強調表示されていることを確認します。  
  
    この手順を実行したら、単体テスト内のテスト アクション用のテスト スクリプトを作成できます。  
  
2.  Transact\-SQL エディターで、次のステートメントに一致するように Transact\-SQL ステートメントを更新します。  
  
    ```  
    -- ssNoVersion unit test for Sales.uspFillOrder  
    DECLARE @RC AS INT, @CustomerID AS INT, @Amount AS INT, @FilledDate AS DATETIME, @Status AS CHAR (1);  
    DECLARE @CustomerName AS NVARCHAR(40), @OrderID AS INT;  
  
    SELECT @RC = 0,  
           @CustomerID = 0,  
           @OrderID = 0,  
           @CustomerName = N'Fictitious Customer',  
           @Amount = 100,  
           @FilledDate = getdate(),  
           @Status = 'O';  
  
    -- NOTE: Assumes that you inserted a Customer record with CustomerName='Fictitious Customer' in the pre-test script.  
    SELECT @CustomerID = [CustomerID] FROM [Sales].[Customer] WHERE [CustomerName] = @CustomerName;  
    -- Get the most recently added order.  
    SELECT @OrderID = MAX([OrderID]) FROM [Sales].[Orders] WHERE [CustomerID] = @CustomerID;  
  
    -- fill an order for that customer  
    EXECUTE @RC = [Sales].[uspFillOrder] @OrderID, @FilledDate;  
  
    -- verify that the YTDOrders value is correct.  
    SELECT @RC = [YTDSales] FROM [Sales].[Customer] WHERE [CustomerID] = @CustomerID  
  
    SELECT @RC AS RC;  
    ```  
  
3.  **[テスト条件]** ウィンドウで、[結果不確定] テスト条件をクリックし、 **[テスト条件を削除します]** をクリックします。  
  
4.  **[テスト条件]** ウィンドウの一覧で、 **[スカラー値]** をクリックし、 **[テスト条件を追加します]** をクリックします。  
  
5.  **[プロパティ]** ウィンドウで、 **[予期される値]** プロパティを 100 に設定します。  
  
6.  SQL Server 単体テスト デザイナーのナビゲーション バーで、 **[Sales_uspFillOrderTest]** をクリックし、 **[事前テスト]** が隣接する一覧で強調表示されていることを確認します。 この手順の実行後に、テストの実行に必要な状態にデータを変更するステートメントを指定できます。 この例では、注文を行う前に Customer レコードを作成する必要があります。  
  
7.  **[作成するにはここをクリックしてください]** をクリックし、事前テスト スクリプトを作成します。  
  
8.  Transact\-SQL エディターで、次のステートメントに一致するように Transact\-SQL ステートメントを更新します。  
  
    ```  
    /*  
    Add Transact-SQL statements here that you want to run before  
    the test script is run.  
    */  
    BEGIN TRANSACTION  
  
    -- Add a customer for this test with the name 'CustomerB'  
    DECLARE @NewCustomerID AS INT, @RC AS INT, @CustomerName AS NVARCHAR (40);  
  
    SELECT @RC = 0,  
           @NewCustomerID = 0,  
           @CustomerName = N'Fictitious Customer';  
  
    IF NOT EXISTS(SELECT * FROM [Sales].[Customer] WHERE CustomerName = @CustomerName)  
    BEGIN  
    EXECUTE @NewCustomerID = [Sales].[uspNewCustomer] @CustomerName;  
    END  
  
    DECLARE @CustomerID AS INT, @Amount AS INT, @OrderDate AS DATETIME, @Status AS CHAR (1);  
  
    SELECT @RC = 0,  
           @CustomerID = 0,  
           @CustomerName = N'Fictitious Customer',  
           @Amount = 100,  
           @OrderDate = getdate(),  
           @Status = 'O';  
  
    -- NOTE: Assumes that you inserted a Customer record with CustomerName='Fictitious Customer' in the pre-test script.  
    SELECT @CustomerID = [CustomerID] FROM [Sales].[Customer] WHERE [CustomerName] = @CustomerName;  
  
    -- delete any old records in the Orders table and clear out the YTD Sales/Orders fields  
    DELETE from [Sales].[Orders] WHERE [CustomerID] = @CustomerID;  
    UPDATE [Sales].[Customer] SET YTDOrders = 0, YTDSales = 0 WHERE [CustomerID] = @CustomerID;  
  
    -- place an order for that customer  
    EXECUTE @RC = [Sales].[uspPlaceNewOrder] @CustomerID, @Amount, @OrderDate, @Status;  
  
    COMMIT TRANSACTION  
    ```  
  
9. **[ファイル]** メニューの **[すべてを保存]** をクリックします。  
  
#### <a name="to-write-the-sql-server-unit-test-for-uspshoworderdetails"></a>uspShowOrderDetails に対して SQL Server の単体テストを作成するには  
  
1.  SQL Server 単体テスト デザイナーのナビゲーション バーで、 **[Sales_uspShowOrderDetailsTest]** をクリックし、 **[テスト]** が隣接する一覧で強調表示されていることを確認します。  
  
    この手順を実行したら、単体テスト内のテスト アクション用のテスト スクリプトを作成できます。  
  
2.  Transact\-SQL エディターで、次のステートメントに一致するように Transact\-SQL ステートメントを更新します。  
  
    ```  
    -- ssNoVersion unit test for Sales.uspFillOrder  
    DECLARE @RC AS INT, @CustomerID AS INT, @Amount AS INT, @FilledDate AS DATETIME, @Status AS CHAR (1);  
    DECLARE @CustomerName AS NVARCHAR(40), @OrderID AS INT;  
  
    SELECT @RC = 0,  
           @CustomerID = 0,  
           @OrderID = 0,  
           @CustomerName = N'Fictitious Customer',  
           @Amount = 100,  
           @FilledDate = getdate(),  
           @Status = 'O';  
  
    -- NOTE: Assumes that you inserted a Customer record with CustomerName='Fictitious Customer' in the pre-test script.  
    SELECT @CustomerID = [CustomerID] FROM [Sales].[Customer] WHERE [CustomerName] = @CustomerName;  
  
    -- fill an order for that customer  
    EXECUTE @RC = [Sales].[uspShowOrderDetails] @CustomerID;  
  
    SELECT @RC AS RC;  
    ```  
  
3.  **[テスト条件]** ウィンドウで、[結果不確定] テスト条件をクリックし、 **[テスト条件を削除します]** をクリックします。  
  
4.  **[テスト条件]** ウィンドウの一覧で、 **[必要なスキーマ]** をクリックし、 **[テスト条件を追加します]** をクリックします。  
  
5.  **[プロパティ]** ウィンドウの **[構成]** プロパティで、参照ボタン ( **[...]** ) をクリックします。  
  
6.  **[expectedSchemaCondition1 の構成]** ダイアログ ボックスで、データベースへの接続を指定します。 たとえば、既定の配置場所 (LocalDB) を使用した場合は、 **[新しい接続]** をクリックして **(LocalDB)\Projects** を指定します。 次に、データベース名を選択します。  
  
7.  **[取得]** をクリックします。 (必要に応じて、データが表示されるまで **[取得]** をクリックします)。  
  
    単体テストの Transact\-SQL 本文が実行され、結果のスキーマがダイアログ ボックスに表示されます。 事前テスト コードが実行されなかったため、データは返されません。 ここでは、データではなくスキーマのみを検証しているため、問題はありません。  
  
8.  **[OK]** をクリックします。  
  
    必要なスキーマがテスト条件と共に格納されます。  
  
9. SQL Server 単体テスト デザイナーのナビゲーション バーで、 **[Sales_uspShowOrderDetailsTest]** をクリックし、 **[事前テスト]** が隣接する一覧で強調表示されていることを確認します。 この手順の実行後に、テストの実行に必要な状態にデータを変更するステートメントを指定できます。 この例では、注文を行う前に Customer レコードを作成する必要があります。  
  
10. **[作成するにはここをクリックしてください]** をクリックし、事前テスト スクリプトを作成します。  
  
11. Transact\-SQL エディターで、次のステートメントに一致するように Transact\-SQL ステートメントを更新します。  
  
    ```  
    /*  
    Add Transact-SQL statements here to run before the test script is run.  
    */  
    BEGIN TRANSACTION  
  
    -- Add a customer for this test with the name 'FictitiousCustomer'  
    DECLARE @NewCustomerID AS INT, @RC AS INT, @CustomerName AS NVARCHAR (40);  
  
    SELECT @RC = 0,  
           @NewCustomerID = 0,  
           @CustomerName = N'Fictitious Customer';  
  
    IF NOT EXISTS(SELECT * FROM [Sales].[Customer] WHERE CustomerName = @CustomerName)  
    BEGIN  
    EXECUTE @NewCustomerID = [Sales].[uspNewCustomer] @CustomerName;  
    END  
  
    DECLARE @CustomerID AS INT, @Amount AS INT, @OrderDate AS DATETIME, @Status AS CHAR (1);  
  
    SELECT @RC = 0,  
           @CustomerID = 0,  
           @CustomerName = N'Fictitious Customer',  
           @OrderDate = getdate(),  
           @Status = 'O';  
  
    -- NOTE: Assumes that you inserted a Customer record with CustomerName='Fictitious Customer' in the pre-test script.  
    SELECT @CustomerID = [CustomerID] FROM [Sales].[Customer] WHERE [CustomerName] = @CustomerName;  
  
    -- delete any old records in the Orders table and clear out the YTD Sales/Orders fields  
    DELETE from [Sales].[Orders] WHERE [CustomerID] = @CustomerID;  
    UPDATE [Sales].[Customer] SET YTDOrders = 0, YTDSales = 0 WHERE [CustomerID] = @CustomerID;  
  
    -- place 3 orders for that customer  
    EXECUTE @RC = [Sales].[uspPlaceNewOrder] @CustomerID, 100, @OrderDate, @Status;  
    EXECUTE @RC = [Sales].[uspPlaceNewOrder] @CustomerID, 50, @OrderDate, @Status;  
    EXECUTE @RC = [Sales].[uspPlaceNewOrder] @CustomerID, 5, @OrderDate, @Status;  
  
    COMMIT TRANSACTION  
    ```  
  
12. SQL Server 単体テスト デザイナーのナビゲーション バーで、 **[Sales_uspShowOrderDetailsTest]** をクリックし、隣接する一覧で **[テスト]** をクリックします。  
  
    この操作が必要なのは、チェックサムの条件を事前テストではなくテストに適用するためです。  
  
13. **[テスト条件]** ウィンドウの一覧で、 **[データ チェックサム]** クリックし、 **[テスト条件を追加します]** をクリックします。  
  
14. **[プロパティ]** ウィンドウの **[構成]** プロパティで、参照ボタン ( **[...]** ) をクリックします。  
  
15. **[checksumCondition1 の構成]** ダイアログ ボックスで、データベースへの接続を指定します。  
  
16. ( **[接続の編集]** をクリックすると表示される) ダイアログ ボックスで Transact\-SQL を次のコードに置き換えます。  
  
    ```  
    BEGIN TRANSACTION  
  
    -- Add a customer for this test with the name 'CustomerB'  
    DECLARE @NewCustomerID AS INT, @RC AS INT, @CustomerName AS NVARCHAR (40);  
  
    SELECT @RC = 0,  
           @NewCustomerID = 0,  
           @CustomerName = N'Fictitious Customer';  
  
    IF NOT EXISTS(SELECT * FROM [Sales].[Customer] WHERE CustomerName = @CustomerName)  
    BEGIN  
    EXECUTE @NewCustomerID = [Sales].[uspNewCustomer] @CustomerName;  
    END  
  
    DECLARE @CustomerID AS INT, @Amount AS INT, @OrderDate AS DATETIME, @Status AS CHAR (1);  
  
    SELECT @RC = 0,  
           @CustomerID = 0,  
           @CustomerName = N'Fictitious Customer',  
           @OrderDate = getdate(),  
           @Status = 'O';  
  
    -- NOTE: Assumes that you inserted a Customer record with CustomerName='Fictitious Customer' in the pre-test script.  
    SELECT @CustomerID = [CustomerID] FROM [Sales].[Customer] WHERE [CustomerName] = @CustomerName;  
  
    -- delete any old records in the Orders table and clear out the YTD Sales/Orders fields  
    DELETE from [Sales].[Orders] WHERE [CustomerID] = @CustomerID;  
    UPDATE [Sales].[Customer] SET YTDOrders = 0, YTDSales = 0 WHERE [CustomerID] = @CustomerID;  
  
    -- place 3 orders for that customer  
    EXECUTE @RC = [Sales].[uspPlaceNewOrder] @CustomerID, 100, @OrderDate, @Status;  
    EXECUTE @RC = [Sales].[uspPlaceNewOrder] @CustomerID, 50, @OrderDate, @Status;  
    EXECUTE @RC = [Sales].[uspPlaceNewOrder] @CustomerID, 5, @OrderDate, @Status;  
  
    COMMIT TRANSACTION  
  
    -- ssNoVersion unit test for Sales.uspFillOrder  
    DECLARE @FilledDate AS DATETIME;  
    DECLARE @OrderID AS INT;  
  
    SELECT @RC = 0,  
           @CustomerID = 0,  
           @OrderID = 0,  
           @CustomerName = N'Fictitious Customer',  
           @Amount = 100,  
           @FilledDate = getdate(),  
           @Status = 'O';  
  
    -- NOTE: Assumes that you inserted a Customer record with CustomerName='Fictitious Customer' in the pre-test script.  
    SELECT @CustomerID = [CustomerID] FROM [Sales].[Customer] WHERE [CustomerName] = @CustomerName;  
  
    -- fill an order for that customer  
    EXECUTE @RC = [Sales].[uspShowOrderDetails] @CustomerID;  
  
    SELECT @RC AS RC;  
    ```  
  
    このコードは、事前テストの Transact\-SQL コードとテスト自体の Transact\-SQL コードを組み合わせたものです。 どちらのコードも、テストの実行時に返される結果と同じ結果を返すために必要です。  
  
17. **[取得]** をクリックします。 (必要に応じて、データが表示されるまで **[取得]** をクリックします)。  
  
    指定した Transact\-SQL が実行され、返されたデータのチェックサムが計算されます。  
  
18. **[OK]** をクリックします。  
  
    計算されたチェックサムがテスト条件と共に格納されます。 [データ チェックサム] テスト条件の [値] 列には、必要なチェックサムが表示されます。  
  
19. **[ファイル]** メニューの **[すべてを保存]** をクリックします。  
  
    これで、テストを実行する準備が整いました。  
  
## <a name="RunTests"></a>SQL Server の単体テストを実行する  
  
#### <a name="to-run-the-sql-server-unit-tests"></a>SQL Server の単体テストを実行するには  
  
1.  **[テスト]** メニューの **[ウィンドウ]** をポイントし、 **[テスト ビュー]** (Visual Studio 2010 の場合) または **[テスト エクスプローラー]** ( Visual Studio 2012の場合) をクリックします。  
  
2.  **[テスト ビュー]** ウィンドウ (Visual Studio 2010) で、ツール バーの **[最新の情報に更新]** をクリックし、テストの一覧を更新します。 **テスト エクスプローラー** (Visual Studio 2012) でテストの一覧を表示するには、ソリューションをビルドします。  
  
    **[テスト ビュー]** ウィンドウまたは **[テスト エクスプローラー]** ウィンドウには、このチュートリアルの前の手順で作成し、Transact\-SQL ステートメントとテスト条件を追加したテストの一覧が表示されます。 TestMethod1 という名前のテストは空で、このチュートリアルでは使用しません。  
  
3.  **[Sales_uspNewCustomerTest]** を右クリックし、 **[選択範囲の実行]** をクリックします。  
  
    Visual Studio では、指定した特権コンテキストを使用してデータベースに接続し、データ生成計画を適用します。 Visual Studio は実行コンテキストに切り替わり、テストの Transact\-SQL スクリプトが実行されます。 最後に、 Visual Studio は、 Transact\-SQL スクリプトの結果を、テスト条件で指定した内容と照合して評価し、成功したか失敗したかという結果を **[テスト結果]** ウィンドウに表示します。  
  
4.  **[テスト結果]** ウィンドウの結果を確認します。  
  
    テストが成功したということは、 **SELECT** ステートメントの実行時に 1 行が返されたことを意味します。  
  
5.  Sales_uspPlaceNewOrderTest、Sales_uspFillOrderTest、Sales_uspShowOrderDetailsTest の各テストについて、手順 3. を繰り返します。 結果は次のようになります。  
  
    |[テスト]|予想される結果|  
    |--------|-------------------|  
    |Sales_uspPlaceNewOrderTest|成功|  
    |Sales_uspShowOrderDetailsTest|成功|  
    |Sales_uspFillOrderTest|次のエラーにより失敗しました:"ScalarValueCondition 条件 (scalarValueCondition2) が失敗しました:ResultSet 1 の行 1 の列 1: 値が一致しません。実際は '-100'、予期した値は '100'。"このエラーは、ストアド プロシージャの定義に軽度なエラーが含まれていることが原因で発生します。|  
  
    次に、エラーを修正してテストを再実行します。  
  
#### <a name="to-correct-the-error-in-salesuspfillorder"></a>Sales.uspFillOrder のエラーを修正するには  
  
1.  **SQL Server オブジェクト エクスプローラー**のデータベースの [プロジェクト] ノードで **uspFillOrder** ストアド プロシージャをダブルクリックし、Transact\-SQL エディターで定義を開きます。  
  
2.  定義内で、次の Transact\-SQL ステートメントを探します。  
  
    ```  
    UPDATE [Sales].[Customer]  
       SET  
       YTDSales = YTDSales - @Delta  
        WHERE [CustomerID] = @CustomerID  
    ```  
  
3.  このステートメント内の SET 句を次のステートメントのように変更します。  
  
    ```  
    UPDATE [Sales].[Customer]  
       SET  
       YTDSales = YTDSales + @Delta  
        WHERE [CustomerID] = @CustomerID  
    ```  
  
4.  **[ファイル]** メニューの **[uspFillOrder.sql の保存]** をクリックします。  
  
5.  **[テスト ビュー]** で、 **[Sales_uspFillOrderTest]** を右クリックし、 **[選択範囲の実行]** をクリックします。  
  
    テストは成功します。  
  
## <a name="NegativeTest"></a>ネガティブ単体テストを追加する  
ネガティブ テストを作成し、テストがエラーになる必要があるときにエラーになるかどうかを検証する場合があります。 たとえば、既に入力された注文を取り消そうとした場合、そのテストはエラーになる必要があります。 チュートリアルのこの部分では、Sales.uspCancelOrder ストアド プロシージャのネガティブ単体テストを作成します。  
  
ネガティブ テストを作成して検証するには、次のタスクを実行する必要があります。  
  
-   エラー条件をテストするようにストアド プロシージャを更新する  
  
-   新しい単体テストを定義する  
  
-   予期されたエラーであることを示すように単体テストのコードを変更する  
  
-   単体テストを実行する  
  
#### <a name="to-update-the-stored-procedure"></a>ストアド プロシージャを更新するには  
  
1.  **SQL Server オブジェクト エクスプローラー**で、SimpleUnitTestDB データベースの [プロジェクト] ノードの [プログラミング] ノード、[ストアド プロシージャ] ノードの順に展開し、[uspCancelOrder] をダブルクリックします。  
  
2.  Transact\-SQL エディターで、プロシージャの定義を次のコードに一致するように更新します。  
  
    ```  
    CREATE PROCEDURE [Sales].[uspCancelOrder]  
    @OrderID INT  
    AS  
    BEGIN  
        DECLARE @Delta INT, @CustomerID INT, @PriorStatus CHAR(1)  
        BEGIN TRANSACTION  
            BEGIN TRY  
                IF (NOT EXISTS(SELECT [CustomerID] from [Sales].[Orders] WHERE [OrderID] = @OrderID))  
                BEGIN  
                    -- Specify WITH LOG option so that the error is  
                    -- written to the application log.  
                    RAISERROR( 'That order does not exist.', -- Message text  
                               16, -- severity  
                                1 -- state  
                            ) WITH LOG;  
                END  
  
                SELECT @Delta = [Amount], @CustomerID = [CustomerID], @PriorStatus = [Status]  
                 FROM [Sales].[Orders] WHERE [OrderID] = @OrderID  
  
                IF @PriorStatus <> 'O'   
                BEGIN  
                    -- Specify WITH LOG option so that the error is  
                    -- written to the application log.  
                    RAISERROR ( 'You can only cancel open orders.', -- Message text  
                                16, -- Severity  
                                1 -- State  
                                ) WITH LOG;  
                END  
                ELSE  
                BEGIN  
                    -- If we make it to here, then we can cancel the order. Update the status to 'X' first...  
                    UPDATE [Sales].[Orders]  
                       SET [Status] = 'X'  
                    WHERE [OrderID] = @OrderID  
                    -- and then remove the amount from the YTDOrders for the customer  
                    UPDATE [Sales].[Customer]  
                           SET  
                               YTDOrders = YTDOrders - @Delta  
                    WHERE [CustomerID] = @CustomerID  
                    COMMIT TRANSACTION  
                    RETURN 1; -- indicate success  
                END  
            END TRY  
            BEGIN CATCH  
                DECLARE @ErrorMessage NVARCHAR(4000);  
                DECLARE @ErrorSeverity INT;  
                DECLARE @ErrorState INT;  
  
                SELECT @ErrorMessage = ERROR_MESSAGE(),  
                       @ErrorSeverity = ERROR_SEVERITY(),  
                       @ErrorState = ERROR_STATE();  
  
                ROLLBACK TRANSACTION  
                -- Use RAISERROR inside the CATCH block to return  
                -- error information about the original error that  
                -- caused execution to jump to the CATCH block.  
                RAISERROR (@ErrorMessage, -- Mesasge text  
                           @ErrorSeverity, -- Severity  
                           @ErrorState -- State  
                          );  
                RETURN 0; -- indicate failure  
            END CATCH;  
    END  
    ```  
  
3.  **[ファイル]** メニューの **[uspCancelOrder.sql の保存]** をクリックします。  
  
4.  F5 キーを押して **SimpleUnitTestDB**を配置します。  
  
    uspCancelOrder ストアド プロシージャへの更新を配置します。 その他のオブジェクトは変更していないため、そのストアド プロシージャのみが更新されます。  
  
    次に、このプロシージャの関連付けられた単体テストを定義します。  
  
#### <a name="to-write-the-sql-server-unit-test-for-uspcancelorder"></a>uspCancelOrder に対して SQL Server の単体テストを作成するには  
  
1.  SQL Server 単体テスト デザイナーのナビゲーション バーで、 **[Sales_uspCancelOrderTest]** をクリックし、 **[テスト]** が隣接する一覧で強調表示されていることを確認します。  
  
    この手順を実行したら、単体テスト内のテスト アクション用のテスト スクリプトを作成できます。  
  
2.  Transact\-SQL エディターで、次のステートメントに一致するように Transact\-SQL ステートメントを更新します。  
  
    ```  
    -- ssNoVersion unit test for Sales.uspFillOrder  
    DECLARE @RC AS INT, @CustomerID AS INT, @Amount AS INT, @FilledDate AS DATETIME, @Status AS CHAR (1);  
    DECLARE @CustomerName AS NVARCHAR(40), @OrderID AS INT;  
  
    SELECT @RC = 0,  
           @CustomerID = 0,  
           @OrderID = 0,  
           @CustomerName = N'Fictitious Customer',  
           @Amount = 100,  
           @FilledDate = getdate(),  
           @Status = 'O';  
  
    -- NOTE: Assumes that you inserted a Customer record with CustomerName='Fictitious Customer' in the pre-test script.  
    SELECT @CustomerID = [CustomerID] FROM [Sales].[Customer] WHERE [CustomerName] = @CustomerName;  
    -- Get the most recently added order.  
    SELECT @OrderID = MAX([OrderID]) FROM [Sales].[Orders] WHERE [CustomerID] = @CustomerID;  
  
    -- try to cancel an order for that customer that has already been filled  
    EXECUTE @RC = [Sales].[uspCancelOrder] @OrderID;  
  
    SELECT @RC AS RC;  
    ```  
  
3.  **[テスト条件]** ウィンドウで、[結果不確定] テスト条件をクリックし、 **[テスト条件を削除します]** アイコンをクリックします。  
  
4.  **[テスト条件]** ウィンドウの一覧で、 **[スカラー値]** をクリックし、 **[テスト条件を追加します]** アイコンをクリックします。  
  
5.  **[プロパティ]** ウィンドウで、 **[予期される値]** プロパティを 0 に設定します。  
  
6.  SQL Server 単体テスト デザイナーのナビゲーション バーで、 **[Sales_uspCancelOrderTest]** をクリックし、 **[事前テスト]** が隣接する一覧で強調表示されていることを確認します。 この手順の実行後に、テストの実行に必要な状態にデータを変更するステートメントを指定できます。 この例では、注文を行う前に Customer レコードを作成する必要があります。  
  
7.  **[作成するにはここをクリックしてください]** をクリックし、事前テスト スクリプトを作成します。  
  
8.  Transact\-SQL エディターで、次のステートメントに一致するように Transact\-SQL ステートメントを更新します。  
  
    ```  
    /*  
    Add Transact-SQL statements here to run before the test script is run.  
    */  
    BEGIN TRANSACTION  
  
    -- Add a customer for this test with the name 'CustomerB'  
    DECLARE @NewCustomerID AS INT, @RC AS INT, @CustomerName AS NVARCHAR (40);  
  
    SELECT @RC = 0,  
           @NewCustomerID = 0,  
           @CustomerName = N'Fictitious Customer';  
  
    IF NOT EXISTS(SELECT * FROM [Sales].[Customer] WHERE CustomerName = @CustomerName)  
    BEGIN  
    EXECUTE @NewCustomerID = [Sales].[uspNewCustomer] @CustomerName;  
    END  
  
    DECLARE @CustomerID AS INT, @Amount AS INT, @OrderDate AS DATETIME, @FilledDate AS DATETIME, @Status AS CHAR (1), @OrderID AS INT;  
  
    SELECT @RC = 0,  
           @CustomerID = 0,  
       @OrderID = 0,  
           @CustomerName = N'Fictitious Customer',  
           @Amount = 100,  
           @OrderDate = getdate(),  
       @FilledDate = getdate(),  
           @Status = 'O';  
  
    -- NOTE: Assumes that you inserted a Customer record with CustomerName='Fictitious Customer' in the pre-test script.  
    SELECT @CustomerID = [CustomerID] FROM [Sales].[Customer] WHERE [CustomerName] = @CustomerName;  
  
    -- delete any old records in the Orders table and clear out the YTD Sales/Orders fields  
    DELETE from [Sales].[Orders] WHERE [CustomerID] = @CustomerID;  
    UPDATE [Sales].[Customer] SET YTDOrders = 0, YTDSales = 0 WHERE [CustomerID] = @CustomerID;  
  
    -- place an order for that customer  
    EXECUTE @OrderID = [Sales].[uspPlaceNewOrder] @CustomerID, @Amount, @OrderDate, @Status;  
  
    -- fill the order for that customer  
    EXECUTE @RC = [Sales].[uspFillOrder] @OrderID, @FilledDate;  
  
    COMMIT TRANSACTION  
    ```  
  
9. **[ファイル]** メニューの **[すべてを保存]** をクリックします。  
  
    これで、テストを実行する準備が整いました。  
  
#### <a name="to-run-the-sql-server-unit-tests"></a>SQL Server の単体テストを実行するには  
  
1.  **[テスト ビュー]** で、 **[Sales_uspCancelOrderTest]** を右クリックし、 **[選択範囲の実行]** をクリックします。  
  
2.  **[テスト結果]** ウィンドウの結果を確認します。  
  
    テストは失敗し、次のエラーが表示されます。  
  
    **テスト メソッド TestProject1.SqlServerUnitTests1.Sales_uspCancelOrderTest で、次の例外がスローされました。System.Data.SqlClient.SqlException: 未処理注文のみキャンセルすることができます。**  
  
    次に、例外が予期されたものであることを示すようにコードを変更します。  
  
#### <a name="to-modify-the-code-for-the-unit-test"></a>単体テストのコードを変更するには  
  
1.  **ソリューション エクスプローラー**で、 **[TestProject1]** を展開し、 **[SqlServerUnitTests1.cs]** を右クリックして、 **[コードの表示]** をクリックします。  
  
2.  コード エディターで、Sales_uspCancelOrderTest メソッドに移動します。 メソッドの属性を次のコードのように変更します。  
  
    ```  
    [TestMethod(), ExpectedSqlException(Severity=16, MatchFirstError=false, State=1)]  
    public void Sales_uspCancelOrderTest()  
    ```  
  
    特定の例外が表示されることを予期するよう指定します。 必要に応じて、特定のエラー番号を指定することもできます。 この属性を追加しないと、単体テストは失敗し、メッセージが [テスト結果] ウィンドウに表示されます。  
  
    > [!IMPORTANT]  
    > 現在、Visual Studio 2012 では ExpectedSqlException 属性がサポートされていません。 これに対処する方法については、「 ["予期されるエラー" データベース単体テストを実行できない](https://social.msdn.microsoft.com/Forums/en-US/e74e06ad-e3c9-4cb0-97ad-a6f235a52345/unable-to-run-quotexpected-failurequot-database-unit-test)」を参照してください。  
  
3.  [ファイル] メニューの [SqlServerUnitTests1.cs の保存] をクリックします。  
  
    次に、単体テストを再実行し、予期したとおりにエラーになるかどうかを検証します。  
  
#### <a name="to-re-run-the-sql-server-unit-tests"></a>SQL Server の単体テストを再実行するには  
  
1.  **[テスト ビュー]** で、 **[Sales_uspCancelOrderTest]** を右クリックし、 **[選択範囲の実行]** をクリックします。  
  
2.  **[テスト結果]** ウィンドウの結果を確認します。  
  
    テストが成功したということは、プロシージャが失敗すると想定されていた場合に失敗したことを意味します。  
  
## <a name="next-steps"></a>Next Steps  
一般的なプロジェクトでは、追加の単体テストを定義して、重要なデータベース オブジェクトがすべて正しく動作することを確認します。 一連のテストが完了したら、これらのテストをバージョン管理にチェックインしてチームと共有します。  
  
ベースラインを設定したら、データベース オブジェクトを作成および変更し、変更によって予期される動作が妨げられないかどうかを確認するための関連テストを作成できます。  
  
## <a name="see-also"></a>参照  
[SQL Server の単体テストの作成と定義](../ssdt/creating-and-defining-sql-server-unit-tests.md)  
[SQL Server の単体テストを使用したデータベース コードの検証](../ssdt/verifying-database-code-by-using-sql-server-unit-tests.md)  
[空の SQL Server の単体テストを作成する方法](../ssdt/how-to-create-an-empty-sql-server-unit-test.md)  
[SQL Server の単体テストの実行を構成する方法](../ssdt/how-to-configure-sql-server-unit-test-execution.md)  
  
