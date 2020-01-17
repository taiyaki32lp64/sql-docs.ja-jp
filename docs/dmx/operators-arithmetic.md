---
title: 算術演算子 (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: e78241252733e8298c0bc727f9c45dd6df2768ac
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68008214"
---
# <a name="operators---arithmetic"></a>演算子 - 算術
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  算術演算を行うのため、算術演算子データ マイニング拡張機能 (DMX) でを使用できます[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]加算、減算、乗算、および除算を含め、します。  
  
 次の表は、DMX をサポートする算術演算子を識別します。  
  
|演算子|説明|  
|--------------|-----------------|  
|[+&#40;追加&#41; &#40;DMX&#41;](../dmx/add-dmx.md)|2 つの数値を加算します。|  
|[-&#40;減算&#41; &#40;DMX&#41;](../dmx/subtract-dmx.md)|ある数値から別の数値を減算します。|  
|[&#42;&#40;乗算&#41; &#40;DMX&#41;](../dmx/multiply-dmx.md)|ある数値を別の数値によって乗算します。|  
|[&#40;分割&#41; &#40;DMX&#41;](../dmx/divide-dmx.md)|1 つの数値を別の数値を除算します。|  
  
 次の規則は、DMX 式に算術演算子の優先順位の順序を決定します。  
  
-   式では、複数の算術演算子がある場合は、乗算と除算計算最初に、後に減算と加算されます。  
  
-   式のすべての算術演算子の優先順位の同じレベルとは、実行の順序を左右から。  
  
-   かっこ内にある式は、その他のすべての操作よりも優先されます。  
  
## <a name="see-also"></a>関連項目  
 [データ マイニング拡張機能 &#40;DMX&#41; リファレンス](../dmx/data-mining-extensions-dmx-reference.md)   
 [データ マイニング拡張機能&#40;DMX&#41;関数リファレンス](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [データ マイニング拡張機能&#40;DMX&#41;演算子リファレンス](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [データ マイニング拡張機能&#40;DMX&#41;ステートメント リファレンス](../dmx/data-mining-extensions-dmx-statements.md)   
 [データ マイニング拡張機能&#40;DMX&#41;構文表記規則](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [データ マイニング拡張機能&#40;DMX&#41;構文要素](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [式&#40;DMX&#41;](../dmx/expressions-dmx.md)   
 [一般的な予測関数&#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [演算子&#40;DMX&#41;](../dmx/operators-dmx.md)   
 [構造と DMX 予測クエリの使用](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [DMX 選択ステートメントについて](../dmx/understanding-the-dmx-select-statement.md)  
  
  
