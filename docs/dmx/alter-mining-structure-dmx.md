---
title: ALTER マイニング構造 (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 5535428d89a0d14b60e3ac79d281f63b4c69bfb5
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68889864"
---
# <a name="alter-mining-structure-dmx"></a>ALTER MINING STRUCTURE (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  既存のマイニング構造に基づいて新しいマイニング モデルを作成します。  **ALTER マイニング structure**ステートメントを使用して新しいマイニングモデルを作成する場合は、構造が既に存在している必要があります。 これに対して、ステートメントを使用して[マイニングモデル&#40;DMX&#41;を作成](../dmx/create-mining-model-dmx.md)する場合は、モデルを作成し、その基になるマイニング構造を同時に自動的に生成します。  
  
## <a name="syntax"></a>構文  
  
```  
  
ALTER MINING STRUCTURE <structure>  
ADD MINING MODEL <model>  
(  
    <column definition list>  
  [(<nested column definition list>) [WITH FILTER (<nested filter criteria>)]]  
)  
USING <algorithm> [(<parameter list>)]   
[WITH DRILLTHROUGH]  
[,FILTER(<filter criteria>)]  
```  
  
## <a name="arguments"></a>引数  
 *データ*  
 マイニング モデルが追加されるマイニング構造の名前です。  
  
 *model*  
 マイニング モデルの一意の名前です。  
  
 *列定義の一覧*  
 列定義のコンマ区切りのリストです。  
  
 *入れ子になった列の定義リスト*  
 入れ子になったテーブルの列のコンマ区切りのリストです (該当する場合)。  
  
 *入れ子になったフィルター条件*  
 入れ子になったテーブルの列に適用されるフィルター式です。  
  
 *アルゴリズム*  
 プロバイダーによって定義されたデータマイニングアルゴリズムの名前。  
  
> [!NOTE]  
>  現在のプロバイダーでサポートされているアルゴリズムの一覧は、 [DMSCHEMA_MINING_SERVICES Rowset](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/dmschema-mining-services-rowset)を使用して取得できます。 の現在のインスタンスでサポートされている[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]アルゴリズムを表示するには、「[データマイニングのプロパティ](https://docs.microsoft.com/analysis-services/server-properties/data-mining-properties)」を参照してください。  
  
 *パラメーターリスト*  
 任意。 アルゴリズムのプロバイダー定義パラメーターのコンマ区切りのリストです。  
  
 *フィルター条件*  
 ケース テーブルの列に適用されるフィルター式です。  
  
## <a name="remarks"></a>コメント  
 マイニング構造に複合キーが含まれる場合、マイニング モデルは、構造に定義されているすべてのキー列を含む必要があります。  
  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] クラスタリング アルゴリズムと [!INCLUDE[msCoName](../includes/msconame-md.md)] シーケンス クラスター アルゴリズムを使用して作成されるモデルなど、モデルに予測可能列が必要ない場合、ステートメントに列定義を含める必要はありません。 結果モデルのすべての属性は入力として処理されます。  
  
 ケーステーブルに適用される**WITH**句では、フィルター処理とドリルスルーの両方のオプションを指定できます。  
  
-   **フィルター**キーワードとフィルター条件を追加します。 フィルターはマイニング モデルのケースに適用されます。  
  
-   **ドリルスルー**キーワードを追加して、マイニングモデルのユーザーがモデルの結果からケースデータにドリルダウンできるようにします。 データマイニング拡張機能 (DMX) では、ドリルスルーはモデルの作成時にのみ有効にすることができます。  
  
 ケースフィルターとドリルスルーの両方を使用するには、次の例に示す構文を使用して、単一**の WITH**句でキーワードを結合します。  
  
 `WITH DRILLTHROUGH, FILTER(Gender = 'Male')`  
  
## <a name="column-definition-list"></a>列定義リスト  
 モデルの構造を定義するには、各列の次の情報を含む列定義リストを指定します。  
  
-   名前 (必須)  
  
-   別名 (省略可能)  
  
-   モデリングフラグ  
  
-   予測要求。予測可能な値が列に含まれているかどうかをアルゴリズムに示します。これは、 **PREDICT**句または**PREDICT_ONLY**句によって示されます。  
  
 列定義リストの次の構文を使用して、単一列を定義します。  
  
```  
<structure column name>  [AS <model column name>]  [<modeling flags>]    [<prediction>]  
```  
  
### <a name="column-name-and-alias"></a>列名と別名  
 列定義リストで使用する列名は、マイニング構造で使用されている列の名前にする必要があります。 ただし、マイニング モデルの構造列を表すために、必要に応じて別名を定義できます。 同じ構造列に複数の列定義を作成し、列の各コピーに異なる別名と予測の使用方法を割り当てることもできます。 既定では、別名を定義しない場合、構造列の名前が使用されます。 詳細については、「[モデル列の別名を作成](https://docs.microsoft.com/analysis-services/data-mining/create-an-alias-for-a-model-column)する」を参照してください。  
  
 入れ子になったテーブルの列の場合は、入れ子になったテーブルの名前を指定し、データ型を**テーブル**として指定します。次に、モデルに含める入れ子になった列の一覧をかっこで囲んで指定します。  
  
 入れ子になったテーブル列の定義の後にフィルター条件式を配置することで、入れ子になったテーブルに適用されるフィルター式を定義できます。  
  
### <a name="modeling-flags"></a>ModelingFlags  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] では、マイニング モデル列で使用する次のモデリング フラグをサポートしています。  
  
> [!NOTE]  
>  NOT_NULL モデリング フラグは、マイニング構造列に適用されます。 詳細については、「[CREATE MINING STRUCTURE &#40;DMX&#41;](../dmx/create-mining-structure-dmx.md)」を参照してください。  
  
|||  
|-|-|  
|項目|定義|  
|**REGRESSOR**|アルゴリズムが、指定した列を回帰アルゴリズムの回帰式に使用できることを示します。|  
|**MODEL_EXISTENCE_ONLY**|属性列の値が属性の有無ほど重要ではないことを示します。|  
  
 列には複数のモデリング フラグを定義できます。 モデリングフラグの使用方法の詳細については、「 [ &#40;モデリング&#41;フラグ DMX](../dmx/modeling-flags-dmx.md)」を参照してください。  
  
### <a name="prediction-clause"></a>予測句  
 予測句では、予測列の使用方法を説明します。 次の表は、使用可能な句を示しています。  
  
|||  
|-|-|  
|**PREDICT**|この列は、モデルによって予測が可能で、その値は他の予測可能列の値を予測するための入力として使用できます。|  
|**PREDICT_ONLY**|この列は、モデルによって予測が可能ですが、その他の予測可能列の値を予測するためにこの列の値を入力ケースで使用することはできません。|  
  
## <a name="filter-criteria-expressions"></a>フィルター条件式  
 マイニング モデルで使用するケースを制限するフィルターを定義できます。 フィルターは、ケース テーブルの列、入れ子になったテーブルの行、またはその両方に適用できます。  
  
 フィルター条件式は、簡略化された DMX 述語で、WHERE 句に似ています。 フィルター式は、基本的な算術演算子、スカラー、および列名を使用する式に制限されます。 ただし、EXISTS 演算子は例外です。これは、サブクエリに対して少なくとも 1 行が返される場合は true に評価されます。 述語は、共通の論理演算子を使用して組み合わせることができます。AND、OR、および NOT。  
  
 マイニングモデルで使用されるフィルターの詳細については、「[データマイニング&#40;&#41;Analysis Services マイニングモデルのフィルター](https://docs.microsoft.com/analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining)」を参照してください。  
  
> [!NOTE]  
>  フィルター内の列は、マイニング構造列である必要があります。 モデル列または別名の列に対してフィルターを作成することはできません。  
  
 DMX の演算子と構文の詳細については、「[マイニングモデル列](https://docs.microsoft.com/analysis-services/data-mining/mining-model-columns)」を参照してください。  
  
## <a name="parameter-definition-list"></a>パラメーター定義リスト  
 アルゴリズム パラメーターをパラメーター リストに追加して、モデルのパフォーマンスと機能を調整できます。 使用できるパラメーターは、USING 句で指定するアルゴリズムによって異なります。 各アルゴリズムに関連付けられているパラメーターの一覧については、「データマイニング[アルゴリズム&#40;Analysis Services-データマイニング&#41;](https://docs.microsoft.com/analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining)」を参照してください。  
  
 パラメーター リストの構文は次のとおりです。  
  
```  
[<parameter> = <value>, <parameter> = <value>,...]  
```  
  
## <a name="example-1-add-a-model-to-a-structure"></a>例 1 : 構造へのモデルの追加  
 次の例では、Naive Bayes マイニングモデルを**新しいメーリング**マイニング構造に追加し、属性状態の最大数を50に制限しています。  
  
```  
ALTER MINING STRUCTURE [New Mailing]  
ADD MINING MODEL [Naive Bayes]  
(  
    CustomerKey,   
    Gender,  
    [Number Cars Owned],  
    [Bike Buyer] PREDICT  
)  
USING Microsoft_Naive_Bayes (MAXIMUM_STATES = 50)  
```  
  
## <a name="example-2-add-a-filtered-model-to-a-structure"></a>例 2:フィルター選択されたモデルを構造に追加する  
 次の例では、マイニングモデル`Naive Bayes Women`を**新しいメーリング**マイニング構造に追加します。 新しいモデルの基本構造は、例 1 で追加されたマイニング モデルと同じです。ただし、このモデルでは、マイニング構造のケースを 51 歳以上の女性の顧客だけに制限します。  
  
```  
ALTER MINING STRUCTURE [New Mailing]  
ADD MINING MODEL [Naive Bayes Women]  
(  
    CustomerKey,   
    Gender,  
    [Number Cars Owned],  
    [Bike Buyer] PREDICT  
)  
USING Microsoft_Naive_Bayes  
WITH FILTER([Gender] = 'F' AND [Age] >50)  
```  
  
## <a name="example-3-add-a-filtered-model-to-a-structure-with-a-nested-table"></a>例 3: 入れ子になったテーブルを含む構造へのフィルター選択されたモデルの追加  
 次の例では、変更した Market Basket マイニング構造にマイニング モデルを追加します。 この例で使用するマイニング構造は、customer region の属性を含む**region**列を追加するように変更されています。また、 **"高"、"中"** の値を使用して顧客の収入を分類する**収益グループ**列を追加するように変更されています。、または**低**。  
  
 マイニング構造には、顧客が購入した品目を一覧表示する、入れ子になったテーブルも含まれます。  
  
 マイニング構造に入れ子になったテーブルが含まれているため、ケース テーブル、入れ子になったテーブル、またはその両方にフィルターを定義できます。 この例では、ケース フィルターと入れ子になった行フィルターを組み合わせて、Road Tire モデルのいずれかの品目を購入した富裕なヨーロッパの顧客だけにケースを制限します。  
  
```  
ALTER MINING STRUCTURE [Market Basket with Region and Income]  
ADD MINING MODEL [Decision Trees]  
(  
    CustomerKey,   
    Region,  
    [Income Group],  
    [Product] PREDICT (Model)   
WITH FILTER (EXISTS (SELECT * FROM [v Assoc Seq Line Items] WHERE   
 [Model] = 'HL Road Tire' OR  
 [Model] = 'LL Road Tire' OR  
 [Model] = 'ML Road Tire' )  
)  
) WITH FILTER ([Income Group] = 'High' AND [Region] = 'Europe')  
USING Microsoft_Decision Trees  
```  
  
## <a name="see-also"></a>参照  
 [データマイニング拡張&#40;機能&#41; DMX データ定義ステートメント](../dmx/dmx-statements-data-definition.md)   
 [データマイニング拡張&#40;機能&#41; DMX データ操作ステートメント](../dmx/dmx-statements-data-manipulation.md)   
 [データ マイニング拡張機能 &#40;DMX&#41; ステートメント リファレンス](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
