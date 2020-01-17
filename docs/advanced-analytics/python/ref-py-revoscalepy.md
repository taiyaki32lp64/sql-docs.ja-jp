---
title: revoscalepy Python パッケージ
description: SQL Server Machine Learning Services における Python モジュール revoscalepy の概要
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/06/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: c6de9072c32155446b3ff40df3f81af9073c1090
ms.sourcegitcommit: b4ad3182aa99f9cbfd15f4c3f910317d6128a2e5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/06/2019
ms.locfileid: "73706822"
---
# <a name="revoscalepy-python-module-in-sql-server"></a>revoscalepy (SQL Server の Python モジュール)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

**revoscalepy** は Microsoft が提供する Python35 対応モジュールであり、分散コンピューティング、リモート計算コンテキスト、ハイパフォーマンス データ サイエンス アルゴリズムをサポートしています。 これは (Microsoft R Server と SQL Server R Services で配布される) R 向けの **RevoScaleR** パッケージを基礎としており、同様の機能性を提供します。

+ 同じバージョンの **revoscalepy** が与えられたシステムでのローカルとリモートの計算コンテキスト
+ データ変換と視覚化の機能
+ 分散または並列処理によってスケーラブルとなるデータ サイエンス関数
+ Intel 数学ライブラリの使用など、パフォーマンスの向上

**revoscalepy** で作成したデータソースと計算コンテキストは機械学習アルゴリズムでも使用できます。 これらのアルゴリズムの概要については、「[SQL Server の microsoftml Python モジュール](ref-py-microsoftml.md)」を参照してください。

## <a name="full-reference-documentation"></a>完全なリファレンス ドキュメント

**revoscalepy** ライブラリは複数の Microsoft 製品で配布されていますが、SQL Server または別の製品のどちらでライブラリを取得した場合でも、使用方法は同じです。 これらの関数は同じであるため、[個々の revoscalepy 関数のドキュメント](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package)は Microsoft Machine Learning Server の [Python リファレンス](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference)の下でのみ公開されています。 製品固有の動作が存在する場合、関数のヘルプ ページにその相違点が示されます。

## <a name="versions-and-platforms"></a>バージョンとプラットフォーム

**revoscalepy** モジュールは Python 3.5 に基づいており、次のいずれかの Microsoft 製品またはダウンロードをインストールした場合にのみ利用できます。

+ [SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server 9.2.0 以降](https://docs.microsoft.com/machine-learning-server/)
+ [データ サイエンス クライアント用の Python クライアント ライブラリ](setup-python-client-tools-sql.md)

> [!NOTE]
> 完全な製品リリース バージョンは、SQL Server 2017 では Windows のみです。 [SQL Server 2019](../../linux/sql-server-linux-setup-machine-learning.md) の **revoscalepy** では、Windows と Linux の両方がサポートされています。

## <a name="functions-by-category"></a>カテゴリ別の関数

このセクションでは、関数をカテゴリ別に一覧表示し、それぞれの使用方法について説明します。 [目次](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference)を使用して関数をアルファベット順に検索することもできます。

## <a name="1-data-source-and-compute"></a>1 - データ ソースと計算

**revoscalepy** には、データ ソースを作成したり、場所、つまり、計算が実行される場所である*計算コンテキスト*を設定したりするための関数が含まれています。 SQL Server シナリオに関連する関数を次の表に示します。

SQL Server と Python では、場合によっては異なるデータ型が使用されます。 SQL のデータ型と Python のデータ型の対応表が必要であれば、[Python と SQL のデータ型マッピング](python-libraries-and-data-types.md) ページを参照してください。

| 機能| [説明]|
| ------- | ---------- |
| [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxinsqlserver) |  SQL Server 計算コンテキスト オブジェクトを作成し、リモート インスタンスに計算をプッシュします。 一部の **revoscalepy** 関数では、計算コンテキストが引数として受け取られます。 コンテキストスイッチの例については、[revoscalepy を使用したモデルの作成](../tutorials/use-python-revoscalepy-to-create-model.md)に関するページを参照してください。|
| [RxSqlServerData](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxsqlserverdata) | SQL Server クエリまたはテーブルに基づいてデータ オブジェクトを作成します。 |
| [RxOdbcData](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxodbcdata)| ODBC 接続に基づいてデータ ソースを作成します。 |
| [RxXdfData](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxxdfdata) | ローカル XDF ファイルに基づいてデータ ソースを作成します。 XDF ファイルはしばしば、メモリ内データをディスクにオフロードするために使用されます。 XDF ファイルが役立つのは、扱うデータ容量がデータベースから 1 回で転送できない場合や、メモリに収まりきらない場合です。 たとえば、大容量データを定期的にデータベースからローカル ワークステーションに移す場合、R 操作ごとにデータベースに対してクエリを繰り返し実行する代わりに、XDF ファイルを一種のキャッシュとして使用してデータをローカルに保存し、R ワークスペースでそのデータを処理できます。 |

> [!TIP]
> データ ソースまたは計算コンテキストの概念を初めて使用する場合、Microsoft Machine Learning Server ドキュメントで[分散コンピューティング](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-distributed-computing)から始めることをお勧めします。

## <a name="2-data-manipulation-etl"></a>2 - データ操作 (ETL)

| 機能 | [説明] |
|----------|-------------|
|[rx_import](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-import) | .xdf ファイルまたはデータ フレームにデータをインポートします。|
|[rx_data_step](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-data-step) | 入力データ セットのデータを出力データ セットに変換します。|

<a name="bkmk_algorithms"></a>

## <a name="3-training-and-summarization"></a>3 - トレーニングと概要

| 機能| [説明]|
| ------- | ---------- |
|[rx_btrees](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-btrees) | 確率的勾配ブースト デシジョン ツリーを合わせる|
|[rx_dforest](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dforest) | 分類と回帰のデシジョン フォレストを合わせる|
|[rx_dtree](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dtree) | 分類と回帰のツリーを合わせる |
|[rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod) | 線形回帰モデルを作成する|
|[rx_logit](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-logit) | ロジスティック回帰モデルを作成する|
|[rx_summary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary) | revoscalepy でオブジェクトの一変量のまとめを生成します。|

その他の方法については、[microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) の関数も確認してください。

<a name="ml-scoring"></a>

## <a name="4-scoring-functions"></a>4 - スコアリング関数

| 機能| [説明]|
| ------- | ---------- |
| [rx_predict](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict) | トレーニング済みのモデルから予測を生成する|) | トレーニング済みのモデルから予測を生成します。リアルタイムのスコアリングに使用できます。 |
|[rx_predict_default](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict-default) | rx_lin_mod and rx_logit オブジェクトを利用し、予測値と残余を計算します。 |
|[rx_predict_rx_dforest](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict-rx-dforest) | rx_dforest または rx_btrees オブジェクトからデータ セットの予測値または調整値を計算します。 |
|[rx_predict_rx_dtree](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict-rx-dtree) | rx_dtree オブジェクトからデータ セットの予測値または調整値を計算します。 |

## <a name="how-to-work-with-revoscalepy"></a>revoscalepy の使用方法

**revoscalepy** 内の関数は、ストアド プロシージャにカプセル化された Python コードで呼び出すことができます。 ほとんどの開発者は、**revoscalepy** ソリューションをローカルでビルドし、完成した Python コードを展開の練習としてストアド プロシージャに移行します。

ローカルで実行するとき、通常、コマンド ラインまたは Python 開発環境から Python スクリプトを実行し、いずれかの **revoscalepy** 関数で SQL Server 計算コンテキストを指定します。 コード全体または個々の関数に対してリモート計算コンテキストを使用できます。 たとえば、最新のデータを使用してデータの移動を回避するために、モデルのトレーニングをサーバーにオフロードすることがあります。

Python スクリプトをストアド プロシージャ [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) 内にカプセル化する準備ができたら、入力と出力が明確に定義された 1 つの関数としてコードを書き直すことをお勧めします。 

入力と出力は **pandas** データ フレームにする必要があります。 これが完了したら、T-SQL 対応のあらゆるクライアントからストアド プロシージャを呼び出し、入力として SQL クエリを簡単に渡し、結果を SQL テーブルに保存できます。 例については、[SQL 開発者向けのデータベース内 Python 分析の学習](../tutorials/sqldev-in-database-python-for-sql-developers.md)ページを参照してください。

### <a name="using-revoscalepy-with-microsoftml"></a>microsoftml で revoscalepy を使用する

[microsoftml](ref-py-microsoftml.md) の Python 関数は、revoscalepy で与えられる計算コンテキストとデータ ソースと統合されます。 モデルを定義してトレーニングするときなど、microsoftml から関数を呼び出すとき、revoscalepy 関数を使用し、ローカルか SQl Server リモート計算コンテキストで Python コードを実行します。

次の例では、Python コードでモジュールをインポートするための構文を示しています。 その後、必要な個々の関数を参照できます。

```python
from microsoftml.modules.logistic_regression.rx_logistic_regression import rx_logistic_regression
from revoscalepy.functions.RxSummary import rx_summary
from revoscalepy.etl.RxImport import rx_import_datasource
```

## <a name="see-also"></a>参照

+ [Python のチュートリアル](../tutorials/sql-server-python-tutorials.md)
+ [チュートリアル: T-SQL に Python コードを埋め込む](../tutorials/run-python-using-t-sql.md)
+ [Python リファレンス (Microsoft Machine Learning Server)](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference)
