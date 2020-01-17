---
title: ダウンロードしてインストールする
titleSuffix: Azure Data Studio
description: Windows、macOS、または Linux 用の Azure Data Studio をダウンロードしてインストールします
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.custom: seodec18
ms.date: 12/26/2019
ms.reviewer: alayu; sstein
ms.openlocfilehash: e0094ffaaa1be646b470547277026385c9dae24e
ms.sourcegitcommit: 0d5b0aeee2a2b34fd448aec2e72c0fa8be473ebe
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/07/2020
ms.locfileid: "75727029"
---
# <a name="download-and-install-azure-data-studio"></a>Azure Data Studio のダウンロードとインストール

[!INCLUDE[name-sos](../includes/name-sos.md)] は、Windows、macOS、Linux 上で実行されます。


最新リリースのダウンロードとインストール:

> [!NOTE]
> SQL Operations Studio から更新していて、設定、キーボード ショートカット、またはコード スニペットを保持する場合は、「[ユーザー設定を移動する](#move-user-settings)」を参照してください。

|プラットフォーム|ダウンロード|リリース日| Version |
|:---|:---|:---|:---|
|Windows|[ユーザー インストーラー (推奨)](https://go.microsoft.com/fwlink/?linkid=2113530)<br>[システム インストーラー](https://go.microsoft.com/fwlink/?linkid=2113628)<br>[.zip](https://go.microsoft.com/fwlink/?linkid=2113529)|2019 年 12 月 26 日|1.14.1|
|macOS|[.zip](https://go.microsoft.com/fwlink/?linkid=2113528)|2019 年 12 月 26 日|1.14.1|
|Linux|[.deb](https://go.microsoft.com/fwlink/?linkid=2113344)<br>[.rpm](https://go.microsoft.com/fwlink/?linkid=2113718)<br>[.tar.gz](https://go.microsoft.com/fwlink/?linkid=2113627)|2019 年 12 月 26 日|1.14.1|

最新リリースに関する詳細については、[リリース ノート](release-notes.md)をご覧ください。

## <a name="get-azure-data-studio-for-windows"></a>Azure Data Studio for Windows を取得する

[!INCLUDE[name-sos](../includes/name-sos-short.md)] のこのリリースには、標準の Windows インストーラーのエクスペリエンスと、.zip ファイルが含まれています。

管理者特権を必要としないため、*ユーザー インストーラー*をお勧めします。これにより、インストールとアップグレードの両方が簡略化されます。 場所はユーザーの Local AppData (LOCALAPPDATA) フォルダーの下にあるため、ユーザー インストーラーに管理者特権は必要ありません。 また、ユーザーインストーラーでは、より滑らかなバックグラウンドの更新エクスペリエンスも提供されます。 詳細については、[Windows 用のユーザーのセットアップ](https://code.visualstudio.com/updates/v1_26#_user-setup-for-windows)に関するセクションを参照してください。

**ユーザー インストーラー** (推奨)

1. [Windows 用の [!INCLUDE[name-sos](../includes/name-sos-short.md)] *ユーザー* インストーラー](https://go.microsoft.com/fwlink/?linkid=2113530)をダウンロードして実行します。
2. [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] アプリを起動します。

**システム インストーラー**

1. [Windows 用の [!INCLUDE[name-sos](../includes/name-sos-short.md)] *システム* インストーラー](https://go.microsoft.com/fwlink/?linkid=2113628)をダウンロードして実行します。
2. [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] アプリを起動します。

**zip ファイル**

1. [[!INCLUDE[name-sos](../includes/name-sos-short.md)] .zip for Windows](https://go.microsoft.com/fwlink/?linkid=2113529) をダウンロードします。
2. ダウンロードしたファイルを参照して抽出します。
3. `\azuredatastudio-windows\azuredatastudio.exe` を実行します。


## <a name="get-azure-data-studio-for-macos"></a>Azure Data Studio for macOS を取得する

1. [[!INCLUDE[name-sos](../includes/name-sos-short.md)] for macOS](https://go.microsoft.com/fwlink/?linkid=2113528) をダウンロードします。
2. zip のコンテンツを展開するには、ダブルクリックします。
3. [!INCLUDE[name-sos](../includes/name-sos-short.md)] を*スタート パッド*で使用できるようにするには、*Azure Data Studio.app* を *[アプリケーション]* フォルダーにドラッグします。


## <a name="get-azure-data-studio-for-linux"></a>Linux 用の Azure Data Studio を取得する

1. インストーラーのいずれか、または tar.gz アーカイブを使用することで、Linux 用の [!INCLUDE[name-sos](../includes/name-sos-short.md)] をダウンロードします。
    - [.deb](https://go.microsoft.com/fwlink/?linkid=2113344)
    - [.rpm](https://go.microsoft.com/fwlink/?linkid=2113718)
    - [.tar.gz](https://go.microsoft.com/fwlink/?linkid=2113627)
1. ファイルを抽出して [!INCLUDE[name-sos](../includes/name-sos-short.md)] を起動するには、新しいターミナル ウィンドウを開いて次のコマンドを入力します。

   **Debian のインストール:**
   ```bash
   cd ~
   sudo dpkg -i ./Downloads/azuredatastudio-linux-<version string>.deb

   azuredatastudio
   ```

   **rpm のインストール:**
   ```bash
   cd ~
   yum install ./Downloads/azuredatastudio-linux-<version string>.rpm

   azuredatastudio
   ```

   **tar.gz のインストール:**
   ```bash 
   cd ~ 
   cp ~/Downloads/azuredatastudio-linux-<version string>.tar.gz ~ 
   tar -xvf ~/azuredatastudio-linux-<version string>.tar.gz 
   echo 'export PATH="$PATH:~/azuredatastudio-linux-x64"' >> ~/.bashrc
   source ~/.bashrc 
   azuredatastudio 
   ``` 

   > [!NOTE]
   > Debian、Redhat、および Ubuntu では、依存関係が不足する場合があります。 ご自身の Linux のバージョンに応じて、次のコマンドを使ってこれらの依存関係をインストールします。
   

   **Debian:** 
   ```bash
   sudo apt-get install libunwind8
   ```

   **Redhat:** 
   ```bash
   yum install libXScrnSaver
   ```

   **Ubuntu:** 
   ```bash
   sudo apt-get install libxss1

   sudo apt-get install libgconf-2-4

   sudo apt-get install libunwind8
   ```
## <a name="download-insiders-build-of-azure-data-studio"></a>Azure Data Studio の Insider ビルドをダウンロードする
一般に、ユーザーは上記の Azure Data Studio の安定したリリースをダウンロードする必要があります。 ただし、ベータ版の機能を試して、フィードバックをお寄せいただく場合は、[Azure Data Studio の Insider ビルド](https://github.com/microsoft/azuredatastudio#try-out-the-latest-insiders-build-from-master)をダウンロードできます。

## <a name="uninstall-azure-data-studio"></a>Azure Data Studio のアンインストール

Windows インストーラーを使用して [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] をインストールした場合は、Windows アプリケーションを削除するのと同じ方法でアンインストールします。

.zip やその他のアーカイブを使って [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] をインストールした場合は、シンプルにファイルを削除します。

## <a name="supported-operating-systems"></a>サポートされるオペレーティング システム

[!INCLUDE[name-sos](../includes/name-sos-short.md)] は、Windows、macOS、Linux 上で実行され、次のプラットフォーム上でサポートされます。

### <a name="windows"></a>Windows
- Windows 10 (64 ビット)
- Windows 8.1 (64 ビット)
- Windows 8 (64 ビット)
- Windows 7 (SP1) (64 ビット) - [KB2533623](https://www.microsoft.com/download/details.aspx?id=26767) が必要です
- Windows Server 2019
- Windows Server 2016
- Windows Server 2012 R2 (64 ビット)
- Windows Server 2012 (64 ビット)
- Windows Server 2008 R2 (64 ビット)

### <a name="macos"></a>macOS
- macOS 10.13 High Sierra
- macOS 10.12 Sierra

### <a name="linux"></a>Linux
- Red Hat Enterprise Linux 7.4
- Red Hat Enterprise Linux 7.3
- SUSE Linux Enterprise Server v12 SP2
- Ubuntu 16.04

## <a name="recommended-system-requirements"></a>推奨されるシステム要件

|             | CPU コア | メモリ/RAM |
|:-----------|:---------|:----------|
| 推奨 |     4     |      8 GB    |
|   最小値   |     2     |      4 GB     |
|             |           |            |

## <a name="check-for-updates"></a>更新プログラムをチェックする
最新の更新プログラムを確認するには、ウィンドウの左下にある歯車アイコンをクリックし、 **[更新プログラムのチェック]** をクリックします。

## <a name="supported-sql-offerings"></a>サポートされる SQL 製品

* このバージョンの Azure Data Studio は、すべての[サポート対象バージョンである SQL Server 2014 から [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]](https://support.microsoft.com/lifecycle?C2=1044) で動作し、Azure SQL Database および Azure SQL Data Warehouse で最新のクラウド機能と連携するためのサポートが提供されます。 Azure Data Studio では、Azure SQL Managed Instance のプレビューもサポートされています。

## <a name="upgrade-from-sql-operations-studio"></a>SQL Operations Studio からのアップグレード

引き続き SQL Operations Studio を使用している場合は、Azure Data Studio にアップグレードする必要があります。 SQL Operations Studio はプレビュー名であり、Azure Data Studio のプレビュー バージョンでした。 2018 年 9 月に、[名前を Azure Data Studio に変更](https://cloudblogs.microsoft.com/sqlserver/2018/09/25/azure-data-studio-for-sql-server/)し、一般公開 (GA) バージョンをリリースしました。 SQL Operations Studio は更新またはサポートされなくなったため、Microsoft では、すべての SQL Operations Studio ユーザーに、最新の機能、セキュリティ更新プログラム、修正プログラムを入手するため、最新バージョンの Azure Data Studio をダウンロードするように求めます。
 
以前のプレビューから最新の Azure Data Studio にアップグレードすると、現在の設定と拡張機能が失われます。 設定を移動するには、次の「*ユーザー設定を移動する*」セクションの手順に従います。


## <a name="move-user-settings"></a>ユーザー設定を移動する

カスタム設定、キーボード ショートカット、またはコード スニペットを移動する場合は、次の手順に従います。 これは SQL Operations Studio バージョンから Azure Data Studio にアップグレードする場合に重要です。

*既に Azure Data Studio がある場合、または SQL Operations Studio をインストールまたはカスタマイズしたことがない場合は、このセクションを無視することができます。*


1. 左下の歯車をクリックし、 **[設定]** をクリックすることで、[設定] を開きます。

   ![設定を開く](./media/download/open-settings.png)

2. 上部の **[ユーザー設定]** タブを右クリックし、 **[Explorer で表示]** をクリックします。

   ![Explorer で表示](./media/download/reveal-in-explorer.png)

3. このフォルダー内のファイルをすべてコピーし、[ドキュメント] フォルダーのように、ローカル ドライブ上の検索しやすい場所に保存します。

   ![設定のコピー](./media/download/copy-settings.png)

4. 新しいバージョンの Azure Data Studio で、手順 1 から 2 に従い、手順 3 で保存した内容をそのフォルダーに貼り付けます。 また、設定、キー バインド、またはスニペットをそれぞれの場所に手動でコピーすることもできます。

5. 既存のインストールをオーバーライドする場合は、インストールの前に古いインストール ディレクトリを削除して、リソース エクスプローラーの Azure アカウントに接続する際のエラーを回避します。

## <a name="next-steps"></a>次の手順

作業を開始するには、次のクイック スタートのいずれかを参照してください。
- [SQL Server に対する接続およびクエリ](quickstart-sql-server.md)
- [Azure SQL Database に対する接続およびクエリ](quickstart-sql-database.md)
- [Azure Data Warehouse に対する接続およびクエリ](quickstart-sql-dw.md)

[!INCLUDE[get-help-sql-tools](../includes/paragraph-content/get-help-sql-tools.md)]

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]

[Microsoft のプライバシーに関する声明](https://go.microsoft.com/fwlink/?LinkId=521839)と[利用状況データの収集](usage-data-collection.md)。
