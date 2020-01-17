---
title: グラフの凡例項目を非表示にする (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 92256240-0cd5-4be4-8904-d1e3b93cb6b3
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: e2a9f9364f790e88f119ee46ed17ad2051d23b64
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66106260"
---
# <a name="hide-legend-items-on-the-chart-report-builder-and-ssrs"></a>グラフの凡例項目を非表示にする (レポート ビルダーおよび SSRS)
  既定では、図形グラフ以外のグラフに追加した系列は、凡例の項目として使用されます。 円グラフ、ドーナツ グラフ、じょうごグラフ、およびピラミッド グラフでは、グラフに系列を追加すると、凡例に個々のデータ ポイントが追加されます。  
  
 凡例の任意の項目を非表示にすることができます。 凡例の項目を非表示にした場合も、グラフには表示されます。 これは、グラフに追加した系列の詳細な情報を表示したくないときに便利です。 たとえば、移動平均のような計算系列をグラフに追加した場合、凡例のこのエントリを非表示にし、元の系列の詳細な情報のみを表示できます。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-hide-an-item-from-display-in-the-legend"></a>凡例の項目を非表示にするには  
  
1.  非表示にする系列を右クリックし、 **[系列のプロパティ]** をクリックします。  
  
2.  **[凡例]** をクリックします。 **[凡例内の次の系列を非表示にする]** オプションを選択します。  
  
    > [!NOTE]  
    >  あるグループの系列を非表示にし、他のグループの系列を表示することはできません。 **[系列グループ]** 領域にフィールドを追加している場合、このグループに属するすべての系列は非表示になります。  
  
## <a name="see-also"></a>関連項目  
 [グラフの凡例の書式設定 &#40;レポート ビルダーおよび SSRS&#41;](chart-legend-formatting-report-builder.md)   
 [グラフでのデータ ポイントの書式設定 &#40;レポート ビルダーおよび SSRS&#41;](formatting-data-points-on-a-chart-report-builder-and-ssrs.md)   
 [凡例アイテムのテキストの変更 &#40;レポート ビルダーおよび SSRS&#41;](chart-legend-change-item-text-report-builder.md)   
 [グラフへの移動平均の追加 &#40;レポート ビルダーおよび SSRS&#41;](add-a-moving-average-to-a-chart-report-builder-and-ssrs.md)   
 [[全般] ([凡例のプロパティ] ダイアログ ボックス) &#40;レポート ビルダーおよび SSRS&#41;](../legend-properties-dialog-box-general-report-builder-and-ssrs.md)  
  
  
