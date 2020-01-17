---
title: 軸のプロパティ] ダイアログ ボックス、[軸のオプション (レポート ビルダーおよび SSRS) |Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.axisproperties.axisoptions.f1
- "10138"
ms.assetid: b276e210-7a12-48ae-971b-7dabae51df11
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ff9f3281e47cf6dfdf8a189c653d0e061f4a761d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66109958"
---
# <a name="axis-properties-dialog-box-axis-options-report-builder-and-ssrs"></a>[軸のオプション] ([軸のプロパティ] ダイアログ ボックス) (レポート ビルダーおよび SSRS)
  選択**軸のオプション**で、**水平**または **[縦軸のプロパティ**] ダイアログ ボックスで、グラフの指定された軸の外観を定義します。 以前のバージョンの [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]では、既定でグラフの X 軸上にすべてのラベルが表示されていました。 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 2008 では、グラフ内の画像を見やすくし、ラベルの重なりを回避するために、ラベルは省略されます。 詳細については、「[グラフの軸ラベルの書式設定 &#40;レポート ビルダーおよび SSRS&#41;](report-design/formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)」を参照してください。  
  
## <a name="options"></a>および  
 **スケール区切りを有効にします。**  
 必要に応じてグラフでスケールの区切り線を描画できるようにする場合にオンにします。 このチェック ボックスがオンの場合、データセット内の高い点と低い点の差異がスケールの区切り線を描画するのに十分であるかどうかが自動的に判断されます。  
  
 **方向を反転します。**  
 グラフの方向を反転させる場合にオンにします。 たとえば、既定の縦棒グラフでは、グラフの左側に Y 軸が表示され、左から右にカテゴリが表示されます。 このチェック ボックスをオンにすると、グラフの右側に Y 軸が表示され、右から左にカテゴリが表示されます。  
  
 **インター レース色を使用します。**  
 グラフにストリップ ラインを追加した後、色を選択したり式を入力したりするには、このオプションを選択します。 ストリップ ラインはグラフ領域上の影付きの帯であり、グリッド線の間で明るい領域と暗い領域を交互に適用する効果を与えることができます。 これらのストリップ ラインは、軸上でのパターンの繰り返しを強調表示する場合に役立ちます。  
  
 **常に 0 を含める**  
 軸のスケールで常に 0 を含める場合にオンにします。 このオプションが有効でない場合、グラフの軸には値 0 というラベルが付きません。 データセットに負の値や 0 が含まれている場合は、0 を含めると役立ちます。  
  
 **スカラー軸**  
 一連の軸の値を連続して表示する場合にオンにします。 たとえば、データセットに 1 月、3 月、および 11 月のデータが含まれている場合は、非スカラー軸にはこれらの月だけが表示されますが、スカラー軸には 1 年のすべての月が表示されます。  
  
 **対数スケールを使用します。**  
 軸のスケールが対数であることを示す場合にオンにします。 このチェック ボックスを Y 軸で使用できるのは、Y 軸に正の数値が含まれている場合のみです。  
  
 ボックスには、対数スケールを使用するように軸が設定されている場合に使用する対数の底を入力します。 既定では、軸の対数スケールに使用される底は 10 です。 このオプションを Y 軸で使用できるのは、Y 軸が数値を表している場合のみです。  
  
 **最小**  
 X 軸の最小値を示す式または値を入力します。 省略した場合、最小値はデータセットから返されるデータによって決まります。  
  
 **[最大]**  
 X 軸の最大値を示す式または値を入力します。 省略した場合、最大値はデータセットから返されるデータによって決まります。  
  
 **間隔**  
 軸ラベルの間の間隔を示す式または値を入力します。 たとえば、軸上に各カテゴリ ラベルを表示するには、「1」と入力します。 カテゴリ ラベルを 1 つおきに表示するには、「2」と入力します。 省略した場合、ラベルは、データセットの値に基づいて自動的に計算されます。  
  
 **間隔の種類**  
 指定した間隔の種類を表す式または値を入力します。 たとえば、間隔を 2 日間にする場合は、間隔に「 **2** 」を指定し、間隔の種類に「 **日** 」を指定します。  
  
 **[横余白]**  
 グラフ要素とグラフの横の間にある余白を追加または削除するための式を入力するかまたは値を選択します。 このオプションが **[自動]** に設定されている場合、横の余白が追加されます。  
  
## <a name="see-also"></a>参照  
 [グラフの軸ラベルの書式設定 (レポート ビルダーおよび SSRS)](report-design/formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)   
 [グラフ &#40;レポート ビルダーおよび SSRS&#41;](report-design/charts-report-builder-and-ssrs.md)   
 [グラフの系列の色の書式設定 &#40;レポート ビルダーおよび SSRS&#41;](report-design/formatting-series-colors-on-a-chart-report-builder-and-ssrs.md)   
 [軸の間隔の指定 &#40;レポート ビルダーおよび SSRS&#41;](report-design/specify-an-axis-interval-report-builder-and-ssrs.md)   
 [日付または通貨として軸ラベルを書式設定する &#40;レポート ビルダーおよび SSRS&#41;](report-design/format-axis-labels-as-dates-or-currencies-report-builder-and-ssrs.md)   
 [セカンダリ軸にデータをプロット&#40;レポート ビルダーおよび SSRS&#41;](report-design/plot-data-on-a-secondary-axis-report-builder-and-ssrs.md)   
 [スパークラインとデータ バー (レポート ビルダーおよび SSRS)](report-design/sparklines-and-data-bars-report-builder-and-ssrs.md)   
 [グラフの余白の追加または削除 &#40;レポート ビルダーおよび SSRS&#41;](report-design/add-or-remove-margins-from-a-chart-report-builder-and-ssrs.md)  
  
  
