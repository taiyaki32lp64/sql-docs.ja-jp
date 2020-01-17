---
title: '[モデル&lt;&gt;から] を選択します。コンテンツ (DMX) |Microsoft Docs'
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 61cbacee45147b7b6203e9cb2164c02cdc2c7453
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68892831"
---
# <a name="select-from-ltmodelgtcontent-dmx"></a>[モデル&lt;&gt;から] を選択します。コンテンツ (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  指定されたデータ マイニング モデルのマイニング モデル スキーマ行セットを返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
SELECT [FLATTENED] [TOP <n>] <expression list> FROM <model>.CONTENT   
[WHERE <condition expression>]  
[ORDER BY <expression> [DESC|ASC]]  
```  
  
## <a name="arguments"></a>引数  
 *n*  
 任意。 返す行数を指定する整数値です。  
  
 *式の一覧*  
 Content スキーマ行セットから派生する、列のコンマ区切りのリストです。  
  
 *model*  
 モデル識別子です。  
  
 *条件式*  
 任意。 列のリストから返される値を制限する条件です。  
  
 *式 (expression)*  
 任意。 スカラー値を返す式。  
  
## <a name="remarks"></a>コメント  
 **SELECT**  _FROM\<model >_ **。CONTENT**ステートメントでは、各アルゴリズムに固有のコンテンツが返されます。 たとえば、カスタム アプリケーション内のアソシエーション ルール モデルに関するすべてのルールの記述を使用する場合があります。 **[モデルから\<選択] > を使用できます。** モデルの NODE_RULE 列の値を返すコンテンツステートメント。  
  
 次の表に、マイニング モデル コンテンツに含まれる列を示します。  
  
> [!NOTE]  
>  アルゴリズムでは、コンテンツを適切に表すため、列の解釈が異なる場合があります。 各アルゴリズムのマイニングモデルコンテンツの説明、および各種類のモデルのマイニングモデルコンテンツの解釈とクエリの方法に関するヒントについては、「[マイニングモデルコンテンツ&#40;Analysis Services&#41;-データマイニング](https://docs.microsoft.com/analysis-services/data-mining/mining-model-content-analysis-services-data-mining)」を参照してください。  
  
|CONTENT 行セット列|説明|  
|---------------------------|-----------------|  
|MODEL_CATALOG|カタログ名です。 プロバイダーがカタログをサポートしない場合は NULL です。|  
|MODEL_SCHEMA|修飾されていないスキーマ名です。 プロバイダーがスキーマをサポートしない場合は NULL です。|  
|MODEL_NAME|モデル名です。 この列に NULL を含むことはできません。|  
|ATTRIBUTE_NAME|ノードに対応する属性の名前です。|  
|NODE_NAME|ノードの名前。|  
|NODE_UNIQUE_NAME|モデル内のノードの一意な名前です。|  
|NODE_TYPE|ノードの種類を表す整数です。 .|  
|NODE_GUID|ノードの GUID です。 GUID がない場合は NULL です。|  
|NODE_CAPTION|ノードに関連付けられているラベルまはたキャプションです。 主に表示のために使用されます。 キャプションが存在しない場合は、NODE_NAME を返します。|  
|CHILDREN_CARDINALITY|ノードが持つ子の数です。|  
|PARENT_UNIQUE_NAME|ノードの親の一意な名前です。|  
|NODE_DESCRIPTION|ノードの説明です。|  
|NODE_RULE|ノードに埋め込まれたルールを表す XML フラグメントです。 XML 文字列の形式は PMML 標準規格に基づいています。|  
|MARGINAL_RULE|親ノードからノードまでのパスを表す XML フラグメントです。|  
|NODE_PROBABILITY|パスの末尾がノードになる確率です。|  
|MARGINAL_PROBABILITY|親ノードからノードに到達する確率です。|  
|NODE_DISTRIBUTION|ノード内の値の分布を表す統計を含むテーブルです。|  
|NODE_SUPPORT|このノードをサポートするケース数です。|  
  
## <a name="examples"></a>使用例  
 次のコードでは、Targeted Mailing マイニング構造に追加されたデシジョン ツリー モデルの親ノードの ID を返します。  
  
```  
SELECT MODEL_NAME, NODE_NAME FROM [TM Decision Tree].CONTENT  
WHERE NODE_TYPE = 1  
```  
  
 期待される結果:  
  
|MODEL_NAME|NODE_NAME|  
|-----------------|----------------|  
|TM_DecisionTree|0|  
  
 次のクエリでは、 **Isdescendant**関数を使用して、前のクエリで返されたノードの直下の子を返します。  
  
> [!NOTE]  
>  NODE_NAME の値は文字列であるため、サブ select ステートメントを使用して NODE_ID を**Isdescendant**関数の引数として返すことはできません。  
  
```  
SELECT NODE_NAME, NODETYPE, NODE_CAPTION   
FROM [TM Decision Tree].CONTENT  
WHERE ISDESCENDANT('0')  
```  
  
 期待される結果:  
  
 モデルがデシジョン ツリー モデルであるため、モデルの親ノードの子孫には、1 つのマージナル統計ノード、予測可能な属性を表すノード、および入力属性と入力値を含む複数のノードが含まれています。 詳細については、「 [デシジョン ツリー モデルのマイニング モデル コンテンツ &#40;Analysis Services - データ マイニング&#41;](https://docs.microsoft.com/analysis-services/data-mining/mining-model-content-for-decision-tree-models-analysis-services-data-mining)」を参照してください。  
  
## <a name="using-the-flattened-keyword"></a>FLATTENED キーワードの使用  
 多くの場合、マイニング モデル コンテンツには、入れ子になったテーブル列のモデルに関する有用な情報が含まれています。 FLATTENED キーワードを使用すると、階層的な行セットをサポートするプロバイダーを使用しなくても、入れ子になったテーブル列からデータを取得することができます。  
  
 次のクエリでは、Naive Bayes モデルからマージナル統計ノード (NODE_TYPE = 26) という 1 つのノードが返されます。 ただし、このノードには、NODE_DISTRIBUTION 列の入れ子になったテーブルが含まれています。 その結果、入れ子になったテーブル列がフラット化され、入れ子になったテーブルの行ごとに 1 つの行が返されます。 スカラー列 MODEL_NAME の値は、入れ子になったテーブルの各行に繰り返し表示されます。  
  
 また、入れ子になったテーブル列の名前だけを指定した場合は、入れ子になったテーブルの各列に新しい列が返されることにも注意してください。 既定では、入れ子になったテーブルの名前が、入れ子になったテーブル列それぞれの名前の先頭に含まれます。  
  
```  
SELECT FLATTENED MODEL_NAME, NODE_DISTRIBUTION  
FROM [TM_NaiveBayes].CONTENT  
WHERE NODE_TYPE = 26  
```  
  
 例の結果を次に示します。  
  
|MODEL_NAME|NODE_DISTRIBUTION.ATTRIBUTE_NAME|NODE_DISTRIBUTION.ATTRIBUTE_VALUE|NODE_DISTRIBUTION.SUPPORT|NODE_DISTRIBUTION.PROBABILITY|NODE_DISTRIBUTION.VARIANCE|NODE_DISTRIBUTION.VALUETYPE|  
|-----------------|----------------------------------------|-----------------------------------------|--------------------------------|------------------------------------|---------------------------------|----------------------------------|  
|TM_NaiveBayes|Bike Buyer|Missing|0|0|0|1|  
|TM_NaiveBayes|Bike Buyer|0|6556|0.506685215240745|0||  
|TM_NaiveBayes|Bike Buyer|1|6383|0.493314784759255|0||  
  
 次の例は、下位選択ステートメントを使用して、入れ子になったテーブルから一部の列のみを返す方法を示しています。 次に示すように、入れ子になったテーブルの名前に別名を付けることで表示を簡略化できます。  
  
```  
SELECT MODEL_NAME,   
(SELECT ATTRIBUTE_NAME, ATTRIBUTE_VALUE, [SUPPORT] AS t  
FROM NODE_DISTRIBUTION)   
FROM TM_NaiveBayes.CONTENT  
WHERE NODE_TYPE = 26  
```  
  
 例の結果を次に示します。  
  
|MODEL_NAME|T.ATTRIBUTE_NAME|t.ATTRIBUTE_VALUE|t.SUPPORT|  
|-----------------|-----------------------|------------------------|---------------|  
|TM_NaiveBayes|Bike Buyer|Missing|0|  
|TM_NaiveBayes|Bike Buyer|0|6556|  
|TM_NaiveBayes|Bike Buyer|1|6383|  
  
## <a name="see-also"></a>参照  
 [SELECT&#40;DMX&#41;](../dmx/select-dmx.md)   
 [データマイニング拡張&#40;機能&#41; DMX データ操作ステートメント](../dmx/dmx-statements-data-manipulation.md)   
 [データ マイニング拡張機能 &#40;DMX&#41; ステートメント リファレンス](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
