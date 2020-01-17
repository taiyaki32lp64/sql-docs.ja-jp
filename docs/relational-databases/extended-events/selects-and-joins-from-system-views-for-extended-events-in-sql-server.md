---
title: 拡張イベントに対するシステム ビューからの SELECT と JOIN
ms.date: 08/02/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xevents
ms.topic: tutorial
ms.assetid: 04521d7f-588c-4259-abc2-1a2857eb05ec
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d3bcb7e272c1a5120b65018aab781546ba8d0f2b
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75242899"
---
# <a name="selects-and-joins-from-system-views-for-extended-events-in-sql-server"></a>SQL Server の拡張イベントに対するシステム ビューからの SELECT と JOIN

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]


この記事では、SQL Server および Azure SQL Database の拡張イベントに関連するシステム ビューの 2 つのセットについて説明します。 以下のことについて説明します。

- さまざまなシステム ビューを結合 (JOIN) する方法。
- システム ビューから特定の種類の情報を選択 (SELECT) する方法。
- さまざまな技術的観点からの同じイベント セッション情報の表現方法。各観点の理解を助けます。


ほとんどの例は SQL Server 用に作成されています。 ただし、少し編集すれば SQL Database でも動作します。



## <a name="a-foundational-information"></a>A. 基礎的な情報


拡張イベントには 2 セットのシステム ビューがあります。


#### <a name="catalog-views"></a>カタログ ビュー:

- カタログ ビューには、 *CREATE EVENT SESSION* または SSMS の同等の UI によって作成された各イベント セッションの [定義](../../t-sql/statements/create-event-session-transact-sql.md)についての情報が格納されます。 ただし、これらのビューでは、セッションの実行が開始しているかどうかはわかりません。
    - たとえば場合は、SSMS の **オブジェクト エクスプローラー** でイベント セッションが定義されていないことが示されている場合、ビュー *sys.server_event_session_targets* に対する SELECT からは行が返りません。


- 名前プレフィックス:
    - *sys.server\_event\_session\** は、SQL Server での名前プレフィックスです。
    - *sys.database\_event\_session\** は、SQL Database での名前プレフィックスです。


#### <a name="dynamic-management-views-dmvs"></a>動的管理ビュー (DMV):

- 実行中のイベント セッションの *現在のアクティビティ* に関する情報が格納されます。 ただし、これらの DMV はセッションの定義に関してはほとんどわかりません。
    - 現在すべてのイベント セッションが停止されていても、さまざまなパッケージがサーバー起動時にアクティブなメモリに読み込まれるので、ビュー *sys.dm_xe_packages* に対する SELECT からは行が返ります。
    - 同じ理由から、*sys.dm_xe_objects* *sys.dm_xe_object_columns* も行を返します。


- 拡張イベント DMV の名前プレフィックス:
    - *sys.dm\_xe\_\** は、SQL Server での名前プレフィックスです。
    - *sys.dm\_xe\_database\_\** は、一般に SQL Database での名前プレフィックスです。


#### <a name="permissions"></a>権限:


システム ビューの SELECT を行うには、次の権限が必要です。

- VIEW SERVER STATE - Microsoft SQL Server の場合。
- VIEW DATABASE STATE - Azure SQL Database の場合。


<a name="section_B_catalog_views"></a>

## <a name="b-catalog-views"></a>B. カタログ ビュー


このセクションでは、同じ定義済みイベント セッションを 3 つの異なる技術で示して関連付けます。 セッションは定義されていて SQL Server Management Studio (SSMS.exe) の **オブジェクト エクスプローラー** に表示されますが、現在は実行していません。

予期しない障害を防ぐため、 [SSMS の最新の更新プログラムを毎月インストール](https://msdn.microsoft.com/library/mt238290.aspx)してください。


拡張イベントのカタログ ビューに関するリファレンス ドキュメントについては、「 [拡張イベント カタログ ビュー (Transact-SQL)](../../relational-databases/system-catalog-views/extended-events-catalog-views-transact-sql.md)」をご覧ください。


&nbsp;



#### <a name="the-sequence-in-this-section-b"></a>このセクション B のシーケンス:


- [B.1 SSMS UI パースペクティブ](#section_B_1_SSMS_UI_perspective)
    - SSMS UI を使用してイベント セッションの定義を作成します。 スクリーンショットで手順を示します。


- [B.2 Transact-SQL パースペクティブ](#section_B_2_TSQL_perspective)
    - SSMS コンテキスト メニューを使用して、定義済みのイベント セッションを Transact-SQL の同等の **CREATE EVENT SESSION** ステートメントにリバース エンジニアリングします。 T-SQL は、SSMS のスクリーンショットでの選択と完全に一致します。


- [B.3 カタログ ビュー SELECT JOIN UNION パースペクティブ](#section_B_3_Catalog_view_S_J_UNION)
    - イベント セッションに対してシステム カタログ ビューから T-SQL の SELECT ステートメントを実行します。 結果は、 **CREATE EVENT SESSION** ステートメントでの指定と一致します。


&nbsp;



<a name="section_B_1_SSMS_UI_perspective"></a>

### <a name="b1-ssms-ui-perspective"></a>B.1 SSMS UI パースペクティブ


SSMS の **オブジェクト エクスプローラー**で、 **[管理]** 、 **[拡張イベント]**  >  **[セッション]** を右クリックして **[新しいセッション]**  >  **[管理]** 」をご覧ください。

大きい **[新しいセッション]** ダイアログの最初の **[全般]** セクションで、 **[サーバーの起動時にイベント セッションを開始する]** がオンになっています。

![[新しいセッション] > [全般]、[サーバーの起動時にイベント セッションを開始する]](../../relational-databases/extended-events/media/xevents-ssms-ac105-eventname-startup.png)


次に、 **[イベント]** セクションでは **[lock_deadlock]** イベントが選択されています。 このイベントに対して、3 つの **アクション** が選択されています。 これは **[構成]** ボタンがクリックされたことを意味し、クリックされた後でボタンはグレーになっています。

![[新しいセッション] > [イベント]、[グローバル フィールド (アクション)]](../../relational-databases/extended-events/media/xevents-ssms-ac110-actions-global.png)


<a name="resource_type_PAGE_cat_view"></a>

次に、同じ **[イベント]**  >  **[構成]** セクションでは、[**resource_type** が **PAGE**](#resource_type_dmv_actual_row) に設定されています。 これは、**resource_type** の値が **PAGE** 以外の場合はイベント データがイベント エンジンからターゲットに送信されないことを意味します。

データベース名とカウンターの述語フィルターを確認します。

![[新しいセッション] > [イベント]、[フィルター (述語)] フィールド (アクション)](../../relational-databases/extended-events/media/xevents-ssms-ac115-predicate-db.png)


次に、 **[データ ストレージ]** セクションでは、 **[event_file]** がターゲットとして選択されています。 さらに、 **[ファイル ロールオーバーを有効にする]** オプションがオンになっています。

![[新しいセッション] > [データ ストレージ]、eventfile_enablefileroleover](../../relational-databases/extended-events/media/xevents-ssms-ac120-target-eventfile.png)


最後に、 **[詳細]** セクションでは、 **[ディスパッチの最大待機時間]** の値が 4 秒に短縮されています。

![[新しいセッション] > [詳細]、[ディスパッチの最大待機時間]](../../relational-databases/extended-events/media/xevents-ssms-ac125-latency4.png)


以上で、SSMS UI でのイベント セッションの定義は終わりです。


<a name="section_B_2_TSQL_perspective"></a>

### <a name="b2-transact-sql-perspective"></a>B.2 Transact-SQL パースペクティブ


イベント セッション定義の作成方法にかかわらず、SSMS UI では、セッションを完全に一致する Transact-SQL スクリプトにリバース エンジニアリングできます。 前に示した [新しいセッション] のスクリーンショットで示されている指定と、次に示す生成された T-SQL **CREATE EVENT SESSION** スクリプトの句を比較してください。

イベント セッションをリバース エンジニアリングするには、 **オブジェクト エクスプローラー** でセッション ノードを右クリックし、 **[セッションをスクリプト化]**  >  **[CREATE]**  >  **[クリップボード]** 」をご覧ください。

SSMS でリバース エンジニアリングすることにより、次の T-SQL スクリプトが作成されます。 次のスクリプトは空白のみを使用して手作業で整形されています。


```sql
CREATE EVENT SESSION [event_session_test3]
    ON SERVER  -- Or, if on Azure SQL Database, ON DATABASE.

    ADD EVENT sqlserver.lock_deadlock
    (
        SET
            collect_database_name = (1)
        ACTION
        (
            package0  .collect_system_time,
            package0  .event_sequence,
            sqlserver .client_hostname
        )
        WHERE
        (
            [database_name]           = N'InMemTest2'
            AND [package0].[counter] <= (16)
            AND [resource_type]       = (6)
        )
    )

    ADD TARGET package0.event_file
    (
        SET
            filename           = N'C:\Junk\event_session_test3_EF.xel',
            max_file_size      = (20),
            max_rollover_files = (2)
    )

    WITH
    (
        MAX_MEMORY            = 4096 KB,
        EVENT_RETENTION_MODE  = ALLOW_SINGLE_EVENT_LOSS,
        MAX_DISPATCH_LATENCY  = 4 SECONDS,
        MAX_EVENT_SIZE        = 0 KB,
        MEMORY_PARTITION_MODE = NONE,
        TRACK_CAUSALITY       = OFF,
        STARTUP_STATE         = ON
    );
```


T-SQL パースペクティブは以上です。


<a name="section_B_3_Catalog_view_S_J_UNION"></a>

### <a name="b3-catalog-view-select-join-union-perspective"></a>B.3 カタログ ビュー SELECT JOIN UNION パースペクティブ


次に示す T-SQL の SELECT ステートメントは長いですが、複数の小さい SELECT が UNION でまとめられているためです。 どの小さい SELECT もそれだけで実行できます。 小さい SELECT は、さまざまなシステム カタログ ビューを JOIN する方法を示しています。


```sql
SELECT
        s.name        AS [Session-Name],
        '1_EVENT'     AS [Clause-Type],
        'Event-Name'  AS [Parameter-Name],
        e.name        AS [Parameter-Value]
    FROM
              sys.server_event_sessions         AS s
        JOIN  sys.server_event_session_events   AS e

            ON  e.event_session_id = s.event_session_id
    WHERE
        s.name = 'event_session_test3'

UNION ALL
SELECT
        s.name         AS [Session-Name],
        '2_EVENT_SET'  AS [Clause-Type],
        f.name         AS [Parameter-Name],
        f.value        AS [Parameter-Value]
    FROM
              sys.server_event_sessions         AS s
        JOIN  sys.server_event_session_events   AS e

            ON  e.event_session_id = s.event_session_id

        JOIN  sys.server_event_session_fields   As f

            ON  f.event_session_id = s.event_session_id
            AND f.object_id        = e.event_id
    WHERE
        s.name = 'event_session_test3'

UNION ALL
SELECT
        s.name              AS [Session-Name],
        '3_EVENT_ACTION'    AS [Clause-Type],

        a.package + '.' + a.name
                            AS [Parameter-Name],

        '(Not_Applicable)'  AS [Parameter-Value]
    FROM
              sys.server_event_sessions         AS s
        JOIN  sys.server_event_session_events   AS e

            ON  e.event_session_id = s.event_session_id

        JOIN  sys.server_event_session_actions  As a

            ON  a.event_session_id = s.event_session_id
            AND a.event_id         = e.event_id
    WHERE
        s.name = 'event_session_test3'

UNION ALL
SELECT
        s.name                AS [Session-Name],
        '4_EVENT_PREDICATES'  AS [Clause-Type],
        e.predicate           AS [Parameter-Name],
        '(Not_Applicable)'    AS [Parameter-Value]
    FROM
              sys.server_event_sessions         AS s
        JOIN  sys.server_event_session_events   AS e

            ON  e.event_session_id = s.event_session_id
    WHERE
        s.name = 'event_session_test3'

UNION ALL
SELECT
        s.name              AS [Session-Name],
        '5_TARGET'          AS [Clause-Type],
        t.name              AS [Parameter-Name],
        '(Not_Applicable)'  AS [Parameter-Value]
    FROM
              sys.server_event_sessions         AS s
        JOIN  sys.server_event_session_targets  AS t

            ON  t.event_session_id = s.event_session_id
    WHERE
        s.name = 'event_session_test3'

UNION ALL
SELECT
        s.name          AS [Session-Name],
        '6_TARGET_SET'  AS [Clause-Type],
        f.name          AS [Parameter-Name],
        f.value         AS [Parameter-Value]
    FROM
              sys.server_event_sessions         AS s
        JOIN  sys.server_event_session_targets  AS t

            ON  t.event_session_id = s.event_session_id

        JOIN  sys.server_event_session_fields   As f

            ON  f.event_session_id = s.event_session_id
            AND f.object_id        = t.target_id
    WHERE
        s.name = 'event_session_test3'

UNION ALL
SELECT
        s.name               AS [Session-Name],
        '7_WITH_MAX_MEMORY'  AS [Clause-Type],
        'max_memory'         AS [Parameter-Name],
        s.max_memory         AS [Parameter-Value]
    FROM
              sys.server_event_sessions  AS s
    WHERE
        s.name = 'event_session_test3'

UNION ALL
SELECT
        s.name                  AS [Session-Name],
        '7_WITH_STARTUP_STATE'  AS [Clause-Type],
        'startup_state'         AS [Parameter-Name],
        s.startup_state         AS [Parameter-Value]
    FROM
              sys.server_event_sessions  AS s
    WHERE
        s.name = 'event_session_test3'

ORDER BY
    [Session-Name],
    [Clause-Type],
    [Parameter-Name]
;
```


#### <a name="output"></a>Output


次に示すのは、前の SELECT JOIN UNION を実行した実際の出力です。 出力のパラメーターの名前と値は、前の CREATE EVENT SESSION ステートメントと対応します。


```
Session-Name          Clause-Type            Parameter-Name                  Parameter-Value
------------          -----------            --------------                  ---------------
event_session_test3   1_EVENT                Event-Name                      lock_deadlock
event_session_test3   2_EVENT_SET            collect_database_name           1
event_session_test3   3_EVENT_ACTION         sqlserver.client_hostname       (Not_Applicable)
event_session_test3   3_EVENT_ACTION         sqlserver.collect_system_time   (Not_Applicable)
event_session_test3   3_EVENT_ACTION         sqlserver.event_sequence        (Not_Applicable)
event_session_test3   4_EVENT_PREDICATES     ([sqlserver].[equal_i_sql_unicode_string]([database_name],N'InMemTest2') AND [package0].[counter]<=(16))   (Not_Applicable)
event_session_test3   5_TARGET               event_file                      (Not_Applicable)
event_session_test3   6_TARGET_SET           filename                        C:\Junk\event_session_test3_EF.xel
event_session_test3   6_TARGET_SET           max_file_size                   20
event_session_test3   6_TARGET_SET           max_rollover_files              2
event_session_test3   7_WITH_MAX_MEMORY      max_memory                      4096
event_session_test3   7_WITH_STARTUP_STATE   startup_state                   1
```


以上でカタログ ビューのセクションは終わりです。



<a name="section_C_DMVs"></a>

## <a name="c-dynamic-management-views-dmvs"></a>C. 動的管理ビュー (DMV)


次に DMV について説明します。 ここでは、それぞれが特定の目的でビジネスに役立つ Transact-SQL SELECT ステートメントをいくつか示します。 さらに、新しい用途のために DMV を JOIN する方法を示します。


DMV のリファレンス ドキュメントについては、「 [拡張イベントの動的管理ビュー](../../relational-databases/system-dynamic-management-views/extended-events-dynamic-management-views.md)」をご覧ください。


特に記述していない限り、以下の SELECT からの実際の出力行は SQL Server 2016 のものです。


セクション C で示す DMV の SELECT の一覧:

- [C.1 すべてのパッケージのリスト](#section_C_1_list_packages)
- [C.2 すべてのオブジェクト タイプの数](#section_C_2_count_object_type)
- [C.3 使用可能なすべてのアイテムをタイプ別に並べ替える SELECT](#section_C_3_select_all_available_objects)
- [C.4 イベントに使用できるデータ フィールド](#section_C_4_data_fields)
- [C.5 *sys.dm_xe_map_values* とイベント フィールド](#section_C_5_map_values_fields)
- [C.6 ターゲットのパラメーター](#section_C_6_parameters_targets)
- [C.7 target_data 列を XML にキャストする DMV SELECT](#section_C_7_dmv_select_target_data_column)
- [C.8 ディスク ドライブから event_file データを取得する関数の SELECT](#section_C_8_select_function_disk)



<a name="section_C_1_list_packages"></a>

### <a name="c1-list-of-all-packages"></a>C.1 すべてのパッケージのリスト


拡張イベントの領域で使用できるすべてのオブジェクトは、システムに読み込まれるパッケージから取得されます。 次の SELECT はすべてのパッケージとその説明をリストします。


```sql
SELECT  --C.1
        p.name         AS [Package],
        p.description  AS [Package-Description]
    FROM
        sys.dm_xe_packages  AS p
    ORDER BY
        p.name;
```


#### <a name="output"></a>Output

パッケージのリストです。


```
/***  (The unique p.guid values are not shown.)
Package        Package-Description
-------        -------------------
filestream     Extended events for SQL Server FILESTREAM and FileTable
package0       Default package. Contains all standard types, maps, compare operators, actions and targets
qds            Extended events for Query Store
SecAudit       Security Audit Events
sqlclr         Extended events for SQL CLR
sqlos          Extended events for SQL Operating System
SQLSatellite   Extended events for SQL Satellite
sqlserver      Extended events for Microsoft SQL Server
sqlserver      Extended events for Microsoft SQL Server
sqlserver      Extended events for Microsoft SQL Server
sqlsni         Extended events for Microsoft SQL Server
ucs            Extended events for Unified Communications Stack
XtpCompile     Extended events for the XTP Compile
XtpEngine      Extended events for the XTP Engine
XtpRuntime     Extended events for the XTP Runtime
***/
```


*上記の頭字語の定義:*

- clr = .NET の共通言語ランタイム
- qds = クエリ データ ストア
- sni = サーバー ネットワーク インターフェイス
- ucs = ユニファイド コミュニケーション スタック
- xtp = 大量トランザクション処理


<a name="section_C_2_count_object_type"></a>

### <a name="c2-count-of-every-object-type"></a>C.2 すべてのオブジェクト タイプの数


このセクションの SELECT は、イベント パッケージに含まれるオブジェクトのタイプを表示します。 *sys.dm\_xe\_objects* に含まれるすべてのオブジェクト タイプとそれぞれの数のリストが表示されます。


```sql
SELECT  --C.2
        Count(*)  AS [Count-of-Type],
        o.object_type
    FROM
        sys.dm_xe_objects  AS o
    GROUP BY
        o.object_type
    ORDER BY
        1  DESC;
```


#### <a name="output"></a>Output

オブジェクト タイプごとのオブジェクトの数です。 約 1915 個のオブジェクトがあります。


```
/***  Actual output, sum is about 1915:

Count-of-Type   object_type
-------------   -----------
1303            event
351             map
84              message
77              pred_compare
53              action
46              pred_source
28              type
17              target
***/
```


<a name="section_C_3_select_all_available_objects"></a>

### <a name="c3-select-all-available-items-sorted-by-type"></a>C.3 使用可能なすべてのアイテムをタイプ別に並べ替える SELECT


次の SELECT は、オブジェクトごとに 1 行ずつ、約 1915 行を返します。



```sql
SELECT  --C.3
        o.object_type  AS [Type-of-Item],
        p.name         AS [Package],
        o.name         AS [Item],
        o.description  AS [Item-Description]
    FROM
             sys.dm_xe_objects  AS o
        JOIN sys.dm_xe_packages AS p  ON o.package_guid = p.guid
    WHERE
        o.object_type IN ('action' , 'target' , 'pred_source')
        AND
        (
            (o.capabilities & 1) = 0
            OR
            o.capabilities IS NULL
        )
    ORDER BY
        [Type-of-Item],
        [Package],
        [Item];
```


#### <a name="output"></a>Output

次に示すのは上の SELECT によって返されるオブジェクトの例です。


```
/***
Type-of-Item   Package        Item                          Item-Description
------------   -------        ----                          ----------------
action         package0       callstack                     Collect the current call stack
action         package0       debug_break                   Break the process in the default debugger
action         sqlos          task_time                     Collect current task execution time
action         sqlserver      sql_text                      Collect SQL text
event          qds            query_store_aprc_regression   Fired when Query Store detects regression in query plan performance
event          SQLSatellite   connection_accept             Occurs when a new connection is accepted. This event serves to log all connection attempts.
event          XtpCompile     cgen                          Occurs at start of C code generation.
map            qds            aprc_state                    Query Store Automatic Plan Regression Correction state
message        package0       histogram_event_required      A value is required for the parameter 'filtering_event_name' when source type is 0.
pred_compare   package0       equal_ansi_string             Equality operator between two ANSI string values
pred_compare   sqlserver      equal_i_sql_ansi_string       Equality operator between two SQL ANSI string values
pred_source    sqlos          task_execution_time           Get current task execution time
pred_source    sqlserver      client_app_name               Get the current client application name
target         package0       etw_classic_sync_target       Event Tracing for Windows (ETW) Synchronous Target
target         package0       event_counter                 Use the event_counter target to count the number of occurrences of each event in the event session.
target         package0       event_file                    Use the event_file target to save the event data to an XEL file, which can be archived and used for later analysis and review. You can merge multiple XEL files to view the combined data from separate event sessions.
target         package0       histogram                     Use the histogram target to aggregate event data based on a specific event data field or action associated with the event. The histogram allows you to analyze distribution of the event data over the period of the event session.
target         package0       pair_matching                 Pairing target
target         package0       ring_buffer                   Asynchronous ring buffer target.
type           package0       xml                           Well formed XML fragment
***/
```



<a name="section_C_4_data_fields"></a>

### <a name="c4-data-fields-available-for-your-event"></a>C.4 イベントに使用できるデータ フィールド


次の SELECT は、イベント タイプに固有のすべてのデータ フィールドを返します。

- WHERE 句の項目 *column_type = 'data'* に注意してください。
- また、 *o.name =* の WHERE 句の値を編集する必要があります。


```sql
SELECT  -- C.4
        p.name         AS [Package],
        c.object_name  AS [Event],
        c.name         AS [Column-for-Predicate-Data],
        c.description  AS [Column-Description]
    FROM
              sys.dm_xe_object_columns  AS c
        JOIN  sys.dm_xe_objects         AS o

            ON  o.name = c.object_name

        JOIN  sys.dm_xe_packages        AS p

            ON  p.guid = o.package_guid
    WHERE
        c.column_type = 'data'
        AND
        o.object_type = 'event'
        AND
        o.name        = '\<EVENT-NAME-HERE!>'  --'lock_deadlock'
    ORDER BY
        [Package],
        [Event],
        [Column-for-Predicate-Data];
```


#### <a name="output"></a>Output

前の SELECT、WHERE `o.name = 'lock_deadlock'`では次の行が返されます。

- 各行は、 *sqlserver.lock_deadlock* イベントのオプションのフィルターを表します。
- 次の表示では *\[Column-Description\]* 列は省略されています。 その値は多くの場合 NULL です。


```
/***
Actual output, except for the omitted Description column which is often NULL.
These rows are where object_type = 'lock_deadlock'.

Package     Event           Column-for-Predicate-Data
-------     -----           -------------------------
sqlserver   lock_deadlock   associated_object_id
sqlserver   lock_deadlock   database_id
sqlserver   lock_deadlock   database_name
sqlserver   lock_deadlock   deadlock_id
sqlserver   lock_deadlock   duration
sqlserver   lock_deadlock   lockspace_nest_id
sqlserver   lock_deadlock   lockspace_sub_id
sqlserver   lock_deadlock   lockspace_workspace_id
sqlserver   lock_deadlock   mode
sqlserver   lock_deadlock   object_id
sqlserver   lock_deadlock   owner_type
sqlserver   lock_deadlock   resource_0
sqlserver   lock_deadlock   resource_1
sqlserver   lock_deadlock   resource_2
sqlserver   lock_deadlock   resource_description
sqlserver   lock_deadlock   resource_type
sqlserver   lock_deadlock   transaction_id
***/
```



<a name="section_C_5_map_values_fields"></a>

### <a name="c5-sysdm_xe_map_values-and-event-fields"></a>C.5 *sys.dm_xe_map_values* とイベント フィールド


次の SELECT には、 *sys.dm_xe_map_values*という名前の巧妙なビューに対する JOIN が含まれます。

この SELECT の目的は、イベント セッションから選択できるさまざまなフィールドを表示することです。 イベント フィールドは、2 つの方法で使用できます。

- イベントが発生するたびにターゲットに書き込まれるフィールドの値を選択する。
- 発生したイベントをターゲットに送るかどうかをフィルター処理する。


```sql
SELECT  --C.5
        dp.name         AS [Package],
        do.name         AS [Object],
        do.object_type  AS [Object-Type],
        'o--c'     AS [O--C],
        dc.name         AS [Column],
        dc.type_name    AS [Column-Type-Name],
        dc.column_type  AS [Column-Type],
        dc.column_value AS [Column-Value],
        'c--m'     AS [C--M],
        dm.map_value    AS [Map-Value],
        dm.map_key      AS [Map-Key]
    FROM
              sys.dm_xe_objects         AS do
        JOIN  sys.dm_xe_object_columns  AS dc

            ON  dc.object_name = do.name

        JOIN  sys.dm_xe_map_values      AS dm

            ON  dm.name = dc.type_name

        JOIN  sys.dm_xe_packages        AS dp

            ON  dp.guid = do.package_guid
    WHERE
        do.object_type = 'event'
        AND
        do.name        = '\<YOUR-EVENT-NAME-HERE!>'  --'lock_deadlock'
    ORDER BY
        [Package],
        [Object],
        [Column],
        [Map-Value];
```


#### <a name="output"></a>Output

<a name="resource_type_dmv_actual_row"></a>

次に示すのは、実際には 153 行ある前記の T-SQL SELECT からの出力のサンプルです。 **resource_type** の行は、この記事の [event_session_test3](#resource_type_PAGE_cat_view) の例で使用されている述語のフィルター処理に **関連** しています。


```
/***  5 sampled rows from the actual 153 rows returned.
    NOTE:  'resource_type' under 'Column'.

Package     Object          Object-Type   O--C   Column          Column-Type-Name     Column-Type   Column-Value   C--M   Map-Value        Map-Key
-------     ------          -----------   ----   ------          ----------------     -----------   ------------   ----   ---------        -------
sqlserver   lock_deadlock   event         o--c   CHANNEL         etw_channel          readonly      2              c--m   Operational      4
sqlserver   lock_deadlock   event         o--c   KEYWORD         keyword_map          readonly      16             c--m   access_methods   1024
sqlserver   lock_deadlock   event         o--c   mode            lock_mode            data          NULL           c--m   IX               8
sqlserver   lock_deadlock   event         o--c   owner_type      lock_owner_type      data          NULL           c--m   Cursor           2
sqlserver   lock_deadlock   event         o--c   resource_type   lock_resource_type   data          NULL           c--m   PAGE             6

Therefore, on your CREATE EVENT SESSION statement, in its ADD EVENT WHERE clause,
you could put:
    WHERE( ... resource_type = 6 ...)  -- Meaning:  6 = PAGE.
***/
```


<a name="section_C_6_parameters_targets"></a>

### <a name="c6-parameters-for-targets"></a>C.6 ターゲットのパラメーター


次の SELECT は、ターゲットのすべてのパラメーターを返します。 各パラメーターには、必須かどうかを示すタグが付けられます。 パラメーターに割り当てる値によって、ターゲットの動作が変わります。

- WHERE 句の項目 *object_type = 'customizable'* に注意してください。
- また、 *o.name =* の WHERE 句の値を編集する必要があります。


```sql
SELECT  --C.6
        p.name        AS [Package],
        o.name        AS [Target],
        c.name        AS [Parameter],
        c.type_name   AS [Parameter-Type],

        CASE c.capabilities_desc
            WHEN 'mandatory' THEN 'YES_Mandatory'
            ELSE 'Not_mandatory'
        END  AS [IsMandatoryYN],

        c.description AS [Parameter-Description]
    FROM
              sys.dm_xe_objects   AS o
        JOIN  sys.dm_xe_packages  AS p

            ON  o.package_guid = p.guid

        LEFT OUTER JOIN  sys.dm_xe_object_columns  AS c

            ON  o.name        = c.object_name
            AND c.column_type = 'customizable'  -- !
    WHERE
        o.object_type = 'target'
        AND
        o.name     LIKE '%'    -- Or '\<YOUR-TARGET-NAME-HERE!>'.
    ORDER BY
        [Package],
        [Target],
        [IsMandatoryYN]  DESC,
        [Parameter];
```


#### <a name="output"></a>Output

次のパラメーター行は、SQL Server 2016 で前の SELECT で返された結果の一部です。


```
/***  Actual output, all rows, where target name = 'event_file'.
Package    Target       Parameter            Parameter-Type       IsMandatoryYN   Parameter-Description
-------    ------       ---------            --------------       -------------   ---------------------
package0   event_file   filename             unicode_string_ptr   YES_Mandatory   Specifies the location and file name of the log
package0   event_file   increment            uint64               Not_mandatory   Size in MB to grow the file
package0   event_file   lazy_create_blob     boolean              Not_mandatory   Create blob upon publishing of first event buffer, not before.
package0   event_file   max_file_size        uint64               Not_mandatory   Maximum file size in MB
package0   event_file   max_rollover_files   uint32               Not_mandatory   Maximum number of files to retain
package0   event_file   metadatafile         unicode_string_ptr   Not_mandatory   Not used
***/
```


<a name="section_C_7_dmv_select_target_data_column"></a>

### <a name="c7-dmv-select-casting-target_data-column-to-xml"></a>C.7 target_data 列を XML にキャストする DMV SELECT


この DMV SELECT は、アクティブなイベント セッションのターゲットからデータ行を返します。 データは XML にキャストされており、返されたセルをクリックして SSMS で簡単に表示できます。

- イベント セッションが停止すると、この SELECT はゼロ行を返します。
- *s.name =* の WHERE 句の値を編集する必要があります。


```sql
SELECT  --C.7
        s.name,
        t.target_name,
        CAST(t.target_data AS XML)  AS [XML-Cast]
    FROM
              sys.dm_xe_session_targets  AS t
        JOIN  sys.dm_xe_sessions         AS s

            ON s.address = t.event_session_address
    WHERE
        s.name = '\<Your-Session-Name-Here!>';
```


#### <a name="output-the-only-row-including-its-xml-cell"></a>XML セルを含む唯一の出力行

次に示すのは、上記の SELECT から出力される唯一の行です。 列 *XML-Cast* には、SSMS が認識する XML の文字列が含まれます。 したがって、SSMS は XML-Cast セルをクリック可能にします。


次のように設定されています。

- *s.name =* の値には、 *checkpoint_begin* イベントのイベント セッションが設定されています。
- ターゲットは *ring_buffer*です。


```XML
name                              target_name   XML-Cast
----                              -----------   --------
checkpoint_session_ring_buffer2   ring_buffer   <RingBufferTarget truncated="0" processingTime="0" totalEventsProcessed="2" eventCount="2" droppedCount="0" memoryUsed="104"><event name="checkpoint_begin" package="sqlserver" timestamp="2016-07-09T01:28:23.508Z"><data name="database_id"><type name="uint32" package="package0" /><value>5</value></data></event><event name="checkpoint_begin" package="sqlserver" timestamp="2016-07-09T01:28:26.975Z"><data name="database_id"><type name="uint32" package="package0" /><value>5</value></data></event></RingBufferTarget>
```


#### <a name="output-xml-displayed-pretty-when-cell-is-clicked"></a>セルをクリックすると XML で表示される出力


XML-Cast セルをクリックすると、次の出力が表示されます。


```xml
<RingBufferTarget truncated="0" processingTime="0" totalEventsProcessed="2" eventCount="2" droppedCount="0" memoryUsed="104">
  <event name="checkpoint_begin" package="sqlserver" timestamp="2016-07-09T01:28:23.508Z">
    <data name="database_id">
      <type name="uint32" package="package0" />
      <value>5</value>
    </data>
  </event>
  <event name="checkpoint_begin" package="sqlserver" timestamp="2016-07-09T01:28:26.975Z">
    <data name="database_id">
      <type name="uint32" package="package0" />
      <value>5</value>
    </data>
  </event>
</RingBufferTarget>
```


<a name="section_C_8_select_function_disk"></a>

### <a name="c8-select-from-a-function-to-retrieve-event_file-data-from-disk-drive"></a>C.8 ディスク ドライブから event_file データを取得する関数の SELECT


イベント セッションがデータを収集した後で停止されたものとします。 セッションが event_file ターゲットを使用するように定義されている場合でも、関数 *sys.fn_xe_target_read_file*を呼び出すことによってデータを取得できます。

- この SELECT を実行する前に、関数呼び出しのパスとファイル名のパラメーターを編集する必要があります。
    - セッションを再起動するたびに SQL システムが実際の .XEL ファイル名に埋め込む余分な桁に注意する必要はありません。 通常のルート名と拡張子を指定するだけです。


```sql
SELECT  --C.8
        f.module_guid,
        f.package_guid,
        f.object_name,
        f.file_name,
        f.file_offset,
        CAST(f.event_data AS XML)  AS [Event-Data-As-XML]
    FROM
        sys.fn_xe_file_target_read_file(

            '\<YOUR-PATH-FILE-NAME-ROOT-HERE!>*.xel',
            --'C:\Junk\Checkpoint_Begins_ES*.xel',  -- Example.

            NULL, NULL, NULL
        )  AS f;
```


#### <a name="output-rows-returned-by-select-from-the-function"></a>関数の SELECT FROM によって返される出力行


次に示すのは、前記の関数の SELECT FROM によって返される行です。 右端の XML 列には、イベント発生についての具体的なデータが含まれます。


```
module_guid                            package_guid                           object_name        file_name                                                           file_offset   Event-Data-As-XML
-----------                            ------------                           -----------        ---------                                                           -----------   -----------------
D5149520-6282-11DE-8A39-0800200C9A66   03FDA7D0-91BA-45F8-9875-8B6DD0B8E9F2   checkpoint_begin   C:\Junk\Checkpoint_Begins_ES_20160615bb-_0_131125086091700000.xel   5120          <event name="checkpoint_begin" package="sqlserver" timestamp="2016-07-09T03:30:14.023Z"><data name="database_id"><value>5</value></data><action name="session_id" package="sqlserver"><value>60</value></action><action name="database_id" package="sqlserver"><value>5</value></action></event>
D5149520-6282-11DE-8A39-0800200C9A66   03FDA7D0-91BA-45F8-9875-8B6DD0B8E9F2   checkpoint_end     C:\Junk\Checkpoint_Begins_ES_20160615bb-_0_131125086091700000.xel   5120          <event name="checkpoint_end" package="sqlserver" timestamp="2016-07-09T03:30:14.025Z"><data name="database_id"><value>5</value></data></event>
D5149520-6282-11DE-8A39-0800200C9A66   03FDA7D0-91BA-45F8-9875-8B6DD0B8E9F2   checkpoint_begin   C:\Junk\Checkpoint_Begins_ES_20160615bb-_0_131125086091700000.xel   5632          <event name="checkpoint_begin" package="sqlserver" timestamp="2016-07-09T03:30:17.704Z"><data name="database_id"><value>5</value></data><action name="session_id" package="sqlserver"><value>60</value></action><action name="database_id" package="sqlserver"><value>5</value></action></event>
D5149520-6282-11DE-8A39-0800200C9A66   03FDA7D0-91BA-45F8-9875-8B6DD0B8E9F2   checkpoint_end     C:\Junk\Checkpoint_Begins_ES_20160615bb-_0_131125086091700000.xel   5632          <event name="checkpoint_end" package="sqlserver" timestamp="2016-07-09T03:30:17.709Z"><data name="database_id"><value>5</value></data></event>
```


#### <a name="output-one-xml-cell"></a>出力、1 個の XML セル


次に示すのは、上記の返された行セットの最初の XML セルの内容です。


```xml
<event name="checkpoint_begin" package="sqlserver" timestamp="2016-07-09T03:30:14.023Z">
  <data name="database_id">
    <value>5</value>
  </data>
  <action name="session_id" package="sqlserver">
    <value>60</value>
  </action>
  <action name="database_id" package="sqlserver">
    <value>5</value>
  </action>
</event>
```


