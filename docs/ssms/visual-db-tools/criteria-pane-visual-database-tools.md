---
title: 抽出条件ペイン (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- Query Designer [SQL Server], Criteria pane
- View Designer, Criteria pane
- entering query options into grid [SQL Server]
- Criteria pane
- inserting query options into grid
- grid showing query options [SQL Server]
- adding query options into grid
ms.assetid: 6291affe-580e-482f-a7ff-45ce3837956a
author: markingmyname
ms.author: maghan
ms.openlocfilehash: cf5d5f7a306b443fd01f9112b4197485ce3ce2ba
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68263903"
---
# <a name="criteria-pane-visual-database-tools"></a>抽出条件ペイン (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
抽出条件ペインでは、表示するデータ列、結果の順序、選択する行などのクエリ オプションを選択してスプレッドシート形式のグリッドに入力することにより、クエリ オプションを指定できます。 抽出条件ペインでは次の内容を指定できます。  
  
-   表示する列と列名のエイリアス  
  
-   列が属しているテーブル  
  
-   計算が必要な列に対する式  
  
-   クエリの並べ替え順序  
  
-   検索条件  
  
-   グループ化の条件 (サマリ レポートで使用する集計関数など)  
  
-   更新クエリまたは値の挿入クエリに対する新しい値  
  
-   結果の挿入クエリの挿入先の列名  
  
抽出条件ペインで行った変更は、ダイアグラム ペインと SQL ペインに自動的に反映されます。 同様に、他のペインが変更されると、その変更を反映して抽出条件ペインも自動的に更新されます。  
  
## <a name="about-the-criteria-pane"></a>抽出条件ペインについて  
抽出条件ペインの行には、クエリで使用されるデータ列が表示されます。抽出条件ペインの列には、クエリ オプションが表示されます。  
  
抽出条件ペインに表示される具体的な情報は、作成中のクエリの種類によって異なります。  
  
抽出条件ペインが表示されていない場合は、デザイナーを右クリックし、 **[ペイン]** をポイントして **[抽出条件]** をクリックします。  
  
## <a name="options"></a>オプション  
  
|**列**|**[クエリの種類]**|**[説明]**|  
|--------------|------------------|-------------------|  
|[列]|All|クエリに使用されるデータ列の名前、または計算が必要な列の式が表示されます。 水平にスクロールしても常に表示されるよう、この列はロックされています。|  
|別名|選択、結果の挿入、更新、テーブルの作成|列に対する別名、または計算列で使用できる名前を指定します。|  
|テーブル|選択、結果の挿入、更新、テーブルの作成|対応するデータ列のテーブルまたはテーブル構造オブジェクトの名前を指定します。 計算列の場合は空白です。|  
|[出力]|選択、結果の挿入、テーブルの作成|データ列をクエリの出力に表示するかどうかを指定します。<br /><br />注:データベースが対応している場合は、データ列を結果セットに表示せずに、並べ替えや検索の句として使用できます。|  
|[並べ替えの種類]|選択、結果の挿入|クエリ結果を並べ替えるために対応するデータ列を使用すること、および並べ替えが昇順であるか降順であるかを指定します。|  
|[並べ替え順序]|選択、結果の挿入|結果セットの並べ替えに使用するデータ列の並べ替え優先順位を指定します。 データ列の並べ替え順序を変更すると、他のすべての列の並べ替え順序もその変更に従って更新されます。|  
|[グループ化]|選択、結果の挿入、テーブルの作成|対応するデータ列を集計クエリの作成に使用することを指定します。 このグリッド列が表示されるのは、 **[ツール]** メニューの **[グループ化]** をクリックした場合、または SQL ペインに GROUP BY 句を追加した場合だけです。<br /><br />既定では、この列の値は **[グループ化]** に設定されていて、列は GROUP BY 句の中で使用されます。<br /><br />この列のセルに移動し、対応するデータ列に適用する集計関数を選択すると、既定では、結果として作成される式が、結果セットの出力列として追加されます。|  
|[抽出条件]|All|対応するデータ列に対する検索条件 (フィルター) を指定します。 演算子 (既定では "=") と検索する値を入力します。 テキスト値は単一引用符で囲みます。<br /><br />対応するデータ列が GROUP BY 句の一部である場合、入力した式は HAVING 句で使用されます。<br /><br />**[抽出条件]** グリッド列の複数のセルに値を入力した場合は、結果として生成される検索条件が自動的に論理 AND で連結されます。<br /><br />1 つのデータベース列に複数の検索条件式 (たとえば (fname > 'A') AND (fname < 'M')) を指定するには、そのデータ列を抽出条件ペインに 2 回入力し、データ列の各インスタンスの **[抽出条件]** グリッド列に異なる値を入力します。|  
|[または...]|All|データ列に追加する検索条件式を指定します。指定した式は、前の式と論理 OR で連結されます。 右端の **[または...]** 列で Tab キーを押すと、 **[または...]** グリッド列を追加できます。|  
|追加|結果の挿入|対応するデータ列の挿入先データ列の名前を指定します。 結果の挿入クエリを作成すると、クエリおよびビュー デザイナーは、挿入元データ列を適切な挿入先データ列に照合しようとします。 一致するデータ列をクエリおよびビュー デザイナーが選択できない場合は、列の名前を指定する必要があります。|  
|[新しい値]|更新、値の挿入|対応する列に格納する値を指定します。 リテラル値または式を入力します。|  
  
## <a name="see-also"></a>参照  
[クエリおよびビューのデザインの操作方法に関するトピック (Visual Database Tools)](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[ダイアグラム ペイン (Visual Database Tools)](../../ssms/visual-db-tools/diagram-pane-visual-database-tools.md)  
[検索値を入力するときの規則 (Visual Database Tools)](../../ssms/visual-db-tools/rules-for-entering-search-values-visual-database-tools.md)  
[クエリ結果の並べ替えおよびグループ化 (Visual Database Tools)](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
[結果ペイン (Visual Database Tools)](../../ssms/visual-db-tools/results-pane-visual-database-tools.md)  
[SQL ペイン (Visual Database Tools)](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md)  
  
