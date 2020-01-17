---
title: Microsoft ツリー ビューアーを使用してモデルの参照 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Tree Viewer [Analysis Services]
- predictions [Analysis Services], discrete attributes
- mining model content, viewing
- predictions [Analysis Services], continuous attributes
- mining legend [Analysis Services]
- discrete attributes [Analysis Services]
- Microsoft Decision Trees algorithm [Analysis Services]
- decision tree algorithms [Analysis Services]
- Microsoft Tree Viewer
- decision trees [Analysis Services]
- dependencies [Analysis Services]
- continuous attributes
ms.assetid: 0c96d518-ed20-40b7-8d62-b26ad6244287
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5f7ac483e0883386f620a654d6257a49fa8baf52
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66085938"
---
# <a name="browse-a-model-using-the-microsoft-tree-viewer"></a>Microsoft ツリー ビューアーを使用したモデルの参照
   [!INCLUDE[msCoName](../../includes/msconame-md.md)]  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ツリー ビューアーには、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] デシジョン ツリー アルゴリズムを使用して作成されたデシジョン ツリーが表示されます。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] デシジョン ツリー アルゴリズムは、分類と回帰の両方をサポートする複合的なデシジョン ツリー アルゴリズムです。 したがって、このビューアーには [!INCLUDE[msCoName](../../includes/msconame-md.md)] 線形回帰アルゴリズムに基づくモデルを表示できます。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] デシジョン ツリー アルゴリズムは、不連続属性と連続属性の両方の予測モデリングに使用します。 このアルゴリズムの詳細については、「 [Microsoft デシジョン ツリー アルゴリズム](microsoft-decision-trees-algorithm.md)」を参照してください。  
  
> [!NOTE]  
>  モデルで使用された式と、検出されたパターンの詳細情報を表示するには、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 汎用コンテンツ ツリー ビューアーを使用します。 詳細については、「[Microsoft 汎用コンテンツ ツリー ビューアーを使用したモデルの参照](browse-a-model-using-the-microsoft-generic-content-tree-viewer.md)」または「[Microsoft 汎用コンテンツ ツリー ビューアー (データ マイニング)](../microsoft-generic-content-tree-viewer-data-mining.md)」を参照してください。  
  
##  <a name="BKMK_TabsPanes"></a> ビューアーのタブ  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]でマイニング モデルを参照すると、そのモデルに適したビューアーを使用してデータ マイニング デザイナーの **[マイニング モデル ビューアー]** タブにモデルが表示されます。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] ツリー ビューアーには、次のタブとペインがあります。  
  
-   [[デシジョン ツリー]](#BKMK_DecisionTree)  
  
-   [依存関係ネットワーク](#BKMK_DependencyNetwork)  
  
-   [マイニング凡例](#BKMK_MiningLegend)  
  
###  <a name="BKMK_DecisionTree"></a> [デシジョン ツリー]  
 デシジョン ツリー モデルを作成すると、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] によって、予測可能な属性ごとにツリーが個別に作成されます。 個別のツリーを表示するには、ビューアーの **[デシジョン ツリー]** タブにある **[ツリー]** 一覧から表示するツリーを選択します。  
  
 デシジョン ツリーは一連の分割で構成されており、アルゴリズムによって最も重要と判別された分割は、ビューアーの左側にある **[すべて]** ノードに表示されます。 その他の分割は右側に表示されます。 **[すべて]** ノード内の分割は最も重要です。なぜなら、データセット内で最も強い分割発生条件が含まれており、その結果として最初の分割が発生したからです。  
  
 ツリー内の個々のノードを展開したり折りたたんだりすると、各ノードの後にある分割を表示または非表示にすることができます。 また、 **[デシジョン ツリー]** タブのオプションを使用して、ツリーの表示方法を変更することもできます。 ツリーに表示されるレベルの数を調整するには、 **[表示レベル]** スライダーを使用します。 モデル内のすべてのツリーに表示される既定のレベル数を設定するには、 **[既定の展開]** を使用します。  
  
#### <a name="predicting-discrete-attributes"></a>不連続属性の予測  
 予測可能な不連続属性を使用してツリーを作成した場合、ビューアーにはツリーの各ノードに関する次の情報が表示されます。  
  
-   分割が発生した条件  
  
-   ポピュラリティ順に並べられた、予測可能な属性の状態の分布を表すヒストグラム  
  
 **[ヒストグラム]** オプションを使用すると、ツリーのヒストグラムに表示される状態の数を変更できます。 これは、予測可能な属性に多数の状態が含まれている場合に便利です。 ヒストグラムには、状態がポピュラリティ順に左から右に表示されます。表示するように選択した状態の数が属性内の状態の総数よりも少ない場合は、最も一般的でない状態がまとめて灰色で表示されます。 ノードの各状態の正確な数を表示するには、ノードにポインターを合わせてヒントを表示するか、またはノードを選択して **[マイニング凡例]** に詳細を表示します。  
  
 各ノードの背景色は、 **[背景]** オプションを使用して選択した特定の属性状態のケースの集中度を表しています。 このオプションを使用して、関心のある特定の対象が含まれたノードを強調表示できます。  
  
#### <a name="predicting-continuous-attributes"></a>連続属性の予測  
 予測可能な連続属性を使用してツリーを作成した場合、ビューアーにはヒストグラムの代わりにツリーの各ノードのダイヤモンド チャートが表示されます。 ダイヤモンド チャートには、属性の範囲を表す線があります。 ダイヤモンドはノードの中間にあり、ダイヤモンドの幅がそのノードの属性の分散を表します。 ダイヤモンドの幅が狭いほど、そのノードでより正確な予測を作成できることを示します。 また、ビューアーには、ノード内の分割を決定するために使用される回帰式も表示されます。  
  
#### <a name="additional-decision-tree-display-options"></a>その他のデシジョン ツリー表示オプション  
 デシジョン ツリー モデルのドリルスルーが有効な場合は、ツリーでノードを右クリックして **[ドリルスルー]** を選択すると、ノードをサポートするトレーニング ケースにアクセスできます。 ドリルスルーを有効にするには、データ マイニング ウィザード内で設定するか、または **[マイニング モデル]** タブでマイニング モデルのドリルスルー プロパティを調整します。  
  
 **[デシジョン ツリー]** タブのズーム オプションを使用すると、ツリーを拡大または縮小できます。 **[サイズの自動調整]** を使用すると、モデル全体をビューアー画面に合わせることができます。 ツリーが大きすぎて画面に合うようにサイズを調整できない場合は、 **[ナビゲーション]** オプションを使用してツリー内を移動できます。 **[ナビゲーション]** をクリックすると、表示するモデルのセクションを選択できる別のナビゲーション ウィンドウが開きます。  
  
 ツリー ビューの画像をクリップボードにコピーして、ドキュメントや画像操作ソフトウェアに貼り付けることができます。 ビューアーに表示されているツリーのセクションだけをコピーするには、 **[グラフ ビューのコピー]** を使用します。ツリーで展開されているすべてのノードをコピーするには、 **[グラフ全体のコピー]** を使用します。  
  
 [トップに戻る](#BKMK_TabsPanes)  
  
###  <a name="BKMK_DependencyNetwork"></a> 依存関係ネットワーク  
 **[依存関係ネットワーク]** には、モデル内にある入力属性と予測可能属性の間の依存関係が表示されます。 ビューアーの左側にあるスライダーは、依存関係の強さに関連付けられたフィルターとして機能します。 スライダーを下げると、最も強いリンクだけが表示されます。  
  
 ノードを選択すると、そのノードに固有の依存関係が強調表示されます。 たとえば、予測可能なノードを選択した場合は、その予測可能なノードの予測に役立つ各ノードも強調表示されます。  
  
 ビューアーに多数のノードがある場合は、 **[ノードの検索]** ボタンを使用して特定のノードを検索できます。 **[ノードの検索]** をクリックすると、 **[ノードの検索]** ダイアログ ボックスが開き、フィルターを使用して特定のノードを検索して選択できます。  
  
 ビューアーの下部にある凡例は、グラフ内の依存関係の種類に色を関連付けています。 たとえば、予測可能なノードを選択すると、予測可能なノードが水色で網掛けされ、選択したノードを予測するノードがオレンジ色で網掛けされます。  
  
 [トップに戻る](#BKMK_TabsPanes)  
  
###  <a name="BKMK_MiningLegend"></a> マイニング凡例  
 デシジョン ツリー モデルでノードを選択すると、 **[マイニング凡例]** に次の情報が表示されます。  
  
-   予測可能な属性の状態によって分類された、ノード内のケースの数。  
  
-   ノードの予測可能な属性の各ケースの確率。  
  
-   予測可能な属性の各状態の数が含まれたヒストグラム。  
  
-   特定のノードに到達するために必要な条件。" *ノード パス*" としても知られています。  
  
-   線形回帰モデルの回帰式。  
  
 ソリューション エクスプローラーと同様の方法で **[マイニング凡例]** をドッキングして操作できます。  
  
 [トップに戻る](#BKMK_TabsPanes)  
  
## <a name="see-also"></a>関連項目  
 [Microsoft デシジョン ツリー アルゴリズム](microsoft-decision-trees-algorithm.md)   
 [マイニング モデル ビューアー (データ マイニング モデル デザイナー)](../mining-model-viewers-data-mining-model-designer.md)   
 [マイニング モデル ビューアーのタスクと操作方法](mining-model-viewer-tasks-and-how-tos.md)   
 [データ マイニング ツール](data-mining-tools.md)   
 [データ マイニング モデル ビューアー](data-mining-model-viewers.md)  
  
  
