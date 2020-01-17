---
title: 四角形またはコンテナーの追加 (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
f1_keywords:
- "10061"
- sql13.rtp.rptdesigner.rectangleproperties.general.f1
ms.assetid: f905c35f-754d-4d02-80f3-85e29ddda826
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 2079eeb5cb871b5006ac4b2c45b60e9c8a3a3c97
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65574775"
---
# <a name="add-a-rectangle-or-container-report-builder-and-ssrs"></a>四角形またはコンテナーの追加 (レポート ビルダーおよび SSRS)
  グラフィック要素によってレポートの領域を分けたり、レポートの領域を強調したり、1 つ以上のレポート アイテムに背景を提供したりするには、 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] のページ分割されたレポートに四角形を追加します。 また、四角形をコンテナーとして使用すると、レポートでのデータ領域のレンダリング方法を制御することもできます。 四角形の外観は、背景や罫線の色など、四角形のプロパティを編集することによりカスタマイズできます。 四角形をコンテナーとして使用する方法について詳しくは、「[四角形と線 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/rectangles-and-lines-report-builder-and-ssrs.md)」および「[マトリックスとグラフでの同じデータの表示 &#40;レポート ビルダー&#41;](../../reporting-services/report-design/display-the-same-data-on-a-matrix-and-a-chart-report-builder.md)」をご覧ください。    
   
## <a name="to-add-a-rectangle"></a>四角形を追加するには    
    
1.  **[挿入]** タブの **[レポート アイテム]** グループで **[四角形]** をクリックします。    
    
2.  デザイン画面で、四角形の左上隅となる位置をクリックし、四角形の右下隅となる位置までドラッグします。    
    
     カーソルを移動すると、デザイン画面の他のオブジェクトと並んだときに "スナップ線" が表示されます。 これらのスナップ線はオブジェクトを配置する場合に役に立ちます。    
    
## <a name="to-create-a-container"></a>コンテナーを作成するには    
    
1.  四角形レポート アイテムをレポートに追加します。    
    
2.  レポート アイテムを四角形にドラッグします。    
    
    > [!NOTE]    
    >  四角形はアイテムの単なるコンテナーで、アイテムを四角形内で作成するか四角形にドラッグします。 デザイン画面に既に存在するアイテムの周囲に四角形を描画した場合、四角形はコンテナーとして機能しません。    
    
## <a name="to-change-rectangle-properties-such-as-color-style-or-weight"></a>色、スタイル、太さなどの四角形のプロパティを変更するには    
    
1.  四角形を選択し、[ホーム] タブの **[罫線]** セクションで線の色、スタイル、または太さのオプションをクリックします。    
    
2.  **[罫線]** ボタンの横にある矢印をクリックして、四角形のどの辺を変更するかを指定します。    
    
    > [!NOTE]    
    >  罫線のスタイルを **[二重線]** に設定した場合に、線の幅が 1 1/2 ポイントより狭いと、レポート ビルダー、レポート デザイナー、または [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] Web ポータルでレポートを実行しても、罫線が二重に表示されないことがあります。 レポートを他の形式 (Microsoft Word、Acrobat PDF など) にエクスポートすると、二重に表示されます。    
    
## <a name="see-also"></a>参照    
 [四角形と線 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/rectangles-and-lines-report-builder-and-ssrs.md)     
 [レンダリングの動作 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)    
    
  
