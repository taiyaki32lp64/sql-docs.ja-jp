---
title: Descendants (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 2a981595c19c321ab498fe9eb65b8570eb17f3ee
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67999986"
---
# <a name="descendants-mdx"></a>Descendants (MDX)


  他のレベルの子孫を除外したり、指定されたレベルまたは距離にあるメンバーの子孫のセットを返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Member expression syntax using a level expression  
Descendants(Member_Expression [ , Level_Expression [ ,Desc_Flag ] ] )  
  
Member expression syntax using a numeric expression  
Descendants(Member_Expression [ , Distance [ ,Desc_Flag ] ] )  
  
Set expression syntax using a level expression  
Descendants(Set_Expression [ , Level_Expression [ ,Desc_Flag ] ] )  
  
Member expression syntax using a numeric expression  
Descendants(Set_Expression [ , Distance [ ,Desc_Flag ] ] )  
  
```  
  
## <a name="arguments"></a>引数  
 *メンバー式*  
 メンバーを 1 つ返す有効な多次元式 (MDX) 式です。  
  
 *Set_Expression*  
 セットを返す有効な多次元式 (MDX) です。  
  
 *Level_Expression*  
 レベルを返す有効な多次元式 (MDX) 式。  
  
 *Distance*  
 指定されたメンバーからの距離を指定する有効な数値式です。  
  
 *Desc_Flag*  
 子孫のセットを区別するための説明フラグを指定する有効な文字列式です。  
  
## <a name="remarks"></a>コメント  
 レベルが指定されている場合、**Descendants**関数は、指定されたメンバーまたは指定されたフラグによって必要に応じて変更、指定されたレベルに、指定されたセットのメンバーの子孫を含むセットを返します*Desc_Flag*します。  
  
 場合*距離*が指定されている、**Descendants**関数は、指定されたメンバーまたは指定した数のレベルをすぐに指定されたセットのメンバーの子孫を含むセットを返します指定されているフラグによって必要に応じて変更して、指定したメンバーの階層*Desc_Flag*します。 この関数は、不規則階層を対象とする場合に Distance 引数と共に使用されるのが一般的です。 距離に 0 が指定された場合は、指定されたメンバーのみで構成されるセットまたは指定されたセットを返します。  
  
 セット式が指定されている場合、**Descendants**関数が、セットのメンバーごとに個別に解決されると、セットを再作成します。 つまり、使用する構文、**Descendants**関数は、機能的には、MDX[Generate](../mdx/generate-mdx.md)関数。  
  
 関数によって使用されているレベルの既定値は呼び出すことによって決まりますレベルまたは距離が指定されていない場合、[level](../mdx/level-mdx.md)関数 (<\<メンバー >> します。レベル) (メンバーが指定された) 場合は、指定されたメンバーのまたは呼び出すことによって、**レベル**(セットが指定した) 場合に、指定されたセットの各メンバーに対して機能します。 レベル式、距離、フラグを指定しない場合、関数は、次の構文が使用された場合、実行します。  
  
 `Descendants`  
  
 `(`  
  
 `Member_Expression ,`  
  
 `Member_Expression.Level ,`  
  
 `SELF_BEFORE_AFTER`  
  
 `)`  
  
 レベルが指定した説明フラグが指定されていない場合、次の構文が使用された場合と同様、関数を実行します。  
  
 `Descendants`  
  
 `(`  
  
 `Member_Expression ,`  
  
 `Level_Expression,`  
  
 `SELF`  
  
 `)`  
  
 説明フラグの値を変更すると、含めるか、指定されたレベルまたは距離、指定されたレベルまたは (リーフ ノードにある) までの距離の前後の子と、指定されたレベルに関係なくリーフの子の子孫を除外するか、距離です。 次の表に指定できるフラグ、 *Desc_Flag*引数。  
  
|フラグ|説明|  
|----------|-----------------|  
|SELF|指定されたレベルまたは指定された距離にある子孫メンバーのみを返します。 指定されたレベルが、指定されたメンバーのレベルである場合は、指定されたメンバーを含めます。|  
|AFTER|指定されたレベルまたは距離のすべての下位レベルにある子孫メンバーを返します。|  
|BEFORE|指定されたメンバーと指定されたレベルの間、または指定された距離のすべてのレベルにある子孫メンバーを返します。 指定されたメンバーが含まれていますが、指定されたレベルまたは距離からのメンバーは含まれません。|  
|BEFORE_AND_AFTER|すべてのレベルの指定されたメンバーのレベルの下位にある子孫メンバーを返します。 指定されたメンバーは含めますが、指定されたレベルまたは指定された距離にあるメンバーは含めません。|  
|SELF_AND_AFTER|指定されたレベルまたは指定された距離とすべての指定されたレベルを下位レベルで、指定された距離にある子孫メンバーを返します。|  
|SELF_AND_BEFORE|指定されたメンバーと指定されたレベルの間、または指定されたメンバーを含む、指定された距離にある、指定されたレベルまたは指定された距離、およびすべてのレベルからある子孫メンバーを返します。|  
|SELF_BEFORE_AFTER|すべてのレベルから下位指定されたメンバーのレベルにある子孫メンバーを返します、指定されたメンバーが含まれています。|  
|LEAVES|リーフ、指定されたメンバーと指定されたレベルの間、または指定された距離にある子孫メンバーを返します。|  
  
## <a name="examples"></a>使用例  
 次の例では、指定されたメンバー (United States)、および指定されたメンバー (United States) と指定されたレベル (City) の前のレベルのメンバー間にあるメンバーを返しています。この例では、指定されたメンバー自体 (United States)、および State-Province レベル (City レベルの前のレベル) のメンバーが返されます。 この例には、この関数の他の引数を容易にテストできるように、コメント アウトした引数も含まれています。  
  
```  
SELECT Descendants  
   ([Geography].[Geography].[Country].&[United States]  
      //, [Geography].[Geography].[Country]  
   , [Geography].[Geography].[City]  
      //, [Geography].[Geography].Levels (3)  
      //, SELF   
      //, AFTER  
      , BEFORE  
      // BEFORE_AND_AFTER  
      //, SELF_AND_AFTER  
      //, SELF_AND_BEFORE  
      //,SELF_BEFORE_AFTER  
      //,LEAVES   
   ) ON 0  
FROM [Adventure Works]   
```  
  
 次の例は、の日次平均を返します、`Measures.[Gross Profit Margin]`から、2003年会計年度の各月の日間にわたって計算、メジャー、 **Adventure Works**キューブ。 **Descendants**関数の現在のメンバーから判別される日のセットを返します、`[Date].[Fiscal]`階層。  
  
```  
WITH MEMBER Measures.[Avg Gross Profit Margin] AS Avg  
   (  
      Descendants( [Date].[Fiscal].CurrentMember,   
           [Date].[Fiscal].[Date]  
          ),   
        Measures.[Gross Profit Margin]  
   )  
SELECT  
   Measures.[Avg Gross Profit Margin] ON COLUMNS,  
   [Date].[Fiscal].[Month].Members ON ROWS  
FROM [Adventure Works]  
WHERE ([Date].[Fiscal Year].&[2003])  
```  
  
 次の例は、レベル式を使用して、Australia の State-province ごとの Internet Sales Amount を返し、State-province ごと、オーストラリアの合計 Internet Sales Amount の割合を返します。 この例では、Item 関数を使用して、によって返されるセットから最初 (で唯一) の組を抽出、**Ancestors**関数。  
  
```  
WITH MEMBER Measures.x AS   
   [Measures].[Internet Sales Amount] /   
   ( [Measures].[Internet Sales Amount],  
      Ancestors   
         ( [Customer].[Customer Geography].CurrentMember,   
           [Customer].[Customer Geography].[Country]  
         ).Item (0)  
   ), FORMAT_STRING = '0%'  
SELECT {[Measures].[Internet Sales Amount], Measures.x} ON 0,  
{Descendants   
   ( [Customer].[Customer Geography].[Country].&[Australia],   
     [Customer].[Customer Geography].[State-Province], SELF   
   )    
} ON 1  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>関連項目  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
