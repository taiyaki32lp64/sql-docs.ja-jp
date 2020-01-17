---
title: レッスン 2:Market Basket マイニング構造にマイニング モデルの追加 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: d96a7a7d-35d7-4b34-abb5-f0822c256253
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: b9573d9359983e33cf23533787c26039572710ea
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63204720"
---
# <a name="lesson-2-adding-mining-models-to-the-market-basket-mining-structure"></a>レッスン 2:マイニング モデルを Market Basket マイニング構造に追加する
  このレッスンで作成した Market Basket マイニング構造に 2 つのマイニング モデルを追加[レッスン 1。Market Basket マイニング構造を作成する](../../2014/tutorials/lesson-1-creating-the-market-basket-mining-structure.md)します。 これらのマイニング モデルを使用すると、予測を作成できます。  
  
 使用して 2 つのマイニング モデルを作成すると同時に購入する傾向が強い製品の種類を予測する、 [Microsoft アソシエーション アルゴリズム](../../2014/analysis-services/data-mining/microsoft-association-algorithm.md)と 2 つの異なる値、 *MINIMUM_PROBABILTY*パラメーター。  
  
 *MINIMUM_PROBABILTY*は、[!INCLUDE[msCoName](../includes/msconame-md.md)]アソシエーション アルゴリズム パラメーター ルールが必要な最小の確率を指定することで、マイニング モデルを含むルールの数を決定するのに役立ちます。 たとえば、この値を 0.4 に設定すると、ルールで記述する製品の組み合わせの発生確率が 40% 以上である場合にのみ、ルールが生成されます。  
  
 変更した効果を表示、 *MINIMUM_PROBABILTY*後のレッスンでのパラメーター。  
  
## <a name="alter-mining-structure-statement"></a>ALTER MINING STRUCTURE ステートメント  
 使用するマイニング構造に入れ子になったテーブルを含むマイニング モデルを追加する、 [ALTER MINING STRUCTURE &#40;DMX&#41; ](/sql/dmx/alter-mining-structure-dmx?view=sql-server-2016)ステートメント。 ステートメント内のコードは、次の部分に分けることができます。  
  
-   マイニング構造の指定  
  
-   マイニング モデルの名前指定  
  
-   キー列の定義  
  
-   入力列と予測可能列の定義  
  
-   入れ子になったテーブル列の定義  
  
-   アルゴリズムとパラメーターの変更を特定します。  
  
 入れ子になったテーブル列を含む構造にマイニング モデルを追加する `ALTER MINING STRUCTURE` ステートメントの汎用例を次に示します。  
  
```  
ALTER MINING STRUCTURE [<Mining Structure Name>]  
ADD MINING MODEL [<Mining Model Name>]  
(  
    [<key column>],  
    <mining model column> <usage>,  
    <table columns>  
    (  [<nested key column>],  
       <nested mining model columns> )  
) USING <algorithm>( <algorithm parameters> )  
```  
  
 コードの最初の行では、マイニング モデルの追加先となる既存のマイニング構造を指定します。  
  
```  
ALTER MINING STRUCTURE [<mining structure name>]  
```  
  
 コードの次の行では、マイニング構造に追加するマイニング モデルを指定します。  
  
```  
ADD MINING MODEL [<mining model name>]  
```  
  
 データ マイニング拡張機能 (DMX) でオブジェクトの名前付け方法の詳細については、次を参照してください。[識別子&#40;DMX&#41;](/sql/dmx/identifiers-dmx)します。  
  
 コードの次の行では、マイニング モデルで使用されるマイニング構造で列を定義します。  
  
```  
[<key column>],  
<mining model columns> <usage>,  
```  
  
 使用できるのは、マイニング構造内に既に存在する列だけです。  
  
 マイニング モデル列の一覧の最初の列は、マイニング構造のキー列にする必要があります。 ただし、入力する必要はない`KEY`使用量を指定するキー列の後にします。 マイニング構造の作成時に、この列をキーとして定義済みであるためです。  
  
 残りの行では、新しいマイニング モデルにおける列の使用法を指定します。 マイニング モデル内の列が予測のため、次の構文を使用して、使用されることを指定できます。  
  
```  
<column name> PREDICT,  
```  
  
 使用法を指定しない場合は、データ マイニング構造列を一覧に含める必要がありません。 参照されたデータ マイニング構造で使用されているすべての列が、その構造に基づくマイニング モデルで自動的に使用可能になります。 ただし、使用法を指定していない列は、モデルのトレーニングに使用されません。  
  
 コードの最後の行では、マイニング モデルの生成に使用するアルゴリズムとアルゴリズム パラメーターを定義します。  
  
```  
) USING <algorithm>( <algorithm parameters> )  
```  
  
## <a name="lesson-tasks"></a>このレッスンの作業  
 このレッスンでは、次のタスクを実行するされます。  
  
-   既定の確率を使用して、アソシエーション マイニング モデルを構造に追加します。  
  
-   変更した確率を使用して、アソシエーション マイニング モデルを構造に追加します。  
  
## <a name="adding-an-association-mining-model-to-the-structure-using-the-default-minimumprobability"></a>既定の MINIMUM_PROBABILITY を使用した、構造への Association マイニング モデルの追加  
 最初のタスクがに基づいて、Market Basket マイニング構造に新しいマイニング モデルを追加するには、[!INCLUDE[msCoName](../includes/msconame-md.md)]の既定値を使用してアソシエーション アルゴリズム*MINIMUM_PROBABILITY*します。  
  
#### <a name="to-add-an-association-mining-model"></a>Association マイニング モデルを追加するには  
  
1.  **オブジェクト エクスプ ローラー**のインスタンスを右クリックして[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]、をポイント**新しいクエリ**、をクリックし、 **DMX**します。  
  
     クエリ エディターが開き、新しい空のクエリが表示されます。  
  
    > [!NOTE]  
    >  特定の [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] データベースに対する DMX クエリを作成するには、インスタンスではなくデータベースを右クリックします。  
  
2.  `ALTER MINING STRUCTURE` ステートメントの汎用例を空のクエリにコピーします。  
  
3.  次の部分を探します。  
  
    ```  
    <mining structure name>   
    ```  
  
     これを次の文字列に置き換えます。  
  
    ```  
    [Market Basket]  
    ```  
  
4.  次の部分を探します。  
  
    ```  
    <mining model name>   
    ```  
  
     これを次の文字列に置き換えます。  
  
    ```  
    [Default Association]  
    ```  
  
5.  次の部分を探します。  
  
    ```  
    [<key column>],  
    <mining model columns>,  
    <table columns>  
    (  [<nested key column>],  
       <nested mining model columns> )  
    ```  
  
     これを次の文字列に置き換えます。  
  
    ```  
    OrderNumber,  
        [Products] PREDICT (  
            [Model]  
        )  
    ```  
  
     この場合、`[Products]` テーブルは予測可能列として指定されています。`.`また、`[Model]` 列は入れ子になったテーブルのキー列であるため、入れ子になったテーブル列の一覧に含まれています。  
  
    > [!NOTE]  
    >  入れ子になったキーは、ケース キーとは異なります。 ケース キーは、入れ子になったキー属性をモデル化するには、ケースの一意な識別子です。  
  
6.  次の部分を探します。  
  
    ```  
    USING <algorithm>( <algorithm parameters> )  
    ```  
  
     これを次の文字列に置き換えます。  
  
    ```  
    Using Microsoft_Association_Rules  
    ```  
  
     これで、ステートメントは次のようになります。  
  
    ```  
    ALTER MINING STRUCTURE [Market Basket]  
    ADD MINING MODEL [Default Association]  
    (  
        OrderNumber,  
        [Products] PREDICT (  
            [Model]  
        )  
    )  
    Using Microsoft_Association_Rules  
    ```  
  
7.  **ファイル** メニューのをクリックして**付けて DMXQuery1.dmx を保存**します。  
  
8.  **付けて** ダイアログ ボックスで、適切なフォルダーを参照し、ファイル名前`Default_Association_Model.dmx`します。  
  
9. ツールバーの**Execute**ボタンをクリックします。  
  
## <a name="adding-an-association-mining-model-to-the-structure-changing-the-default-minimumprobability"></a>既定の MINIMUM_PROBABILITY を変更した値による、構造への Association マイニング モデルの追加  
 次に、[!INCLUDE[msCoName](../includes/msconame-md.md)] アソシエーション アルゴリズムに基づいて、Market Basket マイニング構造に別のマイニング モデルを追加します。このとき、MINIMUM_PROBABILITY の既定値を 0.01 に変更します。 パラメーターを変更すると、[!INCLUDE[msCoName](../includes/msconame-md.md)] アソシエーション アルゴリズムによってさらに多くのルールが作成されます。  
  
#### <a name="to-add-an-association-mining-model"></a>Association マイニング モデルを追加するには  
  
1.  **オブジェクト エクスプ ローラー**のインスタンスを右クリックして[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]、をポイント**新しいクエリ**、をクリックし、 **DMX**します。  
  
     クエリ エディターが開き、新しい空のクエリが表示されます。  
  
2.  `ALTER MINING STRUCTURE` ステートメントの汎用例を空のクエリにコピーします。  
  
3.  次の部分を探します。  
  
    ```  
    <mining structure name>   
    ```  
  
     これを次の文字列に置き換えます。  
  
    ```  
    Market Basket  
    ```  
  
4.  次の部分を探します。  
  
    ```  
    <mining model name>   
    ```  
  
     これを次の文字列に置き換えます。  
  
    ```  
    [Modified Association]  
    ```  
  
5.  次の部分を探します。  
  
    ```  
    <mining model columns>,  
    <table columns>  
    (  [<nested key column>],  
       <nested mining model columns> )  
    ```  
  
     これを次の文字列に置き換えます。  
  
    ```  
    OrderNumber,  
    [Products] PREDICT (  
            [Model]  
        )  
    ```  
  
     この場合、`[Products]` テーブルは予測可能列として指定されています。 また、`[MODEL]` 列は入れ子になったテーブルのキー列であるため、一覧に含まれています。  
  
6.  次の部分を探します。  
  
    ```  
    USING <algorithm>( <algorithm parameters> )  
    ```  
  
     これを次の文字列に置き換えます。  
  
    ```  
    USING Microsoft_Association_Rules (Minimum_Probability = 0.1)  
    ```  
  
     これで、ステートメントは次のようになります。  
  
    ```  
    ALTER MINING STRUCTURE [Market Basket]  
    ADD MINING MODEL [Modified Assocation]  
    (  
        OrderNumber,  
        [Products] PREDICT (  
            [Model]  
        )  
    )  
    USING Microsoft_Association_Rules (Minimum_Probability = 0.1)  
    ```  
  
7.  **ファイル** メニューのをクリックして**付けて DMXQuery1.dmx を保存**します。  
  
8.  **付けて** ダイアログ ボックスで、適切なフォルダーを参照し、ファイル名前`Modified Association_Model.dmx`します。  
  
9. ツールバーの**Execute**ボタンをクリックします。  
  
 次のレッスンでは、Market Basket マイニング構造とそれに関連するマイニング モデルを処理します。  
  
## <a name="next-lesson"></a>次のレッスン  
 [レッスン 3:Market Basket マイニング構造の処理](../../2014/tutorials/lesson-3-processing-the-market-basket-mining-structure.md)  
  
  
