---
title: Python のチュートリアル:ユーザーのカテゴリー化
description: この 4 部構成のチュートリアル シリーズでは、SQL Server Machine Learning Services で Python を使用した SQL データベースで K-Means アルゴリズムを使用して、顧客のクラスタリングを実行します。
ms.prod: sql
ms.technology: machine-learning
ms.devlang: python
ms.date: 08/30/2019
ms.topic: tutorial
author: garyericson
ms.author: garye
ms.reviewer: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 245a1566bfbbf19821323d0b474669eaba1d2e6e
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727075"
---
# <a name="tutorial-categorizing-customers-using-k-means-clustering-with-sql-server-machine-learning-services"></a>チュートリアル:SQL Server Machine Learning Services と K-Means クラスタリングを使用して顧客を分類する

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

この 4 部構成のチュートリアル シリーズでは、Python を使用して、[SQL Server Machine Learning Services](../what-is-sql-server-machine-learning.md) で K-Means クラスタリング モデルを開発および展開して、顧客データをクラスター化します。

このシリーズの第 1 部では、チュートリアルの前提条件を設定してから、サンプル データセットを SQL データベースに復元します。 このシリーズの後半では、このデータを使用して、SQL Server Machine Learning Services を使用する Python でクラスタリング モデルをトレーニングし展開します。

このシリーズの第 2 部と第 3 部では、Azure Data Studio ノートブックでいくつかの Python スクリプトを開発して、データを準備し、機械学習モデルをトレーニングします。 次に第 4 部では、ストアド プロシージャを使用して、SQL データベース内でこれらの Python スクリプトを実行します。

*クラスター化*は、グループのメンバーにある意味で類似点があるグループにデータを編成すること、として説明できます。 このチュートリアル シリーズでは、小売事業を営んでいる場合を想定しています。 **K-Means** アルゴリズムを使用して、製品の購入と返品のデータセット内で、顧客のクラスタリングを実行します。 顧客をクラスタリングすることで、特定のグループをターゲットして、マーケティングの取り組みをより効果的に進めることができます。
K-Means クラスタリングは、類似性に基づいてデータのパターンを探す*教師なし学習*アルゴリズムです。

この記事では、次の方法について学習します。

> [!div class="checklist"]
> * サンプル データベースを SQL Server インスタンスに復元する

[第 2 部](python-clustering-model-prepare-data.md)では、SQL データベースからデータを準備してクラスタリングを実行する方法を学びます。

[第 3 部](python-clustering-model-build.md)では、Python で K-Means クラスタリング モデルを作成し、トレーニングする方法を学びます。

[第 4 部](python-clustering-model-deploy.md)では、新しいデータに基づいて Python でクラスタリングを実行できるストアド プロシージャを SQL データベースに作成する方法について説明します。

## <a name="prerequisites"></a>Prerequisites

* [SQL Server Machine Learning Services](../what-is-sql-server-machine-learning.md) に Python 言語オプションがあること。[Windows インストール ガイド](../install/sql-machine-learning-services-windows-install.md)または [Linux インストール ガイド](https://docs.microsoft.com/sql/linux/sql-server-linux-setup-machine-learning?toc=%2fsql%2fadvanced-analytics%2ftoc.json&view=sql-server-linux-ver15)に記載されているインストール手順に従ってください。

* Python IDE - このチュートリアルは、[Azure Data Studio](../../azure-data-studio/what-is.md) で Python のノートブックを使用します。 詳細については、「[Azure Data Studio でノートブックを使用する方法](../../azure-data-studio/sql-notebooks.md)」を参照してください。 Jupyter Notebook や [Visual Studio Code](https://code.visualstudio.com/docs) などの独自の Python IDE を使用することもできます。これには [Python 拡張機能](https://marketplace.visualstudio.com/items?itemName=ms-python.python)と [MSSQL 拡張機能](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql)を使用します。

* [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) パッケージ - **revoscalepy** パッケージは SQL Server Machine Learning Services に含まれています。 クライアント コンピューターでパッケージを使用するには、このパッケージをローカルにインストールするオプションについて、「[Python 開発用のデータ サイエンス クライアントのセットアップ](../python/setup-python-client-tools-sql.md)」を参照してください。

  Azure Data Studio で Python のノートブックを使用している場合は、**revoscalepy** を使用するために次の追加の手順に従います。

  1. Azure Data Studio を開きます
  1. **[ファイル]** メニューから、 **[基本設定]** を選択し、次に **[設定]** を選択します
  1. **[拡張機能]** を展開し、 **[Notebook の構成]** を選択します
  1. **[Python パス]** に、ライブラリをインストールしたパス (たとえば `C:\path-to-python-for-mls`) を入力します
  1. **[既存の Python を使用]** がチェックされていることを確認してください
  1. Azure Data Studio を再起動します

  別の Python IDE を使用している場合は、IDE に対して同様の手順を踏んでください。

* SQL クエリ ツール - このチュートリアルでは、[Azure Data Studio](../../azure-data-studio/what-is.md) を使用していることを前提としています。 [SQL Server Management Studio](../../ssms/sql-server-management-studio-ssms.md) (SSMS) を使用することもできます。

* 追加の Python パッケージ - このチュートリアル シリーズの例では、インストールされていない Python パッケージを使用する可能性があります。 次の **pip** コマンドを使用して、必要に応じてこれらのパッケージをインストールします。

  ```console
  pip install matplotlib
  pip install scipy
  pip install sklearn
  ```

## <a name="restore-the-sample-database"></a>サンプル データベースを復元する

このチュートリアルで使用するサンプル データセットは、ダウンロードして使用できるように **.bak** データベース バックアップ ファイルに保存されています。 このデータセットは、[トランザクション処理性能評議会 (TPC)](http://www.tpc.org/default.asp) によって提供される [tpcx-bb](http://www.tpc.org/tpcx-bb/default.asp) データセットから派生しています。

1. [tpcxbb_1gb.bak](https://sqlchoice.blob.core.windows.net/sqlchoice/static/tpcxbb_1gb.bak) ファイルをダウンロードします。

1. Azure Data Studio で、以下の詳細情報を使用して、「[バックアップ ファイルからデータベースを復元する](../../azure-data-studio/tutorial-backup-restore-sql-server.md#restore-a-database-from-a-backup-file)」に記載されている手順に従います。

   * ダウンロードした **tpcxbb_1gb.bak** ファイルからインポートします
   * ターゲット データベースに "tpcxbb_1gb" という名前を指定します

1. **dbo.customer** テーブルに対してクエリを実行することで、データベースを復元した後にデータセットが存在することを確認できます。

    ```sql
    USE tpcxbb_1gb;
    SELECT * FROM [dbo].[customer];
    ```

## <a name="clean-up-resources"></a>リソースをクリーンアップする

このチュートリアルを続行しない場合は、SQL Server から tpcxbb_1gb データベースを削除してください。

## <a name="next-steps"></a>次の手順

このチュートリアル シリーズの第 1 部では、これらの手順を完了しました。

* サンプル データベースを SQL Server インスタンスに復元する

機械学習モデル用にデータを準備するには、このチュートリアル シリーズの第 2 部の手順を実行します。

> [!div class="nextstepaction"]
> [チュートリアル: SQL Server Machine Learning Services を使用して Python でクラスター化を実行するためのデータを準備する](python-clustering-model-prepare-data.md)
