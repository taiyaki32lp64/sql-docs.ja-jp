---
title: dm_exec_query_profiles (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 10/25/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_exec_query_profiles_TSQL
- sys.dm_exec_query_profiles_TSQL
- dm_exec_query_profiles
- sys.dm_exec_query_profiles
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_query_profiles dynamic management view
ms.assetid: 54efc6cb-eea8-4f6d-a4d0-aa05eeb54081
author: stevestein
ms.author: sstein
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: cd30a6c07bccde04bb38189fab00f688dd763356
ms.sourcegitcommit: f018eb3caedabfcde553f9a5fc9c3e381c563f1a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2019
ms.locfileid: "74165498"
---
# <a name="sysdm_exec_query_profiles-transact-sql"></a>sys.dm_exec_query_profiles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

クエリの実行中にリアルタイムでクエリの進行状況を監視します。 たとえば、この DMV を使用して、クエリのどの部分が低速で実行されているかを判断します。 この DMV をシステムの他の DMV と結合するには、説明フィールドで特定されている列を使用します。 または、timestamp 列を使用して、この DMV を他のパフォーマンスカウンター (Performance Monitor、xperf など) に結合します。  
  
## <a name="table-returned"></a>返されるテーブル  
返されるカウンターは、スレッドごとの演算子ごとになります。 結果は動的であり、クエリの終了時にのみ出力を作成する `SET STATISTICS XML ON` などの既存のオプションの結果とは一致しません。  
  
|列名|データ型|[説明]|  
|-----------------|---------------|-----------------|  
|session_id|**smallint**|このクエリが実行されるセッションを識別します。 dm_exec_sessions.session_id を参照します。|  
|request_id|**int**|ターゲット要求を識別します。 Dm_exec_sessions を参照しています。 request_id。|  
|sql_handle|**varbinary(64)**|クエリが含まれているバッチまたはストアドプロシージャを一意に識別するトークンです。 Dm_exec_query_stats を参照しています。 sql_handle。|  
|plan_handle|**varbinary(64)**|は、実行され、そのプランがプランキャッシュに存在するか、現在実行中のバッチのクエリ実行プランを一意に識別するトークンです。 Dm_exec_query_stats を参照しています。 plan_handle。|  
|physical_operator_name|**nvarchar (256)**|物理操作名。|  
|node_id|**int**|クエリ ツリー内の演算子ノードを識別します。|  
|thread_id|**int**|同じクエリ演算子ノードに属している (並列クエリの) スレッドを識別します。|  
|task_address|**varbinary(8)**|このスレッドが使用している SQLOS タスクを識別します。 Dm_os_tasks を参照しています。 task_address。|  
|row_count|**bigint**|これまでに演算子によって返された行の数。|  
|rewind_count|**bigint**|これまでの巻き戻しの数。|  
|rebind_count|**bigint**|これまでの再バインドの数。|  
|end_of_scan_count|**bigint**|これまでのスキャンの終了の数。|  
|estimate_row_count|**bigint**|予測行数。 実際の row_count に estimated_row_count と比較すると便利な場合があります。|  
|first_active_time|**bigint**|演算子が最初に呼び出されたときの時間 (ミリ秒単位)。|  
|last_active_time|**bigint**|演算子が最後に呼び出された時刻 (ミリ秒単位)。|  
|open_time|**bigint**|開いたときのタイムスタンプ (ミリ秒単位)。|  
|first_row_time|**bigint**|最初の行が開かれたときのタイムスタンプ (ミリ秒単位)。|  
|last_row_time|**bigint**|最後の行を開いたときのタイムスタンプ (ミリ秒単位)。|  
|close_time|**bigint**|終了時のタイムスタンプ (ミリ秒単位)。|  
|elapsed_time_ms|**bigint**|これまでのターゲットノードの操作で使用された経過時間の合計 (ミリ秒単位)。|  
|cpu_time_ms|**bigint**|これまでのターゲットノードの操作で使用された合計 CPU 時間 (ミリ秒)。|  
|database_id|**smallint**|読み取りおよび書き込みが実行されたオブジェクトを含むデータベースの ID。|  
|object_id|**int**|読み取りおよび書き込みが実行されたオブジェクトの識別子。 sys.objects.object_id を参照します。|  
|index_id|**int**|行セットが開かれている対象のインデックス (ある場合)。|  
|scan_count|**bigint**|これまでのテーブル/インデックス スキャンの数。|  
|logical_read_count|**bigint**|これまでの論理読み取りの数。|  
|physical_read_count|**bigint**|これまでの物理読み取りの数。|  
|read_ahead_count|**bigint**|これまでの先読みの数。|  
|write_page_count|**bigint**|書き込むによるこれまでのページ書き込み回数。|  
|lob_logical_read_count|**bigint**|これまでの LOB 論理読み取り数。|  
|lob_physical_read_count|**bigint**|これまでの LOB 物理読み取りの数。|  
|lob_read_ahead_count|**bigint**|これまでの LOB 先読みの数。|  
|segment_read_count|**int**|これまでのセグメント先行読み取りの数。|  
|segment_skip_count|**int**|これまでにスキップされたセグメントの数。| 
|actual_read_row_count|**bigint**|残存述語が適用される前に演算子によって読み取られた行の数。| 
|estimated_read_row_count|**bigint**|**適用対象:** [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] SP1 以降。 <br/>残存述語が適用される前に、演算子によって読み取られると推定される行の数。|  
  
## <a name="general-remarks"></a>全般的な解説  
 [クエリプラン] ノードに i/o がない場合は、i/o 関連のすべてのカウンターが NULL に設定されます。  
  
 この DMV によって報告される i/o 関連のカウンターは、次の2つの方法で `SET STATISTICS IO` によって報告されたものよりも詳細です。  
  
-   `SET STATISTICS IO` は、指定されたテーブルに対するすべての i/o のカウンターをグループ化します。 この DMV では、テーブルに対して i/o を実行するクエリプラン内のすべてのノードに対して個別のカウンターを取得します。  
  
-   並列スキャンがある場合、この DMV では、スキャンで使用される並列スレッドごとにカウンターがレポートされます。
 
[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 以降では、*標準のクエリ実行統計プロファイルインフラストラクチャ*が、*軽量のクエリ実行統計プロファイルインフラストラクチャ*とサイドバイサイドで存在します。 `SET STATISTICS XML ON` と `SET STATISTICS PROFILE ON` は常に*標準のクエリ実行統計プロファイルインフラストラクチャ*を使用します。 `sys.dm_exec_query_profiles` に設定するには、クエリプロファイルインフラストラクチャの1つを有効にする必要があります。 詳細については、「[クエリ プロファイリング インフラストラクチャ](../../relational-databases/performance/query-profiling-infrastructure.md)」を参照してください。    

>[!NOTE]
> 調査対象のクエリは、クエリのプロファイルインフラストラクチャが有効になっ**た後**に開始する必要があります。これを有効にすると、クエリの開始後に、`sys.dm_exec_query_profiles`で結果が生成されなくなります。 クエリプロファイルインフラストラクチャを有効にする方法の詳細については、「[クエリプロファイリングインフラストラクチャ](../../relational-databases/performance/query-profiling-infrastructure.md)」を参照してください。

## <a name="permissions"></a>アクセス許可  
[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] および [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] マネージインスタンスでは、`VIEW DATABASE STATE` 権限と `db_owner` データベースロールのメンバーシップが必要です。   
[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] Premium レベルでは、データベースの `VIEW DATABASE STATE` アクセス許可が必要です。 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] Standard レベルと Basic レベルでは、**サーバー管理**者または**Azure Active Directory 管理者**アカウントが必要です。   
   
## <a name="examples"></a>使用例  
 手順 1: `sys.dm_exec_query_profiles`で分析するクエリの実行を計画しているセッションにログインします。 プロファイル用のクエリを構成するには `SET STATISTICS PROFILE ON`を使用します。 同じセッションでクエリを実行します。  
  
```sql  
--Configure query for profiling with sys.dm_exec_query_profiles  
SET STATISTICS PROFILE ON;  
GO  

--Or enable query profiling globally under SQL Server 2016 SP1 or above (not needed in SQL Server 2019)  
DBCC TRACEON (7412, -1);  
GO 
  
--Next, run your query in this session, or in any other session if query profiling has been enabled globally 
```  
  
 手順 2: クエリが実行されているセッションとは異なる2番目のセッションにログインします。  
  
 次のステートメントは、セッション54で現在実行されているクエリの進行状況をまとめたものです。 これを行うには、各ノードのすべてのスレッドから出力行の合計数を計算し、そのノードの出力行数の予測値と比較します。  
  
```sql  
--Run this in a different session than the session in which your query is running. 
--Note that you may need to change session id 54 below with the session id you want to monitor.
SELECT node_id,physical_operator_name, SUM(row_count) row_count, 
  SUM(estimate_row_count) AS estimate_row_count, 
  CAST(SUM(row_count)*100 AS float)/SUM(estimate_row_count)  
FROM sys.dm_exec_query_profiles   
WHERE session_id=54
GROUP BY node_id,physical_operator_name  
ORDER BY node_id;  
```  
  
## <a name="see-also"></a>参照  
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [実行関連の動的管理ビューおよび関数 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)  
 
