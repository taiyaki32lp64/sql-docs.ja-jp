---
title: sql 式の依存関係 (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sql_expression_dependencies
- sql_expression_dependencies_TSQL
- sql_expression_dependencies
- sys.sql_expression_dependencies_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sql_expression_dependencies catalog view
ms.assetid: 78a218e4-bf99-4a6a-acbf-ff82425a5946
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ade6ffc213d570fcb7da965cf73f43e2db335d17
ms.sourcegitcommit: 3d189b68c0965909d167de61546b574af1ef7a96
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/16/2019
ms.locfileid: "69561127"
---
# <a name="syssql_expression_dependencies-transact-sql"></a>sys.sql_expression_dependencies (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  ユーザー定義エンティティに対する名前による依存関係ごとに 1 つの行を現在のデータベースに格納します。 これには、ネイティブコンパイル、スカラーユーザー定義関数、およびその[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]他のモジュール間の依存関係が含まれます。 2つのエンティティ間の依存関係は、*参照先*エンティティと呼ばれる1つのエンティティが、別のエンティティの永続化された SQL 式 (参照*元エンティティ*と呼ばれます) で名前によって表示される場合に作成されます。 たとえば、ビューの定義内でテーブルが参照されている場合、参照元エンティティであるビューは、参照先エンティティであるテーブルに依存します。 テーブルが削除された場合、ビューは使用できなくなります。  
  
 詳しくは、「[インメモリ OLTP でのユーザー定義のスカラー関数](../../relational-databases/in-memory-oltp/scalar-user-defined-functions-for-in-memory-oltp.md)」をご覧ください。  
  
 このカタログ ビューを使用すると、次のエンティティについて依存関係情報をレポートできます。  
  
-   スキーマ バインド エンティティ。  
  
-   非スキーマ バインド エンティティ。  
  
-   複数のデータベースやサーバーにまたがるエンティティ。 エンティティ名はレポートされますが、エンティティ ID は解決されません。  
  
-   スキーマ バインド エンティティの列レベルの依存関係。 スキーマバインドされていないオブジェクトの列レベルの依存関係を返すには、その[エンティティ](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql.md)を使用します。  
  
-   サーバーレベルの DDL トリガー (master データベースのコンテキスト内)。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|referencing_id|**int**|参照元エンティティの ID。 NULL 値は許可されません。|  
|referencing_minor_id|**int**|参照元エンティティが列の場合は列 ID。それ以外の場合は 0。 NULL 値は許可されません。|  
|referencing_class|**tinyint**|参照元エンティティのクラス。<br /><br /> 1 = オブジェクトまたは列<br /><br /> 12 = データベース DDL トリガー<br /><br /> 13 = サーバー DDL トリガー<br /><br /> NULL 値は許可されません。|  
|referencing_class_desc|**nvarchar(60)**|参照元エンティティのクラスの説明。<br /><br /> OBJECT_OR_COLUMN<br /><br /> DATABASE_DDL_TRIGGER<br /><br /> SERVER_DDL_TRIGGER<br /><br /> NULL 値は許可されません。|  
|is_schema_bound_reference|**bit**|1 = 参照先エンティティはスキーマ バインドです。<br /><br /> 0 = 参照先エンティティは非スキーマ バインドです。<br /><br /> NULL 値は許可されません。|  
|referenced_class|**tinyint**|参照先エンティティのクラス。<br /><br /> 1 = オブジェクトまたは列<br /><br /> 6 = 型<br /><br /> 10 = XML スキーマ コレクション<br /><br /> 21 = パーティション関数<br /><br /> NULL 値は許可されません。|  
|referenced_class_desc|**nvarchar(60)**|参照先エンティティのクラスの説明。<br /><br /> OBJECT_OR_COLUMN<br /><br /> TYPE<br /><br /> XML_SCHEMA_COLLECTION<br /><br /> PARTITION_FUNCTION<br /><br /> NULL 値は許可されません。|  
|referenced_server_name|**sysname**|参照先エンティティのサーバー名。<br /><br /> 有効な 4 部構成の名前を指定することによって作成されたサーバー間依存関係については、この列に値が格納されます。 マルチパート名の詳細については、「transact-sql[構文表記&#40;規則&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)」を参照してください。<br /><br /> 4 部構成の名前を指定せずにエンティティが参照される非スキーマ バインド エンティティの場合は NULL。<br /><br /> スキーマバインドエンティティの場合は NULL。同じデータベース内に存在する必要があるため、2つの部分 (*schema. object*) 名を使用してのみ定義できます。|  
|referenced_database_name|**sysname**|参照先エンティティのデータベース名。<br /><br /> 有効な 3 部構成または 4 部構成の名前を指定することによって作成された複数データベースまたは複数サーバーにまたがる参照については、この列に値が格納されます。<br /><br /> 1 部構成または 2 部構成の名前を使って指定された非スキーマ バインド参照の場合は NULL。<br /><br /> スキーマバインドエンティティの場合は NULL。同じデータベース内に存在する必要があるため、2つの部分 (*schema. object*) 名を使用してのみ定義できます。|  
|referenced_schema_name|**sysname**|参照先エンティティが属しているスキーマ。<br /><br /> スキーマ名を指定せずにエンティティが参照される非スキーマ バインド参照の場合は NULL。<br /><br /> スキーマ バインド エンティティは 2 つの部分で構成される名前を使用して定義および参照する必要があるので、スキーマ バインド参照の場合、NULL にすることはできません。|  
|referenced_entity_name|**sysname**|参照先エンティティの名前。 NULL 値は許可されません。|  
|referenced_id|**int**|参照先エンティティの ID。 スキーマバインド参照の場合、この列の値は NULL になりません。 サーバー間およびデータベース間の参照の場合、この列の値は常に NULL になります。<br /><br /> データベース内の参照で ID を判別できない場合は、NULL。 非スキーマ バインド参照では、次の場合に ID を解決できません。<br /><br /> 参照先エンティティがデータベースに存在しない。<br /><br /> 参照先エンティティのスキーマが呼び出し元に依存し、実行時に解決される。 この場合、is_caller_dependent は 1 に設定されます。|  
|referenced_minor_id|**int**|参照元エンティティが列の場合は参照される列の ID。それ以外の場合は 0。 NULL 値は許可されません。<br /><br /> 参照元エンティティの中で列が名前で指定されていた場合、または SELECT * ステートメントの中で親エンティティが使用されていた場合、参照先エンティティは列になります。|  
|is_caller_dependent|**bit**|参照先エンティティのスキーマ バインドが実行時に行われるため、エンティティ ID の解決が呼び出し元のスキーマに依存することを示します。 これが該当するのは、参照先エンティティがストアド プロシージャ、拡張ストアド プロシージャ、または、EXECUTE ステートメント内で呼び出される非スキーマ バインド ユーザー定義関数である場合です。<br /><br /> 1 = 参照先エンティティは呼び出し元に依存し、実行時に解決されます。 この場合、referenced_id は NULL です。<br /><br /> 0 = 参照先エンティティの ID は呼び出し元に依存しません。<br /><br /> スキーマ バインド参照のほか、スキーマ名を明示的に指定するデータベース間参照やサーバー間参照の場合は常に 0 になります。 たとえば、`EXEC MyDatabase.MySchema.MyProc` 形式のエンティティ参照は呼び出し元に依存しません。 ただし、`EXEC MyDatabase..MyProc` 形式の参照は呼び出し元に依存します。|  
|is_ambiguous|**bit**|参照があいまいであり、実行時にユーザー定義関数、ユーザー定義型 (UDT)、または**xml**型の列への xquery 参照に解決できることを示します。<br /><br /> たとえば、ストアドプロシージャでステートメント`SELECT Sales.GetOrder() FROM Sales.MySales`が定義されているとします。 `Sales.GetOrder()` が `Sales` スキーマ内のユーザー定義関数なのか、`Sales` という名前のメソッドを持つ UDT 型の `GetOrder()` という名前の列なのかは、ストアド プロシージャが実行されるまで不明です。<br /><br /> 1 = 参照はあいまいです。<br /><br /> 0 = 参照は明確です。つまり、ビューを呼び出したときに、エンティティを正しくバインドできます。<br /><br /> スキーマバインド参照の場合は常に0です。|  
  
## <a name="remarks"></a>コメント  
 次の表に、依存関係情報が作成および管理されるエンティティの種類を示します。 ルール、既定値、一時テーブル、一時ストアド プロシージャ、またはシステム オブジェクトについては、依存関係情報は作成も管理もされません。  

> [!NOTE]
> Azure SQL Data Warehouse および並列データウェアハウスでは、この一覧からテーブル、ビュー、フィルター選択された統計情報、および Transact-sql ストアドプロシージャのエンティティ型をサポートしています。  依存関係情報は、テーブル、ビュー、およびフィルター選択された統計情報に対してのみ作成および管理されます。  
  
|エンティティの種類|参照元エンティティ|参照先エンティティ|  
|-----------------|------------------------|-----------------------|  
|テーブル|可*|はい|  
|表示|はい|はい|  
|フィルター選択されたインデックス|可**|いいえ|  
|フィルター選択された統計情報|可**|いいえ|  
|[!INCLUDE[tsql](../../includes/tsql-md.md)] ストアド プロシージャ***|はい|はい|  
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
  
 \*テーブルは、計算列、check 制約、または DEFAULT 制約[!INCLUDE[tsql](../../includes/tsql-md.md)]の定義でモジュール、ユーザー定義型、または XML スキーマコレクションを参照している場合にのみ、参照元エンティティとして追跡されます。  
  
 ** フィルター述語で使用する各列は、参照元エンティティとして追跡されます。  
  
 *** 1 より大きな整数値を持つ番号付きストアド プロシージャは、参照元エンティティとしても、参照先エンティティとしても追跡されません。  
  
## <a name="permissions"></a>アクセス許可  
 データベースに対する VIEW DEFINITION 権限およびデータベースの sys.sql_expression_dependencies に対する SELECT 権限が必要です。 既定では、SELECT 権限は db_owner 固定データベース ロールのメンバーだけに与えられます。 SELECT 権限と VIEW DEFINITION 権限が別のユーザーに与えられている場合、権限が許可されているユーザーはデータベース内のすべての依存関係を表示できます。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-returning-entities-that-are-referenced-by-another-entity"></a>A. 別のエンティティによって参照されるエンティティを取得する  
 次の例では、ビュー `Production.vProductAndDescription` 内で参照されているテーブルおよび列を取得します。 ビューは、列`referenced_entity_name`および`referenced_column_name`列に返されるエンティティ (テーブルおよび列) によって異なります。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT OBJECT_NAME(referencing_id) AS referencing_entity_name,   
    o.type_desc AS referencing_desciption,   
    COALESCE(COL_NAME(referencing_id, referencing_minor_id), '(n/a)') AS referencing_minor_id,   
    referencing_class_desc,  
    referenced_server_name, referenced_database_name, referenced_schema_name,  
    referenced_entity_name,   
    COALESCE(COL_NAME(referenced_id, referenced_minor_id), '(n/a)') AS referenced_column_name,  
    is_caller_dependent, is_ambiguous  
FROM sys.sql_expression_dependencies AS sed  
INNER JOIN sys.objects AS o ON sed.referencing_id = o.object_id  
WHERE referencing_id = OBJECT_ID(N'Production.vProductAndDescription');  
GO  
  
```  
  
### <a name="b-returning-entities-that-reference-another-entity"></a>B. 別のエンティティを参照するエンティティを取得する  
 次の例では、テーブル `Production.Product` を参照するエンティティを取得します。 `referencing_entity_name` 列に返されるエンティティは、`Product` テーブルに依存します。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT OBJECT_SCHEMA_NAME ( referencing_id ) AS referencing_schema_name,  
    OBJECT_NAME(referencing_id) AS referencing_entity_name,   
    o.type_desc AS referencing_desciption,   
    COALESCE(COL_NAME(referencing_id, referencing_minor_id), '(n/a)') AS referencing_minor_id,   
    referencing_class_desc, referenced_class_desc,  
    referenced_server_name, referenced_database_name, referenced_schema_name,  
    referenced_entity_name,   
    COALESCE(COL_NAME(referenced_id, referenced_minor_id), '(n/a)') AS referenced_column_name,  
    is_caller_dependent, is_ambiguous  
FROM sys.sql_expression_dependencies AS sed  
INNER JOIN sys.objects AS o ON sed.referencing_id = o.object_id  
WHERE referenced_id = OBJECT_ID(N'Production.Product');  
GO  
  
```  
  
### <a name="c-returning-cross-database-dependencies"></a>C. データベース間の依存関係を取得する  
 次の例では、データベース間の依存関係をすべて取得します。 この例では、まず`db1`データベースを作成し、データベース`db2`と`db3`のテーブルを参照する2つのストアドプロシージャを作成します。 次に、`sys.sql_expression_dependencies` テーブルに対してクエリを実行して、プロシージャとテーブルの間のデータベース間依存関係をレポートします。 参照先エンティティ `referenced_schema_name` の `t3` 列に NULL が返されることに注意してください。これは、プロシージャの定義の中でそのエンティティにスキーマ名が指定されていないためです。  
  
```  
CREATE DATABASE db1;  
GO  
USE db1;  
GO  
CREATE PROCEDURE p1 AS SELECT * FROM db2.s1.t1;  
GO  
CREATE PROCEDURE p2 AS  
    UPDATE db3..t3  
    SET c1 = c1 + 1;  
GO  
SELECT OBJECT_NAME (referencing_id),referenced_database_name,   
    referenced_schema_name, referenced_entity_name  
FROM sys.sql_expression_dependencies  
WHERE referenced_database_name IS NOT NULL;  
GO  
USE master;  
GO  
DROP DATABASE db1;  
GO  
  
```  
  
## <a name="see-also"></a>参照  
 [sys.dm_sql_referenced_entities &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql.md)   
 [sys.dm_sql_referencing_entities &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referencing-entities-transact-sql.md)  
  
  
