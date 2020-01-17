---
title: レッスン 2:時系列マイニング構造にマイニング モデルの追加 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 75c2a74b-21ce-44fb-a26b-68be4c685c12
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: ae0bb91fafb53c0c077a4e0d82558b550d0e6070
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62855715"
---
# <a name="lesson-2-adding-mining-models-to-the-time-series-mining-structure"></a>レッスン 2:時系列マイニング構造へのマイニング モデルの追加
  このレッスンで作成したマイニング構造に新しいマイニング モデルを追加[レッスン 1。タイム シリーズ マイニング モデルとマイニング構造を作成する](../../2014/tutorials/lesson-1-creating-a-time-series-mining-model-and-mining-structure.md)します。  
  
## <a name="alter-mining-structure-statement"></a>ALTER MINING STRUCTURE ステートメント  
 使用する既存のマイニング構造に新しいマイニング モデルを追加するには、 [ALTER MINING STRUCTURE &#40;DMX&#41; ](/sql/dmx/alter-mining-structure-dmx?view=sql-server-2016)ステートメント。 ステートメント内のコードは、次の部分に分けることができます。  
  
-   マイニング構造の指定  
  
-   マイニング モデルの名前指定  
  
-   キー列の定義  
  
-   予測可能列の定義  
  
-   アルゴリズムとパラメーター変更の指定  
  
 ALTER MINING STRUCTURE ステートメントの汎用例を次に示します。  
  
```  
ALTER MINING STRUCTURE [<mining structure name>]  
ADD MINING MODEL [<mining model name>]  
   ([<key columns>],  
    <mining model columns>  
   )  
USING <algorithm name>([<algorithm parameters>])  
[WITH DRILLTHROUGH]  
```  
  
 コードの最初の行では、マイニング モデルの追加先となる既存のマイニング構造を示します。  
  
```  
ALTER MINING STRUCTURE [<mining structure name>]  
```  
  
 コードの次の行では、マイニング構造に追加するマイニング モデルを指定します。  
  
```  
ADD MINING MODEL [<mining model name>]  
```  
  
 DMX でオブジェクトの名前付け方法の詳細については、次を参照してください。[識別子&#40;DMX&#41;](/sql/dmx/identifiers-dmx)します。  
  
 コードの次の数行では、マイニング モデルで使用するマイニング構造の列を定義します。  
  
```  
[<key columns>],  
<mining model columns>  
```  
  
 使用できるのは、マイニング構造内に既に存在する列だけです。一覧の最初の列は、マイニング構造のキー列にする必要があります。  
  
 コードの次の行では、マイニング モデルを生成するマイニング アルゴリズムと、アルゴリズムに設定できるアルゴリズム パラメーターを定義し、マイニング モデルからトレーニング ケースの詳細データの表示にドリル ダウンできるかどうかを指定します。  
  
```  
USING <algorithm name>([<algorithm parameters>])  
WITH DRILLTHROUGH  
```  
  
 調整できるアルゴリズム パラメーターの詳細については、次を参照してください。 [Microsoft タイム シリーズ アルゴリズム テクニカル リファレンス](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md)します。  
  
 次の構文で、マイニング モデルの列を予測に使用するよう指定できます。  
  
```  
<mining model column> PREDICT  
```  
  
## <a name="lesson-tasks"></a>このレッスンの作業  
 このレッスンでは、次のタスクを実行するされます。  
  
-   新しい時系列マイニング モデルを構造に追加します。  
  
-   異なる分析方法と予測方法を使用するようにアルゴリズム パラメーターを変更します。  
  
## <a name="adding-an-arima-time-series-model-to-the-structure"></a>構造への ARIMA 時系列モデルの追加  
 まず、新しい予測マイニング モデルを既存の構造に追加します。 既定では、[!INCLUDE[msCoName](../includes/msconame-md.md)] タイム シリーズ アルゴリズムは、ARIMA および ARTXP の 2 つのアルゴリズムを使用し、その結果を組み合わせて時系列マイニング モデルを作成します。 ただし、アルゴリズムを 1 つだけ使用するように指定することも、正確なアルゴリズムの組み合わせを指定することもできます。 この手順では、ARIMA アルゴリズムのみを使用する新しいモデルを追加します。 このアルゴリズムは、長期的な予測に適しています。  
  
#### <a name="to-add-an-arima-time-series-mining-model"></a>ARIMA 時系列マイニング モデルを追加するには  
  
1.  **オブジェクト エクスプ ローラー**のインスタンスを右クリックして[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]、をポイント**新しいクエリ**、をクリックし、 **DMX**クエリ エディターと新しい空のクエリを開きます。  
  
2.  上の ALTER MINING STRUCTURE ステートメントの汎用例を空のクエリにコピーします。  
  
3.  次の部分を探します。  
  
    ```  
    <mining structure name>   
    ```  
  
     これを次の文字列に置き換えます。  
  
    ```  
    [Forecasting_MIXED_Structure]  
    ```  
  
4.  次の部分を探します。  
  
    ```  
    <mining model name>   
    ```  
  
     これを次の文字列に置き換えます。  
  
    ```  
    Forecasting_ARIMA  
    ```  
  
5.  次の部分を探します。  
  
    ```  
    <key columns>,  
    ```  
  
     これを次の文字列に置き換えます。  
  
    ```  
    [ReportingDate],  
    [ModelRegion]  
    ```  
  
     CREATE MINING MODEL ステートメントで指定したデータ型やコンテンツの種類に関する情報は、マイニング構造に既に保存されているため、繰り返し指定する必要はありません。  
  
6.  次の部分を探します。  
  
    ```  
    <mining model columns>  
    ```  
  
     これを次の文字列に置き換えます。  
  
    ```  
    ([Quantity] PREDICT,  
    [Amount] PREDICT  
    )  
    ```  
  
7.  次の部分を探します。  
  
    ```  
    USING <algorithm name>([<algorithm parameters>])   
    [WITH DRILLTHROUGH]  
    ```  
  
     これを次の文字列に置き換えます。  
  
    ```  
    USING Microsoft_Time_Series (AUTO_DETECT_PERIODICITY = .08, FORECAST_METHOD = 'ARIMA')  
    WITH DRILLTHROUGH  
    ```  
  
     これで、ステートメントは次のようになります。  
  
    ```  
    ALTER MINING STRUCTURE [Forecasting_MIXED_Structure]  
    ADD MINING MODEL [Forecasting_ARIMA]  
       (  
       ([ReportingDate],  
        [ModelRegion],  
        ([Quantity] PREDICT,  
        [Amount] PREDICT  
       )   
    USING Microsoft_Time_Series (AUTO_DETECT_PERIODICITY = .08, FORECAST_METHOD = 'ARIMA')  
    WITH DRILLTHROUGH  
    ```  
  
8.  **ファイル** メニューのをクリックして**付けて DMXQuery1.dmx を保存**します。  
  
9. **付けて** ダイアログ ボックスで、適切なフォルダーを参照し、ファイル名前`Forecasting_ARIMA.dmx`します。  
  
10. ツールバーの**Execute**ボタンをクリックします。  
  
## <a name="adding-an-artxp-time-series-model-to-the-structure"></a>構造への ARTXP 時系列モデルの追加  
 ARTXP アルゴリズムは、SQL Server 2005 の既定のタイム シリーズ アルゴリズムで、短期の予測に適しています。 3 つのアルゴリズムをすべて使用して予測を比較するために、ARTXP アルゴリズムに基づくモデルをもう 1 つ追加します。  
  
#### <a name="to-add-an-artxp-time-series-mining-model"></a>ARTXP 時系列マイニング モデルを追加するには  
  
1.  空のクエリ ウィンドウに次のコードをコピーします。  
  
     変更する必要があるのは、新しいマイニング モデルの名前と FORECAST_METHOD パラメーターの値だけです。  
  
    ```  
    ALTER MINING STRUCTURE [Forecasting_MIXED_Structure]  
    ADD MINING MODEL [Forecasting_ARTXP]  
       (  
       ([ReportingDate],  
        [ModelRegion],  
        ([Quantity] PREDICT,  
        [Amount] PREDICT  
       )   
    USING Microsoft_Time_Series (AUTO_DETECT_PERIODICITY = .08, FORECAST_METHOD = 'ARTXP')  
    WITH DRILLTHROUGH  
    ```  
  
2.  **ファイル** メニューのをクリックして**付けて DMXQuery1.dmx を保存**します。  
  
3.  **付けて** ダイアログ ボックスで、適切なフォルダーを参照し、ファイル名前`Forecasting_ARTXP.dmx`します。  
  
4.  ツールバーの**Execute**ボタンをクリックします。  
  
 次のレッスンでは、すべてのモデルとマイニング構造を処理します。  
  
## <a name="next-lesson"></a>次のレッスン  
 [レッスン 3:タイム シリーズを処理構造およびモデル](../../2014/tutorials/lesson-3-processing-the-time-series-structure-and-models.md)  
  
## <a name="see-also"></a>参照  
 [Microsoft タイム シリーズ アルゴリズム](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm.md)   
 [Microsoft タイム シリーズ アルゴリズム テクニカル リファレンス](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md)  
  
  
