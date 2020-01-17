---
title: SELECT (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 8bf766c6f0a7fd757b280b0f950a43cfdc025929
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67928424"
---
# <a name="select-dmx"></a>SELECT (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  **SELECT**データ マイニングでは、次のタスクのデータ マイニング拡張機能 (DMX) ステートメントを使用します。  
  
-   既存のマイニング モデルの内容の参照  
  
-   既存のマイニング モデルからの予測の作成  
  
-   既存のマイニング モデルのコピーの作成  
  
-   マイニング構造の参照  
  
 このステートメントの全構文は複雑なので、モデルとその基になる構造の参照に使用される主な句を次にまとめます。  
  
```  
SELECT [FLATTENED] [TOP <n>] <select list>  
FROM <model/structure>[.aspect]  
[WHERE <condition expression>]  
[ORDER BY <expression>[DESC|ASC]]  
```  
  
## <a name="flattened"></a>FLATTENED  
 データ マイニング クライアントによっては、データ マイニング プロバイダーから階層形式の結果セットを受け取ることができない場合があります。 クライアントが階層を処理できない場合や、結果を 1 つの非正規化テーブルに格納しなければならない場合があります。 入れ子になったテーブルからフラット テーブルにデータを変換するには、クエリ結果を平面化する必要があります。  
  
 クエリの結果をフラット化するには、次の例に示すように **FLATTENED** オプション** を指定して **SELECT** 構文を使用します。  
  
```  
SELECT FLATTENED <select list> FROM ...  
```  
  
## <a name="top-n-and-order-by"></a>TOP \<n > および ORDER BY  
 式を使用してクエリの結果を並べ替えてから、**ORDER BY** 句と **TOP** 句の組み合わせを使用して結果のサブセットを返すことができます。 これは、最も可能性の高い回答者にのみ結果を配信するような配信先指定メーリングなどのシナリオで役に立ちます。 ターゲットメーリング予測クエリの結果を予測確率順に並べてから、上位の \<n > 個の結果のみを返すことができます。  
  
## <a name="select-list"></a>SELECTリスト  
 *\<SELECTリスト>* スカラー列参照、予測関数、および式に含めることができます。 使用できるオプションは、アルゴリズムと以下のコンテキストに依存します。  
  
-   クエリの対象がマイニング構造であるかマイニング モデルであるか  
  
-   クエリの対象がコンテンツであるかケースであるか  
  
-   ソース データがリレーショナル テーブルであるかキューブであるか  
  
-   予測を作成する場合  
  
 多くの場合、別名を使用したり、またはSELECTリストの項目に基づいて単純な式を作成したりできます。 たとえば、次の例は、モデル列の単純な式を示します。  
  
```  
SELECT [CustomerID], [Last Name] + ', ' + [FirstName] AS FullName  
FROM <model>.CASES  
```  
  
 次の例では、予測関数の結果を格納する列の別名を作成します。  
  
```  
SELECT Predict([Column1], 'Value') as Column1Prediction  
FROM MyModel  
JOIN <source data query>  
```  
  
## <a name="where"></a>WHERE  
 **WHERE** 句を使用して、クエリから返されるケースを制限できます。 **WHERE** 句では、**WHERE** 式内の列参照が **SELECT** ステートメントの *\<SELECTリスト>* の列参照と同じ意味を持つ必要があり、ブール式のみを返すことができることを指定します。 **WHERE** 句の構文は次のとおりです。  
  
```  
WHERE < condition expression >  
```  
  
 **SELECT**ステートメントの SELECTリストと**WHERE**句は、次の規則に従う必要があります。  
  
-   SELECTリストには、ブール型の結果を返さない式が含まれている必要があります。 この式は変更することができますが、式はブール型ではない結果を返す必要があります。  
  
-   **WHERE**句は、ブール型の結果を返す式を含める必要があります。 この句は変更することができますが、ブール型の結果を返す必要があります。  
  
## <a name="predictions"></a>予測  
 予測の作成に使用できる構文には 2 つの種類があります。  
  
-   [SELECT FROM&#60;モデル&#62;PREDICTION JOIN &#40;DMX&#41;](../dmx/select-from-model-prediction-join-dmx.md)  
  
-   [SELECT FROM&#60;モデル&#62; &#40;DMX&#41;](../dmx/select-from-model-dmx.md)  
  
 前者の予測では、複雑な予測をリアルタイムで、またはバッチとして作成することができます。  
  
 後者の予測では、マイニング モデル内の予測可能な列に空の予測結合を作成し、列の最も可能性の高い状態を返します。 このクエリの結果は、マイニング モデルの内容に完全に基づいています。  
  
 SELECT FROM PREDICTION JOIN ステートメントのソース クエリに select ステートメントを挿入するには、次の構文を使用します。  
  
```  
SELECT FROM PREDICTION JOIN (<SELECT statement>) AS t, WHERE <SELECT statement>  
```  
  
 予測クエリの作成の詳細については、次を参照してください。[構造と DMX 予測クエリの使用状況](../dmx/structure-and-usage-of-dmx-prediction-queries.md)します。  
  
## <a name="clause-syntax"></a>句の構文  
 **SELECT** ステートメントを使用した参照は複雑なため、詳細な構文要素と引数は句ごとに示されます。 それぞれの句の詳細については、次のリストのトピックをクリックしてください。  
  
 [SELECT DISTINCT FROM&#60;モデル&#62; &#40;DMX&#41;](../dmx/select-distinct-from-model-dmx.md)  
  
 [SELECT FROM<モデル> CONTENT(DMX)](../dmx/select-from-model-content-dmx.md)  
  
 [SELECT FROM<モデル> .CASES(DMX)](../dmx/select-from-model-cases-dmx.md)  
  
 [SELECT FROM<モデル>SAMPLE_CASES(DMX)](../dmx/select-from-model-sample-cases-dmx.md)  
  
 [SELECT FROM<モデル>.DIMENSION_CONTENT(DMX)](../dmx/select-from-model-dimension-content-dmx.md)  
  
 [SELECT FROM&#60;モデル&#62;PREDICTION JOIN &#40;DMX&#41;](../dmx/select-from-model-prediction-join-dmx.md)  
  
 [SELECT FROM&#60;モデル&#62; &#40;DMX&#41;](../dmx/select-from-model-dmx.md)  
  
 [SELECT FROM<構造>.CASES](../dmx/select-from-structure-cases.md)  
  
## <a name="see-also"></a>参照  
 [データ マイニング拡張機能&#40;DMX&#41;データ定義ステートメント](../dmx/dmx-statements-data-definition.md)   
 [データ マイニング拡張機能&#40;DMX&#41;データ操作ステートメント](../dmx/dmx-statements-data-manipulation.md)   
 [データ マイニング拡張機能&#40;DMX&#41;ステートメント リファレンス](../dmx/data-mining-extensions-dmx-statements.md)   
 [データ マイニング拡張機能&#40;DMX&#41;データ操作ステートメント](../dmx/dmx-statements-data-manipulation.md)  
  
  
