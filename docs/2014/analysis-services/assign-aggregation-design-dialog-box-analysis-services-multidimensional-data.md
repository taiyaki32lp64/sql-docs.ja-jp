---
title: 集計デザイン ダイアログ ボックス (Analysis Services - 多次元データ) を割り当てる |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.sqlserverstudio.copyaggregationdesign.f1
ms.assetid: 50c26cb1-c294-4f17-8b9e-435fdbd4806d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 11ee89e8849155f905e3908e491184f78a8f08b7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66062228"
---
# <a name="assign-aggregation-design-dialog-box-analysis-services---multidimensional-data"></a>[集計デザインの割り当て] ダイアログ ボックス (Analysis Services - 多次元データ)
  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] の **[集計デザインの割り当て]** ダイアログ ボックスを使用すると、1 つまたは複数のコピー先パーティションに集計デザインを割り当てることができます。 **[集計デザインの割り当て]** ダイアログ ボックスを表示するには、 **オブジェクト エクスプローラー** でパーティションまたは集計デザインを右クリックし、 **[集計デザインの割り当て]** をクリックします。  
  
## <a name="options"></a>および  
  
|項目|定義|  
|----------|----------------|  
|**集計デザイン**|1 つまたは複数のコピー先パーティションに割り当てる集計デザインを選択します。|  
|**コピー先パーティション**|集計デザインを割り当てるパーティションを選択します。 次のグリッドを使用して、コピー先パーティションを指定します。<br /><br /> \<チェック ボックス >:選択するか、またはコピー先パーティションとして表示されているすべてのパーティションを除外する列ヘッダーのチェック ボックスをオフにします。 パーティション横にあるチェック ボックスをオンまたはオフにすることで、そのパーティションをコピー先パーティションとして選択または選択解除できます。<br /><br /> **パーティション**:パーティションの名前が表示されます。<br /><br /> **ソース**:パーティションのソース テーブルまたはクエリが表示されます。<br /><br /> **集計デザイン**:パーティションの既存の集計デザインの名前が表示されます。|  
|**集計デザインを含むパーティションを非表示にします。**|オンにすると、集計デザインが割り当てられていないパーティションだけが表示されます。|  
  
## <a name="see-also"></a>関連項目  
 [集計と集計デザイン](multidimensional-models-olap-logical-cube-objects/aggregations-and-aggregation-designs.md)  
  
  
