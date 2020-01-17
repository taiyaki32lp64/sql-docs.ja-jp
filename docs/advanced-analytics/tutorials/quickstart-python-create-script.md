---
title: 'クイック スタート: Python スクリプトを作成する'
titleSuffix: SQL Server Machine Learning Services
description: SQL Server Machine Learning Services を使用して SQL Server インスタンスでの単純な Python スクリプトを作成して実行します。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/04/2019
ms.topic: quickstart
author: garyericson
ms.author: garye
ms.reviewer: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 8409eaf8129d7c8eb2eecd5a1157a17444341734
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727024"
---
# <a name="quickstart-create-and-run-simple-python-scripts-with-sql-server-machine-learning-services"></a>クイック スタート: SQL Server Machine Learning Services を使用して単純な Python スクリプトを作成して実行する
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

このクイックスタートでは、[SQL Server Machine Learning Services](../what-is-sql-server-machine-learning.md) を使用して、一連の単純な Python スクリプトを作成して実行します。 ストアド プロシージャ [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) で適切な形式の Python スクリプトをラップし、SQL Server インスタンスでスクリプトを実行する方法について説明します。

## <a name="prerequisites"></a>Prerequisites

- このクイック スタートでは、Python 言語がインストールされている [SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) を使用して SQL Server のインスタンスにアクセスする必要があります。

- また、Python スクリプトを含む SQL クエリを実行するためのツールも必要です。 これらのスクリプトは、SQL Server インスタンスに接続し、T-SQL クエリまたはストアド プロシージャを実行できる限り、任意のデータベース管理ツールまたはクエリ ツールを使用して実行できます。 このクイック スタートでは、[SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms) を使用します。

## <a name="run-a-simple-script"></a>単純なスクリプトを実行する

Python スクリプトを実行するには、これを引数としてシステム ストアド プロシージャ [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) に渡します。
このシステム ストアド プロシージャを使用して、SQL Server のコンテキストで Python ランタイムを起動し、データを Python に渡し、Python ユーザー セッションを安全に管理し、何らかの結果をクライアントに返します。

次の手順では、このサンプル Python スクリプトを SQL Server インスタンスで実行します。

```python
a = 1
b = 2
c = a/b
d = a*b
print(c, d)
```

1. SQL Server インスタンスに接続された **SQL Server Management Studio** で新しいクエリ ウィンドウを開きます。

1. 完全な Python スクリプトを `sp_execute_external_script` ストアド プロシージャに渡します。

   このスクリプトは、`@script` 引数を通して渡されます。 `@script` 引数内のすべては、有効な Python コードである必要があります。

    ```sql
    EXECUTE sp_execute_external_script @language = N'Python'
        , @script = N'
    a = 1
    b = 2
    c = a/b
    d = a*b
    print(c, d)
    '
    ```

1. 正しい結果が計算され、Python `print` 関数によって **Messages** ウィンドウに結果が返されます。

   次のように表示されます。

    **結果**

    ```text
    STDOUT message(s) from external script:
    0.5 2
    ```

## <a name="run-a-hello-world-script"></a>Hello World スクリプトを実行する

一般的なスクリプトの例では、文字列 "Hello World" を出力するだけです。 次のコマンドを実行します。

```sql
EXECUTE sp_execute_external_script @language = N'Python'
    , @script = N'OutputDataSet = InputDataSet'
    , @input_data_1 = N'SELECT 1 AS hello'
WITH RESULT SETS(([Hello World] INT));
GO
```

`sp_execute_external_script` ストアド プロシージャへの入力は次のとおりです。

| | |
|-|-|
| @language | 呼び出す言語拡張機能 (この例では Python) を定義します |
| @script | Python ランタイムに渡されるコマンドを定義します<br>Python 全体は、Unicode テキストとして、この引数で囲まれている必要があります。 **nvarchar** 型の変数にテキストを追加して、その変数を呼び出すこともできます |
| @input_data_1 | クエリによって返されるデータは、Python ランタイムに渡され、そこからデータがデータ フレームとして SQL Server に返されます |
|WITH RESULT SETS | 句では、SQL Server に対して返されるデータ テーブルのスキーマを定義します。この場合は、列名として "Hello World" を追加し、データ型に **int** を追加します |

このコマンドは、次のテキストを出力します。

| Hello World |
|-------------|
| 1 |

## <a name="use-inputs-and-outputs"></a>入力と出力を使用する

既定では、`sp_execute_external_script` は 1 つのデータセットを入力として受け入れます。通常は、有効な SQL クエリの形式で指定します。 次に、1 つの Python データ フレームを出力として返します。

ここでは、`sp_execute_external_script` の既定の入力変数と出力変数を使用します。**InputDataSet** および **OutputDataSet**。

1. テスト データの小さなテーブルを作成します。

    ```sql
    CREATE TABLE PythonTestData (col1 INT NOT NULL)
    
    INSERT INTO PythonTestData
    VALUES (1);
    
    INSERT INTO PythonTestData
    VALUES (10);
    
    INSERT INTO PythonTestData
    VALUES (100);
    GO
    ```

1. テーブルのクエリを実行するには、`SELECT` ステートメントを使用します。
  
    ```sql
    SELECT *
    FROM PythonTestData
    ```

    **結果**

    ![PythonTestData テーブルの内容](./media/select-pythontestdata.png)

1. 次の Python スクリプトを実行します。 `SELECT` ステートメントを使用してテーブルからデータを取得し、それを Python ランタイムを介して渡し、データをデータ フレームとして返します。 `WITH RESULT SETS` 句では、SQL に対して返されたデータ テーブルのスキーマを定義して、列名 *NewColName* を追加します。

    ```sql
    EXECUTE sp_execute_external_script @language = N'Python'
        , @script = N'OutputDataSet = InputDataSet;'
        , @input_data_1 = N'SELECT * FROM PythonTestData;'
    WITH RESULT SETS(([NewColName] INT NOT NULL));
    ```

    **結果**

    ![テーブルからデータを返す Python スクリプトからの出力](./media/python-output-pythontestdata.png)

1. 次に、入力変数と出力変数の名前を変更します。 既定の入力変数名と出力変数名は **InputDataSet** と **OutputDataSet** で、次のスクリプトによって名前が **SQL_in** および **SQL_out** に変更されます。

    ```sql
    EXECUTE sp_execute_external_script @language = N'Python'
        , @script = N'SQL_out = SQL_in;'
        , @input_data_1 = N'SELECT 12 as Col;'
        , @input_data_1_name  = N'SQL_in'
        , @output_data_1_name = N'SQL_out'
    WITH RESULT SETS(([NewColName] INT NOT NULL));
    ```

    Python では大文字と小文字が区別されることに注意してください。 Python スクリプトで使用される入力変数と出力変数は (**SQL_out**、**SQL_in**)、大文字と小文字を区別して、`@input_data_1_name` と `@output_data_1_name`で定義されている名前と一致する必要があります。

   > [!TIP]
   > パラメーターとして渡すことができるのは、1 つの入力データセットのみです。また、1 つのデータセットのみを返すことができます。 ただし、Python コード内から他のデータセットを呼び出し、データセットに加えて他の型の出力を返すことができます。 また、OUTPUT キーワードを任意のパラメーターに追加して、その結果を受け取ることもできます。

1. 入力データを含まない Python スクリプトを使用して値を生成することもできます (`@input_data_1` は空白に設定されます)。

   次のスクリプトは、"hello" と "world" というテキストを出力します。

   ```sql
   EXECUTE sp_execute_external_script @language = N'Python'
       , @script = N'
   import pandas as pd
   mytextvariable = pandas.Series(["hello", " ", "world"]);
   OutputDataSet = pd.DataFrame(mytextvariable);
   '
       , @input_data_1 = N''
   WITH RESULT SETS(([Col1] CHAR(20) NOT NULL));
   ```

   **結果**

   ![入力として @script を使用したクエリ結果](./media/python-data-generated-output.png)

> [!NOTE]
> Python では、先頭のスペースを使用してステートメントをグループ化します。 そのため、前述のスクリプトのように、埋め込まれた Python スクリプトが複数の行にまたがる場合は、SQL コマンドに合わせるために Python コマンドにインデントを設定しようとしないでください。 たとえば、次のスクリプトでは次のエラーが生成されます。

  ```text
  EXECUTE sp_execute_external_script @language = N'Python'
      , @script = N'
      import pandas as pd
      mytextvariable = pandas.Series(["hello", " ", "world"]);
      OutputDataSet = pd.DataFrame(mytextvariable);
      '
      , @input_data_1 = N''
  WITH RESULT SETS(([Col1] CHAR(20) NOT NULL));
  ```

## <a name="check-python-version"></a>Python バージョンの確認

SQL Server インスタンスにインストールされている Python のバージョンを確認するには、次のスクリプトを実行します。

```sql
EXECUTE sp_execute_external_script @language = N'Python'
    , @script = N'
import sys
print(sys.version)
'
GO
```

Python `print` 関数は、**Messages** ウィンドウにバージョンを返します。 次の出力例では、この場合、Python バージョン 3.5.2 がインストールされていることが分かります。

**結果**

```text
STDOUT message(s) from external script: 
3.5.2 |Continuum Analytics, Inc.| (default, Jul  5 2016, 11:41:13) [MSC v.1900 64 bit (AMD64)]
```

## <a name="list-python-packages"></a>Python パッケージを一覧表示します

Microsoft では、SQL Server インスタンスに SQL Server Machine Learning Services と共にプレインストールされた多数の Python パッケージを提供しています。

バージョンなど、インストールされている Python パッケージの一覧を表示するには、次のスクリプトを実行します。

```SQL
EXECUTE sp_execute_external_script @language = N'Python'
    , @script = N'
import pip
for i in pip.get_installed_distributions():
    print(i)
'
GO
```

出力は Python の `pip.get_installed_distributions()` からのものであり、`STDOUT` メッセージとして返されます。

**結果**

```text
STDOUT message(s) from external script:
xlwt 1.2.0
XlsxWriter 0.9.6
xlrd 1.0.0
win-unicode-console 0.5
widgetsnbextension 2.0.0
wheel 0.29.0
Werkzeug 0.12.1
wcwidth 0.1.7
unicodecsv 0.14.1
traitlets 4.3.2
tornado 4.4.2
toolz 0.8.2
. . .
```

## <a name="next-steps"></a>次の手順

SQL Server Machine Learning Services で Python を使用する場合のデータ構造の使用方法については、次のクイックスタートを参照してください。

> [!div class="nextstepaction"]
> [SQL Server Machine Learning Services での Python を使用したデータ型とオブジェクトの処理](quickstart-python-data-structures.md)

SQL Server Machine Learning Services での Python の使用に関する詳細については、次の記事を参照してください。

- [SQL Server Machine Learning Services を使用した高度な Python 関数を作成する](quickstart-python-functions.md)
- [SQL Server Machine Learning Services を使用して Python で予測モデルを作成してスコア付けする](quickstart-python-train-score-model.md)
- [SQL Server Machine Learning Services とは (Python と R)](../what-is-sql-server-machine-learning.md)
