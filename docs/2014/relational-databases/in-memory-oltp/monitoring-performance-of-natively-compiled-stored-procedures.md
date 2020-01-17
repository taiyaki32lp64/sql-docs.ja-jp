---
title: ネイティブ コンパイル ストアド プロシージャのパフォーマンスの監視 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 55548cb2-77a8-4953-8b5a-f2778a4f13cf
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 9b8d6f35f8dedeb4539dc8299ca32f6566beb03f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63161953"
---
# <a name="monitoring-performance-of-natively-compiled-stored-procedures"></a>ネイティブ コンパイル ストアド プロシージャのパフォーマンスの監視
  このトピックでは、ネイティブ コンパイル ストアド プロシージャのパフォーマンスを監視する方法を説明します。  
  
## <a name="using-extended-events"></a>拡張イベントの使用  
 クエリの実行をトレースするには、`sp_statement_completed` 拡張イベントを使用します。 このイベントを使用して拡張イベント セッションを作成し、オプションで、特定のネイティブ コンパイル ストアド プロシージャに対応する object_id でフィルター処理を実行します。各クエリの実行後に、拡張イベントが生成されます。 拡張イベントによって報告された CPU 時間と期間は、クエリが使用した CPU 時間と実行時間の長さを示します。 多くの CPU 時間を使用しているネイティブ コンパイル ストアド プロシージャには、パフォーマンスの問題が存在している可能性があります。  
  
 拡張イベント内の `line_number` と `object_id` を組み合わせて使用し、クエリを調査することができます。 次のクエリを使用して、プロシージャの定義を取得することができます。 行番号を使用して、定義内のクエリを特定できます:  
  
```sql  
select [definition] from sys.sql_modules where object_id=object_id  
```  
  
 詳細については、`sp_statement_completed`イベントを拡張するを参照してください[イベントの原因となったステートメントを取得する方法](https://blogs.msdn.com/b/extended_events/archive/2010/05/07/making-a-statement-how-to-retrieve-the-t-sql-statement-that-caused-an-event.aspx)します。  
  
## <a name="using-data-management-views"></a>データ管理ビューの使用  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、プロシージャ レベルとクエリ レベルの両方で、ネイティブ コンパイル ストアド プロシージャに関する実行の統計の収集をサポートしています。 パフォーマンスに与える影響が原因で、実行の統計の収集は既定では有効になっていません。  
  
 ネイティブ コンパイル ストアド プロシージャに対する統計コレクションは、[sys.sp_xtp_control_proc_exec_stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-control-proc-exec-stats-transact-sql) を使用して有効化または無効化することができます。  
  
 [sys.sp_xtp_control_proc_exec_stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-control-proc-exec-stats-transact-sql) で統計コレクションを有効にすると、[sys.dm_exec_procedure_stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql) を使用してネイティブ コンパイル ストアド プロシージャのパフォーマンスを監視することができます。  
  
 [sys.sp_xtp_control_query_exec_stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-control-query-exec-stats-transact-sql) で統計コレクションを有効にすると、[sys.dm_exec_query_stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql) を使用してネイティブ コンパイル ストアド プロシージャのパフォーマンスを監視することができます。  
  
 収集を開始するには、統計コレクションを有効にします。 次に、ネイティブ コンパイル ストアド プロシージャを実行します。 収集を終了するには、統計コレクションを無効にします。 次に、DMV によって返された実行の統計を分析します。  
  
 統計を収集した後、ネイティブ コンパイル ストアド プロシージャに関する実行の統計を要求するには、プロシージャに対して [sys.dm_exec_procedure_stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql) を使用し、クエリに対して [sys.dm_exec_query_stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql) を使用することが実行できます。  
  
> [!NOTE]  
>  ネイティブ コンパイル ストアド プロシージャに対する統計コレクションが有効になっている場合は、ワーカー時間がミリ秒単位で収集されます。 クエリが 1 ミリ秒未満で実行された場合は、値は 0 になります。 ネイティブ コンパイル ストアド プロシージャに関して、多くの実行が 1 ミリ秒未満である場合は、 **total_worker_time** は精度が高くない可能性があります。  
  
 次のクエリは、統計コレクションを有効にした後、現在のデータベース内で実行されたネイティブ コンパイル ストアド プロシージャに関するプロシージャ名と実行の統計を返します。  
  
```sql  
select object_id,  
       object_name(object_id) as 'object name',  
       cached_time,  
       last_execution_time,  
       execution_count,  
       total_worker_time,  
       last_worker_time,  
       min_worker_time,  
       max_worker_time,  
       total_elapsed_time,  
       last_elapsed_time,  
       min_elapsed_time,  
       max_elapsed_time   
from sys.dm_exec_procedure_stats  
where database_id=db_id() and object_id in (select object_id   
from sys.sql_modules where uses_native_compilation=1)  
order by total_worker_time desc  
```  
  
 次のクエリは、統計コレクションが有効になっている現在のデータベースに対して実行されたネイティブ コンパイル ストアド プロシージャ内のすべてのクエリに対応するクエリ テキストと実行の統計を返し、合計ワーカー時間の降順に並べ替えます。  
  
```sql  
select st.objectid,   
       object_name(st.objectid) as 'object name',   
       SUBSTRING(st.text, (qs.statement_start_offset/2) + 1, ((qs.statement_end_offset-qs.statement_start_offset)/2) + 1) as 'query text',   
       qs.creation_time,  
       qs.last_execution_time,  
       qs.execution_count,  
       qs.total_worker_time,  
       qs.last_worker_time,  
       qs.min_worker_time,  
       qs.max_worker_time,  
       qs.total_elapsed_time,  
       qs.last_elapsed_time,  
       qs.min_elapsed_time,  
       qs.max_elapsed_time  
from sys.dm_exec_query_stats qs cross apply sys.dm_exec_sql_text(sql_handle) st  
where  st.dbid=db_id() and st.objectid in (select object_id   
from sys.sql_modules where uses_native_compilation=1)  
order by qs.total_worker_time desc  
```  
  
 ネイティブ コンパイル ストアド プロシージャでは、SHOWPLAN_XML (推定実行プラン) がサポートされています。 推定実行プランを使用してクエリ プランを調査し、不適切なプランの問題を見つけることができます。 不適切なプランの一般的な理由は次のとおりです。  
  
-   プロシージャを作成する前に統計を更新していません。  
  
-   欠落したインデックス  
  
 Showplan XML を取得するには、次の [!INCLUDE[tsql](../../includes/tsql-md.md)]を実行します。  
  
```sql  
SET SHOWPLAN_XML ON  
GO  
EXEC my_proc   
GO  
SET SHOWPLAN_XML OFF  
GO  
```  
  
 代わりに、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]でプロシージャ名を選択し、 **[推定実行プランの表示]** をクリックすることもできます。  
  
 ネイティブ コンパイル ストアド プロシージャに対応する推定実行プランでは、プロシージャ内に存在するクエリに関するクエリ演算子と式が表示されます。 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] では、ネイティブ コンパイル ストアド プロシージャに対して、すべての SHOWPLAN_XML をサポートしているわけではありません。 たとえば、クエリ オプティマイザー コストに関連する属性は、プロシージャに対応する SHOWPLAN_XML の一部ではありません。  
  
## <a name="see-also"></a>参照  
 [ネイティブ コンパイル ストアド プロシージャ](natively-compiled-stored-procedures.md)  
  
  
