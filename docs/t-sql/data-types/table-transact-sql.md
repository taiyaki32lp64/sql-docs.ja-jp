---
title: table (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/27/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- table data type [SQL Server]
- table variables [SQL Server]
ms.assetid: 1ef0b60e-a64c-4e97-847b-67930e3973ef
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: a3ff2605e0c872bd5e544d618c88dc179e3c3b43
ms.sourcegitcommit: 03884a046aded85c7de67ca82a5b5edbf710be92
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/27/2019
ms.locfileid: "74564800"
---
# <a name="table-transact-sql"></a>table (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

後で処理できるように結果セットを格納するための特別なデータ型です。 **table** は主に、テーブル値関数の結果セットとして返される行のセットの一時的な保存に使用します。 型には、関数および変数を宣言することができます **テーブル**です。 **テーブル** 変数は、関数、ストアド プロシージャ、およびバッチで使用できます。 **table** 型の変数を宣言するには、[DECLARE @local_variable](../../t-sql/language-elements/declare-local-variable-transact-sql.md)を使用します。
  

**適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降)、[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>構文  
  
```sql
table_type_definition ::=   
    TABLE ( { <column_definition> | <table_constraint> } [ ,...n ] )   
  
<column_definition> ::=   
    column_name scalar_data_type   
    [ COLLATE <collation_definition> ]   
    [ [ DEFAULT constant_expression ] | IDENTITY [ ( seed , increment ) ] ]   
    [ ROWGUIDCOL ]   
    [ column_constraint ] [ ...n ]   
  
 <column_constraint> ::=   
    { [ NULL | NOT NULL ]   
    | [ PRIMARY KEY | UNIQUE ]   
    | CHECK ( logical_expression )   
    }   
  
<table_constraint> ::=   
     { { PRIMARY KEY | UNIQUE } ( column_name [ ,...n ] )  
     | CHECK ( logical_expression )   
     }   
```  
  
## <a name="arguments"></a>引数  
*table_type_definition*  
CREATE TABLE でテーブルを定義するために使用する情報のサブセットと同じです。 テーブルの定義には、列の定義、名前、データ型、制約が含まれます。 許可される制約の種類は、PRIMARY KEY、UNIQUE KEY、NULL だけです。  
構文の詳細については、「[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)」、「[CREATE FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md)」、および「[DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)」をご覧ください。
  
*collation_definition*  
[!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows ロケールと比較形式、Windows ロケールとバイナリ表記から構成される列の照合順序、または [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 照合順序です。 *collation_definition* が指定されていない場合、列は現在のデータベースの照合順序を継承します。 または、列が共通言語ランタイム (CLR) ユーザー定義型として定義されている場合は、ユーザー定義型の照合順序が列に継承されます。
  
## <a name="remarks"></a>解説  
以下の例に示すように、バッチの FROM 句の名前による **table** 参照変数:
  
```sql
SELECT Employee_ID, Department_ID FROM @MyTableVar;  
```  
  
FROM 句では、外部 **テーブル** 変数は、次の例で示すように、別名を使用して参照する必要があります。
  
```sql
SELECT EmployeeID, DepartmentID   
FROM @MyTableVar m  
JOIN Employee on (m.EmployeeID =Employee.EmployeeID AND  
   m.DepartmentID = Employee.DepartmentID);  
```  
  
**table** 変数では、クエリ プランが変化せず、再コンパイルの影響が大きい場合がある小規模のクエリに対して、次の利点を提供します。
-   A **テーブル** 変数は、ローカル変数のように動作します。 この変数には適切に定義されたスコープがあります。 この変数は、それが宣言されている関数、ストアド プロシージャ、またはバッチです。  
     そのスコープの中、 **テーブル** 変数は、通常のテーブルのように使用できます。 また、SELECT、INSERT、UPDATE、および DELETE の各ステートメントで、テーブルまたはテーブル式が使用されている任意の場所で適用できます。 ただし、**table** は次のステートメントで使用できません。  
  
```sql
SELECT select_list INTO table_variable;
```
  
**table** 変数は、それが定義されている関数、ストアド プロシージャ、またはバッチの終了時に自動的に削除されます。
  
-   ストアド プロシージャで **table** 変数を使用すると、パフォーマンスに影響を与えるコストベースの選択肢がないとき、一時テーブルを使用する場合に比べ、ストアド プロシージャの再コンパイルが少なくなります。  
-   使用するトランザクション **テーブル** で変数が最後の更新の間のみ、 **テーブル** 変数です。 そのため、**table** 変数の場合、ロックとログに必要なリソースが少なくなります。  
  
## <a name="limitations-and-restrictions"></a>制限事項と制約事項
**table** 変数には配布の統計情報がありません。 再コンパイルをトリガーしません。 多くの場合、オプティマイザーはテーブル変数に行がないことを前提としてクエリ プランを構築します。 このため、多数の行 (100 行を超える行) を使用する可能性がある場合は、テーブル変数を慎重に使用する必要があります。 このような場合、一時テーブルによって問題が解決することがあります。 テーブル変数を他のテーブルに結合するクエリの場合は、RECOMPILE ヒントを使用します。このヒントを使用すると、オプティマイザーがテーブル変数に適切なカーディナリティを使用するようになります。
  
**table** 変数は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オプティマイザーのコストベース推論モデルでサポートされていません。 したがって、効果的なクエリ プランを実現するためにコストベースの選択が必要な場合は、使用しないでください。 コストベースの選択が必要な場合は、一時テーブルが推奨されます。 このプランには通常、結合、並列処理の決定、インデックス選択を含むクエリが含まれます。
  
**table** 変数を変更するクエリでは、並列クエリ実行プランを生成しません。 大きな **table** 変数や複雑なクエリの **table** 変数を変更すると、パフォーマンスに影響が出ることがあります。 **table** 変数が変更されるような状況では、一時テーブルを代わりに使用することを検討してください。 詳細については、「[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)」を参照してください。 読み取るクエリは **テーブル** 変数を変更せずの並列処理を実行できます。

> [!IMPORTANT]
> データベース互換性レベル 150 では、**テーブル変数の遅延コンパイル**の導入により、テーブル変数のパフォーマンスが向上します。  詳細については、「[テーブル変数の遅延コンパイル](../../relational-databases/performance/intelligent-query-processing.md#table-variable-deferred-compilation)」をご覧ください。
>
  
**table** 変数でインデックスを明示的に作成することはできません。**table** 変数では統計が保持されません。 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 以降では、特定のインデックスの種類をテーブル定義にインライン作成できる新しい構文が導入されました。  この新しい構文を使うと、テーブル定義の一部として**テーブル**変数にインデックスを作成できます。 場合によっては、完全なインデックスのサポートと統計を提供する一時テーブルを使用した方が、パフォーマンスが向上する場合があります。 一時テーブルとインライン インデックス作成について詳しくは、「[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)」をご覧ください。

CHECK 制約、既定値、計算列、**table** 型の宣言は、ユーザー定義関数を呼び出すことはできません。
  
**table** 変数間の代入操作はサポートされていません。
  
**table** 変数はスコープが限られており、持続性のあるデータベースに含まれないため、トランザクション ロールバックの影響を受けません。
  
table 変数は作成後に変更できません。
  
## <a name="examples"></a>例  
  
### <a name="a-declaring-a-variable-of-type-table"></a>A. table 型の変数を宣言する  
次の例では、UPDATE ステートメントの OUTPUT 句で指定される値を格納する `table` 変数を作成します。 この後に、`SELECT` 内の値、および `@MyTableVar` テーブルの更新操作の結果を返す 2 つの `Employee` ステートメントが続きます。 `INSERTED.ModifiedDate` 列の結果が、`Employee` テーブルの `ModifiedDate` 列の値と異なります。 この違いは、`AFTER UPDATE` の値を現在の日付に更新する `ModifiedDate` トリガーが `Employee` テーブルで定義されることに起因します。 ただし、`OUTPUT` が返す列には、トリガーが起動される前の値が反映されています。 詳細については、「[OUTPUT 句 &#40;Transact-SQL&#41;](../../t-sql/queries/output-clause-transact-sql.md)」を参照してください。
  
```sql
USE AdventureWorks2012;  
GO  
DECLARE @MyTableVar table(  
    EmpID int NOT NULL,  
    OldVacationHours int,  
    NewVacationHours int,  
    ModifiedDate datetime);  
UPDATE TOP (10) HumanResources.Employee  
SET VacationHours = VacationHours * 1.25   
OUTPUT INSERTED.BusinessEntityID,  
       DELETED.VacationHours,  
       INSERTED.VacationHours,  
       INSERTED.ModifiedDate  
INTO @MyTableVar;  
--Display the result set of the table variable.  
SELECT EmpID, OldVacationHours, NewVacationHours, ModifiedDate  
FROM @MyTableVar;  
GO  
--Display the result set of the table.  
--Note that ModifiedDate reflects the value generated by an  
--AFTER UPDATE trigger.  
SELECT TOP (10) BusinessEntityID, VacationHours, ModifiedDate  
FROM HumanResources.Employee;  
GO  
```  
  
### <a name="b-creating-an-inline-table-valued-function"></a>B. インライン テーブル値関数を作成する  
次の例では、インライン テーブル値関数を返します。 ここでは、店舗に販売された製品ごとに 3 つの列を返します。`ProductID`、`Name`、`YTD Total` (今年に入ってからの店舗別合計の集計) です。
  
```sql
USE AdventureWorks2012;  
GO  
IF OBJECT_ID (N'Sales.ufn_SalesByStore', N'IF') IS NOT NULL  
    DROP FUNCTION Sales.ufn_SalesByStore;  
GO  
CREATE FUNCTION Sales.ufn_SalesByStore (@storeid int)  
RETURNS TABLE  
AS  
RETURN   
(  
    SELECT P.ProductID, P.Name, SUM(SD.LineTotal) AS 'Total'  
    FROM Production.Product AS P   
    JOIN Sales.SalesOrderDetail AS SD ON SD.ProductID = P.ProductID  
    JOIN Sales.SalesOrderHeader AS SH ON SH.SalesOrderID = SD.SalesOrderID  
    JOIN Sales.Customer AS C ON SH.CustomerID = C.CustomerID  
    WHERE C.StoreID = @storeid  
    GROUP BY P.ProductID, P.Name  
);  
GO  
```  
  
関数を呼び出すには、次のクエリを実行します。
  
```sql
SELECT * FROM Sales.ufn_SalesByStore (602);  
```  
  
## <a name="see-also"></a>参照
[COLLATE &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/4ba6b7d8-114a-4f4e-bb38-fe5697add4e9)  
[CREATE FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md)  
[ユーザー定義関数](../../relational-databases/user-defined-functions/user-defined-functions.md)  
[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
[テーブル値パラメーターの使用 &#40;データベース エンジン&#41;](../../relational-databases/tables/use-table-valued-parameters-database-engine.md)  
[クエリ ヒント &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md)
