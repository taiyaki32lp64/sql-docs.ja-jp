---
title: 新しい R パッケージのインストール
description: qlmlutils を使用して、新しい Python パッケージを、SQL Server Machine Learning Services または SQL Server R Services のインスタンスにインストールする方法について説明します。
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/15/2019
ms.topic: conceptual
author: garyericson
ms.author: garye
ms.reviewer: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 827e83a0d1b363d3b91477b9ae85fec156ee4fc9
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727502"
---
# <a name="install-new-r-packages-with-sqlmlutils"></a>sqlmlutils で新しい R パッケージをインストールする

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

この記事では、[**sqlmlutils**](https://github.com/Microsoft/sqlmlutils) パッケージの関数を使用して、新しい R パッケージを、SQL Server Machine Learning Services または SQL Server R Services のインスタンスにインストールする方法について説明します。 インストールするパッケージは、[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) T-SQL ステートメントを使用してデータベース内で実行されている R スクリプトで使用できます。

> [!NOTE]
> SQL Server に R パッケージを追加する際に、標準の R `install.packages` コマンドは推奨されません。 代わりに、この記事で説明するように **sqlmlutils** を使用します。

## <a name="prerequisites"></a>Prerequisites

- [R](https://www.r-project.org) と [RStudio Desktop](https://www.rstudio.com/products/rstudio/download/) を、SQL Server への接続に使用するクライアント コンピューターに インストールします。 スクリプトの実行には任意の R IDE を使用できますが、この記事では RStudio を想定しています。

- [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/what-is) または [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms) (SSMS) を、SQL Server への接続に使用するクライアント コンピューターにインストールします。 他のデータベース管理ツールまたはクエリ ツールも使用できますが、この記事では Azure Data Studio または SSMS を想定しています。

### <a name="other-considerations"></a>その他の考慮事項

- SQL Server で実行されている R スクリプトでは、既定のインスタンス ライブラリにインストールされているパッケージのみを使用できます。 SQL Server では、外部ライブラリからパッケージを読み込むことはできません。これには同じコンピューター上にある外部ライブラリや、 他の Microsoft 製品と共にインストールされた R ライブラリも含まれます。

- 強化された SQL Server 環境では、次のパッケージを避けることをお勧めします。
  - ネットワーク アクセスを必要とするパッケージ
  - 管理者特権でのファイル システム アクセスが必要なパッケージ
  - Web 開発、または SQL Server 内で実行しても効果のないタスクに使用されるパッケージ

## <a name="install-sqlmlutils-on-the-client-computer"></a>sqlmlutils をクライアント コンピューターにインストールする

**sqlmlutils** を使用するには、最初に sqlmlutils を、SQL Server への接続に使用するクライアント コンピューターにインストールする必要があります。

**sqlmlutils** パッケージは **RODBCext** パッケージに依存し、**RODBCext** は他の複数のパッケージに依存します。 次の手順では、これらのパッケージすべてが正しい順序でインストールされます。

### <a name="install-sqlmlutils-online"></a>sqlmlutils をオンラインでインストールする

クライアント コンピューターがインターネットにアクセスされている場合は、**sqlmlutils** とその依存パッケージをオンラインでダウンロードしてインストールできます。

1. 最新の **sqlmlutils** zip ファイルを、 https://github.com/Microsoft/sqlmlutils/tree/master/R/dist からクライアント コンピューターにダウンロードします。 ファイルは解凍しないでください。

1. **コマンド プロンプト**を開き、次のコマンドを実行して、**sqlmlutils** パッケージと **RODBCext** パッケージをインストールします。 ダウンロードした **sqlmlutils** zip ファイルへの完全なパスに置き換えます (この例では、ご自身の [ドキュメント] フォルダーにファイルがあることを想定しています)。 **RODBCext** パッケージはオンラインで、インストールされています。

   ```console
   R -e "install.packages('RODBCext', repos='https://cran.microsoft.com')"
   R CMD INSTALL %UserProfile%\Documents\sqlmlutils_0.7.1.zip
   ```

### <a name="install-sqlmlutils-offline"></a>sqlmlutils をオフラインでインストールする

クライアント コンピューターがインターネットに接続されていない場合は、インターネットにアクセスできるコンピューターを使用して、**sqlmlutils** パッケージと **RODBCext** パッケージを事前にダウンロードしておく必要があります。 その後、ファイルをクライアント コンピューターのフォルダーにコピーし、パッケージをオフラインでインストールできます。

**RODBCext** パッケージには多数の依存パッケージがあり、パッケージに対する依存関係すべてを特定するのは複雑です。 [**miniCRAN**](https://andrie.github.io/miniCRAN/) を使用して、すべての依存パッケージが含まれるパッケージ用のローカル リポジトリ フォルダーを作成することをお勧めします。
詳細については、「[miniCRAN を使用してローカル R パッケージ リポジトリを作成する](create-a-local-package-repository-using-minicran.md)」を参照してください。

**sqlmlutils** パッケージは、クライアント コンピューターにコピーしてインストールできる 1 つの zip ファイルです。

インターネットに接続されているコンピューターでの操作:

1. **miniCRAN** をインストールします。 詳細については、「[miniCRAN をインストールする](create-a-local-package-repository-using-minicran.md#install-minicran)」を参照してください。

1. RStudio で、次の R スクリプトを実行して、**RODBCext** パッケージのローカル リポジトリ を作成します。 この例では、`c:\downloads\rodbcext` フォルダーにリポジトリが作成されます。

   ::: moniker range=">=sql-server-2016||=sqlallproducts-allversions"

   ```R
   CRAN_mirror <- c(CRAN = "https://cran.microsoft.com")
   local_repo <- "c:/downloads/rodbcext"
   pkgs_needed <- "RODBCext"
   pkgs_expanded <- pkgDep(pkgs_needed, repos = CRAN_mirror);

   makeRepo(pkgs_expanded, path = local_repo, repos = CRAN_mirror, type = "win.binary", Rversion = "3.5");
   ```

   ::: moniker-end

   ::: moniker range=">=sql-server-linux-ver15||=sqlallproducts-allversions"

   ```R
   CRAN_mirror <- c(CRAN = "https://cran.microsoft.com")
   local_repo <- "c:/downloads/rodbcext"
   pkgs_needed <- "RODBCext"
   pkgs_expanded <- pkgDep(pkgs_needed, repos = CRAN_mirror);

   makeRepo(pkgs_expanded, path = local_repo, repos = CRAN_mirror, type = "source", Rversion = "3.5");
   ```

   ::: moniker-end

   `Rversion` 値については、SQL Server にインストールされている R のバージョンを使用します。 インストールされているバージョンを確認するには、次の T-SQL コマンドを使用します。

   ```sql
   EXECUTE sp_execute_external_script @language = N'R'
    , @script = N'print(R.version)'
   ```

1. 最新の **sqlmlutils** zip ファイルを https://github.com/Microsoft/sqlmlutils/tree/master/R/dist からダウンロードします (ファイルを解凍しないでください)。 たとえば、ファイルを `c:\downloads\sqlmlutils_0.7.1.zip` にダウンロードします。

1. **RODBCext** リポジトリ フォルダー (`c:\downloads\rodbcext`) と **sqlmlutils** zip ファイル (`c:\downloads\sqlmlutils_0.7.1.zip`) 全体をクライアント コンピューターにコピーします。 たとえば、それらを、クライアント コンピューターの `c:\temp\packages` フォルダーにコピーします。

SQL Server への接続に使用するクライアント コンピューターでコマンド プロンプトを開き、次のコマンドを実行して、**RODBCext**、**sqlmlutils** の順にインストールします。

```console
R -e "install.packages('RODBCext', repos='c:\temp\packages\rodbcext')"
R CMD INSTALL c:\temp\packages\sqlmlutils_0.7.1.zip
```

## <a name="add-an-r-package-on-sql-server"></a>SQL Server で R パッケージを追加する

次の例では、[**glue**](https://cran.r-project.org/web/packages/glue/) パッケージを SQL Server に追加します。

### <a name="add-the-package-online"></a>パッケージをオンラインで追加する

SQL Server への接続に使用するクライアント コンピューターがインターネットにアクセスできる場合は、インターネット経由で **sqlmlutils** を使って **glue** パッケージおよびすべての依存関係を検索し、そのパッケージを SQL Server インスタンスにリモートでインストールできます。

1. クライアント コンピューターで RStudio を開き、新しい **R スクリプト** ファイルを作成します。

1. 次の R スクリプトを使用して、**sqlmlutils** を使って **glue** パッケージをインストールします。 ご自身の SQL Server データベース接続情報に置き換えます (Windows 認証を使用しない場合は、`uid` パラメーターと `pwd` パラメーターを追加します)。

   ```R
   library(sqlmlutils)
   connection <- connectionInfo(
     server= "yourserver",
     database = "yourdatabase")

   sql_install.packages(connectionString = connection, pkgs = "glue", verbose = TRUE, scope = "PUBLIC")
   ```

   > [!TIP]
   > **スコープ**には、**PUBLIC** または **PRIVATE** を指定できます。 パブリック スコープは、すべてのユーザーが使用できるパッケージを、データベース管理者がインストールするときに役に立ちます。 プライベート スコープを指定すると、パッケージを使用できるのは、そのパッケージをインストールしたユーザーだけになります。 スコープを指定しない場合、既定のスコープは **PRIVATE** です。

### <a name="add-the-package-offline"></a>パッケージをオフラインで追加する

クライアント コンピューターがインターネットに接続されていない場合は、インターネットにアクセスできるコンピューターを使用して、**miniCRAN** を使って **glue** パッケージをダウンロードできます。 次に、パッケージをオフラインでインストールできるクライアント コンピューターにパッケージをコピーします。
**miniCRAN** のインストールについては、「[miniCRAN をインストールする](create-a-local-package-repository-using-minicran.md#install-minicran)」を参照してください。

インターネットに接続されているコンピューターでの操作:

1. 次の R スクリプトを実行して、**glue** のローカル リポジトリ を作成します。 この例では、`c:\downloads\glue` にリポジトリ フォルダーが作成されます。

   ::: moniker range=">=sql-server-2016||=sqlallproducts-allversions"

   ```R
   CRAN_mirror <- c(CRAN = "https://cran.microsoft.com")
   local_repo <- "c:/downloads/glue"
   pkgs_needed <- "glue"
   pkgs_expanded <- pkgDep(pkgs_needed, repos = CRAN_mirror);

   makeRepo(pkgs_expanded, path = local_repo, repos = CRAN_mirror, type = "win.binary", Rversion = "3.5");
   ```

   ::: moniker-end

   ::: moniker range=">=sql-server-linux-ver15||=sqlallproducts-allversions"

   ```R
   CRAN_mirror <- c(CRAN = "https://cran.microsoft.com")
   local_repo <- "c:/downloads/glue"
   pkgs_needed <- "glue"
   pkgs_expanded <- pkgDep(pkgs_needed, repos = CRAN_mirror);

   makeRepo(pkgs_expanded, path = local_repo, repos = CRAN_mirror, type = "source", Rversion = "3.5");
   ```

   ::: moniker-end


   `Rversion` 値については、SQL Server にインストールされている R のバージョンを使用します。 インストールされているバージョンを確認するには、次の T-SQL コマンドを使用します。

   ```sql
   EXECUTE sp_execute_external_script @language = N'R'
    , @script = N'print(R.version)'
   ```

1. **glue** リポジトリ フォルダー全体 (`c:\downloads\glue`) をクライアント コンピューターにコピーします。 たとえば、`c:\temp\packages\glue` フォルダーにコピーします。

クライアント コンピューターでの操作:

1. RStudio を開き、新しい **R スクリプト** ファイルを作成します。

1. 次の R スクリプトを使用して、**sqlmlutils** を使って **glue** パッケージをインストールします。 ご自身の SQL Server データベース接続情報に置き換えます (Windows 認証を使用しない場合は、`uid` パラメーターと `pwd` パラメーターを追加します)。

   ```R
   library(sqlmlutils)
   connection <- connectionInfo(
     server= "yourserver",
     database = "yourdatabase")
   localRepo = "c:/temp/packages/glue"

   sql_install.packages(connectionString = connection, pkgs = "glue", verbose = TRUE, scope = "PUBLIC", repos=paste0("file:///",localRepo))
   ```

   > [!TIP]
   > **スコープ**には、**PUBLIC** または **PRIVATE** を指定できます。 パブリック スコープは、すべてのユーザーが使用できるパッケージを、データベース管理者がインストールするときに役に立ちます。 プライベート スコープを指定すると、パッケージを使用できるのは、そのパッケージをインストールしたユーザーだけになります。 スコープを指定しない場合、既定のスコープは **PRIVATE** です。

## <a name="use-the-package"></a>パッケージを使用する

**glue** パッケージがインストールされたら、T-SQL の **sp_execute_external_script** コマンドを使用して、SQL Server の R スクリプトでそのパッケージを使用できます。

1. Azure Data Studio または SSMS を開き、ご自身の SQL Server データベースに接続します。

1. 次のコマンドを実行します。

   ```sql
   EXECUTE sp_execute_external_script @language = N'R'
       , @script = N'
   library(glue)

   name <- "Fred"
   birthday <- as.Date("2020-06-14")
   text <- glue(''My name is {name} '',
   ''and my birthday is {format(birthday, "%A, %B %d, %Y")}.'')

   print(text)
         ';
   ```

    **結果**

    ```text
    My name is Fred and my birthday is Sunday, June 14, 2020.
    ```

## <a name="remove-the-package"></a>パッケージを削除する

**glue** パッケージを削除する場合は、次の R スクリプトを実行します。 先ほど定義したものと同じ**接続**変数を使用します。

```R
sql_remove.packages(connectionString = connection, pkgs = "glue", scope = "PUBLIC")
```

## <a name="next-steps"></a>次の手順

- インストール済み R パッケージの詳細については、「[R パッケージ情報の取得](r-package-information.md)」を参照してください
- R パッケージの操作情報については、「[R パッケージを使用するためのヒント](tips-for-using-r-packages.md)」を参照してください
- Python パッケージのインストールの詳細については、[pip を使用した Python パッケージのインストール](install-additional-python-packages-on-sql-server.md)に関するページをご覧ください
- SQL Server Machine Learning Services の詳細については、「[SQL Server Machine Learning Services とは (Python と R)](../what-is-sql-server-machine-learning.md)」を参照してください
