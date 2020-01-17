---
title: クエリからのテーブルの削除 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- deleting tables
- removing tables
- dropping tables
- queries [SQL Server], tables
ms.assetid: 8fea0b4f-99b7-4050-8d6f-a97ffb839619
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: bda582c7b9171e89a43b6870b3b6c2df139b7b11
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62670465"
---
# <a name="remove-tables-from-queries-visual-database-tools"></a>クエリからのテーブルの削除 (Visual Database Tools)
  クエリからテーブルまたはテーブル値オブジェクトを削除できます。  
  
> [!NOTE]  
>  テーブルまたはテーブル値オブジェクトを削除しても、現在のクエリから削除されるだけです。データベースからは何も削除されません。 データベースからテーブルを削除する方法の詳細については、次を参照してください。[テーブルの削除&#40;データベース エンジン&#41;](../../relational-databases/tables/delete-tables-database-engine.md)します。  
  
### <a name="to-remove-a-table-or-table-structured-object"></a>テーブルまたはテーブル構造オブジェクトを削除するには  
  
-   **ダイアグラム ペイン**で、テーブル、ビュー、ユーザー定義関数、シノニム、またはクエリを選択し、Del キーを押すか、オブジェクトを右クリックして、表示されるダイアログ ボックスの **[削除]** をクリックします。 同時に複数のオブジェクトを選択して削除することもできます。  
  
     \- または -  
  
-   **SQL ペイン**でオブジェクトへのすべての参照を削除します。  
  
 テーブルまたはテーブル値オブジェクトを削除すると、クエリおよびビュー デザイナーでは、そのテーブルまたはテーブル値オブジェクトを含む結合が自動的に削除され、これらのオブジェクトの列に対する参照も **SQL ペイン** および **抽出条件ペイン**から自動的に削除されます。 ただし、オブジェクトを含む複合式がクエリに含まれる場合、オブジェクトに対する参照がすべて削除されるまで、オブジェクトが自動的に削除されることはありません。  
  
## <a name="see-also"></a>参照  
 [クエリにテーブルを追加する&#40;Visual Database Tools&#41;](visual-database-tools.md)   
 [テーブルの別名の作成&#40;Visual Database Tools&#41;](create-table-aliases-visual-database-tools.md)   
 [検索条件を指定&#40;Visual Database Tools&#41;](specify-search-criteria-visual-database-tools.md)   
 [クエリ結果の要約&#40;Visual Database Tools&#41;](summarize-query-results-visual-database-tools.md)   
 [クエリに関する基本操作の実行 (Visual Database Tools)](perform-basic-operations-with-queries-visual-database-tools.md)  
  
  
