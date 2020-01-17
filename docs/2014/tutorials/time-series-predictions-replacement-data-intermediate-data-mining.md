---
title: 置き換え後のデータ (中級者向けデータ マイニング チュートリアル) を使用して時系列予測 |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: a23a6e1d-1d49-41ea-8314-925dc8e4df5e
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: c96b70775105ea9446810ac3b064ae7cb07d4337
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63312880"
---
# <a name="time-series-predictions-using-replacement-data-intermediate-data-mining-tutorial"></a>時系列予測での置き換え後のデータの使用 (中級者向けデータ マイニング チュートリアル)
  ここでは、全世界の売上データに基づく新しいモデルを作成します。 その後、全世界の売上モデルを個々の地域のいずれかに適用する予測クエリを作成します。  
  
## <a name="building-a-general-model"></a>汎用モデルの作成  
 元のマイニング モデルの結果を分析したところ、地域間や製品ライン間で大きな差が見られました。 たとえば、North America では M200 モデルの売上が強い一方で、T1000 モデルの売上はそれほどでもありません。 ただし、分析は多くのデータ、またはデータの時間内に別の時点で開始一部の系列がありませんでしたという事実によって複雑になります。 不足しているデータもあります。  
  
 ![M200 および T1000 の数量を予測するシリーズ](../../2014/tutorials/media/6series-defaultforecasting.gif "M200 および T1000 の数量を予測するシリーズ")  
  
 データの品質の問題の一部に対処するために、全世界の売上データをマージし、その全体的な売上傾向を使用して、任意の地域の将来の売上を予測するために適用できるモデルを作成します。  
  
 予測を作成する際、全世界の売上データをトレーニングして生成されるパターンを使用しますが、履歴データのポイントをそれぞれの地域の売上データに置き換えます。 これにより、全体的な傾向は維持しながら、各予測値をそれぞれの地域やモデルの売上額の履歴と対応させることができます。  
  
## <a name="performing-cross-prediction-with-a-time-series-model"></a>時系列モデルでのクロス予測の実行  
 ある系列のデータを使用して別の系列の傾向を予測するプロセスのことをクロス予測と呼びます。 クロス予測はさまざまなシナリオで使用できます。たとえば、テレビの売上が経済活動全般の適切な予測子であると特定できれば、テレビの売上でトレーニングしたモデルを全般的な経済データに適用できます。  
  
 SQL Server データ マイニングでの関数の引数に REPLACE_MODEL_CASES パラメーターを使用してクロス予測を実行する[PredictTimeSeries &#40;DMX&#41;](/sql/dmx/predicttimeseries-dmx)します。  
  
 次の作業では、REPLACE_MODEL_CASES の使用方法について学習します。 マージした全世界の売上データを使用してモデルを作成し、汎用モデルを置き換え後のデータにマップする予測クエリを作成します。  
  
 データ マイニング モデルの作成方法については、既に理解していることを前提に、ここでは簡略化して説明しています。  
  
#### <a name="to-build-a-mining-structure-and-mining-model-using-the-aggregated-data"></a>集計データを使用してマイニング構造とマイニング モデルを作成するには  
  
1.  **ソリューション エクスプ ローラー**を右クリックして**マイニング構造**、し、**新しいマイニング構造の**データ マイニング ウィザードを起動します。  
  
2.  データ マイニング ウィザードで、以下の選択を行います。  
  
    -   アルゴリズム:Microsoft タイム シリーズ  
  
    -   モデルのソースとして、この高度なレッスンで既に作成したデータ ソースを使用する。 参照してください[タイム シリーズ予測を高度な&#40;中級者向けデータ マイニング チュートリアル&#41;](../../2014/tutorials/advanced-time-series-predictions-intermediate-data-mining-tutorial.md)します。  
  
         データ ソース ビュー: `AllRegions`  
  
    -   系列キーおよび時間キーの列として、次の列を選択する。  
  
         キー時刻:ReportingDate  
  
         キー:Region  
  
    -   `Input` および `Predict` の列として、次の列を選択する。  
  
         SumQty  
  
         SumAmt  
  
         AvgAmt  
  
         AvgQty  
  
    -   **マイニング構造名**種類。 `All Regions`  
  
    -   **マイニング モデル名**種類。 `All Regions`  
  
3.  新しい構造と新しいモデルを処理します。  
  
#### <a name="to-build-the-prediction-query-and-map-the-replacement-data"></a>予測クエリを作成して置き換え後のデータをマップするには  
  
1.  モデルがまだ開いていない場合、AllRegions 構造をダブルクリックし、データ マイニング デザイナーでクリックして、**マイニング モデル予測**タブ。  
  
2.  **マイニング モデルの**ペインで、モデル AllRegions が選択されている必要があります。 選択されていない場合はクリックして**モデルの選択**、モデル AllRegions を選択します。  
  
3.  **入力テーブルの選択**ウィンドウで、をクリックして**ケース テーブルの**します。  
  
4.  **テーブルの選択**ダイアログ ボックスで、変更データをソースを T1000 Pacific Region、 をクリックし、 **OK**します。  
  
5.  マイニング モデルと入力データ間の結合線を右クリックして**接続の変更**します。 次のように、データ ソース ビューのデータをモデルにマップします。  
  
    1.  マイニング モデルの ReportingDate 列が入力データの ReportingDate 列にマップされていることを確認します。  
  
    2.  **マッピングの変更**AvgQty、モデル列の行で、ダイアログ ボックスの **テーブル列**T1000 Pacific.Quantity を選択するとします。 **[OK]** をクリックします。  
  
         この手順によって、平均数量を予測するモデルで作成した列が T1000 系列の販売数量の実際のデータにマップされます。  
  
    3.  どの入力列には、モデルの列領域はマップできません。  
  
         モデルはすべての系列にわたってデータを集計しているので、T1000 Pacific などの系列値に一致するものはなく、予測クエリが実行されるとエラーが発生します。  
  
6.  ここで、予測クエリを作成します。  
  
     まず、モデルから予測と共に AllRegions ラベルを出力する列を結果に追加します。 これにより、汎用モデルに基づく結果であることがわかるようになります。  
  
    1.  グリッドの場合は、最初の空白行をクリックします**ソース**、し AllRegions マイニング モデルを選択します。  
  
    2.  **フィールド**リージョンを選択します。  
  
    3.  **エイリアス**、型**モデルが使用される**します。  
  
7.  次に、予測がどの系列に対するものかを表す別のラベルを結果に追加します。  
  
    1.  空の行をクリックし、**ソース**を選択します**カスタム式**します。  
  
    2.  **エイリアス**列に「 **ModelRegion**します。  
  
    3.  **条件と引数**列に「`'T1000 Pacific'`します。  
  
8.  ここで、クロス予測関数を設定します。  
  
    1.  空の行をクリックし、**ソース**を選択します**予測関数**します。  
  
    2.  **フィールド**列で、 **PredictTimeSeries**します。  
  
    3.  **エイリアス**、型**Predicted Values**します。  
  
    4.  フィールド AvgQty をドラッグしてから、**マイニング モデルの**ペイン、**条件と引数**ドラッグ アンド ドロップ操作を使用して列。  
  
    5.  **条件と引数**列で、フィールド名の後に次のテキストを入力します。 `,5, REPLACE_MODEL_CASES`  
  
         テキストの全文、**条件と引数**テキスト ボックスに次のようにする必要があります。 `[AllRegions].[AvgQty],5,REPLACE_MODEL_CASES`  
  
9. クリックして**結果**します。  
  
## <a name="creating-the-cross-prediction-query-in-dmx"></a>DMX でのクロス予測クエリの作成  
 既にお気付きかもしれませんが、クロス予測で別のデータ系列 (北米地域の T1000 製品モデルなど) に汎用モデルを適用するには、系列ごとに異なるクエリを作成し、それぞれの入力セットをモデルにマップできるようにする必要があります。  
  
 ただし、デザイナーでクエリを作成する代わりに、DMX ビューに切り替えて、作成した DMX ステートメントを編集することができます。 たとえば、次の DMX ステートメントは、先ほど作成したクエリを表します。  
  
```  
SELECT  
      ([All Regions].[Region]) as [Model Used],  
      ('T-1000 Pacific') as [ModelRegion],  
      (PredictTimeSeries([All Regions].[Avg Qty],5, REPLACE_MODEL_CASES)) as [Predicted Quantity]  
     FROM [All Regions]  
PREDICTION JOIN  
    OPENQUERY([Adventure Works DW2003R2], 'SELECT [ReportingDate] FROM  
      (  
       SELECT  ReportingDate, ModelRegion, Quantity, Amount   
       FROM dbo.vTimeSeries   
       WHERE (ModelRegion = N''T1000 Pacific'')  
       ) as [T1000 Pacific]    ')   
    AS t  
ON   
[All Regions].[Reporting Date] = t.[ReportingDate]   
AND   
[All Regions].[Avg Qty] = t.[Quantity]  
```  
  
 このクエリを別のモデルに適用するには、クエリ ステートメントを編集して、フィルター条件を置き換え、各結果に関連付けられているラベルを更新するだけで済みます。  
  
 たとえば、'Pacific' を 'North America' に置き換えてフィルター条件と列ラベルを変更すると、汎用モデル内のパターンに基づく北米の T1000 製品の予測を取得できます。  
  
## <a name="next-task-in-lesson"></a>このレッスンの次の作業  
 [予測モデルの予測を比較する&#40;中級者向けデータ マイニング チュートリアル&#41;](../../2014/tutorials/comparing-predictions-for-forecasting-models-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>参照  
 [タイム シリーズ モデルのクエリ例](../../2014/analysis-services/data-mining/time-series-model-query-examples.md)   
 [PredictTimeSeries &#40;DMX&#41;](/sql/dmx/predicttimeseries-dmx)  
  
  
