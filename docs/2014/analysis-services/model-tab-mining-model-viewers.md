---
title: モデル タブ (マイニング モデル ビューアー) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.timeseries.decisiontree.f1
ms.assetid: 50570bb4-fcac-411e-b530-0398437efda7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 05c0a25ceded07264e4dbe10467e9dc6f093f6c0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66077622"
---
# <a name="model-tab-mining-model-viewers"></a>[モデル] タブ (マイニング モデル ビューアー)
  Microsoft タイム シリーズ ビューアーの **[モデル]** タブは、タイム シリーズの表現をグラフのノードとして表示します。これは、デシジョン ツリー モデルで使用されるものに似ています。  
  
 時系列分析に関する有用な情報を抽出するには、グラフの式、ARIMA 期間、および係数を含むタイム シリーズ モデルのこのビューを使用します。  
  
 **詳細情報。** [Microsoft タイム シリーズ アルゴリズム](data-mining/microsoft-time-series-algorithm.md)、 [、Microsoft タイム シリーズ ビューアーを使用してモデルの参照](data-mining/browse-a-model-using-the-microsoft-time-series-viewer.md)、 [Microsoft タイム シリーズ アルゴリズム](data-mining/microsoft-time-series-algorithm.md)  
  
## <a name="options"></a>および  
 **ビューアーのコンテンツを更新します。**  
 ビューアーにマイニング モデルを再読み込みします。  
  
 **[マイニング モデル]**  
 表示するマイニング モデルを選択します。 関連付けられているビューアーが開き、マイニング モデルが表示されます。  
  
 **ビューアー**  
 選択したマイニング モデルを調べるために使用するビューアーを選択します。 このモデルの種類用のカスタム ビューアーまたは **Microsoft 汎用コンテンツ ツリー** ビューアーを使用できます。 利用可能な場合プラグイン ビューアーを使用することもできます。  
  
 **ズーム イン**  
 ダイアグラムを拡大します。  
  
 **ズーム アウト**  
 グラフを縮小します。  
  
 **グラフ ビューのコピー**  
 ダイアグラムで表示されている部分をクリップボードにコピーします。  
  
 **グラフ全体のコピー**  
 ダイアグラム全体をクリップボードにコピーします。  
  
 **ウィンドウに合わせてダイアグラムの倍率**  
 画面の大きさに合うようにダイアグラム全体を縮小します。  
  
 **ツリー**  
 ビューアーに表示するツリーをドロップダウン リストから選択します。  
  
 タイム シリーズ モデルに複数のシリーズが含まれている場合、各シリーズは個別のツリーで表されます。 たとえば、[Quantity] と [Sales Amount] の両方に対して期間の予測を作成した場合、予測可能な属性ごとにシリーズが作成されます。  
  
 リストで強調表示される色の長さは、ツリーのレベル数を示します。 つまり、単一のノードで表すことができるタイム シリーズ モデルには傾向を記述する式が 1 つだけ存在し、色分けされたバーの長さは非常に短くなります (言うまでもなく、モデルが MIXED モデルの場合、ノードには ARIMA 式と ARTXP 式の両方が含まれます)。  
  
 ドロップダウン リストに表示されるツリーの色分けされたバーが長い場合は、モデルのツリーに多数の分岐が存在します。 分岐は、回帰がより複雑であり、各ノードで異なる式 (または式のペア) を使用してモデルを複数のセグメントに分割する必要があることを意味します。  
  
 **背景情報**  
 このコントロールを使用して、各ノードの背景色によって表される状態を選択します。  
  
 **既定の展開**  
 モデル内のすべてのツリーに対して表示される、レベルの既定の数を調整します。  
  
 **レベルを表示します。**  
 ツリーに表示されるレベルの数を変更します。  
  
## <a name="see-also"></a>参照  
 [データ マイニング アルゴリズム &#40;Analysis Services - データ マイニング&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [マイニング モデル ビューアー (データ マイニング モデル デザイナー)](mining-model-viewers-data-mining-model-designer.md)   
 [データ マイニング モデル ビューアー](data-mining/data-mining-model-viewers.md)  
  
  
