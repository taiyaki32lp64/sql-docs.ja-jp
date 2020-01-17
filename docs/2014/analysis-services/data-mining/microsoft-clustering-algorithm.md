---
title: Microsoft クラスタ リング アルゴリズム |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- segmentation algorithms [Analysis Services]
- nearest neighbor [Data Mining]
- clustering [Data Mining]
- clusters [Analysis Services]
- relationships [Analysis Services], clusters
- algorithms [data mining]
- classification algorithms [Analysis Services]
- datasets [Analysis Services]
- clustering algorithms [Analysis Services]
ms.assetid: 92a1e67e-f46e-4960-99b2-4d20f6192fbd
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: da8511361badbdfa1ded7497aaf623fdc35252d0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66084004"
---
# <a name="microsoft-clustering-algorithm"></a>Microsoft クラスタリング アルゴリズム
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] クラスタリング アルゴリズムは、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] によって提供される分割アルゴリズムです。 このアルゴリズムは、反復的な手法を使用して、類似の特性を持つクラスターにデータセット内のケースをグループ化します。 このグループ化は、データの探索、データの異常の特定、および予測の作成に役立ちます。  
  
 クラスタリング モデルでは、一般レベルの観察では論理的に推論できないデータセット内の関係が識別されます。 たとえば、自転車で通勤している従業員は、一般的に勤め先から遠くないところに住んでいることは、だれでも明確に理解できます。 しかし、このアルゴリズムでは、それほど明確でない自転車通勤者に関する他の特性を見つけることができます。 次の図では、クラスター A は勤め先に車で通勤する従業員に関するデータを表し、クラスター B は勤め先に自転車で通勤する従業員に関するデータを表しています。  
  
 ![通勤者のクラスター パターン](../media/clustering-example.gif "通勤者のクラスター パターン")  
  
 クラスタリング アルゴリズムは、クラスタリング モデルを作成するために予測可能列を指定する必要がないという点において、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] デシジョン ツリー アルゴリズムなどの他のデータ マイニング アルゴリズムと異なります。 クラスタリング アルゴリズムでは、データに存在する関係と、アルゴリズムで識別されたクラスターからのみモデルをトレーニングします。  
  
## <a name="example"></a>例  
 類似の人口統計情報を共有しており、 [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)] 社から類似の製品を購入する人々のグループがあるとします。 このような人々のグループが、データの 1 クラスターを表し、 データベース内にいくつか存在します。 クラスターを構成する列を観察することによって、データセットの各レコードが互いにどのように関係しているかを明確に理解できます。  
  
## <a name="how-the-algorithm-works"></a>アルゴリズムの動作  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] クラスタリング アルゴリズムでは、まずデータセット内の関係が識別され、その関係に基づいて一連のクラスターが生成されます。 次の図のように、アルゴリズムによってデータがどのようにグループ化されるかを視覚的に表すには、散布図が便利です。 散布図にはデータセット内のすべてのケースが表され、各ケースはグラフ上にポイントで示されます。 クラスターは、グラフ上のポイントをグループ化したもので、アルゴリズムによって識別された関係を示します。  
  
 ![散布図、データセット内のケースの](../media/clustering-plot.gif "データセット内のケースの散布図")  
  
 アルゴリズムはクラスターを定義した後、そのクラスターがポイントのグループをどの程度適切に表しているかを判断し、グループを再定義して、データをより適切に表すクラスターを作成します。 このプロセスは、クラスターの再定義によってそれ以上結果を向上できなくなるまで繰り返されます。  
  
 クラスタリング技法を指定したり、クラスターの最大数を制限したり、クラスターの作成に必要なサポート量を変更したりして、アルゴリズムの動作をカスタマイズできます。 詳細については、「 [Microsoft クラスタリング アルゴリズム テクニカル リファレンス](microsoft-clustering-algorithm-technical-reference.md)」を参照してください。  
  
## <a name="data-required-for-clustering-models"></a>クラスタリング モデルに必要なデータ  
 クラスタリング モデルのトレーニングに使用するデータを用意する際には、必要なデータ量やデータの使用方法など、このアルゴリズムにおける要件を把握しておいてください。  
  
 クラスタリング モデルの要件は次のとおりです。  
  
-   **単一キー列** : それぞれのモデルには、各レコードを一意に識別する数値列またはテキスト列が 1 つ含まれている必要があります。 複合キーは使用できません。  
  
-   **入力列** : 各モデルには、クラスターの作成に使用される値が含まれた入力列が 1 つ以上必要です。 入力列はいくつあってもかまいませんが、各列内の値の数によっては、列を追加するとモデルのトレーニングにかかる時間が長くなる場合があります。  
  
-   **省略可能な予測可能列** : このアルゴリズムでモデルを作成するために予測可能列は必要ありません。しかし、ほぼすべてのデータ型の予測可能列を追加することができます。 予測可能列の値は、クラスタリング モデルへの入力として扱うことも、予測のみに使用するよう指定することもできます。 たとえば、地域や年齢などの人口統計に対してクラスタリングを実行することにより顧客の収入を予測する場合、収入を `PredictOnly` として指定し、地域や年齢など、その他すべての列を入力として追加します。  
  
 クラスタリング モデルでサポートされるコンテンツの種類とデータ型の詳細については、「 [Microsoft クラスタリング アルゴリズム テクニカル リファレンス](microsoft-clustering-algorithm-technical-reference.md)」の「必要条件」を参照してください。  
  
## <a name="viewing-a-clustering-model"></a>クラスタリング モデルの表示  
 モデルを参照するには、 **Microsoft クラスター ビューアー**を使用します。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] でクラスタリング モデルを表示すると、クラスター間の相互関係がダイアグラムで示され、各クラスターの詳細なプロファイル、クラスターどうしを識別する属性の一覧、およびトレーニング データセット全体の特性も提供されます。 詳細については、「 [Microsoft クラスター ビューアーを使用したモデルの参照](browse-a-model-using-the-microsoft-cluster-viewer.md)」を参照してください。  
  
 さらに詳細を知るには、 [Microsoft 汎用コンテンツ ツリー ビューアー](browse-a-model-using-the-microsoft-generic-content-tree-viewer.md)でモデルを参照してください。 モデルに保存される内容には、各ノードのすべての値の分布や、各クラスターの確率などの情報が含まれます。 詳細については、「[クラスター モデルのマイニング モデル コンテンツ &#40;Analysis Services - データ マイニング&#41;](mining-model-content-for-clustering-models-analysis-services-data-mining.md)」を参照してください。  
  
## <a name="creating-predictions"></a>予測の作成  
 モデルのトレーニング後、結果がパターンのセットとして保存されます。これを参照したり、これを使用して予測を実行したりできます。  
  
 クエリを作成して、検出されたクラスターに新しいデータが合致するかどうかの予測を返したり、クラスターに関する説明的な統計情報を取得したりすることもできます。  
  
 データ マイニング モデルに対するクエリの作成方法については、「 [データ マイニング クエリ](data-mining-queries.md)」を参照してください。 クラスタリング モデルでクエリを使用する方法の例については、「 [クラスタリング モデルのクエリ例](clustering-model-query-examples.md)」を参照してください。  
  
## <a name="remarks"></a>コメント  
  
-   Predictive Model Markup Language (PMML) を使用したマイニング モデルの作成がサポートされています。  
  
-   ドリルスルーがサポートされています。  
  
-   OLAP マイニング モデルの使用およびデータ マイニング ディメンションの作成がサポートされています。  
  
## <a name="see-also"></a>参照  
 [データ マイニング アルゴリズム &#40;Analysis Services - データ マイニング&#41;](data-mining-algorithms-analysis-services-data-mining.md)   
 [Microsoft クラスタリング アルゴリズム テクニカル リファレンス](microsoft-clustering-algorithm-technical-reference.md)   
 [クラスター モデルのマイニング モデル コンテンツ &#40;Analysis Services - データ マイニング&#41;](mining-model-content-for-clustering-models-analysis-services-data-mining.md)   
 [クラスタリング モデルのクエリ例](clustering-model-query-examples.md)  
  
  
