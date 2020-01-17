---
title: 構造体 (基本的なデータ マイニング チュートリアル) のテスト データ セットの指定 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 75cd508f-b126-418b-848d-3c4c3e6c303f
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 21eaa86fb1ff594e8b9d2b779b787276ee13ab4b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62720101"
---
# <a name="specifying-a-testing-data-set-for-the-structure-basic-data-mining-tutorial"></a>構造のテスト データ セットの指定 (基本的なデータ マイニング チュートリアル)
  データ マイニング ウィザードの最後の数画面では、データをテスト セットとトレーニング セットに分割します。 次に、構造に名前を付けて、モデルのドリルスルーを有効にします。  
  
## <a name="specifying-a-testing-set"></a>テスト セットの指定  
 マイニング構造を作成する際にデータをトレーニング セットとテスト セットに分割すると、後で作成するマイニング モデルの精度を簡単に評価できるようになります。 テスト セットの詳細については、次を参照してください。[トレーニングとテスト データ セット](../../2014/analysis-services/data-mining/training-and-testing-data-sets.md)します。  
  
#### <a name="to-specify-the-testing-set"></a>テスト セットを指定するには  
  
1.  **テスト セットの作成** ページの**テスト用データの割合**の既定値をそのまま`30`します。  
  
2.  **テスト データ セット内のケースの最大数**、型`1000`します。  
  
3.  **[次へ]** をクリックします。  
  
## <a name="specifying-drillthrough"></a>ドリルスルーの指定  
 ドリルスルーは、モデルおよび構造で有効にできます。 このダイアログ ボックスのチェック ボックスを使って、該当するモデルに対するドリルスルーを有効にします。 モデルの処理後は、モデルの作成に使用されたトレーニング データから、詳細情報を取得できます。  
  
 基になるマイニング構造もドリルスルーを許可するように構成されている場合は、モデル ケースとマイニング構造の両方から、詳細な情報 (マイニング モデルに含まれていなかった列など) を取得できます。 詳細については、「 [ドリルスルー クエリ (データ マイニング)](../../2014/analysis-services/data-mining/drillthrough-queries-data-mining.md)」をご覧ください。  
  
#### <a name="to-name-the-model-and-structure-and-specify-drillthrough"></a>モデルおよび構造に名前を付けてドリルスルーを指定するには  
  
1.  **ウィザードの完了**] ページの [**マイニング構造名**、型`Targeted Mailing`します。  
  
2.  **マイニング モデル名**、型`TM_Decision_Tree`します。  
  
3.  選択、**ドリルスルーを許可する**チェック ボックスをオンします。  
  
4.  レビュー、**プレビュー**ウィンドウ。 として選択されている列だけであることを確認**キー**、**入力**または**予測可能**が表示されます。 選択した他の列 (AddressLine1 など) は、モデルの作成には使用されませんが、基になる構造で使用することができ、モデルを処理および配置した後でクエリすることができます。  
  
5.  **[完了]** をクリックします。  
  
## <a name="previous-task-in-lesson"></a>このレッスンの前の作業  
 [データ型とコンテンツの種類を指定する&#40;基本的なデータ マイニング チュートリアル&#41;](../../2014/tutorials/specifying-the-data-type-and-content-type-basic-data-mining-tutorial.md)  
  
## <a name="next-lesson"></a>次のレッスン  
 [レッスン 3:追加して、モデルの処理](../../2014/tutorials/lesson-3-adding-and-processing-models.md)  
  
## <a name="see-also"></a>参照  
 [マイニング モデルのドリルスルーを有効にします。](../../2014/analysis-services/data-mining/enable-drillthrough-for-a-mining-model.md)   
 [ドリルスルー クエリ (データ マイニング)](../../2014/analysis-services/data-mining/drillthrough-queries-data-mining.md)   
 [トレーニング データの指定&#40;データ マイニング ウィザード&#41;](../../2014/analysis-services/specify-the-training-data-data-mining-wizard.md)  
  
  
