---
title: R ストアド プロシージャを作成する
description: SQL Server の sqlrutils R パッケージを使用して、R 言語コードを 1 つの関数にバンドルし、引数としてストアド プロシージャに渡せるようにします。
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: e0846442abce6dd598c6318e4ba7cf9e74685066
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727471"
---
# <a name="create-a-stored-procedure-using-sqlrutils"></a>sqlrutils を使用してストアド プロシージャを作成する
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

この記事では、T-SQL ストアド プロシージャとして実行する R コードを変換するための手順について説明します。 考えられる最良の結果を得るために、コードを少し変更し、すべての入力をパラメーター化できるようにする必要がある場合があります。

## <a name="bkmk_rewrite"></a>手順 1. R スクリプトを再生成する

最良の結果を得るには、R コードを再生成して、それを 1 つの関数としてカプセル化する必要があります。

関数で使用されるすべての変数を関数内で定義するか、入力パラメーターとして定義する必要があります。 この記事の[サンプル コード](#samples)を参照してください。

また、R 関数の入力パラメーターは SQL ストアド プロシージャの入力パラメーターになるため、ご自身の入出力が次の種類の要件に従っていることを確認する必要があります。

### <a name="inputs"></a>入力

入力パラメーターで使用できるデータ フレームは最大で 1 つです。

データ フレーム内のオブジェクトと、関数の他のすべての入力パラメーターは、次の R データ型でなければなりません。
- POSIXct
- NUMERIC
- character
- 整数 (integer)
- logical
- raw

入力の種類が上記の種類でない場合は、シリアル化し、 *raw*として関数に渡す必要があります。 その場合、関数に入力を逆シリアル化するコードを含める必要もあります。

### <a name="outputs"></a>出力

関数は次のいずれかを出力できます。

- サポートされているデータ型を含むデータ フレーム。 データ フレームのすべてのオブジェクトでは、サポートされているデータ型のいずれかを使用する必要があります。
- 最大で 1 つのデータ フレームを含む名前付きリスト。 リストのすべてのメンバーでは、サポートされるデータ型のいずれかを使用する必要があります。
- NULL (関数が結果を返さない場合)

## <a name="step-2-generate-required-objects"></a>手順 2. 必要なオブジェクトを生成する

ご自身の R コードのクリーンアップが完了し、1 つの関数として呼び出せるようになったら、**sqlrutils** パッケージの関数を使用して、実際にストアド プロシージャをビルドするコンストラクターに渡すことができる形式で入出力を準備します。

**sqlrutils** には、入力データと出力データのスキーマと型を定義する関数が用意されています。 また、必要な出力の種類に R オブジェクトを変換できる関数も含まれています。 コードで使用されているデータ型によっては、必要なオブジェクトを作成するために複数の関数を呼び出すことがあります。

### <a name="inputs"></a>入力

関数が入力を取る場合は、入力ごとに次の関数を呼び出します。

- `setInputData`。入力がデータ フレームの場合
- `setInputParameter`。その他すべての入力

関数を呼び出すたびに、R オブジェクトが作成されます。後でこのオブジェクトを引数として `StoredProcedure` に渡して、完全なストアド プロシージャを作成します。

### <a name="outputs"></a>出力

**sqlrutils** には、リストなどの R オブジェクトを、SQL Server で必要な data.frame に変換するための関数が複数用意されています。
関数でデータ フレームが直接出力された場合は、最初にリストにラップせずに、この手順を省略できます。
関数で NULL が返された場合も、この変換手順を省略できます。

リストを変換する場合、またはリストから特定の項目を取得する場合は、次の関数から選択します。

- `setOutputData`。リストから取得する変数がデータ フレームの場合
- `setOutputParameter`。リストのその他のメンバーすべて

関数を呼び出すたびに、R オブジェクトが作成されます。後でこのオブジェクトを引数として `StoredProcedure` に渡して、完全なストアド プロシージャを作成します。

## <a name="step-3-generate-the-stored-procedure"></a>手順 3. ストアド プロシージャを生成する

すべての入出力パラメーターの準備ができたら、`StoredProcedure` コンストラクターを呼び出します。

**使用方法**

`StoredProcedure (func, spName, ..., filePath = NULL ,dbName = NULL, connectionString = NULL, batchSeparator = "GO")`

たとえば、次のパラメーターを使用して、**sp_rsample** という名前のストアド プロシージャを作成するとします。

- 既存の関数 **foosql** を使用します。 関数は R 関数 **foo** の既存のコードに基づいていましたが、[こちらのセクション](#bkmk_rewrite)で説明されている要件に準拠するためにその関数を再生成し、更新された関数に **foosql** という名前を付けました。
- データ フレーム **queryinput** を入力として使用します
- R 変数名 **sqloutput** を使用して、データ フレームを出力として生成します
- T-SQL コードはファイルとして `C:\Temp` フォルダーに作成します。これは後から SQL Server Management Studio を使用して実行できます

```R
StoredProcedure (foosql, sp_rsample, queryinput, sqloutput, filePath = "C:\\Temp")
```

> [!NOTE]
> ファイルをファイル システムに書き込んでいるため、データベース接続を定義する引数は省略できます。

関数の出力は、SQL Server 2016 のインスタンスで実行できる (R Services が必要)、または SQL Server 2017 のインスタンスで実行できる (Machine Learning Services と R が必要) T-SQL ストアド プロシージャです。 

その他の例については、R 環境から `help(StoredProcedure)` を呼び出して、パッケージのヘルプを参照してください。

## <a name="step-4-register-and-run-the-stored-procedure"></a>手順 4. ストアド プロシージャを登録して実行する

ストアド プロシージャは 2 つの方法で実行できます。

- SQL Server 2016 インスタンスまたは SQL Server 2017 インスタンスへの接続がサポートされる任意のクライアントから T-SQL を使用する
- R 環境から

どちらの方法を使用する場合も、ストアド プロシージャを使用するデータベースで、そのストアド プロシージャを登録する必要があります。

### <a name="register-the-stored-procedure"></a>ストアド プロシージャを登録する

ストアド プロシージャは R を使用して登録できます。または、T-SQL で CREATE PROCEDURE ステートメントを実行できます。

- T-SQL の使用。  T-SQL に慣れている場合は、SQL Server Management Studio (または SQL DDL コマンドを実行できるその他のクライアント) を開き、`StoredProcedure` 関数によって準備されたコードを使用して CREATE PROCEDURE ステートメントを実行します。
- R の使用。まだ R 環境にいる場合は、**sqlrutils** で `registerStoredProcedure` 関数を使用して、ストアド プロシージャをデータベースに登録できます。

  たとえば、次の R 呼び出しを行うと、*sqlConnStr* で定義されているインスタンスとデータベースで、ストアド プロシージャ **sp_rsample** を登録できます。

  ```R
  registerStoredProcedure(sp_rsample, sqlConnStr)
  ```


> [!IMPORTANT]
> R と SQL のどちらを使用する場合でも、ステートメントは、新しいデータベース オブジェクトを作成する権限を持つアカウントを使用して実行する必要があります。

### <a name="run-using-sql"></a>SQL を使用して実行する

ストアド プロシージャの作成後、T-SQL がサポートされている任意のクライアントを使用して SQL データベースへの接続を開き、ストアド プロシージャで必要なパラメーターの値を渡します。

### <a name="run-using-r"></a>R を使用して実行する

SQL Server ではなく R コードからストアド プロシージャを実行するには、追加の準備が必要です。 たとえば、ストアド プロシージャで入力値が必要な場合は、関数を実行する前にその入力パラメーターを設定し、そのオブジェクトを R コードでストアド プロシージャに渡す必要があります。

準備された SQL ストアド プロシージャを呼び出す全体的なプロセスを次に示します。

1. 入力パラメーター オブジェクトのリストを取得するには、 `getInputParameters` を呼び出します。
2. `$query` を定義するか、入力パラメーターごとに `$value` を設定します。
3. `executeStoredProcedure` を使用して、設定した入力パラメーター オブジェクトのリストを渡し、R 開発環境からストアド プロシージャを実行します。

## <a name = "samples"></a>例

次の例は、SQL Server データベースからデータを取得し、そのデータに対して何らかの変換を実行して、別のデータベースに保存する R スクリプトの準備前と準備後のバージョンを示しています。

このシンプルな例は、R コードを並べ替えてストアド プロシージャへの変換を容易にする方法を示す目的でのみ使用されます。

### <a name="before-code-preparation"></a>コードを準備する前


```R
sqlConnFrom <- "Driver={ODBC Driver 13 for SQL Server};Server=MyServer01;Database=AirlineSrc;Trusted_Connection=Yes;"
  
sqlConnTo <- "Driver={ODBC Driver 13 for SQL Server};Server=MyServer01;Database=AirlineTest;Trusted_Connection=Yes;"
  
sqlQueryAirline <- "SELECT TOP 10000 ArrDelay, CRSDepTime, DayOfWeek FROM [AirlineDemoSmall]"
  
dsSqlFrom <- RxSqlServerData(sqlQuery = sqlQueryAirline, connectionString = sqlConnFrom)
  
dsSqlTo <- RxSqlServerData(table = "cleanData", connectionString = sqlConnTo)
  
xFunc <- function(data) {
    data$CRSDepHour <- as.integer(trunc(data$CRSDepTime))
    return(data)
    }
  
xVars <- c("CRSDepTime")
  
sqlCompute <- RxInSqlServer(numTasks = 4, connectionString = sqlConnTo)
  
rxOpen(dsSqlFrom)
rxOpen(dsSqlTo)
  
if (rxSqlServerTableExists("cleanData", connectionString = sqlConnTo))   {
    rxSqlServerDropTable("cleanData")}
  
rxDataStep(inData = dsSqlFrom, 
     outFile = dsSqlTo,
     transformFunc = xFunc,
     transformVars = xVars,
     overwrite = TRUE)
```

> [!NOTE]
> 
> *RxSqlServerData* を呼び出すのではなく、ODBC 接続を使用する場合は、データベースで操作を実行する前に、*rxOpen* を使用して接続を開く必要があります。


### <a name="after-code-preparation"></a>コードを準備した後

更新されたバージョンで、最初の行で関数名を定義します。 元の R ソリューションからの他のすべてのコードは、その関数の一部になります。

```R
myetl1function <- function() { 
   sqlConnFrom <- "Driver={ODBC Driver 13 for SQL Server};Server=MyServer01;Database=Airline01;Trusted_Connection=Yes;"
   sqlConnTo <- "Driver={ODBC Driver 13 for SQL Server};Server=MyServer02;Database=Airline02;Trusted_Connection=Yes;"
    
   sqlQueryAirline <- "SELECT TOP 10000 ArrDelay, CRSDepTime, DayOfWeek FROM [AirlineDemoSmall]"

   dsSqlFrom <- RxSqlServerData(sqlQuery = sqlQueryAirline, connectionString = sqlConnFrom)
  
   dsSqlTo <- RxSqlServerData(table = "cleanData", connectionString = sqlConnTo)
  
   xFunc <- function(data) {
     data$CRSDepHour <- as.integer(trunc(data$CRSDepTime))
     return(data)}
  
   xVars <- c("CRSDepTime")
  
   sqlCompute <- RxInSqlServer(numTasks = 4, connectionString = sqlConnTo)
  
   if (rxSqlServerTableExists("cleanData", connectionString = sqlConnTo)) {rxSqlServerDropTable("cleanData")}
  
   rxDataStep(inData = dsSqlFrom, 
        outFile = dsSqlTo,
        transformFunc = xFunc,
        transformVars = xVars,
        overwrite = TRUE)
   return(NULL)
}
```

> [!NOTE]
> 
> コードの一部として明示的に ODBC 接続を開く必要はありませんが、 **sqlrutils**を使用するには引き続き ODBC 接続が必要になります。

## <a name="see-also"></a>参照

[sqlrutils (SQL)](ref-r-sqlrutils.md)


