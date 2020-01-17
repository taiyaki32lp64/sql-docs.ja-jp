---
title: 空のポイントのグラフを追加 (レポート ビルダーおよび SSRS) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 2b056119-439f-494f-83cf-ee0c05dc6487
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 59c79d4824c7df4709c571d5d46476fd89f3cbe4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66106607"
---
# <a name="add-empty-points-to-the-chart-report-builder-and-ssrs"></a>空のポイントのグラフへの追加 (レポート ビルダーおよび SSRS)
  NULL 値は、系列内のデータ ポイント間の空白 (すきま) としてグラフに表示されます。 空のポイントとは、NULL 値によって作成された空白に挿入できるデータ ポイントのことです。  
  
 既定では、空のポイントは、値が含まれている前のデータ ポイントと次のデータ ポイントの平均値を求めることによって計算されます。 この既定の動作を変更して、すべての空のポイントが値ゼロのデータ ポイントとして挿入されるようにすることもできます。  
  
 詳細については、「[グラフ内の空のデータ ポイントおよび NULL データ ポイント &#40;レポート ビルダーおよび SSRS&#41;](charts-report-builder-and-ssrs.md)」を参照してください。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-specify-empty-points-on-a-chart"></a>空のポイントをグラフ上で指定するには  
  
1.  プロパティ ペインを開きます。  
  
2.  デザイン画面で、NULL 値が含まれている系列を右クリックします。 系列のプロパティが [プロパティ] ペインに表示されます。  
  
3.  **[EmptyPoint]** ノードを展開します。  
  
4.  Color プロパティの色の値を選択します。  
  
5.  **[EmptyPoint]** ノードで [Marker] ノードを展開します。  
  
6.  MarkerType プロパティのマーカーの種類を選択します。  
  
    > [!NOTE]  
    >  空のポイントを横棒グラフ、縦棒グラフ、または散布図に追加するには、マーカーの種類を選択する必要があります。 ただし、面グラフ、折れ線グラフ、およびレーダー グラフの場合は、マーカーを指定しなくても空白 (すきま) が自動的に塗りつぶされるので、マーカーの種類の選択は省略可能です。  
  
7.  空のポイントの値を設定します。  
  
    1.  プロパティ ペインで、 **[CustomAttributes]** ノードを展開します。  
  
    2.  EmptyPointValue プロパティを設定します。 前のデータ ポイントと次のデータ ポイントの平均値で空のポイントを挿入するには、 **[Average]** を選択します。 値ゼロのデータ ポイントとして空のポイントを挿入するには、 **[Zero]** を選択します。  
  
## <a name="see-also"></a>参照  
 [データセット フィルター、データ領域フィルター、およびグループ フィルターの追加 (レポート ビルダーおよび SSRS)](add-dataset-filters-data-region-filters-and-group-filters.md)   
 [グラフの種類 &#40;レポート ビルダーおよび SSRS&#41;](chart-types-report-builder-and-ssrs.md)   
 [グラフへのスケール区切りの追加 (レポート ビルダーおよび SSRS)](add-scale-breaks-to-a-chart-report-builder-and-ssrs.md)   
 [グラフ &#40;レポート ビルダーおよび SSRS&#41;](charts-report-builder-and-ssrs.md)  
  
  
