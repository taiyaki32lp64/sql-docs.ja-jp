---
title: SQL Server Machine Learning Services の新機能
titleSuffix: ''
description: SQL Server Machine Learning Services および SQL Server 2016 R Services の各リリースの新機能に関するお知らせ。
ms.date: 11/04/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: sqlseattle
ms.prod: sql
ms.technology: machine-learning
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 3e21dfe719f40165e0e68e7bf6242c526c298eb4
ms.sourcegitcommit: b4ad3182aa99f9cbfd15f4c3f910317d6128a2e5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/06/2019
ms.locfileid: "73707437"
---
# <a name="whats-new-in-sql-server-machine-learning-services"></a>SQL Server Machine Learning Services の新機能

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

データ プラットフォーム、高度な分析、データ サイエンスの間の統合を継続的に拡大、拡張、強化するために、機械学習機能は、SQL Server の各リリースに追加されています。 

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
## <a name="new-in-sql-server-2019"></a>SQL Server 2019 の新機能

このリリースでは、SQL Server での Python および R の機械学習操作に対して最も要望の多かった機能が追加されています。 このリリースのすべての機能の詳細については、[SQL Server 2019 の新機能](../sql-server/what-s-new-in-sql-server-ver15.md)に関するページ、および「[SQL Server 2019 のリリース ノート](../sql-server/sql-server-ver15-release-notes.md)」を参照してください。

> [!NOTE]
> SQL Server 2019 の Java の新機能に関するドキュメントについては、「[SQL Server 言語拡張機能の新機能](https://docs.microsoft.com/sql/language-extensions/language-extensions-whats-new)」を参照してください。

SQL Server Machine Learning Services の新機能を次に示します。

- [Python または R スクリプトから SQL Server へのループバック接続](connect/loopback-connection.md)が、Windows と Linux の両方でサポートされるようになりました。 
- Windows および Linux で、R および Python 用の [CREATE EXTERNAL LIBRARY (Transact-SQL)](../t-sql/statements/create-external-library-transact-sql.md) がサポートされるようになりました。
- Linux プラットフォームで R および Python の機械学習がサポートされるようになりました。 [Linux で SQL Server Machine Learning Services のインストール](../linux/sql-server-linux-setup-machine-learning.md)を開始します。
- [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) によって、パーティション分割されたデータから複数のモデルを簡単に生成できる 2 つの新しいパラメーターが導入されています。 詳細については、[R でパーティションベースのモデルの作成](tutorials/r-tutorial-create-models-per-partition.md)のチュートリアルを参照してください。
- すべてのノードで SQL Server Launchpad サービスが開始されていることを前提として、フェールオーバー クラスターが Windows および Linux でサポートされるようになりました。 詳細については、「[SQL Server フェールオーバー クラスターのインストール](../sql-server/failover-clusters/install/sql-server-failover-cluster-installation.md)」を参照してください。
::: moniker-end

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
## <a name="new-in-sql-server-2017"></a>SQL Server 2017 の新機能

このリリースでは [Python サポートと業界をリードする機械学習アルゴリズム](https://cloudblogs.microsoft.com/sqlserver/2017/04/19/python-in-sql-server-2017-enhanced-in-database-machine-learning/)が追加されています。 SQL Server 2017 は、新しいスコープを反映するように名前が変更され、[SQL Server Machine Learning Services (データベース内)](what-is-sql-server-machine-learning.md) の導入と、Python と R の両方の言語サポートが示されています。 

すべての機能に関する発表については、[SQL Server 2017 の新機能](../sql-server/what-s-new-in-sql-server-2017.md)に関するページを参照してください。

### <a name="r-enhancements"></a>R の機能強化

SQL Server Machine Learning Services の R コンポーネントは SQL Server 2016 R Services の次世代で、基本の R、RevoScaler、およびその他のパッケージの更新バージョンが含まれています。

R の新機能には、次のような特徴を持つ[**パッケージ管理**](r/install-additional-r-packages-on-sql-server.md)が含まれます。 

+ データベース ロールは、DBA がパッケージを管理したり、パッケージのインストールにアクセス許可を割り当てたりするのに役立ちます。
+ [CREATE EXTERNAL LIBRARY](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) は、DBA が使い慣れた T-SQL 言語でパッケージを管理するのに役立ちます。
+ [RevoScaleR](r/use-revoscaler-to-manage-r-packages.md) 関数は、ユーザーが所有するパッケージをインストール、削除、または一覧表示するのに役立ちます。 詳細については、[RevoScaleR 関数を使用した SQL Server での R パッケージの検出またはインストール](r/use-revoscaler-to-manage-r-packages.md)に関するページを参照してください。

### <a name="r-libraries"></a>R ライブラリ

| [パッケージ] | [説明] |
|---------|-------------|
| [**MicrosoftML**](r/ref-r-microsoftml.md) | このリリースでは、MicrosoftML は既定の R インストールに含まれており、前の SQL Server 2016 R Services で必要だったアップグレード手順が不要になっています。 MicrosoftML は、最先端の機械学習アルゴリズムと、リモート計算コンテキストでスケーリングまたは実行できるデータ変換を提供します。 アルゴリズムには、カスタマイズ可能なディープ ニューラル ネットワーク、高速デシジョン ツリーとデシジョン フォレスト、線形回帰、およびロジスティック回帰が含まれます。  |

### <a name="python-integration-for-in-database-analytics"></a>データベース内分析のための Python 統合

Python は、さまざまな機械学習タスクに高い柔軟性と強力な機能を提供する言語です。 Python 用のオープンソース ライブラリには、カスタマイズ可能なニューラル ネットワーク用の複数のプラットフォームに加え、自然言語処理用の一般的なライブラリが含まれています。 

Python はデータベース エンジンと統合されているため、データの近くで分析を行い、データ移動に伴うコストとセキュリティ上のリスクを排除できます。 Visual Studio などのツールを使用して、Python に基づいた機械学習ソリューションを展開できます。 実稼働アプリケーションでは、SQL Server のデータ アクセス方法を使用して、Python 3.5 ランタイムから予測、モデル、またはビジュアルを取得できます。

T-SQL と Python の統合は、[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) システム ストアド プロシージャを通じてサポートされています。 このストアド プロシージャを使用して、任意の Python コードを呼び出すことができます。 コードは、セキュリティで保護されたデュアル アーキテクチャで実行されます。これにより、単純なストアド プロシージャを使用してアプリケーションから呼び出すことができる、Python モデルとスクリプトのエンタープライズレベルの展開が可能になります。 SQL から Python プロセスおよび MPI リング並列処理のデータをストリーミングすることで、パフォーマンスがさらに向上します。

T-SQL [PREDICT](../t-sql/queries/predict-transact-sql.md) 関数を使用すると、以前に必要なバイナリ形式で保存した事前トレーニング済みのモデルに対して[ネイティブ スコアリング](sql-native-scoring.md)を実行できます。

### <a name="python-libraries"></a>Python ライブラリ

| [パッケージ] | [説明] |
|---------|-------------|
|[**revoscalepy**](python/ref-py-revoscalepy.md)| Python で RevoScaleR に相当するもの。 線形回帰およびロジスティック回帰、デシジョン ツリー、ブースト ツリー、ランダム フォレストに対し、すべて並列化可能で、リモート計算コンテキストで実行することができる Python モデルを作成することができます。 このパッケージでは、複数のデータ ソースとリモート計算コンテキストの使用がサポートされています。 データ サイエンティストや開発者は、リモート SQL Server で Python コードを実行して、データを移動せずに、データを探索したり、モデルを構築したりすることができます。 |
|[**microsoftml**](python/ref-py-microsoftml.md) |Python で MicrosoftML R パッケージに相当するもの。 |

### <a name="pre-trained-models"></a>トレーニング済みモデル

[**事前トレーニング済みモデル**](install/sql-pretrained-models-install.md)は、Python と R の両方で使用できます。これらのモデルを使用して、イメージの認識と肯定的および否定的感情分析を行って、独自のデータに対する予測を生成します。 

### <a name="standalone-server-as-a-shared-feature-in-sql-server-setup"></a>SQL Server セットアップの共有機能としてのスタンド アロンサーバー

このリリースでは、完全に独立したデータ サイエンス サーバーである [SQL Server Machine Learning Server (スタンドアロン)](r/r-server-standalone.md)も追加され、R および Python での統計分析と予測分析がサポートされます。 R Services と同様に、このサーバーは SQL Server 2016 R Server (スタンドアロン) の次のバージョンです。 スタンドアロン サーバーを使用すると、SQL Server と依存関係のない R または Python ソリューションを配布し、スケーリングすることができます。
::: moniker-end

::: moniker range=">=sql-server-2016||=sqlallproducts-allversions"
## <a name="new-in-sql-server-2016"></a>SQL Server 2016 の新機能

このリリースでは、**SQL Server 2016 R Services** を通じて SQL Server に機械学習機能が導入されました。SQL Server 2016 R Services は、データベース エンジン インスタンス内の常駐データに対して R スクリプトを処理するためのデータベース内分析エンジンです。

また、Windows Server に Microsoft R Server をインストールする方法として、**SQL Server 2016 R Server (スタンドアロン)** がリリースされました。 当初は、SQL Server セットアップが、Microsoft R Server for Windows をインストールする唯一の方法を提供していました。 その後のリリースで、Windows 上で Microsoft R Server を必要とする開発者やデータ サイエンティストは、別のスタンドアロン インストーラーを使用して同じ目的を達成できるようになりました。 SQL Server のスタンドアロン サーバーは、スタンドアロン サーバー製品の [Microsoft R Server for Windows](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows) と機能的に同等です。

すべての機能に関する発表については、「[SQL Server 2016 の新機能](../sql-server/what-s-new-in-sql-server-2016.md)」を参照してください。

| リリース |機能更新プログラム |
|---------|----------------|
| CU の追加 | [**リアルタイム スコアリング**](real-time-scoring.md) は、ネイティブ C++ ライブラリに依存して、最適化されたバイナリ形式で格納されたモデルを読み取り、R ランタイムを呼び出すことなく予測を生成します。 これにより、スコアリング操作が大幅に高速化します。 リアルタイム スコアリングを使用すると、R コードからストアド プロシージャを実行したり、リアルタイム スコアリングを実行したりすることができます。 インスタンスが [!INCLUDE[rsql-platform-md](../includes/rsql-platform-md.md)] の最新リリースにアップグレードされている場合、リアルタイム スコアリングは SQL Server 2016 でも利用できます。 |
| 最初のリリース | [**データベース内分析のための R 統合**](r/sql-server-r-services.md)。 <br/><br/> T-SQL で R 関数を呼び出すための R パッケージ。その逆も同様です。 RevoScaleR 関数では、データをコンポーネント パーツにチャンク化し、分散処理を調整および管理し、結果を集計することによって、大規模な R 分析を提供します。 SQL Server 2016 R Services (データベース内) では、RevoScaleR エンジンがデータベース エンジンのインスタンスと統合され、データと分析が同じ処理コンテキストにまとめられます。 <br/><br/>[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) を使用した T-SQL と R の統合。 このストアド プロシージャを使用して、任意の R コードを呼び出すことができます。 このセキュリティで保護されたインフラストラクチャにより、単純なストアド プロシージャを使用してアプリケーションから呼び出すことができる、Rn モデルとスクリプトのエンタープライズレベルの展開が可能になります。 SQL から R プロセスおよび MPI リング並列処理のデータをストリーミングすることで、パフォーマンスがさらに向上します。 <br/><br/>T-SQL [PREDICT](../t-sql/queries/predict-transact-sql.md) 関数を使用すると、以前に必要なバイナリ形式で保存した事前トレーニング済みのモデルに対して[ネイティブ スコアリング](sql-native-scoring.md)を実行できます。|

::: moniker-end

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
## <a name="linux-support"></a>Linux Support

SQL Server 2019 では、データベース エンジンのインスタンスを使用して機械学習パッケージをインストールすると、R と Python に対する Linux Support が追加されます。 詳細については、[Linux に SQL Server Machine Learning Services をインストールする](../linux/sql-server-linux-setup-machine-learning.md)方法に関するページを参照してください。

Linux では、SQL Server 2017 に R または Python の統合はありませんが、Linux で[ネイティブ スコアリング](sql-native-scoring.md)を使用することができます。これは、この機能が Linux で実行される T-SQL [PREDICT](../t-sql/queries/predict-transact-sql.md) を通じて使用できるためです。 ネイティブ スコアリングにより、事前トレーニング済みモデルの高パフォーマンスなスコア付けが可能になりします。R ランタイムを呼び出すことも、必要になることもありません。
::: moniker-end

<a name="azure-sql-database-roadmap"></a>

## <a name="machine-learning-services-in-azure-sql-database"></a>Azure SQL Database の Machine Learning Services

Azure SQL Database の Machine Learning Services はパブリック プレビューの段階にあります。 詳細については、[Azure SQL Database Machine Learning Services (プレビュー)](https://docs.microsoft.com/azure/sql-database/sql-database-machine-learning-services-overview) に関するページを参照してください。

## <a name="next-steps"></a>次の手順

+ [SQL Server Machine Learning サービス (データベース内) のインストール](install/sql-machine-learning-services-windows-install.md)
+ [機械学習のチュートリアルとサンプル](tutorials/machine-learning-services-tutorials.md)
