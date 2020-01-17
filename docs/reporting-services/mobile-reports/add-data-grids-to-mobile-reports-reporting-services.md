---
title: モバイル レポートにデータ グリッドを追加する | Reporting Services | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: mobile-reports
ms.topic: conceptual
ms.assetid: fe98a970-90d3-44d1-9189-9141c237f141
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 2658eb0eec1bd99c4e4503e8d8ae8894638e8c23
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63280461"
---
# <a name="add-data-grids-to-mobile-reports--reporting-services"></a>モバイル レポートにデータ グリッドを追加する | Reporting Services
最善の視覚化がデータ自体である場合があります。 ここでは、 *に使用できる次種類*データ グリッド [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-long.md)]つまりテーブルについて説明します。
* シンプル データ グリッド
* インジケーター データ グリッド
* グラフのデータ グリッド

## <a name="simple-data-grid"></a>シンプル データ グリッド
最も基本的なシンプル データ グリッドでは、カスタム書式設定とヘッダーを使用して、複数のデータ列を表示できます。 

![mobile-report-simple-data-grid](../../reporting-services/mobile-reports/media/mobile-report-simple-data-grid.png)

データ グリッドをデザイン画面に追加した後は、実際のデータに接続できます。

1. シンプル データ グリッドを **[レイアウト]** タブからデザイン グリッドにドラッグし、目的のサイズに調整します。

2. [Excel または共有データセットのデータ](../../reporting-services/mobile-reports/data-for-reporting-services-mobile-reports.md)を取得します。

3. **[データ]** タブを選択し、 **[データのプロパティ]** ペインの **[グリッド ビューのデータ]** で、データ テーブルを選択します。

4. **[列]** ペインで、表示する列を選択します。 順序と名前を変更し、書式と集計を設定します。 

 
##  <a name="indicator-data-grid"></a>インジケーター データ グリッド
インジケーター データ グリッドには、ゲージを含む列を追加できます。

![mobile-report-indicator-data-grid](../../reporting-services/mobile-reports/media/mobile-report-indicator-data-grid.png)

1. インジケーター データ グリッドを **[レイアウト]** タブからデザイン グリッドにドラッグし、目的のサイズに調整します。

2. **[データ]** タブの **[列]** ペインで、 **[ゲージ列の追加]** を選択します。 

3. **[オプション]** を選択し、 **[ゲージの種類]** を選択します。 

4. **[値]** フィールドと **[比較]** フィールドを設定し、 **モバイル レポートに直接追加するゲージ**と同じように [[値の方向]](../../reporting-services/mobile-reports/add-gauges-to-mobile-reports-reporting-services.md)を設定します。

データ グリッドの対応する行に固有のデータのみが、データ グリッドによって自動的にゲージに設定されます。  

## <a name="chart-data-grid"></a>グラフのデータ グリッド
グラフのデータ グリッドにはゲージまたはグラフの列を追加できます。 

![mobile-report-chart-data-grid](../../reporting-services/mobile-reports/media/mobile-report-chart-data-grid.png)

グラフの列をデータ グリッドに追加する場合は、個別のデータ テーブルを追加して、各行のグラフにデータを提供する必要があります。 この 2 つ目のデータ テーブルは、メイン データ テーブルとフィールドを共有して、各行を関連するグラフのデータにリンクする必要があります。 

1. グラフのデータ グリッドを **[レイアウト]** タブからデザイン グリッドにドラッグし、目的のサイズに調整します。

2. **[データ]** タブの **[列]** ペインで、 **[グラフ列の追加]** を選択します。 

3. まだ行っていない場合は、 [Excel または共有データセットからデータ](../../reporting-services/mobile-reports/data-for-reporting-services-mobile-reports.md) を取得し、メイン データ テーブルとフィールドを共有する第 2 のデータ テーブルを追加します。

4. **[データのプロパティ]** の **[グリッド ビューのデータ]** でメイン データ テーブルを選択し、 **[グラフの視覚化の参照データ]** で第 2 のテーブルを選択します。

5. **[オプション]** を選択し、 **[グラフの種類]** を選択します。
 
6. **[Chart data field (グラフのデータ フィールド)]** 、 **[ソースのルックアップ]** 、 **[対象のルックアップ]** を選択します。 
   これらの 3 つのプロパティは、データ グリッドから列内の各グラフへのデータの提供方法を指定します。
   
   *   **[ソースのルックアップ]** には、 **[グリッド ビューのデータ]** で選択したデータ テーブルのフィールドを設定します。 このフィールドは、各行の埋め込みグラフにデータを提供するためにグラフの参照データ テーブルに適用される、行ごとのフィルターとして機能します。 
   * **[対象のルックアップ]** は、 **[グラフの視覚化の参照データ]** で選択したデータ テーブルのフィールドです。 各行のグラフのデータは、これらの 2 つのフィールドで結合されます。   
   * **[Chart data field (グラフのデータ フィールド)]** は、各行のグラフで Y 軸の値または系列として使用される、 **[グラフの視覚化の参照データ]** のデータ テーブル内のメトリックを決定します。  

## <a name="see-also"></a>参照 
* [Maps in SQL Server mobile reports](../../reporting-services/mobile-reports/maps-in-reporting-services-mobile-reports.md)
* [Reporting Services モバイル レポートのナビゲーター](../../reporting-services/mobile-reports/add-navigators-to-reporting-services-mobile-reports.md)
* [Reporting Services モバイル レポートの視覚エフェクト](../../reporting-services/mobile-reports/add-visualizations-to-reporting-services-mobile-reports.md)
* [Reporting Services モバイル レポートのゲージ](../../reporting-services/mobile-reports/add-gauges-to-mobile-reports-reporting-services.md)  
 
  
