---
title: ディメンション式の使用 |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 0373bbda2d0c97946f15e048b7cc49175ca66669
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68097173"
---
# <a name="using-dimension-expressions"></a>ディメンション式の使用


  通常使用するディメンションと階層式で多次元式 (MDX) 関数にパラメーターを渡すときに、階層のメンバー、セット、または組を返します。  
  
 ディメンション式は、オブジェクト識別子であるために、単純な式を指定のみできます。 参照してください[式&#40;MDX&#41; ](../mdx/expressions-mdx.md)単純および複雑な式の詳細についてはします。  
  
## <a name="dimension-expressions"></a>ディメンション式  
 ディメンション式には、ディメンション識別子またはディメンション関数のいずれかが含まれます。  
  
 ディメンション式が自身でほとんど使用しません。 代わりに、ディメンションに階層を指定するは、通常はたいです。 唯一の例外は、Measures ディメンションを操作している場合です。このディメンションには階層がありません。  
  
 次の例では、式 [Measures] を .Members 関数および Count() 関数と共に使用して Measures ディメンションのメンバー数を返す、計算されるメンバーを示しています。  
  
 `WITH MEMBER [Measures].[MeasureCount] AS`  
  
 `COUNT([Measures].MEMBERS)`  
  
 `SELECT [Measures].[MeasureCount] ON 0`  
  
 `FROM [Adventure Works]`  
  
 ディメンションの識別子*Dimension_Name* MDX ステートメントの記述に使用される BNF 表記でします。  
  
## <a name="hierarchy-expressions"></a>階層式  
 階層式にも同様に、階層識別子または階層関数のいずれかが含まれます。 次の例では、階層式 [Date].[Calendar] を .Levels 関数および .Count 関数と共に使用して、Date ディメンションの Calendar 階層のレベル数を返す方法を示しています。  
  
 `WITH MEMBER [Measures].[CalendarLevelCount] AS`  
  
 `[Date].[Calendar].Levels.Count`  
  
 `SELECT [Measures].[CalendarLevelCount] ON 0`  
  
 `FROM [Adventure Works]`  
  
 階層式を使用する最も一般的なシナリオでは、.Members 関数と組み合わせて階層のすべてのメンバーを返します。 次の例では、[Date] のすべてのメンバーを返します。[Calendar]、行軸上。  
  
 `SELECT [Measures].[Internet Sales Amount] ON 0,`  
  
 `[Date].[Calendar].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
 階層識別子*Dimension_Name.Hierarchy_Name* MDX ステートメントの記述に使用される BNF 表記でします。  
  
## <a name="see-also"></a>関連項目  
 [式&#40;MDX&#41;](../mdx/expressions-mdx.md)  
  
  
