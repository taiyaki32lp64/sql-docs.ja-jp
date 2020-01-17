---
title: データ マイニング オブジェクトの処理 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- processing objects [Analysis Services]
- mining structures [Analysis Services]
- process [Analysis Services]
- mining structures [Analysis Services], creating
- mining structures [Analysis Services], how-to topics
- mining structures [Analysis Services], processing
ms.assetid: 0f6993c0-0917-4935-82f9-7b8a8a7cc627
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 65c61f6e4b571880b6607bb647d2629a3b6864f7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66083149"
---
# <a name="processing-data-mining-objects"></a>データ マイニング オブジェクトの処理
  データ マイニング オブジェクトは、処理されるまでは単なる空のコンテナーです。 データ マイニング モデルの*処理* は *トレーニング*とも呼ばれます。  
  
 **マイニング構造の処理。** マイニング構造では、列バインドと使用方法のメタデータで定義されている外部データ ソースからデータを取得し、データを読み取ります。 このデータの全体が読み取られて分析され、さまざまな統計情報が抽出されます。 Analysis Services では、データ マイニング アルゴリズムによる分析に適した、簡潔な表現のデータがローカル キャッシュに格納されます。 モデルを処理した後、このキャッシュを保持することも削除することもできます。 既定では、キャッシュが保存されます。 詳細については、「 [Process a Mining Structure](process-a-mining-structure.md)」 (マイニング構造の処理) を参照してください。  
  
 **マイニング モデルの処理。** マイニング モデルでは、空の場合、それが処理されるまでにのみの定義を含むです。 マイニング モデルを処理するには、基になるマイニング構造の処理が完了している必要があります。 マイニング モデルは、マイニング構造のキャッシュからデータを取得し、モデルに対して作成されたフィルターがあれば適用した後、データセットをアルゴリズムに渡してパターンを検出します。 処理後のモデルには、データ自体ではなく処理結果だけが保存されます。 詳細については、「 [Process a Mining Model](process-a-mining-model.md)」 (マイニング モデルの処理) を参照してください。  
  
 次の図は、マイニング構造とマイニング モデルの処理時のデータ フローを示しています。  
  
 ![データの処理: ソース、構造モデル、](../media/dmcon-modelarch.gif "データの処理: ソース、モデルの構造")  
  
## <a name="viewing-the-results-of-processing"></a>処理結果の表示  
 処理後のマイニング構造には、統計分析に使用できる、簡潔な表現のデータが含まれています。 キャッシュが消去されていない場合、このキャッシュ内のデータには次の方法でアクセスできます。  
  
-   モデルに対するデータ マイニング拡張機能 (DMX) クエリを作成し、構造にドリルスルーします。 詳細については、「[SELECT FROM &#60;model&#62;.CASES (DMX)](/sql/dmx/select-from-model-content-dmx)」を参照してください。  
  
-   構造に基づいてモデルを参照し、ユーザー インターフェイスでいずれかのオプションを使用して構造ケースにドリルスルーします。 詳細については、「 [Data Mining Model Viewers](data-mining-model-viewers.md)」 (データ マイニング モデル ビューアー) または「 [マイニング モデルからケース データへのドリルスルー](drill-through-to-case-data-from-a-mining-model.md)」を参照してください。  
  
-   構造ケースに対する DMX クエリを作成します。 詳細については、「[SELECT FROM &#60;structure&#62;.CASES](/sql/dmx/select-from-structure-cases)」を参照してください。  
  
 処理後のマイニング モデルには、分析によって生成されたパターンと、モデルの結果からキャッシュ内のトレーニング データへのマッピングだけが含まれています。 モデルの結果 ( *モデル コンテンツ*) に対して参照やクエリを実行できます。また、キャッシュされている場合は、モデル ケースや構造ケースに対してクエリを実行することもできます。  
  
 各マイニング モデルのモデル コンテンツは、作成に使用されたアルゴリズムによって異なります。 たとえば、クラスター モデルとデシジョン ツリー モデルでは、まったく同じデータを使用した場合でも、モデル コンテンツが大きく異なります。 詳細については、「[マイニング モデル コンテンツ (Analysis Services - データ マイニング)](mining-model-content-analysis-services-data-mining.md)」を参照してください。  
  
## <a name="processing-requirements"></a>処理の要件  
 処理の要件は、マイニング モデルがリレーショナル データのみに基づいているか多次元データ ソースに基づいているかに応じて異なる場合があります。  
  
 リレーショナル データソースの処理には、トレーニング データを作成し、そのデータでマイニング アルゴリズムを実行することだけが必要です。 ただし、マイニング モデルがディメンション、メジャーなどの OLAP オブジェクトに基づいている場合は、基になるデータが処理済みの状態であることが必要です。 これには、多次元オブジェクトを処理して、マイニング モデルを作成する必要があります。  
  
 詳細については、「[処理の要件および注意事項 &#40;データ マイニング&#41;](processing-requirements-and-considerations-data-mining.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [ドリルスルー クエリ &#40;データ マイニング&#41;](drillthrough-queries-data-mining.md)   
 [マイニング構造 &#40;Analysis Services - データ マイニング&#41;](mining-structures-analysis-services-data-mining.md)   
 [マイニング モデル &#40;Analysis Services - データ マイニング&#41;](mining-models-analysis-services-data-mining.md)   
 [論理アーキテクチャ &#40;Analysis Services - データ マイニング&#41;](logical-architecture-analysis-services-data-mining.md)  
  
  
