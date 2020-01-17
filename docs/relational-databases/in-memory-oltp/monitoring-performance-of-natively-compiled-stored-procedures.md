---
title: ネイティブ コンパイル ストアド プロシージャのパフォーマンスの監視
ms.custom: seo-dt-2019
ms.date: 04/03/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 55548cb2-77a8-4953-8b5a-f2778a4f13cf
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e16276b7b514d921261ea9b53af13162d0aa3b8b
ms.sourcegitcommit: 384e7eeb0020e17a018ef8087970038aabdd9bb7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/23/2019
ms.locfileid: "74412621"
---
# <a name="monitoring-performance-of-natively-compiled-stored-procedures"></a>ネイティブ コンパイル ストアド プロシージャのパフォーマンスの監視

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  この記事では、ネイティブ コンパイル ストアド プロシージャとその他のネイティブ コンパイル T-SQL モジュールのパフォーマンスを監視する方法を説明します。  
  
## <a name="using-extended-events"></a>拡張イベントの使用  
 クエリの実行をトレースするには、 **sp_statement_completed** 拡張イベントを使用します。 このイベントを使用して拡張イベント セッションを作成し、オプションで、特定のネイティブ コンパイル ストアド プロシージャに対応する object_id でフィルター処理を実行します。 各クエリの実行後に、拡張イベントが生成されます。 拡張イベントによって報告された CPU 時間と期間は、クエリが使用した CPU 時間と実行時間の長さを示します。 多くの CPU 時間を使用しているネイティブ コンパイル ストアド プロシージャには、パフォーマンスの問題が存在している可能性があります。  
  
 拡張イベント内の**line_number**と **object_id** を組み合わせて使用し、クエリを調査することができます。 次のクエリを使用して、プロシージャの定義を取得することができます。 行番号を使用して、定義内のクエリを特定できます:  
  
```sql  
SELECT [definition]
    from sys.sql_modules
    where object_id=object_id;
```  
  
  
## <a name="using-data-management-views-and-query-store"></a>データ管理ビューとクエリ ストアの使用
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] と [!INCLUDE[ssSDS](../../includes/sssds-md.md)] は、プロシージャ レベルとクエリ レベルの両方で、ネイティブ コンパイル ストアド プロシージャに関する実行の統計の収集をサポートしています。 パフォーマンスに与える影響が原因で、実行の統計の収集は既定では有効になっていません。  

実行統計は、[sys.dm_exec_procedure_stats](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md) および [sys.dm_exec_query_stats](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md) のシステム ビューと、[クエリ ストア](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)にも反映されます。

## <a name="procedure-level-execution-statistics"></a>プロシージャ レベルの実行統計

**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** :[sys.sp_xtp_control_proc_exec_stats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-xtp-control-proc-exec-stats-transact-sql.md) を使用して、プロシージャ レベルでネイティブ コンパイル ストアド プロシージャの統計コレクションを有効または無効にします。  次のステートメントは、現在のインスタンス上のすべてのネイティブ コンパイル T-SQL モジュールに対し、プロシージャ レベルの実行統計のコレクションを有効にします。
```sql
EXEC sys.sp_xtp_control_proc_exec_stats 1
```

**[!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]** :[database-scoped configuration](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md) オプション `XTP_PROCEDURE_EXECUTION_STATISTICS` を使用して、プロシージャ レベルでネイティブ コンパイル ストアド プロシージャの統計コレクションを有効または無効にします。 次のステートメントは、現在のデータベース内のすべてのネイティブ コンパイル T-SQL モジュールに対し、プロシージャ レベルの実行統計のコレクションを有効にします。
```sql
ALTER DATABASE
    SCOPED CONFIGURATION
    SET XTP_PROCEDURE_EXECUTION_STATISTICS = ON;
```

## <a name="query-level-execution-statistics"></a>クエリレベルの実行の統計

**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** :[sys.sp_xtp_control_query_exec_stats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-xtp-control-query-exec-stats-transact-sql.md) を使用して、クエリ レベルでネイティブ コンパイル ストアド プロシージャの統計コレクションを有効または無効にします。  次のステートメントは、現在のインスタンス上のすべてのネイティブ コンパイル T-SQL モジュールに対し、クエリ レベルの実行統計のコレクションを有効にします。
```sql
EXEC sys.sp_xtp_control_query_exec_stats 1
```

**[!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]** :[database-scoped configuration](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md) オプション `XTP_QUERY_EXECUTION_STATISTICS` を使用して、ステートメント レベルでネイティブ コンパイル ストアド プロシージャの統計コレクションを有効または無効にします。 次のステートメントは、現在のデータベース内のすべてのネイティブ コンパイル T-SQL モジュールに対し、クエリ レベルの実行統計のコレクションを有効にします。
```sql
ALTER DATABASE
    SCOPED CONFIGURATION
    SET XTP_QUERY_EXECUTION_STATISTICS = ON;
```

## <a name="sample-queries"></a>サンプル クエリ

 統計を収集した後、ネイティブ コンパイル ストアド プロシージャに関する実行の統計を要求するには、プロシージャに対して [sys.dm_exec_procedure_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md) を使用し、クエリに対して [sys.dm_exec_query_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md) を使用することが実行できます。  
 
  
 次のクエリは、統計コレクションを有効にした後、現在のデータベース内で実行されたネイティブ コンパイル ストアド プロシージャに関するプロシージャ名と実行の統計を返します。  

```sql
SELECT
        object_id,
        object_name(object_id) as 'object name',
        cached_time,
        last_execution_time,  execution_count,
        total_worker_time,    last_worker_time,
        min_worker_time,      max_worker_time,
        total_elapsed_time,   last_elapsed_time,
        min_elapsed_time,     max_elapsed_time
    from
        sys.dm_exec_procedure_stats
    where
        database_id = db_id()
        and
        object_id in
            (
            SELECT object_id
                from sys.sql_modules
                where uses_native_compilation=1
            )
    order by
        total_worker_time desc;
```

次のクエリは、統計コレクションが有効になっている現在のデータベースに対して実行されたネイティブ コンパイル ストアド プロシージャ内のすべてのクエリに対応するクエリ テキストと実行の統計を返し、合計ワーカー時間の降順に並べ替えます。  

```sql
SELECT
        st.objectid,
        object_name(st.objectid) as 'object name',
        SUBSTRING()
            st.text,
            (qs.statement_start_offset/2) + 1,
            ((qs.statement_end_offset-qs.statement_start_offset)/2) + 1
            ) as 'query text',
        qs.creation_time,
        qs.last_execution_time,   qs.execution_count,
        qs.total_worker_time,     qs.last_worker_time,
        qs.min_worker_time,       qs.max_worker_time,
        qs.total_elapsed_time,    qs.last_elapsed_time,
        qs.min_elapsed_time,      qs.max_elapsed_time
    FROM
                    sys.dm_exec_query_stats qs
        cross apply sys.dm_exec_sql_text(sql_handle) st
    WHERE
        st.dbid = db_id()
        and
        st.objectid in
            (SELECT object_id
                from sys.sql_modules
                where uses_native_compilation=1
            )
    ORDER BY
        qs.total_worker_time desc;
```

## <a name="query-execution-plans"></a>クエリ実行プラン

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
 [ネイティブ コンパイル ストアド プロシージャ](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)  
  
  
