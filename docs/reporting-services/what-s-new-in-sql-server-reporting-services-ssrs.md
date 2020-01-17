---
title: Reporting Services (SSRS) の新機能 | Microsoft Docs
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
ms.reviewer: ''
ms.custom: ''
ms.date: 10/30/2019
ms.openlocfilehash: 0fea81e009d4d281c36d1882ac41835af609294b
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 11/04/2019
ms.locfileid: "73536282"
---
# <a name="whats-new-in-sql-server-reporting-services-ssrs"></a>SQL Server Reporting Services (SSRS) の新機能

[!INCLUDE[ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../includes/ssrs-appliesto-not-pbirs.md)]

SQL Server [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]のさまざまなバージョンの新機能について説明します。 この記事では、主要な機能領域を扱います。新しいアイテムがリリースされた場合は更新されます。

Power BI Report Server については、「[Power BI Report Server とは](https://docs.microsoft.com/power-bi/report-server/get-started)」を参照してください。

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"

## <a name="sql-server-2019-reporting-services"></a>SQL Server 2019 Reporting Services

**ダウンロードの**![ダウンロード](https://docs.microsoft.com/analysis-services/analysis-services/media/download.png "download")

[SQL Server 2019 Reporting Services](https://www.microsoft.com/download/details.aspx?id=100122)は、Microsoft ダウンロードセンターからダウンロードできます。

### <a name="azure-sql-managed-instance-support"></a>Azure SQL Managed Instance のサポート

VM またはデータセンターでホストされている Azure SQL Managed Instance (MI) で SQL Server Reporting Services (SSRS) に使用されるデータベースカタログをホストできるようになりました。 SQL MI への接続には、データベース資格情報の使用に制限されています。

### <a name="power-bi-premium-dataset-support"></a>データセットのサポートの Power BI Premium

Microsoft レポートビルダーまたは SQL Server Data Tools (SSDT) を使用して、Power BI データセットに接続できます。 次に、SQL Server Analysis Services 接続を使用してこれらのレポートを SSRS 2019 に発行できます。 ユーザーは、保存されている Windows ユーザー名とパスワードを使用してシナリオを有効にする必要があります。

### <a name="alttext-alternative-text-support-for-report-elements"></a>AltText (代替テキスト) レポート要素のサポート

レポート作成時に、ツールヒントを使用してレポートの各要素のテキストを指定できます。 スクリーンリーダーテクノロジは、これらのヒントを適切に識別します。

### <a name="azure-active-directory-application-proxy-support"></a>Azure Active Directory アプリケーション プロキシのサポート

Azure Active Directory アプリケーションプロキシでは、web アプリまたはモバイルアプリを使用してセキュリティで保護されたアクセスを可能にするために、独自の web アプリケーションプロキシを管理する必要がなくなりました。

### <a name="transparent-database-encryption"></a>Transparent Database Encryption

SQL Server 2019 では、Enterprise edition と Standard edition で、SSRS カタログデータベースの Transparent Database Encryption がサポートされるようになりました。 

### <a name="microsoft-report-builder-update"></a>Microsoft レポート ビルダーの更新プログラム

新しくリリースされたバージョンのレポートビルダーは、Reporting Services の2016、2017、2019の各バージョンと完全に互換性があります。 また、すべてのリリースバージョンとサポートされているバージョンの Power BI Report Server とも互換性があります。

::: moniker-end

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"

## <a name="sql-server-2017-reporting-services"></a>SQL Server 2017 Reporting Services

**ダウンロードの**![ダウンロード](https://docs.microsoft.com/analysis-services/analysis-services/media/download.png "download")

SQL Server 2017 Reporting Services をダウンロードするには、「 **[Microsoft ダウンロード センター](https://www.microsoft.com/download/details.aspx?id=55252)** 」に移動します。

### <a name="comments-on-reports"></a>レポートのコメント

レポートでコメントが使用できるようになり、分析観点の追加や、他のユーザーとの共同作業ができるようになりました。 コメントに添付ファイルを含めることもできます。

![レポート サーバー内のコメント](media/what-s-new-in-sql-server-reporting-services-ssrs/report-server-comments.png)

詳細については、「[レポート サーバーのレポートにコメントを追加する](https://powerbi.microsoft.com/documentation/reportserver-add-comments/)」を参照してください。

### <a name="dax-queries-in-reporting-tools"></a>レポート ツールの DAX クエリ

レポート ビルダーと SQL Server Data Tools の最新リリースでは、SQL Server Analysis Services 表形式データ モデルに対して、ネイティブの DAX クエリを作成できます。 クエリ デザイナーでフィールドをドラッグ アンド ドロップできます。 [Reporting Services のブログ](https://blogs.msdn.microsoft.com/sqlrsteamblog/2017/03/09/query-designer-support-for-dax-now-available-in-report-builder-and-sql-server-data-tools/)を参照してください。

### <a name="rest-api-support"></a>REST API のサポート

最新のアプリケーションとカスタマイズを開発できるようにするため、SQL Server Reporting Services は OpenAPI に完全に対応する RESTful API をサポートするようになりました。 API の完全な仕様とドキュメントは、[swaggerhub](https://app.swaggerhub.com/apis/microsoft-rs/SSRS/2.0) で入手できます。

### <a name="query-designer-support-for-dax-now-in-report-builder-and-sql-server-data-tools"></a>レポート ビルダーおよび SQL Server Data Tools での DAX に対するクエリ デザイナーのサポート

レポート ビルダーと SQL Server Data Tools で、サポートされている SQL Server Analysis Services 表形式データ モデルに対して、ネイティブの DAX クエリが作成できるようになりました。 どちらのツールでも、クエリ デザイナーを使って、必要なフィールドをドラッグ アンド ドロップできます。 そうすると、DAX クエリが自動的に生成されます。

詳細については、[Reporting Services のブログ](https://blogs.msdn.microsoft.com/sqlrsteamblog/2017/03/09/query-designer-support-for-dax-now-available-in-report-builder-and-sql-server-data-tools/)を参照してください。

* [Microsoft SQL Server レポート ビルダー](https://go.microsoft.com/fwlink/?LinkId=734968)のダウンロード
* [SQL Server Data Tools - リリース候補](https://docs.microsoft.com/sql/ssdt/sql-server-data-tools-ssdt-release-candidate)のダウンロード

> [!NOTE]
> DAX のクエリ デザイナーは、SQL Server 2016+ に組み込まれた SSAS 表形式のデータ ソースでのみ使用できます。
::: moniker-end

## <a name="ssrs-2016"></a>SSRS 2016

### <a name="reporting-services-includessrswebportal-non-markdownincludesssrswebportal-non-markdown-mdmd"></a>Reporting Services [!INCLUDE[ssRSWebPortal-Non-Markdown](../includes/ssrswebportal-non-markdown-md.md)]  

新しい [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] [!INCLUDE[ssRSWebPortal-Non-Markdown](../includes/ssrswebportal-non-markdown-md.md)] を利用できます。 更新された Web ポータルには次が含まれています
- KPI
- モバイル レポート
- ページネーションのあるレポート
- Excel ファイル
- Power BI Desktop ファイル

以前のリリースの Report Manager がこの [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)] に置き換えられています。

モバイル レポートを作成するには、[!INCLUDE[SS_MobileReptPub_Short](../includes/ss-mobilereptpub-short.md)] が必要です。

[!INCLUDE[ssRSWebPortal-Non-Markdown](../includes/ssrswebportal-non-markdown-md.md)]の詳細については、「 [Web ポータル (SSRS ネイティブ モード)](../reporting-services/web-portal-ssrs-native-mode.md)」を参照してください。  

![ssRSPortal](../reporting-services/media/ssrsportal.png "ssRSPortal")  

#### <a name="custom-branding-for-the-includessrswebportal-non-markdownincludesssrswebportal-non-markdown-mdmd"></a>[!INCLUDE[ssRSWebPortal-Non-Markdown](../includes/ssrswebportal-non-markdown-md.md)] のカスタム ブランド化 

ブランド化パックを使用して、組織のロゴや色で [!INCLUDE[ssRSWebPortal-Non-Markdown](../includes/ssrswebportal-non-markdown-md.md)] をカスタマイズできます。  

カスタムブランド化の詳細については、「 [Web ポータルのブランド化](https://msdn.microsoft.com/6dac97f7-02a6-4711-81a3-e850a6b40bf1)」を参照してください。

#### <a name="key-performance-indicators-kpi-in-the-includessrswebportal-non-markdownincludesssrswebportal-non-markdown-mdmd"></a>[!INCLUDE[ssRSWebPortal-Non-Markdown](../includes/ssrswebportal-non-markdown-md.md)] での主要業績評価指標 (KPI) 

現在のフォルダーのコンテキストに適合する KPI を [!INCLUDE[ssRSWebPortal-Non-Markdown](../includes/ssrswebportal-non-markdown-md.md)] 内で直接作成します。 KPI を作成するときに、データセットを選択し、その値を集計できます。 ドリル スルーする関連コンテンツを選択して、詳細を公開することもできます。

![ssrs-webportal-kpi](../reporting-services/media/ssrs-webportal-kpi.png)

詳細については、「 [Reporting Services で KPI を使用する](https://msdn.microsoft.com/a28cf500-6d47-4268-a248-04837e7a09eb)」を参照してください。

### <a name="mobile-reports"></a>モバイル レポート

Reporting Services モバイル レポートは、多様なフォーム ファクター用に最適化された専用レポートであり、モバイル デバイスでレポートにアクセスするユーザーに最適なエクスペリエンスを提供します。 モバイル レポートでは、時間、カテゴリ、比較のグラフから、ツリーマップやカスタム マップまで、多種多様な視覚化を使用できます。 モバイル レポートは、オンプレミスの SQL Server Analysis Services 多次元およびテーブル データを含むさまざまなデータ ソースに接続できます。 グリッド行および列を調節したデザイン サーフェイス上に、モバイル レポート用のフィールドを配置できます。 柔軟なモバイル レポート要素は、任意の画面サイズに合わせて自動的に拡大縮小します。 Reporting Service サーバーに保存したモバイル レポートを、ブラウザーまたは Power BI モバイル アプリで表示および操作できます。 次のデバイスがサポートされています。

- iPad
- iPhones
- Android フォン
- または Windows 10 デバイス

#### <a name="mobile-report-publisher"></a>Mobile Report Publisher  

[!INCLUDE[SS_MobileReptPub_Long](../includes/ss-mobilereptpub-long.md)]では、SQL Server モバイル レポートを作成して [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] [!INCLUDE[ssRSWebPortal-Non-Markdown](../includes/ssrswebportal-non-markdown-md.md)]に公開できます。  

![SS_MRP_LayoutTabSmall](../reporting-services/media/ss-mrp-layouttabsm.png "|::ref4::|")  

詳細については、「 [SQL Server Mobile Report Publisher を使用してモバイル レポートを作成する](../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)」をご覧ください。  

#### <a name="sql-server-mobile-reports-hosted-in-reporting-services-available-in-power-bi-mobile-app"></a>Reporting Services でホストされている SQL Server モバイル レポートを Power BI モバイル アプリで使用可能  

iPad および iPhone の iOS 用 Power BI モバイル アプリでは、ローカル レポート サーバーでホストされている SQL Server モバイル レポートを表示できるようになりました。  

![SS_MRP_iPad_HomeSm](../reporting-services/media/ss-mrp-ipad-homesm.png "|::ref5::|")  

一部の構成を変更しないと、既定では接続できません。 Power BI モバイル アプリがレポート サーバーに接続できるようにする方法の詳細については、「 [Power BI モバイル アクセス用のレポート サーバーを有効にする](../reporting-services/report-server/enable-a-report-server-for-power-bi-mobile-access.md)」をご覧ください。

### <a name="support-of-sharepoint-mode-and-sharepoint-2016"></a>SharePoint モードと SharePoint 2016 のサポート  

[!INCLUDE[ssSQL15](../includes/sssql15-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] では、SharePoint 2013 および SharePoint 2016 との統合をサポートしています。

詳細については、以下をご覧ください。  

- [SharePoint、Reporting Services サーバー、Reporting Services アドインのサポートされる組み合わせ &#40;SQL Server 2016&#41;](../reporting-services/install-windows/supported-combinations-of-sharepoint-and-reporting-services-server.md)  

- [SharePoint 製品用 Reporting Services アドインの検索場所](../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)  

- [Reporting Services SharePoint モードのインストール](../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md)  

### <a name="microsoft-net-framework-4-support"></a>Microsoft .NET Framework 4 のサポート  

[!INCLUDE[ssRSCurrent-md](../includes/ssrscurrent-md.md)] では、Microsoft .NET Framework 4 の現在のバージョン (バージョン 4.0 と 4.5.1 を含む) がサポートされています。 .Net Framework のバージョン 4.x がまだインストールされていない場合、[!INCLUDE[ssNoVersion-md](../includes/ssnoversion-md.md)] のセットアップにより、機能のインストール手順の間に .NET 4.0 がインストールされます。  

### <a name="report-improvements"></a>レポートの強化機能

**HTML5 レンダリング エンジン:** 新しい HTML5 レンダリング エンジンは、最新の Web の "完全" 標準モードと最新ブラウザーを対象としています。  新しいレンダリング エンジンは、一部の古いブラウザーで使用される互換モードに依存しなくなりました。

ブラウザーのサポートの詳細については、「 [Reporting Services と Power View のブラウザー サポート](../reporting-services/browser-support-for-reporting-services-and-power-view.md)」を参照してください。  

**最新のページ分割されたレポート:** グラフ、ゲージ、マップ、その他のデータ ビジュアル化のための最新スタイルで改ページ調整されたレポートを美しくデザインします。

**ツリー マップとサンバースト グラフ:** ツリーマップ ![ssrs_treemap_icon](../reporting-services/media/ssrs-treemap-icon.png "|::ref6::|") とサンバースト グラフ ![ssrs_sunburst_icon](../reporting-services/media/ssrs-sunburst-icon.png "|::ref7::|") を使用してレポートを強化できます。これらは、階層データを表示する優れた方法です。 詳細については、「 [Reporting Services のツリー マップとサンバースト グラフ](../reporting-services/report-design/tree-map-and-sunburst-charts-in-reporting-services.md)」を参照してください。  

**レポートの埋め込み:** モバイルおよびページ分割されたレポートを、URL パラメーターと共に、他の Web ページに (また、iframe を使ってアプリケーションに) 埋め込むことができるようになりました。  

**レポートアイテムの Power BI ダッシュボードへのピン留め:** [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)]でレポートを表示しているときに、レポート アイテムを選択し、 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] ダッシュボードにピン留めできます。   ピン留めできるアイテムは、グラフ、ゲージ パネル、マップ、イメージです。 可能な代替手段としては以下の方法があります。

1. ピン留めするダッシュボードを含むグループを選択します。
2. アイテムをピン留めするダッシュボードを選択します。
3. ダッシュボードのタイルをどのくらいの頻度で更新するかを選択します。

![注](https://docs.microsoft.com/analysis-services/analysis-services/instances/install-windows/media/ssrs-fyi-note.png "note") 更新は [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] サブスクリプションによって管理されます。アイテムをピン留めした後に、サブスクリプションを編集し、別の更新スケジュールを構成できます。

![ssRS_Pin_to_PowerBI](../reporting-services/media/ssrs-pin-to-powerbi.png) 

詳細については、「[Power BI Report Server の統合 &#40;構成マネージャー&#41;](../reporting-services/install-windows/power-bi-report-server-integration-configuration-manager.md)」および「[Power BI ダッシュボードへの Reporting Services のアイテムのピン留め](../reporting-services/pin-reporting-services-items-to-power-bi-dashboards.md)」を参照してください。  

**PowerPoint のレンダリングとエクスポート:** Microsoft PowerPoint (PPTX) 形式は、 [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] の新しい表示拡張機能です。 通常のアプリケーション (レポート ビルダー、レポート デザイナー (SSDT)、および [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)]) から PPTX 形式のレポートをエクスポートできます。 たとえば、次の図は [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)]のエクスポート メニューを示しています。 

![ssrs-export-powerpoint](../reporting-services/media/ssrs-export-powerpoint.png) 

サブスクリプション出力用に PPTX 形式を選択し、レポート サーバー URL アクセスを使用してレポートをレンダリングおよびエクスポートすることもできます。 たとえば、ブラウザーで次の URL コマンドを実行すると、レポート サーバーの名前付きインスタンスからレポートがエクスポートされます。  

```https
https://servername/ReportServer_THESQLINSTANCE/Pages/ReportViewer.aspx?%2freportfolder%2freport+name+with+spaces&rs:Format=pptx  
```  

詳細については、「 [URL アクセスを使用してレポートをエクスポート](../reporting-services/export-a-report-using-url-access.md)」を参照してください。

**リモート印刷での PDF による ActiveXの置き換え:** レポート ビューアー ツール バーでの印刷が、ActiveX コントロールではなく PDF を使うようになりました。 新しいレポート ビューアーは、Microsoft Edge を含む、ほとんどの最新ブラウザーでサポートされています。 ActiveX コントロールをダウンロードする必要はなくなります。 使用するブラウザーと、インストールされている PDF 表示アプリケーションおよびサービスに応じて、[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] ではレポートを印刷するための印刷ダイアログ ボックスが開かれるか、.PDF ファイルをダウンロードするプロンプトが表示されます。 管理者が [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] からクライアント側の印刷を無効にすることもできます。

詳細については、「 [Reporting Services のクライアント側印刷機能の有効化と無効化](../reporting-services/report-server/enable-and-disable-client-side-printing-for-reporting-services.md)」を参照してください。

![ssrs-pdf-printing](../reporting-services/media/ssrs-pdf-printing.png)

### <a name="subscription-improvements"></a>サブスクリプションの機能強化  

|機能|サポートされるサーバー モード|  
|-------------|---------------------------|  
|**サブスクリプションを有効または無効にする**: サブスクリプションを簡単に無効または有効にできる新しいユーザー インターフェイス オプション。 サブスクリプションを無効にしても、スケジュールなどの他の構成プロパティは維持され、簡単に有効にすることができます。<br /><br /> ![ssrs-enable-disable-subscriptions](../reporting-services/media/ssrs-enable-disable-subscriptions.png)<br /><br /> 詳細については、「 [レポートとサブスクリプションの処理を無効化または一時停止する](../reporting-services/subscriptions/disable-or-pause-report-and-subscription-processing.md)」を参照してください。|ネイティブ モード|  
|**サブスクリプションの説明**: 新しいサブスクリプションを作成するときに、サブスクリプションのプロパティの一部として、レポートの説明を含めることができるようになりました。 説明はサブスクリプションの概要ページに表示されます。|SharePoint モードとネイティブ モード|  
|**サブスクリプションの所有者の変更**: サブスクリプションの所有者をすばやく変更できる拡張ユーザー インターフェイス。 以前のバージョンの [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] では、管理者はスクリプトを使用してサブスクリプションの所有者を変更できます。 [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] リリース以降では、ユーザー インターフェイスまたはスクリプトを使用してサブスクリプションの所有者を変更できます。 サブスクリプションの所有者の変更は、ユーザーが組織を離れたり、組織での役割が変更されたりしたときに行う一般的な管理タスクです。|SharePoint モードとネイティブ モード|  
|**ファイル共有サブスクリプションの共有資格情報**: [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] のファイル共有サブスクリプションには、現在 2 つのワークフローがあります。<br /><br /> このリリースの新機能として、[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] の管理者が、複数のサブスクリプションで使える 1 つのファイル共有アカウントを構成できるようになりました。 ファイル共有アカウントは、[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] のネイティブ モードの構成マネージャー **[ファイル共有アカウントを指定します]** で構成されます。 ユーザーは、サブスクリプションの構成ページで、 **[ファイル共有アカウントを使用する]** を選択します。<br /><br /> 宛先のファイル共有の具体的な資格情報を使って、個々のサブスクリプションを構成します。<br /><br /> この 2 つの方法を組み合わせて、一部のファイル共有サブスクリプションでは管理者が構成したファイル共有アカウントを使用し、他のサブスクリプションでは特定の資格情報を使用することもできます。|ネイティブ モード|

### <a name="sql-server-data-tools-ssdt"></a>SQL Server Data Tools (SSDT)

新しいリリースの SSDT には、 [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)]用のプロジェクト テンプレート (レポート サーバー プロジェクト ウィザードとレポート サーバー プロジェクト) が含まれています。 SSDT のダウンロードについては、 [SQL Server Data Tools for Visual Studio 2015](https://go.microsoft.com/fwlink/?LinkId=827542)に関するページをご覧ください。  

### <a name="report-builder-improvements"></a>レポート ビルダーの機能強化

**新しいレポート ビルダーのユーザー インターフェイス:** [!INCLUDE[ssRBnoversion](../includes/ssrbnoversion.md)] コア ユーザー インターフェイスの UI 要素が簡素化され、最新の外観になりました。  

|||  
|-|-|  
|ボタンを使用して新しい|Previous|  
|![ssrs_rbfacelift_new](../reporting-services/media/ssrs-rbfacelift-new.png "|::ref9::|")|![ssrs_rbfacelift_old](../reporting-services/media/ssrs-rbfacelift-old.png "|::ref10::|")|  

**カスタム パラメーター ペイン:** ペインをカスタマイズできるようになりました。 レポート ビルダーのデザイン サーフェイスを使用して、パラメーター ペインの特定の列や行にパラメーターをドラッグできます。 列を追加または削除して、ペインのレイアウトを変更することもできます。 詳細については、「 [レポートのパラメーター ペインをカスタマイズする (レポート ビルダー)](../reporting-services/report-design/customize-the-parameters-pane-in-a-report-report-builder.md)で作成するモバイル レポートで使用できます。  

![レポートデータペインとパラメーターペインのパラメーターリスト](../reporting-services/media/ssrs-customizeparameter-parameterlist-reportdatapane.png "|::ref11::|")  

**高 DPI のサポート:** [!INCLUDE[ssRBnoversion](../includes/ssrbnoversion.md)] では、高 DPI (インチあたりのドット数) スケーリングと高 DPI デバイスがサポートされます。  高 DPI の詳細については、次の記事をご覧ください。  

- [Windows 8.1 の DPI スケーリング拡張機能](https://blogs.windows.com/windowsexperience/2013/07/15/windows-8-1-dpi-scaling-enhancements/)  

- [高 DPI と Windows 8.1](https://technet.microsoft.com/library/dn528848.aspx)  

## <a name="next-steps"></a>次の手順

[Analysis Services の新機能](https://msdn.microsoft.com/aa69c299-b8f4-4969-86d8-b3292fe13f08)  
[旧バージョンとの互換性](reporting-services-backward-compatibility.md)  
[SQL Server の各エディションがサポートする Reporting Services の機能](../reporting-services/reporting-services-features-supported-by-the-editions-of-sql-server-2016.md)  
[Reporting Services のアップグレードと移行](../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)  
[Reporting Services](../reporting-services/create-deploy-and-manage-mobile-and-paginated-reports.md)  

その他の質問 [Reporting Services のフォーラムに質問してみてください](https://go.microsoft.com/fwlink/?LinkId=620231)
