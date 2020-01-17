---
title: Naive Bayes モデルのマイニング モデル コンテンツ (Analysis Services - データ マイニング) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- naive bayes model [Analysis Services]
- Bayesian classifiers
- naive bayes algorithms [Analysis Services]
- mining model content, naive bayes models
ms.assetid: 63fa15b0-e00c-4aa3-aa49-335f5572ff7e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9b899ef4daba73237490d06df58c3447f6b2356d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66083646"
---
# <a name="mining-model-content-for-naive-bayes-models-analysis-services---data-mining"></a>Naive Bayes モデルのマイニング モデル コンテンツ (Analysis Services - データ マイニング)
  このトピックでは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Naive Bayes アルゴリズムを使用するモデルに固有のマイニング モデル コンテンツについて説明します。 すべてのモデルの種類に共通の統計および構造を解釈する方法の説明、およびマイニング モデル コンテンツに関連する用語の一般的な定義については、「 [マイニング モデル コンテンツ (Analysis Services - データ マイニング)](mining-model-content-analysis-services-data-mining.md)」を参照してください。  
  
## <a name="understanding-the-structure-of-a-naive-bayes-model"></a>Naive Bayes モデルの構造について  
 Naive Bayes モデルには、モデルとそのメタデータを表す 1 つの親ノードがあり、その親ノードの下に、選択した予測可能な属性を表す任意の数の独立したツリーがあります。 属性のツリーに加え、各モデルに 1 つ、トレーニング ケースのセットに関する説明的な統計情報を提供するマージナル統計ノード (NODE_TYPE = 26) が含まれます。 詳細については、「 [マージナル統計ノードの情報](#bkmk_margstats)」を参照してください。  
  
 予測可能な属性および値ごとに、モデルでは、さまざまな入力列が特定の予測可能な属性の結果にどのように影響したかを示す情報を含むツリーが出力されます。 各ツリーには、予測可能な属性とその値 (NODE_TYPE = 9) が含まれ、さらに入力属性を表す一連のノード (NODE_TYPE = 10) が含まれます。 一般に入力属性には複数の値が含まれるため、各入力属性 (NODE_TYPE = 10) には、属性の特定の状態にそれぞれ対応する複数の子ノード (NODE_TYPE = 11) を含めることができます。  
  
> [!NOTE]  
>  Naive Bayes モデルでは、連続するデータ型が許可されないため、入力列のすべての値が不連続値または分離された値として処理されます。 値を分離する方法は指定できます。 詳細については、「 [マイニング モデルでの列の分離の変更](change-the-discretization-of-a-column-in-a-mining-model.md)」を参照してください。  
  
 ![単純ベイズのモデル コンテンツの構造体](../media/modelcontentstructure-nb.gif "単純ベイズのモデル コンテンツの構造")  
  
## <a name="model-content-for-a-naive-bayes-model"></a>Naive Bayes モデルのモデル コンテンツ  
 ここでは、マイニング モデル コンテンツの列のうち、Naive Bayes モデルに関連する列についてのみ詳細と例を紹介します。  
  
 ここに記載されていないスキーマ行セットの汎用の列 (MODEL_CATALOG や MODEL_NAME など) の詳細や、マイニング モデルの用語の説明については、「[マイニング モデル コンテンツ (Analysis Services - データ マイニング)](mining-model-content-analysis-services-data-mining.md)」を参照してください。  
  
 MODEL_CATALOG  
 モデルが格納されているデータベースの名前。  
  
 MODEL_NAME  
 モデルの名前。  
  
 ATTRIBUTE_NAME  
 このノードに対応する属性の名前です。  
  
 **モデル ルート** 予測可能な属性の名前。  
  
 **マージナル統計** 適用なし。  
  
 **予測可能な属性** 予測可能な属性の名前。  
  
 **入力属性** 入力属性の名前。  
  
 **入力属性の状態** 入力属性の名前のみ。 状態を取得するには、MSOLAP_NODE_SHORT_CAPTION を使用します。  
  
 NODE_NAME  
 ノードの名前。  
  
 この列には NODE_UNIQUE_NAME と同じ値が格納されます。  
  
 ノードの名前付け規則の詳細については、「 [ノードの名前と ID の使用](#bkmk_nodenames)」を参照してください。  
  
 NODE_UNIQUE_NAME  
 ノードの一意の名前。 一意の名前は、ノード間のリレーションシップに関する情報を示す規則に従って割り当てられます。 ノードの名前付け規則の詳細については、「 [ノードの名前と ID の使用](#bkmk_nodenames)」を参照してください。  
  
 NODE_TYPE  
 Naive Bayes モデルでは、次のノードの種類が出力されます。  
  
|ノードの種類の ID|説明|  
|------------------|-----------------|  
|26 (マージナル統計ノード)|モデルのトレーニング ケースのセット全体を表す統計が含まれます。|  
|9 (予測可能な属性)|予測可能な属性の名前が含まれます。|  
|10 (入力属性)|入力属性列の名前、および属性の値を含む子ノードが含まれます。|  
|11 (入力属性の状態)|特定の出力属性と対になったすべての入力属性の値または分離された値が含まれます。|  
  
 NODE_CAPTION  
 ノードに関連付けられたラベルまたはキャプション。 このプロパティは、主に表示を目的としています。  
  
 **モデル ルート** 空白。  
  
 **マージナル統計** 空白。  
  
 **予測可能な属性** 予測可能な属性の名前。  
  
 **入力属性** 予測可能な属性と現在の入力属性の名前。 例:  
  
 Bike Buyer -> Age  
  
 **入力属性の状態** 予測可能な属性と現在の入力属性の名前、および入力値。 例:  
  
 Bike Buyer -> Age = Missing  
  
 CHILDREN_CARDINALITY  
 ノードが持つ子の数です。  
  
 **モデル ルート** モデル内の予測可能な属性の数に 1 (マージナル統計ノードの分) を加算した数。  
  
 **マージナル統計** 定義上、子はありません。  
  
 **予測可能な属性**  現在の予測可能な属性に関連付けられた入力属性の数。  
  
 **入力属性** 現在の入力属性の不連続値または分離された値の数。  
  
 **入力属性の状態** 常に 0 です。  
  
 PARENT_UNIQUE_NAME  
 親ノードの一意の名前。 親ノードと子ノードの関連付けの詳細については、「 [ノードの名前と ID の使用](#bkmk_nodenames)」を参照してください。  
  
 NODE_DESCRIPTION  
 ノードのキャプションと同じです。  
  
 NODE_RULE  
 ノードのキャプションの XML 表現。  
  
 MARGINAL_RULE  
 ノード ルールと同じです。  
  
 NODE_PROBABILITY  
 このノードに関連付けられている確率。  
  
 **モデル ルート** 常に 0 です。  
  
 **マージナル統計** 常に 0 です。  
  
 **予測可能な属性**  常に 1 です。  
  
 **入力属性** 常に 1 です。  
  
 **入力属性の状態** 現在の値の確率を表す小数値。 親入力属性ノードの下にあるすべての入力属性の状態の値を合計すると 1 になります。  
  
 MARGINAL_PROBABILITY  
 ノードの確率と同じです。  
  
 NODE_DISTRIBUTION  
 ノードの確率ヒストグラムが含まれているテーブル。 詳細については、「 [NODE_DISTRIBUTION テーブル](#bkmk_nodedist)」を参照してください。  
  
 NODE_SUPPORT  
 このノードをサポートするケースの数。  
  
 **モデル ルート** トレーニング データ内のすべてのケースの数。  
  
 **マージナル統計** 常に 0 です。  
  
 **予測可能な属性** トレーニング データ内のすべてのケースの数。  
  
 **入力属性** トレーニング データ内のすべてのケースの数。  
  
 **入力属性の状態** トレーニング データ内のケースのうち、この特定の値のみを含むケースの数。  
  
 MSOLAP_MODEL_COLUMN  
 表示目的で使用されるラベル。 通常、ATTRIBUTE_NAME と同じです。  
  
 MSOLAP_NODE_SCORE  
 モデル内の属性または値の重要度を表します。  
  
 **モデル ルート** 常に 0 です。  
  
 **マージナル統計** 常に 0 です。  
  
 **予測可能な属性**  常に 0 です。  
  
 **入力属性** 現在の予測可能な属性との関連における現在の入力属性の興味深さのスコア。  
  
 **入力属性の状態** 常に 0 です。  
  
 MSOLAP_NODE_SHORT_CAPTION  
 列の名前または値を表すテキスト文字列。  
  
 **モデル ルート** 空白。  
  
 **マージナル統計** 空白。  
  
 **予測可能な属性**  予測可能な属性の名前。  
  
 **入力属性** 入力属性の名前。  
  
 **入力属性の状態** 入力属性の値または分離された値。  
  
##  <a name="bkmk_nodenames"></a> ノードの名前と ID の使用  
 Naive Bayes モデルのノードの名前付けでは、モデル内の情報間のリレーションシップをわかりやすくするために、ノードの種類に関する追加情報が提供されます。 次の表に、さまざまなノードの種類に割り当てられる ID の規則を示します。  
  
|ノードの種類|ノード ID の規則|  
|---------------|----------------------------|  
|モデル ルート (1)|常に 0 です。|  
|マージナル統計ノード (26)|任意の ID 値。|  
|予測可能な属性 (9)|10000000 で始まる 16 進数。<br /><br /> 例:100000001、10000000b です。|  
|入力属性 (10)|2 つの部分で構成される 16 進数。最初の部分は常に 20000000 であり、2 番目の部分は関連する予測可能な属性の 16 進数の識別子で始まります。<br /><br /> 例:20000000b00000000<br /><br /> この場合、関連する予測可能な属性は 10000000b です。|  
|入力属性の状態 (11)|3 つの部分で構成される 16 進数。最初の部分は常に 30000000 であり、2 番目の部分は関連する予測可能な属性の 16 進数の識別子で始まります。3 番目の部分は値の識別子を表します。<br /><br /> 例:30000000b00000000200000000<br /><br /> この場合、関連する予測可能な属性は 10000000b です。|  
  
 これらの ID を使用すると、入力属性と状態を予測可能な属性に関連付けることができます。 たとえば、次のクエリでは、 `TM_NaiveBayes`というモデルについて、入力属性と予測可能な属性の考えられる組み合わせを表すノードの名前とキャプションが返されます。  
  
```  
SELECT NODE_NAME, NODE_CAPTION  
FROM TM_NaiveBayes.CONTENT  
WHERE NODE_TYPE = 10  
```  
  
 期待される結果:  
  
|NODE_NAME|NODE_CAPTION|  
|----------------|-------------------|  
|20000000000000001|Bike Buyer -> Commute Distance|  
|20000000000000002|Bike Buyer -> English Education|  
|20000000000000003|Bike Buyer -> English Occupation|  
|20000000000000009|Bike Buyer -> Marital Status|  
|2000000000000000a|Bike Buyer -> Number Children At Home|  
|2000000000000000b|Bike Buyer -> Region|  
|2000000000000000c|Bike Buyer -> Total Children|  
  
 また、親ノードの ID を使用して子ノードを取得できます。 次のクエリでは、 `Marital Status` 属性の値を含むノードを、各ノードの確率と共に取得します。  
  
```  
SELECT NODE_NAME, NODE_CAPTION, NODE_PROBABILITY  
FROM TM_NaiveBayes.CONTENT  
WHERE NODE_TYPE = 11  
AND [PARENT_UNIQUE_NAME] = '20000000000000009'  
```  
  
> [!NOTE]  
>  PARENT_UNIQUE_NAME という列の名前は、同名の予約済みキーワードと区別するために角かっこで囲む必要があります。  
  
 期待される結果:  
  
|NODE_NAME|NODE_CAPTION|NODE_PROBABILITY|  
|----------------|-------------------|-----------------------|  
|3000000000000000900000000|Bike Buyer -> Marital Status = Missing|0|  
|3000000000000000900000001|Bike Buyer -> Marital Status = S|0.457504004|  
|3000000000000000900000002|Bike Buyer -> Marital Status = M|0.542495996|  
  
##  <a name="bkmk_nodedist"></a> NODE_DISTRIBUTION テーブル  
 入れ子になったテーブル列である NODE_DISTRIBUTION には、通常、ノード内の値の分布に関する統計が含まれます。 Naive Bayes モデルでは、このテーブルは次のノードに対してのみ作成されます。  
  
|ノードの種類|入れ子になったテーブルの内容|  
|---------------|-----------------------------|  
|モデル ルート (1)|空白。|  
|マージナル統計ノード (24)|トレーニング データのセット全体についてのすべての予測可能な属性および入力属性の概要情報が含まれます。|  
|予測可能な属性 (9)|空白。|  
|入力属性 (10)|空白。|  
|入力属性の状態 (11)|予測可能な値と入力属性値のこの特定の組み合わせについてのトレーニング データ内の値の分布を表す統計が含まれます。|  
  
 ノード ID またはノードのキャプションを使用すると、より詳細な情報を取得できます。 たとえば、次のクエリでは、値 `'Marital Status = S'`に関連付けられた入力属性ノードのみについて、NODE_DISTRIBUTION テーブルから特定の列を取得します。  
  
```  
SELECT FLATTENED NODE_CAPTION,  
(SELECT ATTRIBUTE_NAME, ATTRIBUTE_VALUE, [SUPPORT], [PROBABILITY], VALUETYPE  
FROM NODE_DISTRIBUTION) as t  
FROM TM_NaiveBayes.content  
WHERE NODE_TYPE = 11  
AND NODE_CAPTION = 'Bike Buyer -> Marital Status = S'  
```  
  
 期待される結果:  
  
|NODE_CAPTION|T.ATTRIBUTE_NAME|t.ATTRIBUTE_VALUE|t.SUPPORT|t.PROBABILITY|t.VALUETYPE|  
|-------------------|-----------------------|------------------------|---------------|-------------------|-----------------|  
|Bike Buyer -> Marital Status = S|Bike Buyer|Missing|0|0|1|  
|Bike Buyer -> Marital Status = S|Bike Buyer|0|3783|0.472934117|4|  
|Bike Buyer -> Marital Status = S|Bike Buyer|1|4216|0.527065883|4|  
  
 これらの結果の SUPPORT 列の値は、指定した結婚歴に当てはまる顧客のうち、自転車を購入した顧客の数を示します。 PROBABILITY 列には、このノードのみについて計算された各属性値の確率が格納されます。 NODE_DISTRIBUTION テーブルで使用される用語の一般的な定義については、「 [マイニング モデル コンテンツ (Analysis Services - データ マイニング)](mining-model-content-analysis-services-data-mining.md)」を参照してください。  
  
###  <a name="bkmk_margstats"></a> マージナル統計ノードの情報  
 Naive Bayes モデルでは、マージナル統計ノードの入れ子になったテーブルに、トレーニング データのセット全体の値の分布が含まれます。 たとえば、次の表は、 `TM_NaiveBayes`モデルの入れ子になった NODE_DISTRIBUTION テーブルに含まれる統計の一部を示しています。  
  
|ATTRIBUTE_NAME|ATTRIBUTE_VALUE|SUPPORT|PROBABILITY|VARIANCE|VALUETYPE|  
|---------------------|----------------------|-------------|-----------------|--------------|---------------|  
|Bike Buyer|Missing|0|0|0|1|  
|Bike Buyer|0|8869|0.507263784|0|4|  
|Bike Buyer|1|8615|0.492736216|0|4|  
|Marital Status|Missing|0|0|0|1|  
|Marital Status|S|7999|0.457504004|0|4|  
|Marital Status|M|9485|0.542495996|0|4|  
|Total Children|Missing|0|0|0|1|  
|Total Children|0|4865|0.278254404|0|4|  
|Total Children|3|2093|0.119709449|0|4|  
|Total Children|1|3406|0.19480668|0|4|  
  
 マージナル統計ノードには常に予測可能な属性とその取り得る値の説明が含まれるため、`Bike Buyer` 列が含まれます。 表中のその他の列はすべて入力属性を表し、モデルで使用された値と共に表示されています。 値は不足値、不連続値、または分離された値のみになります。  
  
 Naive Bayes モデルでは、連続属性を含めることはできないため、数値データはすべて不連続値 (VALUE_TYPE = 4) または分離された値 (VALUE_TYPE = 5) として表されます。  
  
 トレーニング データには存在しなかった有効な値を表すために、すべての入力属性と出力属性に `Missing` 値 (VALUE_TYPE = 1) が追加されます。 "missing" という文字列と既定の `Missing` 値を区別するように注意する必要があります。 詳細については、「 [不足値 &#40;Analysis Services - データ マイニング&#41;](missing-values-analysis-services-data-mining.md)であらかじめ定義されているフラグに加えて他のモデリング フラグがある場合もあります。  
  
## <a name="see-also"></a>参照  
 [マイニング モデル コンテンツ &#40;Analysis Services - データ マイニング&#41;](mining-model-content-analysis-services-data-mining.md)   
 [データ マイニング モデル ビューアー](data-mining-model-viewers.md)   
 [データ マイニング クエリ](data-mining-queries.md)   
 [Microsoft Naive Bayes アルゴリズム](microsoft-naive-bayes-algorithm.md)  
  
  
