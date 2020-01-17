---
title: (MDX) を抽出 |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 26edefab1a81aebaa9bf63e69e24067428266de1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67906038"
---
# <a name="extract-mdx"></a>Extract (MDX)


  抽出された階層要素から組のセットを返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Extract(Set_Expression, Hierarchy_Expression1 [,Hierarchy_Expression2, ...n] )  
```  
  
## <a name="arguments"></a>引数  
 *Set_Expression*  
 セットを返す有効な多次元式 (MDX) です。  
  
 *Hierarchy_Expression1*  
 階層を返す有効な多次元式 (MDX) 式。  
  
 *Hierarchy_Expression2*  
 階層を返す有効な多次元式 (MDX) 式。  
  
## <a name="remarks"></a>コメント  
 **抽出**関数抽出された階層要素から組で構成されるセットを返します。 指定したセット内の組ごとに、指定した階層のメンバーが結果セット内の新しい組に抽出されます。 この関数は、常に、重複する組を削除します。  
  
 **抽出**関数は逆の操作を実行する、 [Crossjoin](../mdx/crossjoin-mdx.md)関数。  
  
## <a name="examples"></a>使用例  
 次のクエリを使用する方法を示しています、**抽出**関数によって返される組のセットに対して、 **NonEmpty**関数。  
  
 `SELECT [Measures].[Internet Sales Amount] ON 0,`  
  
 `//Returns the distinct combinations of Customer and Date for all purchases`  
  
 `//of Bike Racks or Bike Stands`  
  
 `EXTRACT(`  
  
 `NONEMPTY(`  
  
 `[Customer].[Customer].[Customer].MEMBERS`  
  
 `*`  
  
 `[Date].[Date].[Date].MEMBERS`  
  
 `*`  
  
 `{[Product].[Product Categories].[Subcategory].&[26],[Product].[Product Categories].[Subcategory].&[27]}`  
  
 `*`  
  
 `{[Measures].[Internet Sales Amount]}`  
  
 `)`  
  
 `,  [Customer].[Customer], [Date].[Date])`  
  
 `ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>関連項目  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
