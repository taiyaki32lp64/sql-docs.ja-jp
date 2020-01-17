---
title: クエリおよびビュー デザイナー ツール (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.querydesigner
- vdt.pane.diagram
- vdt.pane.grid
- vdt.dlgbox.querybuilder
- vdt.pane.sql
- vdt.pane.results
helpviewer_keywords:
- Query Designer [SQL Server], panes
- View Designer, panes
- Query Designer [SQL Server], components
- View Designer, components
ms.assetid: 12e4b5a5-b793-4b6c-a0e5-c450c49bf26f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 639e6b7640f3463bfe100345d044437d619a5546
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63460002"
---
# <a name="query-and-view-designer-tools-visual-database-tools"></a>クエリおよびビュー デザイナー ツール (Visual Database Tools)
  クエリ、ビュー、インライン関数、または単一ステートメント ストアド プロシージャをデザインするときに使用するデザイナーは、ダイアグラム ペイン、抽出条件ペイン、SQL ペイン、および結果ペインで構成されています。  
  
 ![クエリ デザイナー](../../database-engine/media//vs-queryviewdsgpanes.gif "クエリ デザイナー")  
  
-   ダイアグラム ペインには、問い合わせているテーブルおよび他のテーブル値オブジェクトが表示されます。 それぞれの四角形は、テーブルまたはテーブル値オブジェクトを表し、使用可能なデータ列を表示します。 結合は、四角形の間を結ぶ線で示されます。 詳細については、「[ダイアグラム ペイン (Visual Database Tools)](visual-database-tools.md)」を参照してください。  
  
-   抽出条件ペインにはスプレッドシート形式のグリッドが表示されます。このグリッドで、表示するデータ列、選択する行、行をグループ化する方法などを指定できます。 詳細については、「[抽出条件ペイン (Visual Database Tools)](criteria-pane-visual-database-tools.md)」を参照してください。  
  
-   SQL ペインには、クエリまたはビューの SQL ステートメントが表示されます。 デザイナーで作成された SQL ステートメントを編集したり、独自の SQL ステートメントを入力したりできます。 このペインは、UNION クエリなど、ダイアグラム ペインや抽出条件ペインでは作成できない SQL ステートメントを入力する場合に特に便利です。 詳細については、「[SQL ペイン (Visual Database Tools)](sql-pane-visual-database-tools.md)」を参照してください。  
  
-   結果ペインのグリッドには、クエリまたはビューによって取得されたデータが表示されます。 クエリおよびビュー デザイナーでは、最後に実行した選択クエリの結果がペインに表示されます。 グリッドのセルの値を編集してデータベースを変更できます。また、行を追加したり削除したりできます。 詳細については、「[SQL ペイン (Visual Database Tools)](results-pane-visual-database-tools.md)」を参照してください。  
  
 どのペインでも、クエリやビューを作成できます。たとえば、表示する列を指定するには、ダイアグラム ペインの場合は、その列を選択します。抽出条件ペインの場合は、その列を入力します。SQL ペインの場合は、その列を SQL ステートメント内に記述します。  
  
## <a name="displaying-and-hiding-panes"></a>ペインの表示と非表示  
 ペインを非表示にする場合、または非表示になっているペインを表示する場合は、デザイン画面を右クリックして **[ペイン]** をポイントし、ペインの名前をクリックします。 クエリおよびビュー デザイナーがクエリ デザイナー モードで開かれている場合、 **[結果]** ペインは使用できません。  
  
## <a name="see-also"></a>参照  
 [クエリおよびビューの操作方法に関するトピックを設計&#40;Visual Database Tools&#41;](design-queries-and-views-how-to-topics-visual-database-tools.md)   
 [クエリおよびビュー デザイナーを開く&#40;Visual Database Tools&#41;](open-the-query-and-view-designer-visual-database-tools.md)   
 [SQL エディター (Visual Database Tools)](sql-editor-visual-database-tools.md)  
  
  
