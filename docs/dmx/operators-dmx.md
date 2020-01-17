---
title: 演算子 (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 2f03c3152e3144b137c079cbdfddeff5b9cd5156
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68008167"
---
# <a name="operators-dmx"></a>演算子 (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  内のクエリで算術演算子、比較、連結、および論理演算を実行するデータ マイニング拡張機能 (DMX) 演算子を使用することができます[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]します。  
  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 演算子を使用して、次の操作を実行します。  
  
-   特定の条件を満たしている値またはオブジェクトの検索  
  
-   値の間または式の間での判断  
  
 DMX では、複数のカテゴリの演算子を使用します。これについては、次のセクションで説明します。 個々 の演算子の詳細については、次を参照してください。[データ マイニング拡張機能&#40;DMX&#41;演算子リファレンス](../dmx/data-mining-extensions-dmx-operator-reference.md)します。  
  
|演算子のカテゴリ|演算子の型|  
|-----------------------|-----------------------|  
|[算術演算子&#40;DMX&#41;](../dmx/operators-arithmetic.md)|加算、減算、乗算、除算を実行します。|  
|[比較演算子&#40;DMX&#41;](../dmx/operators-comparison.md)|1 つの値を別の値または式を比較します。|  
|[論理演算子&#40;DMX&#41;](../dmx/operators-logical.md)|条件の真偽を調べます (AND、OR、NOT など)。|  
|[単項演算子&#40;DMX&#41;](../dmx/operators-unary.md)|1 つのオペランドに対して演算を実行します。|  
  
 演算子を使用することで、DMX の短い式を組み合わせて、より複雑な式を作成することができます。 基づく順序で、複雑な式に演算子の評価、[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]演算子の優先順位の定義。 優先順位の高い演算子は、優先順位の低い演算子より先に実行されます。 式の詳細については、次を参照してください。[式&#40;DMX&#41;](../dmx/expressions-dmx.md)します。  
  
 複数の単純式を 1 つの複合式に結合する場合、結合した式のデータ型は、演算子のルールとデータ型の優先順位のルールが組み合わされて決定されます。 結果が文字または Unicode 値では場合、[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]の演算子の照合順序の優先順位の規則と規則を組み合わせることによって、結果の照合順序を決定します。 単純式の有効桁数、小数点以下桁数、長さに基づいて結果の有効桁数、小数点以下桁数、長さを指定するルールもあります。  
  
## <a name="see-also"></a>参照  
 [データ マイニング拡張機能 &#40;DMX&#41; リファレンス](../dmx/data-mining-extensions-dmx-reference.md)   
 [データ マイニング拡張機能&#40;DMX&#41;関数リファレンス](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [データ マイニング拡張機能&#40;DMX&#41;ステートメント リファレンス](../dmx/data-mining-extensions-dmx-statements.md)   
 [データ マイニング拡張機能&#40;DMX&#41;構文表記規則](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [データ マイニング拡張機能&#40;DMX&#41;構文要素](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [一般的な予測関数&#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [構造と DMX 予測クエリの使用](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [DMX 選択ステートメントについて](../dmx/understanding-the-dmx-select-statement.md)  
  
  
