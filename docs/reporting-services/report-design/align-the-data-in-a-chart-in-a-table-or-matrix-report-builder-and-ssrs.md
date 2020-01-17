---
title: テーブル内のグラフまたはマトリックスでのデータの整列 (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.date: 03/03/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 75137575-d1bf-46d6-8527-5afc85eea5e1
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: d639e686251effc19e445a39c97860a3336c8ff2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65581872"
---
# <a name="align-the-data-in-a-chart-in-a-table-or-matrix-report-builder-and-ssrs"></a>テーブル内のグラフまたはマトリックスでのデータの整列 (レポート ビルダーおよび SSRS)
  スパークラインとデータ バーは小さく単純なグラフであり、余分な情報を最小限に抑えて多くの情報を伝えます。 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] の改ページ調整されたレポートでは、このオプションをオンにすると、基礎となるデータに欠落した値がある場合でも、スパークラインおよびデータ バーの値がテーブルまたはマトリックスのさまざまなセルに整列します。  
  
 ![rs_SparklineAlignData](../../reporting-services/report-design/media/rs-sparklinealigndata.gif "rs_SparklineAlignData")  
  
 次の画像には、各従業員の毎日の売り上げが縦棒グラフで示されています。 売り上げのない日にはグラフが空白になり、後続の日が横に整列していることに注意してください。 また、異なるグラフのサイズを互いに相対させてグラフを縦にも並べています。 詳細については、「 [スパークラインとデータ バー (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/sparklines-and-data-bars-report-builder-and-ssrs.md)」を参照してください。  
  
## <a name="align-the-data-in-a-sparkline-or-data-bar"></a>スパークラインまたはデータ バー内のデータの整列  
  
1.  テーブルまたはマトリックスに[スパークラインまたはデータ バーを追加します](../../reporting-services/report-design/add-sparklines-and-data-bars-report-builder-and-ssrs.md) 。  
  
2. スパークラインまたはデータ バーをクリックし、 **[水平軸のプロパティ]** または **[垂直軸のプロパティ]** をクリックします。  
  
2.  **[軸のオプション]** タブで **[軸を整列する]** ボックスをオンにし、ドロップダウン ボックスで軸を整列するグループを選択します。  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>参照  
 [グラフ &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
 [スパークラインとデータ バーの追加 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/add-sparklines-and-data-bars-report-builder-and-ssrs.md)  
  
  
