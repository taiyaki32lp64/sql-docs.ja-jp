---
title: Ascendants (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 16c6f812d1d7cae5a81a8e64fb425f4d33f4cb5c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68017061"
---
# <a name="ascendants-mdx"></a>Ascendants (MDX)


  指定されたメンバー自体も含めたメンバーの先祖のセットを返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Ascendants(Member_Expression)  
```  
  
## <a name="arguments"></a>引数  
 *メンバー式*  
 メンバーを 1 つ返す有効な多次元式 (MDX) 式です。  
  
## <a name="remarks"></a>コメント  
 **Ascendants**関数がメンバーの階層の最上位までメンバーからすべてのメンバーの先祖を返します具体的には、指定されたメンバーの階層の逆順にたどってを実行し、。セット自体も含めたメンバーに関連するすべての先祖メンバーを返します。 これとは対照的に、[Ancestor](../mdx/ancestor-mdx.md)関数で、特定の先祖メンバー、または特定のレベルの先祖を返します。  
  
## <a name="examples"></a>使用例  
 次の例は、再販業者の注文の数を返します、`[Sales Territory].[Northwest]`メンバーとそのメンバーからのすべての先祖、 **Adventure Works**キューブ。 **Ascendants**関数を含むセットを構築します、`[Sales Territory].[Northwest]`メンバーとその先祖 ROWS 軸。  
  
```  
SELECT  
   Measures.[Reseller Order Count] ON COLUMNS,  
   Order(  
      Ascendants(  
         [Sales Territory].[Northwest]  
      ),  
      DESC  
   ) ON ROWS  
FROM  
   [Adventure Works]  
```  
  
## <a name="see-also"></a>関連項目  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
