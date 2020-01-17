---
title: 探索とデータのクリーニング |Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 7c888c95-8986-461e-9f11-2395044b9d97
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 79d356aa1b14ac30ba5bc9a8f579fc66ddebea92
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66081266"
---
# <a name="exploring-and-cleaning-data"></a>データの探索とクリーニング
  データの準備は、データのクレンジングよりはるかに大きな概念です。 データの準備方法によって、最終的な結果の解釈も影響を受けることを忘れないでください。 データの準備には、次のようなタスクがあります。  
  
-   データの分布を探索し確認します。  
  
-   不良レコードをクリーニングして、データ マイニング用の列を選択します。  
  
-   null 値を適切に処理します。  
  
-   異なる期間によって、値のビン分割または値の集計を実行します。  
  
-   ラベルを追加して、結果を使いやすくします。  
  
-   分析の必要に応じて、データ型の変換または値のカテゴリ分類を実行します。  
  
 データ モデリングについて詳しくない場合は、関連トピック「[データ マイニングの準備のチェック リスト](checklist-of-preparation-for-data-mining.md)」を参照することをお勧めします。  
  
## <a name="data-preparation-tools"></a>データ準備ツール  
 Office 用データ マイニング アドインには、データのクレンジングおよび準備を行う次のツールが含まれています。  
  
### <a name="explore-data"></a>データの探索  
 次のデータ準備タスクを行うには、**データの探索**ウィザードを使用します。  
  
-   データをプレビューし、分析前に解決する必要のあるエラーを特定します。  
  
-   データのバランスと必要なクリーンアップ タスクを理解するうえで役に立つ統計情報を収集します。  
  
-   分析に役立つ列を特定し、データ モデリング フェーズを計画します。  
  
 [データの探索 &#40;SQL Server データ マイニング アドイン&#41;](explore-data-sql-server-data-mining-add-ins.md)。  
  
### <a name="detect-and-handle-outliers"></a>外れ値の検出と処理  
 **外れ値**ウィザードを使用して、データ内の値の分布をグラフ化し、極端な値を削除できます。 次のデータ準備タスクを行うには、**外れ値**ツールを使用します。  
  
-   データで検出されたパターンに基づいて、個々の値が信頼できるかどうかを判断します。  
  
-   通常とは異なる値を確認し、それらを削除または置換します。  
  
-   モデルを特定の値の範囲にスコープします。 たとえば、特定の店舗に外れ値があることが判明している場合は、その値を除去することで、より正確に他の店舗の値を予測するモデルを取得することができます。  
  
 [外れ値 &#40;SQL Server データ マイニング アドイン&#41;](outliers-sql-server-data-mining-add-ins.md)。  
  
### <a name="relabel-and-bin-data"></a>データのラベル変更とビン分割  
 **ラベルの変更**ウィザードでは、データのラベルを変更できるように、データが値でグループ化されます。 次のデータ準備タスクを行うには、ラベルの変更ツールを使用します。  
  
-   調査結果で使用されている数値コードを、そのコードの意味を示すテキストに変更します。  
  
     たとえば、"性別 = 1" を "性別 = 女性" に置き換えるなど、データ エントリを置き換えることができます。  
  
-   数値の範囲を表すグループを作成することで、データをビン分割します。  
  
     ラベルが付いたなど、Income 列の数値を置換するなど、**収入 - モデレートする**と**収入 - 高**します。  
  
-   不連続値をカテゴリに分類して集約します。  
  
     たとえば、購入のパターンを検出するには個別の製品が多すぎる場合、製品をより幅広いカテゴリに割り当てることができます。  
  
 [ラベルの変更&#40;SQL Server データ マイニング アドイン&#41;](relabel-sql-server-data-mining-add-ins.md)  
  
### <a name="cleanse-data"></a>データのクレンジング  
 データ クレンジングでは、さまざまな処理が行われ、そのほとんどがアドインによってサポートされています。  
  
-   NULL 値を識別して、それを実際の値に変更するか、`Missing` 値として処理するかを決定します。  
  
-   不足値を検出して削除するか、平均値や NULL などの適切な値を帰属させます。  
  
 [データの探索&#40;SQL Server データ マイニング アドイン&#41;](explore-data-sql-server-data-mining-add-ins.md)  
  
 [ラベルの変更&#40;SQL Server データ マイニング アドイン&#41;](relabel-sql-server-data-mining-add-ins.md)  
  
 [例の全体適用](fill-from-example-table-analysis-tools-for-excel.md)  
  
### <a name="sample-data"></a>サンプル データ  
 サンプル データ ウィザードでは、モデルのトレーニングとテストに使用する均衡の取れたデータ セットを 2 つの方法で作成できます。  
  
-   **ランダムにサンプリングします。** トレーニングやテストに使用するために、大きなデータ セットから対応するデータ セットを抽出する場合にこのオプションを使用します。 データ マイニング アドインでは、*階層化されたサンプリング*を使用して、サンプリングされた各変数に対してバランスの取れた値のセットが取得されるようにします。  
  
-   **オーバー サンプリングします。** 対象となる結果に対してデータが不足しており、そのデータにより重みを付ける必要がある場合にこのオプションを使用します。 たとえば、詐欺行為は比較的まれにしか発生しませんが、詐欺行為に関連するケースをオーバーサンプリングして、モデリングするための最適化データを取得できます。  
  
 [サンプル データ &#40;SQL Server データ マイニング アドイン&#41;](sample-data-sql-server-data-mining-add-ins.md)。  
  
## <a name="see-also"></a>参照  
 [データ マイニング モデルを作成します。](creating-a-data-mining-model.md)   
 [モデルの検証と予測用モデルの使用&#40;データ マイニング Excel 用アドイン&#41;](validating-models-and-using-models-for-prediction-data-mining-add-ins-for-excel.md)   
 [展開して、マイニング モデルのスケーリング&#40;データ マイニング Excel 用アドイン&#41;](deploying-and-scaling-mining-models-data-mining-add-ins-for-excel.md)  
  
  
