---
title: 文字列関数の使用 |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 74eec478baad335cb5be6a78ec1faea2d15030ba
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68037996"
---
# <a name="using-string-functions"></a>文字列関数の使用


  文字列関数は、多次元式 (MDX) 内のほとんどすべてのオブジェクトに対して使用できます。 ストアド プロシージャでは、主にオブジェクトを文字列表記に変換するために文字列関数を使用します。 また、文字列式をオブジェクトに対して評価して値を返すために文字列関数を使用することもできます。  
  
 最も広く使用されている文字列関数は**Name**と**Uniquename**です。 これらの関数はそれぞれ、オブジェクトの名前と一意の名前を返します。 ほとんどの場合、これらは、計算をデバッグする際に、関数によって返されるメンバーを検出するために使用されます。  
  
## <a name="examples"></a>使用例  
 次のクエリでは、これらの関数の使用方法を示しています。  
  
 `WITH`  
  
 `//Returns the name of the current Product on rows`  
  
 `MEMBER [Measures].[ProductName] AS [Product].[Product].CurrentMember.Name`  
  
 `//Returns the uniquename of the current Product on rows`  
  
 `MEMBER [Measures].[ProductUniqueName] AS [Product].[Product].CurrentMember.Uniquename`  
  
 `//Returns the name of the Product dimension`  
  
 `MEMBER [Measures].[ProductDimensionName] AS [Product].Name`  
  
 `SELECT  {[Measures].[ProductName],[Measures].[ProductUniqueName],[Measures].[ProductDimensionName]}`  
  
 `ON COLUMNS,`  
  
 `[Product].[Product].MEMBERS  ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 **Generate**を一連のすべてのメンバーに文字列関数を実行し、結果を連結関数を使用できます。 また、セットの内容を視覚化できるようになるため、計算をデバッグする際に役立つ場合もあります。 次の例では、この用途で関数を使用する方法を示します。  
  
 `WITH`  
  
 `//Returns the names of the current Product and its ancestors up to the All Member`  
  
 `MEMBER [Measures].[AncestorNames] AS`  
  
 `GENERATE(`  
  
 `ASCENDANTS([Product].[Product Categories].CurrentMember)`  
  
 `, [Product].[Product Categories].CurrentMember.Name, ", ")`  
  
 `SELECT`  
  
 `{[Measures].[AncestorNames]}`  
  
 `ON COLUMNS,`  
  
 `[Product].[Product Categories].MEMBERS  ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 広く使われているもう 1 つのグループの文字列関数は、オブジェクトやそのオブジェクトに解決される式の一意の名前を含む文字列を、そのオブジェクト自体にキャストできるようにする関数です。 次のクエリを示していますが、どのように**StrToMember**と**StrToSet**関数は。  
  
 `SELECT`  
  
 `{StrToMember("[Measures].[Inter" + "net Sales Amount]")}`  
  
 `ON COLUMNS,`  
  
 `StrToSet("{`  
  
 `[Product].[Product Categories].[Category].&[3],`  
  
 `[Product].[Product Categories].[Product].&[477],`  
  
 `[Product].[Product Categories].[Product].&[788],`  
  
 `[Product].[Product Categories].[Product].&[708],`  
  
 `[Product].[Product Categories].[Product].&[711]`  
  
 `}")`  
  
 `ON ROWS`  
  
 `FROM [Adventure Works]`  
  
> [!NOTE]  
>  **StrToMember**と**StrToSet**関数は、注意して使用する必要があります。 これらの関数を計算の定義内で使用すると、クエリのパフォーマンスが低下する場合があります。  
  
## <a name="see-also"></a>参照  
 [Generate&#40;MDX&#41;](../mdx/generate-mdx.md)   
 [Name&#40;MDX&#41;](../mdx/name-mdx.md)   
 [UniqueName &#40;MDX&#41;](../mdx/uniquename-mdx.md)   
 [Functions&#40;MDX 構文&#41;](../mdx/functions-mdx-syntax.md)   
 [ストアド プロシージャの使用&#40;MDX&#41;](../mdx/using-stored-procedures-mdx.md)   
 [StrToMember &#40;MDX&#41;](../mdx/strtomember-mdx.md)   
 [StrToSet &#40;MDX&#41;](../mdx/strtoset-mdx.md)  
  
  
