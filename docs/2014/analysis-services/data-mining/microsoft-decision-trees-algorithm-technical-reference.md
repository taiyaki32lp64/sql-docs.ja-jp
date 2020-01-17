---
title: Microsoft デシジョンツリーアルゴリズムテクニカルリファレンス |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- MAXIMUM_INPUT_ATTRIBUTES parameter
- SPLIT_METHOD parameter
- MINIMUM_SUPPORT parameter
- MAXIMUM_OUTPUT_ATTRIBUTES parameter
- FORCED_REGRESSOR parameter
- decision tree algorithms [Analysis Services]
- decision trees [Analysis Services]
- COMPLEXITY_PENALTY parameter
- SCORE_METHOD parameter
ms.assetid: 1e9f7969-0aa6-465a-b3ea-57b8d1c7a1fd
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 304cd31b4d89d56bee5dbc903c784ee4bf7af5fe
ms.sourcegitcommit: baa40306cada09e480b4c5ddb44ee8524307a2ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/06/2019
ms.locfileid: "73637528"
---
# <a name="microsoft-decision-trees-algorithm-technical-reference"></a>Microsoft デシジョン ツリー アルゴリズム テクニカル リファレンス
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] デシジョン ツリー アルゴリズムは、さまざまなツリー作成手法が組み込まれた複合アルゴリズムであり、回帰、分類、アソシエーションなど、複数の分析タスクをサポートしています。 Microsoft デシジョン ツリー アルゴリズムは、不連続属性と連続属性の両方のモデリングをサポートしています。  
  
 このトピックでは、アルゴリズムの実装について説明し、さまざまなタスクに合わせてアルゴリズムの動作をカスタマイズする方法を示します。また、デシジョン ツリー モデルに対するクエリに関する追加情報へのリンクも示します。  
  
## <a name="implementation-of-the-decision-trees-algorithm"></a>デシジョン ツリー アルゴリズムの実装  
 Microsoft デシジョン ツリー アルゴリズムは、モデルの近似的事後分布を取得して、因果的相互作用のモデルの学習にベイジアン アプローチを適用します。 このアプローチの詳細な説明については、Microsoft Research サイトにある [構造とパラメーターの学習](https://go.microsoft.com/fwlink/?LinkId=237640&clcid=0x409)に関する論文を参照してください。  
  
 学習に必要な *事前分布* 情報の価値を評価する手法は、 *尤度等価*の想定に基づいています。 この想定では、条件的に独立した同じアサーションのネットワーク構造は、データでは識別できないものと見なします。 各ケースには、ベイジアン事前分布ネットワークと、そのネットワークの信頼メジャーが、それぞれ 1 つずつあるものと見なされます。  
  
 アルゴリズムでは、これらの事前分布ネットワークを使用して、現在のトレーニング データからネットワーク構造の相対的な *事後確率* を計算し、事後確率が最も高いネットワーク構造を特定します。  
  
 Microsoft デシジョン ツリー アルゴリズムでは、さまざまな方法を使用して最適なツリーを計算します。 使用される方法はタスクによって異なり、線形回帰、分類、またはアソシエーション分析があります。 個々のモデルには、各種の予測可能な属性に応じて複数のツリーが含まれる可能性があります。 さらに、データ内の属性と値の数に応じて、各ツリーに複数の分岐が含まれる可能性があります。 特定のモデル内に作成されるツリーの形状と深さは、スコアリング方法と、使用された他のパラメーターによって決まります。 パラメーターの変更も、ノードの分割場所に影響する可能性があります。  
  
### <a name="building-the-tree"></a>ツリーの作成  
 Microsoft デシジョン ツリー アルゴリズムは、使用可能な入力値のセットを作成すると *機能の選択* を実行して最も多くの情報を提供する属性と値を特定し、頻度の低い値を考慮対象からはずします。 また、このアルゴリズムは、パフォーマンスを最適化するため、値を *ビン*にグループ化し、まとめて処理できる値のグループを作成します。  
  
 ツリーは、入力と対象の結果との間の相関関係を調べることによって作成されます。 すべての属性が関連付けられた後、結果を最も明確に区分する 1 つの属性がアルゴリズムによって識別されます。 この最良の区分点は、情報利得を計算する式を使用して測定されます。 情報利得のスコアが最も高い属性によってケースがサブセットに分割され、次にそのサブセットが同じプロセスで再帰的に分析され、ツリーを分割できなくなるまで繰り返されます。  
  
 情報利得の評価に使用される正確な式は、アルゴリズムの作成時に設定したパラメーター、予測可能列のデータ型、および入力のデータ型によって異なります。  
  
### <a name="discrete-and-continuous-inputs"></a>不連続および連続の入力  
 予測可能属性および入力が不連続の場合、入力あたりの結果をカウントするには、マトリックスを作成し、マトリックスの各セルのスコアを生成します。  
  
 ただし、予測可能属性が不連続で入力が連続の場合、連続列の入力が自動的に分離されます。 既定の動作を受け入れると、最適なビン数を [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] で検出できます。また、 <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationMethod%2A> プロパティと <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationBucketCount%2A> プロパティを設定して、連続する入力の分離方法を制御することもできます。 詳細については、「 [マイニング モデルでの列の分離の変更](change-the-discretization-of-a-column-in-a-mining-model.md)」を参照してください。  
  
 連続属性の場合、アルゴリズムでは線型回帰を使用して、デシジョン ツリーの分割ポイントが判断されます。  
  
 予測可能属性が連続する数値データ型の場合、結果数をできるだけ減らしてモデルの作成を高速化するために、機能の選択が出力にも適用されます。 MAXIMUM_OUTPUT_ATTRIBUTES パラメーターを設定することにより、機能の選択のしきい値を変更して、使用可能な値の数を増減できます。  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] デシジョン ツリー アルゴリズムが、不連続の予測可能列をどのように処理するかについては、「 [ベイジアン ネットワークの学習 : 知識と統計データの組み合わせ](https://go.microsoft.com/fwlink/?LinkId=45963)」を参照してください。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] デシジョン ツリー アルゴリズムが、連続する予測可能列をどのように処理するかについては、「 [時系列分析の自動回帰ツリー モデル](https://go.microsoft.com/fwlink/?LinkId=45966)」の付録を参照してください。  
  
### <a name="scoring-methods-and-feature-selection"></a>スコアリング方法と機能の選択  
 Microsoft デシジョン ツリー アルゴリズムには、情報利得のスコアを計算する式が 3 つ用意されています。Shannon のエントロピー、K2 事前分布を指定したベイジアン ネットワーク、および均一なディリクレ事前分布を指定したベイジアン ネットワークです。 データ マイニング フィールドには、3 つの方法すべてが準備されています。 最適な結果を得るには、複数のパラメーターとスコアリング方法を試してみることをお勧めします。 これらのスコアリング方法の詳細については、「 [機能の選択](../../sql-server/install/feature-selection.md)」を参照してください。  
  
 すべての [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データ マイニング アルゴリズムでは、分析の向上と処理負荷の削減のため、機能の選択が自動的に使用されます。 機能の選択に使用される方法は、モデルの作成に使用したアルゴリズムによって異なります。 デシジョン ツリー モデルに対する機能の選択を制御するアルゴリズム パラメーターは、MAXIMUM_INPUT_ATTRIBUTES と MAXIMUM_OUTPUT です。  
  
|アルゴリズム|分析の方法|コメント|  
|---------------|------------------------|--------------|  
|デシジョン ツリー|興味深さのスコア<br /><br /> Shannon のエントロピー<br /><br /> K2 事前分布を指定したベイズ定理<br /><br /> 均一な事前分布を指定したベイズ ディリクレ等式 (既定値)|非バイナリの連続する値を含む列がある場合は、一貫性を保つため、すべての列に対して興味深さのスコアが使用されます。 それ以外の場合は、既定の方法か、指定した方法が使用されます。|  
|線形回帰|興味深さのスコア|線形回帰でサポートされるのは連続列だけであるため、興味深さのスコアのみが使用されます。|  
  
### <a name="scalability-and-performance"></a>スケーラビリティとパフォーマンス  
 分類は、重要なデータ マイニング戦略です。 一般に、ケースの分類に必要な情報量は、入力レコードの数に正比例して増加します。 このため、分類可能なデータのサイズが制限されます。 Microsoft デシジョン ツリー アルゴリズムでは次の方法を使用して、これらの問題を解決し、パフォーマンスを向上させ、メモリの制限を回避します。  
  
-   機能の選択で、属性の選択を最適化します。  
  
-   ベイジアン スコアリングで、ツリーの拡大を制御します。  
  
-   連続属性のビン分割を最適化します。  
  
-   入力値の動的なグループ化で、最も重要な値を特定します。  
  
 Microsoft デシジョン ツリー アルゴリズムは、高速かつスケーラブルで、簡単に並列処理できるよう設計されています。つまり、すべてのプロセッサが連携し、単一の一貫したモデルを作成します。 これらの特性を兼ね備えているため、デシジョン ツリー分類子はデータ マイニングに最適のツールです。  
  
 パフォーマンスの制約が大きい場合、次の方法を使用すると、デシジョン ツリー モデルのトレーニング中の処理時間を短縮できる場合があります。 ただし、このとき、処理パフォーマンスを向上させるために属性を削除すると、モデルの結果が変わり、母集団を正しく代表しなくなる可能性があります。  
  
-   ツリーの拡大を制限するには、COMPLEXITY_PENALTY パラメーターの値を大きくします。  
  
-   作成されるツリー数を制限するには、アソシエーション モデル内のアイテム数を制限します。  
  
-   オーバーフィットを回避するには、MINIMUM_SUPPORT パラメーターの値を大きくします。  
  
-   任意の属性に対する不連続値の数を、10 以下に制限します。 モデルに応じたさまざまな方法で、値のグループ化を試みることができます。  
  
    > [!NOTE]  
    >  [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] のデータ探索ツールを使用すると、データ マイニングの開始前に、データ内の値の分布を視覚化し、値を適切にグループ化することができます。 詳細については、「 [データ プロファイル タスクとビューアー](../../integration-services/control-flow/data-profiling-task-and-viewer.md)」を参照してください。 また、 [Excel 2007 用データ マイニング アドイン](https://www.microsoft.com/download/details.aspx?id=8569)を使用すると、データの探索、グループ化、およびラベル変更を Microsoft Excel で行うことができます。  
  
## <a name="customizing-the-decision-trees-algorithm"></a>デシジョン ツリー アルゴリズムのカスタマイズ  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] デシジョン ツリー アルゴリズムでは、結果として得られるマイニング モデルのパフォーマンスおよび精度に影響を与えるパラメーターがサポートされています。 マイニング モデル列またはマイニング構造列にモデリング フラグを設定して、データの処理方法を制御することもできます。  
  
> [!NOTE]  
>  Microsoft デシジョン ツリー アルゴリズムは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のすべてのエディションで利用できます。ただし、Microsoft デシジョン ツリー アルゴリズムの動作をカスタマイズするためのいくつかの高度なパラメーターは、特定のエディションの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]だけで使用できます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の各エディションでサポートされる機能の一覧については、「[SQL Server 2012 の各エディションがサポートする機能](https://go.microsoft.com/fwlink/?linkid=232473)」(https://go.microsoft.com/fwlink/?linkid=232473) を参照してください。  
  
### <a name="setting-algorithm-parameters"></a>アルゴリズム パラメーターの設定  
 次の表は、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] デシジョン ツリー アルゴリズムで使用できるパラメーターを示しています。  
  
 *COMPLEXITY_PENALTY*  
 デシジョン ツリーの拡大を制御します。 値を小さくすると分割数が増加し、値を大きくすると分割数が減少します。 次に示すように、既定値は特定のモデルの属性数に基づいて決定されます。  
  
-   属性数が 1 ～ 9 の場合、既定値は 0.5 です。  
  
-   属性数が 10 ～ 99 の場合、既定値は 0.9 です。  
  
-   属性数が 100 以上の場合、既定値は 0.99 です。  
  
 *FORCE_REGRESSOR*  
 アルゴリズムによって計算された列の重要性にかかわらず、指定した列をアルゴリズムでリグレッサーとして使用するように設定します。 このパラメーターは、連続属性を予測するデシジョン ツリーでのみ使用します。  
  
> [!NOTE]  
>  このパラメーターを設定すると、属性がアルゴリズムのリグレッサーとして使用されます。 ただし、最終的なモデルにおいて属性が実際にリグレッサーとして使用されるかどうかは、分析結果によって決まります。 リグレッサーとして使用された列を確認するには、モデル コンテンツに対するクエリを実行します。  
  
 [一部のエディションの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] だけで利用可能]  
  
 *MAXIMUM_INPUT_ATTRIBUTES*  
 選択した機能を呼び出す前にアルゴリズムが処理できる入力属性の数を定義します。  
  
 既定値は 255 です。  
  
 この値を 0 に設定すると、機能の選択がオフになります。  
  
 [一部のエディションの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]だけで利用可能]  
  
 *MAXIMUM_OUTPUT_ATTRIBUTES*  
 選択した機能を呼び出す前にアルゴリズムが処理できる出力属性の数を定義します。  
  
 既定値は 255 です。  
  
 この値を 0 に設定すると、機能の選択がオフになります。  
  
 [一部のエディションの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]だけで利用可能]  
  
 *MINIMUM_SUPPORT*  
 デシジョン ツリー内で分割を生成するために必要なリーフ ケースの最小数を決定します。  
  
 既定値は、10 です。  
  
 データセットが非常に大きい場合は、オーバートレーニングを回避するため、この値を大きくする必要が生じることがあります。  
  
 *SCORE_METHOD*  
 分割スコアを計算するために使用する方法を決定します。 使用できるオプションは以下のとおりです。  
  
|ID|[オブジェクト名]|  
|--------|----------|  
|@shouldalert|エントロピー|  
|3|K2 事前分布を指定したベイズ定理|  
|4|均一な事前分布を指定したベイズ ディリクレ等式 (BDE)<br /><br /> (既定値)。|  
  
 既定値は 4、または BDE です。  
  
 これらのスコアリング方法の詳細については、「 [機能の選択](../../sql-server/install/feature-selection.md)」を参照してください。  
  
 *SPLIT_METHOD*  
 ノードを分割するために使用する方法を決定します。 使用できるオプションは以下のとおりです。  
  
|ID|[オブジェクト名]|  
|--------|----------|  
|@shouldalert|**Binary:** 属性値の実際の数にかかわらず、ツリーが 2 つの分岐に分割されることを示します。|  
|2|**Complete:** 属性値と同じ数の分割をツリーに作成できることを示します。|  
|3|**Both:** バイナリ分割と完全分割のどちらを使用すると最適な結果が生成されるのかが、Analysis Services によって判断されることを示します。|  
  
 既定値は 3 です。  
  
### <a name="modeling-flags"></a>ModelingFlags  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] デシジョン ツリー アルゴリズムでは、次のモデリング フラグがサポートされています。 モデリング フラグは、マイニング構造やマイニング モデルを作成するときに定義し、分析時に各列の値をどのように処理するかを指定します。 詳細については、「[モデリング フラグ &#40;データ マイニング&#41;](modeling-flags-data-mining.md)」を参照してください。  
  
|モデリング フラグ|[説明]|  
|-------------------|-----------------|  
|MODEL_EXISTENCE_ONLY|列が、`Missing` および `Existing` の 2 つの可能な状態を持つ列として扱われることを示します。 NULL は Missing 値になります。<br /><br /> マイニング モデル列に適用されます。|  
|NOT NULL|列に NULL を含めることはできないことを示します。 モデルのトレーニング中に NULL が検出された場合はエラーが発生します。<br /><br /> マイニング構造列に適用されます。|  
  
### <a name="regressors-in-decision-tree-models"></a>デシジョン ツリー モデルのリグレッサー  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 線形回帰アルゴリズムを使用していない場合でも、連続属性の回帰を表すノードが、連続する数値の入出力を持つデシジョン ツリー モデルに含まれることがあります。  
  
 連続する数値データ列がリグレッサーを表すことを指定する必要はありません。 列に REGRESSOR フラグを設定しなくても、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] デシジョン ツリー アルゴリズムにより、列が自動的にリグレッサー候補として使用され、データセットが意味のあるパターンを持つ領域に分割されます。  
  
 しかし、FORCE_REGRESSOR パラメーターを使用すると、アルゴリズムで特定のリグレッサーが使用されるようにすることができます。 このパラメーターは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] デシジョン ツリー アルゴリズムと [!INCLUDE[msCoName](../../includes/msconame-md.md)] 線形回帰アルゴリズムでのみ使用できます。 モデリングフラグを設定すると、アルゴリズムによって、a * C1 + b\*C2 +... という形式の回帰式が検索されます。は、ツリーのノードのパターンに適合します。 残差の合計が計算され、偏差が大きすぎる場合には、ツリーが強制的に分割されます。  
  
 たとえば、 **Income** を属性として使用して顧客の購入行動を予測する場合に、その列に REGRESSOR モデリング フラグを設定すると、アルゴリズムはまず、標準の回帰式を使用して **Income** の値を試します。 偏差が大きすぎる場合はその回帰式が放棄され、ツリーが他の属性で分割されます。 その後デシジョン ツリー アルゴリズムは、分割後の各分岐で、Income をリグレッサーとして使用できるかどうかを試します。  
  
## <a name="requirements"></a>の要件  
 デシジョン ツリー モデルには、キー列、入力列、および少なくとも 1 つの予測可能列が必要です。  
  
### <a name="input-and-predictable-columns"></a>入力列と予測可能列  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] デシジョン ツリー アルゴリズムでは、次の表に示す特定の入力列と予測可能列がサポートされています。 マイニング モデルにおけるコンテンツの種類の意味については、「[コンテンツの種類 (データ マイニング)](content-types-data-mining.md)」を参照してください。  
  
|列|コンテンツの種類|  
|------------|-------------------|  
|入力属性|Continuous、Cyclical、Discrete、Discretized、Key、Ordered、Table|  
|予測可能な属性|Continuous、Cyclical、Discrete、Discretized、Ordered、Table|  
  
> [!NOTE]  
>  コンテンツの種類 Cyclical および Ordered はサポートされますが、アルゴリズムはこれらを不連続の値として扱い、特別な処理は行いません。  
  
## <a name="see-also"></a>参照  
 [Microsoft デシジョン ツリー アルゴリズム](microsoft-decision-trees-algorithm.md)   
 [デシジョン ツリー モデルのクエリ例](decision-trees-model-query-examples.md)   
 [デシジョン ツリー モデルのマイニング モデル コンテンツ (Analysis Services - データ マイニング)](mining-model-content-for-decision-tree-models-analysis-services-data-mining.md)  
  
  
