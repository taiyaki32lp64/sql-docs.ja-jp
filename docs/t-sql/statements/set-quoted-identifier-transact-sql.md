---
title: SET QUOTED_IDENTIFIER (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/21/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- QUOTED_IDENTIFIER_TSQL
- SET_QUOTED_IDENTIFIER_TSQL
- SET QUOTED_IDENTIFIER
- QUOTED_IDENTIFIER
dev_langs:
- TSQL
helpviewer_keywords:
- delimited identifiers [SQL Server]
- identifiers [SQL Server], delimited
- QUOTED_IDENTIFIER option
- quoted identifiers
- ISO delimited identifiers rules
- SET QUOTED_IDENTIFIER statement
ms.assetid: 10f66b71-9241-4a3a-9292-455ae7252565
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b080efcb7af0f813f798c7f572f464d4718fdd75
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68008877"
---
# <a name="set-quotedidentifier-transact-sql"></a>SET QUOTED_IDENTIFIER (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に対して、識別子とリテラル文字列を区切る引用符に関して、ISO 規格に従うことを指定します。 [!INCLUDE[tsql](../../includes/tsql-md.md)] の予約済みキーワードを指定する場合や、[!INCLUDE[tsql](../../includes/tsql-md.md)] の構文規則で通常は識別子として許可されない文字がある場合は、二重引用符で識別子を区切ることができます。

![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

## <a name="syntax"></a>構文

```
-- Syntax for SQL Server and Azure SQL Database

SET QUOTED_IDENTIFIER { ON | OFF }
```

```
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse

SET QUOTED_IDENTIFIER ON
```

## <a name="remarks"></a>Remarks

SET QUOTED_IDENTIFIER が ON の場合は、識別子を二重引用符で区切ることができます。リテラルは単一引用符で区切る必要があります。 SET QUOTED_IDENTIFIER が OFF の場合、識別子を引用符で区切ることはできません。識別子に関しては [!INCLUDE[tsql](../../includes/tsql-md.md)] のすべての規則に従う必要があります。 詳細については、「[データベース識別子](../../relational-databases/databases/database-identifiers.md)」を参照してください。 リテラルは単一引用符と二重引用符のどちらで区切ることもできます。

SET QUOTED_IDENTIFIER が ON (既定値) の場合、二重引用符で区切られた文字列はすべてオブジェクト識別子として解釈されます。 したがって、引用符で区切られた識別子は、識別子に関する [!INCLUDE[tsql](../../includes/tsql-md.md)] の規則に従う必要はありません。 このような識別子では予約済みキーワードを使用でき、通常は [!INCLUDE[tsql](../../includes/tsql-md.md)] の識別子として許可されない文字を含めることもできます。 リテラル文字列式を二重引用符で区切ることはできません。リテラル文字列を区切るには、単一引用符を使用する必要があります。 単一引用符 ( **'** ) がリテラル文字列の一部に含まれている場合は、2 つの連続する単一引用符 ( **''** ) を使用してください。 データベース内のオブジェクト名に対して予約済みキーワードを使用する場合は、SET QUOTED_IDENTIFIER を ON にする必要があります。

SET QUOTED_IDENTIFIER が OFF (既定値) の場合、式の内部のリテラル文字列は、単一引用符と二重引用符のどちらで区切ることもできます。 リテラル文字列を二重引用符で区切る場合は、文字列の内部でアポストロフィなどの埋め込み単一引用符を使用できます。

計算列やインデックス付きビューのインデックスを作成または操作するときには、SET QUOTED_IDENTIFIER を ON に設定する必要があります。 SET QUOTED_IDENTIFIER が OFF の場合、計算列上にインデックスが設定されているテーブルやインデックス付きビューに対して CREATE、UPDATE、INSERT、および DELETE ステートメントを実行しようとすると失敗します。 インデックス付きビューおよび計算列上のインデックスに必要な SET オプション設定の詳細については、[SET ステートメント](../../t-sql/statements/set-statements-transact-sql.md)関するページの「SET ステートメントの使用に関する留意事項」を参照してください。

フィルター選択されたインデックスを作成する場合は、SET QUOTED_IDENTIFIER を ON に設定する必要があります。

XML データ型のメソッドを呼び出す場合は、SET QUOTED_IDENTIFIER を ON に設定する必要があります。

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーおよび [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB Provider for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、接続時に自動的に QUOTED_IDENTIFIER が ON に設定されます。 これは、ODBC データ ソース、ODBC 接続属性、または OLE DB 接続プロパティを使って構成できます。 DB-Library アプリケーションからの接続に対しては、SET QUOTED_IDENTIFIER は既定で OFF に設定されています。

テーブルの作成時に QUOTED IDENTIFIER オプションが OFF に設定されていても、作成されるテーブルのメタデータでは、このオプションは常に ON として格納されます。

ストアド プロシージャを作成すると、SET QUOTED_IDENTIFIER と SET ANSI_NULLS の設定が取得され、以降そのストアド プロシージャを呼び出すときに使用されます。

SET QUOTED_IDENTIFIER をストアド プロシージャの内部で実行する場合、この設定は変更されません。

SET ANSI_DEFAULTS が ON の場合、SET QUOTED_IDENTIFIER は有効になります。

SET QUOTED_IDENTIFIER は、ALTER DATABASE の QUOTED_IDENTIFIER 設定にも対応します。 データベースの設定の詳細については、[ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md) に関するページをご覧ください。

SET QUOTED_IDENTIFIER は解析時に有効であり、解析に対してのみ影響を与え、クエリの実行には影響しません。

最上位のアドホック バッチの場合、解析は QUOTED_IDENTIFIER に対するセッションの現在の設定を使って開始します。 バッチが解析される過程で、SET QUOTED_IDENTIFIER が出現すると、それ以降の解析動作が変更され、セッションのその設定が保存されます。 したがって、バッチが解析されて実行された後、セッションの QUOTED_IDENTIFER の設定は、バッチでの SET QUOTED_IDENTIFIER の最後の出現に従って設定されます。

ストアド プロシージャ内の静的な SQL は、ストアド プロシージャを作成または変更したバッチで有効な QUOTED_IDENTIFIER の設定を使って解析されます。 SET QUOTED_IDENTIFIER は、静的 SQL としてストアド プロシージャの本体内に出現する場合は効果がありません。

sp_executesql または exec() を使う入れ子になったバッチの場合、解析はセッションの QUOTED_IDENTIFIER の設定を使って開始します。 入れ子になったバッチがストアド プロシージャの内部にある場合は、解析はストアド プロシージャの QUOTED_IDENTIFIER の設定を使って開始します。 入れ子になったバッチが解析される過程で、SET QUOTED_IDENTIFIER が出現すると、それ以降の解析動作が変更されますが、セッションの QUOTED_IDENTIFIER の設定は更新されません。

識別子を区切るための角かっこ ( **[** および **]** ) の使用は、QUOTED_IDENTIFIER オプションの設定に影響されません。

この設定の現在の設定を表示するには、次のクエリを実行します。

```sql
DECLARE @QUOTED_IDENTIFIER VARCHAR(3) = 'OFF';
IF ( (256 & @@OPTIONS) = 256 ) SET @QUOTED_IDENTIFIER = 'ON';
SELECT @QUOTED_IDENTIFIER AS QUOTED_IDENTIFIER;

```

## <a name="permissions"></a>アクセス許可

public ロールのメンバーシップが必要です。

## <a name="examples"></a>使用例

### <a name="a-using-the-quoted-identifier-setting-and-reserved-word-object-names"></a>A. 引用符で囲まれた識別子の設定と、予約済みキーワードを用いたオブジェクト名を使用する

次の例では、予約済みキーワード名を含むオブジェクト名を作成して使用するときに、`SET QUOTED_IDENTIFIER` の設定を `ON` にして、テーブル名のキーワードを二重引用符で区切る必要があることを示しています。

```sql
SET QUOTED_IDENTIFIER OFF
GO
-- An attempt to create a table with a reserved keyword as a name
-- should fail.
CREATE TABLE "select" ("identity" INT IDENTITY NOT NULL, "order" INT NOT NULL);
GO

SET QUOTED_IDENTIFIER ON;
GO

-- Will succeed.
CREATE TABLE "select" ("identity" INT IDENTITY NOT NULL, "order" INT NOT NULL);
GO

SELECT "identity","order"
FROM "select"
ORDER BY "order";
GO

DROP TABLE "SELECT";
GO

SET QUOTED_IDENTIFIER OFF;
GO
```

### <a name="b-using-the-quoted-identifier-setting-with-single-and-double-quotation-marks"></a>B. 引用符で囲まれた識別子の設定と、単一引用符および二重引用符を使用する

 次の例では、`SET QUOTED_IDENTIFIER` を `ON` に設定した場合と `OFF` に設定した場合のそれぞれに対して、文字列式で単一引用符と二重引用符を使用する方法を示しています。

```sql
SET QUOTED_IDENTIFIER OFF;
GO
USE AdventureWorks2012;
IF EXISTS(SELECT TABLE_NAME FROM INFORMATION_SCHEMA.TABLES
    WHERE TABLE_NAME = 'Test')
    DROP TABLE dbo.Test;
GO
USE AdventureWorks2012;
CREATE TABLE dbo.Test (ID INT, String VARCHAR(30)) ;
GO

-- Literal strings can be in single or double quotation marks.
INSERT INTO dbo.Test VALUES (1, "'Text in single quotes'");
INSERT INTO dbo.Test VALUES (2, '''Text in single quotes''');
INSERT INTO dbo.Test VALUES (3, 'Text with 2 '''' single quotes');
INSERT INTO dbo.Test VALUES (4, '"Text in double quotes"');
INSERT INTO dbo.Test VALUES (5, """Text in double quotes""");
INSERT INTO dbo.Test VALUES (6, "Text with 2 """" double quotes");
GO

SET QUOTED_IDENTIFIER ON;
GO

-- Strings inside double quotation marks are now treated
-- as object names, so they cannot be used for literals.
INSERT INTO dbo."Test" VALUES (7, 'Text with a single '' quote');
GO

-- Object identifiers do not have to be in double quotation marks
-- if they are not reserved keywords.
SELECT ID, String
FROM dbo.Test;
GO

DROP TABLE dbo.Test;
GO

SET QUOTED_IDENTIFIER OFF;
GO
```

[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
 ID          String
 ----------- ------------------------------
 1           'Text in single quotes'
 2           'Text in single quotes'
 3           Text with 2 '' single quotes
 4           "Text in double quotes"
 5           "Text in double quotes"
 6           Text with 2 "" double quotes
 7           Text with a single ' quote
 ```

## <a name="see-also"></a>参照

- [CREATE DATABASE](../../t-sql/statements/create-database-transact-sql.md?view=sql-server-2017)
- [CREATE DEFAULT](../../t-sql/statements/create-default-transact-sql.md)
- [CREATE PROCEDURE](../../t-sql/statements/create-procedure-transact-sql.md)
- [CREATE RULE](../../t-sql/statements/create-rule-transact-sql.md)
- [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md)
- [CREATE TRIGGER](../../t-sql/statements/create-trigger-transact-sql.md)
- [CREATE VIEW](../../t-sql/statements/create-view-transact-sql.md)
- [データ型](../../t-sql/data-types/data-types-transact-sql.md)
- [EXECUTE](../../t-sql/language-elements/execute-transact-sql.md)
- [SELECT](../../t-sql/queries/select-transact-sql.md)
- [SET Statements](../../t-sql/statements/set-statements-transact-sql.md)
- [SET ANSI_DEFAULTS](../../t-sql/statements/set-ansi-defaults-transact-sql.md)
- [sp_rename](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md)
