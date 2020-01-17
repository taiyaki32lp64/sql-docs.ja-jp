---
title: データ マイニング拡張機能 (DMX) 関数リファレンス |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 68d57ac2db4149178a61424affef5e8948de0063
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68070949"
---
# <a name="data-mining-extensions-dmx-function-reference"></a>データ マイニング拡張機能 (DMX) 関数リファレンス
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] は、データ マイニング拡張機能 (DMX) 言語のいくつかの関数をサポートしています。 関数は、さらに、予測を説明する情報を追加する予測クエリの結果を展開します。 関数は、さらに、予測の結果を返す方法制御も提供します。 次の表では、DMX の関数を使用する方法の理解に役立つリソースへのリンクを提供します。  
  
|関数|説明|  
|--------------|-----------------|  
|[一般的な予測関数&#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)|すべての種類のモデルで使用でき、特定の種類のマイニング モデルのクエリを実行する方法に関する詳細情報へのリンクを提供するリスト関数。|  
|[構造と DMX 予測クエリの使用](../dmx/structure-and-usage-of-dmx-prediction-queries.md)|DMX を使用して予測クエリを作成する方法の概要を示します。|  
|[BottomCount &#40;DMX&#41;](../dmx/bottomcount-dmx.md)|順位付け式に基づいてデータを昇順に並べ替え、最下位行から指定数を含むテーブルを返します。|  
  
 次の表は、DMX がサポートする関数の一覧を示しています。  
  
|関数|説明|  
|--------------|-----------------|  
|[BottomCount &#40;DMX&#41;](../dmx/bottomcount-dmx.md)|昇順に順位付け式に基づいて並べ替え、テーブル式の最後の n 項目行を含むテーブルを返します。|  
|[BottomPercent &#40;DMX&#41;](../dmx/bottompercent-dmx.md)|順位付け式に基づいてランクの増加順に、指定されたパーセント式を満たす最下位行の最小数を含むテーブルを返します。|  
|[BottomSum &#40;DMX&#41;](../dmx/bottomsum-dmx.md)|順位付け式に基づいてランクの増加順に、指定された合計式を満たす最下位行の最小数を含むテーブルを返します。|  
|[Cluster &#40;DMX&#41;](../dmx/cluster-dmx.md)|入力ケースを含んでいる可能性が最も高いクラスターを返します。|  
|[ClusterProbability &#40;DMX&#41;](../dmx/clusterprobability-dmx.md)|入力ケースがクラスターに所属する確率を返します。|  
|[存在する&#40;DMX&#41;](../dmx/exists-dmx.md)|指定した SELECT ステートメントから返された結果セットに少なくとも 1 行が含まれる場合は true を返します。|  
|[IsDescendant &#40;DMX&#41;](../dmx/isdescendant-dmx.md)|現在のノードが、指定したノードから下降かどうかを示します。|  
|[IsInNode &#40;DMX&#41;](../dmx/isinnode-dmx.md)|指定したノードが、ケースを含むかどうかを示します。|  
|[IsTestCase &#40;DMX&#41;](../dmx/istestcase-dmx.md)|ケースがテスト_ケースのセットに属するかどうかを示します。|  
|[IsTrainingCase &#40;DMX&#41;](../dmx/istrainingcase-dmx.md)|ケースがトレーニング ケースのセットに属するかどうかを示します。|  
|[Lag &#40;DMX&#41;](../dmx/lag-dmx.md)|データの現在のケースの日付と最後の日付間のタイム スライスを返します。|  
|[Predict &#40;DMX&#41;](../dmx/predict-dmx.md)|指定した列に対して予測を実行します。|  
|[PredictAdjustedProbability &#40;DMX&#41;](../dmx/predictadjustedprobability-dmx.md)|指定した予測可能列の調整済みの確率を返します。|  
|[PredictAssociation &#40;DMX&#41;](../dmx/predictassociation-dmx.md)|列内の結合メンバーシップを予測します。|  
|[PredictCaseLikelihood &#40;DMX&#41;](../dmx/predictcaselikelihood-dmx.md)|入力したケースが既存のモデル内に収まる確率値を返します。 この関数は、クラスター モデルでのみ使用できます。|  
|[PredictHistogram &#40;DMX&#41;](../dmx/predicthistogram-dmx.md)|指定された列のヒストグラムを表すテーブルを返します。|  
|[PredictNodeId &#40;DMX&#41;](../dmx/predictnodeid-dmx.md)|選択したケースの NodeID を返します。|  
|[PredictProbability &#40;DMX&#41;](../dmx/predictprobability-dmx.md)|指定された列の確率を返します。|  
|[PredictSequence (DMX)](../dmx/predictsequence-dmx.md)|シーケンス内の次の値を予測します。|  
|[PredictStdev &#40;DMX&#41;](../dmx/predictstdev-dmx.md)|指定された列の標準偏差値を取得します。|  
|[PredictSupport &#40;DMX&#41;](../dmx/predictsupport-dmx.md)|列のサポート値を返します。|  
|[PredictTimeSeries &#40;DMX&#41;](../dmx/predicttimeseries-dmx.md)|時系列に対する将来の値を予測します。|  
|[PredictVariance &#40;DMX&#41;](../dmx/predictvariance-dmx.md)|指定された列の変位値を返します。|  
|[RangeMax &#40;DMX&#41;](../dmx/rangemax-dmx.md)|指定した discretized 型の列に対して検出される予測バケットの上限値を返します。|  
|[RangeMid &#40;DMX&#41;](../dmx/rangemid-dmx.md)|指定した discretized 型の列に対して検出される予測バケットの中間値を返します。|  
|[RangeMin &#40;DMX&#41;](../dmx/rangemin-dmx.md)|指定した discretized 型の列に対して検出された予測済みバケットの下限値を返します。|  
|[StructureColumn &#40;DMX&#41;](../dmx/structurecolumn-dmx.md)|指定したテーブル マイニング構造列の値を返します。|  
|[TopCount &#40;DMX&#41;](../dmx/topcount-dmx.md)|指定された最上位行数を含むテーブルを、順位付け式に基づいて降順で返します。|  
|[TopPercent &#40;DMX&#41;](../dmx/toppercent-dmx.md)|順位付け式に基づいてランクの減少順で、指定されたパーセント式を満たす最上位の行の最小数を含むテーブルを返します。|  
|[TopSum &#40;DMX&#41;](../dmx/topsum-dmx.md)|順位付け式に基づいてデータを降順に並べ替え、最上位行から指定された合計式を満たすまでの最小行数を含むテーブルを返します。|  
  
## <a name="see-also"></a>関連項目  
 [データ マイニング拡張機能&#40;DMX&#41;演算子リファレンス](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [データ マイニング拡張機能&#40;DMX&#41;ステートメント リファレンス](../dmx/data-mining-extensions-dmx-statements.md)   
 [データ マイニング拡張機能&#40;DMX&#41;構文表記規則](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [データ マイニング拡張機能&#40;DMX&#41;構文要素](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [一般的な予測関数&#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [構造と DMX 予測クエリの使用](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [DMX 選択ステートメントについて](../dmx/understanding-the-dmx-select-statement.md)  
  
  
