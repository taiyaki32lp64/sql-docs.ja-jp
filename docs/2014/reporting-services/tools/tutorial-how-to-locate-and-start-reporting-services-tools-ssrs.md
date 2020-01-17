---
title: チュートリアル:Reporting Services ツールを検索および開始する方法 (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Report Builder 1.0, locating and starting tool
- Reporting Services, tutorials
- Reporting Services, tools
- Reporting Services Configuration tool
- Business Intelligence Development Studio, locating and starting tool
- Model Designer [Reporting Services], locating and starting tool
- Report Designer [Reporting Services], tutorials
- tools [Reporting Services]
- tutorials [Reporting Services]
- Report Manager [Reporting Services]
ms.assetid: 51ad69d8-fe92-4662-a7cd-d235692f0c03
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 4edd0b6e3928a2bc3a280403a87eda5bb797e620
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66099478"
---
# <a name="tutorial-how-to-locate-and-start-reporting-services-tools-ssrs"></a>チュートリアル:Reporting Services ツールを検索および開始する方法 (SSRS)
  このチュートリアルでは、レポート サーバーの設定、レポート サーバーのコンテンツと動作の管理、レポートの作成とパブリッシュに使用できるツールを紹介します。 このチュートリアルの目的は、ツールを初めて使用する場合にそれぞれのツールをすぐに見つけて起動できるようにすることです。 既にツールを使用している場合は、 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]を使用するときの重要なスキルを学ぶことができるその他のチュートリアルへお進みください。 その他のチュートリアルの詳細については、次を参照してください。 [Reporting Services のチュートリアル&#40;SSRS&#41;](../reporting-services-tutorials-ssrs.md)します。  
  
 このトピックの内容  
  
-   [Reporting Services Configuration Manager (ネイティブ モード)](#bkmk_configuration_manager)  
  
-   [レポート マネージャー (ネイティブ モード)](#bkmk_report_manager)  
  
-   [Management Studio](#bkmk_managements_studio)  
  
-   [レポート デザイナーとレポート ウィザードで SQL Server Data Tools](#bkmk_ssdt)  
  
-   [レポート ビルダー](#bkmk_report_builder)  
  
##  <a name="bkmk_configuration_manager"></a> Reporting Services 構成マネージャー (ネイティブ モード)  
 ネイティブ モードの構成マネージャーを使用して、次の処理を行います。  
  
-   サービス アカウントを指定します。  
  
-   レポート サーバー データベースを作成またはアップグレードします。  
  
-   接続プロパティを変更します。  
  
-   URL を指定します。  
  
-   暗号化キーを管理します。  
  
-   自動レポート処理および電子メールによるレポート配信を構成します。  
  
 **インストール:** [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 構成マネージャーは、[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] ネイティブ モードのインストール時にインストールされます。 詳細については、「 [Reporting Services ネイティブ モードのレポート サーバーのインストール](../install-windows/install-reporting-services-native-mode-report-server.md)」を参照してください。  
  
#### <a name="to-start-the-reporting-services-configuration-manager"></a>Reporting Services 構成マネージャーを起動するには  
  
1.  Windows スタート画面で、「`reporting`し、**アプリ**検索結果で、[] をクリック**Reporting Services 構成マネージャー**します。  
  
     ![Reporting Services 構成マネージャーの起動](../media/bi-ssrs-configmanager-win8-startscreen.gif "Reporting Services 構成マネージャーの起動")  
  
     **Or**  
  
     **[スタート]** ボタンをクリックして、 **[プログラム]** をクリックし、[ [!INCLUDE[ssCurrentUI](../../../includes/sscurrentui-md.md)]]、 **[構成ツール]** 、 **[Reporting Services 構成マネージャー]** の順にクリックします。  
  
     **[レポート サーバー インスタンスの選択]** ダイアログ ボックスが表示されます。このダイアログ ボックスでは構成するレポート サーバー インスタンスを選択します。  
  
2.  **[サーバー名]** ボックスに、レポート サーバー インスタンスがインストールされているコンピューターの名前を指定します。 既定ではローカル コンピューターの名前が設定されていますが、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のリモート インスタンスの名前を入力することもできます。  
  
     リモート コンピューターを指定する場合は、 **[検索]** をクリックして接続を確立します。 ここで指定するレポート サーバーは、リモートで管理するための構成が事前に行われている必要があります。 詳細については、「 [リモート管理用のレポート サーバーの構成](../report-server/configure-a-report-server-for-remote-administration.md)」を参照してください。  
  
3.  **stance Name**で、構成する [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] インスタンスを選択します。 この一覧には [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]、 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、および [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] のレポート サーバー インスタンスのみが表示されます。 以前のバージョンの [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]を構成することはできません。  
  
4.  **[接続]** をクリックします。  
  
5.  ツールが起動したかどうかを確認するには、次の図と比較します。  
  
     ![Reporting Services 構成ツール](../media/rs-ui-reportserverconfigkatmai.gif "Reporting Services 構成ツール")  
  
 **次の手順:** 「[レポート サーバーを構成および管理する (SSRS ネイティブ モード)](../report-server/configure-and-administer-a-report-server-ssrs-native-mode.md)」と「[Reporting Services 構成マネージャー (ネイティブ モード)](../../sql-server/install/reporting-services-configuration-manager-native-mode.md)」。  
  
##  <a name="bkmk_report_manager"></a> レポート マネージャー (ネイティブ モード)  
 使用[レポート マネージャー &#40;SSRS ネイティブ モード&#41;](../report-manager-ssrs-native-mode.md)と、アクセス許可を設定、サブスクリプションおよびスケジュールの管理、レポートを使用します。 また、レポート マネージャーを使ってレポートを閲覧することもできます。  
  
 **インストール:** インストールすると、レポート マネージャーがインストールされている[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]ネイティブ モード。[Reporting Services ネイティブ モードのレポート サーバーのインストール](../install-windows/install-reporting-services-native-mode-report-server.md)  
  
 レポート マネージャーを起動するには適切なアクセス許可が必要です。初期状態では、レポート マネージャーの機能へのアクセス許可は、ローカルの管理者グループのメンバーにのみ与えられています。 レポート マネージャーに表示されるページとオプションは、現在のユーザーに割り当てられているロールによって異なります。 アクセス許可のないユーザーには空白のページが表示され、 レポート閲覧用のアクセス許可が与えられているユーザーにはリンクが表示されます。このユーザーはリンクをクリックしてレポートを表示することができます。 アクセス許可の詳細については、「[ロールと権限 &#40;Reporting Services&#41;](../security/roles-and-permissions-reporting-services.md)」を参照してください。  
  
#### <a name="to-start-report-manager"></a>レポート マネージャーを起動するには  
  
1.  ブラウザーを開きます。 サポートされているブラウザーおよびブラウザー バージョンについては、次を参照してください。 [Reporting Services と Power View のブラウザー サポートの計画&#40;Reporting Services 2014&#41;](../browser-support-for-reporting-services-and-power-view.md)します。  
  
2.  Web ブラウザーのアドレス バーに、レポート マネージャーの URL を入力します。 既定では、URL は**http://\<serverName >/reports**します。 Reporting Services 構成ツールを使用して、サーバー名と URL を確認できます。 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] で使用される URL の詳細については、「[レポート サーバー URL の構成 &#40;SSRS 構成マネージャー&#41;](../install-windows/configure-report-server-urls-ssrs-configuration-manager.md)」を参照してください。  
  
3.  レポート マネージャーがブラウザー ウィンドウ内に表示されます。 最初のページは [ホーム] フォルダーです。 アクセス許可に応じて、最初のページにその他のフォルダー、レポートへのハイパーリンク、リソース ファイルなどが表示される場合もあります。 ツール バーに追加のボタンやコマンドが表示される場合もあります。  
  
4.  ローカル レポート サーバーでレポート マネージャーを実行する場合は、次を参照してください。[ローカル管理用のネイティブ モード レポート サーバーの構成&#40;SSRS&#41;](../report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md)します。  
  
 **次の手順:** [レポート マネージャーの構成&#40;ネイティブ モード&#41;](../report-server/configure-web-portal.md)します。  
  
##  <a name="bkmk_managements_studio"></a> Management Studio  
 レポート サーバー管理者は、 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] を使用して、レポート サーバーと共に他の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] コンポーネント サーバーを管理できます。 詳細については、「 [Use SQL Server Management Studio](../../database-engine/use-sql-server-management-studio.md)」を参照してください。  
  
#### <a name="to-start-sql-server-management-studio"></a>SQL Server Management Studio を起動するには  
  
1.  Windows スタート画面「から`sql server`し、**アプリ**検索結果で、[] をクリック**SQL Server Management Studio**します。  
  
     ![Windows のスタート画面の Management Studio](../media/bi-ssms-win8-startscreen.gif "Windows のスタート画面の Management Studio")  
  
     **Or**  
  
     **[スタート]** 、 **[すべてのプログラム]** とクリックし、[ [!INCLUDE[ssCurrentUI](../../../includes/sscurrentui-md.md)]]、 **[SQL Server Management Studio]** の順にクリックします。 **[サーバーへの接続]** ダイアログ ボックスが表示されます。  
  
2.  **[サーバーへの接続]** ダイアログ ボックスが表示されない場合は、 **[オブジェクト エクスプローラー]** で **[接続]** をクリックし、 **[Reporting Services]** を選択します。  
  
3.  **[サーバーの種類]** ボックスの一覧で、 **[Reporting Services]** を選択します。 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] が一覧に表示されない場合、Reporting Services はインストールされていません。  
  
4.  **[サーバー名]** ボックスの一覧で、レポート サーバーのインスタンスを選択します。 一覧にはローカル インスタンスが表示されますが、 リモートの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスの名前を入力することもできます。  
  
5.  **[接続]** をクリックします。 ルート ノードを展開して、サーバーのプロパティを設定したり、ロールの定義を変更したり、レポート サーバー機能をオフにすることができます。  
  
##  <a name="bkmk_ssdt"></a> レポート デザイナーとレポート ウィザードが統合された SQL Server データ ツール  
 レポート デザイナーは、[!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] - Business Intelligence for Visual Studio 2012 で使用できます。 このツールのデザイン画面にはタブ付きウィンドウ、ウィザード、メニューが用意されており、これらを使ってレポートの作成機能にアクセスできます。 レポート デザイナー ツールは、レポート サーバー プロジェクトまたはレポート サーバー ウィザードのテンプレートを選択すると使用可能になります。 詳細については、「[SQL Server データ ツールの Reporting Services (SSDT)](reporting-services-in-sql-server-data-tools-ssdt.md)」を参照してください。  
  
#### <a name="to-start-report-designer"></a>レポート デザイナーを起動するには  
  
1.  Windows のスタート画面から「 **data** 」と入力し、 **[アプリ]** の検索結果で **[SQL Server Data Tools for Visual Studio 2012]** をクリックします。  
  
     **Or**  
  
     クリックして**開始**、 をポイント**すべてのプログラム**、 をポイント[!INCLUDE[ssCurrentUI](../../../includes/sscurrentui-md.md)]、順にクリックします**SQL Server Data Tools (SSDT)** します。  
  
2.  **[ファイル]** メニューの **[新規作成]** をポイントし、 **[プロジェクト]** をクリックします。  
  
3.  **[プロジェクトの種類]** ボックスの一覧で、 **[ビジネス インテリジェンス プロジェクト]** をクリックします。  
  
4.  **[テンプレート]** ボックスの一覧で、 **[レポート サーバー プロジェクト]** をクリックします。 次の図は、プロジェクトのテンプレートがダイアログ ボックスに表示された状態を示しています。  
  
     ![新しいプロジェクト テンプレートのダイアログ ボックス](../media/rs-ui-newrsproject.gif "新しいプロジェクト テンプレートのダイアログ ボックス")  
  
5.  プロジェクトの名前と場所を入力するか、 **[参照]** ボタンをクリックして場所を選択します。  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)] [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] で [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] の開始ページが開きます。 ソリューション エクスプローラーには、レポートとデータ ソースがそれぞれカテゴリとして表示されます。 これらのカテゴリを使用して、新しいレポートとデータ ソースを作成できます。 タブ付きウィンドウは、レポート定義を作成すると表示されます。 このウィンドウは [データ]、[レイアウト]、[プレビュー] の 3 つのタブで構成されます。  
  
 初めてレポートを作成する場合は、「[基本的なテーブル レポートの作成 &#40;SSRS チュートリアル&#41;](../create-a-basic-table-report-ssrs-tutorial.md)」を参照してください。 レポート デザイナーで使用できるクエリ デザイナーの詳細については、次を参照してください。[レポート デザイナーの SQL Server Data Tools でのクエリ デザイン ツール&#40;SSRS&#41;](../report-data/query-design-tools-ssrs.md)します。  
  
##  <a name="bkmk_report_builder"></a> レポート ビルダー  
 使用[レポート ビルダー &#40;SSRS&#41; ](report-builder-authoring-environment-ssrs.md)でレポートを作成、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office と同様の環境を作成します。 レポート デザイナーで作成したレポートであっても、以前のバージョンのレポート ビルダーでデザインしたレポートであっても、あらゆる既存レポートのカスタマイズおよび更新が可能です。 レポート ビルダーをローカル コンピューターにインストールするために実行する ReportBuilder3.msi ファイルの場所については、管理者に問い合わせてください。  
  
 **インストール:** クリック-いずれかでレポート ビルダーのバージョンがインストールされると[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]ネイティブ モードまたは SharePoint モード。 レポート ビルダーのスタンドアロン バージョンは別のダウンロードです。  参照してください[レポート ビルダーのスタンドアロン バージョンをインストール&#40;レポート ビルダー&#41;](../install-windows/install-report-builder.md)  
  
#### <a name="to-start-report-builder-clickonce-from-report-manager-native-mode"></a>レポート マネージャーからレポート ビルダー ClickOnce を起動するには (ネイティブ モード)  
  
1.  Web ブラウザーで、レポート マネージャーの URL を入力します。 既定の URL は http://\<*servername*>/reports です。 レポート マネージャーが開きます。  
  
2.  **[レポート ビルダー]** をクリックします。  
  
     レポート ビルダーが開き、レポート サーバー上でレポートを作成したり、レポートを開いたりできます。  
  
#### <a name="to-start-report-builder-clickonce-using-a-url"></a>URL を使用してレポート ビルダー ClickOnce を起動するには  
  
1.  Web ブラウザーでアドレス バーに次の URL を入力します。  
  
     **http://\<servername>/reportserver/reportbuilder/ReportBuilder_3_0_0_0.application**  
  
2.  Enter キーを押します。  
  
     レポート ビルダーが開き、レポート サーバー上でレポートを作成したり、レポートを開いたりできます。  
  
#### <a name="to-start-report-builder-clickonce-in-reporting-services-sharepoint-mode"></a>レポート ビルダー ClickOnce を Reporting Services SharePoint モードで起動するには  
  
1.  新しいレポートを作成するライブラリがあるサイトに移動します。  
  
2.  ライブラリを開きます。  
  
3.  **[新規作成]** メニューの **[レポート ビルダー レポート]** をクリックします。  
  
     レポート ビルダーが開き、レポート サーバー上でレポートを作成したり、レポートを開いたりできます。  
  
#### <a name="to-start-report-builder-stand-alone"></a>レポート ビルダー スタンドアロンを起動するには  
  
1.  Windows のスタート画面から、「 **report builder** 」と入力し、 **[レポート ビルダー 3.0]** をクリックします。  
  
     **Or**  
  
     [スタート] メニューの **[すべてのプログラム]** をクリックして、 **[Microsoft SQL Server 2014 レポート ビルダー]** をクリックします。  
  
2.  **[レポート ビルダー]** をクリックします。  
  
     レポート ビルダーが開き、レポートを作成したり、レポートを開いたりできます。  
  
3.  レポート ビルダーに関するドキュメントを開くには、 **[Report Builder ヘルプ]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [インストール、アンインストール、およびレポート ビルダーのサポート](../install-uninstall-and-report-builder-support.md)   
 [Reporting Services の SharePoint モード インストール&#40;SharePoint 2010 および SharePoint 2013&#41;](../install-windows/install-reporting-services-sharepoint-mode.md)   
 [Reporting Services Report Server](../reporting-services-report-server.md)   
 [クエリ デザイン ツールでレポート デザイナーの SQL Server Data Tools &#40;SSRS&#41;](../report-data/query-design-tools-ssrs.md)   
 [Reporting Services チュートリアル &#40;SSRS&#41;](../reporting-services-tutorials-ssrs.md)  
  
  
