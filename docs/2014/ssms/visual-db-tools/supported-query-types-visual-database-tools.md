---
title: サポートされるクエリの種類 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- Delete query
- queries [SQL Server], types
- Update query
- Query Designer [SQL Server], query types
- Criteria pane
- Insert Values query
- Select query
- Make Table query
- Insert Results query
- Diagram pane [Visual Database Tools]
- View Designer, query types
ms.assetid: 72b9116c-c128-4078-a78d-257a2955a3f6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 752467d058a6618ccfa44d7e2f75ac33b632878e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63204652"
---
# <a name="supported-query-types-visual-database-tools"></a>サポートされるクエリの種類 (Visual Database Tools)
  [クエリおよびビュー デザイナー](visual-database-tools.md)のダイアグラム ペインと抽出条件ペイン (グラフィカルなペイン) では、次のクエリを作成できます。  
  
-   **選択クエリ** 1 つ以上のテーブルまたはビューからデータを取得します。 このクエリは、SQL の SELECT ステートメントを作成します。  
  
-   **結果の挿入クエリ** あるテーブルの既存の行を別のテーブルにコピーして、新しい行を作成します。または、同じテーブルに行をコピーして新しい行を作成します。 このクエリは、SQL の INSERT INTO...SELECT ステートメントを作成します。  
  
-   **値の挿入クエリ** 新しい行を作成し、指定された列に値を挿入します。 このクエリは、SQL の INSERT INTO...VALUES ステートメントを作成します。  
  
-   **更新クエリ** テーブル内の 1 つ以上の既存の行にある特定の列の値を変更します。 このクエリは、SQL の UPDATE...SET ステートメントを作成します。  
  
-   **削除クエリ** テーブルから 1 つ以上の行を削除します。 このクエリは、SQL の DELETE ステートメントを作成します。  
  
    > [!NOTE]  
    >  削除クエリは、テーブルから行全体を削除します。 特定のデータ列から値を削除する場合は、更新クエリを使用します。  
  
-   **テーブルの作成クエリ** 新しいテーブルを作成し、クエリの結果をコピーしてテーブル内に行を作成します。 このクエリは、SQL の SELECT...INTO ステートメントを作成します。  
  
 クエリを作成するには、グラフィカルなペインを使用する方法だけでなく、UNION クエリなど、任意の SQL ステートメントを SQL ペインに入力して作成する方法があります。  
  
 グラフィカルなペインで表示できない SQL ステートメントを使用してクエリを作成すると、グラフィカルなペインは淡色表示になります。これは、これらのペインに作成中のクエリが反映されていないことを示します。 ただし、これらのペインは淡色表示されていてもアクティブ状態なので、多くの場合、ペインに表示されているクエリを変更できます。 変更の結果、グラフィカルなペインで表示できるクエリになった場合、ペインの淡色表示は解除されます。  
  
## <a name="see-also"></a>参照  
 [クエリおよびビューの操作方法に関するトピックを設計&#40;Visual Database Tools&#41;](design-queries-and-views-how-to-topics-visual-database-tools.md)   
 [クエリの種類 (Visual Database Tools)](types-of-queries-visual-database-tools.md)  
  
  
