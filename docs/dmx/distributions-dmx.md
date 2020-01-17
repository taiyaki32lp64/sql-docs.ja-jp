---
title: ディストリビューション (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: fda2eb169985eb670614f611764fbf149c71a42d
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68892789"
---
# <a name="distributions-dmx"></a>分布 (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  で[!INCLUDE[msCoName](../includes/msconame-md.md)] は、マイニング[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]モデルの作成時にアルゴリズムがこれらの列のデータを処理する方法に影響を与えるように、マイニング構造の列のコンテンツを定義できます。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] いくつかのアルゴリズムは、列が値の一般的な分布を含むことが認識された場合、モデルを処理する前にすべての連続列の分布を定義するために使用されます。 分布が定義されない場合、アルゴリズムが持つデータを解釈するための情報が少ないため、分布が定義されたときよりも、マイニング モデルの結果が実際の予測より小さくなる場合があります。  
  
 [!INCLUDE[msCoName](../includes/msconame-md.md)]データマイニングアルゴリズムでは、次の分布の種類がサポートされています。  
  
 **通常**  
 連続列の値は、正規のガウス分布によるヒストグラムを形成します。  
  
 **Log Normal**  
 連続列の値は、値の対数が正規分布であるヒストグラムを形成します。  
  
 **単色**  
 連続列の値はフラット曲線を形成し、すべての値が等しくなります。  
  
 [!INCLUDE[msCoName](../includes/msconame-md.md)]データマイニングアルゴリズムの詳細については、「データマイニング[アルゴリズム&#40;Analysis Services-&#41;データマイニング](https://docs.microsoft.com/analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining)」を参照してください。 サードパーティのアルゴリズム プロバイダーは、追加の分布の種類をサポートしている場合があります。 アルゴリズムでサポートされている分布の種類を確認するには、 **SUPPORTED_DISTRIBUTION_FLAGS**スキーマ行セットを使用します。  
  
 分布の種類の詳細については、「 [ &#40;列&#41;分布データマイニング](https://docs.microsoft.com/analysis-services/data-mining/column-distributions-data-mining)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [コンテンツの種類 &#40;です。 データ マイニング&#41;](https://docs.microsoft.com/analysis-services/data-mining/content-types-data-mining)   
 [データ マイニング拡張機能 &#40;DMX&#41; リファレンス](../dmx/data-mining-extensions-dmx-reference.md)   
 [データマイニング拡張&#40;機能&#41; DMX 構文要素](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [データマイニング拡張&#40;機能&#41; DMX 関数リファレンス](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [データマイニング拡張&#40;機能&#41; DMX オペレーターリファレンス](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [データマイニング拡張&#40;機能&#41; DMX ステートメントリファレンス](../dmx/data-mining-extensions-dmx-statements.md)   
 [データマイニング拡張&#40;機能&#41; DMX 構文表記規則](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [一般的な予測&#40;関数 DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [構造と DMX 予測クエリの使用](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [DMX 選択ステートメントについて](../dmx/understanding-the-dmx-select-statement.md)  
  
  
