---
title: SQL Server Data Tools (SSDT) のダウンロード | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssdt
ms.topic: conceptual
keywords: ssdt のインストール, ssdt のダウンロード, 最新の ssdt
ms.assetid: b0fc4987-d260-4d0a-9dd1-98099835b361
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: ''
ms.date: 08/15/2019
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||=azuresqldb-mi-current'
ms.openlocfilehash: a79940fa5696a65ed580d8550984d090a48eebdf
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/23/2019
ms.locfileid: "72807446"
---
# <a name="download-and-install-sql-server-data-tools-ssdt-for-visual-studio"></a>Visual Studio の SQL Server Data Tools (SSDT) をダウンロードし、インストールする

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md.md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

**SQL Server Data Tools** は、SQL Server リレーショナル データベース、Azure SQL データベース、Analysis Services (AS) データ モデル、Integration Services (IS) パッケージ、Reporting Services (RS) レポートをビルドするための最新の開発ツールです。 SSDT では、Visual Studio でアプリケーションを開発する場合と同じくらい簡単に、SQL Server のコンテンツの種類を設計および展開できます。

## <a name="changes-in-ssdt-for-visual-studio-2019"></a>SSDT for Visual Studio 2019 の変更点

Visual Studio 2019 では、Analysis Services、Integration Services、Reporting Services のプロジェクトを有効にするために必要な機能がそれぞれの Visual Studio 拡張機能に移行されました。 データベース プロジェクトを作成するためのコア SSDT 機能は、引き続き Visual Studio に不可欠です (インストール中に [データの保存と処理] ワークロードを選択する必要があります)。 スタンドアロン SSDT のインストールは不要になりました。

Visual Studio 2019 のライセンスが既にある場合:

- SQL Database プロジェクトでは、Visual Studio の [データの保存と処理] ワークロードをインストールする
- Analysis Services、Integration Services または Reporting Services のプロジェクトでは、マーケットプレースから適切な[拡張機能](https://docs.microsoft.com/visualstudio/ide/finding-and-using-visual-studio-extensions)をインストールする

Visual Studio 2019 のライセンスがまだない場合:

- [Visual Studio 2019 Community](https://visualstudio.microsoft.com/downloads/) をインストールする
- Analysis Services、Integration Services、Reporting Services [拡張機能](https://docs.microsoft.com/visualstudio/ide/finding-and-using-visual-studio-extensions)を適宜インストールする

## <a name="changes-in-ssdt-for-visual-studio-2017"></a>SSDT for Visual Studio 2017 の変更点

Visual Studio 2017 以降では、データベース プロジェクトの作成機能が Visual Studio のインストールに統合されています。 Core SSDT エクスペリエンス用の SSDT のスタンドアロン インストーラーをインストールする必要はありません。 Integration Services/Analysis Services/Reporting Services のプロジェクトを作成するには、依然として SSDT のスタンドアロン インストーラーが必要です。

- データベース プロジェクトでは、Visual Studio の [データの保存と処理] ワークロードをインストールする
- Analysis Services、Integration Services または Reporting Services のプロジェクトでは、[SQL Server Data Tools](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt?view=sql-server-2017) をダウンロードしてインストールする

## <a name="install-ssdt-with-visual-studio-2017"></a>Visual Studio 2017 で SSDT をインストールする

[Visual Studio インストール](https://docs.microsoft.com/visualstudio/install/install-visual-studio)中に SSDT をインストールするには、 **[データの保存と処理]** ワークロードを選択し、 **[SQL Server Data Tools]** を選択します。 Visual Studio が既にインストールされている場合、[ワークロードの一覧を編集し](https://docs.microsoft.com/visualstudio/install/modify-visual-studio)、SSDT:![データの保存と処理ワークロード](../ssdt/media/download-sql-server-data-tools-ssdt/data-workload.png)を含めることができます。

## <a name="install-analysis-services-integration-services-and-reporting-services-tools"></a>Analysis Services、Integration Services、Reporting Services ツールをインストールする

AS、IS、RS プロジェクト サポートをインストールするには、[SSDT スタンドアロン インストーラー](#ssdt-for-vs-2017-standalone-installer)を実行します。

このインストーラーは、SSDT ツールの追加先となる Visual Studio インスタンスを一覧表示します。 Visual Studio がインストールされていない場合、 **[Install a new SQL Server Data Tools instance]\(新しい SQL Server Data Tools インスタンスをインストールする\)** を選択すると、SSDT と最小バージョンの Visual Studio がインストールされますが、SSDT と共に、最も使い勝手の良い[最新バージョンの Visual Studio](https://www.visualstudio.com/downloads) を利用することをお勧めします。

![AS、IS、RS を選択する](../ssdt/media/download-sql-server-data-tools-ssdt/select-services.png)

## <a name="ssdt-for-vs-2017-standalone-installer"></a>SSDT for VS 2017 (スタンドアロン インストーラー)

[![ダウンロード](../ssdt/media/download.png) SSDT for Visual Studio 2017 (15.9.2) をダウンロードする](https://go.microsoft.com/fwlink/?linkid=2095463)

> [!IMPORTANT]
> - SSDT for Visual Studio 2017 (15.9.2) をインストールする前に、*Analysis Services プロジェクト*と *Reporting Services プロジェクト*の拡張機能がインストールされている場合はアンインストールし、すべての VS インスタンスを閉じます。
> - Teradata のソース/変換先を含む SSIS パッケージを設計する場合は、Visual Studio 2017 (15.8.0) 以前のバージョン用の SSDT を使用してください。 15.8.0 より後の Visual Studio 2017 用の SSDT では、Attunity による Teradata のソース/変換先を含む SSIS パッケージを設計できません。

### <a name="version-information"></a>バージョン情報

リリース番号:15.9.2 ビルド番号:14.0.16194.0 リリース日:2019 年 7 月 17 日 

すべての変更の一覧については、「[SQL Server Data Tools (SSDT) リリース ノート](release-notes-ssdt.md)」をご覧ください。

SSDT for Visual Studio 2017 の[システム要件](https://docs.microsoft.com/visualstudio/productinfo/vs2017-system-requirements-vs)は Visual Studio と同じです。

### <a name="available-languages---ssdt-for-vs-2017"></a>使用できる言語 - SSDT for VS 2017

**SSDT for VS 2017** の今回のリリースは、次の言語でインストールできます。

- [簡体中国語]( https://go.microsoft.com/fwlink/?linkid=2095463&clcid=0x804)
- [繁体中国語]( https://go.microsoft.com/fwlink/?linkid=2095463&clcid=0x404)
- [英語 (米国)]( https://go.microsoft.com/fwlink/?linkid=2095463&clcid=0x409)
- [フランス語]( https://go.microsoft.com/fwlink/?linkid=2095463&clcid=0x40c)
- [ドイツ語]( https://go.microsoft.com/fwlink/?linkid=2095463&clcid=0x407)
- [イタリア語]( https://go.microsoft.com/fwlink/?linkid=2095463&clcid=0x410)
- [日本語]( https://go.microsoft.com/fwlink/?linkid=2095463&clcid=0x411)
- [韓国語]( https://go.microsoft.com/fwlink/?linkid=2095463&clcid=0x412)
- [ポルトガル語 (ブラジル)]( https://go.microsoft.com/fwlink/?linkid=2095463&clcid=0x416)
- [ロシア語]( https://go.microsoft.com/fwlink/?linkid=2095463&clcid=0x419)
- [スペイン語]( https://go.microsoft.com/fwlink/?linkid=2095463&clcid=0x40a)

## <a name="offline-install"></a>オフライン インストール

インターネットに接続されていない状態で SSDT をインストールするには、このセクションの手順に従います。 詳細については、「[Visual Studio 2017 のネットワーク インストールを作成する](https://docs.microsoft.com/visualstudio/install/create-a-network-installation-of-visual-studio)」を参照してください。

まず、**オンライン**のときに次の手順を完了します。

1. [SSDT スタンドアロン インストーラーをダウンロードします](#ssdt-for-vs-2017-standalone-installer)。
2. [Download vs_sql.exe](https://aka.ms/vs/15/release/vs_sql.exe)。
3. 引き続き、オンラインのときに、次のコマンドのいずれかを実行し、オフライン インストールに必要なすべてのファイルをダウンロードします。 `--layout` オプションの使用がキーとなり、オフライン インストールのために実際のファイルがダウンロードされます。 `<filepath>` はファイルを保存する実際のレイアウトのパスに置き換えます。
   1. 特定の言語には、`vs_sql.exe --layout c:\<filepath> --lang en-us` のようにロケールを渡します (1 つの言語は 1 GB まで)。
   1. すべての言語には、`vs_sql.exe --layout c:\<filepath>` のように `--lang` 引数を省略します (すべての言語は 3.9 GB まで)。

4. `SSDT-Setup-ENU.exe /layout c:\<filepath>` を実行して、VS2017 ファイルがダウンロードされたのと同じ `<filepath>` の場所に SSDT ペイロードを抽出します。 このアクションにより、両方からのすべてのファイルが 1 つのレイアウト フォルダーにまとめられます。

前述の手順を完了したら、以下の手順を**オフライン**で実行できます。

1. `vs_setup.exe --NoWeb` を実行して、VS2017 Shell と SQL Server Data Project をインストールします。
2. レイアウト フォルダーから `SSDT-Setup-ENU.exe /install` を実行し、SSIS/SSRS/SSAS を選択します。
   - 無人インストールを実行する場合は、`SSDT-Setup-ENU.exe /INSTALLALL[:vsinstances] /passive` を実行します。

利用可能なオプションについては、`SSDT-Setup-ENU.exe /help` を実行します。

> [!NOTE]
> Visual Studio 2017 の完全バージョンを使用する場合は、SSDT 専用のオフライン フォルダーを作成し、この新しく作成したフォルダーから `SSDT-Setup-ENU.exe` を実行します (別の Visual Studio 2017 のオフライン レイアウトに SSDT を追加しないでください)。 既存の Visual Studio のオフライン レイアウトに SSDT レイアウトを追加すると、必要なランタイム コンポーネント (.exe) がそこに作成されません。

### <a name="considerations-and-limitations"></a>注意点と制限事項

- コミュニティ バージョンをオフラインでインストールすることはできません
- SSDT をアップグレードするには、SSDT のインストールに使用したのと同じパスに従う必要があります。 たとえば、VSIX を使用して SSDT を追加した場合は、VSIX 経由でアップグレードします。 別のインストール経由で SSDT をインストールした場合は、その方法を使用してアップグレードする必要があります。

## <a name="supported-sql-versions"></a>サポートされる SQL のバージョン
 
|プロジェクト テンプレート|サポートされている SQL プラットフォーム| 
|-------------------|--------------------| 
|リレーショナル データベース| SQL Server 2005\* - SQL Server 2017<br> (SSDT 17.x または SSDT for Visual Studio 2017 を使って、[SQL Server on Linux](../linux/sql-server-linux-overview.md) に接続します)<br /><br />Azure SQL データベース<br /><br />Azure SQL Data Warehouse (クエリのみサポートします。データベース プロジェクトはまだサポートされていません)<br /><br /> \* SQL Server 2005 のサポートは非推奨とされます。<br /><br /> 正式にサポートされている SQL バージョンに移行します|
|Analysis Services モデル<br /><br />Reporting Services レポート | SQL Server 2008 - SQL Server 2017|
|Integration Services パッケージ| SQL Server 2012 - SQL Server 2019 |

## <a name="dacfx"></a>DacFx

SSDT for Visual Studio 2015 と SSDT for Visual Studio 2017 は、どちらも DacFx 17.4.1 を使用します。[データ層アプリケーション フレームワーク (DacFx) 17.4.1 をダウンロードする](https://www.microsoft.com/download/details.aspx?id=56508)。

## <a name="previous-versions"></a>以前のバージョン

Visual Studio 2015 の SSDT、または古いバージョンの SSDT をダウンロードしてインストールするには、「[SQL Server Data Tools (SSDT と SSDT-BI) の以前のリリース](previous-releases-of-sql-server-data-tools-ssdt-and-ssdt-bi.md)」を参照してください。

## <a name="next-steps"></a>次の手順

SSDT をインストールした後、次のチュートリアルを使用して、SSDT を使ったデータベース、パッケージ、データ モデル、およびレポートの作成方法を学ぶことができます。 

- [プロジェクト指向のオフライン データベース開発](project-oriented-offline-database-development.md) 
- [SSIS チュートリアル:シンプルな ETL パッケージの作成](../integration-services/ssis-how-to-create-an-etl-package.md) 
- [Analysis Services チュートリアル](https://docs.microsoft.com/analysis-services/analysis-services-tutorials-ssas) 
- [基本的なテーブル レポートの作成 (SSRS チュートリアル)](../reporting-services/create-a-basic-table-report-ssrs-tutorial.md) 

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]

## <a name="see-also"></a>参照

[SSDT MSDN フォーラム](https://social.msdn.microsoft.com/Forums/sqlserver/home?forum=ssdt) 
[SSDTチームのブログ](https://blogs.msdn.com/b/ssdt/) 
[DACFx API リファレンス](https://msdn.microsoft.com/library/dn645454.aspx) 
[SQL Server Management Studio (SSMS) のダウンロード](../ssms/download-sql-server-management-studio-ssms.md) 
