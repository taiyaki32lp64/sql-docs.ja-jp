---
title: rxDataStep を使用したテーブルの作成
description: このチュートリアルは、SQL Server で R 言語を使用してSQL Server テーブルを作成する方法について詳しく説明しています。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: f4ac51fc1affb4128abab017eb00cba4b56960fa
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727249"
---
# <a name="create-new-sql-server-table-using-rxdatastep-sql-server-and-revoscaler-tutorial"></a>RxDataStep を使用して新しい SQL Server テーブルを作成する (SQL Server と RevoScaleR のチュートリアル)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

このレッスンは、SQL Server で [RevoScaleR 関数](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)を使用する方法についての [RevoScaleR チュートリアル](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)の一部です。

このレッスンでは、インメモリ データ フレーム、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] コンテキスト、およびローカル ファイルの間でデータを移動する方法を学習します。

> [!NOTE]
> このレッスンでは、別のデータセットを使用します。 航空便遅延データセットは、機械学習実験に広く使用されている公開データセットです。 この例に使用するデータ ファイルは、その他の製品サンプルと同じディレクトリにあります。

## <a name="load-data-from-a-local-xdf-file"></a>ローカル XDF ファイルからのデータの読み込み

このチュートリアルの前半では、**RxTextData** 関数を使用してデータをテキスト ファイルから R にインポートし、**RxDataStep** 関数を使用してデータを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に移動しました。

このレッスンでは、別のアプローチを採用し、[XDF 形式](https://en.wikipedia.org/wiki/Extensible_Data_Format)で保存されたファイルのデータを使用します。 XDF ファイルを使用するデータに簡単な変換を実行した後に、変換後のデータを新しい [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブルに保存します。

**XDF とは**

XDF 形式は、高次元データ用に開発された XML 標準であり、[Machine Learning Server](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-xdf) によって使用されるネイティブ ファイル形式です。 XDF は、R インターフェイスを使用したバイナリ ファイル形式です。行と列の処理と分析を最適化しています。  XDF 形式は、データの移動や、分析に有用なデータのサブセットを格納するために使用できます。

1. 計算コンテキストをローカル ワークステーションに設定します。 **この手順には、DDL の権限が必要です。**

    ```R
    rxSetComputeContext("local")
    ```
  
2. **RxXdfData** 関数を使用して新しいデータ ソース オブジェクトを定義します。 XDF データ ソースを定義するには、データ ファイルへのパスを指定します。  

    テキスト変数を使用して、ファイルへのパスを指定できます。 ただし、この場合は便利なショートカットがあります。これは、**rxGetOption** 関数を使用し、サンプル データ ディレクトリからファイル (AirlineDemoSmall.xdf) を取得するものです。
  
    ```R
    xdfAirDemo <- RxXdfData(file.path(rxGetOption("sampleDataDir"),  "AirlineDemoSmall.xdf"))
    ```

3. インメモリ データに対して [rxGetVarInfo](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxgetvarinfoxdf) を呼び出して、データセットの概要を表示します。
  
    ```R
    rxGetVarInfo(xdfAirDemo)
    ```

**結果**

```R
Var 1: ArrDelay, Type: integer, Low/High: (-86, 1490)
Var 2: CRSDepTime, Type: numeric, Storage: float32, Low/High: (0.0167, 23.9833)
Var 3: DayOfWeek 7 factor levels: Monday Tuesday Wednesday Thursday Friday Saturday Sunday
```

> [!NOTE]
> 
> ご覧のように、データを XDF ファイルに読み込むために他の関数を呼び出す必要がなく、データに対して **rxGetVarInfo** をすぐに呼び出すことができます。 これは、XDF が **RevoScaleR** の既定の中間格納方法であるためです。 XDF ファイルに加えて、**rxGetVarInfo** 関数は、複数のソースの種類をサポートするようになりました。

## <a name="move-contents-to-sql-server"></a>コンテンツの SQL Server への移動

ローカル R セッションで XDF データ ソースが作成されたので、このデータをデータベース テーブルに移動し、*DayOfWeek* を 1 ~ 7 の値を持つ整数として格納できるようになりました。

1. データを格納するテーブルとリモート サーバーへの接続を指定して、SQL Server データ ソース オブジェクトを定義します。
  
    ```R
    sqlServerAirDemo <- RxSqlServerData(table = "AirDemoSmallTest", connectionString = sqlConnString)
    ```
  
2. 念のため、同じ名前のテーブルが既に存在しないか確認する手順が含め、存在する場合はそのテーブルを削除します。 同じ名前のテーブルが既に存在する場合、新しいテーブルを作成できません。
  
    ```R
    if (rxSqlServerTableExists("AirDemoSmallTest",  connectionString = sqlConnString))  rxSqlServerDropTable("AirDemoSmallTest",  connectionString = sqlConnString)
    ```
  
3. **rxDataStep** を使用して、テーブルにデータを読み込みます。 この関数は、既に定義されている 2 つのデータ ソースの間でデータを移動し、必要に応じて途中でデータを変換できます。
  
    ```R
    rxDataStep(inData = xdfAirDemo, outFile = sqlServerAirDemo,
        transforms = list( DayOfWeek = as.integer(DayOfWeek),
        rowNum = .rxStartRow : (.rxStartRow + .rxNumRows - 1) ),
        overwrite = TRUE )
    ```
  
    これは非常に大きなテーブルであるため、次のような最終的なステータス メッセージが表示されるまで待ちます。*読み取られる行:200000、処理された行数の合計:600000*。
     
## <a name="load-data-from-a-sql-table"></a>SQL テーブルからのデータの読み込み

テーブルにデータが存在する場合は、単純な SQL クエリを使用してデータを読み込むことができます。 

1. SQL Server の新規データベースを作成します。 この入力は、先ほど作成してデータと共に読み込まれた新しいテーブルに対するクエリです。 この定義では、*colInfo* 引数を **RxSqlServerData** に使用して、*DayOfWeek* 列の因子レベルを追加します。
  
    ```R
    sqlServerAirDemo2 <- RxSqlServerData(
        sqlQuery = "SELECT * FROM AirDemoSmallTest",
        connectionString = sqlConnString,
        rowsPerRead = 50000,
        colInfo = list(DayOfWeek = list(type = "factor",  levels = as.character(1:7))))
    ```
  
2. クエリ内のデータの概要を確認するには、再度 **rxSummary** を呼び出します。
  
    ```R
    rxSummary(~., data = sqlServerAirDemo2)
    ```

## <a name="next-steps"></a>次の手順

> [!div class="nextstepaction"]
> [rxDataStep を使用したチャンク分析の実行](../../advanced-analytics/tutorials/deepdive-perform-chunking-analysis-using-rxdatastep.md)