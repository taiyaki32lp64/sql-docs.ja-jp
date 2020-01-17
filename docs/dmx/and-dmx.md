---
title: および (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: e0c727e6a6f981dd2862575bfb4943b104196080
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67913746"
---
# <a name="and-dmx"></a>AND (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  2 つの数値式の論理積演算を実行します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Expression1 AND Expression2  
```  
  
#### <a name="parameters"></a>パラメーター  
 *Expression1*  
 数値の値を返す有効なデータ マイニング拡張機能 (DMX) 式。  
  
 *Expression2*  
 数値の値を返す有効な DMX 式。  
  
## <a name="return-value"></a>戻り値  
 True の場合、両方のパラメーターが評価されるを TRUE にするブール値それ以外の場合は FALSE です。  
  
## <a name="remarks"></a>コメント  
 両方のパラメーターはブール値として扱われます (0 FALSE の場合それ以外の場合 TRUE) 論理積を実行します。 次の表では、パラメーター値のさまざまな組み合わせに基づいて返される値を示します。  
  
|Expression1|Expression2|戻り値は|  
|-----------------------|-----------------------|---------------------|  
|TRUE|TRUE|TRUE|  
|TRUE|FALSE|FALSE|  
|false|TRUE|FALSE|  
|FALSE|FALSE|FALSE|  
  
## <a name="see-also"></a>関連項目  
 [データ マイニング拡張機能&#40;DMX&#41;演算子リファレンス](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [論理演算子&#40;DMX&#41;](../dmx/operators-logical.md)   
 [演算子&#40;DMX&#41;](../dmx/operators-dmx.md)  
  
  
