---
title: データ マイニング モデルの作成 |Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data mining models, creating
- forecasting [data mining]
- mining models, creating
- clustering [data mining]
- association [data mining]
- data modeling [data mining]
- estimation
- classification [data mining]
ms.assetid: 804b7db3-1f6a-4f73-a81d-bbe02520d7c6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1a8893960b5177563ccf98dbd21cb528ce399ea3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66086727"
---
# <a name="creating-a-data-mining-model"></a>データ マイニング モデルの作成
  データ モデリングは、適用することでパターンや傾向を作成する場所のデータ マイニング手順*アルゴリズム*データにします。 その後、それらのデータを使って追加の分析を行ったり、予測を立てたりすることができます。  
  
 Office 用データ マイニング アドインは、ウィザードによるデータ マイニングをサポートすることで、モデルの作成を簡素化しています。 ウィザードでは、データの分析、相関関係の特定、あらゆる変数の統計的有意性の計算、最適なモデルの自動選択が実行されます。  
  
 この機能は、強力でデータ マイニング ツールによって提供されるすべてのビットが[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]と[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]ウィザードと、使い慣れた Excel のインターフェイスの組み合わせにより、簡単に作成、変更、およびデータ マイニングを使用できます。  
  
## <a name="advanced-data-mining"></a>詳細設定 (データ マイニング)  
 高度なウィザードでは、データ マイニング アルゴリズムのいずれかを使用して Excel では、格納されたデータに基づいて、新しいデータ マイニング モデルを作成できます。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]します。  
  
### <a name="create-mining-structure"></a>マイニング構造の作成  
 マイニング構造の作成ウィザードを使用すると、新しいデータ マイニング構造を構築し、複数のマイニング モデルの基礎として使用できます。 このウィザードには、テスト セットとして使用するデータの一部を確保するオプションが用意されているので、一貫したテスト標準に従って同じデータを使用するすべてのモデルを評価できます。  
  
 [マイニング構造の作成&#40;SQL Server データ マイニング アドイン&#41;](create-mining-structure-sql-server-data-mining-add-ins.md)  
  
### <a name="add-model-to-structure"></a>構造へのモデルの追加  
 構造へのモデルの追加ウィザードを使用すると、既存のデータ マイニング構造を選択して、その構造に使用する新しいデータ マイニング モデルを作成できます。 複数のマイニング モデルを構造に追加し、パラメーターを変更するか、別のデータ マイニング アルゴリズムを選択して、出力をカスタマイズできます。  
  
 [モデルを構造に追加&#40;データ マイニング Excel 用アドイン&#41;](add-model-to-structure-data-mining-add-ins-for-excel.md)  
  
## <a name="analyze-key-influencers-analyze"></a>主要な影響元の分析 (分析)  
 目的の列または出力値を選択すると、アルゴリズムがすべての入力データを分析して、対象に最大の影響を与えている要因を特定します。 必要に応じて、2 つの値を比較するレポートを作成できます。これにより、影響元がどのように変化するかを確認できます。  
  
 **分析の主要な影響元**ツールは、Microsoft 単純ベイズ アルゴリズムを使用します。  
  
 [主要な影響元の分析&#40;Excel 用テーブル分析ツール&#41;](analyze-key-influencers-table-analysis-tools-for-excel.md)  
  
## <a name="associate-data-mining"></a>アソシエーション (データ マイニング)  
 **関連付ける**ウィザードは、複数のトランザクションに表示される項目間のアソシエーションを検出するアソシエーション モデルを構築: たとえば、マーケット バスケット分析にします。  
  
 [アソシエーション ウィザード&#40;Excel 用データ マイニング クライアント&#41;](associate-wizard-data-mining-client-for-excel.md)  
  
## <a name="classify-data-mining"></a>分類 (データ マイニング)  
 **分類**ウィザードは、対象となる結果をもたらした要因を分析する分類モデルを構築します。 このウィザードでは、デシジョン ツリー、Naïve Bayes、ニューラル ネットワークを含む複数のアルゴリズムを使用できます。  
  
 [分類ウィザード&#40;データ マイニング Excel 用アドイン&#41;](classify-wizard-data-mining-add-ins-for-excel.md)  
  
## <a name="cluster-data-mining"></a>クラスター (データ マイニング)  
 **クラスター**ウィザードは、類似した特性を共有する行のグループを検出するクラスター モデルを構築します。 クラスタ リング (とも呼ばれる*セグメンテーション*) はパターンや新しいデータのグループを理解する際に非常に便利ですが、教師なし学習手法です。  
  
 Microsoft クラスタリング アルゴリズムは、K-Means および Expectation Maximization (EM) クラスタリング両方について、複数の種類をサポートします。  
  
 [クラスター ウィザード&#40;データ マイニング アドインを Excel の&#41;](cluster-wizard-data-mining-add-ins-for-excel.md)します。  
  
## <a name="detect-categories-analyze"></a>カテゴリの検出 (分析)  
 **カテゴリの検出**ツールでは、任意のデータ セットを追加し、データのグループを検索するクラスタ リングを適用することができます。 類似点を検索するため、さらに分析するグループを作成するために便利です。  
  
 **カテゴリの検出**ツールは、Microsoft クラスタ リング アルゴリズムを使用します。  
  
 [カテゴリの検出&#40;Excel 用テーブル分析ツール&#41;](detect-categories-table-analysis-tools-for-excel.md)  
  
## <a name="estimate-data-mining"></a>推定 (データ マイニング)  
 推定ウィザードを使用すると、データのパターンを抽出し、そのパターンを基に、連続する数値、日付、または時刻の値を予測する推定モデルを構築できます。 [!INCLUDE[msCoName](../includes/msconame-md.md)] のデシジョン ツリー アルゴリズムが使用されます。  
  
 [推定ウィザード&#40;データ マイニング Excel 用アドイン&#41;](estimate-wizard-data-mining-add-ins-for-excel.md)  
  
## <a name="fill-from-example-analyze"></a>自動推論 (分析)  
 **推論**ツールを使用して、欠損値を補完できます。 不足値の例をいくつか指定すると、このツールはテーブル内のすべてのデータに基づいてパターンを作成し、データのパターンに基づいて新しい値を推奨します。  
  
 **推論**ツールは、Microsoft ロジスティック回帰アルゴリズムを使用します。  
  
 [自動推論&#40;Excel 用テーブル分析ツール&#41;](fill-from-example-table-analysis-tools-for-excel.md)  
  
## <a name="forecast-analyze"></a>予測 (分析)  
 **予測**ツールは、時間の経過と共に変更し、将来の値を予測するデータを取得します。  
  
 **予測**ツールは、Microsoft タイム シリーズ アルゴリズムを使用します。  
  
 [予測&#40;Excel 用テーブル分析ツール&#41;](forecast-table-analysis-tools-for-excel.md)  
  
## <a name="forecast-data-mining"></a>予測 (データ マイニング)  
 **予測**ウィザードは、一連のセルのパターンを検出し、追加の値を予測する予測モデルを構築します。  
  
 [予測ウィザード&#40;データ マイニング Excel 用アドイン&#41;](forecast-wizard-data-mining-add-ins-for-excel.md)  
  
## <a name="highlight-exceptions-analyze"></a>例外の強調表示 (分析)  
 **例外の強調表示**ツールは、テーブルのデータのパターンを分析し、行と、パターンに一致しない値を検索します。 ユーザーは、これらの値を確認し、修正してモデルを再実行することも、後で処理するためにこれらの値にフラグを設定することもできます。  
  
 **例外の強調表示**ツールは、Microsoft クラスタ リング アルゴリズムを使用します。  
  
 [例外の強調表示&#40;Excel 用テーブル分析ツール&#41;](highlight-exceptions-table-analysis-tools-for-excel.md)  
  
## <a name="prediction-calculator-analyze"></a>予測計算ツール (分析)  
 このツールは、目標の結果の達成につながる要因を分析し、これらのパターンから派生した基準に基づいて新しい入力の結果を予測するモデルを作成します。また、新しい入力を簡単にスコアするために役立つ対話形式の意思決定ワークシートを生成します。 ユーザーは、オフラインで使用できるスコアリング ワークシートの印刷バージョンを作成することもできます。  
  
 **予測計算**ツールは、Microsoft ロジスティック回帰アルゴリズムを使用します。  
  
 [予測計算&#40;Excel 用テーブル分析ツール&#41;](prediction-calculator-table-analysis-tools-for-excel.md)  
  
## <a name="scenario-goal-seek-analyze"></a>シナリオ:ゴール シーク (分析)  
 **ゴール シーク**ターゲット値、およびツールをそのターゲットを満たすために変更する必要がありますのある基になる要因を識別します。 を指定するツール。 たとえば、電話対応満足度を 20% 向上させる必要がある場合、その目標を達成するために変更する必要のある要因を予測するようモデルに要求できます。  
  
 **ゴール シーク**ツールは、Microsoft ロジスティック回帰アルゴリズムを使用します。  
  
 詳細情報  
  
 [ゴール シーク シナリオ&#40;Excel 用テーブル分析ツール&#41;](goal-seek-scenario-table-analysis-tools-for-excel.md)  
  
## <a name="scenario-what-if-scenario-analyze"></a>シナリオ:What-if シナリオ (分析)  
 **What-If 分析**ツールを補完、**ゴール シーク**ツール。 このツールで変更する必要のある値を入力すると、モデルはその変更が目標の結果を達成するために十分であるかどうかを予測します。 たとえば、電話オペレーターを 1 人追加することによって顧客満足度が 1 ポイント向上するかどうかを推測するようモデルに要求できます。  
  
 **What-if**ツールは、Microsoft ロジスティック回帰アルゴリズムを使用します。  
  
 [What If シナリオ&#40;Excel 用テーブル分析ツール&#41;](what-if-scenario-table-analysis-tools-for-excel.md)  
  
## <a name="shopping-basket-analysis-analyze"></a>買い物かご分析 (分析)  
 **買い物かご分析**ツールは、アップセル、またはクロスセルで使用できるパターンを識別するために一緒に購入される頻度が製品のグループを作成します。 また、意思決定の際に役立つ、関連する製品バンドルの価格とコストに基づくレポートを生成します。  
  
 このツールは、頻繁に同時発生するイベント、診断につながる要因、またはその他の考えられる原因と結果のセットを特定するために使用することもできます。  
  
 **買い物かご分析**ツールは、Microsoft アソシエーション アルゴリズムを使用します。  
  
 [買い物かご分析&#40;Excel 用のテーブル分析ツール&#41;](shopping-basket-analysis-table-analysistools-for-excel.md)  
  
## <a name="see-also"></a>参照  
 [探索とデータのクリーニング](exploring-and-cleaning-data.md)   
 [モデルの検証と予測用モデルの使用&#40;データ マイニング Excel 用アドイン&#41;](validating-models-and-using-models-for-prediction-data-mining-add-ins-for-excel.md)   
 [展開して、マイニング モデルのスケーリング&#40;データ マイニング Excel 用アドイン&#41;](deploying-and-scaling-mining-models-data-mining-add-ins-for-excel.md)  
  
  
