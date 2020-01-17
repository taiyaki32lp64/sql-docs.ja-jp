---
title: SQL Notebook の使用方法
titleSuffix: Azure Data Studio
description: Azure Data Studio で SQL Notebook を使用する方法について説明します
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: achatter; alayu; maghan; sstein
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.custom: seodec18
ms.date: 06/28/2019
ms.openlocfilehash: df1e49af0378b6af4a3d82b5a5ec2a4293be5e35
ms.sourcegitcommit: 39ea690996a7390e3d13d6fb8f39d8641cd5f710
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/10/2019
ms.locfileid: "74957086"
---
# <a name="how-to-use-notebooks-in-azure-data-studio"></a>Azure Data Studio でノートブックを使用する方法

この記事では、Azure Data Studio でノートブック エクスペリエンスを起動する方法と、独自のノートブックを作成する方法について説明します。 さらに、さまざまなカーネルを使用してノートブックを作成する方法についても説明します。


## <a name="connect-to-sql-server"></a>SQL Server への接続

Azure Data Studio で Microsoft SQL Server 接続の種類に接続できます。
Azure Data Studio では、F1 キーを押して、 **[新しい接続]**  をクリックし、SQL Server に接続することもできます。

![image1](media/sql-notebooks/connection-info.png)

## <a name="launch-notebooks"></a>ノートブックを起動する

新しいノートブックを起動するには、複数の方法があります。

1. Azure Data Studio の **[ファイル] メニュー**に移動し、 **[新しいノートブック]** をクリックします。

    ![image3](media/sql-notebooks/file-new-notebook.png)

3. **[SQL Server]** 接続を右クリックして、 **[新しいノートブック]** を開始します。 
    ![image3](media/sql-notebooks/server-new-notebook.png)

4. コマンド パレット (**Ctrl + Shift + P**) を開き、 **[新しいノートブック]** に入力します。 `Notebook-1.ipynb` という名前の新しいファイルが開きます。

## <a name="supported-kernels-and-attach-to-context"></a>サポートされているカーネルとコンテキストへのアタッチ

Azure Data Studio でノートブックをインストールすると、SQL カーネルがネイティブにサポートされます。 SQL 開発者がノートブックを使用する場合は、これが選択されたカーネルになります。 

また、SQL カーネルを使用して、PostgreSQL サーバー インスタンスに接続することもできます。 PostgreSQL 開発者が PostgreSQL サーバーに接続する場合は、Azure Data Studio の拡張機能マーケットプレースで [**PostgreSQL 拡張機能**](postgres-extension.md)をダウンロードしてください。

![image7](media/sql-notebooks/sql-kernel-dropdown.png)

### <a name="sql-kernel"></a>SQL カーネル

このノートブック内のコード セルでは、クエリ エディターと同様に、最新の SQL コーディング エクスペリエンスがサポートされており、豊富な SQL エディター、IntelliSense、組み込みのコード スニペットなどの組み込みの機能を使用して、日常的なタスクを簡単に行うことができます。 コード スニペットを使用すると、データベース、テーブル、ビュー、ストアド プロシージャなどを作成するための適切な SQL 構文を生成したり、既存のデータベース オブジェクトを更新したりすることができます。 開発またはテストを目的としたデータベースのコピーをすばやく作成したり、スクリプトを生成および実行したりするには、コード スニペットを使用します。

**[実行]** をクリックして、各セルを実行します。

SQL Server インスタンスに接続する SQL カーネル

![image7](media/sql-notebooks/intellisense-code-cell.png)

クエリ結果

![image19](media/sql-notebooks/sql-cell-results.png)

PostgreSQL サーバー インスタンスに接続する SQL カーネル 

![image18](media/sql-notebooks/pgsql-code-cell.png)

クエリ結果

![image20](media/sql-notebooks/pgsql-cell-results.png)

### <a name="configure-python-for-notebooks"></a>ノートブック用の Python の構成

[カーネル] ドロップダウンから、SQL 以外の他のカーネルを選択すると、**ノートブック用に Python を構成**するよう求められます。 ノートブックの依存関係は、指定した場所にインストールされますが、インストールの場所を設定するかどうかを決めることができます。 このインストールには時間がかかる場合があるため、インストールが完了するまでアプリケーションを終了しないことをお勧めします。 インストールが完了すると、サポートされている言語でコードの記述を開始できます。

![image21](media/sql-notebooks/configure-python.png)

インストールが成功すると、出力ターミナルで実行されている Jupyter バックエンド サーバーの場所と共に、タスク履歴に通知が表示されます。

![image22](media/sql-notebooks/jupyter-backend.png)

|カーネル|[説明]
|:-----|:-----
| SQL カーネル | リレーショナル データベースを対象とした SQL コードを記述します。
|PySpark3 と PySpark カーネル| クラスターから Spark コンピューティングを使用して Python コードを作成します。
|Spark カーネル|クラスターから Spark コンピューティングを使用して Scala および R コードを作成します。
|Python カーネル|ローカル開発用の Python コードを作成します。

`Attach to` によって、アタッチするカーネルのコンテキストが提供されます。 SQL カーネルを使用している場合は、任意の SQL Server インスタンスに `Attach to` することができます。

Python3 カーネルを使用している場合、`Attach to` は `localhost` です。 このカーネルは、ローカルの Python 開発に使用できます。

SQL Server 2019 ビッグ データ クラスターに接続している場合、既定の `Attach to` がクラスターのエンド ポイントになり、クラスターの Spark コンピューティングを使用して Python、Scala、R コードを送信できるようになります。

### <a name="code-cells-and-markdown-cells"></a>コードセルと Markdown セル

ツールバーの **[+Code]** コマンドをクリックして、新しいコード セルを追加します。

ツールバーの **[+Text]** コマンドをクリックして、新しいテキスト セルを追加します。

![image8](media/sql-notebooks/notebook-toolbar.png)

セルは編集モードに変わり、「markdown」と入力すると、プレビューが同時に表示されます。

![image9](media/sql-notebooks/notebook-markdown-cell.png)

テキスト セルの外側をクリックすると、markdown テキストが表示されます。

![image10](media/sql-notebooks/notebook-markdown-preview.png)

### <a name="trusted-and-non-trusted"></a>"信頼されている" と "信頼されていない"

Azure Data Studio で開いているノートブックは、既定で**信頼されている**状態です。

他のソースからノートブックを開くと、**信頼されていない**モードで開かれます。その後、**信頼されている**状態にすることができます。

### <a name="save"></a>保存 

**Ctrl+S** キーを押すか、または [ファイル] メニューの **[保存]** 、 **[名前を付けて保存]** 、および **[すべて保存]** コマンドをクリックすると、ノートブックを保存できます。また、コマンド パレットに **[ファイル] - [保存]** コマンドを入力して保存することもできます。

### <a name="pyspark3pyspark-kernel"></a>Pyspark3/PySpark カーネル

`PySpark Kernel` を選択して、セルに次のコードを入力します。

**[実行]** をクリックします。

Spark アプリケーションが起動し、次の出力が返されます。

![image12](media/sql-notebooks/pyspark.png)

### <a name="spark-kernel--scala-language"></a>Spark カーネル | Scala 言語

`Spark|Scala Kernel` を選択して、セルに次のコードを入力します。

![image13](media/sql-notebooks/spark-scala.png)

下のオプションアイコンをクリックすると、"セル オプション" を表示することもできます。

![image14](media/sql-notebooks/scala-cell-options.png)

### <a name="spark-kernel--r-language"></a>Spark カーネル | R 言語

カーネルのドロップダウンで Spark | R を選択します。 セルにコードを入力するか、貼り付けます。 **[実行]** をクリックすると、次の出力が表示されます。

![image15](media/sql-notebooks/spark-r.png)

### <a name="local-python-kernel"></a>ローカル Python カーネル

ローカルの Python カーネルを選択し、セルに次のように入力します。

![image16](media/sql-notebooks/local-python.png)

## <a name="manage-packages"></a>パッケージの管理
ローカルの Python 開発向けに最適化されたものの 1 つは、顧客がシナリオに必要とするパッケージをインストールする機能を含めることでした。 既定では、`pandas` や `numpy` などの共通パッケージが含まれていますが、含まれていないパッケージを想定している場合は、ノートブック セルに次のコードを記述します。 

```python
import <package-name>
```

このコマンドを実行すると、`Module not found` が返されます。 パッケージが存在する場合、このエラーは表示されません。

`Module not Found` エラーが返された場合は、 **[パッケージの管理]** をクリックしてウィザード エクスペリエンスを起動します。 

![image17](media/sql-notebooks/manage-packages.png)

このウィザードでは、**インストールされている**パッケージを確認できます。 これらのパッケージの一覧と、各パッケージの関連付けられたバージョンを検索できます。 これらのパッケージのいずれかを**アンインストール**する必要がある場合は、パッケージのいずれかをクリックし、 **[選択したパッケージをアンインストールする]** オプションをクリックします。

また、パッケージの **[新規追加]** をクリックして、特定のパッケージを **[検索]** し、関連するバージョンを選択して、 **[インストール]** をクリックすることもできます。 既定では、検索したパッケージの最新バージョンが選択されます。 

パッケージがインストールされたら、ノートブック セルに移動して、次のコマンドを入力することができます。

```python
import <package-name>
```

これらのパッケージのいずれかを**アンインストール**する必要がある場合は、1 つ以上のパッケージをクリックし、 **[選択したパッケージをアンインストールする]** オプションをクリックします。

## <a name="next-steps"></a>次のステップ

既存のノートブックを操作する方法については、「[Azure Data Studio でノートブックを管理する方法](https://docs.microsoft.com/sql/big-data-cluster/notebooks-how-to-manage?view=sqlallproducts-allversions)」を参照してください。