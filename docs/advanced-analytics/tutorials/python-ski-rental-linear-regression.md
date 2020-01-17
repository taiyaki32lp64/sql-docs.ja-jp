---
title: Python のチュートリアル:スキー レンタル
description: このチュートリアルでは、SQL Server Machine Learning Services で Python と線形回帰を使用して、スキーのレンタル数を予測します。
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/03/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 927816988be8882d4149115f6d4aee38dd3a8f3f
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727036"
---
# <a name="python-tutorial-predict-ski-rental-with-linear-regression-in-sql-server-machine-learning-services"></a>Python のチュートリアル:SQL Server Machine Learning Services での線形回帰を使用したスキー レンタルの予測
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

この 4 部構成のチュートリアル シリーズでは、[SQL Server Machine Learning Services](../what-is-sql-server-machine-learning.md) で Python と線形回帰を使用して、スキーのレンタル数を予測します。 このチュートリアルでは [Azure Data Studio で Python notebook](../../azure-data-studio/sql-notebooks.md) を使用しますが、独自の Python 統合開発環境 (IDE) を使用することもできます。

たとえば、スキー レンタル事業を所有していて、将来の日付に対するレンタル数を予測したい場合を考えてみましょう。 この情報は、在庫、スタッフおよび設備の準備に役立ちます。

このシリーズのパート 1 では、前提条件を設定します。 パート 2 と 3 では、Jupyter notebook でいくつかの Python スクリプトを開発して、データを準備し、機械学習モデルをトレーニングします。 次にパート 3 では、T-SQL ストアド プロシージャを使用して、SQL Server 内でこれらの Python スクリプトを実行します。

この記事では、次の方法について学習します。

> [!div class="checklist"]
> * サンプル データベースを SQL Server にインポートする 

[パート 2](python-ski-rental-linear-regression-prepare-data.md) では、SQL Server から Python データ フレームにデータを読み込み、Python でデータを準備する方法を学習します。

[パート 3](python-ski-rental-linear-regression-train-model.md) では、Python で線形回帰モデルをトレーニングする方法について学習します。

[パート 4](python-ski-rental-linear-regression-deploy-model.md) では、モデルを SQL Server に格納し、そしてパート 2 と 3 で開発した Python スクリプトからストアド プロシージャを作成する方法について学習します。 ストアド プロシージャは、新しいデータに基づいて予測を行うために SQL Server で実行されます。

## <a name="prerequisites"></a>Prerequisites

* SQL Server Machine Learning Services - Machine Learning Services をインストールする方法については、「[Windows インストール ガイド](../install/sql-machine-learning-services-windows-install.md)」または「[Linux インストール ガイド](../../linux/sql-server-linux-setup-machine-learning.md?toc=%2Fsql%2Fadvanced-analytics%2Ftoc.json)」に関するページを参照してください。

* Python IDE - このチュートリアルでは、[Azure Data Studio](../../azure-data-studio/what-is.md)で Python notebook を使用します。 詳細については、「[Azure Data Studio で notebook を使用する方法](../../azure-data-studio/sql-notebooks.md)」を参照してください。 

    Jupyter notebook や [Visual Studio Code](https://code.visualstudio.com/docs) などの独自の Python IDE を使用することもできます。これには [Python 拡張機能](https://marketplace.visualstudio.com/items?itemName=ms-python.python) と [mssql 拡張機能](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql)を使用します。 

* [revoscalepy](../python/ref-py-revoscalepy.md) パッケージ - **revoscalepy** パッケージは SQL Server Machine Learning Services に含まれています。 クライアント コンピューターでパッケージを使用するには、このパッケージをローカルにインストールするオプションについて、「[Python 開発用のデータ サイエンス クライアントをセットアップする](../python/setup-python-client-tools-sql.md)」に関するページを参照してください。

    Azure Data Studio で Python notebook を使用している場合は、**revoscalepy** を使用するために次の追加の手順に従います。

    1. Azure Data Studio を開きます
    1. **[ファイル]** メニューから **[基本設定]** を選択し、次に **[設定]** を選択します
    1. **[拡張機能]** を展開し、 **[Notebook configuration]\(Notebook の構成\)** を選択します
    1. **[Python パス]** に、ライブラリをインストールしたパス (たとえば `C:\path-to-python-for-mls`) を入力します
    1. **[Use Existing Python]\(既存の Python を使用\)** がチェックされていることを確認してください
    1. Azure Data Studio を再起動します

    別の Python IDE を使用している場合は、IDE に対して同様の手順を踏んでください。

* SQL クエリ ツール - このチュートリアルでは、[Azure Data Studio](../../azure-data-studio/what-is.md) を使用していることを前提としています。 [SQL Server Management Studio](../../ssms/sql-server-management-studio-ssms.md) (SSMS) を使用することもできます。

* 追加の Python パッケージ - このチュートリアル シリーズの例では、インストールされていない Python パッケージを使用する可能性があります。 次の **pip** コマンドを使用して、必要に応じてこれらのパッケージをインストールします。

    ```console
    pip install pandas
    pip install sklearn
    pip install pickle
    ```

## <a name="restore-the-sample-database"></a>サンプル データベースを復元する

このチュートリアルで使用するサンプル データセットは、ダウンロードして使用できるように **.bak** データベース バックアップ ファイルに保存されています。

1. ファイル [TutorialDB.bak](https://sqlchoice.blob.core.windows.net/sqlchoice/static/TutorialDB.bak) をダウンロードします。

1. 以下の詳細情報を使用して、Azure Data Studio で「[バックアップ ファイルからデータベースを復元する](../../azure-data-studio/tutorial-backup-restore-sql-server.md#restore-a-database-from-a-backup-file)」に記載の手順に従います。

   * ダウンロードした **TutorialDB.bak** ファイルからインポートします
   * ターゲット データベースに "TutorialDB" という名前を指定します

1. **dbo.rental_data** テーブルに対してクエリを実行することで、データベースを復元した後にデータセットが存在することを確認できます。

    ```sql
    USE TutorialDB;
    SELECT * FROM [dbo].[rental_data];
    ```

## <a name="next-steps"></a>次の手順

このチュートリアル シリーズのパート 1 では、次の手順を完了しました。

* 必須コンポーネントのインストール
* サンプル データベースを SQL Server にインポートする

TutorialDB データベースからデータを準備するには、このチュートリアル シリーズのパート 2 の手順を実行します。

> [!div class="nextstepaction"]
> [Python のチュートリアル:線形回帰モデルをトレーニングするためのデータを準備する](python-ski-rental-linear-regression-prepare-data.md)