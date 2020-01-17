---
title: コンテンツの種類 (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: da8a5e5602b877c12284d8410f6b2a1c7da6bc58
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68889143"
---
# <a name="content-types-dmx"></a>コンテンツの種類 (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  データ マイニング アルゴリズムが正しく機能するためには、コンテンツの種類など、データ型以外の追加情報が必要です。 コンテンツの種類は、列内のデータが機能する方法をアルゴリズムが判断するために役立ちます。  
  
 各アルゴリズムは特定のコンテンツの種類をサポートします。 たとえば、[!INCLUDE[msCoName](../includes/msconame-md.md)] Naive Bayes アルゴリズムは、連続列を使用できません。 [!INCLUDE[msCoName](../includes/msconame-md.md)] Naive Bayes モデルで連続列を使用するには、列のデータを分離する必要があります。 一部のアルゴリズムでは、正しく機能するために特定のコンテンツの種類が必要です。 たとえば、[!INCLUDE[msCoName](../includes/msconame-md.md)] タイム シリーズ アルゴリズムは、データが収集された経過時間を識別する、Key Time 列が必要です。  
  
 がサポートする[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]コンテンツの種類の詳細については、「[コンテンツの種類&#40;のデータ&#41;マイニング](https://docs.microsoft.com/analysis-services/data-mining/content-types-data-mining)」を参照してください。  
  
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
  
  
