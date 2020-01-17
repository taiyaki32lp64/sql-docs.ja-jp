---
title: CASE ステートメント (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 756300f1efc93e47a7af3913b34d9318cbe5e559
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68016835"
---
# <a name="case-statement-mdx"></a>CASE ステートメント (MDX)


  複数の比較から、条件付きで特定の値を返します。 case ステートメントには、次の 2 種類があります。  
  
-   一連の特定の値を返す単純な式に式を比較する単純な case ステートメント。  
  
-   検索 case ステートメントは一連の特定の値を返すブール式を評価します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Simple Case Statement  
CASE [input_expression]  
WHEN when_expression THEN when_true_result_expression  
[...n]  
[ELSE else_result_expression]  
END  
  
Search Case Statement  
CASE   
WHEN Boolean_expression THEN when_true_result_expression  
[...n]  
[ELSE else_result_expression]  
END  
```  
  
## <a name="arguments"></a>引数  
 *input_expression*  
 スカラー値に解決される多次元式 (MDX) 式を指定します。  
  
 *when_expression*  
 対象となるスカラー値を指定、 *input_expression*が評価され、true を返しますのスカラー値に評価されると、 *else_result_expression*します。  
  
 *when_true_result_expression*  
 スカラー値が返されるときに、WHEN 句が true に評価されます。  
  
 *else_result_expression*  
 True と評価される WHEN 句がない場合に返されるスカラー値。  
  
 *Boolean_expression*  
 スカラー値に評価される MDX 式です。  
  
## <a name="remarks"></a>コメント  
 ELSE 句がなく、すべての WHEN 句が false に評価される場合は、空のセルになります。  
  
## <a name="simple-case-expression"></a>単純 Case 式  
 MDX は、解決することで単純 case 式を評価、 *input_expression*スカラー値にします。 このスカラー値はのスカラー値と比較し、 *when_expression*します。 CASE ステートメントの値を返します 2 つのスカラー値が一致している場合、 *when_true_expression*します。 2 つのスカラー値が一致しなかった場合は、次の WHEN 句が評価されます。 False の値に評価される WHEN 句のすべてかどうか*else_result_expression*から、ELSE 句が存在する場合が返されます。  
  
 次の例では、句および Reseller Order Count の値に基づいて結果を返しますが各年の測定時に、いくつかに対して Reseller Order Count メジャーが評価されます。 Reseller Order Count 値で指定されたスカラー値と一致しないため、 *when_expression* WHEN 句のスカラー値で、 *else_result_expression*が返されます。  
  
```  
WITH MEMBER [Measures].x AS   
CASE [Measures].[Reseller Order Count]  
   WHEN 0 THEN 'NONE'  
   WHEN 1 THEN 'SMALL'  
   WHEN 2 THEN 'SMALL'  
   WHEN 3 THEN 'MEDIUM'  
   WHEN 4 THEN 'MEDIUM'  
   WHEN 5 THEN 'LARGE'  
   WHEN 6 THEN 'LARGE'  
      ELSE 'VERY LARGE'  
END  
SELECT Calendar.[Calendar Year] on 0  
, NON EMPTY [Geography].[Postal Code].Members ON 1  
FROM [Adventure Works]  
WHERE [Measures].x  
```  
  
## <a name="searched-case-expression"></a>検索 case 式  
 Case 式を使用してより複雑な評価を実行する、検索 case 式を使用します。 検索式の 1 つである検索 case 式を使用すると、入力式が一定範囲内の値であるかどうかを評価できます。 MDX では、これらの句は、CASE ステートメント内に表示される順序で WHEN 句を評価します。  
  
 Reseller Order Count メジャーが評価される次の例では、指定された*Boolean_expression*それぞれ複数の WHEN 句。 年ごとの Reseller Order Count メジャーの値に基づいて、結果が返されます。 句の順序が評価されるタイミングために表示されている 6 簡単に割り当てることができます"VERY LARGE"の値をそれぞれの値を明示的に指定しなくてもより大きいすべての値。 WHEN 句のスカラー値で指定されていない Reseller Order Count 値に対して、 *else_result_expression*が返されます。  
  
```  
WITH MEMBER [Measures].x AS   
CASE   
   WHEN [Measures].[Reseller Order Count] > 6 THEN 'VERY LARGE'  
   WHEN [Measures].[Reseller Order Count] > 4 THEN 'LARGE'  
   WHEN [Measures].[Reseller Order Count] > 2 THEN 'MEDIUM'  
   WHEN [Measures].[Reseller Order Count] > 0 THEN 'SMALL'  
   ELSE "NONE"  
END  
SELECT Calendar.[Calendar Year] on 0,  
NON EMPTY [Geography].[Postal Code].Members on 1  
FROM [Adventure Works]  
WHERE [Measures].x  
```  
  
## <a name="see-also"></a>関連項目  
 [MDX スクリプト ステートメント &#40;MDX&#41;](../mdx/mdx-scripting-statements-mdx.md)  
  
  
