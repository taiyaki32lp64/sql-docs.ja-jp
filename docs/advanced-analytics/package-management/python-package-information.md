---
title: Python パッケージ情報の取得
description: SQL Server Machine Learning Services にインストールした Python パッケージのバージョンやインストール場所などの情報を取得する方法について説明します。
ms.custom: ''
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/22/2019
ms.topic: conceptual
author: garyericson
ms.author: garye
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 1aa12da4a138ea8f292fa8b64db00456d3c35fe3
ms.sourcegitcommit: 01c8df19cdf0670c02c645ac7d8cc9720c5db084
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/23/2019
ms.locfileid: "70000450"
---
# <a name="get-python-package-information"></a>Python パッケージ情報の取得

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

この記事では、SQL Server Machine Learning Services にインストールした Python パッケージのバージョンやインストール場所などの情報を取得する方法について説明します。 Python のスクリプト例では、インストール パスやバージョンなどのパッケージ情報を一覧表示する方法を示しています。

## <a name="default-python-library-location"></a>Python ライブラリの既定の場所

SQL Server と共に機械学習をインストールすると、インストールした言語ごとに 1 つのパッケージ ライブラリがインスタンス レベルで作成されます。 このインスタンス ライブラリは、Windows では SQL Server に登録されているセキュリティで保護されたフォルダーです。

SQL Server のデータベース内で実行されるすべてのスクリプトまたはコードは、このインスタンス ライブラリから関数を読み込む必要があります。 SQL Server は、他のライブラリにインストールされているパッケージにはアクセスできません。 これはリモート クライアントにも当てはまります。サーバーの計算のコンテキストで実行されているすべての Python コードは、インスタンス ライブラリにインストールされているパッケージしか使用できません。
既定のインスタンス ライブラリは、サーバーの資産を保護するために、コンピューターの管理者のみが変更できるようになっています。

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
Python のバイナリの既定のパスは次のとおりです。

`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES`
::: moniker-end

::: moniker range=">sql-server-2017||=sqlallproducts-allversions"
Python のバイナリの既定のパスは次のとおりです。

`C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\PYTHON_SERVICES`
::: moniker-end

既定の SQL インスタンスは、MSSQLSERVER と想定されています。 SQL Server がユーザー定義の名前付きインスタンスとしてインストールされている場合、代わりにその指定の名前を使用します。

次のステートメントを実行すると、現在のインスタンスの既定のライブラリを確認することができます。 この例では、Python の `sys.path` 変数に含まれるフォルダーの一覧が返されます。 一覧には、現在のディレクトリと標準ライブラリ パスが含まれています。

```sql
EXECUTE sp_execute_external_script
  @language =N'Python',
  @script=N'import sys; print("\n".join(sys.path))'
```

変数 `sys.path` の詳細と、これを使用したモジュールのインタープリターの検索パスの設定方法については、[モジュールの検索パス](https://docs.python.org/2/tutorial/modules.html#the-module-search-path)に関する記事を参照してください。

## <a name="default-python-packages"></a>Python の既定のパッケージ

セットアップ時に Python の機能を選択すると、SQL Server Machine Learning Services と共に次の Python パッケージがインストールされます。

| パッケージ | Version |  [説明] |
| ---------|---------|--------------|
| [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) | 9.2 | リモートでの計算のコンテキスト、ストリーミング、データのインポートと変換、モデリング、視覚化、および分析での rx 関数の並列実行で使用します。 |
| [microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) | 9.2 | Python に機械学習アルゴリズムを追加します。 |

### <a name="component-upgrades"></a>コンポーネントのアップグレード

既定で Python パッケージは、サービス パックと累積的な更新プログラムで更新されます。 その他のパッケージおよび Python のコア コンポーネントのバージョンの完全アップグレードは、製品のアップグレード、または Microsoft Machine Learning Server に Python サポートをバインドすることによってのみ可能です。

詳細については、[SQL Server での R および Python コンポーネントのアップグレード](../install/upgrade-r-and-python.md)に関する記事を参照してください。

## <a name="default-open-source-python-packages"></a>既定のオープンソースの Python パッケージ

セットアップ時に Python の言語オプションを選択すると、(Python 3.5 に) Anaconda 4.2 のディストリビューションがインストールされます。 標準インストールには、Python のコード ライブラリに加え、サンプル データ、単体テスト、およびサンプル スクリプトが含まれます。

> [!IMPORTANT]
> SQL Server のセットアップでインストールされた Python のバージョンは、手動で Web 上の新しいバージョンに上書きしないでください。 Microsoft Python のパッケージは、特定のバージョンの Anaconda に基づいています。 インストールを変更すると、それが不安定になる可能性があります。

## <a name="list-all-installed-python-packages"></a>インストールされているすべての Python パッケージの一覧表示

次のスクリプト例では、インストールされているパッケージとそのバージョンが一覧表示されます。

```sql
EXECUTE sp_execute_external_script 
  @language = N'Python', 
  @script = N'
import pkg_resources
import pandas as pd
installed_packages = pkg_resources.working_set
installed_packages_list = sorted(["%s==%s" % (i.key, i.version) for i in installed_packages])
df = pd.DataFrame(installed_packages_list)
OutputDataSet = df
  '
WITH RESULT SETS (( PackageVersion nvarchar (150) ))
```

## <a name="find-a-single-python-package"></a>1 つの Python パッケージの検索

インストールした Python パッケージが、特定の SQL Server インスタンスで使用できることを確認したい場合、ストアド プロシージャを実行してパッケージを読み込み、メッセージが返されるようにします。

たとえば、次のコードでは `scikit-learn` パッケージが検索されます。
パッケージが見つかった場合、コードによって「パッケージ scikit-learn がインストールされています」というメッセージが返されます。

```sql
EXECUTE sp_execute_external_script
  @language = N'Python',
  @script = N'
import pkg_resources
pckg_name = "scikit-learn"
pckgs = pandas.DataFrame([(i.key) for i in pkg_resources.working_set], columns = ["key"])
installed_pckg = pckgs.query(''key == @pckg_name'')
print("Package", pckg_name, "is", "not" if installed_pckg.empty else "", "installed")
  '
```

<a name="get-package-vers"></a>

次の例では、revoscalepy パッケージと Python のバージョンが返されます。

```sql
EXECUTE sp_execute_external_script
  @language = N'Python',
  @script = N'
import revoscalepy
import sys
print(revoscalepy.__version__)
print(sys.version)
  '
```

## <a name="next-steps"></a>次の手順

+ [新しい Python パッケージのインストール](../python/install-additional-python-packages-on-sql-server.md)
+ [R パッケージ情報の取得](r-package-information.md)
+ [新しい R パッケージのインストール](../r/install-additional-r-packages-on-sql-server.md)
+ [R および Python のチュートリアル](../tutorials/machine-learning-services-tutorials.md)
