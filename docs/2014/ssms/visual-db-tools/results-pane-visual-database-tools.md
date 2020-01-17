---
title: 結果ペイン (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- View Designer, Results pane
- result sets [SQL Server], queries
- synchronization [SQL Server], query results with definition
- displaying query results in grid
- grid showing query results [SQL Server]
- showing query results in grid
- Query Designer [SQL Server], Results pane
- results [SQL Server], query
- viewing query results
- queries [SQL Server], results
- Results pane
ms.assetid: 6309a1bc-a628-4141-8bb5-b35924bd19f9
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 87bfaef1ad5dc4c9b1f907c27955ca3f156038a8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63067808"
---
# <a name="results-pane-visual-database-tools"></a>結果ペイン (Visual Database Tools)
  結果ペインには、最後に実行された選択クエリの結果が表示されます。 他の種類のクエリ結果は、メッセージ ボックスに表示されます。結果ペインを表示するには、クエリまたはビューを表示または作成するか、テーブルのデータを返します。 結果ペインが既定で表示されない場合は、 **[クエリ デザイナー]** メニューの **[ペイン]** をポイントし、 **[結果]** をクリックします。  
  
## <a name="what-you-can-do-in-the-results-pane"></a>結果ペインで可能な操作  
  
-   最後に実行された選択クエリの結果セットを表形式で参照。  
  
-   単一のテーブルまたはビューからのデータを表示するクエリまたはビューについて、結果セットに含まれる各列の値の編集、新しい行の追加、既存の行の削除。  
  
## <a name="limitations-in-the-results-pane"></a>結果ペインの制限  
  
-   テーブル値関数から返された結果は、一部の場合に限り更新できます。  
  
-   複数のテーブルまたはビューの列を含むクエリまたはビューは更新できません。  
  
-   ストアド プロシージャから返された結果は更新できません。  
  
-   GROUP BY 句または DISTINCT 句を使用したクエリまたはビューは更新できません。  
  
## <a name="navigating-in-the-results-pane"></a>結果ペイン内を移動する  
 結果ペインの下端にあるナビゲーション バーを使用すると、レコード間をすばやく移動できます。  
  
 最初のレコードと最後のレコードに移動するボタンや、次のレコードと前のレコードに移動するボタン、特定のレコードに移動するボタンがあります。  
  
 特定のレコードに移動するには、ナビゲーション バー内のテキスト ボックスに行番号を入力し、Enter キーを押します。  
  
 クエリおよびビュー デザイナーでキーボード ショートカットを使用する方法については、「[クエリおよびビュー デザイナーでの操作 (Visual Database Tools)](visual-database-tools.md)」を参照してください。  
  
## <a name="keeping-the-results-set-synchronized-with-the-query-definition"></a>結果セットとクエリ定義を同期化する  
 クエリまたはビューの結果を操作していると、結果ペイン内のレコードがクエリ定義の同期化対象から外れてしまう場合があります。 たとえば、テーブル内の 5 列のうち 4 列についてクエリを実行し、ダイアグラム ペインを使用して 5 番目の列をクエリの定義に追加した場合、その 5 番目の列のデータは、結果ペインに自動的に追加されません。 結果ペインに新たなクエリ定義を反映するには、再度クエリを実行します。  
  
 クエリが変更されると、結果ペインの右下端に警告アイコンと "クエリが変更されました。" というテキストが表示され、 ペインの左上端にも警告アイコンが表示されます。  
  
## <a name="see-also"></a>関連項目  
 [クエリを作成する&#40;Visual Database Tools&#41;](create-queries-visual-database-tools.md)   
 [クエリを実行して&#40;Visual Database Tools&#41;](run-queries-visual-database-tools.md)   
 [クエリおよびビューの操作方法に関するトピックを設計&#40;Visual Database Tools&#41;](design-queries-and-views-how-to-topics-visual-database-tools.md)   
 [ダイアグラム ペイン&#40;Visual Database Tools&#41;](diagram-pane-visual-database-tools.md)   
 [抽出条件ペイン&#40;Visual Database Tools&#41;](criteria-pane-visual-database-tools.md)   
 [結果ペインのデータの操作 (Visual Database Tools)](results-pane-visual-database-tools.md)  
  
  
