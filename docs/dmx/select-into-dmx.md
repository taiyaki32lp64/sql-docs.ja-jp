---
title: SELECT INTO (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: a2e9fb0dfd3607adc1773d4a43561f32ba650ee5
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68887680"
---
# <a name="select-into-dmx"></a>SELECT INTO (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  既存のマイニング モデルのマイニング構造を基にした新しいマイニング モデルを作成します。 **SELECT INTO**ステートメントでは、スキーマや実際のアルゴリズムに固有ではないその他の情報をコピーすることによって、新しいマイニングモデルを作成します。  
  
## <a name="syntax"></a>構文  
  
```  
  
SELECT INTO <new model>   
USING <algorithm> [(<parameter list>)] [WITH DRILLTHROUGH[,] [FILTER(<expression>)]]  
FROM <existing model>  
```  
  
## <a name="arguments"></a>引数  
 *新しいモデル*  
 作成中の新しいモデルに対する一意の名前です。  
  
 *アルゴリズム*  
 プロバイダーによって定義された、データ マイニング アルゴリズムの名前です。  
  
 *パラメーターリスト*  
 任意。 アルゴリズムのプロバイダー定義パラメーターのコンマ区切りのリストです。  
  
 *式 (expression)*  
 トレーニング データに対する有効なフィルター条件に評価される式です。 フィルターとして使用できる式の詳細については、「[データマイニング&#40;&#41;Analysis Services マイニングモデルのフィルター](https://docs.microsoft.com/analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining)」を参照してください。  
  
 *既存のモデル*  
 コピーする既存のモデルの名前です。  
  
## <a name="remarks"></a>コメント  
 既存のモデルが学習済みの場合、新しいモデルはこのステートメントの実行時に自動的に処理されます。 学習済みではない場合、新しいモデルは処理されないままとなります。  
  
 **SELECT INTO**ステートメントは、既存のモデルの構造が新しいモデルのアルゴリズムと互換性がある場合にのみ機能します。 そのため、このステートメントは、同じアルゴリズムに基づくモデルを短時間で作成およびテストする場合に最も役に立ちます。 アルゴリズムの種類を変更する場合は、新しいアルゴリズムで、既存のモデル内の各列のデータ型がサポートされている必要があります。サポートされていない場合は、モデルが処理されるときにエラーが発生する可能性があります。  
  
 **WITH ドリルスルー**句を使用すると、新しいマイニングモデルでドリルスルーを実行できます。 ドリルスルーは、モデルの作成時にのみ可能です。  
  
## <a name="example-1-altering-the-parameters-of-the-model"></a>例 1 : モデルのパラメーターを変更する  
 次の例では、 `TM_Clustering`「[基本的なデータマイニングチュートリアル](https://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c)」で作成した既存のマイニングモデルに基づいて、新しいマイニングモデルを作成します。 新しいモデルでは、新しいモデル内に最大 5 つのクラスターが存在するよう CLUSTER_COUNT パラメーターが変更されています。 これに対して、既存のモデルでは既定値 10 が使用されています。  
  
```  
SELECT * INTO [New_Clustering]  
USING [Microsoft_Clustering] (CLUSTER_COUNT = 5)   
FROM [TM Clustering]  
```  
  
## <a name="example-2-adding-a-filter-to-the-model"></a>例 2:モデルへのフィルターの追加  
 次の例では、既存のマイニング モデルに基づいた新しいマイニング モデルを作成し、モデルにフィルターを追加します。 フィルターは、トレーニング データを特定の地域に住んでいる顧客だけに制限します。  
  
```  
SELECT * INTO [Clustering Europe Region]  
USING [Microsoft_Clustering] WITH FILTER(Region='Europe')  
FROM [TM Clustering]  
```  
  
> [!NOTE]  
>  ケース テーブルに適用されるフィルターは、この例に示すように、SELECT INTO ステートメントを使用して変更できます。ただし、入れ子になったテーブルに対するフィルターが元のモデルに含まれている場合、入れ子になったテーブルのフィルターは、この構文を使用しても変更または削除することができず、元のモデルからそのままコピーされます。 入れ子になったテーブルに別のフィルターを使用しているモデルを作成するには、ALTER STRTUCTURE...ADD MODEL 構文を使用します。  
  
## <a name="see-also"></a>参照  
 [データマイニング拡張&#40;機能&#41; DMX データ定義ステートメント](../dmx/dmx-statements-data-definition.md)   
 [データマイニング拡張&#40;機能&#41; DMX データ操作ステートメント](../dmx/dmx-statements-data-manipulation.md)   
 [データ マイニング拡張機能 &#40;DMX&#41; ステートメント リファレンス](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
