---
title: Visio (データ マイニング アドイン) でのデータ マイニング モデルの表示 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- diagram, modifying
- templates [Visio]
- shapes, data mining
- diagram
ms.assetid: 5841adea-6650-4fae-8526-26af33edbede
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c287e840c07d11a527e980f9f07fb39fb3852739
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66065519"
---
# <a name="viewing-data-mining-models-in-visio-data-mining-add-ins"></a>Visio でのデータ マイニング モデルの参照 (データ マイニング アドイン)
  データ マイニング用 Visio 図形は、サーバーに接続して、既存のデータ マイニング モデルを表すダイアグラムを作成します。 ダイアグラムは、Visio のコントロールを使用してカスタマイズできますが、データのドリル ダウン、基になる統計の公開、基になるモデルの操作もすることができます。  
  
## <a name="building-a-model-diagram"></a>モデル ダイアグラムの作成  
 データ マイニング用 Visio 図形を含むファイルを開くと、**図形**ウィンドウには、次の図形が表示されます。  
  
 Visio を開いたときにデータ マイニング図形が表示されない場合は、インストール フォルダーにあるテンプレート ファイルを開きます。  
  
 ![DM](media/dm-stencil.gif "DM")  
  
 図形を使用するには、図形をページにドラッグします。 図形ごとに異なるウィザードが起動されます。ウィザードに従って、ソース データを選択し、そのダイアグラムに必要なオプションを設定します。さらに、網掛けやその他の表示オプションを指定します。  
  
 次の表は、ダイアグラムの種類とそれぞれに使用できるモデルの種類を示しています。  
  
|Visio 図形|サポートされているモデル|  
|-----------------|----------------------|  
|[デシジョン ツリー]|この図形はデシジョン ツリー アルゴリズムまたは線形回帰アルゴリズムに基づくモデルに使用します。|  
|依存関係ネットワーク|次のアルゴリズムに基づくモデルには、この図形を使用します。Naive Bayes、デシジョン ツリー、またはアソシエーション ルール。|  
|クラスター|この図形はクラスタリング アルゴリズムに基づくモデルに使用します。|  
  
 マイニング モデルのデータの種類に応じて、ウィザードに表示されるオプションも異なります。 たとえば、連続する数値を含む列はカテゴリ変数とは異なる方法で視覚化されます。  
  
## <a name="working-with-completed-shapes"></a>完成した図形の操作  
 ダイアグラムが完成したら、それを使用してデータ マイニング モデルを参照したり、プレゼンテーションで使用できるように強化したりできます。  
  
### <a name="visio-menus"></a>Visio のメニュー  
 Visio には、ダイアグラムの強化に役立つさまざまな描画コントロール、配色テーマ、ショートカット メニューが用意されています。  
  
-   Visio のテーマを使用してダイアグラムの色を変更します。  
  
-   コネクタまたはダイアグラムのレイアウトを変更します。  
  
### <a name="data-mining-menus"></a>データ マイニングのメニュー  
 これらのツール バーとメニュー項目は、各図形またはモデルの種類に固有のアドインによって提供されます。  
  
-   それぞれのダイアグラムの種類には図形のショートカット メニューがあり、これを使用すると特殊なオプションにアクセスできます。 このメニューで、多くのオプションは、すべての Visio 図形に共通する、いくつかのオプションは、データ マイニング テンプレートに固有  
  
     たとえば、デシジョン ツリー ダイアグラムにおいて、個々のノードをクリックし、その子ノードを折りたたむと、ダイアグラムを単純化できます。また、子ノードを別のページに移動することもできます。  
  
-   図形はモデル データにバインドされているため、ダイアグラムを使用してある程度の操作も実行できます。  
  
     表示されるノードをフィルター処理する、グラフのツリーのレベルまたは深さを変更する。  
  
     特定のセクションを拡大する、特定の属性を含んでいるノードを検索する、または依存グラフをそのエッジ (確率) でフィルター処理する。  
  
## <a name="walkthroughs"></a>チュートリアル  
 完成したダイアグラムを操作および解釈する方法の例については、次のトピックを参照してください。  
  
 [クラスター ダイアグラムのチュートリアル](cluster-diagram-walkthrough-data-mining-add-ins.md)  
  
 [依存関係ネットワーク ダイアグラムのチュートリアル](dependency-network-diagram-walkthrough-data-mining-add-ins.md)  
  
 [デシジョン ツリー ダイアグラムのチュートリアル](decision-tree-diagram-walkthrough-data-mining-add-ins.md)  
  
## <a name="see-also"></a>参照  
 [Excel におけるモデルの参照&#40;SQL Server データ マイニング アドイン&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md)  
  
  
