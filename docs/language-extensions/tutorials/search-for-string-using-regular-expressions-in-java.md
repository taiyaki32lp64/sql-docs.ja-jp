---
title: チュートリアル:Java での regex 文字列検索
description: このチュートリアルでは、SQL Server の言語拡張を使用し、正規表現 (regex) を使用して文字列を検索する Java コードを実行する方法について説明します。
author: dphansen
ms.author: davidph
ms.date: 11/05/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: language-extensions
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 9740e8c93fbac0d7727ba9922342df96d9190e10
ms.sourcegitcommit: baa40306cada09e480b4c5ddb44ee8524307a2ab
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/06/2019
ms.locfileid: "73658793"
---
# <a name="tutorial-search-for-a-string-using-regular-expressions-regex-in-java"></a>チュートリアル:Java での正規表現 (regex) を使用した文字列の検索
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

このチュートリアルでは、[SQL Server の言語拡張](../language-extensions-overview.md)を使用し、SQL Server から 2 つの列 (ID とテキスト) と、正規表現の入力パラメーターを受け取る Java クラスを作成する方法について説明します。 このクラスでは、SQL Server に 2 つの列 (ID とテキスト) を返します。

Java クラスに送信されるテキスト列内の指定のテキストが、指定した正規表現を満たしているかどうかをコードが確認し、元の ID と共にそのテキストが返されます。

このサンプル コードでは、テキストに "Java" または "java" の単語が含まれているかどうかを確認する正規表現を使用しています。

## <a name="prerequisites"></a>Prerequisites

+ [Windows](../install/install-sql-server-language-extensions-on-windows.md) または [Linux](https://docs.microsoft.com/sql/linux/sql-server-linux-setup-language-extensions) 用の SQL Server 2019 データベース エンジン インスタンスと拡張機能、および Java プログラミングの拡張機能。 詳細については、[SQL Server 2019 での言語拡張](../language-extensions-overview.md)に関する記事を参照してください。 コードの要件については、[SQL Server での Java の呼び出し方法](../how-to/call-java-from-sql.md)に関する記事を参照してください。

+ T-SQL 実行用の SQL Server Management Studio または Azure Data Studio。

+ Windows または Linux 用の Java SE Development Kit (JDK) 8 または JRE 8。

+ [Microsoft SQL Server 用 Microsoft Java Extensibility SDK](../how-to/extensibility-sdk-java-sql-server.md) の **mssql-java-lang-extension.jar** ファイル。

このチュートリアルでは、コマンド ラインから **javac** を使用してコンパイルするので十分です。

## <a name="create-sample-data"></a>サンプル データの作成

まず、新しいデータベースを作成し、**testdata** テーブルに **ID** と **text** 列を含めます。

```sql
CREATE DATABASE javatest
GO

USE javatest
GO

CREATE TABLE testdata (
    id int NOT NULL,
    "text" nvarchar(100) NOT NULL
)
GO

-- Insert data into test table
INSERT INTO testdata(id, "text") VALUES (1, 'This sentence contains java')
INSERT INTO testdata(id, "text") VALUES (2, 'This sentence does not')
INSERT INTO testdata(id, "text") VALUES (3, 'I love Java!')
GO
```

## <a name="create-the-main-class"></a>メイン クラスの作成

この手順では、**RegexSample.java** という名前のクラス ファイルを作成し、そのファイルに次の Java コードをコピーします。

このメイン クラスが SDK をインポートします。つまり、手順 1 でダウンロードした jar ファイルをこのクラスで検出できるようにする必要があります。

```java
package pkg;

import com.microsoft.sqlserver.javalangextension.PrimitiveDataset;
import com.microsoft.sqlserver.javalangextension.AbstractSqlServerExtensionExecutor;
import java.util.LinkedHashMap;
import java.util.LinkedList;
import java.util.ListIterator;
import java.util.regex.*;

public class RegexSample extends AbstractSqlServerExtensionExecutor {
    private Pattern expr;

    public RegexSample() {
        // Setup the expected extension version, and class to use for input and output dataset
        executorExtensionVersion = SQLSERVER_JAVA_LANG_EXTENSION_V1;
        executorInputDatasetClassName = PrimitiveDataset.class.getName();
        executorOutputDatasetClassName = PrimitiveDataset.class.getName();
    }
    
    public PrimitiveDataset execute(PrimitiveDataset input, LinkedHashMap<String, Object> params) {
        // Validate the input parameters and input column schema
        validateInput(input, params);

        int[] inIds = input.getIntColumn(0);
        String[] inValues = input.getStringColumn(1);
        int rowCount = inValues.length;

        String regexExpr = (String)params.get("regexExpr");
        expr = Pattern.compile(regexExpr);

        System.out.println("regex expression: " + regexExpr);

        // Lists to store the output data
        LinkedList<Integer> outIds = new LinkedList<Integer>();
        LinkedList<String> outValues = new LinkedList<String>();

        // Evaluate each row
        for(int i = 0; i < rowCount; i++) {
            if (check(inValues[i])) {
                outIds.add(inIds[i]);
                outValues.add(inValues[i]);
            }
        }

        int outputRowCount = outValues.size();

        int[] idOutputCol = new int[outputRowCount];
        String[] valueOutputCol = new String[outputRowCount];

        // Convert the list of output columns to arrays
        outValues.toArray(valueOutputCol);

        ListIterator<Integer> it = outIds.listIterator(0);
        int rowId = 0;

        System.out.println("Output data:");
        while (it.hasNext()) {
            idOutputCol[rowId] = it.next().intValue();

            System.out.println("ID: " + idOutputCol[rowId] + " Value: " + valueOutputCol[rowId]);
            rowId++;
        }

        // Construct the output dataset
        PrimitiveDataset output = new PrimitiveDataset();

        output.addColumnMetadata(0, "ID", java.sql.Types.INTEGER, 0, 0);
        output.addColumnMetadata(1, "Text", java.sql.Types.NVARCHAR, 0, 0);

        output.addIntColumn(0, idOutputCol, null);
        output.addStringColumn(1, valueOutputCol);

        return output;
    }

    private void validateInput(PrimitiveDataset input, LinkedHashMap<String, Object> params) {
        // Check for the regex expression input parameter
        if (params.get("regexExpr") == null) {
            throw new IllegalArgumentException("Input parameter 'regexExpr' is not found");
        }

        // The expected input schema should be at least 2 columns, (INTEGER, STRING)
        if (input.getColumnCount() < 2) {
            throw new IllegalArgumentException("Unexpected input schema, schema should be an (INTEGER, NVARCHAR or VARCHAR)");
        }

        // Check that the input column types are expected
        if (input.getColumnType(0) != java.sql.Types.INTEGER &&
                (input.getColumnType(1) != java.sql.Types.VARCHAR && input.getColumnType(1) == java.sql.Types.NVARCHAR )) {
            throw new IllegalArgumentException("Unexpected input schema, schema should be an (INTEGER, NVARCHAR or VARCHAR)");
        }
    }

    private boolean check(String text) {
        Matcher m = expr.matcher(text);

        return m.find();
    }
}
```

## <a name="compile-and-create-a-jar-file"></a>.jar ファイルのコンパイルおよび作成

ご自分のクラスと依存関係を `.jar` ファイルにパッケージ化します。 (Eclipse や IntelliJ などの) ほとんどの Java IDE は、プロジェクトのビルドまたはコンパイル時の `.jar` ファイルの生成をサポートしています。 `.jar` ファイルに **regex.jar** という名前を付けます。

Java IDE を使用していない場合は、手動で `.jar` ファイルを作成します。 詳細については、[クラス ファイルからの Java jar ファイルの作成方法](../how-to/create-a-java-jar-file-from-class-files.md)に関する記事を参照してください。

> [!NOTE]
> このチュートリアルではパッケージを使用します。 このクラスの上部にある `package pkg;` 行により、コンパイルされたコードが **pkg** という名前のサブ フォルダーに保存されるようになります。 IDE を使用している場合、コンパイルしたコードはこのフォルダーに自動的に保存されます。 このクラスの手動でのコンパイルに **javac** を使用した場合は、コンパイルしたコードを **pkg** フォルダーに配置する必要があります。

## <a name="create-external-language"></a>外部言語の作成

データベースには、外部言語を作成する必要があります。 外部言語とは、データベースで Java などの外部言語を使用する場合、使用する各データベースに作成する必要があるデータベース スコープのオブジェクトです。

### <a name="create-external-language-on-windows"></a>Windows での外部言語の作成

Windows を使用している場合は、次の手順に従って Java 用の外部言語を作成できます。

1. 拡張機能を含む .zip ファイルを作成します。

    Windows で SQL Server を設定する一環で、Java 拡張機能の **.zip** ファイルは `[SQL Server install path]\MSSQL\Binn\java-lang-extension.zip` の場所にインストールされます。 この zip ファイルに **javaextension.dll** が含まれます。

2. .zip ファイルから外部言語 Java ファイルを作成する方法は次のとおりです。

    ```sql
    CREATE EXTERNAL LANGUAGE Java
    FROM
    (CONTENT = N'[SQL Server install path]\MSSQL\Binn\java-lang-extension.zip', FILE_NAME = 'javaextension.dll',
    ENVIRONMENT_VARIABLES = N'{"JRE_HOME":"<path to JRE>"}' );
    GO
    ```

### <a name="create-external-language-on-linux"></a>Linux での外部言語の作成

設定の一環で、拡張機能 **.tar.gz** ファイルはこの `/opt/mssql-extensibility/lib/java-lang-extension.tar.gz` のパスの下に保存されます。

Linux で次の T-SQL ステートメントを実行し、外部言語の Java を作成します。

```sql
CREATE EXTERNAL LANGUAGE Java
FROM (CONTENT = N'/opt/mssql-extensibility/lib/java-lang-extension.tar.gz', file_name = 'javaextension.so',
ENVIRONMENT_VARIABLES = N'{"JRE_HOME":"<path to JRE>"}' );
GO
```

### <a name="permissions-to-execute-external-language"></a>外部言語を実行するアクセス許可

Java コードを実行するユーザーには、その特定の言語を外部スクリプトから実行する許可を付与する必要があります。

詳しくは、「[CREATE EXTERNAL LANGUAGE](https://docs.microsoft.com/sql/t-sql/statements/create-external-language-transact-sql)」をご覧ください。

## <a name="create-external-libraries"></a>外部ライブラリの作成

お使いの `.jar` ファイル用の外部ライブラリを作成するには、[CREATE EXTERNAL LIBRARY](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) を使用します。 SQL Server は `.jar` ファイルにアクセスできるため、**classpath** に特別なアクセス許可を設定する必要はありません。

このサンプルでは、2 つの外部ライブラリを作成します。 1 つは SDK 用で、もう 1 つは RegEx Java コード用です。

1. SDK jar ファイルの **mssql-java-lang-extension** は、Windows と Linux の両方で SQL Server 2019 の一部としてインストールされます。

    + Windows の既定のインストール パス: **[instance installation home directory]\MSSQL\Binn\mssql-java-lang-extension.jar**

    + Linux の既定のインストール パス: **/opt/mssql/lib/mssql-java-lang-extension.jar**

    このコードもオープン ソースであり、[SQL Server の言語拡張機能 GitHub リポジトリ](https://github.com/microsoft/sql-server-language-extensions)に関するページにあります。 詳細については、「[Microsoft SQL Server 向けの Java 用 Microsoft Extensibility SDK](../how-to/extensibility-sdk-java-sql-server.md)」を参照してください。

2. SDK 用の外部ライブラリを作成します。

    ```sql
    CREATE EXTERNAL LIBRARY sdk
    FROM (CONTENT = '<OS specific path from above>/mssql-java-lang-extension.jar')
    WITH (LANGUAGE = 'Java');
    GO
    ```

3. RegEx コード用の外部ライブラリを作成します。

    ```sql
    CREATE EXTERNAL LIBRARY regex
    FROM (CONTENT = '<path>/regex.jar')
    WITH (LANGUAGE = 'Java');
    GO
    ```

## <a name="set-permissions"></a>アクセス許可を設定する

> [!NOTE]
> 前の手順で外部ライブラリを使用している場合は、この手順を省略してください。 外部ライブラリは、ご自分の `.jar` ファイルから作成することをお勧めします。

外部ライブラリを使用しない場合は、必要なアクセス許可を設定する必要があります。 スクリプトの実行は、プロセス ID がお使いのコードにアクセスできる場合にのみ成功します。 アクセス許可の設定の詳細については、[インストール ガイド](../install/install-sql-server-language-extensions-on-windows.md)を参照してください。

### <a name="on-linux"></a>Linux の場合

**mssql_satellite** ユーザーに、クラス パスに対する読み取り/実行アクセス許可を付与します。

### <a name="on-windows"></a>Windows の場合

コンパイルされたご自分の Java コードを含むフォルダー上で **SQLRUserGroup** と、**All application packages** SID に対して "読み取りと実行" アクセス許可を付与します。

アクセス許可は、ルートの親から最後のサブ フォルダーまで、ツリー全体で必要です。

1. フォルダーを右クリックし (`C:\myJavaCode` など)、 **[プロパティ]**  >  **[セキュリティ]** の順に選択します。
2. **[編集]** をクリックします。
3. **[追加]** をクリックします。
4. **[ユーザー、コンピューター、サービス アカウントまたはグループの選択]** で次を実行します。
   1. **[オブジェクトの種類]** をクリックし、 *[Built-in security principles]* \(組み込みのセキュリティ プリンシパル\) と *[グループ]* が選択されていることを確認します。
   2. **[場所]** をクリックして、一覧の最上部にあるローカル コンピューター名を選択します。
5. 「**SQLRUserGroup**」と入力し、名前を確認し、[OK] をクリックしてグループを追加します。
6. 「**ALL APPLICATION PACKAGES**」と入力し、名前を確認し、[OK] をクリックして追加します。 
    名前が解決されない場合は、[場所] の手順を再実行します。 SID は、お使いのコンピューターに対してローカルです。

両方のセキュリティ ID に、フォルダーおよび **pkg** サブ フォルダーに対する**読み取りと実行**のアクセス許可があることを確認します。

<a name="call-method"></a>

## <a name="call-the-java-class"></a>Java クラスの呼び出し

SQL Server から Java コードを呼び出す、`sp_execute_external_script` を呼び出すストアド プロシージャを作成します。 呼び出す `package.class` を、**script** パラメーターに定義します。 次のコードでは、クラスは **pkg** という名前のパッケージと、**RegexSample.java** というクラス ファイルに属しています。

> [!NOTE]
> このコードでは、どのメソッドを呼び出すか定義されていません。 既定では、**execute** メソッドが呼び出されます。 つまり、SQL Server からクラスを呼び出したい場合には、SDK インターフェイスに従い、メソッドをお使いの Java クラスに実装して実行する必要があります。

このストアド プロシージャは、入力クエリ (入力データセット) と正規表現を受け取り、指定された正規表現を満たす行を返します。 これでは、テキストに **Java** または **java** の単語が含まれているかどうかを確認する正規表現 `[Jj]ava` を使用しています。

```sql
CREATE OR ALTER PROCEDURE [dbo].[java_regex] @expr nvarchar(200), @query nvarchar(400)
AS
BEGIN
--Call the Java program by giving the package.className in @script
--The method invoked in the Java code is always the "execute" method
EXEC sp_execute_external_script
  @language = N'Java'
, @script = N'pkg.RegexSample'
, @input_data_1 = @query
, @params = N'@regexExpr nvarchar(200)'
, @regexExpr = @expr
with result sets ((ID int, text nvarchar(100)));
END
GO

--Now execute the above stored procedure and provide the regular expression and an input query
EXECUTE [dbo].[java_regex] N'[Jj]ava', N'SELECT id, text FROM testdata'
GO
```

### <a name="results"></a>[結果]

呼び出しを実行すると、2 つの行の結果セットが返されるはずです。

![Java サンプルの結果](../media/java/java-sample-results.png "サンプルの結果")

### <a name="if-you-get-an-error"></a>エラーが表示された場合

+ クラスをコンパイルするときに、**pkg** サブ フォルダーには、3 つのクラスのすべてのコンパイル済みコードが含まれている必要があります。

+ 外部ライブラリを使用していない場合は、外部プロセスを実行しているセキュリティ ID にご自分のコードに対する読み取りおよび実行のアクセス許可があることを確かめるために、**ルート**から **pkg** サブ フォルダーまでの*各*フォルダーのアクセス許可を確認します。

## <a name="next-steps"></a>次の手順

+ [SQL Server で Java を呼び出す方法](../how-to/call-java-from-sql.md)
+ [SQL Server の Java 拡張機能](../language-extensions-overview.md)
+ [Java および SQL Server のデータ型](../how-to/java-to-sql-data-types.md)
