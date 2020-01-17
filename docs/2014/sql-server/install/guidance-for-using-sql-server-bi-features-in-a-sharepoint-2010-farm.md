---
title: SharePoint 2010 ファームで SQL Server BI 機能を使用するためのガイダンス |Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 5f9a94c4-854b-4577-a8b1-7142f19904e3
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 08323d12fb787ea3989555070632d9716ad41152
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952258"
---
# <a name="guidance-for-using-sql-server-bi-features-in-a-sharepoint-2010-farm"></a>SharePoint 2010 ファームで SQL Server BI 機能を使用するためのガイド
  このトピックでは、使用しているソフトウェアの各バージョンやエディションで利用可能な機能の概要を説明します。 また、特定の SQL Server 機能を使用するために必要な SharePoint 2010 インストールについても説明します。 SharePoint 2013 に関連する情報については、「 [sharepoint の SQL SERVER BI 機能の配置トポロジ](deployment-topologies-for-sql-server-bi-features-in-sharepoint.md)」を参照してください。  
  
 このトピックの内容:  
  
-   [SharePoint 2010 の一般的な要件](#bkmk_generalsharepoint)  
  
-   [SharePoint 2010 Service Pack 1 (SP1)](#bkmk_sp1)  
  
-   [SharePoint のエディションと BI 機能のサポート](#bkmk_vers)  
  
-   [SharePoint 2010 製品準備ツール](#bkmk_prereq)  
  
-   [SharePoint インストールを実行するための要件と推奨事項](#bkmk_install)  
  
##  <a name="bkmk_generalsharepoint"></a>SharePoint 2010 の一般的な要件  
  
-   SharePoint 2010 製品は 64 ビットのみです。 32 ビットの以前のバージョンの SharePoint を使用していて、[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] が SharePoint 統合モードでインストールされている場合、SharePoint 2010 にアップグレードすることはできません。 詳細については、SharePoint のドキュメントを参照してください。  
  
-   Reporting Services には、SharePoint 製品用のアドインが含まれています。 このアドインとレポート サーバーに対してサポートされる構成については、ここに示す情報よりも詳細な情報が提供されています。 詳細については、「[サポートされている SharePoint と Reporting Services Server &#40;およびアドイン&#41;SQL Server 2014](../../reporting-services/install-windows/supported-combinations-of-sharepoint-and-reporting-services-server.md)」を参照してください。  
  
-   SharePoint 開発者ツールのみ SharePoint スタンドアロン構成をサポートします。  詳細については、SharePoint のドキュメント「 [Sharepoint ソリューションを開発するための要件](https://msdn.microsoft.com/library/ee231582.aspx)」を参照してください。  
  
##  <a name="bkmk_vers"></a>SharePoint のエディションと BI 機能のサポート  
 いくつかの [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] ビジネス インテリジェンス機能は、SharePoint 製品の特定のエディションでのみサポートされます。  
  
|サポートされている機能|SharePoint 製品|  
|------------------------|------------------------|  
|[!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]、[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[SPS2010](../../includes/sps2010-md.md)] Enterprise Edition 用の [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] アドインの機能です。<br /><br /> [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] データ警告<br /><br /> [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]。|[!INCLUDE[SPS2010](../../includes/sps2010-md.md)] Enterprise Edition。|  
|一般的な [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] レポートの表示と SharePoint との機能統合|[!INCLUDE[SPS2010](../../includes/sps2010-md.md)] Standard Edition と Enterprise Edition<br /><br /> [!INCLUDE[SPF2010](../../includes/spf2010-md.md)]。|  
  
 詳細については、「 [SQL Server 2012 の各エディションがサポートする機能](https://go.microsoft.com/fwlink/?linkid=232473)」を参照してください。  
  
##  <a name="bkmk_sp1"></a>SharePoint 2010 Service Pack 1 (SP1)  
 SharePoint 2010 のインストールを SharePoint 2010 Service Pack 1 (SP1) に更新することをお勧めします。 SharePoint SP1 は、次の場合に必要です。  
  
-   SharePoint コンテンツ データベースまたは [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] カタログ データベースに [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] バージョンのデータベース エンジンを使用する必要があります。  
  
-   [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] および [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 構成ツールを使用します。  
  
 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] で実行されている SharePoint インストールに SP1 が必要な主な理由の1つは、以前のリリースで非推奨とされたデータベースエンジンの機能**sp_dboption**が [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] リリースで廃止されたことです。 詳細については、「 [SQL Server 2014 で廃止されたデータベースエンジンの機能](../../database-engine/discontinued-database-engine-functionality-in-sql-server-2016.md)」を参照してください。  
  
### <a name="sharepoint-2010-sp1-installation-guidance"></a>SharePoint 2010 SP1 インストール ガイド  
 [SharePoint Server 2010 SP1 をダウンロード](https://go.microsoft.com/fwlink/?LinkID=219697)し、ファーム内のすべてのサーバーに適用します。  
  
> [!NOTE]  
>  既存のファームで、SharePoint SP1 のアップグレードを完了するには、次の**追加**の手順のいずれかを使用する必要があります。 詳細については、「 [Office 2010 sp1 および sharepoint 2010 sp1 のインストール時の既知の問題](https://support.microsoft.com/kb/2532126)」と「 [SHAREPOINT Server 2010 SP1 の説明](https://support.microsoft.com/kb/2460045)」を参照してください。  
  
-   **SharePoint 製品構成ウィザード:** ウィザードを実行して、SP1 のアップグレードと構成を完了します。  
  
-   **Psconfig.exe を使用したアップグレードを完了します。** コマンド `psconfig -upgrade` を実行して SP1 のアップグレードを完了します。  
  
 詳細については、「 [(Sharepoint Server 2010)](https://technet.microsoft.com/library/cc263093.aspx) 」および「 [Resource center: sharepoint 2010 製品用の更新プログラム](https://technet.microsoft.com/sharepoint/ff800847.aspx)」の「アップグレード」セクションを参照してください。  
  
## <a name="sharepoint-installation-with-sql-server-bi-features"></a>SQL Server BI 機能による SharePoint のインストール  
  
###  <a name="bkmk_prereq"></a>SharePoint 2010 製品準備ツール  
 SharePoint 製品準備ツールは、オペレーティング システム内のサーバー ロールを有効化し、SharePoint インストールに必要なその他の前提要件ソフトウェアをインストールします。 次の表は、サーバーを [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 用に構成するための追加手順を示したものです。  
  
|コンポーネント|操作|  
|---------------|------------|  
|Reporting Services アドイン|SharePoint 2010 製品準備ツールは、[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] バージョンの Reporting Services アドインをインストールします。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] には、[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] の機能に必要な新しいバージョンのアドインが含まれます。 アドインは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インストール ウィザードを使用してインストールすることも、MSDN からダウンロードすることもできます。 現在のバージョンのアドインを取得する場所とそのインストール方法の詳細については、「sharepoint[製品用の Reporting Services アドインの検索場所](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)」と「sharepoint [2010 および sharepoint 2013 &#40;&#41;用の Reporting Services アドインのインストールまたはアンインストール](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)」を参照してください。|  
|Analysis Services OLE DB Provider (MSOLAP)|SharePoint 2010 は、SQL Server 2008 バージョンの OLE DB プロバイダーを Excel Services の一部としてインストールします。 このバージョンでは、[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] データ アクセスはサポートされません。 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] データ接続をサポートする SharePoint サーバーに最新バージョンのプロバイダーをインストールする必要があります。 詳細については、「 [SharePoint サーバーに Analysis Services OLE DB Provider をインストールする](../../../2014/sql-server/install/install-the-analysis-services-ole-db-provider-on-sharepoint-servers.md)」を参照してください。|  
|ADO.NET Services|SharePoint 2010 では、前提要件のリストに ADO.NET サービスが含まれていますが、このサービスは Prerequisite インストーラーではインストールされません。 ADO.NET サービスを追加するには、手動でインストールする必要があります。 ADO.NET サービスのインストールは、SharePoint リストを [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] ブックまたは Reporting Services レポートへのデータ フィードとして使用する場合に必要です。 手順については、「 [SharePoint リストのデータフィードのエクスポートをサポートするための ADO.NET Data Services のインストール」を](../../../2014/sql-server/install/install-ado-net-data-services-to-support-data-feed-exports-of-sharepoint-lists.md)参照してください。|  
  
###  <a name="bkmk_install"></a>SharePoint インストールを実行するための要件と推奨事項  
 インストールする [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 機能とそれらのインストール順序によって、利用可能な SharePoint との統合レベルが決まります。 たとえば、組み込みデータベースを使用する SharePoint サーバー上の Reporting Services を通じて利用できる機能統合レベルもあります。ただし、一部の BI 機能に必要なインフラストラクチャはファーム インストールでしか提供されないため、多く機能統合シナリオでは、SharePoint のファーム インストールが必要となります。  
  
 SharePoint ファームは、単一サーバーにすることも、複数サーバーにすることもできます。 ファームがスタンドアロン インストールと違う点は、追加のインフラストラクチャ (Claims to Windows Token Service など) が存在するという点です。  
  
 SharePoint セットアップで **[サーバーファーム]** オプションを選択すると、ファームが有効になります。 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint または [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] を使用する場合は、ファーム インストールが必要です。 スタンドアロンの SharePoint インストールは、[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の開発環境用にサポートされており、この用途に多く使用されます。 ただし、本番環境には SharePoint のファーム インストールを使用することをお勧めします。  
  
 ![GMNI_SetupUI_SharePoint2010InstallType](../../../2014/sql-server/install/media/gmni-setupui-sharepoint2010installtype.gif "GMNI_SetupUI_SharePoint2010InstallType")  
  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint または [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 共有サービスには、完全なサーバー インストールも必要です。  
  
 ![GMNI_SetupUI_SharePoint2010ServerType](../../../2014/sql-server/install/media/gmni-setupui-sharepoint2010servertype.gif "GMNI_SetupUI_SharePoint2010ServerType")  
  
 セットアップ ウィザードの最後のページでは、ファームを構成するよう求められると共に、必要に応じてデフォルトの Web アプリケーションとルート サイト コレクションを構成するよう求められます。 ほとんどのセットアップ ユーザーはこのインストール パスでインストールします。 なんらかの理由でファームを構成しなかった場合は、[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 構成ツールのファーム構成オプションを使用することでファームを構成できます。  
  
 以前のリリースでは、[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] をインストールする場合、ファームを未構成のままにすることが推奨されていました。これは、SQL Server のインストール オプションを使用して、[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint を使用準備完了状態でインストールする場合に、後の手順を省略できたためです。 今リリースでは、これは重要ではなくなりました。 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 構成ツールを使用して既存のファームを調整し、[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint インストール用の推奨設定が使用されるようにできます。  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] は、既存の SharePoint ファームにインストールできます。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] または SharePoint は任意の順序でインストールできますが、[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の構成は順序に応じて変わります。 詳細については、「追加の[レポートサーバーをファーム&#40;に追加する SSRS&#41;スケールアウト](../../reporting-services/install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md)および[sharepoint 2010 用 Reporting Services sharepoint モードのインストール](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)」を参照してください。  
  
 ![GMNI_SetupUI_DoNotConfigureMOSS](../../../2014/sql-server/install/media/gmni-setupui-donotconfiguremoss.gif "GMNI_SetupUI_DoNotConfigureMOSS")  
  
## <a name="see-also"></a>参照  
 [SharePoint Server 2010  のインストールと配置](https://technet.microsoft.com/sharepoint/ee518643.aspx)  
 [3層ファーム用の複数サーバー (SharePoint Server 2010)](https://go.microsoft.com/fwlink/?linkID=219834)  
  
  
