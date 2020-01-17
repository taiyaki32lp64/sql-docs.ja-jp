---
title: データ マイニング モデル トレーニング変換先 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.dataminingmodeltrainingdest.f1
helpviewer_keywords:
- destinations [Integration Services], Data Mining Model Training
- Data Mining Model Training destination
- mining models [Analysis Services], training
- training mining models
ms.assetid: 6bc8cbe2-46af-4f7b-93d6-86779313c9d7
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 5dac84fe42185806ae468593876a6bd439c1c689
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68890642"
---
# <a name="data-mining-model-training-destination"></a>データ マイニング モデル トレーニング変換先
  データ マイニング モデル トレーニング変換先は、変換先が受け取るデータをデータ マイニング モデル アルゴリズムに渡すことにより、データ マイニング モデルのトレーニングを行います。 複数のデータ マイニング モデルが同じデータ マイニング構造に基づいて構築されている場合は、1 つの変換先を使用してトレーニングできます。 詳細については、「 [マイニング構造列](https://docs.microsoft.com/analysis-services/data-mining/mining-structure-columns) 」と「 [マイニング モデル列](https://docs.microsoft.com/analysis-services/data-mining/mining-model-columns)」を参照してください。  
  
## <a name="configuration-of-the-data-mining-model-training-destination"></a>データ マイニング モデル トレーニング変換先の構成  
 対象になる構造とその構造に基づいて構築されているモデルのケース レベル列で、コンテンツの種類が KEY TIME または KEY SEQUENCE の列がある場合、入力データをその列で並べ替える必要があります。 たとえば、Microsoft Time Series アルゴリズムを使用して構築されたモデルでは、コンテンツの種類に KEY TIME が使用されます。 入力データが並べ替えられていない場合、そのモデルの処理が失敗する場合があります。 データを並べ替える必要がある場合、データ フロー内で事前に並べ替え変換を使用してデータを並べ替えることができます。 コンテンツの種類が KEY である列には、この要件は適用されません。 詳細については、「[コンテンツの種類 (データ マイニング)](https://docs.microsoft.com/analysis-services/data-mining/content-types-data-mining)」と「[並べ替え変換](transformations/sort-transformation.md)」を参照してください。  
  
> [!NOTE]  
>  データ マイニング モデル トレーニング変換先への入力は、並べ替えられている必要があります。 データを並べ替えるため、データ フロー内のデータ マイニング モデル トレーニング変換先の上流に、並べ替え変換を含めることができます。 詳細については、「 [Sort Transformation](transformations/sort-transformation.md)」を参照してください。  
  
 この変換先は 1 つの入力をとりますが、出力はありません。  
  
 データ マイニング モデル トレーニング変換先を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] インスタンスに接続するには、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 接続マネージャーを使用します。 詳細については、「 [Analysis Services 接続マネージャー](../connection-manager/analysis-services-connection-manager.md)」を参照してください。  
  
 プロパティを設定するには [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 **[データ マイニング モデル トレーニング エディター]** ダイアログ ボックスで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [データ マイニング モデル トレーニング エディター ([接続] タブ)](../data-mining-model-training-editor-connection-tab.md)  
  
-   [データ マイニング モデル トレーニング エディター([列] タブ)](../data-mining-model-training-editor-columns-tab.md)  
  
 **[詳細エディター]** ダイアログ ボックスには、プログラムによって設定できるプロパティが反映されます。 **[詳細エディター]** ダイアログ ボックスまたはプログラムで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [共通プロパティ](../common-properties.md)  
  
-   [データ マイニング モデル トレーニング変換先のカスタム プロパティ](data-mining-model-training-destination-custom-properties.md)  
  
 データ フロー コンポーネントのプロパティの設定方法については、「 [データ フロー コンポーネントのプロパティを設定する](set-the-properties-of-a-data-flow-component.md)」を参照してください。  
  
  
