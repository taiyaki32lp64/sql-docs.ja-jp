---
title: 保存データ マイニングのクエリ結果 ダイアログ ボックス (マイニング モデル予測 ビュー) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dm.savedataminingqueryresult.f1
helpviewer_keywords:
- Save Data Mining Query Result dialog box
ms.assetid: 112fb527-7466-4fd4-9cf1-75596135648f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 97b391e24f98b230dbfe352e0cf1a574c7549984
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66070020"
---
# <a name="save-data-mining-query-result-dialog-box-mining-model-prediction-view"></a>[データ マイニングのクエリ結果を保存] ダイアログ ボックス ([マイニング モデル予測] ビュー)
  **[データ マイニングのクエリ結果を保存]** ダイアログ ボックスを使用すると、新しいテーブルに、データ マイニング クエリの結果を保存できます。  
  
 この新しいテーブルは、データ ソースで定義されたデータベースに作成されます。  
  
## <a name="options"></a>および  
 **Data Source**  
 現在のプロジェクトからデータ ソースを選択します。 適切なデータ ソースがない場合には、 **[新規作成]** をクリックして新しいデータ ソースを作成します。  
  
 **[新規作成]**  
 **データ ソース ウィザード**を開きます。  
  
 **テーブル名**  
 新しいテーブルの名前を入力します。  
  
 **場合は上書きが存在します。**  
 同じ名前を持つ既存のテーブルを上書きする場合は、このオプションをオンにします。  
  
 次のいずれかに該当する場合は、既存のテーブルを上書きする必要があります。  
  
-   予測クエリに列を追加した場合。  
  
-   予測クエリで列の名前やデータ型を変更した場合。  
  
-   対象となるテーブルで ALTER ステートメントを実行した場合。  
  
 複数の列の名前が同じである場合 (複数の派生列の名前が既定の列名 **Expression**である場合など) は、重複する名前を持つ各列に対して別名を作成する必要があります。 テーブル内の列には一意の名前が必要であるため、列に一意の名前が存在しない場合は、デザイナーが SQL Server に結果を保存しようとするとエラーが発生します。  
  
 **DSV に追加します。**  
 (省略可能) 既存のデータ ソースにテーブルを追加する場合に、プロジェクトに含まれているデータ ソース ビューを選択します。  
  
 このオプションは、すべての関連テーブルを保持する場合、モデルなどのトレーニング データ、予測ソース データ、およびクエリ結果で、同じデータ ソースに便利です。  
  
## <a name="see-also"></a>関連項目  
 [予測クエリ ビルダー &#40;データ マイニング&#41;](prediction-query-builder-data-mining.md)   
 [データ マイニング クエリ インターフェイス](data-mining/data-mining-query-tools.md)   
 [データ マイニング拡張機能 &#40;DMX&#41; ステートメント リファレンス](/sql/dmx/data-mining-extensions-dmx-statements)  
  
  
