---
title: INTO 句 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/23/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- INTO_TSQL
- INSERT_INTO_TSQL
- INSERT INTO
- INTO
- INTO clause
- INTO_clause_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- copying data [SQL Server], into a new table
- INTO clause
- moving data, to a new table
- table creation [SQL Server], INTO clause
- SELECT INTO statement
- inserting rows
- clauses [SQL Server], INTO
- row additions [SQL Server], INTO clause
ms.assetid: b48d69e8-5a00-48bf-b2f3-19278a72dd88
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d88b0c8e36b69bbc2a341917ec96e12ed8bfdc17
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "73981728"
---
# <a name="select---into-clause-transact-sql"></a>SELECT - INTO 句 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

SELECT...INTO は、既定のファイル グループに新しいテーブルを作成し、クエリの結果得られた行をそのテーブルに挿入します。 SELECT の完全な構文を確認するには、「[SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)」を参照してください。  
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
[ INTO new_table ]
[ ON filegroup ]
```  
  
## <a name="arguments"></a>引数  
 *new_table*   
 新しいテーブルの名前を指定します。このテーブルは選択リストで指定した列とデータ ソースから選択された行を基に作成されます。  
 
 *new_table* の形式は、選択リスト内の式を評価することによって決まります。 *new_table* 内の列は、選択リストの指定順に作成されます。 *new_table* 内の各列の名前、データ型、NULL 値の許容属性、値は、選択リスト内の対応する式と同じになります。 列の IDENTITY プロパティは、[解説] の "ID 列の使用" に示されている条件に当てはまる場合を除いて転送されます。  
  
 同じ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスの別のデータベースにテーブルを作成するには、*new_table* を *database.schema.table_name* の形式で完全修飾名として指定します。  
  
 リモート サーバーに *new_table* を作成することはできませんが、*new_table* にリモート データ ソースのデータを設定することはできます。 リモート ソース テーブルから *new_table* を作成するには、SELECT ステートメントの FROM 句で、*linked_server*.*catalog*.*schema*.*object* という形式の 4 部構成の名前を使用してソース テーブルを指定します。 FROM 句で [OPENQUERY](../../t-sql/functions/openquery-transact-sql.md) 関数か [OPENDATASOURCE](../../t-sql/functions/opendatasource-transact-sql.md) 関数を使用してリモート データ ソースを指定することもできます。  
 
 *filegroup*    
 新しいテーブルを作成するファイル グループの名前を指定します。 指定されたファイル グループがデータベースに存在する必要があります。存在しない場合は、SQL Server エンジンからエラーがスローされます。   
 
 **適用対象:** [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 以降。
  
## <a name="data-types"></a>データ型  
 FILESTREAM 属性は新しいテーブルに転送されません。 FILESTREAM BLOB がコピーされ、**varbinary(max)** BLOB として新しいテーブルに格納されます。 FILESTREAM 属性がない場合、**varbinary(max)** データ型は 2 GB までに制限されます。 FILESTREAM BLOB がこの値を超えると、エラー 7119 が発生して、ステートメントが中止されます。  
  
 既存の ID 列が新しいテーブルに選択された場合は、次の条件のいずれかが満たされている場合を除き、新しい列には IDENTITY プロパティが継承されます。  
  
-   SELECT ステートメントに結合が含まれています。  
  
-   複数の SELECT ステートメントが UNION を使用して結合されている。  
  
-   ID 列が選択リストに 2 回以上指定されている。  
  
-   ID 列が式の一部である。  
  
-   ID 列がリモート データ ソースから取得されている。  
  
これらの条件が 1 つでも満たされている場合は、列に IDENTITY プロパティは継承されず、代わりに NOT NULL として作成されます。 新しいテーブルに ID 列が必要であるものの使用できる列がない場合や、ソースの ID 列とは異なるシード値や増分値が必要な場合は、選択リストで IDENTITY 関数を使用してその列を定義します。 以下の「例」の「IDENTITY 関数を使用して ID 列を作成する」を参照してください。  

## <a name="remarks"></a>Remarks  
`SELECT...INTO` ステートメントによる操作は 2 つの部分からなります。新しいテーブルが作成され、それから行が挿入されます。  つまり、挿入できない場合、すべてロールバックされますが、新しい (空の) テーブルは残ります。  操作が全体として成功または失敗した場合、[明示的なトランザクション](../language-elements/begin-transaction-transact-sql.md)を使用します。
  
## <a name="limitations-and-restrictions"></a>制限事項と制約事項  
 テーブル変数やテーブル値パラメーターを新しいテーブルとして指定することはできません。  
  
 ソース テーブルがパーティション分割されている場合でも、`SELECT...INTO` を使用してパーティション テーブルを作成することはできません。 `SELECT...INTO` では、ソース テーブルのパーティション構成が使用されず、新しいテーブルが既定のファイル グループに作成されます。 パーティション テーブルに行を挿入するには、まずパーティション テーブルを作成してから `INSERT INTO...SELECT...FROM` ステートメントを使用する必要があります。  
  
 ソース テーブルに定義されているインデックス、制約、およびトリガーは、新しいテーブルに転送されません。`SELECT...INTO` ステートメントで指定することもできません。 これらのオブジェクトが必要な場合は、`SELECT...INTO` ステートメントの実行後に作成できます。  
  
 `ORDER BY` 句を指定しても、行が指定した順序どおりに挿入されるかどうかは保証されません。  
  
 選択リストにスパース列が含まれている場合、新しいテーブルの列にスパース列のプロパティは転送されません。 新しいテーブルでこのプロパティが必要な場合は、SELECT...INTO ステートメントの実行後に列の定義を変更してプロパティを追加してください。  
  
 リストに計算列が指定されている場合、新しいテーブル内の対応する列は計算列にはなりません。 新しい列の値は、`SELECT...INTO` が実行された時点の計算値になります。  
  
## <a name="logging-behavior"></a>ログ記録の動作  
 `SELECT...INTO` のログ記録量は、データベースに対して有効な復旧モデルによって異なります。 単純復旧モデルまたは一括ログ復旧モデルでは、一括操作は最小限しかログに記録されません。 最小ログ記録を使用する場合は、テーブルを作成してから INSERT ステートメントでそのテーブルにデータを設定するより、`SELECT...INTO` ステートメントを使用する方が効率的である可能性があります。 詳細については、「 [トランザクション ログ &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)」を参照してください。  
  
## <a name="permissions"></a>アクセス許可  
 対象となるデータベースの CREATE TABLE 権限が必要です。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-creating-a-table-by-specifying-columns-from-multiple-sources"></a>A. 複数のソースの列を指定してテーブルを作成する  
 次の例では、各種の従業員関連テーブルと住所関連テーブルから 7 つの列を選択して、[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] データベースにテーブル `dbo.EmployeeAddresses` を作成します。  
  
```sql  
SELECT c.FirstName, c.LastName, e.JobTitle, a.AddressLine1, a.City,   
    sp.Name AS [State/Province], a.PostalCode  
INTO dbo.EmployeeAddresses  
FROM Person.Person AS c  
    JOIN HumanResources.Employee AS e   
    ON e.BusinessEntityID = c.BusinessEntityID  
    JOIN Person.BusinessEntityAddress AS bea  
    ON e.BusinessEntityID = bea.BusinessEntityID  
    JOIN Person.Address AS a  
    ON bea.AddressID = a.AddressID  
    JOIN Person.StateProvince as sp   
    ON sp.StateProvinceID = a.StateProvinceID;  
GO  
```  
  
### <a name="b-inserting-rows-using-minimal-logging"></a>B. 最小ログ記録を使用して行を挿入する  
 次の例では、テーブル `dbo.NewProducts` を作成し、`Production.Product` テーブルの行を挿入します。 この例では、[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] データベースの復旧モデルが FULL に設定されていると想定しています。 したがって、最小ログ記録が使用されるようにするために、行を挿入する前に [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] データベースの復旧モデルを BULK_LOGGED に設定し、SELECT...INTO ステートメントの後に FULL に戻しています。 これにより、SELECT...INTO ステートメントが使用するトランザクション ログの領域が最小化され、ステートメントが効率的に実行されるようになります。  
  
```sql  
ALTER DATABASE AdventureWorks2012 SET RECOVERY BULK_LOGGED;  
GO  
  
SELECT * INTO dbo.NewProducts  
FROM Production.Product  
WHERE ListPrice > $25   
AND ListPrice < $100;  
GO  
ALTER DATABASE AdventureWorks2012 SET RECOVERY FULL;  
GO  
```  
  
### <a name="c-creating-an-identity-column-using-the-identity-function"></a>C. IDENTITY 関数を使用して ID 列を作成する  
 次の例では、IDENTITY 関数を使用して、[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] データベースの新しいテーブル `Person.USAddress` に ID 列を作成します。 この操作が必要になるのは、テーブルを定義する SELECT ステートメントに結合が含まれているため、IDENTITY プロパティが新しいテーブルに転送されないからです。 IDENTITY 関数で、ソース テーブル `AddressID` の `Person.Address` 列とは異なるシード値と増分値が指定されていることに注意してください。  
  
```sql  
-- Determine the IDENTITY status of the source column AddressID.  
SELECT OBJECT_NAME(object_id) AS TableName, name AS column_name, 
  is_identity, seed_value, increment_value  
FROM sys.identity_columns  
WHERE name = 'AddressID';  
  
-- Create a new table with columns from the existing table Person.Address. 
-- A new IDENTITY column is created by using the IDENTITY function.  
SELECT IDENTITY (int, 100, 5) AS AddressID,   
       a.AddressLine1, a.City, b.Name AS State, a.PostalCode  
INTO Person.USAddress   
FROM Person.Address AS a  
INNER JOIN Person.StateProvince AS b 
  ON a.StateProvinceID = b.StateProvinceID  
WHERE b.CountryRegionCode = N'US';   
  
-- Verify the IDENTITY status of the AddressID columns in both tables.  
SELECT OBJECT_NAME(object_id) AS TableName, name AS column_name, 
  is_identity, seed_value, increment_value  
FROM sys.identity_columns  
WHERE name = 'AddressID';  
```  
  
### <a name="d-creating-a-table-by-specifying-columns-from-a-remote-data-source"></a>D. リモート データ ソースの列を指定してテーブルを作成する  
 次の例は、ローカル サーバーで新しいテーブルをリモート データ ソースから作成するための 3 つの方法を示しています。 最初にリモート データ ソースへのリンクを作成した後、 リンク サーバー名の `MyLinkServer,` を、1 つ目の SELECT...INTO ステートメントの FROM 句と、2 つ目の SELECT...INTO ステートメントの OPENQUERY 関数に指定しています。 3 つ目の SELECT...INTO ステートメントでは、OPENDATASOURCE 関数を使用して、リンク サーバー名を使用する代わりに直接リモート データ ソースを指定しています。  
  
 **適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降。  
  
```sql
USE master;  
GO  
-- Create a link to the remote data source.   
-- Specify a valid server name for @datasrc as 'server_name' 
-- or 'server_name\instance_name'.  
EXEC sp_addlinkedserver @server = N'MyLinkServer',  
    @srvproduct = N' ',  
    @provider = N'SQLNCLI',   
    @datasrc = N'server_name',  
    @catalog = N'AdventureWorks2012';  
GO  

USE AdventureWorks2012;  
GO  
-- Specify the remote data source in the FROM clause using a four-part name   
-- in the form linked_server.catalog.schema.object.  
SELECT DepartmentID, Name, GroupName, ModifiedDate  
INTO dbo.Departments  
FROM MyLinkServer.AdventureWorks2012.HumanResources.Department  
GO  
-- Use the OPENQUERY function to access the remote data source.  
SELECT DepartmentID, Name, GroupName, ModifiedDate  
INTO dbo.DepartmentsUsingOpenQuery  
FROM OPENQUERY(MyLinkServer, 'SELECT *  
               FROM AdventureWorks2012.HumanResources.Department');   
GO  
-- Use the OPENDATASOURCE function to specify the remote data source.  
-- Specify a valid server name for Data Source using the format 
-- server_name or server_name\instance_name.  
SELECT DepartmentID, Name, GroupName, ModifiedDate  
INTO dbo.DepartmentsUsingOpenDataSource  
FROM OPENDATASOURCE('SQLNCLI',  
    'Data Source=server_name;Integrated Security=SSPI')  
    .AdventureWorks2012.HumanResources.Department;  
GO  
```  
  
### <a name="e-import-from-an-external-table-created-with-polybase"></a>E. PolyBase で作成された外部テーブルをインポートする  
 Hadoop または Azure ストレージからデータを永続的なストレージの SQL Server にインポートします。 `SELECT INTO` を使用して、SQL Server の永続記憶装置に、外部テーブルで参照されるデータをインポートします。 リレーショナル テーブルにその場を作成し、2 番目の手順で、テーブルの上に列ストア インデックスを作成します。  
  
 **適用対象:** [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]」を参照してください。  
  
```sql
-- Import data for car drivers into SQL Server to do more in-depth analysis.  
SELECT DISTINCT   
        Insured_Customers.FirstName, Insured_Customers.LastName,   
        Insured_Customers.YearlyIncome, Insured_Customers.MaritalStatus  
INTO Fast_Customers from Insured_Customers INNER JOIN   
(  
        SELECT * FROM CarSensor_Data where Speed > 35   
) AS SensorD  
ON Insured_Customers.CustomerKey = SensorD.CustomerKey  
ORDER BY YearlyIncome;  
```  
### <a name="f-creating-a-new-table-as-a-copy-of-another-table-and-loading-it-a-specified-filegroup"></a>F. 新しいテーブルを別のテーブルのコピーとして作成し、指定したファイル グループに読み込む
次の例は、新しいテーブルを別のテーブルのコピーとして作成し、ユーザーの既定のファイル グループとは異なる、指定したファイル グループに読み込む方法を示しています。

 **適用対象:** [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 以降。

```sql
ALTER DATABASE [AdventureWorksDW2016] ADD FILEGROUP FG2;
ALTER DATABASE [AdventureWorksDW2016]
ADD FILE
(
NAME='FG2_Data',
FILENAME = '/var/opt/mssql/data/AdventureWorksDW2016_Data1.mdf'
)
TO FILEGROUP FG2;
GO
SELECT * INTO [dbo].[FactResellerSalesXL] ON FG2 FROM [dbo].[FactResellerSales];
```
  
## <a name="see-also"></a>参照  
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [SELECT の例 &#40;Transact-SQL&#41;](../../t-sql/queries/select-examples-transact-sql.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [IDENTITY &#40;関数&#41; &#40;Transact-SQL&#41;](../../t-sql/functions/identity-function-transact-sql.md)  
  
  
