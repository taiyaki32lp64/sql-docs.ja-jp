---
title: システム バージョン管理のテンポラル テーブルのデータの変更 | Microsoft Docs
ms.custom: ''
ms.date: 03/28/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
ms.assetid: 5f398470-c531-47b5-84d5-7c67c27df6e5
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: fe84e3a8a74f50ffb19efd3bfe62dbd6900be3f2
ms.sourcegitcommit: f018eb3caedabfcde553f9a5fc9c3e381c563f1a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2019
ms.locfileid: "74165713"
---
# <a name="modifying-data-in-a-system-versioned-temporal-table"></a>システム バージョン管理のテンポラル テーブルのデータの変更

[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

システム バージョン管理のテンポラル テーブル内のデータは、通常の DML ステートメントを使用して変更しますが、1 つの重要な違いがあり、期間の列のデータは直接変更できません。 データが更新されると、バージョンが更新されて、更新された各行の以前のバージョンが、履歴テーブルに挿入されます。 データが削除された場合、削除は論理的で、行が現在のテーブルから履歴テーブルに移動され、完全に削除されるわけではありません。

## <a name="inserting-data"></a>データの挿入

新しいデータを挿入する際に、 **PERIOD** 列が **HIDDEN**でない場合、それらの列を考慮する必要があります。 システム バージョン管理のテンポラル テーブルでは、パーティション切り替えを使用することもできます。

### <a name="insert-new-data-with-visible-period-columns"></a>表示する period 列のある新しいデータの挿入

表示する **PERIOD** 列がある場合、次のように **INSERT** ステートメントを構築して、新しい **PERIOD** 列を考慮できます。

- **INSERT** ステートメントで列リストを指定する場合、システムによって、 **PERIOD** 列の値が自動的に生成されるため、それらの列を省略できます。

  ```sql
  -- Insert with column list and without period columns
  INSERT INTO [dbo].[Department]0
    (  [DeptID]
          , [DeptName]
          , [ManagerID]
          ,[ParentDeptID]
    )
       VALUES
         (  10
         , 'Marketing'
         , 101
         , 1
         ) ;
   ```

- **INSERT** ステートメントで列リストに **PERIOD** 列を指定した場合、それらの値として **DEFAULT** を指定する必要があります。

  ```sql
  INSERT INTO [dbo].[Department]
    (  [DeptID]
          , [DeptName]
          , [ManagerID]
          , [ParentDeptID]
          , SysStartTime
          , SysEndTime
    )
       VALUES
         (  11
          , 'Sales'
          , 101
          , 1
          , default
          , default) ;
   ```

- **INSERT** ステートメントで列リストを指定しない場合は、 **PERIOD** 列に **DEFAULT** を指定します。

  ```sql
    -- Insert without column list and DEFAULT values for period columns
    INSERT INTO [dbo].[Department]
    VALUES(12, 'Production', 101, 1, default, default);

  ```

### <a name="insert-data-into-a-table-with-hidden-period-columns"></a>HIDDEN period 列のあるテーブルへのデータの挿入

**PERIOD** 列を HIDDEN として指定する場合、INSERT を使用する際に、列リストを指定せずに、表示する列の値を指定するだけです。 **INSERT** ステートメントで新しい **PERIOD** 列を考慮する必要はありません。 この動作により、バージョン管理からメリットが得られるテーブルのシステム バージョン管理を有効にしたときに、レガシ アプリケーションが引き続き機能します。

```sql
CREATE TABLE [dbo].[CompanyLocation]
(
     [LocID] [int] IDENTITY(1,1) NOT NULL PRIMARY KEY
   , [LocName] [varchar](50) NOT NULL
   , [City] [varchar](50) NOT NULL
   , [SysStartTime] [datetime2] GENERATED ALWAYS AS ROW START HIDDEN NOT NULL
   , [SysEndTime] [datetime2] GENERATED ALWAYS AS ROW END HIDDEN NOT NULL
   , PERIOD FOR SYSTEM_TIME ([SysStartTime], [SysEndTime])
)
WITH ( SYSTEM_VERSIONING = ON );
GO
INSERT INTO [dbo].[CompanyLocation]
VALUES ('Headquarters', 'New York');

```

### <a name="inserting-data-using-partition-switch"></a>PARTITION SWITCH を使用したデータの挿入

現在のテーブルがパーティション分割されている場合、空のパーティションにデータを読み込むか、または複数のパーティションに並列に読み込むための効率的なメカニズムとしてパーティション切り替えを使用できます。

システム バージョン管理のテンポラル テーブルと共に **PARTITION SWITCH IN** ステートメントで使用されるステージング テーブルは、 **SYSTEM_TIME PERIOD** が定義されている必要がありますが、システム バージョン管理のテンポラル テーブルである必要はありません。
これにより、ステージング テーブルへのデータの挿入時または、設定済みのステージング テーブルに SYSTEM_TIME 期間が追加されたときに、一時的な整合性チェックが実行されます。

```sql
/*Create staging table with period definition for SWITCH IN temporal table*/
CREATE TABLE [dbo].[Staging_Department_Partition2]
(
     [DeptID] [int] NOT NULL
   , [DeptName] [varchar](50) NOT NULL
   , [ManagerID] [int] NULL
   , [ParentDeptID] [int] NULL
   , [SysStartTime] [datetime2] GENERATED ALWAYS AS ROW START NOT NULL
   , [SysEndTime] [datetime2] GENERATED ALWAYS AS ROW END NOT NULL
   , PERIOD FOR SYSTEM_TIME ( [SysStartTime], [SysEndTime] )
) ON [PRIMARY]

/*Create aligned primary key*/
ALTER TABLE [dbo].[Staging_Department_Partition2]
ADD CONSTRAINT [Staging_Department_Partition2_PK]
   PRIMARY KEY CLUSTERED
   ( [DeptID] ASC )
   ON [PRIMARY]
  
/*
Create and enforce constraints for partition boundaries.
Partition 2 contains rows with DeptID > 100 and DeptID <=200
*/
ALTER TABLE [dbo].[Staging_Department_Partition2]
   WITH CHECK ADD  CONSTRAINT [chk_staging_Department_partition_2]
   CHECK  ([DeptID]>N'100' AND [DeptID]<=N'200')
ALTER TABLE [dbo].[Staging_Department_Partition2]
   CHECK CONSTRAINT [chk_staging_Department_partition_2]

/*Load data into staging table*/
INSERT INTO [dbo].[staging_Department] ([DeptID],[DeptName],[ManagerID],[ParentDeptID])
VALUES (101,'D101',1,NULL)

/*Use PARTITION SWITCH IN to efficiently add data to current table */
ALTER TABLE [Staging_Department]
SWITCH TO [dbo].[Department] PARTITION 2;
```

期間定義のないテーブルから PARTITION SWITCH を実行しようとすると、エラー メッセージが表示されます。 `Msg 13577, Level 16, State 1, Line 25 ALTER TABLE SWITCH statement failed on table 'MyDB.dbo.Staging_Department_2015_09_26' because target table has SYSTEM_TIME PERIOD while source table does not have it.`

## <a name="updating-data"></a>データを更新する

標準の **UPDATE** ステートメントで、現在のテーブルのデータを更新します。 「不測の」シナリオに備えて、履歴テーブルから現在のテーブルのデータを更新できます。 ただし、 **PERIOD** 列を更新できず、 **SYSTEM_VERSIONING = ON**の間、履歴テーブル内のデータを直接更新することはできません。

**SYSTEM_VERSIONING = OFF** を設定し、現在および履歴テーブルの行を更新しますが、システムは変更の履歴を保持しないことに注意してください。

### <a name="updating-the-current-table"></a>現在のテーブルの更新

この例では、DeptID = 10 の各行に対し、ManagerID 列が更新されます。 **PERIOD** 列は参照されません。

```sql
UPDATE [dbo].[Department] SET [ManagerID] = 501 WHERE [DeptID] = 10
```

ただし、 **PERIOD** 列を更新できず、履歴テーブルを更新できません。 この例では、 **PERIOD** 列を更新しようとすると、エラーが生成されます。

```sql
UPDATE [dbo].[Department]
SET SysStartTime = '2015-09-23 23:48:31.2990175'
WHERE DeptID = 10 ;

Msg 13537, Level 16, State 1, Line 3
Cannot update GENERATED ALWAYS columns in table 'TmpDev.dbo.Department'.
```

### <a name="updating-the-current-table-from-the-history-table"></a>履歴テーブルからの現在のテーブルの更新

現在のテーブルに対して **UPDATE** を使用して、実際の行の状態を、過去の特定の時点で有効な状態に戻すことができます ("最終の正常な既知の行バージョン" への復元)。 次の例は、2015-04-25 現在の履歴テーブル内の値に戻すことを示しています。ここで、DeptID = 10 です。

```sql
UPDATE Department
SET DeptName = History.DeptName
FROM Department
FOR SYSTEM_TIME AS OF '2015-04-25' AS History
WHERE History.DeptID = 10
AND Department.DeptID = 10 ;
```

## <a name="deleting-data"></a>データを削除する

通常の **DELETE** ステートメントで、現在のテーブル内のデータを削除します。 削除された行の終了期間列には、基になるトランザクションの開始時間が設定されます。 **SYSTEM_VERSIONING = ON**の間、履歴テーブルから行を直接削除することはできません。 **SYSTEM_VERSIONING = OFF** を設定し、現在および履歴テーブルから行を削除しますが、システムは変更の履歴を保持しないことに注意してください。 **SYSTEM_VERSIONING = ON**の間、現在のテーブルの **TRUNCATE** と **SWITCH PARTITION OUT** 、および履歴テーブルの **SWITCH PARTITION IN**はサポートされません。

## <a name="using-merge-to-modify-data-in-temporal-table"></a>MERGE を使用したテンポラル テーブルのデータの変更

**MERGE** 操作は、 **INSERT** および **UPDATE** ステートメントの **PERIOD** 列に関して持つ制限と同じ制限付きでサポートされます。

```sql
CREATE TABLE DepartmentStaging (DeptId INT, DeptName varchar(50));
GO
INSERT INTO DepartmentStaging VALUES (1, 'Company Management');
INSERT INTO DepartmentStaging VALUES (10, 'Science & Research');
INSERT INTO DepartmentStaging VALUES (15, 'Process Management');

MERGE dbo.Department AS target
USING (SELECT DeptId, DeptName FROM DepartmentStaging) AS source (DeptId, DeptName)
ON (target.DeptId = source.DeptId)
WHEN MATCHED THEN
    UPDATE
   SET DeptName = source.DeptName
WHEN NOT MATCHED THEN
   INSERT (DeptName)
   VALUES (source.DeptName);
```

## <a name="next-steps"></a>次のステップ

- [テンポラル テーブル](../../relational-databases/tables/temporal-tables.md)
- [システム バージョン管理されたテンポラル テーブルの作成](../../relational-databases/tables/creating-a-system-versioned-temporal-table.md)
- [システム バージョン管理されたテンポラル テーブルのデータのクエリ](../../relational-databases/tables/querying-data-in-a-system-versioned-temporal-table.md)
- [システム バージョン管理されたテンポラル テーブルのスキーマを変更する](../../relational-databases/tables/changing-the-schema-of-a-system-versioned-temporal-table.md)
- [システム バージョン管理されたテンポラル テーブルでシステム バージョン管理を停止する](../../relational-databases/tables/stopping-system-versioning-on-a-system-versioned-temporal-table.md)
