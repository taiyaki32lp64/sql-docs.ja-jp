---
title: SQL Server の拡張イベントのターゲット
ms.date: 09/07/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xevents
ms.topic: conceptual
ms.assetid: 47c64144-4432-4778-93b5-00496749665b
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||=azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 942f69fc92fa06b5131cee2dba9145f4faaae0cc
ms.sourcegitcommit: 12f529b811d308b169735740b78c6d5439ffefc7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/27/2019
ms.locfileid: "75501986"
---
# <a name="targets-for-extended-events-in-sql-server"></a>SQL Server の拡張イベントのターゲット

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]


この記事では、SQL Server の拡張イベントに package0 ターゲットを使用するタイミングと方法について説明します。 各ターゲットについて次のことを説明します。

- イベントによって送信されるデータを収集およびレポートする package0 の機能。
- package0 のパラメーター。名前を見ればわかるパラメーターは除きます。


#### <a name="xquery-example"></a>XQuery の例


「 [ring_buffer ターゲット](#h2_target_ring_buffer) 」セクションには、 [Transact-SQL で XQuery](../../xquery/xquery-language-reference-sql-server.md) を使用して XML の文字列をリレーショナル行セットにコピーする例が含まれます。


### <a name="prerequisites"></a>前提条件


- 次に説明されている拡張イベントの基本について一般的に理解していること。「[クイック スタート: SQL Server 拡張イベント](../../relational-databases/extended-events/quick-start-extended-events-in-sql-server.md)」を参照してください。


- 頻繁に更新される SQL Server Management Studio (SSMS.exe) ユーティリティの最近のバージョンをインストールしてあること。 詳細については、次の項目を参照してください。
    - [SQL Server Management Studio (SSMS) のダウンロード](../../ssms/download-sql-server-management-studio-ssms.md)


- SSMS.exe の **オブジェクト エクスプローラー** でイベント セッションのターゲット ノードを右クリックして [出力データを簡単に表示する](../../relational-databases/extended-events/advanced-viewing-of-target-data-from-extended-events-in-sql-server.md)方法を知っていること。
    - イベント データは XML 文字列としてキャプチャされます。 この記事ではまだデータはリレーショナル行で表示されます。 SSMS を使用してデータを表示した後、コピーしてこの記事に貼り付けました。
    - T-SQL を使用して XML から行セットを生成する別の方法については、「 [ring_buffer ターゲット](#h2_target_ring_buffer)」セクションの説明をご覧ください。 その方法では XQuery を使用します。



## <a name="parameters-actions-and-fields"></a>パラメーター、アクション、フィールド


Transact-SQL で拡張イベントの中心になるのは [CREATE EVENT SESSION](~/t-sql/statements/create-event-session-transact-sql.md) ステートメントです。 ステートメントを書くには、多くの場合、次のものに関するリストと記述が必要になります。

- 選択したイベントに関連付けられているフィールド。
- 選択したイベントに関連付けられているパラメーター。

システム ビューからこのようなリストを返す SELECT ステートメントは、次の記事のセクション C からコピーできます。

- [SQL Server の拡張イベントに対するシステム ビューからの SELECT と JOIN](../../relational-databases/extended-events/selects-and-joins-from-system-views-for-extended-events-in-sql-server.md)
    - [C.4](../../relational-databases/extended-events/selects-and-joins-from-system-views-for-extended-events-in-sql-server.md#section_C_4_data_fields) : イベントに対する SELECT のフィールド。
    - [C.6](../../relational-databases/extended-events/selects-and-joins-from-system-views-for-extended-events-in-sql-server.md#section_C_6_parameters_targets) : ターゲットに対する SELECT のパラメーター。
    - [C.3](../../relational-databases/extended-events/selects-and-joins-from-system-views-for-extended-events-in-sql-server.md#section_C_3_select_all_available_objects) : SELECT のアクション。


実際の CREATE EVENT SESSION ステートメントのコンテキストで使用されているパラメーター、フィールド、アクションについては、 [こちらのリンク](../../relational-databases/extended-events/selects-and-joins-from-system-views-for-extended-events-in-sql-server.md#section_B_2_TSQL_perspective)をご覧ください。



<a name="h2_target_etw_classic_sync_target"></a>

## <a name="etw_classic_sync_target-target"></a>etw_classic_sync_target ターゲット


SQL Server の拡張イベントは、Event Tracing for Windows (ETW) と連携してシステムの使用状況を監視できます。 詳細については、次を参照してください。

- [Event Tracing for Windows ターゲット](../../relational-databases/extended-events/event-tracing-for-windows-target.md)
- [拡張イベントを使用したシステムの使用状況の監視](../../relational-databases/extended-events/monitor-system-activity-using-extended-events.md)


この ETW ターゲットは受信したデータを *同期的* に処理しますが、ほとんどのターゲットは *非同期的*に処理します。

> [!NOTE]
> Azure SQL Database では、`etw_classic_sync_target target` はサポートされません。

<!-- After OPS Versioning is live, the above !NOTE could be converted into a "3colon ZONE".  GeneMi = MightyPen. -->

<a name="h2_target_event_counter"></a>

## <a name="event_counter-target"></a>event_counter ターゲット


event_counter ターゲットは、指定された各イベントが発生した回数をカウントするだけです。


他のほとんどのターゲットとは次の点が異なります。

- event_counter にはパラメーターがありません。


- 受信したデータを *同期的* に処理します。
    - event_counter は処理がほとんどない単純なターゲットなので、同期処理でもかまいません。
    - データベース エンジンは、処理が遅く、データベース エンジンのパフォーマンスが低下する可能性のあるターゲットからは切断します。 これは、ほとんどのターゲットが *非同期*処理である理由の 1 つです。


#### <a name="example-output-captured-by-event_counter"></a>event_counter によってキャプチャされる出力の例


```
package_name   event_name         count
------------   ----------         -----
sqlserver      checkpoint_begin   4
```


次に示すのは、上のような結果が得られた CREATE EVENT SESSION です。 このテストでは、EVENT...WHERE 句で **package0.counter** フィールドを使用して、カウントが 4 に達したらカウントを終了しました。


```sql
CREATE EVENT SESSION [event_counter_1]
    ON SERVER 
    ADD EVENT sqlserver.checkpoint_begin   -- Test by issuing CHECKPOINT; statements.
    (
        WHERE ([package0].[counter] <= (4))   -- A predicate filter.
    )
    ADD TARGET package0.event_counter
    WITH
    (
        MAX_MEMORY = 4096 KB,
        MAX_DISPATCH_LATENCY = 3 SECONDS
    );
```



<a name="h2_target_event_file"></a>

## <a name="event_file-target"></a>event_file ターゲット


**event_file** ターゲットは、イベント セッションの出力をバッファーからディスク ファイルに書き込みます。


- ADD TARGET 句で *filename=* パラメーターを指定します。
    - ファイルの拡張子は、 **.xel** でなければなりません。


- 指定したファイル名をプレフィックスとして使用し、その後に日時に基づく長い整数と、.xel 拡張子が付加されます。

::: moniker range="= azuresqldb-current || = azuresqldb-mi-current || = sqlallproducts-allversions"

> [!NOTE]
> Azure SQL Database でサポートされるのは、Azure Blob Storage に `xel` ファイルを格納することのみです。 
>
> 特に SQL Database (および SQL Database Managed Instance) の **event_file** のコード例については、「[SQL Database の拡張イベントのためのイベント ファイル ターゲット コード](https://docs.microsoft.com/azure/sql-database/sql-database-xevent-code-event-file)」を参照してください。

::: moniker-end


#### <a name="create-event-session-with-event_file-target"></a>CREATE EVENT SESSION と **event_file** ターゲット


次に示すのは、テストに使用した CREATE EVENT SESSION です。 ADD TARGET 句の 1 つで、event_file を指定しています。


```sql
CREATE EVENT SESSION [locks_acq_rel_eventfile_22]
    ON SERVER 
    ADD EVENT sqlserver.lock_acquired
    (
        SET
            collect_database_name=(1),
            collect_resource_description=(1)

        ACTION (sqlserver.sql_text,sqlserver.transaction_id)

        WHERE
        (
            [database_name]=N'InMemTest2'
            AND
            [object_id]=(370100359)
        )
    ),
    ADD EVENT sqlserver.lock_released
    (
        SET
            collect_database_name=(1),
            collect_resource_description=(1)

        ACTION(sqlserver.sql_text,sqlserver.transaction_id)

        WHERE
        (
            [database_name]=N'InMemTest2'
            AND
            [object_id]=(370100359)
        )
    )
    ADD TARGET package0.event_counter,
    ADD TARGET package0.event_file
    (
        SET     filename=N'C:\Junk\locks_acq_rel_eventfile_22-.xel'
    )
    WITH
    (
        MAX_MEMORY=4096 KB,
        MAX_DISPATCH_LATENCY=10 SECONDS
    );
```


#### <a name="sysfn_xe_file_target_read_file-function"></a>sys.fn_xe_file_target_read_file 関数


event_file ターゲットは、人間が読むことのできないバイナリ形式で、受信したデータを格納します。 [**sys.fn_xe_file_target_read_file**](../../relational-databases/system-functions/sys-fn-xe-file-target-read-file-transact-sql.md) 関数に対して SELECT と FROM を使用して、.xel ファイルの内容を取得できます。


SQL Server **2016** 移行の場合、次の T-SQL SELECT でデータを取得します。 *.xel サフィックス 


```
SELECT f.*
        --,CAST(f.event_data AS XML)  AS [Event-Data-Cast-To-XML]  -- Optional
    FROM
        sys.fn_xe_file_target_read_file(
            'C:\junk\locks_acq_rel_eventfile_22-*.xel',
            null, null, null)  AS f;
```


SQL Server **2014**では、次のような SELECT でデータを取得します。 SQL Server 2014 より後では、.xem ファイルは使われなくなっています。


```
SELECT f.*
        --,CAST(f.event_data AS XML)  AS [Event-Data-Cast-To-XML]  -- Optional
    FROM
        sys.fn_xe_file_target_read_file(
            'C:\junk\locks_acq_rel_eventfile_22-*.xel',
            'C:\junk\metafile.xem',
            null, null)  AS f;
```


もちろん、SSMS UI を使用して手動で .xel データを見ることはできます。


#### <a name="data-stored-in-the-event_file-target"></a>event_file ターゲットに格納されているデータ


SQL Server 2016 で **sys.fn_xe_file_target_read_file**に SELECT を使用した結果を次に示します。


```
module_guid                            package_guid                           object_name     event_data                                                                                                                                                                                                                                                                                          file_name                                                      file_offset
-----------                            ------------                           -----------     ----------                                                                                                                                                                                                                                                                                          ---------                                                      -----------
D5149520-6282-11DE-8A39-0800200C9A66   03FDA7D0-91BA-45F8-9875-8B6DD0B8E9F2   lock_acquired   <event name="lock_acquired" package="sqlserver" timestamp="2016-08-07T20:13:35.827Z"><action name="transaction_id" package="sqlserver"><value>39194</value></action><action name="sql_text" package="sqlserver"><value><![CDATA[  select top 1 * from dbo.T_Target;  ]]></value></action></event>   C:\junk\locks_acq_rel_eventfile_22-_0_131150744126230000.xel   11776
D5149520-6282-11DE-8A39-0800200C9A66   03FDA7D0-91BA-45F8-9875-8B6DD0B8E9F2   lock_released   <event name="lock_released" package="sqlserver" timestamp="2016-08-07T20:13:35.832Z"><action name="transaction_id" package="sqlserver"><value>39194</value></action><action name="sql_text" package="sqlserver"><value><![CDATA[  select top 1 * from dbo.T_Target;  ]]></value></action></event>   C:\junk\locks_acq_rel_eventfile_22-_0_131150744126230000.xel   11776
```



<a name="h2_target_histogram"></a>

## <a name="histogram-target"></a>histogram ターゲット


**histogram** ターゲットは、event_counter ターゲットより高機能です。 histogram では次のことができます。

- 複数の項目の発生を個別にカウントする。
- 異なる種類の項目の発生をカウントする。
    - イベント フィールド。
    - アクション。


**source_type** パラメーターは、histogram ターゲットを制御するためのキーです。

- **source_type=0** - *イベント フィールド*のデータを収集します。
- **source_type=1** - *アクション*のデータを収集します。
    - 1 が既定値です。


"slots" パラメーターの既定値は 256 です。 別の値を割り当てると、値は次の 2 の累乗に切り上げられます。

- たとえば、slots=59 は 64 に切り上げられます。


### <a name="action-example-for-histogram"></a>histogram の*アクション* の例


次の CREATE EVENT SESSION ステートメントの TARGET...SET 句では、ターゲット パラメーターとして **source_type=1**を指定しています。 1 は、histogram ターゲットがアクションを追跡することを意味します。

この例では、EVENT...ACTION 句は **sqlos.system_thread_id**というターゲットの 1 つのアクションだけを提供します。 TARGET...SET 句では、 **source=N'sqlos.system_thread_id'** と割り当てられています。

- 複数のソース アクションを追跡するには、CREATE EVENT SESSION ステートメントに histogram ターゲットを追加します。


```sql
CREATE EVENT SESSION [histogram_lockacquired]
    ON SERVER 
    ADD EVENT sqlserver.lock_acquired
        (
        ACTION
            (
            sqlos.system_thread_id
            )
        )
    ADD TARGET package0.histogram
        (
        SET
            filtering_event_name=N'sqlserver.lock_acquired',
            slots=(16),
            source=N'sqlos.system_thread_id',
            source_type=1
        )
    WITH
        (
        <.... (For brevity, numerous parameter assignments generated by SSMS.exe are not shown here.) ....>
        );
```


 キャプチャされたデータを次に示します。 **value** 列の値は、system_thread_id の値です。 たとえば、全部で 236 個のロックがスレッド 6540 で取得されました。


```
value   count
-----   -----
 6540     236
 9308      91
 9668      74
10144      49
 5244      44
 2396      28
```


#### <a name="select-to-discover-available-actions"></a>使用可能なアクションを検出するための SELECT


[C.3](../../relational-databases/extended-events/selects-and-joins-from-system-views-for-extended-events-in-sql-server.md#section_C_3_select_all_available_objects) の SELECT ステートメントを使用すると、CREATE EVENT SESSION ステートメントで使用できるアクションを取得できます。 WHERE 句で、 **o.name LIKE** フィルターを編集して目的のアクションを指定します。


C.3 の SELECT で返される行セットの例を次に示します。 **system_thread_id** アクションは 2 行目にあります。


```
Package-Name   Action-Name                 Action-Description
------------   -----------                 ------------------
package0       collect_current_thread_id   Collect the current Windows thread ID
sqlos          system_thread_id            Collect current system thread ID
sqlserver      create_dump_all_threads     Create mini dump including all threads
sqlserver      create_dump_single_thread   Create mini dump for the current thread
```


### <a name="event-field-example-for-histogram"></a>histogram のイベント *フィールド* の例


次の例では、 **source_type=0**を設定します。 **source=** に割り当てられる値は、アクションではなくイベント フィールドです。



```sql
CREATE EVENT SESSION [histogram_checkpoint_dbid]
    ON SERVER 
    ADD EVENT  sqlserver.checkpoint_begin
    ADD TARGET package0.histogram
    (
    SET
        filtering_event_name = N'sqlserver.checkpoint_begin',
        source               = N'database_id',
        source_type          = (0)
    )
    WITH
    ( <....> );
```


histogram ターゲットでは次のようなデータがキャプチャされます。 このデータは、ID=5 のデータベースで checkpoint_begin イベントが 7 回発生したことを示しています。


```
value   count
-----   -----
5       7
7       4
6       3
```


#### <a name="select-to-discover-available-fields-on-your-chosen-event"></a>選択したイベントで使用可能なフィールドを検出する SELECT


[C.4](../../relational-databases/extended-events/selects-and-joins-from-system-views-for-extended-events-in-sql-server.md#section_C_4_data_fields) の SELECT ステートメントでは、選択できるイベント フィールドが示されます。 最初に、 **o.name LIKE** フィルターを編集して選択するイベント名を指定します。


C.4 SELECT からは次のような行セットが返されます。 この行セットでは、checkpoint_begin イベントが histogram ターゲットに提供できるフィールドは database_id の 1 つだけであることがわかります。


```
Package-Name   Event-Name         Field-Name   Field-Description
------------   ----------         ----------   -----------------
sqlserver      checkpoint_begin   database_id  NULL
sqlserver      checkpoint_end     database_id  NULL
```


<a name="h2_target_pair_matching"></a>

## <a name="pair_matching-target"></a>pair_matching ターゲット


pair_matching ターゲットを使用すると、対応する終了イベントのない開始イベントを検出できます。 たとえば、lock_acquired イベントが発生した後に適切なタイミングで対応する lock_released イベントが発生しないと、問題になる可能性があります。


システムで開始イベントと終了イベントが自動的にマッチングされることはありません。 代わりに、開発者が CREATE EVENT SESSION ステートメントでシステムにマッチングを示す必要があります。 開始イベントと終了イベントがマッチングする場合、ペアは破棄されるので、マッチングしていない開始イベントに注目できます。


#### <a name="finding-matchable-fields-for-the-start-and-end-event-pair"></a>開始イベントと終了イベントのペアのマッチングが可能なフィールドの検索


[C.4 の SELECT](../../relational-databases/extended-events/selects-and-joins-from-system-views-for-extended-events-in-sql-server.md#section_C_4_data_fields)を使用することで、次の行セットには lock_acquired イベントの対象になるフィールドが約 16 個あることがわかります。 ここで示されている行セットは、マッチングするフィールドがわかるように手動で分割されています。 **duration** などの一部のフィールドでは両方のイベントをマッチングできません。


```
Package-Name   Event-Name   Field-Name               Field-Description
------------   ----------   ----------               -----------------
sqlserver   lock_acquired   database_name            NULL
sqlserver   lock_acquired   mode                     NULL
sqlserver   lock_acquired   resource_0               The ID of the locked object, when lock_resource_type is OBJECT.
sqlserver   lock_acquired   resource_1               NULL
sqlserver   lock_acquired   resource_2               The ID of the lock partition, when lock_resource_type is OBJECT, and resource_1 is 0.
sqlserver   lock_acquired   transaction_id           NULL

sqlserver   lock_acquired   associated_object_id     The ID of the object that requested the lock that was acquired.
sqlserver   lock_acquired   database_id              NULL
sqlserver   lock_acquired   duration                 The time (in microseconds) between when the lock was requested and when it was canceled.
sqlserver   lock_acquired   lockspace_nest_id        NULL
sqlserver   lock_acquired   lockspace_sub_id         NULL
sqlserver   lock_acquired   lockspace_workspace_id   NULL
sqlserver   lock_acquired   object_id                The ID of the locked object, when lock_resource_type is OBJECT. For other lock resource types it will be 0
sqlserver   lock_acquired   owner_type               NULL
sqlserver   lock_acquired   resource_description     The description of the lock resource. The description depends on the type of lock. This is the same value as the resource_description column in the sys.dm_tran_locks view.
sqlserver   lock_acquired   resource_type            NULL
```


### <a name="example-of-pair_matching"></a>pair_matching の例


次の CREATE EVENT SESSION ステートメントでは、2 つのイベントと 2 つのターゲットが指定されています。 pair_matching ターゲットでは、イベントをペアにするために 2 つのフィールド セットが指定されています。 **begin_matching_columns=** と **end_matching_columns=** に割り当てるコンマ区切りフィールドのシーケンスは同じでなければなりません。 コンマ区切り値で示されるフィールドの間にタブや改行文字があってはなりませんが、スペースは許されます。

結果を絞り込むため、最初に sys.objects から SELECT でテスト テーブルの object_id を抽出してあります。 その 1 つの ID に対するフィルターを EVENT...WHERE 句に追加してあります。


```sql
CREATE EVENT SESSION [pair_matching_lock_a_r_33]
    ON SERVER 
    ADD EVENT sqlserver.lock_acquired
    (
        SET
            collect_database_name = (1),
            collect_resource_description = (1)

        ACTION (sqlserver.transaction_id)

        WHERE
        (
            [database_name] = 'InMemTest2'
            AND
            [object_id] = 370100359
        )
    ),
    ADD EVENT sqlserver.lock_released
    (
        SET
            collect_database_name = (1),
            collect_resource_description = (1)

        ACTION (sqlserver.transaction_id)

        WHERE
        (
            [database_name] = 'InMemTest2'
            AND
            [object_id] = 370100359
        )
    )
    ADD TARGET package0.event_counter,
    ADD TARGET package0.pair_matching
    (
        SET
            begin_event = N'sqlserver.lock_acquired',
            begin_matching_columns =
                N'resource_0, resource_1, resource_2, transaction_id, database_id',

            end_event = N'sqlserver.lock_released',
            end_matching_columns =
                N'resource_0, resource_1, resource_2, transaction_id, database_id',

            respond_to_memory_pressure = (1)
    )
    WITH
    (
        MAX_MEMORY = 8192 KB,
        MAX_DISPATCH_LATENCY = 15 SECONDS
    );
```


イベント セッションをテストするため、意図的に、取得したロックが解放されないようにしています。 次のような T-SQL 手順を使用しました。

1. BEGIN TRANSACTION
2. UPDATE MyTable...
3. ターゲットを調べる終わるまで、意図的に COMMIT TRANSACTION を発行しない
4. テストの後で、COMMIT TRANSACTION を発行する

簡単な **event_counter** ターゲットでは次のような出力行が得られました。 52-50=2 なので、この出力からは、pair-matching ターゲットからの出力を調べるときにペアになっていない 2 つの lock_acquired イベントを探す必要があることがわかります。


```
package_name   event_name      count
------------   ----------      -----
sqlserver      lock_acquired   52
sqlserver      lock_released   50
```


**pair_matching** の出力は次のとおりです。 event_counter の出力で示されているように、2 つの lock_acquired 行を調べます。 これら 2 つの lock_acquired イベントはペアになっていません。


```
package_name   event_name      timestamp                     database_name   duration   mode   object_id   owner_type   resource_0   resource_1   resource_2   resource_description   resource_type   transaction_id
------------   ----------      ---------                     -------------   --------   ----   ---------   ----------   ----------   ----------   ----------   --------------------   -------------   --------------
sqlserver      lock_acquired   2016-08-05 12:45:47.9980000   InMemTest2      0          S      370100359   Transaction  370100359    3            0            [INDEX_OPERATION]      OBJECT          34126
sqlserver      lock_acquired   2016-08-05 12:45:47.9980000   InMemTest2      0          IX     370100359   Transaction  370100359    0            0                                   OBJECT          34126
```


ペアになっていない lock_acquired イベントの行には、ロックを取得する T-SQL テキスト **sqlserver.sql_text**が含まれる場合があります。 表示が多くなるので示してはありません。


<a name="h2_target_ring_buffer"></a>

## <a name="ring_buffer-target"></a>ring_buffer ターゲット


ring_buffer ターゲットは、簡単なイベントのテストに便利です。 イベント セッションを停止すると、格納されている出力は破棄されます。

この ring_buffer のセクションでは、XQuery の Transact-SQL 実装を使用して ring_buffer の XML の内容をもっと読みやすいリレーショナル行セットにコピーする方法も示します。


#### <a name="create-event-session-with-ring_buffer"></a>CREATE EVENT SESSION と ring_buffer


ring_buffer を使用するこの CREATE EVENT SESSION ステートメントに関して特別なことは何もありません。


```sql
CREATE EVENT SESSION [ring_buffer_lock_acquired_4]
    ON SERVER 
    ADD EVENT sqlserver.lock_acquired
    (
        SET collect_resource_description=(1)

        ACTION(sqlserver.database_name)

        WHERE
        (
            [object_id]=(370100359)  -- ID of MyTable
            AND
            sqlserver.database_name='InMemTest2'
        )
    )
    ADD TARGET package0.ring_buffer
    (
        SET max_events_limit=(98)
    )
    WITH
    (
        MAX_MEMORY=4096 KB,
        MAX_DISPATCH_LATENCY=3 SECONDS
    );
```


### <a name="xml-output-received-for-lock_acquired-by-ring_buffer"></a>ring_buffer が受け取る lock_acquired に関する XML 形式の出力


SELECT から取得する内容は XML 形式の文字列です。 このテストで ring_buffer ターゲットが格納した XML 文字列を次に示します。 ただし、簡潔にするため、2 つの &#x3c;event&#x3e; 要素以外はすべて除去してあります。 さらに、各 &#x3c;event&#x3e; に含まれる関係のない &#x3c;data&#x3e; 要素も削除してあります。


```xml
<RingBufferTarget truncated="0" processingTime="0" totalEventsProcessed="6" eventCount="6" droppedCount="0" memoryUsed="1032">
  <event name="lock_acquired" package="sqlserver" timestamp="2016-08-05T23:59:53.987Z">
    <data name="mode">
      <type name="lock_mode" package="sqlserver"></type>
      <value>1</value>
      <text><![CDATA[SCH_S]]></text>
    </data>
    <data name="transaction_id">
      <type name="int64" package="package0"></type>
      <value>111030</value>
    </data>
    <data name="database_id">
      <type name="uint32" package="package0"></type>
      <value>5</value>
    </data>
    <data name="resource_0">
      <type name="uint32" package="package0"></type>
      <value>370100359</value>
    </data>
    <data name="resource_1">
      <type name="uint32" package="package0"></type>
      <value>0</value>
    </data>
    <data name="resource_2">
      <type name="uint32" package="package0"></type>
      <value>0</value>
    </data>
    <data name="database_name">
      <type name="unicode_string" package="package0"></type>
      <value><![CDATA[]]></value>
    </data>
    <action name="database_name" package="sqlserver">
      <type name="unicode_string" package="package0"></type>
      <value><![CDATA[InMemTest2]]></value>
    </action>
  </event>
  <event name="lock_acquired" package="sqlserver" timestamp="2016-08-05T23:59:56.012Z">
    <data name="mode">
      <type name="lock_mode" package="sqlserver"></type>
      <value>1</value>
      <text><![CDATA[SCH_S]]></text>
    </data>
    <data name="transaction_id">
      <type name="int64" package="package0"></type>
      <value>111039</value>
    </data>
    <data name="database_id">
      <type name="uint32" package="package0"></type>
      <value>5</value>
    </data>
    <data name="resource_0">
      <type name="uint32" package="package0"></type>
      <value>370100359</value>
    </data>
    <data name="resource_1">
      <type name="uint32" package="package0"></type>
      <value>0</value>
    </data>
    <data name="resource_2">
      <type name="uint32" package="package0"></type>
      <value>0</value>
    </data>
    <data name="database_name">
      <type name="unicode_string" package="package0"></type>
      <value><![CDATA[]]></value>
    </data>
    <action name="database_name" package="sqlserver">
      <type name="unicode_string" package="package0"></type>
      <value><![CDATA[InMemTest2]]></value>
    </action>
  </event>
</RingBufferTarget>
```


上の XML を取得するには、イベント セッションがアクティブになっている間に次の SELECT を発行します。 アクティブな XML データが、システム ビュー **sys.dm_xe_session_targets**から取得されます。


```sql
SELECT
        CAST(LocksAcquired.TargetXml AS XML)  AS RBufXml
    INTO
        #XmlAsTable
    FROM
        (
        SELECT
                CAST(t.target_data AS XML)  AS TargetXml
            FROM
                     sys.dm_xe_session_targets  AS t
                JOIN sys.dm_xe_sessions         AS s

                    ON s.address = t.event_session_address
            WHERE
                t.target_name = 'ring_buffer'
                AND
                s.name        = 'ring_buffer_lock_acquired_4'
        )
            AS LocksAcquired;


SELECT * FROM #XmlAsTable;
```


### <a name="xquery-to-see-the-xml-as-a-rowset"></a>XML を行セットとして表示するための XQuery


上の XML をリレーショナル行セットとして表示するには、上の SELECT ステートメントに続けて次の T-SQL ステートメントを発行します。 コメントの付いた行では、各 XQuery の使用方法が説明されています。


```sql
SELECT
         -- (A)
         ObjectLocks.value('(@timestamp)[1]',
            'datetime'     )  AS [OccurredDtTm]

        -- (B)
        ,ObjectLocks.value('(data[@name="mode"]/text)[1]',
            'nvarchar(32)' )  AS [Mode]

        -- (C)
        ,ObjectLocks.value('(data[@name="transaction_id"]/value)[1]',
            'bigint' )  AS [TxnId]

        -- (D)
        ,ObjectLocks.value('(action[@name="database_name" and @package="sqlserver"]/value)[1]',
            'nvarchar(128)')  AS [DatabaseName]
    FROM
        #TableXmlCell
    CROSS APPLY
        -- (E)
        TargetDateAsXml.nodes('/RingBufferTarget/event[@name="lock_acquired"]')  AS T(ObjectLocks);
```


#### <a name="xquery-notes-from-preceding-select"></a>前の SELECT で使用されている XQuery に関するメモ


(A)
- timestamp = &#x3c;event&#x3e; 要素での属性の値。
- '(...)[1]' の構造により、繰り返しごとにただ 1 つの値が返されることが保証されます。これは、XML データ型の変数と列を持つ .value() XQuery メソッドで要求されている制限です。


(B)
- name= 属性が "mode" に等しい &#x3c;data&#x3e; 要素内の &#x3c;text&#x3e; 要素の中の値。


(C)
- name= 属性が "transaction_id" に等しい &#x3c;data&#x3e; 要素内の &#x3c;value&#x3e; 要素の中の値。


(D)
- &#x3c;event&#x3e; には &#x3c;action&#x3e; が含まれます。
- name= 属性が "database_name" で package= 属性が "sqlserver" ("package0" ではありません) である &#x3c;action&#x3e; は、&#x3c;value&#x3e; 要素の中の値を取得します。


(E)
- この CROSS APPLY 句は、name= 属性が "lock_acquired" であるすべての &#x3c;event&#x3e; 要素を個別に反復処理します。
- これは、上の FROM 句から返された XML に対して行われます。


#### <a name="output-from-xquery-select"></a>XQuery SELECT からの出力


次に示すのは、前の XQuery を含む T-SQL によって生成された行セットです。


```
OccurredDtTm              Mode    DatabaseName
------------              ----    ------------
2016-08-05 23:59:53.987   SCH_S   InMemTest2
2016-08-05 23:59:56.013   SCH_S   InMemTest2
```



## <a name="xevent-net-namespaces-and-cx23"></a>XEvent .NET の名前空間と C&#x23;


Package0 にはさらに次の 2 つのターゲットがありますが、Transact-SQL では使用できません。

- compressed_history
- event_stream


これら 2 つのターゲットを T-SQL で使用できない理由の 1 つは、列 *sys.dm_xe_objects.capabilities* の非 null 値にビット 0x1 が含まれないことです。


event_stream ターゲットは、C# などの言語で記述された .NET プログラムでは使用できます。 C# および他の .NET 開発者は、名前空間 Microsoft.SqlServer.XEvents.Linq に含まれるものなどの .NET Framework クラスを使用して、イベント ストリームにアクセスできます。

発生する可能性がある **25726** エラーは、データが格納されたイベント ストリームがクライアントのデータ処理より速いことを意味します。 これにより、サーバーのパフォーマンス低下を回避するため、データベース エンジンはイベント ストリームから切断されています。


### <a name="xevent-namespaces"></a>XEvent の名前空間


- [Microsoft.SqlServer.Management.XEvent 名前空間](https://msdn.microsoft.com/library/microsoft.sqlserver.management.xevent.aspx)

- [Microsoft.SqlServer.XEvent.Linq 名前空間](https://msdn.microsoft.com/library/microsoft.sqlserver.xevent.linq.aspx)



