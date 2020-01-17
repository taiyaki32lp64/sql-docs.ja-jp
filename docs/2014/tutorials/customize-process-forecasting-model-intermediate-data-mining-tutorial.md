---
title: カスタマイズと処理、予測モデル (中級者向けデータ マイニング チュートリアル) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 4bd25e15-9d9e-4528-b7bc-ccb856643aec
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: d2d0e73d1d9a4058ff63320552604b2bfa1bca8a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63249402"
---
# <a name="customizing-and-processing-the-forecasting-model-intermediate-data-mining-tutorial"></a>予測モデルのカスタマイズと処理 (中級者向けデータ マイニング チュートリアル)
  [!INCLUDE[msCoName](../includes/msconame-md.md)] タイム シリーズ アルゴリズムには、モデルの作成方法と時間データの分析方法に影響するいくつかのパラメーターがあります。 これらのプロパティを変更すると、マイニング モデルでの予測の作成方法に大きく影響する場合があります。  
  
 このチュートリアルでは、次の作業を行ってモデルを変更します。  
  
1.  モデルの新しい値を追加することで時間間隔を処理する方法をカスタマイズ、 *PERIODICITY_HINT*パラメーター。  
  
2.  Microsoft タイム シリーズ アルゴリズムの他の 2 つの重要なパラメーターを学びます。FORECAST_METHOD で、予測に使用する方法を制御することができます、や PREDICTION_SMOOTHING では、することができます、長期間および短期間の予測の組み合わせをカスタマイズできます。  
  
3.  必要に応じて、不足値を帰属させる方法を指定します。  
  
4.  すべての変更が完了したら、モデルを配置して処理します。  
  
## <a name="setting-time-series-parameters"></a>時系列のパラメーターの設定  
 **周期性のヒント**  
  
 *PERIODICITY_HINT*パラメーターは、データに必要な追加の期間についての情報をアルゴリズムに指定します。 時系列モデルでは、既定でデータのパターンの検出が自動的に試行されますが、 予想される周期が既にわかっている場合は、周期性のヒントを指定することでモデルの精度を高めることができます。 ただし、適切でない周期性のヒントを指定すると精度が低下することがあるため、どの値を使用すればよいか確信がない場合は、既定値を使用することをお勧めします。  
  
 たとえば、このモデルで使用されるビューでは、1 か月ごとに [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)] から売上データが集計されます。 したがって、このモデルで使用される各タイム スライスは 1 か月を表し、予測もすべて月単位で行われます。 年の 12 か月間、売り上げのパターンが多いか少ない繰り返している毎年、設定が期待どおりであるため、 *PERIODICITY_HINT*パラメーターを`12`12 のタイム スライスを示すために、(月) が 1 つを構成します。販売サイクルを完了します。  
  
 **予測メソッド**  
  
 *FORECAST_METHOD*パラメーターは、タイム シリーズ アルゴリズムは短期または長期の予測に適しているかどうかを制御します。 既定で、 *FORECAST_METHOD*パラメーターが MIXED、つまり 2 つの異なるアルゴリズムが組み合わされ、短期的および長期的な予測を良い結果を得るためのバランスに設定されます。  
  
 ただし、使用するアルゴリズムが決まっている場合は、ARIMA または ARTXP に値を変更することができます。  
  
 **長期予測と短期的な予測**  
  
 PREDICTION_SMOOTHING パラメーターを使用して、長期予測と短期予測の組み合わせ方法をカスタマイズすることもできます。 既定では、このパラメーターは 0.5 に設定されます。一般には、これが全体的な精度を確保するための最適なバランスです。  
  
#### <a name="to-change-the-algorithm-parameters"></a>アルゴリズム パラメーターを変更するには  
  
1.  **マイニング モデル** タブを右クリックして**Forecasting**、選択と**アルゴリズム パラメーターの設定**します。  
  
2.  `PERIODICITY_HINT`の行、**アルゴリズム パラメーター**ダイアログ ボックスで、をクリックして、**値**列、入力`{12}`、波かっこを含みます。  
  
     既定で、値 {1} も追加されます。  
  
3.  `FORECAST_METHOD`行で、いることを確認、**値**テキスト ボックスは空白のままか、設定を`MIXED`します。 別の値が入力されている場合は、入力`MIXED`パラメーターを既定値に変更します。  
  
4.  **PREDICTION_SMOOTHING**行で、いることを確認、**値**テキスト ボックスは空白のままか、設定を 0.5 にします。 別の値が入力されている場合にクリックします**値**と種類`0.5`パラメーターを既定値に変更します。  
  
    > [!NOTE]  
    >  PREDICTION_SMOOTHING パラメーターは、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Enterprise Edition でのみ使用できます。 したがって、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Standard Edition では PREDICTION_SMOOTHING パラメーターの値を表示または変更できません。 ただし、既定の動作では両方のアルゴリズムが使用され、同等の重み付けが行われます。  
  
5.  **[OK]** をクリックします。  
  
## <a name="handling-missing-data-optional"></a>不足データの処理 (オプション)  
 売上データに NULL で埋められたギャップ (途切れ) が含まれていたり、店舗からのレポートが期限に間に合わなかったために系列の終了時点で空のセルが残されたりすることがよくあります。 このような場合は、[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] から次のエラーが表示されてモデルが処理されません。  
  
 "エラー (データ マイニング)。タイムスタンプが同期されていないシリーズ以降\<系列名 >、マイニング モデルの\<モデル名 >。 すべての時系列は同一の時点で終了する必要があります。また、データ消失点をそれぞれが任意に持つこともできません。 MISSING_VALUE_SUBSTITUTION パラメーターを Previous または数値定数に設定すると、可能な場所にデータ消失点が自動的に設定されます。"  
  
 このエラーを回避するには、次のいずれかの方法で、ギャップを埋めるための新しい値が [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] から自動的に提供されるように指定します。  
  
-   平均値を使用する。 平均は、同じデータ系列のすべての有効値を使用して計算されます。  
  
-   前の値を使用する。 複数の不足セルに前の値を割り当てることは可能ですが、開始値を埋めることはできません。  
  
-   指定した定数値を使用する。  
  
#### <a name="to-specify-that-gaps-be-filled-by-averaging-values"></a>値の平均を計算してギャップを埋めるように指定するには  
  
1.  **マイニング モデル** タブで、右クリックし、 **Forecasting**列、および選択**アルゴリズム パラメーターの設定**します。  
  
2.  **アルゴリズム パラメーター**  ダイアログ ボックスで、 **MISSING_VALUE_SUBSTITUTION**行で、をクリックして、**値**列、および種類`Mean`します。  
  
## <a name="build-the-model"></a>モデルを構築します。  
 モデルを使用するには、サーバーにモデルを配置し、アルゴリズムを使用してトレーニング データを実行することでそのモデルを処理する必要があります。  
  
#### <a name="to-process-the-forecasting-model"></a>予測モデルを処理するには  
  
1.  **マイニング モデルの**のメニュー[!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]を選択します**マイニング構造の処理とすべてのモデル**します。  
  
2.  プロジェクトをビルドおよび配置するかどうかを確認する警告をクリックし、**はい**します。  
  
3.  **マイニング構造の処理 - 予測**ダイアログ ボックスで、をクリックして**実行**します。  
  
     **処理の進行状況**モデルの処理に関する情報を表示するダイアログ ボックスが開きます。 モデルの処理には、時間がかかることがあります。  
  
4.  処理が完了したら、クリックして**閉じる**を終了する、**処理の進行状況** ダイアログ ボックス。  
  
5.  クリックして**閉じる**を終了するには、もう一度、**マイニング構造の処理 - 予測** ダイアログ ボックス。  
  
## <a name="next-task-in-lesson"></a>このレッスンの次の作業  
 [予測モデルの検証&#40;中級者向けデータ マイニング チュートリアル&#41;](../../2014/tutorials/exploring-the-forecasting-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>参照  
 [Microsoft タイム シリーズ アルゴリズム テクニカル リファレンス](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md)   
 [Microsoft タイム シリーズ アルゴリズム](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm.md)   
 [処理の要件および注意事項 &#40;データ マイニング&#41;](../../2014/analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)  
  
  
