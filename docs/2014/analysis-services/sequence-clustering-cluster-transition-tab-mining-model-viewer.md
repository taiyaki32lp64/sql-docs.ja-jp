---
title: シーケンス クラスターのクラスターの状態遷移 タブ (マイニング モデル ビューアー) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.sequenceclustering.transition.f1
ms.assetid: 40aef457-d69f-4905-a2d3-924c37bd3d97
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8a236805ac047b351aa49c2486b8acac84818017
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66069078"
---
# <a name="sequence-clustering-cluster-transition-tab-mining-model-viewer"></a>シーケンス クラスターの [状態遷移] タブ (マイニング モデル ビューアー)
  **Microsoft シーケンス クラスター ビューアー**の **[状態遷移]** タブでは、選択したクラスターにおける属性と値のペア間または状態間の遷移を詳細に調べることができます。  
  
 パターンを表示するには、シーケンス クラスタリング モデルのこのビューを使用します。 ダイアグラム内のリンクは遷移の確率を表し、ノードはシーケンスの状態を表します。  
  
 **詳細情報。** [Microsoft シーケンス クラスター アルゴリズム](data-mining/microsoft-sequence-clustering-algorithm.md)、 [Microsoft シーケンス クラスター ビューアーを使用してモデルの参照](data-mining/browse-a-model-using-the-microsoft-sequence-cluster-viewer.md)  
  
## <a name="options"></a>および  
 **ビューアーのコンテンツを更新します。**  
 ビューアーにマイニング モデルを再読み込みします。  
  
 **[マイニング モデル]**  
 現在のマイニング構造に含まれているマイニング モデルから、表示するモデルを選択します。 関連付けられているビューアーが開き、マイニング モデルが表示されます。  
  
 **ビューアー**  
 選択したマイニング モデルを調べるために使用するビューアーを選択します。 カスタム ビューアーまたは **Microsoft 汎用コンテンツ ツリー ビューアー**を使用できます。 利用可能な場合プラグイン ビューアーを使用することもできます。  
  
 **ズーム イン**  
 ダイアグラムをズーム アウトして、状態を詳しく表示します。  
  
 **ズーム アウト**  
 ダイアグラムを縮小して、クラスター内の状態の全体的なビューを取得します。  
  
 **グラフ ビューのコピー**  
 ダイアグラムで表示されている部分をクリップボードにコピーします。  
  
 **グラフ全体のコピー**  
 ダイアグラム全体をクリップボードにコピーします。  
  
 **Cluster**  
 ビューアーに表示するクラスターを選択します。 既定値として **[母集団 (すべて)]** が選択されています。これは、モデル全体の状態と遷移がグラフに含まれることを意味します。 特定のクラスターを選択すると、選択したクラスターに含まれる状態と遷移だけが表示されます。  
  
 **ヒント:** 使用してクラスターの名前を変更することができます、**クラスター ダイアグラム**タブ。操作は、クラスターを選択して右クリックし、 **[名前の変更]** をクリックするだけです。 クラスターをわかりやすい名前に変更すると、 **[状態遷移]** タブでクラスターを簡単に比較できます。  
  
 **Edge ラベルを表示します。**  
 遷移の確率を示すグラフに各エッジの番号を表示するには、このオプションを選択します。  
  
 **リンク**  
 スライダーを使用して、グラフに表示される状態と遷移の数を制御します。 スライダーを下に移動すると、確率が最も高い状態と遷移だけが表示されます。  
  
## <a name="see-also"></a>関連項目  
 [データ マイニング アルゴリズム &#40;Analysis Services - データ マイニング&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [マイニング モデル ビューアー (データ マイニング モデル デザイナー)](mining-model-viewers-data-mining-model-designer.md)   
 [データ マイニング モデル ビューアー](data-mining/data-mining-model-viewers.md)  
  
  
