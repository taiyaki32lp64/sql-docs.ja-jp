---
title: sys.dm_db_xtp_checkpoint_stats (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: language-reference
f1_keywords:
- dm_db_xtp_checkpoint_stats
- dm_db_xtp_checkpoint_stats_TSQL
- sys.dm_db_xtp_checkpoint_stats
- sys.dm_db_xtp_checkpoint_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_xtp_checkpoint_stats dynamic management view
ms.assetid: 8d0b18ca-db4d-4376-9905-3e4457727c46
author: stevestein
ms.author: sstein
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 84cbfafdba3bca9b06f250ed9996f0a87e71a18c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68026857"
---
# <a name="sysdm_db_xtp_checkpoint_stats-transact-sql"></a>sys.dm_db_xtp_checkpoint_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  現在のデータベースのインメモリ OLTP チェックポイント操作に関する統計を返します。 データベースがインメモリ OLTP オブジェクトを持たない場合は、空の結果セットを返します。  
  
 詳細については、「[インメモリ OLTP &#40;インメモリ最適化&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)」を参照してください。  
  
```  
USE In_Memory_db_name
SELECT * FROM sys.dm_db_xtp_checkpoint_stats;  
```  
  
**[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 新しいバージョンから大幅に異なるし、下位にあるトピックの説明は[SQL Server 2014](#bkmk_2014)します。**
  
## <a name="includesssql15includessssql15-mdmd-and-later"></a>[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] およびそれ以降  
 次の表に、列の記述`sys.dm_db_xtp_checkpoint_stats`以降 **[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]** します。  
  
|列名|型|説明|  
|-----------------|----------|-----------------|  
|last_lsn_processed|**bigint**|最後の LSN がコント ローラーに表示します。|  
|end_of_log_lsn|**numeric(38)**|ログの最後の LSN。|  
|bytes_to_end_of_log|**bigint**|ログ バイト数の間のバイト数に対応する、コント ローラーによって`last_lsn_processed`と`end_of_log_lsn`します。|  
|log_consumption_rate|**bigint**|トランザクション ログの使用量 (KB/秒) でコント ローラーでの比率。|  
|active_scan_time_in_ms|**bigint**|トランザクション ログを積極的にスキャンすることで、コント ローラーによって費やされた時間。|  
|total_wait_time_in_ms|**bigint**|ログをスキャンしない中に、コント ローラーの累積待機時間。|  
|waits_for_io|**bigint**|ログ、コント ローラー スレッドによって発生する IO の待機の数。|  
|io_wait_time_in_ms|**bigint**|コント ローラー スレッドによって、ログ IO の待機に費やされた累積的な時間が表示します。|  
|waits_for_new_log_count|**bigint**|新しいログを生成するためのコント ローラー スレッドによって発生する待機の数。|  
|new_log_wait_time_in_ms|**bigint**|累積的な時間では、コント ローラー スレッドによって、新しいログ待機に費やされました。|  
|idle_attempts_count|**bigint**|アイドル状態に移行して、コント ローラーの数です。|  
|tx_segments_dispatched|**bigint**|コント ローラーに表示され、シリアライザーにディスパッチのセグメントの数。 セグメントは、シリアル化の単位を形成するログの連続する部分です。 現在のサイズは 1 MB には、後で変更できます。|  
|segment_bytes_dispatched|**bigint**|データベースを再起動するために、コント ローラーに、シリアライザーによってディスパッチされるバイトの合計バイト数。|  
|bytes_serialized|**bigint**|バイトの合計数は、データベースを再起動するためにシリアル化されます。|  
|serializer_user_time_in_ms|**bigint**|ユーザー モードでのシリアライザーで費やされた時間。|  
|serializer_kernel_time_in_ms|**bigint**|カーネル モードでのシリアライザーで費やされた時間。|  
|xtp_log_bytes_consumed|**bigint**|データベースを再起動するために使用されるログのバイト数の合計数。|  
|checkpoints_closed|**bigint**|データベースが再起動した後に閉じられたチェックポイント数のカウントします。|  
|last_closed_checkpoint_ts|**bigint**|最後の閉じられたチェックポイントのタイムスタンプ。|  
|hardened_recovery_lsn|**numeric(38)**|回復は、この LSN から開始されます。|  
|hardened_root_file_guid|**uniqueidentifier**|最後に完了したチェックポイントの結果として書き込まれたルート ファイルの GUID です。|  
|hardened_root_file_watermark|**bigint**|**内部のみ**します。 どの程度が最大ルート ファイルの読み取りに有効な (これは、内部的に関連する型のみ - BSN と呼ばれます)。|  
|hardened_truncation_lsn|**numeric(38)**|切り捨てのポイントの LSN です。|  
|log_bytes_since_last_close|**bigint**|最後からのバイトは、ログの現在の末尾を閉じます。|  
|time_since_last_close_in_ms|**bigint**|チェックポイントの最後の終了からの経過時間。|  
|current_checkpoint_id|**bigint**|新しい現在のセグメントが、このチェックポイントに割り当てられています。 チェックポイントのシステムは、パイプラインです。 現在のチェックポイントにログからのセグメントが割り当てられている中です。 制限に達するとそれが、チェックポイントは、コント ローラーと新しいものを現在作成して解放されます。|  
|current_checkpoint_segment_count|**bigint**|現在のチェックポイントのセグメントの数。|  
|recovery_lsn_candidate|**bigint**|**内部でのみ**します。 Current_checkpoint_id ときに recoverylsn として選択されるように候補。|  
|outstanding_checkpoint_count|**bigint**|終了を待機しているパイプラインでのチェックポイントの数。|  
|closing_checkpoint_id|**bigint**|終了のチェックポイントの ID。<br /><br /> シリアライザーが並列で作業しているため、完了したら、チェックポイントはスレッドを終了して、終了する候補です。 スレッドを終了は一度に 1 つずつを閉じるだけことができ、終了のチェックポイントでは、スレッドを終了に取り組んでいますので順番にあります。|  
|recovery_checkpoint_id|**bigint**|回復に使用されるチェックポイントの ID。|  
|recovery_checkpoint_ts|**bigint**|チェックポイントの復旧のタイムスタンプ。|  
|bootstrap_recovery_lsn|**numeric(38)**|ブートス トラップの LSN を回復します。|  
|bootstrap_root_file_guid|**uniqueidentifier**|ブートス トラップのルート ファイルの GUID です。|  
|internal_error_code|**bigint**|コント ローラー、シリアライザー、close、およびマージのスレッドのいずれかで表示されるエラー。|
|bytes_of_large_data_serialized|**bigint**|シリアル化されたデータの量。 |  
  
##  <a name="bkmk_2014"></a> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
 次の表に、列の記述`sys.dm_db_xtp_checkpoint_stats`の **[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]** します。  
  
|列名|型|説明|  
|-----------------|----------|-----------------|  
|log_to_process_in_bytes|**bigint**|スレッドの現在ログ シーケンス番号 (LSN) とログの最後のログ バイト数。|  
|total_log_blocks_processed|**bigint**|サーバーの起動以降に処理されたログ ブロックの合計数。|  
|total_log_records_processed|**bigint**|サーバーが起動した後で処理されたログ レコードの合計数。|  
|xtp_log_records_processed|**bigint**|サーバーの起動以降に処理されたインメモリ OLTP ログ レコードの合計数。|  
|total_wait_time_in_ms|**bigint**|累積待機時間 (ミリ秒)。|  
|waits_for_io|**bigint**|ログ IO の待機の数。|  
|io_wait_time_in_ms|**bigint**|ログ IO の待機に費やされた累積的な時間が表示されます。|  
|waits_for_new_log|**bigint**|新しいログを生成する間、待機の数。|  
|new_log_wait_time_in_ms|**bigint**|新しいログ待機に費やされた累積時間。|  
|log_generated_since_last_checkpoint_in_bytes|**bigint**|前回のインメモリ OLTP チェックポイント以降に生成されたログの量。|  
|ms_since_last_checkpoint|**bigint**|前回のインメモリ OLTP チェックポイント以降のミリ秒単位の時間。|  
|checkpoint_lsn|**numeric(38)**|復旧ログ シーケンス番号 (LSN) 最後に完了したインメモリ OLTP チェックポイントに関連付けられています。|  
|current_lsn|**numeric(38)**|現在処理しているログ レコードの LSN。|  
|end_of_log_lsn|**numeric(38)**|ログの最後の LSN。|  
|task_address|**varbinary(8)**|SOS_Task のアドレス。 追加の情報を得るには、sys.dm_os_tasks と組み合わせます。|  
  
## <a name="permissions"></a>アクセス許可  
 サーバーに対する `VIEW DATABASE STATE` 権限が必要です。  
  
## <a name="see-also"></a>関連項目  
 [メモリ最適化テーブルの動的管理ビュー &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  
