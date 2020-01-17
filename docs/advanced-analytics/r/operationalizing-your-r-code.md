---
title: ストアド プロシージャで R コードをデプロイする
description: R 言語コードを SQL Server ストアド プロシージャに埋め込んで、SQL Server データベースにアクセスできる任意のクライアント アプリケーションで使用できるようにします。
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/15/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 15c3406d6745802ece620942bf51b23c4d3643ee
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727448"
---
# <a name="operationalize-r-code-using-stored-procedures-in-sql-server-machine-learning-services"></a>SQL Server Machine Learning Services でストアド プロシージャを使用して R コードを運用可能にする
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

SQL Server Machine Learning Services の R および Python 機能を使用しているとき、ソリューションを運用環境に移行するアプローチとして最も一般的なのは、コードをストアド プロシージャに埋め込むことです。 この記事では、SQL Server を使用して R コードを運用可能にするときの SQL 開発者を対象とした重要な考慮事項についてまとめます。

## <a name="deploy-production-ready-script-using-t-sql-and-stored-procedures"></a>T-SQL とストアド プロシージャを使用して、すぐに使用できるスクリプトをデプロイする

従来、データ サイエンス ソリューションの統合は、パフォーマンスと統合をサポートするための広範な再コーディングを意味していました。 このタスクは SQL Server Machine Learning Services によって簡素化されます。R と Python コードは SQL Server で実行でき、ストアド プロシージャを使って呼び出すことができるためです。 ストアド プロシージャにコードを埋め込むしくみの詳細については、以下を参照してください。

+ [SQL Server でシンプルな R スクリプトを作成して実行する](../tutorials/quickstart-r-create-script.md)
+ [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)

ストアド プロシージャを使用して R コードを運用環境にデプロイするより包括的な例については、「[チュートリアル: SQL 開発者向けの R data analytics](../../advanced-analytics/tutorials/sqldev-in-database-r-for-sql-developers.md)」を参照してください

## <a name="guidelines-for-optimizing-r-code-for-sql"></a>SQL 向け R コードを最適化するためのガイドライン

R または Python コードで事前に最適化をいくつか行うと、お使いの R コードを SQL で変換しやすくなります。 これには、問題の原因となるデータ型を回避する、不要なデータ変換が行われないようにする、簡単にパラメーター化できる 1 つの関数呼び出しとして R コードを再生成する、などの作業が含まれます。 詳細については、以下をご覧ください。

+ [R ライブラリとデータ型](r-libraries-and-data-types.md)
+ [R Services で使用する R コードの変換](converting-r-code-for-use-in-sql-server.md)
+ [sqlrutils ヘルパー関数を使用する](ref-r-sqlrutils.md)

## <a name="integrate-r-and-python-with-applications"></a>R および Python をアプリケーションと統合する

ストアド プロシージャから R または Python を実行できるため、T-SQL ステートメントを送信して結果を処理できる任意のアプリケーションからスクリプトを実行できます。 たとえば、Integration Services で [T-SQL の実行タスク](https://docs.microsoft.com/sql/integration-services/control-flow/execute-t-sql-statement-task)を使用するか、ストアド プロシージャを実行できる別のジョブ スケジューラを使用して、スケジュールに従ってモデルを再トレーニングする場合があります。

外部アプリケーションから簡単に自動化、または開始できる重要なタスクがスコアリングです。 R または Python またはストアド プロシージャを使用してモデルを事前にトレーニングし、テーブルに[そのモデルをバイナリ形式で保存](../tutorials/walkthrough-build-and-save-the-model.md)します。 その後、モデルは、T-SQL から次のいずれかのスコアリング オプションを使用して、ストアド プロシージャ呼び出しの一部として変数に読み込むことができます。

+ リアルタイム スコアリング。小規模なバッチ用に最適化
+ 単一行スコアリング。アプリケーションからの呼び出し
+ [ネイティブ スコアリング](../sql-native-scoring.md)。R を呼び出さずに SQL Server から高速バッチ予測

このチュートリアルでは、バッチ モードと単一行モードの両方における、ストア ドプロシージャを使用したスコアリングの例を示します。

+ [SQL Server における R 用エンド ツー エンド データ サイエンスのチュートリアル](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)

アプリケーションでスコアリングを統合する方法の例については、次のソリューション テンプレートを参照してください。

+ [小売予測](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/RetailForecasting/Introduction.md)
+ [不正行為の検出](https://github.com/Microsoft/r-server-fraud-detection)
+ [顧客クラスタリング](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/r-services/getting-started/customer-clustering)

## <a name="boost-performance-and-scale"></a>パフォーマンスとスケールの向上

オープン ソース R 言語には、大規模データ セットに関する既知の制限がありますが、SQL Server Machine Learning Service に含まれる [RevoScaleR パッケージ API](ref-r-revoscaler.md) は大規模なデータ セットを処理でき、マルチスレッド、マルチコア、マルチプロセスのデータベース内計算のメリットを得ることができます。

R ソリューションで複雑な集計が使用されている場合、または大規模なデータセットが含まれる場合は、SQL Server の非常に効率的なインメモリ集計と列ストア インデックスを利用して、R コードで統計の計算結果とスコア付けを処理できます。

SQL Server Machine Learning Services でパフォーマンスを向上させる方法の詳細については、以下をご覧ください。

+ [SQL Server R Services のパフォーマンス チューニング](../../advanced-analytics/r/sql-server-r-services-performance-tuning.md)
+ [パフォーマンス最適化のヒントとテクニック](https://gallery.cortanaintelligence.com/Tutorial/SQL-Server-Optimization-Tips-and-Tricks-for-Analytics-Services)

## <a name="adapt-r-code-for-other-platforms-or-compute-contexts"></a>他のプラットフォームまたはコンピューティング コンテキストに合わせて R コードを調整する

SQL Server セットアップで[スタンドアロン サーバー オプション](../install/sql-machine-learning-standalone-windows-install.md)を使用する場合、または SQL 以外の製品、Microsoft Machine Learning Server (以前の **Microsoft R Server**) をインストールする場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データに対して実行する R コードと同じものを、Spark over HDFS などの他のデータ ソースに対して使用できます。

+ [Machine Learning Server のドキュメント](https://docs.microsoft.com/r-server/)

+ [R および RevoScaleR について調べる](https://docs.microsoft.com/r-server/r/tutorial-r-to-revoscaler)

+ [チャンク アルゴリズムを記述する](https://docs.microsoft.com/r-server/r/how-to-developer-write-chunking-algorithms)

+ [ビッグデータを使用した R でのコンピューティング](https://docs.microsoft.com/r-server/r/tutorial-large-data-tips)

+ [独自の並列アルゴリズムを開発する](https://docs.microsoft.com/r-server/r-reference/revopemar/pemar)

