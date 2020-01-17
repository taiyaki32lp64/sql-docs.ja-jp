---
title: 線、色、および画像の書式設定 (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
f1_keywords:
- sql13.rtp.rptdesigner.textboxproperties.border.f1
- "10502"
- "10094"
- sql13.rtp.rptdesigner.shared.borderdv.f1
- sql13.rtp.rptdesigner.reportbody.border.f1
- "10063"
- sql13.rtp.rptdesigner.pictureproperties.border.f1
- sql13.rtp.rptdesigner.rectangleproperties.border.f1
- "10055"
- "10126"
- "10066"
- sql13.rtp.rptdesigner.subreportproperties.border.f1
ms.assetid: 0f5f0d2a-9537-4152-b441-b40d7f04cf4c
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 3bc6e9b634ce9872b069381d58ed2dc89a0dc1d4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65576004"
---
# <a name="formatting-lines-colors-and-images-report-builder-and-ssrs"></a>線、色、および画像の書式設定 (レポート ビルダーおよび SSRS)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] には、線、色、データ領域、画像、その他のレポート アイテムの書式を設定する機能が用意されています。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="borders-lines-and-gridlines"></a>罫線、線、グリッド線  
 罫線、線、およびグリッド線を使用すると、ページ上のアイテムを視覚的に結合できるため、レポートを表示するユーザーにとってレポートの内容が読みやすくなります。 定義済みの罫線スタイルを使用すると、テキスト ボックス、テキスト ボックスのグループ、画像などの周囲に簡単に罫線を追加できます。 また、罫線、線、グリッド線のスタイル、幅、および色を変更することもできます。 罫線は、選択したアイテム全体の周り、またはアイテムの端に沿って (テキスト ボックスの下辺に沿った罫線など) 追加されます。  
  
 テキスト ボックス内、レポート レイアウト内、または画像の周囲の罫線とグリッド線を書式設定するには、レポート アイテムの **プロパティ** ダイアログ ボックスの **[罫線]** タブを使用します。 たとえば、画像の周りに罫線を追加するには、画像を右クリックし、 **[画像のプロパティ]** ダイアログ ボックスで **[罫線]** をクリックします。  
  
 標準の罫線枠だけでなく、追加の罫線枠もグラフに適用できます。 詳細については、「[グラフへの枠線の追加 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/add-a-border-frame-to-a-chart-report-builder-and-ssrs.md)」を参照してください。  
  
 罫線をレポート自体に追加することもできます。 詳細については、「 [レポートへの罫線の追加 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/add-a-border-to-a-report-report-builder-and-ssrs.md)の詳細を参照してください。  
  
## <a name="applying-background-colors"></a>背景色の適用  
 レポート全体の背景、レポート内のテキスト ボックスの背景、またはデータ領域内のセルやセルのグループに、塗りつぶしの色を追加できます。 既定の背景色は白ですが、レポート アイテムの **プロパティ** ダイアログ ボックスの **[塗りつぶし]** タブで色を選択できます。 たとえば、テキスト ボックスの背景色を変更する場合は、テキスト ボックスを右クリックして、 **[テキスト ボックスのプロパティ]** をクリックします。 **[塗りつぶし]** をクリックして、適切な色を選択します。 このダイアログ ボックスでは、選択したアイテムの背景色を選択することも、背景に表示される画像を追加することもできます。  
  
 グラフを使用する場合は、背景色のグラデーションとパターンのスタイルも指定できます。 詳細については、「[グラフの書式設定 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md)」を参照してください。  
  
## <a name="using-images-as-formatting"></a>書式設定での画像の使用  
 画像が含まれているフィールドはデータ領域に追加できます。 画像フィールドを使用した場合、画像はレポートの実行時にレポートに表示されます。  
  
 ロゴなどの画像をレポートの背景に追加したり、四角形、テキスト ボックス、テーブル、マトリックスなどのグラフの一部、またはレポートの本文やページのセクションに追加することもできます。 詳細については、「[画像 &#40;レポート ビルダーおよび SSRS& #41;](../../reporting-services/report-design/images-report-builder-and-ssrs.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [テキストとプレースホルダーの書式設定 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/formatting-text-and-placeholders-report-builder-and-ssrs.md)   
 [数値と日付の書式設定 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/formatting-numbers-and-dates-report-builder-and-ssrs.md)   
 [テキスト ボックス内のテキストの書式設定 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/format-text-in-a-text-box-report-builder-and-ssrs.md)   
 [[塗りつぶし] ダイアログ ボックス &#40;レポート ビルダーおよび SSRS&#41;](https://msdn.microsoft.com/library/93a91d02-d558-4a0e-8d17-3fdf21e208d3)  
  
  
