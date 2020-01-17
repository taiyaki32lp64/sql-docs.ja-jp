---
title: 拡張イベントを使用して、ロックが最も多いオブジェクトを検索する
ms.date: 10/18/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xevents
ms.topic: tutorial
helpviewer_keywords:
- objects [SQL Server], extended events
- xe
- extended events [SQL Server], locks
- objects [SQL Server], locks
ms.assetid: fcbadbda-c91c-43f0-a1b5-601e40110e07
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 66a28ef1b0f6dcd683097bcd6b8d38a07fe15204
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75234477"
---
# <a name="find-the-objects-that-have-the-most-locks-taken-on-them"></a>ロックの大半を取得しているオブジェクトを見つける

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

データベース管理者は、データベース パフォーマンスを低下させているロックのソースを特定しなければならないことがよくあります。  
  
たとえば、実稼動サーバーのボトルネックを監視しているとします。 競合の多いリソースがあるため、それらのオブジェクトで取得されているロックの数を調べようと思います。 最も頻繁にロックされているオブジェクトを特定できれば、競合するオブジェクトへのアクセスを最適化する手順を実行できます。  
  
そのためには、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]のクエリ エディターを使用します。  
  
### <a name="to-find-the-objects-that-have-the-most-locks"></a>ロックの大半を取得しているオブジェクトを見つけるには  
  
1. クエリ エディターで、次のステートメントを実行します。

    ```sql
    -- Find objects in a particular database that have the most
    -- lock acquired. This sample uses AdventureWorksDW2012.
    -- Create the session and add an event and target.
    
    IF EXISTS(SELECT * FROM sys.server_event_sessions WHERE name='LockCounts')
        DROP EVENT session LockCounts ON SERVER;
    GO
    DECLARE @dbid int;
  
    SELECT @dbid = db_id('AdventureWorksDW2012');
  
    DECLARE @sql nvarchar(1024);
    SET @sql = '
        CREATE event session LockCounts ON SERVER
            ADD EVENT sqlserver.lock_acquired (WHERE database_id ='
                + CAST(@dbid AS nvarchar) +')
            ADD TARGET package0.histogram(
                SET filtering_event_name=''sqlserver.lock_acquired'',
                    source_type=0, source=''resource_0'')';
  
    EXEC (@sql);
    GO
    ALTER EVENT session LockCounts ON SERVER
        STATE=start;
    GO
    -- Create a simple workload that takes locks.
    
    USE AdventureWorksDW2012;
    GO
    SELECT TOP 1 * FROM dbo.vAssocSeqLineItems;
    GO
    -- The histogram target output is available from the
    -- sys.dm_xe_session_targets dynamic management view in
    -- XML format.
    -- The following query joins the bucketizing target output with
    -- sys.objects to obtain the object names.
    
    SELECT name, object_id, lock_count
        FROM
        (
        SELECT objstats.value('.','bigint') AS lobject_id,
            objstats.value('@count', 'bigint') AS lock_count
            FROM (
                SELECT CAST(xest.target_data AS XML)
                    LockData
                FROM     sys.dm_xe_session_targets xest
                    JOIN sys.dm_xe_sessions        xes  ON xes.address = xest.event_session_address
                    JOIN sys.server_event_sessions ses  ON xes.name    = ses.name
                WHERE xest.target_name = 'histogram' AND xes.name = 'LockCounts'
                 ) Locks
            CROSS APPLY LockData.nodes('//HistogramTarget/Slot') AS T(objstats)
        ) LockedObjects
        INNER JOIN sys.objects o  ON LockedObjects.lobject_id = o.object_id
        WHERE o.type != 'S' AND o.type = 'U'
        ORDER BY lock_count desc;
    GO
    
    -- Stop the event session.
    
    ALTER EVENT SESSION LockCounts ON SERVER
        state=stop;
    GO
    ```

> [!NOTE]
> 上記の Transact-SQL コードの例は、オンプレミスの SQL Server で実行されますが、"_Azure SQL Database では完全には実行されない_" 可能性があります。 この例で、`ADD EVENT sqlserver.lock_acquired` など、イベントに直接関係している中核の部分は、Azure SQL Database でも機能します。 ただし、`sys.server_event_sessions` などの予備項目は、例を実行するために `sys.database_event_sessions` のように、対応する Azure SQL Database に編集する必要があります。
> オンプレミスの SQL Server と Azure SQL Database のこれらの軽微な違いの詳細については、次の記事を参照してください。
> - [Azure SQL Database での拡張イベント](/azure/sql-database/sql-database-xevent-db-diff-from-svr#transact-sql-differences)
> - [拡張イベントをサポートするシステム オブジェクト](xevents-references-system-objects.md)

上記の Transact-SQL スクリプトのステートメント実行が完了すると、クエリ エディターの **[結果]** タブに次の列が表示されます。
  
- name
- object_id
- lock_count
  
## <a name="see-also"></a>参照

[CREATE EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/create-event-session-transact-sql.md)  
[ALTER EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-event-session-transact-sql.md)  
[sys.dm_xe_session_targets &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xe-session-targets-transact-sql.md)  
[sys.dm_xe_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xe-sessions-transact-sql.md)  
[sys.server_event_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-event-sessions-transact-sql.md)  
