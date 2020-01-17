---
title: 値 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: f373f626d778c4d77ec5843dca5bb11da728451d
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68887443"
---
# <a name="value-mdx"></a>Value (MDX)


  クエリのコンテキストで、属性階層の現在のメンバーと交差する、Measures ディメンションの現在のメンバーの値を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Member_Expression[.Value]   
```  
  
## <a name="arguments"></a>引数  
 *メンバー式*  
 メンバーを 1 つ返す有効な多次元式 (MDX) 式です。  
  
## <a name="remarks"></a>コメント  
 **Value**関数は、指定されたメンバーの値を文字列として返します。 **Value**引数は省略可能です。これは、メンバーの値がメンバーの既定のプロパティであり、他の値が指定されていない場合にメンバーに対して返される値であるためです。 メンバーのプロパティの詳細については、「[固有&#40;メンバー&#41;プロパティ mdx](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/mdx-member-properties-intrinsic-member-properties) 」および「[ユーザー &#40;定義&#41;メンバープロパティ (mdx](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/mdx-member-properties-user-defined-member-properties))」を参照してください。  
  
## <a name="examples"></a>使用例  
 次の例では、明示的にメンバーの名前を返すだけでなく、メンバーの値も返します。  
  
```  
WITH MEMBER [Date].[Calendar].NumericValue as [Date].[Calendar].[July 1, 2001].Value  
MEMBER [Date].[Calendar].MemberName AS [Date].[Calendar].[July 1, 2001].Name  
  
SELECT {[Date].[Calendar].NumericValue, [Date].[Calendar].MemberName} ON 0  
from [Adventure Works]  
```  
  
 次の例では、軸上のメンバーに対して返される既定値として、メンバーの値を返します。  
  
```  
SELECT {[Date].[Calendar].[July 1, 2001]} ON 0  
from [Adventure Works]  
```  
  
## <a name="see-also"></a>関連項目  
 [MemberValue &#40;MDX&#41;](../mdx/membervalue-mdx.md)   
 [Properties &#40;MDX&#41;](../mdx/properties-mdx.md)   
 [Name&#40;MDX&#41;](../mdx/name-mdx.md)   
 [UniqueName &#40;MDX&#41;](../mdx/uniquename-mdx.md)   
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
