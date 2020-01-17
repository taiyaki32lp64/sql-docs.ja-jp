---
title: Set 式を使用する |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 1588d955e728830da4417160591a5c2b6c231473
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68893504"
---
# <a name="using-set-expressions"></a>セット式の使用


  セットは、0 個以上のタプルの順序付きリストで構成されます。 タプルを 1 つも含まないセットは、空のセットと呼ばれます。  
  
 一連の完全な式は、ゼロまたは複数の明示的に指定されたタプル、中かっこで囲まれています。  
  
 { [ { *Tuple_expression* | *Member_expression* } [ , { *Tuple_expression* | *Member_expression* } ] ... ] }  
  
 セット式で指定されたメンバー式は、1 つのメンバーのタプル式に変換されます。  
  
## <a name="example"></a>例  
 次の例では、クエリの列軸と行軸で使用される2つのセット式を示します。  
  
 `SELECT`  
  
 `{[Measures].[Internet Sales Amount], [Measures].[Internet Tax Amount]} ON COLUMNS,`  
  
 `{([Product].[Product Categories].[Category].&[4], [Date].[Calendar].[Calendar Year].&[2004]),`  
  
 `([Product].[Product Categories].[Category].&[1], [Date].[Calendar].[Calendar Year].&[2003]),`  
  
 `([Product].[Product Categories].[Category].&[3], [Date].[Calendar].[Calendar Year].&[2004])}`  
  
 `ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 Columns 軸のセット  
  
 {[Measures].[Internet Sales Amount], [Measures].[Internet Tax Amount]}  
  
 Measures ディメンションの2つのメンバーで構成されます。 ROWS 軸のセットを次に示します。  
  
 {([Product]。[製品カテゴリ]。[Category] です。 & [4]、[Date] です。[カレンダー]。[Calendar Year] & [2004])、  
  
 ([Product]。[製品カテゴリ]。[Category] です。 & [1]、[Date] です。[カレンダー]。[Calendar Year] & [2003])、  
  
 ([Product]。[製品カテゴリ]。[Category] です。 & [3]、[Date] です。[カレンダー]。[Calendar Year] です。 & [2004])}  
  
 このセットは 3 つのタプルで構成されており、それぞれのタプルには、Product ディメンションの Product Categories 階層のメンバーと Date ディメンションの Calendar 階層のメンバーへの、2 つの明示的な参照が含まれています。  
  
 セットを返す関数の例については、次を参照してください。[メンバー、タプル、およびセットの操作&#40;MDX&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/working-with-members-tuples-and-sets-mdx)します。  
  
## <a name="see-also"></a>関連項目  
 [MDX &#40;の式&#41;](../mdx/expressions-mdx.md)  
  
  
