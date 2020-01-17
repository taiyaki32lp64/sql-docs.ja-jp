---
title: Reporting Services レポート (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Reporting Services, report creation
ms.assetid: 52ed9e74-f2c8-488b-a2c2-6dfbc2a2c8cc
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 97e99e90d50b6a033f8cc2fe12ce3233ee56c959
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66102468"
---
# <a name="reporting-services-reports-ssrs"></a>Reporting Services レポート (SSRS)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] レポートは、レポート データ要素とレポート レイアウト要素を含む XML ベースのレポート定義です。 クライアント ファイル システムでは、レポート定義に .rdl というファイル拡張子が付きます。 レポートがパブリッシュされると、レポート サーバーまたは SharePoint サイトに格納されたレポート アイテムです。 レポートは、[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] によって提供されるサーバー ベースのレポート プラットフォームの一部です。  
  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] を初めて使用する場合は、必ず「[Reporting Services Concepts (SSRS)](../reporting-services-concepts-ssrs.md)」(Reporting Services の概念 (SSRS)) を参照してください。  
  
## <a name="benefits-of-reporting-services-reports"></a>Reporting Services レポートの利点  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] レポート ソリューションは、次の目的に使用できます。  
  
-   1 つのバージョンのファクトを提供する 1 つのデータ ソース セットを使用する。 レポートの基本をこれらのデータ ソースにして、ビジネス上の意思決定に役立つ統合データ表示を行うことができます。  
  
-   データ領域を使用して相互接続された複数の方法でデータを表示する。 テーブル、マトリックス、またはクロス集計に構成したデータの表示、グループ、グラフ、ゲージ、インジケーター、または KPI、およびマップの展開/折りたたみを行います。テーブルのグラフを入れ子にすることもできます。  
  
-   個人的に使用するためにレポートを表示したり、レポート サーバーまたは SharePoint サイトにレポートをパブリッシュしてチームまたは組織と共有する。  
  
-   一度定義したレポートをさまざまな方法で表示する。 レポートをさまざまなファイル形式にエクスポートしたり、レポートを電子メールでサブスクライバーに配信したり、共有ファイルに配信できます。 同じレポート定義に異なるパラメーター セットを適用する複数のリンク レポートを作成できます。  
  
-   レポート パーツ、共有データ ソース、共有クエリ、およびサブレポートを使用して、再利用のためのデータの視覚化を定義する。  
  
-   レポート定義とは別にレポート データ ソースを管理する。 たとえば、レポートを変更しなくても、テスト データ ソースから実稼働データ ソースに変更できます。  
  
-   自由形式のレイアウトでレポートをデザインする。 レポート レイアウトは、データを帯状に配置するだけではありません。 理解を助け、明確で対策を取りやすい形式にデータを構成することができます。  
  
-   ドリルスルー アクション、展開/折りたたみの切り替え、並べ替えボタン、ツールヒント、およびレポート パラメーターを有効にし、レポートを表示するユーザーがレポートを対話形式で操作できるようにする。 レポート パラメーターを作成された式と組み合わせて使用することで、レポートを表示するユーザーがデータのフィルター方法、グループ化方法、および並べ替え方法を制御できるようにします。  
  
-   レポート データのフィルター方法、グループ化方法、および並べ替え方法をカスタマイズする機能を提供するための式を定義する。  
  
 ![rs_GettingStartedReport](../media/rs-gettingstartedreport.gif "rs_GettingStartedReport")  
  
##  <a name="bkmk_StagesSummary"></a> レポート処理の段階  
 レポートを作成するときは、XML 形式でレポート定義ファイル (.rdl) を定義します。 このファイルには、レポート プロセッサでレポート データとレポート レイアウトを組み合わせるために必要なすべての情報が含まれます。 レポートを表示すると、次の段階に従ってレポートが処理されます。  
  
-   **コンパイル。** レポート定義の式を評価し、コンパイルされた中間形式をレポート サーバーの内部に格納します。  
  
-   **処理。** データセット クエリを実行し、中間形式をデータおよびレイアウトと組み合わせます。  
  
-   **表示。** 処理したレポートを表示拡張機能に送信し、各ページに配置できる情報量を判断してページ分けしたレポートを作成します。  
  
-   **エクスポート (省略可能)。** レポートを別のファイル形式にエクスポートします。  
  
 詳細については、「[Reporting Services の概念 &#40;SSRS &#41;](../reporting-services-concepts-ssrs.md)」の「[レポート開発の段階](../reporting-services-concepts-ssrs.md#bkmk_StagesofReports)」を参照してください。  
  
## <a name="create-reports"></a>レポートの作成  
 レポートを作成するには:  
  
-   **レポートの目的を決定します。** レポートを使用する対象ユーザーのためにレポートの目的を確認します。 適切にデザインされたレポートでは、レポートを表示するユーザーの理解を助け具体的な行動につながる情報が得られます。 この段階で行われたデザイン上の決定によって、後で選択するレポート パラメーター、レポート レイアウトのデザイン、およびレポートの表示方法が決まります。 詳細については、msdn.microsoft.com の[レポート ビルダーに関するドキュメント](https://go.microsoft.com/fwlink/?LinkId=154494)の「[ &#40;レポート ビルダー&#41;](../report-design/planning-a-report-report-builder.md)」および「[ &#40;レポート ビルダーおよび SSRS&#41;](../report-design/report-design-tips-report-builder-and-ssrs.md)」を参照してください。  
  
-   **クエリの種類を選択します。** 一般的な共有データセット クエリまたはレポート セットに固有のデータセット クエリのどちらを使用するかを決定します。 一般的なクエリの共有データセットは複数のレポートに使用する場合に維持しやすい一方で、各レポート デザイナーが特定のレポート セットの必要性に応じてデータをフィルターする必要があります。 詳細については、「[Report Data (SSRS)](../report-data/report-data-ssrs.md)」(レポート データ (SSRS)) を参照してください。  
  
-   **関連データの表示を計画します。** レポートを表示するユーザーのための表示方法を計画します。 詳細データをドリル ダウンできる集計レポートは、大量のデータを処理するときに有益なアプローチです。 詳細については、「 [ドリルスルー、ドリルダウン、サブレポート、および入れ子になったデータ領域 (レポート ビルダーおよび SSRS)](../report-design/drillthrough-drilldown-subreports-and-nested-data-regions.md)」を参照してください。  
  
-   **権限を構成します。** 適切なレベルの権限を許可するための方法を計画します。 一般的には、レポート サーバーにフォルダー構造を作成し、レポートおよびレポート関連アイテムをベースとするロールとフォルダーのセキュリティにアクセスを許可します。 詳細については、「 [レポートのセキュリティ保護](#bkmk_SecureReportsSummary)」を参照してください。  
  
-   **作成環境を選択します。** 各作成ツールは異なる機能をサポートしています。 詳細については、「 [Reporting Services ツール](../tools/reporting-services-tools.md)」を参照してください。  
  
-   各レポートに対して:  
  
    -   **データのソースを特定します。** データの各ソースに対して、1 つのレポート データ ソースを定義します。 詳細については、「[Reporting Services でのデータ接続、データ ソース、および接続文字列](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)」を参照してください。  
  
    -   **各ソースから使用するデータを選択します。** 各データ ソースに対して、レポート データセットを定義します。 各データセットには、使用するデータを指定するためのクエリが含まれます。 レポート パラメーターがある場合、データセットを定義して各パラメーターに使用できる値リストを設定します。 詳細については、「[レポートへのデータの追加 &#40;レポート ビルダーおよび SSRS&#41;](../report-data/report-datasets-ssrs.md)」および「[レポート パラメーター &#40;レポート ビルダーおよびレポート デザイナー&#41;](../report-design/report-parameters-report-builder-and-report-designer.md)」を参照してください。  
  
    -   **データの視覚化を選択します。** 各データセットに対して、データの表示に使用するデータ領域を選択します。 テーブル、グラフ、ゲージ、およびマップからリストを選択します。 詳細については、次の各トピックを参照してください。  
  
        -   [テーブル、マトリックス、および一覧 (レポート ビルダーおよび SSRS)](../report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)  
  
        -   [グラフ &#40;レポート ビルダーおよび SSRS&#41;](../report-design/charts-report-builder-and-ssrs.md)  
  
        -   [スパークラインとデータ バー (レポート ビルダーおよび SSRS)](../report-design/sparklines-and-data-bars-report-builder-and-ssrs.md)  
  
        -   [インジケーター (レポート ビルダーおよび SSRS)](../report-design/indicators-report-builder-and-ssrs.md)  
  
        -   [マップ (レポート ビルダーおよび SSRS)](../report-design/maps-report-builder-and-ssrs.md)  
  
        -   [ゲージ (レポート ビルダーおよび SSRS)](../report-design/gauges-report-builder-and-ssrs.md)  
  
    -   **データとレイアウトをカスタマイズします。** レポート レイアウトをデザインします。 レポート定義には、レポート本文、データ ソース、データセット、データ領域、テキスト ボックス、線、および画像があります。 四角形はレイアウトおよび視覚的要素のコンテナーとして使用されます。 データのフィルター、グループ化、並べ替え、書式、および表示を制御するための式を作成することで、各データ領域をカスタマイズします。 レポート名、場所、および数十または数百単位のレポートの管理に役立つその他の識別情報を追加します。 ページのレイアウト要素をまとめるために、視覚的要素およびコンテナーを追加します。 詳細については、次の各トピックを参照してください。  
  
        -   [データのフィルター、グループ化、および並べ替え (レポート ビルダーおよび SSRS)](../report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)  
  
        -   [レポート パラメーター &#40;レポート ビルダーおよびレポート デザイナー&#41;](../report-design/report-parameters-report-builder-and-report-designer.md)  
  
        -   [式 (レポート ビルダーおよび SSRS)](../report-design/expressions-report-builder-and-ssrs.md)  
  
        -   [レポート アイテムの書式設定 (レポート ビルダーおよび SSRS)](../report-design/formatting-report-items-report-builder-and-ssrs.md)  
  
        -   [画像、テキスト ボックス、四角形、および罫線 (レポート ビルダーおよび SSRS)](../report-design/rectangles-and-lines-report-builder-and-ssrs.md)  
  
        -   [ページ レイアウトとレンダリング (レポート ビルダーおよび SSRS)](../report-design/page-layout-and-rendering-report-builder-and-ssrs.md)  
  
    -   **対話機能を構成します。** レポートを表示するユーザーのために、対話機能を追加します。 たとえば、並べ替えボタンやクエリを表示するための切り替えアイテムを追加します。 詳細については、「[Interactive Sort, Document Maps, and Links (Report Builder and SSRS)](../report-design/interactive-sort-document-maps-and-links-report-builder-and-ssrs.md)」(対話的な並べ替え、ドキュメント マップ、およびリンク (レポート ビルダーおよび SSRS)) を参照してください。  
  
    -   **デザインを確認して繰り返し使用します。** レポートをプレビューします。 予備バージョンをパブリッシュして、レポートを表示するユーザーからフィードバックを得ます。 デザインを繰り返し使用します。  
  
-   **レポート ソリューションを確認します。** レポート セットが正しく対話することを確認します。  
  
-   **再利用できるコンポーネントを検討します。**  再利用のために共有できるデータ ソースまたはデータセット クエリがあるかどうかを確認します。 再利用できる場合は、レポート サーバーまたは SharePoint サイトで共有データ ソースと共有データセットを作成します。 データ領域がレポート パーツとして再利用するために適しているかどうかを確認します。 詳細については、「[レポート デザイナーでのレポート パーツ (SSRS)](../report-design/report-parts-in-report-designer-ssrs.md)」を参照してください。  
  
## <a name="preview-reports"></a>レポートのプレビュー  
 各レポート作成ツールでは、レポートのプレビューがサポートされています。 詳細については、msdn.microsoft.com の[レポート ビルダーに関するドキュメント](https://go.microsoft.com/fwlink/?LinkId=154494)の「[プレビュー](../tools/design-reporting-services-paginated-reports-with-report-designer-ssrs.md#bkmk_Preview)」、「[レポート ビルダー &#40;SSRS&#41;](../tools/report-builder-authoring-environment-ssrs.md)」、および「[レポート ビルダーでのレポートのプレビュー](../report-builder/previewing-reports-in-report-builder.md)」を参照してください。  
  
## <a name="save-or-publish-reports"></a>レポートの保存またはパブリッシュ  
 各レポート作成ツールでは、レポートのローカル保存またはレポート サーバーか SharePoint サイトへのレポートのパブリッシュがサポートされています。 詳細については、msdn.microsoft.com の[レポート ビルダーに関するドキュメント](https://go.microsoft.com/fwlink/?LinkId=154494)の「[保存と配置](../tools/design-reporting-services-paginated-reports-with-report-designer-ssrs.md#bkmk_SaveandDeploy)」、「[レポート ビルダー &#40;SSRS&#41;](../tools/report-builder-authoring-environment-ssrs.md)」、および「[レポートの保存 &#40;レポート ビルダー&#41;](../report-builder/saving-reports-report-builder.md)」を参照してください。  
  
## <a name="view-reports"></a>レポートの表示  
 ローカル保存されたレポートやレポート サーバーにパブリッシュされたレポートのプレビューに加えて、ユーザーのためにさまざまなレポート表示方法を提供できます。 レポートを表示するには:  
  
-   **ブラウザー。**  レポート サーバー Web サービスまたは SharePoint サイトを使用してパブリッシュされたレポートを表示します。 SharePoint サイトでは、Web パーツを構成してパブリッシュされたレポートを表示することもできます。 詳細については、「[Reporting Services と Power View のブラウザー サポートの計画 &#40;Reporting Services 2014&#41;](../browser-support-for-reporting-services-and-power-view.md)」、「[ &#40;SSRS ネイティブ モード&#41;](../report-manager-ssrs-native-mode.md)」、および「[URL アクセス &#40;SSRS&#41;](../url-access-ssrs.md)」を参照してください。  
  
-   **配信。**  サブスクリプションを構成して、レポートを電子メールでレポートのユーザーに配信するか、共有ファイル フォルダーに配信します。  詳細については「[サブスクリプションと配信 &#40;Reporting Services&#41;](../subscriptions/subscriptions-and-delivery-reporting-services.md)」を参照してください。  
  
-   **エクスポート。**  レポートを表示するユーザーは、レポート ビューアー ツール バーからレポートを異なるファイル形式にエクスポートできます。 エクスポートするファイル形式は、レポート サーバー管理者が構成できます。 詳細については、「[レポートのエクスポート &#40;レポート ビルダーおよび SSRS&#41;](../report-builder/export-reports-report-builder-and-ssrs.md)」を参照してください。  
  
-   **印刷。**  レポートを表示するユーザーは、表示方法に応じてレポートまたはレポートのページを印刷できます。 詳細については、「[Print Reports (Report Builder and SSRS)](../report-builder/print-reports-report-builder-and-ssrs.md)」(レポートの印刷(レポート ビルダーと SSRS)) を参照してください。  
  
-   **Web または Windows フォーム アプリケーション。**  Visual Studio を使用して、レポート ビューアー コントロールをホストする ASP.NET AJAX アプリケーションまたは Windows フォーム アプリケーションを開発します。 このコントロールは、レポート サーバー上にパブリッシュされたレポートを指すことができます。 詳細については、「 [Microsoft レポート](https://go.microsoft.com/fwlink/?LinkID=205399)」を参照してください。  
  
## <a name="manage-reports"></a>レポートの管理  
 パブリッシュされたレポートを管理するには:  
  
-   **データ ソース:** 共有データ ソースと埋め込みデータ ソースはレポート定義とは別に管理されます。  
  
-   **データセット:**  共有データセットはレポート定義とは別に管理されます。  
  
-   **パラメーター。**  パラメーターはレポート定義とは別に管理されます。 レポート サーバーでパラメーターを変更すると、レポート作成クライアントはサーバーで加えた変更をパブリッシュできません。  
  
-   **リソース。**  ESRI シェープファイルの画像および空間データは、レポート定義とは別にパブリッシュして管理できるリソースです。  
  
-   **レポート キャッシュ。**  大きなレポートをオフピーク時に実行するようにスケジュールを設定することで、ピーク時にレポート サーバーに与える処理の影響を軽減できます。  
  
-   **スナップショット。**  同一のデータを使用して作業する必要のある複数のユーザーに一貫した結果を提供するときに、レポート スナップショットを使用します。 変化しやすいデータを使用した場合、レポートを要求するたびに異なる結果が生成される可能性があります。 一方、レポート スナップショットでは、同時点のデータを含む他のレポートや分析ツールとの有効な比較が可能になります。  
  
-   **レポート履歴。** 一連のレポート スナップショットを作成することにより、時間の経過と共にデータがどのように変化するのかを示すレポートの履歴を構築できます。  
  
 パフォーマンスの詳細については、「[Performance, Snapshots, Caching (Reporting Services)](../report-server/performance-snapshots-caching-reporting-services.md)」(パフォーマンス、スナップショット、キャッシュ (Reporting Services)) を参照してください。  
  
##  <a name="bkmk_SecureReportsSummary"></a> レポートのセキュリティ保護  
 レポートのセキュリティを保護するには:  
  
-   レポート サーバー管理者に、 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] のインストールに使用されている承認システムと認証システムを確認します。 既定では、 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] は Windows 認証、統合セキュリティ、およびロールの割り当てを使用してパブリッシュされたレポートへのアクセスを制御しています。 詳細については、「[ロールとアクセス許可 (Reporting Services)](../security/roles-and-permissions-reporting-services.md)」と「[Reporting Services のセキュリティと保護](../security/reporting-services-security-and-protection.md)」を参照してください。  
  
## <a name="create-notifications-based-on-report-data"></a>レポート データに基づく通知の作成  
 SharePoint サイトにパブリッシュされたレポートのデータ警告を作成できます。 データ警告は、レポートのデータ領域からのデータ フィードに基づきます。 既定では、データ領域に自動的に名前が付けられます。 レポート作成者は、ビジネス用途に基づいてデータ領域に名前を付けることで、レポートのデータ警告を作成しやすくすることができます。 データ警告を作成すると、データが指定した条件を満たす場合に、電子メールで通知を受信します。 詳細については、「[Generating Data Feeds from Reports (Report Builder and SSRS)](../report-builder/generating-data-feeds-from-reports-report-builder-and-ssrs.md)」(複数のレポートからのデータ フィードの生成 (レポート ビルダーおよび SSRS))、「[データ警告デザイナーでのデータ警告の作成](../create-a-data-alert-in-data-alert-designer.md)」、「[Reporting Services Data Alerts](../reporting-services-data-alerts.md)」を参照してください。  
  
## <a name="upgrade-reports"></a>Upgrade Reports  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] では、複数バージョンのレポート定義、レポート サーバー、および SharePoint サイトがサポートされています。 レポートをアップグレードするには:  
  
-   レポート サーバーのインストールをアップグレードします。 レポート サーバー上に格納されたコンパイル済みレポートは、初めて使用するときに自動的にアップグレードされます。 レポート定義 (.rdl) は変更されません。 詳細については、「 [Upgrade and Migrate Reporting Services](../install-windows/upgrade-and-migrate-reporting-services.md)」を参照してください。  
  
-   レポート作成環境でレポートを開きます。 多くの場合、レポート定義がアップグレードされます。 詳細については、「[レポートのアップグレード](../install-windows/upgrade-reports.md)」と「[Deployment and Version Support in SQL Server Data Tools (SSRS)](../tools/deployment-and-version-support-in-sql-server-data-tools-ssrs.md)」(SQL Server データ ツールの配置およびバージョン サポート (SSRS)) を参照してください。  
  
## <a name="troubleshoot-reports"></a>レポートのトラブルシューティング  
 レポートのトラブルシューティングを行うには:  
  
-   **問題の発生場所を確認します。** 「 [Stages of a Report](#bkmk_StagesSummary)」(レポートの段階) の情報を確認します。  
  
-   **詳細情報の情報源を確認します。** たとえば、式を含むレポート デザインの場合、レポート ビルダー ツールよりもレポート デザイナー ツールで式の評価問題に関する詳細情報が得られます。 レポートの処理エラーの場合は、ログ ファイルに詳細情報が記録されています。  
  
## <a name="tasks"></a>処理手順  
 手順のリンクについては、このトピックの前のセクションで触れた記事の「タスク」セクションを参照してください。  
  
## <a name="see-also"></a>参照  
 [Reporting Services ツール](../tools/reporting-services-tools.md)   
 [拡張機能 (SSRS)](../extensions-ssrs.md)   
 [Reporting Services Report Server](../reporting-services-report-server.md)  
  
  
