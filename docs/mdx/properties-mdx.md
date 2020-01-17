---
title: Properties (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 9a9aa2ab3fbfdbe10246e0dcf8758cfcf7732375
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68893673"
---
# <a name="properties-mdx"></a>Properties (MDX)


  メンバー プロパティ値を含む文字列または厳密に型指定された値を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Member_Expression.Properties(Property_Name [, TYPED])  
```  
  
## <a name="arguments"></a>引数  
 *メンバー式*  
 メンバーを 1 つ返す有効な多次元式 (MDX) 式です。  
  
 *Property_Name*  
 メンバープロパティ名の有効な文字列式です。  
  
## <a name="remarks"></a>コメント  
 **Properties**関数は、指定したメンバー プロパティの指定されたメンバーの値を返します。 メンバープロパティには、**名前**、 **ID**、**キー**、**キャプション**などの固有メンバープロパティを使用することも、ユーザー定義メンバープロパティを使用することもできます。 詳細については、「[固有&#40;メンバー&#41;プロパティ mdx](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/mdx-member-properties-intrinsic-member-properties) 」および「[ユーザー &#40;定義&#41;メンバープロパティ (mdx](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/mdx-member-properties-user-defined-member-properties))」を参照してください。  
  
 既定では、値は文字列に変換されます。 **型**指定された場合、戻り値は厳密に型指定されます。  
  
-   プロパティの型が組み込み型の場合、この関数はメンバーの元の型を返します。  
  
-   プロパティの型がユーザー定義の場合、戻り値の型は**membervalue**関数の戻り値の型と同じになります。  
  
> [!NOTE]  
>  プロパティ (' Key ') は、複合キーを除き、Key0 と同じ結果を返します。 プロパティ (' Key ') は、複合キーに対して null を返します。 例に示すように、複合キーには Key*x*構文を使用します。 プロパティ (' Key0 ')、プロパティ (' Key1 ')、プロパティ (' Key2 ') などは、全体が複合キーを形成します。  
  
## <a name="example"></a>例  
 次の例では、固有メンバー プロパティとユーザー定義メンバー プロパティを返しています。Day Name メンバー プロパティについては TYPED 引数を使用して、戻り値の型を厳密に指定しています。  
  
```  
WITH MEMBER Measures.MemberName AS   
   [Date].[Calendar].[July 1, 2003].Properties('Name')  
MEMBER Measures.MemberVal AS   
   [Date].[Calendar].[July 1, 2003].Properties('Member_Value')  
MEMBER Measures.MemberKey AS   
   [Date].[Calendar].[July 1, 2003].Properties('Key')  
MEMBER Measures.MemberID AS   
   [Date].[Calendar].[July 1, 2003].Properties('ID')  
MEMBER Measures.MemberCaption AS   
   [Date].[Calendar].[July 1, 2003].Properties('Caption')  
MEMBER Measures.DayName AS   
   [Date].[Calendar].[July 1, 2003].Properties('Day Name', TYPED)  
MEMBER Measures.DayNameTyped AS   
   [Date].[Calendar].[July 1, 2003].Properties('Day Name')  
MEMBER Measures.DayofWeek AS   
   [Date].[Calendar].[July 1, 2003].Properties('Day of Week')  
MEMBER Measures.DayofMonth AS   
   [Date].[Calendar].[July 1, 2003].Properties('Day of Month')  
MEMBER Measures.DayofYear AS   
   [Date].[Calendar].[July 1, 2003].Properties('Day of Year')  
  
SELECT {Measures.MemberName  
   , Measures.MemberVal  
   , Measures.MemberKey  
   , Measures.MemberID  
   , Measures.MemberCaption  
   , Measures.DayName  
   , Measures.DayNameTyped  
   , Measures.DayofWeek  
   , Measures.DayofMonth  
   , Measures.DayofYear  
   }  ON 0  
FROM [Adventure Works]  
```  
  
 次の例は、KEY*x*プロパティの使用方法を示しています。  
  
```  
WITH   
MEMBER Measures.MemberKey AS   
   [Customer].[Customer Geography].[State-Province].&[QLD]&[AU].Properties('Key')  
MEMBER Measures.MemberKey0 AS   
   [Customer].[Customer Geography].[State-Province].&[QLD]&[AU].Properties('Key0')  
MEMBER Measures.MemberKey1 AS   
   [Customer].[Customer Geography].[State-Province].&[QLD]&[AU].Properties('Key1')  
  
SELECT {Measures.MemberKey  
   , Measures.MemberKey0  
   , Measures.MemberKey1     
   }  ON 0  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>参照  
 [メンバー プロパティの使用 &#40;MDX&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/mdx-member-properties)   
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
