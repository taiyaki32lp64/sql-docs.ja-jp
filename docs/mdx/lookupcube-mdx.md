---
title: LookupCube (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: ec18b600c369de872df5f6eadf06ef6c30c88efa
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68098511"
---
# <a name="lookupcube-mdx"></a>LookupCube (MDX)


  同じデータベース内で別に指定されたキューブに対して評価される多次元式 (MDX) 式の値を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Numeric expression syntax  
LookupCube(Cube_Name, Numeric_Expression )  
  
String expression syntax  
LookupCube(Cube_Name, String_Expression )  
```  
  
## <a name="arguments"></a>引数  
 *Cube_Name*  
 キューブの名前を指定する有効な文字列式。  
  
 *Numeric_Expression*  
 有効な数値式は、通常、数値を返すセル座標の多次元式 (MDX) 式です。  
  
 *String_Expression*  
 通常、有効な多次元式 (MDX) 式セル座標の有効な文字列式文字列が返されます。  
  
## <a name="remarks"></a>コメント  
 数値式が指定されている場合、 **LookupCube**関数は、指定されたキューブ内の指定された数値式を評価し、結果として得られる数値を返します。  
  
 文字列式が指定されている場合、 **LookupCube**関数は、指定されたキューブ内の指定された文字列式を評価し、結果の文字列値を返します。  
  
 **LookupCube**関数は、MDX ではこれでクエリをソース キューブに含まれているため、同じデータベース内のキューブは、 **LookupCube**関数が実行されています。  
  
> [!IMPORTANT]  
>  現在のクエリのコンテキストが照会されるキューブに引き継がれないため、数値または文字列式で必要な現在のメンバーを提供する必要があります。  
  
 使用するどの計算、 **LookupCube**関数は、パフォーマンスが低下する可能性があります。 この関数を使用せずにすべての必要なデータが 1 つのキューブに存在するように、ソリューションを再設計を検討してください。  
  
## <a name="examples"></a>使用例  
 次のクエリでは、LookupCube の使用方法を示しています。  
  
 `WITH MEMBER MEASURES.LOOKUPCUBEDEMO AS`  
  
 `LOOKUPCUBE("Adventure Works", "[Measures].[In" + "ternet Sales Amount]")`  
  
 `SELECT MEASURES.LOOKUPCUBEDEMO  ON 0`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>関連項目  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
