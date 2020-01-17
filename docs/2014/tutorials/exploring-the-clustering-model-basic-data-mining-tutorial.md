---
title: クラスタ リング モデル (基本的なデータ マイニング チュートリアル) の検証 |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: ce8aa034-161b-473f-baec-9c29e0a8e5f5
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 9bb2c6457122a5ea49824ca178b6950d88f75563
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63280432"
---
# <a name="exploring-the-clustering-model-basic-data-mining-tutorial"></a>クラスター モデルの検証 (基本的なデータ マイニング チュートリアル)
  [!INCLUDE[msCoName](../includes/msconame-md.md)]クラスタ リング アルゴリズムは、類似した特性を持つクラスターにケースをグループ化します。 このグループ化は、データの探索、データの異常の特定、および予測の作成に役立ちます。  
  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] クラスター ビューアーには、クラスタリング マイニング モデルを調べるための次のタブがあります。  
  

  
##  <a name="ClusterDiagramTab"></a> クラスター ダイアグラム タブ  
 [クラスター ダイアグラム] タブには、マイニング モデル内のすべてのクラスターが表示されます。 クラスター間を結ぶ線は "緊密度" を表しており、緊密度が高いほど濃い線で表示されます。 各クラスター本体の色は、クラスター内の変数の頻度と状態を表します。  
  
#### <a name="to-explore-the-model-in-the-cluster-diagram-tab"></a>[クラスター ダイアグラム] タブでモデルを調査するには  
  
1.  使用して、**マイニング モデルの**一覧の上部にある、**マイニング モデル ビューアー**  タブに切り替える、`TM_Clustering`モデル。  
  
2.  **ビューアー**一覧で、 **Microsoft クラスター ビューアー**します。  
  
3.  **網掛け変数**ボックスで、 **Bike Buyer**します。  
  
     既定変数は**母集団**、どのクラスターが必要な属性を持つメンバーを含めることが検出するために、モデル内のすべての属性に変更することができますが、します。  
  
4.  選択**1**で、**状態**自転車を購入したこれらのケースを調べたりボックス。  
  
     **密度**凡例には、シェーディング変数と状態で選択した属性状態のペアの密度がについて説明します。 この例では、わかります clusterwith 最も暗い網掛けが自転車購入者の最高の割合。  
  
5.  最も色の濃いクラスター上にマウス ポインターを置きます。  
  
     ツールヒントに、属性が `Bike Buyer = 1` であるケースの割合が表示されます。  
  
6.  クラスターが、クラスターを右クリックして、最高の密度を選択します**クラスター名の変更**と種類**自転車購入者率高**の後で識別します。 [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  最も色の薄い (最も密度の低い) クラスターを見つけます。 クラスターを右クリックして**クラスター名の変更**と種類**自転車購入者率低**します。 [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
8.  をクリックして、**自転車購入者率高**クラスターし、その他のクラスターとの接続を明確に表示するためのウィンドウの領域にドラッグします。  
  
     クラスターを選択すると、そのクラスターと別のクラスターをつなぐ線が強調表示され、このクラスターに対するすべての関係を簡単に確認できます。 クラスターが選択されていないときは、ダイアグラム内にあるすべてのクラスター間の相互関係の度合いを、線の濃さによって確認できます。 網掛けが薄いか存在しない場合は、クラスターがあまり似ていません。  
  
9. ネットワークの左側にあるスライダーを使用して、緊密度の低いリンクを非表示にし、緊密な関係にあるクラスターだけを表示します。 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] のマーケティング部門は、絞り込みメール配信に最適な方法を決定する際に、類似するクラスターをまとめることができます。  
  

  
##  <a name="ClusterProfilesTab"></a> クラスターのプロファイル タブ  
 **クラスターのプロファイル** タブの全体像を提供する、`TM_Clustering`モデル。 **クラスターのプロファイル** タブには、モデル内の各クラスターの列が含まれています。 一番左側の列には、少なくとも 1 つのクラスターに関連付けられているすべての属性が表示されます。 その他の部分には、それぞれのクラスターについて、各属性の状態の分布状況が表示されます。 離散変数の分布は、色分けされたバーに表示されるバーの最大数として表示されます、**ヒストグラム バー**一覧。 連続属性はダイヤモンド グラフで示されます。このグラフでは、各クラスターの平均と標準偏差を確認できます。  
  
#### <a name="to-explore-the-model-in-the-cluster-profiles-tab"></a>[クラスターのプロファイル] タブでモデルを調査するには  
  
1.  設定**ヒストグラム**バーに**5**します。  
  
     このモデルでは、1 つの変数に対する状態の最大数が 5 になります。  
  
2.  場合、**マイニング凡例**の表示をブロック、**属性のプロファイル**、邪魔に移動します。  
  
3.  選択、**自転車購入者率高**列の右にドラッグし、**母集団**列。  
  
4.  選択、**自転車購入者率低**列の右にドラッグし、**自転車購入者率高**列。  
  
5.  をクリックして、**自転車購入者率高**列。  
  
     **変数**列がそのクラスターの重要度順に並べ替えられます。 列をスクロールし、[自転車購入者率高] クラスターの特性を確認します。 たとえば、多くの場合、このクラスターに属する人は通勤距離が短い傾向にあります。  
  
6.  ダブルクリックして、**年齢**セル、**自転車購入者率高**列。  
  
     **マイニング凡例**詳細ビューとは、平均年齢と同様にこれらの顧客の年齢の範囲を表示できます。  
  
7.  右クリックし、**自転車購入者率低**列と select**列の非表示**します。  
  

  
##  <a name="ClusterCharacteristicsTab"></a> クラスターの特性 タブ  
 **クラスターの特性** タブで、する特徴を調べ、さらに詳しく、クラスターを構成します。 ([クラスターのプロファイル] タブのように) すべてのクラスターの特性を比較するのではなく、一度に 1 つのクラスターを検証することができます。 たとえば、選択した**自転車購入者率高**から、**クラスター**一覧で、このクラスター内の顧客の特性を確認できます。 [クラスターのプロファイル] ビューアーとは表示が異なりますが、結果は同じです。  
  
> [!NOTE]  
>  初期値を設定しない限り**holdoutseed**結果は、モデルを処理するたびに異なります。 詳細については、次を参照してください[HoldoutSeed 要素。](https://docs.microsoft.com/bi-reference/assl/properties/holdoutseed-element)  
  

  
##  <a name="ClusterDiscriminationTab"></a> クラスターの識別 タブ  
 **クラスターの識別** タブで、別の 1 つのクラスターを識別する特性を調べることができます。 1 つ、2 つのクラスターを選択した後、**クラスター 1**リスト、および 1 つから、**クラスター 2**ビューアー ボックスの一覧は、クラスター間の相違点を計算し、属性の一覧を表示します。ほとんどのクラスターを区別します。  
  
#### <a name="to-explore-the-model-in-the-cluster-discrimination-tab"></a>[クラスターの識別] タブでモデルを調査するには  
  
1.  **クラスター 1**ボックスで、**自転車購入者率高**します。  
  
2.  **クラスター 2**ボックスで、**自転車購入者率低**します。  
  
3.  クリックして**変数**アルファベット順に並べ替えます。  
  
     お客様の間でより大きな違いの一部、**自転車購入者率低**と**自転車購入者率高**クラスターには、年齢、車の所有、子供、リージョンの数が含まれます。  
  
## <a name="related-tasks"></a>Related Tasks  
 他のマイニング モデルを探索するには、次のトピックを参照してください。  
  
-   [デシジョン ツリー モデルの検証&#40;基本的なデータ マイニング チュートリアル&#41;](../../2014/tutorials/exploring-the-decision-tree-model-basic-data-mining-tutorial.md)  
  
-   [Naive Bayes モデルの検証&#40;基本的なデータ マイニング チュートリアル&#41;](../../2014/tutorials/exploring-the-naive-bayes-model-basic-data-mining-tutorial.md)  
  
## <a name="next-task-in-lesson"></a>このレッスンの次の作業  
 [Naive Bayes モデルの検証&#40;基本的なデータ マイニング チュートリアル&#41;](../../2014/tutorials/exploring-the-naive-bayes-model-basic-data-mining-tutorial.md)  
  
## <a name="previous-task-in-lesson"></a>このレッスンの前の作業  
 [デシジョン ツリー モデルの検証&#40;基本的なデータ マイニング チュートリアル&#41;](../../2014/tutorials/exploring-the-decision-tree-model-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>関連項目  
 [Microsoft クラスター ビューアーを使用してモデルを参照します。](../../2014/analysis-services/data-mining/browse-a-model-using-the-microsoft-cluster-viewer.md)   
 [クラスターの識別 タブ&#40;マイニング モデル ビューアー&#41;](../../2014/analysis-services/cluster-discrimination-tab-mining-model-viewer.md)   
 [クラスター プロファイル タブ&#40;マイニング モデル ビューアー&#41;](../../2014/analysis-services/cluster-profiles-tab-mining-model-viewer.md)   
 [クラスターの特性 タブ&#40;マイニング モデル ビューアー&#41;](../../2014/analysis-services/cluster-characteristics-tab-mining-model-viewer.md)   
 [クラスター ダイアグラム タブ&#40;マイニング モデル ビューアー&#41;](../../2014/analysis-services/cluster-diagram-tab-mining-model-viewer.md)  
  
  
