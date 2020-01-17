---
title: SQL Server のレポート ビルダー | Microsoft Docs
ms.date: 05/10/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-builder
ms.topic: conceptual
f1_keywords:
- "10428"
helpviewer_keywords:
- overview of Report Builder
- getting started
ms.assetid: 55bf4f9c-d037-412f-ae57-3fc39ce32fa5
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: c10e37d7c1231a3ed4db2d7412ea223cccc6922d
ms.sourcegitcommit: 5d839dc63a5abb65508dc498d0a95027d530afb6
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/09/2019
ms.locfileid: "67688511"
---
# <a name="report-builder-in-sql-server"></a>SQL Server のレポート ビルダー

 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] は、Visual Studio/SSDT のレポート デザイナーよりもスタンドアロン環境での作業を好むビジネス ユーザー向けの、ページ分割されたレポートを作成するためのツールです。  ページ分割されたレポートをデザインすることは、取得するデータ、その取得場所、およびその表示方法を指定するレポート定義を作成することです。 レポートを実行するとき、レポート プロセッサは、指定されたレポート定義を受け取り、データを取得し、それをレポート レイアウトに結合して、レポートを生成します。 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)]でレポートをプレビューできます。 その後、ネイティブ モードまたは SharePoint 統合モード (2016 以前) でレポートを [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] レポート サーバーにパブリッシュします。 

ページ分割されたレポートを Power BI サービスにパブリッシュすることもできます。 詳しくは、[Power BI Premium のページ分割されたレポート](https://docs.microsoft.com/power-bi/paginated-reports-report-builder-power-bi) (プレビュー) に関するページをご覧ください。
  
 ![rs_GettingStartedReport](../../reporting-services/report-builder/media/rs-gettingstartedreport.png "rs_GettingStartedReport")  
  
 この改ページ調整されたレポートでは、行グループ、列グループ、スパークライン、インジケーター、およびコーナー セルの概要円グラフが含まれたマトリックスが使用されています。色と円サイズで表される 2 組の地理データが含まれた地図も使用されています。  
  
##  <a name="JumpStartReptCreation"></a> レポート作成の開始  
  
-   **共有データセットから開始する**。 共有データセットは、共有データ ソースに基づくクエリで、ネイティブ モードまたは SharePoint 統合モードの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] レポート サーバーに保存されます。  
  
-   **テーブル、マトリックス、グラフの各ウィザードから開始**します。 データ ソース接続を選択したり、フィールドをドラッグ アンド ドロップしてデータセット クエリを作成したりできます。また、レイアウトとスタイルを選択して、レポートをカスタマイズできます。  
  
-   **マップ ウィザードから開始** して、地図や幾何図形を背景として集計データを表示するレポートを作成します。 マップ データには、 [!INCLUDE[tsql](../../includes/tsql-md.md)] クエリや Environmental Systems Research Institute, Inc. (ESRI) シェープファイルの空間データを指定できます。 また、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Bing のマップ タイルの背景を追加することもできます。  
  
-   **レポート パーツからレポートの作成を開始する**。 レポート パーツとは、ネイティブ モードまたは SharePoint 統合モードの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] レポート サーバーに個別にパブリッシュされたレポート アイテムです。 レポート パーツは、他のレポートに再利用できます。 テーブル、マトリックス、グラフ、画像などのレポート アイテムを、レポート パーツとしてパブリッシュできます。  
  
##  <a name="DesignRept"></a> レポートのデザイン  
  
-   **テーブル、マトリックス、グラフ、および自由形式のレポート レイアウトの改ページ調整されたレポートを作成します。** 列単位のデータにはテーブル形式のレポート、集約されたデータにはマトリックス形式のレポート (クロス集計レポートや PivotTable レポートなど)、グラフィック データにはグラフ形式のレポート、これ以外のすべてのデータには自由形式のレポートを作成します。 レポートでは、Web ベースの動的アプリケーションのリスト、グラフィック、およびコントロールと共に、他のレポートやグラフを埋め込むことができます。  
  
-   **さまざまなデータ ソースからレポートを作成します。** [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] マネージド データ プロバイダー、OLE DB プロバイダー、ODBC データ ソースのいずれかを含む任意のデータ ソースの種類のデータを使用してレポートを作成します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] と [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]、Oracle、Hyperion、およびその他のデータベースのリレーショナル データおよび多次元データを使用するレポートを作成できます。 XML データ処理拡張機能を使用すると、任意の XML データ ソースからデータを取得できます。 テーブル値関数を使用すると、カスタム データ ソースをデザインできます。  
  
-   **既存のレポートを変更します。** [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)]を使用すると、 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]のレポート デザイナーで作成されたレポートをカスタマイズおよび更新できます。  
  
-   データのフィルター選択、グループ化と並べ替え、または数式や式の追加によって、**データを変更します。**  
-   データをビジュアルな形式でまとめ、大量の集計情報がひとめでわかるようにするため、**グラフ、ゲージ、スパークライン、およびインジケーターを追加します。**  
  
-   ドキュメント マップ、表示/非表示を切り替えるボタン、サブレポートおよび詳細レポートへのドリルスルー リンクなど、**対話機能を追加します** 。 パラメーターとフィルターを使用すると、カスタマイズされたビューのデータをフィルター処理できます。  
  
-   外部コンテンツなど、**画像やその他のリソースを埋め込んだり参照したりします。**  
  
##  <a name="ManageRpt"></a> レポートの管理  
  
-   コンピューターまたはレポート サーバーに**レポートの定義を保存** し、そこでレポートを管理し、他のユーザーと共有します。  
  
-   レポートを開くとき、またはレポートを開いた後、**表示形式を選択** します。 Web 指向、ページ指向、およびデスクトップ アプリケーションの形式を選択できます。 形式には、HTML、MHTML、PDF、XML、CSV、TIFF、Word、および Excel があります。  
  
-   **サブスクリプションを設定します。** レポート サーバーまたは SharePoint 統合モードのレポート サーバーにレポートをパブリッシュした後、特定の時刻にレポートを実行したり、レポート履歴の作成や、電子メール サブスクリプションの設定を行うなど、レポートに対するさまざまな構成を行うことができます。  
  
-   Reporting Services の Atom 表示拡張機能を使用して、レポートから**データ フィードを生成** します。  
  
> [!NOTE]  
>  パブリッシュされたレポートは、レポート サーバー上または SharePoint 統合モードのレポート サーバー上で、レポート サーバー管理者が管理します。 レポート サーバー管理者は、セキュリティの定義、プロパティの設定、および操作 (レポート履歴や電子メールによるレポート配信など) のスケジュール設定を行うことができます。 共有スケジュールおよび共有データ ソースを作成し、それらを一般的な用途で使用できます。 管理者はさらに、レポート サーバーのすべてのフォルダーの管理も行います。 実行できる管理タスクは、ユーザー権限により異なります。  
  
## <a name="see-also"></a>参照  
  [レポート ビルダーの起動](../../reporting-services/report-builder/start-report-builder.md)  
  
  [レポート ビルダーをインストールする](../../reporting-services/install-windows/install-report-builder.md)

  [SQL Server Reporting Services とレポート ビルダーの新機能](~/reporting-services/what-s-new-in-sql-server-reporting-services-ssrs.md)  
  このバージョンの [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] および [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)]の新機能について説明します。   
  [チュートリアル: オフラインでのクイック グラフ レポートの作成](../../reporting-services/report-builder/tutorial-create-a-quick-chart-report-offline-report-builder.md)  
 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] とレポートの作成に使用できるウィザードを紹介します。 このチュートリアルには、作業用の一連のデータが用意されているため、データ ソースに接続せずに実習を開始できます。  
  
 [レポートの計画 (レポート ビルダー)](../../reporting-services/report-design/planning-a-report-report-builder.md)  
 レポートを作成する前の考慮事項について説明します。  
  
 [Reporting Services の概念 (SSRS)](../reporting-services-concepts-ssrs.md)  
 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] のドキュメント全体で使用する主要な概念について説明します。  
  
 [レポート デザイン ビュー (レポート ビルダー)](../../reporting-services/report-builder/report-design-view-report-builder.md)  
 レポート デザイン ビューの各ペインと領域について説明します。  
  
 [共有データセット デザイン ビュー (レポート ビルダー)](../../reporting-services/report-builder/shared-dataset-design-view-report-builder.md)  
 共有データセット デザイン ビューの各ペインと領域について説明します。  
  
 [キーボード ショートカット (レポート ビルダー)](../../reporting-services/report-builder/keyboard-shortcuts-report-builder.md)  
 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)]でレポートのナビゲーションとデザインに使用できるショートカット キーについて説明します。  
  

