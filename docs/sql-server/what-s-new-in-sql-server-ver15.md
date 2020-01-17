---
title: SQL Server 2019 の新機能 | Microsoft Docs
ms.date: 11/04/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: release-landing
ms.topic: article
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 3aa251e7d31f21cf51f4f528b1f0ccd35c0afb2c
ms.sourcegitcommit: f688a37bb6deac2e5b7730344165bbe2c57f9b9c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/08/2019
ms.locfileid: "73844563"
---
# <a name="whats-new-in-includesql-server-2019includessssqlv15-mdmd"></a>[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] の新機能

[!INCLUDE[tsql-appliesto-ss-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss-xxxx-xxxx-xxx-md.md)]

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] は以前のリリースに基づいて構築され、開発言語、データ型、オンプレミスまたはクラウド環境、オペレーティング システムを選択できるプラットフォームとしての SQL Server がいっそう成長しています。

この記事では、[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] の新機能と拡張機能について要約します。

詳細および既知の問題については、「[[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] リリース ノート](sql-server-version-15-release-notes.md)」を参照してください。

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] で最良のエクスペリエンスを得るには、[最新のツール](https://aka.ms/getazuredatastudio)を使用してください。

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] では、[!INCLUDE[sql-server](../includes/ssnoversion-md.md)] 用の [!INCLUDE[big-data-clusters](../includes/ssbigdataclusters-nover.md)] が導入されています。 また、SQL Server データベース エンジン、SQL Server Analysis Services、SQL Server Machine Learning Services、SQL Server on Linux、SQL Server マスター データ サービスに対する追加機能と機能強化も提供されています。

以下のセクションでは、これらの機能の概要について説明します。

## <a name="data-virtualization-and-includebig-data-clusters-2019includesssbigdataclusters-ver15md"></a>データの仮想化と [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]

現代の企業はしばしば、データという財産を大量に管理しています。その財産はさまざまなデータ セットからなりますが、サイロ化されたデータ ソースでホストされるデータ セットは会社全体で増加の一途をたどります。 SQL Server 2019 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] を利用すると、機械学習機能や AI 機能など、大量のデータ セットを処理できる環境を実現し、あらゆるデータから分析情報をほぼリアルタイムで取得できます。

| 新機能または更新 | 詳細 |
|:---|:---|
| スケーラブルなビッグ データ ソリューション | Kubernetes で実行している SQL Server、Spark、HDFS コンテナーの[スケーラブルなクラスターを配置します](../big-data-cluster/deploy-get-started.md)。 <br/><br/> Transact-SQL または Spark からビッグ データの読み取り、書き込み、処理を行います。<br/><br/> 大量のビッグ データを使用して、価値の高いリレーショナル データを簡単に組み合わせて分析します。<br/><br/>外部データ ソースを照会します。<br/><br/>SQL Server によって管理される HDFS にビッグ データを格納します。<br/><br/>クラスターを介して複数の外部データ ソースからデータを照会します。<br/><br/> AI、機械学習、その他の分析タスクにデータを使用します。<br/><br/> [!INCLUDE[big-data-clusters](../includes/ssbigdataclusters-nover.md)] に[アプリケーションをデプロイして実行します](../big-data-cluster/concept-application-deployment.md)。 <br/><br/> SQL Server マスター インスタンスは、Always On 可用性グループ テクノロジを利用した、あらゆるデータベースを対象とする高可用性とディザスター リカバリーを備えています。<br/>|
|PolyBase によるデータ仮想化 | 外部の SQL Server、Oracle、Teradata、MongoDB、ODBC データ ソースと外部のテーブルのデータのクエリを実行します。現在、[UTF-8 エンコード対応](../relational-databases/collations/collation-and-unicode-support.md)になりました。 詳細については、「[PolyBase とは](../relational-databases/polybase/polybase-guide.md)」を参照してください。|
| &nbsp; | &nbsp; |

詳細については、「[SQL Server [!INCLUDE[big-data-clusters](../includes/ssbigdataclusters-nover.md)]とは](../big-data-cluster/big-data-cluster-overview.md)」を参照してください。

## <a name="intelligent-database"></a>インテリジェント データベース
[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] は、以前のバージョンのイノベーションに基づいており、既定の設定で業界をリードするパフォーマンスを実現できます。 [インテリジェントなクエリ処理](../relational-databases/performance/intelligent-query-processing.md)から永続メモリ デバイスのサポートまで、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のインテリジェント データベース機能を利用することで、アプリケーションやデータベースの設計を変更することなく、すべてのデータベース ワークロードのパフォーマンスとスケーラビリティが向上します。

### <a name="intelligent-query-processing"></a>インテリジェントなクエリ処理
[インテリジェントなクエリ処理](../relational-databases/performance/intelligent-query-processing.md)を使用すると、大規模な処理時に重要な並列ワークロードが改善されることがわかります。 同時に、絶えず変化するデータの世界に常に対応することができます。 インテリジェントなクエリ処理は、最新の[データベース互換性レベル](../t-sql/statements/alter-database-transact-sql-compatibility-level.md#differences-between-compatibility-level-140-and-level-150)設定に基づいて既定で使用できます。また、最小限の実装作業で既存のワークロードのパフォーマンスが向上する幅広い影響をもたらします。

|新機能または更新 | 詳細 |
|:---|:---|
|行モード メモリ許可フィードバック |バッチ モードと行モード両方の演算子のメモリ許可サイズを調整することで、バッチ モード メモリ許可フィードバックの機能が拡張されます。 この調整により、メモリが無駄になり、同時実行性が低下する原因となる過剰な許可が自動的に修正されます。 また、メモリ許可が不十分なためにディスクへの負荷が高くなる問題も修正できます。 「[行モード メモリ許可フィードバック](../relational-databases/performance/intelligent-query-processing.md#row-mode-memory-grant-feedback)」を参照してください。 |
|行ストアでのバッチ モード | 列ストア インデックスを使用せずにバッチ モードを実行できます。 バッチ モードの実行では、分析ワークロードの間の CPU 使用効率が向上しますが、[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] までは、クエリに列ストア インデックスを使用する操作が含まれている場合にのみ使用されました。 ただし、一部のアプリケーションでは、列ストア インデックスでサポートされていない機能が使用されている可能性があるため、バッチ モードを利用できませんでした。 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 以降では、任意の種類のインデックス (行ストアまたは列ストア) を使用する操作がクエリに含まれる適格な分析ワークロードで、バッチ モードが有効になります。 「[行ストアでのバッチ モード](../relational-databases/performance/intelligent-query-processing.md#batch-mode-on-rowstore)」を参照してください。 |
|スカラー UDF のインライン化|スカラー UDF が関係式に自動的に変換され、それらが呼び出し元の SQL クエリに埋め込まれます。 この変換により、スカラー UDF を利用するワークロードのパフォーマンスが向上します。 [スカラー UDF のインライン化](../relational-databases/performance/intelligent-query-processing.md#scalar-udf-inlining)に関するページを参照してください。|
|テーブル変数の遅延コンパイル|テーブル変数を参照するクエリのプランの品質および全体的なパフォーマンスが向上します。 最適化と最初のコンパイルの実行中に、この機能は実際テーブル変数の行数に基づくカーディナリティの推定を反映します。 この正確な行数の情報によって、ダウンストリーム プラン操作が最適化されます。 「[テーブル変数の遅延コンパイル](../relational-databases/performance/intelligent-query-processing.md#table-variable-deferred-compilation)」を参照してください。 |
|`APPROX_COUNT_DISTINCT` による概数クエリ処理 |絶対精度は重要でないが応答性は重要であるシナリオでは、優れたコンカレンシーのための `COUNT(DISTINCT())` よりリソース使用量が少ない `APPROX_COUNT_DISTINCT` で大規模なデータセットを集計します。 「[概数クエリ処理](../relational-databases/performance/intelligent-query-processing.md#approximate-query-processing)」を参照してください。|
| &nbsp; | &nbsp; |


### <a name="in-memory-database"></a>メモリ内データベース
[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の[メモリ内データベース](../relational-databases/in-memory-database.md) テクノロジでは、最新のハードウェア イノベーションを活用して、高度なパフォーマンスとスケールを実現しています。 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] は、メモリ内オンライン トランザクション処理 (OLTP) など、この分野の先行するイノベーションに基づいており、すべてのデータベース ワークロードにわたって新しいレベルのスケーラビリティを実現します。  

|新機能または更新 | 詳細 |
|:---|:---|
|ハイブリッド バッファー プール| 永続的なメモリ (PMEM) デバイス上に置かれたデータベース ファイル上のデータベース ページが必要に応じて直接アクセスされる [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] の新機能。 「[ハイブリッド バッファー プール](../database-engine/configure-windows/hybrid-buffer-pool.md)」を参照してください。|
|メモリ最適化 TempDB メタデータ| [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] では、[メモリ内データベース](../relational-databases/in-memory-database.md)機能ファミリの一部として、メモリ最適化 TempDB メタデータという新機能が導入されています。この機能により、効果的にこのボトルネックが除去され、TempDB が多用されるワークロードに対して新たなレベルのスケーラビリティが実現されます。 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] では、一時テーブルのメタデータの管理に関連するシステム テーブルを、ラッチ フリーの非持続的メモリ最適化テーブルに移動できます。 「[メモリ最適化 TempDB メタデータ](../relational-databases/databases/tempdb-database.md#memory-optimized-tempdb-metadata)」をご覧ください。|
| データベース スナップショットのためのメモリ内 OLTP サポート | [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] では、メモリ最適化されたファイルグループが含まれるデータベースの[データベース スナップショット](../relational-databases/databases/database-snapshots-sql-server.md)を作成するためのサポートが導入されました。 |
| &nbsp; | &nbsp; |

### <a name="intelligent-performance"></a>インテリジェントなパフォーマンス
[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] は以前のリリースのインテリジェント データベースのイノベーションに基づいて構築されており、[さらに高速な実行](https://blogs.msdn.microsoft.com/bobsql/tag/it-just-runs-faster/)が保証されています。 こうした機能強化により、既知のリソースのボトルネックを克服できます。また、すべてのワークロードにわたって予測可能なパフォーマンスを実現するようにデータベース サーバーを構成するオプションが用意されています。

|新機能または更新 | 詳細 |
|:---|:---|
|`OPTIMIZE_FOR_SEQUENTIAL_KEY`|インデックスへの高コンカレンシーの挿入のスループット向上に役立つ、[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 内での最適化を有効にします。 このオプションは、最終ページ挿入の競合が起きやすいインデックスを対象としています。これは、一般に、ID 列、シーケンス、または日付/時刻列などの連続したキーを持つインデックスでよく見られます。 「[CREATE INDEX](../t-sql/statements/create-index-transact-sql.md#sequential-keys)」を参照してください。|
|高速順方向カーソルと静的カーソルを強制する | 高速順方向カーソルと静的カーソルのサポートを強制するクエリ ストア プランが用意されています。 [高速順方向カーソルと静的カーソルのサポートを強制するプラン](../relational-databases/performance/monitoring-performance-by-using-the-query-store.md#ctp23)に関するページを参照してください。|
|リソース管理| `CREATE WORKLOAD GROUP` と `ALTER WORKLOAD GROUP` の `REQUEST_MAX_MEMORY_GRANT_PERCENT` オプションの構成可能値が整数から float データ型に変更されており、メモリ上限をさらに細かく制御できます。 「[ALTER WORKLOAD GROUP](../t-sql/statements/alter-workload-group-transact-sql.md)」と「[CREATE WORKLOAD GROUP](../t-sql/statements/create-workload-group-transact-sql.md)」を参照してください。|
|ワークロードの再コンパイルの削減| 不要な再コンパイルを減らすことにより、複数のスコープで一時テーブルを使用する場合のパフォーマンスが向上します。 [ワークロードの再コンパイルの削減](../relational-databases/tables/tables.md#ctp23)に関するページを参照してください。 |
|間接チェックポイントのスケーラビリティ |[間接チェックポイントのスケーラビリティの向上](../relational-databases/logs/database-checkpoints-sql-server.md#ctp23)に関するページを参照してください。|
|PFS の同時更新|[Page Free Space (PFS) ページ](https://techcommunity.microsoft.com/t5/SQL-Server/Under-the-covers-GAM-SGAM-and-PFS-pages/ba-p/383125)はデータベース ファイル内の特別なページであり、オブジェクト用の領域を割り当てるときに空き領域を探すために SQL Server によって使用されます。 PFS ページでのページ ラッチの競合は、一般に [TempDB](https://support.microsoft.com/en-us/help/2154845/recommendations-to-reduce-allocation-contention-in-sql-server-tempdb-d) に関連していますが、多数の同時オブジェクト割り当てスレッドがあるときは、ユーザー データベースでも発生する可能性があります。 この機能強化により、PFS の更新でのコンカレンシー管理方法が変更され、排他的ラッチではなく共有ラッチで更新できるようになります。 この動作は、[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 以降のすべてのデータベース (TempDB など) で、既定でオンになります。|
|Scheduler worker の移行 |worker の移行ではアイドル状態のスケジューラを利用し、同じ NUMA ノード上の別のスケジューラの実行可能キューから worker を移行し、移行された worker のタスクをすぐに再開できます。 この機能強化により、実行時間が長いタスクが偶然同じスケジューラに割り当てられる状況で、よりバランスのとれた CPU 使用率を実現できるようになります。 詳細については、「[SQL Server 2019 のインテリジェント パフォーマンス - worker の移行](https://techcommunity.microsoft.com/t5/SQL-Server/SQL-Server-2019-Intelligent-Performance-Worker-Migration/ba-p/939610)」を参照してください。 |
| &nbsp; | &nbsp; |

### <a name="monitoring"></a>監視
監視機能が強化され、必要なときにデータベースのワークロードに関するパフォーマンスの分析情報が得られるようになりました。

|新機能または更新 | 詳細 |
|:---|:---|
|`WAIT_ON_SYNC_STATISTICS_REFRESH` | `sys.dm_os_wait_stats` 動的管理ビューの新しい待機の種類。 これには、統計更新の同期操作に費やされたインスタンス レベルの累積時間が表示されます。 [`sys.dm_os_wait_stats`](../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)に関するページを参照してください。|
|クエリ ストア用のカスタム キャプチャ ポリシー | このポリシーを有効にすると、新しいクエリ ストア キャプチャ ポリシーの設定で追加のクエリ ストア構成を使用して、特定のサーバーでのデータ収集を微調整することができます。 「[ALTER DATABASE の SET オプション](../t-sql/statements/alter-database-transact-sql-set-options.md)」を参照してください。|
|`LIGHTWEIGHT_QUERY_PROFILING`| 新しいデータベース スコープの構成。 [`LIGHTWEIGHT_QUERY_PROFILING`](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md#lqp)に関するページを参照してください。 |
|`command` 列の `sys.dm_exec_requests` | `SELECT` で、クエリの実行を続行する前に、同期統計の更新操作の完了を待機している場合、`SELECT (STATMAN)` が表示されます。 [`sys.dm_exec_requests`](../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)に関するページを参照してください。|
|`sys.dm_exec_query_plan_stats` | すべてのクエリに対して、最後の既知の実際の実行プランと同等のものが返される新しい動的管理関数 (DMF)。 [sys.dm_exec_query_plan_stats](../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-stats-transact-sql.md) に関するページを参照してください。|
|`LAST_QUERY_PLAN_STATS` | `sys.dm_exec_query_plan_stats` を有効にする新しいデータベーススコープの構成。 「[ALTER DATABASE SCOPED CONFIGURATION (ALTER データベース スコープ ベースの構成)](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)」を参照してください。|
|`query_post_execution_plan_profile` | 標準プロファイリングを使用する `query_post_execution_showplan` とは異なり、軽量のプロファイリングに基づいて、実際の実行プランと同等のものが収集される拡張イベント。 [クエリ プロファイリング インフラストラクチャ](../relational-databases/performance/query-profiling-infrastructure.md)に関するページを参照してください。|
|`sys.dm_db_page_info(database_id, file_id, page_id, mode)` | データベースのページに関する情報が返される新しい DMF。 「[sys.dm_db_page_info (Transact-SQL)](../relational-databases/system-dynamic-management-views/sys-dm-db-page-info-transact-sql.md)」を参照してください。|
| &nbsp; | &nbsp; |

## <a name="developer-experience"></a>開発者エクスペリエンス
[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] は、グラフおよび空間データ型の機能強化、UTF-8 のサポート、新しい拡張フレームワークを備えた世界クラスの開発者エクスペリエンスを提供し続けており、開発者は好みの言語を使ってあらゆるデータの分析情報を得ることができます。

### <a name="graph"></a>グラフ

|新機能または更新 | 詳細 |
|:---|:---|
|エッジ制約のカスケード削除アクション | グラフ データベースでのエッジ制約で連鎖削除操作を定義できるようになりました。 「[エッジ制約](../relational-databases/tables/graph-edge-constraints.md)」を参照してください。 |
|新しいグラフ関数 - `SHORTEST_PATH` | `MATCH` 内で `SHORTEST_PATH` を使用し、グラフ内の任意の 2 ノード間の最短パスを検索することや、任意の長さのトラバーサルを実行することができるようになりました。|
|パーティション テーブルとパーティション インデックス| グラフ テーブルでテーブルとインデックスのパーティション分割がサポートされるようになりました。 |
|グラフ一致クエリで派生テーブルまたはビューの別名を使用する |[グラフ一致クエリ](../t-sql/queries/match-sql-graph.md)に関するページを参照してください。 |
| &nbsp; | &nbsp; |

### <a name="unicode-support"></a>Unicode のサポート
複数の国や地域にまたがるビジネスをサポートします。このような場合、顧客の要求に応え、特定の市場規制に準拠する上で、グローバルな多言語データベース アプリケーションとサービスを提供するという要件が重要です。 

|新機能または更新 | 詳細 |
|:---|:---|
|UTF-8 文字エンコードのサポート |インポートおよびエクスポートのエンコード時と、文字列データのデータベースレベルまたは列レベルの照合順序として UTF-8 がサポートされるようになりました。 サポートには、PolyBase 外部テーブルと Always Encrypted (Enclaves で使用しない場合) が含まれます。 [照合順序と Unicode のサポート](../relational-databases/collations/collation-and-unicode-support.md)に関するページを参照してください。|
| &nbsp; | &nbsp; |

### <a name="language-extensions"></a>言語拡張機能

|新機能または更新 | 詳細 |
|:---|:---|
|新しい Java 言語 SDK | SQL Server から実行できる Java プログラムの開発が簡略化されます。 「[SQL Server 用の Microsoft Extensibility SDK for Java](../language-extensions/how-to/extensibility-sdk-java-sql-server.md)」を参照してください。 |
|Java 言語の SDK はオープンソースです |[Microsoft SQL Server 用の Microsoft Extensibility SDK for Java](https://docs.microsoft.com/sql/language-extensions/how-to/extensibility-sdk-java-sql-server) がオープン ソース化され、[GitHub で入手可能](https://github.com/microsoft/sql-server-language-extensions)になりました。|
|Java データ型のサポート|[Java のデータ型](../language-extensions/how-to/java-to-sql-data-types.md)に関するページを参照してください。|
|新しい既定の Java Runtime | SQL Server には、製品全体での Java サポート用に Azul Systems Zulu Embedded が含まれようになりました。 「[Free supported Java in SQL Server 2019 is now available](https://cloudblogs.microsoft.com/sqlserver/2019/07/24/free-supported-java-in-sql-server-2019-is-now-available/)」(SQL Server 2019 で無料サポートの Java が利用可能に) を参照してください。 |
|SQL Server 言語拡張機能| 拡張性フレームワークで外部コードを実行します。 「[SQL Server 言語拡張機能](https://docs.microsoft.com/sql/language-extensions/language-extensions-overview)」を参照してください。
|外部言語を登録する|新しいデータ定義言語 (DDL) である `CREATE EXTERNAL LANGUAGE` では、Java などの外部言語が SQL Server に登録されます。 [CREATE EXTERNAL LANGUAGE](../t-sql/statements/create-external-language-transact-sql.md) に関するページを参照してください。 |
| &nbsp; | &nbsp; |

### <a name="spatial"></a>空間インデックス

|新機能または更新 | 詳細 |
|:---|:---|
| 新しい Spatial Reference Identifier (SRID) |[オーストラリアの GDA2020](http://www.ga.gov.au/scientific-topics/positioning-navigation/geodesy/datums-projections/gda2020) は、グローバル測位システムとより密接に連携した、さらに堅牢で正確なデータムを提供します。 新しい SRID は次のとおりです。<ul><li>地理 2D 用の 7843</li><li>地理 3D 用の 7844</li></ul> 新しい SRIDs の定義については、[sys.spatial_reference_systems](../relational-databases/system-catalog-views/sys-spatial-reference-systems-transact-sql.md) ビューを参照してください。 |
| &nbsp; | &nbsp; |

### <a name="error-messages"></a>エラー メッセージ
ソースとターゲットでデータ型や長さが一致しないために抽出、変換、読み込み (ETL) プロセスが失敗した場合、これまではトラブルシューティングには時間がかかりました。大規模なデータセットでは特にそうです。 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] を使用すると、データの切り捨てエラーを迅速に分析できます。

|新機能または更新 | 詳細 |
|:---|:---|
|詳細な切り捨ての警告 | データの切り捨てエラー メッセージに、テーブル名および列名と切り捨てられた値が既定で含まれるようになりました。 [VERBOSE_TRUNCATION_WARNINGS](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md#verbose-truncation)に関するページを参照してください。|
| &nbsp; | &nbsp; |

## <a name="mission-critical-security"></a>ミッションクリティカル セキュリティ
[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] には、データベース管理者と開発者が安全なデータベース アプリケーションを作成し、脅威に対抗できるように設計されたセキュリティ アーキテクチャが用意されています。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の各バージョンには新しい機能が導入され、以前のバージョンよりも改良されています。また、[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] もこのストーリーに基づいて引き続き構築されています。

|新機能または更新 | 詳細 |
|:---|:---|
|セキュア エンクレーブを使用する Always Encrypted|Always Encrypted、インプレース暗号化、さまざまな計算法を基盤に拡張し、サーバー側のセキュア エンクレーブ内でプレーンテキスト データの計算を可能にします。 インプレース暗号化では、データをデータベースの外に移動することが回避されるため、暗号操作 (列の暗号化、列のローテーション、暗号化鍵など) の性能と信頼度が上がります。<br><br> さまざまな計算法 (パターン一致や比較演算) がサポートされることで、機密データの保護が求められ、同時に Transact-SQL クエリで豊富な機能性が求められる幅広いシナリオや用途に Always Encrypted が対応できます。 「[セキュリティで保護されたエンクレーブが設定された Always Encrypted](../relational-databases/security/encryption/always-encrypted-enclaves.md)」をご覧ください。|
|SQL Server 構成マネージャーでの証明書管理|[証明書の管理 (SQL Server 構成マネージャー)](../database-engine/configure-windows/manage-certificates.md) に関するページを参照してください。|
|データの検出と分類|データの検出と分類には、データベース内の機密データを分類、ラベル付け、および保護するために、SQL Server にネイティブに組み込まれている高度な機能が用意されています。 最も機密性の高いデータ (ビジネス、財務、医療、PII など) の分類は、組織の情報保護の達成において極めて重要な役割を果たすことができます。 次のような場合にインフラストラクチャとして使用できます。<ul><li>データのプライバシー基準と規制のコンプライアンス要件を満たせるようにする。</li><li>監視 (監査) や、機密データへの異常アクセスに対するアラートなど、さまざまなセキュリティ シナリオ。</li><li>管理者がデータベースをセキュリティで保護する適切な手順を実行できるように、企業内で機密データが存在する場所を識別しやすくする。</li></ul>[監査](../relational-databases/security/auditing/sql-server-audit-database-engine.md)も、新しいフィールド `data_sensitivity_information` が監査ログに追加されて強化されました。このフィールドには、クエリによって返された実際のデータの機密度の分類 (ラベル) が記録されます。 詳細と例については、「[ADD SENSITIVITY CLASSIFICATION](../t-sql/statements/add-sensitivity-classification-transact-sql.md)」をご覧ください。|
| &nbsp; | &nbsp; |

## <a name="high-availability"></a>高可用性
[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] を展開する誰もが考慮する必要がある一般的なタスクの 1 つは、すべてのミッションクリティカルな [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] インスタンスとその中のデータベースを、ビジネスおよびエンド ユーザーが必要なときにいつでも利用できるようにすることです。 可用性は [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] プラットフォームの重要な柱であり、[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] では、企業がデータベース環境の高可用性を確保できる多くの新機能と機能強化が導入されています。

### <a name="availability-groups"></a>可用性グループ

|新機能または更新 | 詳細 |
|:---|:---|
|最大 5 つの同期レプリカ|[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] では 3 つであった同期レプリカの最大数が、[!INCLUDE[ssSQL17](../includes/sssql17-md.md)] では 5 つに増加します。 この 5 つのレプリカのグループを、グループ内で自動フェールオーバーするように構成できます。 1 つのプライマリ レプリカと、4 つの同期セカンダリ レプリカがあります。|
|セカンダリからプライマリ レプリカへの接続のリダイレクト| 接続文字列に指定されたターゲット サーバーに関係なく、クライアント アプリケーションの接続先をプライマリ レプリカにすることができます。 詳しくは、「[セカンダリからプライマリ レプリカへの読み取り/書き込み接続のリダイレクト (Always On 可用性グループ)](../database-engine/availability-groups/windows/secondary-replica-connection-redirection-always-on-availability-groups.md)」をご覧ください。|
|HADR の利点| SQL Server のいずれのソフトウェア アシュアランスをご利用のお客様でも、Microsoft が現在サポートしているすべての SQL Server リリースについて、3 つの強化された利点を使用できます。 詳細については、[こちらのお知らせ](https://cloudblogs.microsoft.com/sqlserver/2019/10/30/new-high-availability-and-disaster-recovery-benefits-for-sql-server/)を参照してください。
| &nbsp; | &nbsp; |

### <a name="recovery"></a>Recovery

|新機能または更新 | 詳細 |
|:---|:---|
|高速データベース復旧 | 高速データベース復旧 (ADR) を使用すると、再起動後、または実行時間が長いトランザクションのロールバック後の復旧時間が短縮されます。 [高速データベース復旧](../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md#adr)に関するページを参照してください。|
| &nbsp; | &nbsp; |

### <a name="resumable-operations"></a>再開可能な操作

|新機能または更新 | 詳細 |
|:---|:---|
|オンラインでのクラスター化列ストア インデックスのビルドとリビルド | [オンラインでのインデックス操作の実行](../relational-databases/indexes/perform-index-operations-online.md)に関するページを参照してください。 |
|再開可能なオンライン行ストア インデックスのビルド | [オンラインでのインデックス操作の実行](../relational-databases/indexes/perform-index-operations-online.md)に関するページを参照してください。 |
|Transparent Data Encryption (TDE) に対する初期スキャンの一時停止および再開|[Transparent Data Encryption (TDE) スキャンの一時停止と再開](../relational-databases/security/encryption/transparent-data-encryption.md#scan-suspend-resume)に関するページを参照してください。|
| &nbsp; | &nbsp; |

## <a name="platform-choice"></a>プラットフォームの選択肢
[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] は、[!INCLUDE[ssSQL17](../includes/sssql17-md.md)] で導入されたイノベーションに基づいており、お客様が選択したプラットフォーム上で、これまでよりも多くの機能とセキュリティを備えた [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] を実行できます。

### <a id="sql-server-on-linux"></a>Linux

| 新機能または更新 | 詳細 |
|:-----|:-----|
|レプリケーションのサポート | 「[Linux での SQL Server のレプリケーション](../linux/sql-server-linux-replication.md)」を参照してください。 |
|Microsoft 分散トランザクション コーディネーター (MSDTC) のサポート | 「[Linux で MSDTC を構成する方法](../linux/sql-server-linux-configure-msdtc.md)」を参照してください。 |
|サード パーティの AD プロバイダーに対する OpenLDAP のサポート | 「[チュートリアル:SQL Server on Linux で Active Directory 認証を使用する](../linux/sql-server-linux-active-directory-authentication.md)」を参照してください。 |
|Linux 上の Machine Learning Services | 「[Linux に SQL Server Machine Learning Services (Python と R) をインストールする](../linux/sql-server-linux-setup-machine-learning.md)」を参照してください。 |
|TempDB の機能強化 | 既定では、Linux 上に SQL Server を新しくインストールすると、論理コアの数に基づいて複数の TempDB データ ファイルが作成されます (最大で 8 個のデータ ファイル)。 これは、マイナー バージョンまたはメジャー バージョンのインプレース アップグレードには適用されません。 各 TempDB ファイルは 8 MB で、64 MB まで自動拡張します。 この動作は、Windows への SQL Server の既定のインストールに似ています。 |
|Linux での PolyBase | 非 Hadoop コネクタ向けの「[Linux への PolyBase のインストール](../relational-databases/polybase/polybase-linux-setup.md)」を参照してください。<br/><br/>[PolyBase の型マッピング](../relational-databases/polybase/polybase-type-mapping.md)に関するページを参照してください。 |
| 変更データ キャプチャ (CDC) のサポート | [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] では、変更データ キャプチャ (CDC) が Linux でサポートされるようになりました。 |
| &nbsp; | &nbsp; |

### <a name="containers"></a>[SSIS ログの構成]
[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] を使い始める最も簡単な方法は、コンテナーを使用することです。 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] は、以前のバージョンで導入されたイノベーションに基づいており、より安全な方法で、より多くの機能を備えた [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] コンテナーを新しいプラットフォームに展開できます。

|新機能または更新 | 詳細 |
|:---|:---|
| Microsoft Container Registry | [Microsoft Container Registry](https://azure.microsoft.com/blog/microsoft-syndicates-container-catalog/) では、[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] など、Microsoft の新しい公式コンテナー イメージのために Docker Hub が取り替えられます。 |
| ルート以外のコンテナー | [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] では、既定でルート以外のユーザーとして [!INCLUDE[sql-server](../includes/ssnoversion-md.md)] を起動することで、より安全なコンテナーを作成できるようになりました。 [非ルート ユーザーとして SQL Server コンテナーを作成して実行する](../linux/sql-server-linux-configure-docker.md#buildnonrootcontainer)方法に関する記事を参照してください。 |
| Red Hat 認定コンテナー イメージ | [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 以降、Red Hat Enterprise Linux 上で SQL Server コンテナーを実行できるようになりました。 |
| PolyBase と Machine Learning のサポート| [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] では、Machine Learning Services や PolyBase など、SQL Server コンテナーの新しい使用方法が導入されました。 [コンテナー GitHub リポジトリ内の SQL Server](https://github.com/microsoft/mssql-docker/tree/master/linux/preview/examples) の例を参照してください。 |
| &nbsp; | &nbsp; |

## <a name="setup-options"></a>セットアップ オプション

|新機能または更新 | 詳細 |
|:---|:---| 
|新しいメモリ セットアップ オプション | インストール中に "*最小サーバー メモリ (MB)* " および "*最大サーバー メモリ (MB)* " のサーバー構成を設定します。 「[[データベース エンジンの構成] - [メモリ] ページ](https://docs.microsoft.com/sql/sql-server/install/instance-configuration?view=sql-server-ver15#memory)」および「[コマンド プロンプトからの SQL Server のインストール](../database-engine/install-windows/install-sql-server-from-the-command-prompt.md#Install)」の `USESQLRECOMMENDEDMEMORYLIMITS`、`SQLMINMEMORY`、`SQLMAXMEMORY` パラメーターを参照してください。 提案される値は、「[サーバー メモリ構成オプション](../database-engine/configure-windows/server-memory-server-configuration-options.md#setting-the-memory-options-manually)」のメモリ構成ガイドラインに沿っています。| 
|新しい並列処理セットアップ オプション | インストールの間に "*並列処理の最大限度*" サーバー構成オプションを設定します。 「[[データベース エンジンの構成] - [MAXDOP] ページ](https://docs.microsoft.com/sql/sql-server/install/instance-configuration?view=sql-server-ver15#maxdop)」および「[コマンド プロンプトからの SQL Server のインストール](../database-engine/install-windows/install-sql-server-from-the-command-prompt.md#Install)」の `SQLMAXDOP` パラメーターを参照してください。 既定値は、「[max degree of parallelism サーバー構成オプションの構成](../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md#Guidelines)」の並列処理の最大限度ガイドラインに沿っています。| 
| &nbsp; | &nbsp; |

## <a id="ml"></a> SQL Server Machine Learning Services

|新機能または更新 | 詳細 |
|:---|:---|
|パーティション ベースのモデリング | `sp_execute_external_script` に追加された新しいパラメーターを使用して、データのパーティションごとに外部スクリプトを処理できます。 この機能は、1 つの大きいモデルではなく、多数の小さいモデル (データのパーティションごとに 1 つのモデル) のトレーニングをサポートします。 [パーティション ベースのモデルの作成](../advanced-analytics/tutorials/r-tutorial-create-models-per-partition.md)に関する記事を参照してください。|
|Windows Server フェールオーバー クラスター| Windows Server フェールオーバー クラスター上の Machine Learning Services に高可用性を構成できます。|
| &nbsp; | &nbsp; |

## <a name="sql-server-analysis-services"></a>SQL Server Analysis Services (SQL Server Analysis Services)

このリリースでは、パフォーマンス、リソース ガバナンス、およびクライアント サポートの新機能と機能強化が導入されました。

| 新機能または更新 | 詳細 |
|:---|:---|
|表形式モデルでの計算グループ| 計算グループを使用すると、一般的なメジャー式を*計算品目*としてグループ化することにより、冗長なメジャーの数を大幅に削減できます。 詳細については、[表形式モデルの計算グループ](/analysis-services/tabular-models/calculation-groups)に関する記事を参照してください。 |
|クエリ インターリーブ| クエリ インターリーブは、同時実行性の高いシナリオでユーザー クエリの応答時間を向上させることができる表形式モードのシステム構成です。 詳細については、「[クエリ インターリーブ](/analysis-services/tabular-models/query-interleaving)」を参照してください。 |
|表形式モデルでの多対多リレーションシップ| 両列が一意でない場合の多対多リレーションシップを使用できます。 詳細については、[表形式モデルでのリレーションシップ](/analysis-services/tabular-models/relationships-ssas-tabular)に関する記事を参照してください。|
|リソース ガバナンス用のプロパティ設定| このリリースでは、新しいメモリ設定が追加されました: リソース ガバナンス用の Memory\QueryMemoryLimit、DbpropMsmdRequestMemoryLimit、OLAP\Query\RowsetSerializationLimit。 詳細については、[メモリの設定](/analysis-services/server-properties/memory-properties)に関する記事を参照してください。|
|Power BI キャッシュの更新に対するガバナンス設定 | このリリースでは、ClientCacheRefreshPolicy プロパティが導入されました。これを使うと、Power BI サービスによるライブ接続レポートの初期読み込み時に、ダッシュボード タイル データとレポート データのキャッシュがオーバーライドされます。 詳細については、「[全般プロパティ](/analysis-services/server-properties/general-properties)」を参照してください。 |
| オンラインのアタッチ  | オンラインのアタッチは、オンプレミスのクエリ スケールアウト環境で読み取り専用レプリカを同期するために使用できます。 詳細については、「[オンラインのアタッチ](/analysis-services/what-s-new-in-sql-server-analysis-services#online-attach)」を参照してください。 |
| &nbsp; | &nbsp; |

## <a name="sql-server-integration-services"></a>SQL Server Integration Services

このリリースでは、ファイル操作を改善する新機能が導入されています。

| 新機能または更新 | 詳細 |
|:---|:---|
|柔軟なファイル タスク |ローカルファイルシステム、Azure Blob Storage、および Azure Data Lake Storage Gen2 でファイル操作を実行します。 「[柔軟なファイル タスク](../integration-services/control-flow/flexible-file-task.md)」を参照してください。|
|柔軟なファイルの変換元と変換先 |Azure Blob Storage、および Azure Data Lake Storage Gen2 のデータの読み取りと書き込みを行います。 「[柔軟なファイルの変換元](../integration-services/data-flow/flexible-file-source.md)」と「[柔軟なファイルの変換先](../integration-services/data-flow/flexible-file-destination.md)」を参照してください。 |

## <a name="sql-server-includemaster-data-servicesincludesssmdsshort-mdmd"></a>SQL Server [!INCLUDE[master-data-services](../includes/ssmdsshort-md.md)]

| 新機能または更新 | 詳細 |
|:---|:---|
|Azure SQL Database Managed Instance データベースのサポート| マネージド インスタンス上で [!INCLUDE[master-data-services](../includes/ssmdsshort-md.md)] をホストします。 [[!INCLUDE[master-data-services](../includes/ssmdsshort-md.md)] のインストールと構成](../master-data-services/master-data-services-installation-and-configuration.md#SetUpWeb)に関するページを参照してください。|
|新しい HTML コントロール| HTML コントロールでは、以前の Silverlight コンポーネントがすべて置き換えられます。 Silverlight の依存関係が削除されました。|
| &nbsp; | &nbsp; |

## <a name="sql-server-reporting-services"></a>SQL Server Reporting Services (SQL Server Reporting Services)

このリリースの SQL Server Reporting Services では、Azure SQL Database Managed Instance、Power BI Premium データセット、強化されたアクセシビリティ、Azure Active Directory アプリケーション プロキシ、Transparent Data Encryption がサポートされています。 また、Microsoft レポート ビルダーの更新プログラムも提供されます。 詳細については、[SQL Server Reporting Services の新機能](../reporting-services/what-s-new-in-sql-server-reporting-services-ssrs.md)に関する記事を参照してください。

## <a name="see-also"></a>参照

- [`SqlServer` PowerShell モジュール](https://www.powershellgallery.com/packages/Sqlserver)
- [SQL Server PowerShell ドキュメント](../powershell/sql-server-powershell.md)

## <a name="next-steps"></a>次の手順

- [SQL Server ワークショップ](https://aka.ms/sqlworkshops)
- [[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] リリース ノート](sql-server-version-15-release-notes.md)
- [Microsoft [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]:テクニカル ホワイト ペーパー](https://aka.ms/sql2019whitepaper)

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
