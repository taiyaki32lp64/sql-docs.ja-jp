---
title: 存在 (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 0197417dfef604f3cb90b5fa032dae892de272c7
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68889050"
---
# <a name="exists-dmx"></a>存在 (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  指定されたサブクエリが少なくとも1つの行を返す場合に**true**を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
EXISTS(<subquery>)  
```  
  
## <a name="arguments"></a>引数  
 *subquery*  
 Select * FROM \<列名 > [WHERE \<述語 list >] の形式の select ステートメント。  
  
## <a name="result-type"></a>結果の種類  
 サブクエリによって返される結果セットに少なくとも1つの行が含まれている場合に**true**を返します。それ以外の場合は**false**を返します。  
  
## <a name="remarks"></a>コメント  
 EXISTS の前に NOT キーワードを使用できます。たとえば`WHERE NOT EXISTS (<subquery>)`、のようになります。  
  
 EXISTS のサブクエリ引数に追加する列の一覧は、関係ありません。関数は、条件を満たす行が存在するかどうかのみをチェックします。  
  
## <a name="examples"></a>使用例  
 EXISTS と NOT EXISTS を使用して、入れ子になったテーブルの条件を確認することができます。 これは、データマイニングモデルのトレーニングまたはテストに使用されるデータを制御するフィルターを作成する場合に便利です。 詳細については、「[マイニング モデルのフィルター選択 (Analysis Services - データ マイニング)](https://docs.microsoft.com/analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining)」を参照してください。  
  
 次の例は、「 `[Association]` [基本的なデータマイニングチュートリアル](https://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c)」で作成したマイニング構造とマイニングモデルに基づいています。 このクエリでは、顧客が少なくとも1つの patch kit を購入したケースのみが返されます。  
  
```  
SELECT * FROM [Association].CASES  
WHERE EXISTS  
(  
SELECT * FROM [v Assoc Seq Line Numbers]  
WHERE [[Model] = 'Patch kit'  
)  
```  
  
 このクエリによって返される同じデータを表示する別の方法として、アソシエーションビューアーでモデルを開き、[アイテム**セット Patch kit = Existing**] を右クリックし**て [ドリルスルー** ] オプションを選択し、[**モデルケースのみ**] を選択します。  
  
## <a name="see-also"></a>関連項目  
 [DMX &#40;関数&#41;](../dmx/functions-dmx.md)   
 [モデルフィルターの構文と&#40;例 Analysis Services-データマイニング&#41;](https://docs.microsoft.com/analysis-services/data-mining/model-filter-syntax-and-examples-analysis-services-data-mining)  
  
  
