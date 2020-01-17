---
title: dm_exec_query_stats (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 05/30/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_exec_query_stats_TSQL
- dm_exec_query_stats
- sys.dm_exec_query_stats
- sys.dm_exec_query_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_query_stats dynamic management view
ms.assetid: eb7b58b8-3508-4114-97c2-d877bcb12964
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a4fba10bd080c4b97cd38a7330611bed51f3d225
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "73982650"
---
# <a name="sysdm_exec_query_stats-transact-sql"></a>sys.dm_exec_query_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

キャッシュされたクエリ プランの集計パフォーマンス統計を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に返します。 このビューには、キャッシュされたプラン内のクエリ ステートメントごとに 1 行が含まれており、その行の有効期間はプラン自体に関連付けられています。 つまり、プランがキャッシュから削除されると、対応する行もこのビューから削除されます。  
  
> [!NOTE]
> - データには完了したクエリだけが反映され、まだ処理中ではないため、dm_exec_query_stats の結果は実行ごとに異なる場合があります **。**
> - [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] または [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]から呼び出すには、「 **sys. dm_pdw_nodes_exec_query_stats**」という名前を使用します。    

  
|列名|データ型|[説明]|  
|-----------------|---------------|-----------------|  
|**sql_handle**|**varbinary(64)**  |クエリが含まれているバッチまたはストアドプロシージャを一意に識別するトークンです。<br /><br /> **sql_handle**を**statement_start_offset**と**statement_end_offset**と共に使用すると、 **dm_exec_sql_text**動的管理関数を呼び出すことによって、クエリの sql テキストを取得できます。|  
|**statement_start_offset**|**int**|バッチまたは保存されるオブジェクトのテキスト内での、行が示すクエリの開始位置 (バイト単位)。0 で始まります。|  
|**statement_end_offset**|**int**|バッチまたは保存されるオブジェクトのテキスト内での、行が示すクエリの終了位置 (バイト単位)。0 で始まります。 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]前のバージョンでは、値-1 はバッチの終了を示します。 末尾のコメントは含まれなくなりました。|  
|**plan_generation_num**|**bigint**|再コンパイル後、プランのインスタンスを区別するために使用できるシーケンス番号。|  
|**plan_handle**|**varbinary(64)**|は、実行され、そのプランがプランキャッシュに存在するか、現在実行中のバッチのクエリ実行プランを一意に識別するトークンです。 この値は、クエリプランを取得するために、dm_exec_query_plan の動的管理関数に渡すことができます[。](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md)<br /><br /> ネイティブ コンパイル ストアド プロシージャがメモリ最適化テーブルに対してクエリを実行するときは、常に 0x000 になります。|  
|**creation_time**|**datetime**|プランがコンパイルされた時刻。|  
|**last_execution_time**|**datetime**|前回プランの実行が開始された時刻。|  
|**execution_count**|**bigint**|前回のコンパイル時以降に、プランが実行された回数。|  
|**total_worker_time**|**bigint**|コンパイル後にプランの実行で使用された CPU 時間の合計 (マイクロ秒単位)。ただし、精度はミリ秒単位までです。<br /><br /> ネイティブ コンパイル ストアド プロシージャに関して、多くの実行が 1 ミリ秒未満である場合は、 **total_worker_time** は精度が高くない可能性があります。|  
|**last_worker_time**|**bigint**|プランを前回実行したときに使用された CPU 時間 (マイクロ秒単位)。ただし、精度はミリ秒単位までです。 <sup>1</sup>|  
|**min_worker_time**|**bigint**|プランの 1 回の実行で使用された最小 CPU 時間 (マイクロ秒単位)。ただし、精度はミリ秒単位までです。 <sup>1</sup>|  
|**max_worker_time**|**bigint**|プランの 1 回の実行で使用された最大 CPU 時間 (マイクロ秒単位)。ただし、精度はミリ秒単位までです。 <sup>1</sup>|  
|**total_physical_reads**|**bigint**|コンパイル後にこのプランの実行で行われた物理読み取りの合計数。<br /><br /> は常にメモリ最適化テーブルを照会する0になります。|  
|**last_physical_reads**|**bigint**|プランを前回実行したときに行われた物理読み取りの数。<br /><br /> は常にメモリ最適化テーブルを照会する0になります。|  
|**min_physical_reads**|**bigint**|プランの 1 回の実行で行われた物理読み取りの最小数。<br /><br /> は常にメモリ最適化テーブルを照会する0になります。|  
|**max_physical_reads**|**bigint**|プランの 1 回の実行で行われた物理読み取りの最大数。<br /><br /> は常にメモリ最適化テーブルを照会する0になります。|  
|**total_logical_writes**|**bigint**|コンパイル後にプランの実行で行われた論理書き込みの合計数。<br /><br /> は常にメモリ最適化テーブルを照会する0になります。|  
|**last_logical_writes**|**bigint**|前回完了したプランの実行中にダーティされたバッファープールページの数。<br /><br />ページが読み取られた後、ページは最初に変更されたときにのみダーティになります。 ページがダーティになると、この数が増加します。 その後、既にダーティページを変更しても、この数値には影響しません。<br /><br />メモリ最適化テーブルに対してクエリを実行する場合、この数は常に0になります。|  
|**min_logical_writes**|**bigint**|プランの 1 回の実行で行われた論理書き込みの最小数。<br /><br /> は常にメモリ最適化テーブルを照会する0になります。|  
|**max_logical_writes**|**bigint**|プランの 1 回の実行で行われた論理書き込みの最大数。<br /><br /> は常にメモリ最適化テーブルを照会する0になります。|  
|**total_logical_reads**|**bigint**|コンパイル後にこのプランの実行で行われた論理読み取りの合計数。<br /><br /> は常にメモリ最適化テーブルを照会する0になります。|  
|**last_logical_reads**|**bigint**|プランを前回実行したときに行われた論理読み取りの数。<br /><br /> は常にメモリ最適化テーブルを照会する0になります。|  
|**min_logical_reads**|**bigint**|プランの 1 回の実行で行われた論理読み取りの最小数。<br /><br /> は常にメモリ最適化テーブルを照会する0になります。|  
|**max_logical_reads**|**bigint**|プランの 1 回の実行で行われた論理読み取りの最大数。<br /><br /> は常にメモリ最適化テーブルを照会する0になります。|  
|**total_clr_time**|**bigint**|コンパイルされてから、このプランの実行によって共通言語ランタイム (CLR) オブジェクト [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] [!INCLUDE[msCoName](../../includes/msconame-md.md)] 内部で使用された時間 (マイクロ秒単位)。ただし、精度はミリ秒単位までです。 CLR オブジェクトには、ストアド プロシージャ、関数、トリガー、型、および集計を指定できます。|  
|**last_clr_time**|**bigint**|このプランの前回の実行中に [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] CLR オブジェクト内で実行によって使用された時間 (マイクロ秒単位)。ただし、精度はミリ秒単位までです。 CLR オブジェクトには、ストアド プロシージャ、関数、トリガー、型、および集計を指定できます。|  
|**min_clr_time**|**bigint**|プランの 1 回の実行で、[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] CLR オブジェクト内部で使用された最小時間 (マイクロ秒単位)。ただし、精度はミリ秒単位までです。 CLR オブジェクトには、ストアド プロシージャ、関数、トリガー、型、および集計を指定できます。|  
|**max_clr_time**|**bigint**|プランの 1 回の実行で、[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] CLR 内部で使用された最大時間 (マイクロ秒単位)。ただし、精度はミリ秒単位までです。 CLR オブジェクトには、ストアド プロシージャ、関数、トリガー、型、および集計を指定できます。|  
|**total_elapsed_time**|**bigint**|このプランの実行完了までの経過時間の合計 (マイクロ秒単位)。ただし、精度はミリ秒単位までです。|  
|**last_elapsed_time**|**bigint**|このプランの前回の実行完了までの経過時間 (マイクロ秒単位)。ただし、精度はミリ秒単位までです。|  
|**min_elapsed_time**|**bigint**|任意のプランの実行完了までの最小経過時間 (マイクロ秒単位)。ただし、精度はミリ秒単位までです。|  
|**max_elapsed_time**|**bigint**|任意のプランの実行完了までの最大経過時間 (マイクロ秒単位)。ただし、精度はミリ秒単位までです。|  
|**query_hash**|**Binary(8)**|クエリで計算され、同様のロジックを持つクエリを識別するために使用される、バイナリのハッシュ値です。 クエリ ハッシュを使用して、リテラル値だけが異なるクエリの全体的なリソース使用率を決定できます。|  
|**query_plan_hash**|**binary(8)**|クエリ実行プランで計算され、同様のクエリ実行プランを識別するために使用される、バイナリのハッシュ値です。 クエリ プラン ハッシュを使用して、同様の実行プランを持つクエリの累積コストを確認できます。<br /><br /> ネイティブ コンパイル ストアド プロシージャがメモリ最適化テーブルに対してクエリを実行するときは、常に 0x000 になります。|  
|**total_rows**|**bigint**|クエリによって返される行の合計数。 null にすることはできません。<br /><br /> ネイティブ コンパイル ストアド プロシージャがメモリ最適化テーブルに対してクエリを実行するときは、常に 0 になります。|  
|**last_rows**|**bigint**|クエリの前回の実行で返された行数。 null にすることはできません。<br /><br /> ネイティブ コンパイル ストアド プロシージャがメモリ最適化テーブルに対してクエリを実行するときは、常に 0 になります。|  
|**min_rows**|**bigint**|1回の実行中にクエリによって返される行の最小数。 null にすることはできません。<br /><br /> ネイティブ コンパイル ストアド プロシージャがメモリ最適化テーブルに対してクエリを実行するときは、常に 0 になります。|  
|**max_rows**|**bigint**|1回の実行中にクエリによって返される行の最大数。 null にすることはできません。<br /><br /> ネイティブ コンパイル ストアド プロシージャがメモリ最適化テーブルに対してクエリを実行するときは、常に 0 になります。|  
|**statement_sql_handle**|**varbinary(64)**|**適用対象**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 以降。<br /><br /> クエリストアが有効になっていて、その特定のクエリの統計情報を収集している場合にのみ、NULL 以外の値が設定されます。|  
|**statement_context_id**|**bigint**|**適用対象**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 以降。<br /><br /> クエリストアが有効になっていて、その特定のクエリの統計情報を収集している場合にのみ、NULL 以外の値が設定されます。|  
|**total_dop**|**bigint**|並列処理の次数の合計。このプランはコンパイルされた後に使用されます。 メモリ最適化テーブルに対してクエリを実行する場合は、常に0になります。<br /><br /> **適用対象**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降。|  
|**last_dop**|**bigint**|このプランが最後に実行されたときの並列処理の次数。 メモリ最適化テーブルに対してクエリを実行する場合は、常に0になります。<br /><br /> **適用対象**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降。|  
|**min_dop**|**bigint**|並列処理の最小限度。このプランは、1回の実行中に使用されます。 メモリ最適化テーブルに対してクエリを実行する場合は、常に0になります。<br /><br /> **適用対象**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降。|  
|**max_dop**|**bigint**|並列処理の最大限度。このプランは、1回の実行中に使用されます。 メモリ最適化テーブルに対してクエリを実行する場合は、常に0になります。<br /><br /> **適用対象**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降。|  
|**total_grant_kb**|**bigint**|予約済みメモリの合計量は、このプランがコンパイルされてからこのプランを受信したことを KB 単位で付与します。 メモリ最適化テーブルに対してクエリを実行する場合は、常に0になります。<br /><br /> **適用対象**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降。|  
|**last_grant_kb**|**bigint**|このプランが最後に実行されたときに予約されているメモリの量 (KB 単位)。 メモリ最適化テーブルに対してクエリを実行する場合は、常に0になります。<br /><br /> **適用対象**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降。|  
|**min_grant_kb**|**bigint**|予約済みメモリの最小量は、このプランが1回の実行中に受信したことを KB 単位で付与します。 メモリ最適化テーブルに対してクエリを実行する場合は、常に0になります。<br /><br /> **適用対象**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降。|  
|**max_grant_kb**|**bigint**|予約済みメモリの最大量は、このプランが1回の実行中に受信したことを KB 単位で付与します。 メモリ最適化テーブルに対してクエリを実行する場合は、常に0になります。<br /><br /> **適用対象**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降。|  
|**total_used_grant_kb**|**bigint**|予約済みメモリの合計量は、このプランがコンパイルされた後に使用されたことを KB 単位で付与します。 メモリ最適化テーブルに対してクエリを実行する場合は、常に0になります。<br /><br /> **適用対象**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降。|  
|**last_used_grant_kb**|**bigint**|このプランの前回の実行時に使用されたメモリ許可の量 (KB 単位)。 メモリ最適化テーブルに対してクエリを実行する場合は、常に0になります。<br /><br /> **適用対象**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降。|  
|**min_used_grant_kb**|**bigint**|使用されるメモリの最小量は、このプランの1回の実行中に使用されることを KB 単位で付与します。 メモリ最適化テーブルに対してクエリを実行する場合は、常に0になります。<br /><br /> **適用対象**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降。|  
|**max_used_grant_kb**|**bigint**|使用済みメモリの最大量は、このプランが1回の実行中に使用されたことを KB 単位で付与します。 メモリ最適化テーブルに対してクエリを実行する場合は、常に0になります。<br /><br /> **適用対象**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降。|  
|**total_ideal_grant_kb**|**bigint**|理想的なメモリの合計量は、このプランがコンパイルされてから推定される、KB 単位で付与されます。 メモリ最適化テーブルに対してクエリを実行する場合は、常に0になります。<br /><br /> **適用対象**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降。|  
|**last_ideal_grant_kb**|**bigint**|このプランが最後に実行されたときの理想的なメモリ許可の量 (KB 単位)。 メモリ最適化テーブルに対してクエリを実行する場合は、常に0になります。<br /><br /> **適用対象**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降。|  
|**min_ideal_grant_kb**|**bigint**|理想的なメモリの最小量は、このプランの1回の実行中に推定されることを KB 単位で付与します。 メモリ最適化テーブルに対してクエリを実行する場合は、常に0になります。<br /><br /> **適用対象**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降。|  
|**max_ideal_grant_kb**|**bigint**|理想的なメモリの最大量は、このプランの1回の実行中に推定されることを KB 単位で付与します。 メモリ最適化テーブルに対してクエリを実行する場合は、常に0になります。<br /><br /> **適用対象**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降。|  
|**total_reserved_threads**|**bigint**|予約済みの並列スレッドの合計。このプランは、コンパイルされた後に使用されます。 メモリ最適化テーブルに対してクエリを実行する場合は、常に0になります。<br /><br /> **適用対象**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降。|  
|**last_reserved_threads**|**bigint**|このプランが最後に実行されたときに予約済みの並列スレッドの数。 メモリ最適化テーブルに対してクエリを実行する場合は、常に0になります。<br /><br /> **適用対象**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降。|  
|**min_reserved_threads**|**bigint**|予約済みの並列スレッドの最小数。このプランでは、1回の実行中に使用されます。  メモリ最適化テーブルに対してクエリを実行する場合は、常に0になります。<br /><br /> **適用対象**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降。|  
|**max_reserved_threads**|**bigint**|予約済みの並列スレッドの最大数。このプランでは、1回の実行中に使用されます。 メモリ最適化テーブルに対してクエリを実行する場合は、常に0になります。<br /><br /> **適用対象**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降。|  
|**total_used_threads**|**bigint**|使用済みの並列スレッドの合計。このプランは、コンパイルされた後に使用されます。 メモリ最適化テーブルに対してクエリを実行する場合は、常に0になります。<br /><br /> **適用対象**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降。|  
|**last_used_threads**|**bigint**|このプランの前回の実行時に使用された並列スレッドの数。 メモリ最適化テーブルに対してクエリを実行する場合は、常に0になります。<br /><br /> **適用対象**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降。|  
|**min_used_threads**|**bigint**|このプランで1回の実行中に使用された並列スレッドの最小数。 メモリ最適化テーブルに対してクエリを実行する場合は、常に0になります。<br /><br /> **適用対象**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降。|  
|**max_used_threads**|**bigint**|使用される並列スレッドの最大数。このプランでは、1回の実行中に使用されます。 メモリ最適化テーブルに対してクエリを実行する場合は、常に0になります。<br /><br /> **適用対象**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降。|  
|**total_columnstore_segment_reads**|**bigint**|クエリによって読み取られた列ストアセグメントの合計。 null にすることはできません。<br /><br /> **適用対象**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 および [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3 以降|    
|**last_columnstore_segment_reads**|**bigint**|クエリが最後に実行されたときに読み取られた列ストアセグメントの数。 null にすることはできません。<br /><br /> **適用対象**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 および [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3 以降|    
|**min_columnstore_segment_reads**|**bigint**|1回の実行中にクエリによって読み取られた列ストアセグメントの最小数。 null にすることはできません。<br /><br /> **適用対象**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 および [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3 以降|    
|**max_columnstore_segment_reads**|**bigint**|1回の実行中にクエリによって読み取られた列ストアセグメントの最大数。 null にすることはできません。<br /><br /> **適用対象**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 および [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3 以降|    
|**total_columnstore_segment_skips**|**bigint**|クエリでスキップされた列ストアセグメントの合計合計。 null にすることはできません。<br /><br /> **適用対象**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 および [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3 以降|    
|**last_columnstore_segment_skips**|**bigint**|クエリの最後の実行でスキップされた列ストアセグメントの数。 null にすることはできません。<br /><br /> **適用対象**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 および [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3 以降|    
|**min_columnstore_segment_skips**|**bigint**|1回の実行中にクエリによってスキップされた列ストアセグメントの最小数。 null にすることはできません。<br /><br /> **適用対象**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 および [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3 以降|    
|**max_columnstore_segment_skips**|**bigint**|1回の実行中にクエリによってスキップされた列ストアセグメントの最大数。 null にすることはできません。<br /><br /> **適用対象**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 および [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3 以降|
|**total_spills**|**bigint**|コンパイル後にこのクエリの実行によって書き込まれたページの合計数。<br /><br /> **適用対象**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 および [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3 以降|  
|**last_spills**|**bigint**|クエリが最後に実行されたときに書き込まれたページの数。<br /><br /> **適用対象**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 および [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3 以降|  
|**min_spills**|**bigint**|このクエリで1回の実行中に書き込まれたページの最小数。<br /><br /> **適用対象**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 および [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3 以降|  
|**max_spills**|**bigint**|このクエリで1回の実行中に書き込まれたページの最大数。<br /><br /> **適用対象**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 および [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3 以降|  
|**pdw_node_id**|**int**|このディストリビューションが配置されているノードの識別子。<br /><br /> **適用対象**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]、[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]| 
|**total_page_server_reads**|**bigint**|このプランがコンパイルされてから、このプランの実行でリモートページサーバーの読み取り回数の合計。<br /><br /> **適用対象:** Azure SQL DB のハイパースケール |  
|**last_page_server_reads**|**bigint**|プランを最後に実行したときに実行されたリモートページサーバーの読み取り回数。<br /><br /> **適用対象:** Azure SQL DB のハイパースケール |  
|**min_page_server_reads**|**bigint**|このプランの1回の実行で行われたリモートページサーバー読み取りの最小数。<br /><br /> **適用対象:** Azure SQL DB のハイパースケール |  
|**max_page_server_reads**|**bigint**|このプランで1回の実行で行われたリモートページサーバー読み取りの最大数。<br /><br /> **適用対象:** Azure SQL DB のハイパースケール |  
> [!NOTE]
> <sup>1</sup>ネイティブコンパイルストアドプロシージャの統計コレクションが有効になっている場合、ワーカー時間はミリ秒単位で収集されます。 クエリが1ミリ秒未満で実行された場合、値は0になります。  
  
## <a name="permissions"></a>アクセス許可  

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]では、`VIEW SERVER STATE` のアクセス許可が必要です。   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Premium レベルでは、データベースの `VIEW DATABASE STATE` アクセス許可が必要です。 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Standard レベルと Basic レベルでは、**サーバー管理**者または**Azure Active Directory 管理者**アカウントが必要です。   
   
## <a name="remarks"></a>Remarks  
 ビュー内の統計は、クエリが完了したときに更新されます。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-finding-the-top-n-queries"></a>A. TOP N クエリを確認する  
 次の例では、CPU の平均時間で順位付けされた上位 5 つのクエリに関する情報を返します。 この例では、クエリ ハッシュに従ってクエリを集計して、論理的に等価のクエリを累積リソース使用量別にグループ化しています。  
  
```sql  
SELECT TOP 5 query_stats.query_hash AS "Query Hash",   
    SUM(query_stats.total_worker_time) / SUM(query_stats.execution_count) AS "Avg CPU Time",  
    MIN(query_stats.statement_text) AS "Statement Text"  
FROM   
    (SELECT QS.*,   
    SUBSTRING(ST.text, (QS.statement_start_offset/2) + 1,  
    ((CASE statement_end_offset   
        WHEN -1 THEN DATALENGTH(ST.text)  
        ELSE QS.statement_end_offset END   
            - QS.statement_start_offset)/2) + 1) AS statement_text  
     FROM sys.dm_exec_query_stats AS QS  
     CROSS APPLY sys.dm_exec_sql_text(QS.sql_handle) as ST) as query_stats  
GROUP BY query_stats.query_hash  
ORDER BY 2 DESC;  
```  
  
### <a name="b-returning-row-count-aggregates-for-a-query"></a>b. クエリの行数集計を返す  
 次の例では、クエリに対して行数の集計情報 (行の総数、最小行数、最大行数、および最後の行) を返します。  
  
```sql  
SELECT qs.execution_count,  
    SUBSTRING(qt.text,qs.statement_start_offset/2 +1,   
                 (CASE WHEN qs.statement_end_offset = -1   
                       THEN LEN(CONVERT(nvarchar(max), qt.text)) * 2   
                       ELSE qs.statement_end_offset end -  
                            qs.statement_start_offset  
                 )/2  
             ) AS query_text,   
     qt.dbid, dbname= DB_NAME (qt.dbid), qt.objectid,   
     qs.total_rows, qs.last_rows, qs.min_rows, qs.max_rows  
FROM sys.dm_exec_query_stats AS qs   
CROSS APPLY sys.dm_exec_sql_text(qs.sql_handle) AS qt   
WHERE qt.text like '%SELECT%'   
ORDER BY qs.execution_count DESC;  
```  
  
## <a name="see-also"></a>参照  
[実行関連の動的管理ビューおよび関数 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)    
[sys.dm_exec_sql_text &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)    
[sys.dm_exec_query_plan &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md)    
[dm_exec_procedure_stats &#40;transact-sql&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md)     
[sys.dm_exec_trigger_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-trigger-stats-transact-sql.md)  
[sys.dm_exec_cached_plans &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)    
  


