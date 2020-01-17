---
title: RevoScaleR を使用してデータを視覚化する
description: このチュートリアルは、SQL Server で R 言語を使用してデータを視覚化する方法について詳しく説明しています。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: f64b42e69b1399e67211e82e26502c3fcec96254
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727119"
---
#  <a name="visualize-sql-server-data-using-r-sql-server-and-revoscaler-tutorial"></a>R を使用して SQL Server データを視覚化する (SQL Server と RevoScaleR のチュートリアル)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

このレッスンは、SQL Server で [RevoScaleR 関数](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)を使用する方法についての [RevoScaleR チュートリアル](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)の一部です。

このレッスンでは、R 関数を使用して、*creditLine* 列の値の分布を男女別に表示します。

> [!div class="checklist"]
> * ヒストグラム入力用の最小最大変数を作成します
> * **RevoScaleR** から **rxHistogram** を使用して、ヒストグラムのデータを視覚化します
> * 基本 R ディストリビューションに含まれている **lattice** から **levelplot** を使用して、散布図で視覚化します

このレッスンでは、オープンソースと Microsoft 固有の関数を同じスクリプトで組み合わせることができます。

## <a name="add-maximum-and-minimum-values"></a>最小値と最大値を追加する

前のレッスンで計算された概要統計情報に基づき、後続の計算のためにデータ ソースに挿入できるデータに関する有益な情報がいくつか得られました。 たとえば、最小値と最大値を使用して、ヒストグラムを計算できます。 この演習では、**RxSqlServerData** データ ソースに大きい値と小さい値を追加します。

1. まず、仮の変数をいくつか設定します。
  
    ```R
    sumDF <- sumOut$sDataFrame
    var <- sumDF$Name
    ```
  
2. 前のレッスンで作成した変数 *ccColInfo* を利用し、データ ソースに列を定義します。
  
   また、元の定義をオーバーライドする列コレクションに新しく計算された列をいくつか追加します (*numTrans*、*numIntlTrans*、*creditLine*)。 次のスクリプトは、**rxSummary** からのインメモリ出力を格納している sumOut から取得した最小値と最大値に基づいて要素を追加します。 
  
    ```R 
    ccColInfo <- list(
        gender = list(type = "factor",
          levels = c("1", "2"), 
          newLevels = c("Male", "Female")),
        cardholder = list(type = "factor",
          levels = c("1", "2"), 
          newLevels = c("Principal", "Secondary")), 
        state = list(type = "factor", 
          levels = as.character(1:51), 
          newLevels = stateAbb), 
        balance  = list(type = "numeric"),
        numTrans = list(type = "factor", 
          levels = as.character(sumDF[var == "numTrans", "Min"]:sumDF[var == "numTrans", "Max"])),
        numIntlTrans = list(type = "factor",  
            levels = as.character(sumDF[var == "numIntlTrans", "Min"]:sumDF[var =="numIntlTrans", "Max"])),
        creditLine = list(type = "numeric")
            )
    ```
  
3. 列コレクションを更新しているので、次のステートメントを適用し、先に定義した [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ ソースの更新版を作成します。
  
    ```R
    sqlFraudDS <- RxSqlServerData(
        connectionString = sqlConnString,
        table = sqlFraudTable,
        colInfo = ccColInfo,
        rowsPerRead = sqlRowsPerRead)
    ```
  
    これで、*sqlFraudDS* データ ソースに、ccColInfo を使用して追加された新しい列が含まれます。
  
この時点で、変更は R のデータ ソース オブジェクトにのみ影響を与えます。新しいデータはデータベース テーブルにまだ書き込まれていません。 ただし、sumOut 変数でキャプチャされたデータを使用し、視覚化とサマリーを作成できます。 

> [!TIP]
> 使用しているコンピューティング コンテキストがわからなくなった場合は、**rxGetComputeContext()** を実行してください。 "RxLocalSeq Compute Context" という戻り値は、ローカルのコンピューティング コンテキストで実行されていることを示します。

## <a name="visualize-data-using-rxhistogram"></a>rxHistogram を使用してデータを視覚化する

1. 次の R コードを使用して [rxHistogram](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxhistogram) 関数を呼び出し、式とデータ ソースを渡します。 ローカルで最初にこの操作を実行することで、予想される結果と、所要時間を確認できます。
  
    ```R
    rxHistogram(~creditLine|gender, data = sqlFraudDS,  histType = "Percent")
    ```
 
    内部的には、 **rxHistogram** は、 [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcube) パッケージに含まれる **rxCube** 関数を呼び出します。 **rxCube** は、式で指定された各変数の 1 つの列を含む 1 つのリスト (またはデータ フレーム) とカウント列を出力します。
    
2. ここで、リモート SQL Server コンピューターにコンピューティング コンテキストを設定し、**rxHistogram** を再度実行します。
  
    ```R
    rxSetComputeContext(sqlCompute)
    rxHistogram(~creditLine|gender, data = sqlFraudDS,  histType = "Percent")
    ```
 
3. 同じデータ ソースを使用しているため、結果はまったく同じです。ただし、2 番目の手順では、計算はリモート サーバーで実行されます。 結果は、表示のためにローカル ワークステーションに返されます。
   
  ![ヒストグラムの結果](media/rsql-sue-histogramresults.jpg "ヒストグラムの結果")


## <a name="visualize-with-scatter-plots"></a>散布図で視覚化する

散布図は、データ探索時に 2 つの変数間の関係を比較するためによく使用されます。 この目的には、組み込みの R パッケージと **RevoScaleR** 関数によって提供される入力を使用できます。

1. [rxCube](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcrosstabs) 関数を呼び出して、*numTrans* と *numIntlTrans* のすべての組み合わせに対する *fraudRisk* の平均を計算します。
  
    ```R
    cube1 <- rxCube(fraudRisk~F(numTrans):F(numIntlTrans),  data = sqlFraudDS)
    ```
  
    グループの平均の計算に使用するグループを指定するには、 `F()` 表記を使用します。 この例では、`F(numTrans):F(numIntlTrans)` は、変数 `numTrans` と `numIntlTrans` の整数を各整数値をレベルとするカテゴリ変数として処理する必要があることを示します。
  
    **rxCube** の既定の戻り値は、クロス集計を表す *rxCube object* です。 
  
2. [rxResultsDF](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxresultsdf) 関数を呼び出して、R の標準プロット関数のいずれかで簡単に使用できるデータ フレームに、結果を変換できます。
  
    ```R
    cubePlot <- rxResultsDF(cube1)
    ```
  
    **rxCube** 関数にはオプションの引数 *returnDataFrame* = **TRUE** が含まれています。これを使うと、結果をデータ フレームに直接変換できます。 例:
    
    `print(rxCube(fraudRisk~F(numTrans):F(numIntlTrans), data = sqlFraudDS, returnDataFrame = TRUE))`
       
    ただし、**rxResultsDF** の出力の方が簡潔であり、ソース列の名前が保持されます。 `head(cube1)` を実行し、その後 `head(cubePlot)` を実行して出力を比較することができます。
  
3. すべての R ディストリビューションに含まれる **lattice** パッケージの **levelplot** 関数を使用して、ヒート マップを作成します。
  
    ```R
    levelplot(fraudRisk~numTrans*numIntlTrans, data = cubePlot)
    ```
  
    **結果**
  
    ![散布図の結果](media/rsql-sue-scatterplotresults.jpg "散布図の結果")
  
この簡単な分析から、トランザクションの数および国際的トランザクションの数の両方に伴って不正行為のリスクが高くなることがわかります。

一般的な **rxCube** 関数およびクロス集計表の詳細については、「[RevoScaleR を使用したデータのサマリー](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-data-summaries)」を参照してください。

## <a name="next-steps"></a>次の手順

> [!div class="nextstepaction"]
> [SQL Server データを使用して R モデルを作成する](../../advanced-analytics/tutorials/deepdive-create-models.md)