---
title: テーブル値パラメーターを使用する |Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 3af61054-a886-4e1a-ad85-93f87c6d3584
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 98863afb5a47eddfd311563bd03a1c7c7120b161
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2019
ms.locfileid: "69025716"
---
# <a name="using-table-valued-parameters"></a>テーブル値パラメーターの使用

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

テーブル値パラメーターは、複数行のデータをクライアント アプリケーションから SQL Server に簡単にマーシャリングするための手段です。複数のラウンド トリップや、データ処理用の特別なサーバー側ロジックは必要ありません。 テーブル値パラメーターを使用すると、クライアント アプリケーションで複数行のデータをカプセル化してサーバーに送信する処理を 1 つのパラメーター化コマンドで実行できます。 受信データ行はテーブル変数に格納され、Transact-SQL を使用して操作できます。  
  
テーブル値パラメーターの列値には、標準の Transact-sql SELECT ステートメントを使用してアクセスできます。 テーブル値パラメーターは厳密に型指定され、その構造は自動的に検証されます。 テーブル値パラメーターのサイズは、サーバーのメモリによってのみ制限されます。  
  
> [!NOTE]  
> テーブル値パラメーターのサポートは、Microsoft JDBC Driver 6.0 for SQL Server から入手できます。
>
> テーブル値パラメーターにデータを返すことはできません。 テーブル値パラメーターは入力専用です。OUTPUT キーワードはサポートされていません。  
  
 テーブル値パラメーターの詳細については、次のリソースを参照してください。  
  
| リソース                                                                                                             | [説明]                                                                         |
| -------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------- |
| SQL Server オンラインブックの[テーブル値パラメーター (データベースエンジン)](https://go.microsoft.com/fwlink/?LinkId=98363) | テーブル値パラメーターを作成して使用する方法について説明します。                             |
| SQL Server オンラインブックでの[ユーザー定義テーブル型](https://go.microsoft.com/fwlink/?LinkId=98364)                  | テーブル値パラメーターを宣言するために使用されるユーザー定義テーブル型について説明します。 |
| CodePlex の[Microsoft SQL Server データベースエンジン](https://go.microsoft.com/fwlink/?LinkId=120507)セクション        | SQL Server の機能を使用する方法を示すサンプルが含まれています。  |
  
## <a name="passing-multiple-rows-in-previous-versions-of-sql-server"></a>以前のバージョンの SQL Server で複数の行を渡す  

SQL Server 2008 にテーブル値パラメーターが導入される前に、複数行のデータをストアドプロシージャまたはパラメーター化 SQL コマンドに渡すオプションは限られていました。 開発者は、次のオプションを選択して、複数の行をサーバーに渡すことができます。  
  
- 複数の列とデータ行の値を表すために、一連の個別のパラメーターを使用します。 このメソッドを使用して渡すことができるデータの量は、許可されているパラメーターの数によって制限されます。 SQL Server プロシージャは、最大で2100のパラメーターを持つことができます。 これらの個々の値をテーブル変数または一時テーブルにまとめて処理するには、サーバー側のロジックが必要です。  
  
- 複数のデータ値を区切られた文字列または XML ドキュメントにバンドルし、それらのテキスト値をプロシージャまたはステートメントに渡します。 そのためには、プロシージャまたはステートメントに、データ構造の検証と値のバンドル化に必要なロジックが含まれている必要があります。  
  
- 複数の行に影響を与えるデータ変更のために、一連の個別の SQL ステートメントを作成します。 変更は、個別にサーバーに送信したり、グループにバッチ処理したりすることができます。 ただし、複数のステートメントを含むバッチで送信された場合でも、各ステートメントはサーバー上で個別に実行されます。  
  
- Bcp ユーティリティプログラムまたは[SQLServerBulkCopy](https://msdn.microsoft.com/library/system.data.sqlclient.sqlbulkcopy(v=vs.110).aspx)オブジェクトを使用して、多数のデータ行をテーブルに読み込みます。 この手法は非常に効率的ですが、データが一時テーブルまたはテーブル変数に読み込まれない限り、サーバー側の処理はサポートされません。  
  
## <a name="creating-table-valued-parameter-types"></a>テーブル値パラメーターの型の作成  

テーブル値パラメーターは、transact-sql `CREATE TYPE`ステートメントを使用して定義される、厳密に型指定されたテーブル構造に基づいています。 クライアントアプリケーションでテーブル値パラメーターを使用するには、テーブル型を作成し、その構造を SQL Server で定義する必要があります。 テーブル型の作成の詳細については、「SQL Server オンラインブックの[ユーザー定義テーブル型](https://go.microsoft.com/fwlink/?LinkID=98364)」を参照してください。  

```sql
CREATE TYPE dbo.CategoryTableType AS TABLE  
    ( CategoryID int, CategoryName nvarchar(50) )  
```

テーブル型を作成した後は、その型に基づいてテーブル値パラメーターを宣言できます。 次の Transact-sql フラグメントは、ストアドプロシージャの定義でテーブル値パラメーターを宣言する方法を示しています。 テーブル値パラメーター `READONLY`を宣言するには、キーワードが必要であることに注意してください。  

```sql
CREATE PROCEDURE usp_UpdateCategories
    (@tvpNewCategories dbo.CategoryTableType READONLY)  
```

## <a name="modifying-data-with-table-valued-parameters-transact-sql"></a>テーブル値パラメーターを使用したデータの変更 (Transact-sql)  

テーブル値パラメーターは、1つのステートメントを実行して複数の行に影響を与えるセットベースのデータ変更で使用できます。 たとえば、テーブル値パラメーター内のすべての行を選択してデータベーステーブルに挿入できます。また、更新するテーブルにテーブル値パラメーターを結合して update ステートメントを作成することもできます。  
  
次の Transact-sql UPDATE ステートメントは、テーブル値パラメーターを Categories テーブルに結合して使用する方法を示しています。 FROM 句の中でテーブル値パラメーターを JOIN と共に使用する場合は、次に示すように、テーブル値パラメーターのエイリアスを "ec" にする必要があります。  

```sql
UPDATE dbo.Categories  
    SET Categories.CategoryName = ec.CategoryName  
    FROM dbo.Categories INNER JOIN @tvpEditedCategories AS ec  
    ON dbo.Categories.CategoryID = ec.CategoryID;  
```

この Transact-sql の例では、テーブル値パラメーターから行を選択して、1つのセットベースの操作で挿入を実行する方法を示します。

```sql
INSERT INTO dbo.Categories (CategoryID, CategoryName)  
    SELECT nc.CategoryID, nc.CategoryName FROM @tvpNewCategories AS nc;  
```

## <a name="limitations-of-table-valued-parameters"></a>テーブル値パラメーターの制限事項

テーブル値パラメーターにはいくつかの制限があります。  
  
- テーブル値パラメーターをユーザー定義関数に渡すことはできません。  
  
- テーブル値パラメーターは、UNIQUE 制約または PRIMARY KEY 制約をサポートするためにのみインデックスを設定できます。 SQL Server では、テーブル値パラメーターの統計が保持されません。  
  
- テーブル値パラメーターは、Transact-sql コードでは読み取り専用です。 テーブル値パラメーターの行の列の値を更新することはできません。行を挿入したり削除したりすることはできません。 テーブル値パラメーターのストアドプロシージャまたはパラメーター化されたステートメントに渡されるデータを変更するには、一時テーブルまたはテーブル変数にデータを挿入する必要があります。  
  
- ALTER TABLE ステートメントを使用して、テーブル値パラメーターのデザインを変更することはできません。

- 大きなオブジェクトは、テーブル値パラメーターでストリームできます。  
  
## <a name="configuring-a-table-valued-parameter"></a>テーブル値パラメーターの構成

Microsoft JDBC Driver 6.0 for SQL Server 以降、テーブル値パラメーターは、パラメーター化されたステートメントまたはパラメーター化されたストアドプロシージャでサポートされます。 テーブル値パラメーターは、SQLServerDataTable、ResultSet、またはユーザーが指定した ISQLServerDataRecord インターフェイスの実装から設定できます。 準備されたクエリに対してテーブル値パラメーターを設定する場合は、サーバーで以前に作成した互換性のある型の名前と一致する必要がある型名を指定する必要があります。  
  
次の2つのコードフラグメントでは、SQLServerPreparedStatement を使用してテーブル値パラメーターを構成する方法と、データを挿入する SQLServerCallableStatement を使用する方法を示します。 ここで、sourceTVPObject には SQLServerDataTable、ResultSet、または ISQLServerDataRecord オブジェクトを指定できます。 この例では、接続がアクティブな接続オブジェクトであることを想定しています。  

```java
// Using table-valued parameter with a SQLServerPreparedStatement.  
SQLServerPreparedStatement pStmt =
    (SQLServerPreparedStatement) connection.prepareStatement("INSERT INTO dbo.Categories SELECT * FROM ?");  
pStmt.setStructured(1, "dbo.CategoryTableType", sourceTVPObject);  
pStmt.execute();  
```

```java
// Using table-valued parameter with a SQLServerCallableStatement.  
SQLServerCallableStatement pStmt =
    (SQLServerCallableStatement) connection.prepareCall("exec usp_InsertCategories ?");
pStmt.setStructured(1, "dbo.CategoryTableType", sourceTVPObject);;  
pStmt.execute();  
```

> [!NOTE]  
> テーブル値パラメーターの設定に使用できる Api の完全な一覧については、次の「 **JDBC Driver 用のテーブル値パラメーター API** 」セクションを参照してください。  
  
## <a name="passing-a-table-valued-parameter-as-a-sqlserverdatatable-object"></a>SQLServerDataTable オブジェクトとしてテーブル値パラメーターを渡す  

SQL Server 用の Microsoft JDBC Driver 6.0 以降では、SQLServerDataTable クラスはリレーショナルデータのメモリ内テーブルを表します。 この例では、SQLServerDataTable オブジェクトを使用して、インメモリデータからテーブル値パラメーターを構築する方法を示します。 このコードでは、まず SQLServerDataTable オブジェクトを作成し、そのスキーマを定義して、テーブルにデータを挿入します。 このコードは、このデータテーブルを SQL Server にテーブル値パラメーターとして渡す SQLServerPreparedStatement を構成します。  

```java
/* Assumes connection is an active Connection object. */

// Create an in-memory data table.  
SQLServerDataTable sourceDataTable = new SQLServerDataTable();
  
// Define metadata for the data table.  
sourceDataTable.addColumnMetadata("CategoryID" ,java.sql.Types.INTEGER);
sourceDataTable.addColumnMetadata("CategoryName" ,java.sql.Types.NVARCHAR);
  
// Populate the data table.  
sourceDataTable.addRow(1, "CategoryNameValue1");
sourceDataTable.addRow(2, "CategoryNameValue2");
  
// Pass the data table as a table-valued parameter using a prepared statement.  
SQLServerPreparedStatement pStmt =
        (SQLServerPreparedStatement) connection.prepareStatement(  
            "INSERT INTO dbo.Categories SELECT * FROM ?;");  
pStmt.setStructured(1, "dbo.CategoryTableType", sourceDataTable);  
pStmt.execute();  
```

> [!NOTE]  
> テーブル値パラメーターの設定に使用できる Api の完全な一覧については、次の「 **JDBC Driver 用のテーブル値パラメーター API** 」セクションを参照してください。  
  
## <a name="passing-a-table-valued-parameter-as-a-resultset-object"></a>テーブル値パラメーターを ResultSet オブジェクトとして渡す  

この例では、結果セットからテーブル値パラメーターにデータの行をストリームする方法を示します。 このコードでは、まず、内のソーステーブルからデータを取得して、SQLServerDataTable オブジェクトを作成し、そのスキーマを定義して、テーブルにデータを読み込みます。 このコードは、このデータテーブルを SQL Server にテーブル値パラメーターとして渡す SQLServerPreparedStatement を構成します。  

```java
/* Assumes connection is an active Connection object. */

// Create the source ResultSet object. Here SourceCategories is a table defined with the same schema as Categories table.
ResultSet sourceResultSet = connection.createStatement().executeQuery("SELECT * FROM SourceCategories");  

// Pass the source result set as a table-valued parameter using a prepared statement.  
SQLServerPreparedStatement pStmt =
        (SQLServerPreparedStatement) connection.prepareStatement(  
                "INSERT INTO dbo.Categories SELECT * FROM ?;");  
pStmt.setStructured(1, "dbo.CategoryTableType", sourceResultSet);  
pStmt.execute();  
```

> [!NOTE]  
> テーブル値パラメーターの設定に使用できる Api の完全な一覧については、次の「 **JDBC Driver 用のテーブル値パラメーター API** 」セクションを参照してください。  

## <a name="passing-a-table-valued-parameter-as-an-isqlserverdatarecord-object"></a>ISQLServerDataRecord オブジェクトとしてテーブル値パラメーターを渡す  

SQL Server 用の Microsoft JDBC Driver 6.0 以降では、テーブル値パラメーターを使用してデータをストリーミングする (ユーザーがどのように実装するかに応じて) 新しいインターフェイス ISQLServerDataRecord を使用できます。 次の例は、ISQLServerDataRecord インターフェイスを実装する方法と、それをテーブル値パラメーターとして渡す方法を示しています。 わかりやすくするために、次の例では、ハードコードされた値を含む1行だけをテーブル値パラメーターに渡します。 ユーザーは、テキストファイルなど、任意のソースから行をストリームするために、このインターフェイスを実装するのが理想的です。  

```java
class MyRecords implements ISQLServerDataRecord  
{  
    int currentRow = 0;  
    Object[] row = new Object[2];  
  
    MyRecords(){  
        // Constructor. This implementation has just one row.
        row[0] = new Integer(1);  
        row[1] = "categoryName1";  
    }  
  
    public int getColumnCount(){  
        // Return the total number of columns, for this example it is 2.  
        return 2;  
    }  
  
    public SQLServerMetaData getColumnMetaData(int columnIndex) {  
        // Return the column metadata.  
        if (1 == columnIndex)  
            return new SQLServerMetaData("CategoryID", java.sql.Types.INTEGER);  
        else  
            return new SQLServerMetaData("CategoryName", java.sql.Types.NVARCHAR);  
    }  
  
    public Object[] getRowData(){  
        // Return the columns in the current row as an array of objects. This implementation has just one row.  
        return row;
    }  
  
    public boolean next(){  
        // Move to the next row. This implementation has just one row, after processing the first row, return false.  
        currentRow++;  
        if (1 == currentRow)  
            return true;  
        else  
            return false;  
    }
}

// Following code demonstrates how to pass MyRecords object as a table-valued parameter.  
MyRecords sourceRecords = new MyRecords();  
SQLServerPreparedStatement pStmt =
        (SQLServerPreparedStatement) connection.prepareStatement(  
                "INSERT INTO dbo.Categories SELECT * FROM ?;");  
pStmt.setStructured(1, "dbo.CategoryTableType", sourceRecords);  
pStmt.execute();  
```

> [!NOTE]  
> テーブル値パラメーターの設定に使用できる Api の完全な一覧については、次の「 **JDBC driver 用のテーブル値パラメーター API** 」セクションを参照してください。

## <a name="table-valued-parameter-api-for-the-jdbc-driver"></a>JDBC ドライバー用のテーブル値パラメーター API

### <a name="sqlservermetadata"></a>SQLServerMetaData

このクラスは、列のメタデータを表します。 ISQLServerDataRecord インターフェイスでは、列のメタデータをテーブル値パラメーターに渡すために使用されます。 このクラスのメソッドは次のとおりです。  

| [オブジェクト名]                                                                                                                                                                             | [説明]                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| パブリック SQLServerMetaData (文字列 columnName、int sqlType、int precision、int scale、boolean useServerDefault、boolean isUniqueKey、SQLServerSortOrder 並べ替え、int sortOrdinal) | 指定された列名、sql 型、有効桁数、小数点以下桁数、およびサーバーの既定値を使用して、SQLServerMetaData の新しいインスタンスを初期化します。 この形式のコンストラクターは、テーブル値パラメーターで列が一意であるかどうか、列の並べ替え順序、および並べ替え列の序数を指定できるようにすることで、テーブル値パラメーターをサポートしています。 <br/><br/>useServerDefault-この列で既定のサーバー値を使用する必要があるかどうかを指定します。既定値は false です。<br>isUniqueKey-テーブル値パラメーターの列が一意であるかどうかを示します。既定値は false です。<br>順序付け-列の並べ替え順序を示します。既定値は SQLServerSortOrder です。<br>sortOrdinal-並べ替え列の序数を指定します。sortOrdinal は0から始まります。既定値は-1 です。 |
| public SQLServerMetaData (文字列 columnName, int sqlType)                                                                                                                        | 列名と sql 型を使用して、SQLServerMetaData の新しいインスタンスを初期化します。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| public SQLServerMetaData (文字列 columnName、int sqlType、int length)                                                                                                                        | 列名、sql 型、および長さ (文字列データの場合) を使用して、SQLServerMetaData の新しいインスタンスを初期化します。 長さは、長さが4000文字未満の文字列から大きな文字列を区別するために使用されます。 JDBC ドライバーのバージョン7.2 で導入されました。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| public SQLServerMetaData (文字列 columnName、int sqlType、int precision、int scale)                                                                                              | 列名、sql 型、有効桁数、および小数点以下桁数を使用して、SQLServerMetaData の新しいインスタンスを初期化します。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| パブリック SQLServerMetaData (SQLServerMetaData sqlServerMetaData)                                                                                                                    | 別の SQLServerMetaData オブジェクトから SQLServerMetaData の新しいインスタンスを初期化します。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| public String getColumName()                                                                                                                                                     | 列名を取得します。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| public int getSqlType()                                                                                                                                                          | Java sql 型を取得します。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| public int getPrecision()                                                                                                                                                        | 列に渡される型の有効桁数を取得します。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| public int getScale()                                                                                                                                                            | 列に渡された型の小数点以下桁数を取得します。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| public SQLServerSortOrder getSortOrder ()                                                                                                                                         | 並べ替え順序を取得します。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| public int getSortOrdinal()                                                                                                                                                      | 並べ替えの序数を取得します。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| public boolean isUniqueKey ()                                                                                                                                                     | 列が一意であるかどうかを返します。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| public boolean useServerDefault()                                                                                                                                                | 列が既定のサーバー値を使用するかどうかを返します。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
  
### <a name="sqlserversortorder"></a>SQLServerSortOrder

並べ替え順序を定義する列挙型。 指定できる値は、昇順、降順、および未指定です。
  
### <a name="sqlserverdatatable"></a>SQLServerDataTable

このクラスは、テーブル値パラメーターで使用されるメモリ内データテーブルを表します。 このクラスのメソッドは次のとおりです。  

| [オブジェクト名]                                                          | [説明]                                          |
| ------------------------------------------------------------- | ---------------------------------------------------- |
| パブリック SQLServerDataTable ()                                   | SQLServerDataTable の新しいインスタンスを初期化します。    |
| パブリック反復子 <\<エントリ整数、オブジェクト [] > > getiterator ()      | データテーブルの行の反復子を取得します。 |
| public void addColumnMetadata(String columnName, int sqlType) | 指定された列のメタデータを追加します。              |
| public void addColumnMetadata (SQLServerDataColumn 列)     | 指定された列のメタデータを追加します。              |
| public void addRow (オブジェクト...値                          | データテーブルに1行のデータを追加します。              |
| public Map\<Integer, SQLServerDataColumn> getColumnMetadata() | このデータテーブルの列メタデータを取得します。       |
| public void clear()                                           | このデータテーブルをクリアします。                              |

### <a name="sqlserverdatacolumn"></a>SQLServerDataColumn

このクラスは、SQLServerDataTable によって表されるメモリ内データテーブルの列を表します。 このクラスのメソッドは次のとおりです。  

| [オブジェクト名]                                                       | [説明]                                                                      |
| ---------------------------------------------------------- | -------------------------------------------------------------------------------- |
| public SQLServerDataColumn (文字列 columnName, int sqlType) | 列の名前と型を使用して、SQLServerDataColumn の新しいインスタンスを初期化します。 |
| public String getColumnName()                              | 列名を取得します。                                                       |
| public int getColumnType()                                 | 列の型を取得します。                                                       |

### <a name="isqlserverdatarecord"></a>ISQLServerDataRecord

このクラスは、ユーザーがテーブル値パラメーターにデータをストリームするために実装できるインターフェイスを表します。 このインターフェイスのメソッドは次のとおりです。  
  
| [オブジェクト名]                                                    | [説明]                                                                                             |
| ------------------------------------------------------- | ------------------------------------------------------------------------------------------------------- |
| public SQLServerMetaData getColumnMetaData (int 列); | 指定された列インデックスの列メタデータを取得します。                                               |
| public int getColumnCount();                            | 列の合計数を取得します。                                                                  |
| public Object[] getRowData();                           | オブジェクトの配列として、現在の行のデータを取得します。                                          |
| public boolean next();                                  | 次の行に移動します。 移動が成功し、次の行がある場合は True を返します。それ以外の場合は false を返します。 |

### <a name="sqlserverpreparedstatement"></a>SQLServerPreparedStatement

次のメソッドは、テーブル値パラメーターの引き渡しをサポートするために、このクラスに追加されました。  

| [オブジェクト名]                                                                                                    | [説明]                                                                                                                                                                                                                                                                                                |
| ------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| パブリック final void setStructured (int parameterIndex、String tvpName、SQLServerDataTable Tvpname)    | テーブル値パラメーターにデータテーブルを設定します。 parameterIndex はパラメーターインデックス、tvpName はテーブル値パラメーターの名前、Tvpname はソースデータテーブルオブジェクトです。                                                                                                          |
| パブリック final void setStructured (int parameterIndex、String tvpName、ResultSet tvpResultSet)             | 別のテーブルから取得した結果セットを使用して、テーブル値パラメーターを設定します。 parameterIndex はパラメーターインデックス、tvpName はテーブル値パラメーターの名前、tvpResultSet は変換元の結果セットオブジェクトです。                                                                               |
| パブリック final void setStructured (int parameterIndex, String tvpName, ISQLServerDataRecord tvpDataRecord) | ISQLServerDataRecord オブジェクトを使用して、テーブル値パラメーターを設定します。 ISQLServerDataRecord はデータをストリーミングするために使用され、ユーザーはその使用方法を決定します。 parameterIndex はパラメーターインデックス、tvpName はテーブル値パラメーターの名前、tvpDataRecord は ISQLServerDataRecord オブジェクトです。 |
  
### <a name="sqlservercallablestatement"></a>SQLServerCallableStatement

次のメソッドは、テーブル値パラメーターの引き渡しをサポートするために、このクラスに追加されました。  
  
| [オブジェクト名]                                                                                                        | [説明]                                                                                                                                                                                                                                                                                                                      |
| ----------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| パブリック final void setStructured (文字列 paratemeterName、文字列 tvpName、SQLServerDataTable Tvpname)    | データテーブルを使用してストアドプロシージャに渡されるテーブル値パラメーターを設定します。 paratemeterName はパラメーターの名前、tvpName は TVP 型の名前、Tvpname はデータテーブルオブジェクトです。                                                                                                                 |
| パブリック final void setStructured (文字列 paratemeterName、文字列 tvpName、ResultSet tvpResultSet)             | 別のテーブルから取得した結果セットを使用して、ストアドプロシージャに渡されるテーブル値パラメーターを設定します。 paratemeterName はパラメーターの名前、tvpName は TVP 型の名前、tvpResultSet はソース結果セットオブジェクトです。                                                                              |
| パブリック final void setStructured (文字列 paratemeterName、文字列 tvpName、ISQLServerDataRecord tvpDataRecord) | ISQLServerDataRecord オブジェクトを使用してストアドプロシージャに渡されるテーブル値パラメーターを設定します。 ISQLServerDataRecord はデータをストリーミングするために使用され、ユーザーはその使用方法を決定します。 paratemeterName はパラメーターの名前、tvpName は TVP 型の名前、tvpDataRecord は ISQLServerDataRecord オブジェクトです。 |

## <a name="see-also"></a>参照

[JDBC ドライバーの概要](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
