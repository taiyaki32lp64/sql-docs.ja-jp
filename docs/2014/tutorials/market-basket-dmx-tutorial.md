---
title: マーケット バスケット DMX のチュートリアル |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- DMX [Analysis Services], tutorials
- data mining [Analysis Services], tutorials
- statements [DMX], tutorials
- Data Mining Extensions [Analysis Services], tutorials
- market basket analysis [Analysis Services]
- tutorials [Data Mining]
- tutorials [DMX]
ms.assetid: 6e262a1d-c89e-4033-8368-46cf25168ef5
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: fe12f1c4ca1c0946572c61e89f4f4edb8ba9a762
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63185644"
---
# <a name="market-basket-dmx-tutorial"></a>マーケット バスケット DMX のチュートリアル
  このチュートリアルでは、作成、トレーニング、およびデータ マイニング拡張機能 (DMX) クエリ言語を使用してマイニング モデルを調査する方法を学びます。 その後、このマイニング モデルを使用して、同時に購入される傾向が高い製品を示す予測を作成します。  
  
 マイニング モデルは、[!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] サンプル データベース内のデータから作成します。このサンプル データベースには、架空の企業である [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] のデータが格納されています。 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] は、多国籍の大規模な製造企業です。 北米、ヨーロッパ、およびアジアの市場向けに、金属製自転車や複合材製自転車の製造および販売を行っています。 企業の拠点は従業員 290 人を擁する米国ワシントン州ボセルで、また各国の市場の拠点として、複数の地域販売チームが配置されています。  
  
## <a name="tutorial-scenario"></a>チュートリアルのシナリオ  
 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] は、データ マイニング機能を用いたカスタム アプリケーションを作成して、同時に購入する傾向が高い製品の種類を予測することにしました。 このカスタム アプリケーションの目標は、一連の製品を指定できるようにし、指定した製品と共に購入される追加製品を予測できるようにすることです。 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] はこれらの情報を使用して、企業の Web サイトで "お勧め" の製品を表示すると共に、顧客によりわかりやすく情報を表示したいと考えています。  
  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] このタスクの実行に使用できるいくつかのツールを提供します。  
  
-   DMX クエリ言語  
  
-   [Microsoft アソシエーション アルゴリズム](../../2014/analysis-services/data-mining/microsoft-association-algorithm.md)  
  
-   [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] のクエリ エディター  
  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] で提供されるデータ マイニング拡張機能 (DMX) は、マイニング モデルの作成と作業に使用できるクエリ言語です。 [!INCLUDE[msCoName](../includes/msconame-md.md)]アソシエーション アルゴリズムを一緒に購入される可能性のある製品を予測できるモデルを作成します。  
  
 このチュートリアルの目標は、カスタム アプリケーションで使用する DMX クエリを設定することです。  
  
 **詳細:** [データ マイニング ソリューション](../../2014/analysis-services/data-mining/data-mining-solutions.md)  
  
## <a name="mining-structure-and-mining-models"></a>マイニング構造とマイニング モデル  
 DMX ステートメントを作成するにあたっては、[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] がマイニング モデルの作成に使用する主なオブジェクトを理解しておくことが重要です。 *マイニング構造*はマイニング モデルの作成元となるデータ ドメインを定義するデータ構造です。 1 つのマイニング構造に複数含めることができます*マイニング モデル*同じドメインを共有します。 マイニング モデルは、マイニング構造によって表されるデータにマイニング モデル アルゴリズムを適用します。  
  
 マイニング構造の構成要素は、データ ソースに格納されているデータについて記述したマイニング構造列です。 マイニング構造列には、データ型、コンテンツの種類、データの配布方法などの情報が格納されます。  
  
 マイニング モデルには、マイニング構造で記述されたキー列と、残りの列のサブセットが含まれる必要があります。 マイニング モデルでは、各列の使用法と、マイニング モデルの作成に使用するアルゴリズムを定義します。 たとえば、DMX では列がキー列または PREDICT 列であることを指定できます。 指定されない列は入力列として扱われます。  
  
 DMX でマイニング モデルを作成するには、2 つの方法があります。 1 つは、`CREATE MINING MODEL` ステートメントを使用して、マイニング構造とそれに関連するマイニング モデルを一度に作成する方法です。もう 1 つは、最初に `CREATE MINING STRUCTURE` ステートメントを使用してマイニング構造を作成し、`ALTER STRUCTURE` ステートメントを使用してマイニング モデルを追加する方法です。 これらの方法について次に説明します。  
  
 `CREATE MINING MODEL`  
 このステートメントを使用すると、マイニング構造とそれに関連するマイニング モデルを一度に、同じ名前を使って作成できます。 マイニング構造と区別するため、マイニング モデルの名前には "Structure" という文字列が付加されます。  
  
 このステートメントは、1 つのマイニング モデルを含むマイニング構造を作成する場合に便利です。  
  
 詳細については、「[CREATE MINING MODEL (DMX)](/sql/dmx/create-mining-model-dmx)」を参照してください。  
  
 CREATE MINING STRUCTURE  
 新しいマイニング構造をモデルなしで作成するには、このステートメントを使用します。  
  
 CREATE MINING STRUCTURE を使用すると、予約データ セットも作成できます。予約データ セットは、同一のマイニング構造に基づくすべてのモデルをテストするために使用できます。  
  
 詳細については、「[CREATE MINING STRUCTURE &#40;DMX&#41;](/sql/dmx/create-mining-structure-dmx)」を参照してください。  
  
 `ALTER MINING STRUCTURE`  
 このステートメントを使用すると、サーバー上に既に存在するマイニング構造にマイニング モデルを追加できます。  
  
 1 つのマイニング構造に複数のマイニング モデルを追加すると、いくつかの作業に役立ちます。 たとえば、異なるアルゴリズムを使用して複数のマイニング モデルを作成し、最適なアルゴリズムを見つけ出すことができます。 または、同じのアルゴリズムを使用して複数のマイニング モデルの作成がパラメーターを持つでそのパラメーターの最適な設定を検索するには、各マイニング モデルを異なる方法で設定する可能性があります。  
  
 詳細については、次を参照してください。 [ALTER MINING STRUCTURE &#40;DMX&#41;](/sql/dmx/alter-mining-structure-dmx?view=sql-server-2016)します。  
  
 このチュートリアルでは複数のマイニング モデルを含むマイニング構造を作成します。したがって、2 つ目の方法を使用します。  
  
 **詳細については**  
  
 [データ マイニング拡張機能&#40;DMX&#41;参照](/sql/dmx/data-mining-extensions-dmx-reference)、 [Select ステートメントを DMX を理解する](/sql/dmx/understanding-the-dmx-select-statement)、[構造と DMX 予測クエリの使用](/sql/dmx/structure-and-usage-of-dmx-prediction-queries)  
  
## <a name="what-you-will-learn"></a>学習する内容  
 このチュートリアルは次のレッスンで構成されています。  
  
 [レッスン 1:Market Basket マイニング構造を作成します。](../../2014/tutorials/lesson-1-creating-the-market-basket-mining-structure.md)  
 このレッスンでは、`CREATE` ステートメントを使用して、マイニング構造を作成する方法を学習します。  
  
 [レッスン 2:Market Basket マイニング構造にマイニング モデルの追加](../../2014/tutorials/lesson-2-adding-mining-models-to-the-market-basket-mining-structure.md)  
 このレッスンでは、`ALTER` ステートメントを使用して、マイニング モデルをマイニング構造に追加する方法を学習します。  
  
 [レッスン 3:Market Basket マイニング構造の処理](../../2014/tutorials/lesson-3-processing-the-market-basket-mining-structure.md)  
 このレッスンでは、使用する方法について説明します、`INSERT INTO`マイニング構造とその関連マイニング モデルを処理するステートメント。  
  
 [レッスン 4:マーケット バスケット予測の実行](../../2014/tutorials/lesson-4-executing-market-basket-predictions.md)  
 このレッスンでは、`PREDICTION JOIN` ステートメントを使用して、マイニング モデルに対する予測を作成する方法を学習します。  
  
## <a name="requirements"></a>必要条件  
 このチュートリアルを行う前に、次のソフトウェアがインストールされていることを確認してください。  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]  
  
-   [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]データベース  
  
 セキュリティ強化のため、既定ではサンプル データベースがインストールされません。 公式サンプル データベースをインストールする[!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]に移動して、 [ http://www.CodePlex.com/MSFTDBProdSamples ](https://go.microsoft.com/fwlink/?LinkId=88417)または Microsoft SQL Server の製品サンプルのセクションでは Microsoft SQL Server のサンプルとコミュニティのプロジェクトのホーム ページ。 をクリックして**データベース**、 をクリックし、**リリース**タブし、データベースを選択します。  
  
> [!NOTE]  
>  追加することをお勧めのチュートリアルを確認するとき**次のトピック**と**前のトピック**ドキュメント ビューアーのツールバーのボタン。  
  
## <a name="see-also"></a>参照  
 [Bike Buyer DMX のチュートリアル](../../2014/tutorials/bike-buyer-dmx-tutorial.md)   
 [基本的なデータ マイニング チュートリアル](../../2014/tutorials/basic-data-mining-tutorial.md)   
 [レッスン 3:マーケット バスケット シナリオの作成&#40;中級者向けデータ マイニング チュートリアル&#41;](../../2014/tutorials/lesson-3-building-a-market-basket-scenario-intermediate-data-mining-tutorial.md)  
  
  
