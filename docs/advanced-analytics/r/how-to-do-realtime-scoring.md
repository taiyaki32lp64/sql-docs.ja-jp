---
title: フォーキャストと予測を生成する
description: SQL Server Machine Learning での R および Python による予測とフォーキャストでは、リアルタイム スコアリングには rxPredict または sp_rxPredict を使用し、ネイティブ スコアリングには PREDICT T-SQL を使用します。
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/30/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 7822cd56a52e47493fe175c293dbfe491a9524af
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727437"
---
# <a name="how-to-generate-forecasts-and-predictions-using-machine-learning-models-in-sql-server"></a>SQL Server で機械学習モデルを使用してフォーキャストと予測を生成する方法
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

既存のモデルを使用して新しいデータ入力に対する結果をフォーキャストまたは予測することは、機械学習の中核となるタスクです。 この記事では、SQL Server で予測を生成するための方法を列挙します。 これらの方法の中には、高速予測のための内部処理方法があります。速度は、実行時の依存関係の段階的な削減に基づきます。 依存関係が少ないほど、予測が高速になります。

内部処理のインフラストラクチャ (リアルタイムまたはネイティブ スコアリング) を使用するには、ライブラリの要件があります。 関数は、Microsoft ライブラリからのものである必要があります。 オープンソースまたはサードパーティの関数を呼び出す R または Python のコードは、CLR または C++ 拡張機能ではサポートされていません。

次の表に、フォーキャストおよび予測に使用するスコアリング フレームワークの概要を示します。 

| 手法           | インターフェイス         | ライブラリの要件 | 処理速度 |
|-----------------------|-------------------|----------------------|----------------------|
| 機能拡張フレームワーク | [rxPredict (R)](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict) <br/>[rx_predict (Python)](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict) | [なし] : モデルは任意の R または Python 関数を基にすることができます | 数百ミリ秒。 <br/>ランタイム環境の読み込み時には、新しいデータがスコアリングされる前に、平均 300 ~ 600 ミリ秒の固定コストがかかります。 |
| [リアルタイム スコアリング CLR 拡張機能](../real-time-scoring.md) | シリアル化されたモデルでの [sp_rxPredict](https://docs.microsoft.com//sql/relational-databases/system-stored-procedures/sp-rxpredict-transact-sql) | R:RevoScaleR、MicrosoftML <br/>Python: revoscalepy、microsoftml | 平均で数十ミリ秒。 |
| [ネイティブ スコアリング C++ 拡張機能](../sql-native-scoring.md) | シリアル化されたモデルでの [PREDICT T-SQL 関数](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql) | R:RevoScaleR <br/>Python: revoscalepy | 平均で 20 ミリ秒未満。 | 

出力の内容ではなく、処理速度が差別化する特徴です。 同じ関数と入力を想定する場合、使用する方法によってスコアリングされた出力が異なることはありません。

モデルは、サポートされている関数を使用して作成され、ディスクに保存された未加工のバイト ストリームにシリアル化されるか、またはデータベースにバイナリ形式で格納される必要があります。 ストアド プロシージャまたは T-SQL を使用すると、R または Python 言語の実行時間のオーバーヘッドなしでバイナリ モデルを読み込んで使用できます。その結果、新しい入力で予測スコアを生成する際の完了までの時間が短縮されます。

CLR および C++ 拡張機能の意義は、データベース エンジンそれ自体に近いことです。 データベース エンジンのネイティブ言語は C++ です。つまり、C++ で記述された拡張機能は、実行時の依存関係が少なくなります。 これに対し、CLR の拡張機能は .NET Core に依存します。 

ご想像のとおり、プラットフォームのサポートは、これらの実行時の環境の影響を受けます。 ネイティブ データベース エンジン拡張機能は、リレーショナル データベースがサポートされていれば、どこでも実行できます。Windows、Linux、Azure 上などです。 .NET Core 要件を持つ CLR 拡張は、現在は Windows のみ対応です。

## <a name="scoring-overview"></a>スコアリングの概要

_スコアリング_ は 2 ステップのプロセスです。 まず、既にトレーニング済みのモデルを指定して、テーブルから読み込みます。 次に、新しい入力データを関数に渡して、予測値 (または_スコア_) を生成します。 多くの場合、入力は T-SQL クエリであり、表形式または単一の行のどちらかを返します。 確率を表す単一の列の値を出力することもできますし、信頼区間、エラー、その他の便利な予測の補完などの、いくつかの値を出力することもできます。

少し前に戻ると、モデルを準備してスコアを生成する全体的なプロセスは、次のようにまとめられます。

1. サポートされているアルゴリズムを使用してモデルを作成します。 サポートは選択したスコアリング方法によって異なります。
2. モデルをトレーニングします。
3. 特別なバイナリ形式を使用して、モデルをシリアル化します。
3. モデルを SQL Server に保存します。 通常、これは、シリアル化されたモデルを SQL Server テーブルに格納することを意味します。
4. モデルとデータの入力をパラメーターとして指定して、関数またはストアド プロシージャを呼び出します。

入力に多数のデータ行が含まれている場合、通常は、スコアリング プロセスの一部として予測値をテーブルに挿入する方が高速です。 フォームまたはユーザー要求から入力値を取得し、スコアをクライアント アプリケーションに返すシナリオでは、単一のスコアを生成するほうがより一般的です。 連続したスコアを生成するときのパフォーマンスを向上させるために、SQL Server はモデルをキャッシュしてメモリに再読み込みできるようにすることがあります。

## <a name="compare-methods"></a>方法の比較

コア データベース エンジン プロセスの完全性を維持するために、R と Python のサポートは、言語処理を RDBMS 処理から分離するデュアル アーキテクチャとして有効になっています。 SQL Server 2016 以降、Microsoft は T-SQL から R スクリプトを実行できる機能拡張フレームワークを追加しました。 SQL Server 2017 では、Python 統合が追加されました。 

拡張機能フレームワークは、単純な関数から複雑な機械学習モデルのトレーニングまで、R または Python で実行できるあらゆる操作をサポートしています。 ただし、デュアル プロセス アーキテクチャでは操作の複雑さに関係なく、すべての呼び出しに対して外部の R または Python プロセスを呼び出す必要があります。 ワークロードで事前トレーニング済みのモデルをテーブルから読み込んで、既に SQL Server にあるデータに対してスコアリングする必要がある場合、外部プロセスの呼び出しによるオーバーヘッドのために、特定の状況では許容できない待機時間が発生します。 たとえば、不正行為の検出では、迅速なスコアリングが必要です。

不正行為の検出などのシナリオでスコアリング速度を向上させるために、SQL Server では C++ および CLR の拡張機能として、R と Python の起動プロセスのオーバーヘッドを解消する、組み込みのスコアリング ライブラリが追加されました。

[**リアルタイム スコアリング**](../real-time-scoring.md)は、ハイ パフォーマンス スコアリングのための最初のソリューションでした。 SQL Server 2017 の初期バージョンで導入され、後に SQL Server 2016 に更新されました。リアルタイム スコアリングは、RevoScaleR、MicrosoftML (R)、revoscalepy、および microsoftml (Python) において Microsoft が管理する関数を介して R と Python のプロセスを代替する、CLR ライブラリに依存しています。 CLR ライブラリは、R または Python ランタイムを呼び出さずに、サポートされている任意のモデル タイプからスコアを生成するために、**sp_rxPredict** ストアド プロシージャを使用して呼び出されます。

[**ネイティブ スコアリング**](../sql-native-scoring.md)は SQL Server 2017 の機能で、ネイティブ C++ ライブラリとして実装されていますが、RevoScaleR モデルと revoscalepy モデルにのみ実装されています。 これは、最速かつ安全な方法ですが、他の方法と比較して、より少ない関数セットをサポートしています。

## <a name="choose-a-scoring-method"></a>スコアリング メソッドを選択する

プラットフォームの要件によって、使用するスコアリング メソッドが決まることもよくあります。

| 製品バージョンとプラットフォーム | 手法 |
|------------------------------|-------------|
| Windows 上の SQL Server 2017、SQL Server 2017 Linux、および Azure SQL Database | T-SQL PREDICT による**ネイティブ スコアリング** |
| SQL Server 2017 (Windows のみ)、SQL Server 2016 R Services SP1 以降 | sp\_rxPredict ストアド プロシージャによる**リアルタイム スコアリング** |

私たちは PREDICT 関数を使用したネイティブ スコアリングをお勧めします。 sp\_rxPredict を使用するには、SQLCLR 統合を有効にする必要があります。 このオプションを有効にする前に、セキュリティへの影響について検討してください。

## <a name="serialization-and-storage"></a>シリアル化とストレージ

高速スコアリング オプションのいずれかとともにモデルを使用するには、サイズおよびスコアリング効率のために最適化された、特別なシリアル化の形式を使用してモデルを保存します。

+ [rxSerializeModel](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxserializemodel) を呼び出して、サポートされているモデルを **raw** 形式に書き込みます。
+ 他の R コードで使用するため、またはモデルを表示するためにモデルを再構成するには、[rxUnserializeModel](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxserializemodel) を呼び出します。

**SQL の使用**

SQL コードからは、[sp_execute_external_script](https://docs.microsoft.com//sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) を使用してモデルをトレーニングし、トレーニング済みのモデルをテーブルに直接挿入することができます。これには **varbinary(max)** 型の列を使用します。 単純な例については、「[R での予測モデルの作成](../tutorials/quickstart-r-train-score-model.md)」に関するページを参照してください。

**R の使用**

R コードから、[rxWriteObject](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxwriteobject) 関数を RevoScaleR パッケージから呼び出して、モデルをデータベースに直接書き込みます。 **rxWriteObject()** 関数は、SQL Server などの ODBC データ ソースから R オブジェクトを取得したり、SQL Server にオブジェクトを書き込んだりできます。 この API は、単純なキー値のストア後にモデル化さます。
  
この関数を使用する場合は、最初に [rxSerializeModel](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxserializemodel) を使用してモデルをシリアル化してください。 次に、シリアル化の手順が繰り返されないように、**rxWriteObject** の *serialize* 引数を FALSE に設定します。

モデルをバイナリ形式にシリアル化することは便利ですが、拡張機能フレームワークで R および Python 実行時環境を使用して予測をスコアリングする場合には必要ありません。 モデルを未加工のバイト形式でファイルに保存し、そのファイルから SQL Server に読み込むことができます。 このオプションは、環境間でモデルを移動またはコピーする場合に便利な場合があります。

## <a name="scoring-in-related-products"></a>関連製品でのスコアリング

[スタンドアロン サーバー](r-server-standalone.md)または [Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server) を使用している場合は、ストアド プロシージャと T-SQL 関数以外にも、予測を迅速に生成するための選択肢があります。 スタンドアロン サーバーと Machine Learning Server はどちらも、コードのデプロイのための *web service* の概念をサポートしています。 R または Python 事前トレーニング済みモデルを web サービスとしてバンドルすることができます。これは、新しいデータ入力を評価するために、実行時に呼ばれます。 詳細については、次の記事を参照してください。

+ [Machine Learning Server の Web サービスとは](https://docs.microsoft.com/machine-learning-server/operationalize/concept-what-are-web-services)
+ [操作化とは](https://docs.microsoft.com/machine-learning-server/what-is-operationalization)
+ [azureml-model-management-sdk を使用して Python モデルを web サービスとしてデプロイする](https://docs.microsoft.com/machine-learning-server/operationalize/python/quickstart-deploy-python-web-service)
+ [新しい web サービスとして R コード ブロックまたはリアルタイム モデルを発行する](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/publishservice)
+ [R 用の mrsdeploy パッケージ](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/mrsdeploy-package)


## <a name="see-also"></a>参照

+ [rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel)  
+ [rxRealTimeScoring](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxrealtimescoring)
+ [sp-rxPredict](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-rxpredict-transact-sql)
+ [PREDICT T-SQL](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql)