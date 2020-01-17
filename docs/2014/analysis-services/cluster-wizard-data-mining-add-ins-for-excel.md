---
title: クラスター ウィザード (データ マイニング Excel 用アドイン) |Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- clustering [data mining]
ms.assetid: 85b25625-a7ab-4960-9f9c-df22e8ecae37
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d93f676aec67b5d791924cbbda8f71a966d5bbc2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66087807"
---
# <a name="cluster-wizard-data-mining-add-ins-for-excel"></a>クラスター ウィザード (Excel 用データ マイニング アドイン)
  ![クラスター ウィザードでデータ マイニング リボン](media/dmc-cluster.gif "クラスター ウィザードでデータ マイニング リボン")  
  
 クラスター ウィザードでは、似た特性を共有する行を検出し、それらをグループ化してグループ間の距離を最大化するモデルを構築できます。 このウィザードは、あらゆる種類のデータのパターンを検索する場合に有用です。  
  
 クラスター ウィザードは、Microsoft クラスタリング アルゴリズムを使用しており、広範なカスタマイズが可能です。 このウィザードは、Excel テーブル、Excel 範囲、または [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] クエリからの既存のデータで動作します。 によって同様の機能が提供される、[カテゴリの検出](detect-categories-table-analysis-tools-for-excel.md)ツール、Excel 用テーブル分析ツールで提供します。 ただし、カテゴリの検出ツールはカスタマイズできないため、Excel テーブルのデータを使用する必要があります。  
  
## <a name="using-the-cluster-wizard"></a>クラスター ウィザードの使用  
  
1.  データ マイニング リボン**クラスター**、順にクリックします**次**します。  
  
2.  **ソース データの選択**ページで、Excel テーブルまたは範囲を選択します。 または、外部データ ソースを指定します。  
  
     外部データ ソースを使用する場合、カスタム ビューを作成するかカスタム クエリ テキストを貼り付けて、データ セットを [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] データ ソースとして保存できます。  
  
3.  **クラスタ リング** ページで、モデルの構築方法をカスタマイズすることができます。  
  
    -   **セグメント数**、固定数のカテゴリを作成するウィザードの指示またはグループの最適な数を自動的に検出できるようにすることができます。  
  
    -   内の列の一覧を確認、**入力列**一覧、およびパターンの作成には使用できないすべての列の選択を解除します。 除外する必要のある列には、ID 番号や顧客名などがあります。  
  
4.  必要に応じてクリックして**パラメーター**アルゴリズム パラメーターを変更し、クラスタ リング モデルの動作をカスタマイズします。  
  
5.  **データをトレーニング セットとテスト セットに分割**ページで、テスト保持するためにデータの量を指定します。 残りのデータは、常にモデルのトレーニングに使用されます。  
  
     既定の設定では、30% がテスト データ、70% がトレーニング データです。  
  
6.  **完了**ページで、データ セットと、モデルのわかりやすい名前を指定し、完成したモデルを使用する方法を制御する次のオプションを設定します。  
  
    -   **モデルの参照**します。 このオプションを選択すると、ウィザードとすぐ、モデルの処理が完了すると表示されます、**参照** ウィンドウに結果を検証してください。 ビューアーの内容は、構築したモデルの種類によって異なります。 詳細については、次を参照してください。[クラスタ リング モデルの参照](browsing-a-clustering-model.md)します。  
  
    -   **ドリルスルーを有効にする**します。 このチェック ボックスをオンにすると、完成したモデルから基になるデータを表示できます。 このオプションは、デシジョン ツリー モデルを構築する場合にのみ使用できます。  
  
    -   **一時的なモデルを使用する**します。 このチェック ボックスをオンにすると、モデルがサーバーに保存されません。 一時的なモデルは、Excel の終了時に削除されます。  
  
## <a name="more-about-clustering-models"></a>クラスタ リング モデルの詳細  
 クリックして、このウィザードで使用するクラスタ リング アルゴリズムを変更する**詳細設定**を使用して、**アルゴリズム パラメーター**  ダイアログ ボックス。  
  
 Microsoft クラスタリング アルゴリズムには、次のクラスタリング手法が用意されています。  
  
-   K-Means - スケーラブルまたは非スケーリング。  
  
-   Expectation Maximization (EM) - スケーラブルまたは非スケーリング。  
  
 また、CLUSTER_SEED パラメーターを使用して開始値を制御し、同じデータ セットを使用して繰り返されるモデルは常に同じ結果になるようにできます。  
  
### <a name="requirements"></a>要件  
 クラスター ウィザードを使用するには、[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] データベースに接続する必要があります。 詳細については、次を参照してください。[ソース データへの接続&#40;Excel 用データ マイニング クライアント&#41;](connect-to-source-data-data-mining-client-for-excel.md)します。  
  
## <a name="see-also"></a>参照  
 [データ マイニング モデルを作成します。](creating-a-data-mining-model.md)   
 [カテゴリの検出&#40;Excel 用テーブル分析ツール&#41;](detect-categories-table-analysis-tools-for-excel.md)  
  
  
