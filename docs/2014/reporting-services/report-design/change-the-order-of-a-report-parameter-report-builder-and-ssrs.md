---
title: レポート パラメーターの順序の変更 (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: abd61e19-dba3-423c-a26c-e8bc43197d3f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 7a1d9413332ed19bd4db94fc60beecff85f02ac7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66106328"
---
# <a name="change-the-order-of-a-report-parameter-report-builder-and-ssrs"></a>レポート パラメーターの順序の変更 (レポート ビルダーおよび SSRS)
  従属パラメーターが、そのパラメーターが依存するパラメーターの前にリストされている場合、レポート パラメーターの順序を変更します。 カスケード型パラメーターがある場合や、パラメーターの既定値をユーザーに対して示してから他のパラメーターの値をユーザーが選択する場合に、パラメーターの順序は重要です。 従属レポート パラメーターには、既定値のクエリまたは有効値のクエリのいずれかの、クエリ パラメーターへの参照が含まれます。これは、レポート データ ペインのパラメーター リストでその後にあるレポート パラメーターを参照します。  
  
 レポート ビューアー ツール バーにパラメーターを表示する順序は、レポート データ ペインのパラメーターの順序によって決まります。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-change-the-order-of-report-parameters"></a>レポート パラメーターの表示順を変更するには  
  
1.  レポート データ ペインで [パラメーター] ノードを展開します。  
  
2.  パラメーターをクリックしますおよびを使用し、下向きの矢印ボタンの一覧で上または下のパラメーターを移動するレポート データ ペインのツールバー。 次の図は、レポート ビルダーのレポート データ ペインを示しています。  
  
     ![レポート データ ペイン](../media/reportdatapane.png "レポート データ ペイン")  
  
## <a name="see-also"></a>参照  
 [レポート パラメーター &#40;レポート ビルダーおよびレポート デザイナー&#41;](report-parameters-report-builder-and-report-designer.md)   
 [レポート ビルダーのダイアログ ボックス、ペイン、およびウィザードに関するヘルプ](../report-builder-help-for-dialog-boxes-panes-and-wizards.md)   
 [カスケード型パラメーターのレポートへの追加 (レポート ビルダーおよび SSRS)](add-cascading-parameters-to-a-report-report-builder-and-ssrs.md)   
 [チュートリアル: レポートへのパラメーターの追加 &#40;レポート ビルダー&#41;](../tutorial-add-a-parameter-to-your-report-report-builder.md)   
 [データセット フィルター、データ領域フィルター、およびグループ フィルターの追加 (レポート ビルダーおよび SSRS)](add-dataset-filters-data-region-filters-and-group-filters.md)   
 [Parameters コレクションの参照 &#40;レポート ビルダーおよび SSRS&#41;](built-in-collections-parameters-collection-references-report-builder.md)  
  
  
