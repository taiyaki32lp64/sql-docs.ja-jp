---
title: 散布図 (Analysis Services - データ マイニング) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- charts [Analysis Services]
- mining models [Analysis Services], validating
- scatter charts
- regression algorithms [Analysis Services]
ms.assetid: 166812ec-fd1c-47c8-88db-d5041142be91
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d3319b72f1c3b37805a653d1f315aa0a3363521a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66082943"
---
# <a name="scatter-plot-analysis-services---data-mining"></a>散布図 (Analysis Services - データ マイニング)
  *散布図* では、モデルで予測された値とデータの実際の値がグラフで比較されます。 実際の値は X 軸に表示され、予測された値は Y 軸に表示されます。 そのほかに、完璧な予測 (予測された値が実際の値と完全に一致する状態) を表す線も表示されます。 この理想的な 45 度の線からの距離により、それぞれの点の予測の正確さがわかります。  
  
## <a name="understanding-the-scatter-plot"></a>散布図について  
 たとえば、マーケティング部門で、販促用電子メールで送信したリンクがクリックされた回数に基づいて毎日の売上を予測するモデルが使用されていたとします。 クリックの回数と売上高はどちらも連続する数値なので、クリックの回数を独立変数とし、売上を従属変数として、グラフに表すことができます。 この場合、グラフの直線は期待される直線関係を表し、直線の周りに散らばる点は、実際のデータがその予測からどれだけ逸脱しているかを表します。 この分析により、一連の結果と特定の入力との関連性と、理想的なモデルからの偏差の大きさがひとめでわかります。  
  
## <a name="interpreting-the-results"></a>結果の解釈  
 次の図は、上で説明したシナリオのために作成された散布図の例を示しています。  
  
 ![線形回帰の散布図の例](../media/scatterplot-callctr.gif "線形回帰の散布図の例")  
  
 直線の周りに散らばっている点の上にマウス ポインターを置くと、予測された値と実際の値がツールヒントに表示されます。 散布図には **[マイニング凡例]** はありませんが、グラフ自体に、モデルに関連付けられているスコアを表示する凡例が含まれています。 詳細については、「[線形回帰モデルのマイニング モデル コンテンツ (Analysis Services - データ マイニング)](mining-model-content-for-linear-regression-models-analysis-services-data-mining.md)」を参照してください。  
  
 グラフの視覚的な表現はクリップボードにコピーできますが、基になるデータや式をコピーすることはできません。 直線の回帰式を表示するには、モデルに対するコンテンツ クエリを作成します。 詳細については、「 [線形回帰モデルのクエリ例](linear-regression-model-query-examples.md)」を参照してください。  
  
## <a name="restrictions-on-scatter-plots"></a>散布図に関する制限  
 散布図は、 **[入力の選択]** タブで選択したモデルに連続する予測可能な属性が含まれている場合にのみ作成できます。 特に項目を選択する必要はありません。モデルと属性の種類に基づいて、 **[リフト チャート]** タブに "散布図" グラフの種類が自動的に表示されます。  
  
 タイム シリーズ モデルでは連続する数値が予測されますが、散布図を使用してタイム シリーズ モデルの精度を測定することはできません。 履歴データの一部を取っておくなど、別の方法を使用できます。 詳細については、「 [タイム シリーズ モデルのクエリ例](time-series-model-query-examples.md)」を参照してください。  
  
## <a name="related-content"></a>関連コンテンツ  
 次のトピックには、散布図および関連する精度チャートの構築方法と使用方法に関する詳細な情報が含まれています。  
  
|トピック|リンク|  
|------------|-----------|  
|Targeted Mailing モデルのリフト チャートの作成方法に関するチュートリアルが含まれています。|[基本的なデータ マイニング チュートリアル](../../tutorials/basic-data-mining-tutorial.md)<br /><br /> [リフト チャートを使用した精度テスト (基本的なデータ マイニング チュートリアル)](../../tutorials/testing-accuracy-with-lift-charts-basic-data-mining-tutorial.md)|  
|関連するグラフの種類について説明します。|[リフト チャート (Analysis Services - データ マイニング)](lift-chart-analysis-services-data-mining.md)<br /><br /> [利益チャート (Analysis Services - データ マイニング)](profit-chart-analysis-services-data-mining.md)<br /><br /> [分類マトリックス &#40;Analysis Services - データ マイニング&#41;](classification-matrix-analysis-services-data-mining.md)|  
|マイニング モデルとマイニング構造の相互検証の使用法について説明します。|[相互検証 (Analysis Services - データ マイニング)](cross-validation-analysis-services-data-mining.md)|  
|リフト チャートおよびその他の精度チャートを作成する手順について説明します。|[テストおよび検証タスク、および操作方法 (データ マイニング)](testing-and-validation-tasks-and-how-tos-data-mining.md)|  
  
## <a name="see-also"></a>参照  
 [テストおよび検証 (データ マイニング)](testing-and-validation-data-mining.md)  
  
  
