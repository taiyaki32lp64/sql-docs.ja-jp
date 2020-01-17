---
title: Microsoft シーケンス クラスター アルゴリズム テクニカル リファレンス |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- MAXIMUM_SEQUENCE_STATES parameter
- MINIMUM_SUPPORT parameter
- MAXIMUM_STATES parameter
- sequence clustering algorithms [Analysis Services]
- CLUSTER_COUNT parameter
ms.assetid: 251c369d-6b02-4687-964e-39bf55c9b009
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6ae48fe00fb9c24e2d6d0ddde61302cff3ceba0b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66083838"
---
# <a name="microsoft-sequence-clustering-algorithm-technical-reference"></a>Microsoft シーケンス クラスタリング アルゴリズム テクニカル リファレンス
  Microsoft シーケンス クラスター アルゴリズムは、複合的なアルゴリズムです。このアルゴリズムでは、Markov 連鎖分析を使用して順序付けられたシーケンスを特定し、この分析結果とクラスタリング技法を組み合わせて、シーケンスおよびモデル内のその他の属性に基づいてクラスターを生成します。 このトピックでは、アルゴリズムの実装、アルゴリズムをカスタマイズする方法、およびシーケンス クラスター モデルの特別な要件について説明します。  
  
 シーケンス クラスター モデルの参照およびクエリを行う方法を含む、アルゴリズムに関する一般的な情報については、「 [Microsoft Sequence Clustering Algorithm](microsoft-sequence-clustering-algorithm.md)」をご覧ください。  
  
## <a name="implementation-of-the-microsoft-sequence-clustering-algorithm"></a>Microsoft シーケンス クラスター アルゴリズムの実装  
 Microsoft シーケンス クラスター モデルでは、Markov モデルを使用して、シーケンスの特定やシーケンスの確率の決定を行います。 Markov モデルは、さまざまな状態の間の遷移を格納する有向グラフです。 Microsoft シーケンス クラスター アルゴリズムでは n 次 Markov 連鎖を使用します。隠れ Markov モデルは使用しません。  
  
 Markov 連鎖の次数は、現在の状態の確率を決定するために使用される状態の数を示しています。 1 次 Markov モデルでは、現在の状態の確率は直前の状態のみに依存します。 2 次 Markov 連鎖では、状態の確率は前の 2 つの状態に依存し、以下同様に増えていきます。 Markov 連鎖ごとに、状態の各組み合わせの遷移が遷移マトリックスに格納されます。 Markov 連鎖が長くなるにつれ、マトリックスのサイズも指数関数的に大きくなり、マトリックスが非常に疎になります。 処理時間も比例して長くなります。  
  
 特定のサイトの Web ページへのアクセスを分析するクリックストリーム分析の例を使用して、連鎖がどうなるかを思い浮かべてみるとわかりやすくなります。 各ユーザーによって、セッションごとにクリックの長いシーケンスが作成されます。 Web サイトでのユーザーの行動を分析するモデルを作成する場合、トレーニングに使用するデータセットは、同じクリック パスのインスタンスの総数を含むグラフに変換される URL のシーケンスです。 たとえば、このグラフには、ユーザーがページ 1 からページ 2 に移動する確率 (10%)、ユーザーがページ 1 からページ 3 に移動する確率 (20%) などが含まれます。 すべての有効なパスおよび部分的なパスを合わせると、いずれか 1 つのパスを監視する場合よりもずっと長く複雑なグラフになります。  
  
 既定では、Microsoft シーケンス クラスター アルゴリズムではクラスタリングの Expectation Maximization (EM) 手法を使用します。 詳細については、「 [Microsoft クラスタリング アルゴリズム テクニカル リファレンス](microsoft-clustering-algorithm-technical-reference.md)」を参照してください。  
  
 クラスタリングの対象の属性は、シーケンシャルかどうかに依存しません。 各クラスターは、確率分布を使用してランダムに選択されます。 各クラスターには、パスの完全なセットを表す Markov 連鎖、およびシーケンスの状態遷移と確率を含むマトリックスがあります。 初期分布に基づいて、特定のクラスターで、シーケンスなど任意の属性の確率が Bayes ルールを使用して計算されます。  
  
 Microsoft シーケンス クラスター アルゴリズムでは、モデルへの非シーケンシャル属性の追加がサポートされています。 つまり、一般的なクラスター モデルの場合と同様に、追加属性をシーケンス属性と組み合わせて、類似する属性を含むケースのクラスターを作成できます。  
  
 傾向として、シーケンス クラスター モデルでは、一般的なクラスター モデルより多くのクラスターを作成します。 そのため、Microsoft シーケンス クラスター アルゴリズムでは、 *クラスター分解*を実行して、シーケンスやその他の属性に基づいてクラスターを分割します。  
  
### <a name="feature-selection-in-a-sequence-clustering-model"></a>シーケンス クラスター モデルでの機能の選択  
 シーケンスの作成時には機能の選択は実行されません。ただし、クラスタリングの段階で機能の選択が適用されます。  
  
|モデルの種類|機能の選択の方法|コメント|  
|----------------|------------------------------|--------------|  
|シーケンス クラスター|使用しない|機能の選択は実行されません。ただし、パラメーター MINIMUM_SUPPORT および MINIMUM_PROBABILIITY の値を設定することによってアルゴリズムの動作を制御できます。|  
|クラスター|興味深さのスコア|クラスタリング アルゴリズムでは不連続のアルゴリズムや分離されたアルゴリズムを使用できますが、各属性のスコアは距離として計算されるため連続値です。したがって、興味深さのスコアが使用されます。|  
  
 詳しくは、「 [Feature Selection](../../sql-server/install/feature-selection.md)」をご覧ください。  
  
### <a name="optimizing-performance"></a>パフォーマンスの最適化  
 Microsoft シーケンス クラスター アルゴリズムでは、処理を最適化するさまざまな方法がサポートされています。  
  
-   CLUSTER_COUNT パラメーターの値を設定すると、生成されるクラスターの数を制御できます。  
  
-   MINIMUM_SUPPORT パラメーターの値を増やすと、属性として含まれるシーケンスの数を減らすことができます。 その結果、頻度の低いシーケンスが除外されます。  
  
-   関連属性をグループ化すると、モデルを処理する前に複雑さを軽減できます。  
  
 通常、いくつかの方法で、n 次 Markov 連鎖モードのパフォーマンスを最適化できます。  
  
-   可能なシーケンスの長さを制御します。  
  
-   n の値をプログラムによって小さくします。  
  
-   指定したしきい値を超える確率のみを格納します。  
  
 これらの方法の詳細については、このトピックでは説明しません。  
  
## <a name="customizing-the-sequence-clustering-algorithm"></a>シーケンス クラスター アルゴリズムのカスタマイズ  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] シーケンス クラスター アルゴリズムでは、結果として得られるマイニング モデルの動作、パフォーマンス、および精度に影響を与えるパラメーターがサポートされています。 また、アルゴリズムによるトレーニング データの処理方法を制御するモデリング フラグを設定して、完成したモデルの動作を変更することもできます。  
  
### <a name="setting-algorithm-parameters"></a>アルゴリズム パラメーターの設定  
 次の表は、Microsoft シーケンス クラスター アルゴリズムで使用できるパラメーターを示しています。  
  
 CLUSTER_COUNT  
 アルゴリズムによって作成されるクラスターの概数を指定します。 その数のクラスターをデータから作成できない場合は、可能な限り多数のクラスターが作成されます。 CLUSTER_COUNT パラメーターを 0 に設定すると、アルゴリズムではヒューリスティックを使用して、作成するクラスターの数が最適に決定されます。  
  
 既定値は 10 です。  
  
> [!NOTE]  
>  0 以外の数値を指定すると、アルゴリズムへのヒントとして機能します。アルゴリズムでは指定の数を取得することを目標に処理が進められますが、指定の数以外になる場合もあります。  
  
 MINIMUM_SUPPORT  
 クラスターの作成に必要とされる、属性をサポートするケースの最小数を指定します。  
  
 既定値は 10 です。  
  
 MAXIMUM_SEQUENCE_STATES  
 シーケンスの状態の最大数を指定します。  
  
 この値を 100 より大きい数値に設定すると、アルゴリズムは意味のある情報を提供するモデルを作成できなくなります。  
  
 既定値は、64 です。  
  
 MAXIMUM_STATES  
 アルゴリズムによってサポートされる非シーケンス属性用の状態の最大数を指定します。 アルゴリズムが、属性の最も一般的な状態を使用し、残りの状態として扱われます非シーケンス属性の状態の数が状態の最大数よりも大きい場合は、`Missing`します。  
  
 既定値は、100 です。  
  
### <a name="modeling-flags"></a>ModelingFlags  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] シーケンス クラスター アルゴリズムでは、次のモデリング フラグを使用できます。  
  
 NOT NULL  
 列に NULL を含めることはできないことを示します。 モデルのトレーニング中に NULL が検出された場合はエラーが発生します。  
  
 マイニング構造列に適用されます。  
  
 MODEL_EXISTENCE_ONLY  
 列が、`Missing` および `Existing` の 2 つの可能な状態を持つ列として扱われることを示します。 NULL は `Missing` 値として扱われます。  
  
 マイニング モデル列に適用されます。  
  
 マイニング モデルでの Missing 値の使用、および確率スコアへの Missing 値の影響の詳細については、「[不足値 (Analysis Services - データ マイニング)](missing-values-analysis-services-data-mining.md)」をご覧ください。  
  
## <a name="requirements"></a>必要条件  
 ケース テーブルにはケース ID 列が必要です。 オプションで、ケースに関する属性を格納する他の列をケース テーブルに含めることができます。  
  
 Microsoft シーケンス クラスター アルゴリズムには、入れ子になったテーブルとして格納されるシーケンス情報が必要です。 入れ子になったテーブルには、1 つの Key Sequence 列が必要です。 `Key Sequence` 列には、文字列データ型など、並べ替え可能な任意の型のデータを含めることができますが、ケースごとに一意の値を含める必要があります。 さらに、モデルを処理する前に、ケース テーブルと入れ子になったテーブルの両方が、テーブルを関連付けるキーに基づいて昇順に並べ替えられていることを確認する必要があります。  
  
> [!NOTE]  
>  Microsoft シーケンス アルゴリズムを使用するがシーケンス列は使用しないモデルを作成する場合、結果として得られるモデルでは、シーケンスが含まれるのではなく、モデルに含まれている他の属性に基づいてケースがクラスター化されるだけです。  
  
### <a name="input-and-predictable-columns"></a>入力列と予測可能列  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] シーケンス クラスター アルゴリズムでは、次の表に示す特定の入力列と予測可能列がサポートされています。 マイニング モデルにおけるコンテンツの種類の意味については、「[コンテンツの種類 (データ マイニング)](content-types-data-mining.md)」を参照してください。  
  
|[列]|コンテンツの種類|  
|------------|-------------------|  
|入力属性|Continuous、Cyclical、Discrete、Discretized、Key、Key Sequence、Table、Ordered|  
|予測可能な属性|Continuous、Cyclical、Discrete、Discretized、Table、Ordered|  
  
## <a name="remarks"></a>コメント  
  
-   シーケンスの予測には [PredictSequence (DMX)](/sql/dmx/predictsequence-dmx) 関数を使用します。 各エディションの詳細については[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]シーケンス予測をサポートするを参照してください[機能は、SQL Server 2012 の各エディションでサポートされている](https://go.microsoft.com/fwlink/?linkid=232473)(https://go.microsoft.com/fwlink/?linkid=232473) します。  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] シーケンス クラスター アルゴリズムでは、Predictive Model Markup Language (PMML) を使用したマイニング モデルの作成はサポートされていません。  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] シーケンス クラスター アルゴリズムでは、ドリルスルー、OLAP マイニング モデルの使用、およびデータ マイニング ディメンションの使用がサポートされています。  
  
## <a name="see-also"></a>参照  
 [Microsoft Sequence Clustering Algorithm](microsoft-sequence-clustering-algorithm.md)   
 [Sequence Clustering Model Query Examples](clustering-model-query-examples.md)   
 [シーケンス クラスター モデルのマイニング モデル コンテンツ (Analysis Services - データ マイニング)](mining-model-content-for-sequence-clustering-models.md)  
  
  
