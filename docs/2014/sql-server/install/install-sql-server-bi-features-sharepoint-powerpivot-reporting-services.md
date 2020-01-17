---
title: SharePoint を使用した SQL Server BI 機能のインストール (PowerPivot および Reporting Services) |Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 3166107c-30c2-468e-bb1b-bb42b79b37c3
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 42bc370a4e1eebddb3293afe6843f3ed19338656
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952139"
---
# <a name="install-sql-server-bi-features-with-sharepoint-powerpivot-and-reporting-services"></a>SharePoint を使用した SQL Server の BI 機能のインストール (PowerPivot と Reporting Services)
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] および [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] を Microsoft SharePoint ファームに統合することで、SharePoint のビジネス インテリジェンス (BI) 機能を有効にすることができます。 機能には、 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]、 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]、および [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]が含まれます。 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] は、SharePoint ファーム内の [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] データ アクセスに使用されます。 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] は、[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for Excel で作成され、SharePoint ライブラリからアクセスされるブック用のデータ エンジンです。 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] ブックを SharePoint に保存したら、それを [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] レポートのデータ ソースとして使用できます。  
  
 SharePoint 2010 で必要になるインストールと構成の手順は、SharePoint 2013 で必要な手順と一部異なります。 このセクションの一部のトピックは、SharePoint の両方のバージョンに適用されます。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  SharePoint 2013 &#124; SharePoint 2010|  
  
 ![注](../../../2014/reporting-services/media/rs-fyinote.png "最新のリリースノートについて")は、「 [SQL server 2014 リリースノート](https://go.microsoft.com/fwlink/?LinkID=296445)」を参照してください。  
  
##  <a name="bkmk_top"></a> このトピックの内容  
  
-   [SQL Server BI シナリオと SharePoint 2013](#bkmk_bi_scenarios)  
  
-   [インストールの概要](#bkmk_install_sharepoint2013_overview)  
  
## <a name="in-this-section"></a>このセクションの内容  
 このトピックの情報に加えて、次の関連項目は、このセクションの内容に含まれます。  
  
 [SharePoint の SQL Server BI 機能の配置トポロジ](deployment-topologies-for-sql-server-bi-features-in-sharepoint.md)  
  
 [SharePoint 2010 ファームで SQL Server BI 機能を使用するためのガイド](../../../2014/sql-server/install/guidance-for-using-sql-server-bi-features-in-a-sharepoint-2010-farm.md)  
  
 [SharePoint を使用した BI 機能のインストール用チェック リスト](../../../2014/sql-server/install/checklists-for-installing-bi-features-with-sharepoint.md)  
  
 [Sharepoint モードのインストール&#40;Reporting Services sharepoint 2010 および sharepoint 2013&#41;](../../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md)  
  
 [PowerPivot for SharePoint 2013 のインストール](https://docs.microsoft.com/analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode)  
  
 [PowerPivot for SharePoint 2010 のインストール](../../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md)  
  
##  <a name="bkmk_bi_scenarios"></a>SQL Server BI シナリオと SharePoint 2013  
 このセクションでは、インストールおよび構成するために選択できる、さまざまなレベルの BI 機能について説明します。  
  
 SharePoint 2013 の Excel Services には、ブラウザーで [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] ブックを操作できるようにするためのデータ モデル機能が含まれます。 基本的なデータ モデル機能の場合、ファームに [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013 アドインを配置する必要はありません。 必要な操作は、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] サーバーを SharePoint モードでインストールし、Excel Services の **[データ モデルの設定]** でサーバーを登録するだけです。  
  
 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013 アドインを配置すると、SharePoint ファームで追加の機能を有効にすることができます。 追加の機能には、 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] ギャラリー、データ更新スケジュール、および PowerPivot 管理ダッシュボードがあります。 詳細については、表を参照してください。  
  
||Level|機能のインストール|インストールまたは構成|  
|-|-----------|--------------|--------------------------|  
|@shouldalert|SharePoint のみ|Excel Services のネイティブ機能|SharePoint Server 2013 に含まれる Excel Services やその他のサービス。|  
|**2**|SharePoint モードの Analysis Services が統合された SharePoint|ブラウザー内での対話型の PowerPivot ブック|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] を SharePoint モードでインストールします。<br /><br /> Excel Services で Analysis Services サーバーを登録します。|  
|**3**|SharePoint モードの Reporting Services が統合された SharePoint|Power View|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] を SharePoint モードでインストールします。<br /><br /> SharePoint 用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] アドイン **(Rssharepoint .msi)** をインストールします。 詳細については、「sharepoint [2010 および sharepoint 2013 &#40;&#41;用の Reporting Services アドインのインストールまたはアンインストール](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)」を参照してください。|  
|**4**|PowerPivot のすべての機能|ファームの外部からのデータ ソースとしてのブックへのアクセス。<br /><br /> 定期データ更新。<br /><br /> PowerPivot ギャラリー。<br /><br /> 管理ダッシュボード。<br /><br /> BISM リンク ファイルのコンテンツの種類。|PowerPivot for SharePoint 2013 アドイン **(Sppowerpivot .msi)** をデプロイします。 詳細については、以下をご覧ください。<br /><br /> [PowerPivot for SharePoint アドイン&#40;SharePoint 2013 をインストールまたはアンインストールする&#41;](https://docs.microsoft.com/analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013)<br /><br /> **spPowerPivot.msi**のダウンロード方法の詳細については、 [SQL Server 2014 PowerPivot for SharePoint のダウンロード ページ](https://go.microsoft.com/fwlink/?LinkID=296473)を参照してください。|  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 機能の有効化の詳細については、「 [SharePoint 2013 の SQL SERVER BI のライトアップストーリー](https://blogs.msdn.com/b/analysisservices/archive/2012/07/27/introducing-the-bi-light-up-story-for-sharepoint-2013.aspx) 」 (https://blogs.msdn.com/b/analysisservices/archive/2012/07/27/introducing-the-bi-light-up-story-for-sharepoint-2013.aspx)を参照してください。  
  
##  <a name="bkmk_install_sharepoint2013_overview"></a>インストールの概要  
 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] と [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]の両方を使用する場合は、SQL Server インストール ウィザードを 2 回実行します。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] と [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] は、SQL Server セットアップウィザードの **[セットアップロール]** ページで個別に選択できます。  
  
 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] は SharePoint 2010 と SharePoint 2013 の両方をサポートしますが、使用されるアーキテクチャとインストール プロセスは SharePoint のバージョンに応じて異なります。  
  
 シングル サーバーに [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] の BI 機能を配置するインストール手順の概要を以下に示します。  
  
 **[!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013**  
  
 **SharePoint 2013**の場合、 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] のインストールは、SharePoint 製品がインストールされていないサーバーで実行できます。 SharePoint 2013 で使用されている [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] アーキテクチャは、SharePoint ファームの **外部** で実行されるため、SharePoint もインストールされているサーバーにインストールすることも、SharePoint がインストールされてないサーバーにインストールすることもできます。  
  
1.  SharePoint Server 2013 をインストールし、Excel Services を有効にします。  
  
2.  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] を SharePoint モードでインストールし、SharePoint ファームおよびサービス アカウントに [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]のサーバー管理者権限を付与します。  
  
     SharePoint の両方のバージョンで、 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] のインストール プロセスの開始時に **[SQL Server PowerPivot for SharePoint]** のロールを設定します。これには SQL Server インストール ウィザードを使用するか、コマンド プロンプトによる SQL Server のインストールを使用します。  
  
     ![ロール]の(../../../2014/sql-server/install/media/gmni-setupui-featurerole-sql2012sp1.gif "セットアップロール")のセットアップ  
  
3.  SharePoint 2013 では、 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] の機能とエクスペリエンスを拡張できます。 **spPowerPivot.msi** をダウンロードして実行すると、 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] ブックに対するサーバー側のデータ更新処理、コラボレーション、および管理のサポートが追加されます。 詳細については、「 [Microsoft SQL Server 2014 PowerPivot for Microsoft® SharePoint](https://go.microsoft.com/fwlink/?LinkID=324854)」を参照してください。  
  
     SharePoint ファーム内の各サーバーで [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013 のインストール パッケージ **spPowerPivot.msi** を実行し、適切なバージョンのデータ プロバイダーがインストールされていることを確認します。  
  
4.  [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 2013 を構成するには、 **PowerPivot for SharePoint 2013 構成** ツールを使用します。  
  
     SQL Server インストール ウィザードでは、2 つの [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 構成ツールがインストールされます。 構成ツールの 1 つは SharePoint 2013 をサポートし、もう 1 つは SharePoint 2010 をサポートします。  
  
     ![2 つの PowerPivot 構成ツール](https://docs.microsoft.com/analysis-services/analysis-services/media/as-powerpivot-configtools-bothicons.gif "2 つの PowerPivot 構成ツール")  
  
5.  SharePoint Server 2013 で、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] インスタンスを使用するように Excel Services を構成します。 詳細については、「 [PowerPivot for SharePoint 2013 のインストール](https://docs.microsoft.com/analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode)」の「基本的な Analysis Services SharePoint 統合の構成」、および「 [Excel Services のデータモデル設定の管理 (sharepoint Server 2013)](https://technet.microsoft.com/library/jj219780.aspx) 」 (https://technet.microsoft.com/library/jj219780.aspx)を参照してください。  
  
6.  詳しくは、「 [PowerPivot for SharePoint 2013 Installation](https://docs.microsoft.com/analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode)」をご覧ください。  
  
 **[!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2010**  
  
 SharePoint 2010 の場合、 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint のインストールは、既に SharePoint 2010 がインストールされているサーバー、またはインストールする予定のサーバーで実行する必要があります。 SharePoint 2010 の [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] アーキテクチャは、ファームの **内部** で実行されるため、 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint がインストールされているサーバー上に SharePoint を必要とします。  
  
1.  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] を SharePoint モードでインストールし、SharePoint ファームおよびサービス アカウントに [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]のサーバー管理者権限を付与します。  
  
     SharePoint 2010 の配置は spPowerPivot.msi をサポートしません。この .msi は SharePoint 2010 には **不要** です。  
  
     SharePoint の両方のバージョンで、 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] のインストール プロセスの開始時に **[SQL Server PowerPivot for SharePoint]** のロールを設定します。これには SQL Server インストール ウィザードを使用するか、コマンド プロンプトによる SQL Server のインストールを使用します。  
  
2.  SQL Server インストール ウィザードでは、2 つの [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 構成ツールがインストールされます。 構成ツールの 1 つは SharePoint 2013 をサポートし、もう 1 つは SharePoint 2010 をサポートします。  
  
     [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 2010 を構成するには、 **PowerPivot 構成ツール** を使用します。  
  
3.  詳しくは、「 [PowerPivot for SharePoint 2010 Installation](../../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md)」をご覧ください。  
  
 **[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]**  
  
1.  SharePoint モードの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のインストールは、以前のリリースから変更されていません。  
  
     [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のインストール手順は、SharePoint 2010 と SharePoint 2013 とで非常に共通しています。 SharePoint のバージョンに関する重要な注意事項を次に示します。  
  
    -   次のサポートされる組み合わせを確認してください。  
  
        -   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のバージョン。  
  
        -   SharePoint 製品用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] アドイン。  
  
        -   SharePoint 製品のバージョン。  
  
         [SharePoint と Reporting Services Server のサポートされている組み合わせ&#40;SQL Server 2014&#41;](../../reporting-services/install-windows/supported-combinations-of-sharepoint-and-reporting-services-server.md)  
  
    -   SharePoint 2010 の [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] には SharePoint 2010 Service Pack 2 (SP2) が必要です。  
  
    1.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] を SharePoint モードでインストールします。 [Sharepoint モードのインストール&#40;で sharepoint 2010 および sharepoint&#41; 2013 を Reporting Services](../../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md)し、sharepoint [2010 用の sharepoint モード Reporting Services インストール](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)します。  
  
    2.  SharePoint 製品用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] アドイン (rsSharePoint.msi) をインストールします。 「Sharepoint [2010 および sharepoint 2013 &#40;&#41;用の Reporting Services アドインのインストールまたはアンインストール](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)」を参照してください。 SharePoint 用の [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] アドインの現在のバージョンについては、「 [Sharepoint 製品用の Reporting Services アドインの検索場所](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)」を参照してください。  
  
    3.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint サービスと 1 つ以上の [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サービス アプリケーションを構成します。 詳細については、「 [sharepoint 2013 用 Reporting Services Sharepoint モードのインストール](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2013.md)」の「Reporting Services サービスアプリケーションの作成」セクションを参照してください。  
  
##  <a name="bkm_database_attach"></a>データベースアタッチアップグレードと SharePoint 2013 の概要  
 SharePoint 2013 では、インプレース アップグレードはサポートされていません。 ただし、 **データベース アタッチ アップグレードはサポートされています**。  
  
 SharePoint 2010 と統合された PowerPivot の既存のインストールを使用している場合は、SharePoint サーバーのインプレース アップグレードを行うことはできません。  ただし、SharePoint のデータベース アタッチ アップグレードの一環として以下の手順を実行できます。  
  
1.  新しい SharePoint Server 2013 ファームをインストールします。  
  
2.  SharePoint のデータベース アタッチ アップグレードを完了し、PowerPivot に関連するコンテンツ データベースを SharePoint 2013 ファームに移行します。  
  
3.  SQL Server Analysis Services のインスタンスを SharePoint モードでインストールし、SharePoint ファームおよびサービス アカウントに [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]のサーバー管理者権限を付与します。  
  
4.  SharePoint ファーム内の各サーバーに PowerPivot for SharePoint 2013 のインストール パッケージ **spPowerPivot.msi** をインストールします。  
  
5.  [SharePoint 2013 サーバーの全体管理] で、手順 3. で作成した、SharePoint モードで実行している Analysis Services サーバーを使用するように Excel Services を構成します。  
  
     更新スケジュールを移行するには、PowerPivot サービス アプリケーションを構成します。  
  
> [!NOTE]  
>  PowerPivot および SharePoint データベース アタッチ アップグレードの詳細については、以下を参照してください。  
  
-   [SharePoint 2013 への PowerPivot の移行](https://docs.microsoft.com/analysis-services/instances/install-windows/migrate-power-pivot-to-sharepoint-2013)  
  
-   [SharePoint 2013 へのアップグレード プロセスの概要](https://go.microsoft.com/fwlink/p/?LinkId=256688)。  
  
-   [SharePoint 2013 へのアップグレードの前に環境をクリーンアップする](https://go.microsoft.com/fwlink/p/?LinkId=256689)  
  
-   [SharePoint 2010 から SharePoint 2013 にデータベースをアップグレードする](https://go.microsoft.com/fwlink/p/?LinkId=256690)。  
  
## <a name="see-also"></a>参照  
 [SharePoint 製品用 Reporting Services アドインの検索場所](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)   
 [サポートされている SharePoint および Reporting Services サーバーとアドイン&#40;SQL Server 2014&#41;の組み合わせ](../../reporting-services/install-windows/supported-combinations-of-sharepoint-and-reporting-services-server.md)   
 [SharePoint &#40;2010 および sharepoint 2013 用の Reporting Services アドインのインストールまたはアンインストール&#41;](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)  
  
  
