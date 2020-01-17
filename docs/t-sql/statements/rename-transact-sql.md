---
title: RENAME (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/21/2019
ms.service: sql-data-warehouse
ms.reviewer: ''
ms.topic: language-reference
ms.assetid: 0907cfd9-33a6-4fa6-91da-7d6679fee878
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 624131beece632cffd13bde3d6ad378f67b3a340
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68141268"
---
# <a name="rename-transact-sql"></a>RENAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

[!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 内のユーザーが作成したテーブルの名前を変更します。 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 内のユーザーが作成したテーブルまたはデータベースの名前を変更します。

> [!NOTE]
> [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] でデータベースの名前を変更するには、[ALTER DATABASE (Azure SQL Data Warehouse)](alter-database-transact-sql.md?view=aps-pdw-2016-au7) を使用します。 Azure SQL Database でデータベースの名前を変更するには、[ALTER DATABASE (Azure SQL Database)](alter-database-transact-sql.md?view=azuresqldb-mi-current) ステートメントを使用します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内のデータベースの名前を変更するには、ストアド プロシージャ [sp_renamedb](../../relational-databases/system-stored-procedures/sp-renamedb-transact-sql.md) を使用します。

## <a name="syntax"></a>構文

```
-- Syntax for Azure SQL Data Warehouse

-- Rename a table.
RENAME OBJECT [::] [ [ database_name . [schema_name ] ] . ] | [schema_name . ] ] table_name TO new_table_name
[;]

```

```
-- Syntax for Analytics Platform System

-- Rename a table
RENAME OBJECT [::] [ [ database_name . [ schema_name ] . ] | [ schema_name . ] ] table_name TO new_table_name
[;]

-- Rename a database
RENAME DATABASE [::] database_name TO new_database_name
[;]
```

## <a name="arguments"></a>引数

RENAME OBJECT [::] [ [*database_name* . [ *schema_name* ] . ] | [ *schema_name* . ] ]*table_name* TO *new_table_name*
**APPLIES TO:** [!INCLUDE[ssSDW](../../includes/sssdw-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]

ユーザー定義テーブルの名前を変更します。 1、2、または 3 部構成の名前で名前を変更するテーブルを指定します。 新しいテーブル *new_table_name* を 1 部構成の名前として指定します。

RENAME DATABASE [::] [ *database_name* TO *new_database_name*
**APPLIES TO:** [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]

ユーザー定義のデータベースの名前を *database_name* から *new_database_name* に変更します。 これらの [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] で予約されたいずれかのデータベース名に名前を変更することはできません。

- master
- model
- msdb
- tempdb
- pdwtempdb1
- pdwtempdb2
- DWConfiguration
- DWDiagnostics
- DWQueue

## <a name="permissions"></a>アクセス許可

このコマンドを実行するには、次のアクセス許可が必要です。

- テーブルに対する **ALTER** 権限。

## <a name="limitations-and-restrictions"></a>制限事項と制約事項

### <a name="cannot-rename-an-external-table-indexes-or-views"></a>外部テーブル、インデックス、またはビューの名前は変更できない

外部テーブル、インデックス、またはビューの名前は変更できません。 この名前を変更する代わりに、外部テーブル、インデックス、またはビューを削除し、新しい名前を指定して再作成することができます。

### <a name="cannot-rename-a-table-in-use"></a>使用中のテーブルの名前は変更できない

使用中に、テーブルまたはデータベースの名前を変更することはできません。 テーブルの名前を変更するには、テーブルに排他ロックが必要です。 テーブルを使用している場合は、テーブルを使用しているセッションを終了する必要があります。 セッションを終了するには、KILL コマンドを使用することができます。 セッションが終了すると、コミットされていない作業はロールバックされるので、KILL は注意して使用してください。 SQL Data Warehouse 内のセッションには、'SID' が付きます。 KILL コマンドを呼び出すときは、'SID' とセッション番号を含めます。 この例では、アクティブまたはアイドル状態のセッションの一覧を表示し、'SID1234' のセッションを終了します。

### <a name="views-are-not-updated"></a>ビューは更新されません。

データベースの名前を変更すると、以前のデータベース名を使用するすべてのビューは無効になります。 この動作は、データベースの内部と外部の両方のビューに適用されます。 たとえば、Sales データベースの名前を変更する場合、`SELECT * FROM Sales.dbo.table1` を含むビューが無効になります。 この問題を解決するには、ビューでは、3 部構成の名前は使用しないようにするか、新しいデータベース名を参照するようにビューを更新します。

テーブルの名前を変更したときに、新しいテーブルの名前を参照するようにビューは更新されません。 元のテーブル名を参照するとデータベース内部と外部の各ビューは無効になります。 この問題を解決するために、新しいテーブルの名前を参照するように各ビューを更新することができます。

## <a name="locking"></a>ロック

テーブルの名前を変更するときは、DATABASE オブジェクトの共有ロック、SCHEMA オブジェクトの共有ロック、およびテーブルに対する排他ロックを取得します。

## <a name="examples"></a>使用例

### <a name="a-rename-a-database"></a>A. データベースの名前変更

**適用対象:** [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] のみ

この例では、ユーザー定義のデータベースの名前 AdWorks を AdWorks2 に変更します。

```sql
-- Rename the user defined database AdWorks
RENAME DATABASE AdWorks to AdWorks2;

```

 テーブルの名前を変更すると、テーブルに関連付けられているすべてのオブジェクトとプロパティが、新しいテーブル名を参照するように更新されます。 たとえば、テーブルの定義、インデックス、制約、およびアクセス許可が更新されます。 ビューは更新されません。

### <a name="b-rename-a-table"></a>B. テーブル名の変更

**適用対象:** [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]、[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]

この例では、Customer テーブルの名前を Customer1 に変更します。

```sql
-- Rename the customer table
RENAME OBJECT Customer TO Customer1;

RENAME OBJECT mydb.dbo.Customer TO Customer1;
```

テーブルの名前を変更すると、テーブルに関連付けられているすべてのオブジェクトとプロパティが、新しいテーブル名を参照するように更新されます。 たとえば、テーブルの定義、インデックス、制約、およびアクセス許可が更新されます。 ビューは更新されません。

### <a name="c-move-a-table-to-a-different-schema"></a>C. 別のスキーマにテーブルを移動する

**適用対象:** [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]、[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]

オブジェクトを別のスキーマに移動する場合、[ALTER SCHEMA](../../t-sql/statements/alter-schema-transact-sql.md) を使用します。 たとえば、次のステートメントは、テーブルの項目を product スキーマから dbo スキーマに移動します。

```sql
ALTER SCHEMA dbo TRANSFER OBJECT::product.item;
```

### <a name="d-terminate-sessions-before-renaming-a-table"></a>D. テーブルの名前を変更する前にセッションを終了する

**適用対象:** [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]、[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]

使用中にはテーブル名を変更できないことに注意してください。 テーブル名を変更するには、テーブルに排他ロックが必要です テーブルを使用している場合は、テーブルを使用しているセッションを終了する必要があります。 セッションを終了するには、KILL コマンドを使用することができます。 セッションが終了すると、コミットされていない作業はロールバックされるので、KILL は注意して使用してください。 SQL Data Warehouse 内のセッションには、'SID' が付きます。 KILL コマンドを呼び出すときに、'SID' とセッション番号を含める必要があります。 この例では、アクティブまたはアイドル状態のセッションの一覧を表示し、'SID1234' のセッションを終了します。

```sql
-- View a list of the current sessions
SELECT session_id, login_name, status
FROM sys.dm_pdw_exec_sessions
WHERE status='Active' OR status='Idle';

-- Terminate a session using the session_id.
KILL 'SID1234';
```