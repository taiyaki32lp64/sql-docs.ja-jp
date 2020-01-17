---
title: モバイル レポートにゲージを追加する | Reporting Services | Microsoft Docs
ms.date: 03/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: mobile-reports
ms.topic: conceptual
ms.assetid: 76d8fc8f-c37f-44d3-ab44-45fbeed4e064
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 90440119ec21cbfe97096b439e61074c7e515e00
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63280565"
---
# <a name="add-gauges-to-mobile-reports--reporting-services"></a>モバイル レポートにゲージを追加する | Reporting Services
ゲージは、モバイル レポートで広く使用されている最も基本的なビジュアルです。 データセットに含まれる 1 つの値 (値自体か、目標値と比較した値) を表示します。

![PBI_SSMRP_Gauges](../../reporting-services/mobile-reports/media/pbi-ssmrp-gauges.png)  
  
*[レイアウト] タブに表示されたゲージの視覚エフェクト*  
  
SQL Server Mobile Report Publisher のすべてのゲージに少なくとも 1 つの共通プロパティ (主要な値) があります。このプロパティは、モバイル レポート内のいずれかのデータ テーブルに含まれる 1 つの数値フィールドに設定されています。  

[数値] ゲージを除くすべてのゲージには、比較対象値、または主要な値と比較対象値の間の関係を示す *差分*値を表示することもできます。 多くの場合、比較対象値は目標値となっており、ゲージは、目標の達成状況や、実際の値と目標値の間の差分を視覚的に示します。

ゲージは、その主要な値と比較対象値について、それぞれ 1 つの集計値のみを表示できます。 ゲージでは標準的な集計 (合計、平均、最小、最大など) を使用できます。 既定では、ゲージの値は合計に設定されており、ゲージ コントロールで利用できる現在のフィルター済みデータに含まれるすべての値の合計が表示されます。 

ゲージの値は、モバイル レポート上のナビゲーターに接続することでフィルター処理できます。 

## <a name="set-the-main-and-comparison-values-for-a-gauge"></a>ゲージの主要な値と比較対象値を設定する

1. ゲージを **[レイアウト]** タブからデザイン グリッドにドラッグし、目的のサイズに調整します。

2. [Excel または共有データセットのデータ](../../reporting-services/mobile-reports/data-for-reporting-services-mobile-reports.md)を取得します。

3. **[データ]** タブを選択し、 **[データのプロパティ]** ペインの **[主要な値]** で、データ テーブルと数値フィールドを選択します。

3. [数値] ゲージ以外のゲージの場合、 **[データのプロパティ]** ペインの **[比較対象値]** で、データ テーブルと数値フィールドを選択します。

4. (省略可能) 集計を変更するには、 **[オプション]** をクリックして別の集計を選択します。
   
   >**注**: 主要な値の集計を変更すると、多くの場合、比較対象値の集計も変更する必要があります。ただし、場合によっては異なる集計方法を組み合わせることもできます。  

## <a name="filter-a-gauge"></a>ゲージにフィルターを適用する
  
モバイル レポートにナビゲーターがある場合は、ゲージを 1 つ以上のナビゲーターにバインドしてフィルターを適用することができます。 ゲージの値と比較対象値は、1 つ以上の異なるナビゲーターにバインドできるため、ゲージのオプションをほとんど無制限に指定することができます。  

1. ゲージを選択し、 **[データ]** タブの **[データのプロパティ]** ペインで、 **[主要な値]** または **[比較対象値]** の隣にある **[オプション]** をクリックします。

2. [次に基づいてフィルター] の下で、ゲージをフィルターするナビゲーターを選択します。

   ![モバイル レポートのゲージのナビゲーター](../../reporting-services/mobile-reports/media/mobile-report-gauge-navigator.png)
 
## <a name="set-visual-properties-for-a-gauge"></a>ゲージのビジュアルのプロパティを設定する
  
ゲージの要素をデータ フィールドに結び付けるデータのプロパティのほかにも、数多くの機能に関するプロパティやビジュアルのプロパティをカスタマイズできます。 

### <a name="set-value-direction-high-or-low-is-better"></a>値の方向を設定する: [大きい値が適当] または [低い値が適当]
* ゲージを選択し、 **[レイアウト]** タブの **[ビジュアルのプロパティ]** ペインで、 **[値の方向]** を **[大きい値が適当]** または **[低い値が適当]** に設定します。 

**[大きい値が適当]** を選択すると、正の数は緑色で表示され、望ましい良い変化であることを示し、低下した値は赤色で表示され、望ましくない悪い変化であることを示します。 

**[低い値が適当]** を選択すると、色の設定が反対になります。

[値の方向] プロパティは、比較対象値をサポートするゲージ要素にのみ関連付けられています。 ゲージの色は、差分を表す整数の符号と [値の方向] プロパティの設定によって決まります。  
  
### <a name="set-range-stops-for-a-gauge"></a>ゲージの範囲停止を設定する
ゲージ固有の 2 つ目の非データ プロパティは、範囲停止です。 

* ゲージを選択し、 **[レイアウト]** タブの **[ビジュアルのプロパティ]** ペインで、 **[範囲停止]** を選択します。

範囲停止では、比較対象値がどの程度の割合に達すると、視覚エフェクトが目標内 (緑)、中間 (黄)、目標外 (赤) として表されるかを設定します (ゲージの比較対象値を目標とした場合)。 範囲停止がサポートされるのは、比較対象値を持つゲージのみです。  

### <a name="format-the-numbers-in-the-gauge"></a>ゲージの数値書式を設定する  
他の多くの要素と共有される、ゲージ要素のもう 1 つの非データ プロパティは、数値形式です。 

* ゲージを選択し、 **[レイアウト]** タブの **[ビジュアルのプロパティ]** ペインで、 **[範囲停止]** を選択します。

ここでは、[通貨]、[パーセント]、[時間]、または [一般] など、ゲージに表示される数値の書式を設定します。 モバイル レポートの各要素に対して数値書式を設定します。
  
### <a name="see-also"></a>参照 

* [SQL Server Mobile Report Publisher を使用してモバイル レポートを作成する](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)
* [Maps in SQL Server mobile reports](../../reporting-services/mobile-reports/maps-in-reporting-services-mobile-reports.md)
* [Reporting Services モバイル レポートのナビゲーター](../../reporting-services/mobile-reports/add-navigators-to-reporting-services-mobile-reports.md)
* [Reporting Services モバイル レポートの視覚エフェクト](../../reporting-services/mobile-reports/add-visualizations-to-reporting-services-mobile-reports.md)
* [Reporting Services モバイル レポートのデータ グリッド](../../reporting-services/mobile-reports/add-data-grids-to-mobile-reports-reporting-services.md) 
