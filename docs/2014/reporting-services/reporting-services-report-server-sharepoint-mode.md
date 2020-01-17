---
title: Reporting Services レポート サーバー (SharePoint モード) | Microsoft Docs
ms.prod: sql-server-2014
ms.technology: reporting-services-native
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.custom: ''
ms.date: 06/13/2017
ms.openlocfilehash: c89596d916f9a8ec2fea91cdea8f72b1958c5b6c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66102825"
---
# <a name="reporting-services-report-server-sharepoint-mode"></a>Reporting Services レポート サーバー (SharePoint モード)

[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint モード **用に構成された** レポート サーバーは、SharePoint 製品の配置内で実行できます。 SharePoint モードのレポート サーバーは、レポートおよびその他の [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] コンテンツの種類に対して、SharePoint のコラボレーション機能や管理機能を使用できます。 SharePoint モードでは、適切なバージョンの SharePoint 用 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] アドインを、SharePoint Web フロント エンド上にインストールする必要があります。  
  
インストールと構成の詳細については、以下を参照してください。  
  
- [For SharePoint 2013 の Reporting Services SharePoint モードをインストールします。](../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2013.md)  
  
- [SharePoint 2010 用 Reporting Services の SharePoint モードのインストール](../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)。  
  
- [レポート サーバーをファームに追加&#40;SSRS スケール アウト&#41;](install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md)します。  
  
 このリリースの新機能新機能については、'SharePoint'」を参照してください。[新&#40;Reporting Services&#41;](../../2014/reporting-services/what-s-new-reporting-services.md)します。  
  
 **このトピックの内容:**  
  
-   [機能の要約](#bkmk_featuresum)  
  
-   [接続モードとローカル モード](#bkmk_connectedandlocal)  
  
-   [サポートされていない SharePoint 機能](#bkmk_unsupportedsharepoint)  
  
-   [SharePoint アドインとレポート サーバーのサポートされる組み合わせ](#bkmk_supportedcombinations)  
  
-   [統合を実現するコンポーネント](#bkmk_components)  
  
-   [言語に関する注意点](#bkmk_language)  
  
-   [関連タスク](#bkmk_relatedtasks)  
  
##  <a name="bkmk_featuresum"></a> 機能の要約

 SharePoint 統合モードで動作するようにレポート サーバーを構成すると、次のことが可能になります。これらの追加機能はこのモードでレポート サーバーを配置した場合にのみ利用できます。  
  
-   SharePoint ドキュメント管理とコラボレーションの機能 (警告など) を使用できます。 SharePoint サイトは、すべてのレポート アイテムを 1 か所で利用および管理するための統合ポータルとして使用できます。  
  
-   SharePoint の権限と認証プロバイダーを使用して、レポート、モデル、その他のアイテムへのアクセスを制御できます。  
  
-   SharePoint の配置トポロジを使用して、ファイアウォール外のインターネット接続を経由してレポートを配信できます。 レポート サーバーでは、インターネット アクセス用に構成されている大規模な SharePoint 配置でレポートとデータを処理するサービスが提供されます。  
  
-   SharePoint サイトのカスタム アプリケーション ページで、レポート、モデル、データ ソース、スケジュール、レポート履歴を管理できます。 SharePoint サイトでは、プロパティの設定、スケジュールとサブスクリプションの定義、レポート履歴の作成と管理などを、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]で他のツールを使って作成し管理するときと同じ方法で行うことができます。  
  
-   レポート、レポート モデル、リソース、および共有データ ソース ファイルを、Office SharePoint Server のレポート センターなどの SharePoint ライブラリにパブリッシュまたはアップロードできます。  
  
     レポート デザイナー、モデル デザイナー、およびレポート ビルダーを使用して、SharePoint ライブラリに直接パブリッシュするレポートおよびデータ ソースを作成します。 また、SharePoint サイトで [アップロード] アクションを使用して、レポート定義やレポート モデルを SharePoint ライブラリに追加することもできます。  
  
     レポート サーバーでは、使用しているサーバー モードに関係なく同じ方法でレポート定義が処理されるため、レポートのデータとレイアウトがサーバー モードの影響を受けることはありません。 ネイティブ モードのレポート サーバーで実行できるレポートであれば、SharePoint 統合モード用に構成されたレポート サーバーで実行できます。  
  
-   新しい SharePoint 配信拡張機能を使用して、SharePoint ライブラリに対しレポートのサブスクライブと配信を行うことができます。 電子メールや共有フォルダーを使ってレポートを配信することもできます。 レポートの配信にはレポート サーバーの配信拡張機能が使用されます。 実行時にクエリを行うサブスクライバー データを使用して、大規模なレポート配信用のデータ ドリブン サブスクリプションを作成できます。  
  
-   レポート ビューアー Web パーツを SharePoint ページに追加して、SharePoint Web アプリケーション内でレポートを表示することができます。 Web パーツには、ページ ナビゲーション、検索、印刷、エクスポートなどの機能があります。  
  
-   新しい SOAP エンドポイントに対してプログラムを実行し、SharePoint サイトと統合されるカスタム アプリケーションを作成できます。 更新された Windows Management Instrumentation (WMI) プロバイダーを使用して、SharePoint 統合モードで動作するレポート サーバー インスタンスをプログラムから構成することもできます。  
  
-   接続モードの Microsoft Access サービスのレポート機能。  
  
-   SharePoint リストの AAM 領域、インターネットに直接つながっている配置、および SharePoint ユーザー トークン。  
  
##  <a name="bkmk_connectedandlocal"></a> 接続モードとローカル モード

 SQL Server 2008 R2 リリースでは、SharePoint 2010 用 Microsoft SQL Server 2008 R2 以降の Reporting Services アドインがインストールされている SharePoint 2010 サーバーからレポートを表示するための新しい *ローカル モード* が導入されました。  
  
-   *ローカル モード*:ローカル モードでは、 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] レポート サーバーと統合することなく、SharePoint ドキュメント ライブラリからレポートをローカルに表示できます。 SharePoint 製品では [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] アドインは必須ですが、 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] レポート サーバーは必須ではありません。 アドインは、いくつかの異なる方法でインストールできます (SharePoint 2010 製品準備ツールなど)。 ローカル モードの詳細については、「[レポート ビューアーでのローカル モードと接続モードのレポートをレポート ビューアーで&#40;Reporting Services SharePoint モードの&#41;](../../2014/reporting-services/local-vs-connected-mode-report-viewer-reporting-services-sharepoint-mode.md)と[SharePoint 製品用 Reporting Services アドインの検索場所](install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)します。  
  
-   *接続モード*:統合することによって接続モードがサポートされている、[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]レポート サーバーを SharePoint サーバーの全体管理を使用して SharePoint ファームにします。 レポート サーバーとの統合により、完全なエンド ツー エンドのレポート、SharePoint 2010 のコラボレーション機能およびサーバー ベースのレポート サーバーなどの機能を提供することができます。サブスクリプション、スナップショット、およびサーバー ベースの処理。  
  
##  <a name="bkmk_unsupportedsharepoint"></a> サポートされていない SharePoint 機能

 すべての SharePoint 機能が統合操作に使用できるわけではありません。 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] が直接統合していない SharePoint の機能を次に示します。  
  
-   Secure Store Service。  
  
-   ドキュメント ライブラリの Reporting Services ファイルに対して SharePoint Outlook カレンダー統合や SharePoint スケジュール機能を使用することはできません。  
  
-   SharePoint ビジネス データ カタログ。  
  
-   SharePoint のパーソナル化も [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] ページではサポートされていません。 SharePoint Web アプリケーションが匿名アクセスに対して有効になっている場合、レポート サーバー統合はサポートされません。  
  
-   SharePoint ドキュメント ライブラリのバージョン管理は、SQL Server Reporting Services では **サポートされません** 。 "ドキュメントの改版履歴" が有効なドキュメント ライブラリにレポート アイテムを保存した場合、Reporting Services の機能が正しく働かず、ULS ログにエラーが出力されます。 ULS ログに出力されるエラーの例を次に示します。  
  
    -   "レポートに関連付けられているデータ ソースが無効になっています。"  
  
     ドキュメント ライブラリのバージョン履歴は、[ライブラリ設定] の [バージョン設定] ページで構成されます。  
  
##  <a name="bkmk_supportedcombinations"></a> SharePoint アドインとレポート サーバーのサポートされる組み合わせ

 レポート サーバー、SharePoint 用 Reporting Services アドイン、および SharePoint 製品のすべての組み合わせで、すべての機能がサポートされているわけではありません。 詳細については、次を参照してください[SharePoint の組み合わせをサポートし、Reporting Services サーバーとアドイン&#40;SQL Server 2014。&#41;](install-windows/supported-combinations-of-sharepoint-and-reporting-services-server.md)  
  
> [!NOTE]  
>  Reporting Services アドインの正しいバージョンを SharePoint 製品の対応するバージョンと共に使用する必要があります。  
  
##  <a name="bkmk_components"></a> 統合を実現するコンポーネント

 複数のサーバーを単一の展開にまとめるには、インストールされている [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] と SharePoint 製品のインスタンスを統合します。  
  
 統合は、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] と、SharePoint 用 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] アドインによって実現します。 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] アドインは自由に配布できるコンポーネントです。ダウンロードして、適切なバージョンの SharePoint が動作しているサーバーにインストールできます。  
  
> [!TIP]  
>  レポート サーバー、SharePoint 用 Reporting Services アドイン、および SharePoint 製品のすべての組み合わせで、すべての機能がサポートされているわけではありません。 詳細については、「 [SharePoint 組み合わせをサポートし、、Reporting Services サーバーとアドイン&#40;SQL Server 2014&#41;](install-windows/supported-combinations-of-sharepoint-and-reporting-services-server.md)します。  
  
-   SharePoint 上では、 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] アドインによって ReportServer プロキシ エンドポイント、レポート ビューアー Web パーツ、およびアプリケーション ページが提供されます。これにより、SharePoint のサイトまたはファームでレポート サーバー コンテンツを表示、保存、および管理することができます。  
  
-   [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] では、更新済みプログラム ファイル、SOAP エンドポイント、カスタムのセキュリティおよび配信の拡張機能が提供されます。 レポート サーバーは、SharePoint 統合モードで実行し、レポートのアクセスと配信を SharePoint サイトのみで専用に行うように構成する必要があります。  
  
 SharePoint 上に [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] アドインをインストールし、2 つのサーバーを統合用に構成した後は、レポート サーバー コンテンツの種類のドキュメントを SharePoint ライブラリにアップロードまたはパブリッシュできます。その後、SharePoint サイトからこれらのドキュメントを表示したり管理できるようになります。 レポート サーバー コンテンツのアップロードとパブリッシュは重要な最初の手順です。Web パーツやページは、SharePoint サイトでレポート定義 (.rdl)、レポート モデル (.smdl)、および共有データ ソース (.rsds) を選択すると使用可能になります。  
  
##  <a name="bkmk_language"></a> 言語に関する注意点

 [!INCLUDE[SPF2010](../includes/spf2010-md.md)] 」および「 [!INCLUDE[SPS2010](../includes/sps2010-md.md)] 製品は、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  
  
 SharePoint 製品の配置内で動作するようにレポート サーバーを構成すると、複数の言語が表示されることがあります。 ユーザー インターフェイス、ドキュメント、メッセージは次の言語で表示されます。  
  
-   [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] から提供されるすべてのアプリケーション ページ、ツール、エラー、警告、およびメッセージは、 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] の言語のうち [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] インスタンスによって使用される言語で表示されます。  
  
-   SharePoint サイトで開くアプリケーション ページ、レポート ビューアー Web パーツ、およびレポート ビルダーは、[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] アドインでサポートされている言語のいずれかで表示されます。 サポートされている言語の一覧を表示するには、[SQL Server ダウンロード](https://msdn.microsoft.com/sql/downloads/)にアクセスし、[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)][!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] アドインのダウンロード ページを開いてください。  
  
-   SharePoint サイト、SharePoint のサーバーの全体管理、オンライン ヘルプ、メッセージは、Office Server 製品でサポートされる言語で使用できます。  
  
 使用している SharePoint の製品またはテクノロジの言語とレポート サーバーの言語が異なる場合、 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] では言語ファミリの中で最も近い言語が使用されます。 近い言語が使用できない場合、レポート サーバーでは英語が使用されます。  
  
##  <a name="bkmk_relatedtasks"></a> 関連タスク

 次の表は、 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint モードのレポート サーバーに関するタスクをまとめたものです。  
  
|**タスク**|**リンク**|  
|--------------|--------------|  
|SharePoint モードの [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] をインストールおよび構成するための詳細な手順。|[SharePoint 2010 用の SharePoint モード インストールの Reporting Services](../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)と[ファームにレポート サーバーを追加&#40;SSRS スケール アウト&#41;](install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md)します。|  
|レポート サーバーの追加による [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 配置のスケールアウト。|[レポート サーバーをファームに追加&#40;SSRS スケール アウト&#41;](install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md)と[SharePoint での SQL Server BI 機能の配置トポロジ](../sql-server/install/deployment-topologies-for-sql-server-bi-features-in-sharepoint.md)します。|  
|表示およびレポート アイテム用の [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] コンポーネントがインストールされている SharePoint Web フロントエンドの追加。|[ファームへの Reporting Services Web フロントエンドの追加](install-windows/add-an-additional-reporting-services-web-front-end-to-a-farm.md)|  
|[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] のデータ警告機能およびサブスクリプション機能の電子メールの構成。|[Reporting Services サービス アプリケーションの電子メールの構成 (SharePoint 2010 および SharePoint 2013)](install-windows/configure-e-mail-for-a-reporting-services-service-application.md)|  
|TechNet Wiki に掲載されている、今リリース向けの最新情報。|[SQL Server 2012 Reporting Services の役立つヒントおよびトラブルシューティング](https://go.microsoft.com/fwlink/?LinkId=221297)。|  
  
## <a name="see-also"></a>関連項目  
 [インストールまたはアンインストール、Reporting Services アドイン、SharePoint の&#40;SharePoint 2010 および SharePoint 2013&#41; ](install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md) [Hardware and Software Requirements for Reporting Services SharePoint モードの](../../2014/sql-server/install/hardware-and-software-requirements-for-reporting-services-in-sharepoint-mode.md) [SharePoint サイトのレポート ビューアー Web パーツ](../../2014/reporting-services/report-viewer-web-part-on-a-sharepoint-site.md)