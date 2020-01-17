---
title: RevoScaleR を使用してデータを変換する
description: このチュートリアルは、SQL Server で R 言語を使用してデータを変換する方法について詳しく説明しています。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 773607c7800ed1d507aa721ca7cf86a03857ab8b
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727163"
---
# <a name="transform-data-using-r-sql-server-and-revoscaler-tutorial"></a>R を使用してデータを変換する (SQL Server と RevoScaleR のチュートリアル)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

このレッスンは、SQL Server で [RevoScaleR 関数](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)を使用する方法についての [RevoScaleR チュートリアル](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)の一部です。

このレッスンでは、分析のさまざまな段階におけるデータの変換に関して **RevoScaleR** 関数について説明します。

> [!div class="checklist"]
> * **rxDataStep** を使用してデータ サブセットを作成し変換する
> * **rxImport** を使用して、インポート中に XDF ファイルまたはメモリ内のデータ フレームとの間で転送中のデータを変換する

データ移動専用ではありませんが、 **rxSummary**、 **rxCube**、 **rxLinMod**、 **rxLogit** の各関数もすべてデータ変換をサポートします。

## <a name="use-rxdatastep-to-transform-variables"></a>rxDataStep を使用して変数を変換する

[rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep) 関数は一度に 1 つのチャンクのデータを処理し、1 つのデータ ソースからデータを読み取って別のデータ ソースに書き込みます。 変換する列や読み込む変換などを指定できます。

この例を興味深いものにするため、別の R パッケージの関数を使用してデータを変換します。 **boot** パッケージは "推奨" パッケージの 1 つであり、 **boot** は R のすべてのディストリビューションに含まれますが、起動時に自動的に読み込まれることはありません。 そのため、パッケージは、R 統合用に構成された [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスで既に使用できるようになっている必要があります。

**boot** パッケージからは、ロジットの逆数を計算する、**inv.logit** 関数を使用します。 つまり、 **inv.logit** 関数はロジットを [0,1] のスケールで確率に変換します。

> [!TIP] 
> このスケールの予測を取得するもう 1 つの方法としては、 *rxPredict* の元の呼び出しで **type** パラメーターを **response**に設定します。

1. まず、テーブル `ccScoreOutput` 用のデータを保持するためのデータ ソースを作成して開始します。
  
    ```R
    sqlOutScoreDS <- RxSqlServerData( table =  "ccScoreOutput",  connectionString = sqlConnString, rowsPerRead = sqlRowsPerRead )
    ```
  
2. テーブル `ccScoreOutput2` のデータを保持するための別のデータ ソースを追加します。
  
    ```R
    sqlOutScoreDS2 <- RxSqlServerData( table =  "ccScoreOutput2",  connectionString = sqlConnString, rowsPerRead = sqlRowsPerRead )
    ```
  
    新しいテーブルでは、前の `ccScoreOutput` テーブルのすべての変数に加えて、新しく作成された変数を格納します。
  
3. 計算コンテキストを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに設定します。
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```
  
4. **rxSqlServerTableExists** 関数を使用して、出力テーブル `ccScoreOutput2` が既に存在するかどうかを確認します。存在する場合は、**rxSqlServerDropTable** 関数を使用してテーブルを削除します。
  
    ```R
    if (rxSqlServerTableExists("ccScoreOutput2"))     rxSqlServerDropTable("ccScoreOutput2")
    ```
  
5. **rxDataStep** 関数を呼び出して、一覧で目的の変換を指定します。
  
    ```R
    rxDataStep(inData = sqlOutScoreDS,
        outFile = sqlOutScoreDS2,
        transforms = list(ccFraudProb = inv.logit(ccFraudLogitScore)),
        transformPackages = "boot",
        overwrite = TRUE)
    ```

    各列に適用される変換を定義するときは、変換の実行に必要な追加の R パッケージも指定できます。  実行できる変換の種類の詳細については、[RevoScaleR を使用したデータの変換およびサブセット化の方法](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-data-transform)に関するセクションを参照してください。
  
6. **rxGetVarInfo** を呼び出して、新しいデータ セットの変数の概要を表示します。
  
```R
rxGetVarInfo(sqlOutScoreDS2)
```

**結果**

```R
Var 1: ccFraudLogitScore, Type: numeric
Var 2: state, Type: character
Var 3: gender, Type: character
Var 4: cardholder, Type: character
Var 5: balance, Type: integer
Var 6: numTrans, Type: integer
Var 7: numIntlTrans, Type: integer
Var 8: creditLine, Type: integer
Var 9: ccFraudProb, Type: numeric
```

元のロジット スコアは保持されますが、新しい列の *ccFraudProb*が追加されており、ロジット スコアが 0 ～ 1 の値として表示されます。

ファクト変数が文字データとしてテーブル `ccScoreOutput2` に書き込まれていることに注意してください。 以降の解析で因子として使用するには、 *colInfo* パラメーターを使用してレベルを指定します。

## <a name="next-steps"></a>次の手順

> [!div class="nextstepaction"]
> [rxImport を使用してメモリにデータを読み込む](../../advanced-analytics/tutorials/deepdive-load-data-into-memory-using-rximport.md)