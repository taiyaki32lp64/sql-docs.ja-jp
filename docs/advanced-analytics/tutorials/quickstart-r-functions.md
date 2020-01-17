---
title: 'クイック スタート: R 関数の記述'
titleSuffix: SQL Server Machine Learning Services
description: このクイック スタートでは、SQL Server Machine Learning Services を使用した高度な統計計算用の R 関数を作成する方法について説明します。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/04/2019
ms.topic: quickstart
author: garyericson
ms.author: garye
ms.reviewer: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: e725282aaacde748b43a37a317037b5471efd009
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73726883"
---
# <a name="quickstart-write-advanced-r-functions-with-sql-server-machine-learning-services"></a>クイック スタート: SQL Server Machine Learning Services を使用した高度な R 関数を作成する
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

このクイック スタートでは、SQL Server Machine Learning Services を使用して SQL ストアド プロシージャに R の数学関数とユーティリティ関数を埋め込む方法について説明します。 T-SQL で実装するのが複雑な高度な統計関数は、R を使用すると 1 行のコードだけで実行できます。

## <a name="prerequisites"></a>Prerequisites

- このクイック スタートでは、R 言語がインストールされている [SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) を使用して SQL Server のインスタンスにアクセスする必要があります。

  あなたの SQL Server インスタンスは、Azure 仮想マシンまたはオンプレミスに配置できます。 外部スクリプト機能が既定で無効になっていることに注意してください。そのため、開始する前に、[外部スクリプトを有効にし](../install/sql-machine-learning-services-windows-install.md#bkmk_enableFeature)、**SQL Server Launchpad サービス**が実行されていることを確認する必要があります。

- また、R スクリプトを含む SQL クエリを実行するためのツールも必要です。 これらのスクリプトは、SQL Server インスタンスに接続し、T-SQL クエリまたはストアドプロシージャを実行できる限り、任意のデータベース管理ツールまたはクエリ ツールを使用して実行できます。 このクイック スタートでは、[SQL Server Management Studio (SSMS) を使用します。](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms)

## <a name="create-a-stored-procedure-to-generate-random-numbers"></a>乱数を生成するストアド プロシージャを作成する

わかりやすくするために、R `stats` パッケージを使用します。このパッケージは、R がインストールされた SQL Server Machine Learning Services が既定でインストールおよびロードされていてます。 パッケージには、一般的な統計タスク用の数百の関数が含まれますが、その中の `rnorm` 関数は、指定された標準偏差と平均に対し、正規分布を使用して、指定された個数の乱数を生成します。

たとえば、次の R コードは、指定された 3 の標準偏差で、平均値が 50 の 100 個の数値を返します。

```R
as.data.frame(rnorm(100, mean = 50, sd = 3));
```

この R の行を T-SQL から呼び出すには、次のように、`sp_execute_external_script` の R スクリプト パラメーターに R 関数を追加します。

```sql
EXECUTE sp_execute_external_script
      @language = N'R'
    , @script = N'
         OutputDataSet <- as.data.frame(rnorm(100, mean = 50, sd =3));'
    , @input_data_1 = N'   ;'
      WITH RESULT SETS (([Density] float NOT NULL));
```

別の乱数のセットをもっと簡単に生成するにはどうすればよいでしょうか。

これは、SQL Server と組み合わせると簡単です。 ユーザーから引数を取得し、これらの引数を変数として R スクリプトに渡すストアド プロシージャを定義します。

```sql
CREATE PROCEDURE MyRNorm (
    @param1 INT
    , @param2 INT
    , @param3 INT
    )
AS
EXECUTE sp_execute_external_script @language = N'R'
    , @script = N'
         OutputDataSet <- as.data.frame(rnorm(mynumbers, mymean, mysd));'
    , @input_data_1 = N'   ;'
    , @params = N' @mynumbers int, @mymean int, @mysd int'
    , @mynumbers = @param1
    , @mymean = @param2
    , @mysd = @param3
WITH RESULT SETS(([Density] FLOAT NOT NULL));
```

- 最初の行では、ストアド プロシージャが実行されるときに必要な各 SQL 入力パラメーターを定義します。

- `@params` で始まる行は、R コードで使用されるすべての変数と、対応する SQL データ型を定義します。

- それに続く行は、SQL パラメーター名を対応する R 変数名にマップします。

ストアド プロシージャで R 関数をラップしたので、次のように関数を簡単に呼び出し、別の値を渡すことができます。

```sql
EXECUTE MyRNorm @param1 = 100,@param2 = 50, @param3 = 3
```

## <a name="use-r-utility-functions-for-troubleshooting"></a>トラブルシューティングのための R ユーティリティ関数の使用

既定では、**utils** パッケージが含まれます。このパッケージは、現在の R 環境を調査するためのさまざまなユーティリティ関数を提供します。 これらの関数は、SQL Server と外部環境で R コードが実行する方法に不一致が見つかった場合に役立つ可能性があります。

たとえば、R `memory.limit()` 関数を使用して、現在の R 環境のメモリを取得できます。 `utils` パッケージはインストールされていますが既定で読み込まれていないため、最初に `library()` 関数を使用して読み込む必要があります。

```sql
EXECUTE sp_execute_external_script
      @language = N'R'
    , @script = N'
        library(utils);
        mymemory <- memory.limit();
        OutputDataSet <- as.data.frame(mymemory);'
    , @input_data_1 = N' ;'
WITH RESULT SETS (([Col1] int not null));
```

> [!TIP]
> R プロセスによって使用される時間をキャプチャし、パフォーマンスの問題を分析するのに、多くのユーザーが `system.time` や `proc.time` など、R のシステム タイミング関数を使用しています。 例については、「[データ機能の作成](../tutorials/walkthrough-create-data-features.md)」チュートリアルを参照してください。R タイミング関数がソリューションに埋め込まれています。

## <a name="next-steps"></a>次の手順

SQL Server で R を使用して機械学習モデルを作成するには、次のクイック スタートに従ってください。

> [!div class="nextstepaction"]
> [SQL Server Machine Learning Services を使用して R で予測モデルを作成してスコア付けする](quickstart-r-train-score-model.md)

SQL Server Machine Learning Services の詳細については、以下を参照してください。

- [SQL Server Machine Learning Services とは（Python と R）](../what-is-sql-server-machine-learning.md)
