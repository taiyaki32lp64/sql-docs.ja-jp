---
title: rxImport を使用したデータの読み込み
description: SQL Server で R 言語を使用してデータを読み込む方法についてのチュートリアルです。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: ee0a1ddf8ccfdaf9c2b7b4f2ba5724451e7d71b8
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727229"
---
# <a name="load-data-into-memory-using-rximport-sql-server-and-revoscaler-tutorial"></a>rxImport を使用したメモリへのデータの読み込み (SQL Server と RevoScaleR のチュートリアル)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

このレッスンは、SQL Server で [RevoScaleR 関数](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)を使用する方法についての [RevoScaleR チュートリアル](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)の一部です。

[rxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rximport) 関数を使用すると、データ ソースからセッション メモリ内のデータ フレームに、またはディスク上の XDF ファイルにデータを移動できます。 移動先としてファイルを指定しない場合、データはデータ フレームとしてメモリに格納されます。

この手順では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] からデータを取得し、**rxImport** 関数を使用して目的のデータをローカル ファイルに保存する方法について説明します。 この方法を利用すると、データベースに対して再クエリすることなく、ローカルの計算コンテキストでデータを繰り返し分析できます。

## <a name="extract-a-subset-of-data-from-sql-server-to-local-memory"></a>SQL Server のデータのサブセットをローカル メモリに抽出する

リスクの高い個人のみを精査することになった場合を例に説明します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のソース テーブルが大きいため、リスクの高い顧客に関する情報のみを取得する必要があります。 その後、そのデータをローカル ワークステーションのメモリ内のデータ フレームに読み込みます。

1. 計算コンテキストをローカル ワークステーションにリセットします。

    ```R
    rxSetComputeContext("local")
    ```

2. 新しい SQL Server データ ソース オブジェクトを作成し、 *sqlQuery* パラメーターに有効な SQL ステートメントを指定します。 この例では、リスク スコアが最上位になっている観察のサブセットが取得されます。 この方法なら、本当に必要なデータのみがローカル メモリに格納されます。

    ```R
    sqlServerProbDS \<- RxSqlServerData(
        sqlQuery = paste("SELECT * FROM ccScoreOutput2",
        "WHERE (ccFraudProb > .99)"),
        connectionString = sqlConnString)
    ```

3. 関数 [rxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rximport) を呼び出して、ローカル R セッションのデータ フレームにデータを読み取ります。

    ```R
    highRisk <- rxImport(sqlServerProbDS)
    ```

    操作が成功した場合は、次のようなステータス メッセージが表示されます。"Rows Read (読み取られた行) :35, Total Rows Processed (処理された行数の合計) :35, Total Chunk Time (合計チャンク時間) :0.036 seconds (0.036 秒) "

4. これで、高いリスクの観測対象がイン メモリ データ フレームに格納され、さまざまな R 関数を使用してデータ フレームを操作できるようになりました。 この例では、リスク スコアで顧客を並べ替え、高いリスクがあると考えられる顧客の一覧を印刷できます。

    ```R
    orderedHighRisk <- highRisk[order(-highRisk$ccFraudProb),]
    row.names(orderedHighRisk) <- NULL
    head(orderedHighRisk)
    ```

**結果**

```R
ccFraudLogitScore   state gender cardholder balance numTrans numIntlTrans creditLine ccFraudProb1
9.786345    SD   Male  Principal   23456       25            5 75   0.99994382
9.433040    FL Female  Principal   20629       24           28 75   0.99992003
8.556785    NY Female  Principal   19064       82           53 43   0.99980784
8.188668    AZ Female  Principal   19948       29            0 75   0.99972235
7.551699    NY Female  Principal   11051       95            0 75   0.99947516
7.335080    NV   Male  Principal   21566        4            6  75   0.9993482
```

## <a name="more-about-rximport"></a>rxImport の詳細

**rxImport** は、データの移動だけでなく、読み取りプロセスでデータを変換する場合にも使用できます。 たとえば、幅が固定された列の文字数を指定する、変数の説明を指定する、要素列のレベルを設定する、さらにはインポート後に使用する新しいレベルを作成することもできます。

**rxImport** 関数は、インポート プロセス時に変数名を列に割り当てますが、*colInfo* パラメーターを使用して新しい変数名を指定したり、*colClasses* パラメーターを使用してデータ型を変更したりすることができます。

*transforms* パラメーターで追加の操作を指定すると、読み取り対象の各データ群に対して基本的な処理を実行できます。

## <a name="next-steps"></a>次の手順

> [!div class="nextstepaction"]
> [rxDataStep を使用した新しい SQL Server テーブルの作成](../../advanced-analytics/tutorials/deepdive-move-data-between-sql-server-and-xdf-file.md)