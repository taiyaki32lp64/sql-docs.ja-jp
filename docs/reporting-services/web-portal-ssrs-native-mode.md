---
title: レポート サーバーの Web ポータル (SSRS ネイティブ モード) | Microsoft Docs
ms.date: 12/05/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.description: The web portal of a Reporting Services report server is a web-based experience for viewing reports, mobile reports, KPIs, and navigating through the elements in your report server instance.
ms.topic: conceptual
ms.assetid: 7349e626-6ed5-4d21-b05f-cf042ad9ad70
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 42844a8783f5d1e1066667ed828906c0549f84c2
ms.sourcegitcommit: f76b4e96c03ce78d94520e898faa9170463fdf4f
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70874912"
---
# <a name="the-web-portal-of-a-report-server-ssrs-native-mode"></a>レポート サーバーの Web ポータル (SSRS ネイティブ モード)

[!INCLUDE[ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../includes/ssrs-appliesto-pbirs.md)]

Reporting Services レポート サーバーの Web ポータルは Web ベース エクスペリエンスです。 このポータルでは、レポート、モバイル レポート、KPI を表示したり、レポート サーバー インスタンス内の要素間を移動したりできます。 Web ポータルを利用し、1 つのレポート サーバー インスタンスを管理することもできます。

![ssRSPortal](../reporting-services/media/ssrsportal.png)

## <a name="what-is-the-web-portal"></a>Web ポータルとは何か

Web ポータルを利用し、次のタスクを実行できます。

- レポートの表示、検索、印刷、およびサブスクライブ。
- サーバー上のアイテムを整理するフォルダー階層の作成、セキュリティ保護、および保守。
- アイテムおよび操作に対するアクセスを決定するロールベースのセキュリティの構成。
- レポート実行プロパティ、レポート履歴、およびレポート パラメーターの構成。
- スケジュールおよびデータ ソース接続をさらに管理しやすくする共有スケジュールおよび共有データ ソースの作成。
- 大きい受信者一覧にレポートをロール アウトするデータ ドリブン サブスクリプションの作成。
- 既存レポートの再利用や目的変更を行うための、リンク レポートの作成。
- Report Builder や Mobile Report Publisher など、一般的なツールのダウンロード。
- [KPI の作成](../reporting-services/working-with-kpis-in-reporting-services.md)。
- フィードバックや機能要求の送信。

Web ポータルでは、レポート サーバー フォルダーを参照したり、特定のレポートを検索したりできます。 レポート、その全般プロパティ、レポート履歴にキャプチャされているレポートの過去のコピーを表示できます。 権限に応じて、レポートにサブスクライブし、電子メールの受信ボックスやファイル システム上の共有フォルダーに配信させることもできます。

> [!NOTE]
> サポートされているブラウザーやバージョンの詳細については、「 [Reporting Services のブラウザー サポートの計画](../reporting-services/browser-support-for-reporting-services-and-power-view.md)」を参照してください。

Web ポータルは、ネイティブ モードで実行されているレポート サーバーでのみ使用されます。 SharePoint 統合モード用に構成されたレポート サーバーでは使用できません。

一部の Web ポータル機能は、特定のエディションの [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] だけで利用できます。 詳しくは、「[SQL Server の各エディションがサポートする Reporting Services の機能](../reporting-services/reporting-services-features-supported-by-the-editions-of-sql-server-2016.md)」をご覧ください。

新しくインストールした場合、コンテンツおよび設定を操作するのに十分な権限を持っているのはローカル管理者のみです。 他のユーザーに権限を与えるには、ローカル管理者がレポート サーバーへのアクセスを許可するロールの割り当てを作成する必要があります。 ロールの割り当てが作成された後、ユーザーがアクセスできるようになるアプリケーション ページとタスクは、そのユーザーに対するロールの割り当てによって異なります。 詳細については、「[レポート サーバーへのユーザー アクセスを許可する](security/grant-user-access-to-a-report-server-report-manager.md)」をご覧ください。

> [!NOTE]
> サーバーが実行されているローカル コンピューターで Web ポータルを閲覧している場合、このフォルダーの表示が禁止されている旨のメッセージが表示されることがあります。 これは Universal Access Control (UAC) による規制であり、また、ユーザーが管理者としてブラウザーを実行していないことに起因します。Microsoft Edge を管理者として実行することはできません。Internet Explorer を使用する必要があります。 リモートでサーバーを閲覧するか、管理者として Internet Explorer を起動し、Web ポータルを閲覧できます。 Web ポータルをリモートで利用する場合、自分のアカウントにフォルダーのコンテンツ管理権限を与える必要があります。  

## <a name="start-and-use-the-web-portal"></a>Web ポータルの開始と使用

Web ポータルは Web アプリケーションであり、ブラウザー ウィンドウのアドレス バーに [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)] の URL を入力して起動します。 [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)] の起動時に表示されるページ、リンク、オプションは、レポート サーバーに対してユーザーが持っている権限によって異なります。 タスクを実行するには、そのタスクを含むロールに割り当てられている必要があります。  すべての権限を持つロールに割り当てられたユーザーは、レポート サーバーの管理に利用できるすべてのアプリケーション メニューとページにアクセスできます。 一方、レポートの表示と実行の権限を持つロールに割り当てられたユーザーは、それらの操作をサポートするメニューとページのみを表示できます。 各ユーザーに対して、レポート サーバーごとに異なるロールを割り当てることも、単一のレポート サーバーに保存されている多様なレポートまたはフォルダーごとに異なるロールを割り当てることもできます。

ロールの詳細については、「 [ネイティブ モードのレポート サーバーに対する権限の許可](../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)」を参照してください。

### <a name="start-the-web-portal"></a>Web ポータルを開始するには

次の手順でブラウザーから Web ポータルを起動します。

1. Web ブラウザーを開きます。 サポートされている Web ブラウザーの一覧は「 [Reporting Services のブラウザー サポートの計画](../reporting-services/browser-support-for-reporting-services-and-power-view.md)」でご確認いただけます。

2. Web ブラウザーのアドレス バーに、Web ポータルの URL を入力します。

    既定の URL は *https://[ComputerName]/reports*です。

    レポート サーバーは、特定のポートを使用するように構成できます。 たとえば、*https://[ComputerName]:80/reports* または *https://[ComputerName]:8080/reports*。

## <a name="grouping-by-categories"></a>カテゴリ別のグループ化

Web ポータルは、アイテムを複数のカテゴリにグループ化します。 次のようなカテゴリがあります。

- KPI
- モバイル レポート
- ページネーションのあるレポート
- Power BI Desktop レポート
- Excel ブック
- [データセット]
- ソリューション エクスプローラー
- リソース

右上の **[表示]** を選択すると、表示内容を変更できます。 [非表示項目の表示] を選択した場合、そのアイテムは薄い色で表示されます。

![ssRSWebPortal-view](../reporting-services/media/ssrswebportal-view.png)

![ssRSWebPortal-hidden](../reporting-services/media/ssrswebportal-hidden.png)

### <a name="power-bi-desktop-reports-and-excel-workbooks"></a>Power BI Desktop レポートと Excel ブック

Power BI Desktop レポートと Excel ブックのアクセス許可をアップロード、整理、管理できます。 Web ポータル内でグループ化されます。

![ssRSWebPortal-view-pbi-and-excel](../reporting-services/media/ssrswebportal-view-pbi-and-excel.png)

ファイルは他のリソース ファイルと同様に Reporting Services 内に保管されます。 いずれかのアイテムを選択すると、デスクトップにローカル ダウンロードされます。 レポート サーバーに再アップロードすることで、変更を保存できます。

## <a name="search-for-items"></a>アイテムの検索

検索語句を入力すると、ユーザーがアクセスできるアイテムが表示されます。 結果は KPI、レポート、データセット、その他のアイテムに分類されます。 その後、結果を使用したり、お気に入りに追加したりできます。

![ssRSWebPortal-Search](../reporting-services/media/ssrswebportal-search.png)

## <a name="web-portal-tasks"></a>Web ポータル タスク

[Web ポータルのブランド化](../reporting-services/branding-the-web-portal.md)

[KPI の操作](../reporting-services/working-with-kpis-in-reporting-services.md)

[共有データセットの操作](../reporting-services/work-with-shared-datasets-web-portal.md)

## <a name="see-also"></a>参照

[SQL Server Mobile Report Publisher を使用してモバイル レポートを作成する](../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)  
[URL の構成 (SSRS 構成マネージャー)](../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)  
[Reporting Services ツール](../reporting-services/tools/reporting-services-tools.md)  
[Reporting Services のブラウザー サポートの計画](../reporting-services/browser-support-for-reporting-services-and-power-view.md)  
[SQL Server の各エディションがサポートする Reporting Services の機能](../reporting-services/reporting-services-features-supported-by-the-editions-of-sql-server-2016.md)  

その他の質問 [Reporting Services のフォーラムにアクセスします](https://go.microsoft.com/fwlink/?LinkId=620231)
