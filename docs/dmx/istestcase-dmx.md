---
title: IsTestCase (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 050ceeaa8eb5700f108b7135616817e09c0031cb
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68889037"
---
# <a name="istestcase-dmx"></a>IsTestCase (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  ケースが、指定されたデータ マイニング モデルまたはマイニング構造のテスト ケースとして使用されるかどうかを示します。  
  
## <a name="syntax"></a>構文  
  
```  
  
IsTestCase()  
```  
  
## <a name="result-type"></a>結果の種類  
 ケースがテストデータセットの一部である場合は**true**を返します。それ以外の場合は**false**。  
  
## <a name="remarks"></a>コメント  
 データ マイニング ウィザードを使用してマイニング構造および関連マイニング モデルを作成する場合、既定では全ケースの 30% がテスト データセットの使用のために確保されます。 残りのケースは、データ マイニング モデルのトレーニングに使用されます。 その構造に基づくすべてのモデルで同じテスト データセットを使用できます。 ただし、DMX を使用してマイニング モデルを作成する場合は、既定ですべてのデータがモデルのトレーニングに使用され、テスト セットは作成されません。 テストデータセットの作成を有効にするには、WITH 予約句のパラメーターを設定する必要があります。  
  
 <xref:Microsoft.AnalysisServices.MiningStructure.HoldoutMaxCases%2A> プロパティと <xref:Microsoft.AnalysisServices.MiningStructure.HoldoutMaxPercent%2A> プロパティの値を表示すると、特定のマイニング構造にテスト セットが作成されたかどうかを確認できます。  
  
> [!NOTE]  
>  IsTrainingCase 関数または IsTestCase 関数を使用して特定のモデルのケースに関する詳細を返す場合は、モデルでドリルスルーを有効にする必要があります。 詳細については、「 [Enable Drillthrough for a Mining Model](https://docs.microsoft.com/analysis-services/data-mining/enable-drillthrough-for-a-mining-model)」(マイニング モデルのドリルスルーの有効化) を参照してください。  
  
 トレーニングデータセットの一部であるケースを返すには、 [IsTrainingCase &#40;DMX&#41;](../dmx/istrainingcase-dmx.md)関数を使用します。  
  
## <a name="examples"></a>使用例  
 次の例では`Targeted Mailing` 、「[基本的なデータマイニングチュートリアル](https://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c)」で作成したマイニング構造を使用します。 このクエリでは、テストに使用される構造内のすべてのケースが返されます。  
  
```  
SELECT *  
FROM [Targeted Mailing].CASES  
WHERE IsTestCase()  
```  
  
 データマイニングで使用されるケースをクエリする方法の詳細については、「 [SELECT FROM &#60;model&#62;」を参照してください。&#40;DMX&#41; ](../dmx/select-from-model-cases-dmx.md)と[SELECT FROM &#60;structure&#62;。ケース](../dmx/select-from-structure-cases.md)。  
  
## <a name="see-also"></a>参照  
 [DMX &#40;関数&#41;](../dmx/functions-dmx.md)   
 [データ マイニング クエリ](https://docs.microsoft.com/analysis-services/data-mining/data-mining-queries)   
 [トレーニング データ セットとテスト データ セット](https://docs.microsoft.com/analysis-services/data-mining/training-and-testing-data-sets)  
  
  
