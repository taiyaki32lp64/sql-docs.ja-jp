---
title: レッスン 4:Bike Buyer マイニング モデルの参照 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 8de3c500-f881-42da-a096-b6c03300d58d
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 709df371d840d4b24e420b4fcd08750fd31e8075
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63070893"
---
# <a name="lesson-4-browsing-the-bike-buyer-mining-models"></a>レッスン 4:Bike Buyer マイニング モデルの参照
  このレッスンでは、使用、 [SELECT (DMX)](/sql/dmx/select-dmx)デシジョン ツリー モデルとマイニングをクラスタ リングでコンテンツを参照するステートメントをモデル化で作成した[レッスン 2。予測マイニング構造にマイニング モデルの追加](../../2014/tutorials/lesson-2-adding-mining-models-to-the-bike-buyer-mining-structure.md)します。  
  
 マイニング モデルに含まれる列は、マイニング構造で定義されている列ではなく、アルゴリズムによって検出された傾向とパターンを記述している、特定の列のセットです。 これらのマイニング モデル列に記載されて、 [DMSCHEMA_MINING_MODEL_CONTENT 行セット](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/dmschema-mining-model-content-rowset)スキーマ行セット。 たとえば、コンテンツ スキーマ行セットの MODEL_NAME 列には、マイニング モデルの名前が含まれます。 クラスター マイニング モデルの場合、NODE_CAPTION 列には各クラスターの名前が含まれ、NODE_DESCRIPTION 列には各クラスターの特性の説明が含まれます。 SELECT FROM を使用してこれらの列を参照する\<モデル >。DMX でコンテンツのステートメント。 このステートメントを使用すると、マイニング モデルの作成に使用されたデータを調査することもできます。 このステートメントを使用するには、マイニング構造上でドリルスルーを有効にする必要があります。 ステートメントの詳細については、次を参照してください。 [SELECT FROM&#60;モデル&#62;します。ケース&#40;DMX&#41;](/sql/dmx/select-from-model-content-dmx)します。  
  
 SELECT DISTINCT ステートメントを使用することにより、不連続列のすべての状態を返すこともできます。 たとえば、性別の列でこの操作を実行すると、クエリでは `male` と `female` が返されます。  
  
## <a name="lesson-tasks"></a>このレッスンの作業  
 このレッスンでは、次のタスクを実行するされます。  
  
-   マイニング モデルに含まれる内容の調査  
  
-   マイニング モデルのトレーニングに使用されたソース データからケースを返す  
  
-   特定の不連続列に対して可能な状態の調査  
  
## <a name="returning-the-content-of-a-mining-model"></a>マイニング モデルの内容を返す  
 このレッスンでは使用して、 [SELECT FROM&#60;モデル&#62;します。コンテンツ&#40;DMX&#41; ](/sql/dmx/select-from-model-dimension-content-dmx)ステートメントは、クラスタ リング モデルの内容を返します。  
  
 SELECT FROM の汎用例を次に\<モデル >。コンテンツのステートメント。  
  
```  
SELECT <select list> FROM [<mining model>].CONTENT  
WHERE <where clause>  
```  
  
 コードの 1 行目では、マイニング モデルの内容から返す列と、それらの列が関連付けられているマイニング モデルを定義します。  
  
```  
SELECT <select list> FROM [<mining model].CONTENT  
```  
  
 マイニング モデル名の後の .CONTENT 句は、マイニング モデルから内容を返すことを示します。 マイニング モデルに含まれる列に関する詳細については、次を参照してください。 [DMSCHEMA_MINING_MODEL_CONTENT 行セット](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/dmschema-mining-model-content-rowset)します。  
  
 コードの最終行では、ステートメントで返される結果をフィルター選択します。この行は省略可能です。  
  
```  
WHERE <where clause>  
```  
  
 たとえば、クエリの結果を制限して、多数のケースが含まれるクラスターのみを返すようにする場合は、SELECT ステートメントに次の WHERE 句を追加します。  
  
```  
WHERE NODE_SUPPORT > 100  
```  
  
 WHERE ステートメントの使用に関する詳細については、次を参照してください。[選択&#40;DMX&#41;](/sql/dmx/select-dmx)します。  
  
#### <a name="to-return-the-content-of-the-clustering-mining-model"></a>クラスター マイニング モデルの内容を返すには  
  
1.  **オブジェクト エクスプ ローラー**のインスタンスを右クリックして[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]、をポイント**新しいクエリ**、をクリックし、 **DMX**します。  
  
     クエリ エディターが開き、新しい空のクエリが表示されます。  
  
2.  SELECT FROM の汎用例をコピー\<モデル >。空のクエリにコンテンツのステートメント。  
  
3.  次の部分を探します。  
  
    ```  
    <select list>   
    ```  
  
     これを次の文字列に置き換えます。  
  
    ```  
    *  
    ```  
  
     置換することもできます * のいずれかに含まれる列の一覧で、 [DMSCHEMA_MINING_MODEL_CONTENT 行セット](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/dmschema-mining-model-content-rowset)します。  
  
4.  次の部分を探します。  
  
    ```  
    [<mining model>]   
    ```  
  
     これを次の文字列に置き換えます。  
  
    ```  
    [Clustering]  
    ```  
  
     最終的なステートメントは次のようになります。  
  
    ```  
    SELECT * FROM [Clustering].CONTENT  
    ```  
  
5.  **ファイル** メニューのをクリックして**付けて DMXQuery1.dmx を保存**します。  
  
6.  **付けて** ダイアログ ボックスで、適切なフォルダーを参照し、ファイル名前`SELECT_CONTENT.dmx`します。  
  
7.  ツールバーの**Execute**ボタンをクリックします。  
  
     クエリが実行され、マイニング モデルの内容が返されます。  
  
## <a name="use-drillthrough"></a>ドリルスルーの使用  
 次の手順では、ドリルスルー ステートメントを使用して、デシジョン ツリー マイニング モデルのトレーニングに使用されたケースの一部を返します。 このレッスンでは使用して、 [SELECT FROM&#60;モデル&#62;します。ケース&#40;DMX&#41; ](/sql/dmx/select-from-model-content-dmx)ステートメント、デシジョン ツリー モデルの内容を返します。  
  
 SELECT FROM の汎用例を次に\<モデル >。ステートメントの場合:  
  
```  
SELECT <select list>   
FROM [<mining model>].CASES  
WHERE IsInNode('<node id>')  
```  
  
 コードの 1 行目では、ソース データから返す列と、それらの列が含まれるマイニング モデルを定義します。  
  
```  
SELECT <select list> FROM [<mining model>].CASES  
```  
  
 .CASES 句は、ドリルスルー クエリを実行することを示します。 ドリルスルーを使用するには、マイニング モデルの作成時にドリルスルーを有効にする必要があります。  
  
 コードの最終行では、ケースを要求するマイニング モデル内のノードを指定します。この行は省略可能です。  
  
```  
WHERE IsInNode('<node id>')  
```  
  
 IsInNode で WHERE ステートメントの使用に関する詳細については、次を参照してください。 [SELECT FROM&#60;モデル&#62;します。ケース&#40;DMX&#41;](/sql/dmx/select-from-model-content-dmx)します。  
  
#### <a name="to-return-the-cases-that-were-used-to-train-the-mining-model"></a>マイニング モデルのトレーニングに使用されたケースを返すには  
  
1.  **オブジェクト エクスプ ローラー**のインスタンスを右クリックして[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]、をポイント**新しいクエリ**、をクリックし、 **DMX**します。  
  
     クエリ エディターが開き、新しい空のクエリが表示されます。  
  
2.  SELECT FROM の汎用例をコピー\<モデル >。空のクエリに CASES ステートメント。  
  
3.  次の部分を探します。  
  
    ```  
    <select list>   
    ```  
  
     これを次の文字列に置き換えます。  
  
    ```  
    *  
    ```  
  
     \* は、ソース データ内に含まれる任意の列の一覧 ([Bike Buyer] など) に置き換えることもできます。  
  
4.  次の部分を探します。  
  
    ```  
    [<mining model>]   
    ```  
  
     これを次の文字列に置き換えます。  
  
    ```  
    [Decision Tree]  
    ```  
  
     最終的なステートメントは次のようになります。  
  
    ```  
    SELECT *   
    FROM [Decision Tree].CASES  
    ```  
  
5.  **ファイル** メニューのをクリックして**付けて DMXQuery1.dmx を保存**します。  
  
6.  **付けて** ダイアログ ボックスで、適切なフォルダーを参照し、ファイル名前`SELECT_DRILLTHROUGH.dmx`します。  
  
7.  ツールバーの**Execute**ボタンをクリックします。  
  
     クエリが実行され、デシジョン ツリー マイニング モデルのトレーニングに使用されたソース データが返されます。  
  
## <a name="return-the-states-of-a-discrete-mining-model-column"></a>マイニング モデルの不連続列の状態を返す  
 次の手順では、SELECT DISTINCT ステートメントを使用して、指定されたマイニング モデル列に対して可能な状態を返します。  
  
 SELECT DISTINCT ステートメントの汎用例を次に示します。  
  
```  
SELECT DISTINCT [<column>]   
FROM [<mining model>]  
```  
  
 コードの 1 行目では、状態を返すマイニング モデル列を定義します。  
  
```  
SELECT DISTINCT [<column>]   
```  
  
 列のすべての状態を返すには、DISTINCT を含める必要があります。 DISTINCT を指定しない場合は、ステートメント全体が予測用のショートカットとなり、指定した列で最も可能性の高い状態が返されます。 詳細については、「[SELECT &#40;DMX&#41;](/sql/dmx/select-dmx)」を参照してください。  
  
#### <a name="to-return-the-states-of-a-discrete-column"></a>不連続列の状態を返すには  
  
1.  **オブジェクト エクスプ ローラー**のインスタンスを右クリックして[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]、をポイント**新しいクエリ**、をクリックし、 **DMX**します。  
  
     クエリ エディターが開き、新しい空のクエリが表示されます。  
  
2.  上の SELECT Distinct ステートメントの汎用例を空のクエリにコピーします。  
  
3.  次の部分を探します。  
  
    ```  
    [<column,name>   
    ```  
  
     これを次の文字列に置き換えます。  
  
    ```  
    [Bike Buyer]  
    ```  
  
4.  次の部分を探します。  
  
    ```  
    [<mining model>]   
    ```  
  
     これを次の文字列に置き換えます。  
  
    ```  
    [Decision Tree]  
    ```  
  
     最終的なステートメントは次のようになります。  
  
    ```  
    SELECT DISTINCT [Bike Buyer]   
    FROM [Decision Tree]  
    ```  
  
5.  **ファイル** メニューのをクリックして**付けて DMXQuery1.dmx を保存**します。  
  
6.  **付けて** ダイアログ ボックスで、適切なフォルダーを参照し、ファイル名前`SELECT_DISCRETE.dmx`します。  
  
7.  ツールバーの**Execute**ボタンをクリックします。  
  
     クエリが実行され、Bike Buyer 列の可能な状態が返されます。  
  
 次のレッスンでは、デシジョン ツリー マイニング モデルを使用して、潜在顧客が自転車の購入者になるかどうかを予測します。  
  
## <a name="next-lesson"></a>次のレッスン  
 [レッスン 5: 予測クエリの実行](../../2014/tutorials/lesson-5-executing-prediction-queries.md)  
  
  
