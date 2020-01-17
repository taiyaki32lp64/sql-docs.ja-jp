---
title: R チュートリアル:SQL でモデルを開発する
description: データベース内分析用のエンドツーエンド R ソリューションを作成する方法を示すチュートリアル。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/11/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 9844746d6887c14e5524ed54c39e2de7e0375eb1
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73723795"
---
# <a name="tutorial-sql-development-for-r-data-scientists"></a>チュートリアル:R データ サイエンティスト向けの SQL 開発
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

データ サイエンティスト向けのこのチュートリアルでは、SQL Server 2016 または SQL Server 2017 の R 機能のサポートに基づいて、予測モデリングのためのエンドツーエンド ソリューションを構築する方法について説明します。 このチュートリアルでは、SQL Server で [NYCTaxi_sample](demo-data-nyctaxi-in-sql.md) データベースを使用します。 

R コード、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ、カスタム SQL 関数の組み合わせを使用して、ドライバーが特定のタクシー乗車でチップを受け取ることができる確率を示す分類モデルを構築します。 また、R モデルを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に配置し、サーバーのデータを使用してモデルに基づくスコアを生成します。

この例は、販売キャンペーンに対する顧客の反応の予測やイベントでの支出や出席の予測など、あらゆる種類の実際の問題に合わせて拡張できます。 このモデルはストアド プロシージャから呼び出すことができるため、アプリケーションに簡単に埋め込むことができます。

このチュートリアルは、R 開発者に [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] を紹介する目的で設計されているため、可能な場合には R が使用されています。 ただしこれは、各タスクにとって必ずしも R が最適なツールであるという意味ではありません。 多くの場合、特にデータ集計と機能エンジニアリングについては、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の方が優れたパフォーマンスを示す可能性があります。  このようなタスクでは、特に [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]の新機能 (メモリ最適化列ストア インデックスなど) のメリットが得られます。 可能な最適化については、レッスンの中でご紹介します。

## <a name="prerequisites"></a>Prerequisites

+ [R が統合された SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md#verify-installation) または [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)

+ [データベース権限](../security/user-permission.md) と SQL Server データベース ユーザー ログイン

+ [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)

+ [NYC タクシーのデモ データベース](demo-data-nyctaxi-in-sql.md)

+ R に付属する RStudio や組み込みの RGUI ツールなどの R IDE

このチュートリアルは、クライアント ワークステーションで行うことをお勧めします。 同じネットワーク上で SQL Server と R 言語が有効になっている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] コンピューターに接続できる必要があります。 ワークステーションの構成手順については、[R 開発用にデータ サイエンス クライアントをセットアップする](../r/set-up-a-data-science-client.md)に関するページを参照してください。

または、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] と R 開発環境の両方を備えたコンピューターでこのチュートリアルを実行することもできますが、この構成は運用環境にはお勧めできません。 クライアントとサーバーを同じコンピューターに配置する必要がある場合は、"リモート" クライアントから R スクリプトを送信するために、Microsoft R ライブラリの 2 つ目のセットを必ずインストールしてください。 SQL Server インスタンスのプログラム ファイルにインストールされている R ライブラリは使用しないでください。 具体的には、1 台のコンピューターを使用している場合は、クライアントとサーバーの操作をサポートするために、次の両方の場所に RevoScaleR ライブラリが必要です。

+ C:\Program Files\Microsoft\R Client\R_SERVER\library\RevoScaleR 
+ C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library\RevoScaleR

> [!NOTE]
> R クライアントではなく [Machine Learning Server](https://docs.microsoft.com/machine-learning-server/) または [Data Science Virtual Machine](https://docs.microsoft.com/azure/machine-learning/data-science-virtual-machine/)を使用している場合、RevoScaleR へのパスは C:\Program Files\Microsoft\ML Server\R_SERVER\library\RevoScaleR になります。

<a name="add-packages"></a>

## <a name="additional-r-packages"></a>追加の R パッケージ

このチュートリアルでは、[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] の一部として既定ではインストールされない R ライブラリがいくつか必要です。 これらのパッケージは、ソリューションを開発するクライアントと、ソリューションを展開する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] コンピューターの両方にインストールする必要があります。

### <a name="on-a-client-workstation"></a>クライアント ワークステーション上

ご使用の R 環境に次の行をコピーし、コンソール ウィンドウ (Rgui または IDE) でコードを実行します。 一部のパッケージでは、必須パッケージもインストールされます。 全部で、約 32 パッケージがインストールされます。 この手順を完了するには、インターネット接続が必要です。
    
  ```R
  # Install required R libraries, if they are not already installed.
  if (!('ggmap' %in% rownames(installed.packages()))){install.packages('ggmap')}
  if (!('mapproj' %in% rownames(installed.packages()))){install.packages('mapproj')}
  if (!('ROCR' %in% rownames(installed.packages()))){install.packages('ROCR')}
  if (!('RODBC' %in% rownames(installed.packages()))){install.packages('RODBC')}
  ```

### <a name="on-the-server"></a>サーバー上

SQL Server にパッケージをインストールするには、いくつかのオプションがあります。 たとえば、SQL Server では [R パッケージ管理](../r/install-additional-r-packages-on-sql-server.md)機能が用意されています。これにより、データベース管理者はパッケージ リポジトリを作成し、ユーザーが独自のパッケージをインストールするための権限をユーザーに割り当てることができます。 ただし、コンピューターの管理者の場合は、正しいライブラリにインストールする場合に限り、R を使用して新しいパッケージをインストールできます。

> [!NOTE]
> サーバー上には、求められたとしてもユーザー ライブラリをインストール**しないでください**。 ユーザー ライブラリをインストールすると、SQL Server インスタンスでパッケージを見つけることも、実行することもできなくなります。 詳細については、[SQL Server に新しい R パッケージをインストールする](../r/install-additional-r-packages-on-sql-server.md)に関するページを参照してください。

1. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] コンピューターで、**管理者権限で** RGui.exe を開きます。  既定値を使用して SQL Server R Services をインストールした場合、Rgui.exe は C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64 にあります。

2. R プロンプトで、次の R コマンドを実行します。
  
  ```R
  install.packages("ggmap", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
  install.packages("mapproj", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
  install.packages("ROCR", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
  install.packages("RODBC", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
  ```
  この例では、R grep 関数を使用して、使用できるパスのベクトルを検索し、"Program Files" を含むパスを見つけます。 詳細については、[https://www.rdocumentation.org/packages/base/functions/grep](https://www.rdocumentation.org/packages/base/functions/grep) を参照してください。

  パッケージが既にインストールされている場合は、`installed.packages()` を実行してインストール済みパッケージの一覧を確認します。

## <a name="next-steps"></a>次の手順

> [!div class="nextstepaction"]
> [データの探索と集計](walkthrough-view-and-summarize-data-using-r.md)
