---
title: 'T-SQL のチュートリアル: データベース オブジェクトの作成とクエリ | Microsoft Docs'
ms.custom: ''
ms.date: 07/30/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: conceptual
ms.assetid: 9fb8656b-0e4e-4ada-b404-4db4d3eea995
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c6e19142ab4d447678aedf6c841a74ed435eccea
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75257025"
---
# <a name="lesson-1-create-and-query-database-objects"></a>レッスン 1: データベース オブジェクトの作成とクエリ
[!INCLUDE[tsql-appliesto-ss2008-all-md](../includes/tsql-appliesto-ss2008-all-md.md)]

このレッスンでは、データベースを作成する方法、データベースにテーブルを作成する方法、およびテーブル内のデータにアクセスして変更する方法を説明します。 これは [!INCLUDE[tsql](../includes/tsql-md.md)]の入門レッスンであるため、これらのステートメントの各種オプションは使用せず、その説明も含まれていません。  
  
[!INCLUDE[tsql](../includes/tsql-md.md)] ステートメントは次の方法で作成して [!INCLUDE[ssDE](../includes/ssde-md.md)] に送信できます。  
  
-   [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]を使用する。 このチュートリアルでは、 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]を使用することを前提としていますが、 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] Express も使用できます。これは [Microsoft ダウンロード センター](https://www.microsoft.com/download/details.aspx?id=7593)から無料でダウンロードできます。  
  
-   [sqlcmd ユーティリティ](../tools/sqlcmd-utility.md)を使用する。  
  
-   作成したアプリケーションから接続する。  
  
コードは、そのステートメントを送信する方法にかかわらず、 [!INCLUDE[ssDE](../includes/ssde-md.md)] で同じ権限を使用して同様に実行します。  
  
[!INCLUDE[tsql](../includes/tsql-md.md)] で [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]ステートメントを実行するには、 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] を開き、 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]のインスタンスに接続します。  

## <a name="prerequisites"></a>前提条件
このチュートリアルを実行するには、SQL Server Management Studio と SQL Server インスタンスへのアクセスが必要です。 

- [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) をインストールします。

SQL Server インスタンスへのアクセス権を持っていない場合は、次のリンクからプラットフォームを選択します。 SQL 認証を選択する場合は、SQL Server のログイン資格情報を使用します。
- **Windows**:[SQL Server 2017 Developer Edition をダウンロードする](https://www.microsoft.com/sql-server/sql-server-downloads)。
- **macOS**:[Docker で SQL Server 2017 をダウンロードする](https://docs.microsoft.com/sql/linux/quickstart-install-connect-docker)。

## <a name="create-a-database"></a>データベースを作成する
多くの [!INCLUDE[tsql](../includes/tsql-md.md)] ステートメント同様、CREATE DATABASE ステートメントには、必須パラメーターがあります。必須パラメーターはデータベースの名前です。 また、CREATE DATABASE には、データベース ファイルを配置するディスクの場所など、多くのオプションのパラメーターがあります。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] でオプション パラメーターを指定せずに CREATE DATABASE を実行すると、これらの多くのパラメーターでは既定の値が使用されます。 このチュートリアルでは、オプションの構文パラメーターをほとんど使用しません。   

1.  クエリ エディターのウィンドウで、次のコードを入力します。ただし実行しないでください。  
  
    ```sql  
    CREATE DATABASE TestData  
    GO  
    ```  
  
2.  ポインターを使用して `CREATE DATABASE`の語句を選択し、 **F1**キーを押します。 SQL Server オンライン ブックの CREATE DATABASE のトピックが開きます。 この方法を使用して、このチュートリアルで使用する CREATE DATABASE やその他のステートメントの全構文を見つけることができます。  
  
3.  クエリ エディターで、 **F5** キーを押してステートメントを実行し、 `TestData`という名前のデータベースを作成します。  
  
データベースを作成すると、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] によって **モデル** データベースのコピーが作成され、その名前がデータベース名に変更されます。 オプション パラメーターでデータベースに大きな初期サイズを指定しなければ、この操作は数秒で完了します。  
  
> [!NOTE]  
> GO キーワードは、複数のステートメントを単一のバッチで送信した場合に、ステートメントを区切ります。 GO は、バッチにステートメントが 1 つしか入っていない場合はオプションです。  

## <a name="create-a-table"></a>テーブルを作成する
[!INCLUDE[tsql-appliesto-ss2008-all-md](../includes/tsql-appliesto-ss2008-all-md.md)]

テーブルを作成するには、テーブルの名前と、テーブル内の各列の名前とデータ型を入力する必要があります。 また、各列でヌル値を許可するかどうかを指定することも推奨されます。 テーブルを作成するには、テーブルを追加するスキーマに対して `CREATE TABLE` アクセス許可と `ALTER SCHEMA` アクセス許可を持っている必要があります。 [`db_ddladmin`](../relational-databases/security/authentication-access/database-level-roles.md) 固定データベース ロールには、これらのアクセス許可があります。  
  
ほとんどのテーブルに、テーブルの 1 つ以上の列で構成された主キーがあります。 主キーは常に一意です。 [!INCLUDE[ssDE](../includes/ssde-md.md)] によって、主キーの値がテーブルで重複しないように制限されます。  
  
データ型のリストと、それぞれの説明のリンクについては、「[データ型 (Transact-SQL)](../t-sql/data-types/data-types-transact-sql.md)」を参照してください。  
  
> [!NOTE]  
> [!INCLUDE[ssDE](../includes/ssde-md.md)] は、大文字と小文字を区別するか区別しないかを設定してインストールできます。 大文字と小文字を区別するように設定して [!INCLUDE[ssDE](../includes/ssde-md.md)] をインストールした場合は、オブジェクト名を常に大文字か小文字に統一する必要があります。 たとえば、OrderData という名前のテーブルと、ORDERDATA という名前のテーブルは別のテーブルです。 大文字と小文字を区別しないように設定して [!INCLUDE[ssDE](../includes/ssde-md.md)] をインストールした場合、この 2 つのテーブル名は同じテーブルと見なされるため、その名前は一度しか使用できません。  
  
  
### <a name="switch-the-query-editor-connection-to-the-testdata-database"></a>クエリ エディター接続から TestData データベースへの切り替え  
接続を `TestData` データベースに変更するには、クエリ エディターのウィンドウで次のコードを入力して実行します。  
  
  ```sql  
  USE TestData  
  GO  
  ```  
  
### <a name="create-the-table"></a>テーブルの作成
クエリ エディターのウィンドウで、次のコードを入力して実行し、 `Products`という名前の単純なテーブルを作成します。 テーブルの列は `ProductID`、 `ProductName`、 `Price`、 `ProductDescription`という名前です。 `ProductID` 列がテーブルの主キーです。 `int`、 `varchar(25)`、 `money`、 `varchar(max)` は、すべてデータ型です。 行を挿入または変更するときにデータを入力しなくてもよい列は、 `Price` と `ProductionDescription` のみです。 このステートメントには、スキーマというオプションの要素 (`dbo.`) が含まれています。 スキーマは、テーブルを所有するデータベース オブジェクトです。 管理者の場合は、 `dbo` が既定のスキーマです。 `dbo` はデータベース所有者を表します。  
  
  ```sql  
  CREATE TABLE dbo.Products  
     (ProductID int PRIMARY KEY NOT NULL,  
     ProductName varchar(25) NOT NULL,  
     Price money NULL,  
     ProductDescription varchar(max) NULL)  
  GO  
 ```  

## <a name="insert-and-update-data-in-a-table"></a>テーブルでのデータの挿入と更新
**Products** テーブルを作成したので、INSERT ステートメントを使用してデータをテーブルに挿入する準備ができました。 データを挿入した後は、UPDATE ステートメントを使用して行の内容を変更します。 更新を 1 つの行に制限するには、UPDATE ステートメントの WHERE 句を使用します。 4 つのステートメントによって、次のデータが入力されます。  
  
|ProductID|ProductName|Price|ProductDescription|  
|-------------|---------------|---------|----------------------|  
|1|Clamp|12.48|Workbench clamp|  
|50|Screwdriver|3.17|Flat head|  
|75|Tire Bar||Tool for changing tires|  
|3000|3mm Bracket|.52||  
  
基本構文は次のとおりです。INSERT、テーブル名、列一覧、VALUES、挿入する値の一覧。 行の先頭にある 2 つのハイフンは、その行がコメントであることを示します。この行のテキストはコンパイラによって無視されます。 この場合、コメントは構文に許可されているバリエーションを記述します。  
  
### <a name="insert-data-into-a-table"></a>データをテーブルに挿入  
  
1.  次のステートメントを実行し、前のタスクで作成した `Products` テーブルに行を挿入します。 これは基本構文です。  
  
   ```sql 
   -- Standard syntax  
   INSERT dbo.Products (ProductID, ProductName, Price, ProductDescription)  
       VALUES (1, 'Clamp', 12.48, 'Workbench clamp')  
   GO   
   ```  
  
2.  次のステートメントは、フィールド一覧 (かっこ内) と値一覧の両方にある `ProductID` と `ProductName` の配置を交換することで、パラメーターの順序を変更する方法を示しています。  
  
   ```sql  
   -- Changing the order of the columns  
   INSERT dbo.Products (ProductName, ProductID, Price, ProductDescription)  
       VALUES ('Screwdriver', 50, 3.17, 'Flat head')  
   GO    
   ```  
  
3.  次のステートメントは、値が正しい順序で示されている限り、列の名前はオプションであることを示しています。 この構文は一般的ですが、他のユーザーがコードを理解しにくいため、推奨されません。 `NULL` が `Price` 列に指定されているのは、この製品の価格が不明ためです。  
  
   ```sql  
   -- Skipping the column list, but keeping the values in order  
   INSERT dbo.Products  
       VALUES (75, 'Tire Bar', NULL, 'Tool for changing tires.')  
   GO  
  ```  
  
4.  スキーマ名は、既定のスキーマ内のテーブルにアクセスし、変更している場合にはオプションです。 `ProductDescription` 列では NULL 値が許可されており、値が提供されていないため、 `ProductDescription` 列の名前と値はステートメントから完全に省略できます。  
  
   ```sql  
   -- Dropping the optional dbo and dropping the ProductDescription column  
   INSERT Products (ProductID, ProductName, Price)  
       VALUES (3000, '3mm Bracket', .52)  
   GO  
   ```  
  
### <a name="update-the-products-table"></a>Products テーブルの更新  
次の `UPDATE` ステートメントを入力して実行し、2 番目の製品の `ProductName` を `Screwdriver`から `Flat Head Screwdriver`に変更します。  
  
  ```sql  
  UPDATE dbo.Products  
      SET ProductName = 'Flat Head Screwdriver'  
      WHERE ProductID = 50  
  GO  
  ```  

## <a name="read-data-from-a-table"></a>テーブルからデータを読み取る
テーブルのデータを読み取るには、SELECT ステートメントを使用します。 SELECT ステートメントは最も重要な [!INCLUDE[tsql](../includes/tsql-md.md)] ステートメントの 1 つで、構文には多くのバリエーションがあります。 このチュートリアルでは、5 つの単純なバージョンを使用します。  
  
### <a name="read-the-data-in-a-table"></a>テーブル内のデータを読み取る  
  
1.  次のステートメントを入力して実行し、 `Products` テーブルのデータを読み取ります。  
  
  ```sql 
  -- The basic syntax for reading data from a single table  
  SELECT ProductID, ProductName, Price, ProductDescription  
      FROM dbo.Products  
  GO  
  ```  
  
2.  アスタリスクを使用すると、テーブルの列をすべて選択できます。 これはアドホック クエリでよく使用されます。 永続的なコード内では列一覧を指定して、新しい列が後からテーブルに追加された場合でも、予測された列がステートメントによって返されるようにしてください。  
  
  ```sql  
  -- Returns all columns in the table  
  -- Does not use the optional schema, dbo  
  SELECT * FROM Products  
  GO   
  ```  
  
3.  返す必要のない列は省略できます。 列は、一覧内の順序で返されます。  
  
  ```sql  
  -- Returns only two of the columns from the table  
  SELECT ProductName, Price  
      FROM dbo.Products  
  GO    
  ```  
  
4.  ユーザーに返される行を制限するには、 `WHERE` 句を使用します。  
  
  ``` sql 
  -- Returns only two of the records in the table  
  SELECT ProductID, ProductName, Price, ProductDescription  
      FROM dbo.Products  
      WHERE ProductID < 60  
  GO    
  ```  
  
5.  列内の値は、列が返されたときに操作できます。 次の例では、 `Price` 列に対して数学的演算を実行します。 このようにして変更された列には、 `AS` キーワードを使用して名前を指定しない限り、名前が付けられません。  
  
  ```sql  
  -- Returns ProductName and the Price including a 7% tax  
  -- Provides the name CustomerPays for the calculated column  
  SELECT ProductName, Price * 1.07 AS CustomerPays  
      FROM dbo.Products  
  GO  
  ```  
  
### <a name="useful-functions-in-a-select-statement"></a>SELECT ステートメント内で役に立つ関数  
SELECT ステートメント内のデータの操作に使用できる関数の詳細については、次のトピックを参照してください。  
  
|||  
|-|-|  
|[文字列関数 &#40;Transact-SQL&#41;](../t-sql/functions/string-functions-transact-sql.md)|[日付と時刻のデータ型および関数 &#40;Transact-SQL&#41;](../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)|  
|[数学関数 &#40;Transact-SQL&#41;](../t-sql/functions/mathematical-functions-transact-sql.md)|[テキスト関数とイメージ関数 (Transact-SQL)](https://msdn.microsoft.com/library/b9c70488-1bf5-4068-a003-e548ccbc5199)|  

## <a name="create-views-and-stored-procedures"></a>ビューとストアド プロシージャの作成
ビューは、格納された SELECT ステートメントで、ストアド プロシージャは、バッチとして実行される 1 つ以上の [!INCLUDE[tsql](../includes/tsql-md.md)] ステートメントです。  
  
ビューに対しては、テーブルと同じようにクエリが実行されます。パラメーターは使用できません。 ストアド プロシージャは、ビューよりも複雑です。 ストアド プロシージャは、入力と出力のパラメーターを指定でき、IF ステートメントや WHILE ステートメントなどの、コードの流れを制御するステートメントを含めることができます。 データベース内でのすべての繰り返し操作には、ストアド プロシージャを使用することをお勧めします。  
  
この例では、CREATE VIEW を使用して、 **Products** テーブル内の 2 つの列だけを選択するビューを作成します。 次に、CREATE PROCEDURE を使用して、価格のパラメーターを受け入れ、指定されたパラメーター値よりも価格が安い製品のみを返すストアド プロシージャを作成します。  
  
### <a name="create-a-view"></a>ビューの作成  
  
次のステートメントを実行して、SELECT ステートメントを実行する非常に単純なビューを作成し、製品の名前と価格をユーザーに返します。  
  
  ```sql  
  CREATE VIEW vw_Names  
     AS  
     SELECT ProductName, Price FROM Products;  
  GO    
  ```  
  
### <a name="test-the-view"></a>ビューのテスト  
  
ビューはテーブルと同じように処理されます。 ビューにアクセスするには `SELECT` ステートメントを使用します。  
  
  ```sql  
  SELECT * FROM vw_Names;  
  GO   
  ```  
  
### <a name="create-a-stored-procedure"></a>ストアド プロシージャの作成  
  
次のステートメントでは、 `pr_Names`という名前のストアド プロシージャを作成し、 `@VarPrice` という名前の、 `money`データ型の入力パラメーターを受け入れます。 このストアド プロシージャによって、 `Products less than` データ型から `money` 文字データ型に変更される入力パラメーターと連結されるステートメント `varchar(10)` が出力されます。 次に、ビューに対して `SELECT` ステートメントが実行され、 `WHERE` 句の一部として入力パラメーターが渡されます。 これによって、入力パラメーター値よりも価格が安い製品がすべて返されます。  
  
  ```sql  
  CREATE PROCEDURE pr_Names @VarPrice money  
     AS  
     BEGIN  
        -- The print statement returns text to the user  
        PRINT 'Products less than ' + CAST(@VarPrice AS varchar(10));  
        -- A second statement starts here  
        SELECT ProductName, Price FROM vw_Names  
              WHERE Price < @varPrice;  
     END  
  GO    
  ```  
  
### <a name="test-the-stored-procedure"></a>ストアド プロシージャのテスト  
  
ストアド プロシージャをテストするには、次のステートメントを入力して実行します。 このプロシージャによって、レッスン 1 で `Products` テーブルに入力した、価格が `10.00`より安い 2 つの製品の名前が返されます。  
  
  ```sql  
  EXECUTE pr_Names 10.00;  
  GO  
  ```  

## <a name="next-steps"></a>次のステップ
次の記事では、データベース オブジェクトに対してアクセス許可を構成する方法について説明します。 レッスン 1 で作成したオブジェクトは、レッスン 2 でも使用されます。 

詳細については、次の記事に進んでください
> [!div class="nextstepaction"]
> [次の手順](../t-sql/lesson-2-configuring-permissions-on-database-objects.md)
  
  
  
