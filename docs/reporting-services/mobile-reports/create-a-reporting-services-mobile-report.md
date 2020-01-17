---
title: Reporting Services モバイル レポートの作成 | Microsoft Docs
ms.date: 03/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: mobile-reports
ms.topic: conceptual
ms.assetid: e84dc855-aede-4fb4-b721-e6d8787961f4
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: b3fd0fc3530ec35da61e2314ef7a80a58d9bdd7d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63316455"
---
# <a name="create-a-reporting-services-mobile-report"></a>Reporting Services モバイル レポートの作成
SQL Server Mobile Report Publisher を使用すると、調整可能なグリッド行とグリッド列、および柔軟なモバイル レポート要素を備えたデザイン画面で、任意の画面サイズに対応する SQL Server Reporting Services モバイル レポートをすばやく作成できます。  
  
初めてモバイル レポートを作成するときは、Reporting Services Web ポータルから SQL Server Mobile Report Publisher をローカル コンピューターにインストールできます。 または、 [Microsoft ダウンロード センター](https://go.microsoft.com/fwlink/?LinkID=733527)からインストールすることもできます。 2 回目以降は、Web ポータルまたはローカルのいずれかから開始できます。   
    
1. Reporting Services Web ポータルの上部のバーで、 **[新規]**  >  **[モバイル レポート]** の順に選択します。  
  
   ![PBI_SSMRP_NewMenu](../../reporting-services/mobile-reports/media/pbi-ssmrp-newmenu.png)  
     
2. Mobile Report Publisher の **[レイアウト]** タブで、ナビゲーター、ゲージ、グラフ、マップ、またはデータグリッドを選択して、デザイン グリッドにドラッグします。  
  
3. 要素の右下隅をクリックし、希望のサイズにドラッグします。  
  
   ![SSMRP_ResizeChart](../../reporting-services/mobile-reports/media/ssmrp-resizechart.png)  
  
   これが、レポートに含める要素を作成する **マスター** デザイン グリッドです。 後で、 [タブレットまたはスマートフォン用にレポートをレイアウト](../../reporting-services/mobile-reports/lay-out-a-reporting-services-mobile-report-for-phone-or-tablet.md)できます。     
     
   デザイン グリッドの下の **[ビジュアル プロパティ]** にさまざまなプロパティを設定することに注意してください。  
     
4. 左上隅の **[データ]** タブを選択すると、既にグラフにシミュレーションされたデータが関連付けられていることを確認できます。   
  
   ![SSMRP_SimTable](../../reporting-services/mobile-reports/media/ssmrp-simtable.png)  
  
5. 右上隅の **[データの追加]** を選択します。  
  
6. **[ローカル Excel]** または **[レポート サーバー]** を選択します。  
  
   >**ヒント**: Excel からデータを追加する場合、次を確認します。  
    >* モバイル レポートで作業できるよう、 [Excel データを準備します](../../reporting-services/mobile-reports/prepare-excel-data-for-reporting-services-mobile-reports.md) 。  
    >* まずファイルを閉じます。  
7. 目的のワークシートを選択し、 **[インポート]** を選択します。   
   ブックから一度に 1 つ以上のワークシートを追加できます。  
    
     ![SSMRP_AddExcelData](../../reporting-services/mobile-reports/media/ssmrp-addexceldata.png)  
  
8. 引き続き、 **[データ]** タブの **[データ プロパティ]** ボックスで、グラフに必要なテーブルとフィールドを選択します。  
  
   ![SSMRP_DataProps](../../reporting-services/mobile-reports/media/ssmrp-dataprops.png)  
  
9. **[レイアウト]** タブに戻り、 **[表示プロパティ]** ボックスで、 **[タイトル]** 、 **[時間の単位]** 、 **[数値書式]** などのプロパティを設定します。  
  
   ![SSMRP_ChartVizProps](../../reporting-services/mobile-reports/media/ssmrp-chartvizprops.png)  
    
10. 左上の **[プレビュー]** を選択し、レポートがどのように整形されたか確認します。  
  
11. 次にレポートを保存します。 左上隅の [保存] アイコンを選択して、 **[ローカルに保存]** または **[サーバーに保存]** を選択します。  
  
   サーバーに保存するには、SQL Server Reporting Services レポート サーバーにアクセスできる必要があります。  
     
   ### <a name="see-also"></a>参照  
     
-   [Create and publish mobile reports with SQL Server Mobile Report Publisher (SQL Server Mobile Report Publisher でモバイル レポートを作成し発行する)](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)  
-   [スマートフォンやタブレット向けに Reporting Services モバイル レポートをレイアウトする](../../reporting-services/mobile-reports/lay-out-a-reporting-services-mobile-report-for-phone-or-tablet.md)  
  
   
