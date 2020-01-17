---
title: 円グラフの値の開始位置を円の最上部にする (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: d0e6fb59-ca4e-4d70-97cb-0ad183da21d3
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 2610534159be781e2719034b41276be5f0d7d473
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66104823"
---
# <a name="start-pie-chart-values-at-the-top-of-the-pie-report-builder-and-ssrs"></a>円グラフの値の開始位置を円の最上部にする (レポート ビルダーおよび SSRS)
  円グラフでは、既定でデータセットの最初の値が円の最上部から 90 度の位置から開始されます。 最初の値の開始位置を最上部にすることが望ましい場合もあります。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-start-the-pie-chart-at-the-top-of-the-pie"></a>円グラフの開始位置を円の最上部にするには  
  
1.  円グラフをクリックします。  
  
2.  **プロパティ** ペインが開いていない場合は、 **[表示]** タブの **[プロパティ]** をクリックします。  
  
3.  **プロパティ** ペインの **[カスタム属性]** で、 **[PieStartAngle]** を **0** から **270**に変更します。  
  
4.  **[実行]** をクリックして、レポートをプレビューします。  
  
 最初の値の開始位置が円グラフの最上部になります。  
  
## <a name="see-also"></a>関連項目  
 [グラフの書式設定 &#40;レポート ビルダーおよび SSRS&#41;](formatting-a-chart-report-builder-and-ssrs.md)   
 [円グラフ (レポート ビルダーおよび SSRS)](charts-report-builder-and-ssrs.md)  
  
  
