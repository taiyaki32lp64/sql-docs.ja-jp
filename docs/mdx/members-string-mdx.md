---
title: Members (String) (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 05df2d0a846af30d46e702c1d5489945d57c9115
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68001491"
---
# <a name="members-string-mdx"></a>Members (String) (MDX)


  文字列式で指定されたメンバーを返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Members(Member_Name)   
```  
  
## <a name="arguments"></a>引数  
 *Member_Name*  
 メンバー名を指定する有効な文字列式を指定します。  
  
## <a name="remarks"></a>コメント  
 **Members (String)** 関数は、指定する名前を持つ 1 つのメンバーを返します。 通常、使用して、 **Members (String)** に提供する外部の関数と併用、 **Members (String)** 関数メンバーを識別する文字列、 **Members (String)** 関数がその指定したメンバーについて、値を返します。  
  
## <a name="example"></a>例  
 次の例では、 **Members (String)** 有効なメンバーに指定した文字列を変換する関数を文字列で指定されたメンバーの既定のメジャーを返します。 指定した文字列では、単一引用符でします。 既定のメジャーは、Reseller Sales Amount メジャーです。  
  
```  
SELECT Members ('[Geography].[Geography].[Country].&[United States] ') ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>関連項目  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
