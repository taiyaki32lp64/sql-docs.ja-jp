---
title: レポートサーバーのコンテンツの種類をライブラリに追加する (SharePoint 統合モードの Reporting Services) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: ac9136c8-9ef4-484c-8e9d-05008a186db5
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 78c9080f1ea9ac0d733a45718886e31ab52171c8
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68891629"
---
# <a name="add-report-server-content-types-to-a-library-reporting-services-in-sharepoint-integrated-mode"></a>レポート サーバー コンテンツの種類をライブラリに追加する (Reporting Services の SharePoint 統合モード)
  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] では、共有データ ソース (.rsds) ファイル、レポート モデル (.smdl)、レポート ビルダーのレポート定義 (.rdl) ファイルを管理する際に使用するコンテンツの種類が、あらかじめ定義されています。 コンテンツの種類として、 **[レポート ビルダー レポート]** 、 **[レポート モデル]** 、および **[レポート データ ソース]** をライブラリに追加すると、 **[新規作成]** コマンドが有効になり、その種類のドキュメントを新規作成できるようになります。  
  
 **[!INCLUDE[applies](../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint モード:  
  
 コンテンツの種類をライブラリに追加するには、サイトの管理者であるか、またはフル コントロール レベルの権限を持っている必要があります。  
  
 次の [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] ビジネス インテリジェンス センター **サイト テンプレートから作成された既存のサイト コレクションのすべてのドキュメント ライブラリで** コンテンツの種類およびコンテンツの種類の管理が自動的に有効になります。  
  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 統合後に作成されたサイトでは、 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] のコンテンツの種類が有効になっていません。  
  
> [!TIP]  
>  以前にライブラリのコンテンツの種類を構成して **いない** 場合は、コンテンツの種類の管理を有効にしてから、 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] のコンテンツの種類を有効にします。 単一のドキュメント ライブラリでコンテンツの種類の管理を有効にするための手順を参照してください。  
  
 **短いビデオ:** [(SSRS) sharepoint2010.wmv でコンテンツタイプを有効にする](http://www.youtube.com/watch?v=yqhm3DrtT1w)(http://www.youtube.com/watch?v=yqhm3DrtT1w).  
  
 **このトピックの内容:**  
  
-   [既存のビジネス インテリジェント センターのすべてのドキュメント ライブラリでコンテンツの種類を有効にする](#bkmk_enable_all)  
  
-   [1 つのドキュメント ライブラリでコンテンツの種類の管理を有効にするには (SharePoint 2013)](#bkmk_enable_content_management)  
  
-   [Reporting Services のコンテンツの種類を追加するには (SharePoint 2013)](#bkmk_add_single)  
  
-   [1 つのドキュメント ライブラリでコンテンツの種類の管理を有効にするには (SharePoint 2010)](#bkmk_enable_content_management_2010)  
  
-   [レポート サーバーのコンテンツの種類を追加するには (SharePoint 2010)](#bkmk_add_single_2010)  
  
-   [複数の BI サイトのコンテンツの種類とコンテンツ管理を有効にするには](#bkmk_enable_multiple_sites)  
  
##  <a name="bkmk_enable_all"></a> 既存のビジネス インテリジェント センターのすべてのドキュメント ライブラリでコンテンツの種類を有効にする  
  
1.  既存の **ビジネス インテリジェント センター** サイトのすべてのドキュメント ライブラリでコンテンツの種類とコンテンツ管理を有効にするには、 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 統合機能を切り替えます。  
  
2.  **[サイトの設定]** に移動します。  
  
    -   SharePoint 2013 の場合、 **[設定]** アイコンをクリックします。 ![SharePoint の設定](https://docs.microsoft.com/analysis-services/analysis-services/media/as-sharepoint2013-settings-gear.gif "SharePoint の設定")  
  
    -   SharePoint 2010 の場合、 **[サイトの操作]** をクリックし、 **[サイトの設定]** をクリックします。  
  
3.  **[サイト コレクションの機能]** をクリックします。  
  
4.  **[レポート サーバーの統合機能]** を見つけて **[非アクティブ化]** をクリックします。  
  
     ![rs_reportserver_integration_active](media/rs-reportserver-integration-active.gif "rs_reportserver_integration_active")  
  
5.  ブラウザーを更新します。 **[レポート サーバーの統合機能]** の **[アクティブ化]** をクリックします。  
  
    ![非アクティブ化](media/rs-reportserver-integration-deactivate.gif "rs_reportserver_integration_deactive")  
  
##  <a name="bkmk_enable_content_management"></a> 1 つのドキュメント ライブラリでコンテンツの種類の管理を有効にするには (SharePoint 2013)  
  
1.  複数のコンテンツの種類を有効にする対象ライブラリを開きます。  
  
2.  リボンで、 **[ライブラリ]** をクリックします。  
  
     ![rs_SharePoint2013_LibraryRibbon](media/rs-sharepoint2013-libraryribbon.gif "rs_SharePoint2013_LibraryRibbon")  
  
3.  **[ライブラリ]** リボンで、 **[ライブラリの設定]** をクリックします。 **[ライブラリの設定]** が表示されない場合やボタンが無効になっている場合は、コンテンツの種類を含むライブラリ設定を構成する権限がありません。  
  
     ![rs_SharePoint2013_LibrarySettings](media/rs-sharepoint2013-librarysettings.gif "rs_SharePoint2013_LibrarySettings")  
  
4.  **[全般設定]** セクションの **[詳細設定]** をクリックします。  
  
     ![rs_SharePoint2013_LibrarySettings_AdvancedSettings](media/rs-sharepoint2013-librarysettings-advancedsettings.gif "rs_SharePoint2013_LibrarySettings_AdvancedSettings")  
  
5.  コンテンツの種類を管理できるようにするには、 **[コンテンツ タイプ]** の **[はい]** をクリックします。  
  
6.  **[OK]** をクリックします。  
  
##  <a name="bkmk_add_single"></a> Reporting Services のコンテンツの種類を追加するには (SharePoint 2013)  
  
1.  Reporting Services のコンテンツの種類を追加する対象のライブラリを開きます。  
  
2.  リボンで、 **[ライブラリ]** をクリックします。  
  
3.  **[ライブラリの設定]** をクリックします。  
  
4.  **[コンテンツ タイプ]** の **[既存のサイト コンテンツ タイプから追加]** をクリックします。  
  
5.  **[サイト コンテンツ タイプの選択元]** で、 **[SQL Server Reporting Services のコンテンツの種類]** を選択します。  
  
6.  **[利用可能なサイト コンテンツ タイプ]** ボックスの一覧で **[レポート ビルダー]** をクリックし、 **[追加]** をクリックして、選択したコンテンツ タイプを **[追加するコンテンツ タイプ]** ボックスの一覧に追加します。  
  
7.  コンテンツの種類として **[レポート モデル]** および **[レポート データ ソース]** を追加するには、前の手順を繰り返します。  
  
8.  コンテンツの種類の追加操作が完了したら、 **[OK]** をクリックします。  
  
9. > [!NOTE]  
    >  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] コンテンツの種類のグループ **[SQL Server Reporting Services のコンテンツの種類]** が **[コンテンツ タイプの追加]** ページに表示されない場合は、次のいずれかの状況に該当しています。  
  
    -   SharePoint 製品用の [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] アドインがインストールされていません。 詳細については、「sharepoint [2010 および sharepoint 2013 &#40;&#41;用の Reporting Services アドインのインストールまたはアンインストール](install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)」を参照してください。 このトピックには、アドインのインストール方法、アドインのファイルのみのインストールをステップ実行して問題に対処する方法が記載されています。  
  
    -   アドインはインストールされていますが、サイト コレクション機能 **[レポート サーバーの統合機能]** がアクティブになっていません。 **[サイトの設定]** でサイト コレクション機能を確認してください。  
  
    -   [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] のすべてのコンテンツの種類が既にライブラリに追加されています。 すべてのコンテンツの種類がライブラリの一部である場合、このグループは **[コンテンツ タイプの追加]** ページから削除されます。 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] の 1 つまたは複数のコンテンツの種類を削除すると、 **[SQL Server Reporting Services のコンテンツの種類]** グループが **[コンテンツ タイプの追加]** ページに表示されます。  
  
##  <a name="bkmk_enable_content_management_2010"></a> 1 つのドキュメント ライブラリでコンテンツの種類の管理を有効にするには (SharePoint 2010)  
  
1.  複数のコンテンツの種類を有効にする対象ライブラリを開きます。 ライブラリ メニュー バーには、以下のメニューが表示されます。 **[新規]** 、 **[アップロード]** 、 **[アクション]** 、および **[設定]** 。 コンテンツの種類を追加する権限を持っていない場合は、 **[設定]** が表示されません。  
  
2.  **[ライブラリ ツール]** リボンで、 **[ライブラリ]** をクリックします。  
  
     ![rs_SharePoint2010_LibraryRibbon](media/rs-sharepoint2010-libraryribbon.gif "rs_SharePoint2010_LibraryRibbon")  
  
3.  **[設定]** リボン グループの **[ライブラリの設定]** をクリックします。  
  
4.  **[全般設定]** の **[詳細設定]** をクリックします。  
  
5.  コンテンツの種類を管理できるようにするには、 **[コンテンツ タイプ]** の **[はい]** をクリックします。  
  
6.  **[OK]** をクリックします。  
  
##  <a name="bkmk_add_single_2010"></a> レポート サーバーのコンテンツの種類を追加するには (SharePoint 2010)  
  
1.  Reporting Services のコンテンツの種類を追加する対象のライブラリを開きます。  
  
2.  **[ライブラリ ツール]** リボン タブで **[ライブラリ]** タブをクリックします。  
  
3.  **[設定]** リボン グループの **[ライブラリの設定]** をクリックします。  
  
4.  **[コンテンツ タイプ]** の **[既存のサイト コンテンツ タイプから追加]** をクリックします。  
  
5.  **[コンテンツ タイプの選択]** セクションの **[サイト コンテンツ タイプの選択元]** で、矢印をクリックして **[SQL Server Reporting Services のコンテンツの種類]** を選択します。  
  
6.  **[利用可能なサイト コンテンツ タイプ]** ボックスの一覧で **[レポート ビルダー]** をクリックし、 **[追加]** をクリックして、選択したコンテンツ タイプを **[追加するコンテンツ タイプ]** ボックスの一覧に追加します。  
  
7.  コンテンツの種類として **[レポート モデル]** および **[レポート データ ソース]** を追加するには、前の手順を繰り返します。  
  
8.  コンテンツの種類の追加操作が完了したら、 **[OK]** をクリックします。  
  
##  <a name="bkmk_enable_multiple_sites"></a> 複数の BI サイトのコンテンツの種類とコンテンツ管理を有効にするには  
  
1.  SQL Server Reporting Services 2008 および 2008 R2 レポート サーバーの場合は、複数のビジネス インテリジェンス センター サイトのコンテンツの種類とコンテンツ管理を有効にすることができます。  
  
2.  SharePoint サーバーの全体管理で **[アプリケーションの全般設定]** をクリックします。 **[SQL Server Reporting Services (2008 および 2008 R2)]** セクションで、 **[Reporting Services 統合]** をクリックします。  
  
     ![rs_general_app_settings](media/rs-general-app-settings.gif "rs_general_app_settings")  
  
3.  **[すべての既存のサイト コレクションで機能をアクティブ化する]** をクリックします。  
  
     ![rs_general_app_settings_old_integrations](media/rs-general-app-settings-old-integrations.gif "rs_general_app_settings_old_integrations")  
  
4.  **[OK]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [レポート サーバー アイテムの SharePoint サイトおよびリスト権限のリファレンス](security/sharepoint-site-and-list-permission-reference-for-report-server-items.md)   
 [レポートビルダー &#40;レポートビルダーの開始&#41;](report-builder/start-report-builder.md)  
  
  
