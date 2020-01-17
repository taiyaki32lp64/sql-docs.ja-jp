---
title: RevoScaleR でのチャンク分析
description: このチュートリアルは、SQL Server で R 言語を使用して分散された分析のデータをチャックに分割する方法について詳しく説明しています。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 8c7aa853f44a04e55802012e81e59a15d2b5282b
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727237"
---
# <a name="perform-chunking-analysis-using-rxdatastep-sql-server-and-revoscaler-tutorial"></a>RxDataStep を使用したチャンク分析の実行 (SQL Server と RevoScaleR のチュートリアル)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

このレッスンは、SQL Server で [RevoScaleR 関数](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)を使用する方法についての [RevoScaleR チュートリアル](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)の一部です。

このレッスンでは、**rxDataStep** 関数を利用して、従来の R のように、データセット全体をメモリに読み込み、一度に処理することを要求せず、データをチャンク単位で処理します。**rxDataStep** 関数は、データをチャンク単位で読み込み、データの各チャンクに R 関数を順々に適用し、各チャンクをまとめた結果を共通の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ ソースに書き込みます。 すべてのデータが読み込まれると、結果が結合されます。

> [!TIP]
> このレッスンでは、R で **table** 関数を使用して、コンティンジェンシー テーブルを計算します。この例は、説明のみを目的としています。 
> 
> 実世界のデータセットを表にする場合、**RevoScaleR** の **rxCrossTabs** 関数または **rxCube** 関数の使用が推奨されます。この種類の操作のために最適です。

## <a name="partition-data-by-values"></a>値によるデータのパーティション分割

1. 最初に、データの格チャンクで R **table** 関数を呼び出すカスタム R 関数を作成し、新しい関数に **ProcessChunk** という名前を付けます。
  
    ```R
    ProcessChunk <- function( dataList) {
    # Convert the input list to a data frame and compute contingency table
    chunkTable <- table(as.data.frame(dataList))
  
    # Convert table output to a data frame with a single row
    varNames <- names(chunkTable)
    varValues <- as.vector(chunkTable)
    dim(varValues) <- c(1, length(varNames))
    chunkDF <- as.data.frame(varValues)
    names(chunkDF) <- varNames
  
    # Return the data frame, which has a single row
    return( chunkDF )
    }
    ```

2. コンピューティング コンテキストをサーバーに設定します。
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```
  
3. 処理しているデータを保持する SQL Server データ ソースを定義します。 最初に SQL クエリを変数に代入します。 次に、新しい SQL Server データ ソースの *sqlQuery* 引数でその変数を使用します。
  
    ```R
    dayQuery <-  "SELECT DayOfWeek FROM AirDemoSmallTest"
    inDataSource <- RxSqlServerData(sqlQuery = dayQuery,
        connectionString = sqlConnString,
        rowsPerRead = 50000,
        colInfo = list(DayOfWeek = list(type = "factor",
            levels = as.character(1:7))))
    ```

4. 必要に応じて、このデータ ソースで **rxGetVarInfo** を実行できます。 この時点で、1 つの列が含まれます。*Var 1:DayOfWeek, Type: factor, no factor levels available*
     
5. この因子変数をソース データに適用する前に、中間結果を保持するための別のテーブルを作成します。 もう一度 **RxSqlServerData** 関数を使用してデータを定義し、同じ名前の既存テーブルを削除したことを確認します。
  
    ```R
    iroDataSource = RxSqlServerData(table = "iroResults",   connectionString = sqlConnString)
    # Check whether the table already exists.
    if (rxSqlServerTableExists(table = "iroResults",  connectionString = sqlConnString))  { rxSqlServerDropTable( table = "iroResults", connectionString = sqlConnString) }
    ```
  
7.  カスタム関数の **ProcessChunk** を呼び出し、読み込まれると同時にデータを変換します。そのとき、データを *rxDataStep* 関数の **transformFunc** 引数として使用します。
  
    ```R
    rxDataStep( inData = inDataSource, outFile = iroDataSource, transformFunc = ProcessChunk, overwrite = TRUE)
    ```
  
8.  **ProcessChunk** の中間結果を表示するには、**rxImport** の結果を変数に代入し、結果をコンソールに出力します。
  
    ```R
    iroResults <- rxImport(iroDataSource)
    iroResults
    ```

    **結果の一部**

    |      |    1  |   2   |  3   |  4   |  5  |   6   |  7 |
    | --- | ---  | --- | ---  |  ---  | ---  | ---  | --- |
    | 1 | 8228 | 8924 | 6916 | 6932 | 6944 | 5602 | 6454 |
    | 2  | 8321  | 5351 | 7329 | 7411 | 7409 | 6487 | 7692 |

9. チャンク全体の最終結果を計算するには、列を合計し、結果をコンソールに表示します。

    ```R
    finalResults <- colSums(iroResults)
    finalResults
    ```

    **結果**

    1  |   2  |   3  |   4  |   5  |   6  |   7
    ---  |   ---  |   ---  |   ---  |   ---  |   ---  |   ---
    97975 | 77725 | 78875 | 81304 | 82987 | 86159 | 94975 

10. 中間結果テーブルを削除するには、**rxSqlServerDropTable** を呼び出します。
  
    ```R
    rxSqlServerDropTable( table = "iroResults", connectionString = sqlConnString)
    ```

## <a name="next-steps"></a>次の手順

> [!div class="nextstepaction"]
> [SQL Server の R チュートリアル](sql-server-r-tutorials.md)