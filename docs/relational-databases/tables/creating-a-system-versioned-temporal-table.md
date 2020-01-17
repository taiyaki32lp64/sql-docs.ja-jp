---
title: システム バージョン管理されたテンポラル テーブルの作成 | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
ms.assetid: 21e6d74f-711f-40e6-a8b7-85f832c5d4b3
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 50c2d3aba84ce537e34b5c2bf5948c6ee84ac359
ms.sourcegitcommit: f018eb3caedabfcde553f9a5fc9c3e381c563f1a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2019
ms.locfileid: "74165224"
---
# <a name="creating-a-system-versioned-temporal-table"></a>システム バージョン管理されたテンポラル テーブルの作成

[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

システム バージョン管理されたテンポラル テーブルを作成する場合、履歴テーブルの指定方法に関して 3 つの方法があります。

- 匿名履歴テーブルでのテンポラル テーブル: 現在のテーブルのスキーマを指定し、システムが自動生成された名前で対応する履歴テーブルを作成できるようにします。
- 既定の履歴テーブルでのテンポラル テーブル: 履歴テーブルのスキーマ名とテーブル名を指定し、システムがそのスキーマで履歴テーブルを作成できるようにします。
- あらかじめ作成してあるユーザー定義履歴テーブルでのテンポラル テーブル: ニーズに最適な履歴テーブルをユーザーが作成し、テンポラル テーブルの作成時にそのテーブルを参照します。

## <a name="creating-a-temporal-table-with-an-anonymous-history-table"></a>匿名履歴テーブルによるテンポラル テーブルの作成

"匿名" 履歴テーブルを使用したテンポラル テーブルの作成は、すばやくオブジェクトを作成するための便利なオプションであり、プロトタイプおよびテスト環境で特に有効です。 また、**SYSTEM_VERSIONING** 句でパラメーターを指定する必要がないため、テンポラル テーブルを作成する最も簡単な方法でもあります。 次の例では、システム バージョン管理が有効な新しいテーブルを、履歴テーブルの名前を定義することなく作成しています。

```sql
CREATE TABLE Department
(
    DeptID INT NOT NULL PRIMARY KEY CLUSTERED
  , DeptName VARCHAR(50) NOT NULL
  , ManagerID INT NULL
  , ParentDeptID INT NULL
  , SysStartTime DATETIME2 GENERATED ALWAYS AS ROW START NOT NULL
  , SysEndTime DATETIME2 GENERATED ALWAYS AS ROW END NOT NULL
  , PERIOD FOR SYSTEM_TIME (SysStartTime,SysEndTime)
)
WITH (SYSTEM_VERSIONING = ON);
```

### <a name="important-remarks"></a>重要な解説

- システム バージョン管理されたテンポラル テーブルには、主キーと、 **PERIOD FOR SYSTEM_TIME** として宣言された 2 つの datetime2 列で定義された厳密に 1 つの **PERIOD FOR SYSTEM_TIME**が必要です。
- **PERIOD** 列は、null 値許容性が指定されていない場合でも、常に null 値非許容と見なされます。 **PERIOD** 列が明示的に Null 許容として定義されている場合、**CREATE TABLE** ステートメントは失敗します。
- 履歴テーブルは、列の数、列名、順序、データ型に関して、現在のテーブルまたはテンポラル テーブルと常にスキーマが整合している必要があります。
- 匿名履歴テーブルは、現在のテーブルまたはテンポラル テーブルと同じスキーマで自動的に作成されます。
- 匿名履歴テーブルの名前は次の形式になります。*MSSQL_TemporalHistoryFor_<current_temporal_table_object_id>_[suffix]* 。 サフィックスは省略可能であり、テーブル名の最初の部分が一意ではない場合にのみ追加されます。
- 履歴テーブルは、行ストア テーブルとして作成されます。 可能な場合はページの圧縮が適用されます。不可能な場合は、履歴テーブルは圧縮されません。 たとえば、スパース列などの一部のテーブル構成では、圧縮は許可されません。
- 履歴テーブルの既定のクラスター化インデックスは、*IX_<history_table_name>* という形式の自動生成される名前で作成されます。 クラスター化インデックスには、 **PERIOD** 列 (終了、開始) が含まれます。
- メモリ最適化テーブルとして現在のテーブルを作成する場合は、「 [メモリ最適化テーブルでのシステム バージョン管理されたテンポラル テーブル](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)」を参照してください。

## <a name="creating-a-temporal-table-with-a-default-history-table"></a>既定の履歴テーブルによるテンポラル テーブルの作成

既定の履歴テーブルによるテンポラル テーブルの作成は、名前付けを制御しながら、一方で既定の構成による履歴テーブルの作成はシステムに任せたい場合に、便利なオプションです。 次の例では、システム バージョン管理が有効な新しいテーブルを、履歴テーブルの名前を明示的に定義して作成しています。

```sql
CREATE TABLE Department
(
    DeptID INT NOT NULL PRIMARY KEY CLUSTERED
  , DeptName VARCHAR(50) NOT NULL
  , ManagerID INT NULL
  , ParentDeptID INT NULL
  , SysStartTime DATETIME2 GENERATED ALWAYS AS ROW START NOT NULL
  , SysEndTime DATETIME2 GENERATED ALWAYS AS ROW END NOT NULL
  , PERIOD FOR SYSTEM_TIME (SysStartTime, SysEndTime)
)
WITH (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.DepartmentHistory));
```

### <a name="important-remarks"></a>重要な解説

履歴テーブルは "匿名" 履歴テーブルの作成に適用されるのと同じ規則を使用して作成されますが、以下の規則は名前付き履歴テーブルだけに適用されます。

- **HISTORY_TABLE** パラメーターにはスキーマ名が必須です。
- 指定したスキーマが存在しない場合、 **CREATE TABLE** ステートメントは失敗します。
- **HISTORY_TABLE** パラメーターによって指定されているテーブルが既に存在する場合、新しく作成されるテンポラル テーブルに対して、 [スキーマの整合性およびテンポラル データの整合性](https://msdn.microsoft.com/library/dn935015.aspx)が検証されます。 無効な履歴テーブルを指定した場合、**CREATE TABLE** ステートメントは失敗します。

## <a name="creating-a-temporal-table-with-a-user-defined-history-table"></a>ユーザー定義の履歴テーブルによるテンポラル テーブルの作成

ユーザー定義の履歴テーブルによるテンポラル テーブルの作成は、ユーザーが特定のストレージ オプションと追加インデックスで履歴テーブルを指定したい場合に便利なオプションです。 次の例では、作成されるテンポラル テーブルと整合するスキーマで、ユーザー定義の履歴テーブルを作成します。 このユーザー定義の履歴テーブルに対して、クラスター化列ストア インデックスおよびその他の非クラスター化行ストア (B ツリー) インデックスが、ポイント参照用に作成されます。 このユーザー定義の履歴テーブルを作成した後、ユーザー定義の履歴テーブルを既定の履歴テーブルとして指定して、システム バージョン管理されたテンポラル テーブルを作成します。

```sql
CREATE TABLE DepartmentHistory
(
    DeptID INT NOT NULL
  , DeptName VARCHAR(50) NOT NULL
  , ManagerID INT NULL
  , ParentDeptID INT NULL
  , SysStartTime DATETIME2 NOT NULL
  , SysEndTime DATETIME2 NOT NULL
);
GO

CREATE CLUSTERED COLUMNSTORE INDEX IX_DepartmentHistory
    ON DepartmentHistory;
CREATE NONCLUSTERED INDEX IX_DepartmentHistory_ID_PERIOD_COLUMNS
    ON DepartmentHistory (SysEndTime, SysStartTime, DeptID);
GO

CREATE TABLE Department
(
    DeptID int NOT NULL PRIMARY KEY CLUSTERED
  , DeptName VARCHAR(50) NOT NULL
  , ManagerID INT NULL
  , ParentDeptID INT NULL
  , SysStartTime DATETIME2 GENERATED ALWAYS AS ROW START NOT NULL
  , SysEndTime DATETIME2 GENERATED ALWAYS AS ROW END NOT NULL
  , PERIOD FOR SYSTEM_TIME (SysStartTime,SysEndTime)
)
WITH (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.DepartmentHistory));
```

### <a name="important-remarks"></a>重要な解説

- 集計関数またはウィンドウ関数を使用する分析クエリを履歴データに対して実行する予定の場合は、圧縮とクエリ パフォーマンスを考慮し、プライマリ インデックスとしてクラスター化列ストアを作成することを強くお勧めします。
- データの監査に主に使用する場合は (つまり、現在のテーブルから単一行の変更履歴を検索する場合)、クラスター化インデックスを含む行ストア履歴テーブルを作成するのがよい方法です。
- 履歴テーブルは、主キー、外部キー、一意なインデックス、テーブル制約、トリガーを持つことはできません。 変更データ キャプチャ、変更追跡、トランザクション レプリケーション、またはマージ レプリケーション用に構成することはできません。

## <a name="alter-non-temporal-table-to-be-a-system-versioned-temporal-table"></a>非テンポラル テーブルをシステム バージョン管理されたテンポラル テーブルに変更する

カスタム テンポラル ソリューションを組み込みサポートに移行する場合など、既存のテーブルを使用してシステム バージョン管理を有効にする必要がある場合があります。
たとえば、一連のテーブルにトリガーを使用してバージョン管理を実装できます。 テンポラル システム バージョン管理を使用すると、それほど複雑ではなく、次のような利点もあります。

- 変更不可能な履歴
- タイム トラベル クエリ用の新しい構文
- DML パフォーマンスの向上
- 最小限のメンテナンス コスト

 既存のテーブルを変換するときは、新しい列を処理するように設計されていない既存のアプリケーションに影響しないように、**HIDDEN** 句を使用して新しい **PERIOD** 列 (datetime2 列の **SysStartTime** と **SysEndTime**) を非表示にすることを検討します。

### <a name="adding-versioning-to-non-temporal-tables"></a>非テンポラル テーブルへのバージョン管理の追加

データを含む非テンポラル テーブルの変更の追跡を開始する場合は、 **PERIOD** 定義を追加する必要があり、必要に応じて、SQL Server で作成される空の履歴テーブルの名前を指定します。

```sql
CREATE SCHEMA History;
GO

ALTER TABLE InsurancePolicy
    ADD
        SysStartTime DATETIME2 GENERATED ALWAYS AS ROW START HIDDEN
            CONSTRAINT DF_SysStart DEFAULT SYSUTCDATETIME()
      , SysEndTime DATETIME2 GENERATED ALWAYS AS ROW END HIDDEN
            CONSTRAINT DF_SysEnd DEFAULT CONVERT(DATETIME2, '9999-12-31 23:59:59'),
        PERIOD FOR SYSTEM_TIME (SysStartTime, SysEndTime);
GO

ALTER TABLE InsurancePolicy
    SET (SYSTEM_VERSIONING = ON (HISTORY_TABLE = History.InsurancePolicy));
```

> [!IMPORTANT]
> DATETIME2 の有効桁数は、基になるテーブルの有効桁数に合わせる必要があります。次の解説を参照してください。

#### <a name="important-remarks"></a>重要な解説

- データが含まれる既存のテーブルに既定値のある null 非許容列を追加することは、SQL Server Enterprise Edition 以外のすべてのエディションではデータ サイズ操作 (Enterprise Edition ではメタデータ操作) となります。 SQL Server Standard Edition では、データが含まれる既存の大規模な履歴テーブルの場合、非 null 列の追加はコストのかかる操作になることがあります。
- 期間開始列および期間終了列に対する制約は、慎重に選択する必要があります。

  - 開始列の既定値では、既存の行が有効であると考慮することを始める時点を指定します。 未来の時刻は指定できません。
  - 終了日時は、特定の datetime2 精度に対する最大値として指定する必要があります。
- 期間を追加すると、現在のテーブルでデータ整合性チェックが実行されて、期間列の既定値が有効であることが確認されます。
- **SYSTEM_VERSIONING**を有効にするときに既存の履歴テーブルを指定すると、現在のテーブルと履歴テーブルの両方に対してデータの整合性チェックが行われます。 **DATA_CONSISTENCY_CHECK = OFF** を追加パラメーターとして指定した場合は、スキップできます。

### <a name="migrate-existing-tables-to-built-in-support"></a>既存のテーブルを組み込みサポートに移行する

この例では、トリガーに基づく既存のソリューションを組み込みのテンポラル サポートに移行する方法を示します。 この例では、現在のカスタム ソリューションによって現在および過去のデータが 2 つの異なるユーザー テーブル (**ProjectTaskCurrent** と **ProjectTaskHistory**) に分割されるものとします。 既存のソリューションが 1 つのテーブルを使用して実際の行と過去の行を格納している場合は、この例に示す移行手順を実行する前に、データを 2 つのテーブルに分割する必要があります。

```sql
/*Drop trigger on future temporal table*/
DROP TRIGGER ProjectCurrent_OnUpdateDelete;
/*Make sure that future period columns are non-nullable*/
ALTER TABLE ProjectTaskCurrent ALTER COLUMN [ValidFrom] datetime2 NOT NULL;
ALTER TABLE ProjectTaskCurrent ALTER COLUMN [ValidTo] datetime2 NOT NULL;
ALTER TABLE ProjectTaskHistory ALTER COLUMN [ValidFrom] datetime2 NOT NULL;
ALTER TABLE ProjectTaskHistory ALTER COLUMN [ValidTo] datetime2 NOT NULL;
ALTER TABLE ProjectTaskCurrent
    ADD PERIOD FOR SYSTEM_TIME ([ValidFrom], [ValidTo])
ALTER TABLE ProjectTaskCurrent
    SET (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.ProjectTaskHistory, DATA_CONSISTENCY_CHECK = ON));
```

#### <a name="important-remarks"></a>重要な解説

- **PERIOD** 定義の既存の列を参照すると、generated_always_type がこれらの列の **AS_ROW_START** および **AS_ROW_END** に暗黙的に変更されます。
- **PERIOD** を追加すると、現在のテーブルでデータ整合性チェックが実行されて、期間列の既存の値が有効であることが確認されます。
- **DATA_CONSISTENCY_CHECK = ON** で **SYSTEM_VERSIONING** を設定し、既存データに対するデータ整合性チェックを強制的に行うことを強くお勧めします。
- 非表示列が優先される場合は、`ALTER TABLE [tableName] ALTER COLUMN [columnName] ADD HIDDEN;` コマンドを使用します。

## <a name="next-steps"></a>次のステップ

- [テンポラル テーブル](../../relational-databases/tables/temporal-tables.md)
 [システム バージョン管理されたテンポラル テーブルの概要](../../relational-databases/tables/getting-started-with-system-versioned-temporal-tables.md)
- [システム バージョン管理されたテンポラル テーブルの履歴データの保有期間管理](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)
- [メモリ最適化テーブルでのシステム バージョン管理されたテンポラル テーブル](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)
- [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)
- [システム バージョン管理のテンポラル テーブルのデータの変更](../../relational-databases/tables/modifying-data-in-a-system-versioned-temporal-table.md)
- [システム バージョン管理されたテンポラル テーブルのデータのクエリ](../../relational-databases/tables/querying-data-in-a-system-versioned-temporal-table.md)
- [システム バージョン管理されたテンポラル テーブルのスキーマを変更する](../../relational-databases/tables/changing-the-schema-of-a-system-versioned-temporal-table.md)
- [システム バージョン管理されたテンポラル テーブルでシステム バージョン管理を停止する](../../relational-databases/tables/stopping-system-versioning-on-a-system-versioned-temporal-table.md)  
