---
title: メモリ最適化のためのシステム バージョン管理されたテンポラル テーブルを作成する | Microsoft Docs
ms.custom: ''
ms.date: 05/05/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
ms.assetid: 1c1fc682-bf5b-4096-a0ff-3235d71c205a
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 79831c782524a1a9b0b7acea55ccce437e5733fd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68123625"
---
# <a name="creating-a-memory-optimized-system-versioned-temporal-table"></a>メモリ最適化のためのシステム バージョン管理されたテンポラル テーブルを作成する

[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

ディスク ベースの履歴テーブルの作成と同様、メモリ最適化されたテンポラル テーブルはさまざまな方法で作成できます。

> [!NOTE]
> メモリ最適化テーブルを作成するには、まず [メモリ最適化ファイルグループ](../../relational-databases/in-memory-oltp/the-memory-optimized-filegroup.md)を作成する必要があります。

既定の履歴テーブルによるテンポラル テーブルの作成は、名前付けを制御しながら、一方で既定の構成による履歴テーブルの作成はシステムに任せたい場合に、便利なオプションです。 次の例では、新しいシステム バージョン管理されたメモリ最適化のテンポラル テーブルが、新しいディスク ベースの履歴テーブルにリンクされています。

```sql
CREATE SCHEMA History
GO
CREATE TABLE dbo.Department
   (  
      DepartmentNumber char(10) NOT NULL PRIMARY KEY NONCLUSTERED,
      DepartmentName varchar(50) NOT NULL,
      ManagerID int NULL,
      ParentDepartmentNumber char(10) NULL,
      SysStartTime datetime2 GENERATED ALWAYS AS ROW START HIDDEN NOT NULL,
      SysEndTime datetime2 GENERATED ALWAYS AS ROW END HIDDEN NOT NULL,
      PERIOD FOR SYSTEM_TIME (SysStartTime,SysEndTime)
   )
WITH
   (
       MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA,
          SYSTEM_VERSIONING = ON ( HISTORY_TABLE = History.DepartmentHistory )
    );
```

カスタム テンポラル ソリューションを組み込みサポートに移行する場合など、既存のテーブルを使用してシステム バージョン管理を有効にする必要がある場合は、既存の履歴テーブルにリンクしたテンポラル テーブルを作成すると便利です。 次の例では、既存の履歴テーブルにリンクした新しいテンポラル テーブルを作成します。

```sql
--Existing table
CREATE TABLE Department_History
   (
      DepartmentNumber char(10) NOT NULL,
      DepartmentName varchar(50) NOT NULL,
      ManagerID int NULL,
      ParentDepartmentNumber char(10) NULL,
      SysStartTime datetime2 NOT NULL, SysEndTime datetime2 NOT NULL
   )
;
--Temporal table
CREATE TABLE Department
   (
      DepartmentNumber char(10) NOT NULL PRIMARY KEY NONCLUSTERED,
      DepartmentName varchar(50) NOT NULL,
      ManagerID INT NULL,
      ParentDepartmentNumber char(10) NULL,
      SysStartTime datetime2 GENERATED ALWAYS AS ROW START HIDDEN NOT NULL,
      SysEndTime datetime2 GENERATED ALWAYS AS ROW END HIDDEN NOT NULL,
      PERIOD FOR SYSTEM_TIME (SysStartTime,SysEndTime)
   )
WITH
   (
      SYSTEM_VERSIONING = ON
         (  
            HISTORY_TABLE = dbo.Department_History
            , DATA_CONSISTENCY_CHECK = ON
         )  
      , MEMORY_OPTIMIZED = ON
      , DURABILITY = SCHEMA_AND_DATA
   )
;
```

## <a name="see"></a>参照先

- [メモリ最適化テーブルでのシステム バージョン管理されたテンポラル テーブル](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)
- [メモリ最適化およびシステム バージョン管理されたテンポラル テーブルの使用](../../relational-databases/tables/working-with-memory-optimized-system-versioned-temporal-tables.md)
- [システムでバージョン管理されたメモリ最適化テンポラル テーブルの監視](../../relational-databases/tables/monitoring-memory-optimized-system-versioned-temporal-tables.md)
- [メモリ最適化およびシステム バージョン管理されたテンポラル テーブルのパフォーマンスに関する考慮事項](../../relational-databases/tables/memory-optimized-system-versioned-temporal-tables-performance.md)
- [テンポラル テーブル](../../relational-databases/tables/temporal-tables.md)
- [テンポラル テーブルのシステム一貫性のチェック](../../relational-databases/tables/temporal-table-system-consistency-checks.md)
- [システム バージョン管理されたテンポラル テーブルの履歴データの保有期間管理](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)
- [テンポラル テーブル メタデータのビューおよび関数](../../relational-databases/tables/temporal-table-metadata-views-and-functions.md)
