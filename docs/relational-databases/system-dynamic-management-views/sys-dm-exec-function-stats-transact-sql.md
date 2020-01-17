---
title: sys _exec_function_stats (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 05/30/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
f1_keywords:
- sys.dm_exec_function_stats
- sys.dm_exec_function_stats_tsql
- dm_exec_function_stats
- dm_exec_function_stats_tsql
helpviewer_keywords:
- sys.dm_exec_function_stats dynamic management view
ms.assetid: 4c3d6a02-08e4-414b-90be-36b89a0e5a3a
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 89d66217536d5cd552eb11de67d6d97d21ec9f6e
ms.sourcegitcommit: c5e2aa3e4c3f7fd51140727277243cd05e249f78
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/02/2019
ms.locfileid: "68742829"
---
# <a name="sysdmexecfunctionstats-transact-sql"></a>sys _exec_function_stats (Transact-sql)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  キャッシュされた関数の集計パフォーマンス統計を返します。 ビューは、キャッシュされた関数プランごとに1行の値を返します。行の有効期間は、関数がキャッシュされたままである限り保持されます。 関数がキャッシュから削除されると、対応する行がこのビューから削除されます。 その時点で、パフォーマンス統計 SQL トレースイベントが **_exec_query_stats**と同様に発生します。 メモリ内の関数や CLR スカラー関数など、スカラー関数に関する情報を返します。 テーブル値関数に関する情報は返しません。  
  
 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]では、動的管理ビューでデータベースの包含に影響を与える情報を公開することや、ユーザーがアクセスできる他のデータベースに関する情報を公開することはできません。 この情報を公開しないように、接続されたテナントに属していないデータを含むすべての行がフィルターで除外されます。  
  
> [!NOTE]
> データには完了したクエリだけが反映され、まだ処理中ではないため、 **_exec_function_stats**の結果は実行ごとに異なる場合があります。 

  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|関数が存在するデータベース ID。|  
|**object_id**|**int**|関数のオブジェクト id 番号。|  
|**type**|**char(2)**|次のいずれかのオブジェクトの種類。 FN = スカラー値関数|  
|**type_desc**|**nvarchar(60)**|オブジェクトの種類の説明。SQL_SCALAR_FUNCTION|  
|**sql_handle**|**varbinary(64)**|これを使用すると、この関数内から実行された **_exec_query_stats**内のクエリと関連付けることができます。|  
|**plan_handle**|**varbinary(64)**|インメモリプランの識別子。 この識別子は一時的なものであり、プランがキャッシュに残っている間だけ一定のままです。 この値は、 **_exec_cached_plans**動的管理ビューで使用できます。<br /><br /> ネイティブコンパイル関数がメモリ最適化テーブルに対してクエリを実行する場合、は常に0x000 になります。|  
|**cached_time**|**datetime**|関数がキャッシュに追加された時刻。|  
|**last_execution_time**|**datetime**|関数が最後に実行された時刻。|  
|**execution_count**|**bigint**|関数が最後にコンパイルされてから実行された回数。|  
|**total_worker_time**|**bigint**|コンパイル後にこの関数の実行で消費された CPU 時間の合計 (マイクロ秒単位)。<br /><br /> ネイティブコンパイル関数では、多くの実行に1ミリ秒未満の場合、 **total_worker_time**は正確ではない可能性があります。|  
|**last_worker_time**|**bigint**|関数が最後に実行されたときに消費された CPU 時間 (マイクロ秒単位)。 <sup>1</sup>|  
|**min_worker_time**|**bigint**|この関数が1回の実行で消費した最小 CPU 時間 (マイクロ秒単位)。 <sup>1</sup>|  
|**max_worker_time**|**bigint**|この関数が1回の実行で消費した最大 CPU 時間 (マイクロ秒単位)。 <sup>1</sup>|  
|**total_physical_reads**|**bigint**|コンパイル後にこの関数の実行で行われた物理読み取りの合計数。<br /><br /> は常にメモリ最適化テーブルを照会する0になります。|  
|**last_physical_reads**|**bigint**|関数が最後に実行されたときに実行された物理読み取りの数。<br /><br /> は常にメモリ最適化テーブルを照会する0になります。|  
|**min_physical_reads**|**bigint**|この関数が1回の実行で行われた物理読み取りの最小数。<br /><br /> は常にメモリ最適化テーブルを照会する0になります。|  
|**max_physical_reads**|**bigint**|この関数が1回の実行で行われた物理読み取りの最大数。<br /><br /> は常にメモリ最適化テーブルを照会する0になります。|  
|**total_logical_writes**|**bigint**|コンパイル後にこの関数の実行によって実行された論理書き込みの合計数。<br /><br /> は常にメモリ最適化テーブルを照会する0になります。|  
|**last_logical_writes**|**bigint**|前回プランが実行されたときにダーティになったバッファー プール ページの数。 ページが既にダーティの場合 (変更された場合)、書き込みはカウントされません。<br /><br /> は常にメモリ最適化テーブルを照会する0になります。|  
|**min_logical_writes**|**bigint**|この関数が1回の実行で行われた論理書き込みの最小数。<br /><br /> は常にメモリ最適化テーブルを照会する0になります。|  
|**max_logical_writes**|**bigint**|この関数が1回の実行で行われた論理書き込みの最大数。<br /><br /> は常にメモリ最適化テーブルを照会する0になります。|  
|**total_logical_reads**|**bigint**|コンパイル後にこの関数の実行で行われた論理読み取りの合計数。<br /><br /> は常にメモリ最適化テーブルを照会する0になります。|  
|**last_logical_reads**|**bigint**|関数が最後に実行されたときに実行された論理読み取りの数。<br /><br /> は常にメモリ最適化テーブルを照会する0になります。|  
|**min_logical_reads**|**bigint**|この関数が1回の実行で行われた論理読み取りの最小数。<br /><br /> は常にメモリ最適化テーブルを照会する0になります。|  
|**max_logical_reads**|**bigint**|この関数が1回の実行で行われた論理読み取りの最大数。<br /><br /> は常にメモリ最適化テーブルを照会する0になります。|  
|**total_elapsed_time**|**bigint**|この関数の実行完了までの経過時間の合計 (マイクロ秒単位)。|  
|**last_elapsed_time**|**bigint**|最後に完了したこの関数の実行の経過時間 (マイクロ秒単位)。|  
|**min_elapsed_time**|**bigint**|この関数の実行完了までの最小経過時間 (マイクロ秒単位)。|  
|**max_elapsed_time**|**bigint**|この関数の実行完了までの最大経過時間 (マイクロ秒単位)。|  
|**total_page_server_reads**|**bigint**|コンパイル後にこの関数の実行によって実行されたページサーバーの読み取りの合計数。<br /><br /> **適用対象:** Azure SQL Database ハイパースケール。|  
|**last_page_server_reads**|**bigint**|関数が最後に実行されたときに実行されたページサーバーの読み取り回数。<br /><br /> **適用対象:** Azure SQL Database ハイパースケール。|  
|**min_page_server_reads**|**bigint**|この関数が1回の実行で行われたページサーバーの読み取りの最小数。<br /><br /> **適用対象:** Azure SQL Database ハイパースケール。|  
|**max_page_server_reads**|**bigint**|この関数が1回の実行で行われたページサーバー読み取りの最大数。<br /><br /> **適用対象:** Azure SQL Database ハイパースケール。|
  
## <a name="permissions"></a>アクセス許可  

で[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]は、 `VIEW SERVER STATE`権限が必要です。   
Premium [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]レベルでは、データベース`VIEW DATABASE STATE`の権限が必要です。 Standard [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]レベルおよび Basic レベルでは、**サーバー管理**者または**Azure Active Directory 管理者**アカウントが必要です。   
  
## <a name="examples"></a>使用例  
 次の例では、平均経過時間で識別される上位10個の関数に関する情報を返します。  
  
```  
SELECT TOP 10 d.object_id, d.database_id, OBJECT_NAME(object_id, database_id) 'function name',   
    d.cached_time, d.last_execution_time, d.total_elapsed_time,  
    d.total_elapsed_time/d.execution_count AS [avg_elapsed_time],  
    d.last_elapsed_time, d.execution_count  
FROM sys.dm_exec_function_stats AS d  
ORDER BY [total_worker_time] DESC;  
```  
  
## <a name="see-also"></a>関連項目  
 [実行関連の動的管理ビューおよび&#40;関数 transact-sql&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [_exec_sql_text &#40;transact-sql (dm)&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)   
 [sys.dm_exec_query_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)   
 
 [_exec_trigger_stats &#40;transact-sql (dm)&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-trigger-stats-transact-sql.md)   
 [_exec_procedure_stats &#40;transact-sql (dm)&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md)  
  
  
