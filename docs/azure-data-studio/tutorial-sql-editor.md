---
title: Transact-SQL エディターを使用し、データベース オブジェクトを作成する
titleSuffix: Azure Data Studio
description: このチュートリアルでは、T-SQL の操作を簡単にする Azure Data Studio の主な機能について説明します。
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: tutorial
author: markingmyname
ms.author: maghan
ms.reviewer: alayu; sstein
ms.custom: seodec18; seo-lt-2019
ms.date: 09/24/2018
ms.openlocfilehash: 65f078c16080f9ae54563acb5bd21c50d2036057
ms.sourcegitcommit: 39ea690996a7390e3d13d6fb8f39d8641cd5f710
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/10/2019
ms.locfileid: "74957036"
---
# <a name="tutorial-use-the-transact-sql-editor-to-create-database-objects---includename-sosincludesname-sos-shortmd"></a>チュートリアル:Transact-SQL エディターを使用し、データベース オブジェクトを作成する - [!INCLUDE[name-sos](../includes/name-sos-short.md)]

クエリ、ストアド プロシージャ、スクリプトなどの作成と実行は、データベース プロフェッショナルの中心的な仕事です。 このチュートリアルでは、データベース オブジェクトを作成するための T-SQL の主な機能について説明します。

このチュートリアルでは、次の目的で [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] を使用する方法について学習します。
> [!div class="checklist"]
> * データベース オブジェクトを検索する
> * テーブル データを編集する 
> * スニペットを利用して T-SQL を簡単に記述する
> * *[定義をここに表示]* と *[定義へ移動]* を使用し、データベース オブジェクトの詳細を表示する


## <a name="prerequisites"></a>前提条件

このチュートリアルには、SQL Server か Azure SQL Database *TutorialDB* が必要です。 *TutorialDB* データベースを作成するには、次のクイックスタートのいずれかを実行します。

- [[!INCLUDE[name-sos-short](../includes/name-sos-short.md)] を使用して SQL Server に接続し、クエリを実行する](quickstart-sql-server.md)
- [[!INCLUDE[name-sos-short](../includes/name-sos-short.md)] を使用して Azure SQL Database に接続し、クエリを実行する](quickstart-sql-database.md)


## <a name="quickly-locate-a-database-object-and-perform-a-common-task"></a>データベース オブジェクトを簡単に見つけ、一般的タスクを実行する

[!INCLUDE[name-sos-short](../includes/name-sos-short.md)] には、データベース オブジェクトを簡単に見つけるための検索ウィジェットがあります。 結果一覧からは、テーブルの*データ編集*など、選択したオブジェクトに関連する一般的タスクのコンテキスト メニューが与えられます。

1. [サーバー] サイドバーを開き (**Ctrl + G**)、 **[データベース]** を展開し、 **[TutorialDB]** を選択します。 

1. **[TutorialDB]** を右クリックし、コンテキスト メニューから **[管理]** を選択することで *[TutorialDB ダッシュボード]* を開きます。

   ![コンテキスト メニュー - 管理](./media/tutorial-sql-editor/insight-open-dashboard.png)

1. ダッシュボードで (検索ウィジェットで) **[dbo.Customers]** を右クリックし、 **[データの編集]** を選択します。
   
   > [!TIP]
   > オブジェクトがたくさん含まれるデータベースの場合、検索ウィジェットを使用することで、探しているテーブルやビューなどが簡単に見つかります。

   ![クイック検索ウィジェット](./media/tutorial-sql-editor/quick-search-widget.png)

1. 最初の行の **[電子メール]** 列を編集して「*orlando0\@adventure-works.com*」と入力し、**Enter** キーを押して変更を保存します。

   ![データの編集](./media/tutorial-sql-editor/edit-data.png)

## <a name="use-t-sql-snippets-to-create-stored-procedures"></a>T-SQL スニペットを使用し、ストアド プロシージャを作成する

[!INCLUDE[name-sos](../includes/name-sos-short.md)] には、ステートメントを簡単に作成するための T-SQL スニペットがたくさん組み込まれています。


1. **Ctrl + N** を押し、新しいクエリ エディターを開きます。

2. エディターに「**sql**」と入力し、矢印を下に押して **[sqlCreateStoredProcedure]** を見つけ、*Tab* キー (または *Enter*) を押して create ストアド プロシージャ スニペットを読み込みます。

   ![スニペットの一覧](./media/tutorial-sql-editor/snippet-list.png)

3. create ストアド プロシージャには、簡単に編集するためのフィールドが 2 つ設定されています。*StoredProcedureName* と *SchemaName* です。 *[StoredProcedureName]* を選択し、右クリックし、 **[すべての出現箇所を変更]** を選択します。 ここで「*getCustomer*」と入力すると、*StoredProcedureName* エントリがすべて、*getCustomer* に変わります。

   ![スニペット](./media/tutorial-sql-editor/snippet.png)

5. *SchemaName* が出現する箇所をすべて *dbo* に変更します。 
6. このスニペットには、更新を必要とするプレースホルダー パラメーターと本文テキストが含まれています。 *EXECUTE* ステートメントには、プレースホルダー テキストも含まれています。プロシージャに与えられるパラメーターの数がわからないためです。 このチュートリアルのために、次のコードのようになるようにスニペットを更新します。

    ```sql
    -- Create a new stored procedure called 'getCustomer' in schema 'dbo'
    -- Drop the stored procedure if it already exists
    IF EXISTS (
    SELECT *
    FROM INFORMATION_SCHEMA.ROUTINES
    WHERE SPECIFIC_SCHEMA = N'dbo'
    AND SPECIFIC_NAME = N'getCustomer'
    )
    DROP PROCEDURE dbo.getCustomer
    GO
    -- Create the stored procedure in the specified schema
    CREATE PROCEDURE dbo.getCustomer
    @ID int
    -- add more stored procedure parameters here
    AS
    -- body of the stored procedure
    SELECT  c.CustomerId, 
    c.Name, 
    c.Location, 
    c.Email
    FROM dbo.Customers c
    WHERE c.CustomerId = @ID
    FOR JSON PATH

    GO
    -- example to execute the stored procedure we just created
    EXECUTE dbo.getCustomer 1
    GO
    ```
    
5. ストアド プロシージャを作成し、テスト実行するには、**F5** を押します。

これでストアド プロシージャが作成され、 **[結果]** ペインに返された顧客が JSON で表示されます。 書式設定された JSON を表示するには、返されたレコードをクリックします。 


## <a name="use-peek-definition"></a>[定義をここに表示] を使用する 

[!INCLUDE[name-sos](../includes/name-sos-short.md)] では、[定義をここに表示] 機能を使用し、オブジェクトの定義を表示できます。 このセクションでは、2 つ目のストアド プロシージャを作成します。[定義をここに表示] を使用してテーブルに入っている列を表示し、ストアド プロシージャの本文を簡単に作成します。

1. **Ctrl + N** を押し、新しいエディターを開きます。 

2. エディターに「*sql*」と入力し、矢印を下に押して *[sqlCreateStoredProcedure]* を見つけ、*Tab* キー (または *Enter*) を押して create ストアド プロシージャ スニペットを読み込みます。
3. *[StoredProcedureName]* に「*setCustomer*」と入力し、 *[SchemaName]* に「*dbo*」と入力します。

3. @param プレースホルダーを次のパラメーター定義に置き換えます。

   ```sql
   @json_val nvarchar(max)
   ```

4. ストアド プロシージャの本文を次のコードに置き換えます。
   ```sql
   INSERT INTO dbo.Customers
   ```

5. 追加したばかりの *[INSERT]* 行で、 **[dbo.Customers]** を右クリックし、 **[定義をここに表示]** を選択します。

   ![[定義をここに表示]](./media/tutorial-sql-editor/peek-definition.png)

6. テーブルの定義が表示されるので、テーブルに入っている列を簡単に確認できます。 列の一覧を参照することで、ストアド プロシージャのステートメント入力が簡単になります。 前に追加した INSERT ステートメントを作成してストアド プロシージャの本文を完了し、[定義をここに表示] ウィンドウを閉じます。

   ```sql
   INSERT INTO dbo.Customers (CustomerId, Name, Location, Email)
       SELECT CustomerId, Name, Location, Email
       FROM OPENJSON (@json_val)
       WITH(   CustomerId int, 
               Name nvarchar(50), 
               Location nvarchar(50), 
               Email nvarchar(50)
    )
   ```
7. クエリの一番下にある *EXECUTE* コマンドを削除します (または、コメントアウトします)。
8. ステートメント全体は次のコードのようになります。

   ```sql
   -- Create a new stored procedure called 'setCustomer' in schema 'dbo'
   -- Drop the stored procedure if it already exists
   IF EXISTS (
   SELECT *
       FROM INFORMATION_SCHEMA.ROUTINES
       WHERE SPECIFIC_SCHEMA = N'dbo'
       AND SPECIFIC_NAME = N'setCustomer'
   )
   DROP PROCEDURE dbo.setCustomer
   GO
   -- Create the stored procedure in the specified schema
   CREATE PROCEDURE dbo.setCustomer
       @json_val nvarchar(max) 
   AS
       -- body of the stored procedure
       INSERT INTO dbo.Customers (CustomerId, Name, Location, Email)
       SELECT CustomerId, Name, Location, Email
       FROM OPENJSON (@json_val)
       WITH(   CustomerId int, 
               Name nvarchar(50), 
               Location nvarchar(50), 
               Email nvarchar(50)
       )
   GO
   ```

8. *setCustomer* ストアド プロシージャを作成するには、**F5** を押します。

## <a name="use-save-query-results-as-json-to-test-the-setcustomer-stored-procedure"></a>クエリ結果を JSON として保存し、setCustomer ストアド プロシージャをテストする

前のセクションで作成した *setCustomer* ストアド プロシージャでは、JSON データを *\@json_val* パラメーターに渡す必要があります。 このセクションでは、ストアド プロシージャをテストできるように、パラメーターに渡す目的で正しく書式設定した JSON を用意する方法について説明します。

1. **[サーバー]** サイドバーで、 *[dbo.Customers]* テーブルを右クリックし、 **[SELECT TOP 1000 Rows]\(上位 1000 行を選択する\)** をクリックします。

2. 結果ビューの最初の行を選択し、行全体が選択されるようにします (左端の列の番号 1 をクリックします)。それから **[Save as JSON]\(JSON として保存\)** を選択します。  
3. ファイルを後で削除できるように、覚えやすい場所にフォルダーを変更し (デスクトップなど)、 **[保存]** をクリックします。 JSON 形式のファイルが開きます。

   ![JSON として保存する](./media/tutorial-sql-editor/save-as-json.png)

4. エディターで JSON データを選択してコピーします。
5. **Ctrl + N** を押し、新しいエディターを開きます。
6. 前の手順からは、*setCustomer* プロシージャを呼び出せるように正しく書式設定されたデータを簡単に得る方法がわかります。 次のコードでは、新しい顧客詳細で同じ JSON フォーマットを使用しています。そのため、*setCustomer* プロシージャをテストできます。 ステートメントには、パラメーターを宣言し、新しい get プロシージャと set プロシージャを実行する構文が含まれています。 前のセクションからコピーしたデータを貼り付け、次の例と同じになるように編集できます。あるいは、クエリ エディターに次のステートメントを単純に貼り付けてください。

   ```sql
   -- example to execute the stored procedure we just created
   declare @json nvarchar(max) =
   N'[
       {
           "CustomerId": 5,
           "Name": "Lucy",
           "Location": "Canada",
           "Email": "lucy0@adventure-works.com"
       }
   ]'

   EXECUTE dbo.setCustomer @json_val = @json
   GO

   EXECUTE dbo.getCustomer @ID = 5
   ```

7. **F5** を押してスクリプトを実行します。 このスクリプトにより、新しい顧客が挿入され、新しい顧客の情報が JSON 形式で返されます。 結果をクリックし、書式設定されたビューを開きます。

   ![テスト結果](./media/tutorial-sql-editor/test-result.png)

## <a name="next-steps"></a>次のステップ
このチュートリアルでは、以下の内容を学習しました。
> [!div class="checklist"]
> * スキーマ オブジェクトをクイック検索する
> * テーブル データを編集する 
> * スニペットを使用して T-SQL スクリプトを記述する
> * [定義をここに表示] と [定義へ移動] を使用し、データベース オブジェクトの詳細を確認する


**最低速 5 つのクエリ**を有効にする方法については、次のチュートリアルを完了してください。

> [!div class="nextstepaction"]
> [最低速クエリのサンプル分析情報ウィジェットを有効にする](tutorial-qds-sql-server.md)
