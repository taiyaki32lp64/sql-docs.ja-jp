---
title: CREATE PARTITION FUNCTION (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/19/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CREATE PARTITION FUNCTION
- PARTITION
- PARTITION FUNCTION
- PARTITION_FUNCTION_TSQL
- PARTITION_TSQL
- CREATE_PARTITION_FUNCTION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- RANGE RIGHT partition functions
- RANGE LEFT partition functions
- partitioned indexes [SQL Server], functions
- functions [SQL Server], creating
- partition functions [SQL Server], creating
- partitioned tables [SQL Server], functions
- CREATE PARTITION FUNCTION statement
ms.assetid: 9dfe8b76-721e-42fd-81ae-14e22258c4f2
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 2693b552008760025977a4c0ed0d3f3c3065713a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67912613"
---
# <a name="create-partition-function-transact-sql"></a>CREATE PARTITION FUNCTION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  テーブルまたはインデックスの行を指定された列の値に基づいてパーティションにマップする関数を、現在のデータベース内に作成します。 CREATE PARTITION FUNCTION の使用は、パーティション テーブルまたはパーティション インデックスを作成する最初の手順です。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] では、1 つのテーブルまたはインデックスは、最大 15,000 個のパーティションに分割できます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
CREATE PARTITION FUNCTION partition_function_name ( input_parameter_type )  
AS RANGE [ LEFT | RIGHT ]   
FOR VALUES ( [ boundary_value [ ,...n ] ] )   
[ ; ]  
```  
  
## <a name="arguments"></a>引数  
 *partition_function_name*  
 パーティション関数の名前です。 パーティション関数の名前は、データベース内で一意であり、かつ[識別子](../../relational-databases/databases/database-identifiers.md)のルールに従っている必要があります。  
  
 *input_parameter_type*  
 パーティション分割に使用される列のデータ型です。 すべてのデータ型は、 **text**、 **ntext**、 **image**、 **xml**、 **timestamp**、 **varchar(max)** 、 **nvarchar(max)** 、 **varbinary(max)** 、別名データ型、または CLR ユーザー定義データ型を除いて、列を分割して使用することができます。  
  
 パーティション分割列と呼ばれる実際の列は、CREATE TABLE ステートメントまたは CREATE INDEX ステートメントで指定します。  
  
 *boundary_value*  
 *partition_function_name* を使用するパーティション テーブルまたはインデックスの各パーティションの境界値を指定します。 *boundary_value* が空の場合、このパーティション関数では *partition_function_name* を使用するテーブルまたはインデックス全体が 1 つのパーティションにマップされます。 CREATE TABLE ステートメントまたは CREATE INDEX ステートメントで指定された 1 つのパーティション分割列のみが使用できます。  
  
 *boundary_value* は、変数を参照できる定数式です。 これには、ユーザー定義型の変数、または関数およびユーザー定義関数が含まれます。 この定数式で [!INCLUDE[tsql](../../includes/tsql-md.md)] 式を参照することはできません。 *boundary_value* は、*input_parameter_type* に指定された対応するデータ型と同じであるか、そのデータ型に暗黙的に変換できる必要があります。また、暗黙的に変換している間は、対応する *input_parameter_type* と値のサイズおよび小数点以下桁数が異なる方法で切り捨てることはできません。  

> [!NOTE]  
>  *boundary_value* に、**datetime** または **smalldatetime** 型のリテラルが含まれる場合、それらのリテラルは、セッション言語が us_english であることを前提に評価されます。 ただし、この動作は非推奨とされます。 すべてのセッション言語でパーティション関数の定義が正しく認識されるようにするには、yyyymmdd 形式のようにすべての言語設定で同様に解釈される定数を使用するか、リテラルを特定の型に明示的に変換することをお勧めします。 サーバーのセッション言語を確認するには、`SELECT @@LANGUAGE` を実行してください。
>
> 詳細については、「[リテラル日付文字列を DATE 値に非決定論的に変換する](../data-types/nondeterministic-convert-date-literals.md)」を参照してください。
  
 *...n*  
 *boundary_value* で与えられる値の数を指定します。14,999 以下の数を指定する必要があります。 作成されるパーティションの数は *n* + 1 になります。 値を順序どおり指定する必要はありません。 値が順不同の場合、[!INCLUDE[ssDE](../../includes/ssde-md.md)] は値を並び替えて、関数を作成し、値が順に並んでいないという警告を返します。 *n* に重複値が含まれている場合、データベース エンジンはエラーを返します。  
  
 **LEFT** | RIGHT  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]が境界値を左から右の昇順にソートする場合に、*boundary_value* [ **,** _...n_ ] が各境界値間隔のどちら側 (左または右) に属するかを指定します。 指定しない場合は、LEFT が既定値です。  
  
## <a name="remarks"></a>Remarks  
 パーティション関数のスコープは、関数が作成されたデータベース内に制限されます。 データベース内では、パーティション関数は他の関数とは別の名前空間に配置されます。  
  
 NULL が境界値として指定され、RIGHT が指定された場合を除き、パーティション分割列に NULL 値がある行はすべて、左端のパーティションに配置されます。 この場合、左端のパーティションは空のパーティションになり、NULL 値は次のパーティションに配置されます。  
  
## <a name="permissions"></a>アクセス許可  
 CREATE PARTITION FUNCTION を実行するには、次のいずれかの権限を使用できます。  
  
-   ALTER ANY DATASPACE 権限。 この権限は、既定では **sysadmin** 固定サーバー ロール、 **db_owner** 固定データベース ロール、および **db_ddladmin** 固定データベース ロールのメンバーに与えられています。  
  
-   パーティション関数が作成されているデータベースの CONTROL 権限または ALTER 権限。  
  
-   パーティション関数が作成されているデータベースのサーバーでの CONTROL SERVER 権限または ALTER ANY DATABASE 権限。  
  
##  <a name="BKMK_examples"></a> 使用例  
  
### <a name="a-creating-a-range-left-partition-function-on-an-int-column"></a>A. int 型の列に RANGE LEFT パーティション関数を作成する  
 次のパーティション関数は、テーブルまたはインデックスを 4 つのパーティションに分割します。  
  
```sql  
CREATE PARTITION FUNCTION myRangePF1 (int)  
AS RANGE LEFT FOR VALUES (1, 100, 1000);  
```  
  
 次の表は、パーティション分割列 **col1** でこのパーティション関数を使用するテーブルがどのようにパーティション分割されるかを示します。  
  
|パーティション|1|2|3|4|  
|---------------|-------|-------|-------|-------|  
|**値**|**col1** <= `1`|**col1** > `1` AND **col1** <= `100`|**col1** > `100` AND **col1** <=`1000`|**col1** > `1000`|  
  
### <a name="b-creating-a-range-right-partition-function-on-an-int-column"></a>B. int 型の列に RANGE RIGHT パーティション関数を作成する  
 次のパーティション関数は、*boundary_value* [ **,** _...n_ ] に、RANGE RIGHT を除いて前の例と同じ値を指定します。  
  
```sql  
CREATE PARTITION FUNCTION myRangePF2 (int)  
AS RANGE RIGHT FOR VALUES (1, 100, 1000);  
```  
  
 次の表は、パーティション分割列 **col1** でこのパーティション関数を使用するテーブルがどのようにパーティション分割されるかを示します。  
  
|パーティション|1|2|3|4|  
|---------------|-------|-------|-------|-------|  
|**値**|**col1** \< `1`|**col1** >= `1` AND **col1** \< `100`|**col1** >= `100` AND **col1** \< `1000`|**col1** >= `1000`| 
  
### <a name="c-creating-a-range-right-partition-function-on-a-datetime-column"></a>C. datetime 型の列に RANGE RIGHT パーティション関数を作成する  
 次のパーティション関数では、テーブルまたはインデックスを、**datetime** 列の値が表す月ごとに 12 のパーティションに分割します。  
  
```sql  
CREATE PARTITION FUNCTION [myDateRangePF1] (datetime)  
AS RANGE RIGHT FOR VALUES ('20030201', '20030301', '20030401',  
               '20030501', '20030601', '20030701', '20030801',   
               '20030901', '20031001', '20031101', '20031201');  
```  
  
 次の表は、パーティション分割列 **datecol** で、このパーティション関数を使用するテーブルまたはインデックスがどのようにパーティション分割されるかを示します。  
  
|パーティション|1|2|[...]|11|12|  
|---------------|-------|-------|---------|--------|--------|  
|**値**|**datecol** \< `February 1, 2003`|**datecol** >= `February 1, 2003` AND **datecol** \< `March 1, 2003`||**datecol** >= `November 1, 2003` AND **col1** \< `December 1, 2003`|**datecol** >= `December 1, 2003`| 
  
### <a name="d-creating-a-partition-function-on-a-char-column"></a>D. char 型の列にパーティション関数を作成する  
 次のパーティション関数は、テーブルまたはインデックスを 4 つのパーティションに分割します。  
  
```sql  
CREATE PARTITION FUNCTION myRangePF3 (char(20))  
AS RANGE RIGHT FOR VALUES ('EX', 'RXE', 'XR');  
```  
  
 次の表は、パーティション分割列 **col1** でこのパーティション関数を使用するテーブルがどのようにパーティション分割されるかを示します。  
  
|パーティション|1|2|3|4|  
|---------------|-------|-------|-------|-------|  
|**値**|**col1** \< `EX`...|**col1** >= `EX` AND **col1** \< `RXE`...|**col1** >= `RXE` AND **col1** \< `XR`...|**col1** >= `XR`| 
  
### <a name="e-creating-15000-partitions"></a>E. 15,000 のパーティションを作成する  
 次のパーティション関数は、テーブルまたはインデックスを 15,000 のパーティションに分割します。  
  
```sql  
--Create integer partition function for 15,000 partitions.  
DECLARE @IntegerPartitionFunction nvarchar(max) = 
    N'CREATE PARTITION FUNCTION IntegerPartitionFunction (int) 
    AS RANGE RIGHT FOR VALUES (';  
DECLARE @i int = 1;  
WHILE @i < 14999  
BEGIN  
SET @IntegerPartitionFunction += CAST(@i as nvarchar(10)) + N', ';  
SET @i += 1;  
END  
SET @IntegerPartitionFunction += CAST(@i as nvarchar(10)) + N');';  
EXEC sp_executesql @IntegerPartitionFunction;  
GO  
```  
  
### <a name="f-creating-partitions-for-multiple-years"></a>F. 複数年のパーティションを作成する  
 次のパーティション関数は、テーブルまたはインデックスを **datetime2** 列の 50 のパーティションに分割します。 2007 年 1 月から 2011 年 1 月までの各月に対して 1 つのパーティションがあります。  
  
```sql  
--Create date partition function with increment by month.  
DECLARE @DatePartitionFunction nvarchar(max) = 
    N'CREATE PARTITION FUNCTION DatePartitionFunction (datetime2) 
    AS RANGE RIGHT FOR VALUES (';  
DECLARE @i datetime2 = '20070101';  
WHILE @i < '20110101'  
BEGIN  
SET @DatePartitionFunction += '''' + CAST(@i as nvarchar(10)) + '''' + N', ';  
SET @i = DATEADD(MM, 1, @i);  
END  
SET @DatePartitionFunction += '''' + CAST(@i as nvarchar(10))+ '''' + N');';  
EXEC sp_executesql @DatePartitionFunction;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [パーティション テーブルとパーティション インデックス](../../relational-databases/partitions/partitioned-tables-and-indexes.md)   
 [$PARTITION &#40;Transact-SQL&#41;](../../t-sql/functions/partition-transact-sql.md)   
 [ALTER PARTITION FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-partition-function-transact-sql.md)   
 [DROP PARTITION FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-partition-function-transact-sql.md)   
 [CREATE PARTITION SCHEME &#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-scheme-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sys.partition_functions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partition-functions-transact-sql.md)   
 [sys.partition_parameters &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partition-parameters-transact-sql.md)   
 [sys.partition_range_values &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partition-range-values-transact-sql.md)   
 [sys.partitions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md)   
 [sys.tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)  
  
  

