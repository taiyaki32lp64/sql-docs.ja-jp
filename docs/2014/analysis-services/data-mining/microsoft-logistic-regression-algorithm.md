---
title: Microsoft ロジスティック回帰アルゴリズム |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- logical regression algorithms [Analysis Services]
- algorithms [data mining]
- neural network algorithms [Analysis Services]
- regression algorithms [Analysis Services]
ms.assetid: 3dd54d07-1c3b-4b87-b7f0-b962ed8cf844
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 14e86ac2dd32f2a3e1384e08aca597794ee4bc71
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66083955"
---
# <a name="microsoft-logistic-regression-algorithm"></a>Microsoft ロジスティック回帰アルゴリズム
  ロジスティック回帰は、バイナリ結果のモデリングに使用される代表的な統計手法です。  
  
 ロジスティック回帰は、異なる学習技法を使用してさまざまな方法で統計研究に実装されます。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] ロジスティック回帰アルゴリズムは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] ニューラル ネットワーク アルゴリズムの一種を使用して実装されました。 このアルゴリズムは、ニューラル ネットワークの特性の多くを共有しますが、トレーニングはニューラル ネットワークよりも容易です。  
  
 ロジスティック回帰の利点の 1 つは、このアルゴリズムはあらゆる種類の入力を取得するほど柔軟性が高く、次に示すいくつかの分析タスクをサポートすることです。  
  
-   人口統計を使用して、特定の病気のリスクなど、結果に関する予測を行う。  
  
-   結果に影響する要素を探索し、重み付けを行う。 たとえば、顧客が店舗を繰り返し訪れる要因となる要素を求める。  
  
-   多くの属性を持つドキュメント、電子メール、またはその他のオブジェクトを分類する。  
  
## <a name="example"></a>例  
 類似の人口統計情報を共有し、Adventure Works 社から製品を購入する人々のグループがあるとします。 データをモデリング特定の結果 (対象製品の購入など) に関連付けると、人工統計情報が人々の対象製品を購入する確率にどのようにかかわるかを確認できます。  
  
## <a name="how-the-algorithm-works"></a>アルゴリズムの動作  
 ロジスティック回帰は、結果のペアに対する複数の要素の影響を確認するために使用される代表的な統計手法です。 Microsoft による実装では、変更されたニューラル ネットワークを使用して入力と出力の関係をモデル化します。 出力における各入力の影響が評価され、完成したモデルではさまざまな入力が重み付けされます。 ロジスティック回帰という名前は、極端な値の影響を最小限に抑えるためにロジスティック変換を使用してデータ曲線が圧縮されるという事実に基づいています。 実装の詳細とアルゴリズムのカスタマイズ方法については、「 [Microsoft ロジスティック回帰アルゴリズム テクニカル リファレンス](microsoft-logistic-regression-algorithm-technical-reference.md)」を参照してください。  
  
## <a name="data-required-for-logistic-regression-models"></a>ロジスティック回帰モデルに必要なデータ  
 ロジスティック回帰モデルのトレーニングに使用するデータを用意する際には、必要なデータ量やデータの使用方法など、このアルゴリズムにおける要件を把握しておいてください。  
  
 ロジスティック回帰モデルの要件は次のとおりです。  
  
 **単一キー列** : それぞれのモデルには、各レコードを一意に識別する数値列またはテキスト列が 1 つ含まれている必要があります。 複合キーは使用できません。  
  
 **入力列** : 各モデルには、分析の要素として使用される値が含まれた入力列が 1 つ以上必要です。 入力列はいくつあってもかまいませんが、各列内の値の数によっては、列を追加するとモデルのトレーニングにかかる時間が長くなる場合があります。  
  
 **1 つ以上の予測可能列** : モデルには、連続する数値データを含む任意のデータ型の予測可能列が 1 つ以上必要です。 予測可能列の値は、モデルへの入力として扱うことも、予測のみに使用するよう指定することもできます。 入れ子になったテーブルは予測可能列では使用できませんが、入力としては使用できます。  
  
 ロジスティック回帰モデルでサポートされるコンテンツの種類とデータ型の詳細については、「 [Microsoft ロジスティック回帰アルゴリズム テクニカル リファレンス](microsoft-logistic-regression-algorithm-technical-reference.md)」の「必要条件」を参照してください。  
  
## <a name="viewing-a-logistic-regression-model"></a>ロジスティック回帰モデルの表示  
 モデルを参照するには、Microsoft ニューラル ネットワーク ビューアーまたは Microsoft 汎用コンテンツ ツリー ビューアーを使用できます。  
  
 Microsoft ニューラル ネットワーク ビューアーを使用してモデルを表示すると、Analysis Services には、特定の結果に影響する要素がその重要度で順位付けされて表示されます。 比較する属性と値を選択できます。 詳細については、「 [Microsoft ニューラル ネットワーク ビューアーを使用したモデルの参照](browse-a-model-using-the-microsoft-neural-network-viewer.md)」を参照してください。  
  
 さらに詳細を知るには、Microsoft 汎用コンテンツ ツリー ビューアーを使用してモデルの詳細を参照できます。 ロジスティック回帰モデルのモデル コンテンツには、モデルに使用されるすべての入力を示すマージナル ノード、および予測可能な属性を表すサブネットワークが含まれます。 詳細については、「[ロジスティック回帰モデルのマイニング モデル コンテンツ &#40;Analysis Services - データ マイニング&#41;](mining-model-content-for-logistic-regression-models.md)」を参照してください。  
  
## <a name="creating-predictions"></a>予測の作成  
 モデルのトレーニング後、モデル コンテンツに対するクエリを作成して回帰係数およびその他の詳細を取得したり、モデルを使用して予測を作成したりできます。  
  
-   データ マイニング モデルに対するクエリの作成方法については、「 [データ マイニング クエリ](data-mining-queries.md)」を参照してください。  
  
-   ロジスティック回帰モデルでのクエリの例については、「 [クラスタリング モデルのクエリ例](clustering-model-query-examples.md)」を参照してください。  
  
## <a name="remarks"></a>コメント  
  
-   ドリルスルーはサポートされていません。 これは、マイニング モデルのノードの構造がその基になるデータと必ずしも直接対応しているわけではないからです。  
  
-   データ マイニング ディメンションの作成はサポートされていません。  
  
-   OLAP マイニング モデルの使用がサポートされています。  
  
-   Predictive Model Markup Language (PMML) を使用したマイニング モデルの作成はサポートされていません。  
  
## <a name="see-also"></a>参照  
 [ロジスティック回帰モデルのマイニング モデル コンテンツ (Analysis Services - データ マイニング)](mining-model-content-for-logistic-regression-models.md)   
 [Microsoft ロジスティック回帰アルゴリズム テクニカル リファレンス](microsoft-logistic-regression-algorithm-technical-reference.md)   
 [ロジスティック回帰モデルのクエリ例](logistic-regression-model-query-examples.md)  
  
  
