---
title: SQL トレース スクリプトから拡張イベント セッションへの変換
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xevents
ms.topic: tutorial
helpviewer_keywords:
- SQL Trace, convert script to extended events
- extended events [SQL Server], convert SQL Trace script
ms.assetid: 4c8f29e6-0a37-490f-88b3-33493871b3f9
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b41947e50cd2cdd283af77a8d3ee4168f208f57e
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75255755"
---
# <a name="convert-an-existing-sql-trace-script-to-an-extended-events-session"></a>既存の SQL トレース スクリプトから拡張イベント セッションへの変換

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  拡張イベント セッションに変換する SQL トレース スクリプトが既に手元にある場合は、このトピックの手順を使用して、等価な拡張イベント セッションを作成できます。 変換を実行するために必要な情報は、trace_xe_action_map および trace_xe_event_map システム テーブル内の情報を使用して収集できます。  
  
 手順は次のとおりです。  
  
1.  既存のスクリプトを実行して SQL トレース セッションを作成し、トレースの ID を取得します。  
  
2.  fn_trace_geteventinfo 関数を使用したクエリを実行して、SQL トレース イベント クラスとそれに関連付けられた列ごとに、等価な拡張イベントおよびアクションを探します。  
  
3.  使用するフィルターおよび等価な拡張イベントのアクションを、fn_trace_getfilterinfo 関数を使用して特定します。  
  
4.  拡張イベントにおける等価なイベント、アクション、および述語 (フィルター) を使用して、拡張イベント セッションを手動で作成します。  

## <a name="to-obtain-the-trace-id"></a>トレース ID を取得するには  
  
1.  クエリ エディターで SQL トレース スクリプトを開き、スクリプトを実行してトレース セッションを作成します。 この手順を実行するために必ずしもトレース セッションが実行されている必要はありません。  
  
2.  トレースの ID を取得します。 そのためには、次のクエリを使用します。  
  
    ```sql
    SELECT * FROM sys.traces;  
    GO  
    ```  
  
    > [!NOTE]  
    >  トレース ID 1 は通常、既定のトレースを示します。  
  
## <a name="to-determine-the-extended-events-equivalents"></a>等価な拡張イベントを特定するには  
  
1.  拡張イベントにおける等価なイベントとアクションを特定するには、次のクエリを実行します。 *trace_id* は、前の手順で取得したトレース ID の値に設定されています。  
  
    > [!NOTE]  
    >  この例では、既定のトレースの ID (1) が使用されます。  
  
    ```sql
    USE MASTER;  
    GO  
    DECLARE @trace_id int;  
    SET @trace_id = 1;  
    SELECT DISTINCT el.eventid, em.package_name, em.xe_event_name AS 'event'  
       , el.columnid, ec.xe_action_name AS 'action'  
    FROM (sys.fn_trace_geteventinfo(@trace_id) AS el  
       LEFT OUTER JOIN sys.trace_xe_event_map AS em  
          ON el.eventid = em.trace_event_id)  
    LEFT OUTER JOIN sys.trace_xe_action_map AS ec  
       ON el.columnid = ec.trace_column_id  
    WHERE em.xe_event_name IS NOT NULL AND ec.xe_action_name IS NOT NULL;  
    ```  
  
     拡張イベントにおける等価なイベント ID、パッケージ名、イベント名、列 ID、およびアクション名が返されます。 この出力結果は、このトピックの「拡張イベント セッションを作成するには」の手順で使用します。  
  
     場合によっては、フィルター選択された列が、既定で含まれているイベント データ フィールドにマップされていることも考えられます。 このとき、"Extended_Events_action_name" 列は NULL になります。 この場合、次の手順に従って、フィルター選択された列に対応するデータ フィールドを特定する必要があります。  
  
    1.  NULL を返すアクションに関して、スクリプト内のどの SQL トレース イベント クラスに、フィルター選択の対象となる列が含まれているかを特定します。  
  
         たとえば、イベント クラス SP:StmtCompleted を使用し、トレース列名 Duration に対するフィルターを指定したとします (SQL トレース イベント クラス ID が 45 で、SQL トレースの列 ID が 13)。 この場合、クエリの結果には、アクション名が NULL として表示されます。  
  
    2.  前の手順で特定した SQL トレース イベント クラスごとに、拡張イベントにおける等価なイベント名を探します。 (等価なイベント名がわからない場合は、「 [SQL トレースのイベント クラスと等価な拡張イベントを確認する](../../relational-databases/extended-events/view-the-extended-events-equivalents-to-sql-trace-event-classes.md)」のトピックに記載されているクエリを使用してください。)。  
  
    3.  次のクエリを使用して、前の手順で判明したイベントに使用する適切なデータ フィールドを特定します。 このクエリでは、拡張イベントのデータ フィールドが "event_field" 列に反映されます。 クエリ内の *<event_name>* は、前の手順で指定したイベントの名前に置き換えてください。  
  
        ```sql
        SELECT xp.name package_name, xe.name event_name  
           ,xc.name event_field, xc.description  
        FROM sys.trace_xe_event_map AS em  
        INNER JOIN sys.dm_xe_objects AS xe  
           ON em.xe_event_name = xe.name  
        INNER JOIN sys.dm_xe_packages AS xp  
           ON xe.package_guid = xp.guid AND em.package_name = xp.name  
        INNER JOIN sys.dm_xe_object_columns AS xc  
           ON xe.name = xc.object_name  
        WHERE xe.object_type = 'event' AND xc.column_type <> 'readonly'  
           AND em.xe_event_name = '<event_name>';  
        ```  
  
         たとえば、SP:StmtCompleted イベント クラスは、sp_statement_completed 拡張イベントに対応します。 クエリの中で、イベント名として sp_statement_completed を指定した場合、そのイベントに既定で含まれているフィールドが "event_field" 列に表示されます。 これらのフィールドを見ると、"duration" というフィールドが存在するのがわかります。 等価な拡張イベント セッションにフィルターを作成するには、"WHERE duration > 0" などの述語を追加します。 例については、このトピックの「拡張イベント セッションを作成するには」の手順を参照してください。  
  
## <a name="to-create-the-extended-events-session"></a>拡張イベント セッションを作成するには  
 クエリ エディターを使用して拡張イベント セッションを作成し、出力結果をファイル ターゲットに書き込みます。 以降の手順は、単一のクエリについて記述したものです。クエリの実際の作成方法を交えて説明しています。 クエリ全体の例については、このトピックの「使用例」のセクションを参照してください。  
  
1.  イベント セッションを作成するためのステートメントを追加します。*session_name* の部分は、拡張イベント セッションに使用する名前に置き換えてください。  
  
    ```sql
    IF EXISTS(SELECT * FROM sys.server_event_sessions WHERE name='session_name')  
       DROP EVENT SESSION [Session_Name] ON SERVER;  
    CREATE EVENT SESSION [Session_Name]  
    ON SERVER;  
    ```  
  
2.  「等価な拡張イベントを特定するには」の手順の出力結果として返された拡張イベントのイベントとアクションを追加し、「スクリプトに使用されているフィルターを特定するには」の手順で特定した述語 (フィルター) を追加します。  
  
     次の例には、SQL:StmtStarting イベント クラスと SP:StmtCompleted イベント クラス、さらに、セッションの ID と実行時間 (duration) のフィルターを含んだ SQL トレース スクリプトが使用されています。 「等価な拡張イベントを特定するには」の手順で紹介したクエリのサンプル出力では、次の結果セットが返されます。  
  
    ```  
    Eventid  package_name  event                   columnid  action  
    44       sqlserver     sp_statement_starting   6         nt_username  
    44       sqlserver     sp_statement_starting   9         client_pid  
    44       sqlserver     sp_statement_starting   10        client_app_name  
    44       sqlserver     sp_statement_starting   11        server_principal_name  
    44       sqlserver     sp_statement_starting   12        session_id  
    45       sqlserver     sp_statement_completed  6         nt_username  
    45       sqlserver     sp_statement_completed  9         client_pid  
    45       sqlserver     sp_statement_completed  10        client_app_name  
    45       sqlserver     sp_statement_completed  11        server_principal_name  
    45       sqlserver     sp_statement_completed  12        session_id  
    ```  
  
     これを等価な拡張イベントに変換するには、sqlserver.sp_statement_starting イベントと sqlserver.sp_statement_completed events イベントを一連のアクションと共に追加します。 述語のステートメントは、WHERE 句として追加されています。  
  
    ```sql
    ADD EVENT sqlserver.sp_statement_starting  
       (ACTION  
          (  
          sqlserver.nt_username,  
          sqlserver.client_pid,  
          sqlserver.client_app_name,  
          sqlserver.server_principal_name,  
          sqlserver.session_id  
          )  
       WHERE sqlserver.session_id = 59   
       ),  
  
    ADD EVENT sqlserver.sp_statement_completed  
       (ACTION  
          (  
          sqlserver.nt_username,  
          sqlserver.client_pid,  
          sqlserver.client_app_name,  
          sqlserver.server_principal_name,  
          sqlserver.session_id  
          )  
       WHERE sqlserver.session_id = 59 AND duration > 0  
       )  
    ```  
  
3.  非同期のファイル ターゲットを追加します。ファイル パスは、出力結果の実際の保存場所に置き換えてください。 ファイル ターゲットを指定するときは、ログ ファイルとメタデータ ファイルのパス ファイルを含める必要があります。  
  
    ```sql
    ADD TARGET package0.asynchronous_file_target(  
       SET filename='c:\temp\ExtendedEventsStoredProcs.xel', metadatafile='c:\temp\ExtendedEventsStoredProcs.xem');  
    ```  
  
## <a name="to-view-the-results"></a>結果を表示するには  
  
1.  出力結果は、sys.fn_xe_file_target_read_file 関数を使用して表示できます。 そのためには、次のクエリを実行します。ファイル パスは、実際に指定したパスに置き換えてください。  
  
    ```sql
    SELECT *, CAST(event_data as XML) AS 'event_data_XML'  
    FROM sys.fn_xe_file_target_read_file('c:\temp\ExtendedEventsStoredProcs*.xel', 'c:\temp\ExtendedEventsStoredProcs*.xem', NULL, NULL);  
  
    ```  
  
    > [!NOTE]  
    >  イベント データを XML としてキャストしていますが、これは任意です。  
  
     sys.fn_xe_file_target_read_file 関数の詳細については、「[sys.fn_xe_file_target_read_file &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-xe-file-target-read-file-transact-sql.md)」を参照してください。  
  
    ```sql
    IF EXISTS(SELECT * FROM sys.server_event_sessions WHERE name='session_name')  
       DROP EVENT SESSION [session_name] ON SERVER;  
    CREATE EVENT SESSION [session_name]  
    ON SERVER  
  
    ADD EVENT sqlserver.sp_statement_starting  
       (ACTION  
       (  
          sqlserver.nt_username,  
          sqlserver.client_pid,  
          sqlserver.client_app_name,  
          sqlserver.server_principal_name,  
          sqlserver.session_id  
       )  
       WHERE sqlserver.session_id = 59   
       ),  
  
    ADD EVENT sqlserver.sp_statement_completed  
       (ACTION  
       (  
          sqlserver.nt_username,  
          sqlserver.client_pid,  
          sqlserver.client_app_name,  
          sqlserver.server_principal_name,  
          sqlserver.session_id  
       )  
       WHERE sqlserver.session_id = 59 AND duration > 0  
       );  
  
    ADD TARGET package0.asynchronous_file_target  
       (SET filename='c:\temp\ExtendedEventsStoredProcs.xel', metadatafile='c:\temp\ExtendedEventsStoredProcs.xem');  
    ```  
  
## <a name="example"></a>例  
  
```sql
IF EXISTS(SELECT * FROM sys.server_event_sessions WHERE name='session_name')  
   DROP EVENT SESSION [session_name] ON SERVER;  
CREATE EVENT SESSION [session_name]  
ON SERVER  
  
ADD EVENT sqlserver.sp_statement_starting  
   (ACTION  
   (  
      sqlserver.nt_username,  
      sqlserver.client_pid,  
      sqlserver.client_app_name,  
      sqlserver.server_principal_name,  
      sqlserver.session_id  
   )  
   WHERE sqlserver.session_id = 59   
   ),  
  
ADD EVENT sqlserver.sp_statement_completed  
   (ACTION  
   (  
      sqlserver.nt_username,  
      sqlserver.client_pid,  
      sqlserver.client_app_name,  
      sqlserver.server_principal_name,  
      sqlserver.session_id  
   )  
   WHERE sqlserver.session_id = 59 AND duration > 0  
   )  
  
ADD TARGET package0.asynchronous_file_target  
   (SET filename='c:\temp\ExtendedEventsStoredProcs.xel', metadatafile='c:\temp\ExtendedEventsStoredProcs.xem');  
```  
  
## <a name="see-also"></a>参照  
 [SQL トレースのイベント クラスと等価な拡張イベントを確認する](../../relational-databases/extended-events/view-the-extended-events-equivalents-to-sql-trace-event-classes.md)  
  
  
