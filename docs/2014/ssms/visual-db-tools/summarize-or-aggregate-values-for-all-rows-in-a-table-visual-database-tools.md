---
title: 要約または集計値をすべての行のテーブル (Visual Database Tools) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- summarizing query results
- aggregate functions [SQL Server], summarizing query results
ms.assetid: f5af876e-f937-4110-ba09-07999c35a699
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 33d44b48571839d9695893021f6cdc1c8bb63f06
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63204611"
---
# <a name="summarize-or-aggregate-values-for-all-rows-in-a-table-visual-database-tools"></a>テーブルにあるすべての行の値の要約または集計 (Visual Database Tools)
  集計関数を使用すると、テーブルのすべての値の要約を作成できます。 たとえば、`titles` テーブルの本の総額を表示するには、次のようなクエリを作成できます。  
  
```  
SELECT SUM(price)  
FROM titles  
```  
  
 複数の列に対する集計関数を使用して、同じクエリで複数の集計を作成できます。 たとえば、`price` 列の合計と `discount` 列の平均を計算するクエリを作成できます。  
  
 同じクエリで同じ列を合計、カウント、平均などの異なる方法で集計することもできます。 たとえば、次のクエリは、`price` テーブルから `titles` 列の平均および合計を求めます。  
  
```  
SELECT AVG(price), SUM(price)  
FROM titles  
```  
  
 検索条件を追加すると、条件を満たす行のサブセットを集計できます。  
  
> [!NOTE]  
>  行のカウントは、テーブルのすべての行と、特定の条件を満たす行のどちらでも行うことができます。 詳しくは、「[テーブルの行数のカウント (Visual Database Tools)](visual-database-tools.md)」をご覧ください。  
  
 テーブルのすべての行に対して 1 つの集計値を作成すると、集計値だけが表示されます。 たとえば、 `price` テーブルの `titles` 列の値の合計を求める場合、書名、出版社名などは表示されません。  
  
> [!NOTE]  
>  小計を求める、つまりグループを作成する場合は、グループごとに列の値を表示できます。 詳しくは、「[クエリ結果内の行のグループ化 (Visual Database Tools)](group-rows-in-query-results-visual-database-tools.md)」をご覧ください。  
  
### <a name="to-aggregate-values-for-all-rows"></a>すべての行の値を集計するには  
  
1.  集計するテーブルが既にダイアグラム ペインに存在していることを確認します。  
  
2.  ダイアグラム ペインの背景を右クリックし、ショートカット メニューの **[グループ化を追加]** を選択します。 [クエリおよびビュー デザイナー](query-and-view-designer-tools-visual-database-tools.md) により、抽出条件ペインのグリッドに **[グループ化]** 列が追加されます。  
  
3.  集計する列を抽出条件ペインに追加します。 この列の [出力] 列がマークされていることを確認します。  
  
     集計する列に別名が自動的に割り当てられます。 この別名は、わかりやすい名前に変更することができます。 詳しくは、「[列の別名の作成 (Visual Database Tools)](create-column-aliases-visual-database-tools.md)」をご覧ください。  
  
4.  **[グループ化]** グリッド列で、次のような該当する集計関数を選択します: **[合計]** 、 **[平均]** 、 **[最小]** 、 **[最大]** 、 **[カウント]** 。 結果セットの一意の行だけを集計する場合は、 **[個別の最小値]** など、DISTINCT オプションのある集計関数を選択します。 **[グループ化]** 、 **[式]** 、または **[Where 条件]** は、すべての行を集計するときには適用されないため、これらのオプションはクリックしないでください。  
  
     クエリおよびビュー デザイナーにより、 [SQL ペイン](sql-pane-visual-database-tools.md) のステートメントの列名は、指定した集計関数に置き換えられます。 たとえば、SQL ステートメントは次のようになります。  
  
    ```  
    SELECT SUM(price)  
    FROM titles  
    ```  
  
5.  クエリで複数の集計を作成する場合は、手順 3. および手順 4. を繰り返します。  
  
     クエリ出力リストまたは並べ替えリストに他の列を追加すると、グリッドの **[グループ化]** 列に **[グループ化]** という語句が、クエリおよびビュー デザイナーにより自動的に入力されます。 適切な集計関数を選択してください。  
  
6.  集計する行のサブセットを指定する検索条件がある場合は、検索条件も追加します。  
  
 クエリを実行すると、結果ペインに指定した集計が表示されます。  
  
> [!NOTE]  
>  [グループ化] モードを明示的にオフにするまで、集計関数は SQL ペイン内に SQL ステートメントの一部として保持されます。 そのため、クエリの種類を変更したり、ダイアグラム ペインに表示されるテーブルまたはテーブル値オブジェクトを変更したりすると、作成されるクエリに無効な集計関数が含まれる可能性があります。  
  
## <a name="see-also"></a>関連項目  
 [クエリ結果の並べ替えとグループ化&#40;Visual Database Tools&#41;](sort-and-group-query-results-visual-database-tools.md)   
 [クエリ結果の要約 (Visual Database Tools)](summarize-query-results-visual-database-tools.md)  
  
  
