---
title: 更新データ (中級者向けデータ マイニング チュートリアル) を使用して時系列予測 |Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: af73681d-ce1c-4b6e-b195-6df3d2fb5275
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 2017defaba74071b1a12bee14a5d8907e4c71cda
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63067558"
---
# <a name="time-series-predictions-using-updated-data-intermediate-data-mining-tutorial"></a>時系列予測での更新後のデータの使用 (中級者向けデータ マイニング チュートリアル)
    
## <a name="creating-predictions-using-the-extended-sales-data"></a>拡張売上データを使用した予測の作成  
 このレッスンでは、モデルに新しい売上データを追加する予測クエリを作成します。 新しいデータでモデルを拡張することにより、最新のデータ ポイントを含む現時点での予測を取得できます。  
  
 新しいデータを使用する時系列予測の作成は簡単ですパラメーター EXTEND_MODEL_CASES を追加するだけですを、 [PredictTimeSeries &#40;DMX&#41; ](/sql/dmx/predicttimeseries-dmx)関数で、新しいデータのソースを指定して指定数。予測を取得します。  
  
> [!WARNING]  
>  パラメーター EXTEND_MODEL_CASES は省略可能です。既定では、入力として新しいデータを結合して時系列予測クエリを作成するたびに、モデルが拡張されます。  
  
#### <a name="to-build-the-prediction-query-and-add-new-data"></a>予測クエリを作成して新しいデータを追加するには  
  
1.  モデルがまだ開いていない場合、Forecasting 構造をダブルクリックし、データ マイニング デザイナーでクリックして、**マイニング モデル予測**タブ。  
  
2.  **マイニング モデルの**ペインで、モデルの予測は既に選択されている必要があります。 選択されていない場合はクリックして**モデルの選択**、モデルを選択します。 予測。  
  
3.  **入力テーブルの選択**ウィンドウで、をクリックして**ケース テーブルの**します。  
  
4.  **テーブルの選択** ダイアログ ボックスで、データ ソースを選択します。[!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)]します。  
  
     データ ソース ビューの一覧から NewSalesData を選択し、クリックして**OK**します。  
  
5.  デザイン領域の画面を右クリックして**接続の変更**します。  
  
6.  使用して、**マッピングの変更** ダイアログ ボックスで、次のように、モデル内の列を外部データ内の列にマップします。  
  
    -   マイニング モデルの ReportingDate 列を入力データで NewDate 列にマップします。  
  
    -   マイニング モデルの Amount 列を入力データで NewAmount 列にマップします。  
  
    -   マイニング モデルの Quantity 列を入力データで NewQty 列にマップします。  
  
    -   入力データの系列の列をマイニング モデルで、ModelRegion 列をマップします。  
  
7.  ここで、予測クエリを作成します。  
  
     最初に、列を予測クエリに追加し、予測を適用する系列を出力します。  
  
    1.  グリッドの場合は、最初の空白行をクリックします**ソース**、し、予測を選択します。  
  
    2.  **フィールド**Model Region 列および**エイリアス**、型`Model Region`します。  
  
8.  次に、予測関数を追加して編集します。  
  
    1.  空の行をクリックし、**ソース**を選択します**予測関数**します。  
  
    2.  **フィールド**、 **PredictTimeSeries**します。  
  
    3.  **エイリアス**、型**Predicted Values**します。  
  
    4.  数量フィールドをドラッグしてから、**マイニング モデルの**ペイン、**条件と引数**列。  
  
    5.  **条件と引数**列で、フィールド名の後に次のテキストを入力します。**5, EXTEND_MODEL_CASES**  
  
         テキストの全文、**条件と引数**テキスト ボックスに次のようにする必要があります。 `[Forecasting].[Quantity],5,EXTEND_MODEL_CASES`  
  
9. クリックして**結果**し、結果を確認します。  
  
     予測は 7 月 (元のデータが終了した後の最初のタイム スライス) から開始し、11 月 (元のデータが終了した後の 5 番目のタイム スライス) で終了しています。  
  
 この種の予測クエリを効率よく使用するには、古いデータがいつ終了し、新しいデータにタイム スライスがいくつあるかを知る必要があります。  
  
 たとえば、このモデルでは、元のデータ系列は 6 月に終了し、データは 7 月、8 月、9 月のものになります。  
  
 EXTEND_MODEL_CASES を使用する予測は常に、元のデータ系列の終了から開始します。 そのため、不明の月の予測のみを取得するには、予測の開始位置と終了位置を指定する必要があります。 どちらの値も、古いデータの終わりから始まるタイム スライスの数として指定されます。  
  
 次の手順は、これを行う方法を示します。  
  
### <a name="change-the-start-and-end-points-of-the-predictions"></a>予測の開始位置と終了位置を変更します。  
  
1.  予測クエリ ビルダーでは、次のようにクリックします。**クエリ**DMX ビューに切り替えます。  
  
2.  PredictTimeSeries 関数が含まれている DMX ステートメントを見つけて、次のように変更します。  
  
     `PredictTimeSeries([Forecasting 12].[Quantity],4,6,EXTEND_MODEL_CASES)`  
  
3.  クリックして**結果**し、結果を確認します。  
  
     予測が 10 月 (元のデータが終了してから 4 番目のタイム スライス) から開始し、12 月 (元のデータが終了してから 6 番目のタイム スライス) で終了するようになります。  
  
## <a name="next-task-in-lesson"></a>このレッスンの次の作業  
 [置き換え後のデータを使用して時系列予測&#40;中級者向けデータ マイニング チュートリアル&#41;](../../2014/tutorials/time-series-predictions-replacement-data-intermediate-data-mining.md)  
  
## <a name="see-also"></a>参照  
 [Microsoft タイム シリーズ アルゴリズム テクニカル リファレンス](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md)   
 [タイム シリーズ モデルのマイニング モデル コンテンツ &#40;Analysis Services - データ マイニング&#41;](../../2014/analysis-services/data-mining/mining-model-content-for-time-series-models-analysis-services-data-mining.md)  
  
  
