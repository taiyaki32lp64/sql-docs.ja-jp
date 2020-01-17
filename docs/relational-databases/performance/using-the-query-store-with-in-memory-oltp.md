---
title: インメモリ OLTP でのクエリ ストアの使用 | Microsoft Docs
ms.custom: ''
ms.date: 03/29/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Query Store, in-memory
ms.assetid: aae5ae6d-7c90-4661-a1c5-df704319888a
author: julieMSFT
ms.author: jrasnick
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: db274ccde27abf92617e0eadf95b1971e740705a
ms.sourcegitcommit: c426c7ef99ffaa9e91a93ef653cd6bf3bfd42132
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/10/2019
ms.locfileid: "72251295"
---
# <a name="using-the-query-store-with-in-memory-oltp"></a>インメモリ OLTP でのクエリ ストアの使用
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] クエリ ストアでは、ネイティブ コンパイル コードのパフォーマンスを監視して、インメモリ OLTP で実行されているワークロードを確認することができます。  
コンパイルと実行時の統計情報が収集され、ディスク ベースのワークロードと同じように公開されます。   
インメモリ OLTP に移行しても、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] で引き続きクエリ ストア ビューを使用でき、移行前にディスク ベースのワークロード用に開発したカスタム スクリプトを使用することができます。 これにより、クエリ ストア テクノロジを学習するための投資を確保し、すべての種類のワークロードのトラブルシューティングで一般的に使用できるようになります。  
クエリ ストアの使用に関する一般情報については、「 [Monitoring Performance By Using the Query Store](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)」を参照してください。  
  
 インメモリ OLTP でクエリ ストアを使用する場合、追加の機能構成は必要ありません。 データベースで有効にすれば、すべての種類のワークロードで機能します。   
ただし、ユーザーがインメモリ OLTP でクエリ ストアを使用する際に注意する必要がある点がいくつかあります。  
  
-   クエリ ストアを有効にすると、クエリ、プランおよびコンパイル時の統計が既定で収集されます。 ただし、実行時統計の収集は、[sys.sp_xtp_control_query_exec_stats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-xtp-control-query-exec-stats-transact-sql.md) で明示的に有効にしない限り、アクティブになりません。  
  
-   *\@new_collection_value* を 0 に設定すると、クエリ ストアでの影響を受けるプロシージャまたは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンス全体の実行時統計の収集が停止されます。  
  
-   [sys.sp_xtp_control_query_exec_stats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-xtp-control-query-exec-stats-transact-sql.md) で構成された値は保持されません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の再起動後に、統計収集を確認し、再構成するようにしてください。  
  
-   通常のクエリ統計収集の場合と同じように、クエリ ストアを使用してワークロードの実行を追跡する際にパフォーマンスが低下する可能性があります。 ネイティブ コンパイル ストアド プロシージャの重要なサブセットに対してのみ、統計収集を有効にすることを検討してください。  
  
-   クエリとプランは最初のネイティブ コンパイルでキャプチャおよび格納され、再コンパイルのたびに更新されます。  
  
-   すべてのネイティブ ストアド プロシージャがコンパイルされてからクエリ ストアを有効にしたか、その内容をクリアした場合は、手動で再コンパイルし、クエリ ストアでキャプチャされるようにする必要があります。 [sp_query_store_remove_query &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-remove-query-transact-sql.md) または [sp_query_store_remove_plan &#40;Transct-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-remove-plan-transct-sql.md) を使用して手動でクエリを削除した場合も同様です。 [sp_recompile &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-recompile-transact-sql.md) を使用して、プロシージャを強制的に再コンパイルしてください。  
  
-   クエリ ストアではインメモリ OLTP のプラン生成メカニズムを活用して、コンパイル時にクエリ実行プランをキャプチャします。 ストアド プランは、 `SET SHOWPLAN_XML ON` を使用して取得するものと意味的には同じです。ただし、クエリ ストアのプランはステートメントごとに分割され、格納されます。  
    
-   混合ワークロードのデータベースでクエリ ストアを実行する場合は、[sys.query_store_plan &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md) の **is_natively_compiled** フィールドを使用して、ネイティブ コード コンパイルで生成されたクエリ プランをすばやく見つけることができます。  
  
-   クエリ ストアのキャプチャ モード (**ALTER TABLE** ステートメントの *QUERY_CAPTURE_MODE* パラメーター) が、ネイティブ コンパイル モジュールからのクエリに影響することはありません。構成値に関係なく、常にキャプチャされるためです。 これには `QUERY_CAPTURE_MODE = NONE`の設定も含まれます。  
  
-   クエリ ストアでキャプチャされるクエリ コンパイルの期間には、ネイティブ コードが生成される前に、クエリ最適化に要した時間のみが含まれます。 もっと正確に言うと、C コードのコンパイルおよび C コードの生成に必要な内部構造の生成に要した時間は含まれません。  
  
-   [sys.query_store_runtime_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-transact-sql.md) 内のメモリ許可メトリックは、ネイティブ コンパイル クエリでは設定されません。この値は常に 0 です。 メモリの許可の列は、avg_query_max_used_memory、last_query_max_used_memory、min_query_max_used_memory、max_query_max_used_memory、および stdev_query_max_used_memory です。  
  
## <a name="enabling-and-using-query-store-with-in-memory-oltp"></a>クエリ ストアを有効にしてインメモリ OLTP で使用する  
 エンド ツー エンド ユーザー シナリオでのクエリ ストアとインメモリ OLTP の簡単な使用例を以下に示します。 この例は、インメモリ OLTP に対してデータベース (`MemoryOLTP`) が有効になっていることを前提としています。  
    メモリ最適化テーブルの前提条件の詳細については、「 [メモリ最適化テーブルおよびネイティブ コンパイル ストアド プロシージャの作成](../../relational-databases/in-memory-oltp/creating-a-memory-optimized-table-and-a-natively-compiled-stored-procedure.md)」を参照してください。  
  
```  
USE MemoryOLTP;  
GO  
  
-- Create a simple memory-optimized table   
CREATE TABLE dbo.Ord  
   (OrdNo INTEGER not null PRIMARY KEY NONCLUSTERED,   
    OrdDate DATETIME not null,   
    CustCode NVARCHAR(5) not null)   
WITH (MEMORY_OPTIMIZED=ON);  
GO  
  
-- Enable Query Store before native module compilation  
ALTER DATABASE MemoryOLTP SET QUERY_STORE = ON;  
GO  
  
-- Create natively compiled stored procedure  
CREATE PROCEDURE dbo.OrderInsert(@OrdNo integer, @CustCode nvarchar(5))  
WITH NATIVE_COMPILATION, SCHEMABINDING  
AS   
    BEGIN ATOMIC WITH  
    (TRANSACTION ISOLATION LEVEL = SNAPSHOT,  
    LANGUAGE = N'English')  
  
    DECLARE @OrdDate DATETIME = GETDATE();  
    INSERT INTO dbo.Ord (OrdNo, CustCode, OrdDate)   
        VALUES (@OrdNo, @CustCode, @OrdDate);  
END;  
GO  
  
-- Enable runtime stats collection for queries from dbo.OrderInsert stored procedure  
DECLARE @db_id INT = DB_ID()  
DECLARE @proc_id INT = OBJECT_ID('dbo.OrderInsert');  
DECLARE @collection_enabled BIT;  
  
EXEC [sys].[sp_xtp_control_query_exec_stats] @new_collection_value = 1,   
    @database_id = @db_id, @xtp_object_id = @proc_id;  
  
-- Check the state of the collection flag  
EXEC sp_xtp_control_query_exec_stats @database_id = @db_id,   
    @xtp_object_id = @proc_id,   
    @old_collection_value= @collection_enabled output;  
SELECT @collection_enabled AS 'collection status';  
  
-- Execute natively compiled workload  
EXEC dbo.OrderInsert 1, 'A';  
EXEC dbo.OrderInsert 2, 'B';  
EXEC dbo.OrderInsert 3, 'C';  
EXEC dbo.OrderInsert 4, 'D';  
EXEC dbo.OrderInsert 5, 'E';  
  
-- Check Query Store Data  
-- Compile time data  
SELECT q.query_id, plan_id, object_id, query_hash, p.query_plan,  
    p.initial_compile_start_time, p.last_compile_start_time,   
    p.last_execution_time, p.avg_compile_duration,  
    p.last_force_failure_reason, p.force_failure_count  
FROM sys.query_store_query AS q  
JOIN sys.query_store_plan AS p   
    ON q.query_id = p.plan_id  
WHERE q.object_id = OBJECT_ID('dbo.OrderInsert');  
  
-- Get runtime stats  
-- Check count_executions field to verify that runtime statistics   
-- have been collected by the Query Store  
SELECT q.query_id, p.plan_id, object_id, rsi.start_time, rsi.end_time,    
    p.last_force_failure_reason, p.force_failure_count, rs.*  
FROM sys.query_store_query AS q  
JOIN sys.query_store_plan AS p   
    ON q.query_id = p.plan_id  
JOIN sys.query_store_runtime_stats AS rs   
    ON rs.plan_id = p.plan_id  
JOIN sys.query_store_runtime_stats_interval AS rsi   
    ON rs.runtime_stats_interval_id = rsi.runtime_stats_interval_id  
WHERE q.object_id = OBJECT_ID('dbo.OrderInsert');  
```  
  
## <a name="see-also"></a>参照  
 [Monitoring Performance By Using the Query Store](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [メモリ最適化テーブルおよびネイティブ コンパイル ストアド プロシージャの作成](../../relational-databases/in-memory-oltp/creating-a-memory-optimized-table-and-a-natively-compiled-stored-procedure.md)   
 [クエリ ストアを使用する際の推奨事項](../../relational-databases/performance/best-practice-with-the-query-store.md)   
 [クエリ ストアのストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)   
 [クエリ ストアのカタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md)  
  
  
