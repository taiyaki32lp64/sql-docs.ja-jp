---
title: '&lt; (より小さい)(DMX) |Microsoft Docs'
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 9fa97cb3f703a4710c6aafa6a281c0d568e75cc0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68008331"
---
# <a name="lt-less-than-dmx"></a>&lt; (より小さい)(DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  あるデータ マイニング拡張機能 (DMX) 式の値が他の DMX 式の値より小さいかどうかを判断する比較演算子を実行します。  
  
## <a name="syntax"></a>構文  
  
```  
  
DMX_Expression < DMX_Expression  
```  
  
#### <a name="parameters"></a>パラメーター  
 *DMX_Expression*  
 有効な DMX 式です。  
  
## <a name="return-value"></a>戻り値  
 両方のパラメーターが NULL 以外であり、1 番目のパラメーターの値が 2 番目のパラメーターの値よりも小さい場合、TRUE を含むブール値です。 両方のパラメーターが NULL 以外であり、1 番目のパラメーターの値が 2 番目のパラメーターの値以上の場合、FALSE を含むブール値です。 ブール値には、いずれかまたは両方のパラメーターが null 値に評価される場合、null 値が含まれています。  
  
## <a name="see-also"></a>関連項目  
 [比較演算子&#40;DMX&#41;](../dmx/operators-comparison.md)   
 [データ マイニング拡張機能&#40;DMX&#41;演算子リファレンス](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [演算子&#40;DMX&#41;](../dmx/operators-dmx.md)  
  
  
