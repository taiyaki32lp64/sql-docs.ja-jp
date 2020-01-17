---
title: Microsoft Naive Bayes ビューアーを使用してモデルの参照 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- discrimination [Analysis Services]
- naive bayes model [Analysis Services]
- Bayesian classifiers
- mining model content, viewing
- predictive modeling [Analysis Services]
- Naive Bayes Viewer [Analysis Services]
- data mining [Analysis Services], predictive modeling
- Microsoft Naive Bayes Viewer
- histograms [Analysis Services]
- mining models [Analysis Services], predictive modeling
- dependencies [Analysis Services]
ms.assetid: 19743095-63c1-4486-8c1d-2efc143243be
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 668ca4cfae7b660ff9e44de06c8523d8f9324cc9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66086030"
---
# <a name="browse-a-model-using-the-microsoft-naive-bayes-viewer"></a>Microsoft Naive Bayes ビューアーを使用したモデルの参照
  [!INCLUDE[msCoName](../../includes/msconame-md.md)]  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Naive Bayes ビューアーには、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Naive Bayes アルゴリズムを使用して作成されたマイニング モデルが表示されます。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Naive Bayes アルゴリズムは、予測モデリング タスクに非常に適した分類アルゴリズムです。 このアルゴリズムの詳細については、「 [Microsoft Naive Bayes アルゴリズム](microsoft-naive-bayes-algorithm.md)」を参照してください。  
  
 Naive Bayes モデルの主な目的の 1 つはデータセット内のデータを短時間で調査できるようにすることなので、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Naive Bayes ビューアーには、予測可能属性および入力属性の相互関係を表示するための手段がいくつか用意されています。  
  
> [!NOTE]  
>  モデルで使用された式と、検出されたパターンの詳細情報を表示するには、[!INCLUDE[msCoName](../../includes/msconame-md.md)] 汎用コンテンツ ツリー ビューアーに切り替えます。 詳細については、「[Microsoft 汎用コンテンツ ツリー ビューアーを使用したモデルの参照](browse-a-model-using-the-microsoft-generic-content-tree-viewer.md)」または「[Microsoft 汎用コンテンツ ツリー ビューアー (データ マイニング)](../microsoft-generic-content-tree-viewer-data-mining.md)」を参照してください。  
  
##  <a name="BKMK_ViewerTabs"></a> ビューアーのタブ  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]でマイニング モデルを参照すると、そのモデルに適したビューアーを使用してデータ マイニング デザイナーの **[マイニング モデル ビューアー]** タブにモデルが表示されます。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Naive Bayes ビューアーには、データを調査するための次のタブがあります。  
  
-   [依存関係ネットワーク](#BKMK_Dependency)  
  
-   [属性のプロファイル](#BKMK_Profiles)  
  
-   [属性の特性](#BKMK_Characteristics)  
  
-   [属性の識別](#BKMK_Discrimination)  
  
##  <a name="BKMK_Dependency"></a> 依存関係ネットワーク  
 **[依存関係ネットワーク]** タブには、モデル内にある入力属性と予測可能属性の間の依存関係が表示されます。 ビューアーの左側にあるスライダーは、依存関係の強さに関連付けられたフィルターとして機能します。 スライダーを小さく設定すると、緊密なリンクのみが表示されます。  
  
 ノードを選択すると、そのノードに固有の依存関係が強調表示されます。 たとえば、予測可能なノードを選択した場合は、その予測可能なノードの予測に役立つ各ノードも強調表示されます。  
  
 ビューアーの下部にある凡例は、グラフ内の依存関係の種類に色を関連付けています。 たとえば、予測可能なノードを選択すると、予測可能なノードが水色で網掛けされ、選択したノードを予測するノードがオレンジ色で網掛けされます。  
  
 [トップに戻る](#BKMK_ViewerTabs)  
  
##  <a name="BKMK_Profiles"></a> 属性のプロファイル  
 **[属性のプロファイル]** タブでは、グリッドにヒストグラムが表示されます。 このグリッドを使用すると、 **[予測可能]** ボックスで選択した予測可能属性を、モデル内の他のすべての属性と比較できます。 タブ内の各列は、予測可能属性の状態を表します。 予測可能属性に多くの状態がある場合は、 **[ヒストグラム バー]** を調整して、ヒストグラムに表示される状態の数を変更できます。 選択した数が属性内の状態の総数よりも少ない場合、状態はサポートされている順に一覧表示され、残りの状態は 1 つの灰色のバケットにまとめられます。  
  
 ヒストグラムの色を属性の状態に関連付けるマイニング凡例を表示するには、 **[凡例の表示]** チェック ボックスをオンにします。 マイニング凡例には、選択した属性と値の各ペアに関するケースの分布も表示されます。  
  
 グリッドの内容を HTML テーブルとしてクリップボードにコピーするには、 **[属性のプロファイル]** タブを右クリックして **[コピー]** を選択します。  
  
 [トップに戻る](#BKMK_ViewerTabs)  
  
##  <a name="BKMK_Characteristics"></a> 属性の特性  
 **[属性の特性]** タブを使用するには、 **[属性]** 一覧から予測可能属性を選択し、選択した属性の状態を **[値]** 一覧から選択します。 これらの変数を設定すると、選択した属性の選択したケースに関連付けられている属性の状態が **[属性の特性]** タブに表示されます。 属性は、重要なものから順番に並べ替えられます。  
  
 [トップに戻る](#BKMK_ViewerTabs)  
  
##  <a name="BKMK_Discrimination"></a> 属性の識別  
 **[属性の識別]** タブを使用するには、予測可能属性を選択し、 **[属性]** 、 **[値 1]** 、および **[値 2]** の一覧から属性の状態を 2 つ選択します。 **[属性の識別]** タブのグリッドの列に、次の情報が表示されます。  
  
 **[属性]**  
 予測可能属性の 1 つの状態を優先する状態が含まれているデータセット内の別の属性が一覧表示されます。  
  
 **値**  
 **[属性]** 列の属性の値が表示されます。  
  
 **優先\<値 1 >**  
 **[値 1]** の予測可能な属性値が優先される度合いを示す、色分けされたバーが表示されます。  
  
 **優先\<値 2 >**  
 **[値 2]** の予測可能な属性値が優先される度合いを示す、色分けされたバーが表示されます。  
  
 [トップに戻る](#BKMK_ViewerTabs)  
  
## <a name="see-also"></a>参照  
 [Microsoft Naive Bayes アルゴリズム](microsoft-naive-bayes-algorithm.md)   
 [マイニング モデル ビューアーのタスクと操作方法](mining-model-viewer-tasks-and-how-tos.md)   
 [データ マイニング ツール](data-mining-tools.md)   
 [データ マイニング モデル ビューアー](data-mining-model-viewers.md)  
  
  
