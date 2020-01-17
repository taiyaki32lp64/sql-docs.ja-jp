---
title: Aggregate (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 6c75ab71456dc8b7ffc3efdf6bd157693de14881
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68017171"
---
# <a name="aggregate-mdx"></a>Aggregate (MDX)


  セット式によって返されるセルを集計することによって計算される数値を返します。 数値式が指定されていない場合は、メジャーごとに指定されている既定の集計演算子を使用して、現在のクエリ コンテキスト内で各メジャーを集計します。 数値式が指定されている場合、この関数は最初に評価されるを合計し、指定されたセット内の各セルの数値式。  
  
## <a name="syntax"></a>構文  
  
```  
  
Aggregate(Set_Expression [ ,Numeric_Expression ])  
```  
  
## <a name="arguments"></a>引数  
 *Set_Expression*  
 セットを返す有効な多次元式 (MDX) です。  
  
 *Numeric_Expression*  
 有効な数値式は、通常、数値を返すセル座標の多次元式 (MDX) 式です。  
  
## <a name="remarks"></a>コメント  
 一連の空の組または空のセットが指定されている場合、この関数は空の値を返します。  
  
 表で説明する方法、**集計**関数は、各種集計関数の動作します。  
  
|集計演算子|結果|  
|--------------------------|------------|  
|Sum|セット全体の値の合計を返します。|  
|Count|セット全体の値の数を返します。|  
|Max|セット全体の最大値を返します。|  
|Min|セット全体の最小値を返します。|  
|準加法集計関数|時間軸に図形を投影してから、セットに対して準加法の動作の計算を返します。|  
|Distinct Count|スライサー軸にセットが含まれている場合は、サブキューブに関与するファクト データ全体で集計します。<br /><br /> セットのメンバーごとに個別のカウントを返します。 結果は、集計されるセルおよび計算のために必要なセルのセキュリティではなく、セキュリティに依存します。 セットにセル セキュリティが指定されているとエラーが生成されますが、指定されているセットの粒度より下位のセル セキュリティは無視されます。 セットに関する計算では、エラーを生成します。 セットの粒度よりも下位の計算は無視されます。 1 つのメンバーとそのメンバーの子が 1 つ以上含まれているセット全体に対する個別カウントは、子メンバーに関与するファクト全体の個別カウントになります。|  
|集計できない属性|値の合計を返します。|  
|集計関数の混合|サポートされており、エラーが発生しません。|  
|単項演算子|影響しません。値は合計を算出することによって集計されます。|  
|計算されるメジャー|解決順序が計算されるメジャーに適用されるように設定します。|  
|計算されるメンバー|通常の規則の適用、つまり、最後の解決順序が優先されます。|  
|代入|メジャーの集計関数に従って集計の割り当てです。 メジャー集計関数が個別カウントの場合、代入の合計が算出されます。|  
  
## <a name="examples"></a>使用例  
 次の例の合計を返して、`Measures.[Order Quantity]`に含まれている 2003 年の最初の 8 月にわたり、メンバー、`Date`ディメンションから、 **Adventure Works**キューブ。  
  
```  
WITH MEMBER [Date].[Calendar].[First8Months2003] AS  
    Aggregate(  
        PeriodsToDate(  
            [Date].[Calendar].[Calendar Year],   
            [Date].[Calendar].[Month].[August 2003]  
        )  
    )  
SELECT   
    [Date].[Calendar].[First8Months2003] ON COLUMNS,  
    [Product].[Category].Children ON ROWS  
FROM  
    [Adventure Works]  
WHERE  
    [Measures].[Order Quantity]  
```  
  
 次の例の 2003 年下半期の最初の 2 か月集計します。  
  
```  
WITH MEMBER [Date].[Calendar].[First2MonthsSecondSemester2003] AS  
    Aggregate(  
        PeriodsToDate(  
            [Date].[Calendar].[Calendar Semester],   
            [Date].[Calendar].[Month].[August 2003]  
        )  
    )  
SELECT   
    [Date].[Calendar].[First2MonthsSecondSemester2003] ON COLUMNS,  
    [Product].[Category].Children ON ROWS  
FROM  
    [Adventure Works]  
WHERE  
    [Measures].[Order Quantity]  
```  
  
 次の例では、ユーザーが選択した State-province メンバー値に基づいて集計関数を使用して評価前の期間にわたって売上を辞退再販業者の数を返します。 **Hierarchize**と**DrillDownLevel**関数を使用して、Product ディメンションに製品カテゴリに関して減少した売上の値を返します。  
  
```  
WITH MEMBER Measures.[Declining Reseller Sales] AS   
   Count(  
      Filter(  
         Existing(Reseller.Reseller.Reseller),   
            [Measures].[Reseller Sales Amount] < ([Measures].[Reseller Sales Amount],  
            [Date].Calendar.PrevMember)  
            )  
         )  
MEMBER [Geography].[State-Province].x AS   
   Aggregate (   
      {[Geography].[State-Province].&[WA]&[US],   
      [Geography].[State-Province].&[OR]&[US] }   
         )  
SELECT NON EMPTY Hierarchize (  
   AddCalculatedMembers (  
      {DrillDownLevel({[Product].[All Products]})}  
         )  
   )  
        DIMENSION PROPERTIES PARENT_UNIQUE_NAME ON COLUMNS   
FROM [Adventure Works]  
WHERE ([Geography].[State-Province].x,   
    [Date].[Calendar].[Calendar Quarter].&[2003]&[4],  
    [Measures].[Declining Reseller Sales])  
```  
  
## <a name="see-also"></a>関連項目  
 [PeriodsToDate &#40;MDX&#41;](../mdx/periodstodate-mdx.md)   
 [Children &#40;MDX&#41;](../mdx/children-mdx.md)   
 [Hierarchize &#40;MDX&#41;](../mdx/hierarchize-mdx.md)   
 [Count &#40;Set&#41; &#40;MDX&#41;](../mdx/count-set-mdx.md)   
 [Filter &#40;MDX&#41;](../mdx/filter-mdx.md)   
 [AddCalculatedMembers &#40;MDX&#41;](../mdx/addcalculatedmembers-mdx.md)   
 [DrilldownLevel &#40;MDX&#41;](../mdx/drilldownlevel-mdx.md)   
 [Properties &#40;MDX&#41;](../mdx/properties-mdx.md)   
 [PrevMember &#40;MDX&#41;](../mdx/prevmember-mdx.md)   
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
