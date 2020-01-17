---
title: Avg (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: aa8817e35a589def4631bd455637d05fc62d3a0f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68017009"
---
# <a name="avg-mdx"></a>Avg (MDX)


  セットを評価し、セット内のメジャーまたは指定されたメジャーの平均、セット内のセルの空でない値の平均を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Avg( Set_Expression [ , Numeric_Expression ] )  
```  
  
## <a name="arguments"></a>引数  
 *Set_Expression*  
 セットを返す有効な多次元式 (MDX) 式  
  
 *Numeric_Expression*  
 有効な数値式は、通常、数値を返すセル座標の多次元式 (MDX) 式です。  
  
## <a name="remarks"></a>コメント  
 一連の空の組または空のセットが指定されている場合、 **Avg**関数は空の値を返します。  
  
 **Avg**関数は、最初に、指定されたセット内のセルの値の合計を計算し、空でないセルの数で割って計算された合計で指定されたセット内のセルの空でない値の平均を計算指定されたセット。  
  
> [!NOTE]  
>  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] では、数値セットの平均値が計算される際、NULL 値は無視されます。  
  
 特定の数値式 (通常はメジャー) が指定されていない場合、 **Avg**関数、現在のクエリ コンテキスト内の各メジャーの平均を計算します。 特定のメジャーが指定されている場合、 **Avg**関数はまずセットに対してメジャーを評価し、関数が、指定されたメジャーに基づいて平均値を計算します。  
  
> [!NOTE]  
>  使用する場合、 **CurrentMember**関数で計算されるメンバーのステートメントでは、このようなクエリのコンテキストでは、現在の座標に対する既定のメジャーが存在しないので、数値式を指定する必要があります。  
  
 空のセルを含めることを強制するには、アプリケーションを使用する必要があります、 [CoalesceEmpty](../mdx/coalesceempty-mdx.md)関数かを指定する有効な*Numeric_Expression*空の値のゼロ (0) の値を提供します。 空のセルの詳細については、OLE DB のドキュメントを参照してください。  
  
## <a name="examples"></a>使用例  
 次の例では、指定されたセットに対するメジャーの平均値を返しています。 指定されたメジャーできる指定されたセットのメンバーの既定のメジャーまたは指定されたメジャーのいずれかに注意してください。  
  
 `WITH SET [NW Region] AS`  
  
 `{[Geography].[State-Province].[Washington]`  
  
 `, [Geography].[State-Province].[Oregon]`  
  
 `, [Geography].[State-Province].[Idaho]}`  
  
 `MEMBER [Geography].[Geography].[NW Region Avg] AS`  
  
 `AVG ([NW Region]`  
  
 `--Uncomment the line below to get an average by Reseller Gross Profit Margin`  
  
 `--otherwise the average will be by whatever the default measure is in the cube,`  
  
 `--or whatever measure is specified in the query`  
  
 `--, [Measures].[Reseller Gross Profit Margin]`  
  
 `)`  
  
 `SELECT [Date].[Calendar Year].[Calendar Year].Members ON 0`  
  
 `FROM [Adventure Works]`  
  
 `WHERE ([Geography].[Geography].[NW Region Avg])`  
  
 次の例は、の日次平均を返します、`Measures.[Gross Profit Margin]`から、2003年会計年度の各月の日間にわたって計算、メジャー、 **Adventure Works**キューブ。 **Avg**の各月に含まれている日のセットから平均を計算、`[Ship Date].[Fiscal Time]`階層。 2 番目のバージョンは、売上のない日を平均に含める方法を示しています、計算の最初のバージョンは、平均売上が記録されなかった日を除くで Avg の既定の動作を示します。  
  
 `WITH MEMBER Measures.[Avg Gross Profit Margin] AS`  
  
 `Avg(`  
  
 `Descendants(`  
  
 `[Ship Date].[Fiscal].CurrentMember,`  
  
 `[Ship Date].[Fiscal].[Date]`  
  
 `),`  
  
 `Measures.[Gross Profit Margin]`  
  
 `), format_String='percent'`  
  
 `MEMBER Measures.[Avg Gross Profit Margin Including Empty Days] AS`  
  
 `Avg(`  
  
 `Descendants(`  
  
 `[Ship Date].[Fiscal].CurrentMember,`  
  
 `[Ship Date].[Fiscal].[Date]`  
  
 `),`  
  
 `CoalesceEmpty(Measures.[Gross Profit Margin],0)`  
  
 `), Format_String='percent'`  
  
 `SELECT`  
  
 `{Measures.[Avg Gross Profit Margin],Measures.[Avg Gross Profit Margin Including Empty Days]} ON COLUMNS,`  
  
 `[Ship Date].[Fiscal].[Fiscal Year].Members ON ROWS`  
  
 `FROM`  
  
 `[Adventure Works]`  
  
 `WHERE([Product].[Product Categories].[Product].&[344])`  
  
 次の例は、の日次平均を返します、`Measures.[Gross Profit Margin]`からの 2003年会計年度の各半期に関して日間にわたって計算、メジャー、 **Adventure Works**キューブ。  
  
```  
WITH MEMBER Measures.[Avg Gross Profit Margin] AS  
   Avg(  
      Descendants(  
         [Ship Date].[Fiscal].CurrentMember,   
            [Ship Date].[Fiscal].[Date]  
      ),   
      Measures.[Gross Profit Margin]  
   )  
SELECT  
   Measures.[Avg Gross Profit Margin] ON COLUMNS,  
      [Ship Date].[Fiscal].[Fiscal Year].[FY 2003].Children ON ROWS  
FROM  
   [Adventure Works]  
```  
  
## <a name="see-also"></a>関連項目  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
