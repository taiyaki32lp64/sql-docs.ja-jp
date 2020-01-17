---
title: オブジェクト カウント (使用法に基づく最適化ウィザード) の指定 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.storagedesignwizard.calculatingobjectcounts.f1
ms.assetid: 306c7c25-ae24-4852-ab8c-c82f68a4bc1f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e0503192c3c948110f8301c8eb375e1c8203e42f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66068242"
---
# <a name="specify-object-counts-usage-based-optimization-wizard"></a>[オブジェクト カウントの指定] (使用法に基づく最適化ウィザード)
  **[オブジェクト カウントの指定]** ページを使用すると、キューブ内のオブジェクト数を自動的に計算したり、推定カウントを手動で入力したりできます。 使用法に基づく最適化ウィザードでは、オブジェクト カウントを使用してストレージ要件を推定します。  
  
## <a name="options"></a>および  
 **キューブ オブジェクト**  
 キューブ内のディメンションおよび属性を表示します。 属性がないだけその`AggregationUsage`プロパティが None に設定、**集計使用法の確認**カウントを指定の必要のある唯一の属性は、ウィザードのページが表示されます。  
  
 **[推定カウント]**  
 メジャー グループ内の推定行数およびデータベース ディメンション内の属性の推定メンバー数を表示します。 推定カウントとして使用する値を入力することも、推定カウントの値を計算することもできます。 カウントの値を計算するには、フィールドに「0」を入力して **[カウント]** をクリックします。 既にカウントが表示されているフィールドは更新されません。  
  
 **パーティションの数**  
 (省略可) メジャー グループ内の推定行数およびディメンション内の属性の推定メンバー数を竜力します。  
  
 **Count**  
 空のすべてのフィールドに対する **[推定カウント]** 列の値を計算し、再作成します。 既にカウントが表示されているフィールドは更新されません。  
  
## <a name="see-also"></a>参照  
 [集計デザイン ウィザードの F1 ヘルプ](aggregation-design-wizard-f1-help.md)   
 [Analysis Services のウィザード&#40;多次元データ&#41;](analysis-services-wizards-multidimensional-data.md)  
  
  
