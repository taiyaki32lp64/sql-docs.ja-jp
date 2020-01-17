---
title: Microsoft ニューラル ネットワーク アルゴリズム |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- training neural networks
- output neurons [Analysis Services]
- algorithms [data mining]
- neural network algorithms [Analysis Services]
- neurons [Analysis Services]
- classification algorithms [Analysis Services]
- neural networks
- multilayer perceptron network of neurons [Analysis Services]
- hidden neurons
- Back-Propagated Delta Rule network
- input neurons [Analysis Services]
- regression algorithms [Analysis Services]
ms.assetid: 61eb4861-8a6a-4214-a4b8-1dd278ad7a68
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a7330fab8b4c0ecdff296e0daa5e529442fd8b94
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66083868"
---
# <a name="microsoft-neural-network-algorithm"></a>Microsoft Neural Network Algorithm
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]、[!INCLUDE[msCoName](../../includes/msconame-md.md)]ニューラル ネットワーク アルゴリズムは、予測可能な属性の考えられる各状態の入力属性の考えられる各状態を結合し、トレーニング データを使用して確率を計算します。 これらの確率は、分類や回帰で使用することも、入力属性に基づいて予測属性の結果を予測するために使用することもできます。  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] ニューラル ネットワーク アルゴリズムで作成されたマイニング モデルには、入力と予測の両方に使用する列の数または予測のみに使用する列の数に応じて、複数のネットワークを含めることができます。 1 つのマイニング モデルに含まれるネットワークの数は、マイニング モデルで使用される入力列および予測可能列に含まれる状態の数によって異なります。  
  
## <a name="example"></a>例  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] ニューラル ネットワーク アルゴリズムは、製造または商業活動などからの複雑な入力データの分析や、大量のトレーニング データが利用できるが他のアルゴリズムではルールを簡単に導き出すことができない業務上の問題の分析に役立ちます。  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] ニューラル ネットワーク アルゴリズムを使用する推奨シナリオは次のとおりです。  
  
-   ダイレクト メール宣伝やラジオ広告キャンペーンの成功度の測定など、マーケティングおよび宣伝に関する分析  
  
-   履歴データからの、株価の動向、通貨の騰落、その他の流動性の高い金融情報の予測  
  
-   製造および工業プロセスに関する分析  
  
-   テキスト マイニング  
  
-   多数の入力と比較的少数の出力間の複雑なリレーションシップを分析する予測モデル。  
  
## <a name="how-the-algorithm-works"></a>アルゴリズムの動作  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] ニューラル ネットワーク アルゴリズムは、最大 3 層のニューロンで構成されるネットワークを作成します。 これらの層は、入力層、オプションの非表示層、および出力層です。  
  
 **入力層:** 入力ニューロンは、データ マイニング モデル、およびそれらの確率のすべての入力属性値を定義します。  
  
 **非表示層:** 非表示ニューロンは入力ニューロンから入力を受け取り、出力ニューロンに出力を渡します。 非表示層では、入力のさまざまな確率に重みが割り当てられます。 重みは、非表示ニューロンに対する特定の入力の関連性または重要性を表します。 入力に割り当てられている重みが大きいほど、その入力の値の重要性が増加します。 重みには負の値も使用できます。これは、その入力によって特定の結果が優先されるのではなく、抑制されることを意味します。  
  
 **出力層:** 出力ニューロンは、データ マイニング モデルの予測可能属性値を表します。  
  
 入力層、非表示層、および出力層の作成方法およびスコア計算方法の詳細については、「 [Microsoft Neural Network Algorithm Technical Reference](microsoft-neural-network-algorithm-technical-reference.md)」を参照してください。  
  
## <a name="data-required-for-neural-network-models"></a>ニューラル ネットワーク モデルに必要なデータ  
 ニューラル ネットワーク モデルには、単一のキー列、1 つ以上の入力列、および 1 つ以上の予測可能列が必要です。  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] ニューラル ネットワーク アルゴリズムを使用するデータ マイニング モデルは、アルゴリズムで使用できるパラメーターに対して指定した値の影響を強く受けます。 パラメーターでは、データのサンプリング方法、各列へのデータの分散方法またはデータの分散が必要になる状況、および最終的なモデルで使用される値を制限するために機能選択を呼び出すタイミングを定義します。  
  
 モデルの動作をカスタマイズするパラメーターを設定する方法の詳細については、「 [Microsoft Neural Network Algorithm Technical Reference](microsoft-neural-network-algorithm-technical-reference.md)」を参照してください。  
  
## <a name="viewing-a-neural-network-model"></a>ニューラル ネットワーク モデルの表示  
 データを操作したり、モデルと入力および出力との関係性を確認したりするには、 **Microsoft ニューラル ネットワーク ビューアー**を使用します。 このカスタム ビューアーを使用すると、入力属性およびその値をフィルター処理することも、出力への影響を示すグラフを参照することもできます。 このビューアーのツールヒントには、入力値と出力値の各ペアに関連付けられている確率とリフトが示されます。 詳細については、「 [Microsoft ニューラル ネットワーク ビューアーを使用したモデルの参照](browse-a-model-using-the-microsoft-neural-network-viewer.md)」を参照してください。  
  
 モデルの構造を参照するには、 **Microsoft 汎用コンテンツ ツリー ビューアー**を使用するのが最も簡単な方法です。 モデルで作成された入力、出力、およびネットワークを表示したり、任意のノードをクリックして展開して入力層ノード、出力層ノード、または非表示層ノードに関連付けられている統計を参照したりできます。 詳細については、「 [Microsoft 汎用コンテンツ ツリー ビューアーを使用したモデルの参照](browse-a-model-using-the-microsoft-generic-content-tree-viewer.md)」を参照してください。  
  
## <a name="creating-predictions"></a>予測の作成  
 モデルの処理が完了したら、各ノード内に格納されているネットワークと重みを使用して予測を作成できます。 ニューラル ネットワーク モデルは、回帰分析、アソシエーション分析、および分類分析をサポートします。そのため、各予測の意味は異なる場合があります。 またモデル自身に対してクエリを実行して、見つかった相関関係を確認することも、関連した統計を取得することもできます。 ニューラル ネットワーク モデルに対するクエリの作成方法の例については、「 [ニューラル ネットワーク モデルのクエリ例](neural-network-model-query-examples.md)」を参照してください。  
  
 データ マイニング モデルに対するクエリの作成方法については、「 [データ マイニング クエリ](data-mining-queries.md)」を参照してください。  
  
## <a name="remarks"></a>コメント  
  
-   ドリル スルーまたはデータ マイニング ディメンションはサポートされていません。 これは、マイニング モデルのノードの構造がその基になるデータと必ずしも直接対応しているわけではないからです。  
  
-   Predictive Model Markup Language (PMML) 形式のモデルの作成はサポートされていません。  
  
-   OLAP マイニング モデルの使用がサポートされています。  
  
-   データ マイニング ディメンションの作成はサポートされていません。  
  
## <a name="see-also"></a>参照  
 [Microsoft Neural Network Algorithm Technical Reference](microsoft-neural-network-algorithm-technical-reference.md)   
 [ニューラル ネットワーク モデルのマイニング モデル コンテンツ (Analysis Services - データ マイニング)](mining-model-content-for-neural-network-models-analysis-services-data-mining.md)   
 [ニューラル ネットワーク モデルのクエリ例](neural-network-model-query-examples.md)   
 [Microsoft ロジスティック回帰アルゴリズム](microsoft-logistic-regression-algorithm.md)  
  
  
