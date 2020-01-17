---
title: 線形回帰モデルのマイニング モデル コンテンツ (Analysis Services - データ マイニング) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- linear regression algorithms [Analysis Services]
- mining model content, linear regression models
- regression algorithms [Analysis Services]
ms.assetid: a6abcb75-524e-4e0a-a375-c10475ac0a9d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 933b56aaa6e364ce55cac8832fc577acc061d510
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66083638"
---
# <a name="mining-model-content-for-linear-regression-models-analysis-services---data-mining"></a>線形回帰モデルのマイニング モデル コンテンツ (Analysis Services - データ マイニング)
  このトピックでは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 線形回帰アルゴリズムを使用するモデルに固有のマイニング モデル コンテンツについて説明します。 すべての種類のモデルのマイニング モデル コンテンツの一般的な説明については、「 [マイニング モデル コンテンツ &#40;Analysis Services - データ マイニング&#41;](mining-model-content-analysis-services-data-mining.md)」(マイニング モデル コンテンツ (Analysis Services - データ マイニング)) を参照してください。  
  
## <a name="understanding-the-structure-of-a-linear-regression-model"></a>線形回帰モデルの構造について  
 線形回帰モデルの構造は非常に単純です。 各モデルは、モデルとそのメタデータを表す 1 つの親ノードと回帰ツリーのノード (NODE_TYPE = 25) 各予測可能な属性の回帰式を格納しています。  
  
 ![線形回帰モデルの構造](../media/modelcontentstructure-linreg.gif "線形回帰モデルの構造")  
  
 線形回帰モデルでは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] デシジョン ツリーと同じアルゴリズムが使用されますが、ツリーを制約するために使用されるパラメーターが異なっており、また連続属性のみが入力として受け入れられます。 ただし、線形回帰モデルは [!INCLUDE[msCoName](../../includes/msconame-md.md)] デシジョン ツリー アルゴリズムに基づいているため、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] デシジョン ツリー ビューアーで表示できます。 詳細については、「 [Microsoft ツリー ビューアーを使用したモデルの参照](browse-a-model-using-the-microsoft-tree-viewer.md)」を参照してください。  
  
 次のセクションでは、回帰式ノードの情報を解釈する方法について説明します。 この情報は、線形回帰モデルだけでなく、ツリーの一部に回帰を含むデシジョン ツリー モデルにも適用されます。  
  
## <a name="model-content-for-a-linear-regression-model"></a>線形回帰モデルのモデル コンテンツ  
 ここでは、マイニング モデル コンテンツの列のうち、線形回帰に関連する列についてのみ詳細と例を紹介します。  
  
 スキーマ行セットの汎用の列の詳細については、「 [マイニング モデル コンテンツ &#40;Analysis Services - データ マイニング&#41;](mining-model-content-analysis-services-data-mining.md)」(マイニング モデル コンテンツ (Analysis Services - データ マイニング)) を参照してください。  
  
 MODEL_CATALOG  
 モデルが格納されているデータベースの名前。  
  
 MODEL_NAME  
 モデルの名前。  
  
 ATTRIBUTE_NAME  
 **ルート ノード:** 空白  
  
 **回帰ノード:** 予測可能な属性の名前。  
  
 NODE_NAME  
 常に NODE_UNIQUE_NAME と同じです。  
  
 NODE_UNIQUE_NAME  
 モデル内のノードの一意の識別子。 この値は変更できません。  
  
 NODE_TYPE  
 線形回帰モデルでは次の種類のノードが出力されます。  
  
|ノードの種類の ID|型|説明|  
|------------------|----------|-----------------|  
|25|回帰ツリーのルート|入力変数と出力変数のリレーションシップを表す数式が含まれます。|  
  
 NODE_CAPTION  
 ノードに関連付けられたラベルまたはキャプション。 このプロパティは、主に表示を目的としています。  
  
 **ルート ノード:** 空白  
  
 **回帰ノード:** すべて。  
  
 CHILDREN_CARDINALITY  
 ノードの子の推定数。  
  
 **ルート ノード:** 回帰ノードの数を示します。 モデルの予測可能な属性ごとに 1 つの回帰ノードが作成されます。  
  
 **回帰ノード:** 常に 0 です。  
  
 PARENT_UNIQUE_NAME  
 ノードの親の一意な名前です。 ルート レベルのノードには NULL を返します。  
  
 NODE_DESCRIPTION  
 ノードの説明です。  
  
 **ルート ノード:** 空白  
  
 **回帰ノード:** すべて。  
  
 NODE_RULE  
 線形回帰モデルでは使用されません。  
  
 MARGINAL_RULE  
 線形回帰モデルでは使用されません。  
  
 NODE_PROBABILITY  
 このノードに関連付けられている確率。  
  
 **ルート ノード:** 0  
  
 **回帰ノード:** 1  
  
 MARGINAL_PROBABILITY  
 親ノードからノードに到達する確率です。  
  
 **ルート ノード:** 0  
  
 **回帰ノード:** 1  
  
 NODE_DISTRIBUTION  
 ノード内の値に関する統計情報を提供する、入れ子になったテーブル。  
  
 **ルート ノード:** 0  
  
 **回帰ノード:** 回帰式の作成に使用する要素を格納するテーブル。 回帰ノードには、次の値型が含まれます。  
  
|VALUETYPE|  
|---------------|  
|1 (Missing: 不足)|  
|3 (Continuous: 連続)|  
|7 (Coefficient: 係数)|  
|8 (Score Gain: スコア ゲイン)|  
|9 (Statistics: 統計)|  
|11 (Intercept: 切片)|  
  
 NODE_SUPPORT  
 このノードをサポートするケースの数。  
  
 **ルート ノード:** 0  
  
 **回帰ノード:** トレーニング ケースの数。  
  
 MSOLAP_MODEL_COLUMN  
 予測可能な属性の名前。  
  
 MSOLAP_NODE_SCORE  
 NODE_PROBABILITY と同じ。  
  
 MSOLAP_NODE_SHORT_CAPTION  
 表示目的で使用されるラベル。  
  
## <a name="remarks"></a>コメント  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 線形回帰アルゴリズムを使用してモデルを作成すると、データ マイニング エンジンにより、デシジョン ツリー モデルの特殊なインスタンスが作成され、1 つのノードにすべてのトレーニング データを格納するようにツリーを制約するパラメーターが設定されます。 連続する入力はすべて、リグレッサー候補としてフラグが付けられ、評価されます。ただし、リグレッサーとして最終的なモデルに保持されるのは、データに適合するリグレッサーだけです。 分析では、リグレッサーごとに 1 つの回帰式が生成されるか、回帰式がまったく生成されないかのいずれかです。  
  
 **Microsoft ツリー ビューアー**で **[(すべて)]** ノードをクリックすると、完全な回帰式が [[マイニング凡例]](browse-a-model-using-the-microsoft-tree-viewer.md)に表示されます。  
  
 また、連続する予測可能な属性を含むデシジョン ツリー モデルを作成した場合、回帰ツリー ノードのプロパティを共有する回帰ノードがツリーに含まれることがあります。  
  
##  <a name="NodeDist_Regression"></a> 連続属性のノード分布  
 回帰ノードの重要な情報の大部分は、NODE_DISTRIBUTION テーブルに格納されます。 次の例は、NODE_DISTRIBUTION  テーブルのレイアウトを示しています。 この例では、Targeted Mailing マイニング構造を使用して、年齢に基づいて顧客の収入を予測する線形回帰モデルを作成します。 このモデルは単に説明をわかりやすくするためのものであり、 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] の既存のサンプル データとマイニング構造を使用して簡単に作成できます。  
  
|ATTRIBUTE_NAME|ATTRIBUTE_VALUE|SUPPORT|PROBABILITY|VARIANCE|VALUETYPE|  
|---------------------|----------------------|-------------|-----------------|--------------|---------------|  
|Yearly Income|Missing|0|0.000457142857142857|0|1|  
|Yearly Income|57220.8876687257|17484|0.999542857142857|1041275619.52776|3|  
|Age|471.687717702463|0|0|126.969442359327|7|  
|Age|234.680904692439|0|0|0|8|  
|Age|45.4269617936399|0|0|126.969442359327|9|  
||35793.5477381267|0|0|1012968919.28372|11|  
  
 NODE_DISTRIBUTION テーブルには複数の行が格納されており、各行は変数でグループ化されています。 最初の 2 行は、値型が常に 1 と 3 で、対象の属性を表します。 3 行目以降の行は、特定の *リグレッサー*の数式に関する詳細を提供します。 リグレッサーは、出力変数との間に線形のリレーションシップがある入力変数です。 リグレッサーは複数作成することができ、各リグレッサーには、係数 (VALUETYPE = 7)、スコア ゲイン (VALUETYPE = 8)、および統計 (VALUETYPE = 9) が格納される個別の行が作成されます。 さらに、テーブルには、式の切片 (VALUETYPE = 11) が格納される行も含まれます。  
  
### <a name="elements-of-the-regression-formula"></a>回帰式の要素  
 入れ子になった NODE_DISTRIBUTION テーブルでは、回帰式の各要素が個別の行に格納されます。 例の結果に含まれるデータの最初の 2 行には、従属変数を表す予測可能な属性である **Yearly Income**に関する情報が格納されています。 SUPPORT 列には、この属性の 2 つの状態 ( **Yearly Income** 値が使用できたことを示す状態と **Yearly Income** 値が不測していたことを示す状態) をサポートするケースの数が表示されます。  
  
 VARIANCE 列には、予測可能な属性の計算された分散が表示されます。 *分散* は、予想される分布でサンプル内の値がどのぐらい分散しているかを示す尺度です。 ここでは、平均値からの偏差の 2 乗の平均を取ることで分散を算出しています。 分散の平方根は標準偏差とも呼ばれます。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] では標準偏差は提供されませんが、簡単に計算することができます。  
  
 リグレッサーごとに 3 つの行が出力されます。 これらの行には、係数、スコア ゲイン、およびリグレッサーの統計が格納されます。  
  
 テーブルの最後の行には、式の切片 (VALUETYPE = 11) が格納されます。  
  
#### <a name="coefficient"></a>Coefficient  
 リグレッサーごとに係数 (VALUETYPE = 7) が計算されます。 係数自体は ATTRIBUTE_VALUE 列に表示されますが、係数の分散は VARIANCE 列に表示されます。 係数は、線形性が最も高くなるように計算されます。  
  
#### <a name="score-gain"></a>スコア ゲイン  
 各リグレッサーのスコア ゲイン (VALUETYPE = 8) は、属性の興味深さのスコアを表します。 この値を使用すると、複数のリグレッサーの有用性を評価できます。  
  
#### <a name="statistics"></a>統計  
 リグレッサー統計 (VALUETYPE = 9) は、値があるケースの属性の平均値です。 平均値自体は ATTRIBUTE_VALUE 列に表示されますが、平均値からの偏差の合計は VARIANCE 列に表示されます。  
  
#### <a name="intercept"></a>Intercept  
 通常、回帰式の *切片* (VALUETYPE = 11) または *残余* は、入力属性が 0 の位置にあるときの予測可能な属性の値を示します。 入力属性が 0 になることは通常はありません。0 になった場合、直観に反する結果が生じることがあります。  
  
 たとえば、年齢に基づいて収入を予測するモデルでは、年齢が 0 のときの収入がわかっても役には立ちません。 実際には、平均値に対する線の挙動を知る方が通常は役立ちます。 そのため、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] では、各リグレッサーを平均値とのリレーションシップで表すように切片が変更されています。  
  
 この変更は、マイニング モデル コンテンツで確認するのは困難ですが、 **Microsoft ツリー ビューアー** の **[マイニング凡例]** で完全な回帰式を表示するとすぐにわかります。 回帰式が 0 を表す位置から平均値を表す位置へとシフトしています。 これにより、現在のデータがより直感的にわかりやすい形で表示されます。  
  
 したがって、平均年齢が 45 歳前後である場合、回帰式の切片 (VALUETYPE = 11) は平均収入を示します。  
  
## <a name="see-also"></a>関連項目  
 [マイニング モデル コンテンツ &#40;Analysis Services - データ マイニング&#41;](mining-model-content-analysis-services-data-mining.md)   
 [Microsoft 線形回帰アルゴリズム](microsoft-linear-regression-algorithm.md)   
 [Microsoft 線形回帰アルゴリズム テクニカル リファレンス](microsoft-linear-regression-algorithm-technical-reference.md)   
 [線形回帰モデルのクエリ例](linear-regression-model-query-examples.md)  
  
  
