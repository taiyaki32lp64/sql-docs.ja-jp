---
title: アソシエーション モデルのクエリ例 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- itemsets [Analysis Services]
- association algorithms [Analysis Services]
- rules [Data Mining]
- association rules
- content queries [DMX]
ms.assetid: 68b39f5c-c439-44ac-8046-6f2d36649059
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a31052c0d239010407941141997fca8fc343f9cf
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66086122"
---
# <a name="association-model-query-examples"></a>結合モデルのクエリ例
  データ マイニング モデルに対するクエリを作成する際には、コンテンツ クエリを作成することも、予測クエリを作成することもできます。コンテンツ クエリでは、分析の間に検出されたルールやアイテムセットの詳細情報を取得できます。予測クエリでは、データ内で検出されたアソシエーションを使用して予測を行うことができます。 アソシエーション モデルの場合、予測はルールに基づいて行われるのが一般的で、提案を行うために使用できます。一方、コンテンツ クエリではアイテムセット間の関係を調べるのが一般的です。 モデルに関するメタデータを取得することもできます。  
  
 ここでは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] アソシエーション ルール アルゴリズムに基づくモデルに対してこれらの種類のクエリを作成する方法について説明します。  
  
 **コンテンツ クエリ**  
  
 [DMX を使用してモデル メタデータ データを取得する](#bkmk_Query1)  
  
 [スキーマ行セットからメタデータを取得する](#bkmk_Query2)  
  
 [モデルの元のパラメーターを取得する](#bkmk_Query3)  
  
 [アイテムセットと製品のリストを取得する](#bkmk_Query4)  
  
 [上位 10 個のアイテムセットを取得する](#bkmk_Query5)  
  
 **予測クエリ**  
  
 [関連のあるアイテムを予測する](#bkmk_Query6)  
  
 [関連するアイテムセットの信頼度を特定する](#bkmk_Query7)  
  
##  <a name="bkmk_top2"></a> モデルに関する情報の入手  
 すべてのマイニング モデルでは、アルゴリズムによって学習されたコンテンツが、標準化されたスキーマに従って公開されます。このスキーマを、マイニング モデル スキーマ行セットと呼びます。 マイニング モデル スキーマ行セットに対するクエリは、データ マイニング拡張機能 (DMX) ステートメントか [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ストアド プロシージャを使用して作成できます。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]では、SQL に似た構文を使用して、スキーマ行セットに対して直接、システム テーブルとしてクエリを実行することもできます。  
  
###  <a name="bkmk_Query1"></a> サンプル クエリ 1:DMX を使用してモデル メタデータを取得する  
 次のクエリは、アソシエーション モデル `Association`に関する基本的なメタデータ (モデルの名前、モデルが格納されているデータベース、モデルの子ノードの数など) を返します。 このクエリでは、DMX コンテンツ クエリを使用してモデルの親ノードからメタデータを取得しています。  
  
```  
SELECT MODEL_CATALOG, MODEL_NAME, NODE_CAPTION,   
NODE_SUPPORT, [CHILDREN_CARDINALITY], NODE_DESCRIPTION  
FROM Association.CONTENT  
WHERE NODE_TYPE = 1  
```  
  
> [!NOTE]  
>  CHILDREN_CARDINALITY という列名は、MDX の同名の予約済みキーワードと区別するために角かっこで囲む必要があります。  
  
 例の結果を次に示します。  
  
|||  
|-|-|  
|MODEL_CATALOG|Association Test|  
|MODEL_NAME|アソシエーション|  
|NODE_CAPTION|Association Rules Model|  
|NODE_SUPPORT|14879|  
|CHILDREN_CARDINALITY|942|  
|NODE_DESCRIPTION|Association Rules Model; ITEMSET_COUNT=679; RULE_COUNT=263; MIN_SUPPORT=14; MAX_SUPPORT=4334; MIN_ITEMSET_SIZE=0; MAX_ITEMSET_SIZE=3; MIN_PROBABILITY=0.400390625; MAX_PROBABILITY=1; MIN_LIFT=0.14309369632511; MAX_LIFT=1.95758227647523|  
  
 アソシエーション モデル内でのこれらの列の意味については、「 [アソシエーション モデルのマイニング モデル コンテンツ (Analysis Services - データ マイニング)](mining-model-content-for-association-models-analysis-services-data-mining.md)」を参照してください。  
  
 [トップに戻る](#bkmk_top2)  
  
###  <a name="bkmk_Query2"></a> サンプル クエリ 2:スキーマ行セットから追加のメタデータを取得します。  
 データ マイニング スキーマ行セットに対してクエリを実行すると、DMX コンテンツ クエリで返されたのと同じ情報を取得できます。 ただし、スキーマ行セットから返される情報にはいくつかの追加の列があります (モデルが最後に処理された日、マイニング構造、予測可能な属性として使用されている列の名前など)。  
  
```  
SELECT MODEL_CATALOG, MODEL_NAME, SERVICE_NAME, PREDICTION_ENTITY,   
MINING_STRUCTURE, LAST_PROCESSED  
FROM $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = 'Association'  
```  
  
 例の結果を次に示します。  
  
|||  
|-|-|  
|MODEL_CATALOG|Adventure Works DW Multidimensional 2012|  
|MODEL_NAME|アソシエーション|  
|SERVICE_NAME|Association Rules Model|  
|PREDICTION_ENTITY|v Assoc Seq Line Items|  
|MINING_STRUCTURE|アソシエーション|  
|LAST_PROCESSED|9/29/2007 10:21:24 PM|  
  
 [トップに戻る](#bkmk_top2)  
  
###  <a name="bkmk_Query3"></a> サンプル クエリ 3:モデルの元のパラメーターを取得します。  
 次のクエリは、モデルの作成時に使用されたパラメーター設定の詳細を含む 1 つの列を返します。  
  
```  
SELECT MINING_PARAMETERS   
from $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = 'Association'  
```  
  
 例の結果を次に示します。  
  
 MAXIMUM_ITEMSET_COUNT=200000,MAXIMUM_ITEMSET_SIZE=3,MAXIMUM_SUPPORT=1,MINIMUM_SUPPORT=9.40923449156529E-04,MINIMUM_IMPORTANCE=-999999999,MINIMUM_ITEMSET_SIZE=0,MINIMUM_PROBABILITY=0.4  
  
 [トップに戻る](#bkmk_top2)  
  
## <a name="finding-information-about-rules-and-itemsets"></a>ルールとアイテムセットに関する情報の入手  
 アソシエーション モデルの用途としては、頻度の高いアイテムセットに関する情報の検出と、特定のルールやアイテムセットに関する詳細の抽出の 2 つが一般的です。 たとえば、スコアによって特に興味深いとされたルールのリストを抽出したり、最も一般的なアイテムセットのリストを作成したりすることができます。 このような情報を取得するには、DMX コンテンツ クエリを使用します。 **Microsoft アソシエーション ビューアー**を使用してこの情報を参照することもできます。  
  
###  <a name="bkmk_Query4"></a> サンプル クエリ 4:アイテム セットと製品の一覧を取得します。  
 次のクエリは、すべてのアイテムセットを、各アイテムセットに含まれる製品のリストから成る入れ子になったテーブルと共に取得します。 NODE_NAME 列にはモデル内のアイテムセットの一意の ID が、NODE_CAPTION 列にはアイテムの説明テキストが含まれています。 この例では、入れ子になったテーブルがフラット化されているため、アイテムセットに 2 つの製品が含まれている場合は結果に 2 つの行が生成されます。 使用しているクライアントが階層データをサポートしている場合は FLATTENED キーワードを省略できます。  
  
```  
SELECT FLATTENED NODE_NAME, NODE_CAPTION,  
NODE_PROBABILITY, NODE_SUPPORT,  
(SELECT ATTRIBUTE_NAME FROM NODE_DISTRIBUTION) as PurchasedProducts  
FROM Association.CONTENT  
WHERE NODE_TYPE = 7  
```  
  
 例の結果を次に示します。  
  
|||  
|-|-|  
|NODE_NAME|37|  
|NODE_CAPTION|Sport-100 = Existing|  
|NODE_PROBABILITY|0.291283016331743|  
|NODE_SUPPORT|4334|  
|PURCHASEDPRODUCTS.ATTRIBUTE_NAME|v Assoc Seq Line Items(Sport-100)|  
  
 [トップに戻る](#bkmk_top2)  
  
###  <a name="bkmk_Query5"></a> サンプル クエリ 5:上位 10 個のアイテム セットを返す  
 この例は、DMX に既定で用意されているグループ化と順序付けの関数の使用方法を示しています。 このクエリでは、各ノードのサポートで順序付けした場合の上位 10 個のアイテムセットが返されます。 Transact-SQL の場合のように結果を明示的にグループ化する必要はなく、各クエリで集計関数を 1 つ使用するだけで済みます。  
  
```  
SELECT TOP 10 (NODE_SUPPORT),NODE_NAME, NODE_CAPTION  
FROM Association.CONTENT  
WHERE NODE_TYPE = 7  
```  
  
 例の結果を次に示します。  
  
|||  
|-|-|  
|NODE_SUPPORT|4334|  
|NODE_NAME|37|  
|NODE_CAPTION|Sport-100 = Existing|  
  
 [トップに戻る](#bkmk_top2)  
  
## <a name="making-predictions-using-the-model"></a>モデルを使用して予測を行う  
 アソシエーション ルール モデルは、アイテムセットで検出された相関関係に基づく提案を生成するためによく使用されます。 したがって、アソシエーション ルール モデルに基づく予測クエリを作成する際には、そのモデルのルールを使用して新しいデータに基づく推測を行うのが一般的です。  [PredictAssociation (DMX)](/sql/dmx/predictassociation-dmx) は提案を返す関数であり、クエリ結果をカスタマイズするために使用できるいくつかの引数が用意されています。  
  
 アソシエーション モデルに対するクエリは、そのほか、異なるクロスセル戦略の効果を比較できるようにさまざまなルールやアイテムセットの信頼度を取得するためにも使用できます。 以降の例は、このようなクエリの作成方法を示しています。  
  
###  <a name="bkmk_Query6"></a> サンプル クエリ 6:関連付けられているアイテムを予測します。  
 この例では、「[中級者向けデータ マイニング チュートリアル (Analysis Services - データ マイニング)](../../tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md)」で作成したアソシエーション モデルを使用します。 この例は、特定の製品を購入した顧客に対してどの製品を提案すればよいかを示す予測クエリの作成方法を示しています。 このクエリのように、`SELECT...UNION` ステートメントでモデルに値を渡す種類のクエリを、単一クエリと呼びます。 新しい値に対応する予測可能なモデル列は入れ子になったテーブルであるため、1 つの `SELECT` 句を使用して新しい値を入れ子になったテーブル列 (`[Model]`) にマップし、もう 1 つの `SELECT` 句を使用して入れ子になったテーブルの列をケース レベルの列 (`[v Assoc Seq Line Items]`) にマップする必要があります。 キーワード INCLUDE-STATISTICS をクエリに追加すると、提案の確率とサポートも確認できます。  
  
```  
SELECT PredictAssociation([Association].[vAssocSeqLineItems],INCLUDE_STATISTICS, 3)  
FROM [Association]  
NATURAL PREDICTION JOIN   
(SELECT  
(SELECT 'Classic Vest' as [Model])  
AS [v Assoc Seq Line Items])  
AS t  
```  
  
 例の結果を次に示します。  
  
|[モデル]|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Sport-100|4334|0.291283|0.252696|  
|Water Bottle|2866|0.19262|0.175205|  
|Patch kit|2113|0.142012|0.132389|  
  
 [トップに戻る](#bkmk_top2)  
  
###  <a name="bkmk_Query7"></a> サンプル クエリ 7:関連するアイテム セットの信頼度を決定します。  
 提案を生成するにはルールが便利ですが、データセット内のパターンをより深く分析するためにはアイテムセットの方が興味深い対象であると言えます。 たとえば、前のサンプル クエリで返された提案が満足できるものでなかった場合、Product A を含む他のアイテムセットを調べると、Product A があらゆる種類の製品と一緒に購入されるような付属品なのか、それとも特定の製品の購入との間に強い相関関係があるのかがわかります。 これらの関係は、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] アソシエーション ビューアーでアイテムセットにフィルターを適用することによって簡単に調べることができますが、同じ情報をクエリで取得することもできます。  
  
 次のサンプル クエリは、Water Bottle というアイテムを含むすべてのアイテムセットを、単一のアイテムの Water Bottle も含めて返します。  
  
```  
SELECT TOP 100 FROM   
(  
SELECT FLATTENED NODE_CAPTION, NODE_SUPPORT,   
(SELECT ATTRIBUTE_NAME from NODE_DISTRIBUTION  
WHERE ATTRIBUTE_NAME = 'v Assoc Seq Line Items(Water Bottle)') as D  
FROM Association.CONTENT  
WHERE NODE_TYPE = 7  
) AS Items  
WHERE [D.ATTRIBUTE_NAME] <> NULL  
ORDER BY NODE_SUPPORT DESC  
```  
  
 例の結果を次に示します。  
  
|NODE_CAPTION|NODE_SUPPORT|D.ATTRIBUTE_NAME|  
|-------------------|-------------------|-----------------------|  
|Water Bottle = Existing|2866|v Assoc Seq Line Items(Water Bottle)|  
|Mountain Bottle Cage = Existing, Water Bottle = Existing|1136|v Assoc Seq Line Items(Water Bottle)|  
|Road Bottle Cage = Existing, Water Bottle = Existing|1068|v Assoc Seq Line Items(Water Bottle)|  
|Water Bottle = Existing, Sport-100 = Existing|734|v Assoc Seq Line Items(Water Bottle)|  
  
 このクエリでは、条件に一致した入れ子になったテーブルの行と、外部テーブル (ケース テーブル) のすべての行が返されます。 したがって、対象の属性名が NULL 値になっているケース テーブル行を除外する条件を追加する必要があります。  
  
 [トップに戻る](#bkmk_top2)  
  
## <a name="function-list"></a>関数一覧  
 すべての [!INCLUDE[msCoName](../../includes/msconame-md.md)] アルゴリズムでは、共通の関数セットがサポートされています。 ただし、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] アソシエーション アルゴリズムでは、次の表のような追加の関数がサポートされています。  
  
|||  
|-|-|  
|予測関数|使用方法|  
|[IsDescendant &#40;DMX&#41;](/sql/dmx/isdescendant-dmx)|あるノードがニューラル ネットワーク グラフ内の別のノードの子であるかどうかを示します。|  
|[IsInNode &#40;DMX&#41;](/sql/dmx/isinnode-dmx)|指定されたノードが現在のケースを含んでいるかどうかを示します。|  
|[PredictAdjustedProbability &#40;DMX&#41;](/sql/dmx/predictadjustedprobability-dmx)|重み付け確率を返します。|  
|[PredictAssociation &#40;DMX&#41;](/sql/dmx/predictassociation-dmx)|結合データセットのメンバーシップを予測します。|  
|[PredictHistogram &#40;DMX&#41;](/sql/dmx/predicthistogram-dmx)|現在の予測値に関連する値のテーブルを返します。|  
|[PredictNodeId &#40;DMX&#41;](/sql/dmx/predictnodeid-dmx)|各ケースの Node_ID を返します。|  
|[PredictProbability &#40;DMX&#41;](/sql/dmx/predictprobability-dmx)|予測値の確率を返します。|  
|[PredictSupport &#40;DMX&#41;](/sql/dmx/predictsupport-dmx)|指定された状態に対するサポート値を返します。|  
|[PredictVariance (DMX)](/sql/dmx/predictvariance-dmx)|予測値の分散を返します。|  
  
## <a name="see-also"></a>関連項目  
 [Microsoft アソシエーション アルゴリズム](microsoft-association-algorithm.md)   
 [Microsoft アソシエーション アルゴリズム テクニカル リファレンス](microsoft-association-algorithm-technical-reference.md)   
 [アソシエーション モデルのマイニング モデル コンテンツ (Analysis Services - データ マイニング)](mining-model-content-for-association-models-analysis-services-data-mining.md)  
  
  
