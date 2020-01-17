---
title: しない (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 4031b887eb0a42580d6ae8debf6c9177ff67efc3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68088233"
---
# <a name="not-mdx"></a>NOT (MDX)


  1 つの数値式の論理否定を実行します。  
  
## <a name="syntax"></a>構文  
  
```  
  
NOT Expression1  
```  
  
#### <a name="parameters"></a>パラメーター  
 *Expression1*  
 数値の値を返す有効な多次元式 (MDX) 式。  
  
## <a name="return-value"></a>戻り値  
 ブール値を返す**false**に引数が評価された場合**true**、それ以外の**true**します。  
  
## <a name="remarks"></a>コメント  
 **いない**演算子はブール値として式を処理 (つまり、0 として**false**、それ以外の**true**) 論理否定演算を実行します。 次の表は方法、**いない**演算子が論理否定演算を実行します。  
  
|*Expression1*|戻り値|  
|-------------------|------------------|  
|**true**|**false**|  
|**false**|**true**|  
  
## <a name="see-also"></a>関連項目  
 [MDX 演算子リファレンス&#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
