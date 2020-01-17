---
title: (除算)(DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 17f1233310ce8b070e12fbf25dca0e256ff34664
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68070739"
---
# <a name="divide-dmx"></a>(除算) (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  1 つの数値を別の数値で除算する算術演算を実行します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Dividend / Divisor  
```  
  
#### <a name="parameters"></a>パラメーター  
 *被除数*  
 数値の値を返す有効なデータ マイニング拡張機能 (DMX) 式。  
  
 *除数*  
 数値の値を返す有効な DMX 式。  
  
## <a name="return-value"></a>戻り値  
 優先順位の高いパラメーターのデータ型を持つ値です。  
  
## <a name="remarks"></a>コメント  
 この演算子が返す値は、最初の 2 番目の式で割った値式の商を表します。  
  
 両方の式は、同じデータ型でなければなりません。または、一方の式をもう一方の式のデータ型に暗黙的に変換できる必要があります。 除算の結果が NULL 値になる場合、演算子はエラーになります。 除数と被除数の両方が null 値に評価される、演算子は null 値を返します。  
  
## <a name="see-also"></a>関連項目  
 [算術演算子&#40;DMX&#41;](../dmx/operators-arithmetic.md)   
 [データ マイニング拡張機能&#40;DMX&#41;演算子リファレンス](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [演算子&#40;DMX&#41;](../dmx/operators-dmx.md)   
 [分割&#40;SSIS 式&#41;](../integration-services/expressions/divide-ssis-expression.md)   
 [&#40;分割&#41; &#40;TRANSACT-SQL&#41;](../t-sql/language-elements/divide-transact-sql.md)  
  
  
