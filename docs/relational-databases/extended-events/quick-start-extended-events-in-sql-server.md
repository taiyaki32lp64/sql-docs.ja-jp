---
title: クイック スタート:SQL Server の拡張イベント
ms.date: 05/28/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xevents
ms.topic: quickstart
ms.assetid: 7bb78b25-3433-4edb-a2ec-c8b2fa58dea1
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8e4512400d2f05500f2db9a98a72f57ac50bc3a7
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75242921"
---
# <a name="quickstart-extended-events-in-sql-server"></a>クイック スタート:SQL Server の拡張イベント

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]


拡張イベントは、SQL Server に関する問題の監視とトラブルシューティングを行うために必要なデータを収集できるようにする、軽量なパフォーマンス監視システムです。 拡張イベントのアーキテクチャについて詳しくは、「[拡張イベントの概要](extended-events.md)」をご覧ください。  この記事は、拡張イベントを初めて使用する SQL 開発者および数分でイベント セッションを作成したい SQL 開発者を対象としています。 拡張イベントを使用すると、SQL システムと自身のアプリケーションの内部処理に関する詳細を確認できます。 拡張イベント セッションを作成するときに、システムを以下のことを指示します。

- 興味がある事象
- システムにデータを報告させる方法


この記事では、次のことを行います。

- スクリーン ショットを使用して、イベント セッションを作成する SSMS.exe のクリックを示します。
- スクリーン ショットを相当する TRANSACT-SQL ステートメントに関連付けます。
- イベント セッションの用語と、クリックおよび T-SQL の背後にある概念を詳しく説明します。
- イベント セッションをテストする方法を示します。
- 結果を回避する代替策について説明します。
  - 結果のストレージ キャプチャ
  - 処理済み結果と生の結果の比較
  - さまざまな方法および異なる時間単位で結果を表示するためのツール
- 使用可能なすべてのイベントの検索および検出方法を示します。
- 拡張イベントの動的管理ビュー (DMV) 間の、主キーと外部キーの暗黙的なリレーションシップを提供します。
- 関連記事で学習できることについて説明します。


ブログやくだけた会話では、拡張イベントは *xevent*という略称で呼ばれることがあります。


> [!NOTE]
> Microsoft SQL Server と Azure SQL Database の拡張イベントの違いに関する詳細は、「 [SQL データベースの拡張イベント](https://azure.microsoft.com/documentation/articles/sql-database-xevent-db-diff-from-svr/)」を参照してください。


## <a name="preparations-before-demo"></a>デモの準備


次のデモを実際に行うには、以下の準備作業が必要になります。

1. [SQL Server Management Studio (SSMS) のダウンロード](https://msdn.microsoft.com/library/mt238290.aspx)
  - 毎月更新される最新の SSMS を毎月インストールする必要があります。
2. Microsoft SQL Server 2014 以降にログインするか、 `SELECT @@version` が返す値の最初のノードが 12 以上の Azure SQL Database のデータベースにログインします。
3. 自身のアカウントに [ALTER ANY EVENT SESSION](../../t-sql/statements/grant-server-permissions-transact-sql.md) の **サーバー アクセス許可**があることを確認します。
  - 拡張イベントに関するセキュリティとアクセス権に興味がある場合は、この記事の末尾にある「 [付録](#appendix1)」で詳細を確認できます。




## <a name="demo-of-ssms-integration"></a>SSMS 統合のデモ


SSMS.exe では、拡張イベント向けに優れたユーザー インターフェイス (UI) を提供しています。 この UI はとても優れているため、多くのユーザーは拡張イベントを扱うために、Transact-SQL や拡張イベントを対象とする動的管理ビュー (DMV) を使用する必要がありません。

このセクションでは、拡張イベントを作成し、レポート データを表示する UI の手順について確認できます。 この手順の後に、より深く理解するために手順に関係する概念について参照できます。


### <a name="steps-of-demo"></a>デモの手順


デモを行わない場合でも、手順を理解できます。 デモにより **[新しいセッション]** ダイアログが起動します。 次の 4 つのページを処理します。

- 全般
- events
- データ ストレージ
- 詳細設定


SSMS UI が数カ月または数年にわたって微調整されると、テキストとそれを補助するスクリーンショットが少し正確ではなくなる場合があります。 しかしながら、差異がほんのわずかなものであれば、スクリーンショットは説明には十分に役立ちます。


1. SSMS と接続します。

2. オブジェクト エクスプローラーで、 **[管理]**  >  **[拡張イベント]**  >  **[新しいセッション]** をクリックします。 **[新しいセッション]** ダイアログと **新規セッション ウィザード**は互いに似ていますが、[新しいセッション] をお勧めします。

3. 左上で、 **[全般]** ページをクリックします。 *[セッション名]* テキスト ボックスに ” **YourSession** ” または任意の名前を入力します。 **[OK]** ボタンはデモの終了時にのみ押すため、まだ*押さないで*ください。

    ![[新しいセッション] > [全般] > [セッション名]](../../relational-databases/extended-events/media/xevents-session-newsessions-10-general-ssms-yoursessionnode.png)

4. 左上で **[イベント]** ページをクリックして、 **[選択]** ボタンをクリックします。

    ![[新しいセッション] > [イベント] > [選択] > [イベント ライブラリ]、選択されたイベント](../../relational-databases/extended-events/media/xevents-session-newsessions-14-events-ssms-rightclick-not-wizard.png)

5. **[イベント ライブラリ]** の領域で、ドロップダウン リストから **[イベント名のみ]** を選択します。
    - テキスト ボックスに ” **sql**" を入力します。これは、 *contains* 演算子を使用して、使用可能なイベントの長いリストをフィルター処理して短くします。
    - スクロールして、 **sql_statement_completed**という名前のイベントをクリックします。
    - 右矢印ボタン **>** をクリックして、イベントを **[選択したイベント]** ボックスに移動します。

6. **[イベント]** ページで、右端にある **[構成]** ボタンをクリックします。
    - 見やすくするために左側を切り取った次のスクリーンショットで、 **[イベントの構成オプション]** 領域を確認できます。

    ![[新しいセッション] > [イベント] > [構成] > [フィルター (述語)] > [フィールド]](../../relational-databases/extended-events/media/xevents-session-newsessions-20b-events-ssms-yoursessionnode.png)

7. **[フィルター (述語)]** タブをクリックします。次に、HAVING 句を含むすべての SQL SELECT ステートメントをキャプチャするため、 **[句を追加するにはここをクリックします]** をクリックします。

8. **[フィールド]** ドロップ ダウン リストから、 **[sqlserver.sql_text]** を選択します。
   - **[演算子]** に LIKE 演算子を選択します。
   - **[値]** に " **%SELECT%HAVING%** ” を入力します。

    > [!NOTE]
    > この 2 部構成の名前では、 *sqlserver* がパッケージ名、 *sql_text* がフィールド名です。 前の手順で選択したイベント *sql_statement_completed* は、選択したフィールドと同じパッケージ内にある必要があります。

9. 左上で、 **[データ ストレージ]** ページをクリックします。

10. **[ターゲット]** 領域で、 **[ここをクリックしてターゲットを追加]** をクリックします。
    - **[種類]** ドロップダウン リストで、 **[event_file]** を選択します。
    - これは、イベント データが表示可能なファイルに格納されることを意味します。

    ![[新しいセッション] > [データ ストレージ] > [ターゲット] > [種類] > [event_file]](../../relational-databases/extended-events/media/xevents-session-newsessions-30-datastorage-ssms-yoursessionnode.png)

11. **[プロパティ]** 領域で、 **[サーバー上のファイル名]** テキスト ボックスに完全パスとファイル名を入力します。
    - ファイル名の拡張子は *.xel*にする必要があります。
    - この簡単なテストでは、1 MB 未満のファイル サイズが必要になります。

    ![[新しいセッション] > [詳細] > [ディスパッチの最大待機時間] > [OK]](../../relational-databases/extended-events/media/xevents-session-newsessions-40-advanced-ssms-yoursessionnode.png)

12. 左上で、 **[詳細]** ページをクリックします。
    - **[ディスパッチの最大待機時間]** を 3 秒に減らします。
    - 最後に、下部にある **[OK]** ボタンをクリックします。

13. **オブジェクト エクスプローラー**に戻り、 **[管理]**  >  **[セッション]** の順に展開して、**YourSession** の新しいノードを表示します。

    ![オブジェクト エクスプローラーで [管理] > [拡張イベント] > [セッション] の下に表示される YourSession という名前の新しい *イベント セッション* のノード](../../relational-databases/extended-events/media/xevents-session-newsessions-50-objectexplorer-ssms-yoursessionnode.png)


#### <a name="edit-your-event-session"></a>イベント セッションの編集


SSMS **オブジェクト エクスプローラー**でイベント セッションを編集するには、そのノードを右クリックして、 **[プロパティ]** をクリックします。 同じマルチページのダイアログが表示されます。


### <a name="corresponding-t-sql-for-your-event-session"></a>イベント セッションに対応する T-SQL


SSMS UI を使用して、イベント セッションを作成した T-SQL スクリプトを生成しました。 生成されたスクリプトは、次の手順で表示できます。

- セッション ノードを右クリックし、 **[セッションをスクリプト化]**  >  **[CREATE]**  >  **[クリップボード]** の順にクリックします。
- 任意のテキスト エディターに貼り付けます。


次は、UI でのクリックで生成された、 *YourSession*の T-SQL CREATE EVENT SESSION ステートメントです。


```sql
CREATE EVENT SESSION [YourSession]
    ON SERVER 
    ADD EVENT sqlserver.sql_statement_completed
    (
        ACTION(sqlserver.sql_text)
        WHERE
        ( [sqlserver].[like_i_sql_unicode_string]([sqlserver].[sql_text], N'%SELECT%HAVING%')
        )
    )
    ADD TARGET package0.event_file
    (SET
        filename = N'C:\Junk\YourSession_Target.xel',
        max_file_size = (2),
        max_rollover_files = (2)
    )
    WITH (
        MAX_MEMORY = 2048 KB,
        EVENT_RETENTION_MODE = ALLOW_MULTIPLE_EVENT_LOSS,
        MAX_DISPATCH_LATENCY = 3 SECONDS,
        MAX_EVENT_SIZE = 0 KB,
        MEMORY_PARTITION_MODE = NONE,
        TRACK_CAUSALITY = OFF,
        STARTUP_STATE = OFF
    );
GO
```


> [!NOTE]
> Azure SQL Database の場合、上記の CREATE EVENT SESSION ステートメントの ON SERVER 句は ON DATABASE になります。
> 
> Microsoft SQL Server と Azure SQL Database の拡張イベントの違いに関する詳細は、「 [SQL データベースの拡張イベント](https://azure.microsoft.com/documentation/articles/sql-database-xevent-db-diff-from-svr/)」を参照してください。


#### <a name="pre-drop-of-the-event-session"></a>イベント セッションの事前 DROP


CREATE EVENT SESSION ステートメントの前に、名前が既に存在する場合に備えて、DROP EVENT SESSION を条件付きで発行することができます。


```sql
IF EXISTS (SELECT *
      FROM sys.server_event_sessions    -- If Microsoft SQL Server.
    --FROM sys.database_event_sessions  -- If Azure SQL Database in the cloud.
      WHERE name = 'YourSession')
BEGIN
    DROP EVENT SESSION YourSession
          ON SERVER;    -- If Microsoft SQL Server.
        --ON DATABASE;  -- If Azure SQL Database.
END
go
```


#### <a name="alter-to-start-and-stop-the-event-session"></a>イベント セッションを開始または停止するための ALTER


イベント セッションを作成する際の既定は、自動的に実行を開始しないです。 次の T-SQL ALTER EVENT SESSION ステートメントを使用して、いつでもイベント セッションを開始または停止することができます。


```sql
ALTER EVENT SESSION [YourSession]
      ON SERVER
    --ON DATABASE
    STATE = START;   -- STOP;
```


SQL Server インスタンスの開始時に、自動的に開始するようにイベント セッションに指示することもできます。 CREATE EVENT SESSION でキーワード **STARTUP STATE = ON** を参照してください。

- SSMS UI は **[新しいセッション]**  >  **[全般]** ページで対応するチェック ボックスを提供しています。


## <a name="test-your-event-session"></a>イベント セッションのテスト


次の簡単な手順を使って、イベント セッションをテストします。

1. SSMS **オブジェクト エクスプローラー**で、イベント セッション ノードを右クリックし、 **[セッションの開始]** をクリックします。
2. 次の `SELECT...HAVING` ステートメントを 2 回実行します。
    - 理想的には、2 回の実行の間に `HAVING Count` の値を2 と 3 に切り替えます。 これにより結果の違いを確認することができます。
3. セッション ノードを右クリックして、 **[セッションの停止]** をクリックします。
4. 次のサブセクションで、 [SELECT を使用して結果を表示する方法](#select-the-full-results-xml-37)についてお読みください。



```sql
SELECT
        c.name,
        Count(*)  AS [Count-Per-Column-Repeated-Name]
    FROM
             sys.syscolumns  AS c
        JOIN sys.sysobjects  AS o
    
            ON o.id = c.id
    WHERE
        o.type = 'V'
        AND
        c.name like '%event%'
    GROUP BY
        c.name
    HAVING
        Count(*) >= 3   --2     -- Try both values during session.
    ORDER BY
        c.name;
```


完全を期すためだけに、上記の SELECT...HAVING からおおよその出力を以下に示します。


```
/*** Approximate output, 6 rows, all HAVING Count >= 3:
name                   Count-Per-Column-Repeated-Name
---------------------  ------------------------------
event_group_type       4
event_group_type_desc  4
event_session_address  5
event_session_id       5
is_trigger_event       4
trace_event_id         3
***/
```



<a name="select-the-full-results-xml-37"/>

### <a name="select-the-full-results-as-xml"></a>XML での完全な結果の SELECT


SSMS で、次の T-SQL SELECT を実行し、各行が 1 つのイベントの発生に関するデータを提供する結果を返します。 CAST AS XML は、結果を見やすく表示します。


> [!NOTE]
> イベント システムは常に指定した *.xel* event_file ファイル名に long 型の値を付加します。 ファイルから次の SELECT を実行するには、事前にシステムによって付与された完全名をコピーして、SELECT 内に貼り付ける必要があります。


```sql
SELECT
        object_name,
        file_name,
        file_offset,
        event_data,
        'CLICK_NEXT_CELL_TO_BROWSE_XML RESULTS!'
                AS [CLICK_NEXT_CELL_TO_BROWSE_XML_RESULTS],
    
        CAST(event_data AS XML) AS [event_data_XML]
                -- TODO: In ssms.exe results grid, double-click this xml cell!
    FROM
        sys.fn_xe_file_target_read_file(
            'C:\Junk\YourSession_Target_0_131085363367310000.xel',
            null, null, null
        );
```


上記の SELECT では、任意のイベント行の完全な結果を表示するために 2 とおりの方法を提供しています。

- SSMS で SELECT を実行し、 **event_data_XML** 列内のセルをクリックします。 これは非常に便利です。
- **event_data** 列内のセルから長い XML 文字列をコピーします。 文字列を Notepad.exe のようなシンプルなテキスト エディターに貼り付けて、ファイルを .XML 拡張子で保存します。 次に、ブラウザーを使用して .XML ファイルを開きます。


#### <a name="display-of-results-for-one-event"></a>1 つのイベントの結果の表示


次に、XML 形式で結果の一部を確認します。 ここでの XML は、表示を短くするために編集されています。 `<data name="row_count">` は `6`の値を表示します。これは、上記で表示した 6 つの結果の行に一致します。 SELECT ステートメント全体を表示できます。


```xml
<event name="sql_statement_completed" package="sqlserver" timestamp="2016-05-24T04:06:08.997Z">
  <data name="duration">
    <value>111021</value>
  </data>
  <data name="cpu_time">
    <value>109000</value>
  </data>
  <data name="physical_reads">
    <value>0</value>
  </data>
  <data name="last_row_count">
    <value>6</value>
  </data>
  <data name="offset">
    <value>0</value>
  </data>
  <data name="offset_end">
    <value>584</value>
  </data>
  <data name="statement">
    <value>SELECT
        c.name,
        Count(*)  AS [Count-Per-Column-Repeated-Name]
    FROM
             sys.syscolumns  AS c
        JOIN sys.sysobjects  AS o

            ON o.id = c.id
    WHERE
        o.type = 'V'
        AND
        c.name like '%event%'
    GROUP BY
        c.name
    HAVING
        Count(*) &gt;= 3   --2     -- Try both values during session.
    ORDER BY
        c.name</value>
  </data>
</event>
```


## <a name="ssms-to-display-results"></a>SSMS を使用して結果を表示する


拡張イベントからキャプチャされたデータを表示ために使用できる SSMS UI には、いくつかの高度な機能があります。 詳細については、以下を参照してください。

- [SQL Server での拡張イベントからのターゲット データの詳細表示](../../relational-databases/extended-events/advanced-viewing-of-target-data-from-extended-events-in-sql-server.md)


基本は、 **[ターゲット データの表示]** と **[ライブ データの監視]** のラベルが付いた、ショートカット メニュー オプションで始めます。


### <a name="view-target-data"></a>[ターゲット データの表示]


SSMS **オブジェクト エクスプローラー**で、イベント セッション ノードの下にあるターゲット ノードを右クリックします。 コンテキスト メニューで **[ターゲット データの表示]** をクリックします。 SSMS でデータが表示されます。

新しいデータはイベントで報告されているため、表示は更新されません。 しかし、 **[ターゲット データの表示]** をもう一度クリックできます。


![[ターゲット データの表示]、SSMS で、[管理] > [拡張イベント] > [セッション] > [YourSession] > [package0.event_file]、右クリック](../../relational-databases/extended-events/media/xevents-viewtargetdata-ssms-targetnode-61.png)


### <a name="watch-live-data"></a>[ライブ データの監視]


SSMS **オブジェクト エクスプローラー**で、イベント セッション ノードを右クリックします。 コンテキスト メニューで **[ライブ データの監視]** をクリックします。 SSMS では、受信データがリアルタイムで引き続き到着するため、受信データが表示されます。


![[ライブ データの監視]、SSMS で、[管理] > [拡張イベント] > [セッション] > [YourSession]、右クリック](../../relational-databases/extended-events/media/xevents-watchlivedata-ssms-yoursessionnode-63.png)


## <a name="scenarios"></a>シナリオ


拡張イベントの効果的な使用には、多くのシナリオがあります。 次の記事では、クエリ中に取得したロックに関連するシナリオの例を示します。


ロックの評価を目的としたイベント セッションの具体的なシナリオは、次の記事で説明しています。 これらの記事では、 **\@dbid** の使用や、動的な `EXECUTE (@YourSqlString)` の使用など、高度な技法もいくつか紹介されています。

- [ロックの大半を取得しているオブジェクトを見つける](../../relational-databases/extended-events/find-the-objects-that-have-the-most-locks-taken-on-them.md)
  - このシナリオでは、生のイベント データを表示する前に処理するターゲット package0.histogram を使用します。
- [ロックを保持しているクエリの特定](../../relational-databases/extended-events/determine-which-queries-are-holding-locks.md)
  - このシナリオは、sqlserver.lock_acquire と lock_release がイベントのペアとなる、 [ターゲット package0.pair_matching](https://msdn.microsoft.com/library/3c87dcfb-543a-4bd8-a73d-1390bdf4ffa3)を使用します。


## <a name="terms-and-concepts-in-extended-events"></a>拡張イベントの用語と概念


次の表は、拡張イベントで使用される用語とその意味を示しています。


| 期間 | [説明] |
| :--- | :---------- |
| イベント セッション | 1 つ以上のイベントを中心にしたコンストラクトと、アクションなどのサポート アイテムがターゲットです。 CREATE EVENT SESSION ステートメントは、各イベント セッションを構築します。 ALTER を使用してイベント セッションを任意に開始、停止できます。 <br/> <br/> イベント セッションは、文脈から *イベント セッション*を指していることが明らかな場合には、単に *セッション*と呼ばれることがあります。 <br/> <br/> イベント セッションの詳細については、次で説明しています。[SQL Server 拡張イベント セッション](../../relational-databases/extended-events/sql-server-extended-events-sessions.md)。 |
| イベント | アクティブなイベント セッションによって監視されるシステムでの内の特定の事象です。 <br/> <br/> たとえば、 *sql_statement_completed* イベントは、指定された T-SQL ステートメントが完了した時点を表します。 イベントは、その継続時間とその他のデータを報告できます。 |
| ターゲット (target) | キャプチャしたイベントからの出力データを受信するアイテムです。 ターゲットはデータを表示します。 <br/> <br/> 例には、 *event_file*と、それに類似する便利な軽量メモリ *ring_buffer*が含まれています。 より魅力的な *ヒストグラム* ターゲットが、データを表示する前にいくつかの処理を実行します。 <br/> <br/> どのターゲットも任意のイベント セッションに使用できます。 詳細については、「 [Targets for Extended Events in SQL Server](../../relational-databases/extended-events/targets-for-extended-events-in-sql-server.md)」 (SQL Server の拡張イベントのターゲット) を参照してください。 |
| action | イベントにとって既知のフィールドです。 フィールドのデータは、ターゲットに送信されます。 アクション フィールドは *述語フィルター*に密接に関係しています。 |
| 述語フィルター | イベント発生の興味のあるサブセットのみがターゲットに送信されるように使用される、イベント フィールド内のデータのテストです。 <br/> <br/> たとえば、フィルターには、T-SQL ステートメントが文字列 *HAVING* を含めている、これらの *sql_statement_completed*イベント発生のみを含めることができます。 |
| パッケージ | イベントのコアを軸として展開するアイテム セット内の各アイテムにアタッチされている名前修飾子です。 <br/> <br/> たとえば、パッケージには、T-SQL テキストに関するイベントを含めることができます。 1 つのイベントが、GO 区切り文字のバッチ内のすべての T-SQL に関係する場合があります。 一方、個別の T-SQL ステートメントに関する別のより狭義のイベントもあります。 さらに、どの T-SQL ステートメントにも、開始イベントと完了イベントがあります。 <br/> <br/> イベントに適したフィールドも、イベントとともにパッケージされています。 ほとんどのターゲットが *package0* 内にあり、その他の多くのパッケージからのイベントとともに使用されます。 |


## <a name="how-to-discover-the-available-events-in-packages"></a>パッケージ内で使用可能なイベントを見つける方法


次の T-SQL SELECT は、名前に 'sql' の 3 文字を含む使用可能な各イベントの行を返します。 もちろん、LIKE 値を編集して別のイベント名を検索することもできます。 行は、イベントを含むパッケージにも名前を付けます。


```sql
SELECT   -- Find an event you want.
        p.name         AS [Package-Name],
        o.object_type,
        o.name         AS [Object-Name],
        o.description  AS [Object-Descr],
        p.guid         AS [Package-Guid]
    FROM
              sys.dm_xe_packages  AS p
        JOIN  sys.dm_xe_objects   AS o
    
                ON  p.guid = o.package_guid
    WHERE
        o.object_type = 'event'   --'action'  --'target'
        AND
        p.name LIKE '%'
        AND
        o.name LIKE '%sql%'
    ORDER BY
        p.name, o.object_type, o.name;
```


次の表示は返された行を示しています。ここでは列名 = 値の形式に編集されています。 データは、前の手順の例で使用された *sql statement_completed* イベントからのものです。 Object-Descr 列の文が特に便利です。


```  
Package-Name = sqlserver
object_type  = event
Object-Name  = sql_statement_completed
Object-Descr = Occurs when a Transact-SQL statement has completed.
Package-Guid = 655FD93F-3364-40D5-B2BA-330F7FFB6491
```


#### <a name="ssms-ui-for-search"></a>検索の SSMS UI


もう 1 つの検索オプションは、前述のスクリーンショットで示した **[新しいセッション]**  >  **[イベント]**  >  **[イベント ライブラリ]** ダイアログに SSMS UI を使用することです。



#### <a name="sql-trace-event-classes-with-extended-events"></a>SQL トレース イベント クラスと拡張イベント


SQL トレースのイベント クラスと列で拡張されたイベントの使用に関する説明は次の場所で確認できます。[SQL トレースのイベント クラスと等価な拡張イベントを確認する](../../relational-databases/extended-events/view-the-extended-events-equivalents-to-sql-trace-event-classes.md)



#### <a name="event-tracing-for-windows-etw-with-extended-events"></a>Windows イベント トレーシング (ETW) と拡張イベント


拡張イベントと Windows イベント トレーシング (ETW) の使用に関する説明は、以下をご覧ください。

- [Event Tracing for Windows ターゲット](../../relational-databases/extended-events/event-tracing-for-windows-target.md)
- [拡張イベントを使用したシステムの使用状況の監視](../../relational-databases/extended-events/monitor-system-activity-using-extended-events.md)



ETW イベントは、Azure SQL Database の拡張イベントではご利用いただけません。



## <a name="additional-items"></a>その他のアイテム


このセクションでは、その他のアイテムについて簡単に紹介します。


### <a name="event-sessions-installed-with-sql-server"></a>SQL Server でインストールされるイベント セッション


SQL Server には、作成済みの拡張イベントがいくつか付属します。 いずれも SQL システムを起動すると開始されるように設定されています。 これらのイベント セッションは、システム エラーが発生した場合に役立つデータを収集します。 すべての拡張イベントと同様に、これらのセッションはほんの少しのリソースしか消費しないため、実行したままにしておくことをお勧めします。

これらのイベント セッションは、 **[管理]** [拡張イベント] **[セッション]**  > **の下の SSMS** > **オブジェクト エクスプローラー**で確認できます。  2016年 6 月時点での、これらのインストール済みのイベント セッションの一覧は次のとおりです。

- AlwaysOn_health
- system_health
- telemetry_events



### <a name="powershell-provider-for-extended-events"></a>拡張イベントの PowerShell プロバイダー


SQL Server PowerShell を使用して、SQL Server 拡張イベントを管理することができます。 詳細については、以下を参照してください。[拡張イベントへの PowerShell プロバイダーの使用](../../relational-databases/extended-events/use-the-powershell-provider-for-extended-events.md)


### <a name="system-views-for-extended-events"></a>拡張イベントのシステム ビュー


拡張イベントのシステム ビューには次のものが含まれます。

- *カタログ ビュー:* CREATE EVENT SESSION によって定義されているイベント セッションに関する情報を表示します。

- *動的管理ビュー (DMV):* 現在アクティブに実行中のイベント セッションに関する情報を表示します。


[SQL Server の拡張イベントに対するシステム ビューからの SELECT と JOIN](../../relational-databases/extended-events/selects-and-joins-from-system-views-for-extended-events-in-sql-server.md) - 次に関する情報を提供します。


- ビューを互いに結合する方法


- いくつかの便利なビューからの SELECT


- 次の間の相関関係
    - ビュー列
    - CREATE EVENT SESSION 句
    - SSMS UI コントロール

## <a name="code-examples-can-differ-for-azure-sql-database"></a>Azure SQL Database では、コード例が異なる可能性があります。

[!INCLUDE[sql-on-premises-vs-azure-similar-sys-views-include.](../../includes/paragraph-content/sql-on-premises-vs-azure-similar-sys-views-include.md)]

## <a name="appendix1"></a>付録: アクセス許可の所有者を事前に確認するための SELECT

この記事で言及されているアクセス許可は次のとおりです。

- ALTER ANY EVENT SESSION
- VIEW SERVER STATE
- CONTROL SERVER

次の Transact-SQL SELECT ステートメントは、誰がこれらのアクセス許可を持っているかをレポートすることができます。


#### <a name="union-direct-permissions-plus-role-derived-permissions"></a>UNION はアクセス許可とロール派生のアクセス許可を送信する


次の SELECT...UNION ALL ステートメントは、イベント セッションの作成および拡張イベントのシステム カタログ ビューを照会するために必要な権限を持つユーザーを示す行を返します。


```sql
-- Ascertain who has the permissions listed in the ON clause.
-- 'CONTROL SERVER' permission includes the permissions
-- 'ALTER ANY EVENT SESSION' and 'VIEW SERVER STATE'.
SELECT
        'Owner-is-Principal'  AS [Type-That-Owns-Permission],
        NULL                  AS [Role-Name],
        prin.name             AS [Owner-Name],

        perm.permission_name
            COLLATE Latin1_General_CI_AS_KS_WS
            AS [Permission-Name]
    FROM
             sys.server_permissions  AS perm
        JOIN sys.server_principals   AS prin

            ON prin.principal_id = perm.grantee_principal_id
    WHERE
        perm.permission_name IN
            ('ALTER ANY EVENT SESSION',
            'VIEW SERVER STATE',
            'CONTROL SERVER')
UNION ALL

-- Plus check for members of the 'sysadmin' fixed server role,
-- because 'sysadmin' includes the 'CONTROL SERVER' permission.
SELECT
        'Owner-is-Role',
        prin.name,  -- [Role-Name]

        CAST( (IsNull(pri2.name, N'No members'))
            AS nvarchar(128)),

        NULL
    FROM
                         sys.server_role_members  AS rolm
        RIGHT OUTER JOIN sys.server_principals    AS prin

            ON prin.principal_id = rolm.role_principal_id

        LEFT OUTER JOIN sys.server_principals     AS pri2

            ON rolm.member_principal_id = pri2.principal_id
    WHERE
        prin.name = 'sysadmin'
    ORDER BY
        1,2,3,4;
```


#### <a name="has_perms_by_name-function"></a>HAS_PERMS_BY_NAME 関数


次の SELECT はユーザーのアクセス許可を報告します。 これは組み込み関数 [HAS_PERMS_BY_NAME](../../t-sql/functions/has-perms-by-name-transact-sql.md)に依存します。

さらに、一時的に他のアカウントを *偽装する* 権限がある場合は、 [EXECUTE AS LOGIN](../../t-sql/statements/execute-as-transact-sql.md) および REVERT ステートメントをコメント解除して、他のアカウントを照会することができます。


```sql
--EXECUTE AS LOGIN = 'AccountNameHere';
SELECT HAS_PERMS_BY_NAME(
    null, null,
    'ALTER ANY EVENT SESSION'
    );
--REVERT;
```


#### <a name="security-links"></a>セキュリティ関連のリンク

これらの SELECT およびアクセス許可に関するドキュメントのリンクを次に示します。

- 組み込み関数 [HAS_PERMS_BY_NAME (Transact-SQL)](../../t-sql/functions/has-perms-by-name-transact-sql.md)の詳細
- [sys.fn_my_permissions (Transact-SQL)](../../relational-databases/system-functions/sys-fn-my-permissions-transact-sql.md)
- [GRANT (サーバーの権限の許可) (Transact-SQL)](../../t-sql/statements/grant-server-permissions-transact-sql.md)
- [sys.server_principals (Transact-SQL)](https://msdn.microsoft.com/library/ms188786.aspx)
- 特に Azure SQL Database の場合、 [sys.database_principals (Transact-SQL)](https://msdn.microsoft.com/library/ms187328.aspx)
- ブログ: [Effective Database Engine Permissions](https://social.technet.microsoft.com/wiki/contents/articles/15180.effective-database-engine-permissions.aspx)(効果的なデータベース エンジンのアクセス許可)
- すべての SQL Server 権限の階層を表示した、ズーム可能な [ポスター](https://aka.ms/sql-permissions-poster)(PDF)



## <a name="links-to-supporting-information"></a>関連情報へのリンク


- [sys.fn_xe_file_target_read_file (Transact-SQL)](../../relational-databases/system-functions/sys-fn-xe-file-target-read-file-transact-sql.md)


