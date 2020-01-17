---
title: クエリへの列の追加 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- inserting columns
- columns [SQL Server], adding
- queries [SQL Server], columns
- adding columns
ms.assetid: 82f3ba72-3d72-4fb1-8179-2a953a782787
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: aef64ed8031664dcbefa7d0e30bf9f63435b292c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63015703"
---
# <a name="add-columns-to-queries-visual-database-tools"></a>クエリへの列の追加 (Visual Database Tools)
  クエリで列を使用するには、クエリに列を追加する必要があります。 列の追加は、クエリ出力に列を追加する場合、列を並べ替える場合、列の内容を検索する場合、または列の内容を集計する場合に行います。 クエリで使用する列のうち、クエリを実行したときに結果ペインに含める列を指定できます。 詳細については、「 [クエリ結果からの列の削除 (Visual Database Tools)](visual-database-tools.md)」を参照してください。  
  
> [!NOTE]  
>  列のデータ型をクエリおよびビュー デザイナーに表示するには、 **ダイアグラム ペイン** でテーブルまたはテーブル値オブジェクトを選択して、プロパティ ウィンドウの [列一覧] をクリックします。 次に省略記号 ( **[...]** ) をクリックすると、 **[列一覧]** ダイアログ ボックスが開きます。  
  
 クエリで列を使用する場合は、リテラル、演算子、および関数に組み合わせて式にすることもできます。  
  
### <a name="to-add-an-individual-column"></a>列を個別に追加するには  
  
-   **ダイアグラム ペイン**で、追加する列の横のチェック ボックスをオンにします。  
  
     \- または -  
  
-   **抽出条件ペイン**で、最初の空白のグリッド行に移動し、 **[列]** 列のフィールドをクリックして、ドロップダウン リストの列名をクリックします。  
  
### <a name="to-add-all-columns-for-one-table-or-table-valued-object"></a>1 つのテーブルまたはテーブル値オブジェクトの列をすべて追加するには  
  
-   **ダイアグラム ペイン**、横にチェック ボックスをオン **\*(すべての列)** します。  
  
### <a name="to-add-all-columns-for-all-tables-and-table-structured-objects"></a>すべてのテーブルおよびテーブル構造オブジェクトの列をすべて追加するには  
  
1.  **テーブル操作ペイン** の結合線が選択されていないことを確認します。  
  
2.  デザイン ウィンドウの空の領域を右クリックし、ショートカット メニューの **[プロパティ]** をクリックします。  
  
3.  プロパティ ウィンドウの **[すべての列を出力]** をクリックして、ドロップダウン リストの **[はい]** または **[いいえ]** をクリックします。  
  
## <a name="see-also"></a>関連項目  
 [クエリ結果から列を削除&#40;Visual Database Tools&#41;](visual-database-tools.md)   
 [クエリから列を削除する&#40;Visual Database Tools&#41;](remove-columns-from-queries-visual-database-tools.md)   
 [検索条件を指定&#40;Visual Database Tools&#41;](specify-search-criteria-visual-database-tools.md)   
 [クエリ結果の要約&#40;Visual Database Tools&#41;](summarize-query-results-visual-database-tools.md)   
 [クエリに関する基本操作の実行 (Visual Database Tools)](perform-basic-operations-with-queries-visual-database-tools.md)  
  
  
