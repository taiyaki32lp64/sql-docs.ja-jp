---
title: テストのフィルター選択されたモデル (基本的なデータ マイニング チュートリアル) |Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: f0d74f8c-600d-4df5-a742-695e6947a071
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: baa4910b2849c4eb2dd04c6d0115c83683ee8bea
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63044097"
---
# <a name="testing-a-filtered-model-basic-data-mining-tutorial"></a>フィルター選択されたモデルのテスト (基本的なデータ マイニング チュートリアル)
  確認しましたところ、`TM_Decision_Tree`最も正確なモデルは、のニーズに合うように、モデルのカスタマイズ、[!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)]絞り込みメール配信キャンペーン。 具体的には、マーケティング部門では男性顧客と女性顧客に違いがあるかどうかを知りたいと考えています。 情報には、広告のために使用する雑誌を決定するためでしたやにダイレクト_メールで特集する製品です。  
  
## <a name="using-filters"></a>フィルターの使用  
 フィルター選択を行うと、データのサブセットに基づくモデルを簡単に作成できます。 フィルターはモデルにのみ適用され、基になるデータ ソースは変更しません。  
  
 このレッスンでは、性別に基づいてフィルター処理を実行するモデルを作成し、男性と女性それぞれの購買行動に最も大きな影響を及ぼす特性を予測します。  
  
 最初のコピーを作成するが、`TM_Decision_Tree`モデル。  
  
#### <a name="to-copy-the-decision-tree-model"></a>デシジョン ツリー モデルをコピーするには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]、ソリューション エクスプ ローラーで選択**BasicDataMining**します。  
  
2.  **[マイニング モデル]** タブをクリックします。  
  
3.  右クリックして、`TM_Decision_Tree`モデル、および選択**新しいマイニング モデルです。**  
  
4.  **モデル名**フィールドに「`TM_Decision_Tree_Male`します。  
  
5.  **[OK]** をクリックします。  
  
 次に、性別に基づいてモデルの顧客を選択するフィルターを作成します。  
  
#### <a name="to-create-a-case-filter-on-a-mining-model"></a>マイニング モデルに対してケース フィルターを作成するには  
  
1.  右クリックし、`TM_Decision_Tree_Male`マイニング モデルのショートカット メニューを開きます。  
  
     または  
  
     モデルを選択します。 **[マイニング モデル]** メニューの **[モデル フィルターの設定]** をクリックします。  
  
2.  **[モデル フィルター]** ダイアログ ボックスで、 **[マイニング構造列]** ボックスのグリッドの先頭行をクリックします。  
  
     ドロップダウン リストに、そのテーブルの列の名前のみが表示されます。  
  
3.  マイニング構造列] ボックスで、[**性別**します。  
  
     テキスト ボックスの左側のアイコンが変化して、選択されたアイテムがテーブルであるか列であるかが示されます。  
  
4.  をクリックして、**演算子**テキスト ボックスを一覧から等号 (=) 演算子を選択します。  
  
5.  をクリックして、**値**テキスト ボックス、および種類**M**します。  
  
6.  グリッドの次の行をクリックします。  
  
7.  をクリックして**OK**を閉じる、**モデル フィルター**  ダイアログ ボックス。  
  
     フィルターが表示されます、**プロパティ**ウィンドウ。 または、起動することができます、**モデル フィルター**ダイアログから、**プロパティ**ウィンドウ。  
  
8.  上記の手順では、今回の名前、モデルを繰り返して`TM_Decision_Tree_Female`と種類**F**で、**値**テキスト ボックス。  
  
## <a name="process-the-filtered-models"></a>フィルター選択されたモデルの処理  
 モデルを使用するには、事前にそのモデルを配置して処理する必要があります。 処理モデルの詳細については、次を参照してください。[メーリング対象となる構造の処理モデル&#40;Basic Data Mining Tutorial&#41;](../../2014/tutorials/processing-models-in-the-targeted-mailing-structure-basic-data-mining-tutorial.md)します。  
  
#### <a name="to-process-the-filtered-model"></a>フィルター選択されたモデルを処理するには  
  
1.  右クリックし、`TM_Decision_Tree_Male`モデルし、選択**および全モデルのマイニング構造の処理**s  
  
2.  クリックして**実行**新しいモデルを処理します。  
  
3.  処理が完了したら、クリックして**閉じる**両方の処理ウィンドウにします。  
  
     2 つの新しいモデルに表示されるようになりましたがある、**マイニング モデル**タブ。  
  
## <a name="evaluate-the-results"></a>結果の評価  
 結果を表示してフィルター選択されたモデルの精度を評価する方法は、前の 3 つのモデルの場合とほぼ同じです。 詳細については、以下をご覧ください。  
  
 [デシジョン ツリー モデルの検証&#40;基本的なデータ マイニング チュートリアル&#41;](../../2014/tutorials/exploring-the-decision-tree-model-basic-data-mining-tutorial.md)  
  
 [リフト チャートを使用した精度テスト (基本的なデータ マイニング チュートリアル)](../../2014/tutorials/testing-accuracy-with-lift-charts-basic-data-mining-tutorial.md)  
  
#### <a name="to-explore-the-filtered-models"></a>フィルター選択されたモデルを調査するには  
  
1.  選択、**マイニング モデル ビューアー** ] タブの [**データ マイニング デザイナー**します。  
  
2.  マイニング モデル ボックスで選択`TM_Decision_Tree_Male`します。  
  
3.  スライド**レベルを表示する**に`3`します。  
  
4.  変更、**バック グラウンド**値を`1`します。  
  
5.  カーソルを置くというラベルの付いたノード**すべて**自転車非購入者との自転車購入者の数を確認します。  
  
6.  手順 1 ~ 5 を繰り返します`TM_Decision_Tree_Female`します。  
  
7.  結果を検証、`TM_Decision_Tree`モデルが性別のフィルター処理します。 すべての自転車購入者と比較すると、男性の自転車購入者および女性の自転車購入者には、フィルター選択されていない自転車購入者と同じ特性もいくつかありますが、この 3 者には興味深い相違点もあります。 これは、有用な情報を[!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)]を使用してマーケティング キャンペーンを開発できます。  
  
#### <a name="to-test-the-lift-of-the-filtered-models"></a>フィルター選択されたモデルのリフトをテストするには  
  
1.  切り替えて、**マイニング精度チャート** タブで、データ マイニング デザイナーで[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]を選択し、**入力の選択**タブ。  
  
2.  **精度チャートに使用するデータセットの選択**グループ ボックスで、**マイニング構造のテスト_ケースを使用して、** します。  
  
3.  **入力の選択]** データ マイニング デザイナーのタブ [**リフト チャートに表示する予測可能なマイニング モデル列の選択**、チェック ボックスをオン**予測可能列を同期し、値**します。  
  
4.  **予測可能列名**列、いることを確認**Bike Buyer**が各モデルの選択されています。  
  
5.  **表示**列で、モデルの選択ごと。  
  
6.  **予測値**列で、`1`します。  
  
7.  選択、**リフト チャート**リフト チャートを表示するタブ。  
  
     3 つすべてのデシジョン ツリー モデルでランダム推測モデルよりも大幅なリフトが見られ、クラスター モデルや Naive Bayes モデルより高精度であることがわかります。  
  
## <a name="related-tasks"></a>Related Tasks  
 フィルターの詳細については、次を参照してください。[マイニング モデルのフィルター選択&#40;Analysis Services - データ マイニング&#41;](../../2014/analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining.md)します。  
  
 入れ子になったテーブルにフィルターを適用する方法の例は、次を参照してください。[中級者向けデータ マイニング チュートリアル&#40;Analysis Services - データ マイニング&#41;](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md)します。  
  
## <a name="previous-task-in-lesson"></a>このレッスンの前の作業  
 [リフト チャートを使用した精度テスト (基本的なデータ マイニング チュートリアル)](../../2014/tutorials/testing-accuracy-with-lift-charts-basic-data-mining-tutorial.md)  
  
## <a name="next-lesson"></a>次のレッスン  
 [レッスン 6:予測の作成と操作&#40;基本的なデータ マイニング チュートリアル&#41;](../../2014/tutorials/lesson-6-creating-and-working-with-predictions-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>参照  
 [中級者向けデータ マイニング チュートリアル&#40;Analysis Services - データ マイニング&#41;](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md)   
 [マイニング モデル タスクと操作方法](../../2014/analysis-services/data-mining/mining-model-tasks-and-how-tos.md)   
 [マイニング モデルからフィルターを削除します。](../../2014/analysis-services/data-mining/delete-a-filter-from-a-mining-model.md)   
 [マイニング モデルのフィルター &#40;Analysis Services - データ マイニング&#41;](../../2014/analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining.md)  
  
  
