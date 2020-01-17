---
title: システム バージョン管理されたテンポラル テーブルのスキーマを変更する | Microsoft Docs
ms.custom: ''
ms.date: 03/28/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
ms.assetid: 9dbe5a21-9335-4f8b-85fd-9da83df79946
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e9e3cdde5807172ef92f63179a4e9530b1540bfb
ms.sourcegitcommit: f018eb3caedabfcde553f9a5fc9c3e381c563f1a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2019
ms.locfileid: "74165675"
---
# <a name="changing-the-schema-of-a-system-versioned-temporal-table"></a>システム バージョン管理されたテンポラル テーブルのスキーマを変更する

[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

**ALTER TABLE** ステートメントを使用して、列を追加、変更、または削除します。

## <a name="examples"></a>例

ここでは、テンポラル テーブルのスキーマを変更する例をいくつか示します。

```sql
ALTER TABLE dbo.Department
    ALTER COLUMN DeptName varchar(100);

ALTER TABLE dbo.Department
    ADD WebAddress nvarchar(255) NOT NULL
    CONSTRAINT DF_WebAddress DEFAULT 'www.mycompany.com';

ALTER TABLE dbo.Department
    ADD TempColumn INT;

GO

ALTER TABLE dbo.Department
    DROP COLUMN TempColumn;

/* Setting IsHidden property for period columns.
Use ALTER COLUMN <period_column> DROP HIDDEN to clear IsHidden flag */

ALTER TABLE dbo.Department
    ALTER COLUMN SysStartTime ADD HIDDEN;

ALTER TABLE dbo.Department
    ALTER COLUMN SysEndTime ADD HIDDEN;
```

### <a name="important-remarks"></a>重要な解説

- テンポラル テーブルのスキーマを変更するには、現在のテーブルおよび履歴テーブルの**CONTROL** 権限が必要です。
- **ALTER TABLE** 操作中は、システムが両方のテーブルのスキーマ ロックを保持します。
- 指定したスキーマ変更は、適切に (変更の種類に応じて) 履歴テーブルに反映されます。
- NULL 値を許容しない列を追加する、または既存の列を NULL 値を許容しない列に変更する場合、既存の行に既定値を指定する必要があります。 システムは同じ値で追加の既定値を生成し、その既定値を履歴テーブルに適用します。 **DEFAULT** を空でないテーブルに追加すると、(メタデータの操作がある) [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise Edition 以外のすべてのエディション上でのデータ操作のサイズは 1 つになります。
- varchar(max)、nvarchar(max)、varbinary(max)、または既定値のある XML 列を追加すると、すべてのエディションの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]上のデータ操作を更新することになります。
- 列の追加後の行サイズが行サイズの上限を超えた場合、新しい列をオンラインで追加することはできません。
- 新しい NOT NULL の列でテーブルを拡張すると、テーブルのすべての列がシステムから自動的に生成されるため、履歴テーブルの既定の制約が削除されることを考慮してください。
- システムでバージョン管理されたテンポラル テーブルの場合、ONLINE オプション (**WITH (ONLINE = ON**) は **ALTER TABLE ALTER COLUMN** に影響を与えません。 ONLINE オプションに指定された値に関係なく、ALTER 列はオンラインとしては実行されません。
- **ALTER COLUMN** を使用して、期間の列の **IsHidden** プロパティを変更できます。
- 次のスキーマ変更の **ALTER** を直接使用することはできません。 これらの種類の変更には、 **SYSTEM_VERSIONING = OFF**を設定します。

  - 計算列を追加する
  - **IDENTITY** 列を追加する
  - 履歴テーブルが **DATA_COMPRESSION = PAGE** または **DATA_COMPRESSION = ROW**(履歴テーブルの既定値) に設定されている場合に、 **SPARSE** 列を追加する、または既存の列を **SPARSE**に変更する
  - **COLUMN_SET**を追加する
  - **ROWGUIDCOL** 列を追加する、または既存の列を **ROWGUIDCOL**に変更する

**SYSTEM_VERSIONING = OFF** の設定が継続して必要な場合に ( **IDENTITY** 列を追加して)、スキーマを変更する例を次に示します。 この例では、データの整合性チェックを無効にしています。 同時実行データの変更が発生しないときに、トランザクション内でスキーマ変更が行われる場合、このチェックは必要ありません。

```sql
    BEGIN TRAN
        ALTER TABLE [dbo].[CompanyLocation] SET (SYSTEM_VERSIONING = OFF);
        ALTER TABLE [CompanyLocation] ADD Cntr INT IDENTITY (1,1);
        ALTER TABLE [dbo].[CompanyLocationHistory] ADD Cntr INT NOT NULL DEFAULT 0;
        ALTER TABLE [dbo].[CompanyLocation]
    SET
         (
            SYSTEM_VERSIONING = ON
           ( HISTORY_TABLE = [dbo].[CompanyLocationHistory])
         );
    COMMIT ;
```

## <a name="next-steps"></a>次のステップ

- [テンポラル テーブル](../../relational-databases/tables/temporal-tables.md)
 [システム バージョン管理されたテンポラル テーブルの概要](../../relational-databases/tables/getting-started-with-system-versioned-temporal-tables.md)
- [システム バージョン管理されたテンポラル テーブルの履歴データの保有期間管理](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)
- [メモリ最適化テーブルでのシステム バージョン管理されたテンポラル テーブル](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)
- [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)
- [システム バージョン管理されたテンポラル テーブルの作成](../../relational-databases/tables/creating-a-system-versioned-temporal-table.md)
- [システム バージョン管理のテンポラル テーブルのデータの変更](../../relational-databases/tables/modifying-data-in-a-system-versioned-temporal-table.md)
- [システム バージョン管理されたテンポラル テーブルのデータのクエリ](../../relational-databases/tables/querying-data-in-a-system-versioned-temporal-table.md)
- [システム バージョン管理されたテンポラル テーブルでシステム バージョン管理を停止する](../../relational-databases/tables/stopping-system-versioning-on-a-system-versioned-temporal-table.md)
