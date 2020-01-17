---
title: '- (を除く)(MDX) |Microsoft Docs'
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: cf0121d1be3cd2943a801f3c72ca4952b70ec681
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68139080"
---
# <a name="except-mdx-operator"></a>(MDX) 演算子を除く


  2 つのセットの重複メンバーを削除して差集合を返すセット演算を実行します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Set_Expression - Set_Expression  
```  
  
#### <a name="parameters"></a>パラメーター  
 *Set_Expression*  
 セットを返す有効な多次元式 (MDX) です。  
  
## <a name="return-value"></a>戻り値  
 指定した両方のパラメーターによって共有されていないメンバーを含むセットです。  
  
## <a name="remarks"></a>コメント  
 **- (Except)** 演算子は機能的に等価、[を除く](../mdx/except-mdx-function.md)関数。  
  
## <a name="examples"></a>使用例  
 この演算子の使用例を次に示します。  
  
```  
// This query shows the quantity of orders for all product categories  
// with the exception of Components.  
SELECT   
   [Measures].[Order Quantity] ON COLUMNS,  
   [Product].[Product Categories].[All].Children   
   - [Product].[Product Categories].[Components] ON ROWS  
FROM  
    [Adventure Works]  
```  
  
## <a name="see-also"></a>関連項目  
 [MDX 演算子リファレンス&#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
