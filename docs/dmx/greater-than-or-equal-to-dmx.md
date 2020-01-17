---
title: '&gt;= (より大きいまたは等しい) (DMX) |Microsoft Docs'
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 3615dc8b5de0e5057e2dedaa0077aae51ed87ebe
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68074789"
---
# <a name="gt-greater-than-or-equal-to-dmx"></a>&gt;= (より大きいまたは等しい) (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  あるデータ マイニング拡張機能 (DMX) 式の値が他の DMX 式の値以上かどうかを判断する比較演算子を実行します。  
  
## <a name="syntax"></a>構文  
  
```  
  
DMX_Expression >= DMX_Expression  
```  
  
#### <a name="parameters"></a>パラメーター  
 *DMX_Expression*  
 有効な DMX 式です。  
  
## <a name="return-value"></a>戻り値  
 両方のパラメーターが null でないと、最初のパラメーターの値が 2 番目のパラメーターの値以上である場合に TRUE を含むブール値。 両方のパラメーターが NULL 以外であり、1 番目のパラメーターの値が 2 番目のパラメーターの値より小さい場合、FALSE を含むブール値です。 ブール値には、いずれかまたは両方のパラメーターが null 値に評価される場合、null 値が含まれています。  
  
## <a name="see-also"></a>関連項目  
 [比較演算子&#40;DMX&#41;](../dmx/operators-comparison.md)   
 [データ マイニング拡張機能&#40;DMX&#41;演算子リファレンス](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [演算子&#40;DMX&#41;](../dmx/operators-dmx.md)  
  
  
