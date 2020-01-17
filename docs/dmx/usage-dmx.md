---
title: 使用状況 (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: b961282ba6bc25caa260a3e156f843a413a5ef1a
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68893111"
---
# <a name="usage-dmx"></a>使用法 (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  データマイニング拡張機能 (DMX) を使用しての[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]新しいデータマイニングモデルを定義する場合は、モデルを構築するデータマイニングアルゴリズムで各列を使用する方法を指定する必要があります。 列は次の型のうちのいずれかとして指定することができます。  
  
-   **[キー]**  
  
-   **キーシーケンス**  
  
-   **キー時刻**  
  
-   **Predict**  
  
-   **PredictOnly**  
  
 DMX では指定されていない列は入力列として扱われます。  
  
 モデルを正しく処理するには、各行を一意に識別するキー列はどれなのか、予測可能モデルを作成する場合に予測を作成するための対象列はどれなのか、および対象列を予測するリレーションシップを作成するために入力列として使用する列はどれなのかをアルゴリズムに理解させる必要があります。  
  
 **Predict**型として指定された列は、入力列と出力列の両方として使用されます。 **Predictonly**として指定された列は、出力列としてのみ使用されます。 特定のアルゴリズムでは、列の予測を異なる方法で扱うことができます。  
  
 でサポートされる[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]列の使用法の種類の詳細については、「[マイニングモデル列](https://docs.microsoft.com/analysis-services/data-mining/mining-model-columns)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [データ マイニング アルゴリズム &#40;Analysis Services - データ マイニング&#41;](https://docs.microsoft.com/analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining)   
 [データ マイニング拡張機能 &#40;DMX&#41; リファレンス](../dmx/data-mining-extensions-dmx-reference.md)   
 [データマイニング拡張&#40;機能&#41; DMX 構文要素](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [データマイニング拡張&#40;機能&#41; DMX 関数リファレンス](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [データマイニング拡張&#40;機能&#41; DMX オペレーターリファレンス](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [データマイニング拡張&#40;機能&#41; DMX ステートメントリファレンス](../dmx/data-mining-extensions-dmx-statements.md)   
 [データマイニング拡張&#40;機能&#41; DMX 構文表記規則](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [一般的な予測&#40;関数 DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [構造と DMX 予測クエリの使用](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [DMX 選択ステートメントについて](../dmx/understanding-the-dmx-select-statement.md)  
  
  
