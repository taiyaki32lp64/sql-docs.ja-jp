---
title: グラフへのスケール区切りの追加 (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 84d66436-ed62-4967-bbbd-b457593ee787
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d91c65e49d7afda378fb66d5ce65604b7f9b752e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66106532"
---
# <a name="add-scale-breaks-to-a-chart-report-builder-and-ssrs"></a>グラフへのスケール区切りの追加 (レポート ビルダーおよび SSRS)
  スケール区切りは、グラフのプロット エリアに描画される線であり、値軸 (通常は縦軸、つまり Y 軸) 上の最高値と最低値の間の区切りを示します。 スケール区切りを使用すると、同じグラフ領域内で 2 つの異なる範囲を表示できます。  
  
 ![スケール区切り付きのグラフ](../media/rs-multipledatarangeschart-scalebreak.gif "スケール区切り付きのグラフ")  
  
> [!NOTE]  
>  グラフ上でスケール区切りを配置する場所を指定することはできません。 グラフでは、データセット内の値に基づいた独自の計算で、実行時に値軸 (Y 軸) 上にスケール区切りを描画するためにデータ範囲の間が十分に離れているかどうかが判断されます。  
  
 スケール区切り付きのグラフについては、サンプル レポートに例が含まれています。 このサンプル レポートおよびその他のサンプル レポートをダウンロードする方法の詳細については、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][レポート ビルダーおよびレポート デザイナーのサンプル レポート](https://go.microsoft.com/fwlink/?LinkId=198283)に関するページを参照してください。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-enable-scale-breaks-on-the-chart"></a>グラフ上のスケール区切りを有効にするには  
  
1.  縦軸を右クリックし、 **[軸のプロパティ]** をクリックします。 **[縦軸のプロパティ]** ダイアログ ボックスが表示されます。  
  
2.  **[スケールの区切り線を有効にする]** チェック ボックスをオンにします。  
  
### <a name="to-change-the-style-of-the-scale-break"></a>スケール区切りのスタイルを変更するには  
  
1.  プロパティ ペインを開きます。  
  
2.  デザイン画面で、グラフの Y 軸を右クリックします。 Y 軸オブジェクト (既定の名前は "グラフ軸") のプロパティが [プロパティ] ペインに表示されます。  
  
3.  **[スケール]** セクションで、ScaleBreakStyle プロパティを展開します。  
  
4.  BreakLineType や Spacing など、ScaleBreakStyle のプロパティの値を変更します。 スケール区切りプロパティの詳細については、「[グラフ上で複数のデータ範囲を持つ系列の表示 &#40;レポート ビルダーおよび SSRS&#41;](displaying-a-series-with-multiple-data-ranges-on-a-chart.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [グラフ &#40;レポート ビルダーおよび SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [グラフの書式設定 (レポート ビルダーおよび SSRS)](formatting-a-chart-report-builder-and-ssrs.md)   
 [[軸のオプション] ([軸のプロパティ] ダイアログ ボックス) &#40;レポート ビルダーおよび SSRS&#41;](../axis-properties-dialog-box-axis-options-report-builder-and-ssrs.md)  
  
  
