---
title: MemberToStr (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ff7ffb1b57c8af38e1b2eeebc64f2a3e753fc5b3
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2018
ms.locfileid: "52528472"
---
# <a name="membertostr-mdx"></a>MemberToStr (MDX)


  指定されたメンバーに対応する MDX 形式の文字列を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
MemberToStr(Member_Expression)   
```  
  
## <a name="arguments"></a>引数  
 *メンバー式*  
 メンバーを 1 つ返す有効な多次元式 (MDX) 式です。  
  
## <a name="remarks"></a>コメント  
 この関数は、メンバーの一意の名前を表す文字列を返します。 メンバーの一意の名前を外部関数に渡すには、通常使用されます。  
  
## <a name="example"></a>例  
 次の例は、文字列 [Geography].[Geography].[Country].&[United States] を返します。  
  
 `WITH MEMBER Measures.x AS MemberToStr`  
  
 `([Geography].[Geography].[Country].[United States])`  
  
 `SELECT Measures.x ON 0`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>参照  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
