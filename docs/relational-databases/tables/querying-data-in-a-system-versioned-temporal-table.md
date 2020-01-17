---
title: システム バージョン管理されたテンポラル テーブルのデータのクエリ | Microsoft Docs
ms.custom: ''
ms.date: 03/28/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
ms.assetid: 2d358c2e-ebd8-4eb3-9bff-cfa598a39125
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 415e966e2ecebb9004e64ddedd6b96d87cedee35
ms.sourcegitcommit: f018eb3caedabfcde553f9a5fc9c3e381c563f1a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2019
ms.locfileid: "74165608"
---
# <a name="querying-data-in-a-system-versioned-temporal-table"></a>システム バージョン管理されたテンポラル テーブルのデータのクエリ

[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

テンポラル テーブルのデータの最新 (実際) の状態を取得するときは、テンポラル以外のテーブルをクエリするときとまったく同じ方法でクエリできます。 PERIOD 列が非表示ではない場合は、それらの値が SELECT \* クエリで表示されます。 **PERIOD** 列を非表示として指定した場合は、それらの値は SELECT \* クエリでは表示されません。 **PERIOD** 列が非表示の場合は、SELECT 句で **PERIOD** 列を明示的に参照すると、これらの列の値が返されます。

任意の種類の時間ベースの分析を実行するには、新しい **FOR SYSTEM_TIME** 句を使用し、テンポラル固有の 4 つのサブ句を指定して、現在のテーブルと履歴テーブルのデータをクエリします。 これらの句の詳細については、「[テンポラル テーブル](../../relational-databases/tables/temporal-tables.md)」と「[FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)」を参照してください。

- AS OF <date_time>
- FROM <start_date_time> TO <end_date_time>
- BETWEEN <start_date_time> AND <end_date_time>
- CONTAINED IN (<start_date_time> , <end_date_time>)
- ALL

**FOR SYSTEM_TIME** は、クエリで各テーブルに対して個別に指定できます。 共通テーブル式、テーブル値関数、ストアド プロシージャの中で使用できます。

## <a name="query-for-a-specific-time-using-the-as-of-sub-clause"></a>AS OF サブ句を使用した特定時点のクエリ

過去の特定時点におけるデータの状態を再構築する必要がある場合は、**AS OF** サブ句を使用します。 **PERIOD** 列の定義で指定されている datetime2 型の精度でデータを再構築できます。

**AS OF** サブ句を定数リテラルまたは変数と共に使用して、時間条件を動的に指定できます。 指定した値は UTC 時刻として解釈されます。

この最初の例では、過去の特定の日時における dbo.Department テーブルの状態が返されます。

```sql
/*State of entire table AS OF specific date in the past*/
SELECT [DeptID], [DeptName], [SysStartTime],[SysEndTime]
FROM [dbo].[Department]
FOR SYSTEM_TIME AS OF '2015-09-01 T10:00:00.7230011' ;
```

この 2 番目の例では、行のサブセットの値が 2 つの時点について比較されます。

```sql
DECLARE @ADayAgo datetime2
SET @ADayAgo = DATEADD (day, -1, sysutcdatetime())
/*Comparison between two points in time for subset of rows*/
SELECT D_1_Ago.[DeptID], D.[DeptID],
D_1_Ago.[DeptName], D.[DeptName],
D_1_Ago.[SysStartTime], D.[SysStartTime],
D_1_Ago.[SysEndTime], D.[SysEndTime]
FROM [dbo].[Department] FOR SYSTEM_TIME AS OF @ADayAgo AS D_1_Ago
JOIN [Department] AS D ON D_1_Ago.[DeptID] = [D].[DeptID]
AND D_1_Ago.[DeptID] BETWEEN 1 and 5 ;
```

### <a name="using-views-with-as-of-sub-clause-in-temporal-queries"></a>テンポラル クエリにおける AS-OF 句でのビューの使用

複雑な特定時点分析が必要なときは、ビューが非常に役に立ちます。 一般的な例は、過去 1 か月の値を使用して今日のビジネス レポートを生成する場合です。

通常、ユーザーは外部キー リレーションシップを持つ多数のテーブルを含む正規化されたデータベース モデルを使用します。 すべてのテーブルは個別に独立したパターンで変化するので、その正規化されたモデルのデータが過去の特定の時点においてどのようなものになるかは簡単にはわかりません。

このような場合に最善の方法は、ビューを作成し、 **AS OF** サブ句をビュー全体に適用することです。 この方法を使用すると、SQL Server はビューの定義に含まれるすべてのテンポラル テーブルに **AS OF** 句を透過的に適用するので、特定時点分析からデータ アクセス層のモデルを切り離すことができます。 さらに、テンポラル テーブルと非テンポラル テーブルを同じビューに含めることができます。 **AS OF** はテンポラル テーブルに対してのみ適用されます。 ビューでテンポラル テーブルが 1 つも参照されていない場合、テンポラル クエリ句をテーブルに適用するとエラーで失敗します。

```sql
/* Create view that joins three temporal tables: Department, CompanyLocation, LocationDepartments */
CREATE VIEW [dbo].[vw_GetOrgChart]
AS
SELECT
    [CompanyLocation].LocID
   , [CompanyLocation].LocName
   , [CompanyLocation].City
   , [Department].DeptID
   , [Department].DeptName
FROM [dbo].[CompanyLocation]
LEFT JOIN [dbo].[LocationDepartments]
   ON [CompanyLocation].LocID = LocationDepartments.LocID
LEFT JOIN [dbo].[Department]
   ON LocationDepartments.DeptID = [Department].DeptID ;
GO
/* Querying view AS OF */
SELECT * FROM [vw_GetOrgChart]
FOR SYSTEM_TIME AS OF '2015-09-01 T10:00:00.7230011' ;
```

## <a name="query-for-changes-to-specific-rows-over-time"></a>一定期間における特定の行への変更のクエリ

テンポラル サブ句 **FROM...TO**、 **BETWEEN...AND** 、 **CONTAINED IN** は、データの監査を実行するとき、つまり現在のテーブル内の特定の行に対するすべての変更履歴を取得する必要がある場合に、役に立ちます。

最初の 2 つのサブ句は指定された期間と重なる行のバージョンを返します (つまり、指定された期間より前に開始し、期間の後で終了するバージョン) が、CONTAINED IN は指定された期間の範囲内に存在するものだけを返します。

> [!IMPORTANT]
> 最新ではない行のバージョンのみを検索する場合は、クエリのパフォーマンスが最高になるので、履歴テーブルのクエリを直接実行することをお勧めします。 何の制限もなしに現在と履歴のデータをクエリする必要がある場合は、 **ALL** を使用します。

```sql
/* Query using BETWEEN...AND sub-clause*/
SELECT
     [DeptID]
   , [DeptName]
   , [SysStartTime]
   , [SysEndTime]
   , IIF (YEAR(SysEndTime) = 9999, 1, 0) AS IsActual
FROM [dbo].[Department]
FOR SYSTEM_TIME BETWEEN '2015-01-01' AND '2015-12-31'
WHERE DeptId = 1
ORDER BY SysStartTime DESC;

/* Query using CONTAINED IN sub-clause */
SELECT [DeptID], [DeptName], [SysStartTime],[SysEndTime]
FROM [dbo].[Department]
FOR SYSTEM_TIME CONTAINED IN ('2015-04-01', '2015-09-25')
WHERE DeptId = 1
ORDER BY SysStartTime DESC ;

/* Query using ALL sub-clause */
SELECT
     [DeptID]
   , [DeptName]
   , [SysStartTime]
   , [SysEndTime]
   , IIF (YEAR(SysEndTime) = 9999, 1, 0) AS IsActual
FROM [dbo].[Department] FOR SYSTEM_TIME ALL
ORDER BY [DeptID], [SysStartTime] Desc
```

## <a name="next-steps"></a>次のステップ

- [テンポラル テーブル](../../relational-databases/tables/temporal-tables.md)
- [FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)
- [システム バージョン管理されたテンポラル テーブルの作成](../../relational-databases/tables/creating-a-system-versioned-temporal-table.md)
- [システム バージョン管理のテンポラル テーブルのデータの変更](../../relational-databases/tables/modifying-data-in-a-system-versioned-temporal-table.md)
- [システム バージョン管理されたテンポラル テーブルのスキーマを変更する](../../relational-databases/tables/changing-the-schema-of-a-system-versioned-temporal-table.md)
- [システム バージョン管理されたテンポラル テーブルでシステム バージョン管理を停止する](../../relational-databases/tables/stopping-system-versioning-on-a-system-versioned-temporal-table.md)
