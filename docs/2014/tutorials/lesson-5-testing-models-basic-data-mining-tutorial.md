---
title: 'レッスン 5: モデル (基本的なデータ マイニング チュートリアル) のテスト |Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: e9a7ddcf-2b01-485f-bbb5-62638b303bc6
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 88a9d564b297d277d1566152cc11599bec912ddc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63185429"
---
# <a name="lesson-5-testing-models-basic-data-mining-tutorial"></a>レッスン 5: モデル (基本的なデータ マイニング チュートリアル) のテスト
  絞り込みメール配信シナリオのトレーニング セットを使用してモデルを処理したので、テスト セットに対してモデルをテストします。 検証は、データ マイニング プロセスにおける重要な手順です。 運用環境に配置する前に、実際のデータに対する絞り込みメール配信マイニング モデルの性能を把握しておくことが重要です。  
  
 テスト セット内のデータには自転車購入に関する既知の値が既に含まれているため、モデルの予測が正しいかどうかを簡単に判断できます。 パフォーマンスが最高のモデルで使用される、[!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)]マーケティング部門は、ターゲット メーリング キャンペーンの顧客を識別します。  
  
 このレッスンでは、複数の手法を使用してモデルを検証します。  
  
1.  既知の結果に精度のモデルが表示されるテスト セットに対して予測を行います。 使用して、*リフト チャート*にその効果を測定します。  
  
     [リフト チャートを使用した精度テスト (基本的なデータ マイニング チュートリアル)](../../2014/tutorials/testing-accuracy-with-lift-charts-basic-data-mining-tutorial.md)  
  
2.  フィルター選択されたデータ サブセットを対象にしてモデルをテストします。 同じリフト チャート内で複数のモデルを比較できます。  
  
     [フィルター選択されたモデルのテスト&#40;基本的なデータ マイニング チュートリアル&#41;](../../2014/tutorials/testing-a-filtered-model-basic-data-mining-tutorial.md)  
  
 一般にモデルの検証方法の詳細については、「[データ マイニングの概念](../../2014/analysis-services/data-mining/data-mining-concepts.md)します。  
  
## <a name="first-task-in-lesson"></a>このレッスンの最初の作業  
 [リフト チャートを使用した精度テスト (基本的なデータ マイニング チュートリアル)](../../2014/tutorials/testing-accuracy-with-lift-charts-basic-data-mining-tutorial.md)  
  
## <a name="previous-lesson"></a>前のレッスン  
 [レッスン 4:メーリング対象モデルの検証&#40;基本的なデータ マイニング チュートリアル&#41;](../../2014/tutorials/lesson-4-exploring-the-targeted-mailing-models-basic-data-mining-tutorial.md)  
  
## <a name="next-lesson"></a>次のレッスン  
 [レッスン 6:予測の作成と操作&#40;基本的なデータ マイニング チュートリアル&#41;](../../2014/tutorials/lesson-6-creating-and-working-with-predictions-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>参照  
 [リフト チャート タブ&#40;マイニング精度チャート ビュー&#41;](../../2014/analysis-services/lift-chart-tab-mining-accuracy-chart-view.md)   
 [リフト チャート &#40;Analysis Services - データ マイニング&#41;](../../2014/analysis-services/data-mining/lift-chart-analysis-services-data-mining.md)   
 [テストおよび検証 &#40;データ マイニング&#41;](../../2014/analysis-services/data-mining/testing-and-validation-data-mining.md)   
 [[分類マトリックス] タブ&#40;マイニング精度チャート] ビュー&#41;](../../2014/analysis-services/classification-matrix-tab-mining-accuracy-chart-view.md)   
 [分類マトリックス &#40;Analysis Services - データ マイニング&#41;](../../2014/analysis-services/data-mining/classification-matrix-analysis-services-data-mining.md)  
  
  
