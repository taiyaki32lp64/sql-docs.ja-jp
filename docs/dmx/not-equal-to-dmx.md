---
title: '&lt;&gt; (等しくない)(DMX) |Microsoft Docs'
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 7d8a7d790f55e955b92621caa1b1e729486eca19
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68008221"
---
# <a name="ltgt-not-equal-to-dmx"></a>&lt;&gt; (等しくない)(DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  1 つのデータ マイニング拡張機能 (DMX) 式の値が別の DMX 式の値と等しいかどうかを判別する比較演算を実行します。  
  
## <a name="syntax"></a>構文  
  
```  
  
DMX_Expression <> DMX_Expression  
```  
  
#### <a name="parameters"></a>パラメーター  
 *DMX_Expression*  
 有効な DMX 式です。  
  
## <a name="return-value"></a>戻り値  
 両方のパラメーターが NULL 以外であり、1 番目のパラメーターの値が 2 番目のパラメーターの値と等しくない場合、TRUE を含むブール値です。 ブール値には、両方のパラメーターが null でないと、最初のパラメーターの値が 2 番目のパラメーターの値と等しい場合は FALSE が含まれています。 ブール値には、いずれかまたは両方のパラメーターが null 値に評価される場合、null 値が含まれています。  
  
## <a name="see-also"></a>関連項目  
 [比較演算子&#40;DMX&#41;](../dmx/operators-comparison.md)   
 [データ マイニング拡張機能&#40;DMX&#41;演算子リファレンス](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [演算子&#40;DMX&#41;](../dmx/operators-dmx.md)  
  
  
