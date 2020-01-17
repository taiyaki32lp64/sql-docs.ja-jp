---
title: システム バージョン管理されたテンポラル テーブルの概要 | Microsoft Docs
ms.custom: ''
ms.date: 03/28/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
ms.assetid: d431f216-82cf-4d97-825e-bb35d3d53a45
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 725dbc3306f9ad9616b5cbeca2d96249dca1c4a8
ms.sourcegitcommit: f018eb3caedabfcde553f9a5fc9c3e381c563f1a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2019
ms.locfileid: "74165784"
---
# <a name="getting-started-with-system-versioned-temporal-tables"></a>システム バージョン管理されたテンポラル テーブルの概要

[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

シナリオに応じて、システム バージョン管理された新しいテンポラル テーブルを作成するか、既存のテーブル スキーマにテンポラル属性を追加して既存のテーブルを変更できます。 テンポラル テーブル内のデータが変更されると、バージョン履歴がアプリケーションとエンド ユーザーに対して透過的に構築されます。 このため、システム バージョン管理されたテンポラル テーブルの操作では、テーブルの変更方法や最新 (実際の) データへのクエリの実行方法を変更する必要はありません。

また、テンポラルには、通常の DML やクエリ実行のほかに、拡張 Transact-SQL 構文でデータ履歴から情報を簡単かつ便利に取得する方法も用意されています。 すべてのシステム バージョン管理されたテーブルに履歴テーブルが割り当てられていますが、これはユーザーに対して完全に透過的です。ただし、ユーザーが追加のインデックスを作成するか、別のストレージ オプションを選択して、ワークロードのパフォーマンスまたはストレージの使用量を最適化する必要がある場合は除きます。

次の図は、システム バージョン管理されたテンポラル テーブルの一般的なワークフローを示しています。![テンポラルの概要](../../relational-databases/tables/media/getting-started-with-temporal.png "|::ref1::|")

このトピックには、次の 5 つのセクションがあります。

- [システム バージョン管理されたテンポラル テーブルの作成](../../relational-databases/tables/creating-a-system-versioned-temporal-table.md)
- [システム バージョン管理のテンポラル テーブルのデータの変更](../../relational-databases/tables/modifying-data-in-a-system-versioned-temporal-table.md)
- [システム バージョン管理されたテンポラル テーブルのデータのクエリ](../../relational-databases/tables/querying-data-in-a-system-versioned-temporal-table.md)
- [システム バージョン管理されたテンポラル テーブルのスキーマを変更する](../../relational-databases/tables/changing-the-schema-of-a-system-versioned-temporal-table.md)
- [システム バージョン管理されたテンポラル テーブルでシステム バージョン管理を停止する](../../relational-databases/tables/stopping-system-versioning-on-a-system-versioned-temporal-table.md)

## <a name="next-steps"></a>次のステップ

- [テンポラル テーブル](../../relational-databases/tables/temporal-tables.md)
- [テンポラル テーブルのシステム一貫性のチェック](../../relational-databases/tables/temporal-table-system-consistency-checks.md)
- [テンポラル テーブルでのパーティション分割](../../relational-databases/tables/partitioning-with-temporal-tables.md)
- [テンポラル テーブルの考慮事項と制約](../../relational-databases/tables/temporal-table-considerations-and-limitations.md)
- [テンポラル テーブル セキュリティ](../../relational-databases/tables/temporal-table-security.md)
- [システム バージョン管理されたテンポラル テーブルの履歴データの保有期間管理](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)
- [メモリ最適化テーブルでのシステム バージョン管理されたテンポラル テーブル](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)
- [テンポラル テーブル メタデータのビューおよび関数](../../relational-databases/tables/temporal-table-metadata-views-and-functions.md)
