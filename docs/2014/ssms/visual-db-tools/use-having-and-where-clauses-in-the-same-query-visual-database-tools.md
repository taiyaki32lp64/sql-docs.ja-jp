---
title: 使用して、HAVING 句および WHERE 句と同じではクエリ (Visual Database Tools) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- search criteria [SQL Server], excluding rows
- search criteria [SQL Server], WHERE clause
- search conditions [SQL Server], HAVING clause
- row excluded in search [SQL Server]
- search criteria [SQL Server], HAVING clause
- HAVING clause, search criteria
- search conditions [SQL Server], WHERE clause
- WHERE clause, search criteria
- excluding rows
ms.assetid: 1e07cf56-b4b7-4c49-8ddd-c276812a7148
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f7aafcd72eff1d21dfe02c8957496398d327cf38
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63204630"
---
# <a name="use-having-and-where-clauses-in-the-same-query-visual-database-tools"></a>同一クエリ内で HAVING 句および WHERE 句を使用する (Visual Database Tools)
  場合によっては、HAVING を使用してグループ全体に条件を適用する前に、WHERE 句を使用してグループから個別の行を除外する必要があります。  
  
 HAVING 句は WHERE 句に似ていますが、適用先はグループ全体だけであり、グループを示す結果セット内の行だけが対象になります。一方、WHERE 句は個々の行に適用されます。 1 つのクエリに WHERE 句と HAVING 句の両方を含めることができます。 そのような場合は、次の処理を行います。  
  
-   最初に、ダイアグラム ペインのテーブルまたはテーブル値オブジェクトの各行に WHERE 句が適用されます。 WHERE 句の条件を満たす行だけがグループ化されます。  
  
-   その結果セットに含まれている行に、HAVING 句が適用されます。 HAVING 句の条件を満たすグループだけがクエリ出力に表示されます。 HAVING 句は、GROUP BY 句または集計関数にも使用されている列にだけ適用できます。  
  
 たとえば、 `titles` テーブルと `publishers` テーブルを結合して、出版社全体の本の平均価格を表示するクエリを作成するとします。 ここでは、カリフォルニア州の出版社など、特定の出版社グループの平均価格だけを表示するとします。 さらに、$10.00 を超える平均価格だけを表示するとします。  
  
 平均価格を計算する前に、カリフォルニア州以外の出版社を除外するために、WHERE 句で最初の条件を設定します。 2 番目の条件は、データのグループ化および集計の結果に基づくため、HAVING 句で指定する必要があります。 結果として作成される SQL ステートメントは次のようになります。  
  
```  
SELECT titles.pub_id, AVG(titles.price)  
FROM titles INNER JOIN publishers  
   ON titles.pub_id = publishers.pub_id  
WHERE publishers.state = 'CA'  
GROUP BY titles.pub_id  
HAVING AVG(price) > 10  
```  
  
 HAVING 句および WHERE 句は、どちらも抽出条件ペインで作成できます。 既定では、列の検索条件を指定すると、条件が HAVING 句の一部になります。 ただし、条件を WHERE 句に変更することもできます。  
  
 同じ列を含む WHERE 句および HAVING 句を作成することも可能です。 これには、抽出条件ペインに列を 2 回作成し、一方を HAVING 句の一部として、他方を WHERE 句の一部として指定します。  
  
### <a name="to-specify-a-where-condition-in-an-aggregate-query"></a>集計クエリで WHERE 条件を指定するには  
  
1.  検索するグループを指定します。 詳しくは、「[クエリ結果内の行のグループ化 (Visual Database Tools)](visual-database-tools.md)」をご覧ください。  
  
2.  WHERE 条件の基準とする列が抽出条件ペインにまだない場合は、抽出条件ペインに追加します。  
  
3.  データ列が GROUP BY 句または集計関数に含まれていない場合は、 **[出力]** 列をオフにします。  
  
4.  **[フィルター]** 列で WHERE 条件を指定します。 SQL ステートメントの HAVING 句に、指定した条件が追加されます。  
  
    > [!NOTE]  
    >  上の手順の例では、クエリで 2 つのテーブル `titles` および `publishers`を結合しています。  
  
     クエリのこの時点で、SQL ステートメントには HAVING 句が次のように含まれています。  
  
    ```  
    SELECT titles.pub_id, AVG(titles.price)  
    FROM titles INNER JOIN publishers   
       ON titles.pub_id = publishers.pub_id  
    GROUP BY titles.pub_id  
    HAVING publishers.state = 'CA'  
    ```  
  
5.  **[グループ化]** 列で、グループおよび集計のオプションの一覧の **[Where 条件]** をクリックします。 SQL ステートメントの HAVING 句から条件が削除され、WHERE 句に条件が追加されます。  
  
     SQL ステートメントは、WHERE 句を含むように次のように変更されます。  
  
    ```  
    SELECT titles.pub_id, AVG(titles.price)  
    FROM titles INNER JOIN publishers   
       ON titles.pub_id = publishers.pub_id  
    WHERE publishers.state = 'CA'  
    GROUP BY titles.pub_id  
    ```  
  
## <a name="see-also"></a>関連項目  
 [クエリ結果の並べ替えとグループ化&#40;Visual Database Tools&#41;](sort-and-group-query-results-visual-database-tools.md)   
 [クエリ結果の要約 (Visual Database Tools)](summarize-query-results-visual-database-tools.md)  
  
  
