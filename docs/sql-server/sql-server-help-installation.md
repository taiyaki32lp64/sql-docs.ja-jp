---
title: SQL Server のヘルプ コンテンツとヘルプ ビューアー | Microsoft Docs
ms.custom: ''
ms.date: 10/15/2019
ms.prod: sql
ms.technology: ''
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 51f8a08c-51d0-41d8-8bc5-1cb4d42622fb
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4be5552c60a6a401d9333976402088c7fa199f52
ms.sourcegitcommit: 4fb6bc7c81a692a2df706df063d36afad42816af
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/29/2019
ms.locfileid: "73049921"
---
# <a name="sql-server-offline-help-and-help-viewer"></a>SQL Server のオフライン ヘルプとヘルプ ビューアー

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Microsoft ヘルプ ビューアーを使用すると、オンライン ソースまたはローカル ディスクから SQL Server ヘルプ パッケージをダウンロードしてインストールできます。 インストール後、コンテンツをオフラインで表示できます。 ヘルプ ビューアーはさまざまなツールと共にインストールされます。 この記事では、ヘルプ ビューアーをインストールするためのツールの説明に加えて、オフライン ヘルプ コンテンツをインストールする方法とヘルプを表示する方法について説明します。

ヘルプ ビューアーのコンテンツをダウンロードするには、インターネットへのアクセスが必要です。 その後、インターネットにアクセスできないコンピューターにコンテンツを移行できます。

>[!NOTE]
> 現在のバージョンの SQL サーバー用のローカル コンテンツを取得するには、現在のバージョンの SQL Server Management Studio [SQL Server Management Studio 18.x](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) をインストールします。

## <a name="what-tools-install-the-help-viewer-versions"></a>ヘルプ ビューアーの各バージョンはどのツールでインストールされますか?

Microsoft ヘルプ ビューアーには 2 つのメジャー バージョンがあります。  バージョン 1.x と 2.x です。 各バージョンでは、異なるバージョンの SQL Server コンテンツがサポートされています。  オフライン ブックの形式は時間が経つ間に変化しており、古いバージョンのヘルプ ビューアーでは新しいバージョンのブックはサポートされていません。

|**コンテンツ セット**|**ヘルプ ビューアーをインストールするツール**|**ヘルプ ビューアーのバージョン**|
|-|-|-|
|SQL Server 2019 プレビュー <br> SQL Server 2017<br>SQL Server 2016|[Visual Studio 2019 (1)](https://docs.microsoft.com/visualstudio/install/install-visual-studio?view=vs-2019)<br>[Visual Studio 2017 (1)](https://docs.microsoft.com/visualstudio/install/install-visual-studio?view=vs-2017)<br>[SQL Server Management Studio 18.x](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)<br>[SQL Server Management Studio 17.x](https://docs.microsoft.com/sql/ssms/release-notes-ssms?view=sql-server-2017#download-ssms-1791)<br>[SQL Server Data Tools for Visual Studio 2015](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)<br>Visual Studio 2015 | v2.3<br>V2.2|
|SQL Server 2014<br>SQL Server 2012|SQL Server 2016 セットアップ (2)<br>SQL Server 2014 Management Studio<br>SQL Server 2014 セットアップ (2)<br>SQL Server Management Studio 2012<br>SQL Server 2012 セットアップ (2)| v1.x|
| | | |

(1) Visual Studio 2019 または 2017 でヘルプ ビューアーをインストールするには、Visual Studio インストーラーの [個別のコンポーネント] タブで、[コード ツール] にある **[ヘルプ ビューアー]** を選択し、 **[インストール]** をクリックします。

(2) SQL Server セットアップで "ドキュメント コンポーネント" オプションを示します。

>[!NOTE]
> - SQL Server 2016 ではヘルプ ビューアー 1.1 がインストールされますが、ヘルプ ビューアー 1.1 は SQL Server 2016 のヘルプ コンテンツをサポートしていません。 詳細については、「[SQL Server 2016 リリース ノート](sql-server-2016-release-notes.md)」を参照してください。  SQL Server 2016 コンテンツを表示するには、ヘルプ ビューアーの v2.x が必要です。 
> - SQL Server 2017 以降、SQL Server セットアップからヘルプ ビューアーをインストールできなくなりました。

## <a name="use-help-viewer-v2x"></a>ヘルプ ビューアー v2.x を使用する

**ヘルプ ビューアー v2.x を使用してオフライン ヘルプ コンテンツをダウンロードしてインストールするには**

1. SSMS または VS で、[ヘルプ] メニューにある **[ヘルプ コンテンツの追加と削除]** をクリックします。 

   ![ヘルプ ビューアー 2 の [ヘルプ コンテンツの追加と削除]](../sql-server/media/sql-server-help-installation/addremovecontent.png)  

   ヘルプ ビューアーが開き、[コンテンツの管理] タブが表示されます。  
   
2. 最新のヘルプ コンテンツ パッケージをインストールするには、[インストール元] の **[オンライン]** を選択します。
   
   ![HelpViewer2_ManageContent_OnlineSource](../sql-server/media/sql-server-help-installation/helpviewer2-managecontent-onlinesource.png)  
   
   >[!NOTE]
   > ディスクからインストールするには (SQL Server 2014 ヘルプ)、[インストール元] で **[ディスク]** を選択し、ディスクの場所を指定します。
   
   [コンテンツの管理] タブの [ローカル ストア パス] に、ローカル コンピューター上でのコンテンツのインストール先が表示されます。 場所を変更するには、 **[移動]** をクリックし、 **[宛先]** フィールドに異なるフォルダー パスを入力し、 **[OK]** をクリックします。
   ローカル ストア パスの変更後、ヘルプのインストールに失敗した場合、ヘルプ ビューアーを閉じ、再び開いてください。 新しい場所がローカル ストア パスに表示されることを確認し、インストールをもう一度試してください。

3. インストールする各コンテンツ パッケージ (ドキュメント) の横にある **[追加]** をクリックします。 
   SQL Server ヘルプ コンテンツをすべてインストールするには、SQL Server で 13 のドキュメント全部を追加します。 
   
4. 右下の **[更新]** をクリックします。 
   左側に表示されているヘルプの目次に、追加のドキュメントが自動的に反映されます。 
   
   ![HelpViewer2_ManageContent_AddContent](../sql-server/media/sql-server-help-installation/helpviewer2-managecontent-addcontent.png)     
   
> [!NOTE]
> SQL Server の目次にあるすべての最上位ノード タイトルが、対応するダウンロード可能なヘルプ ドキュメントの名前と厳密に一致するとは限りません。 目次のタイトルは、次のようにドキュメント名にマップされています。

(*) SQL Server 2017 コンテンツとそれより古い 2016 コンテンツの最初の一般公開バージョンからのコンテンツ。 SQL Server 2016 および 2017 用の独立した完全なブックには、2019 年 1 月時点でのコンテンツの編集が含まれるため、これらのブックは削除されます。  

| | コンテンツ ウィンドウ | SQL Server のドキュメント |
|-----|-----|-----|
|*|Analysis Services 言語のリファレンス | Analysis Services (MDX) 言語のリファレンス|
|*|Data Analysis Expressions (DAX) リファレンス | Data Analysis Expressions (DAX) リファレンス|
|*|データ マイニング拡張機能 (DMX) リファレンス | データ マイニング拡張機能 (DMX) リファレンス|
|*|SQL Server での機械学習の概要 | Microsoft Machine Learning Services|
|*|Power Query M リファレンス | Power Query M リファレンス|
||SQL Server 2016 ドキュメント | SQL Server 2016 ドキュメント|
||SQL Server 2017 ドキュメント| SQL Server 2017 ドキュメント|
|*|SQL Server の開発者ガイド | SQL Server 開発者用リファレンス|
|*|SQL Server Management Studio のダウンロード | SQL Server Management Studio|
|*|Microsoft SQL Server のクライアント プログラミングのホーム ページ | SQL Server 接続ドライバー|
|*|Linux 上の SQL Server | Linux 上の SQL Server|
|*|SQL Server 技術ドキュメント | SQL Server 技術ドキュメント (SSIS、SSRS、DB エンジン、セットアップ)|
|*|Azure SQL Database 用のツールとユーティリティ | SQL Server のツール|
|*|Transact-SQL リファレンス (データベース エンジン) | Transact-SQL リファレンス|
|*|XQuery 言語リファレンス (SQL Server) | XQuery 言語リファレンス (SQL Server)|

> [!NOTE]
> コンテンツの追加中にヘルプ ビューアーがフリーズ (ハング) した場合は、%LOCALAPPDATA%\Microsoft\HelpViewer2.x\HlpViewer_SSMSx_en-US.settings or HlpViewer_VisualStudiox_en-US.settings ファイル内の Cache LastRefreshed="\<mm/dd/yyyy> 00:00:00" 行を将来の日付に変更します。 この問題の詳細については、「 [Visual Studio ヘルプ ビューアーがフリーズする](/visualstudio/welcome-to-visual-studio)」を参照してください。

**SSMS でヘルプ ビューアー v2.x を使用してオフライン ヘルプ コンテンツを表示するには**

SSMS でインストールされたヘルプを表示するには、Ctrl + Alt + F1 キーを押すか、ヘルプ メニューの **[コンテンツの追加と削除]** を選択してヘルプ ビューアーを起動します。 

   ![ヘルプ ビューアー 2 の [ヘルプ コンテンツの追加と削除]](../sql-server/media/sql-server-help-installation/addremovecontent.png)  

ヘルプ ビューアーが開き、[コンテンツの管理] タブが表示されます。このタブの左側のウィンドウにインストールされたヘルプの目次が表示されます。 目次内の記事をクリックすると、右側のウィンドウに該当するトピックが表示されます。
> [!TIP]
> コンテンツ ウィンドウが表示されない場合は、左余白の [コンテンツ] をクリックします。 プッシュピン アイコンをクリックすると、コンテンツ ウィンドウは開いたままになります。  

   ![コンテンツが表示されたヘルプ ビューアー v2.x](../sql-server/media/sql-server-help-installation/helpviewer2-withcontentinstalled.png)

**VS でヘルプ ビューアー v2.x を使用してオフライン ヘルプ コンテンツを表示するには**

Visual Studio で、インストールされたヘルプを表示するには:
1. [ヘルプ] メニューの **[ヘルプ設定の設定]** をポイントし、 **[ヘルプ ビューアーで起動]** を選択します。 

   ![VS のヘルプ表示の設定、ヘルプ ビューアー](../sql-server/media/sql-server-help-installation/launchviewer.png)

2. [ヘルプ] メニューの **[ヘルプの表示]** をクリックして、ヘルプ ビューアーでコンテンツを表示します。 

   ![ヘルプの表示](../sql-server/media/sql-server-help-installation/viewhelp.png)

   左側にヘルプの目次が表示され、右側に選択したヘルプ記事が表示されます。
  
## <a name="use-help-viewer-v1x"></a>ヘルプ ビューアー v1.x を使用する

SSMS と VS の以前のバージョンではヘルプ ビューアー 1.x が使用されます。ヘルプ ビューアー 1.x は、SQL Server 2014 および 2012 のヘルプ コンテンツをサポートしています。 

**ヘルプ ビューアー v1.x でオフライン ヘルプ コンテンツをダウンロードしてインストールするには**

このプロセスでは、ヘルプ ビューアー 1.x を使用して Microsoft ダウンロード センターから SQL Server 2014 のヘルプをダウンロードして、コンピューターにインストールします。

1. [Microsoft SQL Server 2014 用の製品ドキュメント](https://www.microsoft.com/download/details.aspx?id=42557)のダウンロード サイトに移動し、 **[ダウンロード]** をクリックします。  
2. メッセージ ボックスの **[保存]** をクリックして、*SQLServer2014Documentation\_\*.exe* ファイルをコンピューターに保存します。  
   
   >[!NOTE]
   >ファイアウォールとプロキシによる制限がある環境では、環境内に持ち込むことができる USB ドライブか、その他のポータブル メディアにダウンロードを保存します。   
   
3. .exe をダブルクリックしてヘルプ コンテンツ ファイルをアンパックし、ローカルまたは共有のフォルダーにファイルを保存します。  
4. SSMS または VS を起動してから、[ヘルプ] メニューの **[ヘルプの設定の管理]** をクリックして、 **[ヘルプ ライブラリ マネージャー]** を開きます。  
5. **[ディスクからコンテンツをインストール]** をクリックし、ヘルプ コンテンツ ファイルをアンパックしたフォルダーを参照します。  
   
   ![HelpLibraryManager_MainPage_InstallFromDisk](../sql-server/media/sql-server-help-installation/helplibrarymanager-mainpage-installfromdisk.png)
   
   ![HelpLibraryManager_InstallContentFromDisk_dialog1](../sql-server/media/sql-server-help-installation/helplibrarymanager-installcontentfromdisk-dialog1.png)
   
   > [!IMPORTANT]
   > 目次の一部しかないローカル ヘルプ コンテンツがインストールされるのを防ぐには、 **[ヘルプ ライブラリ マネージャー]** の **[ディスクからコンテンツをインストール]** オプションを使用する必要があります。  **[オンラインからコンテンツをインストール]** を使用した場合は、ヘルプ ビューアーに部分的な目次が表示されます。トラブルシューティング手順については、こちらの[ブログ投稿](https://blogs.msdn.microsoft.com/womeninanalytics/2016/06/21/troubleshoot-local-help-for-sql-server-2014/)をご覧ください。 
   
8. HelpContentSetup.msha ファイルをクリックし、 **[開く]** をクリックして、 **[次へ]** をクリックします。  
9. インストールするドキュメントの横の **[追加]** をクリックし、 **[更新]** をクリックします。  
   
   ![HelpLibraryManager_InstallContentFromDisk_dialog2](../sql-server/media/sql-server-help-installation/helplibrarymanager-installcontentfromdisk-dialog2.png)  
   
10. **[完了]** をクリックして、 **[終了]** をクリックします。

**ヘルプ ビューアー v1.x を使用してオフライン ヘルプ コンテンツを表示するには**

11. インストールされたヘルプを表示するには、 **[ヘルプ ライブラリ マネージャー]** を開き、 **[オンラインまたはローカル ヘルプの選択]** をクリックして、 **[ローカル ヘルプを使用する]** をクリックします。
12. **[ヘルプ]** メニューの **[ヘルプの表示]** をクリックしてヘルプ ビューアーを開き、コンテンツを表示します。 インストールしたコンテンツは左側のウィンドウに表示されます。  
   
   ![HelpViewer1_withContentInstalled_ZoomedIn](../sql-server/media/sql-server-help-installation/helpviewer1-withcontentinstalled-zoomedin.png)  
   


## <a name="view-online-help"></a>オンライン ヘルプを表示する

オンライン ヘルプは常に最新のコンテンツを表示します。 

**SSMS 17.x で SQL Server オンライン ヘルプを表示するには**

- **[ヘルプ]** メニューの **[ヘルプの表示]** をクリックします。 [https://docs.microsoft.com/sql/sql-server/](https://docs.microsoft.com/sql/sql-server/) の最新の SQL Server 2016/2017 ドキュメントがブラウザーに表示されます。

   ![ヘルプの表示](../sql-server/media/sql-server-help-installation/viewhelp.png)

**Visual Studio で Visual Studio オンライン ヘルプを表示するには**

1. [ヘルプ] メニューの **[ヘルプ設定の設定]** をポイントし、 **[ブラウザーで起動]** または **[ヘルプ ビューアーで起動]** を選択します。 
2. [ヘルプ] メニューの **[ヘルプの表示]** をクリックします。 選択した環境で Visual Studio の最新のヘルプが表示されます。 

**ヘルプ ビューアー v1.x でオンライン ヘルプを表示するには**

1. [ヘルプ] メニューの **[ヘルプの設定の管理]** をクリックして、 **[ヘルプ ライブラリ マネージャー]** を開きます。  
2. [ヘルプ ライブラリ マネージャー] ダイアログ ボックスで、 **[オンラインまたはローカル ヘルプの選択]** をクリックします。  
   
   ![HelpLibraryManager_MainPage_ChooseOnlineORLocal.png](../sql-server/media/sql-server-help-installation/helplibrarymanager-mainpage-chooseonlineorlocal.png.png)  
   
3. **[オンライン ヘルプを使用する]** 、 **[OK]** 、 **[終了]** の順にクリックします。  
   
   ![HelpLibraryManager_ChooseOnlineORLocalHelp_OnlineHelpSelected_dialog](../sql-server/media/sql-server-help-installation/helplibrarymanager-chooseonlineorlocalhelp-onlinehelpselected-dialog.png)

4. **[ヘルプ]** メニューの **[ヘルプの表示]** をクリックしてヘルプ ビューアーを開き、コンテンツを表示します。

## <a name="view-f1-help"></a>F1 ヘルプを表示する

F1 を押すか、SSMS または VS のダイアログ ボックスで **[ヘルプ]** または **[?]** アイコンをクリックすると、 状況依存のオンライン ヘルプ記事がブラウザーまたはヘルプ ビューアーに表示されます。

**F1 ヘルプを表示するには**

1. [ヘルプ] メニューで **[ヘルプ設定の設定]** をクリックし、 **[ブラウザーで起動]** または **[ヘルプ ビューアーで起動]** を選択します。
2. F1 キーを押すか、 **[ヘルプ]** または **[?]** を、これらが利用できるダイアログ ボックスでクリックすると、 選択した環境で状況依存のオンライン トピックが表示されます。

> [!NOTE]
> F1 ヘルプは、オンラインのときにのみ機能します。 F1 ヘルプのオフライン ソースはありません。

## <a name="systems-without-internet-access"></a>インターネットに接続されていないシステム
インターネットにアクセスできるシステムでオフライン ブックをダウンロードした後は、次の手順を使用して、インターネットにアクセスできないシステムにコンテンツを移行することができます。

  >[!NOTE]
  >SQL Server Management Studio などのヘルプ ビューアーをサポートするソフトウェアを、オフライン システム上にインストールする必要があります。

1. ヘルプ ビューアーを開きます (Ctrl + Alt + F1)。
1. 関心があるドキュメントを選択します。 たとえば、SQL でフィルター処理し、SQL Server 技術ドキュメントを選択します。
1. ディスク上のファイルの物理パスを特定します。それは、 **[ローカル ストア パス]** で見つけることができます。
1. ご利用のファイル システム エクスプ ローラーを使用して、この場所に移動します。
    1.  既定の場所は次のとおりです。 `C:\Program Files (x86)\Microsoft SQL Server\140\Tools\Binn\ManagementStudio\Extensions\Application`
1. **ContentStore**、**Incoming**、**IndexStore** という 3 つのフォルダーを選択し、ご利用のオフライン システム上の同じ場所にコピーします。 USB や CD などの中間メディア デバイスを使用することが必要になる場合があります。
1. これらのファイルが移動されたら、オフライン システム上でヘルプ ビューアーを起動することで、SQL Server 技術ドキュメントを利用できるようになります。

![physical-location-of-offline-content.png](media/sql-server-help-installation/physical-location-of-offline-content.png)

## <a name="next-steps"></a>次の手順
[Microsoft ヘルプ ビューアー - Visual Studio](/visualstudio/ide/microsoft-help-viewer)  

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
