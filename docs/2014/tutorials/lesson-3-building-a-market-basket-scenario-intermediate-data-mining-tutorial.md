---
title: 'レッスン 3: マーケット バスケット シナリオ (中級者向けデータ マイニング チュートリアル) の作成 |Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data mining [Analysis Services], tutorials
- association algorithms [Analysis Services]
- nested tables
- tutorials [Data Mining]
ms.assetid: 651eef38-772e-4d97-af51-075b1b27fc5a
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: c2f1c5a8ae897284f07c3fd6c65d9735099a41fa
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63042788"
---
# <a name="lesson-3-building-a-market-basket-scenario-intermediate-data-mining-tutorial"></a>レッスン 3: マーケット バスケット シナリオ (中級者向けデータ マイニング チュートリアル) の作成
  [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] のマーケティング部門は、クロスセルを促進するため自社の Web サイトを改善しようとしています。 サイトの更新に伴い、顧客の買い物かごの中に入っている他製品に基づいてその顧客が購入する可能性がある製品を予測できるようにしたいと考えています。 さらに、顧客の購入行動をより深く理解して、一緒に購入される可能性があるアイテムが同時に表示されるように Web サイトを設計したいとも考えています。 彼らはこの種の *マーケット バスケット分析* にはデータ マイニングが非常に効果的であることを理解しており、あなたにデータ マイニング モデルの開発を依頼してきました。  
  
 このレッスンを完了すると、顧客のトランザクション履歴から商品のグループを表示する完全なマイニング モデルを作成できます。 さらに、このマイニング モデルを使用して、顧客が追加購入する可能性がある商品を予測できます。  
  
 このレッスンでは、タスクを完了するには、最初のレッスンで作成したソリューションとデータ ソースを使用するが、[中級者向けデータ マイニング チュートリアル&#40;Analysis Services - データ マイニング&#41;](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md)します。 顧客関連のテーブル (顧客の購入情報が格納される入れ子になったテーブルなど) を含むデータ ソース ビューを追加することで、このソリューションを変更します。  次に、マーケット バスケット シナリオに適した Microsoft アソシエーション ルール アルゴリズムを使用するマイニング モデルを作成します。  
  
 このレッスンの内容は次のとおりです。  
  
-   [入れ子になったテーブルとビューをソース データを追加する&#40;中級者向けデータ マイニング チュートリアル&#41;](../../2014/tutorials/adding-a-data-source-view-with-nested-tables-intermediate-data-mining-tutorial.md)  
  
-   [Market Basket 構造およびモデルの作成&#40;中級者向けデータ マイニング チュートリアル&#41;](../../2014/tutorials/creating-a-market-basket-structure-and-model-intermediate-data-mining-tutorial.md)  
  
-   [変更して、マーケット バスケット モデルの処理&#40;中級者向けデータ マイニング チュートリアル&#41;](../../2014/tutorials/modify-process-market-basket-model-intermediate-data-mining-tutorial.md)  
  
-   [マーケット バスケット モデルの検証&#40;中級者向けデータ マイニング チュートリアル&#41;](../../2014/tutorials/exploring-the-market-basket-models-intermediate-data-mining-tutorial.md)  
  
-   [マイニング モデルの入れ子になったテーブルをフィルター処理&#40;中級者向けデータ マイニング チュートリアル&#41;](../../2014/tutorials/filtering-a-nested-table-in-a-mining-model-intermediate-data-mining-tutorial.md)  
  
-   [アソシエーションを予測する&#40;中級者向けデータ マイニング チュートリアル&#41;](../../2014/tutorials/predicting-associations-intermediate-data-mining-tutorial.md)  
  
## <a name="next-task-in-lesson"></a>このレッスンの次の作業  
 [入れ子になったテーブルとビューをソース データを追加する&#40;中級者向けデータ マイニング チュートリアル&#41;](../../2014/tutorials/adding-a-data-source-view-with-nested-tables-intermediate-data-mining-tutorial.md)  
  
## <a name="all-lessons"></a>すべてのレッスン  
 [レッスン 1:中級者向けデータ マイニング ソリューションを作成する&#40;中級者向けデータ マイニング チュートリアル&#41;](../../2014/tutorials/lesson-1-create-solution-intermediate-data-mining-tutorial.md)  
  
 [レッスン 2:予測シナリオの作成&#40;中級者向けデータ マイニング チュートリアル&#41;](../../2014/tutorials/lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial.md)  
  
 レッスン 3: マーケット バスケット シナリオ (中級者向けデータ マイニング チュートリアル)  
  
 [レッスン 4:シーケンス クラスター シナリオの構築&#40;中級者向けデータ マイニング チュートリアル&#41;](../../2014/tutorials/lesson-4-build-sequence-clustering-scenario-intermediate-data-mining.md)  
  
 [レッスン 5: ニューラル ネットワーク モデルとロジスティック回帰モデルを構築&#40;中級者向けデータ マイニング チュートリアル&#41;](../../2014/tutorials/lesson-5-build-models-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>参照  
 [基本的なデータ マイニング チュートリアル](../../2014/tutorials/basic-data-mining-tutorial.md)   
 [レッスン 2:予測シナリオの作成&#40;中級者向けデータ マイニング チュートリアル&#41;](../../2014/tutorials/lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial.md)   
 [レッスン 4:シーケンス クラスター シナリオの構築&#40;中級者向けデータ マイニング チュートリアル&#41;](../../2014/tutorials/lesson-4-build-sequence-clustering-scenario-intermediate-data-mining.md)  
  
  
