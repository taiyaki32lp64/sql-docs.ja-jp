---
title: MSSQLSERVER_207 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 207 (Database Engine error)
ms.assetid: d1ab00c7-0331-437a-84fe-bae53b82feec
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 0fa8c6371ba5889cde5afe2c66b036a1ec8c031d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68056804"
---
# <a name="mssqlserver207"></a>MSSQLSERVER_207
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|207|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|SQ_BADCOL|  
|メッセージ テキスト|列名 '%.*ls' が無効です。|  
  
## <a name="explanation"></a>説明  
このクエリ エラーは次のいずれかの問題が原因で生じている可能性があります。  
  
-   列名にスペルミスがあるか、指定されたテーブルにその列が存在しません。  
  
-   データベースの照合順序で大文字と小文字が区別され、クエリで指定された列名の大文字と小文字がテーブルで定義された列のものと一致していません。 たとえば、データベースの照合順序で大文字と小文字が区別され、テーブルで列が **LastName** と定義されている場合、クエリで **Lastname** または **lastname** と指定してその列を参照すると、エラー 207 が返されます。これは列名が一致しないためです。  
  
-   列の別名 (SELECT 句で定義) が、WHERE、GROUP BY 句などの別の句で参照されています。 たとえば、次のクエリでは SELECT 句で列の別名 `Year` が定義されており、GROUP BY 句で参照されています。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT DATEPART(yyyy,OrderDate) AS Year, SUM(TotalDue) AS Total  
    FROM Sales.SalesOrderHeader  
    GROUP BY Year;  
    ```  
  
    クエリの各句が論理的に処理される順序に基づいて、この例ではエラー 207 が返されます。 この処理の順序は次のとおりです。  
  
    1.  FROM  
  
    2.  ON  
  
    3.  JOIN  
  
    4.  WHERE  
  
    5.  GROUP BY  
  
    6.  WITH CUBE または WITH ROLLUP  
  
    7.  HAVING  
  
    8.  SELECT  
  
    9. DISTINCT  
  
    10. ORDER BY  
  
    11. TOP  
  
    列の別名は SELECT 句が処理されるまでは定義されないため、GROUP BY 句が処理される時点では別名が不明になってしまいます。  
  
-   *<merge_matched>* 句がソース テーブルの列を参照していて、WHEN NOT MATCHED BY SOURCE 句でソース テーブルから行が返されない場合、MERGE ステートメントでこのエラーが発生します。 このエラーは、クエリに行が返されないと、ソース テーブルの列にアクセスできないために発生します。 たとえば、ソース テーブルの `WHEN NOT MATCHED BY SOURCE THEN UPDATE SET TargetTable.Col1 = SourceTable.Col1` にアクセスできないと、`Col1` 句によってステートメントが失敗することになります。  
  
## <a name="user-action"></a>ユーザーの操作  
次の情報を確認し、必要に応じてステートメントを修正します。  
  
-   列名がテーブルに存在し、スペルも正しい。 次の例では **sys.columns** カタログ ビューに対するクエリが実行され、指定されたテーブルのすべての列名が返されます。  
  
    ```  
    SELECT name FROM sys.columns WHERE object_id = OBJECT_ID('schema_name.table_name');  
    ```  
  
-   データベースの照合順序で大文字と小文字が区別されるかどうか。 次のステートメントでは、指定されたデータベースの照合順序が返されます。  
  
    ```  
    SELECT collation_name FROM sys.databases WHERE name = 'database_name';  
    ```  
  
    照合順序名に含まれる省略形 CS は、照合順序で大文字と小文字が区別されることを示します。 たとえば、Latin1_General_CS_AS は、大文字と小文字およびアクセントが区別される照合順序です。 テーブルで定義されている列名の大文字と小文字に一致するように、列名を変更してください。  
  
-   列の別名が不適切に参照されている。 適切な句の中で、別名を定義する式を再度記述するか、派生テーブルを使って、ステートメントを変更してください。 次の例では、GROUP BY 句の中で、別名 `Year` を定義する式を再度記述しています。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT DATEPART(yyyy,OrderDate) AS Year ,SUM(TotalDue) AS Total  
    FROM Sales.SalesOrderHeader  
    GROUP BY DATEPART(yyyy,OrderDate);  
    ```  
  
    次の例では、派生テーブルを使って、別名をクエリ内の他の句でも使用できるようにしています。 別名 `Year` は FROM 句内で定義されており、これが最初に処理されるため、この別名はクエリ内の他の句でも使用できるようになります。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT d.Year, SUM(TotalDue) AS Total  
    FROM (SELECT DATEPART(yyyy,OrderDate) AS Year, TotalDue  
          FROM Sales.SalesOrderHeader)AS d  
    GROUP BY Year;  
    ```  
  
-   MERGE ステートメントの WHEN NOT MATCHED BY SOURCE 句が、アクセスできる値を参照している。 WHEN NOT MATCHED BY SOURCE 句でソース テーブルから少なくとも 1 行が返されるように MERGE ステートメントを変更します。 たとえば、この句に指定した検索条件を追加または変更する必要があります。 または、句を変更して、ソース テーブルを参照しない値を指定します。 たとえば、`WHEN NOT MATCHED BY SOURCE THEN UPDATE SET TargetTable.Col1 = <expression, or other available value>` のようになります。  
  
## <a name="see-also"></a>参照  
[MERGE &#40;Transact-SQL&#41;](~/t-sql/statements/merge-transact-sql.md)  
[FROM &#40;Transact-SQL&#41;](~/t-sql/queries/from-transact-sql.md)  
[SELECT &#40;Transact-SQL&#41;](~/t-sql/queries/select-transact-sql.md)  
[UPDATE &#40;Transact-SQL&#41;](~/t-sql/queries/update-transact-sql.md)  
  
