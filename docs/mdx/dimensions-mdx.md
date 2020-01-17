---
title: ディメンション (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 84d5ab0caa22c6f35f3e7b790dbfb3348df8ceb1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67999965"
---
# <a name="dimensions-mdx"></a>Dimensions (MDX)


  数値または文字列式で指定された階層を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Numeric expression syntax  
Dimensions(Hierarchy_Number)  
  
String expression syntax  
Dimensions(Hierarchy_Name)  
```  
  
## <a name="arguments"></a>引数  
 *Hierarchy_Number*  
 階層番号を指定する有効な数値式です。  
  
 *Hierarchy_Name*  
 階層名を指定する有効な文字列式です。  
  
## <a name="remarks"></a>コメント  
 階層番号が指定されている場合、**ディメンション**関数は、キューブ内の 0 から始まる位置を階層に指定された階層数を返します。  
  
 階層名が指定されている場合、**ディメンション**関数は、指定された階層を返します。 通常、この文字列バージョンの使用、**ディメンション**ユーザー定義関数と併用します。  
  
> [!NOTE]  
>  **メジャー**ディメンションは常に表される`Dimensions(0)`します。  
  
## <a name="examples"></a>使用例  
 次の例を使用して、**ディメンション**名、レベル数、および数の数値式と文字列式の両方を使用して、指定された階層のメンバーを返す関数。  
  
```  
WITH MEMBER Measures.x AS Dimensions  
   ('[Product].[Product Model Lines]').Name  
SELECT Measures.x on 0  
FROM [Adventure Works]  
  
WITH MEMBER Measures.x AS Dimensions  
   ('[Product].[Product Model Lines]').Levels.Count  
SELECT Measures.x on 0  
FROM [Adventure Works]  
  
WITH MEMBER Measures.x AS Dimensions  
   ('[Product].[Product Model Lines]').Members.Count  
SELECT Measures.x on 0  
FROM [Adventure Works]  
  
WITH MEMBER Measures.x AS Dimensions(0).Name  
SELECT Measures.x on 0  
FROM [Adventure Works]  
  
WITH MEMBER Measures.x AS Dimensions(0).Levels.Count  
SELECT measures.x on 0  
FROM [Adventure Works]  
  
WITH MEMBER Measures.x AS Dimensions(0).Members.Count  
SELECT measures.x on 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>関連項目  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
