---
title: ロックを保持しているクエリの特定
ms.date: 10/18/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xevents
ms.topic: tutorial
helpviewer_keywords:
- queries [SQL Server], extended events
- queries [SQL Server], holding locks
- xe
- extended events [SQL Server], locks
- extended events [SQL Server], holding locks
ms.assetid: bdfce092-3cf1-4b5e-99d5-fd8c6f9ad560
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: fa07161439f8536af056d8d99996d5c19242911e
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75234610"
---
# <a name="determine-which-queries-are-holding-locks"></a>ロックを保持しているクエリの特定

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

データベース管理者は、データベース パフォーマンスを低下させているロックのソースを特定しなければならないことがよくあります。  
  
たとえば、サーバーのパフォーマンスの問題が、ブロックに起因する可能性があるとします。 sys.dm_exec_requests に対してクエリを実行すると、複数のセッションが中断モードになっており、待機の種類から、ロックが待機対象のリソースとなっていることがわかりました。  
  
sys.dm_tran_locks に対してクエリを実行した結果、未解決のロックが多数存在しているにもかかわらず、ロックが許可されたセッションの sys.dm_exec_requests にアクティブな要求がないことがわかりました。  
  
次の例では、ロックが取得されたときのクエリ、クエリのプラン、および [!INCLUDE[tsql](../../includes/tsql-md.md)] スタックを特定する方法を示します。 さらに、拡張イベント セッションでのペアリング ターゲットの使用法も示します。  
  
この作業には、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] のクエリ エディターを使用した次の手順の実行も含まれます。  
  
> [!NOTE]  
>  この例では、AdventureWorks データベースを使用します。  
  
### <a name="to-determine-which-queries-are-holding-locks"></a>ロックを保持しているクエリを特定するには  
  
1.  クエリ エディターで、次のステートメントを実行します。  
  
    ```sql
    -- Perform cleanup.   
    IF EXISTS(SELECT * FROM sys.server_event_sessions WHERE name='FindBlockers')  
        DROP EVENT SESSION FindBlockers ON SERVER  
    GO  
    -- Use dynamic SQL to create the event session and allow creating a -- predicate on the AdventureWorks database id.  
    --  
    DECLARE @dbid int  
  
    SELECT @dbid = db_id('AdventureWorks')  
  
    IF @dbid IS NULL  
    BEGIN  
        RAISERROR('AdventureWorks is not installed. Install AdventureWorks before proceeding', 17, 1)  
        RETURN  
    END  
  
    DECLARE @sql nvarchar(1024)  
    SET @sql = '  
    CREATE EVENT SESSION FindBlockers ON SERVER  
    ADD EVENT sqlserver.lock_acquired   
        (action   
            ( sqlserver.sql_text, sqlserver.database_id, sqlserver.tsql_stack,  
             sqlserver.plan_handle, sqlserver.session_id)  
        WHERE ( database_id=' + cast(@dbid as nvarchar) + ' AND resource_0!=0)   
        ),  
    ADD EVENT sqlserver.lock_released   
        (WHERE ( database_id=' + cast(@dbid as nvarchar) + ' AND resource_0!=0 ))  
    ADD TARGET package0.pair_matching   
        ( SET begin_event=''sqlserver.lock_acquired'',   
                begin_matching_columns=''database_id, resource_0, resource_1, resource_2, transaction_id, mode'',   
                end_event=''sqlserver.lock_released'',   
                end_matching_columns=''database_id, resource_0, resource_1, resource_2, transaction_id, mode'',  
        respond_to_memory_pressure=1)  
    WITH (max_dispatch_latency = 1 seconds)'  
  
    EXEC (@sql)  
    --   
    -- Create the metadata for the event session  
    -- Start the event session  
    --  
    ALTER EVENT SESSION FindBlockers ON SERVER  
    STATE = START  
    ```  
  
2.  サーバーでワークロードを実行したら、クエリ エディターで次のステートメントを実行して、ロックを保持しているクエリを見つけます。  
  
    ```sql
    --  
    -- The pair matching targets report current unpaired events using   
    -- the sys.dm_xe_session_targets dynamic management view (DMV)  
    -- in XML format.  
    -- The following query retrieves the data from the DMV and stores  
    -- key data in a temporary table to speed subsequent access and  
    -- retrieval.  
    --  
    SELECT   
    objlocks.value('(action[@name="session_id"]/value)[1]', 'int')  
            AS session_id,  
        objlocks.value('(data[@name="database_id"]/value)[1]', 'int')   
            AS database_id,  
        objlocks.value('(data[@name="resource_type"]/text)[1]', 'nvarchar(50)' )   
            AS resource_type,  
        objlocks.value('(data[@name="resource_0"]/value)[1]', 'bigint')   
            AS resource_0,  
        objlocks.value('(data[@name="resource_1"]/value)[1]', 'bigint')   
            AS resource_1,  
        objlocks.value('(data[@name="resource_2"]/value)[1]', 'bigint')   
            AS resource_2,  
        objlocks.value('(data[@name="mode"]/text)[1]', 'nvarchar(50)')   
            AS mode,  
        objlocks.value('(action[@name="sql_text"]/value)[1]', 'varchar(MAX)')   
            AS sql_text,  
        CAST(objlocks.value('(action[@name="plan_handle"]/value)[1]', 'varchar(MAX)') AS xml)   
            AS plan_handle,      
        CAST(objlocks.value('(action[@name="tsql_stack"]/value)[1]', 'varchar(MAX)') AS xml)   
            AS tsql_stack  
    INTO #unmatched_locks  
    FROM (  
        SELECT CAST(xest.target_data as xml)   
            lockinfo  
        FROM sys.dm_xe_session_targets xest  
        JOIN sys.dm_xe_sessions xes ON xes.address = xest.event_session_address  
        WHERE xest.target_name = 'pair_matching' AND xes.name = 'FindBlockers'  
    ) heldlocks  
    CROSS APPLY lockinfo.nodes('//event[@name="lock_acquired"]') AS T(objlocks)  
  
    --  
    -- Join the data acquired from the pairing target with other   
    -- DMVs to return provide additional information about blockers  
    --  
    SELECT ul.*  
        FROM #unmatched_locks ul  
        INNER JOIN sys.dm_tran_locks tl ON ul.database_id = tl.resource_database_id AND ul.resource_type = tl.resource_type  
        WHERE resource_0 IS NOT NULL  
        AND session_id IN   
            (SELECT blocking_session_id FROM sys.dm_exec_requests WHERE blocking_session_id != 0)  
        AND tl.request_status='wait'  
        AND REPLACE(ul.mode, 'LCK_M_', '' ) = tl.request_mode  
  
    ```  
  
3.  問題を特定したら、一時テーブルとイベント セッションを削除します。  
  
    ```sql
    DROP TABLE #unmatched_locks  
    DROP EVENT SESSION FindBlockers ON SERVER  
    ```  

> [!NOTE]
> 上記の Transact-SQL コードの例は、オンプレミスの SQL Server で実行されますが、"_Azure SQL Database では完全には実行されない_" 可能性があります。 この例で、`ADD EVENT sqlserver.lock_acquired` など、イベントに直接関係している中核の部分は、Azure SQL Database でも機能します。 ただし、`sys.server_event_sessions` などの予備項目は、例を実行するために `sys.database_event_sessions` のように、対応する Azure SQL Database に編集する必要があります。
> オンプレミスの SQL Server と Azure SQL Database のこれらの軽微な違いの詳細については、次の記事を参照してください。
> - [Azure SQL Database での拡張イベント](/azure/sql-database/sql-database-xevent-db-diff-from-svr#transact-sql-differences)
> - [拡張イベントをサポートするシステム オブジェクト](xevents-references-system-objects.md)

## <a name="see-also"></a>参照  
 [CREATE EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/create-event-session-transact-sql.md)   
 [ALTER EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-event-session-transact-sql.md)   
 [DROP EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-event-session-transact-sql.md)   
 [sys.dm_xe_session_targets &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xe-session-targets-transact-sql.md)   
 [sys.dm_xe_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xe-sessions-transact-sql.md)  
  
  
