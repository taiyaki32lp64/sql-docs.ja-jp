---
title: スタンドアロン Machine Learning Server または R Server とは
description: SQL Server セットアップでのスタンドアロン R Server と Machine Learning Server の概要
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/13/2019
ms.topic: overview
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 2412bfb8bcd3cacc2db2702879353b92e328b09a
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727387"
---
# <a name="what-are-standalone-machine-learning-server-or-r-server-in-sql-server"></a>SQL Server でのスタンドアロン Machine Learning Server または R Server とは
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

SQL Server では、SQL Server とは別に実行されるスタンドアロン R Server または Machine Learning Server のインストールのサポートが提供されます。 SQL Server のバージョンに応じて、スタンドアロン サーバーにはオープンソースの R および場合によっては Python の基盤があり、その上に大規模な統計分析や予測分析を追加する、Microsoft のハイ パフォーマンス ライブラリが準備されています。 ライブラリは、R または Python スクリプトで作成された機械学習タスクも有効にします。 

SQL Server 2016 では、この機能は **R Server (スタンドアロン)** と呼ばれ、R のみでした。 SQL Server 2017 では、これは **Machine Learning Server (スタンドアロン)** と呼ばれ、R と Python の両方が含まれています。  

> [!Note]
> SQL Server のセットアップによってインストールされたスタンドアロン サーバーは、SQL の名前のないバージョンの [Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server) と機能的に同等であり、リモート実行、操作化と Web サービス、R および Python ライブラリの完全なコレクションなど、同じユーザー シナリオをサポートします。

## <a name="components"></a>Components

SQL Server 2016 は R のみです。 SQL Server 2017 では、R と Python がサポートされています。 次の表では、各バージョンの機能について説明します。

| コンポーネント | [説明] |
|-----------|-------------|
| R パッケージ | [**RevoScaleR**](ref-r-revoscaler.md) は、データ操作、変換、視覚化、および分析を行うための機能を備えた、スケーラブルな R のためのプライマリ ライブラリです。  <br/>[**MicrosoftML**](ref-r-microsoftml.md) は、機械学習アルゴリズムを追加して、テキスト分析、画像分析、感情分析のためのカスタム モデルを作成します。 <br/>[**sqlRUtils**](ref-r-sqlrutils.md) には、R スクリプトを T-SQL ストアド プロシージャに配置したり、ストアド プロシージャをデータベースに登録したり、R 開発環境からストアド プロシージャを実行したりするためのヘルパー関数が用意されています。<br/>[**mrsdeploy**](operationalization-with-mrsdeploy.md) では、Web サービスのデプロイが提供されます (SQL Server 2017 のみ)。 <br/>[**olapR**](ref-r-olapr.md) は、R で MDX クエリを指定するためのものです。|
| Microsoft R Open (MRO) | [**MRO**](https://mran.microsoft.com/open) は、Microsoft による R のオープンソース ディストリビューションです。パッケージとインタープリターが含まれています。 セットアップでバンドルされているバージョンの MRO を常に使用してください。 |
| R ツール | R コンソールのウィンドウとコマンド プロンプトは、R ディストリビューションの標準ツールです。 これらは、\Program files\Microsoft SQL Server\140\R_SERVER\bin\x64 で見つかります。 |
| R のサンプルとスクリプト |  オープンソースの R パッケージと RevoScaleR パッケージには、事前にインストールされたデータを使用してスクリプトを作成して実行するための組み込みデータセットが含まれています。 これらのデータは、\Program files\Microsoft SQL Server\140\R_SERVER\library\datasets および \library\RevoScaleR で探してください。 |
| Python パッケージ | [**revoscalepy**](../python/ref-py-revoscalepy.md) は、データ操作、変換、視覚化、および分析を行うための機能を備えた、スケーラブルな Python のためのプライマリ ライブラリです。 <br/>[**microsoftml**](../python/ref-py-microsoftml.md) は、機械学習アルゴリズムを追加して、テキスト分析、画像分析、感情分析のためのカスタム モデルを作成します。  |
| Python ツール | 組み込みの Python コマンドライン ツールは、アドホック テストやタスクに役立ちます。 このツールは、\Program files\Microsoft SQL Server\140\PYTHON_SERVER\python.exe で見つかります。 |
| Anaconda | Anaconda は、Python および必須パッケージのオープンソース ディストリビューションです。 |
| Python のサンプルとスクリプト | R と同様に、Python には組み込みのデータセットとスクリプトが含まれています。 revoscalepy データは、\Program files\Microsoft SQL Server\140\PYTHON_SERVER\lib\site-packages\revoscalepy\data\sample-data で見つかります。 |
| R と Python の事前トレーニング済みのモデル | 事前トレーニング済みのモデルは、特定のユース ケースに対して作成され、Microsoft のデータ サイエンス エンジニアリング チームによって管理されます。 事前トレーニング済みのモデルをそのまま使用することで、提供した新しいデータ入力を使用して、テキスト内で肯定的および否定的な感情をスコアリングしたり、画像の特徴を検出したりできます。 事前トレーニング済みのモデルは、スタンドアロン サーバーでサポートされていて使用可能ですが、SQL Server セットアップを使用してインストールすることはできません。 詳細については、「[SQL Server で事前トレーニング済みの機械学習モデルをインストールする](../install/sql-pretrained-models-install.md)」を参照してください。 |

## <a name="using-a-standalone-server"></a>スタンドアロン サーバーを使用する

R と Python の開発者は、通常、オープンソースの R および Python のメモリと処理の制約を超えるために、スタンドアロン サーバーを選択します。 スタンドアロン サーバーで実行されている R および Python ライブラリは、大量のデータを複数のコアで読み込んで処理し、結果を 1 つの統合された出力に集約できます。 ハイ パフォーマンスの関数は、スケールとユーティリティの両方のために設計されています。それは Microsoft が設計およびサポートしている商用サーバー製品において、予測分析、統計モデリング、データの視覚化、および最先端の機械学習アルゴリズムを提供します。

SQL Server から切り離された独立したサーバーとして、R および Python 環境は、SQL Server ではなくスタンドアロン サーバーに用意されているオペレーティング システム基盤と標準ツールを使用して構成、セキュリティ保護、およびアクセスされます。 SQL Server リレーショナル データの組み込みサポートはありません。 SQL Server データを使用する場合は、任意のクライアントからの場合と同様に、データ ソース オブジェクトおよび接続を作成できます。

SQL Server の付属物として、スタンドアロン サーバーは、ローカルとリモートの両方のコンピューティングが必要な場合に、強力な開発環境としても役立ちます。 スタンドアロン サーバー上の R および Python パッケージは、データベース エンジンのインストールで提供されるものと同じであり、コードの移植性を確保して、[コンピューティング コンテキストの切り替え](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-compute-context)を可能にします。

## <a name="how-to-get-started"></a>開始する方法

セットアップを開始し、お気に入りの開発ツールにバイナリ ファイルをアタッチして、最初のスクリプトを記述します。

### <a name="step-1-install-the-software"></a>手順 1:ソフトウェアをインストールする

次のいずれかのバージョンをインストールします。

+ [SQL Server 2017 Machine Learning Server (スタンドアロン)](../install/sql-machine-learning-standalone-windows-install.md)
+ [SQL Server 2016 R Server (スタンドアロン) - R のみ](../install/sql-r-standalone-windows-install.md)

### <a name="step-2-configure-a-development-tool"></a>手順 2:開発ツールを構成する

スタンドアロン サーバーでは、同じコンピューターにインストールされている開発環境を使用してローカルで作業するのが一般的です。

+ [R ツールの設定](set-up-a-data-science-client.md)
+ [Python ツールの設定](../python/setup-python-client-tools-sql.md)

### <a name="step-3-write-your-first-script"></a>手順 3:最初のスクリプトを作成する

RevoScaleR、revoscalepy、および機械学習アルゴリズムの関数を使用して、R または Python スクリプトを記述します。
  
  + [25 個の関数で R と RevoScaleR を探索する](https://docs.microsoft.com/machine-learning-server/r/tutorial-r-to-revoscaler):基本的な R コマンドから始めて、R ソリューションにハイ パフォーマンスとスケーリングを提供する、RevoScaleR の再頒布可能な分析関数に進みます。 最も一般的な R モデリング パッケージ (K-平均法クラスタリング、デシジョン ツリー、デシジョン フォレストなど) の並列化可能なバージョンの多くと、データ操作のツールを含みます。

  + [クイックスタート: microsoftml Python パッケージを使用した二項分類の例](https://docs.microsoft.com/machine-learning-server/python/quickstart-binary-classification-with-microsoftml):microsoftml の関数と周知の乳がんデータセットを使用して、二項分類モデルを作成します。

タスクに最適な言語を選択します。 R は、SQL を使用して実装するのが困難な統計計算に最適です。 データに対するセット ベースの処理の場合は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の機能を活用して最大のパフォーマンスを実現します。 列の計算を非常に高速で行うには、メモリ内データベース エンジンを使用します。

### <a name="step-4-operationalize-your-solution"></a>手順 4:ソリューションを操作化する

スタンドアロン サーバーでは、SQL 以外の [Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server) の[操作化](https://docs.microsoft.com//machine-learning-server/what-is-operationalization)機能を使用できます。 操作化のためのスタンドアロン サーバーを構成できます。これにより、コードを Web サービスとしてデプロイしてホストし、診断を実行し、Web サービスのキャパシティをテストするという利点が得られます。

### <a name="step-5-maintain-your-server"></a>手順 5:サーバーの保守

SQL Server は、累積的な更新プログラムを定期的にリリースします。 累積的な更新プログラムを適用すると、既存のインストールにセキュリティと機能強化が追加されます。 

新機能または変更された機能の説明については、「[CAB のダウンロード](../install/sql-ml-cab-downloads.md)」に関する記事、ならびに「[SQL Server 2016 の累積的な更新プログラム](https://support.microsoft.com/help/3177312/sql-server-2016-build-versions)」および「[SQL Server 2017 の累積的な更新プログラム](https://support.microsoft.com/help/4047329)」に関する Web ページを参照してください。 

既存のインスタンスに更新プログラムを適用する方法の詳細については、「インストール手順の[更新プログラムの適用](../install/sql-machine-learning-standalone-windows-install.md#apply-cu)」を参照してください。

## <a name="see-also"></a>参照

 [R Server (スタンドアロン) または Machine Learning Server (スタンドアロン) のインストール](../install/sql-machine-learning-standalone-windows-install.md)に関する記事

