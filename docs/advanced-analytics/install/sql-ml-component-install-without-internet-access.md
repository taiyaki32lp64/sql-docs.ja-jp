---
title: インターネットへのアクセスなしでのインストール
description: ネットワーク ファイアウォールの背後に隔離されたコンピューターに SQL Server Machine Learning R および Python をインストールします。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/04/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: e966406a20df723c453a5c8083f00f2e4989d9d0
ms.sourcegitcommit: 385a907ed1de8fa7ada76260ea3f92583eb09238
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/14/2019
ms.locfileid: "74064129"
---
# <a name="install-sql-server-machine-learning-r-and-python-on-computers-with-no-internet-access"></a>インターネットにアクセスできないコンピューターに SQL Server Machine Learning R および Python をインストールする
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

既定では、インストーラーは Microsoft ダウンロード サイトに接続して、SQL Server 上での機械学習に必要なコンポーネントおよび更新されたコンポーネントを取得します。 ファイアウォールの制約によって、インストーラーがこれらのサイトにアクセスできない場合は、インターネットに接続されたデバイスを使ってファイルをダウンロードし、オフラインのサーバーにファイルを転送してから、セットアップを実行できます。

データベース内分析は、データベース エンジンのインスタンスに加え、SQL Server のバージョンに応じて、R および Python 統合用の追加コンポーネントで構成されます。 

+ SQL Server 2019 には、R、Python、Java が含まれます
+ SQL Server 2017 には、R と Python が含まれます
+ SQL Server 2016 は R のみです

分離されたサーバーの場合、機械学習と R/Python 言語固有の機能は、CAB ファイルを通じて追加されます。 

::: moniker range="=sql-server-ver15||=sqlallproducts-allversions"
## <a name="sql-server-2019-offline-install"></a>SQL Server 2019 のオフライン インストール

分離されたサーバーに SQL Server Machine Learning Services (R および Python) をインストールするには、まず、SQL Server の初回リリースと、R および Python サポート用の対応する CAB ファイルをダウンロードします。 サーバーをすぐに更新して、最新の累積的な更新プログラムを使用する予定の場合も、最初に初回リリースをインストールする必要があります。

> [!Note]
> SQL Server 2019 には Service Pack がありません。 初回リリースが唯一のベースラインであり、累積的な更新プログラムを通じてのみサービスが提供されます。

### <a name="1---download-2019-cabs"></a>1 - 2019 用の CAB をダウンロードする

インターネットに接続されているコンピューター上で、SQL Server 2019 の初回リリースおよびインストール メディア用の R および Python 機能を提供する CAB ファイルをダウンロードします。

リリース  |ダウンロード リンク  |
---------|---------------|
Microsoft R Open        | [SRO_3.5.2.125_1033.cab](https://go.microsoft.com/fwlink/?linkid=2085686) |
Microsoft R Server      | [SRS_9.4.7.25_1033.cab](https://go.microsoft.com/fwlink/?linkid=2085792) |
Microsoft Python Open   | [SPO_4.5.12.120_1033.cab](https://go.microsoft.com/fwlink/?linkid=2085793) |
Microsoft Python Server | [SPS_9.4.7.25_1033.cab](https://go.microsoft.com/fwlink/?linkid=2085685) |

> [!NOTE]
> Java 機能は SQL Server のインストール メディアに含まれているため、個別の CAB ファイルは必要ありません。

###  <a name="2---get-sql-server-2019-installation-media"></a>2 - SQL Server 2019 のインストール メディアを入手する

1. インターネットに接続されているコンピューター上で、[SQL Server 2019 のセットアップ プログラム](https://www.microsoft.com/sql-server/sql-server-downloads)をダウンロードします。 

2. セットアップをダブルクリックして、インストールの種類に **[メディアのダウンロード]** を選択します。 このオプションを使用すると、セットアップによって、インストール メディアを含む .iso (または .cab) ファイルが作成されます。

   ![インストールの種類に [メディアのダウンロード] を選択する](media/2019offline-download-tile.png "メディアのダウンロード")

::: moniker-end

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
## <a name="sql-server-2017-offline-install"></a>SQL Server 2017 のオフライン インストール

分離されたサーバーに SQL Server Machine Learning Services (R および Python) をインストールするには、まず、SQL Server の初回リリースと、R および Python サポート用の対応する CAB ファイルをダウンロードします。 サーバーをすぐに更新して、最新の累積的な更新プログラムを使用する予定の場合も、最初に初回リリースをインストールする必要があります。

> [!Note]
> SQL Server 2017 には Service Pack がありません。 初回リリースを唯一のベースラインとして使用するのが SQL Server の最初のリリースであり、累積的な更新プログラムを通じてのみサービスが提供されます。 

### <a name="1---download-2017-cabs"></a>1 - 2017 用の CAB をダウンロードする

インターネットに接続されているコンピューター上で、SQL Server 2017 の初回リリースおよびインストール メディア用の R および Python 機能を提供する CAB ファイルをダウンロードします。 

リリース  |ダウンロード リンク  |
---------|---------------|
Microsoft R Open     |[SRO_3.3.3.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851496)|
Microsoft R Server      |[SRS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851507)|
Microsoft Python Open     |[SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502) |
Microsoft Python Server    |[SPS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851508) |

###  <a name="2---get-sql-server-2017-installation-media"></a>2 - SQL Server 2017 のインストール メディアを入手する

1. インターネットに接続されているコンピューター上で、[SQL Server 2017 のセットアップ プログラム](https://www.microsoft.com/sql-server/sql-server-downloads)をダウンロードします。 

2. セットアップをダブルクリックして、インストールの種類に **[メディアのダウンロード]** を選択します。 このオプションを使用すると、セットアップによって、インストール メディアを含む .iso (または .cab) ファイルが作成されます。

   ![インストールの種類に [メディアのダウンロード] を選択する](media/offline-download-tile.png "メディアのダウンロード")

::: moniker-end

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"

## <a name="sql-server-2016-offline-install"></a>SQL Server 2016 のオフライン インストール

SQL Server 2016 のデータベース内分析は R のみです。これには、製品パッケージ用の CAB ファイル 2 つと、Microsoft によるオープンソースの R のディストリビューションのみが、それぞれ使用されます。 まず、次のリリースのいずれかをインストールします:RTM、SP 1、SP 2。 基本インストールが完了したら、次の手順として累積的な更新プログラムを適用できます。

インターネットに接続しているコンピューター上で、SQL Server 2016 上にデータベース内分析をインストールするためのセットアップで使用される CAB ファイルをダウンロードします。 

### <a name="1---download-2016-cabs"></a>1 - 2016 用の CAB をダウンロードする

リリース  | Microsoft R Open | Microsoft R Server |
---------|-----------------|---------------------|
**SQL Server 2016 RTM**     | [SRO_3.2.2.803_1033.cab](https://go.microsoft.com/fwlink/?LinkId=761266) |[SRS_8.0.3.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=735051) |
**SQL Server 2016 SP 1**     | [SRO_3.2.2.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824879) |[SRS_8.0.3.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824881) | 
**SQL Server 2016 SP 2**  |[SRO_3.2.2.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=866039) |[SRS_8.0.3.17000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=850317) |

### <a name="2---get-sql-server-2016-installation-media"></a>2 - SQL Server 2016 のインストール メディアを入手する

ターゲット コンピューターへの最初のインストールとして、SQL Server 2016 RTM、SP 1、または SP 2 をインストールすることができます。 これらのバージョンはいずれも、累積的な更新プログラムを受け入れることができます。

インストール メディアを含んだ .iso ファイルを入手する方法の 1 つは、[Visual Studio Dev Essentials](https://visualstudio.microsoft.com/dev-essentials/) を使用することです。 サインインした後、 **[ダウンロード]** リンクを使用して、インストールする SQL Server 2016 リリースを見つけます。 ダウンロードは .iso ファイルの形式で行われ、これをオフライン インストール用のターゲット コンピューターにコピーできます。

::: moniker-end

## <a name="transfer-files"></a>ファイルの転送

SQL Server のインストール メディア (.iso または .cab) とデータベース内分析の CAB ファイルを、ターゲット コンピューターにコピーします。 CAB ファイルとインストール メディアのファイルを、ターゲット コンピューター上の同じフォルダーに配置します (セットアップ ユーザーの %TEMP% フォルダーなど)。

Python の CAB ファイル用には %TEMP% フォルダーが必要です。 R 用には、%TEMP% を使用するか、`myrcachedirectory` パラメーターを CAB のパスに設定することができます。

## <a name="run-setup"></a>セットアップの実行

インターネットに接続されていないコンピューター上で SQL Server セットアップを実行すると、セットアップによってウィザードに **[オフライン インストール]** ページが追加され、前の手順でコピーした CAB ファイルの場所を指定できるようになります。

1. インストールを開始するには、.iso または .cab ファイルをダブルクリックして、インストール メディアにアクセスします。 **setup.exe** ファイルが表示されます。

2. **setup.exe** を右クリックし、管理者として実行します。

3. セットアップ ウィザードで、オープンソースの R または Python コンポーネントに対するライセンスのページが表示されたら、 **[同意する]** をクリックします。 ライセンス条項に同意すると、次の手順に進むことができます。

4. **[オフライン インストール]** ページが表示されたら、 **[インストール パス]** に、以前にコピーした CAB ファイルが格納されているフォルダーを指定します。

5. 画面の指示に従って続行し、インストールを完了します。

<a name="apply-cu"></a>

## <a name="apply-cumulative-updates"></a>累積的な更新プログラムの適用

最新の累積的な更新プログラムをデータベース エンジンと機械学習コンポーネントの両方に適用することをお勧めします。 累積的な更新プログラムは、セットアップ プログラムによってインストールされます。 

::: moniker range="=sql-server-ver15||=sqlallproducts-allversions"
1. ベースライン インスタンスを使用して開始します。 累積的な更新プログラムは、SQL Server の初回リリースの既存のインストールにのみ適用できます。

2. インターネットに接続されているデバイスで、使用するバージョンの SQL Server 用の累積更新プログラムの一覧に移動します。

   + SQL Server 2019 更新プログラム " *(2019 用の更新プログラムはまだ利用できません)* "
::: moniker-end

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
1. ベースライン インスタンスを使用して開始します。 累積的な更新プログラムは、SQL Server の初回リリースの既存のインストールにのみ適用できます。

2. インターネットに接続されているデバイスで、使用するバージョンの SQL Server 用の累積更新プログラムの一覧に移動します。

   + [SQL Server 2017 の更新プログラム](https://sqlserverupdates.com/sql-server-2017-updates/)
::: moniker-end

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
1. ベースライン インスタンスを使用して開始します。 累積的な更新プログラムは、SQL Server 2016 初回リリース、SQL Server 2016 SP 1、または SQL Server 2016 SP 2 の既存のインストールに対してのみ適用できます。

2. インターネットに接続されているデバイスで、使用するバージョンの SQL Server 用の累積更新プログラムの一覧に移動します。

   + [SQL Server 2016 更新プログラム](https://sqlserverupdates.com/sql-server-2016-updates/)
::: moniker-end

3. 最新の累積的な更新プログラムを選択して、実行可能ファイルをダウンロードします。

4. R および Python 用の対応する CAB ファイルを入手します。 ダウンロード リンクについては、[SQL Server データベース内分析インスタンスの累積的な更新プログラムの CAB ダウンロード](sql-ml-cab-downloads.md)に関するページを参照してください。

5. すべてのファイル (実行可能ファイルと CAB ファイル) を、オフライン コンピューター上の同じフォルダーに転送します。

6. セットアップを実行します。 ライセンス条項に同意し、[機能の選択] ページで、累積的な更新プログラムが適用される機能を確認します。 機械学習機能を含む、現在のインスタンスにインストールされているすべての機能が表示されます。

   ![機能ツリーから機能を選択する](media/cumulative-update-feature-selection.png "機能の一覧")

5. ウィザードを続行し、R および Python ディストリビューションのライセンス条項に同意します。 インストール中に、更新された CAB ファイルを含むフォルダーの場所を選択するように求められます。

## <a name="set-environment-variables"></a>環境変数の設定

R 機能の統合のみの場合、**MKL_CBWR** 環境変数を設定して、Intel Math Kernel Library (MKL) 計算からの[一貫した出力を保証](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr)する必要があります。

1. コントロール パネルで、 **[システムとセキュリティ]**  >  **[システム]**  >  **[システムの詳細設定]**  >  **[環境変数]** の順にクリックします。

2. 新しいユーザー変数またはシステム変数を作成します。 

   + 変数名を `MKL_CBWR` に設定する
   + 変数値を `AUTO` に設定する

この手順では、サーバーを再起動する必要があります。 スクリプトの実行を有効にしようとしている場合は、すべての構成作業が完了するまで再起動を遅らせることができます。

## <a name="post-install-configuration"></a>インストール後の構成

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
インストールが完了したら、サービスを再起動した後、スクリプトの実行が有効になるようにサーバーを構成します。

+ [外部スクリプトの実行を有効にする](sql-machine-learning-services-windows-install.md#bkmk_enableFeature)

SQL Server Machine Learning Services の初回オフライン インストールには、オンライン インストールと同じ構成が必要です。

+ [インストールの確認](sql-machine-learning-services-windows-install.md#verify-installation)
+ [必要に応じた追加の構成](sql-machine-learning-services-windows-install.md#additional-configuration)
::: moniker-end

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
インストールが完了したら、サービスを再起動した後、スクリプトの実行が有効になるようにサーバーを構成します。

+ [外部スクリプトの実行を有効にする](sql-r-services-windows-install.md#bkmk_enableFeature)

SQL Server R Services の初回オフライン インストールには、オンライン インストールと同じ構成が必要です。

+ [インストールの確認](sql-r-services-windows-install.md#verify-installation)
+ [必要に応じた追加の構成](sql-r-services-windows-install.md#bkmk_FollowUp)
::: moniker-end

## <a name="next-steps"></a>次の手順

インスタンスのインストール状態を確認し、よくある問題を解決するには、[SQL Server のカスタム レポート](../r/monitor-r-services-using-custom-reports-in-management-studio.md)に関する記事をご覧ください。

見慣れないメッセージやログ エントリに関するヘルプについては、[アップグレードとインストールの FAQ - Machine Learning Services](../r/upgrade-and-installation-faq-sql-server-r-services.md) に関する記事をご覧ください。
