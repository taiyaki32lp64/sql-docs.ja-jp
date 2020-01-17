---
title: 'クイック スタート: R スクリプトの作成'
titleSuffix: SQL Server Machine Learning Services
description: SQL Server Machine Learning Services を使用して、SQL Server インスタンスで単純な R スクリプトを作成して実行します。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/04/2019
ms.topic: quickstart
author: garyericson
ms.author: garye
ms.reviewer: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 5a8e2779e930671faa9fa3ab94a7384ab1bdca83
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73726989"
---
# <a name="quickstart-create-and-run-simple-r-scripts-with-sql-server-machine-learning-services"></a>クイック スタート: SQL Server Machine Learning Services で簡単な R スクリプトを作成して実行する
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

このクイックスタートでは、[SQL Server Machine Learning Services](../what-is-sql-server-machine-learning.md) を使用して、一連の単純な R スクリプトを作成して実行します。 ストアド プロシージャ [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) で適切な形式の R スクリプトをラップし、SQL Server インスタンスでスクリプトを実行する方法について説明します。

## <a name="prerequisites"></a>Prerequisites

- このクイック スタートでは、R 言語がインストールされている [SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) を使用して SQL Server のインスタンスにアクセスする必要があります。

  あなたの SQL Server インスタンスは、Azure 仮想マシンまたはオンプレミスに配置できます。 外部スクリプト機能が既定で無効になっていることに注意してください。そのため、開始する前に、[外部スクリプトを有効にし](../install/sql-machine-learning-services-windows-install.md#bkmk_enableFeature)、**SQL Server Launchpad サービス**が実行されていることを確認する必要があります。

- また、R スクリプトを含む SQL クエリを実行するためのツールも必要です。 これらのスクリプトは、SQL Server インスタンスに接続し、T-SQL クエリまたはストアド プロシージャを実行できる限り、任意のデータベース管理ツールまたはクエリ ツールを使用して実行できます。 このクイック スタートでは、[SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms) を使用します。

## <a name="run-a-simple-script"></a>単純なスクリプトを実行する

R スクリプトを実行するには、これを引数としてシステム ストアド プロシージャ [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) に渡します。
このシステムのストアド プロシージャは、SQL Server のコンテキストで、R ランタイムを起動します。このランタイムは、R にデータを渡し、R ユーザー セッションを安全に管理し、結果をクライアントに返します。

次の手順では、このサンプル R スクリプトを SQL Server インスタンスで実行します。

```r
a <- 1
b <- 2
c <- a/b
d <- a*b
print(c(c, d))
```

1. **SQL Server Management Studio** を開き、SQL Server インスタンスに接続します。

1. 完全な R スクリプトを `sp_execute_external_script` ストアド プロシージャに渡します。

   このスクリプトは、`@script` 引数を通して渡されます。 `@script`引数内のすべては、有効な R コードである必要があります。

    ```sql
    EXECUTE sp_execute_external_script @language = N'R'
        , @script = N'
    a <- 1
    b <- 2
    c <- a/b
    d <- a*b
    print(c(c, d))
    '
    ```

1. 正しい結果が計算され、R `print`関数によって**メッセージ** ウィンドウに結果が返されます。

   次のように表示されます。

    **結果**

    ```text
    STDOUT message(s) from external script:
    0.5 2
    ```

## <a name="run-a-hello-world-script"></a>Hello World スクリプトを実行する

一般的なスクリプトの例では、文字列 "Hello World" が出力されるだけです。 次のコマンドを実行します。

```sql
EXECUTE sp_execute_external_script @language = N'R'
    , @script = N'OutputDataSet<-InputDataSet'
    , @input_data_1 = N'SELECT 1 AS hello'
WITH RESULT SETS(([Hello World] INT));
GO
```

`sp_execute_external_script`ストアド プロシージャへの入力は次のとおりです。

| | |
|-|-|
| @language | 呼び出す言語拡張機能 (この例では R) を定義します |
| @script | R ランタイムに渡されるコマンドを定義します Unicode テキストとして、この引数で R スクリプト全体を囲む必要があります。 **nvarchar** 型の変数にテキストを追加して、その変数を呼び出すこともできます |
| @input_data_1 | クエリによって返されるデータは R ランタイムに渡され、そこからデータがデータ フレームとして SQL Server に返されます。 |
|結果セットを含む | 句では、SQL Server に対して返されるデータ テーブルのスキーマを定義し、列名として "Hello World" を追加し、データ型に **int** を追加します |

このコマンドは、次のテキストを出力します。

| Hello World |
|-------------|
| 1 |

## <a name="use-inputs-and-outputs"></a>入力と出力を使用する

既定では、`sp_execute_external_script` は 1 つのデータセットを入力として受け入れます。通常は、有効な SQL クエリの形式で指定します。 次に、1 つの R データ フレームを出力として返します。

ここでは、`sp_execute_external_script` の既定の入力変数と出力変数を使用します。**InputDataSet** および **OutputDataSet**。

1. テスト データの小さなテーブルを作成します。

    ```sql
    CREATE TABLE RTestData (col1 INT NOT NULL)
    
    INSERT INTO RTestData
    VALUES (1);
    
    INSERT INTO RTestData
    VALUES (10);
    
    INSERT INTO RTestData
    VALUES (100);
    GO
    ```

1. テーブルのクエリを実行するには、`SELECT` ステートメントを使用します。
  
    ```sql
    SELECT *
    FROM RTestData
    ```

    **結果**

    ![RTestData テーブルの内容](./media/select-rtestdata.png)

1. 次の R スクリプトを実行します。 `SELECT` ステートメントを使用してテーブルからデータを取得し、それを R ランタイムを介して渡し、データをデータ フレームとして返します。 `WITH RESULT SETS` 句では、SQL に対して返されたデータ テーブルのスキーマを定義して、列名 *NewColName* を追加します。

    ```sql
    EXECUTE sp_execute_external_script @language = N'R'
        , @script = N'OutputDataSet <- InputDataSet;'
        , @input_data_1 = N'SELECT * FROM RTestData;'
    WITH RESULT SETS(([NewColName] INT NOT NULL));
    ```

    **結果**

    ![テーブルからデータを返す R スクリプトからの出力](./media/r-output-rtestdata.png)

1. 次に、入力変数と出力変数の名前を変更します。 既定の入力変数名と出力変数名は **InputDataSet** と **OutputDataSet** で、このスクリプトによって名前が **SQL_in** および **SQL_out** に変更されます。

    ```sql
    EXECUTE sp_execute_external_script @language = N'R'
        , @script = N' SQL_out <- SQL_in;'
        , @input_data_1 = N' SELECT 12 as Col;'
        , @input_data_1_name = N'SQL_in'
        , @output_data_1_name = N'SQL_out'
    WITH RESULT SETS(([NewColName] INT NOT NULL));
    ```

    R では大文字と小文字が区別されることに注意してください。 R スクリプトで使用される入力変数と出力変数は (**SQL_out**、**SQL_in**)、大文字と小文字を区別して、`@input_data_1_name` と `@output_data_1_name` で定義されている名前と一致する必要があります。

   > [!TIP]
   > パラメーターとして渡すことができるのは、1 つの入力データセットのみです。また、1 つのデータセットのみを返すことができます。 ただし、R コード内から他のデータセットを呼び出し、データセットに加えて他の型の出力を返すことができます。 また、OUTPUT キーワードを任意のパラメーターに追加して、その結果を受け取ることもできます。

1. 入力データを含まない R スクリプトを使用して値を生成することもできます (`@input_data_1` は空白に設定されます)。

   次のスクリプトは、 "hello" と "world" というテキストを出力します。

    ```sql
    EXECUTE sp_execute_external_script @language = N'R'
        , @script = N'
    mytextvariable <- c("hello", " ", "world");
    OutputDataSet <- as.data.frame(mytextvariable);
    '
        , @input_data_1 = N''
    WITH RESULT SETS(([Col1] CHAR(20) NOT NULL));
    ```

    **結果**

    ![入力として @script を使用したクエリ結果](./media/r-data-generated-output.png)

## <a name="check-r-version"></a>R バージョンの確認

SQL Server インスタンスにインストールされている R のバージョンを確認するには、次のスクリプトを実行します。

```sql
EXECUTE sp_execute_external_script @language = N'R'
    , @script = N'print(version)';
GO
```

R `print` 関数は、**メッセージ** ウィンドウにバージョンを返します。 次の出力例では、R バージョン 3.4.4 がインストールされていることがわかります。

**結果**

```text
STDOUT message(s) from external script:
                   _
platform       x86_64-w64-mingw32
arch           x86_64
os             mingw32
system         x86_64, mingw32
status
major          3
minor          4.4
year           2018
month          03
day            15
svn rev        74408
language       R
version.string R version 3.4.4 (2018-03-15)
nickname       Someone to Lean On
```

## <a name="list-r-packages"></a>R パッケージの一覧表示

Microsoft では、SQL Server インスタンスに SQL Server Machine Learning Services に R が予めインストールされたパッケージを多数提供しています。

バージョン、依存関係、ライセンス、ライブラリパスの情報など、インストールされている R パッケージの一覧を表示するには、次のスクリプトを実行します。

```SQL
EXEC sp_execute_external_script @language = N'R'
    , @script = N'
OutputDataSet <- data.frame(installed.packages()[,c("Package", "Version", "Depends", "License", "LibPath")]);'
WITH result sets((
            Package NVARCHAR(255)
            , Version NVARCHAR(100)
            , Depends NVARCHAR(4000)
            , License NVARCHAR(1000)
            , LibPath NVARCHAR(2000)
            ));
```

出力は R の `installed.packages()` からのものであり、結果セットとして返されます。

**結果**

![R のインストール済みパッケージ](./media/rsql-installed-packages.png) 

## <a name="next-steps"></a>次の手順

SQL Server Machine Learning Services で R を使用する場合のデータ構造の使用方法については、次のクイックスタートを参照してください。

> [!div class="nextstepaction"]
> [SQL Server Machine Learning Services での R を使用したデータ型とオブジェクトの処理](quickstart-r-data-types-and-objects.md)

SQL Server Machine Learning Services での R の使用に関する詳細は、次の記事を参照してください。

- [SQL Server Machine Learning Services を使用した高度な R 関数の作成](quickstart-r-functions.md)
- [SQL Server Machine Learning Services を使用して R で予測モデルを作成してスコア付けする](quickstart-r-train-score-model.md)
- [SQL Server Machine Learning Services (Python と R) とは](../what-is-sql-server-machine-learning.md)
