---
title: 'クイック スタート: Python でモデルをトレーニングする'
titleSuffix: SQL Server Machine Learning Services
description: SQL Server Machine Learning Services を使用して Python で簡単な予測モデルを作成してから、新しいデータを使用して結果を予測します。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/14/2019
ms.topic: quickstart
author: garyericson
ms.author: garye
ms.reviewer: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: fcf43d57488578020eed09080668156fb926d1b0
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73726997"
---
# <a name="quickstart-create-and-score-a-predictive-model-in-python-with-sql-server-machine-learning-services"></a>クイック スタート: SQL Server Machine Learning Services を使用して Python で予測モデルを作成してスコア付けする
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

このクイックスタートでは、Python を使用して予測モデルを作成してトレーニングし、SQL Server インスタンスのテーブルにモデルを保存します。次に、そのモデルを使用して、[SQL Server Machine Learning Services](../what-is-sql-server-machine-learning.md) を使って新しいデータから値を予測します。

SQL で実行されている 2 つのストアド プロシージャを作成して実行します。 最初の例では、クラシックなアヤメの花のデータセットを使用して、花の特性に基づいてアヤメの種を推測する Naïve Bayes モデルを生成します。 2 番目のプロシージャはスコアリング用で、最初のプロシージャで生成されたモデルを呼び出して、新しいデータに基づいて一連の予測を出力します。 SQL ストアド プロシージャに Python コードを配置することで、操作は SQL に格納され、再利用可能になり、他のストアド プロシージャやクライアント アプリケーションから呼び出すことができます。

このクイックスタートを完了すると、次のことを学習できます。

> [!div class="checklist"]
> - ストアド プロシージャに Python コードを埋め込む方法
> - ストアド プロシージャの入力を介してコードに入力を渡す方法
> - ストアド プロシージャを使用してモデルを運用化する方法

## <a name="prerequisites"></a>Prerequisites

- このクイックスタートでは、Python 言語がインストールされた [SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) をもつ SQL Server のインスタンスへのアクセスが必要となります。

- また、Python スクリプトを含む SQL クエリを実行するためのツールも必要です。 これらのスクリプトは、SQL Server インスタンスに接続し、T-SQL クエリまたはストアド プロシージャを実行できる限り、任意のデータベース管理ツールまたはクエリ ツールを使用して実行できます。 このクイック スタートでは、[SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms) を使用します。

- この演習で使用されるサンプル データは、アヤメのサンプル データです。 [アヤメのデモ データ](demo-data-iris-in-sql.md)の指示に従って、**irissql** サンプル データベースを作成します。

## <a name="create-a-stored-procedure-that-generates-models"></a>モデルを生成するストアド プロシージャを作成する

この手順では、結果を予測するためのモデルを生成するストアド プロシージャを作成します。

1. SSMS を開き、SQL Server インスタンスに接続し、新しいクエリ ウィンドウを開きます。

1. irissql データベースに接続するします。

    ```sql
    USE irissql
    GO
    ```

1. 次のコードをコピーして、新しいストアド プロシージャを作成します。

   このプロシージャを実行すると [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) が呼び出され、Python セッションが開始されます。 
   
   Python コードで必要な入力は、このストアド プロシージャの入力パラメーターとして渡されます。 機械学習アルゴリズムの Python **scikit-learn** ライブラリに基づいて、出力はトレーニング済みのモデルになります。 

   このコードでは、[**pickle**](https://docs.python.org/2/library/pickle.html) を使用して、モデルをシリアル化します。 モデルは、**iris_data** テーブルの列 0 から 4 のデータを使用してトレーニングされます。 
   
   プロシージャの 2 番目の部分に表示されるパラメーターは、データ入力とモデル出力を明確にします。 可能な限り、ストアド プロシージャで実行されている Python コードでは、実行時に渡されたストアド プロシージャの入力と出力にマップされる入力と出力を明確に定義する必要があります。

    ```sql
    CREATE PROCEDURE generate_iris_model (@trained_model VARBINARY(max) OUTPUT)
    AS
    BEGIN
        EXECUTE sp_execute_external_script @language = N'Python'
            , @script = N'
    import pickle
    from sklearn.naive_bayes import GaussianNB
    GNB = GaussianNB()
    trained_model = pickle.dumps(GNB.fit(iris_data[["Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width"]], iris_data[["SpeciesId"]].values.ravel()))
    '
            , @input_data_1 = N'select "Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "SpeciesId" from iris_data'
            , @input_data_1_name = N'iris_data'
            , @params = N'@trained_model varbinary(max) OUTPUT'
            , @trained_model = @trained_model OUTPUT;
    END;
    GO
    ```

1. ストアド プロシージャが存在することを確認します。 

   前の手順の T-SQL スクリプトがエラーなしで実行された場合は、**generate_iris_model** という名前の新しいストアド プロシージャが作成され、**irissql** データベースに追加されます。 ストアド プロシージャは、 **[プログラミング]** の下にある SSMS **[オブジェクト エクスプローラー]** にあります。

## <a name="execute-the-procedure-to-create-and-train-models"></a>手順を実行してモデルを作成およびトレーニングする

この手順では、埋め込みコードを実行するプロシージャを実行し、トレーニング済みのシリアル化されたモデルを出力として作成します。 

SQL Server で再利用するために格納されているモデルは、バイト ストリームとしてシリアル化され、データベース テーブルの「VARBINARY (MAX)」列に格納されます。 モデルの作成、トレーニング、シリアル化、およびデータベースへの保存が完了すると、他のプロシージャ、またはスコアリング ワークロードの [PREDICT T-SQL](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql) 関数から呼び出すことができます。

1. プロシージャを実行するには、次のコードを実行します。 ストアド プロシージャを実行するための特定のステートメントは、4 行目の `EXECUTE` です。

   この特定のスクリプトは、同じ名前の既存のモデル ("Naive Bayes") を削除することで、同じプロシージャを再実行して作成された新しいモデルのスペースを確保します。 モデルを削除しないと、オブジェクトが既に存在することを示すエラーが発生します。 このモデルは、**irissql** データベースを作成したときにプロビジョニングされた **iris_models** という名前のテーブルに格納されます。

    ```sql
    DECLARE @model varbinary(max);
    DECLARE @new_model_name varchar(50)
    SET @new_model_name = 'Naive Bayes'
    EXECUTE generate_iris_model @model OUTPUT;
    DELETE iris_models WHERE model_name = @new_model_name;
    INSERT INTO iris_models (model_name, model) values(@new_model_name, @model);
    GO
    ```

1. モデルが挿入されたことを確認します。

    ```sql
    SELECT * FROM dbo.iris_models
    ```

    **結果**

    | model_name  | model |
    |---|-----------------|
    | Naive Bayes | 0x800363736B6C6561726E2E6E616976655F62617965730A... | 

## <a name="create-and-execute-a-stored-procedure-for-generating-predictions"></a>予測を生成するためのストアド プロシージャを作成および実行する

モデルの作成、トレーニング、保存が完了したので、予測を生成するストアド プロシージャを作成する次の手順に進みます。 これを行うには、`sp_execute_external_script` を呼び出してシリアル化されたモデルを読み込み、スコア付けする新しいデータ入力を提供する Python スクリプトを実行します。

1. 次のコードを実行して、スコアリングを実行するストアド プロシージャを作成します。 このプロシージャを実行すると、バイナリ モデルを読み込み、列 `[1,2,3,4]` を入力として使用し、`[0,5,6]` 列を出力として指定します。

   ```sql
   CREATE PROCEDURE predict_species (@model VARCHAR(100))
   AS
   BEGIN
       DECLARE @nb_model VARBINARY(max) = (
               SELECT model
               FROM iris_models
               WHERE model_name = @model
               );
   
       EXECUTE sp_execute_external_script @language = N'Python'
           , @script = N'
   import pickle
   irismodel = pickle.loads(nb_model)
   species_pred = irismodel.predict(iris_data[["Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width"]])
   iris_data["PredictedSpecies"] = species_pred
   OutputDataSet = iris_data[["id","SpeciesId","PredictedSpecies"]] 
   print(OutputDataSet)
   '
           , @input_data_1 = N'select id, "Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "SpeciesId" from iris_data'
           , @input_data_1_name = N'iris_data'
           , @params = N'@nb_model varbinary(max)'
           , @nb_model = @nb_model
       WITH RESULT SETS((
                   "id" INT
                 , "SpeciesId" INT
                 , "SpeciesId.Predicted" INT
                   ));
   END;
   GO
   ```

2. 使用するモデルをプロシージャが認識できるように、ストアド プロシージャを実行して、モデル名 "Naive Bayes" を指定します。

   ```sql
   EXECUTE predict_species 'Naive Bayes';
   GO
   ```

   ストアド プロシージャを実行すると、Python data.frame が返されます。 T-SQL の次の行は、返される結果のスキーマを指定します: `WITH RESULT SETS ( ("id" int, "SpeciesId" int, "SpeciesId.Predicted" int));`。 結果を新しいテーブルに挿入するか、アプリケーションに返すことができます。

   ![実行中のストアド プロシージャからの結果セット](media/train-score-using-python-NB-model-results.png)

   結果は、花の特性を入力として使用している種に関する 150 件の予測です。 観測の大部分では、予測された種は実際の条件に一致します。

   この例は、トレーニングとスコアリングの両方で Python のアヤメ データセットを使用することで単純化されています。 より一般的な方法では、SQL クエリを実行して新しいデータを取得し、それを `InputDataSet` として Python に渡します。

## <a name="conclusion"></a>まとめ

この演習では、各ストアド プロシージャがシステム ストアド プロシージャ `sp_execute_external_script` を使用して Python プロセスを開始する、さまざまなタスク専用のストアド　プロシージャを作成する方法について学習しました。 Python プロセスへの入力は、パラメーターとして `sp_execute_external` に渡されます。 SQL Server データベースの Python スクリプト自体とデータ変数は両方とも入力として渡されます。

一般的に、SSMS は洗練された Python コードと共に使用するか、行ベースの出力を返す単純な Python コードでのみ使用すべきです。 ツールとして、SSMS は T-SQL などのクエリ言語をサポートし、フラット化された行セットを返します。 コードで散布図やヒストグラムなどの視覚的な出力を生成する場合は、イメージをレンダリングできるツールまたはエンドユーザー向けのアプリケーションが必要です。

さまざまな操作を処理する包括的なスクリプトを記述することに慣れた Python 開発者にとって、タスクを個別の手順で整理することに必要性を感じない場合もあります。 しかし、トレーニングとスコアリングには異なるユース ケースがあります。 これらのタスクを分離することにより、各タスクをそれぞれ異なるスケジュールで進め、各操作に異なるスコープのアクセス許可を設定できます。

同様に、並列処理、リソース管理などの SQL Server のリソース機能を活用したり、ストリーミングと並列実行をサポートする [microsoft ml](../python/ref-py-microsoftml.md) のアルゴリズムを使用するようにスクリプトを記述したりすることもできます。 トレーニングとスコアリングを分けることで、特定のワークロードの最適化をターゲティングすることができます。

最終的な利点は、パラメーターを使用してプロセスを変更できることです。 この演習では、モデルを作成した Python コード (この例では "Naive Bayes" という名前) が、スコアリング プロセスでモデルを呼び出す 2 番目のストアド プロシージャに入力として渡されました。 この演習では 1 つのモデルのみを使用しますが、スコアリング タスクでモデルをパラメーター化することによってスクリプトの有用性が向上することはお分かりいただけるかと思います。

## <a name="next-steps"></a>次の手順

SQL Server Machine Learning Services の詳細については、次を参照してください。

- [SQL Server Machine Learning Services とは (Python と R)](../what-is-sql-server-machine-learning.md)
