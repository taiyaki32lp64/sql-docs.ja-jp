---
title: RevoScaleR の詳細なチュートリアル
description: このチュートリアルでは、SQL Server Machine Learning R 統合を使用して RevoScaleR 関数を呼び出す方法について説明します。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 853f2e33ff4f801c3668a9f79bcec247dc13963e
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727216"
---
# <a name="tutorial-use-revoscaler-r-functions-with-sql-server-data"></a>チュートリアル:SQL Server データでの RevoScaleR R 関数の使用
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) は、データ サイエンスと機械学習のワークロードの分散および並列処理を提供する Microsoft R パッケージです。 SQL Server での R 開発の場合、**RevoScaleR** は最も重要な組み込みパッケージの 1 つで、データ ソース オブジェクトを作成するための機能、コンピューティング コンテキストの設定、パッケージの管理、および最も重要なこととして、インポートから視覚化および分析まで、データをエンドツーエンドで操作する機能を備えています。 SQL Server の Machine Learning アルゴリズムは、**RevoScaleR** データ ソースに依存しています。 **RevoScaleR** の重要性を考えると、その関数を呼び出すタイミングと方法を把握することは、重要なスキルと言えます。 

このマルチパート チュートリアルでは、データ サイエンスに関連するタスク用のさまざまな **RevoScaleR** 関数について紹介します。 このプロセスでは、リモートのコンピューティング コンテキストを作成する方法、ローカルとリモートのコンピューティング コンテキストの間でデータを移動する方法、およびリモート SQL Server で R コードを実行する方法について説明します。 また、ローカルとリモート サーバーの両方でデータを分析してプロットする方法と、モデルを作成して配置する方法についても説明します。

## <a name="prerequisites"></a>Prerequisites

+ R 機能付きの [SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md)、または [SQL Server R Services (データベース内)](../install/sql-r-services-windows-install.md)
  
+ [データベース権限](../security/user-permission.md)と SQL Server データベース ユーザー ログイン

+ [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)

+ R に付属する RStudio や組み込みの RGUI ツールなどの IDE

ローカルとリモートの両方のコンピューティング コンテキストを切り替えるには、2 つのシステムが必要です。 ローカルは、通常、データ サイエンス ワークロードのための十分なパワーを備えた開発ワークステーションです。 この場合、リモートは R 機能が有効になっている SQL Server です。 

コンピューティング コンテキストの切り替えは、ローカルとリモートの両方のシステムに同じバージョン **RevoScaleR** があることを前提としています。 ローカル ワークステーションでは、Microsoft R Client のインストールによって、**RevoScaleR** パッケージと関連するプロバイダーを取得できます。

クライアントとサーバーを同じコンピューターに配置する必要がある場合は、"リモート" クライアントから R スクリプトを送信するために、Microsoft R ライブラリの 2 つ目のセットを必ずインストールしてください。 SQL Server インスタンスのプログラム ファイルにインストールされている R ライブラリは使用しないでください。 具体的には、1 台のコンピューターを使用している場合は、クライアントとサーバーの操作をサポートするために、次の両方の場所に **RevoScaleR** ライブラリが必要です。

+ C:\Program Files\Microsoft\R Client\R_SERVER\library\RevoScaleR 
+ C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library\RevoScaleR

クライアントの構成手順については、[R 開発用にデータ サイエンス クライアントを設定する](../r/set-up-a-data-science-client.md)に関するページを参照してください。


## <a name="r-development-tools"></a>R 開発ツール

R 開発者は、R コードの作成およびデバッグに、通常 IDE を使用します。 推奨事項をいくつか以下に示します。

- **R Tools for Visual Studio** (RTVS) は、Microsoft R に対して Intellisense、デバッグ、およびサポートを提供する無料プラグインです。それを使用して、Microsoft R Server と SQL Server Machine Learning Services の両方で使用できます。 ダウンロードするには、「 [R Tools for Visual Studio](https://www.visualstudio.com/vs/rtvs/)」を参照してください。

- **RStudio** は R 開発用の最も一般的な環境の 1 つです。 詳細については、[https://www.rstudio.com/products/RStudio/](https://www.rstudio.com/products/RStudio/) を参照してください。

- R を SQL Server または R クライアントにインストールするとき、既定では、基本の R ツール (R.exe、RTerm.exe、RScripts.exe) もインストールされます。 IDE をインストールしない場合は、組み込みの R ツールを使用して、このチュートリアルでコードを実行できます。

ローカル コンピューターとリモート コンピューターの両方で **RevoScaleR** が必要であることを思い起こしてください。 Microsoft R ライブラリがない RStudio の汎用インストールまたは他の環境を使用するこのチュートリアルを完了することはできません。 詳しくは、「 [データ サイエンス クライアントのセットアップ](../r/set-up-a-data-science-client.md)」を参照してください。

## <a name="summary-of-tasks"></a>タスクの概要

+ 最初に、CSV ファイルまたは XDF ファイルからデータを取得します。 **RevoScaleR** パッケージの関数を使用して、データを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] にインポートします。
+ モデルのトレーニングとスコアリングは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のコンピューティング コンテキストを使用して実行されます。 
+ スコアリングの結果を保存するために、**RevoScaleR** 関数を使用して新しい [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブルを作成します。
+ サーバーとローカル両方のコンピューティング コンテキストで、プロットを作成します。
+ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスで R を実行して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースのデータでモデルをトレーニングします。
+ データのサブセットを抽出し、ローカル ワークステーションでの分析で再利用できるように、それを XDF ファイルとして保存します。
+ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースへの ODBC 接続を開くことで、スコアリング用の新しいデータを取得します。 スコアリングはローカル ワークステーションで実行されます。
+ カスタム R 関数を作成し、それをサーバー コンピューティング コンテキストで実行してシミュレーションを実行します。

## <a name="next-steps"></a>次の手順

> [!div class="nextstepaction"]
> [レッスン 1:データベースとアクセス許可を作成する](deepdive-work-with-sql-server-data-using-r.md)