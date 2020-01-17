---
title: デシジョン ツリー タブ (マイニング モデル ビューアー) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.decisiontree.f1
ms.assetid: dc88606f-ba7c-4f8d-af65-bfa17ec16e2b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: cee721aca66f5266a29d3bf61babf9060e9aef32
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66082300"
---
# <a name="decision-tree-tab-mining-model-viewer"></a>[デシジョン ツリー] タブ (マイニング モデル ビューアー)
  **[デシジョン ツリー]** ペインは、デシジョン ツリー モデルで作成されたデシジョン ルールをビジュアルに表示します。 デシジョン ルールは、特定の結果に至るパスを記述します。  
  
 **詳細情報。** [Microsoft デシジョン ツリー アルゴリズム](data-mining/microsoft-decision-trees-algorithm.md)、 [Microsoft ツリー ビューアーを使用してモデルの参照](data-mining/browse-a-model-using-the-microsoft-tree-viewer.md)  
  
## <a name="options"></a>および  
 **ビューアーのコンテンツを更新します。**  
 ビューアーにマイニング モデルを再読み込みします。  
  
 **[マイニング モデル]**  
 現在のマイニング構造に含まれているマイニング モデルから選択します。 関連付けられているビューアーが開き、マイニング モデルが表示されます。  
  
 **ビューアー**  
 選択したマイニング モデルを調べるために使用するビューアーを選択します。 カスタム ビューアーまたは [!INCLUDE[msCoName](../includes/msconame-md.md)] マイニング コンテンツ ビューアーを使用できます。 利用可能な場合プラグイン ビューアーを使用することもできます。  
  
 **ズーム イン**  
 デシジョン ツリーのノードと分岐の詳細が表示されるように拡大します。 複雑なモデルでは、デシジョン ツリーに多数の分岐レベルが含まれる可能性があります。  
  
 **ズーム アウト**  
 ツリー構造の全体ビューが表示されるように縮小します。  
  
 **グラフ ビューのコピー**  
 ダイアグラムで表示されている部分をクリップボードにコピーします。  
  
 **グラフ全体のコピー**  
 ダイアグラム全体をクリップボードにコピーします。  
  
 **ウィンドウに合わせてダイアグラムの倍率**  
 画面の大きさに合うようにツリー構造全体を縮小します。  
  
 **ヒストグラム**  
 各ノードのヒストグラムに表示できる状態の数を選択します。 モデルの状態数が選択した値よりも少ない場合でも、追加のバーは表示されません。  
  
 **ツリー**  
 ビューアーに表示するツリーを選択します。 複数の予測可能な属性を含むモデルを作成した場合は、アルゴリズムによって予測可能な属性ごとに別個のツリーが作成されます。  
  
 **背景情報**  
 各ノードの背景色の表現で使用する予測可能な属性の値を設定します。 たとえば、サンプルの AdventureWorks モデルで **[背景情報]** を 1 ([Bike Buyer] = Yes) に設定した場合、Bike Buyer (バイク購入者) の比率が大きければ大きいほど、ノードの影が濃くなります。 このオプションは、ツリーの分岐とノードに対して視覚的な意味を追加します。  
  
 **既定の展開**  
 ツリー グラフに表示するレベル数の既定値を設定するには、リストから値を選択します。  
  
 **レベルを表示します。**  
 ツリー グラフに表示するレベル数を調整するには、スライダー バーを左右に移動します。 モデルのすべてのノードを表示するには、バーを右端までスライドします。  
  
## <a name="see-also"></a>参照  
 [データ マイニング アルゴリズム &#40;Analysis Services - データ マイニング&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [マイニング モデル ビューアー (データ マイニング モデル デザイナー)](mining-model-viewers-data-mining-model-designer.md)   
 [データ マイニング モデル ビューアー](data-mining/data-mining-model-viewers.md)  
  
  
