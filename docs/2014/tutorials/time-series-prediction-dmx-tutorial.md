---
title: タイム シリーズ予測の DMX のチュートリアル |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 38ea7c03-4754-4e71-896a-f68cc2c98ce2
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 1623f824c062c270268323fd45ebf0e9533c8788
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63044189"
---
# <a name="time-series-prediction-dmx-tutorial"></a>時系列予測の DMX のチュートリアル
  このチュートリアルでは、時系列マイニング構造を作成し、3 つのカスタム時系列マイニング モデルを作成し、それらのモデルを使用して予測を行う方法を学習します。  
  
 マイニング モデルの作成は、[!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] サンプル データベース内のデータに基づいて行います。このサンプル データベースには、架空の企業である [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] のデータが格納されています。 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] は、多国籍の大規模な製造企業です。  
  
## <a name="tutorial-scenario"></a>チュートリアルのシナリオ  
 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] は、データ マイニングを使用して売上予測を生成することにしました。 一部地域の予測モデルが既に作成されています。詳細については、次を参照してください。[レッスン 2。予測シナリオの作成&#40;中級者向けデータ マイニング チュートリアル&#41;](../../2014/tutorials/lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial.md)します。 営業部門で、そのデータ マイニング モデルを新しい売上データで定期的に更新できるようにする必要があります。 また、さまざまな予測が得られるようにモデルをカスタマイズしたいとも考えています。  
  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] このタスクの実行に使用できるいくつかのツールを提供します。  
  
-   データ マイニング拡張機能 (DMX) クエリ言語  
  
-   Microsoft タイム シリーズ アルゴリズム  
  
-   [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] のクエリ エディター  
  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] タイム シリーズ アルゴリズムでは、時間に関するデータの予測に使用できるモデルが作成されます。 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] で提供されるデータ マイニング拡張機能 (DMX) は、マイニング モデルと予測クエリの作成に使用できるクエリ言語です。  
  
## <a name="what-you-will-learn"></a>学習する内容  
 このチュートリアルでは、[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] でマイニング モデルを作成するために使用するオブジェクトについて理解していることを前提にしています。 既に作成していないマイニング構造またはマイニング モデルを DMX を使用して場合を参照してください。 [Bike Buyer DMX のチュートリアル](../../2014/tutorials/bike-buyer-dmx-tutorial.md)します。  
  
 このチュートリアルは次のレッスンで構成されています。  
  
 [レッスン 1:タイム シリーズ マイニング モデルとマイニング構造を作成します。](../../2014/tutorials/lesson-1-creating-a-time-series-mining-model-and-mining-structure.md)  
 このレッスンでは、`CREATE MINING MODEL` ステートメントを使用して、新しい予測モデルと関連マイニング モデルを追加する方法を学習します。  
  
 [レッスン 2:時系列マイニング構造にマイニング モデルの追加](../../2014/tutorials/lesson-2-adding-mining-models-to-the-time-series-mining-structure.md)  
 このレッスンでは、ALTER MINING STRUCTURE ステートメントを使用して、新しいマイニング モデルを時系列構造に追加する方法を学習します。 また、時系列の分析に使用されるアルゴリズムをカスタマイズする方法も学習します。  
  
 [レッスン 3:タイム シリーズを処理構造およびモデル](../../2014/tutorials/lesson-3-processing-the-time-series-structure-and-models.md)  
 このレッスンでは、`INSERT INTO` ステートメントを使用して [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] データベースのデータを構造に取り込むことによってモデルをトレーニングする方法を学習します。  
  
 [レッスン 4:DMX を使用して時系列予測の作成](../../2014/tutorials/lesson-4-creating-time-series-predictions-using-dmx.md)  
 このレッスンでは、時系列予測を作成する方法を学習します。  
  
 [レッスン 5: タイム シリーズの拡張モデル](../../2014/tutorials/lesson-5-extending-the-time-series-model.md)  
 このレッスンでは、`EXTEND_MODEL_CASES` パラメーターを使用して、予測を行うときに新しいデータでモデルを更新する方法を学習します。  
  
## <a name="requirements"></a>必要条件  
 このチュートリアルを行う前に、次のソフトウェアがインストールされていることを確認してください。  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]  
  
-   [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]データベース  
  
 セキュリティ強化のため、既定ではサンプル データベースがインストールされません。 公式サンプル データベースをインストールする[!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]に移動して、 [ http://www.CodePlex.com/MSFTDBProdSamples ](https://go.microsoft.com/fwlink/?LinkId=88417)または Microsoft SQL Server の製品サンプルのセクションでは Microsoft SQL Server のサンプルとコミュニティのプロジェクトのホーム ページ。 をクリックして**データベース**、 をクリックし、**リリース**タブし、データベースを選択します。  
  
> [!NOTE]  
>  追加することをお勧めのチュートリアルを確認するとき**次のトピック**と**前のトピック**ドキュメント ビューアーのツールバーのボタン。  
  
## <a name="see-also"></a>参照  
 [基本的なデータ マイニング チュートリアル](../../2014/tutorials/basic-data-mining-tutorial.md)   
 [中級者向けデータ マイニング チュートリアル&#40;Analysis Services - データ マイニング&#41;](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md)  
  
  
