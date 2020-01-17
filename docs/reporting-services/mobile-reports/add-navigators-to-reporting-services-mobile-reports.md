---
title: Reporting Services モバイル レポートへのナビゲーターの追加 | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: mobile-reports
ms.topic: conceptual
ms.assetid: e141f50e-49a9-46c6-983c-f656013aa07c
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 27060715a2d616dd99e294175163ad74b54a17b9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63317041"
---
# <a name="add-navigators-to-reporting-services-mobile-reports"></a>Add navigators to Reporting Services mobile reports
[!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-long.md)]では、時間または選択したものによって視覚エフェクトのデータをフィルター処理するには、 *ナビゲーター* を追加します。 

ナビゲーターは、Power BI や Excel のピボットテーブルのスライサーに似ていますが、ナビゲーター固有の特徴もいくつかあります。

**時間ベースのナビゲーター** は、特定の時間範囲内の行を選択して、テーブルをフィルター処理します。 

**選択ベースのナビゲーター** は、選択したキー値に一致する特定の列値、または階層ツリーの場合は選択したキー値のサブツリーに属する特定の列値の行を選択することにより、テーブルをフィルター処理します。 選択ナビゲーターには 2 種類あります。
* 選択リストは、モバイル レポートのフィルター処理に使用できる単一列のテーブルであり、Power BI や Excel のスライサーに似ています。
* スコアカード グリッドもモバイル レポートをフィルター処理し、モバイル レポートを含むこともできます。 
  
## <a name="time-navigators"></a>時間ナビゲーター   
  
その名前からもわかるように、時間ナビゲーターはデータの範囲を時間範囲によって選択します。   
  
![SSMRP_TimeNav](../../reporting-services/mobile-reports/media/ssmrp-timenav.png)  
*左側の 4 つの折れ線グラフは、[時間範囲の事前設定] で設定されています。右側の折れ線グラフはフィルターです。*  
  
[プレビュー] または [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] Web ポータルでレポートを表示するときは、時間ナビゲーターで矢印をドラッグして、レポートの残りの部分をフィルター処理します。  
  
![SSMRP_TimeNavPreview](../../reporting-services/mobile-reports/media/ssmrp-timenavpreview.png)  
  
既定では、時間ナビゲーターは時間ベースのデータに接続されているレポート内のすべてのビジュアルをフィルター処理します。 テーブルに 1 つ以上の時刻ベースの列が含まれている場合、フィルター処理には最初のもののみが使用されます。 系列テーブルが、埋め込みの視覚エフェクトを駆動し、モバイル レポートの全体的な日付範囲を決定します。  
  
時間ナビゲーターから視覚エフェクトを切断できます。   
1. 視覚エフェクトを選択し、 **[データ]** タブを選択します。  
2. **[データのプロパティ]** で、 **[オプション]** を選択します。  
3. **[次に基づいてフィルター]** チェック ボックスをオフにします。  
  
   ![SSMRP_ClearTimeFilter](../../reporting-services/mobile-reports/media/ssmrp-cleartimefilter.png)  
  
## <a name="selection-lists"></a>選択リスト   
  
選択リストは、ユーザーがリストで選択した値と、フィルター対象のテーブルの各行に指定されている列の値と照合することで、モバイル レポート内のデータをフィルター処理します。 

1. **[レイアウト]** タブから **[選択リスト]** をデザイン画面にドラッグして、サイズを適切に変更します。

2. **[データ]** タブを選択し、 **[データのプロパティ]** ペインの **[キー]** で、フィルターするテーブルと列を選択します。 

3. **[ラベル]** で、表示されるラベルの付いた列を選択します。 キー列とラベル列は同じにすることができます。  
  
   階層ツリー データの場合は、親のキー列を選択します。  
  
4. データのプロパティを設定した後、 **[Tables FIltered by Selection List (選択リストでフィルター処理されるテーブル)]** で、フィルター対象のテーブルとフィルターに使用する列を選択します。 この列が、選択リストのキー列の値と一致する必要があります。 

選択リストでフィルター処理するモバイル レポートの各視覚エフェクトについて次のようにします。

1. 視覚エフェクトを選択し、 **[データ]** タブを選択して、 **[データのプロパティ]** ペインでフィールド名の隣の **[オプション]** を選択します。

   ![mobile-report-set-selection-list](../../reporting-services/mobile-reports/media/mobile-report-set-selection-list.png)

2. **[次に基づいてフィルター]** で、選択リストを選択します。

[プレビュー] または [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] Web ポータルでモバイル レポートを表示し、選択リストの値を選択すると、モバイル レポート内の他の視覚エフェクトがフィルター処理されます。

![mobile-report-selection-list-filtering](../../reporting-services/mobile-reports/media/mobile-report-selection-list-filtering.png) 
     
## <a name="scorecard-grid"></a>スコアカード グリッド  
  
スコアカード グリッドのフィルターは選択リストのフィルターと同じように機能しますが、値列とスコア インジケーターも表示されます。これらは、インジケーター データ グリッド内のインジケーターと同じです。 スコアカードにデータを提供するには、キー、ラベル、および省略可能な親キー列を選択後、入力テーブルと列を選択します。 スコアカードのデータ列は、キー列を使用してフィルター処理できる必要があります。  

1. **[レイアウト]** タブから **[スコアカード グリッド]** をデザイン画面にドラッグして、サイズを適切に変更します。

2. **[データ]** タブを選択し、 **[データのプロパティ]** ペインの **[キー]** で、フィルターするテーブルと列を選択します。 

3. **[ラベル]** で、表示されるラベルの付いた列を選択します。 キー列とラベル列は同じにすることができます。  
  
4. スコア インジケーターを追加するには、 **[データ列]** ペインで **[スコアの追加]** を選択します。   
  
5. スコア インジケーターの名前を指定し、 **[オプション]** を選択して、データ グリッドでインジケーターに対して設定したものと同じプロパティを設定します。  
  
   * ゲージの種類
   * [値] フィールド
   * 比較フィールド
   * 値の方向
  
6. 値インジケーターを追加するには、 **[データ列]** ペインで **[値の追加]** を選択します。

7. 希望の値インジケーター名を指定し、テーブルからそのソース列を選択して、それをどのように書式設定するか選択します。  

   ![mobile-report-scorecard-grid-data-properties](../../reporting-services/mobile-reports/media/mobile-report-scorecard-grid-data-properties.png)

8. データのプロパティを設定した後、 **[Tables FIltered by Selection List (選択リストでフィルター処理されるテーブル)]** で、フィルター対象のテーブルとフィルターに使用する列を選択します。 この列が、選択リストのキー列の値と一致する必要があります。 

[プレビュー] または [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] Web ポータルでモバイル レポートを表示し、スコアカード グリッドの値を選択すると、モバイル レポート内の他の視覚エフェクトがフィルター処理されます。

![mobile-report-scorecard-grid](../../reporting-services/mobile-reports/media/mobile-report-scorecard-grid.png)
    
## <a name="set-which-visualizations-are-filtered"></a>フィルター対象の視覚エフェクトを設定する  
  
ギャラリー要素では、データ ビューで特定の入力用のオプション ボタンをクリックしてフィルターを使用するよう構成します。 フィルターは、適切なチェック ボックスに切り替えることにより有効になります。  

ナビゲーターがフィルター処理するモバイル レポート内の視覚エフェクトを選択できます。

1. 視覚エフェクトを選択し、 **[データ]** タブを選択して、 **[データのプロパティ]** ペインでフィールド名の隣の **[オプション]** を選択します。

   ![mobile-report-set-selection-list](../../reporting-services/mobile-reports/media/mobile-report-set-selection-list.png)

2. **[次に基づいてフィルター]** で、ナビゲーターを選択します。 各視覚エフェクトは、複数のナビゲーターでフィルター処理できます。
  
## <a name="cascading-filters"></a>フィルターのカスケード   
  
フィルターも一緒にカスケードできるので、ある選択値で 2 番目の利用可能な値をフィルター処理できます。 フィルターをカスケードするには、通常のギャラリー要素の場合と同様にキー列にフィルターを適用します。  

### <a name="see-also"></a>参照 
  
* [Maps in SQL Server mobile reports](../../reporting-services/mobile-reports/maps-in-reporting-services-mobile-reports.md)
* [Reporting Services モバイル レポートの視覚エフェクト](../../reporting-services/mobile-reports/add-visualizations-to-reporting-services-mobile-reports.md)
* [Reporting Services モバイル レポートのゲージ](../../reporting-services/mobile-reports/add-gauges-to-mobile-reports-reporting-services.md)
* [Reporting Services モバイル レポートのデータ グリッド](../../reporting-services/mobile-reports/add-data-grids-to-mobile-reports-reporting-services.md)  
