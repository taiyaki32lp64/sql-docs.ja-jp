---
title: 予測 (中級者向けデータ マイニング チュートリアル) のソース ビューのデータの追加 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 2665040a-1291-4064-ba01-f458637dda57
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: f60ea2b2a642cf9435ed8366c42e43abb927e426
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62823132"
---
# <a name="adding-a-data-source-view-for-forecasting-intermediate-data-mining-tutorial"></a>予測用のデータ ソース ビューの追加 (中級者向けデータ マイニング チュートリアル)
  この作業では、予測シナリオに使用するデータ ソース ビューを追加します。 予測モデルでは、時系列内のステップを識別するための列がデータに含まれている必要があります。 複数の系列のデータを分析する場合は、すべての系列が終了する日付または時間ステップが同じである必要があります。  
  
### <a name="to-add-a-data-source-view"></a>データ ソース ビューを追加するには  
  
1.  ソリューション エクスプ ローラーで右クリックして**データ ソース ビュー**、し、**新しいデータ ソース ビュー**します。  
  
2.  **[データ ソース ビュー ウィザードへようこそ]** ページで **[次へ]** をクリックします。  
  
3.  **データ ソースの選択**] ページ [**リレーショナル データ ソース**を選択、[!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]データ ソース。 **[次へ]** をクリックします。  
  
    > [!NOTE]  
    >  内のデータ ソースを作成する手順を見つけることができる場合、このデータ ソースはありません、 [Basic Data Mining Tutorial](../../2014/tutorials/basic-data-mining-tutorial.md)します。  
  
4.  **テーブルおよびビュー**ページで vTimeSeries (dbo) テーブルを選択し、データ ソース ビューに追加する、右矢印をクリックします。  
  
5.  **[次へ]** をクリックします。  
  
6.  **ウィザードの完了** ページで、既定では、データ ソース ビューの名前は[!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)]します。 名を変更して**SalesByRegion**、 をクリックし、**完了**します。  
  
     データ ソース ビュー デザイナーが開き、 **SalesByRegion**データ ソース ビューが表示されます。  
  
## <a name="working-with-the-data-source-view"></a>データ ソース ビューの使用  
 データ ソース ビューを作成したら、次の方法でデータを検証できます。  
  
-   デザイナーで vTimeSeries テーブルを右クリックして**データの探索**をグリッドで選択したテーブルを開きます。  
  
-   クリックして**サンプリング オプション**しを使用して、**データ探索オプション**ダイアログ ボックスのサンプリング メソッドを変更します。 クリックして**更新**新しいオプションの設定を使用してテーブルにデータを読み込みます。 たとえば、サンプルでは、出力または上位 n 行を選択する行の数を指定できます。  
  
-   VTimeSeries テーブルを右クリックして**プロパティ**テーブルに新しい名前を指定します。 データ ソース ビューから個々の列を選択して、列のプロパティを変更することもできます。  
  
-   データ ソース ビューのデザイン領域の任意の場所をクリックして、新しいクエリの作成と名前の割り当て、テーブル間のリレーションシップの作成、デザイン領域のレイアウトの変更を行います。  
  
-   テーブルを右クリックして**新しい名前付き計算**集計などの派生列を作成します。 また、このビューではデータ ソースから新しいテーブルやビューを追加することもできます。  
  
 次の作業では、時系列データについて学習し、時系列識別子として使用するのに最適な列を決定します。 時系列データのギャップを処理する方法についても学習します。  
  
## <a name="next-task-in-lesson"></a>このレッスンの次の作業  
 [モデルの時系列の要件について&#40;中級者向けデータ マイニング チュートリアル&#41;](../../2014/tutorials/time-series-model-requirements-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>参照  
 [Microsoft タイム シリーズ アルゴリズム](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm.md)  
  
  
