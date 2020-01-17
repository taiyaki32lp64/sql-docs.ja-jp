---
title: Reporting Services レポート サーバー (SharePoint モード) | Microsoft Docs
ms.date: 09/26/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-sharepoint
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
monikerRange: '>=sql-server-2016 <=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: af25232f5a1603f25814309270813188c05a89fc
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68262353"
---
# <a name="reporting-services-report-server-sharepoint-mode"></a>Reporting Services レポート サーバー (SharePoint モード)

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

  **SharePoint モード**用に構成された Reporting Services レポート サーバーは、SharePoint 製品の配置内で実行できます。 SharePoint モードのレポート サーバーは、レポートおよびその他の [!INCLUDE[ssRSnfoversion_md](../../includes/ssrsnoversion-md.md)] コンテンツの種類に対して、SharePoint のコラボレーション機能や管理機能を使用できます。 SharePoint モードでは、適切なバージョンの SharePoint 用 Reporting Services アドインを、SharePoint Web フロント エンド上にインストールする必要があります。  
  
> [!NOTE]
> SharePoint と Reporting Services の統合は、SQL Server 2016 以降では使用できません。

 インストールと構成の詳細については、以下を参照してください。  
  
-   [SharePoint 2010 用 Reporting Services の SharePoint モードのインストール](https://msdn.microsoft.com/47efa72e-1735-4387-8485-f8994fb08c8c)。  
  
-   [ファームへのレポート サーバーの追加](../../reporting-services/install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md)。  
  
## <a name="feature-summary"></a>機能の概要

 SharePoint 統合モードで動作するようにレポート サーバーを構成すると、次のことが可能になります。これらの追加機能はこのモードでレポート サーバーを配置した場合にのみ利用できます。  
  
-   SharePoint ドキュメント管理とコラボレーションの機能 (警告など) を使用できます。 SharePoint サイトは、すべてのレポート アイテムを 1 か所で利用および管理するための統合ポータルとして使用できます。  
  
-   SharePoint の権限と認証プロバイダーを使用して、レポート、モデル、その他のアイテムへのアクセスを制御できます。  
  
-   SharePoint の配置トポロジを使用して、ファイアウォール外のインターネット接続を経由してレポートを配信できます。 レポート サーバーでは、インターネット アクセス用に構成されている大規模な SharePoint 配置でレポートとデータを処理するサービスが提供されます。  
  
-   SharePoint サイトのカスタム アプリケーション ページで、レポート、モデル、データ ソース、スケジュール、レポート履歴を管理できます。 SharePoint サイトでは、プロパティの設定、スケジュールとサブスクリプションの定義、レポート履歴の作成と管理などを、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]で他のツールを使って作成し管理するときと同じ方法で行うことができます。  
  
-   レポート、レポート モデル、リソース、および共有データ ソース ファイルを、Office SharePoint Server のレポート センターなどの SharePoint ライブラリにパブリッシュまたはアップロードできます。  
  
     レポート デザイナー、モデル デザイナー、およびレポート ビルダーを使用して、SharePoint ライブラリに直接パブリッシュするレポートおよびデータ ソースを作成します。 また、SharePoint サイトで [アップロード] アクションを使用して、レポート定義やレポート モデルを SharePoint ライブラリに追加することもできます。  
  
     レポート サーバーでは、使用しているサーバー モードに関係なく同じ方法でレポート定義が処理されるため、レポートのデータとレイアウトがサーバー モードの影響を受けることはありません。 ネイティブ モードのレポート サーバーで実行できるレポートであれば、SharePoint 統合モード用に構成されたレポート サーバーで実行できます。  
  
-   新しい SharePoint 配信拡張機能を使用して、SharePoint ライブラリに対しレポートのサブスクライブと配信を行うことができます。 電子メールや共有フォルダーを使ってレポートを配信することもできます。 レポートの配信にはレポート サーバーの配信拡張機能が使用されます。 実行時にクエリを行うサブスクライバー データを使用して、大規模なレポート配信用のデータ ドリブン サブスクリプションを作成できます。  
  
-   レポート ビューアー Web パーツを SharePoint ページに追加して、SharePoint Web アプリケーション内でレポートを表示することができます。 Web パーツには、ページ ナビゲーション、検索、印刷、エクスポートなどの機能があります。  
  
-   新しい SOAP エンドポイントに対してプログラムを実行し、SharePoint サイトと統合されるカスタム アプリケーションを作成できます。 更新された Windows Management Instrumentation (WMI) プロバイダーを使用して、SharePoint 統合モードで動作するレポート サーバー インスタンスをプログラムから構成することもできます。  
  
-   接続モードの Microsoft Access サービスのレポート機能。  
  
-   SharePoint リストの AAM 領域、インターネットに直接つながっている配置、および SharePoint ユーザー トークン。  
  
## <a name="connected-mode-and-local-mode"></a>接続モードとローカル モード

 SQL Server 2008 R2 リリースでは、SharePoint 2010 用 Microsoft SQL Server 2008 R2 以降の Reporting Services アドインがインストールされている SharePoint 2010 サーバーからレポートを表示するための新しい *ローカル モード* が導入されました。  
  
-   *ローカル モード*: ローカル モードでは、Reporting Services レポート サーバーと統合することなく、SharePoint ドキュメント ライブラリからレポートをローカルに表示できます。 SharePoint 製品では Reporting Services アドインは必須ですが、Reporting Services レポート サーバーは必須ではありません。 アドインは、いくつかの異なる方法でインストールできます (SharePoint 2010 製品準備ツールなど)。 ローカル モードの詳細については、「[レポート ビューアーでのローカル モードと接続モードのレポート](../../reporting-services/report-server-sharepoint/local-mode-vs-connected-mode-reports-in-the-report-viewer.md)」および「[SharePoint 製品用 Reporting Services アドインの検索場所](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)」を参照してください。  
  
-   *接続モード*: 接続モードは、SharePoint サーバーの全体管理を使用して Reporting Services レポート サーバーを SharePoint ファームに統合することによってサポートされます。 レポート サーバーとの統合により、完全なエンド ツー エンドのレポート処理が実現され、SharePoint 2010 のコラボレーション機能やレポート サーバーのサーバー ベースの機能 (サブスクリプション、スナップショット、サーバー ベースの処理など) が提供されます。  
  
## <a name="unsupported-sharepoint-features"></a>サポートされていない SharePoint 機能

 すべての SharePoint 機能が統合操作に使用できるわけではありません。 Reporting Services が直接統合していない SharePoint の機能を次に示します。  
  
-   Secure Store Service。  
  
-   ドキュメント ライブラリの Reporting Services ファイルに対して SharePoint Outlook カレンダー統合や SharePoint スケジュール機能を使用することはできません。  
  
-   SharePoint ビジネス データ カタログ。  
  
-   SharePoint のパーソナル化も Reporting Services ページではサポートされていません。 SharePoint Web アプリケーションが匿名アクセスに対して有効になっている場合、レポート サーバー統合はサポートされません。  
  
-   SharePoint ドキュメント ライブラリのバージョン管理は、SQL Server Reporting Services では **サポートされません** 。 "ドキュメントの改版履歴" が有効なドキュメント ライブラリにレポート アイテムを保存した場合、Reporting Services の機能が正しく働かず、ULS ログにエラーが出力されます。 ULS ログに出力されるエラーの例を次に示します。  
  
    -   "レポートに関連付けられているデータ ソースが無効になっています。"  
  
     ドキュメント ライブラリのバージョン履歴は、[ライブラリ設定] の [バージョン設定] ページで構成されます。  
  
## <a name="supported-combinations-of-the-sharepoint-add-in-and-report-server"></a>SharePoint アドインとレポート サーバーのサポートされる組み合わせ

 レポート サーバー、SharePoint 用 Reporting Services アドイン、および SharePoint 製品のすべての組み合わせで、すべての機能がサポートされているわけではありません。 詳細については、「[SharePoint、Reporting Services サーバー、Reporting Services アドインのサポートされる組み合わせ](../../reporting-services/install-windows/supported-combinations-of-sharepoint-and-reporting-services-server.md)」を参照してください。  
  
> [!NOTE]  
>  Reporting Services アドインの正しいバージョンを SharePoint 製品の対応するバージョンと共に使用する必要があります。  
  
## <a name="components-that-provide-integration"></a>統合を実現するコンポーネント

 複数のサーバーを単一の展開にまとめるには、インストールされている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Reporting Services と SharePoint 製品のインスタンスを統合します。  
  
 統合は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] と、SharePoint 用 Reporting Services アドインによって実現します。 Reporting Services アドインは自由に配布できるコンポーネントです。ダウンロードして、適切なバージョンの SharePoint が動作しているサーバーにインストールできます。  
  
> [!TIP]  
>  レポート サーバー、SharePoint 用 Reporting Services アドイン、および SharePoint 製品のすべての組み合わせで、すべての機能がサポートされているわけではありません。 詳細については、「[SharePoint、Reporting Services サーバー、Reporting Services アドインのサポートされる組み合わせ](../../reporting-services/install-windows/supported-combinations-of-sharepoint-and-reporting-services-server.md)」を参照してください。  
  
-   SharePoint 上では、Reporting Services アドインによって ReportServer プロキシ エンドポイント、レポート ビューアー Web パーツ、およびアプリケーション ページが提供されます。これにより、SharePoint のサイトまたはファームでレポート サーバー コンテンツを表示、保存、および管理することができます。  
  
-   Reporting Services では、更新済みプログラム ファイル、SOAP エンドポイント、カスタムのセキュリティおよび配信の拡張機能が提供されます。 レポート サーバーは、SharePoint 統合モードで実行し、レポートのアクセスと配信を SharePoint サイトのみで専用に行うように構成する必要があります。  
  
 SharePoint 上に Reporting Services アドインをインストールし、2 つのサーバーを統合用に構成した後は、レポート サーバー コンテンツの種類のドキュメントを SharePoint ライブラリにアップロードまたはパブリッシュできます。その後、SharePoint サイトからこれらのドキュメントを表示したり管理できるようになります。 レポート サーバー コンテンツのアップロードとパブリッシュは重要な最初の手順です。Web パーツやページは、SharePoint サイトでレポート定義 (.rdl)、レポート モデル (.smdl)、および共有データ ソース (.rsds) を選択すると使用可能になります。  
  
##  <a name="language-considerations"></a>言語に関する注意点

 [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] 」および「 [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] 製品は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
 SharePoint 製品の配置内で動作するようにレポート サーバーを構成すると、複数の言語が表示されることがあります。 ユーザー インターフェイス、ドキュメント、メッセージは次の言語で表示されます。  
  
- Reporting Services から提供されるすべてのアプリケーション ページ、ツール、エラー、警告、およびメッセージは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の言語のうち Reporting Services インスタンスによって使用される言語で表示されます。  
  
- SharePoint サイトで開くアプリケーション ページ、レポート ビューアー Web パーツ、およびレポート ビルダーは、Reporting Services アドインでサポートされている言語のいずれかで表示されます。 サポートされている言語の一覧を表示するには、[SQL Server ダウンロード](https://msdn.microsoft.com/sql/downloads/)にアクセスし、SQL Server 2016 Reporting Services アドインのダウンロード ページを開いてください。  
  
- SharePoint サイト、SharePoint のサーバーの全体管理、オンライン ヘルプ、メッセージは、Office Server 製品でサポートされる言語で使用できます。  
  
 使用している SharePoint の製品またはテクノロジの言語とレポート サーバーの言語が異なる場合、Reporting Services では言語ファミリの中で最も近い言語が使用されます。 近い言語が使用できない場合、レポート サーバーでは英語が使用されます。  
  
## <a name="related-tasks"></a>関連タスク

 次の表は、Reporting Services SharePoint モードのレポート サーバーに関するタスクをまとめたものです。  
  
|**タスク**|**リンク**|  
|--------------|--------------|  
|SharePoint モードの Reporting Services をインストールおよび構成するための詳細な手順。|「[SharePoint 2010 用 Reporting Services の SharePoint モードのインストール](https://msdn.microsoft.com/47efa72e-1735-4387-8485-f8994fb08c8c)」および「[ファームへのレポート サーバーの追加](../../reporting-services/install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md)」。|  
|レポート サーバーの追加による Reporting Services SharePoint 配置のスケールアウト。|「[ファームへのレポート サーバーの追加](../../reporting-services/install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md)」および「[SharePoint の SQL Server BI 機能の配置トポロジ](https://msdn.microsoft.com/library/39f76bc7-94e6-4dbc-bfa5-d56f4430bb26)」。|  
|表示およびレポート アイテム用の Reporting Services コンポーネントがインストールされている SharePoint Web フロントエンドの追加。|[ファームへの Reporting Services Web フロントエンドの追加](../../reporting-services/install-windows/add-an-additional-reporting-services-web-front-end-to-a-farm.md)|  
|SharePoint でレポート サーバーの電子メールを構成します。|[Reporting Services サービス アプリケーションの電子メールの構成](../install-windows/configure-e-mail-for-a-reporting-services-service-application.md)|
|TechNet Wiki に掲載されている、今リリース向けの最新情報。|[SQL Server 2012 Reporting Services の役立つヒントおよびトラブルシューティング](https://go.microsoft.com/fwlink/?LinkId=221297)。|  

## <a name="next-steps"></a>次の手順

[SharePoint 用 Reporting Services アドインのインストールまたはアンインストール](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)
[SharePoint サイトのレポート ビューアー Web パーツ ](../../reporting-services/report-server-sharepoint/report-viewer-web-part-on-a-sharepoint-site.md)

その他の質問 [Reporting Services のフォーラムに質問してみてください](https://go.microsoft.com/fwlink/?LinkId=620231)
