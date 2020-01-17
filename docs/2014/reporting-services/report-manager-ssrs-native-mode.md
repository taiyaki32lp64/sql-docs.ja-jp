---
title: レポート マネージャー (SSRS ネイティブ モード) |Microsoft Docs
ms.prod: sql-server-2014
ms.technology: reporting-services-native
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.custom: ''
ms.date: 04/26/2019
ms.openlocfilehash: 55581ae96660732ee01bf12fa37e1c5e8ac9634e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "64568384"
---
# <a name="report-manager--ssrs-native-mode"></a>レポート マネージャー (SSRS ネイティブ モード)
  レポート マネージャーは、レポートへのアクセスと管理を行う Web ベースのツールです。HTTP 接続を使用して、リモート コンピューターから 1 つのレポート サーバー インスタンスを管理するために使用します。 また、レポート マネージャーでレポートの表示とナビゲーションを行うこともできます。 このトピックの内容  
  
-   [レポート マネージャーとは何ですか。](#bkmk_whatis_report_manager)  
  
-   [開始とレポート マネージャーを使用して](#bkmk_start_report_manager)  
  
-   [アイコンの説明](#bkmk_icon_descriptions)  
  
##  <a name="bkmk_whatis_report_manager"></a> レポート マネージャーとは何ですか。  
 レポート マネージャーを使用して実行できるタスクは次のとおりです。  
  
-   レポートの表示、検索、印刷、およびサブスクライブ。  
  
-   サーバー上のアイテムを整理するフォルダー階層の作成、セキュリティ保護、および保守。  
  
-   アイテムおよび操作に対するアクセスを決定するロールベースのセキュリティの構成。  
  
-   レポート実行プロパティ、レポート履歴、およびレポート パラメーターの構成。  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] データ ソースまたは [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] リレーショナル データ ソースに接続してデータを取得するレポート モデルの作成。  
  
-   モデル内の特定のエンティティへのアクセスを許可するモデル アイテム セキュリティの設定、または事前に作成した定義済みのクリックスルー レポートへのエンティティのマップ。  
  
-   スケジュールおよびデータ ソース接続をさらに管理しやすくする共有スケジュールおよび共有データ ソースの作成。  
  
-   大きい受信者一覧にレポートをロール アウトするデータ ドリブン サブスクリプションの作成。  
  
-   既存レポートの再利用や目的変更を行うための、リンク レポートの作成。  
  
-   レポートを作成するレポート ビルダーの起動。作成したレポートは、レポート サーバーで保存および実行できます。  
  
 レポート マネージャーでは、レポート サーバー フォルダーを参照したり、特定のレポートを検索することができます。 レポート、その全般プロパティ、およびレポート履歴にキャプチャされているレポートの過去のコピーを表示できます。 権限に応じて、レポートにサブスクライブし、電子メールの受信ボックスやファイル システム上の共有フォルダーに配信させることもできます。  
  
> [!NOTE]  
>  サポートされるブラウザーとバージョンについては、次を参照してください。 [Reporting Services と Power View のブラウザー サポートの計画&#40;Reporting Services 2014&#41;](../../2014/reporting-services/browser-support-for-reporting-services-and-power-view.md)します。  
  
 レポート マネージャーは、ネイティブ モードで実行されているレポート サーバーでのみ使用されます。 SharePoint 統合モード用に構成されたレポート サーバーでは使用できません。  
  
 一部のレポート マネージャー機能は、特定のエディションの [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]だけで利用できます。 詳しくは「 [Features Supported by the Editions of SQL Server 2014](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)」をご覧ください。  
  
 新しくインストールした場合、コンテンツおよび設定を操作するのに十分な権限を持っているのはローカル管理者のみです。 他のユーザーに権限を与えるには、ローカル管理者がレポート サーバーへのアクセスを許可するロールの割り当てを作成する必要があります。 ロールの割り当てが作成された後、ユーザーがアクセスできるようになるアプリケーション ページとタスクは、そのユーザーに対するロールの割り当てによって異なります。 詳細については、「 [レポート サーバーへのユーザー アクセスを許可する &#40;レポート マネージャー&#41;](security/grant-user-access-to-a-report-server.md)」を参照してください。  
  
 [!INCLUDE[wiprlhlong](../includes/wiprlhlong-md.md)] または Windows Server 2008 を使用している場合は、レポート マネージャーをローカル管理用に構成する必要があります。 詳細については、「 [ローカル管理用のネイティブ モードのレポート サーバー &#40;SSRS&#41; の構成](report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md)。  
  
##  <a name="bkmk_start_report_manager"></a> 開始とレポート マネージャーを使用して  
 レポート マネージャーは Web アプリケーションであり、ブラウザー ウィンドウのアドレス バーにレポート マネージャーの URL を入力して起動します。 レポート マネージャーの起動時に表示されるページ、リンク、およびオプションは、レポート サーバーに対してユーザーが持っている権限によって異なります。 タスクを実行するには、そのタスクを含むロールに割り当てられている必要があります。 すべての権限を持つロールに割り当てられたユーザーは、レポート サーバーの管理に利用できるすべてのアプリケーション メニューとページにアクセスできます。 一方、レポートの表示と実行の権限を持つロールに割り当てられたユーザーは、それらの操作をサポートするメニューとページのみを表示できます。 各ユーザーに対して、レポート サーバーごとに異なるロールを割り当てることも、単一のレポート サーバーに保存されている多様なレポートまたはフォルダーごとに異なるロールを割り当てることもできます。  
  
 ロールの詳細については、「 [ネイティブ モードのレポート サーバーに対する権限の許可](security/granting-permissions-on-a-native-mode-report-server.md)」を参照してください。  
  
> [!NOTE]  
>  Windows Vista または Windows Server 2008 を使用している場合、レポート マネージャーを使用してローカルのレポート サーバー インスタンスを管理するには、レポート サーバーをローカル管理用に構成する必要があります。 サーバーを構成する方法の詳細については、次を参照してください。[ローカル管理用のネイティブ モード レポート サーバーの構成&#40;SSRS&#41;](report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md)します。  
  
## <a name="start-report-manager"></a>レポート マネージャーの起動  
  
#### <a name="to-start-report-manager-from-a-browser"></a>ブラウザーからレポート マネージャーを起動するには  
  
1.  [!INCLUDE[msCoName](../includes/msconame-md.md)] Internet Explorer 7.0 以降を開きます。  
  
2.  Web ブラウザーのアドレス バーに、レポート マネージャーの URL を入力します。  
  
    -   既定の URL は、 `http://[ComputerName]/reports`です。  
  
    -   レポート サーバーは、特定のポートを使用するように構成できます。 たとえば、 `http:// [ComputerName]:80/reports` や `http:// [ComputerName]:8080/reports`になります。  
  
## <a name="configuring-report-manager"></a>レポート マネージャーの構成  
 レポート マネージャーの構成には、アプリケーションの URL を定義することが含まれます。 別のコンピューターでレポート マネージャーを実行する配置の場合、追加の構成が必要です。  
  
 レポート マネージャーは、ごく限られた範囲でカスタマイズすることができます。 たとえば、[サイトの設定] ページで、アプリケーションのタイトルを変更できます。 Web 開発者は、レポート マネージャーで使用されるスタイル情報を含んだスタイル シートを変更できます。 レポート マネージャーは、カスタマイズをサポートするように特に設計されているわけではないため、変更は十分にテストする必要があります。 レポート マネージャーがニーズに合わない場合は、独自のレポート ビューアーを開発するか、SharePoint サイトでレポートを検索および表示できるように SharePoint Web パーツを構成することができます。 詳細については、「[レポート マネージャーの構成 (ネイティブ モード)](report-server/configure-web-portal.md)」を参照してください。  
  
##  <a name="bkmk_icon_descriptions"></a> アイコンの説明  
 次の表では、レポート マネージャーで使用されるアイコンについて説明します。 レポート ツールバーに表示されるアイコンの詳細については、次を参照してください。 [HTML ビューアーとレポート ツールバー](html-viewer-and-the-report-toolbar.md)します。  
  
|アイコン|説明|操作|  
|----------|-----------------|------------|  
|![レポート アイコン](media/hlp-16doc.gif "レポート アイコン")|レポート|レポート アイコンまたは名前をクリックすると、レポートが開きます。 レポートは、別のウィンドウで開きます。|  
|![モデル アイコン](media/model-icon.gif "モデル アイコン")|レポート モデル|レポート モデル アイコンをクリックすると、モデル プロパティのページが開きます。|  
|![リンク レポート アイコン](media/hlp-16linked.gif "リンク レポート アイコン")|リンク レポート|リンク レポートのアイコンまたは名前をクリックすると、リンク レポートが開きます。 レポートは、別のウィンドウで開きます。|  
|![フォルダー アイコン](media/hlp-16folder.gif "フォルダー アイコン")|フォルダー|フォルダー アイコンまたは名前をクリックすると、フォルダーが開きます。|  
|![サブスクリプション アイコン](media/hlp-16subscription.gif "サブスクリプション アイコン")|サブスクリプション|サブスクリプション アイコンまたは説明をクリックすると、サブスクリプションを編集できます。|  
|![データ ドリブン サブスクリプション アイコン](media/hlp-16subscriptiondd.gif "データ ドリブン サブスクリプション アイコン")|データ ドリブン サブスクリプション|データ ドリブン サブスクリプション アイコンまたは説明をクリックすると、サブスクリプションを編集できます。|  
|![汎用リソース アイコン](media/hlp-16file.gif "汎用リソース アイコン")|リソース|リソース アイコンまたは名前をクリックすると、リソースが開きます。 リソースは、別のウィンドウで開きます。|  
|![共有データ ソースのアイコン](media/hlp-16datasource.png "共有データ ソースのアイコン")|共有データ ソース アイテム|共有データ ソースのアイコンをクリックすると、データ ソースのプロパティ ページ、レポートの一覧、およびサブスクリプションの一覧が開きます。|  
|![プロパティ ページのアイコン](media/hlp-16prop.gif "プロパティ ページ アイコン")|プロパティ ページ|プロパティ ページのアイコンをクリックすると、プロパティおよびセキュリティを設定するためのその他のページにアクセスできます。|  
  
## <a name="see-also"></a>関連項目

- [URL の構成 &#40;SSRS 構成マネージャー&#41;](install-windows/configure-a-url-ssrs-configuration-manager.md)
- [Reporting Services と Power View のブラウザー サポートの計画&#40;Reporting Services 2014&#41;](../../2014/reporting-services/browser-support-for-reporting-services-and-power-view.md)
- [レポート ビルダー &#40;SSRS&#41;](tools/report-builder-authoring-environment-ssrs.md)
- - [Reporting Services ツール](tools/reporting-services-tools.md)
- [レポート サーバー コンテンツの管理 &#40;SSRS ネイティブ モード&#41;](report-server/report-server-content-management-ssrs-native-mode.md)  
[レポート マネージャー F1 ヘルプ](../../2014/reporting-services/report-manager-f1-help.md)