---
title: R パッケージ情報の取得
description: SQL Server Machine Learning Services と SQL Server R Services にインストールされている R パッケージに関する情報を取得する方法について説明します。
ms.custom: ''
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/15/2019
ms.topic: conceptual
author: garyericson
ms.author: garye
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 8c3cf3c1debc03c169c585521b8b46dd8b1365c5
ms.sourcegitcommit: 632ff55084339f054d5934a81c63c77a93ede4ce
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2019
ms.locfileid: "69641159"
---
# <a name="get-r-package-information"></a>R パッケージ情報の取得

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

この記事では、SQL Server Machine Learning Services と SQL Server R Services にインストールされている R パッケージに関する情報を取得する方法について説明します。 R スクリプトの例では、インストール パスやバージョンなどのパッケージ情報を一覧表示する方法を示しています。

## <a name="default-r-library-location"></a>R ライブラリの既定の場所

SQL Server と共に機械学習をインストールすると、インストールした言語ごとに 1 つのパッケージ ライブラリがインスタンス レベルで作成されます。 このインスタンス ライブラリは、Windows では SQL Server に登録されているセキュリティで保護されたフォルダーです。

SQL Server のデータベース内で実行されるすべてのスクリプトは、インスタンス ライブラリから関数を読み込む必要があります。 SQL Server は、他のライブラリにインストールされているパッケージにはアクセスできません。 これはリモート クライアントにも当てはまります。サーバーの計算のコンテキストで実行されているすべての R スクリプトは、インスタンス ライブラリにインストールされているパッケージしか使用できません。
既定のインスタンス ライブラリは、サーバーの資産を保護するために、コンピューターの管理者のみが変更できるようになっています。

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
R のバイナリの既定のパスは次のとおりです。

`C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library`
::: moniker-end

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
R のバイナリの既定のパスは次のとおりです。

`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library`
::: moniker-end

::: moniker range=">sql-server-2017||=sqlallproducts-allversions"
R のバイナリの既定のパスは次のとおりです。

`C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\R_SERVICES\library`
::: moniker-end

既定の SQL インスタンスは、MSSQLSERVER と想定されています。 SQL Server がユーザー定義の名前付きインスタンスとしてインストールされている場合、代わりにその指定の名前を使用します。

<!-- I don't think this note is necessary. If you have these other products installed, you'd already know about them.
> [!NOTE]
> If you find other folders having similar subfolder names and files, you probably have a standalone installation of  Microsoft R Server or Machine Learning Server. These server products have different installers and paths: C:\Program Files\Microsoft\R Server\R_SERVER or C:\Program Files\Microsoft\ML SERVER\R_SERVER. For more information, see [Install R Server 9.1 for Windows](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows) or [Install Machine Learning Server for Windows](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install).
-->

次のステートメントを実行すると、現在のインスタンスの既定の R パッケージ ライブラリを確認することができます。

```sql
EXECUTE sp_execute_external_script  
  @language = N'R',
  @script = N'OutputDataSet <- data.frame(.libPaths());'
WITH RESULT SETS (([DefaultLibraryName] VARCHAR(MAX) NOT NULL));
GO
```

次のステートメントでは、SQL Server が使用するインスタンス ライブラリのパスと RevoScaleR のバージョンを返すために、[rxSqlLibPaths](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqllibpaths) を使用しています。

```sql
EXECUTE sp_execute_external_script
  @language =N'R',
  @script=N'
  sql_r_path <- rxSqlLibPaths("local")
  print(sql_r_path)
  version_info <-packageVersion("RevoScaleR")
  print(version_info)'
```

> [!NOTE]
> [rxSqlLibPaths](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqllibpaths) 関数は、ローカル コンピューター上でのみ実行できます。 この関数では、リモート接続のライブラリ パスは返せません。

## <a name="default-r-packages"></a>既定の R パッケージ

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"

次の R パッケージは、SQL Server R Services と共にインストールされます。

|パッケージ | Version | [説明] |
|---------|---------|-------------|
| [RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)  | 8.0.3 | リモートでの計算のコンテキスト、ストリーミング、データのインポートと変換、モデリング、視覚化、および分析での rx 関数の並列実行で使用します。 |
| [sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils) | 8.0.3 | ストアド プロシージャに R スクリプトを含めるために使用します。 |

::: moniker-end

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"

次の R パッケージは、セットアップ時に R 機能を選択すると、SQL Server Machine Learning Services と共にインストールされます。

|パッケージ | Version | [説明] |
|---------|---------|-------------|
| [RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)  | 9.2 | リモートでの計算のコンテキスト、ストリーミング、データのインポートと変換、モデリング、視覚化、および分析での rx 関数の並列実行で使用します。 |
| [sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils) | 9.2 | ストアド プロシージャに R スクリプトを含めるために使用します。 |
| [MicrosoftML](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package)| 9.2 | R に機械学習アルゴリズムを追加します。 | 
| [olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) | 9.2 | R で MDX ステートメントを記述するために使用します。 |

::: moniker-end

### <a name="component-upgrades"></a>コンポーネントのアップグレード

既定で R パッケージは、サービス パックと累積的な更新プログラムで更新されます。 その他のパッケージおよび R のコア コンポーネントのバージョンの完全アップグレードは、製品のアップグレード、または Microsoft Machine Learning Server への R サポートのバインドによってのみ可能です。

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
また、コンポーネントをアップグレードすると、MicrosoftML および olapR パッケージを SQL Server インスタンスに追加することもできます。
::: moniker-end

詳細については、[SQL Server での R および Python コンポーネントのアップグレード](../install/upgrade-r-and-python.md)に関する記事を参照してください。

## <a name="default-open-source-r-packages"></a>既定のオープンソースの R パッケージ

R では、オープンソースの R をサポートしているので、base R 関数を呼び出して、オープンソースおよびサードパーティ パッケージを追加インストールできます。 R 言語では、**base**、**stats**、**utils** などのコア機能をサポートしています。 R の基本インストールには、**RGui** (軽量の対話型エディター) や **RTerm** (R のコマンド プロンプト) などの多数のサンプル データセットや、標準の R ツールも含まれています。

お使いのインストールに含まれるオープンソースの R のディストリビューションは、[Microsoft R Open (MRO)](https://mran.microsoft.com/open) です。 MRO では、base R に [Intel Math Kernel Library](https://en.wikipedia.org/wiki/Math_Kernel_Library) などのオープンソースのパッケージの付加価値が追加されています。

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
SQL Server R Services のセットアップで MRO が提供する R のバージョンは 3.2.2 です。
::: moniker-end

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
SQL Server Machine Learning Services のセットアップで MRO が提供する R のバージョンは 3.3.3 です。
::: moniker-end

> [!IMPORTANT]
> SQL Server のセットアップでインストールされた R のバージョンは、手動で Web 上の新しいバージョンに上書きしないでください。 Microsoft R パッケージは、R の特定のバージョンに基づいています。インストールを変更すると、それが不安定になる可能性があります。

## <a name="list-all-installed-r-packages"></a>インストールされているすべての R パッケージの列挙

次の [!INCLUDE[tsql](../../includes/tsql-md.md)] ストアド プロシージャの例では、R 関数 `installed.packages()` を使用して、現在の SQL インスタンスの R_SERVICES ライブラリにインストールされている R パッケージを一覧表示します。 このスクリプトでは、DESCRIPTION ファイルのパッケージ名とバージョン フィールドを返します。

```sql
EXECUTE sp_execute_external_script
  @language=N'R',
@script = N'str(OutputDataSet);
packagematrix <- installed.packages();
Name <- packagematrix[,1];
Version <- packagematrix[,3];
OutputDataSet <- data.frame(Name, Version);',
@input_data_1 = N'
  '
WITH RESULT SETS ((PackageName nvarchar(250), PackageVersion nvarchar(max) ))
```

R パッケージの DESCRIPTION フィールドのオプション フィールドおよび既定フィールドの詳細については、「[https://cran.r-project.org](https://cran.r-project.org/doc/manuals/R-exts.html#The-DESCRIPTION-file)」を参照してください。

## <a name="find-a-single-r-package"></a>1 つの R パッケージの検索

インストールした R パッケージが、特定の SQL Server インスタンスで使用できることを確認したい場合、ストアド プロシージャを実行してパッケージを読み込み、メッセージが返されるようにします。

たとえば、次のステートメントは、使用可能な場合に [glue](https://cran.r-project.org/web/packages/glue/) パッケージを検索して読み込みます。
パッケージが見つからないか、読み込めない場合は、「'glue' という名前のパッケージはありません」というテキストを含むエラーが表示されます。

```sql
EXECUTE sp_execute_external_script  
  @language =N'R',
  @script=N'require("glue")'
GO
```

パッケージの詳細については、「`packageDescription`」を参照してください。
次のステートメントでは、**glue** パッケージの情報が返されます。

```sql
EXECUTE sp_execute_external_script
  @language = N'R',
  @script = N'
print(packageDescription("glue"))
  '
```

## <a name="next-steps"></a>次の手順

+ [新しい R パッケージのインストール](../r/install-additional-r-packages-on-sql-server.md)
+ [Python パッケージ情報の取得](python-package-information.md)
+ [新しい Python パッケージのインストール](../python/install-additional-python-packages-on-sql-server.md)
+ [R および Python のチュートリアル](../tutorials/machine-learning-services-tutorials.md)
