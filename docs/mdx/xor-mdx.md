---
title: XOR (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 1657d9e58a0ae729a67e179602cd9a886ae923b1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68125788"
---
# <a name="xor-mdx"></a>XOR (MDX)


  2 つの数値式の排他的論理和演算を実行します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Expression1 XOR Expression2  
  
```  
  
#### <a name="parameters"></a>パラメーター  
 *Expression1*  
 数値の値を返す有効な多次元式 (MDX) 式。  
  
 *Expression2*  
 数値の値を返す有効な MDX 式です。  
  
## <a name="return-value"></a>戻り値  
 ブール値を返す**true**に 1 つだけの引数が評価された場合**true**、それ以外の**false**します。  
  
## <a name="remarks"></a>コメント  
 **XOR**演算子はブール値として両方のパラメーターを処理 (つまり、0 として**false**、それ以外の**true**) 排他的論理和を実行します。 次の表は方法、 **XOR**排他的論理和を実行します。  
  
|*Expression1*|*Expression2*|戻り値|  
|-------------------|-------------------|------------------|  
|**true**|**true**|**false**|  
|**true**|**false**|**true**|  
|**false**|**true**|**true**|  
|**false**|**false**|**false**|  
  
## <a name="see-also"></a>関連項目  
 [MDX 演算子リファレンス&#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
