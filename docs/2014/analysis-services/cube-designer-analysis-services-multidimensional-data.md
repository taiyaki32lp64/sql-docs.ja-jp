---
title: キューブ デザイナー (Analysis Services - 多次元データ) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Cube Designer
ms.assetid: a6692467-da88-4312-8b03-d812f2ae5a96
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c0c52d2598c2fff79d9d7dd6cb99468871f12639
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66086606"
---
# <a name="cube-designer-analysis-services---multidimensional-data"></a>キューブ デザイナー (Analysis Services - 多次元データ)
  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] の**キューブ デザイナー**を使用すると、キューブに含まれているメジャー グループやメジャー、キューブ ディメンションやディメンション リレーションシップ、計算、主要業績評価指標 (KPI)、アクション、パーティション、パースペクティブ、および翻訳を含む、既存のキューブのさまざまなプロパティを編集したり、キューブに含まれているデータを参照したりできます。 **キューブ デザイナー** ダイアログ ボックスを表示するには、次の手順に従います。  
  
-   **ソリューション エクスプローラー** でキューブを右クリックし、ショートカット メニューから **[開く]** または **[デザイナーの表示]** を選択します。  
  
-   **ソリューション エクスプローラー**でキューブをダブルクリックします。  
  
 **キューブ デザイナー** のタブは次のとおりです。  
  
## <a name="tabs"></a>タブ  
  
|タブ|定義|  
|---------|----------------|  
|**キューブの構造**|メジャー グループやメジャーの追加と変更、キューブ ディメンションの追加、およびキューブに含まれているオブジェクトの関連するデータ ソース ビューからの表示を行います。 このタブの詳細については、「[Cube Structure &#40;Cube Designer&#41; &#40;Analysis Services - Multidimensional Data&#41;](cube-structure-cube-designer-analysis-services-multidimensional-data.md)」([キューブ構造] &#40;キューブ デザイナー&#41; &#40;Analysis Services - 多次元データ&#41;) を参照してください。|  
|**ディメンションの使用法**|キューブに含まれるキューブ ディメンションとメジャー グループの間のリレーションシップの作成と変更を行います。 このタブの詳細については、「[Dimension Usage &#40;Cube Designer&#41; &#40;Analysis Services - Multidimensional Data&#41;](dimension-usage-cube-designer-analysis-services-multidimensional-data.md)」([ディメンションの使用方法] &#40;キューブ デザイナー&#41; &#40;Analysis Services - 多次元データ&#41;) を参照してください。|  
|**計算**|キューブに含まれる、計算されるメンバー、名前付きセット、および多次元式 (MDX) スクリプトを含む計算の作成と変更を行います。 このタブの詳細については、「[Calculations &#40;Cube Designer&#41; &#40;Analysis Services - Multidimensional Data&#41;](calculations-cube-designer-analysis-services-multidimensional-data.md)」([計算] &#40;キューブ デザイナー&#41; &#40;Analysis Services - 多次元データ&#41;) を参照してください。|  
|**KPI**|キューブに含まれる KPI の作成と変更を行います。 このタブの詳細については、「[KPIs &#40;Cube Designer&#41; &#40;Analysis Services - Multidimensional Data&#41;](kpis-cube-designer-analysis-services-multidimensional-data.md)」([KPI] &#40;キューブ デザイナー&#41; &#40;Analysis Services - 多次元データ&#41;) を参照してください。|  
|**アクション**|キューブに含まれるドリルスルー アクションおよびレポート アクションを含むアクションの作成と変更を行います。 このタブの詳細については、「[Actions &#40;Cube Designer&#41; &#40;Analysis Services - Multidimensional Data&#41;](actions-cube-designer-analysis-services-multidimensional-data.md)」([アクション] &#40;キューブ デザイナー&#41; &#40;Analysis Services - 多次元データ&#41;) を参照してください。|  
|**パーティション**|キューブに含まれる、メジャー グループおよびパーティションのプロアクティブ キャッシュの設定を含むパーティションの作成と変更を行います。 このタブの詳細については、「[Partitions &#40;Cube Designer&#41; &#40;Analysis Services - Multidimensional Data&#41;](partitions-cube-designer-analysis-services-multidimensional-data.md)」([パーティション] &#40;キューブ デザイナー&#41; &#40;Analysis Services - 多次元データ&#41;) を参照してください。|  
|**パースペクティブ**|キューブに含まれるパースペクティブの作成と変更を行います。 このタブの詳細については、「[Perspectives &#40;Cube Designer&#41; &#40;Analysis Services - Multidimensional Data&#41;](perspectives-cube-designer-analysis-services-multidimensional-data.md)」([パースペクティブ] &#40;キューブ デザイナー&#41; &#40;Analysis Services - 多次元データ&#41;) を参照してください。|  
|**翻訳**|キューブに含まれる、メジャー グループ、メジャー、キューブ ディメンション、パースペクティブ、KPI、アクション、名前付きセット、および計算されるメンバーに対する翻訳の作成と変更を行います。 このタブの詳細については、「[Translations &#40;Cube Designer&#41; &#40;Analysis Services - Multidimensional Data&#41;](translations-cube-designer-analysis-services-multidimensional-data.md)」([翻訳] &#40;キューブ デザイナー&#41; &#40;Analysis Services - 多次元データ&#41;) を参照してください。|  
|**ブラウザー**|キューブのデータおよびメタデータを参照します。 このタブの詳細については、「[Browser &#40;Cube Designer&#41; &#40;Analysis Services - Multidimensional Data&#41;](browser-cube-designer-analysis-services-multidimensional-data.md)」([ブラウザー] &#40;キューブ デザイナー&#41; &#40;Analysis Services - 多次元データ&#41;) を参照してください。|  
  
## <a name="see-also"></a>関連項目  
 [キューブ オブジェクト&#40;Analysis Services - 多次元データ&#41;](multidimensional-models-olap-logical-cube-objects/cube-objects-analysis-services-multidimensional-data.md)   
 [多次元モデルのキューブ](multidimensional-models/cubes-in-multidimensional-models.md)   
 [Analysis Services のデザイナーおよびダイアログ ボックス&#40;多次元データ&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)  
  
  
