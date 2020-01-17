---
title: UniqueName (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 69144341bd9cff344d4514f076517afac52e2a4b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68097292"
---
# <a name="uniquename-mdx"></a>UniqueName (MDX)


  指定されたディメンション、階層、レベル、メンバーの一意の名前を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Dimension expression syntax  
Dimension_Expression.UniqueName  
  
Hierarchy expression syntax  
Hierarchy_Expression.UniqueName  
  
Level expression syntax  
Level_Expression.UniqueName  
  
Member expression syntax  
Member_Expression.UniqueName  
```  
  
## <a name="arguments"></a>引数  
 *Dimension_Expression*  
 ディメンションに解決される有効な多次元式 (MDX) 式です。  
  
 *Hierarchy_Expression*  
 階層を返す有効な多次元式 (MDX) 式。  
  
 *Level_Expression*  
 レベルを返す有効な多次元式 (MDX) 式。  
  
 *メンバー式*  
 メンバーを 1 つ返す有効な多次元式 (MDX) 式です。  
  
## <a name="remarks"></a>コメント  
 **UniqueName**関数によって返される名ではなく、オブジェクトの一意の名前を返します、[名前](../mdx/name-mdx.md)関数。 返される名前では、キューブの名前は含まれません。 返される結果は、サーバー側の設定または MDX Unique Name Style 接続文字列プロパティによって異なります。  
  
## <a name="example"></a>例  
 次の例では、Adventure Works キューブの Product ディメンション、Product Categories 階層、Subcategory レベル、および Bike Racks メンバーの一意の名前値を返します。  
  
```  
WITH MEMBER DimensionUniqueName   
   AS [Product].UniqueName  
MEMBER HierarchyUniqueName   
   AS [Product].[Product Categories].UniqueName  
MEMBER LevelUniqueName   
   AS [Product].[Product Categories].[Subcategory].UniqueName  
MEMBER MemberUniqueName   
   AS [Product].[Product Categories].[Subcategory].[Bike Racks]  
SELECT   
   {DimensionUniqueName  
   , HierarchyUniqueName  
   , LevelUniqueName  
   , MemberUniqueName }  
   ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>関連項目  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
