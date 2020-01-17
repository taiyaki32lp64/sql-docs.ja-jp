---
title: 分離メソッド (データ マイニング) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- content types [data mining]
- discretization [Analysis Services]
- columns [data mining], discretization
- THRESHOLDS method
- CLUSTERS method
- DiscretizationBuckets property
- AUTOMATIC method
- EQUAL_AREAS method
- coding [Data Mining]
ms.assetid: 02c0df7b-6ca5-4bd0-ba97-a5826c9da120
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5e984fe2ea57ab175e3224d099f5392f96287c74
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66084634"
---
# <a name="discretization-methods-data-mining"></a>分離メソッド (データ マイニング)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] でデータ マイニング モデルを作成するための一部のアルゴリズムでは、正常に機能するために特定の種類のコンテンツが必要です。 たとえば、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Naive Bayes アルゴリズムでは、連続列を入力として使用したり、連続する値を予測したりすることはできません。 また、一部の列に含まれている値が多すぎるため、データ マイニング モデルの作成元となるデータ内の対象パターンをアルゴリズムで容易に識別できない場合があります。  
  
 このような場合、アルゴリズムを使用してマイニング モデルを生成できるように、列内のデータを分離できます。 *分離* とは、値をバケットに分割して、限定された数の可能な状態を生成するプロセスです。 バケット自体は、順序付きの不連続の値として処理されます。 数値と文字列の両方の列を分離できます。  
  
 データを分離するためのいくつかのメソッドがあります。 データ マイニング ソリューションでリレーショナル データを使用する場合は、 <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationBucketCount%2A> property プロパティの値を設定して、データのグループ化に使用するバケットの数を制御できます。 既定のバケット数は 5 です。  
  
 データ マイニング ソリューションでオンライン分析処理 (OLAP) キューブのデータを使用する場合、データ マイニング アルゴリズムでは生成するバケットの数が次の式を使用して自動的に計算されます。ここで、n は列のデータの個別の値の数です。  
  
 `Number of Buckets = sqrt(n)`  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] でバケットの数を計算しない場合は、<xref:Microsoft.AnalysisServices.DimensionAttribute.DiscretizationBucketCount%2A> プロパティを使用して、バケットの数を手動で指定できます。  
  
 次の表では、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]でデータを分離するときに使用できるメソッドについて説明します。  
  
|分離メソッド|説明|  
|---------------------------|-----------------|  
|`AUTOMATIC`|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] によって、使用する分離メソッドが決定されます。|  
|`CLUSTERS`|このアルゴリズムは、トレーニング データをサンプリングして多数のランダム ポイントに初期化し、Expectation Maximization (EM) クラスター化アルゴリズムを使用して Microsoft クラスタリング アルゴリズムを何度か繰り返し実行することによって、データをグループに分割します。 `CLUSTERS` メソッドは、どのような分布曲線にも使用できるので便利です。 ただし、その他の分離メソッドよりも処理時間は長くなります。<br /><br /> このメソッドは数値列でのみ使用できます。|  
|`EQUAL_AREAS`|このアルゴリズムは、同数の値が含まれているグループにデータを分割します。 このメソッドは正規分布曲線に最適ですが、連続データの小さなグループに多数の値が含まれている分布の場合は適切に機能しません。 たとえば、品目の半数のコストが 0 である場合、データの半数は曲線の 1 点の下に位置します。 このような分布の場合、このメソッドはデータを分割するときに、複数の領域に均等に分離しようとします。 これにより、データが不適切に表示されます。|  
  
## <a name="remarks"></a>コメント  
  
-   `EQUAL_AREAS` メソッドを使用すると、文字列を分離できます。  
  
-   `CLUSTERS` メソッドでは、ランダム サンプルとして 1,000 個のレコードを使用してデータの分離が行われます。 アルゴリズムでデータをサンプリングしない場合は、`EQUAL_AREAS` メソッドを使用します。  
  
-   ニューラル ネットワーク マイニング モデルのチュートリアルには、分離をカスタマイズする例が示されています。 詳細については、次を参照してください。[レッスン 5。ニューラル ネットワーク モデルとロジスティック回帰モデルを構築&#40;中級者向けデータ マイニング チュートリアル&#41;](../../tutorials/lesson-5-build-models-intermediate-data-mining-tutorial.md)します。  
  
## <a name="see-also"></a>参照  
 [コンテンツの種類 &#40;です。 データ マイニング&#41;](content-types-data-mining.md)   
 [コンテンツの種類 &#40;DMX&#41;](/sql/dmx/content-types-dmx)   
 [データ マイニング アルゴリズム &#40;Analysis Services - データ マイニング&#41;](data-mining-algorithms-analysis-services-data-mining.md)   
 [マイニング構造 &#40;Analysis Services - データ マイニング&#41;](mining-structures-analysis-services-data-mining.md)   
 [データ型 (データ マイニング)](data-types-data-mining.md)   
 [マイニング構造列](mining-structure-columns.md)   
 [列の分布 (データ マイニング)](column-distributions-data-mining.md)  
  
  
