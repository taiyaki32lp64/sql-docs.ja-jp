---
title: 'クイック スタート: R でモデルをトレーニングする'
titleSuffix: SQL Server Machine Learning Services
description: SQL Server Machine Learning Services を使用して R で簡単な予測モデルを作成してから、新しいデータを使用して結果を予測します。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/04/2019
ms.topic: quickstart
author: garyericson
ms.author: garye
ms.reviewer: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: bd91191a84aac8c245bdcbbe0afd2bf3241aa6b3
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73726521"
---
# <a name="quickstart-create-and-score-a-predictive-model-in-r-with-sql-server-machine-learning-services"></a>クイック スタート: SQL Server Machine Learning Services を使用して R で予測モデルを作成してスコア付けする
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

このクイックスタートでは、R を使用して予測モデルを作成してトレーニングし、SQL Server インスタンスのテーブルにモデルを保存します。次に、そのモデルを使用して、[SQL Server Machine Learning Services](../what-is-sql-server-machine-learning.md)を使って新しいデータから値を予測します。

SQL で実行されている 2 つのストアド プロシージャを作成して実行します。 最初のプロシージャでは、R に含まれる **mtcars** データセットを使用して、車両にマニュアル トランスミッションが搭載されている確率を予測する単純な汎用線形モデル (GLM) を生成します。 2 番目のプロシージャはスコアリング用で、最初のプロシージャで生成されたモデルを呼び出して、新しいデータに基づいて一連の予測を出力します。 SQL ストアド プロシージャに R コードを配置することで、操作は SQL に格納され、再利用可能になり、他のストアド プロシージャやクライアント アプリケーションから呼び出すことができます。

> [!TIP]
> 線形モデルの最新の情報に更新する必要がある場合は、rxLinMod を使用したモデルの調整プロセスについて説明しているこのチュートリアルをご覧ください。[線形モデルを調整する](/machine-learning-server/r/how-to-revoscaler-linear-model)

このクイックスタートを完了すると、次のことを学習できます。

> [!div class="checklist"]
> - ストアド プロシージャに R コードを埋め込む方法
> - ストアド プロシージャの入力を介してコードに入力を渡す方法
> - ストアド プロシージャを使用してモデルを運用化する方法

## <a name="prerequisites"></a>Prerequisites

- このクイック スタートでは、R 言語がインストールされている [SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) を使用して SQL Server のインスタンスにアクセスする必要があります。

  あなたの SQL Server インスタンスは、Azure 仮想マシンまたはオンプレミスに配置できます。 外部スクリプト機能が既定で無効になっていることに注意してください。そのため、開始する前に、[外部スクリプトを有効にし](../install/sql-machine-learning-services-windows-install.md#bkmk_enableFeature)、**SQL Server Launchpad サービス**が実行されていることを確認する必要があります。

- また、R スクリプトを含む SQL クエリを実行するためのツールも必要です。 これらのスクリプトは、SQL Server インスタンスに接続し、T-SQL クエリまたはストアド プロシージャを実行できる限り、任意のデータベース管理ツールまたはクエリ ツールを使用して実行できます。 このクイック スタートでは、[SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms) を使用します。

## <a name="create-the-model"></a>モデルを作成する

モデルを作成するには、トレーニング用のソース データを作成し、そのデータを使用してモデルの作成およびトレーニングを行います。次に、モデルを SQL データベースに格納します。ここで、このモデルを使用して、新しいデータで予測を生成できます。

### <a name="create-the-source-data"></a>ソース データを作成する

1. SSMS を開き、SQL Server インスタンスに接続し、新しいクエリ ウィンドウを開きます。

1. トレーニング データを保存するテーブルを作成します。

   ```sql
   CREATE TABLE dbo.MTCars(
       mpg decimal(10, 1) NOT NULL,
       cyl int NOT NULL,
       disp decimal(10, 1) NOT NULL,
       hp int NOT NULL,
       drat decimal(10, 2) NOT NULL,
       wt decimal(10, 3) NOT NULL,
       qsec decimal(10, 2) NOT NULL,
       vs int NOT NULL,
       am int NOT NULL,
       gear int NOT NULL,
       carb int NOT NULL
   );
   ```

1. 組み込みデータセット `mtcars` からデータを挿入します。

   ```SQL
   INSERT INTO dbo.MTCars
   EXEC sp_execute_external_script @language = N'R'
       , @script = N'MTCars <- mtcars;'
       , @input_data_1 = N''
       , @output_data_1_name = N'MTCars';
   ```

   > [!TIP]
   > 小規模と大規模の多くのデータセットが R ランタイムに付属しています。 R と共にインストールされるデータセットの一覧を取得するには、R コマンド プロンプトから「`library(help="datasets")`」と入力します。

### <a name="create-and-train-the-model"></a>モデルの作成とトレーニング

自動車の速度データには、馬力 (`hp`) と重量 (`wt`) という、2 つの列 (どちらも数値) が含まれます。 このデータから、車両にマニュアル トランスミッションが搭載されている確率を予測する汎用線形モデル (GLM) を作成します。

モデルを構築するには、R コード内で式を定義し、データを入力パラメーターとして渡します。

```sql
DROP PROCEDURE IF EXISTS generate_GLM;
GO
CREATE PROCEDURE generate_GLM
AS
BEGIN
    EXEC sp_execute_external_script
    @language = N'R'
    , @script = N'carsModel <- glm(formula = am ~ hp + wt, data = MTCarsData, family = binomial);
        trained_model <- data.frame(payload = as.raw(serialize(carsModel, connection=NULL)));'
    , @input_data_1 = N'SELECT hp, wt, am FROM MTCars'
    , @input_data_1_name = N'MTCarsData'
    , @output_data_1_name = N'trained_model'
    WITH RESULT SETS ((model VARBINARY(max)));
END;
GO
```

- `glm` への最初の引数は *formula* パラメーターで、これは、`am` を `hp + wt` に依存するものとして定義します。
- 入力データは、SQL クエリによって設定される変数 `MTCarsData` に格納されます。 入力データに特定の名前を割り当てない場合、既定の変数名は "_InputDataSet_" になります。

### <a name="store-the-model-in-the-sql-database"></a>SQL データベースにモデルを格納する

次に、モデル を SQL データベースに格納して、それを使用して予測や再トレーニングを行えるようにします。 

1. モデルを格納するテーブルを作成する。

   モデルを作成する R パッケージの出力は、通常はバイナリ オブジェクトです。 したがって、モデルを格納するテーブルには、**varbinary(max)** 型の列を提供している必要があります。

   ```sql
   CREATE TABLE GLM_models (
       model_name varchar(30) not null default('default model') primary key,
       model varbinary(max) not null
   );
   ```

1. 次の Transact-SQL ステートメントを実行してストアド プロシージャを呼び出し、モデルを生成し、作成したテーブルにそれを保存します。

   ```sql
   INSERT INTO GLM_models(model)
   EXEC generate_GLM;
   ```

   > [!TIP]
   > このコードを 2 回目に実行する場合、次のエラーが発生します。"Violation of PRIMARY KEY constraint...Cannot insert duplicate key in object dbo.stopping_distance_models" (PRIMARY KEY 制約違反...オブジェクト dbo.stopping_distance_models に重複するキーを挿入することはできません)。 このエラーを避ける 1 つのオプションは、新しいモデルごとに名前を更新することです。 たとえば、わかりやすい名前に変更し、モデルの種類や作成日などを含めることができます。

     ```sql
     UPDATE GLM_models
     SET model_name = 'GLM_' + format(getdate(), 'yyyy.MM.HH.mm', 'en-gb')
     WHERE model_name = 'default model'
     ```

## <a name="score-new-data-using-the-trained-model"></a>トレーニング済みのモデルを使用して新しいデータをスコアリングする

*スコアリング*は、データ サイエンスで使用される用語で、トレーニング済みのモデルに取り込まれた新しいデータに基づいて、予測、確率、またはその他の値を生成することを意味します。 前のセクションで作成したモデルを使用して、新しいデータに対して予測のスコアリングを行います。

### <a name="create-a-table-of-new-data"></a>新しいデータのテーブルを作成する

まず、新しいデータを使用してテーブルを作成します。

```sql
CREATE TABLE dbo.NewMTCars(
    hp INT NOT NULL
    , wt DECIMAL(10,3) NOT NULL
    , am INT NULL
)
GO

INSERT INTO dbo.NewMTCars(hp, wt)
VALUES (110, 2.634)

INSERT INTO dbo.NewMTCars(hp, wt)
VALUES (72, 3.435)

INSERT INTO dbo.NewMTCars(hp, wt)
VALUES (220, 5.220)

INSERT INTO dbo.NewMTCars(hp, wt)
VALUES (120, 2.800)
GO
```

### <a name="predict-manual-transmission"></a>マニュアル トランスミッションを予測する

モデルに基づく予測を取得するには、次の処理を行う SQL スクリプトを作成する必要があります。

1. 必要なモデルを取得します。
1. 新しい入力データを取得します。
1. そのモデルと互換性がある R 予測関数を呼び出します。

時間の経過とともに、テーブルには複数の R モデルが含まれるようになります。それぞれ異なるパラメーターまたはアルゴリズムを使用して構築されるか、異なるデータのサブセットに対してトレーニングされています。 この例では、`default model` という名前のモデルを使用します。

```sql
DECLARE @glmmodel varbinary(max) = 
    (SELECT model FROM dbo.GLM_models WHERE model_name = 'default model');

EXEC sp_execute_external_script
    @language = N'R'
    , @script = N'
            current_model <- unserialize(as.raw(glmmodel));
            new <- data.frame(NewMTCars);
            predicted.am <- predict(current_model, new, type = "response");
            str(predicted.am);
            OutputDataSet <- cbind(new, predicted.am);
            '
    , @input_data_1 = N'SELECT hp, wt FROM dbo.NewMTCars'
    , @input_data_1_name = N'NewMTCars'
    , @params = N'@glmmodel varbinary(max)'
    , @glmmodel = @glmmodel
WITH RESULT SETS ((new_hp INT, new_wt DECIMAL(10,3), predicted_am DECIMAL(10,3)));
```

上記のスクリプトは、次の手順を実行します。

- SELECT ステートメントを使用して、テーブルから 1 つのモデルを取得し、それを入力パラメーターとして渡します。

- テーブルからモデルを取得したら、モデルに対して `unserialize` 関数を呼び出します。

- 適切な引数を使用して `predict` 関数をモデルに適用し、新しい入力データを提供します。

> [!NOTE]
> この例では、テスト フェーズ中に `str` 関数を追加して、R から返されるデータのスキーマを確認します。このステートメントは後で削除できます。
>
> R スクリプトで使用される列名は、ストアド プロシージャの出力に必ずしも渡されるとは限りません。 ここでは、WITH RESULTS 句を使用して、新しい列名をいくつか定義します。

**結果**

![マニュアル トランスミッションの可能性を予測する結果セット](./media/r-predict-am-resultset.png)

また、[PREDICT (Transact-SQL)](../../t-sql/queries/predict-transact-sql.md) ステートメントを使用して、格納されているモデルに基づいて予測値またはスコアを生成することも可能です。

## <a name="next-steps"></a>次の手順

SQL Server Machine Learning Services の詳細については、次を参照してください。

- [SQL Server Machine Learning Services とは (Python と R)](../what-is-sql-server-machine-learning.md)
