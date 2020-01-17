---
title: システムでバージョン管理されたメモリ最適化テンポラル テーブルのパフォーマンス | Microsoft Docs
ms.custom: ''
ms.date: 03/28/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
ms.assetid: 2e110984-7703-4806-a24b-b41e8c3018c6
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 01db1809ae4a16183673291c135e178dfac5cd7d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68139629"
---
# <a name="memory-optimized-system-versioned-temporal-tables-performance"></a>システムでバージョン管理されたメモリ最適化テンポラル テーブルのパフォーマンス

[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

このトピックでは、システム バージョン管理およびメモリ最適化されたテンポラル テーブルを使用する場合のパフォーマンスに関するいくつかの考慮事項について説明します。

- 既存の非テンポラル テーブルにシステム バージョン管理を追加すると、履歴テーブルが自動的に更新されるため、更新操作および削除操作のパフォーマンスに影響が及ぶ可能性があります。
- 更新操作および削除操作はすべて内部のメモリ最適化履歴テーブルに記録されるため、ワークロードでこれらの 2 つの操作が大量に使用される場合に予期しない量のメモリ消費が発生する可能性があります。 したがって、以下のことをお勧めします。

  - 領域をクリーンアップして利用可能な RAM を増やすために、現在のテーブルに対する大量の削除操作を実行しない。 データの削除は、 [sp_xtp_flush_temporal_history](../../relational-databases/system-stored-procedures/temporal-table-sp-xtp-flush-temporal-history.md)を手動で呼び出してデータ フラッシュを途中で実行しながら複数のバッチに分けて実行するか、または **SYSTEM_VERSIONING = OFF**のときに実行することを検討してください。
  - 一度に大量のテーブルの更新を実行しない。そのような操作を実行すると、非テンポラル メモリ最適化テーブルの更新操作と比較して 2 倍の量のメモリが消費される場合があります。 メモリ消費量が 2 倍になる状態は一時的なものです。これは、定期的にデータ フラッシュ タスクが実行され、計画された境界内の内部ステージング テーブルのメモリ消費量が安定状態 (現在のテンポラル テーブルのメモリ使用量の約 10%) に保たれるためです。 大量の更新を実行するときは、複数のバッチに分けて実行するか、**SYSTEM_VERSIONING = OFF** のときに実行してください (更新を使用して、新しく追加された列の既定値を設定するなど)。

- データ フラッシュ タスクのアクティブ化の期間は構成できませんが、 [sp_xtp_flush_temporal_history](../../relational-databases/system-stored-procedures/temporal-table-sp-xtp-flush-temporal-history.md)のときに実行することを検討してください。
- 履歴データに対して集計またはウィンドウ関数を使用する分析クエリを実行する場合は特に、クラスター化列ストアをディスクベースの履歴テーブルのストレージ オプションとして使用することを検討してください。 そのような場合の履歴テーブル用には、優れたデータ圧縮を提供し、履歴データの生成方法に合致して "挿入操作に対応" するクラスター化列ストアが最適です。

## <a name="see-also"></a>参照

- [メモリ最適化テーブルでのシステム バージョン管理されたテンポラル テーブル](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)
- [メモリ最適化のためのシステム バージョン管理されたテンポラル テーブルを作成する](../../relational-databases/tables/creating-a-memory-optimized-system-versioned-temporal-table.md)
- [メモリ最適化およびシステム バージョン管理されたテンポラル テーブルの使用](../../relational-databases/tables/working-with-memory-optimized-system-versioned-temporal-tables.md)
- [システムでバージョン管理されたメモリ最適化テンポラル テーブルの監視](../../relational-databases/tables/monitoring-memory-optimized-system-versioned-temporal-tables.md)
- [テンポラル テーブル](../../relational-databases/tables/temporal-tables.md)
- [テンポラル テーブルのシステム一貫性のチェック](../../relational-databases/tables/temporal-table-system-consistency-checks.md)
- [システム バージョン管理されたテンポラル テーブルの履歴データの保有期間管理](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)
- [テンポラル テーブル メタデータのビューおよび関数](../../relational-databases/tables/temporal-table-metadata-views-and-functions.md)
