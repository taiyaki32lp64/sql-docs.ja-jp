---
title: 下% (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 9d8b1665c6e6978af7dc673f7dd51a363da5c48d
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68892877"
---
# <a name="bottompercent-dmx"></a>BottomPercent (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  累積合計が指定された割合以上になるテーブルの最下位行を、ランクの増加順 (昇順) に返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
BottomPercent(<table expression>, <rank expression>, <percent>)  
```  
  
## <a name="arguments"></a>引数  
 *\<テーブル式の >*  
 入れ子になったテーブル列またはテーブル値式の名前です。  
  
 *\<順位付け式 >*  
 入れ子になったテーブル列、または結果が列になる式です。  
  
 *\<> の割合*  
 対象全体の比率を示す倍精度浮動小数点数です。  
  
## <a name="result-type"></a>結果の種類  
 テーブルです。  
  
## <a name="remarks"></a>コメント  
 Bottom **percent**関数は、順位の昇順で一番下の行を返します。 ランクは、各行の順位式 > 引数の\<評価値に基づいています。これにより、 \<順位付け式 > 値の合計が、 \<パーセントで指定されているパーセント値以上になるようになり >引数. 下の**パーセント**は、指定された割合の値を維持しながら、可能な限り最小の要素数を返します。  
  
## <a name="examples"></a>使用例  
 次の例では、「[基本的なデータマイニングチュートリアル](https://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c)」で作成したアソシエーションモデルに対して予測クエリを作成します。  
  
 下位パーセントの動作を理解するには、入れ子になったテーブルのみを返す予測クエリを最初に実行すると便利な場合があります。  
  
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
  
 一番下の関数は、このクエリの結果を取得し、指定された割合に合計する最小値の行を返します。  
  
```  
SELECT   
BottomPercent  
    (  
    Predict ([Association].[v Assoc Seq Line Items],INCLUDE_STATISTICS,10),  
    $SUPPORT,  
    50)  
FROM   
     [Association]  
NATURAL PREDICTION JOIN  
(SELECT (SELECT 'Women''s Mountain Shorts' as [Model]) AS [v Assoc Seq Line Items]) AS t  
```  
  
 一番下の引数は、テーブル列の名前です。 この例では、Predict 関数を呼び出し、INCLUDE_STATISTICS 引数を使用して、入れ子になったテーブルが返されます。  
  
 下の2番目の引数は、結果の並べ替えに使用する入れ子になったテーブル内の列です。 この例では、INCLUDE_STATISTICS オプションによって $SUPPORT 列、$PROBABILTY 列、および $ADJUSTED PROBABILITY 列が返されます。 この例では、$SUPPORT を使用しています。サポート値は小数ではないため、検証しやすいからです。  
  
 下の3番目の引数は、パーセントを double として指定します。 サポートの下位の 50% を表す行を取得するには「50」と入力します。  
  
 例の結果を次に示します。  
  
|[モデル]|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Road Bottle Cage|1195|0.080314537|0.077173962|  
|Mountain Bottle Cage|1367|0.091874454|0.087780332|  
|Fender Set - Mountain|1415|0.095100477|0.090718432|  
|Cycling Cap|1473|0.098998589|0.094256014|  
|Road Tire Tube|1588|0.106727603|0.101229538|  
|Mountain-200|1755|0.117951475|0.111260823|  
|Mountain Tire Tube|1992|0.133879965|0.125304948|  
  
 **メモ**この例は、下端% の使用方法を示すためだけに提供されています。 データセットのサイズに応じて、このクエリの実行には長い時間がかかる場合があります。  
  
> [!WARNING]  
>  TOPPERCENT および BOTTOMPERCENT の MDX 関数は、比率の計算に使用される値に負の数が含まれていた場合に、予期しない結果を生成する場合があります。 この動作は、DMX 関数には影響しません。 詳細については、「 [ &#40;MDX&#41;の割合](../mdx/bottompercent-mdx.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [データマイニング拡張&#40;機能&#41; DMX 関数リファレンス](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [DMX &#40;関数&#41;](../dmx/functions-dmx.md)  
  
  
