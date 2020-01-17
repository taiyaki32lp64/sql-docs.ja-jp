---
title: dm_sql_referencing_entities (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_sql_referencing_entities
- dm_sql_referencing_entities_TSQL
- sys.dm_sql_referencing_entities_TSQL
- dm_sql_referencing_entities
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_sql_referencing_entities dynamic management function
ms.assetid: c16f8f0a-483f-4feb-842e-da90426045ae
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: bd09706d1b3de9ebe4a5b333f79be9644c433e7c
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "73982339"
---
# <a name="sysdm_sql_referencing_entities-transact-sql"></a>dm_sql_referencing_entities (Transact-sql)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  別のユーザー定義エンティティを名前で参照する、現在のデータベース内のエンティティごとに1行のデータを返します。 2つのエンティティ間の依存関係は、*参照先*エンティティと呼ばれる1つのエンティティが、別のエンティティの永続化された SQL 式 (参照*元エンティティ*と呼ばれます) で名前によって表示される場合に作成されます。 たとえば、参照先エンティティとしてユーザー定義型 (UDT) が指定されている場合、この関数は、定義内でその型を名前で参照する各ユーザー定義エンティティを返します。 関数は、指定されたエンティティを参照する可能性がある他のデータベース内のエンティティを返しません。 この関数は、サーバーレベルの DDL トリガーを参照元エンティティとして返すために、master データベースのコンテキストで実行する必要があります。  
  
 この動的管理関数に参照先エンティティを指定すると、現在のデータベース内で、そのエンティティを参照する次の種類のエンティティをレポートできます。  
  
-   スキーマ バインドまたは非スキーマ バインド エンティティ  
  
-   データベースレベルの DDL トリガー  
  
-   サーバーレベルの DDL トリガー  
  
**適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降)、[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
sys.dm_sql_referencing_entities (  
    ' schema_name.referenced_entity_name ' , ' <referenced_class> ' )  
  
<referenced_class> ::=  
{  
    OBJECT  
  | TYPE  
  | XML_SCHEMA_COLLECTION  
  | PARTITION_FUNCTION  
}  
```  
  
## <a name="arguments"></a>引数  
 *schema_name.referenced*_*entity_name*  
 参照先エンティティの名前を指定します。  
  
 参照されるクラスが PARTITION_FUNCTION 場合を除き、 *schema_name*が必要です。  
  
 *schema_name。 referenced_entity_name*は**nvarchar (517)** です。  
  
 *< referenced_class >* :: = {OBJECT |TYPE |XML_SCHEMA_COLLECTION |PARTITION_FUNCTION}  
 は、参照先エンティティのクラスです。 クラスは 1 つのステートメントに 1 つだけ指定できます。  
  
 *< referenced_class >* は**nvarchar**(60) です。  
  
## <a name="table-returned"></a>返されるテーブル  
  
|列名|データ型|[説明]|  
|-----------------|---------------|-----------------|  
|referencing_schema_name|**sysname**|参照元エンティティが属しているスキーマ。 NULL 値が許可されます。<br /><br /> データベースレベルおよびサーバーレベルの DDL トリガーの場合は NULL です。|  
|referencing_entity_name|**sysname**|参照元エンティティの名前。 NULL 値は許可されません。|  
|referencing_id|**int**|参照元エンティティの ID。 NULL 値は許可されません。|  
|referencing_class|**tinyint**|参照元エンティティのクラス。 NULL 値は許可されません。<br /><br /> 1 = オブジェクト<br /><br /> 12 = データベース レベル DDL トリガー<br /><br /> 13 = サーバーレベルの DDL トリガー|  
|referencing_class_desc|**nvarchar(60)**|参照元エンティティのクラスの説明。<br /><br /> OBJECT<br /><br /> DATABASE_DDL_TRIGGER<br /><br /> SERVER_DDL_TRIGGER|  
|is_caller_dependent|**bit**|参照先エンティティが呼び出し元のスキーマに依存するため、参照先エンティティ ID の解決は実行時に行われることを示します。<br /><br /> 1 = 参照元エンティティは、エンティティを参照する可能性があります。ただし、参照先エンティティ ID の解決は呼び出し元に依存しているため、特定できません。 これは、ストアドプロシージャ、拡張ストアドプロシージャ、または EXECUTE ステートメントで呼び出されたユーザー定義関数への非スキーマバインド参照に対してのみ発生します。<br /><br /> この値が 0 の場合、参照先エンティティは呼び出し元に依存しません。|  
  
## <a name="exceptions"></a>例外  
 次のいずれかの条件に該当した場合は、空の結果セットが返されます。  
  
-   システム オブジェクトが指定されている。  
  
-   指定されたエンティティが現在のデータベースに存在しない。  
  
-   指定されたエンティティがいずれのエンティティも参照しない。  
  
-   無効なパラメーターが渡される。  
  
 指定された参照先エンティティが番号付きストアドプロシージャの場合、エラーを返します。  
  
## <a name="remarks"></a>Remarks  
 次の表に、依存関係情報が作成および管理されるエンティティの種類を示します。 ルール、既定値、一時テーブル、一時ストアド プロシージャ、またはシステム オブジェクトについては、依存関係情報は作成も管理もされません。  
  
|エンティティの種類|参照元エンティティ|参照先エンティティ|  
|-----------------|------------------------|-----------------------|  
|[ファイル]|可*|はい|  
|[表示]|はい|はい|  
|[!INCLUDE[tsql](../../includes/tsql-md.md)] ストアド プロシージャ**|はい|はい|  
|CLR ストアド プロシージャ (CLR stored procedure)|[いいえ]|はい|  
|[!INCLUDE[tsql](../../includes/tsql-md.md)] ユーザー定義関数|はい|はい|  
|CLR ユーザー定義関数|[いいえ]|はい|  
|CLR トリガー (DML および DDL)|[いいえ]|[いいえ]|  
|[!INCLUDE[tsql](../../includes/tsql-md.md)] DML トリガー|はい|[いいえ]|  
|[!INCLUDE[tsql](../../includes/tsql-md.md)] データベース レベルの DDL トリガー|はい|[いいえ]|  
|[!INCLUDE[tsql](../../includes/tsql-md.md)] サーバー レベルの DDL トリガー|はい|[いいえ]|  
|拡張ストアド プロシージャ|[いいえ]|はい|  
|キュー|[いいえ]|はい|  
|シノニム|[いいえ]|はい|  
|型 (別名および CLR ユーザー定義型)|[いいえ]|はい|  
|XML スキーマ コレクション|[いいえ]|はい|  
|パーティション関数|[いいえ]|はい|  
  
 \* テーブルは、計算列、CHECK 制約、または DEFAULT 制約の定義で [!INCLUDE[tsql](../../includes/tsql-md.md)] モジュール、ユーザー定義型、または XML スキーマコレクションを参照する場合にのみ、参照元エンティティとして追跡されます。  
  
 ** 1 より大きな整数値を持つ番号付きストアド プロシージャは、参照元エンティティとしても、参照先エンティティとしても追跡されません。  
  
## <a name="permissions"></a>アクセス許可  
  
### <a name="includesskatmaiincludessskatmai-mdmd---includesssql11includessssql11-mdmd"></a>[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] - [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
  
-   参照先のオブジェクトに対する CONTROL 権限が必要です。 参照先エンティティがパーティション関数である場合、データベースに対する CONTROL 権限が必要です。  
  
-   Dm_sql_referencing_entities に対する SELECT 権限が必要です。 既定では、SELECT 権限が public に与えられます。  
  
### <a name="includesssql14includessssql14-mdmd---includesscurrentincludessscurrent-mdmd"></a>[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] - [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
  
-   参照先オブジェクトに対する権限は必要ありません。 ユーザーが参照しているエンティティの一部に対してのみ VIEW DEFINITION を持っている場合、結果の一部を返すことができます。  
  
-   参照元エンティティがオブジェクトの場合、オブジェクトに対する VIEW DEFINITION が必要です。  
  
-   参照元エンティティがデータベースレベルの DDL トリガーである場合は、データベースに対する VIEW DEFINITION が必要です。  
  
-   参照元エンティティがサーバーレベルの DDL トリガーである場合は、サーバーの VIEW ANY DEFINITION が必要です。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-returning-the-entities-that-refer-to-a-given-entity"></a>A. 特定のエンティティを参照するエンティティを取得する  
 次の例では、現在のデータベース内で、指定したテーブルを参照するエンティティを取得します。  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT referencing_schema_name, referencing_entity_name, referencing_id, referencing_class_desc, is_caller_dependent  
FROM sys.dm_sql_referencing_entities ('Production.Product', 'OBJECT');  
GO  
```  
  
### <a name="b-returning-the-entities-that-refer-to-a-given-type"></a>b. 指定された型を参照するエンティティを返す  
 次の例では、`dbo.Flag`エイリアスの種類を参照するエンティティを返します。 結果セットは、2つのストアドプロシージャがこの型を使用することを示しています。 `dbo.Flag` 型は、`HumanResources.Employee` テーブル内の複数の列の定義でも使用されます。ただし、この型はテーブル内の計算列、CHECK 制約、または DEFAULT 制約の定義に含まれていないため、`HumanResources.Employee` テーブルに対して行は返されません。  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT referencing_schema_name, referencing_entity_name, referencing_id, referencing_class_desc, is_caller_dependent  
FROM sys.dm_sql_referencing_entities ('dbo.Flag', 'TYPE');  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 referencing_schema_name referencing_entity_name   referencing_id referencing_class_desc is_caller_dependent  
 ----------------------- -------------------------  ------------- ---------------------- -------------------  
 HumanResources          uspUpdateEmployeeHireInfo  1803153469    OBJECT_OR_COLUMN       0  
 HumanResources          uspUpdateEmployeeLogin     1819153526    OBJECT_OR_COLUMN       0  
 (2 row(s) affected)`  
 ``` 
 
## <a name="see-also"></a>参照  
 [sys.dm_sql_referenced_entities &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql.md)   
 [sys.sql_expression_dependencies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)  
  
  
