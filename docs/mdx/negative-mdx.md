---
title: '- (負の)(MDX) |Microsoft Docs'
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 3221a54c8bedd67c28e1bf1f353f2cf7414829ca
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68088372"
---
# <a name="--negative-mdx"></a>- (負号) (MDX)


  数値式の負の値を返す単項演算を実行します。  
  
## <a name="syntax"></a>構文  
  
```  
  
- Numeric_Expression  
```  
  
#### <a name="parameters"></a>パラメーター  
 *Numeric_Expression*  
 数値の値を返す有効な多次元式 (MDX) 式。  
  
## <a name="return-value"></a>戻り値  
 指定されているパラメーターのデータ型を持つ負の値です。  
  
## <a name="examples"></a>使用例  
 次の例では、この演算子の使用を示します。  
  
```  
-- This member creates a negative version of the  
-- Reseller Freight Cost.  
WITH MEMBER   
   Measures.[Resell Cost as Negative]   
   AS -Measures.[Reseller Freight Cost]  
SELECT   
   [Date].[Calendar Month of Year].Children ON COLUMNS,  
   [Product].[Product Categories].Children ON ROWS  
FROM  
    [Adventure Works]  
WHERE  
    {[Measures].[Resell Cost as Negative]}  
```  
  
## <a name="see-also"></a>関連項目  
 [MDX 演算子リファレンス&#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
