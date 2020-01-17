---
title: Root (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: be687d5cbfd4fdbb706ef5c10778a4f3e3f93197
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68037041"
---
# <a name="root-mdx"></a>Root (MDX)


  構成される組を返します、**すべて**キューブ、ディメンション、または組の現在のスコープ内の各属性階層のメンバー。 スコープの詳細については、次を参照してください。 [SCOPE ステートメント&#40;MDX&#41;](../mdx/mdx-scripting-scope.md)します。  
  
> [!NOTE]  
>  属性階層がない場合、**すべて**メンバー、組には、その階層の既定のメンバーが含まれています。  
  
## <a name="syntax"></a>構文  
  
```  
  
Cube syntax  
Root ()  
Dimension syntax  
Root( Dimension_Name )  
Tuple syntax  
Root( Tuple_Expression )  
```  
  
## <a name="arguments"></a>引数  
 *Dimension_Name*  
 ディメンション名を指定する有効な文字列式。  
  
 *Tuple_Expression*  
 組を返す有効な多次元式 (MDX) 式です。  
  
## <a name="remarks"></a>コメント  
 ディメンション名も組式が指定されている場合、**Root**関数を含む組を返します、**すべて**メンバー (または既定のメンバー場合、**すべて**メンバーが存在しない)、キューブ内の各属性階層からです。 組の中のメンバーの順序は、キューブ内で属性階層が定義されている順序に基づきます。  
  
 ディメンション名が指定されている場合、**ルート**関数を含む組を返します、**すべて**メンバー (または既定のメンバー場合、**すべて**メンバーが存在しない) から各現在のメンバーのコンテキストに基づいて、指定したディメンションの属性階層。 組内のメンバーの順序は、属性階層がディメンション内で定義されている順序に基づきます。  
  
> [!NOTE]  
>  階層名が指定されている場合、**タプル**関数は、指定された階層名からディメンション名を取得します。  
  
 組式が指定されている場合、**Root**関数、指定された組の積集合を含む組を返します、**すべて**ディメンション属性を明示的に他のすべてのメンバー指定された組に含まれます。  
  
## <a name="examples"></a>使用例  
 次の例は、含む組を返します、**すべて**メンバー (または既定の場合、**すべて**メンバーが存在しない)、Adventure Works キューブ内の各階層からです。  
  
```  
SELECT Root()ON 0  
FROM [Adventure Works]  
```  
  
 次の例は、含む組を返します、**すべて**メンバー (または既定の場合、**すべて**メンバーが存在しない) の値と、Adventure Works キューブの Date ディメンション内の各階層からこれらの既定のメンバーと交差するメジャー ディメンションの指定されたメンバー。  
  
```  
SELECT Root([Date]) ON 0  
FROM [Adventure Works]  
WHERE [Measures].[Order Count]  
```  
  
 次の例は、指定された組のメンバーを含む組を返します (2001 年 7 月 1 日と共に、**すべて**メンバー (または既定の場合、**すべて**メンバーが存在しない) 内の指定の各階層から日付ディメンションの Adventure Works キューブとこれらのメンバーと交差するメジャー ディメンションの指定されたメンバーの値。  
  
```  
SELECT Root([Date].[July 1, 2001]) ON 0  
FROM [Adventure Works]  
WHERE [Measures].[Order Count]  
```  
  
## <a name="see-also"></a>関連項目  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
