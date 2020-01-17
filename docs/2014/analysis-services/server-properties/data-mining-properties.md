---
title: データ マイニング プロパティ |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- ClusterCount property
- AllowedProvidersInOpenRowset property
- MinimumSeriesValue property
- ScoreMethod property
- MinimumImportance property
- ModellingCardinality property
- BrentTolerance property
- ComplexityPenalty property
- MaximumItemsetCount property
- MinimumSupport property
- AllowSessionMiningModels property
- HoldoutPercentage property
- ClusterCountPrior property
- MaximumSequenceStates property
- OptimizedPredictionCount property
- data mining [Analysis Services], properties
- MaximumStates property
- MaximumContinuousInputAttributes property
- MaximumOutputAttributes property
- AllowAdHocOpenRowsetQueries property
- Enabled property
- HistoricModelGap property
- SampleSize property
- MaximumInputAttributes property
- PeriodicityHint property
- MissingValueSubstitution property
- SplitMethod property
- ForceRegressor property
- MaximumBucketsForContinuousSplit property
- MaxConcurrentPredictionQueries property
- MinimumItemsetSize property
- AcyclicGraph property
- HoldoutMethod property
- StoppingTolerance property
- properties [data mining]
- AutoDetectPeriodicity property
- HoldoutTolerance property
- MinimumLeafCases property
- HoldoutSeed property
- MinimumClusterCases property
- ClusterCountDeviation property
- MinimumDependencyProbability property
- ClusteringMethod property
- MaximumItemsetSize property
- HiddenNodeRatio property
- MaximumSeriesValue property
ms.assetid: 9bc9abed-180a-4bd8-b2eb-89c62fa88110
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 96106fc8bc50a2a1b19c54a6970eeeb72952d82d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66069056"
---
# <a name="data-mining-properties"></a>データ マイニング プロパティ
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] では、次の表に示すデータ マイニング サーバー プロパティがサポートされています。 その他のサーバー プロパティとその設定方法の詳細については、「 [Configure Server Properties in Analysis Services](server-properties-in-analysis-services.md)」を参照してください。  
  
 **適用対象:** 多次元サーバー モードのみ  
  
## <a name="non-specific-category"></a>不特定カテゴリ  
 `AllowSessionMiningModels`  
 セッション マイニング モデルを作成できるかどうかを示すブール型プロパティです。  
  
 このプロパティの既定値は False であり、セッション マイニング モデルを作成できないことを示します。  
  
 `AllowAdHocOpenRowsetQueries`  
 開かれた行セットのアドホック クエリを許可するかどうかを示すブール型プロパティです。  
  
 このプロパティの既定値は False であり、開かれた行セットのクエリがセッション中に許可されないことを示します。  
  
 `AllowedProvidersInOpenRowset`  
 開かれた行セットで許可されるプロバイダーを識別する文字列プロパティです。コンマまたはセミコロンで区切られたプロバイダー ProgID の一覧または [All] で構成されます。  
  
 `MaxConcurrentPredictionQueries`  
 同時予測クエリの最大数を定義する、符号付き 32 ビット整数のプロパティです。  
  
## <a name="algorithms-category"></a>アルゴリズム カテゴリ  
 `Microsoft_Association_Rules\ Enabled`  
 Microsoft_Association_Rules アルゴリズムが有効かどうかを示すブール型プロパティです。  
  
 `Microsoft_Clustering\ Enabled`  
 Microsoft_Clustering algorithm アルゴリズムが有効かどうかを示すブール型プロパティです。  
  
 `Microsoft_Decision_Trees\ Enabled`  
 Microsoft_DecisionTrees アルゴリズムが有効かどうかを示すブール型プロパティです。  
  
 `Microsoft_Naive_Bayes\ Enabled`  
 Microsoft_Naive_Bayes アルゴリズムが有効かどうかを示すブール型プロパティです。  
  
 `Microsoft_Neural_Network\ Enabled`  
 Microsoft_Neural_Network アルゴリズムが有効かどうかを示すブール型プロパティです。  
  
 `Microsoft_Sequence_Clustering\ Enabled`  
 Microsoft_Sequence_Clustering アルゴリズムが有効かどうかを示すブール型プロパティです。  
  
 `Microsoft_Time_Series\ Enabled`  
 Microsoft_Time_Series アルゴリズムが有効かどうかを示すブール型プロパティです。  
  
 `Microsoft_Linear_Regression\ Enabled`  
 Microsoft_Linear_Regression アルゴリズムが有効かどうかを示すブール型プロパティです。  
  
 `Microsoft_Logistic_Regression\ Enabled`  
 Microsoft_Logistic_Regression アルゴリズムが有効かどうかを示すブール型プロパティです。  
  
> [!NOTE]  
>  サーバー上で使用可能なデータ マイニング サービスを定義するプロパティ以外に、特定のアルゴリズムの動作を定義するデータ マイニング プロパティが存在します。 データ マイニング モデルをサーバー レベルでなく、個々に作成する場合は、これらのプロパティを構成します。 詳しくは、「[データ マイニング アルゴリズム &#40;Analysis Services - データ マイニング&#41;](../data-mining/data-mining-algorithms-analysis-services-data-mining.md)」をご覧ください。  
  
## <a name="see-also"></a>関連項目  
 [物理アーキテクチャ &#40;Analysis Services - データ マイニング&#41;](../data-mining/physical-architecture-analysis-services-data-mining.md)   
 [Analysis services サーバーのプロパティを構成します。](server-properties-in-analysis-services.md)   
 [Analysis Services インスタンスのサーバー モードの決定](../instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  
