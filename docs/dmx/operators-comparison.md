---
title: 比較演算子 (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: fcbfb95070783db002d34870e5508df5322210d7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68008201"
---
# <a name="operators---comparison"></a>演算子 - 比較
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  比較演算子を使用するには任意のデータ マイニング拡張機能 (DMX) 式内でスカラー データと共に[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]します。 比較演算子はブール型のデータの型を評価します。TRUE または FALSE の条件がテストされた結果に基づいて返します。  
  
 次の表は、DMX がサポートしている比較演算子について示しています。  
  
|演算子|説明|  
|--------------|-----------------|  
|[&#60;&#40;未満&#41; &#40;DMX&#41;](../dmx/less-than-dmx.md)|NULL 以外の値として評価される引数では、左の引数の値が右の引数の値より小さい場合に TRUE を返します。そうでない場合は FALSE を返します。 いずれかまたは両方の引数は、null 値に評価される、演算子は null 値を返します。|  
|[&#62;&#40;より大きい&#41; &#40;DMX&#41;](../dmx/greater-than-dmx.md)|Null 以外の値に評価される引数では、TRUE を返します、左の引数の値が右の引数の値より大きい場合それ以外の場合は FALSE を返します。 いずれかまたは両方の引数は、null 値に評価される、演算子は null 値を返します。|  
|[=&#40;等しい&#41; &#40;DMX&#41;](../dmx/equal-to-dmx.md)|Null 以外の値に評価される引数では、TRUE を返します、左の引数の値が右の引数の値と等しい場合それ以外の場合は FALSE を返します。 いずれかまたは両方の引数は、null 値に評価される、演算子は null 値を返します。|  
|[&#60;&#62;&#40;等しくない&#41; &#40;DMX&#41;](../dmx/not-equal-to-dmx.md)|Null 以外の値に評価される引数では、TRUE を返します、左の引数の値が右の引数の値と等しくない場合それ以外の場合は FALSE を返します。 いずれかまたは両方の引数は、null 値に評価される、演算子は null 値を返します。|  
|[&#60;=&#40;より小さいまたは等しい&#41; &#40;DMX&#41;](../dmx/less-than-or-equal-to-dmx.md)|NULL 以外の値として評価される引数では、左の引数の値が右の引数の値以下の場合に TRUE を返します。そうでない場合は FALSE を返します。 いずれかまたは両方の引数は、null 値に評価される、演算子は null 値を返します。|  
|[&#62;=&#40;より大きいまたは等しい&#41; &#40;DMX&#41;](../dmx/greater-than-or-equal-to-dmx.md)|Null 以外の値に評価される引数では、右の引数の値と等しいか、左の引数の値がより大きい場合は TRUE を返しますそれ以外の場合は FALSE を返します。 いずれかまたは両方の引数は、null 値に評価される、演算子は null 値を返します。|  
  
 条件を検索する DMX ステートメントや関数で比較演算子を使用することもできます。  
  
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
  
  
