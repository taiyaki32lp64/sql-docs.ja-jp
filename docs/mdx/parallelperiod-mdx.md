---
title: ParallelPeriod (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: b4122c13a5371cc0ffe1c5c6235ad750e7fdadad
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68020701"
---
# <a name="parallelperiod-mdx"></a>ParallelPeriod (MDX)


  指定されたメンバーと同じ相対位置で、前の期間からメンバーを返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
ParallelPeriod( [ Level_Expression [ ,Index [ , Member_Expression ] ] ] )  
```  
  
## <a name="arguments"></a>引数  
 *Level_Expression*  
 レベルを返す有効な多次元式 (MDX) 式。  
  
 *Index*  
 さかのぼる並列期間の数を指定する有効な数値式です。  
  
 *メンバー式*  
 メンバーを 1 つ返す有効な多次元式 (MDX) 式です。  
  
## <a name="remarks"></a>コメント  
 似ていますが、[いとこ](../mdx/cousin-mdx.md)関数の場合、 **ParallelPeriod**関数により密接に関連するタイム シリーズ。 **ParallelPeriod**関数指定されたレベルで指定されたメンバーの先祖を受け取り、指定した間隔で、この先祖の兄弟を検索して最後に、指定されたメンバーの間での並列期間を返します、兄弟の子孫です。  
  
 **ParallelPeriod**関数には、次の既定値。  
  
-   既定のメンバー値の型を持つ最初の次元の最初の階層の現在のメンバーは、レベル式もメンバー式が指定されている場合*時間*メジャー グループ内。  
  
-   既定のメンバー値は、レベル式を指定すると、メンバー式が指定されていない場合、 *Level_Expression*.**Hierarchy.CurrentMember**します。  
  
-   既定のインデックス値には 1 です。  
  
-   既定のレベルは、指定されたメンバーの親のレベルです。  
  
 **ParallelPeriod**関数は、次の MDX ステートメントと同等です。  
  
 `Cousin(Member_Expression, Ancestor(Member_Expression, Level_Expression) .Lag(Numeric_Expression))`  
  
## <a name="example"></a>例  
 次の例では、Quarter レベルを基準として、2003 年 10 月から 3 期間さかのぼった並列期間を返します。つまり、2003 年 1 月が返されます。  
  
```  
SELECT ParallelPeriod ([Date].[Calendar].[Calendar Quarter]  
   , 3  
   , [Date].[Calendar].[Month].[October 2003])  
   ON 0  
   FROM [Adventure Works]  
```  
  
 次の例では、Semester  レベルを基準として、2003 年 10 月から 3 期間さかのぼった並列期間を返します。つまり、2002 年 4 月が返されます。  
  
```  
SELECT ParallelPeriod ([Date].[Calendar].[Calendar Semester]  
   , 3  
   , [Date].[Calendar].[Month].[October 2003])  
   ON 0  
   FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>関連項目  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
