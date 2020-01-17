---
title: データのパフォーマンス チューニング
description: この記事では、SQL Server で実行される R または Python スクリプトのパフォーマンスの最適化について説明します。 また、R コードの更新に使用できるメソッドについても説明します。これにより、パフォーマンスを向上させながら、既知の問題を回避することができます。
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: d966094277f47d3ef12239c32a75c9a3ecbf88c9
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727425"
---
# <a name="performance-for-r-services---data-optimization"></a>R Services のパフォーマンス - データの最適化
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

これは、2 つのケース スタディに基づいて R Services のパフォーマンスの最適化について説明するシリーズの 3 番目の記事です。 この記事では、SQL Server で実行される R または Python スクリプトのパフォーマンスの最適化について説明します。 また、R コードの更新に使用できるメソッドについても説明します。これにより、パフォーマンスを向上させながら、既知の問題を回避することができます。

## <a name="choosing-a-compute-context"></a>計算コンテキストの選択

SQL Server 2016 および 2017 では、R または Python スクリプトを実行するときに、**ローカル**または **SQL** のいずれかの計算コンテキストを使用できます。

**ローカル**の計算コンテキストを使用する場合は、サーバー上ではなく、コンピューター上で分析が実行されます。 したがって、ご自身のコードで使用するために SQL Server からデータを取得する場合、そのデータは、ネットワーク経由でフェッチする必要があります。 このネットワーク転送によるパフォーマンスの低下は、転送されるデータのサイズ、ネットワークの速度、および同時に発生しているその他のネットワーク転送によって異なります。

**SQL Server の計算コンテキスト**を使用する場合、コードはサーバー上で実行されます。 SQL Server からデータを取得する場合、そのデータは、分析が実行されているサーバーに対してローカルである必要があるため、ネットワークのオーバーヘッドは発生しません。 他のソースからデータをインポートする必要がある場合は、事前に ETL を配置することを検討してください。

大規模なデータ セットを操作する場合は、常に SQL 計算コンテキストを使用してください。

## <a name="factors"></a>因子

R 言語には "*因子*" の概念があります。これはカテゴリ データに対する特別な変数です。 データ サイエンティストが因子変数を式で使用することはよくあります。これは、カテゴリ変数を因子として処理することで、データが機械学習関数によって確実かつ適切に処理されるためです。 詳細については、[R for Dummies: 因子変数](https://www.dummies.com/programming/r/how-to-look-at-the-structure-of-a-factor-in-r/)に関するページをご覧ください。

仕様では、因子変数を文字列から整数に変換し、保存または処理するために再度戻すことができます。 引数 *stringsAsFactors* が **False** に設定されていない限り、R `data.frame` 関数では、すべての文字列が因子変数として処理されます。 これは、処理のために文字列が整数に自動変換され、その後、元の文字列に再度マップされることを意味します。

因子のソース データが整数として格納されていると、R は実行時に因子整数を文字列に変換してから、文字列から整数への変換を内部的に実行するため、パフォーマンスが低下する可能性があります。

このような実行時の変換を回避するには、値を整数として SQL Server テーブルに格納し、_colInfo_ 引数を使用して、因子として使用する列のレベル指定することを検討してください。 RevoScaleR のデータ ソース オブジェクトのほとんどが、パラメーター _colInfo_ を取ります。 このパラメーターを使って、データ ソースによって使用される変数に名前を付けて、その型を指定し、列の値に対して変数のレベルまたは変換を定義します。

たとえば、次の R 関数呼び出しによってテーブルから取得されるのは整数 1、2、および 3 ですが、値は "apple"、"orange"、"banana" の各レベルの因子にマップされます。

```R
c("fruit" = c(type = "factor", levels=as.character(c(1:3)), newLevels=c("apple", "orange", "banana")))
```

ソース列に文字列が含まれている場合は、_colInfo_ パラメーターを使用して事前にレベルを指定する方が効率的です。 たとえば、次の R コードでは、読み取り中の文字列が因子として処理されます。

```R
c("fruit" = c(type = "factor", levels= c("apple", "orange", "banana")))
```

モデルの生成でセマンティック上の相違点がない場合は、後者のアプローチによってパフォーマンスが向上する可能性があります。

## <a name="data-transformations"></a>データ変換

多くの場合、データ サイエンティストは、分析の一部として R で記述された変換関数を使用します。 変換関数は、テーブルから取得した各行に適用されます。 SQL Server では、バッチで取得されるすべての行にこのような変換が適用されるため、R インタープリターと分析エンジンの間の通信が必要です。 変換を実行するため、データは SQL から分析エンジンに移動し、その後 R インタープリターで処理されて戻ってきます。

このため、処理されるデータの量によっては、R コードの一部として変換を使用すると、アルゴリズムのパフォーマンスに悪影響を及ぼす可能性があります。

分析を実行する前に必要なすべての列をテーブルまたはビューに用意して、計算中の変換を回避すると、より効率的です。 既存のテーブルに列を追加できない場合は、変換後の列を含む別のテーブルまたはビューを作成し、適切なクエリを使用してデータを取得することを検討してください。

## <a name="batch-row-reads"></a>バッチ行読み取り

お使いのコードで SQL Server データ ソース (`RxSqlServerData`) を使用する場合は、パラメーター _rowsPerRead_ を使用してバッチ サイズを指定することをお勧めします。 このパラメーターでは、クエリ実行後、処理のために外部スクリプトに送信される行数が定義されます。 実行時、アルゴリズムには、各バッチで指定された数の行のみが示されます。

一度に処理するデータ量を制御する機能は、問題の解決や回避に役立ちます。 たとえば、入力データセットの幅が広い (数の列が多い) 場合、またはデータセットに大きな列 (フリー テキストなど) がいくつか含まれている場合は、バッチ サイズを小さくすると、メモリからのデータのページングを回避できます。

既定では、このパラメーターの値は、メモリが少ないマシンでも十分なパフォーマンスを確保できるように 50,000 に設定されています。 サーバーに十分なメモリがある場合は、この値を 500,000 (または 1,000,000) に増やすと、特に大きなテーブルの場合はパフォーマンスが向上する可能性があります。

バッチ サイズを大きくする利点は、大きなデータ セットや、複数のプロセスで実行できるタスクで明らかになります。 ただし、この値を大きくしても最適な結果が得られるとは限りません。 データとアルゴリズムを試して、最適な値を判断することをお勧めします。

## <a name="parallel-processing"></a>並列処理

**rx** 分析関数のパフォーマンスを向上させるために、SQL Server の機能を利用して、サーバー コンピューターで使用可能なコアを使ってタスクを並列で実行できます。

SQL Server で R を使って並列処理を実行する方法は 2 つあります。

-   **\@parallel を使用する。** `sp_execute_external_script` ストアド プロシージャを使用して R スクリプトを実行する場合は、`@parallel` パラメーターを `1` に設定します。 R スクリプトで、他の処理メカニズムを持つ RevoScaleR 関数が使用されて**いない**場合は、この方法が適しています。 スクリプトで RevoScaleR 関数 (通常はプレフィックスが "rx" ) が使用されている場合は、並列処理が自動的に実行されます。明示的に `@parallel` を `1` に設定する必要はありません。

    R スクリプトを並列処理でき、さらに SQL クエリを並列処理できる場合は、データベース エンジンによって複数の並列プロセスが作成されます。 作成できる最大プロセス数は、インスタンスの**並列処理の最大限度** (MAXDOP) の設定と同じです。 その後、すべてのプロセスが同じスクリプトを実行しますが、受け取るのはデータの一部のみです。
    
    したがってこの方法は、モデルをトレーニングしているときのように、すべてのデータを確認する必要があるスクリプトでは役に立ちません。 ただし、バッチ予測などのタスクを並列で実行する場合は便利です。 `sp_execute_external_script` での並列化の使用の詳細については、[Transact-SQL での R コードの使用](../tutorials/quickstart-r-create-script.md)に関するページの**並列処理の高度なヒント**のセクションを参照してください。

-   **numTasks =1 を使用する。** SQL Server 計算コンテキストで **rx** 関数を使用するときは、_numTasks_ パラメーターの値を、作成するプロセスの数に設定します。 作成されたプロセスの数が **MAXDOP** を超えることは決してありませんが、実際に作成されるプロセスの数はデータベース エンジンによって決まり、これが、要求した数よりも少なくなることはあります。

    R スクリプトを並列処理でき、さらに SQL クエリを並列処理できる場合は、rx 関数の実行中、SQL Server によって複数の並列プロセスが作成されます。 作成される実際のプロセスの数は、リソース管理、現在のリソースの使用状況、その他のセッション、R スクリプトで使用されるクエリのクエリ実行プランなど、さまざまな要因によって異なります。

## <a name="query-parallelization"></a>クエリの並列処理

Microsoft R では、ご自身のデータを RxSqlServerData データ ソース オブジェクトとして定義することで、SQL Server データ ソースを操作できます。

テーブルまたはビュー全体に基づいてデータ ソースを作成します。

```R
RxSqlServerData(table= "airline", connectionString = sqlConnString)
```

SQL クエリに基づいてデータ ソースを作成します。

```R
RxSqlServerData(sqlQuery= "SELECT [ArrDelay],[CRSDepTime],[DayOfWeek] FROM  airlineWithIndex WHERE rowNum <= 100000", connectionString = sqlConnString)
```

> [!NOTE]
> データ ソースにクエリではなくテーブルが指定されている場合、R Services は、内部ヒューリスティックを使用して、テーブルから取得する必要がある列を決定します。ただし、この方法は、並列実行になる可能性はほぼありません。

確実にデータを並列で分析するには、データを取得するために使用するクエリは、データベース エンジンが並列クエリ プランを作成できるような方法でフレーム化されている必要があります。 コードまたはアルゴリズムで大量のデータが使用される場合は、`RxSqlServerData` に指定されたクエリが並列実行用に最適化されていることを確認します。 並列実行プランにならないクエリは、計算の 1 つのプロセスになる可能性があります。

大規模なデータセットを処理する必要がある場合は、R コードを実行する前に Management Studio または他の SQL クエリ アナライザーを使用して、実行プランを分析します。 次に、クエリのパフォーマンスを向上させるための推奨手順を実行します。 たとえば、テーブルのインデックス不足は、クエリの実行時間に影響する可能性があります。 詳細については、「[パフォーマンスの監視とチューニング](../../relational-databases/performance/monitor-and-tune-for-performance.md)」を参照してください。

パフォーマンスに影響する可能性がある一般的なミスに、クエリが必要以上の列を取得する、というものがあります。 たとえば、数式が 3 つの列にしか基づいていないのに、ソース テーブルに 30 列が含まれていると、データを不必要に移動することになります。

 + `SELECT *` は使用しないようにしてください。
 + データセット内の列を確認し、分析に必要な列のみを特定します
 + GUID、rowguid など、R コードと互換性のないデータ型を含む列をクエリから削除します
 + サポートされていない日付と時刻の形式を確認します
 + テーブルを読み込むのではなく、特定の値を選択するビューまたは列をキャストするビューを作成して、変換エラーを回避します

## <a name="optimizing-the-machine-learning-algorithm"></a>機械学習アルゴリズムの最適化

このセクションでは、RevoScaleR に固有のその他のヒントとリソース、および Microsoft R のその他のオプションについて説明します。

> [!TIP]
> R の最適化の概要については、この記事では説明しませんが、 コードを高速化する必要がある場合は、「[The R Inferno](https://www.burns-stat.com/pages/Tutor/R_inferno.pdf)」という人気の記事をご覧になることをお勧めします。 この記事では、R のプログラミング構成要素と一般的な落とし穴を明確かつ詳細に説明し、R プログラミング手法のさまざまな例を示します。

### <a name="optimizations-for-revoscaler"></a>RevoScaleR の最適化

RevoScaleR アルゴリズムの多くが、トレーニング モデルの生成方法を制御するパラメーターをサポートしています。 モデルの精度と正確性は重要ですが、アルゴリズムのパフォーマンスも同様に重要な可能性があります。 正確性とトレーニング時間で適切なバランスを得るために、パラメーターを変更することで計算を高速化できます。ほとんどの場合、精度と正確性を低下させることなくパフォーマンスを向上させることができます。

+ [rxDTree](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdtree)

    `rxDTree` では、`maxDepth` パラメーターがサポートされています。これはデシジョン ツリーの深さを制御します。 `maxDepth` が増加するとパフォーマンスが低下する可能性があります。したがって、深さを増やすメリットと、パフォーマンスを低下させるデメリットを分析することが重要です。

    `maxNumBins` `maxDepth`、`maxComplete`、`maxSurrogate` などのパラメーターを調整することで、時間の複雑さと予測の精度のバランスを制御することもできます。 深さを 10 または 15 を超えた値に増やすと、計算が非常に不経済になる可能性があります。

+ [rxLinMod](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlinmod)

    数式の最初の従属変数が因子変数の場合に、`cube` を使用してみます。
    
    `cube` が `TRUE` に設定されているとき、回帰は逆分割を使用して実行されます。これにより、標準的な回帰計算よりも高速になり、使用されるメモリが少なくなる可能性があります。 数式に大量の変数がある場合は、パフォーマンスが大幅に向上する可能性があります。

+ [rxLogit](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlogit)

    数式の最初の従属変数が因子変数の場合に、`cube` を使用します。
    
    `cube` が `TRUE` に設定されている場合は、アルゴリズムにより逆分割が使用されます。これにより高速になり、使用されるメモリが少なくなる可能性があります。 数式に大量の変数がある場合は、パフォーマンスが大幅に向上する可能性があります。

RevoScaleR の最適化に関するその他のガイダンスについては、次の記事を参照してください。

+ サポート記事: [rxDForest と rxDTree のパフォーマンス チューニング オプション](https://support.microsoft.com/kb/3104235)

+ ブースト ツリー モデルに合ったモデルを制御するためのメソッド: [ストキャスティクス勾配ブースティングを使用したモデルの推定](https://docs.microsoft.com/r-server/r/how-to-revoscaler-boosting)

+ RevoScaleR の移動方法とデータの処理方法の概要: [ScaleR でカスタム チャンク アルゴリズムを作成する](https://docs.microsoft.com/r-server/r/how-to-developer-write-chunking-algorithms)

+ RevoScaleR のプログラミング モデル:[RevoScaleR でのスレッドの管理](https://docs.microsoft.com/r-server/r/how-to-developer-manage-threads)

+ [rxDForest](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdforest) 向け関数リファレンス

+ [rxBTrees](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxbtrees) 向け関数リファレンス

### <a name="use-microsoftml"></a>MicrosoftML を使用する

また、新しい **MicrosoftML** パッケージを参照することをお勧めします。このパッケージには、RevoScaleR によって提供される計算コンテキストと変換を使用できる、スケーラブルな機械学習アルゴリズムが用意されています。

+ [MicrosoftML の使用を開始する](https://docs.microsoft.com/r-server/r/concept-what-is-the-microsoftml-package)

+ [MicrosoftML アルゴリズムを選択する方法](https://docs.microsoft.com/r-server/r/how-to-choose-microsoftml-algorithms-cheatsheet)

### <a name="operationalize-a-solution-using-microsoft-r-server"></a>Microsoft R Server を使用してソリューションを運用可能にする

ご自身のシナリオに、格納されたモデルを使用した高速予測、またはアプリケーションへの機械学習の統合が含まれる場合は、Microsoft R Server の[運用可能化](https://docs.microsoft.com/r-server/what-is-operationalization)機能 (以前の DeployR) を使用できます。

+ **データ サイエンティスト**として、[mrsdeploy パッケージ](https://docs.microsoft.com/r-server/r-reference/mrsdeploy/mrsdeploy-package)を使用して、他のコンピューターと R コードを共有し、R 分析を Web、デスクトップ、モバイル、およびダッシュボード アプリケーションに統合します。[Microsoft R Server で R Web サービスを発行および管理する方法](https://docs.microsoft.com/r-server/operationalize/how-to-deploy-web-service-publish-manage-in-r)

+ **管理者**として、パッケージの管理方法、Web ノードと計算ノードの監視方法、および R ジョブでのセキュリティ管理方法を学習します。[R で Web サービスを操作して使用する方法](https://docs.microsoft.com/r-server/operationalize/how-to-consume-web-service-interact-in-r)

## <a name="articles-in-this-series"></a>このシリーズの記事

[R のパフォーマンス チューニング - 概要](sql-server-r-services-performance-tuning.md)

[R のパフォーマンス チューニング - SQL Server の構成](sql-server-configuration-r-services.md)

[R のパフォーマンス チューニング - R コードおよびデータの最適化](r-and-data-optimization-r-services.md)

[パフォーマンス チューニング - ケース スタディの結果](performance-case-study-r-services.md)
