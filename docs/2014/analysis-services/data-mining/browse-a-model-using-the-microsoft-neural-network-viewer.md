---
title: Microsoft ニューラル ネットワーク ビューアーを使用してモデルの参照 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining model content, viewing
- classification mining model [Analysis Services]
- Microsoft Neural Network Viewer
- regression algorithms [Analysis Services]
- Neural Network Viewer [Analysis Services]
- neural network model [Analysis Services]
ms.assetid: 2343d746-c4f4-499b-9d3c-17d63310a9a3
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1628eff6e5c440071126ce3508b977f9f7508ba5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66086055"
---
# <a name="browse-a-model-using-the-microsoft-neural-network-viewer"></a>Microsoft ニューラル ネットワーク ビューアーを使用したモデルの参照
  [!INCLUDE[msCoName](../../includes/msconame-md.md)]  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ニューラル ネットワーク ビューアーには、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] ニューラル ネットワーク アルゴリズムを使用して作成されたマイニング モデルが表示されます。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] ニューラル ネットワーク アルゴリズムでは、複数の入力と出力を分析できる分類および回帰マイニング モデルを作成します。このアルゴリズムは、制限のない分析と探索に非常に役立ちます。 このアルゴリズムの詳細については、「 [Microsoft Neural Network Algorithm](microsoft-neural-network-algorithm.md)」を参照してください。  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] ニューラル ネットワーク ビューアーを使用してモデルを調べる場合、通常は対象の属性と状態を選択してから、ビューアーを使用して入力属性が結果に与える影響を確認します。  
  
 たとえば、潜在的な顧客のクラスについて次の事実がわかっているとします。  
  
-   中高年 (40 ～ 50 歳)。  
  
-   持ち家所有。  
  
-   2 人の子供と同居。  
  
 これらの属性を顧客が購入する可能性とどのように関連付けることができるでしょうか。  
  
 購入行動を対象となる結果として使用してニューラル ネットワーク モデルを作成することにより、高所得などの顧客属性の複数の組み合わせを調べ、購入行動に影響する可能性が最も高い属性の組み合わせを検出できます。 たとえば、決定要因が通勤距離であることを検出できます。  
  
 検出された各パターンを表す式などの詳細情報をさらに表示する必要がある場合は、ビューを切り替えて [!INCLUDE[msCoName](../../includes/msconame-md.md)] 汎用コンテンツ ツリー ビューアーを使用できます。 詳細については、「[Microsoft 汎用コンテンツ ツリー ビューアーを使用したモデルの参照](browse-a-model-using-the-microsoft-generic-content-tree-viewer.md)」または「[Microsoft 汎用コンテンツ ツリー ビューアー (データ マイニング)](../microsoft-generic-content-tree-viewer-data-mining.md)」を参照してください。  
  
##  <a name="BKMK_ViewerTabs"></a> ビューアーのタブ  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]でマイニング モデルを参照すると、そのモデルに適したビューアーを使用してデータ マイニング デザイナーの **[マイニング モデル ビューアー]** タブにモデルが表示されます。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] ニューラル ネットワーク ビューアーには、ニューラル ネットワーク マイニング モデルを調べるための次のタブがあります。  
  
-   [入力](#BKMK_Inputs)  
  
-   [出力](#BKMK_Outputs)  
  
-   [変数](#BKMK_Characteristics)  
  
###  <a name="BKMK_Inputs"></a> 入力  
 **[入力]** タブを使用して、モデルの入力として使用される属性と属性値を選択します。 既定では、ビューアーはすべての属性が含まれた状態で開きます。 この既定のビューでは、表示する最も重要な属性値がモデルによって選択されます。  
  
 入力属性を選択するには、 **[入力]** グリッドの **[属性]** 列内をクリックし、一覧から属性を選択します。 (モデルに含まれている属性のみが一覧に表示されます)。  
  
 **[値]** 列の下に、最初の個別の値が表示されます。 既定値をクリックすると、関連する属性で考えられるすべての状態が含まれた一覧が表示されます。 調査する状態を選択できます。 属性はいくつでも選択できます。  
  
 [トップに戻る](#BKMK_ViewerTabs)  
  
###  <a name="BKMK_Outputs"></a> 出力  
 **[出力]** タブを使用して、調査対象の結果属性を選択します。 モデルの作成時に列が予測可能な属性として定義されたことを前提として、比較する 2 つの結果状態を選択できます。  
  
 **[出力属性]** 一覧を使用して、属性を選びます。 **[値 1]** 一覧と **[値 2]** 一覧から、属性に関連付けられている 2 つの状態を選択できます。 出力属性のこれらの 2 つの状態は、 **[変数]** ペインで比較されます。  
  
 [トップに戻る](#BKMK_ViewerTabs)  
  
###  <a name="BKMK_Characteristics"></a> 変数  
 グリッドに、**変数** タブには、次の列が含まれています。**属性**、**値**、 **[値 1] 優先**、および **[値 2] 優先**します。 既定では、列は **[[値 1] を優先]** の強度によって並べ替えられます。 列見出しをクリックすると、並べ替え順が選択した列に変わります。  
  
 属性の右側のバーには、指定した入力属性の状態によって優先される出力属性の状態が示されます。 バーのサイズで、出力の状態によって入力の状態が優先される強度が示されます。  
  
 [トップに戻る](#BKMK_ViewerTabs)  
  
## <a name="see-also"></a>参照  
 [Microsoft Neural Network Algorithm](microsoft-neural-network-algorithm.md)   
 [マイニング モデル ビューアーのタスクと操作方法](mining-model-viewer-tasks-and-how-tos.md)   
 [マイニング モデル ビューアーのタスクと操作方法](mining-model-viewer-tasks-and-how-tos.md)   
 [データ マイニング ツール](data-mining-tools.md)   
 [データ マイニング モデル ビューアー](data-mining-model-viewers.md)  
  
  
