---
title: DMV を使用してスクリプトを監視する
description: 動的管理ビュー (DMV) を使用して、SQL Server Machine Learning Services での Python および R の外部スクリプトの実行を監視します。
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/17/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: ddaca1490782c8fd3a88b941fbabe6af48531726
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727753"
---
# <a name="monitor-sql-server-machine-learning-services-using-dynamic-management-views-dmvs"></a>動的管理ビュー (DMV) を使用して SQL Server Machine Learning Services を監視する
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

動的管理ビュー (DMV) を使用して、外部スクリプト (Python と R) の実行、使用されたリソース、問題の診断、SQL Server Machine Learning Services のパフォーマンスの調整を監視します。

この記事では、SQL Server Machine Learning Services に固有の DMV について説明します。 また、次のようなクエリの例も紹介します。

+ 機械学習の設定オプションと構成オプション
+ 外部の Python またはスクリプトを実行しているアクティブなセッション
+ Python および R 用の外部ランタイムの実行の統計
+ 外部スクリプトのパフォーマンス カウンター
+ OS、SQL Server、および外部リソース プールのメモリ使用量
+ SQL Server および外部リソース プールのメモリ構成
+ 外部リソース プールを含むリソース ガバナーのリソース プール
+ Python および R 用にインストールされたパッケージ

DMV に関する一般情報については、「[システムの動的管理ビュー](../../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)」を参照してください。

> [!TIP]
> カスタム レポートを使用して、SQL Server Machine Learning Services を監視することもできます。 詳細については、「[Management Studio でカスタム レポートを使用して機械学習を監視する](../../advanced-analytics/r/monitor-r-services-using-custom-reports-in-management-studio.md)」を参照してください。

## <a name="dynamic-management-views"></a>動的管理ビュー

SQL Server で機械学習のワークロードを監視するときに、次の動的管理ビューを使用できます。 DMV に対してクエリを実行するには、インスタンスに対する `VIEW SERVER STATE` 権限が必要です。

| 動的管理ビュー | 型 | [説明] |
|-------------------------|------|-------------|
| [sys.dm_external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md) | 実行 | 外部スクリプトを実行しているアクティブなワーカー アカウントごとに行を返します。 |
| [sys.dm_external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md) | 実行 | 外部スクリプト要求の種類ごとに 1 つの行を返します。 |
| [sys.dm_os_performance_counters](../../relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql.md) | 実行 | サーバーによって管理されているパフォーマンス カウンターごとに 1 つの行を返します。 検索条件 `WHERE object_name LIKE '%External Scripts%'` を使用する場合、この情報を使用して、実行されたスクリプトの数、実行されたスクリプトで使用された認証モード、またはインスタンス全体で発行された R または Python の呼び出しの総数を確認できます。 |
| [sys.dm_resource_governor_external_resource_pools](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pools.md) | [リソース ガバナー] | リソース ガバナーの外部リソース プールの現在の状態、リソース プールの現在の構成、および統計に関する情報を返します。 |
| [sys.dm_resource_governor_external_resource_pool_affinity](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md) | [リソース ガバナー] | リソース ガバナー内の現在の外部リソース プールの構成に関する CPU アフィニティ情報を返します。 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] のスケジューラごとに 1 行のデータを返します。各スケジューラは個別のプロセッサにマップされています。 このビューは、スケジューラの状況の監視やランナウェイ タスクの特定に使用できます。 |

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] インスタンスの監視の詳細については、「[カタログ ビュー](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)」と「[リソース ガバナー関連の動的管理ビュー](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md)」を参照してください。

## <a name="settings-and-configuration"></a>設定と構成

Machine Learning Services のインストール設定と構成オプションを表示します。

![設定と構成クエリからの出力](media/dmv-settings-and-configuration.png "設定と構成クエリからの出力")

この出力を取得するには、次のクエリを実行します。 使用するビューと関数の詳細については、「[sys. dm_server_registry](../../relational-databases/system-dynamic-management-views/sys-dm-server-registry-transact-sql.md)」、「[sys.configurations](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)」、および「[SERVERPROPERTY](../../t-sql/functions/serverproperty-transact-sql.md)」を参照してください。

```sql
SELECT CAST(SERVERPROPERTY('IsAdvancedAnalyticsInstalled') AS INT) AS IsMLServicesInstalled
    , CAST(value_in_use AS INT) AS ExternalScriptsEnabled
    , COALESCE(SIGN(SUSER_ID(CONCAT (
                    CAST(SERVERPROPERTY('MachineName') AS NVARCHAR(128))
                    , '\SQLRUserGroup'
                    , CAST(serverproperty('InstanceName') AS NVARCHAR(128))
                    ))), 0) AS ImpliedAuthenticationEnabled
    , COALESCE((
            SELECT CAST(r.value_data AS INT)
            FROM sys.dm_server_registry AS r
            WHERE r.registry_key LIKE 'HKLM\Software\Microsoft\Microsoft SQL Server\%\SuperSocketNetLib\Tcp'
            AND r.value_name = 'Enabled'
            ), - 1) AS IsTcpEnabled
FROM sys.configurations
WHERE name = 'external scripts enabled';
```

このクエリは次の列を返します。

| [列] | [説明] |
|--------|-------------|
| IsMLServicesInstalled | インスタンスに対して SQL Server Machine Learning Services がインストールされている場合は 1 を返します。 それ以外の場合は 0 を返します。 |
| ExternalScriptsEnabled | インスタンスの外部スクリプトが有効になっている場合は 1 を返します。 それ以外の場合は 0 を返します。 |
| ImpliedAuthenticationEnabled | 暗黙の認証が有効になっている場合は 1 を返します。 それ以外の場合は 0 を返します。 暗黙の認証の構成は、SQLRUserGroup のログインが存在するかどうかを確認することによって確認されます。 |
| IsTcpEnabled | インスタンスの TCP/IP プロトコルが有効になっている場合は 1 を返します。 それ以外の場合は 0 を返します。 詳細については、「[SQL Server の既定のネットワーク プロトコル構成](../../database-engine/configure-windows/default-sql-server-network-protocol-configuration.md)」を参照してください。 |

## <a name="active-sessions"></a>Active sessions

外部のスクリプトを実行しているアクティブなセッションを表示します。

![アクティブな設定クエリからの出力](media/dmv-active-sessions.png "アクティブな設定クエリからの出力")

この出力を取得するには、次のクエリを実行します。 使用される動的管理ビューの詳細については、「[sys. dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md)」、「[sys. dm_external_script_requests](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)」、および「[dm_exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)」を参照してください。

```sql
SELECT r.session_id, r.blocking_session_id, r.status, DB_NAME(s.database_id) AS database_name
    , s.login_name, r.wait_time, r.wait_type, r.last_wait_type, r.total_elapsed_time, r.cpu_time
    , r.reads, r.logical_reads, r.writes, er.language, er.degree_of_parallelism, er.external_user_name
FROM sys.dm_exec_requests AS r
INNER JOIN sys.dm_external_script_requests AS er
ON r.external_script_request_id = er.external_script_request_id
INNER JOIN sys.dm_exec_sessions AS s
ON s.session_id = r.session_id;
```

このクエリは次の列を返します。

| [列] | [説明] |
|--------|-------------|
| session_id | アクティブな各プライマリ接続に関連付けられたセッションを識別します。 |
| blocking_session_id | 要求をブロックしているセッションの ID。 この列が NULL の場合は、要求がブロックされていないか、ブロックしているセッションのセッション情報が使用または識別できません。 |
| ステータス | 要求の状態。 |
| database_name | 各セッションの現在のデータベースの名前。 |
| login_name | 現在セッションを実行している SQL Server ログイン名。 |
| wait_time | 要求が現在ブロックされている場合の現時点での待機時間 (ミリ秒単位)。 NULL 値は許可されません。 |
| wait_type | 要求が現在ブロックされている場合の待機の種類。 待機の種類の詳細については、「[sys.dm_os_wait_stats](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)」を参照してください。 |
| last_wait_type | 要求がブロックされていた場合の最後の待機の種類。 |
| total_elapsed_time | 要求を受信してから経過した総時間 (ミリ秒単位)。 |
| cpu_time | 要求で使用される CPU 時間 (ミリ秒単位)。 |
| reads | 要求で実行された読み取りの数。 |
| logical_reads | 要求で実行された論理読み取りの数。 |
| writes | 要求で実行された書き込みの数。 |
| language | サポートされているスクリプト言語を表すキーワードです。 |
| degree_of_parallelism | 作成された並列処理の数を示す数値です。 この値は、要求された並列処理の数と異なる場合があります。 |
| external_user_name | スクリプトが実行されたときの Windows ワーカー アカウント。 |

## <a name="execution-statistics"></a>実行の統計

R および Python 用の外部ランタイムの実行の統計を表示します。 現在使用できるのは、RevoScaleR、revoscalepy、または microsoftml パッケージ関数の統計情報のみです。

![実行統計クエリからの出力](media/dmv-execution-statistics.png "実行統計クエリからの出力")

この出力を取得するには、次のクエリを実行します。 使用される動的管理ビューの詳細については、「[sys.dm_external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md)」を参照してください。 このクエリは、複数回実行された関数のみを返します。

```sql
SELECT language, counter_name, counter_value
FROM sys.dm_external_script_execution_stats
WHERE counter_value > 0
ORDER BY language, counter_name;
```

このクエリは次の列を返します。

| [列] | [説明] |
|--------|-------------|
| language | 登録されている外部スクリプト言語の名前です。 |
| counter_name | 登録されている外部スクリプト関数の名前です。 |
| counter_value | 登録されている外部スクリプト関数がサーバーで呼び出されたインスタンスの合計数です。 この値は、機能がインスタンスにインストールされてからの累積値で、リセットすることはできません。 |

## <a name="performance-counters"></a>パフォーマンス カウンター

外部スクリプトの実行に関連するパフォーマンス カウンターを表示します。

![パフォーマンス カウンター クエリからの出力](media/dmv-performance-counters.png "パフォーマンス カウンター クエリからの出力")

この出力を取得するには、次のクエリを実行します。 使用される動的管理ビューの詳細については、「[sys.dm_os_performance_counters](../../relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql.md)」を参照してください。

```sql
SELECT counter_name, cntr_value
FROM sys.dm_os_performance_counters 
WHERE object_name LIKE '%External Scripts%'
```

**sys.dm_os_performance_counters** は、外部スクリプトの次のパフォーマンス カウンターを出力します。

| カウンター | [説明] |
|---------|-------------|
| Total Executions | ローカルまたはリモート呼び出しによって開始された外部プロセスの数。 |
| Parallel Executions | スクリプトに _\@並列処理_仕様が含まれ、[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] が並列クエリ プランを生成して使用することができた回数。 |
| Streaming Executions | ストリーミング機能が呼び出された回数。 |
| SQL CC Executions | 呼び出しがリモートでインスタンス化され、SQL Server が計算コンテキストとして使用された外部スクリプトの実行回数。 |
| Implied Auth.Login | ODBC ループバック呼び出しが暗黙の認証を使用して行われた回数。つまり、スクリプト要求を送信したユーザーに代わって [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] が呼び出しを実行した回数。 |
| Total Execution Time (ms) | 呼び出しと呼び出しの完了までの経過時間。 |
| Execution Errors | スクリプトがエラーを報告した回数。 この数には R または Python のエラーは含まれません。 |

## <a name="memory-usage"></a>メモリ使用量

OS、SQL Server、および外部プールによって使用されているメモリに関する情報を表示します。

![メモリ使用量クエリからの出力](media/dmv-memory-usage.png "メモリ使用量クエリからの出力")

この出力を取得するには、次のクエリを実行します。 使用される動的管理ビューの詳細については、「[sys.dm_resource_governor_external_resource_pools](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pools.md)」および「[sys.dm_os_sys_info](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md)」を参照してください。

```sql
SELECT physical_memory_kb, committed_kb
    , (SELECT SUM(peak_memory_kb)
        FROM sys.dm_resource_governor_external_resource_pools AS ep
        ) AS external_pool_peak_memory_kb
FROM sys.dm_os_sys_info;
```

このクエリは次の列を返します。

| [列] | [説明] |
|--------|-------------|
| physical_memory_kb | マシンに搭載されている物理メモリの合計。 |
| committed_kb | メモリ マネージャーでコミットされたメモリ (KB 単位)。 メモリ マネージャー内の予約済みメモリは含まれません。 |
| external_pool_peak_memory_kb | すべての外部リソース プールで使用されるメモリの最大量の合計 (KB 単位)。 |

## <a name="memory-configuration"></a>メモリ構成

SQL Server と外部リソース プールの割合での最大メモリ構成に関する情報を表示します。 SQL Server が `max server memory (MB)` の既定値で実行されている場合、OS メモリの 100% と見なされます。

![メモリ構成クエリからの出力](media/dmv-memory-configuration.png "メモリ構成クエリからの出力")

この出力を取得するには、次のクエリを実行します。 使用されるビューの詳細については、「[sys.configurations](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)」および「[sys.dm_resource_governor_external_resource_pools](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pools.md)」を参照してください。

```sql
SELECT 'SQL Server' AS name
    , CASE CAST(c.value AS BIGINT)
        WHEN 2147483647 THEN 100
        ELSE (SELECT CAST(c.value AS BIGINT) / (physical_memory_kb / 1024.0) * 100 FROM sys.dm_os_sys_info)
        END AS max_memory_percent
FROM sys.configurations AS c
WHERE c.name LIKE 'max server memory (MB)'
UNION ALL
SELECT CONCAT ('External Pool - ', ep.name) AS pool_name, ep.max_memory_percent
FROM sys.dm_resource_governor_external_resource_pools AS ep;
```

このクエリは次の列を返します。

| [列] | [説明] |
|--------|-------------|
| NAME | 外部リソース プールまたは SQL Server の名前。 |
| max_memory_percent | SQL Server または外部リソース プールが使用できる最大メモリ。 |

## <a name="resource-pools"></a>[リソース プール]

[SQL Server のリソース ガバナー](../../relational-databases/resource-governor/resource-governor.md)では、[リソース プール](../../relational-databases/resource-governor/resource-governor-resource-pool.md)は、 インスタンスの物理リソースのサブセットを表します。 受信するアプリケーション要求 (外部スクリプトの実行を含む) がリソース プール内で使用できる CPU、物理 IO、およびメモリの量に制限を指定できます。 SQL Server と外部スクリプトに使用されるリソース プールを表示します。

![リソース プール クエリからの出力](media/dmv-resource-pools.png "リソース プール クエリからの出力")

この出力を取得するには、次のクエリを実行します。 使用される動的管理ビューの詳細については、「[sys.dm_resource_governor_resource_pools](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pools-transact-sql.md)」および「[sys.dm_resource_governor_external_resource_pools](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pools.md)」を参照してください。

```sql
SELECT CONCAT ('SQL Server - ', p.name) AS pool_name
    , p.total_cpu_usage_ms, p.read_io_completed_total, p.write_io_completed_total
FROM sys.dm_resource_governor_resource_pools AS p
UNION ALL
SELECT CONCAT ('External Pool - ', ep.name) AS pool_name
    , ep.total_cpu_user_ms, ep.read_io_count, ep.write_io_count
FROM sys.dm_resource_governor_external_resource_pools AS ep;
```

このクエリは次の列を返します。

| [列] | [説明] |
|--------|-------------|
| pool_name | リソース プールの名前。 SQL Server リソース プールの先頭には `SQL Server` が付けられ、外部リソース プールの先頭には `External Pool` が付けられます。
| total_cpu_usage_hours | リソース ガバナー統計がリセットされてからの累積 CPU 使用率 (ミリ秒単位)。 |
| read_io_completed_total | リソース ガバナー統計がリセットされた後に完了した読み取り IO の合計。 |
| write_io_completed_total | リソース ガバナー統計がリセットされた後に完了した書き込み IO の合計。 |

## <a name="installed-packages"></a>インストール済みパッケージ

SQL Server Machine Learning Services にインストールされている R パッケージと Python パッケージを表示するには、これらを出力する R または Python のスクリプトを実行します。

### <a name="installed-packages-for-r"></a>R のインストール済みパッケージ

SQL Server Machine Learning Services にインストールされた R パッケージを表示します。

![R クエリ用にインストールされたパッケージからの出力](media/dmv-installed-packages-r.png "R クエリ用にインストールされたパッケージからの出力")

この出力を取得するには、次のクエリを実行します。 このクエリでは、R スクリプトを使用して、SQL Server を使用してインストールする R パッケージを決定します。

```sql
EXEC sp_execute_external_script @language = N'R'
, @script = N'
OutputDataSet <- data.frame(installed.packages()[,c("Package", "Version", "Depends", "License", "LibPath")]);'
WITH result sets((Package NVARCHAR(255), Version NVARCHAR(100), Depends NVARCHAR(4000)
    , License NVARCHAR(1000), LibPath NVARCHAR(2000)));
```

返される列は次のとおりです。

| [列] | [説明] |
|--------|-------------|
| [パッケージ] | インストールされているパッケージの名前。 |
| Version | パッケージのバージョン。 |
| 依存 | インストールされているパッケージが依存しているパッケージを一覧表示します。 |
| ライセンス | インストールされているパッケージのライセンス。 |
| LibPath | パッケージが格納されているディレクトリ。 |

### <a name="installed-packages-for-python"></a>Python 用にインストールされたパッケージ

SQL Server Machine Learning Services にインストールされた Python パッケージを表示します。

![Python クエリ用にインストールされたパッケージからの出力](media/dmv-installed-packages-python.png "Python クエリ用にインストールされたパッケージからの出力")

この出力を取得するには、次のクエリを実行します。 このクエリでは、Python スクリプトを使用して、SQL Server を使用してインストールする Python パッケージを決定します。

```sql
EXEC sp_execute_external_script @language = N'Python'
, @script = N'
import pip
OutputDataSet = pandas.DataFrame([(i.key, i.version, i.location) for i in pip.get_installed_distributions()])'
WITH result sets((Package NVARCHAR(128), Version NVARCHAR(128), Location NVARCHAR(1000)));
```

返される列は次のとおりです。

| [列] | [説明] |
|--------|-------------|
| [パッケージ] | インストールされているパッケージの名前。 |
| Version | パッケージのバージョン。 |
| Location | パッケージが格納されているディレクトリ。 |

## <a name="next-steps"></a>次の手順

+ [Machine Learning ソリューションの管理と監視](../../advanced-analytics/r/managing-and-monitoring-r-solutions.md)
+ [機械学習の拡張イベント](../../advanced-analytics/r/extended-events-for-sql-server-r-services.md)
+ [リソース ガバナー関連の動的管理ビュー](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md)
+ [システム動的管理ビュー](../../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)
+ [Management Studio でカスタム レポートを使用して機械学習を監視する](../../advanced-analytics/r/monitor-r-services-using-custom-reports-in-management-studio.md)
