---
title: sys.dm_sql_referenced_entities (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 05/01/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_sql_referenced_entities_TSQL
- dm_sql_referenced_entities
- sys.dm_sql_referenced_entities
- sys.dm_sql_referenced_entities_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_sql_referenced_entities dynamic management function
ms.assetid: 077111cb-b860-4d61-916f-bac5d532912f
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 64ddba95ec5c7fb8dfa6e6e685fcf9d5b6846fe9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68090671"
---
# <a name="sysdmsqlreferencedentities-transact-sql"></a>sys.dm_sql_referenced_entities (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

1 行で指定した参照元エンティティの定義で名前によって参照される各ユーザー定義エンティティを返します[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 1 つのユーザー定義エンティティが呼び出されたときに、2 つのエンティティ間の依存関係が作成された、*エンティティを参照*と呼ばれる、別のユーザー定義エンティティの保存されている SQL 式で名前によって表示される、*エンティティを参照します*。 たとえば、参照元エンティティとしてストアド プロシージャを指定した場合、この関数は、そのストアド プロシージャの中で参照されたすべてのユーザー定義エンティティ (テーブル、ビュー、ユーザー定義型 (UDT)、他のストアド プロシージャなど) を返します。  
  
 この動的管理関数に参照元エンティティを指定すると、そのエンティティによって参照された次の種類のエンティティをレポートできます。  
  
-   スキーマ バインド エンティティ  
  
-   非スキーマ バインド エンティティ  
  
-   複数のデータベースやサーバーにまたがるエンティティ  
  
-   スキーマ バインド エンティティおよび非スキーマ バインド エンティティの列レベルの依存関係  
  
-   ユーザー定義型 (別名および CLR UDT)  
  
-   XML スキーマ コレクション  
  
-   パーティション関数  

## <a name="syntax"></a>構文  
  
```  
sys.dm_sql_referenced_entities (  
    ' [ schema_name. ] referencing_entity_name ' ,
    ' <referencing_class> ' )  
  
<referencing_class> ::=  
{  
    OBJECT  
  | DATABASE_DDL_TRIGGER  
  | SERVER_DDL_TRIGGER  
}  
```  
  
## <a name="arguments"></a>引数  
 [ *schema_name*. *referencing_entity_name*  
 参照元エンティティの名前です。 *schema_name*が参照元のクラスが OBJECT の場合に必要です。  
  
 *schema_name.referencing_entity_name*は**nvarchar (517)** します。  
  
 *< Referencing_class >* :: = {オブジェクト |DATABASE_DDL_TRIGGER |SERVER_DDL_TRIGGER です。  
 指定された参照元エンティティのクラスです。 クラスは 1 つのステートメントに 1 つだけ指定できます。  
  
 *< referencing_class >* は**nvarchar (60)** します。  
  
## <a name="table-returned"></a>返されるテーブル  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|referencing_minor_id|**int**|参照元エンティティが列の場合は列 ID。それ以外の場合は 0。 NULL 値は許可されません。|  
|referenced_server_name|**sysname**|参照先エンティティのサーバー名。<br /><br /> 有効な 4 部構成の名前を指定することによって作成されたサーバー間依存関係については、この列に値が格納されます。 マルチパート名については、次を参照してください。 [TRANSACT-SQL 構文表記規則&#40;TRANSACT-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)します。<br /><br /> 4 部構成の名前を指定せずにエンティティが参照される非スキーマ バインド依存関係の場合は NULL。<br /><br /> のみ定義できます 2 つの部分を使用して、同じデータベースである必要がありますのでスキーマ バインド エンティティの場合は NULL (*schema.object*) の名前。|  
|referenced_database_name|**sysname**|参照先エンティティのデータベース名。<br /><br /> 有効な 3 部構成または 4 部構成の名前を指定することによって作成された複数データベースまたは複数サーバーにまたがる参照については、この列に値が格納されます。<br /><br /> 1 部構成または 2 部構成の名前を使って指定された非スキーマ バインド参照の場合は NULL。<br /><br /> のみ定義できます 2 つの部分を使用して、同じデータベースである必要がありますのでスキーマ バインド エンティティの場合は NULL (*schema.object*) の名前。|  
|referenced_schema_name|**sysname**|参照先エンティティが属しているスキーマ。<br /><br /> スキーマ名を指定せずにエンティティが参照される非スキーマ バインド参照の場合は NULL。<br /><br /> スキーマ バインド参照の場合、NULL にすることはできません。|  
|referenced_entity_name|**sysname**|参照先エンティティの名前。 NULL 値は許可されません。|  
|referenced_minor_name|**sysname**|参照先エンティティが列の場合は列名。それ以外の場合は NULL。 たとえば、参照先エンティティ自体を一覧表示する行では、referenced_minor_name は NULL になります。<br /><br /> 参照元エンティティの中で列が名前で指定されていた場合、または SELECT * ステートメントの中で親エンティティが使用されていた場合、参照先エンティティは列になります。|  
|referenced_id|**int**|参照先エンティティの ID。 referenced_minor_id が 0 以外の場合、referenced_id は、その列が定義されているエンティティになります。<br /><br /> 複数サーバーにまたがる参照の場合は常に NULL。<br /><br /> 複数データベースにまたがる参照で、データベースがオフラインか、エンティティをバインドできないために ID を判別できない場合は NULL。<br /><br /> データベース内の参照で ID を判別できない場合は、NULL。 非スキーマ バインド参照では、データベース、または名前解決は、呼び出し元に依存する参照先のエンティティが存在しない場合、ID を解決できません。  後者の場合、is_caller_dependent は 1 に設定します。<br /><br /> スキーマ バインド参照の場合、NULL にすることはできません。|  
|referenced_minor_id|**int**|参照先エンティティが列の場合は列 ID。それ以外の場合は 0。 たとえば、参照先エンティティ自体を一覧表示する行では、referenced_minor_id は 0 になります。<br /><br /> 非スキーマ バインド参照の場合、列の依存関係は、すべての参照先エンティティがバインドできる場合にのみ報告されます。 バインドできない参照先エンティティが 1 つでも存在した場合、列レベルの依存関係は報告されず、referenced_minor_id は 0 になります。 例 D を参照してください。|  
|referenced_class|**tinyint**|参照先エンティティのクラス。<br /><br /> 1 = オブジェクトまたは列<br /><br /> 6 = 型<br /><br /> 10 = XML スキーマ コレクション<br /><br /> 21 = パーティション関数|  
|referenced_class_desc|**nvarchar(60)**|参照先エンティティのクラスの説明。<br /><br /> OBJECT_OR_COLUMN<br /><br /> TYPE<br /><br /> XML_SCHEMA_COLLECTION<br /><br /> PARTITION_FUNCTION|  
|is_caller_dependent|**bit**|参照先エンティティのスキーマ バインドが実行時に発生することを示します。したがって、エンティティ ID の解決方法は、呼び出し元のスキーマに依存します。 これが該当するのは、参照先エンティティがストアド プロシージャ、拡張ストアド プロシージャ、または、EXECUTE ステートメント内で呼び出されるユーザー定義関数である場合です。<br /><br /> 1 = 参照先エンティティが呼び出し元に依存し、実行時に解決されます。 この場合、referenced_id は NULL です。<br /><br /> 0 = 参照先エンティティの ID は呼び出し元に依存しません。 スキーマ バインド参照のほか、スキーマ名を明示的に指定するデータベース間参照やサーバー間参照の場合は常に 0 になります。 たとえば、`EXEC MyDatabase.MySchema.MyProc` 形式のエンティティ参照は呼び出し元に依存しません。 ただし、`EXEC MyDatabase..MyProc` 形式の参照は呼び出し元に依存します。|  
|is_ambiguous|**bit**|参照があいまいであり、実行時、ユーザー定義関数、ユーザー定義型 (UDT)、または型の列への xquery 参照に解決できることを示します**xml**します。 たとえば、ステートメント`SELECT Sales.GetOrder() FROM Sales.MySales`ストアド プロシージャで定義されています。 `Sales.GetOrder()` が `Sales` スキーマ内のユーザー定義関数なのか、`Sales` という名前のメソッドを持つ UDT 型の `GetOrder()` という名前の列なのかは、ストアド プロシージャが実行されるまで不明です。<br /><br /> 1 = ユーザー定義関数の参照なのか、列のユーザー定義型 (UDT) のメソッドなのかがあいまいです。<br /><br /> 0 = 参照は明確です。つまり、関数を呼び出したときに、エンティティを正しくバインドできます。<br /><br /> スキーマ バインド参照の場合は常に 0 になります。|  
|is_selected|**bit**|1 = オブジェクトまたは列が選択されています。|  
|is_updated|**bit**|1 = オブジェクトまたは列が変更されています。|  
|is_select_all|**bit**|1 = オブジェクトは SELECT * 句で使用されています (オブジェクトレベルのみ)。|  
|is_all_columns_found|**bit**|1 = オブジェクトに対するすべての列の依存関係が見つかりました。<br /><br /> 0 = オブジェクトに対する列の依存関係が見つかりませんでした。|
|is_insert_all|**bit**|1 = INSERT ステートメントに列の一覧 (オブジェクト レベルのみ) で、オブジェクトが使用されます。<br /><br />この列は、SQL Server 2016 で追加されました。|  
|is_incomplete|**bit**|1 = オブジェクトまたは列バインド エラーが発生し、完全ではありません。<br /><br />この列は、SQL Server 2016 SP2 で追加されました。|
| &nbsp; | &nbsp; | &nbsp; |

## <a name="exceptions"></a>例外  
 次のいずれかの条件に該当した場合は、空の結果セットが返されます。  
  
-   システム オブジェクトが指定されている。  
  
-   指定されたエンティティが現在のデータベースに存在しない。  
  
-   指定されたエンティティがいずれのエンティティも参照しない。  
  
-   無効なパラメーターが渡される。  
  
 指定された参照元エンティティが番号付きストアド プロシージャの場合は、エラーが返されます。  
  
 列の依存関係を解決できない場合は、エラー 2020 が返されます。 このエラーによって、クエリからオブジェクト レベルの依存関係が返されなくなることはありません。  
  
## <a name="remarks"></a>コメント  
 この関数は、サーバー レベルの DDL トリガーを参照するエンティティを取得するために、任意のデータベースのコンテキストで実行できます。  
  
 次の表に、依存関係情報が作成および管理されるエンティティの種類を示します。 ルール、既定値、一時テーブル、一時ストアド プロシージャ、またはシステム オブジェクトについては、依存関係情報は作成も管理もされません。  
  
|エンティティの種類|参照元エンティティ|参照先エンティティ|  
|-----------------|------------------------|-----------------------|  
|テーブル|可*|はい|  
|表示|はい|はい|  
|[!INCLUDE[tsql](../../includes/tsql-md.md)] ストアド プロシージャ**|はい|はい|  
|CLR ストアド プロシージャ (CLR stored procedure)|いいえ|はい|  
|[!INCLUDE[tsql](../../includes/tsql-md.md)] ユーザー定義関数|はい|はい|  
|CLR ユーザー定義関数|いいえ|はい|  
|CLR トリガー (DML および DDL)|いいえ|いいえ|  
|[!INCLUDE[tsql](../../includes/tsql-md.md)] DML トリガー|はい|いいえ|  
|[!INCLUDE[tsql](../../includes/tsql-md.md)] データベース レベルの DDL トリガー|はい|いいえ|  
|[!INCLUDE[tsql](../../includes/tsql-md.md)] サーバー レベルの DDL トリガー|はい|いいえ|  
|拡張ストアド プロシージャ|いいえ|はい|  
|キュー|いいえ|はい|  
|シノニム|いいえ|はい|  
|型 (別名および CLR ユーザー定義型)|いいえ|はい|  
|XML スキーマ コレクション|いいえ|はい|  
|パーティション関数|いいえ|はい|  
| &nbsp; | &nbsp; | &nbsp; |

 \* テーブルは、参照する場合にのみ、参照元エンティティとして追跡を[!INCLUDE[tsql](../../includes/tsql-md.md)]モジュール、ユーザー定義型、または計算列、CHECK 制約、または既定の制約の定義の XML スキーマ コレクションです。  
  
 ** 1 より大きな整数値を持つ番号付きストアド プロシージャは、参照元エンティティとしても、参照先エンティティとしても追跡されません。  
  
## <a name="permissions"></a>アクセス許可  
 sys.dm_sql_referenced_entities に対する SELECT 権限および参照元エンティティに対する VIEW DEFINITION 権限が必要です。 既定では、SELECT 権限が public に与えられます。 参照元エンティティがデータベース レベルの DDL トリガーである場合は、データベースに対する VIEW DEFINITION 権限またはデータベースに対する ALTER DATABASE DDL TRIGGER 権限が必要です。 参照元エンティティがサーバー レベルの DDL トリガーである場合は、サーバーに対する VIEW ANY DEFINITION 権限が必要です。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-return-entities-that-are-referenced-by-a-database-level-ddl-trigger"></a>A. データベース レベルの DDL トリガーによって参照されるエンティティを返す  
 次の例では、データベース レベルの DDL トリガー `ddlDatabaseTriggerLog` によって参照されるエンティティ (テーブルおよび列) を取得します。  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT
        referenced_schema_name,
        referenced_entity_name,
        referenced_minor_name,
        referenced_minor_id,
        referenced_class_desc
    FROM
        sys.dm_sql_referenced_entities (
            'ddlDatabaseTriggerLog',
            'DATABASE_DDL_TRIGGER')
;
GO  
```  
  
### <a name="b-return-entities-that-are-referenced-by-an-object"></a>B. オブジェクトによって参照されるエンティティを返す  
 次の例では、ユーザー定義関数 `dbo.ufnGetContactInformation` によって参照されるエンティティを取得します。  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT
        referenced_schema_name,
        referenced_entity_name,
        referenced_minor_name,
        referenced_minor_id,
        referenced_class_desc,
        is_caller_dependent,
        is_ambiguous
    FROM
        sys.dm_sql_referenced_entities (
            'dbo.ufnGetContactInformation',
            'OBJECT')
;
GO  
```  
  
### <a name="c-return-column-dependencies"></a>C. 戻り値の列の依存関係  
 次の例では、`Table1` 列と `c` 列の合計として定義された計算列 `a` を持つテーブル `b` を作成します。 その後、`sys.dm_sql_referenced_entities` ビューが呼び出されます。 このビューは、2 つの行 (計算列で定義された各列につき 1 行) を返します。  
  
```sql  
CREATE TABLE dbo.Table1 (a int, b int, c AS a + b);  
GO  
SELECT
        referenced_schema_name AS schema_name,  
        referenced_entity_name AS table_name,  
        referenced_minor_name  AS referenced_column,  
        COALESCE(
            COL_NAME(OBJECT_ID(N'dbo.Table1'),
            referencing_minor_id),
            'N/A') AS referencing_column_name  
    FROM
        sys.dm_sql_referenced_entities ('dbo.Table1', 'OBJECT')
;
GO

-- Remove the table.  
DROP TABLE dbo.Table1;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```console
 schema_name table_name referenced_column referencing_column  
 ----------- ---------- ----------------- ------------------  
 dbo         Table1     a                 c  
 dbo         Table1     b                 c  
```

### <a name="d-returning-non-schema-bound-column-dependencies"></a>D. 非スキーマ バインド列の依存関係を取得する  
 次の例では、`Table1` を削除し、`Table2` およびストアド プロシージャ `Proc1` を作成します。 このプロシージャは、`Table2` および存在しないテーブル `Table1` を参照します。 ビュー `sys.dm_sql_referenced_entities` は、参照元エンティティとして指定されたストアド プロシージャで実行されます。 結果セットには、`Table1` に対する 1 行と `Table2` に対する 3 行があります。 `Table1` は存在しないので、列の依存関係が解決されず、エラー 2020 が返されます。 `is_all_columns_found` 列の `Table1` に対する 0 は、検出できなかった列があることを示します。  
  
```sql  
DROP TABLE IF EXISTS dbo.Table1;
GO  
CREATE TABLE dbo.Table2 (c1 int, c2 int);  
GO  
CREATE PROCEDURE dbo.Proc1 AS  
    SELECT a, b, c FROM Table1;  
    SELECT c1, c2 FROM Table2;  
GO  
SELECT
        referenced_id,
        referenced_entity_name AS table_name,
        referenced_minor_name  AS referenced_column_name,
        is_all_columns_found
    FROM
        sys.dm_sql_referenced_entities ('dbo.Proc1', 'OBJECT');
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```console
 referenced_id table_name   referenced_column_name  is_all_columns_found  
 ------------- ------------ ----------------------- --------------------  
 935674381     Table2       NULL                    1  
 935674381     Table2       C1                      1  
 935674381     Table2       C2                      1  
 NULL          Table1       NULL                    0  

Msg 2020, Level 16, State 1, Line 1
The dependencies reported for entity "dbo.Proc1" might not include
  references to all columns. This is either because the entity
  references an object that does not exist or because of an error
  in one or more statements in the entity.  Before rerunning the
  query, ensure that there are no errors in the entity and that
  all objects referenced by the entity exist.
 ```
  
### <a name="e-demonstrating-dynamic-dependency-maintenance"></a>E. 依存関係の動的管理を行う  

この例 E では、例 D が実行されたことを前提としています。 例 E では、依存関係が動的に保持されることを示します。 この例では、次のこと。

1. 再作成`Table1`例 D で削除しました。
2. 実行し、`sys.dm_sql_referenced_entities`参照元エンティティとして指定されたストアド プロシージャでもう一度実行します。

結果セット、テーブル、およびストアド プロシージャで定義されている、それぞれの列の両方が返されることがわかります。 さらに、`is_all_columns_found` 列ではすべてのオブジェクトと列に 1 が返されます。

```sql  
CREATE TABLE Table1 (a int, b int, c AS a + b);  
GO   
SELECT
        referenced_id,
        referenced_entity_name AS table_name,
        referenced_minor_name  AS column_name,
        is_all_columns_found
    FROM
        sys.dm_sql_referenced_entities ('dbo.Proc1', 'OBJECT');
GO  
DROP TABLE Table1, Table2;  
DROP PROC Proc1;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```console
 referenced_id table_name   referenced_column_name  is_all_columns_found  
 ------------- ------------ ----------------------- --------------------  
 935674381     Table2       NULL                    1 
 935674381     Table2       c1                      1 
 935674381     Table2       c2                      1 
 967674495     Table1       NULL                    1 
 967674495     Table1       a                       1  
 967674495     Table1       b                       1  
 967674495     Table1       c                       1  
 ```
 
### <a name="f-returning-object-or-column-usage"></a>F. オブジェクトまたは列の使用状況を返す  
 次の例では、ストアド プロシージャ `HumanResources.uspUpdateEmployeePersonalInfo` のオブジェクトと列の依存関係を返します。 この手順は、列を更新`NationalIDNumber`、 `BirthDate,``MaritalStatus`、および`Gender`の`Employee`テーブルに基づいて、指定した`BusinessEntityID`値です。 別のストアド プロシージャ、`upsLogError`で定義しています.CATCH ブロックを実行エラーをキャプチャします。 `is_selected`、`is_updated`、および `is_select_all` 列では、参照元オブジェクト内でのこれらのオブジェクトと列の使用方法についての情報が返されます。 変更されているテーブルと列は、is_updated 列で 1 と示されます。 `BusinessEntityID` 列は選択されているのみで、ストアド プロシージャ `uspLogError` は選択も変更もされていません。  

```sql  
USE AdventureWorks2012;
GO
SELECT
        referenced_entity_name AS table_name,
        referenced_minor_name  AS column_name,
        is_selected,  is_updated,  is_select_all
    FROM
        sys.dm_sql_referenced_entities(
            'HumanResources.uspUpdateEmployeePersonalInfo',
            'OBJECT')
;
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```console
 table_name    column_name         is_selected is_updated is_select_all  
 ------------- ------------------- ----------- ---------- -------------  
 uspLogError   NULL                0           0          0  
 Employee      NULL                0           1          0  
 Employee      BusinessEntityID    1           0          0  
 Employee      NationalIDNumber    0           1          0  
 Employee      BirthDate           0           1          0  
 Employee      MaritalStatus       0           1          0  
 Employee      Gender              0           1          0
 ```
  
## <a name="see-also"></a>関連項目  
 [sys.dm_sql_referencing_entities &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referencing-entities-transact-sql.md)   
 [sys.sql_expression_dependencies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)  
  
  
