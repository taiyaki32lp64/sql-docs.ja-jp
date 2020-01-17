---
title: メモリ最適化およびシステム バージョン管理されたテンポラル テーブルの使用 | Microsoft Docs
ms.custom: ''
ms.date: 05/05/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
ms.assetid: 691d4f80-6754-43f5-8b43-d4facf08f6fc
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 12516c649614bd0d6e3a1e5fa79e3be73f606223
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68017641"
---
# <a name="working-with-memory-optimized-system-versioned-temporal-tables"></a>メモリ最適化およびシステム バージョン管理されたテンポラル テーブルの使用

[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

このトピックでは、メモリ最適化およびシステム バージョン管理されたテンポラル テーブルと、ディスク ベースのシステム バージョン管理されたテンポラル テーブルの違いについて説明します。

> [!NOTE]
> メモリ最適化されたテンポラル テーブルの使用は [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] にのみ適用され、 [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]には適用されません。

## <a name="discovering-metadata"></a>メタデータの検索

メモリ最適化およびシステム バージョン管理されたテンポラル テーブルに関するメタデータを検索するには、[sys.tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)と [sys.internal_tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-internal-tables-transact-sql.md) の情報を結合する必要があります。 システム バージョン管理されたテンポラル テーブルは、内部のインメモリ履歴テーブルの parent_object_id として表されます。

この例では、これらのテーブルをクエリおよび結合する方法を示します。

```sql
SELECT SCHEMA_NAME (T1.schema_id) as TemporalTableSchema
    , OBJECT_NAME(IT.parent_object_id) as TemporalTableName
    , T1.object_id as TemporalTableObjectId
    , IT.Name as InternalHistoryStagingName
    , SCHEMA_NAME (T2.schema_id) as HistoryTableSchema
    , OBJECT_NAME (T1.history_table_id) as HistoryTableName
FROM sys.internal_tables IT
JOIN sys.tables T1
    ON IT.parent_object_id = T1.object_id
JOIN sys.tables T2
    ON T1.history_table_id = T2.object_id
WHERE T1.is_memory_optimized = 1 AND T1.temporal_type = 2

```

## <a name="modifying-data"></a>データの変更

メモリ最適化およびシステム バージョン管理されたテンポラル テーブルは、ネイティブ コンパイル ストアド プロシージャを通じて変更できます。これにより、メモリ最適化された非テンポラル テーブルをシステム バージョン管理されたテーブルに変換し、既存のネイティブ ストアド プロシージャを保持できます。

この例では、以前に作成したテーブルをネイティブ コンパイル モジュールで変更する方法を示します。

```sql
CREATE PROCEDURE dbo.UpdateFXCurrencyPair
   (
      @ProviderID int
      , @CurrencyID1 int
      , @CurrencyID2 int
      , @BidRate decimal(8,4)
      , @AskRate decimal(8,4)
   )
WITH NATIVE_COMPILATION, SCHEMABINDING
   , EXECUTE AS OWNER
AS
   BEGIN ATOMIC WITH
   (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'English')
      UPDATE dbo.FXCurrencyPairs SET AskRate = @AskRate, BidRate = @BidRate
     WHERE ProviderID = @ProviderID AND CurrencyID1 = @CurrencyID1 AND CurrencyID2 = @CurrencyID2
END
GO ;

```

## <a name="see-also"></a>参照

- [メモリ最適化テーブルでのシステム バージョン管理されたテンポラル テーブル](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)
- [メモリ最適化のためのシステム バージョン管理されたテンポラル テーブルを作成する](../../relational-databases/tables/creating-a-memory-optimized-system-versioned-temporal-table.md)
- [システムでバージョン管理されたメモリ最適化テンポラル テーブルの監視](../../relational-databases/tables/monitoring-memory-optimized-system-versioned-temporal-tables.md)
- [メモリ最適化およびシステム バージョン管理されたテンポラル テーブルのパフォーマンスに関する考慮事項](../../relational-databases/tables/
- [テンポラル テーブル](../../relational-databases/tables/temporal-tables.md)
- [テンポラル テーブルのシステム一貫性のチェック](../../relational-databases/tables/temporal-table-system-consistency-checks.md)
- [システム バージョン管理されたテンポラル テーブルの履歴データの保有期間管理](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)
- [テンポラル テーブル メタデータのビューおよび関数](../../relational-databases/tables/temporal-table-metadata-views-and-functions.md)
