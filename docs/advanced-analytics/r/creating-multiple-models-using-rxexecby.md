---
title: rxExecBy で複数のモデルを作成する
description: RevoScaleR ライブラリの rxExecBy 関数を使用して、SQL Server に格納されているマシン データに対して複数のミニモデルを構築します。
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: dbba63ae69997c9c5dbdccf49ec590b3f4eba652
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727485"
---
# <a name="creating-multiple-models-using-rxexecby"></a>rxExecBy を使用して複数のモデルを作成する
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

RevoScaleR の **rxExecBy** 関数では、複数の関連モデルの並列処理がサポートされています。 データ サイエンティストは、複数の類似エンティティのデータに基づいて 1 つの大きなモデルをトレーニングするのではなく、1 つのエンティティに固有のデータをそれぞれ使用して、多数の関連モデルをすばやく作成できます。 

たとえば、デバイスの障害の監視中、さまざまな種類の機器のデータをキャプチャしているとします。 rxExecBy を使用すると、1 つの大規模なデータセットを入力として提供し、データセットを層化する列 (デバイスの種類など) を指定してから、個々のデバイスに対して複数のモデルを作成できます。

このユース ケースは、大きな複雑な問題を複数のコンポーネントに分けて同時に処理するため、"[pleasingly parallel (あきれるほど並列)](https://en.wikipedia.org/wiki/Embarrassingly_parallel)" と呼ばれています。

このアプローチが採用されている一般的なアプリケーションには、個人の家庭用スマート メーター向け予測、製品ラインごとの収益予測の作成、個々の銀行支店に応じたローン承認用モデル作成などがあります。

## <a name="how-rxexec-works"></a>rxExec のしくみ

RevoScaleR の rxExecBy 関数は、多数の小さなデータ セットに対して大量の並列処理を実行するように設計されています。

1. R コードの一部として rxExecBy 関数を呼び出して、順序指定されていないデータのデータセットを渡します。
2. データのグループ化と並べ替えの基準となるパーティションを指定します。
3. 各データ パーティションに適用する変換関数またはモデリング関数を定義します
4. 関数が実行されたとき、データ クエリは、その関数が環境でサポートされていれば並列処理されます。 さらに、モデリング タスクまたは変換タスクが、個々のコアに分散され、並列で実行されます。 これらの操作でサポートされている計算コンテキストには、RxSpark と RxInSQLServer があります。
5. 複数の結果は返されません。

## <a name="rxexecby-syntax-and-examples"></a>rxExecBy の構文と例

**rxExecBy** は 4 つの入力を取ります。入力の 1 つは、指定された**キー**列でパーティション分割できるデータセットまたはデータ ソース オブジェクトです。 関数は、各パーティションの出力を返します。 出力の形式は、引数として渡される関数によって異なります。 たとえば、rxLinMod などのモデリング関数を渡すと、データセットのパーティションごとに個別のトレーニング済みモデルを返すことができます。

### <a name="supported-functions"></a>サポートされる関数

モデリング: `rxLinMod`、`rxLogit`、`rxGlm`、`rxDtree`

スコアリング: `rxPredict`

変換または分析: `rxCovCor`

## <a name="example"></a>例

次の例は、航空会社のデータセットを使用して複数のモデルを作成する方法を示しています。このデータセットは、[DayOfWeek] 列でパーティション分割されています。 rxExecBy を呼び出すことで、ユーザー定義関数 `delayFunc` が各パーティションに適用されます。 この関数により、月曜日、火曜日などの個別のモデルが作成されます。

```sql
EXEC sp_execute_external_script
@language = N'R'
, @script = N'
delayFunc <- function(key, data, params) { 
    df <- rxImport(inData = airlineData) 
    rxLinMod(ArrDelay ~ CRSDepTime, data = df) 
} 
OutputDataSet <- rxExecBy(airlineData, c("DayOfWeek"), delayFunc)
'
, @input_data_1 = N'select ArrDelay, DayOfWeek, CRSDepTime from AirlineDemoSmall]'
, @input_data_1_name = N'airlineData'

```

エラー `varsToPartition is invalid` が発生した場合は、キー列の名前が正しく入力されているかどうかを確認します。 R 言語では大文字と小文字が区別されます。

この特別な例は、SQL Server 用に最適化されていません。多くの場合、SQL を使用してデータをグループ化することで、パフォーマンスを向上させることができます。 ただし、rxExecBy を使用すると、R から並列ジョブを作成できます。

次の例は、SQL Server を計算コンテキストとして使用した R でのプロセスを示しています。

```R
sqlServerConnString <- "SERVER=hostname;DATABASE=TestDB;UID=DBUser;PWD=Password;"
inTable <- paste("airlinedemosmall")
sqlServerDataDS <- RxSqlServerData(table = inTable, connectionString = sqlServerConnString)

# user function
".Count" <- function(keys, data, params)
{
  myDF <- rxImport(inData = data)
  return (nrow(myDF))
}

# Set SQL Server compute context with level of parallelism = 2
sqlServerCC <- RxInSqlServer(connectionString = sqlServerConnString, numTasks = 4)
rxSetComputeContext(sqlServerCC)

# Execute rxExecBy in SQL Server compute context
sqlServerCCResults <- rxExecBy(inData = sqlServerDataDS, keys = c("DayOfWeek"), func = .Count)
```


