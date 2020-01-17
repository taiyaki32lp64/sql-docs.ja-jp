---
title: レッスン 2:予測シナリオ (中級者向けデータ マイニング チュートリアル) の作成 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- time series [Analysis Services]
- data mining [Analysis Services], tutorials
- tutorials [Data Mining]
ms.assetid: 9a988156-c900-4c22-97fa-f6b0c1aea9e2
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: ee814dc0891e70dfeccf2b96383d1d7b5c324aa8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62931530"
---
# <a name="lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial"></a>レッスン 2:予測シナリオ (中級者向けデータ マイニング チュートリアル) の作成
  [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)]のセールス アナリストであるあなたは、翌年の製品売上を予測するよう依頼されました。 具体的には、さまざまな地域および製品ラインの売上予測を比較する必要があります。 さらに、各製品の売上が一年を通じてどのように変化するかも調べなければなりません。  
  
 要求された情報を確認するには、このレッスンでは、月単位のレベルで会社の売上データを要約しますし 3 つのリージョンでの売上集計も。ヨーロッパ、北米、および太平洋します。  
  
 このレッスンのタスクを完了すると、次の情報を取得できるようになります。  
  
-   各種の自転車の売上の時系列における変化。  
  
-   3 つの地域での売上パターンに違いがあるかどうか。  
  
-   売上高が最も多い時期を予測できるか。  
  
 レッスンは、2 つに分けて行うことができます。  
  
-   第 1 部では、タイム シリーズ モデルを作成および使用する方法の基本について説明します。  
  
-   第 2 部では、すべての地域に基づいた汎用的なタイム シリーズ モデルを作成する方法を、順をおって説明します。 この汎用モデルを使用する*クロス予測*します。  
  
 このレッスンでは、次のとおり、タスクを完了するのには、使用、[!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]データ ソースで作成した[レッスン 1。中級者向けデータ マイニング ソリューションを作成する&#40;中級者向けデータ マイニング チュートリアル&#41;](../../2014/tutorials/lesson-1-create-solution-intermediate-data-mining-tutorial.md)します。  
  
> [!WARNING]  
>  [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] サンプル データベース内の日付は、このリリース用に更新されています。 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)]の以前のバージョンを使用する場合は、ここでの手順に従ってモデルを構築することはできますが、異なる結果が表示される場合があります。  
  
 **単純な予測モデルの作成**  
  
-   [予測のためのソース ビューのデータを追加する&#40;中級者向けデータ マイニング チュートリアル&#41;](../../2014/tutorials/adding-a-data-source-view-for-forecasting-intermediate-data-mining-tutorial.md)  
  
-   [Forecasting 構造およびモデルの作成&#40;中級者向けデータ マイニング チュートリアル&#41;](../../2014/tutorials/creating-a-forecasting-structure-and-model-intermediate-data-mining-tutorial.md)  
  
-   [Forecasting 構造の変更&#40;中級者向けデータ マイニング チュートリアル&#41;](../../2014/tutorials/modifying-the-forecasting-structure-intermediate-data-mining-tutorial.md)  
  
-   [予測モデルの処理のカスタマイズと&#40;中級者向けデータ マイニング チュートリアル&#41;](../../2014/tutorials/customize-process-forecasting-model-intermediate-data-mining-tutorial.md)  
  
-   [予測モデルの検証&#40;中級者向けデータ マイニング チュートリアル&#41;](../../2014/tutorials/exploring-the-forecasting-model-intermediate-data-mining-tutorial.md)  
  
-   [時系列予測の作成&#40;中級者向けデータ マイニング チュートリアル&#41;](../../2014/tutorials/creating-time-series-predictions-intermediate-data-mining-tutorial.md)  
  
 **クロス予測の一般的な予測モデルを作成します。**  
  
-   [タイム シリーズ予測を高度な&#40;中級者向けデータ マイニング チュートリアル&#41;](../../2014/tutorials/advanced-time-series-predictions-intermediate-data-mining-tutorial.md)  
  
-   [更新後のデータを使用して時系列予測&#40;中級者向けデータ マイニング チュートリアル&#41;](../../2014/tutorials/time-series-predictions-using-updated-data-intermediate-data-mining-tutorial.md)  
  
-   [置き換え後のデータを使用して時系列予測&#40;中級者向けデータ マイニング チュートリアル&#41;](../../2014/tutorials/time-series-predictions-replacement-data-intermediate-data-mining.md)  
  
-   [予測モデルの予測を比較する&#40;中級者向けデータ マイニング チュートリアル&#41;](../../2014/tutorials/comparing-predictions-for-forecasting-models-intermediate-data-mining-tutorial.md)  
  
## <a name="next-task-in-lesson"></a>このレッスンの次の作業  
 [予測のためのソース ビューのデータを追加する&#40;中級者向けデータ マイニング チュートリアル&#41;](../../2014/tutorials/adding-a-data-source-view-for-forecasting-intermediate-data-mining-tutorial.md)  
  
 [モデルの時系列の要件について&#40;中級者向けデータ マイニング チュートリアル&#41;](../../2014/tutorials/time-series-model-requirements-intermediate-data-mining-tutorial.md)  
  
## <a name="all-lessons"></a>すべてのレッスン  
 [レッスン 1:中級者向けデータ マイニング ソリューションを作成する&#40;中級者向けデータ マイニング チュートリアル&#41;](../../2014/tutorials/lesson-1-create-solution-intermediate-data-mining-tutorial.md)  
  
 レッスン 2:予測シナリオ (中級者向けデータ マイニング チュートリアル)  
  
 [レッスン 3:マーケット バスケット シナリオの作成&#40;中級者向けデータ マイニング チュートリアル&#41;](../../2014/tutorials/lesson-3-building-a-market-basket-scenario-intermediate-data-mining-tutorial.md)  
  
 [レッスン 4:シーケンス クラスター シナリオの構築&#40;中級者向けデータ マイニング チュートリアル&#41;](../../2014/tutorials/lesson-4-build-sequence-clustering-scenario-intermediate-data-mining.md)  
  
 [レッスン 5: ニューラル ネットワーク モデルとロジスティック回帰モデルを構築&#40;中級者向けデータ マイニング チュートリアル&#41;](../../2014/tutorials/lesson-5-build-models-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>関連項目  
 [基本的なデータ マイニング チュートリアル](../../2014/tutorials/basic-data-mining-tutorial.md)   
 [中級者向けデータ マイニング チュートリアル&#40;Analysis Services - データ マイニング&#41;](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md)   
 [Microsoft タイム シリーズ アルゴリズム](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm.md)  
  
  
