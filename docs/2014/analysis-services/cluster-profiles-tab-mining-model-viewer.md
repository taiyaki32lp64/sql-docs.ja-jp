---
title: クラスター プロファイル タブ (マイニング モデル ビューアー) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.clustering.profiles.f1
ms.assetid: 1ebafa1f-74e9-4c05-b278-a690fa8543bd
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 663b12f2e83de016d3f1799536b8a3ed674ef544
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/02/2018
ms.locfileid: "48196082"
---
# <a name="cluster-profiles-tab-mining-model-viewer"></a>[クラスターのプロファイル] タブ (マイニング モデル ビューアー)
  **[クラスターのプロファイル]** タブを使用すると、アルゴリズムによってクラスター モデル内で検出されたクラスターの概要を表示できます。 タブには、各クラスターの属性と、その属性の分布が表示されます。  
  
 **詳細:** [Microsoft クラスター アルゴリズム](data-mining/microsoft-clustering-algorithm.md)、 [Microsoft クラスター ビューアーを使用したモデルの参照](data-mining/browse-a-model-using-the-microsoft-cluster-viewer.md)  
  
## <a name="options"></a>および  
 **ビューアーのコンテンツを更新します。**  
 ビューアーにマイニング モデルを再読み込みします。  
  
 **[マイニング モデル]**  
 現在のマイニング構造に含まれているマイニング モデルから選択します。 関連付けられているビューアーが開き、マイニング モデルが表示されます。  
  
 **ビューアー**  
 選択したマイニング モデルを表示するために使用するビューアーを選択します。 マイニング モデル用のカスタム ビューアー、または [!INCLUDE[msCoName](../includes/msconame-md.md)] マイニング コンテンツ ビューアーを使用できます。 利用可能な場合プラグイン ビューアーを使用することもできます。  
  
 **凡例を表示します。**  
 ビューアーの色と **[状態]** 列の値との対応を示すキーを表示するには、このオプションを選択します。  
  
 **[ヒストグラム バー]**  
 各ヒストグラムに含まれる状態の数を制御するには、この値を変更します。 選択した状態の数よりも多くの状態が存在する場合、確率が最も高い状態が保持され、それ以外の状態は **[その他]** にまとめられます。  
  
 **Attributes**  
 クラスター モデルに含まれる列を一覧表示します。 各属性のヒストグラムは、アルゴリズムによって識別されるクラスター間での属性の分布を示します。  
  
 **状態**  
 対応するクラスター行での各状態の色、または連続する数値の分布を示すひし形付きのスライダーのいずれかを示すキーを表示します。 この列は、 **[凡例]** チェック ボックスを使用して、表示/非表示を切り替えることができます。  
  
 **クラスターのプロファイル**  
 このセクションには、モデル内の各クラスターに対応する列が含まれます。 各属性に対して、各クラスターにおける属性の値の分布を示すヒストグラムが表示されます。 グラフには **[母集団]** 列も含まれます。ここでも、ヒストグラムを使用して各属性の値の分布が表示されますが、モデルのすべてが対象になります。  
  
## <a name="see-also"></a>参照  
 [データ マイニング アルゴリズム&#40;Analysis Services - データ マイニング&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [マイニング モデル ビューアー&#40;データ マイニング モデル デザイナー&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [データ マイニング モデル ビューアー](data-mining/data-mining-model-viewers.md)  
  
  
