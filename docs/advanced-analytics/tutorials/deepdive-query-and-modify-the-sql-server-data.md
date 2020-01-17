---
title: RevoScaleR を使用して SQL データを変更する
description: このチュートリアルでは、SQL Server で R 言語を使用してデータのクエリを実行し、データを変更する方法について詳しく説明しています。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 65db15d8c6778723ff04f82cde985c4827813339
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727187"
---
# <a name="query-and-modify-the-sql-server-data-sql-server-and-revoscaler-tutorial"></a>SQL Server データのクエリを実行し、データを変更する (SQL Server と RevoScaleR のチュートリアル)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

このレッスンは、SQL Server で [RevoScaleR 関数](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)を使用する方法についての [RevoScaleR チュートリアル](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)の一部です。

前のレッスンでは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] にデータを読み込みました。 このステップでは、**RevoScaleR** を使用してデータを探索および変更できます。

> [!div class="checklist"]
> * 変数に関する基本的な情報を返します。
> * 生データからカテゴリ データを作成します。

カテゴリデータまたは *factor 変数*は、探索データの視覚化に役立ちます。 これらをヒストグラムへの入力として使用すると、変数データがどのように表示されるかを把握できます。

## <a name="query-for-columns-and-types"></a>列と型のクエリ

R IDE または RGui を使用して R スクリプトを実行します。 

最初に、列とそのデータ型の一覧を取得します。 関数 [rxGetVarInfo](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxgetvarinfoxdf) を使用し、分析するデータ ソースを指定できます。 **RevoScaleR** のバージョンによっては、[rxGetVarNames](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxgetvarnames) を使用することもできます。 
  
```R
rxGetVarInfo(data = sqlFraudDS)
```

**結果**

```R
Var 1: custID, Type: integer
Var 2: gender, Type: integer
Var 3: state, Type: integer
Var 4: cardholder, Type: integer
Var 5: balance, Type: integer
Var 6: numTrans, Type: integer
Var 7: numIntlTrans, Type: integer
Var 8: creditLine, Type: integer
Var 9: fraudRisk, Type: integer
```

## <a name="create-categorical-data"></a>カテゴリ データを作成します。

すべての変数は整数として格納されますが、一部の変数はカテゴリ データ (R で *要因変数* と呼ばれる) を表します。たとえば、*state* 列には、50 の州およびコロンビア特別区の識別子として使用される数値が含まれています。 データをわかりやすくするために、この数値を州の略称の一覧で置き換えます。

この手順では、略称を含む文字列ベクトルを作成し、そのカテゴリ値を元の整数の識別子にマップします。 その後で、*colInfo* 引数で新しい変数を使用し、この列を要因として処理するように指定します。 データを分析または移動するたびに、省略形が使用され、列が要素として処理されます。

列を略称にマップしてから要因として使用すると、パフォーマンスも改善されます。 詳細については、「[R とデータの最適化](../r/r-and-data-optimization-r-services.md)」を参照してください。

1. まず、次のように R 変数 *stateAbb*を作成し、この変数に追加する文字列のベクトルを定義します。
  
    ```R
    stateAbb <- c("AK", "AL", "AR", "AZ", "CA", "CO", "CT", "DC",
        "DE", "FL", "GA", "HI","IA", "ID", "IL", "IN", "KS", "KY", "LA",
        "MA", "MD", "ME", "MI", "MN", "MO", "MS", "MT", "NB", "NC", "ND",
        "NH", "NJ", "NM", "NV", "NY", "OH", "OK", "OR", "PA", "RI","SC",
        "SD", "TN", "TX", "UT", "VA", "VT", "WA", "WI", "WV", "WY")
    ```

2. 次に、 *ccColInfo*という名前の列情報オブジェクトを作成します。このオブジェクトは、カテゴリ レベル (州の省略形) への既存の整数値のマッピングを指定します。
  
    このステートメントは、性別およびカード名義人の要因変数も作成します。
  
    ```R
    ccColInfo <- list(
    gender = list(
              type = "factor",
              levels = c("1", "2"),
              newLevels = c("Male", "Female")
              ),
    cardholder = list(
                  type = "factor",
                  levels = c("1", "2"),
                  newLevels = c("Principal", "Secondary")
                   ),
    state = list(
             type = "factor",
             levels = as.character(1:51),
             newLevels = stateAbb
             ),
    balance = list(type = "numeric")
    )
    ```
  
3. 最新のデータを使用する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ ソースを作成するには、以前と同様に **RxSqlServerData** を呼び出しますが、今回は *colInfo* 引数を追加します。
  
    ```R
    sqlFraudDS <- RxSqlServerData(connectionString = sqlConnString,
    table = sqlFraudTable, colInfo = ccColInfo,
    rowsPerRead = sqlRowsPerRead)
    ```
  
    - *table* パラメーターでは、先ほど作成したデータ ソースを含む変数 *sqlFraudTable*を渡します。
    - *colInfo* パラメーターでは、列のデータ型および要因レベルを含む変数 *ccColInfo* を渡します。

4.  以上の手順で、関数 **rxGetVarInfo** を使用して新しいデータ ソース内の変数を確認できるようになりました。
  
    ```R
    rxGetVarInfo(data = sqlFraudDS)
    ```

    **結果**
    
    ```R
    Var 1: custID, Type: integer
    Var 2: gender  2 factor levels: Male Female
    Var 3: state   51 factor levels: AK AL AR AZ CA ... VT WA WI WV WY
    Var 4: cardholder  2 factor levels: Principal Secondary
    Var 5: balance, Type: integer
    Var 6: numTrans, Type: integer
    Var 7: numIntlTrans, Type: integer
    Var 8: creditLine, Type: integer
    Var 9: fraudRisk, Type: integer
    ```

これで、指定した 3 つの変数 (*性別*、 *州*、および *カード名義人*) は要素として扱われます。

## <a name="next-steps"></a>次の手順

> [!div class="nextstepaction"]
> [計算コンテキストの定義と使用](../../advanced-analytics/tutorials/deepdive-define-and-use-compute-contexts.md)