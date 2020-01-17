---
title: miniCRAN を使用してリポジトリを作成する
description: miniCRAN パッケージを使用して R パッケージをオフラインでインストールし、パッケージと依存関係のローカル リポジトリを作成する方法について説明します。
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/15/2019
ms.topic: conceptual
author: garyericson
ms.author: garye
ms.reviewer: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 9b83a0c016cf16e4df8ef7fcb90b3711eabe4933
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727575"
---
# <a name="create-a-local-r-package-repository-using-minicran"></a>miniCRAN を使用してローカル R パッケージ リポジトリを作成する
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

この記事では、[miniCRAN](https://cran.r-project.org/web/packages/miniCRAN/index.html) を使用して R パッケージをオフラインでインストールし、パッケージと依存関係のローカル リポジトリを作成する方法について説明します。 **miniCRAN** は、パッケージと依存関係を識別して、それらを 1 つのフォルダーにダウンロードします。オフラインでの R パッケージ インストールでは、このフォルダーを他のコンピューターにコピーします。

1 つまたは複数のパッケージを指定できます。**miniCRAN** は、これらのパッケージの依存関係ツリーを再帰的に読み取ります。 その後、CRAN または類似のリポジトリから、リストされているパッケージとその依存関係のみがダウンロードされます。

この処理が完了すると、**miniCRAN** は、選択したパッケージとすべての必要な依存関係で構成される、内部的に一貫性のあるリポジトリを作成します。 このローカル リポジトリをサーバーに移動し、インターネットに接続せずにパッケージのインストールを続行できます。

経験豊富な R ユーザーは、多くの場合、ダウンロードしたパッケージの DESCRIPTION ファイルで依存パッケージの一覧を確認します。 ただし、**Imports** に記載されているパッケージには、第 2 レベルの依存関係がある場合があります。 このため、必要なパッケージの完全なコレクションをアセンブルするために **miniCRAN** をお勧めします。

## <a name="why-create-a-local-repository"></a>ローカル リポジトリを作成する理由

ローカル パッケージ リポジトリを作成する目的は、サーバー管理者または組織内の他のユーザー (特に、インターネットにアクセスできないユーザー) が、サーバーに新しい R パッケージをインストールするために使用できる 1 つの場所を提供することです。 リポジトリを作成した後、新しいパッケージを追加することで、または既存のパッケージのバージョンをアップグレードすることで、そのリポジトリを変更できます。

パッケージ リポジトリは、次のシナリオに役立ちます。

- **セキュリティ**:多くの R ユーザーは、CRAN またはそのいずれかのミラー サイトから、新しい R パッケージを任意にダウンロードしてインストールすることに慣れています。 ただし、セキュリティ上の理由により、[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] を実行している実稼働サーバーは、通常、インターネットに接続されていません。

- **オフライン インストールの簡素化**:オフライン サーバーにパッケージをインストールするには、すべてのパッケージの依存関係もダウンロードする必要があります。 miniCRAN を使用すると、すべての依存関係を正しい形式で簡単に取得できます。 miniCRAN を使用すると、[CREATE EXTERNAL LIBRARY](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) ステートメントを使用してインストールするパッケージを準備するときに、パッケージの依存関係のエラーを回避できます。

- **バージョン管理の改善**:マルチユーザー環境では、サーバーに複数のパッケージ バージョンを無制限にインストールしないことが適切です。 ローカル リポジトリを使用すると、ユーザーに対して一貫したパッケージのセットを提供できます。

## <a name="install-minicran"></a>miniCRAN をインストールする

**miniCRAN** パッケージ自体は、他の 18 個の CRAN パッケージに依存しています。これらのパッケージのなかに、**RCurl** パッケージがあり、このパッケージには **curl-devel** パッケージに対するシステム依存関係があります。 同様に、パッケージ **XML** は **libxml2-devel** に依存しています。 依存関係を解決するために、インターネットにフル アクセスできるコンピューター上に、ローカル リポジトリを最初に作成することをお勧めします。

基本 R、R ツール、およびインターネット接続があるコンピューターで、次のコマンドを実行します。 このコンピューターが SQL Server コンピューターではないことを前提としています。 次のコマンドは、**miniCRAN** パッケージと **igraph** パッケージをインストールします。 この例では、パッケージが既にインストールされているかどうかを確認しますが、`if` ステートメントをバイパスして、パッケージを直接インストールすることもできます。

```R
if(!require("miniCRAN")) install.packages("miniCRAN") 
if(!require("igraph")) install.packages("igraph") 
library("miniCRAN")
```

## <a name="set-the-cran-mirror-and-mran-snapshot"></a>CRAN ミラーと MRAN スナップショットを設定する

パッケージの取得に使用するミラー サイトを指定します。 たとえば、MRAN サイトや、必要なパッケージがあるリージョン内のその他のサイトを使用できます。 ダウンロードが失敗した場合は、別のミラー サイトを試してください。

```R
CRAN_mirror <- c(CRAN = "https://cran.cnr.berkeley.edu")
```

## <a name="create-a-local-folder"></a>ローカル フォルダーを作成する

収集したパッケージを格納するローカル フォルダーを作成します。 これを頻繁に繰り返す場合、"miniCRANZooPackages" や "miniCRANMyRPackageV2" などのわかりやすい名前を使用することをお勧めします。

フォルダーをローカル リポジトリとして指定します。 R 構文では、パス名にスラッシュを使用します。これは、Windows の規則とは反対です。

```R
local_repo <- "C:/miniCRANZooPackages"
```

## <a name="add-packages-to-the-local-repo"></a>ローカル リポジトリにパッケージを追加する

**miniCRAN** がインストールされて読み込まれたら、ダウンロードする追加パッケージを指定する一覧を作成します。

この最初の一覧には依存関係は追加**しない**でください。 **miniCRAN** によって使用される **igraph** パッケージは、依存関係の一覧を自動的に生成します。 生成された依存関係グラフの使用方法について詳しくは、「[miniCRAN を使用したパッケージの依存関係の識別](https://cran.r-project.org/web/packages/miniCRAN/vignettes/miniCRAN-dependency-graph.html)」を参照してください。

1. ターゲット パッケージ "zoo" と "forecast" を変数に追加します。

    ```R
    pkgs_needed <- c("zoo", "forecast")
    ```

2. 必要に応じて、依存関係グラフをプロットします。 これは必須ではありませんが、有益である場合があります。

    ```R
    plot(makeDepGraph(pkgs_needed))
    ```

3. ローカル リポジトリを作成します。 必要に応じて、R バージョンを、SQL Server インスタンスにインストールされているバージョンに変更してください。 コンポーネントのアップグレードを行った場合、ご使用のバージョンは元のバージョンよりも新しい可能性があります。 詳細については、「[R パッケージ情報の取得](../package-management/r-package-information.md)」を参照してください。

    ```R
    pkgs_expanded <- pkgDep(pkgs_needed, repos = CRAN_mirror);
    makeRepo(pkgs_expanded, path = local_repo, repos = CRAN_mirror, type = "win.binary", Rversion = "3.3");
    ```

   この情報から、miniCRAN パッケージは、後でパッケージを [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] にコピーするために必要なフォルダー構造を作成します。

この時点で、必要なパッケージと必要な追加パッケージを含むフォルダーが作成されているはずです。 このフォルダーには、zip 形式のパッケージのコレクションが含まれている必要があります。 パッケージを解凍したり、ファイルの名前を変更したりしないでください。

必要に応じて、次のコードを実行して、ローカルの miniCRAN リポジトリに含まれているパッケージの一覧を表示します。

```R
pdb <- as.data.frame(pkgAvail(local_repo, type = "win.binary", Rversion = "3.3"), stringsAsFactors = FALSE);
head(pdb);
pdb$Package;
pdb[, c("Package", "Version", "License")]
```

## <a name="add-packages-to-the-instance-library"></a>インスタンス ライブラリにパッケージを追加する

必要なパッケージを含むローカル リポジトリを作成したら、パッケージ リポジトリを SQL Server コンピューターに移動します。 次の手順では、R ツールを使用してパッケージをインストールする方法について説明します。

1. miniCRAN リポジトリが格納されているフォルダー全体を、パッケージのインストール先のサーバーにコピーします。 通常、このフォルダーは次の構造を持ちます。 

   `<miniCRAN root>/bin/windows/contrib/version/<all packages>`

   この手順では、ルート ドライブからのフォルダーを想定しています。

2. インスタンスに関連付けられている R ツールを開きます (たとえば、Rgui.exe を使用できます)。 右クリックして **[管理者として実行]** を選択し、ツールがシステムを更新できるようにします。

   ::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
   - たとえば、RGUI の既定のファイルの場所は `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64` です。
   ::: moniker-end

   ::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
   - たとえば、RGUI のファイルの場所は `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64` です。
   ::: moniker-end

   ::: moniker range=">sql-server-2017||=sqlallproducts-allversions"
   - たとえば、RGUI のファイルの場所は `C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\R_SERVICES\bin\x64` です。
   ::: moniker-end

3. インスタンス ライブラリのパスを取得し、ライブラリ パスの一覧に追加します。

   ::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
   例を次に示します。

   ```R
   outputlib <- "C:/Program Files/Microsoft SQL Server/MSSQL13.MSSQLSERVER/R_SERVICES/library"
   ```

   ::: moniker-end

   ::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
   例を次に示します。

   ```R
   outputlib <- "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER/R_SERVICES/library"
   ```

   ::: moniker-end

   ::: moniker range=">sql-server-2017||=sqlallproducts-allversions"
   例を次に示します。

   ```R
   outputlib <- "C:/Program Files/Microsoft SQL Server/MSSQL15.MSSQLSERVER/R_SERVICES/library"
   ```

   ::: moniker-end

4. **miniCRAN** リポジトリを `server_repo` としてコピーしたサーバー上の新しい場所を指定します。

    この例では、リポジトリをサーバーの一時フォルダーにコピーしたとします。

    ```R
    inputlib <- "C:/miniCRANZooPackages"
    ```

5. サーバーの新しい R ワークスペースで作業しているため、インストールするパッケージの一覧も指定する必要があります。

    ```R
    mypackages <- c("zoo", "forecast")
    ```

6. miniCRAN リポジトリのローカル コピーへのパスを指定して、パッケージをインストールします。

    ```R
    install.packages(mypackages, repos = file.path("file://", normalizePath(inputlib, winslash = "/")), lib = outputlib, type = "win.binary", dependencies = TRUE);
    ```

7. インスタンス ライブラリから、次のようなコマンドを使用して、インストールされているパッケージを表示できます。

    ```R
    installed.packages()
    ```

## <a name="see-also"></a>参照

+ [R パッケージ情報の取得](../package-management/r-package-information.md)
+ [R のチュートリアル](../tutorials/sql-server-r-tutorials.md)
