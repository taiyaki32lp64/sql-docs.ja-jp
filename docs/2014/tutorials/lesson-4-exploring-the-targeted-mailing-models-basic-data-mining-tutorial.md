---
title: レッスン 4:調査対象の絞り込みメール配信モデル (基本的なデータ マイニング チュートリアル) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 1e00c5b9-a9f8-4503-99ee-377c9cc02d7f
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 97db61dc3b9adf2e345957c8e08aa752e51286e0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63312151"
---
# <a name="lesson-4-exploring-the-targeted-mailing-models-basic-data-mining-tutorial"></a>レッスン 4:調査対象の絞り込みメール配信モデル (基本的なデータ マイニング チュートリアル)
  プロジェクト内のモデルを処理した後、そのモデルを検証して、興味深い傾向を探すことができます。 パターンは複雑で、単純に数値を観察するだけでは見つけにくいことがあるため、SQL Server データ マイニング機能は、データを調査する目的、およびアルゴリズムがデータ内で見つけたルールとリレーションシップを理解する目的で役立つビジュアル ツールを用意しています。 また、さまざまな精度テストを使用してデータセットを検証し、モデルを配置する前にどのモデルが最も適切に機能するかを判断することができます。  
  
 使用すると[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]作成した各モデルを記載してモデルを参照する、**マイニング モデル ビューアー**データ マイニング デザイナーのタブ。 各種のビューアーを使用して、モデルを参照できます。 これらのビューアーは、[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] でも使用できます。  
  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] のどのアルゴリズムを使用してモデルを作成したかによって、それぞれ結果が異なります。 したがって、[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] は、機械学習モデルの種類ごとにカスタム ビューアーを用意しています。  
  
 詳細については、する場合[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]と呼ばれる、HTML ビューアーにも提供、**汎用コンテンツ ツリー ビューアー**、モデル データと半表形式で、検出されたパターンに関する詳細情報を表示します。 詳細については、「 [Microsoft 汎用コンテンツ ツリー ビューアーを使用したモデルの参照](../../2014/analysis-services/data-mining/browse-a-model-using-the-microsoft-generic-content-tree-viewer.md)」をご覧ください。  
  
 このレッスンでは、3 つのモデルを使用して結果を観察します。 モデルの種類ごとに、基になるアルゴリズムが異なり、データの検証方法も異なります。  
  
-   デシジョン ツリー モデルでは、自転車の購入に影響を与える要因がわかります。  
  
-   クラスター モデルでは、自転車の購買行動を含む属性やその他の任意の属性ごとに顧客をグループ化できます。  
  
-   Naive Bayes モデルでは、さまざまな属性間のリレーションシップを検証できます。  
  
 各マイニング モデル ビューアーの詳細については、次のトピックを参照してください。  
  
-   [デシジョン ツリー モデルの検証&#40;基本的なデータ マイニング チュートリアル&#41;](../../2014/tutorials/exploring-the-decision-tree-model-basic-data-mining-tutorial.md)  
  
-   [クラスター モデルの検証&#40;基本的なデータ マイニング チュートリアル&#41;](../../2014/tutorials/exploring-the-clustering-model-basic-data-mining-tutorial.md)  
  
-   [Naive Bayes モデルの検証&#40;基本的なデータ マイニング チュートリアル&#41;](../../2014/tutorials/exploring-the-naive-bayes-model-basic-data-mining-tutorial.md)  
  
 使用して 3 つすべてのモデルを表示できます、**汎用コンテンツ ツリー ビューアー**を数式やデータの値を抽出します。  
  
## <a name="first-task-in-lesson"></a>このレッスンの最初の作業  
 [デシジョン ツリー モデルの検証&#40;基本的なデータ マイニング チュートリアル&#41;](../../2014/tutorials/exploring-the-decision-tree-model-basic-data-mining-tutorial.md)  
  
## <a name="previous-lesson"></a>前のレッスン  
 [レッスン 3:追加して、モデルの処理](../../2014/tutorials/lesson-3-adding-and-processing-models.md)  
  
## <a name="next-lesson"></a>次のレッスン  
 [レッスン 5: モデルのテスト&#40;基本的なデータ マイニング チュートリアル&#41;](../../2014/tutorials/lesson-5-testing-models-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>参照  
 [マイニング モデル ビューアーのタスクと操作方法](../../2014/analysis-services/data-mining/mining-model-viewer-tasks-and-how-tos.md)   
 [データ マイニング モデル ビューアー](../../2014/analysis-services/data-mining/data-mining-model-viewers.md)  
  
  
