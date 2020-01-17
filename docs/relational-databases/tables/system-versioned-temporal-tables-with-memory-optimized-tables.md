---
title: メモリ最適化テーブルでのシステム バージョン管理されたテンポラル テーブル | Microsoft Docs
ms.custom: ''
ms.date: 07/12/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
ms.assetid: 23274522-e5cf-4095-bed8-bf986d6342e0
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ba6894a7e30c9b5112ced867766598cd62a0552f
ms.sourcegitcommit: f018eb3caedabfcde553f9a5fc9c3e381c563f1a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2019
ms.locfileid: "74165459"
---
# <a name="system-versioned-temporal-tables-with-memory-optimized-tables"></a>メモリ最適化テーブルでのシステム バージョン管理されたテンポラル テーブル

[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

[Memory-Optimized Tables](../../relational-databases/in-memory-oltp/memory-optimized-tables.md) のシステム バージョン管理されたテンポラル テーブルは、インメモリ OLTP ワークロードで収集されたデータに対して [データ監査および特定時点分析](https://msdn.microsoft.com/library/mt631669.aspx) が必要な場合にコスト効果の高いソリューションを提供するように設計されています。 高いトランザクション スループット、ロックを必要としないコンカレンシー、簡単にクエリできる大量の履歴データを格納する機能を提供します。

## <a name="overview"></a>概要

システム バージョン管理されたテンポラル テーブルは、完全なデータ変更履歴を自動的に保持し、特定時点分析用に便利な Transact-SQL 拡張機能を公開します。 一般的なシナリオでは、データの履歴は、定期的に照会されなくても、非常に長い期間 (複数月、場合によっては複数年) 保持されます。

データ監査と時間ベースの分析は、さまざまな環境で要求されることがあります。非常に大量の要求を処理し、インメモリ OLTP テクノロジが使用されている OLTP システムでは特にそうです。 ただし、テンポラル シナリオでメモリ最適化テーブルを使用するのは、生成される大量の履歴データが一般に使用可能な RAM メモリの制限を超えるため、困難です。 また、古くなるほどサクセスされなくなる読み取り専用の履歴データを格納するために RAM を使用するのは、最適なソリューションではありません。

メモリ最適化テーブルに対するシステム バージョン管理されたテンポラル テーブルは、現在のデータ (テンポラル テーブル) の格納にはメモリ内テーブルを使用し、履歴データにはディスク ベースのテーブルを使用することにより、高いトランザクション スループット、ロックを必要としないコンカレンシー、大量の履歴データを格納する機能を提供します。 内部的に自動生成されるメモリ最適化ステージング テーブルを使用して、最近の履歴を格納し、ネイティブにコンパイルされたコードから DML を実行できるようにすることで、DML 操作への影響は最小になります。

次の図に、このアーキテクチャを示します。![テンポラル インメモリ アーキテクチャ](../../relational-databases/tables/media/temporal-in-memory-architecture.png "テンポラル インメモリ アーキテクチャ")

## <a name="implementation-details"></a>実装の詳細

システム バージョン管理されたメモリ最適化テーブルを作成するときは、メモリ最適化テーブルでのシステム バージョン管理されたテンポラル テーブルについて、次の点を考慮する必要があります。 構文のオプションおよび例については、「[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)」を参照してください。

- システム バージョン管理できるのは、持続性のあるメモリ最適化テーブルだけです (**DURABILITY = SCHEMA_AND_DATA**)。
- メモリ最適化されてシステム バージョン管理されたテーブルの履歴テーブルは、エンド ユーザーまたはシステムのどちらによって作成される場合でも、ディスク ベースでなければなりません。
- 現在のテーブル (インメモリ) のみに影響するクエリは、 [ネイティブ コンパイル T-SQL モジュール](https://msdn.microsoft.com/library/dn133184.aspx)で使用できます。 FOR SYSTEM TIME 句を使用したテンポラル クエリは、ネイティブ コンパイル モジュールではサポートされません。 アドホック クエリおよび非ネイティブ モジュールでの FOR SYSTEM TIME 句とメモリ最適化テーブルの使用はサポートされています。
- **SYSTEM_VERSIONING = ON**のときは、現在のメモリ最適化テーブルでの更新および削除操作の結果である最新のシステム バージョン管理された変更を受け入れるため、内部的なメモリ最適化ステージング テーブルが自動的に作成されます。
- 内部のメモリ最適化ステージング テーブルからのデータは、非同期のデータ フラッシュ タスクによって、ディスク ベースの履歴テーブルに定期的に移動されます。 このデータ フラッシュ メカニズムの目的は、親オブジェクトによる内部メモリ バッファーのメモリ使用量を 10% 未満に維持することです。 [sys.dm_db_xtp_memory_consumers &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-memory-consumers-transact-sql.md) をクエリし、内部メモリ最適化ステージング テーブルと現在のテンポラル テーブルのデータを集計することにより、システム バージョン管理されたメモリ最適化テンポラル テーブルの総メモリ消費量を要約できます。
- データ フラッシュを適用するには、 [sp_xtp_flush_temporal_history](../../relational-databases/system-stored-procedures/temporal-table-sp-xtp-flush-temporal-history.md)を呼び出します。
- **SYSTEM_VERSIONING = OFF** のとき、またはシステム バージョン管理されたテーブルのスキーマが列を追加、削除、または変更することによって変更されると、内部ステージング バッファーの内容全体がディスク ベースの履歴テーブルに移動されます。
- 履歴データのクエリは実質的にスナップショット分離レベルであり、メモリ内ステージング バッファーとディスク ベース テーブルの重複がない和集合を常に返します。
- テーブルのスキーマを内部的に変更する**ALTER TABLE** 操作はデータのフラッシュを実行する必要があり、操作の時間を長引かせる可能性があります。

## <a name="the-internal-memory-optimized-staging-table"></a>内部メモリ最適化ステージング テーブル

内部メモリ最適化ステージング テーブルは、DML の操作を最適化するためにシステムによって作成される内部オブジェクトです。

- テーブル名は次の形式で生成されます。**Memory_Optimized_History_Table_<object_id>** 。この *<object_id>* は現在のテンポラル テーブルの識別子です。
- テーブルは、現在のテンポラル テーブルのスキーマに加えて、1 つの BIGINT 列をレプリケートします。 この追加される列により、内部履歴バッファーに移動される行の一意性が保証されます。
- 追加列の名前は次の形式です。**Change_ID[_< suffix>]** 。この *_\<suffix>* は省略可能であり、*Change_ID* 列がテーブルに既にある場合に追加されます。
- システム バージョン管理されたメモリ最適化テーブルの最大行サイズは、ステージング テーブルに追加される BIGINT 列のため、8 バイトだけ小さくなります。 新しい最大値は、8052 バイトです。
- 内部メモリ最適化ステージング テーブルは、SQL Server Management Studio のオブジェクト エクスプローラーには表されません。
- このテーブルに関するメタデータおよび現在のテンポラル テーブルとの接続については、「[sys.internal_tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-internal-tables-transact-sql.md)」を参照してください。

## <a name="the-data-flush-task"></a>データ フラッシュ タスク

データ フラッシュは定期的にアクティブ化されるタスクであり、データ移動に対するメモリ サイズに基づく条件をメモリ最適化テーブルが満たすかどうかをチェックします。 内部ステージング テーブルのメモリ使用量が現在のテンポラル テーブルのメモリ使用量の 8% に達すると、データ移動が開始します。

データ フラッシュ タスクは、既存のワークロードに基づいて変化するスケジュールで、定期的にアクティブ化されます。 ワークロードが大きいときは最短で 5 秒間隔に、ワークロードが小さいときは最長で 1 分間隔になります。 クリーンアップが必要な内部メモリ最適化ステージング テーブルごとに 1 つのスレッドが生成されます。

データ フラッシュは、現在実行している最も古いトランザクションより古いメモリ内内部バッファーからすべてのレコードを削除して、ディスク ベースの履歴テーブルにこれらのレコードを移動します。

[sp_xtp_flush_temporal_history](../../relational-databases/system-stored-procedures/temporal-table-sp-xtp-flush-temporal-history.md) を呼び出して、スキーマとテーブル名を指定することで、データ フラッシュを強制的に実行することができます: **sys.sp_xtp_flush_temporal_history @schema_name, @object_name** 。 このユーザー実行コマンドを使用すると、内部スケジュールでシステムによってデータ フラッシュ タスクが呼び出されるときと同じデータ移動プロセスが呼び出されます。

## <a name="see-also"></a>参照

- [テンポラル テーブル](../../relational-databases/tables/temporal-tables.md)
- [システム バージョン管理されたテンポラル テーブルの概要](../../relational-databases/tables/getting-started-with-system-versioned-temporal-tables.md)
- [テンポラル テーブルの使用シナリオ](../../relational-databases/tables/temporal-table-usage-scenarios.md)
- [テンポラル テーブルのシステム一貫性のチェック](../../relational-databases/tables/temporal-table-system-consistency-checks.md)
- [テンポラル テーブルでのパーティション分割](../../relational-databases/tables/partitioning-with-temporal-tables.md)
- [テンポラル テーブルの考慮事項と制約](../../relational-databases/tables/temporal-table-considerations-and-limitations.md)
- [テンポラル テーブル セキュリティ](../../relational-databases/tables/temporal-table-security.md)
- [システム バージョン管理されたテンポラル テーブルの履歴データの保有期間管理](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)
- [テンポラル テーブル メタデータのビューおよび関数](../../relational-databases/tables/temporal-table-metadata-views-and-functions.md)
