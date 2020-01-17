---
title: セカンダリ軸へのデータのプロット (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 094f39bf-3634-4852-9fc3-3adec4b266e5
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: a9bff6ec41cc2437c6083e150eb391470cb5a5ab
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66105428"
---
# <a name="plot-data-on-a-secondary-axis-report-builder-and-ssrs"></a>セカンダリ軸へのデータのプロット (レポート ビルダーおよび SSRS)
  グラフには、プライマリ軸とセカンダリ軸という 2 種類の軸があります。 セカンダリ軸は、2 つの値セットを、共通のカテゴリを共有する 2 つの異なるデータ範囲と比較する場合に便利です。  
  
 たとえば、2008 年の収益と税を計算するグラフがあるとします。 この場合、2008 年という期間は両方の値セットに共通しています。 ただし、両方の系列が同じ Y 軸にプロットされると、Y 軸のスケールはデータセット内の最大の値に対して最適化されるため、有効な比較を行うことができません。 収益をプライマリ軸に示し、税をセカンダリ軸に示すと、各系列は、独自の Y 軸に独自の値のスケールを使用して表示されます。 これらの系列では、引き続き共通の X 軸が使用されます。  
  
 比較する系列が 3 つ以上ある場合は、グラフ内で複数の系列を比較して表示する際に別の方法を検討します。 詳細については、「[グラフ上の複数の系列 (レポート ビルダーおよび SSRS)](multiple-series-on-a-chart-report-builder-and-ssrs.md)」を参照してください。  
  
 このグラフについては、サンプル レポートに例が含まれています。 このサンプル レポートおよびその他のサンプル レポートをダウンロードする方法の詳細については、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][のレポート ビルダーおよびレポート デザイナーのサンプル レポートに関するページ](https://go.microsoft.com/fwlink/?LinkId=198283)を参照してください。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-plot-a-series-on-the-secondary-axis"></a>セカンダリ軸に系列をプロットするには  
  
1.  グラフ内の系列を右クリックするか、セカンダリ軸に表示する **[値]** 領域内のフィールドを右クリックして、 **[系列のプロパティ]** をクリックします。 **[系列のプロパティ]** ダイアログ ボックスが表示されます。  
  
2.  **[軸とグラフ領域]** をクリックし、値軸とカテゴリ軸のうち、有効にするセカンダリ軸を選択します。  
  
## <a name="see-also"></a>参照  
 [グラフの軸ラベルの書式設定 (レポート ビルダーおよび SSRS)](formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)   
 [軸の間隔の指定 (レポート ビルダーおよび SSRS)](specify-an-axis-interval-report-builder-and-ssrs.md)  
  
  
