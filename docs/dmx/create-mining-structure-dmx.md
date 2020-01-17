---
title: マイニング構造の作成 (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 87b27f9e1c5927392b4ea221dcb6b7468a42ff9c
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68892822"
---
# <a name="create-mining-structure-dmx"></a>CREATE MINING STRUCTURE (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  データベースに新しいマイニング構造を作成し、必要に応じてトレーニング パーティションとテスト パーティションを定義します。 マイニング構造を作成した後は、 [ALTER マイニング structure &#40;&#41; DMX](../dmx/alter-mining-structure-dmx.md)ステートメントを使用して、マイニング構造にモデルを追加できます。  
  
## <a name="syntax"></a>構文  
  
```  
  
CREATE [SESSION] MINING STRUCTURE <structure>  
(  
    [(<column definition list>)]  
)  
[WITH HOLDOUT (<holdout-specifier> [OR <holdout-specifier>])]  
[REPEATABLE(<holdout seed>)]  
<holdout-specifier>::=  <holdout-maxpercent> PERCENT | <holdout-maxcases> CASES  
```  
  
## <a name="arguments"></a>引数  
 *データ*  
 構造の一意の名前です。  
  
 *列定義の一覧*  
 列定義のコンマ区切りのリストです。  
  
 *予約-maxpercent*  
 テスト用に確保するデータの割合を示す 1 ～ 100 の整数です。  
  
 *予約-maxcases*  
 テストに使用するケースの最大数を示す整数です。  
  
 ケースの最大数に指定された値が入力ケース数を超える場合、すべての入力ケースがテストに使用され、警告が発生します。  
  
> [!NOTE]  
>  ケースの最大数と割合の両方を指定すると、2 つの制限のいずれか小さい方が使用されます。  
  
 *提示したシード*  
 データのパーティション分割を開始するシードとして使用される整数です。  
  
 0 に設定すると、マイニング構造 ID のハッシュがシードとして使用されます。  
  
> [!NOTE]  
>  パーティションを再現できるようにする必要がある場合は、シードを指定する必要があります。  
  
 既定値:REPEATABLE (0)  
  
## <a name="remarks"></a>コメント  
 マイニング構造を定義するには、列リストを指定し、必要に応じて列間の階層リレーションシップを指定して、さらに必要に応じてマイニング構造をトレーニング データセットとテスト データセットにパーティション分割します。  
  
 オプションの SESSION キーワードは、その構造が、現在のセッションの間しか使用できない一時的な構造であることを示します。 セッションが終了すると、構造およびその構造に基づくモデルはすべて削除されます。 一時的なマイニング構造およびモデルを作成するには、まずデータベースプロパティ AllowSessionMiningModels を設定する必要があります。 詳細については、「 [データ マイニング プロパティ](https://docs.microsoft.com/analysis-services/server-properties/data-mining-properties)」を参照してください。  
  
## <a name="column-definition-list"></a>列定義リスト  
 列定義リストに各列の次の情報を含めることによって、マイニング構造を定義します。  
  
-   名前 (必須)  
  
-   データ型 (必須)  
  
-   Distribution  
  
-   モデリングフラグの一覧  
  
-   コンテンツの種類 (必須)  
  
-   RELATED TO 句によって示される、属性列とのリレーションシップです (適用される場合にのみ必須)。  
  
 列定義リストの次の構文を使用して、単一列を定義します。  
  
```  
<column name>    <data type>    [<Distribution>]    [<Modeling Flags>]    <Content Type>    [<column relationship>]  
```  
  
 列定義リストの次の構文を使用して、入れ子になったテーブル列を定義します。  
  
```  
<column name>    TABLE    ( <column definition list> )  
```  
  
 構造列の定義に使用できるデータ型、コンテンツの種類、列の分布、およびモデリングフラグの一覧については、次のトピックを参照してください。  
  
-   [データ型 (データ マイニング)](https://docs.microsoft.com/analysis-services/data-mining/data-types-data-mining)  
  
-   [コンテンツの種類 (データ マイニング)](https://docs.microsoft.com/analysis-services/data-mining/content-types-data-mining)  
  
-   [列の分布 (データ マイニング)](https://docs.microsoft.com/analysis-services/data-mining/column-distributions-data-mining)  
  
-   [モデリング フラグ (データ マイニング)](https://docs.microsoft.com/analysis-services/data-mining/modeling-flags-data-mining)  
  
 列には複数のモデリング フラグ値を定義できます。 ただし、1 つの列に定義できるコンテンツの種類とデータ型はそれぞれ 1 つだけです。  
  
### <a name="column-relationships"></a>列のリレーションシップ  
 列定義ステートメントに句を追加して、2 つの列間のリレーションシップを記述できます。 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]では、次\<の列リレーションシップ > 句の使用がサポートされています。  
  
 **関連**  
 値の階層を示します。 RELATED TO 列の対象にすることが可能なのは、入れ子になったテーブル内のキー列、ケース行内の不連続値の列、RELATED TO 句のある別の列です。これにより、より深い階層が示されます。  
  
## <a name="holdout-parameters"></a>提示されたパラメーター  
 提示されたパラメーターを指定する場合は、構造データのパーティションを作成します。 提示されたパラメーターに指定したデータ量がテスト用に予約され、残りのデータはトレーニングに使用されます。 既定では、[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] を使用してマイニング構造を作成する場合、30% のテスト データと 70% のトレーニング データを含む、提示されたパーティションが作成されます。 詳しくは、「 [Training and Testing Data Sets](https://docs.microsoft.com/analysis-services/data-mining/training-and-testing-data-sets)」をご覧ください。  
  
 データ マイニング拡張機能 (DMX) を使用してマイニング構造を作成する場合、提示されたパーティションが作成されるように手動で指定する必要があります。  
  
> [!NOTE]  
>  **ALTER マイニング STRUCTURE**ステートメントでは、予約はサポートされていません。  
  
 提示されたパラメーターは 3 つまで指定できます。 提示されたケースの最大数と提示されたケースの割合の両方を指定すると、ケースの最大数に達するまでケースの割合が予約されます。 予約のパーセンテージを整数として指定し、その後に**パーセント**キーワードを付けて、ケースの最大数を整数として指定し、その後に**ケース**キーワードを指定します。 次の例に示すように、条件は任意の順序で組み合わせることができます。  
  
```  
WITH HOLDOUT (20 PERCENT)   
WITH HOLDOUT (2000 CASES)   
WITH HOLDOUT (20 PERCENT OR 2000 CASES)   
WITH HOLDOUT (2000 CASES OR 20 PERCENT)  
```  
  
 提示されたシードによって、トレーニング データセットまたはテスト データセットにケースをランダムに割り当てる処理の開始位置が制御されます。 提示されたシードを設定すると、パーティションを反復可能にすることができます。 提示されたシードを指定しない場合、[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] では、マイニング構造の名前を使用してシードが作成されます。 構造の名前を変更すると、シード値が変更されます。 提示されたシード パラメーターは、他の提示されたパラメーターのいずれかまたは両方と共に使用できます。  
  
> [!NOTE]  
>  パーティション情報はトレーニングデータと共にキャッシュされるため、提示を使用するには、マイニング構造の**Cachemode**プロパティが**KeepTrainingData**に設定されていることを確認する必要があります。 これは、の新しいマイニング[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]構造の既定の設定です。 提示されたパーティションを含む既存のマイニング構造で**Cachemode**プロパティを**ClearTrainingCases**に変更しても、処理されたマイニングモデルには影響しません。 ただし、が<xref:Microsoft.AnalysisServices.MiningStructureCacheMode> **KeepTrainingData**に設定されていない場合、提示されたパラメーターは無効になります。 つまり、すべてのソース データがトレーニングに使用され、テスト セットは使用できません。 パーティションの定義は構造と共にキャッシュされます。トレーニング ケースのキャッシュを消去すると、テスト データのキャッシュおよび提示されたセットの定義も消去されます。  
  
## <a name="examples"></a>使用例  
 次の例では、DMX を使用して、提示されたパラメーターによってマイニング構造を作成する方法について説明します。  
  
### <a name="example-1-adding-a-structure-with-no-training-set"></a>例 1 : トレーニングセットのない構造体の追加  
 次の例では、関連するマイニング`New Mailing`モデルを作成せず、予約を使用せずに、という名前の新しいマイニング構造を作成します。 マイニングモデルを構造に追加する方法については、「 [ALTER マイニング&#40;structure&#41;DMX](../dmx/alter-mining-structure-dmx.md)」を参照してください。  
  
```  
CREATE MINING STRUCTURE [New Mailing]  
(  
    CustomerKey LONG KEY,   
    Gender TEXT DISCRETE,  
    [Number Cars Owned] LONG DISCRETE,  
    [Bike Buyer] LONG DISCRETE   
)  
```  
  
### <a name="example-2-specifying-holdout-percentage-and-seed"></a>例 2:提示されたパーセンテージとシードを指定する  
 次の句を列定義リストの後に追加すると、マイニング構造に関連付けられているすべてのマイニング モデルをテストするためのデータセットを定義できます。 このステートメントでは、ケースの最大数を制限せずに、入力ケースの合計の 25% のテスト セットを作成します。 パーティションを作成するためのシードとして 5000 を使用します。 シードを指定した場合は、基になるデータに変更が生じない限り、マイニング構造を処理するたびに、テスト セットに対して同じケースが選択されます。  
  
```  
CREATE MINING STRUCTURE [New Mailing]  
(  
    CustomerKey LONG KEY,   
    Gender TEXT DISCRETE,  
    [Number Cars Owned] LONG DISCRETE,  
    [Bike Buyer] LONG DISCRETE   
)   
WITH HOLDOUT(25 PERCENT) REPEATABLE(5000)  
```  
  
### <a name="example-3-specifying-holdout-percentage-and-max-cases"></a>例 3: 提示された割合と最大ケースの指定  
 次の句では、入力ケースの合計の 25% または 2000 ケースのいずれか少ない方を含むテスト セットを作成します。 シードとして 0 が指定されているので、入力ケースのサンプリングの開始に使用されるシードを作成するためにマイニング構造の名前が使用されます。  
  
```  
CREATE MINING STRUCTURE [New Mailing]  
(  
    CustomerKey LONG KEY,   
    Gender TEXT DISCRETE,  
    [Number Cars Owned] LONG DISCRETE,  
    [Bike Buyer] LONG DISCRETE   
)   
WITH HOLDOUT(25 PERCENT OR 2000 CASES) REPEATABLE(0)  
```  
  
## <a name="see-also"></a>参照  
 [データマイニング拡張&#40;機能&#41; DMX データ定義ステートメント](../dmx/dmx-statements-data-definition.md)   
 [データマイニング拡張&#40;機能&#41; DMX データ操作ステートメント](../dmx/dmx-statements-data-manipulation.md)   
 [データ マイニング拡張機能 &#40;DMX&#41; ステートメント リファレンス](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
