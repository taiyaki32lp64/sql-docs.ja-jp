---
title: SELECT の例 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- parentheses [SQL Server]
- GROUP BY clause, SELECT statement
- query hints [SQL Server]
- ALL keyword
- ROLLUP operator
- SELECT statement [SQL Server], examples
- correlated subqueries, SELECT statement
- SELECT INTO statement
- ORDER BY clause [Transact-SQL]
- GROUPING function
- index hints [SQL Server]
- HAVING clause, SELECT statement
- DISTINCT keyword
- CUBE operator
- UNION operator [SQL Server]
- computed sums
- WHERE clause, SELECT statement
ms.assetid: 9b9caa3d-e7d0-42e1-b60b-a5572142186c
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: e3d7c9b661a69f4a575a18aae03f9eb5e601b69b
ms.sourcegitcommit: ba44730f5cc33295ae2ed1f281186dd266bad4ef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/19/2019
ms.locfileid: "74191084"
---
# <a name="select-examples-transact-sql"></a>SELECT の例 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  ここでは、[SELECT](../../t-sql/queries/select-transact-sql.md) ステートメントの使用例を紹介します。  
  
## <a name="a-using-select-to-retrieve-rows-and-columns"></a>A. SELECT を使用して行および列を取得する  
 3 つのプログラム例を次に示します。 最初の例では、[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベース内の `*` テーブルから、WHERE 句を指定せずにすべての行を返し、また `Product` を使用してすべての列を返しています。  
  
 [!code-sql[Select#SelectExamples1](../../t-sql/queries/codesnippet/tsql/select-examples-transact_1.sql)]  
  
 この例では、[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベース内の `Name` テーブルから、WHERE 句を指定せずにすべての行と、一部の列 (`ProductNumber`、`ListPrice`、`Product`) のみを返しています。 さらに、列ヘッダーが追加されています。  
  
 [!code-sql[Select#SelectExamples2](../../t-sql/queries/codesnippet/tsql/select-examples-transact_2.sql)]  
  
 この例では、製品ラインが `R` で、製造所要日数が `4` 日未満の `Product` の行のみを返しています。  
  
 [!code-sql[Select#SelectExamples3](../../t-sql/queries/codesnippet/tsql/select-examples-transact_3.sql)]  
  
## <a name="b-using-select-with-column-headings-and-calculations"></a>B. 列ヘッダーおよび計算処理と共に SELECT を使用する  
 次の例では、`Product` テーブルのすべての行を返します。 最初の例では、各製品の売上合計と売上割引を返します。 2 番目の例では、製品ごとの合計収入が計算されます。  
  
 [!code-sql[Select#SelectExamples4](../../t-sql/queries/codesnippet/tsql/select-examples-transact_4.sql)]  
  
 次の例は、販売注文ごとに各製品の収入を計算するクエリです。  
  
 [!code-sql[Select#SelectExamples5](../../t-sql/queries/codesnippet/tsql/select-examples-transact_5.sql)]  
  
## <a name="c-using-distinct-with-select"></a>C. DISTINCT を SELECT と共に使用する  
 次の例では、`DISTINCT` を使って重複しているタイトルを取得しないようにしています。  
  
 [!code-sql[Select#SelectExamples6](../../t-sql/queries/codesnippet/tsql/select-examples-transact_6.sql)]  
  
## <a name="d-creating-tables-with-select-into"></a>D. SELECT INTO を使用してテーブルを作成する  
 次の最初の例では、`#Bicycles` 内に `tempdb` という一時テーブルを作成します。  
  
 [!code-sql[Select#SelectExamples7](../../t-sql/queries/codesnippet/tsql/select-examples-transact_7.sql)]  
  
 2 番目の例では、`NewProducts` という名前のパーマネント テーブルを作成します。  
  
 [!code-sql[Select#SelectExamples8](../../t-sql/queries/codesnippet/tsql/select-examples-transact_8.sql)]  
  
## <a name="e-using-correlated-subqueries"></a>E. 相関サブクエリを使用する
相関サブクエリは、外側のクエリによって値が決まるクエリです。 このクエリは、外側のクエリが選択する行に対して 1 回ずつ、繰り返し実行できます。

最初の例では、`EXISTS` キーワードと `IN` キーワードを使用した意味的に等しいクエリと、それらの違いを示します。 いずれも、製品モデルが長袖ジャージで、`ProductModelID` テーブルと `Product` テーブルの間で `ProductModel` 番号が一致する各製品名の 1 つのインスタンスを取得する有効なサブクエリの例です。  
  
 [!code-sql[Select#SelectExamples9](../../t-sql/queries/codesnippet/tsql/select-examples-transact_9.sql)]  
  
 次の例では、`IN` が使用され、`SalesPerson` テーブルのボーナス額が `5000.00` で、従業員の ID 番号が `Employee` テーブルと `SalesPerson` テーブルで一致する各従業員の姓名のインスタンスを 1 つ取得します。  
  
 [!code-sql[Select#SelectExamples10](../../t-sql/queries/codesnippet/tsql/select-examples-transact_10.sql)]  
  
 上記のステートメントのサブクエリは、外側のクエリから独立して評価できません。 このサブクエリは `Employee.EmployeeID` の値を必要としますが、この値は、[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]が調べる `Employee` の行によって変化します。  
  
 相関サブクエリは、外側のクエリの `HAVING` 句でも使えます。 この例では、表示価格がモデルの平均値の 2 倍以上の製品モデルを検索します。  
  
 [!code-sql[Select#SelectExamples11](../../t-sql/queries/codesnippet/tsql/select-examples-transact_11.sql)]  
  
 この例では、2 つの相関サブクエリを使って、特定の製品を販売した従業員の名前を検索します。  
  
 [!code-sql[Select#SelectExamples12](../../t-sql/queries/codesnippet/tsql/select-examples-transact_12.sql)]  
  
## <a name="f-using-group-by"></a>F. GROUP BY を使用する  
 次の例は、データベース内の各販売注文の合計を検索します。  
  
 [!code-sql[Select#SelectExamples13](../../t-sql/queries/codesnippet/tsql/select-examples-transact_13.sql)]  
  
 `GROUP BY` 句があるため、各販売注文につき 1 行だけが返され、この行にその販売注文のすべての売上合計が含まれます。  
  
## <a name="g-using-group-by-with-multiple-groups"></a>G. GROUP BY を複数のグループと共に使用する  
 次の例では、平均価格および今年に入ってからの売り上げの合計を、製品 ID と特価品 ID でグループ化して返します。  
  
 [!code-sql[Select#SelectExamples14](../../t-sql/queries/codesnippet/tsql/select-examples-transact_14.sql)]  
  
## <a name="h-using-group-by-and-where"></a>H. GROUP BY と WHERE を使用する  
 次の例では、表示価格が `$1000` より多い行だけを取得した後、結果をグループ化します。  
  
 [!code-sql[Select#SelectExamples15](../../t-sql/queries/codesnippet/tsql/select-examples-transact_15.sql)]  
  
## <a name="i-using-group-by-with-an-expression"></a>I. 1 つの式と共に GROUP BY を使用する  
 次の例では、式によってグループ化します。 式に集計関数が含まれない限り、式によってグループ化することができます。  
  
 [!code-sql[Select#SelectExamples16](../../t-sql/queries/codesnippet/tsql/select-examples-transact_16.sql)]  
  
## <a name="j-using-group-by-with-order-by"></a>J. ORDER BY と共に GROUP BY を使用する  
 次の例では、それぞれの製品の種類別の平均価格を求め、その結果を平均価格の順序で表示しています。  
  
 [!code-sql[Select#SelectExamples18](../../t-sql/queries/codesnippet/tsql/select-examples-transact_17.sql)]  
  
## <a name="k-using-the-having-clause"></a>K. HAVING 句を使用する  
 最初の例では、`HAVING` 句を集計関数と共に使用しています。 `SalesOrderDetail` テーブルの行を製品 ID 別にグループ化し、平均注文数が 5 以下の製品を除外しています。 2 番目の例では、`HAVING` 句を集計関数なしで使用しています。  
  
 [!code-sql[Select#SelectExamples19](../../t-sql/queries/codesnippet/tsql/select-examples-transact_18.sql)]  
  
 次のクエリでは、`LIKE` 句の中で `HAVING` 句を使用しています。  
  
```sql
USE AdventureWorks2012 ;  
GO  
SELECT SalesOrderID, CarrierTrackingNumber   
FROM Sales.SalesOrderDetail  
GROUP BY SalesOrderID, CarrierTrackingNumber  
HAVING CarrierTrackingNumber LIKE '4BD%'  
ORDER BY SalesOrderID ;  
GO  
```  
  
## <a name="l-using-having-and-group-by"></a>L. HAVING と GROUP BY を使用する  
 次の例では、1 つの `SELECT` ステートメントの中で `GROUP BY` 句、`HAVING` 句、`WHERE` 句、および `ORDER BY` 句を使用しています。 これによって、$25 より高く平均注文数量が 5 未満の製品を除外した、グループとサマリー値が作成されます。 この結果は `ProductID` 別にまとめられます。  
  
 [!code-sql[Select#SelectExamples21](../../t-sql/queries/codesnippet/tsql/select-examples-transact_19.sql)]  
  
## <a name="m-using-having-with-sum-and-avg"></a>M. HAVING を SUM および AVG と共に使用する  
 次の例では、`SalesOrderDetail` テーブルから、注文合計額が `$1000000.00` を超え、かつ平均注文数が `3` 未満の製品を製品 ID 別にグループ化します。  
  
 [!code-sql[Select#SelectExamples22](../../t-sql/queries/codesnippet/tsql/select-examples-transact_20.sql)]  
  
 売上合計が `$2000000.00` を超える製品を検索するには、このクエリを使用します。  
  
 [!code-sql[Select#SelectExamples23](../../t-sql/queries/codesnippet/tsql/select-examples-transact_21.sql)]  
  
 各製品の集計に最低 1,500 の品目が含まれているようにするには、`HAVING COUNT(*) > 1500` を使って、`1500` 未満の合計を返す製品を除外します。 クエリは次のようになります。  
  
 [!code-sql[Select#SelectExamples24](../../t-sql/queries/codesnippet/tsql/select-examples-transact_22.sql)]  
  
## <a name="n-using-the-index-optimizer-hint"></a>北 INDEX オプティマイザー ヒントを使用する  
 次の例では、`INDEX` オプティマイザー ヒントの使用方法を 2 とおり示します。 最初の例では、オプティマイザーで非クラスター化インデックスを使用し、テーブルから行を取得しています。2 番目の例では、index = 0 を使ってテーブル スキャンを実行しています。  
  
 [!code-sql[Select#SelectExamples45](../../t-sql/queries/codesnippet/tsql/select-examples-transact_23.sql)]  
  
## <a name="m-using-option-and-the-group-hints"></a>M. OPTION ヒントと GROUP ヒントを使用する  
 次の例では、`OPTION (GROUP)` 句と共に `GROUP BY` 句を使用する方法を示します。  
  
 [!code-sql[Select#SelectExamples46](../../t-sql/queries/codesnippet/tsql/select-examples-transact_24.sql)]  
  
## <a name="o-using-the-union-query-hint"></a>O. UNION クエリ ヒントを使用する  
 次の例では、`MERGE UNION` クエリ ヒントを使用します。  
  
 [!code-sql[Select#SelectExamples47](../../t-sql/queries/codesnippet/tsql/select-examples-transact_25.sql)]  
  
## <a name="p-using-a-simple-union"></a>P. 単純な UNION を使用する  
 次の例では、結果セットに `ProductModelID` テーブルと `Name` テーブルの `ProductModel` 列と `Gloves` 列の内容が含まれています。  
  
 [!code-sql[Select#SelectExamples48](../../t-sql/queries/codesnippet/tsql/select-examples-transact_26.sql)]  
  
## <a name="q-using-select-into-with-union"></a>Q. UNION と共に SELECT INTO を使用する  
 この例では、2 番目の `INTO` ステートメントの `SELECT` 句で、`ProductResults` および `ProductModel` テーブルの指定された列のユニオンの最終的な結果セットを `Gloves` という名前のテーブルに格納することを指定します。 `Gloves` テーブルは、最初の `SELECT` ステートメントで作成されます。  
  
 [!code-sql[Select#SelectExamples49](../../t-sql/queries/codesnippet/tsql/select-examples-transact_27.sql)]  
  
## <a name="r-using-union-of-two-select-statements-with-order-by"></a>R. ORDER BY 句を指定した 2 つの SELECT ステートメントで UNION 句を使用する  
 UNION 句で使用するある種のパラメーターの順序には重要な意味があります。 次の例では、出力時に列名を変更する 2 つの `SELECT` ステートメントでの `UNION` の誤った使用法と正しい使用法を示しています。  
  
 [!code-sql[Select#SelectExamples50](../../t-sql/queries/codesnippet/tsql/select-examples-transact_28.sql)]  
  
## <a name="s-using-union-of-three-select-statements-to-show-the-effects-of-all-and-parentheses"></a>S. 3 つの SELECT ステートメントで UNION を使用して、ALL とかっこの効果を示す  
 次の例では、`UNION` を使用して 3 つのテーブルのクエリ結果を結合します。これらのテーブルはすべて同じ 5 行のデータで構成されます。 最初の例では、`UNION ALL` を使用して、重複するレコードも含めて 15 行すべてを返します。 2 番目の例では、`ALL` を指定せずに `UNION` を使用して、3 つの `SELECT` ステートメントの結果を結合したものから重複する行を削除し、5 行を返します。  
  
 3 番目の例では、最初の `ALL` と共に `UNION` を使用し、`UNION` を使用していない 2 番目の `ALL` をかっこで囲んでいます。 2 番目の `UNION` はかっこで囲まれているので、最初に処理されます。また、`ALL` オプションを使用せずに重複を削除するので、5 行を返します。 これらの 5 行は、`UNION ALL` キーワードを使用して最初の `SELECT` の結果と結合されます。 これによって 2 組の 5 行の間での重複が削除されることはありません。 最終的な結果は 10 行になります。  
  
 [!code-sql[Select#SelectExamples51](../../t-sql/queries/codesnippet/tsql/select-examples-transact_29.sql)]  
  
## <a name="see-also"></a>参照  
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [CREATE VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/create-view-transact-sql.md)   
 [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)   
 [式 &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [LIKE &#40;Transact-SQL&#41;](../../t-sql/language-elements/like-transact-sql.md)   
 [UNION &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-operators-union-transact-sql.md)   
 [EXCEPT および INTERSECT &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-operators-except-and-intersect-transact-sql.md)   
 [UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)   
 [WHERE &#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)   
 [PathName &#40;Transact-SQL&#41;](../../relational-databases/system-functions/pathname-transact-sql.md)   
 [INTO 句 &#40;Transact-SQL&#41;](../../t-sql/queries/select-into-clause-transact-sql.md)  
  
  
