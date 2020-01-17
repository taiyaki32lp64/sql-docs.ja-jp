---
title: XDF ファイルを使用してデータを移動する
description: このチュートリアルは、SQL Server で XDF と R 言語を使用してデータを移動する方法について詳しく説明しています。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 6935276a47061652647666184637af8ba1535edd
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727209"
---
# <a name="move-data-between-sql-server-and-xdf-file-sql-server-and-revoscaler-tutorial"></a>SQL Server と XDF ファイル間でデータを移動する (SQL Server と RevoScaleR のチュートリアル)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

このレッスンは、SQL Server で [RevoScaleR 関数](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)を使用する方法についての [RevoScaleR チュートリアル](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)の一部です。

この手順では、XDF ファイルを使用して、リモートとローカルの両方のコンピューティング コンテキストでデータを転送する方法について説明します。 XDF ファイルにデータを格納すると、データを変換できるようになります。

完了したら、ファイル内のデータで新しい [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブルを作成します。 関数 [rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep) は、データを変換し、データ フレームと xdf ファイル間で変換を実行できます。
  
## <a name="create-a-sql-server-table-from-an-xdf-file"></a>XDF ファイルから SQL Server テーブルを作成する

この練習では、クレジット カードの不正使用データを再度使用します。 このシナリオでは、カリフォルニア、オレゴン、ワシントンの各州のユーザーに対して追加の分析を実行するように求められています。 効率向上のため、これらの州のデータだけをローカル コンピューターに格納し、性別、カード会員、州、および残高のみの変数を操作します。

1. 以前に作成した `stateAbb` 変数を再利用して、含めるレベルを特定し、新しい変数 `statesToKeep` に書き込みます。
  
    ```R
    statesToKeep <- sapply(c("CA", "OR", "WA"), grep, stateAbb)
    statesToKeep
    ```
    **結果**
    
    CA|OR|WA
    ----|----|----
    5|38|48
    
2. [!INCLUDE[tsql](../../includes/tsql-md.md)] クエリを使用し、SQL Server から引き渡すデータを定義します。  後で、この変数は *rxImport* の **inData** 引数として使用します。
  
    ```R
    importQuery <- paste("SELECT gender,cardholder,balance,state FROM",  sqlFraudTable,  "WHERE (state = 5 OR state = 38 OR state = 48)")
    ```
  
    クエリにライン フィードやタブなどの隠し文字がないことを確認します。
  
3. 次に、R でデータを操作するときに使用する列を定義します。たとえば、データ セットが小さいとき、クエリは 3 つの州のデータのみを返すため、3 つのファクト レベルのみを必要とします。  `statesToKeep` 変数を再利用して、含める正しいレベルを特定します。
  
    ```R
    importColInfo <- list(
        gender = list( type = "factor",  levels = c("1", "2"), newLevels = c("Male", "Female")),
        cardholder = list(  type = "factor",  levels = c("1", "2"), newLevels = c("Principal", "Secondary")),
        state = list(   type = "factor",  levels = as.character(statesToKeep), newLevels = names(statesToKeep))
            )
    ```
  
4. ローカル コンピューターですべてのデータが使用できる必要があるため、コンピューティング コンテキストを**ローカル**に設定します。
  
    ```R
    rxSetComputeContext("local")
    ```
    
    [rxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdata) 関数を使用して、サポートされているデータ ソースからローカル XDF ファイルにデータをインポートできます。 データのローカル コピーを使用することは、同じクエリを何度も実行せずに、データに対してさまざまな分析を行う際に便利なことがあります。

5. **RxSqlServerData** の引数として以前定義したの変数を渡し、データ ソース オブジェクトを作成します。
  
    ```R
    sqlServerImportDS <- RxSqlServerData(
        connectionString = sqlConnString,
        sqlQuery = importQuery,
        colInfo = importColInfo)
    ```
  
6. **rxImport** を呼び出して、現在の作業ディレクトリの `ccFraudSub.xdf` というファイルにデータを書き込みます。
  
    ```R
    localDS <- rxImport(inData = sqlServerImportDS,
        outFile = "ccFraudSub.xdf",
        overwrite = TRUE)
    ```
  
    **rxImport** 関数から返される `localDs` オブジェクトは、ディスクにローカルに保存された `ccFraud.xdf` データ ファイルを表す軽量の **RxXdfData** データ ソース オブジェクトです。
  
7. XDF ファイルで [rxGetVarInfo](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxgetvarinfoxdf) を呼び出し、データ スキーマが同じであることを確認します。
  
    ```R
    rxGetVarInfo(data = localDS)
    ```

    **結果**
    
    ```R
    rxGetVarInfo(data = localDS)
    Var 1: gender, Type: factor, no factor levels available
    Var 2: cardholder, Type: factor, no factor levels available
    Var 3: balance, Type: integer, Low/High: (0, 22463)
    Var 4: state, Type: factor, no factor levels available
    ```

8. これでさまざまな R 関数を呼び出して、SQL Server 上のソース データの場合と同じように、**localDs** オブジェクトを分析できます。 たとえば、性別によって集計することができます。
  
    ```R
    rxSummary(~gender + cardholder + balance + state, data = localDS)
    ```

## <a name="next-steps"></a>次の手順

このレッスンで、**RevoScaleR** と SQL Server に関する複数パートにおよぶチュートリアル シリーズを終了します。 ここでは、さまざまなデータに関係する計算の概念を紹介し、独自のデータとプロジェクトの要件を扱うための基盤を提供しています。

**RevoScaleR** についての知識を深めるため、R チュートリアルの一覧に戻って、見逃した演習を順を追って進めることができます。 または、目次にあるハウツーに関する記事を参照して、一般的なタスクに関する情報を確認してください。

> [!div class="nextstepaction"]
> [SQL Server の R チュートリアル](sql-server-r-tutorials.md)