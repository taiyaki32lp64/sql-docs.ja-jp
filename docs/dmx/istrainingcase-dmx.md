---
title: IsTrainingCase (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 23f36181d0ee4902f56aa4acb8163f7f43af8b31
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68889025"
---
# <a name="istrainingcase-dmx"></a>IsTrainingCase (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  ケースが、指定されたデータ マイニング モデルまたはマイニング構造のトレーニング ケースとして使用されるかどうかを示します。  
  
## <a name="syntax"></a>構文  
  
```  
  
IsTrainingCase()  
```  
  
## <a name="result-type"></a>結果の種類  
 ケースがトレーニングデータセットの一部である場合に**true**を返します。それ以外の場合は**false**。  
  
## <a name="remarks"></a>コメント  
 データ マイニング ウィザードを使用してマイニング構造および関連マイニング モデルを作成する場合、既定では全ケースの 30% がテスト データセットの使用のために確保されます。 指定したデータ ソース内の残りのケースはモデルのトレーニングに使用されます。 ただし、データ マイニング拡張機能 (DMX) を使用してマイニング モデルを作成する場合は、既定ですべてのデータがモデルのトレーニングに使用され、テスト セットは作成されません。 テスト データセットの作成を有効にするには、WITH HOLDOUT 句のパラメーターを設定する必要があります。  
  
 <xref:Microsoft.AnalysisServices.MiningStructure.HoldoutMaxCases%2A> プロパティと <xref:Microsoft.AnalysisServices.MiningStructure.HoldoutMaxPercent%2A> プロパティの値を表示すると、特定のデータ マイニング構造のデータがテスト セットとトレーニング セットにパーティション分割されているかどうかを確認できます。  
  
> [!NOTE]  
>  IsTrainingCase 関数または IsTestCase 関数を使用してモデル内のケースに関する詳細を返す場合は、モデルでドリルスルーを有効にする必要があります。 詳細については、「 [Enable Drillthrough for a Mining Model](https://docs.microsoft.com/analysis-services/data-mining/enable-drillthrough-for-a-mining-model)」(マイニング モデルのドリルスルーの有効化) を参照してください。  
  
 テストデータセットの一部であるケースを返すには、 [IsTestCase &#40;DMX&#41;](../dmx/istestcase-dmx.md)関数を使用します。  
  
## <a name="examples"></a>使用例  
 次の例では、「[基本的なデータマイニングチュートリアル](https://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c)」の絞り込みメール配信シナリオのクラスタリングデータマイニングモデルを使用します。 クエリでは、マイニング モデルのトレーニングで使用されたケースのみが返されます。 さらに、トレーニング ケースは 40 歳未満の顧客だけに制限されます。  
  
```  
SELECT *  
FROM [TM Clustering].CASES  
WHERE IsTrainingCase()  
AND [Age] <40  
```  
  
 データマイニングで使用されるケースをクエリする方法のその他の例については、「 [ &#60;&#62;モデルから選択」を参照してください。&#40;DMX&#41; ](../dmx/select-from-model-cases-dmx.md)と[SELECT FROM &#60;structure&#62;。ケース](../dmx/select-from-structure-cases.md)。  
  
## <a name="see-also"></a>参照  
 [トレーニングデータセットとテストデータセット](https://docs.microsoft.com/analysis-services/data-mining/training-and-testing-data-sets)   
 [DMX &#40;関数&#41;](../dmx/functions-dmx.md)   
 [データ マイニング クエリ](https://docs.microsoft.com/analysis-services/data-mining/data-mining-queries)  
  
  
