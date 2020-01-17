---
title: ClusterDistance (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 523c57811ca29956edc3c18b8143844732c163b6
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68892390"
---
# <a name="clusterdistance-dmx"></a>ClusterDistance (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  **Clusterdistance**関数は、指定されたクラスターから入力したケースの距離を返します。クラスターが指定されていない場合は、最も可能性の高いクラスターと入力したケース間の距離を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
ClusterDistance([<ClusterID expression>])  
```  
  
## <a name="applies-to"></a>適用対象  
 この関数は、基本となるデータ マイニング モデルがクラスターをサポートする場合にのみ使用できます。 関数は、任意の種類のクラスターモデル (EM、K など) で使用できますが、結果はアルゴリズムによって異なります。  
  
## <a name="return-type"></a>戻り値の型  
 スカラー値です。  
  
## <a name="remarks"></a>コメント  
 **Clusterdistance**関数は、入力したケースと、その入力ケースの確率が最も高いクラスターとの距離を返します。  
  
 K がクラスター化されている場合、いずれのケースも1つのクラスターに属することができますが、メンバーシップの重みは1.0 であるため、クラスターの距離は常に0になります。 ただし、K-Means では、各クラスターに重心があると想定されています。 階層の値を取得するには、マイニングモデルコンテンツ内の入れ子になった NODE_DISTRIBUTION テーブルをクエリまたは参照します。 詳細については、「 [クラスター モデルのマイニング モデル コンテンツ &#40;Analysis Services - データ マイニング&#41;](https://docs.microsoft.com/analysis-services/data-mining/mining-model-content-for-clustering-models-analysis-services-data-mining)」を参照してください。  
  
 既定の EM クラスタリング方法の場合、クラスター内のすべてのポイントは同じように見なされます。したがって、設計上、クラスターの重心はありません。 特定のケースと特定のクラスター *N*の間の**clusterdistance**の値は、次のように計算されます。  
  
 ClusterDistance (N) = 1-(メンバーシップの重み (N))  
  
 または:  
  
 ClusterDistance (N) = 1-Clusterdistance (N))  
  
## <a name="related-prediction-functions"></a>関連する予測関数  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]には、クラスターモデルにクエリを実行するための次の関数が用意されています。  
  
-   [クラスター &#40;DMX&#41; ](../dmx/cluster-dmx.md)関数を使用して、最も可能性の高いクラスターを返します。  
  
-   [Clusterprobability &#40;DMX&#41; ](../dmx/clusterprobability-dmx.md)関数は、ケースが特定のクラスターに属する確率を取得するために使用します。 この値は、クラスター距離の逆の役割を果たします。  
  
-   [PredictHistogram &#40;DMX&#41; ](../dmx/predicthistogram-dmx.md)関数を使用すると、各モデルのクラスターに存在する入力ケースの可能性のヒストグラムを取得できます。  
  
-   [Predictcaselikelihood &#40;度 DMX&#41; ](../dmx/predictcaselikelihood-dmx.md)関数を使用すると、アルゴリズムによって学習されたモデルを考慮して入力ケースが存在する可能性を示す 0 ~ 1 のメジャーを返すことができます。  
  
## <a name="example1-obtaining-cluster-distance-to-the-most-likely-cluster"></a>Example1最も可能性の高いクラスターへのクラスターの距離の取得  
 次の例では、指定したケースから、ケースが属する可能性が最も高いクラスターへの距離を返します。  
  
```  
SELECT  
    ClusterDistance()  
FROM  
    [TM Clustering]  
NATURAL PREDICTION JOIN  
(SELECT 28 AS [Age],  
    '2-5 Miles' AS [Commute Distance],  
    'Graduate Degree' AS [Education],  
    0 AS [Number Cars Owned],  
    0 AS [Number Children At Home]) AS t  
```  
  
 例の結果を次に示します。  
  
|式|  
|----------------|  
|0.0477390930705145|  
  
 これがどのクラスターであるかを確認するには、上記の例で `Cluster` の代わりに `ClusterDistance` を使用します。  
  
 例の結果を次に示します。  
  
|$CLUSTER|  
|--------------|  
|クラスター 6|  
  
## <a name="example2-obtaining-distance-to-a-specified-cluster"></a>Example2指定されたクラスターへの距離を取得しています  
 次の構文では、マイニング モデル コンテンツ スキーマ行セットを使用して、マイニング モデル内のクラスターのノードの ID とノードのキャプションの一覧を返します。 その後、 **Clusterdistance**関数でクラスター識別子の引数としてノードのキャプションを使用できます。  
  
```  
SELECT NODE_UNIQUE_NAME, NODE_CAPTION   
FROM <model>.CONTENT   
WHERE NODE_TYPE = 5  
```  
  
 例の結果を次に示します。  
  
|NODE_UNIQUE_NAME|NODE_CAPTION|  
|------------------------|-------------------|  
|001|クラスター 1|  
|002|Cluster 2|  
  
 次の構文例では、Cluster 2 というラベルが付いたクラスターから、指定したケースの距離を返します。  
  
```  
SELECT  
    ClusterDistance('Cluster 2')  
AS [Cluster 2 Distance]  
FROM [TM Clustering]  
NATURAL PREDICTION JOIN  
(SELECT 28 AS [Age],  
    '2-5 Miles' AS [Commute Distance],  
    'Graduate Degree' AS [Education],  
    0 AS [Number Cars Owned],  
    0 AS [Number Children At Home]) AS t  
```  
  
 例の結果を次に示します。  
  
|Cluster 2 Distance|  
|------------------------|  
|0.97008209236394|  
  
## <a name="see-also"></a>関連項目  
 [クラスター &#40;DMX&#41;](../dmx/cluster-dmx.md)   
 [データマイニング拡張&#40;機能&#41; DMX 関数リファレンス](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [DMX &#40;関数&#41;](../dmx/functions-dmx.md)   
 [クラスター モデルのマイニング モデル コンテンツ &#40;Analysis Services - データ マイニング&#41;](https://docs.microsoft.com/analysis-services/data-mining/mining-model-content-for-clustering-models-analysis-services-data-mining)  
  
  
