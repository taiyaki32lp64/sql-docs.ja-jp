---
title: (キューブ ウィザード) の作成方法の選択 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubewizard.cubedefinition.f1
ms.assetid: 985d3b5b-7891-465b-862d-f7e75431b342
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 793c83dba01be84fb468b0be54bb7d0405e39467
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66069631"
---
# <a name="select-creation-method-cube-wizard"></a>[作成方法の選択] (キューブ ウィザード)
  **[作成方法の選択]** ページを使用すると、キューブの作成方法を指定できます。  
  
## <a name="options"></a>および  
 **既存のテーブルを使用します。**  
 データ ソース内の既存のテーブルを使用してキューブを作成する場合に選択します。 ウィザードの指示に従って、既存のテーブルに基づいてメジャー グループとディメンションを選択および定義し、新しいキューブを作成します。  
  
 **空のキューブを作成します。**  
 空のキューブを作成する場合に選択します。 このオプションは、すべてを手動で作成する場合やキューブ内のすべてのメジャー グループがリンク メジャー グループである場合に役立ちます。  
  
> [!NOTE]  
>  このオプションは、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] プロジェクトを使用している場合にのみ使用でき、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] データベースに直接接続している場合は使用できません。  
  
 **データ ソースにテーブルを生成します。**  
 キューブを作成してからそのキューブの定義に基づいてデータ ソースに新しいテーブルを生成する場合に選択します。  
  
> [!NOTE]  
>  このオプションを使用するには、基になるデータ ソースにオブジェクトを作成する権限が必要です。  
  
 このオプションを選択すると、 **[テンプレート]** オプションが有効になります。  
  
 **テンプレート**  
 キューブの作成に使用するテンプレートを選択します。 テンプレートは、特定のビジネス用途向けの定義のセットを提供します。  
  
> [!NOTE]  
>  このオプションは、 **[データ ソースにテーブルを生成]** オプションが選択された場合のみ使用できます。  
  
## <a name="see-also"></a>参照  
 [キューブ オブジェクト&#40;Analysis Services - 多次元データ&#41;](multidimensional-models-olap-logical-cube-objects/cube-objects-analysis-services-multidimensional-data.md)   
 [多次元モデルのキューブ](multidimensional-models/cubes-in-multidimensional-models.md)   
 [多次元モデル内のディメンション](multidimensional-models/dimensions-in-multidimensional-models.md)  
  
  
