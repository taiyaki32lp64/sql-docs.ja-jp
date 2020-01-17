---
title: database_query_store_options (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 01/23/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- DATABASE_QUERY_STORE_OPTIONS_TSQL
- DATABASE_QUERY_STORE_OPTIONS
- SYS.DATABASE_QUERY_STORE_OPTIONS_TSQL
- SYS.DATABASE_QUERY_STORE_OPTIONS
dev_langs:
- TSQL
helpviewer_keywords:
- database_query_store_options catalog view
- sys.database_query_store_options catalog view
ms.assetid: 16b47d55-8019-41ff-ad34-1e0112178067
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||= azure-sqldw-latest||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5f2c8189c19fbdf6dc9a83e62117da517322df86
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "73983167"
---
# <a name="sysdatabase_query_store_options-transact-sql"></a>database_query_store_options (Transact-sql)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  このデータベースのクエリストアオプションを返します。  
  
**適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降)、[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]。
  
|列名|データ型|[説明]|  
|-----------------|---------------|-----------------|  
|**desired_state**|**smallint**|クエリストアの目的の操作モードを示します。ユーザーによって明示的に設定されます。<br /> 0 = OFF <br /> 1 = READ_ONLY<br /> 2 = READ_WRITE|  
|**desired_state_desc**|**nvarchar(60)**|クエリストアの目的の操作モードの説明テキストです。<br />OFF<br />READ_ONLY<br />READ_WRITE|  
|**actual_state**|**smallint**|クエリストアの操作モードを示します。 ユーザーが必要とする状態の一覧に加えて、実際の状態はエラー状態になることがあります。<br /> 0 = OFF <br /> 1 = READ_ONLY<br /> 2 = READ_WRITE<br /> 3 = エラー|  
|**actual_state_desc**|**nvarchar(60)**|クエリストアの実際の操作モードの説明テキスト。<br />OFF<br />READ_ONLY<br />READ_WRITE<br />ERROR<br /><br /> 実際の状態が目的の状態と異なる場合は、次のような状況が考えられます。<br />-データベースが読み取り専用モードに設定されている場合、またはクエリストアサイズが構成されたクォータを超えている場合は、ユーザーが読み取り/書き込みを指定した場合でも、クエリストアが読み取り専用モードで動作する可能性があります。<br />-極端なシナリオではクエリストア内部エラーのためにエラー状態になることがあります。 このような状況が発生した場合、SQL 2017 以降では、影響を受けるデータベースの `sp_query_store_consistency_check` ストアドプロシージャを実行してクエリストアを復旧できます。 `sp_query_store_consistency_check` 実行されて2016いない場合は、を実行してデータをクリアする必要があり `ALTER DATABASE [YourDatabaseName] SET QUERY_STORE CLEAR ALL;`|  
|**readonly_reason**|**int**|**Desired_state_desc**が READ_WRITE、 **actual_state_desc**が READ_ONLY されている場合、readonly_reason が読み取り専用モードである理由を示すビットマップ**が返され**ます。<br /><br /> **1** -データベースは読み取り専用モードです。<br /><br /> **2** -データベースはシングルユーザーモードです<br /><br /> **4** -データベースは緊急モードです。<br /><br /> **8** -データベースはセカンダリレプリカです (Always On と [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] geo レプリケーションに適用されます)。 この値は、**読み取り可能**なセカンダリレプリカでのみ効果的に監視できます。<br /><br /> **65536** -クエリストアが MAX_STORAGE_SIZE_MB オプションによって設定されたサイズ制限に達しました。<br /><br /> **131072** -クエリストア内のさまざまなステートメントの数が内部メモリの制限に達しました。 クエリストアを読み取り/書き込みモードに転送できるようにするために、必要のないクエリを削除するか、上位のサービス階層にアップグレードすることを検討してください。<br />**適用対象:** [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]」をご覧ください。<br /><br /> **262144** -ディスクに保存されるのを待機しているインメモリ項目のサイズが内部メモリの制限に達しました。 メモリ内の項目がディスクに保存されるまで、クエリストアは一時的に読み取り専用モードになります。 <br />**適用対象:** [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]」をご覧ください。<br /><br /> **524288** -データベースがディスクサイズの上限に達しました。 クエリストアはユーザーデータベースの一部であるため、データベースに使用できる空き領域がない場合は、クエリストアがそれ以上大きくなることはありません。<br />**適用対象:** [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]」をご覧ください。 <br /> <br /> クエリストア操作モードを読み取り/書き込みに戻す方法については、「[クエリストアのベストプラクティス](../../relational-databases/performance/best-practice-with-the-query-store.md#Verify)」の「**クエリデータを継続的に収集するクエリストア**」を参照してください。|  
|**current_storage_size_mb**|**bigint**|ディスク上のクエリストアのサイズ (メガバイト単位)。|  
|**flush_interval_seconds**|**bigint**|クエリストアデータをディスクに定期的にフラッシュする期間 (秒単位)。 既定値は**900** (15 分) です。<br /><br /> `ALTER DATABASE <database> SET QUERY_STORE (DATA_FLUSH_INTERVAL_SECONDS  = <interval>)` ステートメントを使用して変更します。|  
|**interval_length_minutes**|**bigint**|統計の集計間隔を分単位で指定します。 任意の値を指定することはできません。 1、5、10、15、30、60、および1440分のいずれかを使用します。 既定値は**60**分です。|  
|**max_storage_size_mb**|**bigint**|クエリストアの最大ディスクサイズ (mb)。 既定値は**100** MB です。<br />[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] Premium edition の場合、既定値は 1 GB、[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] Basic エディションの場合、既定値は 10 MB です。<br /><br /> `ALTER DATABASE <database> SET QUERY_STORE (MAX_STORAGE_SIZE_MB = <size>)` ステートメントを使用して変更します。|  
|**stale_query_threshold_days**|**bigint**|ポリシー設定がないクエリがクエリストアに保持される日数。 既定値は**30**です。 保持ポリシーを無効にするには0に設定します。<br />[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] Basic エディションの場合、既定の日数は 7 日です。<br /><br /> `ALTER DATABASE <database> SET QUERY_STORE ( CLEANUP_POLICY = ( STALE_QUERY_THRESHOLD_DAYS = <value> ) )` ステートメントを使用して変更します。|  
|**max_plans_per_query**|**bigint**|格納されているプランの最大数を制限します。 既定値は**200**です。 最大値に達した場合、クエリストアそのクエリの新しいプランのキャプチャを停止します。 を0に設定すると、キャプチャされたプランの数に関する制限がなくなります。<br /><br /> `ALTER DATABASE<database> SET QUERY_STORE (MAX_PLANS_PER_QUERY = <n>)` ステートメントを使用して変更します。|  
|**query_capture_mode**|**smallint**|現在アクティブなクエリのキャプチャモード:<br /><br /> **1** = すべて-すべてのクエリがキャプチャされます。 これは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降) の既定の構成値です。<br /><br /> 2 = 実行回数とリソース消費量に基づいて、関連するクエリを自動キャプチャします。 これは [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] の既定の構成値です。<br /><br /> 3 = なし-新しいクエリのキャプチャを停止します。 クエリ ストアは、既にキャプチャされたクエリのコンパイルと実行時の統計情報を収集し続けます。 重要なクエリをキャプチャしない場合があるため、この構成は慎重に使用してください。|  
|**query_capture_mode_desc**|**nvarchar(60)**|クエリストアの実際のキャプチャモードの説明テキスト。<br /><br /> ALL ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]の既定値)<br /><br /> **AUTO** ([!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]の既定値)<br /><br /> NONE|  
|**size_based_cleanup_mode**|**smallint**|データの総量が最大サイズに近づいたときに、クリーンアップを自動的にアクティブにするかどうかを制御します。<br /><br /> 0 = オフサイズベースのクリーンアップは自動的にアクティブ化されません。<br /><br /> **1** = 自動サイズベースのクリーンアップは、ディスク上のサイズが*max_storage_size_mb*の**90%** に達したときに自動的にアクティブ化されます。 これは既定の構成値です。<br /><br />サイズのクリーンアップでは、まず最も安価で最も古いクエリを削除します。 *Max_storage_size_mb*の約**80%** に達した時点で停止します。|  
|**size_based_cleanup_mode_desc**|**nvarchar(60)**|クエリストアの実際のサイズに基づくクリーンアップモードの説明テキストです。<br /><br /> OFF <br /> **AUTO** (既定値)|  
|**wait_stats_capture_mode**|**smallint**|クエリストア待機の統計情報のキャプチャを実行するかどうかを制御します。 <br /><br /> 0 = OFF <br /> **1** = オン<br /> **適用対象**: [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] 以降。|
|**wait_stats_capture_mode_desc**|**nvarchar(60)**|実際の待機統計キャプチャモードの説明テキスト。 <br /><br /> OFF <br /> **ON** (既定値)<br /> **適用対象**: [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] 以降。| 
  
## <a name="permissions"></a>アクセス許可  
 `VIEW DATABASE STATE` アクセス許可が必要です。  
  
## <a name="see-also"></a>参照  
 [query_context_settings &#40;transact-sql&#41; ](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)   
 [query_store_plan &#40;transact-sql&#41; ](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)   
 [query_store_query &#40;transact-sql&#41; ](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)   
 [query_store_query_text &#40;transact-sql&#41; ](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)   
 [query_store_runtime_stats &#40;transact-sql&#41; ](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-transact-sql.md)   
 [sys.query_store_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)  
 [query_store_runtime_stats_interval &#40;transact-sql&#41; ](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)   
 [クエリのストアを使用した、パフォーマンスの監視](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [fn_stmt_sql_handle_from_sql_stmt &#40;transact-sql&#41; ](../../relational-databases/system-functions/sys-fn-stmt-sql-handle-from-sql-stmt-transact-sql.md)   
 [ストアドプロシージャ&#40;のクエリストア transact-sql&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)  
  
  
