---
title: Microsoft 線形回帰アルゴリズム テクニカル リファレンス |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- AUTO_DETECT_PERIODICITY parameter
- linear regression algorithms [Analysis Services]
- regression algorithms [Analysis Services]
ms.assetid: 7807b5ff-8e0d-418d-a05b-b1a9644536d2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: db8b36fbccc4139071f54ddf9f73f876e9517799
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66084056"
---
# <a name="microsoft-linear-regression-algorithm-technical-reference"></a>Microsoft 線形回帰アルゴリズム テクニカル リファレンス
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] 線形回帰アルゴリズムは、連続属性のペアのモデリングに最適化された、特殊な Microsoft デシジョン ツリー アルゴリズムです。 このトピックでは、アルゴリズムの実装について説明し、アルゴリズムの動作をカスタマイズする方法を示します。モデルのクエリに関する追加情報へのリンクも示します。  
  
## <a name="implementation-of-the-linear-regression-algorithm"></a>線形回帰アルゴリズムの実装  
 Microsoft デシジョン ツリー アルゴリズムは、線形回帰、分類、またはアソシエーション分析など多くのタスクで使用できます。 線形回帰のためにこのアルゴリズムを実装するには、ツリーの拡張を制限するようにアルゴリズムのパラメーターを制御し、モデル内のすべてのデータを単一のノード内に保持します。 つまり、線形回帰はデシジョン ツリーに基づいていますが、ツリーに含まれるのは単一のルートのみで、分岐は含まれません。すべてのデータがルート ノード内に存在します。  
  
 これを実現するには、アルゴリズムの *MINIMUM_LEAF_CASES* パラメーターを、マイニング モデルのトレーニング時にアルゴリズムで使用されるケースの総数以上に設定します。 このようにパラメーターを設定することにより、アルゴリズムで分割が作成されず、線形回帰が実行されます。  
  
 回帰直線を表す式は、回帰式と呼ばれる y = ax + b という一般的な形式になります。 変数 Y は出力変数を表し、変数 X は入力変数を表します。a と b は調整可能な係数です。 完成したマイニング モデルのクエリを実行して、係数、切片、および回帰式に関するその他の情報を取得することができます。 詳細については、「 [線形回帰モデルのクエリ例](linear-regression-model-query-examples.md)」を参照してください。  
  
### <a name="scoring-methods-and-feature-selection"></a>スコアリング方法と機能の選択  
 すべての [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データ マイニング アルゴリズムでは、分析の向上と処理負荷の削減のため、機能の選択が自動的に使用されます。 モデルでサポートされるのは連続列だけであるため、線形回帰の機能選択に使用される方法は興味深さのスコアです。 参考のため、次の表に線形回帰アルゴリズムとデシジョン ツリー アルゴリズムの機能選択の違いを示します。  
  
|アルゴリズム|分析の方法|コメント|  
|---------------|------------------------|--------------|  
|線形回帰|興味深さのスコア|既定値です。<br /><br /> デシジョン ツリー アルゴリズムで使用できるその他の機能選択の方法は、離散変数のみに適用されるため、線形回帰モデルには適用できません。|  
|デシジョン ツリー|興味深さのスコア<br /><br /> Shannon のエントロピー<br /><br /> K2 事前分布を指定したベイズ定理<br /><br /> 均一な事前分布を指定したベイズ ディリクレ等式 (既定値)|非バイナリの連続する値を含む列がある場合は、一貫性を保つため、すべての列に対して興味深さのスコアが使用されます。 それ以外の場合は、既定の方法か、指定した方法が使用されます。|  
  
 デシジョン ツリー モデルに対する機能の選択を制御するアルゴリズム パラメーターは、MAXIMUM_INPUT_ATTRIBUTES と MAXIMUM_OUTPUT です。  
  
## <a name="customizing-the-linear-regression-algorithm"></a>線形回帰アルゴリズムのカスタマイズ  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 線形回帰アルゴリズムでは、結果として得られるマイニング モデルの動作、パフォーマンス、および精度に影響を与えるパラメーターがサポートされています。 マイニング モデル列またはマイニング構造列にモデリング フラグを設定して、データの処理方法を制御することもできます。  
  
### <a name="setting-algorithm-parameters"></a>アルゴリズム パラメーターの設定  
 次の表に、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 線形回帰アルゴリズムで提供されるパラメーターを示します。  
  
|パラメーター|説明|  
|---------------|-----------------|  
|*MAXIMUM_INPUT_ATTRIBUTES*|選択した機能を呼び出す前にアルゴリズムが処理できる入力属性の数を定義します。 この値を 0 に設定すると、機能の選択がオフになります。<br /><br /> 既定値は 255 です。|  
|*MAXIMUM_OUTPUT_ATTRIBUTES*|選択した機能を呼び出す前にアルゴリズムが処理できる出力属性の数を定義します。 この値を 0 に設定すると、機能の選択がオフになります。<br /><br /> 既定値は 255 です。|  
|*FORCE_REGRESSOR*|アルゴリズムによって計算された列の重要度に関係なく、指定した列をアルゴリズムでリグレッサーとして使用するように設定します。|  
  
### <a name="modeling-flags"></a>ModelingFlags  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 線形回帰アルゴリズムでは、次のモデリング フラグがサポートされています。 モデリング フラグは、マイニング構造やマイニング モデルを作成するときに定義し、分析時に各列の値をどのように処理するかを指定します。 詳細については、「[モデリング フラグ &#40;データ マイニング&#41;](modeling-flags-data-mining.md)」を参照してください。  
  
|モデリング フラグ|説明|  
|-------------------|-----------------|  
|NOT NULL|列に NULL を含めることはできないことを示します。 モデルのトレーニング中に NULL が検出された場合はエラーが発生します。<br /><br /> マイニング構造列に適用されます。|  
|REGRESSOR|列には、分析中に潜在的な独立変数として扱われる連続する数値が含まれることを示します。<br /><br /> 注:列がリグレッサーとしてフラグを設定しても、列が、最終的なモデルでリグレッサーとして使用されることとは限りません。<br /><br /> マイニング モデル列に適用されます。|  
  
### <a name="regressors-in-linear-regression-models"></a>線形回帰モデルのリグレッサー  
 線形回帰モデルは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] デシジョン ツリー アルゴリズムに基づいています。 ただし、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 線形回帰アルゴリズムを使用していない場合でも、連続属性の回帰を表すツリーやノードがデシジョン ツリー モデルに含まれることはあります。  
  
 連続列がリグレッサーを表すことを指定する必要はありません。 列に REGRESSOR フラグを設定しなくても、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] デシジョン ツリー アルゴリズムにより、データセットが意味のあるパターンを持つ領域に分割されます。 その違いは、このモデリング フラグを設定すると、アルゴリズムを検索しようという形式の回帰式を * C1 + b\*C2 +… で、ツリーのノードのパターンに合わせてします。 残差の合計が計算され、偏差が大きすぎる場合には、ツリーが強制的に分割されます。  
  
 たとえば、 **Income** を属性として使用して顧客の購入行動を予測する場合に、その列に REGRESSOR モデリング フラグを設定すると、アルゴリズムはまず、標準の回帰式を使用して **Income** の値を試します。 偏差が大きすぎる場合はその回帰式が放棄され、ツリーが他の属性で分割されます。 その後、デシジョン ツリー アルゴリズムは、分割後の各分岐で Income をリグレッサーとして使用できるかどうかを試します。  
  
 FORCED_REGRESSOR パラメーターを使用すると、アルゴリズムで特定のリグレッサーが使用されるようにすることができます。 このパラメーターは、Microsoft デシジョン ツリー アルゴリズムと Microsoft 線形回帰アルゴリズムで使用できます。  
  
## <a name="requirements"></a>必要条件  
 線形回帰モデルには、キー列、入力列、および少なくとも 1 つの予測可能列が必要です。  
  
### <a name="input-and-predictable-columns"></a>入力列と予測可能列  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 線形回帰アルゴリズムでは、次の表に示す特定の入力列と予測可能列がサポートされています。 マイニング モデルにおけるコンテンツの種類の意味については、「[コンテンツの種類 &#40;データ マイニング&#41;](content-types-data-mining.md)」を参照してください。  
  
|[列]|コンテンツの種類|  
|------------|-------------------|  
|入力属性|Continuous、Cyclical、Key、Table、Ordered|  
|予測可能な属性|Continuous、Cyclical、Ordered|  
  
> [!NOTE]  
>  コンテンツの種類 `Cyclical` および `Ordered` はサポートされますが、アルゴリズムはこれらを不連続の値として扱い、特別な処理は行いません。  
  
## <a name="see-also"></a>関連項目  
 [Microsoft 線形回帰アルゴリズム](microsoft-linear-regression-algorithm.md)   
 [線形回帰モデルのクエリ例](linear-regression-model-query-examples.md)   
 [線形回帰モデルのマイニング モデル コンテンツ (Analysis Services - データ マイニング)](mining-model-content-for-linear-regression-models-analysis-services-data-mining.md)  
  
  
