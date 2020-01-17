---
title: pip を使用した Python パッケージのインストール
description: Python pip を使用して SQL Server Machine Learning Services のインスタンスに新しい Python パッケージをインストールする方法について説明します。
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/22/2019
ms.topic: conceptual
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions'
ms.openlocfilehash: 2e3452a6aad04d0d524e4eb0e6bd473fd39a2bf7
ms.sourcegitcommit: 8cb26b7dd40280a7403d46ee59a4e57be55ab462
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/17/2019
ms.locfileid: "72542152"
---
# <a name="install-python-packages-with-sqlmlutils"></a>sqlmlutils を使用した Python パッケージのインストール

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

この記事では、[**sqlmlutils**](https://github.com/Microsoft/sqlmlutils) パッケージの関数を使用して SQL Server Machine Learning Services のインスタンスに新しい Python パッケージをインストールする方法について説明します。 インストールするパッケージは、[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) T-SQL ステートメントを使用してデータベース内で実行されている Python スクリプトで使用できます。

パッケージの場所とインストール パスの詳細については、「[Get Python package information](../package-management/python-package-information.md)」(Python パッケージ情報の取得) を参照してください。

> [!NOTE]
> SQL Server に Python パッケージを追加する際に、標準の Python `pip install` コマンドは推奨されません。 代わりに、この記事で説明しているように **sqlmlutils** を使用します。

## <a name="prerequisites"></a>Prerequisites

+ Python 言語オプションと共に [SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) がインストールされている必要があります。

+ SQL Server への接続に使用するクライアント コンピューターに [python](https://www.python.org/) をインストールします。 また、[Python の拡張機能](https://marketplace.visualstudio.com/items?itemName=ms-python.python)と共に [Visual Studio Code](https://code.visualstudio.com/download) などの Python 開発環境も必要になる場合があります。 

+ SQL Server への接続に使用するクライアント コンピューターに [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/what-is) または [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms) (SSMS) をインストールします。 他のデータベース管理ツールまたはクエリ ツールを使用することもできますが、この記事では Azure Data Studio または SSMS を想定しています。

### <a name="other-considerations"></a>その他の考慮事項

+ パッケージは Python 3.5 に準拠し、Windows で実行する必要があります。

+ Python パッケージ ライブラリは SQL Server インスタンスの Program Files フォルダー内にあります。既定では、このフォルダーにインストールするには管理者権限が必要です。 詳細については、[パッケージ ライブラリの場所](../package-management/python-package-information.md#default-python-library-location)に関するページを参照してください。

+ パッケージのインストールはインスタンス単位です。 Machine Learning Services のインスタンスが複数ある場合は、各インスタンスにパッケージを追加する必要があります。

+ パッケージを追加する前に、パッケージが SQL Server 環境に適しているかどうかを検討してください。

  + データベースをクエリするだけのタスクではなく、データベース エンジンとの緊密な統合からメリットが得られるタスク (機械学習など) には、データベース内の Python を使用することをお勧めします。

  + サーバーに対して計算の負荷が大きくなるパッケージを追加すると、パフォーマンスが低下します。

  + セキュリティが強化された SQL Server 環境では、次のパッケージを避けることをお勧めします。
    + ネットワーク アクセスを必要とするパッケージ
    + 管理者特権でのファイル システム アクセスが必要なパッケージ
    + SQL Server 内部で実行しても効果のない Web 開発などのタスクに使用されるパッケージ

## <a name="install-sqlmlutils-on-the-client-computer"></a>クライアント コンピューターへの sqlmlutils のインストール

**sqlmlutils** を使用するには、まず、SQL Server への接続に使用するクライアント コンピューターにインストールする必要があります。

1. 最新の **sqlmlutils** zip ファイルを https://github.com/Microsoft/sqlmlutils/tree/master/Python/dist からクライアント コンピューターにダウンロードします。 ファイルは解凍しないでください。

1. **コマンド プロンプト** を開き、次のコマンドを実行して **sqlmlutils** パッケージをインストールします。 ダウンロードした **sqlmlutils** zip ファイルの完全なパスに置き換えます。この例では、ダウンロードしたファイルが `c:\temp\sqlmlutils_0.6.0.zip` であることを想定しています。

   ```console
   pip install --upgrade --upgrade-strategy only-if-needed c:\temp\sqlmlutils_0.6.0.zip
   ```

## <a name="add-a-python-package-on-sql-server"></a>SQL Server への Python パッケージのインストール

次の例では、SQL Server に[テキスト ツール](https://pypi.org/project/text-tools/) パッケージを追加します。

### <a name="add-the-package-online"></a>オンラインでのパッケージの追加

SQL Server への接続に使用するクライアント コンピューターがインターネットにアクセスできる場合は、**sqlmlutils** を使用して、**テキスト ツール** パッケージ、およびインターネット経由のすべての依存関係を検索し、SQL Server インスタンスにパッケージをリモートでインストールすることができます。

1. クライアント コンピューターで、**Python** または Python 環境を開きます。

1. 次のコマンドを使用して、**テキスト ツール** パッケージをインストールします。 独自の SQL Server データベース接続情報に置き換えます (Windows 認証を使用しない場合は、`uid` パラメーターと `pwd` パラメーターを追加します)。

   ```python
   import sqlmlutils
   connection = sqlmlutils.ConnectionInfo(server="yourserver", database="yourdatabase")
   sqlmlutils.SQLPackageManager(connection).install("text-tools")
   ```

### <a name="add-the-package-offline"></a>オフラインでのパッケージの追加

SQL Server への接続に使用するクライアント コンピューターにインターネット接続がない場合は、インターネットにアクセスできるコンピューターで **pip** を使用して、パッケージとそのすべての依存パッケージをローカル フォルダーにダウンロードできます。 次に、パッケージをオフラインでインストールできるクライアント コンピューターにフォルダーをコピーします。

#### <a name="on-a-computer-with-internet-access"></a>インターネットに接続されているコンピューター

1. **コマンド プロンプト**を開き、次のコマンドを実行して、**テキスト ツール** パッケージを含むローカル フォルダーを作成します。 この例では、フォルダー `c:\temp\text-tools` を作成します。

   ```console
   pip download text-tools -d c:\temp\text-tools
   ```

1. `text-tools` フォルダーをクライアント コンピューターにコピーします。 次の例では、`c:\temp\packages\text-tools` にコピーしたことを想定しています。

#### <a name="on-the-client-computer"></a>クライアント コンピューター上

**sqlmlutils** を使用して、**pip** で作成した、ローカル フォルダー内にある各パッケージ (WHL ファイル) をインストールします。 パッケージはどのような順序でインストールしてもかまいません。

この例では、**テキスト ツール**に依存関係がないので、インストールする `text-tools` フォルダー内のファイルは 1 つのみです。 これに対し、**scikit-plot** のようなパッケージには 11 個の依存関係があるため、フォルダー内に 12 個のファイル (**scikit-plot** パッケージと 11 個の依存パッケージ) があり、それぞれをインストールします。

次の Python スクリプトを実行します。 パッケージの実際のファイル パスと名前、および独自の SQL Server データベース接続情報に置き換えます (Windows 認証を使用しない場合は、`uid` パラメーターと `pwd` パラメーターを追加します)。 フォルダー内のパッケージ ファイルごとに `sqlmlutils.SQLPackageManager` ステートメントを繰り返します。

```python
import sqlmlutils
connection = sqlmlutils.ConnectionInfo(server="yourserver", database="yourdatabase")
sqlmlutils.SQLPackageManager(connection).install("c:/temp/packages/text-tools/text_tools-1.0.0-py3-none-any.whl")
```

## <a name="use-the-package-in-sql-server"></a>SQL Server でのパッケージの使用

これで、SQL Server の Python スクリプトでパッケージを使用できるようになりました。 例:

```python
EXECUTE sp_execute_external_script
  @language = N'Python',
  @script = N'
from text_tools.finders import find_best_string
corpus = "Lorem Ipsum text"
query = "Ipsum"
first_match = find_best_string(query, corpus)
print(first_match)
  '
```

## <a name="remove-the-package-from-sql-server"></a>SQL Server からのパッケージの削除

**テキスト ツール** パッケージを削除する場合は、前に定義したのと同じ接続変数を使用して、クライアント コンピューターで次の Python コマンドを使用します。

```python
sqlmlutils.SQLPackageManager(connection).uninstall("text-tools")
```

## <a name="see-also"></a>参照

+ SQL Server Machine Learning Services にインストールされている Python パッケージに関する情報を表示するには、「[Get Python package information](../package-management/python-package-information.md)」(Python パッケージ情報の取得) を参照してください。

+ SQL Server Machine Learning Services への R パッケージのインストールについては、[SQL Server への新しい R パッケージのインストール](../r/install-additional-r-packages-on-sql-server.md)に関するページを参照してください。
