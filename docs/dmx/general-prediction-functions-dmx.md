---
title: 一般的な予測関数 (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 57909c1bb4009ae85b7e1b38b8b3cf3fa0e70ea9
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68892768"
---
# <a name="general-prediction-functions-dmx"></a>一般的な予測関数 (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  データマイニング拡張機能 (DMX) で**select**ステートメントを使用すると、さまざまな種類のクエリを作成できます。 クエリを使用すると、マイニング モデル自体の情報を返したり、新しい予測を作成したり、新しいデータを使用してトレーニングしてモデルを変更したりできます。 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]には、クエリで返される情報の種類を制御するさまざまな特殊な関数が用意されています。 これらの関数を DMX クエリに追加すると、データの統計または列を取得できます。 ただし、各クエリの種類とモデルの種類では、特定の関数しかサポートされていません。  
  
## <a name="common-functions"></a>[共通の関数]  
 関数を使用して、マイニング モデルによって返される結果を拡張できます。 テーブル式を返す**SELECT**ステートメントには、次の関数を使用できます。  
  
|||  
|-|-|  
|[DMX 数&#40;の合計&#41;](../dmx/bottomcount-dmx.md)|[RangeMin &#40;DMX&#41;](../dmx/rangemin-dmx.md)|  
|[DMX の&#40;割合&#41;](../dmx/bottompercent-dmx.md)|[TopCount &#40;DMX&#41;](../dmx/topcount-dmx.md)|  
|[Predict &#40;DMX&#41;](../dmx/predict-dmx.md)|[TopPercent &#40;DMX&#41;](../dmx/toppercent-dmx.md)|  
|[RangeMax &#40;DMX&#41;](../dmx/rangemax-dmx.md)|[TopSum &#40;DMX&#41;](../dmx/topsum-dmx.md)|  
|[RangeMid &#40;DMX&#41;](../dmx/rangemid-dmx.md)||  
  
 さらに、ほぼすべてのモデルの種類で、次の関数がサポートされています。  
  
-   [存在&#40;する DMX&#41;](../dmx/exists-dmx.md)  
  
-   [IsDescendant &#40;DMX&#41;](../dmx/isdescendant-dmx.md)  
  
-   [IsTestCase &#40;DMX&#41;](../dmx/istestcase-dmx.md)  
  
-   [IsTrainingCase &#40;DMX&#41;](../dmx/istrainingcase-dmx.md)  
  
-   [Predict &#40;DMX&#41;](../dmx/predict-dmx.md)  
  
-   [RangeMax &#40;DMX&#41;](../dmx/rangemax-dmx.md)  
  
-   [RangeMid &#40;DMX&#41;](../dmx/rangemid-dmx.md)  
  
-   [RangeMin &#40;DMX&#41;](../dmx/rangemin-dmx.md)  
  
-   [StructureColumn &#40;DMX&#41;](../dmx/structurecolumn-dmx.md)  
  
 個々のアルゴリズムでは、これ以外の関数がサポートされている場合もあります。 各モデルの種類でサポートされている関数の一覧については、「[データマイニングクエリ](https://docs.microsoft.com/analysis-services/data-mining/data-mining-queries)」を参照してください。  
  
## <a name="functions-specific-to-select-syntax"></a>SELECT 構文固有の関数  
 次の表に、 **SELECT**ステートメントの種類ごとに使用できる関数を示します。  
  
 DMX の関数に関する一般的な情報については、「[データマイニング拡張機能&#40;の&#41; dmx 関数リファレンス](../dmx/data-mining-extensions-dmx-function-reference.md)」を参照してください。  
  
|[クエリの種類]|サポートされる関数|コメント|  
|----------------|-------------------------|-------------|  
|[モデルから\<DISTINCT を選択 >](../dmx/select-distinct-from-model-dmx.md)|[RangeMin &#40;DMX&#41;](../dmx/rangemin-dmx.md)<br /><br /> [RangeMid &#40;DMX&#41;](../dmx/rangemid-dmx.md)<br /><br /> [RangeMax &#40;DMX&#41;](../dmx/rangemax-dmx.md)|これらの関数を使用すると、数値データ型を含む任意の列の最大値、最小値、および平均値を提供できます。列が連続しているか離散しているかは関係ありません。|  
|[モデル > \<から選択します。情報](../dmx/select-from-model-content-dmx.md)<br /><br /> または<br /><br /> [モデル > \<から選択します。DIMENSION_CONTENT](../dmx/select-from-model-dimension-content-dmx.md)|[IsDescendant &#40;DMX&#41;](../dmx/isdescendant-dmx.md)|この関数は、モデル内の指定されたノードの子ノードを取得します。また、この関数を使用すると、たとえば、マイニング モデル コンテンツのノードを繰り返し処理できます。 マイニング モデル コンテンツ内でのノードの配置は、モデルの種類によって異なります。 各マイニングモデルの種類の構造については、「[マイニングモデル&#40;コンテンツ Analysis Services-データ&#41;マイニング](https://docs.microsoft.com/analysis-services/data-mining/mining-model-content-analysis-services-data-mining)」を参照してください。<br /><br /> マイニング モデル コンテンツをディメンションとして保存した場合は、属性階層のクエリに使用できる他の多次元式 (MDX) 関数も使用できます。|  
|[モデル > \<から選択します。場合](../dmx/select-from-model-cases-dmx.md)|[IsInNode &#40;DMX&#41;](../dmx/isinnode-dmx.md)<br /><br /> [ClientSettingsGeneralFlag クラス](../relational-databases/wmi-provider-configuration-classes/clientsettingsgeneralflag-class/clientsettingsgeneralflag-class.md)<br /><br /> [IsTrainingCase &#40;DMX&#41;](../dmx/istrainingcase-dmx.md)<br /><br /> [IsTestCase &#40;DMX&#41;](../dmx/istestcase-dmx.md)|Lag 関数は、タイムシリーズモデルでのみサポートされています。<br /><br /> IsTestCase 関数は、テストデータセットを作成するために、提示オプションを使用して作成された構造に基づくモデルでサポートされています。 提示されたテスト セットを含む構造に基づいていない場合は、すべてのケースがトレーニング ケースと見なされます。|  
|[モデル > \<から選択します。SAMPLE_CASES](../dmx/select-from-model-sample-cases-dmx.md)|[IsInNode &#40;DMX&#41;](../dmx/isinnode-dmx.md)|このコンテキストでは、IsInNode 関数は、一連の理想的なサンプルケースに属するケースを返します。|  
|モデル > \<から選択します。PMML|該当なし。 代わりに、XML クエリ関数を使用してください。|PMML 表現は、次のモデルの種類のみでサポートされます。<br /><br /> [!INCLUDE[msCoName](../includes/msconame-md.md)]デシジョンツリー<br /><br /> [!INCLUDE[msCoName](../includes/msconame-md.md)] クラスター|  
|[モデル > \<予測結合から選択します](../dmx/select-from-model-prediction-join-dmx.md)|モデルの作成に使用するアルゴリズムに特有の予測関数です。|各種類のモデルの予測関数の一覧については、「[データマイニングクエリ](https://docs.microsoft.com/analysis-services/data-mining/data-mining-queries)」を参照してください。|  
|[モデルから\<選択 >](../dmx/select-from-model-dmx.md)|モデルの作成に使用するアルゴリズムに特有の予測関数です。|各種類のモデルの予測関数の一覧については、「[データマイニングクエリ](https://docs.microsoft.com/analysis-services/data-mining/data-mining-queries)」を参照してください。|  
  
## <a name="see-also"></a>参照  
 [データ マイニング拡張機能 &#40;DMX&#41; リファレンス](../dmx/data-mining-extensions-dmx-reference.md)   
 [データマイニング拡張&#40;機能&#41; DMX 関数リファレンス](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [データマイニング拡張&#40;機能&#41; DMX オペレーターリファレンス](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [データマイニング拡張&#40;機能&#41; DMX ステートメントリファレンス](../dmx/data-mining-extensions-dmx-statements.md)   
 [データマイニング拡張&#40;機能&#41; DMX 構文表記規則](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [データマイニング拡張&#40;機能&#41; DMX 構文要素](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [構造と DMX 予測クエリの使用](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [DMX 選択ステートメントについて](../dmx/understanding-the-dmx-select-statement.md)  
  
  
