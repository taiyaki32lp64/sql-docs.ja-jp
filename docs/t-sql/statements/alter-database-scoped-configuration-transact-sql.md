---
title: ALTER DATABASE SCOPED CONFIGURATION
description: 複数のデータベース構成を個別データベース レベルで設定できます。
titleSuffix: SQL Server (Transact-SQL)
ms.custom: seo-lt-2019
ms.date: 10/31/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: conceptual
f1_keywords:
- ALTER_DATABASE_SCOPED_CONFIGURATION
- ALTER_DATABASE_SCOPED_CONFIGURATION_TSQL
- DATABASE_SCOPED_CONFIGURATION_TSQL
- SCOPED_CONFIGURATION_TSQL
- SCOPED_TSQL
- ALTER_DATABASE_SCOPED_TSQL
- DATABASE_SCOPED_TSQL
helpviewer_keywords:
- ALTER DATABASE SCOPED CONFIGURATION statement
- configuration [SQL Server], ALTER DATABASE SCOPED CONFIGURATION statement
ms.assetid: 63373c2f-9a0b-431b-b9d2-6fa35641571a
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 9547eaae31787dc01946b8dfd2d2d43781b5a8af
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75258131"
---
# <a name="alter-database-scoped-configuration-transact-sql"></a>ALTER DATABASE SCOPED CONFIGURATION (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

このステートメントでは、複数のデータベース構成を**個別データベース** レベルで設定できます。 このステートメントは、[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降の [!INCLUDE[sssdsfull](../../includes/sssdsfull-md.md)] と [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で利用できます。 次のような設定があります。

- プロシージャ キャッシュをクリアします。
- プライマリ データベースに対して、MAXDOP パラメーターを特定のデータベースに最適な内容に基づいて任意の値 (1、2、...) に設定し、(クエリ レポートなどに) 使用されるすべてのセカンダリ データベースに対して別の値 (0 など) を設定します。
- データベースに依存しないクエリ オプティマイザーのカーディナリティ推定モデルを互換性レベルに設定します。
- データベース レベルでパラメーター スニッフィングを有効または無効にします。
- データベース レベルでのクエリ最適化の修正プログラムを有効または無効にします。
- データベース レベルで ID キャッシュを有効または無効にします。
- バッチが初めてコンパイルされるとき、コンパイルしたプラン スタブのキャッシュ保存を有効または無効にします。
- ネイティブ コンパイル T-SQL モジュールの実行統計コレクションを有効または無効にします。
- `ONLINE =` 構文に対応している DDL ステートメントの既定のオプションでオンラインの有効/無効を変更します。
- `RESUMABLE =` 構文に対応している DDL ステートメントの既定のオプションで再開可能の有効/無効を変更します。
- [インテリジェントなクエリ処理](../../relational-databases/performance/intelligent-query-processing.md)の機能を有効または無効にします。
- 高速プラン強制を有効または無効にします。
- グローバル一時テーブルの自動削除機能を有効または無効にします。
- [軽量クエリ プロファイリング インフラストラクチャ](../../relational-databases/performance/query-profiling-infrastructure.md)を有効または無効にします。
- 新しい `String or binary data would be truncated` のエラー メッセージを有効または無効にします。
- [sys.dm_exec_query_plan_stats](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-stats-transact-sql.md) の最後の実際の実行プランのコレクションを有効または無効にします。
- 再開可能なインデックス操作を一時停止してから、SQL Server エンジンによって自動的に中止されるまでの一時停止される時間を分単位で指定します。

![リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "[リンク] アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

## <a name="syntax"></a>構文

```
ALTER DATABASE SCOPED CONFIGURATION
{
    { [ FOR SECONDARY] SET <set_options>}
}
| CLEAR PROCEDURE_CACHE [plan_handle]
| SET < set_options >
[;]

< set_options > ::=
{
    MAXDOP = { <value> | PRIMARY}
    | LEGACY_CARDINALITY_ESTIMATION = { ON | OFF | PRIMARY}
    | PARAMETER_SNIFFING = { ON | OFF | PRIMARY}
    | QUERY_OPTIMIZER_HOTFIXES = { ON | OFF | PRIMARY}
    | IDENTITY_CACHE = { ON | OFF }
    | INTERLEAVED_EXECUTION_TVF = { ON | OFF }
    | BATCH_MODE_MEMORY_GRANT_FEEDBACK = { ON | OFF }
    | BATCH_MODE_ADAPTIVE_JOINS = { ON | OFF }
    | TSQL_SCALAR_UDF_INLINING = { ON | OFF }
    | ELEVATE_ONLINE = { OFF | WHEN_SUPPORTED | FAIL_UNSUPPORTED }
    | ELEVATE_RESUMABLE = { OFF | WHEN_SUPPORTED | FAIL_UNSUPPORTED }
    | OPTIMIZE_FOR_AD_HOC_WORKLOADS = { ON | OFF }
    | XTP_PROCEDURE_EXECUTION_STATISTICS = { ON | OFF }
    | XTP_QUERY_EXECUTION_STATISTICS = { ON | OFF }
    | ROW_MODE_MEMORY_GRANT_FEEDBACK = { ON | OFF }
    | BATCH_MODE_ON_ROWSTORE = { ON | OFF }
    | DEFERRED_COMPILATION_TV = { ON | OFF }
    | ACCELERATED_PLAN_FORCING = { ON | OFF }
    | GLOBAL_TEMPORARY_TABLE_AUTODROP = { ON | OFF }
    | LIGHTWEIGHT_QUERY_PROFILING = { ON | OFF }
    | VERBOSE_TRUNCATION_WARNINGS = { ON | OFF }
    | LAST_QUERY_PLAN_STATS = { ON | OFF }
    | PAUSED_RESUMABLE_INDEX_ABORT_DURATION_MINUTES = <time>
}
```

> [!IMPORTANT]
> [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 以降。[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] では、一部のオプション名が変更されています。      
> -  `DISABLE_INTERLEAVED_EXECUTION_TVF` を `INTERLEAVED_EXECUTION_TVF` に変更しました
> -  `DISABLE_BATCH_MODE_MEMORY_GRANT_FEEDBACK` を `BATCH_MODE_MEMORY_GRANT_FEEDBACK` に変更しました
> -  `DISABLE_BATCH_MODE_ADAPTIVE_JOINS` を `BATCH_MODE_ADAPTIVE_JOINS` に変更しました

## <a name="arguments"></a>引数

セカンダリの場合

セカンダリ データベースの設定を指定します (すべてのセカンダリ データベースに同じ値を与える必要があります)。

CLEAR PROCEDURE_CACHE [plan_handle]

データベースのプロシージャ (プラン) キャッシュがクリアされ、プライマリとセカンダリの両方で実行することができます。

プラン キャッシュから 1 つのクエリ プランをクリアするクエリ プラン ハンドルを指定します。

**適用対象**:クエリ プラン ハンドルの指定は、Azure SQL Database と SQL Server 2019 以降で利用できます。

MAXDOP **=** {\<value> | PRIMARY } **\<value>**

ステートメントで使用される**並列処理の最大限度 (MAXDOP)** 設定の既定値を指定します。 0 が初期設定値であり、サーバー構成が代わりに使用されることを示します。 データベース スコープの MAXDOP は、サーバー レベルで設定されている**並列処理の最大限度**を p_configure によってオーバーライドします (0 に設定されていない限り)。 別の設定を必要とする特定のクエリを調整する目的で、クエリ ヒントでは引き続き、データベース スコープの MAXDOP をオーバーライドできます。 これらすべての設定の上限は、[ワークロード グループ](create-workload-group-transact-sql.md)に設定されている MAXDOP によって決定されます。

MAXDOP オプションを使用すると、並列プラン実行で使用するプロセッサの数を制限できます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、クエリ、インデックス データ定義言語 (DDL) の操作、並列挿入、オンライン列変更、並行統計コレクション、静的およびキーセット ドリブン カーソルの作成の場合に並列実行プランが検討されます。

> [!NOTE]
> **並列処理の最大限度 (MAXDOP)** の制限は[タスク](../../relational-databases/system-dynamic-management-views/sys-dm-os-tasks-transact-sql.md)ごとに設定されます。 この設定は、[要求](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)ごとまたはクエリ制限ごとではありません。 つまり、並列クエリ実行中に、1 つの要求で、[スケジューラ](../../relational-databases/system-dynamic-management-views/sys-dm-os-tasks-transact-sql.md)に割り当てられてた複数のタスクを生成することができます。 詳細については、「[スレッドおよびタスクのアーキテクチャ ガイド](../../relational-databases/thread-and-task-architecture-guide.md)」を参照してください。 

インスタンス レベルでこのオプションを設定する方法については、「[max degree of parallelism サーバー構成オプションの構成](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)」を参照してください。

> [!NOTE]
> [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] では、サーバーレベルの**並列処理の最大限度**構成は常に 0 に設定されます。 MAXDOP は、現在の記事で説明されているように、データベースごとに構成できます。 MAXDOP の最適な構成に関する推奨事項については、「[その他のリソース](#additional-resources)」を参照してください。

> [!TIP]
> これをクエリ レベルで行うには、**MAXDOP** [クエリ ヒント](../../t-sql/queries/hints-transact-sql-query.md)を使用します。    
> これをサーバー レベルで行うには、**並列処理の最大限度 (MAXDOP)** [サーバー構成オプション](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)を使用します。     
> これをワークロード レベルで行うには、**MAX_DOP** [Resource Governor ワークロード グループ構成オプション](../../t-sql/statements/create-workload-group-transact-sql.md)を使用します。    

PRIMARY

データベースがプライマリにあるとき、セカンダリに対してのみ設定できます。構成はプライマリに設定されている構成になることを示します。 プライマリの構成が変更されると、セカンダリの値も適宜変更されます。セカンダリの値を明示的に設定する必要はありません。 **PRIMARY** はセカンダリの初期設定です。

LEGACY_CARDINALITY_ESTIMATION **=** { ON | **OFF** | PRIMARY }

データベースの互換性レベルに関係なく、クエリ オプティマイザーのカーディナリティ推定モデルを SQL Server 2012 以前のバージョンに設定できます。 既定値は **OFF** であり、クエリ オプティマイザーのカーディナリティ推定モデルがデータベースの互換性レベルに基づいて設定されます。 LEGACY_CARDINALITY_ESTIMATION を **ON** に設定することは、[トレース フラグ 9481](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) を有効にすることと同じです。

> [!TIP]
> これをクエリ レベルで行うには、**QUERYTRACEON** [クエリ ヒント](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)を追加してください。
> [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 以降、クエリ レベルでこれを行うには、トレース フラグの代わりに、**USE HINT** [クエリ ヒント](../../t-sql/queries/hints-transact-sql-query.md#use_hint)を追加してください。

PRIMARY

データベースがプライマリにあるとき、この値はセカンダリでのみ有効になります。すべてのセカンダリのクエリ オプティマイザーのカーディナリティ推定モデル設定がプライマリに設定されている値になることを示します。 クエリ オプティマイザーのカーディナリティ推定モデルの構成がプライマリで変更された場合、セカンダリの値も適宜変更されます。 **PRIMARY** はセカンダリの初期設定です。

PARAMETER_SNIFFING **=** { **ON** | OFF | PRIMARY}

[パラメーター スニッフィング](../../relational-databases/query-processing-architecture-guide.md#ParamSniffing)を有効にするか無効にします。 既定値は ON です。 PARAMETER_SNIFFING を OFF に設定することは、[トレース フラグ 4136](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) を有効にすることと同じです。

> [!TIP]
> クエリ レベルでこれを行う方法については、「**OPTIMIZE FOR UNKNOWN** [クエリ ヒント](../../t-sql/queries/hints-transact-sql-query.md)」を参照してください。
> [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 以降、クエリ レベルでこれを行うには、**USE HINT** [クエリ ヒント](../../t-sql/queries/hints-transact-sql-query.md#use_hint)も利用できます。

PRIMARY

データベースがプライマリにあるとき、この値はセカンダリでのみ有効になります。すべてのセカンダリでこの設定の値がプライマリに設定されている値になることを示します。 [パラメーター スニッフィング](../../relational-databases/query-processing-architecture-guide.md#ParamSniffing)の使用に関するプライマリの構成が変更されると、セカンダリの値も適宜変更されます。セカンダリの値を明示的に設定する必要はありません。 PRIMARY はセカンダリの既定の設定です。

<a name="qo_hotfixes"></a> QUERY_OPTIMIZER_HOTFIXES **=** { ON | **OFF** | PRIMARY }

データベースの互換性レベルに関係なく、クエリ最適化修正プログラムを有効または無効にします。 既定値は **OFF** です。特定のバージョンで利用できる最高の互換性レベルが導入された後に公開されたクエリ最適化修正プログラムが無効になります (RTM 後)。 これを **ON** に設定することは、[トレース フラグ 4199](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) を有効にすることと同じです。

> [!TIP]
> これをクエリ レベルで行うには、**QUERYTRACEON** [クエリ ヒント](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)を追加してください。
> [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 以降、クエリ レベルでこれを行うには、トレース フラグの代わりに、USE HINT [クエリ ヒント](../../t-sql/queries/hints-transact-sql-query.md#use_hint)を追加してください。

PRIMARY

データベースがプライマリにあるとき、この値はセカンダリでのみ有効になります。すべてのセカンダリでこの設定の値がプライマリに設定されている値になることを示します。 プライマリの構成が変更されると、セカンダリの値も適宜変更されます。セカンダリの値を明示的に設定する必要はありません。 PRIMARY はセカンダリの既定の設定です。

IDENTITY_CACHE **=** { **ON** | OFF }

**適用対象**:[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (開始値 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]) および [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]

データベース レベルで ID キャッシュを有効または無効にします。 既定値は **ON** です。 ID キャッシュは、ID 列が含まれるテーブルでの INSERT パフォーマンスを改善するために使用されます。 サーバーが突然再起動したか、セカンダリ サーバーにフェールオーバーしたときに ID 列の値に隔たりができることを回避するには、IDENTITY_CACHE オプションを無効にします。 このオプションは、サーバー レベルのみならずデータベース レベルで設定可能という点を除き、既存の[トレース フラグ 272](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) と似ています。

> [!NOTE]
> このオプションはプライマリにのみ設定できます。 詳細については、「[ID 列](create-table-transact-sql-identity-property.md)」を参照してください。

INTERLEAVED_EXECUTION_TVF **=** { **ON** | OFF }

**適用対象**:[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (開始値 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]) および [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]

複数ステートメントのテーブル値関数のインターリーブ実行は、データベースの互換性レベル 140 以上を維持しながら、データベースまたはステートメント範囲で有効または無効にできます。 インターリーブ実行は、[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] のアダプティブ クエリ処理の一部の機能です。 詳細については、[インテリジェントなクエリ処理](../../relational-databases/performance/intelligent-query-processing.md)に関する記事をご覧ください。

> [!NOTE]
> データベース互換性レベルが 130 以下である場合は、このデータベース スコープの構成に影響がありません。
>
> SQL Server 2017 (14.x) のみでの、オプション INTERLEAVED_EXECUTION_TVF には **DISABLE**_INTERLEAVED_EXECUTION_TVF の古い名前があります。

BATCH_MODE_MEMORY_GRANT_FEEDBACK **=** { **ON** | OFF}

**適用対象**:[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (開始値 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]) および [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]

バッチ モード メモリ許可フィードバックは、データベースの互換性レベル 140 以上を維持しながら、データベース範囲で有効または無効にできます。 バッチ モード メモリ許可フィードバックは、[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] で導入された[インテリジェントなクエリ処理](../../relational-databases/performance/intelligent-query-processing.md)の一部の機能です。

> [!NOTE]
> データベース互換性レベルが 130 以下である場合は、このデータベース スコープの構成に影響がありません。

BATCH_MODE_ADAPTIVE_JOINS **=** { **ON** | OFF}

**適用対象**:[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (開始値 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]) および [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]

バッチ モードの適応結合は、データベースの互換性レベル 140 以上を維持しながら、データベース範囲で有効または無効にできます。 バッチ モードの適応結合は、[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] で導入された[インテリジェントなクエリ処理](../../relational-databases/performance/intelligent-query-processing.md)の一部の機能です。

> [!NOTE]
> データベース互換性レベルが 130 以下である場合は、このデータベース スコープの構成に影響がありません。

TSQL_SCALAR_UDF_INLINING **=** { **ON** | OFF }

**適用対象**:[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 以降) と [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] (機能はパブリック プレビュー段階)

データベースの互換性レベル 150 以上を維持しながら、データベース範囲で T-SQL スカラー UDF のインライン化を有効または無効にできます。 T-SQL スカラー UDF のインライン化は、[インテリジェント クエリの処理](../../relational-databases/performance/intelligent-query-processing.md)機能ファミリの一部です。

> [!NOTE]
> データベース互換性レベルが 140 以下である場合は、このデータベース スコープの構成に影響がありません。

ELEVATE_ONLINE = { OFF | WHEN_SUPPORTED | FAIL_UNSUPPORTED }

**適用対象**: [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)] (機能はパブリック プレビュー段階)

サポートされている操作からオンラインにエンジンを自動的に昇格させるオプションを選択できます。 既定は OFF であり、ステートメントで指定されない限り、操作はオンラインに昇格されません。 [sys.database_scoped_configurations](../../relational-databases/system-catalog-views/sys-database-scoped-configurations-transact-sql.md) は ELEVATE_ONLINE の現在の値を反映します。 これらのオプションは、オンラインでサポートされている操作にのみ適用されます。

FAIL_UNSUPPORTED

この値のとき、サポートされているすべての DDL 操作が ONLINE に昇格されます。 オンライン実行に対応していない操作は失敗し、警告が出ます。

WHEN_SUPPORTED

この値のとき、ONLINE 対応の操作が昇格されます。 オンライン対応ではない操作はオフラインで実行されます。

> [!NOTE]
> ONLINE オプションが指定されたステートメントを送信することで、既定の設定をオーバーライドできます。

ELEVATE_RESUMABLE= { OFF | WHEN_SUPPORTED | FAIL_UNSUPPORTED }

**適用対象**:[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 以降) と [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] (機能はパブリック プレビュー段階)

サポートされている操作から再開可能にエンジンを自動的に昇格させるオプションを選択できます。 既定は OFF であり、ステートメントで指定されない限り、操作は再開可能に昇格されません。 [sys.database_scoped_configurations](../../relational-databases/system-catalog-views/sys-database-scoped-configurations-transact-sql.md) は ELEVATE_RESUMABLE の現在の値を反映します。 これらのオプションは、再開可能実行でサポートされている操作にのみ適用されます。

FAIL_UNSUPPORTED

この値のとき、サポートされているすべての DDL 操作が RESUMABLE に昇格されます。 再開可能実行に対応していない操作は失敗し、警告が出ます。

WHEN_SUPPORTED

この値のとき、RESUMABLE 対応の操作が昇格されます。 再開可能対応ではない操作は再開不可能として実行されます。

> [!NOTE]
> RESUMABLE オプションが指定されたステートメントを送信することで、既定の設定をオーバーライドできます。

OPTIMIZE_FOR_AD_HOC_WORKLOADS **=** { ON | **OFF** }

**適用対象**: [!INCLUDE[sssdsfull](../../includes/sssdsfull-md.md)]

バッチが初めてコンパイルされるとき、コンパイルしたプラン スタブのキャッシュ保存を有効または無効にします。 既定値は OFF です。 あるデータベースに対してデータベース スコープ構成 OPTIMIZE_FOR_AD_HOC_WORKLOADS を有効にすると、バッチを初めてコンパイルしたとき、コンパイル済みのプラン スタブがキャッシュに保存されます。 プラン スタブのメモリ領域は、完全なコンパイル済みプランのサイズに比べて小さくなります。 バッチが再度コンパイルまたは実行されると、コンパイル済みプラン スタブは削除され、完全なコンパイル済みプランと置換されます。

XTP_PROCEDURE_EXECUTION_STATISTICS **=** { ON | **OFF** }

**適用対象**: [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]

現在のデータベース内のすべてのネイティブ コンパイル T-SQL モジュールに対し、モジュール レベルで実行統計コレクションを有効また無効にします。 既定値は OFF です。 実行統計は [sys.dm_exec_procedure_stats](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md) に反映されます。

このオプションが ON の場合、または統計コレクションが [sp_xtp_control_proc_exec_stats](../../relational-databases/system-stored-procedures/sys-sp-xtp-control-proc-exec-stats-transact-sql.md) によって有効化されている場合は、ネイティブ コンパイル T-SQL モジュールのモジュール レベルの実行統計が収集されます。

XTP_QUERY_EXECUTION_STATISTICS **=** { ON | **OFF** }

**適用対象**: [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]

現在のデータベース内のすべてのネイティブ コンパイル T-SQL モジュールに対し、ステートメント レベルで実行統計コレクションを有効また無効にします。 既定値は OFF です。 実行統計は、[sys.dm_exec_query_stats](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md) および[クエリ ストア](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)に反映されます。

このオプションが ON の場合、または統計コレクションが [sp_xtp_control_query_exec_stats](../../relational-databases/system-stored-procedures/sys-sp-xtp-control-query-exec-stats-transact-sql.md) によって有効化されている場合は、ネイティブ コンパイル T-SQL モジュールのステートメント レベルの実行統計が収集されます。

ネイティブ コンパイル [!INCLUDE[tsql](../../includes/tsql-md.md)] モジュールのパフォーマンスの監視の詳細については、「[ネイティブ コンパイル ストアド プロシージャのパフォーマンスの監視](../../relational-databases/in-memory-oltp/monitoring-performance-of-natively-compiled-stored-procedures.md)」を参照してください。

ROW_MODE_MEMORY_GRANT_FEEDBACK **=** { **ON** | OFF}

**適用対象**:[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 以降) と [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] (機能はパブリック プレビュー段階)

行モード メモリ許可フィードバックは、データベースの互換性レベル 150 以上を維持しながら、データベース範囲で有効または無効にできます。 行モード メモリ許可フィードバックは、[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] で導入された[インテリジェントなクエリ処理](../../relational-databases/performance/intelligent-query-processing.md)の一部の機能です (行モードは [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] と [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] でサポートされています)。

> [!NOTE]
> データベース互換性レベルが 140 以下である場合は、このデータベース スコープの構成に影響がありません。

BATCH_MODE_ON_ROWSTORE **=** { **ON** | OFF}

**適用対象**:[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 以降) と [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] (機能はパブリック プレビュー段階)

行ストアのバッチ モードは、データベースの互換性レベル 150 以上を維持しながら、データベース範囲で有効または無効にできます。 行ストアのバッチ モードは、[インテリジェント クエリの処理](../../relational-databases/performance/intelligent-query-processing.md)機能ファミリの一部の機能です。

> [!NOTE]
> データベース互換性レベルが 140 以下である場合は、このデータベース スコープの構成に影響がありません。

DEFERRED_COMPILATION_TV **=** { **ON** | OFF}

**適用対象**:[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 以降) と [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] (機能はパブリック プレビュー段階)

テーブル変数の遅延コンパイルは、データベースの互換性レベル 150 以上を維持しながら、データベース範囲で有効または無効にできます。 テーブル変数の遅延コンパイルは、[インテリジェント クエリの処理](../../relational-databases/performance/intelligent-query-processing.md)機能ファミリの一部の機能です。

> [!NOTE]
> データベース互換性レベルが 140 以下である場合は、このデータベース スコープの構成に影響がありません。

ACCELERATED_PLAN_FORCING **=** { **ON** | OFF }

**適用対象**:[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 以降)

[クエリ ストアのプラン強制](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md#Regressed)、[自動チューニング](../../relational-databases/automatic-tuning/automatic-tuning.md#automatic-plan-correction)、[USE PLAN](../../t-sql/queries/hints-transact-sql-query.md#use-plan) クエリ ヒントなど、あらゆる形式のプラン強制に適用される、クエリ プラン強制のために最適化されたメカニズムを有効にします。 既定値は ON です。

> [!NOTE]
> 高速プラン強制を無効にしないことをお勧めします。

GLOBAL_TEMPORARY_TABLE_AUTODROP **=** { **ON** | OFF }

**適用対象**: [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)] (機能はパブリック プレビュー段階)

[グローバル一時テーブル](../../t-sql/statements/create-table-transact-sql.md#temporary-tables)の自動削除機能を設定できます。 既定値は ON で、グローバル一時テーブルはどのセッションでも使用中でないときに自動的に削除されることを意味します。 OFF に設定すると、グローバル一時テーブルは、DROP TABLE ステートメントを使用して明示的に削除する必要があります。または、サーバーの再起動時に自動的に削除されます。

- [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 単一データベースおよびエラスティック プールでは、このオプションを SQL Database サーバーの個々のユーザー データベース内で設定できます。
- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] および [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] マネージド インスタンス上では、このオプションは `TempDB` 内で設定され、個々のユーザー データベースの設定に影響を与えません。

<a name="lqp"></a>

LIGHTWEIGHT_QUERY_PROFILING **=** { **ON** | OFF}

**適用対象**:[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (開始値 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]) および [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]

[軽量クエリ プロファイリング インフラストラクチャ](../../relational-databases/performance/query-profiling-infrastructure.md)を有効または無効にできます。 軽量クエリ プロファイリング インフラストラクチャ (LWP) は、標準のプロファイリング メカニズムよりも効率的にクエリのパフォーマンス データを提供するもので、既定で有効になっています。

<a name="verbose-truncation"></a>

VERBOSE_TRUNCATION_WARNINGS **=** { **ON** | OFF}

**適用対象**:[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (開始値 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]) および [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]

新しい `String or binary data would be truncated` のエラー メッセージの有効と無効が切り替えられるようになります。 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] では、次のシナリオに対してより具体的な新しいエラー メッセージ (2628) が導入されています。

`String or binary data would be truncated in table '%.*ls', column '%.*ls'. Truncated value: '%.*ls'.`

データベース互換性レベルが 150 の状態で ON に設定すると、切り捨てエラーにより、詳しいコンテキストを提供し、トラブルシューティングのプロセスを簡略化する新しいエラー メッセージ 2628 が発生します。

データベース互換性レベルが 150 の状態で OFF に設定すると、切り捨てエラーにより前のエラー メッセージ 8152 が発生します。

データベース互換性レベルが 140 以下の場合、エラー メッセージ 2628 はオプトインのエラー メッセージとして残ります。このエラー メッセージでは[トレース フラグ](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 460 を有効にする必要があり、このデータベース スコープ構成に影響がありません。

LAST_QUERY_PLAN_STATS **=** { ON | **OFF**}

**適用対象**:[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 以降) (機能はパブリック プレビュー段階)

[sys.dm_exec_query_plan_stats](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-stats-transact-sql.md) の最後の実際の実行プラン (実際の実行プランに相当) のコレクションを有効または無効にすることができます。

PAUSED_RESUMABLE_INDEX_ABORT_DURATION_MINUTES

**適用対象**:Azure SQL Database のみ

`PAUSED_RESUMABLE_INDEX_ABORT_DURATION_MINUTES` オプションでは、エンジンによって自動的に中止される前に、再開可能なインデックスが一時停止される期間 (分単位) を決定します。

- 既定値は、1 日 (1440 分) に設定されています。
- 最小期間は 1 分に設定されています。
- 最大期間は 71582 分です。
- 0 に設定すると、一時停止された操作が自動的に中止されることはありません

このオプションの現在の値は、[sys.database_scoped_configurations](../../relational-databases/system-catalog-views/sys-database-scoped-configurations-transact-sql.md) に表示されます。

## <a name="Permissions"></a> Permissions

データベースに対する `ALTER ANY DATABASE SCOPE CONFIGURATION` が必要です。 この権限は、データベース上で CONTROL 権限を持つユーザーが付与できます。

## <a name="general-remarks"></a>全般的な解説

セカンダリ データベースにはプライマリとは異なるスコープ構成を設定できますが、すべてのセカンダリ データベースで同じ構成が使用されます。 個々のセカンダリに異なる設定を構成することはできません。

このステートメントを実行すると、現在のデータベースのプロシージャ キャッシュが消去されます。つまり、すべてのクエリを再コンパイルする必要があります。

3 部構成の名前のクエリの場合、現在のデータベース コンテキストでコンパイルされる SQL モジュール (プロシージャ、関数、トリガーなど) ではなく、クエリに対する現在のデータベース接続の設定が適用されます。そのため、そのような設定が置かれているデータベースのオプションが使用されます。

`ALTER_DATABASE_SCOPED_CONFIGURATION` イベントは、DDL トリガーの始動に使用できる DDL イベントとして追加されます。`ALTER_DATABASE_EVENTS` トリガー グループの子です。

データベース スコープ構成設定がデータベースに継承されるので、特定のデータベースが復元またはアタッチされたときに、既存の構成設定が残ります。

[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 以降。[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] では、一部のオプション名が変更されています。      
-  `DISABLE_INTERLEAVED_EXECUTION_TVF` を `INTERLEAVED_EXECUTION_TVF` に変更しました
-  `DISABLE_BATCH_MODE_MEMORY_GRANT_FEEDBACK` を `BATCH_MODE_MEMORY_GRANT_FEEDBACK` に変更しました
-  `DISABLE_BATCH_MODE_ADAPTIVE_JOINS` を `BATCH_MODE_ADAPTIVE_JOINS` に変更しました

## <a name="limitations-and-restrictions"></a>制限事項と制約事項

### <a name="maxdop"></a>MAXDOP

詳細設定はグローバル設定をオーバーライドします。その Resource Governor が他のすべての MAXDOP 設定の上限となります。 MAXDOP 設定のロジックは次のようになります。

- クエリ ヒントは `sp_configure` とデータベース スコープ構成の両方をオーバーライドします。 ワークロード グループにリソース グループ MAXDOP が設定されている場合:

  - クエリ ヒントが 0 に設定されている場合、Resource Governor 設定でオーバーライドされます。

  - クエリ ヒントが 0 ではない場合、Resource Governor 設定が上限となります。

- データベース スコープ構成 (0 ではない限り) は、クエリ ヒントがある場合を除き、`sp_configure` 設定をオーバーライドし、Resource Governor 設定が上限となります。

- `sp_configure` 設定は、Resource Governor 設定でオーバーライドされます。

### <a name="query_optimizer_hotfixes"></a>QUERY_OPTIMIZER_HOTFIXES

`QUERYTRACEON` ヒントを使用して SQL Server 7.0 から [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] バージョンの既定のクエリ オプティマイザーまたはクエリ オプティマイザー修正プログラムを有効にするとき、クエリ ヒントとデータベース スコープ構成設定の OR 条件になります。つまり、いずれかが有効になっている場合、データベース スコープ構成が適用されます。

### <a name="geo-dr"></a>Geo DR

読み取り可能なセカンダリ データベース (Always On 可用性グループや [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] の geo レプリケートされたデータベース) では、データベースの状態を確認することでセカンダリ値が使用されます。 フェールオーバーで再コンパイルが行われず、技術的に、セカンダリ設定を使用しているクエリが新しいプライマリに与えられる場合でも、プライマリとセカンダリの間の設定はワークロードが異なるときにのみ変わるというのがその考えです。そのため、キャッシュされたクエリでは最適設定が使用されるが、新しいクエリはそれに適した新しい設定を選択します。

### <a name="dacfx"></a>DacFx

`ALTER DATABASE SCOPED CONFIGURATION` は [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] と [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降) の新しい機能であり、データベース スキーマに影響を与えます。スキーマのエクスポートは (データがあってもなくても)、[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] や [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] など、以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] にはインポートできません。 たとえば、[!INCLUDE[ssSDS](../../includes/sssds-md.md)] または [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] データベースから [DACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_3) または [BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4) にエクスポートしたものは、下位レベルのサーバーにインポートできません。

### <a name="elevate_online"></a>ELEVATE_ONLINE

このオプションは、`WITH (ONLINE = <syntax>)` 対応の DDL ステートメントにのみ適用されます。 XML インデックスは影響を受けません。

### <a name="elevate_resumable"></a>ELEVATE_RESUMABLE

このオプションは、`WITH (RESUMABLE = <syntax>)` 対応の DDL ステートメントにのみ適用されます。 XML インデックスは影響を受けません。

## <a name="metadata"></a>メタデータ

[sys.database_scoped_configurations &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-scoped-configurations-transact-sql.md) システム ビューには、データベース内のスコープ構成に関する情報が表示されます。 データベース スコープ構成オプションはサーバー全体の初期設定にオーバーライドするため、sys.database_scoped_configurations にのみ表示されます。 [sys.configurations &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md) システム ビューは、サーバー全体の設定にのみ表示されます。

## <a name="examples"></a>例

以下は ALTER DATABASE SCOPED CONFIGURATION の使用例です

### <a name="a-grant-permission"></a>A. アクセス許可の付与

この例では、ALTER DATABASE SCOPED CONFIGURATION の実行に必要な権限をユーザー Joe に与えています。

```sql
GRANT ALTER ANY DATABASE SCOPED CONFIGURATION to [Joe] ;
```

### <a name="b-set-maxdop"></a>B. MAXDOP の設定

この例では、geo レプリケーション シナリオでプライマリ データベースに MAXDOP = 1 を、セカンダリ データベースに MAXDOP = 4 を設定します。

```sql
ALTER DATABASE SCOPED CONFIGURATION SET MAXDOP = 1 ;
ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET MAXDOP = 4 ;
```

この例では、geo レプリケーション シナリオで、セカンダリ データベースの MAXDOP をそのプライマリ データベースと同じ値に設定します。

```sql
ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET MAXDOP = PRIMARY ;
```

### <a name="c-set-legacy_cardinality_estimation"></a>C. LEGACY_CARDINALITY_ESTIMATION の設定

この例では、geo レプリケーション シナリオで、セカンダリ データベースの LEGACY_CARDINALITY_ESTIMATION を ON に設定します。

```sql
ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET LEGACY_CARDINALITY_ESTIMATION = ON ;
```

この例では、geo レプリケーション シナリオで、セカンダリ データベースの LEGACY_CARDINALITY_ESTIMATION をそのプライマリ データベースと同じ値に設定します。

```sql
ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET LEGACY_CARDINALITY_ESTIMATION = PRIMARY ;
```

### <a name="d-set-parameter_sniffing"></a>D. PARAMETER_SNIFFING の設定

この例では、geo レプリケーション シナリオで、プライマリ データベースの PARAMETER_SNIFFING を OFF に設定します。

```sql
ALTER DATABASE SCOPED CONFIGURATION SET PARAMETER_SNIFFING = OFF ;
```

この例では、geo レプリケーション シナリオで、セカンダリ データベースの PARAMETER_SNIFFING を OFF に設定します。

```sql
ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET PARAMETER_SNIFFING = OFF ;
```

この例では、geo レプリケーション シナリオで、セカンダリ データベースの PARAMETER_SNIFFING をプライマリ データベースと同じ値に設定します。

```sql
ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET PARAMETER_SNIFFING = PRIMARY ;
```

### <a name="e-set-query_optimizer_hotfixes"></a>E. QUERY_OPTIMIZER_HOTFIXES の設定

geo レプリケーション シナリオで、プライマリ データベースの QUERY_OPTIMIZER_HOTFIXES を ON に設定します。

```sql
ALTER DATABASE SCOPED CONFIGURATION SET QUERY_OPTIMIZER_HOTFIXES = ON ;
```

### <a name="f-clear-procedure-cache"></a>F. プロシージャ キャッシュの消去

この例では、プロシージャ キャッシュを消去します (プライマリ データベースのみ可能)。

```sql
ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE;
```

### <a name="g-set-identity_cache"></a>G. IDENTITY_CACHE の設定

**適用対象**:[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] 以降) と [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] (機能はパブリック プレビュー段階)

この例では、ID キャッシュを無効にします。

```sql
ALTER DATABASE SCOPED CONFIGURATION SET IDENTITY_CACHE = OFF ;
```

### <a name="h-set-optimize_for_ad_hoc_workloads"></a>H. OPTIMIZE_FOR_AD_HOC_WORKLOADS の設定

**適用対象**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]

この例では、バッチが初めてコンパイルされるとき、コンパイルしたプラン スタブのキャッシュ保存を有効にします。

```sql
ALTER DATABASE SCOPED CONFIGURATION SET OPTIMIZE_FOR_AD_HOC_WORKLOADS = ON;
```

### <a name="i-set-elevate_online"></a>I. ELEVATE_ONLINE を設定する

**適用対象**: [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)] (機能はパブリック プレビュー段階)

この例では、ELEVATE_ONLINE が FAIL_UNSUPPORTED に設定されます。

```sql
ALTER DATABASE SCOPED CONFIGURATION SET ELEVATE_ONLINE = FAIL_UNSUPPORTED ;
```

### <a name="j-set-elevate_resumable"></a>J. ELEVATE_RESUMABLE を設定する

**適用対象**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] と [!INCLUDE[ssNoVersion](../../includes/sssqlv15-md.md)] (機能はパブリック プレビュー段階)

この例では、ELEVATE_RESUMABLE が WHEN_SUPPORTED に設定されます。

```sql
ALTER DATABASE SCOPED CONFIGURATION SET ELEVATE_RESUMABLE = WHEN_SUPPORTED ;
```

### <a name="k-clear-a-query-plan-from-the-plan-cache"></a>K. プラン キャッシュからクエリ プランを削除する

**適用対象**:[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (開始値 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]) および [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]

この例では、プロシージャ キャッシュから特定のプランを削除します。

```sql
ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE 0x06000500F443610F003B7CD12C02000001000000000000000000000000000000000000000000000000000000;
```

### <a name="l-set-paused-duration"></a>L. 一時停止される期間を設定する

**適用対象**:Azure SQL Database のみ

この例では、再開可能なインデックスの一時停止される期間を 60 分に設定します。

```sql
ALTER DATABASE SCOPED CONFIGURATION
SET PAUSED_RESUMABLE_INDEX_ABORT_DURATION_MINUTES = 60
```

## <a name="additional-resources"></a>その他のリソース

### <a name="maxdop-resources"></a>MAXDOP リソース

- [並列処理の次数](../../relational-databases/query-processing-architecture-guide.md#DOP)
- [SQL Server の "max degree of parallelism" 構成オプションの推奨事項とガイドライン](https://support.microsoft.com/kb/2806535)

### <a name="legacy_cardinality_estimation-resources"></a>LEGACY_CARDINALITY_ESTIMATION リソース

- [カーディナリティ推定 (SQL Server)](../../relational-databases/performance/cardinality-estimation-sql-server.md)
- [SQL Server 2014 のカーディナリティ推定機能によるクエリプランの最適化](https://msdn.microsoft.com/library/dn673537.aspx)

### <a name="parameter_sniffing-resources"></a>PARAMETER_SNIFFING リソース

- [パラメーター スニッフィング](../../relational-databases/query-processing-architecture-guide.md#ParamSniffing)
- ["I smell a parameter!"](https://blogs.msdn.microsoft.com/queryoptteam/2006/03/31/i-smell-a-parameter/) (パラメーターのにおいがする!)

### <a name="query_optimizer_hotfixes-resources"></a>QUERY_OPTIMIZER_HOTFIXES リソース

- [トレース フラグ](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)
- [SQL Server クエリ オプティマイザー修正プログラム トレース フラグ 4199 サービス モデル](https://support.microsoft.com/kb/974006)

### <a name="elevate_online-resources"></a>ELEVATE_ONLINE リソース

[オンライン インデックス操作のガイドライン](../../relational-databases/indexes/guidelines-for-online-index-operations.md)

### <a name="elevate_resumable-resources"></a>ELEVATE_RESUMABLE リソース

[オンライン インデックス操作のガイドライン](../../relational-databases/indexes/guidelines-for-online-index-operations.md)

## <a name="more-information"></a>詳細情報   
 [sys.database_scoped_configurations](../../relational-databases/system-catalog-views/sys-database-scoped-configurations-transact-sql.md)      
 [SQL Server の "並列処理の最大限度" 構成オプションの推奨事項とガイドライン](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md#Guidelines)      
 [sys.configurations](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)    
 [データベースとファイルのカタログ ビュー](../../relational-databases/system-catalog-views/databases-and-files-catalog-views-transact-sql.md)    
 [サーバー構成オプション](../../database-engine/configure-windows/server-configuration-options-sql-server.md)    
 [オンライン インデックス操作の動作原理](../../relational-databases/indexes/how-online-index-operations-work.md)    
 [オンラインでのインデックス操作の実行](../../relational-databases/indexes/perform-index-operations-online.md)    
 [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)    
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)    
