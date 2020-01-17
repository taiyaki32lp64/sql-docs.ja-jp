---
title: データ マイニング クエリ |Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- prediction queries [Analysis Services]
- queries [DMX], creating
- prediction queries [DMX]
- Prediction Query Builder
- mining models [Analysis Services], querying
ms.assetid: 802806a6-69bb-4c3c-b9aa-d1a1ddfc7fc2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2bfce63f3686f06c0289c818daac82f336fb2b17
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66084969"
---
# <a name="data-mining-queries"></a>データ マイニング クエリ
  データ マイニング クエリは多くの目的で役立ちます。 可能な代替手段としては以下の方法があります。  
  
-   モデルを新しいデータに適用し、1 つまたは複数の予測を作成する。 入力値をパラメーターとして、またはバッチで提供する。  
  
-   トレーニングに使用したデータの統計サマリーを取得する。  
  
-   パターンとルールを抽出する、またはモデル内のパターンを表現する代表的なケースのプロファイルを生成する。  
  
-   回帰式と、パターンを説明する他の計算を抽出する。  
  
-   特定のパターンに適合するケースを取得する。  
  
-   分析で使用されないデータも含め、モデルで使用された個々のケースに関する詳細を取得する。  
  
-   新しいデータの追加、またはクロス予測の実行によりモデルを再トレーニングする。  
  
 ここでは、最初に知っておく必要があるデータ マイニング クエリの概要を説明します。 データ マイニング オブジェクトに対して作成できるクエリの種類を示して、クエリ ツールおよびクエリ言語について説明します。また、SQL Server データ マイニングで提供されるアルゴリズムを使用してビルドしたモデルに対して作成できるクエリ例へのリンクを示します。  
  
 [データ マイニング クエリについて](#bkmk_Understand)  
  
 [クエリ ツールとインターフェイス](#bkmk_Interfaces)  
  
 [さまざまな種類のモデルのクエリ](#bkmk_ModelTypes)  
  
 [必要条件](#bkmk_Reqs)  
  
##  <a name="bkmk_Understand"></a> データ マイニング クエリについて  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データ マイニングでは、次の種類のクエリがサポートされています。  
  
-   [予測クエリ &#40;データ マイニング&#41;](prediction-queries-data-mining.md)  
  
     モデル内のパターンおよび入力データから推論するクエリ。  
  
-   [コンテンツ クエリ &#40;データ マイニング&#41;](content-queries-data-mining.md)  
  
     メタデータ、統計、およびその他、モデル自体の情報を返すクエリ。  
  
-   [ドリルスルー クエリ &#40;データ マイニング&#41;](drillthrough-queries-data-mining.md)  
  
     基になるケース データをモデルから取得できるクエリ。モデルで使用されていないデータさえ構造体から取得できます。  
  
-   [データ定義クエリ &#40;データ マイニング&#41;](data-definition-queries-data-mining.md)  
  
     モデルからの情報は返さないが、モデルおよび構造体のビルド、またはモデルまたは構造体内のデータの更新に使用されるクエリ。  
  
 クエリを作成する前に、SQL Server の各データ マイニング アルゴリズムを使用して作成されるモデルの違いを理解してください。  
  
-   各種のアルゴリズムに対して用意されているカスタム データ マイニング ビューアーを使用して、各種のモデルを参照して調査します。 詳細については、「 [マイニング モデル ビューアーのタスクと操作方法](mining-model-viewer-tasks-and-how-tos.md)」を参照してください。  
  
-   **Microsoft 汎用コンテンツ ツリー ビューアー**を使用して、各種のモデルのモデル コンテンツを確認します。 この情報を解釈する方法については、「[マイニング モデル コンテンツ &#40;Analysis Services - データ マイニング&#41;](mining-model-content-analysis-services-data-mining.md)」を参照してください。  
  
##  <a name="bkmk_Interfaces"></a> クエリ ツールとインターフェイス  
 SQL Server で用意されているクエリ ツールを使用すると、データ マイニング クエリを対話形式で作成できます。 グラフィカルな予測クエリ ビルダーは、 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] と [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]の両方で用意されています。 これまで予測クエリ ビルダーを使用したことがない場合は、インターフェイスに慣れるために「 [Basic Data Mining Tutorial](../../tutorials/basic-data-mining-tutorial.md) 」の手順を実行することをお勧めします。 手順の概要を簡単に把握するには、「 [予測クエリ ビルダーを使用した予測クエリの作成](create-a-prediction-query-using-the-prediction-query-builder.md)」のクエリ作成の手順を参照してください。  
  
 予測クエリ ビルダーは、クエリを開始して後からカスタマイズする際に役立ちます。 簡単にデータ ソースを追加して列にマップすることができ、その後、DMX ビューに切り替えて、WHERE 句や他の関数を追加してクエリをカスタマイズできます。  
  
 データ マイニング モデル、およびクエリのビルド方法を理解したら、データ マイニング拡張機能 (DMX) を使用してクエリを直接作成することもできます。 DMX は Transact-SQL に似たクエリ言語であり、多数のクライアントから使用できます。 DMX は、カスタムの予測と複雑なクエリの両方を作成するために選ばれるツールです。 DMX の概要については、次を参照してください。[の作成とクエリを実行するデータ マイニング モデル DMX を使用しました。チュートリアル&#40;Analysis Services - データ マイニング&#41;](../../tutorials/create-query-data-mining-models-dmx-tutorials.md)します。  
  
 DMX エディターは、 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] と [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]の両方で提供されます。 また、予測クエリ ビルダーを使用してクエリを開始してから、ビューをテキスト エディターに変更し、DMX ステートメントを別のクライアントにコピーすることもできます。 詳細については、次を参照してください。[データ マイニング クエリ インターフェイス](data-mining-query-tools.md)します。  
  
 DMX ステートメントをプログラムで作成し、AMO または XMLA を使用して、クライアントから [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] サーバーに送信できます。 ただし、DMX は、マイニング モデルに対するクエリを作成するために使用する必要がある言語です。  
  
 さらに、データ マイニング スキーマ行セットに基づく動的管理ビュー (DMV) を使用して、メタデータ、統計、またはモデル コンテンツに対してクエリを実行することもできます。 DMV により、SELECT ステートメントを使用してモデルに関する情報を簡単に取得できるようになりますが、予測を作成することはできません。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] でサポートされる DMV の詳細については、「[動的管理ビュー &#40;DMV&#41; を使用した Analysis Services の監視](../instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services.md)」を参照してください。  
  
 また、 [Data Mining Query Task](../../integration-services/control-flow/data-mining-query-task.md)または [Data Mining Query Transformation](../../integration-services/data-flow/transformations/data-mining-query-transformation.md)を使用することで、Integration Services パッケージで使用するデータ マイニング クエリも作成できます。 制御フロー タスクでは複数の種類の DMX クエリがサポートされますが、データ フロー変換ではそのデータ フローのデータに対するクエリ (つまり、PREDICTION JOIN 構文を使用するクエリ) のみがサポートされます。  
  
##  <a name="bkmk_ModelTypes"></a> さまざまな種類のモデルのクエリ  
 データ マイニング クエリで取得できる情報の種類は、モデルの作成時に使用されたアルゴリズムから大きな影響を受けます。 違いの理由は、各アルゴリズムがデータをさまざまな方法で処理し、さまざまなパターンを格納するためです。 たとえば、クラスターを作成するアルゴリズムもあれば、クラスターを作成するアルゴリズムもあります。 したがって、場合によっては、使用するモデルの種類に応じて特定の予測関数やクエリ関数を使用する必要があります。  
  
 次に、クエリで使用できる関数を要約して示します。  
  
-   **汎用の予測関数:** `Predict`関数はポリモーフィックでは、すべての種類のモデルで動作を意味します。 この関数は、使用しているモデルの種類を自動的に検出し、パラメーターの追加を要求します。 詳細については、「[予測 &#40;DMX&#41;](/sql/dmx/predict-dmx)」を参照してください。  
  
    > [!WARNING]  
    >  すべてのモデルが予測に使用されるわけではありません。 たとえば、予測可能な属性を持たないクラスタリングのモデルを作成できます。 ただし、モデルに予測可能属性がない場合でも、モデルから他の役立つ情報を返す予測クエリを作成することはできます。  
  
-   **カスタム予測関数:** 各種のモデルでは、そのアルゴリズムで作成されたパターンを使用するために設計された予測関数のセットを提供します。  
  
     たとえば、`Lag` 関数はタイム シリーズ モデルのために用意されており、このモデルで使用される履歴データを表示できます。 クラスタリング モデルの場合は、`ClusterDistance` などの関数がさらに重要です。  
  
     各種のモデルでサポートされる関数の詳細については、次のリンクを参照してください。  
  
    |||  
    |-|-|  
    |[結合モデルのクエリ例](association-model-query-examples.md)|[Microsoft Naive Bayes アルゴリズム](microsoft-naive-bayes-algorithm.md)|  
    |[クラスタリング モデルのクエリ例](clustering-model-query-examples.md)|[ニューラル ネットワーク モデルのクエリ例](neural-network-model-query-examples.md)|  
    |[デシジョン ツリー モデルのクエリ例](decision-trees-model-query-examples.md)|[シーケンス クラスター モデルのクエリの例](sequence-clustering-model-query-examples.md)|  
    |[線形回帰モデルのクエリ例](linear-regression-model-query-examples.md)|[タイム シリーズ モデルのクエリ例](time-series-model-query-examples.md)|  
    |[ロジスティック回帰モデルのクエリ例](logistic-regression-model-query-examples.md)||  
  
     また、VBA 関数を呼び出したり、独自の関数を作成したりすることもできます。 詳細については、「[関数 &#40;DMX&#41;](/sql/dmx/functions-dmx)」を参照してください。  
  
-   **一般的な統計情報:** ほとんどのモデルの種類で使用できる標準偏差などのわかりやすい統計情報の標準セットを返す関数を数多くあります。  
  
     たとえば、`PredictHistogram` 関数は、指定した列のすべての状態を含むテーブルを返します。  
  
     詳細については、「[一般的な予測関数 &#40;DMX&#41;](/sql/dmx/general-prediction-functions-dmx)」を参照してください。  
  
-   **カスタムの統計情報:** 特定の分析タスクに関連する統計を生成する各モデルの種類の追加のサポート機能が提供されます。  
  
     たとえば、クラスタリング モデルを使用する場合は、特定のケースとクラスターに関連する可能性スコアを返す、関数 `PredictCaseLikelihood` を使用できます。 ただし、線形回帰モデルを作成した場合は、係数と切片を取得することが必要になります。これは、コンテンツ クエリを使用すると実行できます。  
  
-   **モデル コンテンツ関数:** *コンテンツ*のすべてのモデルは、単純なクエリで情報を取得することができます、標準化された形式で表されます。 DMX を使用して、モデル コンテンツに対するクエリを作成します。 一部のモデル コンテンツは、データ マイニング スキーマ行セットを使用して取得することもできます。  
  
     モデル コンテンツでは、返されるテーブルの各行またはノードの意味は、モデルのビルドに使用されたアルゴリズムの種類と列のデータ型によって異なります。 詳細については、「[コンテンツ クエリ &#40;データ マイニング&#41;](content-queries-data-mining.md)」を参照してください。  
  
##  <a name="bkmk_Reqs"></a> 必要条件  
 モデルに対するクエリを作成する前に、データ マイニング モデルを処理する必要があります。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] オブジェクトの処理には特別な権限が必要です。 マイニング モデルの処理の詳細については、「[処理の要件および注意事項 &#40;データ マイニング&#41;](processing-requirements-and-considerations-data-mining.md)」を参照してください。  
  
 データ マイニング モデルに対するクエリを実行するには、実行するクエリの種類により、異なるレベルの権限が必要になります。 たとえば、通常、ケースや構造データのドリルスルーでは、マイニング構造オブジェクトまたはマイニング モデル オブジェクトに対して設定された別の権限が必要になります。  
  
 ただし、クエリが外部データを使用し、OPENROWSET や OPENQUERY などのステートメントが含まれる場合には、クエリ対象のデータベースではそれらのステートメントを有効にする必要があります。また、基になるデータベース オブジェクトに対する権限も必要です。  
  
 データ マイニング クエリを実行するために必要なセキュリティ コンテキストの詳細については、「[セキュリティの概要 &#40;データ マイニング&#41;](security-overview-data-mining.md)」を参照してください。  
  
## <a name="in-this-section"></a>このセクションの内容  
 ここでは、各種のデータ マイニング クエリについて詳しく説明し、データ マイニング モデルに対してクエリを作成する詳しい例へのリンクを示します。  
  
 [予測クエリ &#40;データ マイニング&#41;](prediction-queries-data-mining.md)  
  
 [コンテンツ クエリ &#40;データ マイニング&#41;](content-queries-data-mining.md)  
  
 [ドリルスルー クエリ &#40;データ マイニング&#41;](drillthrough-queries-data-mining.md)  
  
 [データ定義クエリ &#40;データ マイニング&#41;](data-definition-queries-data-mining.md)  
  
 [データ マイニング クエリ インターフェイス](data-mining-query-tools.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 データ マイニング クエリを作成および操作する方法の詳細については、次のリンクを使用してください。  
  
|処理手順|リンク|  
|-----------|-----------|  
|データ マイニング クエリのチュートリアルの表示|[レッスン 6:予測の作成と操作&#40;基本的なデータ マイニング チュートリアル&#41;](../../tutorials/lesson-6-creating-and-working-with-predictions-basic-data-mining-tutorial.md)<br /><br /> [時系列予測の DMX のチュートリアル](../../tutorials/time-series-prediction-dmx-tutorial.md)|  
|SQL Server Management studio と [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]|[SQL Server Management Studio で DMX クエリを作成する](create-a-dmx-query-in-sql-server-management-studio.md)<br /><br /> [予測クエリ ビルダーを使用した予測クエリの作成](create-a-prediction-query-using-the-prediction-query-builder.md)<br /><br /> [モデルへの予測関数の適用](apply-prediction-functions-to-a-model.md)<br /><br /> [手動での予測クエリの編集](manually-edit-a-prediction-query.md)|  
|予測クエリで使用される外部データの操作|[予測クエリの入力データの選択およびマップ](choose-and-map-input-data-for-a-prediction-query.md)<br /><br /> [予測クエリの入力データの選択およびマップ](choose-and-map-input-data-for-a-prediction-query.md)|  
|クエリ結果の操作|[予測クエリの結果の表示および保存](view-and-save-the-results-of-a-prediction-query.md)|  
|Management Studio の DMX クエリ テンプレートと XMLA クエリ テンプレートの使用|[テンプレートからの単一予測クエリの作成](create-a-singleton-prediction-query-from-a-template.md)<br /><br /> [XMLA を使用したデータ マイニング クエリの作成](create-a-data-mining-query-by-using-xmla.md)<br /><br /> [SQL Server Management Studio での Analysis Services テンプレートの使用](../instances/use-analysis-services-templates-in-sql-server-management-studio.md)|  
|コンテンツ クエリの詳細の説明と例の参照|[マイニング モデルのコンテンツ クエリの作成](create-a-content-query-on-a-mining-model.md)<br /><br /> [マイニング モデルの作成に使用されたパラメーターのクエリ](query-the-parameters-used-to-create-a-mining-model.md)<br /><br /> [コンテンツ クエリ &#40;データ マイニング&#41;](content-queries-data-mining.md)|  
|クエリ オプションの設定およびクエリの権限と問題のトラブルシューティング|[データ マイニング クエリのタイムアウト値の変更](data-mining-queries.md)|  
|Integration Services のデータ マイニング コンポーネントの使用|[Data Mining Query Task](../../integration-services/control-flow/data-mining-query-task.md)<br /><br /> [Data Mining Query Transformation](../../integration-services/data-flow/transformations/data-mining-query-transformation.md)|  
  
## <a name="see-also"></a>参照  
 [データ マイニング アルゴリズム &#40;Analysis Services - データ マイニング&#41;](data-mining-algorithms-analysis-services-data-mining.md)   
 [マイニング モデル コンテンツ &#40;Analysis Services - データ マイニング&#41;](mining-model-content-analysis-services-data-mining.md)  
  
  
