---
title: TopCount (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: d4b91b06470c9cb22e98ac76ea52494728a7ca11
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68893102"
---
# <a name="topcount-dmx"></a>TopCount (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  式によって指定された降順のランクで、指定された件数の上位行を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
TopCount(<table expression>, <rank expression>, <count>)  
```  
  
## <a name="applies-to"></a>適用対象  
 テーブル列参照 > などのテーブルを返す\<式、またはテーブルを返す関数。  
  
## <a name="return-type"></a>戻り値の型  
 \<テーブル式の >  
  
## <a name="remarks"></a>コメント  
 \<Rank expression > 引数によって指定された値によって、 \<テーブル式 > 引数に指定された行に対する順位の降順と、に指定されている最上位の行の数が決まります。\<カウント > 引数が返されます。  
  
 TopCount 関数は、最初に、結合された予測を有効にするために導入されており、一般的には、 **SELECT TOP**句と**ORDER BY**句を含むステートメントと同じ結果を生成します。 予測の数の指定をサポートする**Predict (DMX)** 関数を使用すると、結合された予測のパフォーマンスが向上します。  
  
 ただし、TopCount を使用する必要がある場合もあります。 たとえば、DMX は、サブ select ステートメントの**TOP**修飾子をサポートしていません。 [ &#40;PredictHistogram DMX&#41; ](../dmx/predicthistogram-dmx.md)関数では、 **TOP**の追加もサポートされていません。  
  
## <a name="examples"></a>使用例  
 次の例は、「[基本的なデータマイニングチュートリアル](https://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c)」で作成したアソシエーションモデルに対する予測クエリです。 クエリは同じ結果を返しますが、最初の例では TopCount を使用し、2番目の例では Predict 関数を使用します。  
  
 TopCount の動作を理解するために、入れ子になったテーブルのみを返す予測クエリを最初に実行すると便利な場合があります。  
  
```  
SELECT Predict ([Association].[v Assoc Seq Line Items], INCLUDE_STATISTICS, 10)  
FROM   
     [Association]  
NATURAL PREDICTION JOIN  
SELECT (SELECT 'Women''s Mountain Shorts' as [Model]) AS [v Assoc Seq Line Items]) AS t  
```  
  
> [!NOTE]  
>  この例では、入力値として指定された値には単一引用符が含まれているため、この単一引用符の前にもう 1 つ単一引用符に追加してエスケープする必要があります。 エスケープ文字を挿入するための構文がわからない場合は、予測クエリ ビルダーを使用してクエリを作成できます。 ドロップダウン リストから値を選択すると、必要なエスケープ文字が挿入されます。 詳細については、「[データマイニングデザイナーでの単一クエリの作成](https://docs.microsoft.com/analysis-services/data-mining/create-a-singleton-query-in-the-data-mining-designer)」を参照してください。  
  
 例の結果を次に示します。  
  
|[モデル]|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Sport-100|4334|0.291283016|0.252695851|  
|Water Bottle|2866|0.192620472|0.175205052|  
|Patch kit|2113|0.142012232|0.132389356|  
|Mountain Tire Tube|1992|0.133879965|0.125304948|  
|Mountain-200|1755|0.117951475|0.111260823|  
|Road Tire Tube|1588|0.106727603|0.101229538|  
|Cycling Cap|1473|0.098998589|0.094256014|  
|Fender Set - Mountain|1415|0.095100477|0.090718432|  
|Mountain Bottle Cage|1367|0.091874454|0.087780332|  
|Road Bottle Cage|1195|0.080314537|0.077173962|  
  
 TopCount 関数は、このクエリの結果を受け取り、指定された数の最小値の行を返します。  
  
```  
SELECT   
TopCount  
    (  
    Predict ([Association].[v Assoc Seq Line Items],INCLUDE_STATISTICS,10),  
    $SUPPORT,  
    3)  
FROM   
     [Association]  
NATURAL PREDICTION JOIN  
(SELECT (SELECT 'Women''s Mountain Shorts' as [Model]) AS [v Assoc Seq Line Items]) AS t  
```  
  
 TopCount 関数の最初の引数は、テーブル列の名前です。 この例では、Predict 関数を呼び出し、INCLUDE_STATISTICS 引数を使用して、入れ子になったテーブルが返されます。  
  
 TopCount 関数の2番目の引数は、結果の並べ替えに使用する入れ子になったテーブルの列です。 この例では、INCLUDE_STATISTICS オプションによって $SUPPORT 列、$PROBABILTY 列、および $ADJUSTED PROBABILITY 列が返されます。 この例では、$SUPPORT を使用して結果に順位を付けます。  
  
 3番目の引数、TopCount 関数は、返される行の数を整数として指定します。 $SUPPORT で順位が付けられた上位 3 製品を取得するには、「3」と入力します。  
  
 例の結果を次に示します。  
  
|[モデル]|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Sport-100|4334|0.29...|0.25...|  
|Water Bottle|2866|0.19...|0.17...|  
|Patch kit|2113|0.14...|0.13...|  
  
 ただし、この種のクエリは、実稼働設定でのパフォーマンスに影響する可能性があります。 これは、クエリによってアルゴリズムからすべての予測のセットが返され、これらの予測が並べ替えられて上位 3 件が返されるためです。  
  
 次の例は、同じ結果を返すが実行時間が大幅に短縮される代替ステートメントを示しています。 この例では、TopCount を、引数として複数の予測を受け取る Predict 関数に置き換えます。 また、この例では、 **$SUPPORT**キーワードを使用して、入れ子になったテーブル列を直接取得します。  
  
```  
SELECT Predict ([Association].[v Assoc Seq Line Items], INCLUDE_STATISTICS, 3, $SUPPORT)  
```  
  
 結果には、サポート値に基づいて並べ替えられた上位 3 件の予測が含まれます。 $SUPPORT を $PROBABILITY または $ADJUSTED_PROBABILITY に置き換えると、確率または調整済みの確率で順位付けされた予測を取得できます。 詳細については、「 **Predict (DMX)** 」を参照してください。  
  
## <a name="see-also"></a>参照  
 [DMX &#40;関数&#41;](../dmx/functions-dmx.md)   
 [一般的な予測&#40;関数 DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [DMX 数&#40;の合計&#41;](../dmx/bottomcount-dmx.md)   
 [TopPercent &#40;DMX&#41;](../dmx/toppercent-dmx.md)   
 [TopSum &#40;DMX&#41;](../dmx/topsum-dmx.md)  
  
  
