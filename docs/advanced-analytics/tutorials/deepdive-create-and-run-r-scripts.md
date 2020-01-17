---
title: RevoScaleR の概要の統計情報
description: SQL Server で R 言語を使用して概要の統計情報を計算する方法を説明するチュートリアルです。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 4ece8cdac4f39cfd5d4b93484f18b0d415cc2291
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727299"
---
# <a name="compute-summary-statistics-in-r-sql-server-and-revoscaler-tutorial"></a>R での概要統計情報の計算 (SQL Server および RevoScaleR チュートリアル)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

このレッスンは、SQL Server で [RevoScaleR 関数](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)を使用する方法についての [RevoScaleR チュートリアル](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)の一部です。

前のレッスンで作成した確立したデータ ソースとコンピューティング コンテキストを使用して、高性能な R スクリプトを実行します。 このレッスンでは、次のタスクのために、ローカルとリモートのサーバー コンピューティング コンテキストを使用します。

> [!div class="checklist"]
> * コンピューティング コンテキストを SQL Server に切り替える
> * リモート データ オブジェクトに関する概要の統計情報を取得する
> * ローカル 概要を計算する

前のレッスンを完了している場合は、sqlCompute および sqlComputeTrace というリモート コンピューティング コンテキストがあるはずです。 この後のレッスンで、sqlCompute とローカル コンピューティング コンテキストを使用します。

このレッスンでは、R IDE または **Rgui** を使用して R スクリプトを実行します。

## <a name="compute-summary-statistics-on-remote-data"></a>リモート データに関する概要の統計情報を計算する

R コードをリモートで実行する前に、リモート コンピューティング コンテキストを指定する必要があります。 *sqlCompute* パラメーターに指定されている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] コンピューターで後続のすべての計算が行われます。

コンピューティング コンテキストは、変更するまでアクティブな状態が維持されます。 ただし、リモート サーバー コンテキストで実行*できない* R スクリプトは自動的にローカルで実行されます。

コンピューティング コンテキストがどのように動作するかを確認するには、リモート SQL Server で sqlFraudDS データ ソースに関する概要の統計情報を生成します。 このデータ ソース オブジェクトは[レッスン 2](deepdive-create-sql-server-data-objects-using-rxsqlserverdata.md) で作成され、RevoDeepDive データベースの ccFraudSmall テーブルを表しています。 

1. 前のレッスンで作成した sqlCompute にコンピューティング コンテキストを切り替えます。
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```

2. [rxSummary](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsummary) 関数を呼び出し、式やデータ ソースなど、必須の引数を渡し、結果を変数 `sumOut` に代入します。
  
    ```R
    sumOut <- rxSummary(formula = ~gender + balance + numTrans + numIntlTrans + creditLine, data = sqlFraudDS)
    ```
  
    R 言語はさまざまな概要関数を提供しますが、**RevoScaleR** の **rxSummary** は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を含む、さまざまなリモート コンピューティング コンテキストでの実行をサポートします。 同様の関数に関する詳細については、[RevoScaleR を使用したデータの概要](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-data-summaries)を参照してください。
  
3. SumOut の内容をコンソールに印刷します。
  
    ```R
    sumOut
    ```
    > [!NOTE]
    > エラーが発生した場合は、実行が完了するまで数分待ってから、コマンドを再試行してください。

**結果**

```R
Summary Statistics Results for: ~gender + balance + numTrans + numIntlTrans + creditLine
Data: sqlFraudDS (RxSqlServerData Data Source)
Number of valid observations: 10000

 Name  Mean    StdDev  Min Max ValidObs    MissingObs
 balance       4075.0318 3926.558714            0   25626 100000
 numTrans        29.1061   26.619923 0     100 10000    0           100000
 numIntlTrans     4.0868    8.726757 0      60 10000    0           100000
 creditLine       9.1856    9.870364 1      75 10000    0          100000
 
 Category Counts for gender
 Number of categories: 2
 Number of valid observations: 10000
 Number of missing observations: 0

 gender Counts
  Male   6154
  Female 3846
```

## <a name="create-a-local-summary"></a>ローカル 概要を作成する

1. すべての作業をローカルに行うように計算コンテキストを変更します。
  
    ```R
    rxSetComputeContext ("local")
    ```
  
2. SQL Server からデータを抽出するときに、多くの場合、読み取りごとに抽出される行の数を増やすことで、パフォーマンスを向上させることができます。これは、増加したブロック サイズをメモリ内に確保できることを前提としています。 次のコマンドを実行して、データ ソースで *rowsPerRead* パラメーターの値を大きくします。 これまでは、 *rowsPerRead* の値は 5000 に設定されていました。
  
    ```R
    sqlServerDS1 <- RxSqlServerData(
       connectionString = sqlConnString,
       table = sqlFraudTable,
       colInfo = ccColInfo,
       rowsPerRead = 10000)
    ```

3. 新しいデータ ソースに対して **rxSummary** を呼び出します。
  
    ```R
    rxSummary(formula = ~gender + balance + numTrans + numIntlTrans + creditLine, data = sqlServerDS1)
    ```
  
   実際の結果は、 **コンピューターのコンテキストで** rxSummary [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を実行した場合と同じになるはずです。 ただし、処理は速くなる場合と遅くなる場合があります。 データは分析のためのローカル コンピューターに転送されるので、処理速度はデータベースへの接続に左右されます。

4. 次のいくつかのレッスンでは、リモート コンピューティング コンテキストに戻ります。

    ```R
    rxSetComputeContext(sqlCompute)
    ```

## <a name="next-steps"></a>次の手順

> [!div class="nextstepaction"]
> [R を使用して SQL Server のデータを表示する](../../advanced-analytics/tutorials/deepdive-visualize-sql-server-data-using-r.md)