---
title: DBCC CLEANTABLE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CLEANTABLE_TSQL
- DBCC_CLEANTABLE_TSQL
- DBCC CLEANTABLE
- CLEANTABLE
dev_langs:
- TSQL
helpviewer_keywords:
- disk space [SQL Server], reclaiming
- reclaiming space
- reallocating space
- removing columns
- DBCC CLEANTABLE statement
- space [SQL Server], reclaiming
- deleting columns
- dropping columns
ms.assetid: 0dbbc956-15b1-427b-812c-618a044d07fa
author: pmasl
ms.author: umajay
ms.openlocfilehash: 8cb3c1c0eba5c39083b6a6b39b4040639909808c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68101976"
---
# <a name="dbcc-cleantable-transact-sql"></a>DBCC CLEANTABLE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]
テーブルまたはインデックス付きビュー内で削除された可変長列の領域の返還を要求します。
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>構文  
  
```sql
  
DBCC CLEANTABLE  
(  
    { database_name | database_id | 0 }  
    , { table_name | table_id | view_name | view_id }  
    [ , batch_size ]  
)  
[ WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>引数  
 *database_name* | *database_id* | 0  
 クリーンにするテーブルが含まれるデータベースを指定します。 0 を指定すると、現在のデータベースが選択されます。 データベース名は、[識別子](../../relational-databases/databases/database-identifiers.md)のルールに従っている必要があります。  
  
 *table_name* | *table_id* | *view_name*| *view_id*  
 クリーンにするテーブルまたはインデックス付きビューを指定します。  
  
 *batch_size*  
 1 つのトランザクションで処理する行の数を指定します。 値を指定しない場合や 0 を指定した場合は、テーブル全体が 1 つのトランザクションで処理されます。  
  
 WITH NO_INFOMSGS  
 すべての情報メッセージを表示しないようにします。  
  
## <a name="remarks"></a>Remarks  
DBCC CLEANTABLE は、可変長列の削除後に残る領域の返還を要求します。 可変長列には、**varchar**、**nvarchar**、**varchar(max)** 、**nvarchar(max)** 、**varbinary**、**varbinary(max)** 、**text**、**ntext**、**image**、**sql_variant**、**xml** のいずれかのデータ型を使用できます。 固定長列の削除後に残る領域の返還は要求しません。
削除された列が行内にあった場合、DBCC CLEANTABLE は、テーブルの IN_ROW_DATA アロケーション ユニットからの領域の返還を要求します。 削除された列が行外にあった場合、その列のデータ型に応じて、ROW_OVERFLOW_DATA または LOB_DATA アロケーション ユニットからの領域の返還を要求します。 ROW_OVERFLOW_DATA または LOB_DATA ページから領域が返還され空のページとなった場合、ページは削除されます。
DBCC CLEANTABLE は 1 つ以上のトランザクションとして実行されます。 バッチ サイズを指定しない場合は、テーブル全体が 1 つのトランザクションで処理され、その間テーブルが排他ロックされます。 テーブルの規模が大きくなると、シングル トランザクションが長すぎたり必要なログ領域が大きすぎたりする可能性があります。 バッチ サイズを指定すると、コマンドは指定した数の行の一連のトランザクションで処理されるようになります。 DBCC CLEANTABLE は、他のトランザクション内のトランザクションとして実行することはできません。
この操作はすべてログに記録されます。
DBCC CLEANTABLE は、システム テーブル、一時テーブル、またはテーブルの xVelocity メモリ最適化列ストア インデックスの部分での使用はサポートされていません。
  
## <a name="best-practices"></a>ベスト プラクティス  
DBCC CLEANTABLE は、定期的なメンテナンス タスクとして実行するのではなく、 テーブルまたはインデックス付きビュー内の可変長列を大幅に変更した後、未使用領域をすぐに再利用する必要がある場合に使用してください。 DBCC CLEANTABLE を使用しなくても、テーブルまたはビューのインデックスを再構築できます。ただし、この操作ではリソースが大量に消費されます。
  
## <a name="result-sets"></a>結果セット  
DBCC CLEANTABLE は次の値を返します。
  
```sql
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
## <a name="permissions"></a>アクセス許可  
 呼び出し元はテーブルまたはインデックス付きビューを所有しているか、固定サーバー ロール **sysadmin**、固定データベース ロール **db_owner**、または固定データベース ロール **db_ddladmin** のメンバーである必要があります。  
  
## <a name="examples"></a>使用例  
### <a name="a-using-dbcc-cleantable-to-reclaim-space"></a>A. DBCC CLEANTABLE を使用して領域の返還を要求する  
次の例では、[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] サンプル データベースの `Production.Document` テーブルに対して DBCC CLEANTABLE を実行します。
  
```sql  
DBCC CLEANTABLE (AdventureWorks2012,'Production.Document', 0)  
WITH NO_INFOMSGS;  
GO  
```  
  
### <a name="b-using-dbcc-cleantable-and-verifying-results"></a>B. DBCC CLEANTABLE を使用し、その結果を確認する  
次の例では、複数の可変長列を含むテーブルを作成し設定した後、 2 つの列を削除して DBCC CLEANTABLE を実行し、未使用領域の返還を要求します。 クエリを実行し、DBCC CLEANTABLE コマンドの実行前と実行後のページ数と領域の値を確認してください。
  
```sql  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID ('dbo.CleanTableTest', 'U') IS NOT NULL  
    DROP TABLE dbo.CleanTableTest;  
GO  
CREATE TABLE dbo.CleanTableTest  
    (FileName nvarchar(4000),   
    DocumentSummary nvarchar(max),  
    Document varbinary(max)  
    );  
GO  
-- Populate the table with data from the Production.Document table.  
INSERT INTO dbo.CleanTableTest  
    SELECT REPLICATE(FileName, 1000),   
           DocumentSummary,   
           Document  
    FROM Production.Document;  
GO  
-- Verify the current page counts and average space used in the dbo.CleanTableTest table.  
DECLARE @db_id SMALLINT;  
DECLARE @object_id INT;  
SET @db_id = DB_ID(N'AdventureWorks2012');  
SET @object_id = OBJECT_ID(N'AdventureWorks2012.dbo.CleanTableTest');  
SELECT alloc_unit_type_desc,   
       page_count,   
       avg_page_space_used_in_percent,   
       record_count  
FROM sys.dm_db_index_physical_stats(@db_id, @object_id, NULL, NULL , 'Detailed');  
GO  
-- Drop two variable-length columns from the table.  
ALTER TABLE dbo.CleanTableTest  
DROP COLUMN FileName, Document;  
GO  
-- Verify the page counts and average space used in the dbo.CleanTableTest table  
-- Notice that the values have not changed.  
DECLARE @db_id SMALLINT;  
DECLARE @object_id INT;  
SET @db_id = DB_ID(N'AdventureWorks2012');  
SET @object_id = OBJECT_ID(N'AdventureWorks2012.dbo.CleanTableTest');  
SELECT alloc_unit_type_desc,   
       page_count,   
       avg_page_space_used_in_percent,   
       record_count  
FROM sys.dm_db_index_physical_stats(@db_id, @object_id, NULL, NULL , 'Detailed');  
GO  
-- Run DBCC CLEANTABLE.  
DBCC CLEANTABLE (AdventureWorks2012,'dbo.CleanTableTest');  
GO  
-- Verify the values in the dbo.CleanTableTest table after the DBCC CLEANTABLE command.  
DECLARE @db_id SMALLINT;  
DECLARE @object_id INT;  
SET @db_id = DB_ID(N'AdventureWorks2012');  
SET @object_id = OBJECT_ID(N'AdventureWorks2012.dbo.CleanTableTest');  
SELECT alloc_unit_type_desc,   
       page_count,   
       avg_page_space_used_in_percent,   
       record_count  
FROM sys.dm_db_index_physical_stats(@db_id, @object_id, NULL, NULL , 'Detailed');  
GO  
```  
  
## <a name="see-also"></a>参照  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
 [sys.allocation_units &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-allocation-units-transact-sql.md)  
  
  
