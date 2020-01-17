---
title: query_store_runtime_stats (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 07/24/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- SYS.QUERY_STORE_RUNTIME_STATS_TSQL
- QUERY_STORE_RUNTIME_STATS_TSQL
- SYS.QUERY_STORE_RUNTIME_STATS
- QUERY_STORE_RUNTIME_STATS
dev_langs:
- TSQL
helpviewer_keywords:
- query_store_runtime_stats catalog view
- sys.query_store_runtime_stats catalog view
ms.assetid: ccf7a57c-314b-450c-bd34-70749a02784a
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||= azure-sqldw-latest||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 0bd7f1870a88ae2050445050565e0f268f4d9b0e
ms.sourcegitcommit: a154b3050b6e1993f8c3165ff5011ff5fbd30a7e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/30/2019
ms.locfileid: "70148287"
---
# <a name="sysquery_store_runtime_stats-transact-sql"></a>query_store_runtime_stats (Transact-sql)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  クエリのランタイム実行統計情報に関する情報を格納します。  
  
|列名|データ型|[説明]|  
|-----------------|---------------|-----------------|  
|**runtime_stats_id**|**bigint**|**Plan_id**、 **execution_type** 、および**runtime_stats_interval_id**のランタイム実行の統計を表す行の識別子。 これは、過去の実行時統計の間隔に対してのみ一意です。 現在アクティブな間隔では、 **plan_id**によって参照されるプランの実行時統計を表す複数の行が**execution_type**によって表される実行の種類と共に存在する場合があります。 通常、1つの行はディスクにフラッシュされる実行時の統計情報を表し、他の行はメモリ内の状態を表します。 したがって、各間隔の実際の状態を取得するには、メトリックを集計し、 **plan_id**、 **execution_type** 、および**runtime_stats_interval_id**でグループ化する必要があります。<br/>**注:** Azure SQL Data Warehouse は常にゼロ (0) を返します。|
|**plan_id**|**bigint**|外部キー。 [Query_store_plan &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)に結合します。|  
|**runtime_stats_interval_id**|**bigint**|外部キー。 [Query_store_runtime_stats_interval &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)に結合します。|  
|**execution_type**|**tinyint**|クエリ実行の種類を決定します。<br /><br /> 0-通常の実行 (正常に完了)<br /><br /> 3-クライアントが開始した実行中止<br /><br /> 4-例外が実行を中止しました|  
|**execution_type_desc**|**nvarchar(128)**|実行の種類のフィールドの説明テキストです。<br /><br /> 0-標準<br /><br /> 3-中止<br /><br /> 4-例外|  
|**first_execution_time**|**datetimeoffset**|集計間隔内のクエリプランの最初の実行時間。 これは、クエリの実行の終了時刻を示します。|  
|**last_execution_time**|**datetimeoffset**|集計間隔内のクエリプランの最後の実行時間。 これは、クエリの実行の終了時刻を示します。|  
|**count_executions**|**bigint**|集計間隔内のクエリプランの実行の合計数。|  
|**avg_duration**|**float**|集計間隔内のクエリプランの平均実行時間 (マイクロ秒単位で報告)。|  
|**last_duration**|**bigint**|集計間隔内のクエリプランの最後の期間 (マイクロ秒単位で報告)。|  
|**min_duration**|**bigint**|集計間隔内のクエリプランの最小期間 (マイクロ秒単位で報告されます)。|  
|**max_duration**|**bigint**|集計間隔内のクエリプランの最大期間 (マイクロ秒単位で報告されます)。|  
|**stdev_duration**|**float**|集計間隔内のクエリプランの標準偏差 (マイクロ秒単位で報告)。|  
|**avg_cpu_time**|**float**|集計間隔内のクエリプランの平均 CPU 時間 (マイクロ秒単位で報告)。<br/>**注:** Azure SQL Data Warehouse は常にゼロ (0) を返します。|
|**last_cpu_time**|**bigint**|集計間隔内のクエリプランの最後の CPU 時間 (マイクロ秒単位で報告)。<br/>**注:** Azure SQL Data Warehouse は常にゼロ (0) を返します。|
|**min_cpu_time**|**bigint**|集計間隔内のクエリプランの最小 CPU 時間 (マイクロ秒単位で報告されます)。<br/>**注:** Azure SQL Data Warehouse は常にゼロ (0) を返します。|
|**max_cpu_time**|**bigint**|集計間隔内のクエリプランの最大 CPU 時間 (マイクロ秒単位で報告)。<br/>**注:** Azure SQL Data Warehouse は常にゼロ (0) を返します。|
|**stdev_cpu_time**|**float**|集計間隔内のクエリプランの CPU 時間の標準偏差 (マイクロ秒単位で報告されます)。<br/>**注:** Azure SQL Data Warehouse は常にゼロ (0) を返します。|
|**avg_logical_io_reads**|**float**|集計間隔内のクエリプランに対する論理 i/o 読み取りの平均数。 (読み取られた 8 KB ページの数として表現されます)。<br/>**注:** Azure SQL Data Warehouse は常にゼロ (0) を返します。|
|**last_logical_io_reads**|**bigint**|集計間隔内のクエリプランに対する論理 i/o 読み取りの最後の数。 (読み取られた 8 KB ページの数として表現されます)。<br/>**注:** Azure SQL Data Warehouse は常にゼロ (0) を返します。|
|**min_logical_io_reads**|**bigint**|集計間隔内のクエリプランに対する論理 i/o 読み取りの最小数。 (読み取られた 8 KB ページの数として表現されます)。<br/>**注:** Azure SQL Data Warehouse は常にゼロ (0) を返します。|
|**max_logical_io_reads**|**bigint**|集計間隔内のクエリプランの論理 i/o 読み取りの最大数。(読み取られた 8 KB ページの数として表現されます)。<br/>**注:** Azure SQL Data Warehouse は常にゼロ (0) を返します。|
|**stdev_logical_io_reads**|**float**|集計間隔内のクエリプランの標準偏差を読み取る論理 i/o の数。 (読み取られた 8 KB ページの数として表現されます)。<br/>**注:** Azure SQL Data Warehouse は常にゼロ (0) を返します。|
|**avg_logical_io_writes**|**float**|集計間隔内のクエリプランに対する論理 i/o 書き込みの平均数。<br/>**注:** Azure SQL Data Warehouse は常にゼロ (0) を返します。|
|**last_logical_io_writes**|**bigint**|集計間隔内のクエリプランに対する論理 i/o 書き込みの最後の数。<br/>**注:** Azure SQL Data Warehouse は常にゼロ (0) を返します。|
|**min_logical_io_writes**|**bigint**|集計間隔内のクエリプランに対する論理 i/o 書き込みの最小数。<br/>**注:** Azure SQL Data Warehouse は常にゼロ (0) を返します。|
|**max_logical_io_writes**|**bigint**|集計間隔内のクエリプランに対する論理 i/o 書き込みの最大数。<br/>**注:** Azure SQL Data Warehouse は常にゼロ (0) を返します。|
|**stdev_logical_io_writes**|**float**|集計間隔内のクエリプランの標準偏差を書き込む論理 i/o の数。<br/>**注:** Azure SQL Data Warehouse は常にゼロ (0) を返します。|
|**avg_physical_io_reads**|**float**|集計間隔内のクエリプランに対する物理 i/o 読み取りの平均数 (読み取られた 8 KB ページの数として表されます)。<br/>**注:** Azure SQL Data Warehouse は常にゼロ (0) を返します。|
|**last_physical_io_reads**|**bigint**|集計間隔内のクエリプランに対する物理 i/o 読み取りの最後の数 (読み取られた 8 KB ページの数として表されます)。<br/>**注:** Azure SQL Data Warehouse は常にゼロ (0) を返します。|
|**min_physical_io_reads**|**bigint**|集計間隔内のクエリプランに対する物理 i/o 読み取りの最小数 (読み取られた 8 KB ページの数として表されます)。<br/>**注:** Azure SQL Data Warehouse は常にゼロ (0) を返します。|
|**max_physical_io_reads**|**bigint**|集計間隔内のクエリプランの物理 i/o 読み取りの最大数 (読み取られた 8 KB ページの数として表されます)。<br/>**注:** Azure SQL Data Warehouse は常にゼロ (0) を返します。|
|**stdev_physical_io_reads**|**float**|物理 i/o の数は、集計間隔内のクエリプランの標準偏差を読み取ります (8 KB ページ読み取り数として表されます)。<br/>**注:** Azure SQL Data Warehouse は常にゼロ (0) を返します。|
|**avg_clr_time**|**float**|集計間隔内のクエリプランの平均 CLR 時間 (マイクロ秒単位で報告)。<br/>**注:** Azure SQL Data Warehouse は常にゼロ (0) を返します。|
|**last_clr_time**|**bigint**|集計間隔内のクエリプランの最後の CLR 時間 (マイクロ秒単位で報告)。<br/>**注:** Azure SQL Data Warehouse は常にゼロ (0) を返します。|
|**min_clr_time**|**bigint**|集計間隔内のクエリプランの最小 CLR 時間 (マイクロ秒単位で報告)。<br/>**注:** Azure SQL Data Warehouse は常にゼロ (0) を返します。|
|**max_clr_time**|**bigint**|集計間隔内のクエリプランの最大 CLR 時間 (マイクロ秒単位で報告)。<br/>**注:** Azure SQL Data Warehouse は常にゼロ (0) を返します。|
|**stdev_clr_time**|**float**|集計間隔内のクエリプランの CLR 時間標準偏差 (マイクロ秒単位で報告)。<br/>**注:** Azure SQL Data Warehouse は常にゼロ (0) を返します。|
|**avg_dop**|**float**|集計間隔内のクエリプランの平均 DOP (並列処理の次数)。<br/>**注:** Azure SQL Data Warehouse は常にゼロ (0) を返します。|
|**last_dop**|**bigint**|集計間隔内のクエリプランの最後の DOP (並列処理の次数)。<br/>**注:** Azure SQL Data Warehouse は常にゼロ (0) を返します。|
|**min_dop**|**bigint**|集計間隔内のクエリプランの最小 DOP (並列処理の次数)。<br/>**注:** Azure SQL Data Warehouse は常にゼロ (0) を返します。|
|**max_dop**|**bigint**|集計間隔内のクエリプランの最大 DOP (並列処理の次数)。<br/>**注:** Azure SQL Data Warehouse は常にゼロ (0) を返します。|
|**stdev_dop**|**float**|集計間隔内のクエリプランの DOP (並列処理の次数) 標準偏差。<br/>**注:** Azure SQL Data Warehouse は常にゼロ (0) を返します。|
|**avg_query_max_used_memory**|**float**|集計間隔内のクエリプランの平均メモリ許可 (8 KB ページの数として報告されます)。 ネイティブコンパイルメモリ最適化プロシージャを使用するクエリの場合は、常に0になります。<br/>**注:** Azure SQL Data Warehouse は常にゼロ (0) を返します。|
|**last_query_max_used_memory**|**bigint**|集計間隔内のクエリプランの最後のメモリ許可 (8 KB ページの数として報告されます)。 ネイティブコンパイルメモリ最適化プロシージャを使用するクエリの場合は、常に0になります。<br/>**注:** Azure SQL Data Warehouse は常にゼロ (0) を返します。|
|**min_query_max_used_memory**|**bigint**|集計間隔内のクエリプランの最小メモリ許可 (8 KB ページの数として報告されます)。 ネイティブコンパイルメモリ最適化プロシージャを使用するクエリの場合は、常に0になります。<br/>**注:** Azure SQL Data Warehouse は常にゼロ (0) を返します。|
|**max_query_max_used_memory**|**bigint**|集計間隔内のクエリプランの最大メモリ許可 (8 KB ページの数として報告されます)。 ネイティブコンパイルメモリ最適化プロシージャを使用するクエリの場合は、常に0になります。<br/>**注:** Azure SQL Data Warehouse は常にゼロ (0) を返します。|
|**stdev_query_max_used_memory**|**float**|集計間隔内のクエリプランのメモリ許可標準偏差 (8 KB ページの数として報告されます)。 ネイティブコンパイルメモリ最適化プロシージャを使用するクエリの場合は、常に0になります。<br/>**注:** Azure SQL Data Warehouse は常にゼロ (0) を返します。|
|**avg_rowcount**|**float**|集計間隔内のクエリプランで返された行の平均数。<br/>**注:** Azure SQL Data Warehouse は常にゼロ (0) を返します。|
|**last_rowcount**|**bigint**|集計間隔内でクエリプランが最後に実行されたときに返された行の数。<br/>**注:** Azure SQL Data Warehouse は常にゼロ (0) を返します。|
|**min_rowcount**|**bigint**|集計間隔内のクエリプランに返される行の最小数。<br/>**注:** Azure SQL Data Warehouse は常にゼロ (0) を返します。|
|**max_rowcount**|**bigint**|集計間隔内のクエリプランで返される行の最大数。|  
|**stdev_rowcount**|**float**|集計間隔内のクエリプランで返される行の標準偏差の数。|
|**avg_log_bytes_used**|**float**|集計間隔内で、クエリプランによって使用されるデータベースログの平均バイト数。<br/>**注:** Azure SQL Data Warehouse は常にゼロ (0) を返します。|
|**last_log_bytes_used**|**bigint**|集計間隔内で、クエリプランの前回の実行で使用されたデータベースログ内のバイト数。<br/>**注:** Azure SQL Data Warehouse は常にゼロ (0) を返します。|
|**min_log_bytes_used**|**bigint**|集計間隔内で、クエリプランによって使用されるデータベースログの最小バイト数。<br/>**注:** Azure SQL Data Warehouse は常にゼロ (0) を返します。|
|**max_log_bytes_used**|**bigint**|集計間隔内で、クエリプランによって使用されるデータベースログ内の最大バイト数。<br/>**注:** Azure SQL Data Warehouse は常にゼロ (0) を返します。|
|**stdev_log_bytes_used**|**float**|集計間隔内で、クエリプランによって使用されるデータベースログ内のバイト数の標準偏差。<br/>**注:** Azure SQL Data Warehouse は常にゼロ (0) を返します。|  
|**avg_tempdb_space_used**|**float**|集計間隔内のクエリプランの平均ページ読み取り回数。 (読み取られた 8 KB ページの数として表現されます)。<br><br/>**適用対象:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]以降) および [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。|
|**last_tempdb_space_used**|**bigint**|集計間隔内のクエリプランのページ読み取りの最後の数。 (読み取られた 8 KB ページの数として表現されます)。<br><br/>**適用対象:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]以降) および [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。|
|**min_tempdb_space_used**|**bigint**|集計間隔内のクエリプランのページ読み取りの最小数。 (読み取られた 8 KB ページの数として表現されます)。<br><br/>**適用対象:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]以降) および [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。|
|**max_tempdb_space_used**|**bigint**|集計間隔内のクエリプランのページ読み取りの最大数。(読み取られた 8 KB ページの数として表現されます)。<br><br/>**適用対象:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]以降) および [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。|
|**stdev_tempdb_space_used**|**float**|集計間隔内のクエリプランに対するページ読み取りの標準偏差。 (読み取られた 8 KB ページの数として表現されます)。<br><br/>**適用対象:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]以降) および [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。|
|**avg_page_server_io_reads**|**float**|集計間隔内のクエリプランに対するページサーバー i/o 読み取りの平均数。 (読み取られた 8 KB ページの数として表現されます)。<br><br/>**適用対象:** Azure SQL Database ハイパースケール</br>**注:** Azure SQL Data Warehouse、Azure SQL DB、MI (ハイパースケール以外) は常にゼロ (0) を返します。|
|**last_page_server_io_reads**|**bigint**|集計間隔内のクエリプランのページサーバー i/o 読み取りの最後の数。 (読み取られた 8 KB ページの数として表現されます)。<br><br/>**適用対象:** Azure SQL Database ハイパースケール</br>**注:** Azure SQL Data Warehouse、Azure SQL DB、MI (ハイパースケール以外) は常にゼロ (0) を返します。|
|**min_page_server_io_reads**|**bigint**|集計間隔内のクエリプランのページサーバー i/o 読み取りの最小数。 (読み取られた 8 KB ページの数として表現されます)。<br><br/>**適用対象:** Azure SQL Database ハイパースケール</br>**注:** Azure SQL Data Warehouse、Azure SQL DB、MI (ハイパースケール以外) は常にゼロ (0) を返します。|
|**max_page_server_io_reads**|**bigint**|集計間隔内のクエリプランのページサーバー i/o 読み取りの最大数。(読み取られた 8 KB ページの数として表現されます)。<br><br/>**適用対象:** Azure SQL Database ハイパースケール</br>**注:** Azure SQL Data Warehouse、Azure SQL DB、MI (ハイパースケール以外) は常にゼロ (0) を返します。|
|**stdev_page_server_io_reads**|**float**|ページサーバー i/o の数は、集計間隔内のクエリプランの標準偏差を読み取ります。 (読み取られた 8 KB ページの数として表現されます)。<br><br/>**適用対象:** Azure SQL Database ハイパースケール</br>**注:** Azure SQL Data Warehouse、Azure SQL DB、MI (ハイパースケール以外) は常にゼロ (0) を返します。|
  
## <a name="permissions"></a>アクセス許可  
`VIEW DATABASE STATE` アクセス許可が必要です。  
  
## <a name="see-also"></a>参照  
 [database_query_store_options &#40;transact-sql&#41; ](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [query_context_settings &#40;transact-sql&#41; ](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)   
 [query_store_plan &#40;transact-sql&#41; ](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)   
 [query_store_query &#40;transact-sql&#41; ](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)   
 [query_store_query_text &#40;transact-sql&#41; ](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)   
 [sys.query_store_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)  
 [query_store_runtime_stats_interval &#40;transact-sql&#41; ](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)   
 [クエリのストアを使用した、パフォーマンスの監視](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [クエリ ストアのストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)    
 [クエリ ストアを使用する際の推奨事項](../../relational-databases/performance/best-practice-with-the-query-store.md)   
  
