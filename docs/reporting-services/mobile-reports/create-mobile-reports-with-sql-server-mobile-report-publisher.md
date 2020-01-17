---
title: SQL Server Mobile Report Publisher を使用してモバイル レポートを作成する | Microsoft Docs
description: オンプレミス データに接続するモバイル デバイス用の Reporting Services モバイル レポートについて説明します。これらレポートには多様なデータ視覚エフェクトが用意されています。
ms.date: 12/06/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: mobile-reports
ms.custom: seodec18
ms.topic: conceptual
ms.assetid: a5a8dbf6-4c3a-435d-8188-d6656c32f229
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 51708fc41bb154fcf67ac3a21bd6680c69e2f2c2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63200535"
---
# <a name="create-mobile-reports-with-sql-server-mobile-report-publisher"></a>SQL Server Mobile Report Publisher を使用してモバイル レポートを作成する
多様なデータ視覚エフェクトが含まれる [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] モバイル レポートについて学びます。これらのレポートはモバイル デバイス用に最適化されており、オンプレミス データに接続します。 

>[!NOTE]
>  Datazen Server のコンテンツ (ダッシュボードや KPI など) を SQL Server [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] サーバーに移行する必要がありますか。 [SQL Server Migration Assistant for Datazen](https://www.microsoft.com/download/details.aspx?id=53128)を使ってみてください。 
 
![SS_MRP_LayoutTabSm](../../reporting-services/media/ss-mrp-layouttabsm.png)  

[!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-long.md)]を使用すると、モバイル デバイスやその他のさまざまな要因に対して最適化された、 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] モバイル レポートをすばやく作成できます。 モバイル レポートでは、時間グラフ、カテゴリ グラフ、比較グラフ、ツリーマップ、カスタム マップなどの多種多様な視覚エフェクトを使用できます。 

* モバイル レポートは、オンプレミスの SQL Server Analysis Services データを含むさまざまなデータ ソースに接続できます。 
* 調整可能なグリッド行とグリッド列と柔軟なモバイル レポート要素を備えたデザイン画面で、任意の画面サイズに対応するモバイル レポートをレイアウトできます。 
* その後、これらのモバイル レポートを Reporting Services サーバーに保存しておき、iPad、iPhone、Android フォンおよびタブレットと、Windows 10 デバイスのブラウザーまたは Power BI モバイル アプリで表示と操作を実行できます。
  
## <a name="create-includessrsnoversionmdincludesssrsnoversion-mdmd--mobile-reports"></a>[!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)]  モバイル レポートの作成  
  
操作を開始するために次の記事が役立ちます。
-  [SQL Server Mobile Report Publisher](https://go.microsoft.com/fwlink/?LinkID=733527)のダウンロード  
-  [Reporting Services モバイル レポートの作成](../../reporting-services/mobile-reports/create-a-reporting-services-mobile-report.md)  
-  [詳細なチュートリアル: SQL Server Reporting Services でのモバイル レポートと KPI の作成](https://christopherfinlan.com/2015/12/21/how-to-create-mobile-reports-and-kpis-in-sql-server-reporting-services-2016-an-end-to-end-walkthrough/) (Christopher Finlan のブログ)  
- [デザイン優先、またはデータ優先](../../reporting-services/mobile-reports/design-first-or-data-first-when-creating-in-reporting-services-mobile-reports.md): シミュレートされたデータで最初にレポートをデザインするか、独自のデータで開始するかどうかを決定します。  
- [Reporting Services モバイル レポートのデータ](../../reporting-services/mobile-reports/data-for-reporting-services-mobile-reports.md): 共有データセットからデータを使用するか、モバイル レポートで使用する Excel ブックからデータを準備します。
- [Reporting Services のモバイル レポートと KPI におけるデータ更新のしくみ](https://christopherfinlan.com/2016/02/10/so-refreshinghow-data-refresh-works-with-mobile-reports-and-kpis-in-reporting-services/) (Christopher Finlan のブログ): 共有データセットのキャッシュの設定について確認し、データが更新される頻度を制御し、レポートのパフォーマンスを高速化します。
- [モバイル レポートでの視覚化](../../reporting-services/mobile-reports/add-visualizations-to-reporting-services-mobile-reports.md)
- [モバイル レポートでのゲージ](../../reporting-services/mobile-reports/add-gauges-to-mobile-reports-reporting-services.md)
- [モバイル レポートでのマップ](../../reporting-services/mobile-reports/maps-in-reporting-services-mobile-reports.md)
- ビジネスの色とロゴを使用する[Web ポータルとモバイル レポートのブランド化](../../reporting-services/branding-the-web-portal.md)
  
## <a name="ssrs-mobile-reports-in-the-power-bi-mobile-apps"></a>Power BI モバイル アプリでの SSRS モバイル レポート

-  iOS および Android 用の Power BI モバイル アプリで [Reporting Services のモバイル レポートと KPI](https://powerbi.microsoft.com/documentation/powerbi-mobile-iphone-kpis-mobile-reports) を表示する
-  Windows 10 デバイス用の Power BI アプリで [Reporting Services のモバイル レポートと KPI](https://powerbi.microsoft.com/documentation/powerbi-mobile-win10-kpis-mobile-reports/) を表示する   

## <a name="see-also"></a>参照  
  
-   [共有データ ソースを作成、変更、および削除する (SSRS)](../../reporting-services/report-data/create-modify-and-delete-shared-data-sources-ssrs.md)  
-   [共有データセットを管理する](../../reporting-services/report-data/manage-shared-datasets.md)  
-  [Reporting Services で KPI を使用する](../../reporting-services/working-with-kpis-in-reporting-services.md)  
- [Power BI モバイル アクセス用のレポート サーバーを有効にする](../../reporting-services/report-server/enable-a-report-server-for-power-bi-mobile-access.md)  

  
  

