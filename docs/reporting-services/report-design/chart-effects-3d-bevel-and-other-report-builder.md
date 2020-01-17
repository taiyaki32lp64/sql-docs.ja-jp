---
title: グラフに対する 3D、傾斜、およびその他の効果 (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
f1_keywords:
- "10156"
ms.assetid: 18ef2119-2931-43ae-9078-f39b460462dd
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 3d6f854eff07947e16a929acec1c20011dcf0b4b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65581697"
---
# <a name="chart-effects---3d-bevel-and-other-report-builder"></a>グラフの効果 - 3D、ベベルなど (レポート ビルダー)
  3 次元 (3D) 効果を使用すると、グラフに奥行を与え、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の改ページ調整されたグラフの視覚的な効果を高めることができます。 たとえば、分割円グラフの特定のスライスを強調する場合は、そのスライスが最初に目に留まるように、グラフのパースペクティブを回転および変更することができます。 グラフに 3D 効果を適用すると、グラデーションの色および陰影のスタイルはすべて無効になります。  
  
 3 次元効果は個々のグラフに適用することができます。また、2 次元グラフと 3 次元グラフの両方を同じレポートに表示することもできます。  
  
 すべての種類のグラフでは、 **[グラフ領域のプロパティ]** ダイアログ ボックスで **[3D の有効化]** チェック ボックスをオンにすることにより、グラフ領域に 3 次元効果を適用できます。 詳細については、「 [グラフへの 3D 効果の追加 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/chart-effects-add-3d-effects-report-builder.md)チェック ボックスをオンにすることにより、グラフ領域に 3 次元効果を適用できます。  
  
 グラフの視覚的な効果を高めるには、傾斜、エンボス、およびテクスチャのスタイルを横棒グラフ、縦棒グラフ、円グラフ、およびドーナツ グラフに追加する方法もあります。 詳細については、「[グラフへの傾斜、エンボス、およびテクスチャのスタイルの追加 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/chart-effects-add-bevel-emboss-or-texture-report-builder.md)」を参照してください。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="coordinate-based-three-dimensional-charts"></a>座標ベースの 3 次元グラフ  
 座標ベースのグラフ (縦棒グラフ、横棒グラフ、面グラフ、散布図、折れ線グラフ、範囲グラフ) を使用している場合、3 次元効果を適用すると、"z 軸" と呼ばれる 3 つ目の軸がグラフに表示されます。 この 3 つ目の軸の導入により、さまざまな視覚的な機能強化をグラフに適用することが可能になります。  
  
### <a name="changing-the-white-space-in-a-3d-chart"></a>3D グラフ内の空白の変更  
 3 次元モードでグラフ領域を表示すると、各系列は、グラフの z 軸に沿って個別の行に表示されます。 各系列の間の間隔を変更するには、[3D 効果] ダイアログ ボックスの **[ポイントのギャップの深さ]** プロパティを変更することにより、グラフのポイントのギャップの深さを変更します。  
  
### <a name="changing-the-projection-of-a-3d-chart"></a>3D グラフの投影の変更  
 3D 投影には、斜投影と透視投影の 2 種類があります。 グラフに斜投影を適用すると、2 次元グラフに奥行が加わります。 z 軸は横軸と縦軸から等しい角度で描画されます。横軸と縦軸は、2 次元グラフと同様、直角に交わっています。  
  
 透視投影を適用すると、ビュー平面が推定され、その地点を視点としてグラフが再描画されて、グラフが変換されます。 **[回転]** ボックスの値を使用すると、視点を "地面の高さ" (0) から頭上 (90) まで垂直方向に移動できます。 **[傾斜]** ボックスの値を使用すると、表示角度を左または右へ移動できます。 値が 0 の場合は、グラフの 2 次元表示と同じです。 **[奥行]** ボックスの値では、投影を表示する際に使用されるゆがみの比率を定義します。 この種類の投影では、グラフの比率は維持されますが、グラフはゆがんで見えるため、奥行の度合いを低くして使用する方が効果的です。  
  
> [!NOTE]  
>  斜投影と透視投影は異なる種類の投影なので、同じグラフで併用することはできません。  
  
### <a name="clustering-data"></a>データのクラスター化  
 2D グラフでは、複数の系列のデータが並んで表示されます。 クラスター化を行うと、各系列が 3D グラフの個別の行に表示されます。 たとえば、3 つの系列のデータ ポイントを含むグラフがある場合、クラスター化により、3 つの系列それぞれが z 軸に沿って個別の行に表示されます。 既定では、3D で表示されるグラフの種類はすべてクラスター化されます。  
  
 横棒グラフと縦棒グラフでは、クラスター化を無効にできます。 クラスター化を無効にすると、横棒グラフおよび縦棒グラフの複数の系列が 1 行に並んで表示されます。  
  
## <a name="shape-based-three-dimensional-charts"></a>図形ベースの 3 次元グラフ  
 図形ベースのグラフ (円グラフ、ドーナツ グラフ、じょうごグラフ、ピラミッド グラフ) で使用できる 3 次元効果は、座標ベースのグラフよりも少なくなります。 図形ベースのグラフを使用している場合、変更できるのは回転と傾斜の値のみです。  
  
## <a name="rotations"></a>回転  
 グラフは、-90 ～ 90°の範囲で水平方向と垂直方向に回転できます。 水平方向の角度に正の値を指定すると、グラフは x 軸を中心に反時計回りに回転します。一方、垂直方向の角度に正の値を指定すると、グラフは y 軸を中心に時計回りに回転します。  
  
## <a name="highlighting-3d-effects"></a>3D 効果の強調表示  
 強調表示のスタイルは、 **Shading** プロパティを使用して 3D グラフに追加することができます。このプロパティは、グラフ領域を選択すると、プロパティ ペインの [Area3DStyle] の下に表示されます。 単純な光源のスタイルでは、グラフ領域の要素に同じ色合いが適用されます。 写実的なスタイルでは、指定された光源の角度に応じて、グラフ領域の要素の色合いが変わります。  
  
## <a name="see-also"></a>参照  
 [グラフの軸ラベルの書式設定 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)   
 [グラフの書式設定 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md)   
 [グラフへの 3D 効果の追加 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/chart-effects-add-3d-effects-report-builder.md)  
  
  
