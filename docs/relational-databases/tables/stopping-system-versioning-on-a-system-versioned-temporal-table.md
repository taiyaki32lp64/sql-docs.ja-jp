---
title: システム バージョン管理されたテンポラル テーブルでシステム バージョン管理を停止する | Microsoft Docs
ms.custom: ''
ms.date: 10/11/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
ms.assetid: dddd707e-bfb1-44ff-937b-a84c5e5d1a94
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 74b222b8014b3a0e41e34d588d5893b7f4aaf9b8
ms.sourcegitcommit: f018eb3caedabfcde553f9a5fc9c3e381c563f1a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2019
ms.locfileid: "74165449"
---
# <a name="stopping-system-versioning-on-a-system-versioned-temporal-table"></a>システム バージョン管理されたテンポラル テーブルでシステム バージョン管理を停止する

[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

一時的または永続的に、テンポラル テーブルでバージョン管理を停止する場合があります。 その場合は、 **SYSTEM_VERSIONING** 句を **OFF**に設定します。

## <a name="setting-system_versioning--off"></a>SYSTEM_VERSIONING = OFF を設定する

テンポラル テーブルで特定のメンテナンス操作を実行する場合、またはバージョン管理されたテーブルを今後必要としない場合は、システム バージョン管理を停止します。 この操作により、次の 2 つの独立したテーブルが得られます。

- 期間が定義された現在のテーブル

- 通常のテーブルとしての履歴テーブル

### <a name="important-remarks"></a>重要な解説

- **SYSTEM_VERSIONING = OFF** の間、履歴テーブルでは更新の取得が**停止**します。
- **SYSTEM_VERSIONING = OFF** を設定するか、**SYSTEM_TIME** 期間を削除すると、**テンポラル テーブル**でデータが失われません。
- **SYSTEM_VERSIONING = OFF** を設定し、 **SYSTEM_TIME** 期間を削除しない場合、システムでは挿入および更新操作ごとに期間列が引き続き更新されます。 現在のテーブルでの削除は永続的なものになります。
- 期間列を完全に削除するには、 **SYSTEM_TIME** 期間を削除します。
- **SYSTEM_VERSIONING = OFF**を設定すると、十分な権限を持つすべてのユーザーが、履歴テーブルのスキーマおよび内容を変更したり、履歴テーブルを完全に削除したりできます。

### <a name="permanently-remove-system_versioning"></a>SYSTEM_VERSIONING を完全に削除する

この例では、SYSTEM_VERSIONING を完全に削除し、期間列を完全に削除します。 期間の列の削除は省略可能です。

```sql
ALTER TABLE dbo.Department SET (SYSTEM_VERSIONING = OFF);
/*Optionally, DROP PERIOD if you want to revert temporal table to a non-temporal*/
ALTER TABLE dbo.Department
DROP PERIOD FOR SYSTEM_TIME;
```

### <a name="temporarily-remove-system_versioning"></a>SYSTEM_VERSIONING を一時的に削除する

次に、システム バージョン管理を **OFF**に設定する必要がある操作を示します。

- 履歴から不要なデータを削除する (**DELETE** または **TRUNCATE**)
- バージョン管理を行わずに現在のテーブルからデータを削除する (**DELETE**、 **TRUNCATE**)
- 現在のテーブルから **SWITCH OUT** をパーティション分割する
- 現在のテーブルに **SWITCH IN** をパーティション分割する

この例では、特定のメンテナンス操作を実行できるように SYSTEM_VERSIONING を一時的に停止します。 テーブル メンテナンスの前提条件としてバージョン管理を一時的に停止する場合は、データの整合性を保つために、トランザクション内で行うことを強くお勧めします。

> [!NOTE]
> システムのバージョン管理をオンに戻すとき、HISTORY_TABLE 引数を必ず指定してください。 指定しないと、新しい履歴テーブルが作成され、現在のテーブルに関連付けられます。 元の履歴テーブルは通常のテーブルとして残りますが、現在のテーブルに関連付けられません。

```sql
BEGIN TRAN
ALTER TABLE dbo.Department SET (SYSTEM_VERSIONING = OFF);
TRUNCATE TABLE [History].[DepartmentHistory]
WITH (PARTITIONS (1,2))
ALTER TABLE dbo.Department SET
(
SYSTEM_VERSIONING = ON (HISTORY_TABLE = History.DepartmentHistory)
);
COMMIT ;
```

## <a name="next-steps"></a>次のステップ

- [テンポラル テーブル](../../relational-databases/tables/temporal-tables.md)
- [システム バージョン管理されたテンポラル テーブルの概要](../../relational-databases/tables/getting-started-with-system-versioned-temporal-tables.md)
- [システム バージョン管理されたテンポラル テーブルの履歴データの保有期間管理](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)
- [メモリ最適化テーブルでのシステム バージョン管理されたテンポラル テーブル](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)
- [システム バージョン管理されたテンポラル テーブルの作成](../../relational-databases/tables/creating-a-system-versioned-temporal-table.md)
- [システム バージョン管理のテンポラル テーブルのデータの変更](../../relational-databases/tables/modifying-data-in-a-system-versioned-temporal-table.md)
- [システム バージョン管理されたテンポラル テーブルのデータのクエリ](../../relational-databases/tables/querying-data-in-a-system-versioned-temporal-table.md)
- [システム バージョン管理されたテンポラル テーブルのスキーマを変更する](../../relational-databases/tables/changing-the-schema-of-a-system-versioned-temporal-table.md)
