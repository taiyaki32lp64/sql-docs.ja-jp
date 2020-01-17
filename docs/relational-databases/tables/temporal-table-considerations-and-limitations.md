---
title: テンポラル テーブルの考慮事項と制約 | Microsoft Docs
ms.custom: ''
ms.date: 09/12/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
ms.assetid: c8a21481-0f0e-41e3-a1ad-49a84091b422
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 516159955d7e4d69d52f1f462c818e3c005f30b3
ms.sourcegitcommit: d1bc0dd1ac626ee7034a36b81554258994d72c15
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/12/2019
ms.locfileid: "70958335"
---
# <a name="temporal-table-considerations-and-limitations"></a>テンポラル テーブルの考慮事項と制約

[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

テンポラル テーブルを使用する場合は、システムのバージョン管理の性質の上、注意すべき考慮事項と制約がいくつかあります。

テンポラル テーブルを使用する場合は、次のことを考慮してください。

- テンポラル テーブルには、現在のテーブルと履歴テーブルの間でレコードを関連付けるために主キーが定義されている必要があります。履歴テーブルに主キーを定義することはできません。
- データ型 datetime2 を使用して、 **SysStartTime** と **SysEndTime** の値を記録するために使用する SYSTEM_TIME 期間列を定義する必要があります。
- 履歴テーブルの作成時に履歴テーブルの名前を指定すると場合、は、スキーマとテーブルの名前を指定する必要があります。
- 履歴テーブルには既定では、 **PAGE** 圧縮します。
- 現在のテーブルがパーティション分割する場合、履歴テーブルは、パーティション分割構成がレプリケートされていないために自動的に現在のテーブルから履歴テーブルに既定のファイル グループに作成されます。
- テンポラル テーブルと履歴テーブルは **FILETABLE** にすることができず、サポートされている **FILESTREAM** 以外の任意のデータ型の列を含めることができます。これは、 **FILETABLE** と **FILESTREAM** では [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の外部でのデータ操作が可能なので、システムのバージョン管理を保証できないためです。
- ノード テーブルまたはエッジ テーブルは、テンポラル テーブルとして作成することも、テンポラル テーブルに変更することもできません。
- テンポラル テーブルでは、 **(n)varchar(max)** 、 **varbinary(max)** 、 **(n)text**、 **image**などの BLOB データ型がサポートされていますが、これらは多大なストレージ コストを発生させ、サイズが多いためにパフォーマンスに影響を与えます。 そのため、システムの設計時に、これらのデータ型を使用する場合は注意が必要です。
- 履歴テーブルは、現在のテーブルと同じデータベースで作成する必要があります。 **Linked Server** に対するテンポラル クエリはサポートされていません。
- 履歴テーブルには、制約 (主キー、外部キー、テーブル、または列の制約) を含めることはできません。
- テンポラル クエリ (**FOR SYSTEM_TIME** 句を使用するクエリ) 上では、インデックス付きビューはサポートされていません。
- システムでバージョン管理されたテンポラル テーブルの場合、ONLINE オプション (**WITH (ONLINE = ON**) は **ALTER TABLE ALTER COLUMN** に影響を与えません。 ONLINE オプションに指定された値に関係なく、ALTER 列はオンラインとしては実行されません。
- **INSERT** および **UPDATE** ステートメントは、SYSTEM_TIME 期間列を参照できません。 これらの列に値を直接挿入しようとすると、ブロックされます。
- **SYSTEM_VERSIONING** が **オン** になっている時は、 **TRUNCATE TABLE**
- 履歴テーブルのデータを直接変更することはできません。
- 現在のテーブルでは、**ON DELETE CASCADE** と **ON UPDATE CASCADE** は許可されません。 つまり、テンポラル テーブルが外部キー リレーションシップの参照元テーブル (sys.foreign_keys の *parent_object_id* に対応) である場合、CASCADE オプションは使用できません。 この制約を回避するには、アプリケーション ロジックまたは AFTER トリガーを使用して、主キー テーブル (sys.foreign_keys の *referenced_object_id* に対応) での削除の一貫性を維持します。 主キー テーブルがテンポラルで、参照元テーブルが非テンポラルである場合、このような制約はありません。

  > [!NOTE]
  > この制限は SQL Server 2016 にのみ適用されます。 CASCADE オプションは、[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] および SQL Server 2017 CTP 2.0 以降でサポートされます。

- DML ロジックが無効になるのを防ぐために、**INSTEAD OF** トリガーは現在のテーブルでも履歴テーブルでも許可されません。 **AFTER** トリガーは、現在のテーブルでのみ許可されます。 DML ロジックが無効になるのを防ぐために、このトリガーは履歴テーブルではブロックされます。
- レプリケーション テクノロジの使用量は制限されています。

  - **Always On:** 完全にサポートされています
  - **変更データ キャプチャと変更データの追跡:** 現在のテーブルでのみサポートされます
  - **スナップショットおよびトランザクション レプリケーション**:1 つのパブリッシャー (テンポラルが有効化されない)、および 1 つのサブスクライバー (テンポラルが有効化される) でのみサポートされます。 この場合、パブリッシャーは OLTP ワークロードに使用され、サブスクライバーはオフロード レポート ('AS OF' クエリを含む) に使用されます。 複数のサブスクライバーの使用はサポートされません。このシナリオでは、各サブスクライバーがローカル システム クロックに依存するので、テンポラル データが一貫性のないものになる可能性があるためです。
  - **マージ レプリケーション:** テンポラル テーブルではサポートされません

- 定期的なクエリは、現在のテーブルのデータにのみ影響を与えます。 履歴テーブルのデータに対してクエリを実行するには、テンポラル クエリを使用する必要があります。 これらについては、このドキュメントの後半にある「Querying Temporal Data (テンポラル データのクエリ)」セクションで説明します。
- 最適なインデックス作成方法では、最適なストレージのサイズとパフォーマンスのために、現在のテーブルにクラスター化列ストア インデックスまたは B ツリー行ストア インデックス、および履歴テーブルにクラスター化列ストア インデックスを含めます。 独自の履歴テーブルを作成または使用する場合は、期間列の終端から始まる期間列で構成される、この種類のインデックスを作成することを強くお勧めします。これにより、テンポラル クエリだけでなく、データ整合性チェックに含まれるクエリをすばやく実行できます。 既定の履歴テーブルには、期間列 (終了、開始) に基づいて作成されたクラスター化行ストア インデックスが含まれます。 少なくとも、非クラスター化行ストア インデックスを使用することをお勧めします。
- 次のオブジェクト/プロパティは、履歴テーブルの作成時に、現在のテーブルから履歴テーブルにレプリケートされません。

  - 期間の定義
  - ID の定義
  - インデックス
  - 統計
  - CHECK 制約
  - トリガー
  - パーティション分割構成
  - アクセス許可
  - 行レベルのセキュリティ述語

- 履歴テーブルは、履歴テーブルのチェーン内で現在のテーブルとして構成することはできません。

## <a name="see-also"></a>参照

- [テンポラル テーブル](../../relational-databases/tables/temporal-tables.md)
- [システム バージョン管理されたテンポラル テーブルの概要](../../relational-databases/tables/getting-started-with-system-versioned-temporal-tables.md)
- [テンポラル テーブルのシステム一貫性のチェック](../../relational-databases/tables/temporal-table-system-consistency-checks.md)
- [テンポラル テーブルでのパーティション分割](../../relational-databases/tables/partitioning-with-temporal-tables.md)
- [テンポラル テーブル セキュリティ](../../relational-databases/tables/temporal-table-security.md)
- [システム バージョン管理されたテンポラル テーブルの履歴データの保有期間管理](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)
- [メモリ最適化テーブルでのシステム バージョン管理されたテンポラル テーブル](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)
- [テンポラル テーブル メタデータのビューおよび関数](../../relational-databases/tables/temporal-table-metadata-views-and-functions.md)
