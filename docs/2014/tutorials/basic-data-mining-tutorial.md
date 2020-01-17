---
title: 基本的なデータ マイニングのチュートリアル |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- databases [Analysis Services], tutorials
- data mining [Analysis Services], tutorials
- tutorials [Data Mining]
ms.assetid: 6602edb6-d160-43fb-83c8-9df5dddfeb9c
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: d434df95a26485d4d7795d3ab960b8d2457b8ff6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63185576"
---
# <a name="basic-data-mining-tutorial"></a>基本的なデータ マイニング チュートリアル
  ようこそ、 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]基本的なデータ マイニングのチュートリアル。 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] データ マイニング モデルを作成および予測を行うのための統合環境を提供します。 このチュートリアルでは、分析し、顧客の購買行動を予測する機械学習を使用するターゲット メーリング キャンペーンのシナリオを完了します。 このチュートリアルでは、クラスタリング、デシジョン ツリー、Naive Bayes (ナイーブ ベイズ) という非常に重要な 3 つのデータ マイニング アルゴリズムを使用する方法を示します。 マイニング モデル ビューアーを使用して結果の分析、予測と精度のグラフに含まれているデータ マイニング ツールを使用して作成する方法も学習[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]します。 すべての例で、架空の企業である [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] を使用します。  
  
 完了させることをお勧め、データ マイニング ツールを使用して快適なしたら、[中級者向けデータ マイニング チュートリアル&#40;Analysis Services - データ マイニング&#41;](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md)します。 これらのレッスンでは、予測、マーケット バスケット分析、タイム シリーズ (時系列)、アソシエーション モデル、入れ子になったテーブル、およびシーケンス クラスターの使用方法を示します。  
  
## <a name="tutorial-scenario"></a>チュートリアルのシナリオ  
 従業員では、このチュートリアルでは[!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)]命じられた購買履歴に基づいて会社の顧客に関する詳細と、その履歴データを使用して、マーケティングのために使用できる予測を作成します。 会社はこれまでデータ マイニングを行ったことがなかったので、データ マイニング専用の新しいデータベースを作成し、データ マイニング モデルを設定する必要があります。  
  
## <a name="what-you-will-learn"></a>学習する内容  
 このチュートリアルでは、さまざまな種類の機械学習メソッドの作成方法と使用方法を説明します。 また、マイニング モデルのコピーを作成し、入力データにフィルターを適用してさまざまな結果を取得する方法も学習します。 その後、リフト チャートを使用して、両方のモデルの結果を比較できます。 最後に、ドリルスルーを使用して、基になるマイニング構造から詳細なデータを取得します。  
  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] データ マイニングは、次を含むため、簡単に機能の開発し複数の予測モデルを比較および結果に対して操作を実行します。  
  
-   *提示されたテスト セット -* トレーニング セットとテスト セットにマイニング構造内のデータを分割するマイニング構造を作成するときにようになりましたことができます。 これにより、類似のデータ セットに対してモデルをテストし、関連するモデルの精度を比較できます。  
  
-   *マイニング モデルのフィルター -* フィルターをマイニング モデルにアタッチし、トレーニングとテストの両方に、フィルターを適用できます。 これにより、データの異なるサブセットに対して関連モデルを簡単に構築できます。  
  
-   *構造ケースおよび構造列へのドリルスルー*簡単に移行できます、マイニング モデルの一般的なパターンから実用的な詳細に、データ ソース。  
  
 このチュートリアルは次のレッスンで構成されています。  
  
 [レッスン 1:準備、Analysis Services Database&#40;基本的なデータ マイニング チュートリアル&#41;](../../2014/tutorials/lesson-1-preparing-the-analysis-services-database-basic-data-mining-tutorial.md)  
 このレッスンでは、新しい [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] データベースを作成する方法、データ ソースとデータ ソース ビューを追加する方法、およびデータ マイニングで使用する新しいデータベースを準備する方法を学習します。  
  
 [レッスン 2:ターゲット メーリングの構造を構築&#40;基本的なデータ マイニング チュートリアル&#41;](../../2014/tutorials/lesson-2-building-a-targeted-mailing-structure-basic-data-mining-tutorial.md)  
 このレッスンでは、絞り込みメール配信シナリオの一部として使用できるマイニング モデル構造の作成方法を学習します。  
  
 [レッスン 3:追加して、モデルの処理](../../2014/tutorials/lesson-3-adding-and-processing-models.md)  
 このレッスンでは、構造にモデルを追加する方法を学習します。 モデルの作成には、次のアルゴリズムを使用します。  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] デシジョン ツリー  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] クラスター  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] Naive Bayes  
  
 [レッスン 4:メーリング対象モデルの検証&#40;基本的なデータ マイニング チュートリアル&#41;](../../2014/tutorials/lesson-4-exploring-the-targeted-mailing-models-basic-data-mining-tutorial.md)  
 このレッスンでは、ビューアーを使用して各モデルの結果を調査および解釈する方法を学習します。  
  
 [レッスン 5: モデルのテスト&#40;基本的なデータ マイニング チュートリアル&#41;](../../2014/tutorials/lesson-5-testing-models-basic-data-mining-tutorial.md)  
 このレッスンでは、いずれかの絞り込みメール配信モデルのコピーを作成し、トレーニング データを制限するためのマイニング モデル フィルターを特定の顧客のセットに追加し、モデルの実行可能性を評価します。  
  
 [レッスン 6:予測の作成と操作&#40;基本的なデータ マイニング チュートリアル&#41;](../../2014/tutorials/lesson-6-creating-and-working-with-predictions-basic-data-mining-tutorial.md)  
 「基本的なデータ マイニング チュートリアル」の最後のレッスンでは、モデルを使用して、自転車を購入する可能性が最も高い顧客を予測します。 次に、基になるケースをドリルスルーして連絡先情報を取得します。  
  
## <a name="requirements"></a>必要条件  
 次のソフトウェアがインストールされていることを確認してください。  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 多次元モードで  
  
-   [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] データベース。  
  
 セキュリティ強化のため、サンプル データベースは [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] と一緒にインストールされません。 公式データベースをインストールする[!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]を参照してください、 [Microsoft SQL Sample Databases](https://go.microsoft.com/fwlink/?LinkId=88417) ] ページ[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]します。  
  
> [!NOTE]  
>  のチュートリアルに従って作業しているときにした方を追加する場合、手順の間で双方向に移動しやすく、**次のトピック**と**前のトピック**ドキュメント ビューアーのツールバーのボタン。  
  
## <a name="see-also"></a>関連項目  
 [データ マイニング ソリューション](../../2014/analysis-services/data-mining/data-mining-solutions.md)   
 [マイニング モデル タスクと操作方法](../../2014/analysis-services/data-mining/mining-model-tasks-and-how-tos.md)   
 [DMX を使用したデータ マイニング モデルのクエリの作成と:チュートリアル&#40;Analysis Services - データ マイニング&#41;](../../2014/tutorials/create-query-data-mining-models-dmx-tutorials.md)  
  
  
