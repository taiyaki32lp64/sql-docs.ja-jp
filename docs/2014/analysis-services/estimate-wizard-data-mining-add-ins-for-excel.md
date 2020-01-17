---
title: 推定ウィザード (データ マイニング Excel 用アドイン) |Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data modeling [data mining]
- estimation
ms.assetid: 7f2b1d5f-c9b3-4939-b35a-34ae099af15f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9b7ffc1b77d90946a119dc462da2057cf3fe4988
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66081251"
---
# <a name="estimate-wizard-data-mining-add-ins-for-excel"></a>推定ウィザード (Excel 用データ マイニング アドイン)
  ![データ マイニング リボンの推定ウィザード](media/dmc-estimate.gif "データ マイニング リボンの推定ウィザード")  
  
 **見積もり**ウィザードを使用して、推定モデルを作成できます。 推定モデルは、データからパターンを抽出し、そのパターンを使用して結果に影響を与える要因を予測します。  
  
 推定は数値の結果を予測するために使用されます。 たとえば、教育機関の卒業率をパーセンテージで表した値が対象列に格納されている場合、教育機関ごとの生徒数、生徒と教員の比率、教員数など、卒業率の増減に関係する可能性がある要因を分析できます。  
  
## <a name="using-the-estimate-data-wizard"></a>データ推定ウィザードの使用  
  
1.  **データ マイニング**リボンで、をクリックして**見積もり**します。  
  
2.  **ソース データの選択** ダイアログ ボックスを使用するソース データを選択します。 データを使用するには、Excel で**テーブル**、Excel**データ範囲**、または、**外部データ ソース**します。  
  
     外部データ ソースを使用する場合、カスタム ビューまたはカスタム クエリを作成し、それを [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] データ ソースとして保存できます。  
  
3.  **推定**ダイアログ ボックスで、**を分析する列**します。  
  
     対象列には、連続する数値データが格納されている必要があります。  
  
4.  チェックして、入力として使用する列の選択、**入力列**チェック ボックスをオンします。  
  
     選択した列は、パターンの作成に使用されます。 分析には不要と思われる ID 番号などの列や、分析とは無関係なデータを含んだ列は、除外する必要があります。  
  
5.  **見積もり**ウィザードは、データ セットに最適なアルゴリズムを選択します。 ただし、クリックして**パラメーター**を開く、**アルゴリズム パラメーター** ] ダイアログ ボックスと [詳細オプションを設定します。  
  
6.  データが数値で、Microsoft 線形回帰メソッドを使用する場合は、確認、**リグレッサー**知る (または疑いが強い) 数値列のボックスに予測可能な値が関連付けられます。  
  
     そうすると、アルゴリズムによって、その列の値がテストされ、値が出力に影響するかどうかが判断されます。 不明な場合にクリックします**提案**アルゴリズムはすべての列をテストし、リグレッサーとして使用する最適な値を自動的に検出するとします。  
  
    > [!NOTE]  
    >  推定を作成するにはリグレッサーが必要です。 ウィザードでは、データに対する最初のパスに基づいて、常に最適なリグレッサーが提示されます。 このため、どれを選択すればよいかわからない場合は、推奨された選択内容を使用することをお勧めします。  
  
7.  **データをトレーニング セットとテスト セットに分割** ページで、テスト用データの小さなサブセットを作成するかどうかを指定します。  
  
8.  **完了**ページで、新しいマイニング構造とマイニング モデルの名前を指定するか、用意されている既定の名前。  
  
9. モデルを使用するためのオプションを設定します。  
  
    -   選択**参照**を直ちにビューアーでモデルを開きます。  
  
         このグラフィカルなビューアーには、依存関係ネットワーク グラフやアルゴリズムによって生成されたデジション ツリーなどが表示されます。 この情報を調査することで、推測値をもたらした要因をより深く理解できます。  
  
    -   選択**ドリルスルーを有効にする**のしてもらうために、分析が基になるデータを表示します。  
  
         このオプションを使用できるのは、デシジョン ツリー アルゴリズムまたは線形回帰アルゴリズムを使用する場合だけです。  
  
    -   **一時的なモデルを使用する**します。 このチェック ボックスをオンにすると、モデルがサーバーに保存されません。 一時的なモデルは、Excel の終了時に削除されます。  
  
## <a name="more-about-estimation-models"></a>推定モデルの詳細  
 **見積もり**ウィザードには、次のアルゴリズムのいずれかの使用がサポートされています。  
  
-   Microsoft デシジョン ツリー アルゴリズム  
  
-   Microsoft 線形回帰アルゴリズム  
  
-   Microsoft ロジスティック回帰アルゴリズム  
  
-   Microsoft Neural network アルゴリズム  
  
 **アルゴリズム パラメーター**ダイアログ ボックスで、選択したアルゴリズムに応じて、追加の高度なオプションを設定することができます。 各アルゴリズムのオプションの詳細については、SQL Server オンライン ブックの次のトピックを参照してください。  
  
 [Microsoft デシジョン ツリー アルゴリズム テクニカル リファレンス](data-mining/microsoft-decision-trees-algorithm-technical-reference.md)  
  
 [Microsoft 線形回帰アルゴリズム テクニカル リファレンス](data-mining/microsoft-linear-regression-algorithm-technical-reference.md)  
  
 [Microsoft ロジスティック回帰アルゴリズム テクニカル リファレンス](data-mining/microsoft-logistic-regression-algorithm-technical-reference.md)  
  
 [Microsoft ニューラル ネットワーク アルゴリズム テクニカル リファレンス](data-mining/microsoft-neural-network-algorithm-technical-reference.md)  
  
### <a name="requirements"></a>要件  
 データ推定ウィザードを使用するには、[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] データベースに接続する必要があります。  
  
 接続を作成する方法については、次を参照してください。[ソース データへの接続&#40;Excel 用データ マイニング クライアント&#41;](connect-to-source-data-data-mining-client-for-excel.md)します。  
  
 推定アルゴリズムを使用するには、予測しようとしている結果を、通貨、売上高、日付、時刻などの数値で表す必要があります。  
  
## <a name="see-also"></a>参照  
 [データ マイニング モデルを作成します。](creating-a-data-mining-model.md)   
 [デシジョン ツリー ダイアグラムのチュートリアル&#40;データ マイニング アドイン&#41;](decision-tree-diagram-walkthrough-data-mining-add-ins.md)  
  
  
