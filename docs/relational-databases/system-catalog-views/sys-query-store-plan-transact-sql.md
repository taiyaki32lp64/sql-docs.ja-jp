---
title: query_store_plan (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 01/23/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- QUERY_STORE_PLAN_TSQL
- SYS.QUERY_STORE_PLAN
- SYS.QUERY_STORE_PLAN_TSQL
- QUERY_STORE_PLAN
dev_langs:
- TSQL
helpviewer_keywords:
- query_store_plan catalog view
- sys.query_store_plan catalog view
ms.assetid: b4d05439-6360-45db-b1cd-794f4a64935e
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||= azure-sqldw-latest||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 1d1137aab32a98a4699e95b7138bb333f63c65e9
ms.sourcegitcommit: ea6603e20c723553c89827a6b8731a9e7b560b9c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2019
ms.locfileid: "74479457"
---
# <a name="sysquery_store_plan-transact-sql"></a>sys.query_store_plan (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  クエリに関連付けられている各実行プランに関する情報を格納します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|
|**plan_id**|**bigint**|主キー|  
|**query_id**|**bigint**|外部キー。 [Query_store_query &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)に結合します。|  
|**plan_group_id**|**bigint**|プラングループの ID。 通常、カーソルクエリには複数の (設定およびフェッチ) プランが必要です。 同時にコンパイルされたプランの設定とフェッチは、同じグループに含まれます。<br /><br /> 0は、プランがグループに含まれていないことを示します。|  
|**engine_version**|**nvarchar (32)**|**' Major. minor. build. revision '** 形式でプランをコンパイルするために使用されるエンジンのバージョン。|  
|**compatibility_level**|**smallint**|クエリで参照されているデータベースのデータベース互換性レベル。|  
|**query_plan_hash**|**binary (8)**|個々のプランの MD5 ハッシュ。|  
|**query_plan**|**nvarchar (max)**|クエリプランの Showplan XML。|  
|**is_online_index_plan**|**bit**|プランは、オンラインのインデックス構築中に使用されました。 <br/>**注:** Azure SQL Data Warehouse は常にゼロ (0) を返します。|  
|**is_trivial_plan**|**bit**|Plan は、単純なプランです (クエリオプティマイザーのステージ0での出力)。 <br/>**注:** Azure SQL Data Warehouse は常にゼロ (0) を返します。|  
|**is_parallel_plan**|**bit**|計画は並行しています。 <br/>**注:** Azure SQL Data Warehouse は常に1を返します。|  
|**is_forced_plan**|**bit**|ユーザーがストアドプロシージャの**sp_query_store_force_plan**を実行するときに、Plan が forced とマークされます。 強制メカニズムでは、 **query_id**によって参照されるクエリに対してこのプランが確実に使用されることは*保証されません*。 プランの強制を実行すると、クエリが再コンパイルされ、通常は**plan_id**によって参照されるプランに対してまったく同じまたは類似したプランが生成されます。 プランの強制が成功しなかった場合、 **force_failure_count**がインクリメントされ、エラーの理由で**last_force_failure_reason**が設定されます。 <br/>**注:** Azure SQL Data Warehouse は常にゼロ (0) を返します。|  
|**is_natively_compiled**|**bit**|プランには、ネイティブコンパイルメモリ最適化プロシージャが含まれています。 (0 = FALSE、1 = TRUE)。 <br/>**注:** Azure SQL Data Warehouse は常にゼロ (0) を返します。|  
|**force_failure_count**|**bigint**|このプランを強制する回数が失敗しました。 クエリが再コンパイルされる (*すべての実行ではなく*) 場合にのみ、増分できます。 **Is_plan_forced**が**FALSE**から**TRUE**に変更されるたびに0にリセットされます。 <br/>**注:** Azure SQL Data Warehouse は常にゼロ (0) を返します。|  
|**last_force_failure_reason**|**通り**|プランの強制に失敗した理由。<br /><br /> 0: 失敗しません。それ以外の場合、強制に失敗する原因となったエラーのエラー番号<br /><br /> 8637: ONLINE_INDEX_BUILD<br /><br /> 8683: INVALID_STARJOIN<br /><br /> 8684: TIME_OUT<br /><br /> 8689: NO_DB<br /><br /> 8690: HINT_CONFLICT<br /><br /> 8691: SETOPT_CONFLICT<br /><br /> 8694: DQ_NO_FORCING_SUPPORTED<br /><br /> 8698: NO_PLAN<br /><br /> 8712: NO_INDEX<br /><br /> 8713: VIEW_COMPILE_FAILED<br /><br /> \<その他の値>: GENERAL_FAILURE <br/>**注:** Azure SQL Data Warehouse は常にゼロ (0) を返します。|  
|**last_force_failure_reason_desc**|**nvarchar(128)**|Last_force_failure_reason_desc の説明テキスト。<br /><br /> ONLINE_INDEX_BUILD: ターゲットテーブルにオンラインでビルドされているインデックスがあるときに、クエリでデータを変更しようとしています<br /><br /> INVALID_STARJOIN: プランに無効な StarJoin 仕様が含まれています<br /><br /> TIME_OUT: オプティマイザーによって指定されたプランを検索しているときに、オプティマイザーが許可された操作の数を超えました<br /><br /> NO_DB: プランに指定されたデータベースが存在しません<br /><br /> HINT_CONFLICT: プランがクエリヒントと競合するため、クエリをコンパイルできません<br /><br /> DQ_NO_FORCING_SUPPORTED: プランが分散クエリまたはフルテキスト操作の使用と競合しているため、クエリを実行できません。<br /><br /> NO_PLAN: クエリプロセッサはクエリプランを作成できませんでした。強制されたプランをクエリに対して有効であることを確認できませんでした<br /><br /> NO_INDEX: プランに指定されたインデックスは存在しません<br /><br /> VIEW_COMPILE_FAILED: プランで参照されているインデックス付きビューで問題が発生したため、クエリプランを強制できませんでした<br /><br /> GENERAL_FAILURE: 一般的なエラー (上記の理由では説明されていません) <br/>**注:** Azure SQL Data Warehouse は常に*NONE*を返します。|  
|**count_compiles**|**bigint**|コンパイルの統計を計画します。|  
|**initial_compile_start_time**|**datetimeoffset**|コンパイルの統計を計画します。|  
|**last_compile_start_time**|**datetimeoffset**|コンパイルの統計を計画します。|  
|**last_execution_time**|**datetimeoffset**|[最終実行時間] は、クエリ/プランの最後の終了時刻を示します。|  
|**avg_compile_duration**|**点**|コンパイルの統計を計画します。 <br/>**注:** Azure SQL Data Warehouse は常にゼロ (0) を返します。|  
|**last_compile_duration**|**bigint**|コンパイルの統計を計画します。 <br/>**注:** Azure SQL Data Warehouse は常にゼロ (0) を返します。|  
|**plan_forcing_type**|**通り**|プランの強制型。<br /><br />0: なし<br /><br />1: 手動<br /><br />2: AUTO|  
|**plan_forcing_type_desc**|**nvarchar (60)**|Plan_forcing_type の説明テキスト。<br /><br />NONE: プランの強制はありません<br /><br />手動: プランはユーザーによって強制される<br /><br />AUTO: 自動チューニングによって強制されるプラン|  

## <a name="plan-forcing-limitations"></a>プランの適用の制限事項
クエリ ストアには、クエリ オプティマイザーに特定の実行プランを使用させるためのメカニズムがあります。 ただし、適用の適用を妨げる可能性のある制限がいくつかあります。 

第 1 に、プランに次の構造が含まれる場合です。
* INSERT BULK ステートメント
* 外部テーブルの参照
* 分散クエリまたはフルテキスト操作
* グローバル クエリの使用 
* 動的カーソルまたはキーセットカーソル 
* 無効なスター結合の指定 

> [!NOTE]
> Azure SQL Database および SQL Server 2019 では、静的カーソルと高速転送カーソルに対するプランの強制がサポートされています。

第 2 に、プランが依存しているオブジェクトが使用できなくなった場合です。
* データベース (プランの基になっているデータベースが存在しなくなった場合)
* インデックス (存在しない場合、または無効になった場合)

最後に、プラン自体に問題がある場合です。
* クエリに対して有効ではない
* クエリ オプティマイザーが許可されている操作の数を超えた
* プランの XML の形式が正しくない

## <a name="permissions"></a>アクセス許可  
 **VIEW DATABASE STATE**権限が必要です。  
  
## <a name="see-also"></a>参照  
 [database_query_store_options &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [query_context_settings &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)   
 [query_store_query &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)   
 [query_store_query_text &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)   
 [query_store_runtime_stats &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-transact-sql.md)   
 [query_store_wait_stats &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)  
 [query_store_runtime_stats_interval &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)   
 [クエリストアを使用したパフォーマンスの監視](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [Transact-sql&#41;&#40;カタログビュー](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Transact-sql&#41;&#40;のストアドプロシージャのクエリストア](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)  
  
  
