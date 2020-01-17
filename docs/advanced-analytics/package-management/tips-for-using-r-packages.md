---
title: R パッケージを使用するためのヒント
description: R または SQL Server を初めて使用するユーザー向けに、SQL Server で R パッケージを使用する際に役立つヒントについて説明します。
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/06/2019
ms.topic: conceptual
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 5e283ab478a6d65243e9962fd5c26f5f91d87c15
ms.sourcegitcommit: 00350f6ffb73c2c0d99beeded61c5b9baa63d171
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/30/2019
ms.locfileid: "70196345"
---
# <a name="tips-for-using-r-packages"></a>R パッケージを使用するためのヒント

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

この記事では、SQL Server で R パッケージを使用する際に役立つヒントについて説明します。 これらのヒントは、R に不慣れな DBA と、SQL Server インスタンスでのパッケージ アクセスには不慣れで R の経験は豊富な開発者向けです。

## <a name="if-youre-new-to-r"></a>R を初めて使用する場合

初めて R パッケージをインストールする管理者の場合、R パッケージの管理についていくつかの基本事項を理解しておくと、作業の開始に役立ちます。

### <a name="package-dependencies"></a>パッケージの依存関係

R パッケージは、他の複数のパッケージに依存していることが多く、その一部は、インスタンスに使用される既定の R ライブラリでは使用できない場合があります。 パッケージには、既にインストールされているものとは異なるバージョンの依存パッケージが必要になることがあります。 パッケージの依存関係は、パッケージに組み込まれた DESCRIPTION ファイルに記載されていますが、不完全な場合があります。 [iGraph](https://igraph.org/r/) というパッケージを使用すると、依存関係グラフを完全に明確にすることができます。

複数のパッケージをインストールする必要がある場合、または組織内の全員が確実に正しいパッケージの種類とバージョンを取得できるようにする場合は、[miniCRAN](https://mran.microsoft.com/package/miniCRAN) パッケージを使用して完全な依存関係チェーンを分析することをお勧めします。 minicRAN を使うと、複数のユーザーまたはコンピューター間で共有できるローカル リポジトリが作成されます。 詳細については、[miniCRAN を使用してローカル パッケージ リポジトリを作成する](create-a-local-package-repository-using-minicran.md)方法に関する記事を参照してください。

### <a name="package-sources-versions-and-formats"></a>パッケージのソース、バージョン、および形式

[CRAN](https://cran.r-project.org/) や [Bioconductor](https://www.bioconductor.org/) など、R パッケージには複数のソースがあります。 R 言語の公式サイト (<https://www.r-project.org/>) には、このようなリソースの多くが掲載されています。 Microsoft は、オープンソース R ([MRO](https://mran.microsoft.com/open)) やその他のパッケージの配布用に [MRAN](https://mran.microsoft.com/) を提供しています。 多くのパッケージは GitHub に公開されており、開発者はそこでソース コードを入手できます。

::: moniker range=">=sql-server-2016||=sqlallproducts-allversions"
R パッケージは複数のコンピューティング プラットフォームで動作します。 インストールするバージョンが Windows バイナリであることを確認してください。
::: moniker-end

::: moniker range=">=sql-server-linux-ver15||=sqlallproducts-allversions"
R パッケージは複数のコンピューティング プラットフォームで動作します。 インストールするバージョンが Linux バイナリであることを確認してください。
::: moniker-end

### <a name="know-which-library-youre-installing-to-and-which-packages-are-already-installed"></a>インストール先のライブラリとインストール済みのパッケージを把握する

コンピューター上の R 環境を以前に変更したことがある場合は、何かをインストールする前に、R 環境変数 `.libPath` に使用されているパスが 1 つのみであることを確認します。

このパスは、インスタンスの R_SERVICES フォルダーを指すようにします。 既にインストールされているパッケージを確認する方法など、詳細については、「[R パッケージ情報の取得](../package-management/r-package-information.md)」を参照してください。

## <a name="if-youre-new-to-sql-server"></a>SQL Server を初めて使用する場合

SQL Server で実行されているコードを操作する R 開発者の場合、サーバーを保護するセキュリティ ポリシーによって、R 環境を制御する機能が制限されます。 次のヒントでは、一般的な状況について説明し、この環境での作業に関する推奨事項を示します。

### <a name="r-user-libraries-not-supported-on-sql-server"></a>R ユーザー ライブラリ: SQL Server ではサポートされていません

新しい R パッケージをインストールする必要がある R 開発者は、既定のライブラリを使用できない場合、または開発者がコンピューターの管理者でない場合に、非公開のユーザー ライブラリを使用してパッケージを自由にインストールすることに慣れています。 たとえば、一般的な R 開発環境では、ユーザーはパッケージの場所を R 環境変数 `libPath` に追加するか、次のように完全なパッケージ パスを参照します。

```R
library("c:/Users/<username>/R/win-library/packagename")
```

これは、SQL Server で R ソリューションを実行する場合には機能しません。インスタンスに関連付けられている特定の既定のライブラリに対して R パッケージをインストールする必要があるためです。 既定のライブラリでパッケージを使用できない場合、パッケージを呼び出そうとすると、次のエラーが発生します。

*Error in library(xxx) : there is no package called 'package-name' (ライブラリ (xxx) でエラー: 'package-name' という名前のパッケージはありません)*

SQL Server に R パッケージをインストールする方法の詳細については、[SQL Server Machine Learning Services または SQL Server R Services に新しい R パッケージをインストールする](install-additional-r-packages-on-sql-server.md)方法に関する記事を参照してください。

### <a name="how-to-avoid-package-not-found-errors"></a>"パッケージが見つかりません" エラーを回避する方法

次のガイドラインを使用すると、"パッケージが見つかりません" エラーを回避できます。

+ ユーザー ライブラリへの依存関係を排除します。

    カスタム ユーザー ライブラリに必要な R パッケージをインストールすることは、不適切な開発手法です。 このため、ライブラリの場所にアクセス権を持たない別のユーザーがソリューションを実行すると、エラーが発生する可能性があります。

    また、既定のライブラリにパッケージをインストールすると、R コードで別のバージョンを指定しても、R ランタイムでは既定のライブラリからパッケージが読み込まれます。

+ コードを共有環境で実行できることを確認します。

+ ソリューションの一部としてパッケージをインストールしないようにします。 パッケージをインストールするアクセス許可がない場合、コードは失敗します。 パッケージをインストールするアクセス許可がある場合でも、実行する他のコードとは別に行う必要があります。

+ インストールされていないパッケージへの呼び出しがないよう、コードを確認します。

+ R パッケージまたは R ライブラリのパスへの直接参照を削除するようにコードを更新します。

+ インスタンスに関連付けられているパッケージ ライブラリを把握します。 詳細については、「[R パッケージ情報の取得](../package-management/r-package-information.md)」を参照してください。

## <a name="see-also"></a>参照

+ [新しい R パッケージのインストール](install-additional-r-packages-on-sql-server.md)
+ [新しい Python パッケージのインストール](../python/install-additional-python-packages-on-sql-server.md)
+ [チュートリアル、サンプル、ソリューション](../tutorials/machine-learning-services-tutorials.md)