---
title: 分類ウィザード (データ マイニング Excel 用アドイン) |Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data modeling [data mining]
- classification [data mining]
ms.assetid: 409c5076-c4c3-4f09-8f30-d3297df45f13
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a62d937a733ea41b85a83224a043ff4ad7ecdd29
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66087933"
---
# <a name="classify-wizard-data-mining-add-ins-for-excel"></a>分類ウィザード (Excel 用データ マイニング アドイン)
  ![データ マイニング リボンの分類ウィザード](media/dmc-classify.gif "データ マイニング リボンの分類ウィザード")  
  
 **分類**ウィザードを使用して、Excel テーブル、Excel 範囲、または外部データ ソースの既存のデータに基づいて分類モデルを構築できます。  
  
 分類モデルはデータから共通のパターンを抽出します。そのため、分類モデルを使用すると、グループ化された値に基づいて予測を行うことができます。 たとえば、分類モデルを使用して、収入パターンまたは支出パターンに基づくリスクを予測できます。  
  
## <a name="using-the-classify-wizard"></a>分類ウィザードの使用  
  
1.  **データ マイニング**リボンで、をクリックして**分類**、 をクリックし、**次**。  
  
2.  **ソース データの選択** ページで、分析するデータを選択します。  
  
     このウィザードは、複数の種類のデータをサポートしています。Excel テーブル、Excel 範囲、および外部データ ソース。 外部データを使用する場合、外部データを Excel に追加するか、Analysis Services データ ソース内の一連のテーブルまたはビューを選択することができます。 また、テーブルを追加したり列を変更したりして、アドホック データ ソースを作成することもできます。  
  
3.  **分類** ページで、分類する列を選択します。  
  
     一覧で、列を確認**入力列**、一意の値があり、ID 番号、顧客名などのパターンを作成するために適さない列の選択を解除して、具合です。 また、実質的に分類可能な列と重複する列も削除する必要があります。  
  
     たとえば、製品カテゴリの予測を分類する場合、既知のビジネス ルールがある場合はサブカテゴリ フィールドを除外する必要があります。そうしないと、そのルールの強度によって、他の相関関係を発見できなくなる場合があります。  
  
4.  必要に応じてクリックして**パラメーター**アルゴリズム パラメーターを変更し、クラスタ リング モデルの動作をカスタマイズします。  
  
5.  **データをトレーニング セットとテスト セットに分割**ページで、テスト保持するためにデータの量を指定します。 残りのデータは、常にモデルのトレーニングに使用されます。  
  
     既定の設定では、30% がテスト データ、70% がトレーニング データです。  
  
6.  **完了**ページで、データ セットと、モデルのわかりやすい名前を指定し、完成したモデルを使用する方法を制御する次のオプションを設定します。  
  
    -   **モデルの参照**します。 このオプションを選択すると、ウィザードとすぐ、モデルの処理が完了すると表示されます、**参照** ウィンドウに結果を検証してください。 ビューアーの内容は、構築したモデルの種類によって異なります。 詳細については、次を参照してください。[デシジョン ツリー モデルの参照](browsing-a-decision-trees-model.md)と[ニューラル ネットワーク モデルの参照](browsing-a-neural-network-model.md)します。  
  
    -   **ドリルスルーを有効にする**します。 このチェック ボックスをオンにすると、完成したモデルから基になるデータを表示できます。 このオプションは、デシジョン ツリー モデルを構築する場合にのみ使用できます。  
  
    -   **一時的なモデルを使用する**します。 このチェック ボックスをオンにすると、モデルがサーバーに保存されません。 一時的なモデルは、Excel の終了時に削除されます。  
  
## <a name="more-about-classification-models"></a>分類モデルの詳細  
 **アルゴリズム パラメーター**ダイアログ ボックスで、Analysis Services で提供されるこれらのアルゴリズムから分類方法も選択できます。  
  
-   Microsoft デシジョン ツリー  
  
-   Microsoft ロジスティック回帰  
  
-   Microsoft Naïve Bayes  
  
-   Microsoft ニューラル ネットワーク  
  
 複数のアルゴリズムで同様の結果が生じる場合がありますが、アルゴリズムによってデータの分析方法は異なるため、いくつかのアルゴリズムを試して結果を比較することをお勧めします。 既定の方法は、Microsoft デシジョン ツリーです。  
  
 **パラメーター**一覧で、高度なオプションは、選択したアルゴリズムの種類に依存を変更することができます。 各アルゴリズムのパラメーターについては、SQL Server オンライン ブックで詳しく説明します。  
  
 [Microsoft デシジョン ツリー アルゴリズム テクニカル リファレンス](data-mining/microsoft-decision-trees-algorithm-technical-reference.md)  
  
 [Microsoft ロジスティック回帰アルゴリズム テクニカル リファレンス](data-mining/microsoft-logistic-regression-algorithm-technical-reference.md)  
  
 [Microsoft Naive Bayes アルゴリズム テクニカル リファレンス](data-mining/microsoft-naive-bayes-algorithm-technical-reference.md)  
  
 [Microsoft ニューラル ネットワーク アルゴリズム テクニカル リファレンス](data-mining/microsoft-neural-network-algorithm-technical-reference.md)  
  
### <a name="requirements"></a>必要条件  
 使用する、**分類**ウィザード、する必要がありますに接続する、[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]データベース。 接続を作成する方法については、次を参照してください。[ソース データへの接続&#40;Excel 用データ マイニング クライアント&#41;](connect-to-source-data-data-mining-client-for-excel.md)します。  
  
## <a name="see-also"></a>参照  
 [データ マイニング モデルの作成](creating-a-data-mining-model.md)  
  
  
