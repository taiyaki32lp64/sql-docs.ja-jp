---
title: Microsoft アソシエーション アルゴリズム テクニカル リファレンス |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- MINIMUM_ITEMSET_SIZE parameter
- MAXIMUM_SUPPORT parameter
- association algorithms [Analysis Services]
- MINIMUM_SUPPORT parameter
- OPTIMIZED_PREDICTION_COUNT parameter
- associations [Analysis Services]
- MAXIMUM_ITEMSET_COUNT parameter
- MAXIMUM_ITEMSET_SIZE parameter
- MINIMUM_PROBABILITY parameter
ms.assetid: 50a22202-e936-4995-ae1d-4ff974002e88
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 30310cf891d8b5e7ef9a32b5a8e7254cbca2ecd0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66084129"
---
# <a name="microsoft-association-algorithm-technical-reference"></a>Microsoft アソシエーション アルゴリズム テクニカル リファレンス
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] アソシエーション ルール アルゴリズムは、よく知られている Apriori アルゴリズムの直接的な実装です。  
  
 アソシエーションの分析には、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] デシジョン ツリー アルゴリズムと [!INCLUDE[msCoName](../../includes/msconame-md.md)] アソシエーション ルール アルゴリズムの両方を使用できますが、それぞれのアルゴリズムで異なるルールが検出される場合があります。 デシジョン ツリー モデルでは、情報利得に基づく分割によってルールが導き出されるのに対し、アソシエーション モデルでは、ルールは完全に信頼度に基づいています。 したがって、アソシエーション モデルの場合、強力なルール (信頼度が高いルール) は新しい情報を提供するわけではないため、興味深いものになるとは限りません。  
  
## <a name="implementation-of-the-microsoft-association-algorithm"></a>Microsoft アソシエーション アルゴリズムの実装  
 Apriori アルゴリズムは、パターンを分析するのではなく、 *候補アイテムセット*を生成およびカウントします。 アイテムは、分析するデータの種類に応じて、イベント、製品、または属性の値を表します。  
  
 アソシエーション モデルの最も一般的な種類のうち、Yes/No または Missing/Existing の値を表すブール変数は、製品名やイベント名のようなそれぞれの属性に割り当てられます。 マーケット バスケット分析は、ブール変数を使用して顧客の買い物かごに特定の製品が入っているかどうかを表すアソシエーション ルール モデルの 1 つの例です。  
  
 このアルゴリズムでは、各アイテムセットに対して、サポートと信頼度を表すスコアが作成されます。 これらのスコアを使用して、アイテムセットに順位を付けたり、アイテムセットから興味深いルールを引き出したりすることができます。  
  
 アソシエーション モデルは、数値属性に対しても作成できます。 属性が連続的である場合は、数値をバケットに *分離* またはグループ化できます。 その分離された値がブール値または属性と値のペアとして処理されます。  
  
### <a name="support-probability-and-importance"></a>サポート、確率、および重要度  
 *サポート*( *頻度*とも呼ばれます) は、対象となるアイテムまたはアイテムの組み合わせを含むケースの数を表します。 指定した以上のサポートを持つアイテムのみがモデルに含まれます。  
  
 アイテムの組み合わせのサポートも、MINIMUM_SUPPORT パラメーターで定義されているしきい値を超えている場合、そのアイテムの集合を、 *よく使用されるアイテムセット* と呼びます。 たとえば、アイテムセットが {A,B,C} で MINIMUM_SUPPORT の値が 10 の場合、A、B、および C の各アイテムがそれぞれ 10 個以上のケースで検出されないとそれらのアイテムはモデルに含まれませんが、さらにそのアイテムの組み合わせ {A,B,C} も 10 個以上のケースで検出される必要があります。  
  
 **注** アイテムセットの最大長 (長さはアイテムの数を表します) を指定することによってマイニング モデルのアイテムセットの数を制御することもできます。  
  
 特定のアイテムまたはアイテムセットのサポートは、既定ではそのアイテムまたはアイテムセットを含むケースの数を表しますが、 データセット内の全ケースの割合として MINIMUM_SUPPORT を表現することもできます。その場合は、数を 1 未満の 10 進値として入力します。 たとえば 0.03 という MINIMUM_SUPPORT 値を指定した場合、そのアイテムまたはアイテムセットは、データセット内の全ケースの 3% 以上に含まれていないとモデルに含まれません。 数と割合のどちらを使用するのがよいかは、実際にモデルで試して判断する必要があります。  
  
 一方、ルールのしきい値は、数や割合としてではなく確率 ( *信頼度*とも呼ばれます) として表現されます。 たとえば、アイテムセット {A,B,C} が 50 個のケースで発生し、アイテムセット {A,B,D} も 50 個のケースで、さらにアイテムセット {A,B} も別の 50 個のケースで発生する場合、{A,B} が {C} の強力な予測子にならないことは明らかです。 このため、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] では、すべての既知の結果に対して特定の結果に加重するために、アイテムセット {A,B,C} のサポートをすべての関連するアイテムセットのサポートで割って個々のルール (If {A,B} Then {C} など) の確率が計算されます。  
  
 MINIMUM_PROBABILITY の値を設定すると、モデルで生成されるルールの数を制限することができます。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] では、作成される各ルールについて、その *重要度*( *リフト*とも呼ばれます) を示すスコアが出力されます。 重要度 (リフト) の計算方法はアイテムセットとルールで異なります。  
  
 アイテムセットの重要度は、アイテムセットの確率をアイテムセット内の個々のアイテムの合成確率で割って計算されます。 たとえばアイテムセットに {A,B} が含まれている場合、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] は、この A と B の組み合わせを含むすべてのケースをカウントし、それをケースの合計数で割って確率を計算した後、その確率を正規化します。  
  
 ルールの重要度は、与えられたルールの左辺に対するルールの右辺の対数尤度で計算されます。 たとえばルール `If {A} Then {B}`の場合、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] は、A と B を含むケースを B を含み A を含まないケースで割って比率を計算し、その比率を対数スケールを使用して正規化します。  
  
### <a name="feature-selection"></a>機能の選択  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] アソシエーション ルール アルゴリズムでは、自動的な機能の選択は一切行われません。 代わりに、アルゴリズムで使用されるデータを制御するパラメーターが用意されています。 たとえば、各アイテムセットのサイズを制限することも、アイテムセットがモデルに追加されるために必要な最大サポートおよび最小サポートを設定することもできます。  
  
-   一般的すぎて興味深いものではないアイテムやイベントを除外するには、MAXIMUM_SUPPORT の値を小さくして頻度の高いアイテムセットをモデルから削除します。  
  
-   頻度の低いアイテムやアイテムセットを除外するには、MINIMUM_SUPPORT の値を大きくします。  
  
-   ルールを除外するには、MINIMUM_PROBABILITY の値を大きくします。  
  
## <a name="customizing-the-microsoft-association-rules-algorithm"></a>Microsoft アソシエーション ルール アルゴリズムのカスタマイズ  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] アソシエーション ルール アルゴリズムでは、結果として得られるマイニング モデルの動作、パフォーマンス、および精度に影響を与えるいくつかのパラメーターがサポートされています。  
  
### <a name="setting-algorithm-parameters"></a>アルゴリズム パラメーターの設定  
 マイニング モデルのパラメーターは、 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]のデータ マイニング デザイナーを使用していつでも変更できます。 プログラムでを使用してもパラメーターを変更することができます、 <xref:Microsoft.AnalysisServices.MiningModel.AlgorithmParameters%2A> AMO、またはを使用して、コレクション、 [MiningModels 要素&#40;ASSL&#41; ](https://docs.microsoft.com/bi-reference/assl/collections/miningmodels-element-assl) XMLA でします。 次の表では、各パラメーターについて説明します。  
  
> [!NOTE]  
>  DMX ステートメントでは; を使用して、既存のモデル内のパラメーターを変更することはできません。DMX CREATE MODEL または ALTER STRUCTURE では、パラメーターを指定する必要があります.ADD MODEL で指定する必要があります。  
  
 *MAXIMUM_ITEMSET_COUNT*  
 生成されるアイテムセットの最大数を指定します。 数が指定されていない場合は、既定値が使用されます。  
  
 既定値は 200000 です。  
  
> [!NOTE]  
>  アイテムセットはサポートで順位付けされます。 サポートの値が同じアイテムセット間の順序は任意です。  
  
 *MAXIMUM_ITEMSET_SIZE*  
 アイテムセットで使用できるアイテムの最大数を指定します。 この値を 0 に設定すると、アイテムセットのサイズに制限がなくなります。  
  
 既定値は 3 です。  
  
> [!NOTE]  
>  この制限に達するとモデルの処理が中止されるため、この値を小さくすることによってモデルの作成に要する時間を短縮できる場合もあります。  
  
 *MAXIMUM_SUPPORT*  
 アイテムセットをサポートするケースの最大数を指定します。 このパラメーターを使用すると、頻繁に出現するためにあまり意味がないと考えられるアイテムを除外できます。  
  
 この値が 1 より小さい場合、値はケースの総数の割合を表します。 1 より大きい値は、アイテムセットを含むことができるケースの絶対数を表します。  
  
 既定値は 1 です。  
  
 *MINIMUM_ITEMSET_SIZE*  
 アイテムセットで使用できるアイテムの最小数を指定します。 この数を大きくすると、モデルに含まれるアイテムセットが少なくなる可能性があります。 たとえば、1 つのアイテムから成るアイテムセットを無視する場合などに便利です。  
  
 既定値は 1 です。  
  
> [!NOTE]  
>  この最小値を大きくしても、モデルの処理時間を短縮することはできません。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] では、いずれにしても単一のアイテムの確率を処理の一環として計算しなければならないからです。 ただし、この値を大きく設定すると、小さいアイテムセットを除外できます。  
  
 *MINIMUM_PROBABILITY*  
 ルールが true である最小確率を指定します。  
  
 たとえば、この値を 0.5 に設定すると、確率が 50% より低いルールは生成されなくなります。  
  
 既定値は 0.4 です。  
  
 *MINIMUM_SUPPORT*  
 アルゴリズムによってルールが生成される前に、アイテムセットを含む必要があるケースの最小数を指定します。  
  
 この値を 1 より小さい値に設定すると、ケースの最小数がケースの総数の割合として計算されます。  
  
 この値を 1 より大きい整数に設定すると、ケースの最小数が、アイテムセットを含む必要のあるケースの数として計算されます。 メモリに制限がある場合は、アルゴリズムによってこのパラメーターの値が自動的に増加されることがあります。  
  
 既定値は 0.03 です。 この場合、アイテムセットがモデルに含まれるためには少なくとも 3% のケースで検出される必要があります。  
  
 *OPTIMIZED_PREDICTION_COUNT*  
 予測を最適化するためにキャッシュされるアイテムの数を定義します。  
  
 既定値は 0 です。 既定値を使用した場合、クエリで要求された数だけ予測が生成されます。  
  
 *OPTIMIZED_PREDICTION_COUNT* に対して 0 以外の値を指定した場合は、追加の予測を要求したとしても、返される予測の数は多くても指定したアイテム数になります。 ただし、値を設定することで予測のパフォーマンスが向上する場合があります。  
  
 たとえば、この値を 3 に設定すると、3 つのアイテムだけが予測用にキャッシュされます。 返される 3 つの項目と同程度の可能性を持つ他の予測を見ることはできません。  
  
### <a name="modeling-flags"></a>ModelingFlags  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] アソシエーション ルール アルゴリズムでは、次のモデリング フラグを使用できます。  
  
 NOT NULL  
 列に NULL を含めることはできないことを示します。 モデルのトレーニング中に [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] NULL が検出された場合はエラーが発生します。  
  
 マイニング構造列に適用されます。  
  
 MODEL_EXISTENCE_ONLY  
 列が、`Missing` および `Existing` の 2 つの可能な状態を持つ列として扱われることを示します。 NULL は Missing 値になります。  
  
 マイニング モデル列に適用されます。  
  
## <a name="requirements"></a>必要条件  
 アソシエーション モデルには、キー列、入力列、および 1 つの予測可能列が必要です。  
  
### <a name="input-and-predictable-columns"></a>入力列と予測可能列  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] アソシエーション ルール アルゴリズムでは、次の表に示す特定の入力列と予測可能列がサポートされています。 マイニング モデルにおけるコンテンツの種類の意味については、「[コンテンツの種類 (データ マイニング)](content-types-data-mining.md)」を参照してください。  
  
|[列]|コンテンツの種類|  
|------------|-------------------|  
|入力属性|Cyclical、Discrete、Discretized、Key、Table、Ordered|  
|予測可能な属性|Cyclical、Discrete、Discretized、Table、Ordered|  
  
> [!NOTE]  
>  コンテンツの種類 Cyclical および Ordered はサポートされますが、アルゴリズムはこれらを不連続の値として扱い、特別な処理は行いません。  
  
## <a name="see-also"></a>関連項目  
 [Microsoft アソシエーション アルゴリズム](microsoft-association-algorithm.md)   
 [結合モデルのクエリ例](association-model-query-examples.md)   
 [アソシエーション モデルのマイニング モデル コンテンツ &#40;Analysis Services - データ マイニング&#41;](mining-model-content-for-association-models-analysis-services-data-mining.md)  
  
  
