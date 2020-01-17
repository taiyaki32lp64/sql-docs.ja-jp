---
title: 'クイック スタート: Python 関数を記述する'
titleSuffix: SQL Server Machine Learning Services
description: このクイック スタートでは、SQL Server Machine Learning Services を使用した高度な統計計算用の Python 関数を作成する方法について説明します。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/04/2019
ms.topic: quickstart
author: garyericson
ms.author: garye
ms.reviewer: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 08f43c6406d0ca2c95cc21a207cae63af6e86902
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727011"
---
# <a name="quickstart-write-advanced-python-functions-with-sql-server-machine-learning-services"></a>クイック スタート: SQL Server Machine Learning Services を使用した高度な Python 関数の作成
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

このクイック スタートでは、SQL Server Machine Learning Services を使用して SQL ストアド プロシージャに Python の数学関数とユーティリティ関数を埋め込む方法について説明します。 T-SQL で実装するのが複雑な高度な統計関数は、Python を使用すると 1 行のコードだけで実行できます。

## <a name="prerequisites"></a>Prerequisites

- このクイックスタートでは、Python 言語がインストールされた [SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) を持つ SQL Server のインスタンスへのアクセスが必要となります。

  あなたの SQL Server インスタンスは、Azure 仮想マシンまたはオンプレミスに配置できます。 外部スクリプト機能が既定で無効になっていることに注意してください。そのため、開始する前に、[外部スクリプトを有効にし](../install/sql-machine-learning-services-windows-install.md#bkmk_enableFeature)、**SQL Server Launchpad サービス**が実行されていることを確認する必要があります。

- また、Python スクリプトを含む SQL クエリを実行するためのツールも必要です。 これらのスクリプトは、SQL Server インスタンスに接続し、T-SQL クエリまたはストアド プロシージャを実行できる限り、任意のデータベース管理ツールまたはクエリ ツールを使用して実行できます。 このクイック スタートでは、[SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms) を使用します。

## <a name="create-a-stored-procedure-to-generate-random-numbers"></a>乱数を生成するストアド プロシージャを作成する

わかりやすくするために、Python `numpy` パッケージを使用します。このパッケージは、Python がインストールされた SQL Server Machine Learning Services が既定でインストールおよびロードされていてます。 パッケージには、一般的な統計タスク用の数百の関数が含まれますが、その中の `random.normal` 関数は、指定された標準偏差と平均に対し、正規分布を使用して、指定された個数の乱数を生成します。

たとえば、次の Python コードは、指定された 3 の標準偏差で、平均値が 50 の 100 個の数値を返します。

```Python
numpy.random.normal(size=100, loc=50, scale=3)
```

この Python の行を T-SQL から呼び出すには、`sp_execute_external_script` の Python スクリプト パラメーターに Python 関数を追加します。 出力にはデータ フレームが必要であるため、`pandas` を使用して変換します。

```sql
EXECUTE sp_execute_external_script @language = N'Python'
    , @script = N'
import numpy
import pandas
OutputDataSet = pandas.DataFrame(numpy.random.normal(size=100, loc=50, scale=3));
'
    , @input_data_1 = N'   ;'
WITH RESULT SETS(([Density] FLOAT NOT NULL));
```

別の乱数のセットをもっと簡単に生成するにはどうすればよいでしょうか。

これは、SQL Server と組み合わせると簡単です。 ユーザーから引数を取得し、これらの引数を変数として Python スクリプトに渡すストアド プロシージャを定義します。

```sql
CREATE PROCEDURE MyPyNorm (
      @param1 INT
    , @param2 INT
    , @param3 INT
    )
AS
EXECUTE sp_execute_external_script @language = N'Python'
    , @script = N'
import numpy
import pandas
OutputDataSet = pandas.DataFrame(numpy.random.normal(size=mynumbers, loc=mymean, scale=mysd));
'
    , @input_data_1 = N'   ;'
    , @params = N' @mynumbers int, @mymean int, @mysd int'
    , @mynumbers = @param1
    , @mymean = @param2
    , @mysd = @param3
WITH RESULT SETS(([Density] FLOAT NOT NULL));
```

- 最初の行では、ストアド プロシージャが実行されるときに必要な各 SQL 入力パラメーターを定義します。

- `@params` で始まる行は、Python コードで使用されるすべての変数と、対応する SQL データ型を定義します。

- それに続く行は、SQL パラメーター名を対応する Python 変数名にマップします。

ストアド プロシージャで Python 関数をラップしたので、次のように関数を簡単に呼び出し、別の値を渡すことができます。

```sql
EXECUTE MyPyNorm @param1 = 100,@param2 = 50, @param3 = 3
```

## <a name="use-python-utility-functions-for-troubleshooting"></a>トラブルシューティングのための Python ユーティリティ関数の使用

Python パッケージは、現在の Python 環境を調査するためのさまざまなユーティリティ関数を提供します。 これらの関数は、SQL Server と外部環境で Python コードが実行する方法に不一致が見つかった場合に役立つ可能性があります。

たとえば、`time` パッケージでシステム タイミング関数を使用して、Python プロセスによって使用される時間を計測し、パフォーマンスの問題を分析することができます。

```sql
EXECUTE sp_execute_external_script
      @language = N'Python'
    , @script = N'
import time
start_time = time.time()

# Run Python processes

elapsed_time = time.time() - start_time
'
    , @input_data_1 = N' ;';
```

## <a name="next-steps"></a>次の手順

SQL Server で Python を使用して機械学習モデルを作成するには、次のクイック スタートに従ってください。

> [!div class="nextstepaction"]
> [クイックスタート: SQL Server Machine Learning Services を使用して Python で予測モデルを作成してスコア付けする](quickstart-python-train-score-model.md)

SQL Server Machine Learning Services の詳細については、次を参照してください。

- [SQL Server Machine Learning Services とは (Python と R)](../what-is-sql-server-machine-learning.md)
