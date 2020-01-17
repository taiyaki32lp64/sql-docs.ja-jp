---
title: Microsoft タイム シリーズ ビューアーを使用してモデルの参照 |Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data mining [Analysis Services], continuous columns
- mining model content, viewing
- Microsoft Time Series Viewer
- charts [Analysis Services]
- Time Series Viewer [Analysis Services]
- continuous columns
- regression algorithms [Analysis Services]
ms.assetid: a77c16cd-1cd0-4fc5-afeb-d1dab30d1e25
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 85767ce54991950e75b39bf909d6d0ff3cb2cd8c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66085976"
---
# <a name="browse-a-model-using-the-microsoft-time-series-viewer"></a>Microsoft タイム シリーズ ビューアーを使用したモデルの参照
  [!INCLUDE[msCoName](../../includes/msconame-md.md)]  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] タイム シリーズ ビューアーには、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] タイム シリーズ アルゴリズムを使用して作成されたマイニング モデルが表示されます。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] タイム シリーズ アルゴリズムは回帰アルゴリズムであり、予測シナリオで製品売上などの連続列を予測するデータ マイニング モデルを作成します。 これらの時系列モデルには、次のようなアルゴリズムに基づく情報を含めることができます。  
  
-   ARTxp アルゴリズム。短期的な予測に適しています。  
  
-   ARIMA アルゴリズム。長期的な予測に適しています。  
  
-   ARTxp アルゴリズムと ARIMA アルゴリズムの組み合わせ。  
  
 これらのアルゴリズムの詳細については、「 [Microsoft Time Series Algorithm](microsoft-time-series-algorithm.md) 」(Microsoft Time Series アルゴリズム) および「 [Microsoft Time Series Algorithm Technical Reference](microsoft-time-series-algorithm-technical-reference.md)」(Microsoft Time Series アルゴリズム テクニカル リファレンス) を参照してください。  
  
> [!NOTE]  
>  モデルで使用された式と、検出されたパターンの詳細情報を表示するには、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 汎用コンテンツ ツリー ビューアーを使用します。 詳細については、「[Microsoft 汎用コンテンツ ツリー ビューアーを使用したモデルの参照](browse-a-model-using-the-microsoft-generic-content-tree-viewer.md)」または「[Microsoft 汎用コンテンツ ツリー ビューアー (データ マイニング)](../microsoft-generic-content-tree-viewer-data-mining.md)」を参照してください。  
  
##  <a name="BKMK_ViewerTabs"></a> ビューアーのタブ  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]でマイニング モデルを参照すると、そのモデルに適したビューアーを使用してデータ マイニング デザイナーの **[マイニング モデル ビューアー]** タブにモデルが表示されます。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] タイム シリーズ ビューアーには次のタブがあります。  
  
-   [[モデル]](#BKMK_Tree)  
  
-   [グラフ](#BKMK_Charts)  
  
 **注** モデル コンテンツおよび [マイニング凡例] に表示される情報は、モデルで使用されているアルゴリズムによって異なります。 ただし、 **[モデル]** タブと **[グラフ]** タブは、アルゴリズムの組み合わせに関係なく同じです。  
  
###  <a name="BKMK_Tree"></a> [モデル]  
 時系列モデルを作成すると、完成したモデルがツリーとして [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] に表示されます。 データに複数のケース系列が含まれている場合、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] によって系列ごとに個別のツリーが作成されます。 たとえば、太平洋地域、北アメリカ地域、およびヨーロッパ地域の売上を予測するとします。 これらの各地域の予測は、ケース系列です。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] では、これらの系列ごとに個別のツリーが作成されます。 特定の系列を表示するには、 **[ツリー]** ボックスの一覧から系列を選択します。  
  
 時系列モデルでは、各ツリーに **[すべて]** ノードが含まれており、さらに、アルゴリズムで検出された周期的構造を表す一連のノードに分かれています。 各ノードをクリックすると、ケースの数や式などの統計情報が表示されます。  
  
 ARTxp だけを使用してモデルを作成した場合、ルート ノードの **[マイニング凡例]** には、ケースの合計数だけが含まれています。 ルート以外の各ノードの **[マイニング凡例]** には、その分割ツリーに関する詳細情報が含まれています。たとえば、ノードの式やケースの数が表示されます。 凡例の *ルール* には、系列を識別する情報、およびルールが適用されるタイム スライスが含まれます。 たとえば、 `M200 Europe Amount -2` という凡例テキストは、2 タイム スライス前の期間における M200 Europe 系列のモデルをノードが表すことを示します。  
  
 ARIMA だけを使用してモデルを作成した場合、 **[モデル]** タブには、 **[すべて]** というキャプションの 1 つのノードが含まれています。 ルート ノードの **[マイニング凡例]** には、ARIMA 式が含まれています。  
  
 アルゴリズムを混用するモデルを作成した場合、ルート ノードには、ケースの数と ARIMA 式だけが含まれています。 ルート ノードの後、ツリーは周期的構造ごとに個別のノードに分かれます。 ルート以外の各ノードの [マイニング凡例] には、ARTxp と ARIMA の両方のアルゴリズム、ノードの式、およびノード内のケースの数が含まれています。 最初に ARTxp 式が表示され、ツリー ノード式のラベルが付いています。 その後に ARIMA 式が表示されます。 この情報を解釈する方法の詳細については、「 [Microsoft Time Series Algorithm Technical Reference](microsoft-time-series-algorithm-technical-reference.md)」(Microsoft Time Series アルゴリズム テクニカル リファレンス) を参照してください。  
  
 一般に、デシジョン ツリー グラフでは、最も重要な分割である **[すべて]** ノードが、ビューアーの左側に表示されます。 デシジョン ツリーにおいて、 **[すべて]** ノードの後にある分割が最も重要です。トレーニング データ内のケースを分割するための最も強い条件が含まれているためです。 時系列モデルでは、メインの分岐は最も可能性の高い周期性を表します。 **[すべて]** ノードの後の分割が、分岐の右側に表示されます。  
  
 ツリー内の個々のノードを展開したり折りたたんだりすると、各ノードの後にある分割を表示または非表示にすることができます。 また、 **[デシジョン ツリー]** タブのオプションを使用して、ツリーの表示方法を変更することもできます。 ツリーに表示されるレベルの数を調整するには、 **[表示レベル]** スライダーを使用します。 モデル内のすべてのツリーに表示される既定のレベル数を設定するには、 **[既定の展開]** を使用します。  
  
 各ノードの背景色の網掛けは、ノード内のケースの数を表します。 ノード内の正確なケース数を確認するには、ノードにポインターを合わせて、ノードのヒントを表示します。  
  
 [トップに戻る](#BKMK_ViewerTabs)  
  
###  <a name="BKMK_Charts"></a> グラフ  
 **[グラフ]** タブには、時間の経過に伴う予測属性の動作を表すグラフと、予測される将来値が 5 つ表示されます。 グラフの縦軸はタイム シリーズの値を表し、横軸は時間を表します。  
  
> [!NOTE]  
>  時間軸で使用されるタイム スライスは、データで使用される単位に依存し、日、月、さらには秒を表すこともあります。  
  
 絶対曲線と相対曲線を切り替えるには、 **[絶対値]** ボタンを使用します。 グラフに複数のモデルが含まれている場合、各モデルのデータのスケールが大きく異なる可能性があります。 絶対曲線を使用した場合、あるモデルが平坦な線を示す一方で、別のモデルが大きな変化を示すことがあります。 これは、片方のモデルの目盛りが他方のモデルの目盛りよりも大きいためです。 相対曲線に切り替えると、絶対値ではなく変化の割合が目盛りとして示されるようになります。 これによって、異なる目盛りに基づくモデルどうしの比較が簡単になります。  
  
 マイニング モデルに複数の時系列が含まれている場合、1 つ以上の系列を選択してグラフに表示できます。 ビューアーの右側にある一覧をクリックし、必要な系列を一覧から選択します。 グラフが複雑になりすぎた場合、凡例にある系列のチェック ボックスをオンまたはオフにすることで、表示する系列をフィルターで選択できます。  
  
 グラフには、履歴データと将来のデータの両方が表示されます。 履歴データと区別できるよう、予測データの部分は網掛けされて表示されます。 履歴データの値は実線、予測データの値は点線で示されます。 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] または [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]のプロパティを設定することで、各データ系列の線の色を変更できます。 詳細については、「 [データ マイニング ビューアーで使用する色の変更](change-the-colors-used-in-the-data-mining-viewer.md)」を参照してください。  
  
 表示する時間の範囲はズーム オプションを使用して調整できます。 また、特定の時間範囲を表示することもできます。その場合は、グラフをクリックし、グラフ上で時間の選択をドラッグし、再びクリックして選択した範囲を拡大します。  
  
 モデル内に表示する将来の時間 **ステップ** の数を選択するには、 **[予測期間]** を使用します。 **[偏差の表示]** チェック ボックスをオンにすると、ビューアーに誤差範囲が表示され、予測値の精度を確認できるようになります。  
  
 [トップに戻る](#BKMK_ViewerTabs)  
  
## <a name="see-also"></a>関連項目  
 [マイニング モデル ビューアーのタスクと操作方法](mining-model-viewer-tasks-and-how-tos.md)   
 [Microsoft Time Series Algorithm](microsoft-time-series-algorithm.md)   
 [Time Series Model Query Examples](time-series-model-query-examples.md)   
 [データ マイニング モデル ビューアー](data-mining-model-viewers.md)  
  
  
