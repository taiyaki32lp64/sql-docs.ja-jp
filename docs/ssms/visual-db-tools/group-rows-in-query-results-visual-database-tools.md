---
title: クエリ結果内の行のグループ化 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- summarizing table subsets
- grouping rows
- grouping query results
ms.assetid: b07082d5-4d55-4903-9af9-4c470554c6d3
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 3208a3458098b85325a19c014d99bca3b4f05c4d
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68254471"
---
# <a name="group-rows-in-query-results-visual-database-tools"></a>クエリ結果内の行のグループ化 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
小計を作成したり、テーブルのサブセットの他の集計情報を表示したりする場合は、集計クエリを使用してグループを作成します。 各グループは、テーブルで同じ値を持つすべての行のデータを集計します。  
  
たとえば、 `titles` テーブルの本の平均価格を出版社ごとに分類して表示するとします。 そのためには、クエリを出版社 (たとえば、 `pub_id`) でグループ化します。 クエリの出力結果は次のようになります。  
  
![クエリ結果: 出版社別にグループ化された平均価格](../../ssms/visual-db-tools/media/dv3w9e1.gif "クエリ結果: 出版社別にグループ化された平均価格")  
  
データをグループ化すると、次のように集計データまたはグループ化データだけを表示できます。  
  
-   グループ化された列 (GROUP BY 句に表示される列) の値。 上記の例では、 `pub_id` がグループ化された列です。  
  
-   SUM( ) や AVG( ) などの集計関数によって生成される値。 上記の例にある 2 番目の列は、 `price` 列に AVG( ) 関数を使用して生成された列です。  
  
各列の値は表示できません。 たとえば、出版社だけでグループ化する場合は、クエリに書名は表示できません。 そのため、クエリ出力に列を追加すると、 [クエリおよびビュー デザイナー](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md) により、 [SQL ペイン](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md)のステートメントの GROUP BY 句に列が自動的に追加されます。 1 つの列だけを集計する場合は、その列に集計関数を指定できます。  
  
複数の列をグループ化する場合、クエリの各グループには、グループ化された列のすべての集計値が表示されます。  
  
たとえば、 `titles` テーブルに対する次のクエリは、出版社 (`pub_id`) と本の種類 (`type`) の両方でグループ化されています。 クエリ結果は出版社別に並べ替えられ、出版社が発行する本の種類別に集計情報が表示されます。  
  
```  
SELECT pub_id, type, SUM(price) Total_price  
FROM titles  
GROUP BY pub_id, type  
```  
  
出力結果は、次のようになります。  
  
![クエリ結果: 出版社と種類別にグループ化された価格](../../ssms/visual-db-tools/media/dv3w9e2.gif "クエリ結果: 出版社と種類別にグループ化された価格")  
  
### <a name="to-group-rows"></a>列をグループ化するには  
  
1.  集計するテーブルをダイアグラム ペインに追加して、クエリの作成を開始します。  
  
2.  ダイアグラム ペインの背景を右クリックし、ショートカット メニューの **[グループ化を追加]** を選択します。 クエリおよびビュー デザイナーにより、抽出条件ペインのグリッドに **[グループ化]** 列が追加されます。  
  
3.  グループ化する列を抽出条件ペインに追加します。 クエリ出力に列を表示する場合は、出力に対して **[出力]** 列のチェック ボックスがオンになっていることを確認します。  
  
    SQL ペインのステートメントに GROUP BY 句が追加されます。 たとえば、SQL ステートメントは次のようになります。  
  
    ```  
    SELECT pub_id  
    FROM titles  
    GROUP BY pub_id  
    ```  
  
4.  集計する列を抽出条件ペインに追加します。 この列の [出力] 列がマークされていることを確認します。  
  
5.  集計する列の **[グループ化]** グリッド セルで、該当する集計関数を選択します。  
  
    集計する列に別名が自動的に割り当てられます。 この自動的に割り当てられた別名は、わかりやすい名前に変更することができます。 詳細については、「 [列の別名の作成 (Visual Database Tools)](../../ssms/visual-db-tools/create-column-aliases-visual-database-tools.md)」を参照してください。  
  
    ![クエリ結果セットに列の別名を追加](../../ssms/visual-db-tools/media/dv3w9e3.gif "クエリ結果セットに列の別名を追加")  
  
    **SQL** ペインのステートメントは、次のようになります。  
  
    ```  
    SELECT   pub_id, SUM(price) AS Totalprice  
    FROM     titles  
    GROUP BY pub_id  
    ```  
  
## <a name="see-also"></a>参照  
[クエリ結果の並べ替えおよびグループ化 (Visual Database Tools)](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
  
