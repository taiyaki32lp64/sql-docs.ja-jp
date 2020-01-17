---
title: VisualTotals (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: a5becd3382f07a9adc89055a253235495a7e50a8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68125840"
---
# <a name="visualtotals-mdx"></a>VisualTotals (MDX)


  指定されたセットの子メンバーの合計を動的に算出することによって生成したセットを返します。結果セット内で親メンバーの名前に対してパターンを使用することも可能です。  
  
## <a name="syntax"></a>構文  
  
```  
  
VisualTotals(Set_Expression[,Pattern])  
```  
  
## <a name="arguments"></a>引数  
 *Set_Expression*  
 セットを返す有効な多次元式 (MDX) です。  
  
 *パターン*  
 親の名前を置き換える文字のアスタリスク (*) を格納した、セットの親メンバーを表す有効な文字列式です。  
  
## <a name="remarks"></a>コメント  
 指定されたセット式には、1 つのディメンション内の任意のレベルのメンバー、一般に、先祖と子孫のリレーションシップを持つメンバーを含むセットを指定できます。 **VisualTotals**関数が、指定されたセット内の子メンバーの値を合計し、結果の合計を計算するセットに含まれていない子メンバーは無視されます。 階層の順序で並べられたセットの合計が算出されます。 セット内のメンバーの順序と階層の順序が一致しない場合、結果は表示部分の合計になりません。 たとえば、VisualTotals (USA, WA, CA, Seattle) は WA を Seattle として返すのではなく、WA、CA、および Seattle の値を返してから、これらの値の合計を USA の表示部分の合計として算出します。このため、Seattle の売上は 2 回加算されることになります。  
  
> [!NOTE]  
>  適用、 **VisualTotals**メジャーに関連していない、またはメジャー グループの粒度でディメンション メンバーへの関数と、値を null に置き換えられます。  
  
 *パターン*、これは省略可能なには、合計ラベルの形式を指定します。 *パターン*の親メンバーと、残りの部分文字列内のテキストの置換文字は、親の名前と連結されて結果に表示される、アスタリスク (*) が必要です。 リテラルのアスタリスクを表示するには、2 つのアスタリスクを使用 (\*\*)。  
  
## <a name="examples"></a>使用例  
 2001 年の第 3 四半期の表示部分の合計が 1 つの子孫に基づく次の例を返します指定 - 7 月。  
  
```  
SELECT VisualTotals  
   ({[Date].[Calendar].[Calendar Quarter].&[2001]&[3]  
      ,[Date].[Calendar].[Month].&[2001]&[7]}) ON 0  
FROM [Adventure Works]  
```  
  
 次の例では、と共に 2 つの 4 つの子の Product ディメンションに Category 属性階層の [All] メンバーを返します。 Internet Sales Amount メジャーについて [All] メンバーに対して返される合計は、Accessories メンバーと Clothing メンバーのみの合計になります。 また、[All Products] 列のラベルを指定するために、Pattern 引数が使用されています。  
  
```  
SELECT  
   VisualTotals  
   ({[Product].[Category].[All Products]  
      ,[Product].[Category].[Accessories]  
      ,[Product].[Category].[Clothing]}  
      , '* - Visual Total'  
   ) ON Columns  
, [Measures].[Internet Sales Amount] ON Rows  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>関連項目  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
