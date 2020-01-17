---
title: TopSum (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 373fe2f1458b30412f4ee5852baa57b930af4878
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68893042"
---
# <a name="topsum-dmx"></a>TopSum (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  累積合計が指定された値以上になるテーブルの最上位行を、ランクの減少順 (降順) に返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
TopSum(<table expression>, <rank expression>, <sum>)  
```  
  
## <a name="applies-to"></a>適用対象  
 テーブル列参照 > などのテーブルを返す\<式、またはテーブルを返す関数。  
  
## <a name="return-type"></a>戻り値の型  
 \<テーブル式の >  
  
## <a name="remarks"></a>コメント  
 **TopSum**関数は、各行の rank 式 > 引数の\<評価値に基づいて、順位の降順で上位の行を返します。これは、 \<ランク式 > 値の合計が少なくとも指定された値であることを示します。合計 > 引数によって\<指定された合計。 **TopSum**は、指定された合計値を維持しながら、可能な限り最小の要素数を返します。  
  
## <a name="examples"></a>使用例  
 次の例では、「[基本的なデータマイニングチュートリアル](https://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c)」を使用して作成したアソシエーションモデルに対して予測クエリを作成します。  
  
 TopPercent の動作を理解するために、入れ子になったテーブルのみを返す予測クエリを最初に実行すると便利な場合があります。  
  
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
  
 **TopSum**関数は、このクエリの結果を受け取り、最大値が指定された行数になる行を返します。  
  
```  
SELECT   
TopSum  
    (  
    Predict([Association].[v Assoc Seq Line Items],INCLUDE_STATISTICS,10),  
    $PROBABILITY,  
    .5)  
FROM   
     [Association]  
NATURAL PREDICTION JOIN  
(SELECT (SELECT 'Women''s Mountain Shorts' as [Model]) AS [v Assoc Seq Line Items]) AS t  
```  
  
 **TopSum**関数の最初の引数は、テーブル列の名前です。 この例では、Predict 関数を呼び出し、INCLUDE_STATISTICS 引数を使用して、入れ子になったテーブルが返されます。  
  
 **TopSum**関数の2番目の引数は、結果の並べ替えに使用する入れ子になったテーブルの列です。 この例では、INCLUDE_STATISTICS オプションによって $SUPPORT 列、$PROBABILTY 列、および $ADJUSTED PROBABILITY 列が返されます。 この例では $PROBABILITY を使用して、合計して 50% 以上の確率になる行を返します。  
  
 3番目の引数、 **TopSum**関数は、ターゲットの合計を double として指定します。 合計が 50% の確率となる上位の製品の行を取得するには「5」と入力します。  
  
 例の結果を次に示します。  
  
|[モデル]|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Sport-100|4334|0.29...|0.25...|  
|Water Bottle|2866|0.19...|0.17...|  
|Patch kit|2113|0.14...|0.13...|  
  
 **メモ**この例は、 **TopSum**の使用方法を示すことだけを目的としています。 データセットのサイズに応じて、このクエリの実行には長い時間がかかる場合があります。  
  
## <a name="see-also"></a>参照  
 [DMX &#40;関数&#41;](../dmx/functions-dmx.md)   
 [一般的な予測&#40;関数 DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [TopPercent &#40;DMX&#41;](../dmx/toppercent-dmx.md)  
  
  
