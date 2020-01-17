---
title: IsGeneration (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 401a11a10f190cda8efeaffa04e1025ef7f4e681
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68105233"
---
# <a name="isgeneration-mdx"></a>IsGeneration (MDX)


  指定したメンバーが指定された世代内かどうかを返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
IsGeneration(Member_Expression, Generation_Number)   
```  
  
## <a name="arguments"></a>引数  
 *メンバー式*  
 メンバーを 1 つ返す有効な多次元式 (MDX) 式です。  
  
 *Generation_Number*  
 指定されたメンバーの評価対象となる世代を指定する有効な数値式です。  
  
## <a name="remarks"></a>コメント  
 **IsGeneration**関数が返される**true**指定された世代番号が、指定されたメンバーの場合。 関数を返しますそれ以外の場合、 **false**します。 また、指定されたメンバーが空のメンバーに評価された場合、 **IsGeneration**関数が返される**false**します。  
  
 世代インデックスの作成上の目的から、リーフ メンバーの世代インデックスは 0 になっています。 非リーフ メンバーの世代インデックスを判別するには、まず指定されたメンバーのすべての子メンバーの和集合から最高の世代インデックスを取得し、そのインデックスに 1 を加算します。 非リーフ メンバーの世代インデックスはこのような方法で決定されるので、1 つの非リーフ メンバーが複数の世代に属することもあり得ます。  
  
## <a name="example"></a>例  
 次の例では、場合は TRUE を返します。 [Date] です。[Fiscal] です。CurrentMember では、第 2 世代の一部を示します。  
  
 `WITH MEMBER MEASURES.ISGENERATIONDEMO AS`  
  
 `IsGeneration([Date].[Fiscal].CURRENTMEMBER, 2)`  
  
 `SELECT {MEASURES.ISGENERATIONDEMO} ON 0,`  
  
 `[Date].[Fiscal].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>関連項目  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
