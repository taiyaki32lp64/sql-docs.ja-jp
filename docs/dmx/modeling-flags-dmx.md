---
title: モデリングフラグ (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: a610f3aed7f520163dc4e2b30651d8b0397ef644
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68893931"
---
# <a name="modeling-flags-dmx"></a>モデリング フラグ (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  の[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]モデリングフラグを使用して、ケーステーブルで定義されているデータに関する追加情報をデータマイニングアルゴリズムに提供できます。 アルゴリズムは、この情報を使用して、より正確なデータ マイニング モデルを作成することができます。 モデリング フラグは、マイニング構造列およびマイニング モデル列のいずれに対しても定義できます。  
  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]では、次のモデリングフラグがサポートされています。  
  
 **NOT NULL**  
 この属性列の値は NULL 値を含むことはありません。 モデルの学習プロセス中に、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] がこの属性列に NULL 値を検出した場合、エラーが発生します。 このフラグはマイニング構造列で定義されます。  
  
 **REGRESSOR**  
 アルゴリズムが、指定した列を回帰アルゴリズムの回帰式に使用できることを示します。 このフラグは、[!INCLUDE[msCoName](../includes/msconame-md.md)] Linear Regression および [!INCLUDE[msCoName](../includes/msconame-md.md)] Decision Trees アルゴリズムによってサポートされており、マイニング モデル列で定義されます。  
  
 **MODEL_EXISTENCE_ONLY**  
 この属性列の値は、属性の有無ほど重要ではありません。 このフラグはマイニング モデル列で定義されます。  
  
 サード パーティのアルゴリズムによっては、別のモデリング フラグもサポートしている場合があります。 アルゴリズムでサポートされているモデリングフラグを確認するには、 **SUPPORTED_MODELING_FLAGS**スキーマ行セットを使用します。 また、サーバーのマイニング サービスに対してクエリを実行し、特定のアルゴリズムでサポートされているモデリング フラグを判別することもできます。 たとえば、次のクエリでは、現在のサーバー上の Microsoft 線形回帰アルゴリズムでサポートされているモデリング フラグが返されます。  
  
```  
SELECT SUPPORTED_MODELING_FLAGS  
FROM $SYSTEM.DMSCHEMA_MINING_SERVICES  
WHERE SERVICE_NAME = 'Microsoft_Linear_Regression'  
```  
  
 期待される結果:  
  
 NOT NULL、REGRESSOR  
  
## <a name="specifying-modeling-flags-on-a-mining-model"></a>マイニング モデルでのモデリング フラグの指定  
 マイニング構造列にフラグを[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]指定するためにがサポートする構文の例については、「 [CREATE マイニング structure &#40;&#41;DMX](../dmx/create-mining-structure-dmx.md)」を参照してください。  
  
 マイニングモデル列でのモデリングフラグを指定する構文の例については、「 [ALTER マイニング&#40;STRUCTURE&#41;DMX](../dmx/alter-mining-structure-dmx.md)」を参照してください。  
  
 マイニングモデル列の操作の詳細については、「[マイニングモデル列](https://docs.microsoft.com/analysis-services/data-mining/mining-model-columns)」を参照してください。  
  
## <a name="see-also"></a>参照  
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
  
  
