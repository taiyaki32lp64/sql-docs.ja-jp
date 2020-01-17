---
title: クエリ エディターを使用して拡張イベント セッションの作成 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- create extended events session
- extended events [SQL Server], create session
ms.assetid: cba0e02b-b201-4863-bf1b-9164e68e5fa8
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4a541c86029be9a438492a851c0eb16d18120f75
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66065028"
---
# <a name="create-an-extended-events-session-using-query-editor"></a>クエリ エディターを使用した拡張イベント セッションの作成
  拡張イベント セッションを作成するには、クエリ エディターを使用するか、オブジェクト エクスプローラーでセッションを作成します。 オブジェクト エクスプ ローラーでは、拡張イベントは、作成、変更、およびイベント セッション データのイベント セッションの作成プロセスをガイドするウィザードとより高度な構成オプションを提供する新しいセッション UI を表示する際、2 つのユーザー インターフェイスを提供します。 拡張イベント セッションを作成して SQL Server のトレースを診断できます。これにより次のような問題を解決できます。  
  
-   最も高価なクエリを見つける  
  
-   ラッチ競合の根本的な原因を見つける  
  
-   他のクエリをブロックしているクエリを見つける  
  
-   クエリの再コンパイルにより、過剰な CPU 使用率をトラブルシューティングする  
  
-   デッドロックのトラブルシューティング  
  
 新規セッション ウィザードを使用して拡張イベント セッションを作成する方法については、「[ウィザードを使用した拡張イベント セッションの作成 &#40;オブジェクト エクスプローラー&#41;](../ssms/object/object-explorer.md)」を参照してください。 [新しいセッション] UI を使用して拡張イベント セッションを作成する方法については、「[[新しいセッション] ダイアログを使用した拡張イベント セッションの作成](../../2014/database-engine/create-an-extended-events-session-using-the-new-session-dialog.md)」を参照してください。  
  
##  <a name="BeforeYouBegin"></a> Permissions  
 拡張イベント セッションを作成するには、ALTER ANY EVENT SESSION 権限が必要です。  
  
## <a name="creating-an-extended-events-session-using-query-editor"></a>クエリ エディターを使用した拡張イベント セッションの作成  
  
#### <a name="to-create-an-extended-events-session"></a>拡張イベント セッションを作成するには  
  
1.  次の手順は、 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]のクエリ エディターを使用して拡張イベント セッションを作成する方法を示しています。  
  
     セッションに使用するイベントを決めます。 利用可能なすべてのイベントをキーワードおよびチャネルと併せて表示するには、次のクエリを使用します。  
  
    > [!NOTE]  
    >  キーワードおよびチャネルの詳細については、「 [SQL Server 拡張イベント パッケージ](../relational-databases/extended-events/sql-server-extended-events-packages.md)」を参照してください。  
  
    ```  
    SELECT p.name, c.event, k.keyword, c.channel, c.description FROM  
       (  
       SELECT event_package = o.package_guid, o.description,   
       event=c.object_name, channel = v.map_value  
       FROM sys.dm_xe_objects o  
       LEFT JOIN sys.dm_xe_object_columns c ON o.name = c.object_name  
       INNER JOIN sys.dm_xe_map_values v ON c.type_name = v.name   
       AND c.column_value = cast(v.map_key AS nvarchar)  
       WHERE object_type = 'event' AND (c.name = 'CHANNEL' or c.name IS NULL)  
       ) c LEFT JOIN   
       (  
       SELECT event_package = c.object_package_guid, event = c.object_name,   
       keyword = v.map_value  
       FROM sys.dm_xe_object_columns c INNER JOIN sys.dm_xe_map_values v   
       ON c.type_name = v.name AND c.column_value = v.map_key   
       AND c.type_package_guid = v.object_package_guid  
       INNER JOIN sys.dm_xe_objects o ON o.name = c.object_name   
       AND o.package_guid = c.object_package_guid  
       WHERE object_type = 'event' AND c.name = 'KEYWORD'   
       ) k  
       ON  
       k.event_package = c.event_package AND (k.event=c.event or k.event IS NULL)  
       INNER JOIN sys.dm_xe_packages p ON p.guid = c.event_package  
    ORDER BY keyword desc, channel, event  
    ```  
  
2.  新しいクエリ ウィンドウで、イベント セッションを作成するためのステートメントを追加します。 *session_name* の部分は、使用するセッションの名前に置き換えてください。  
  
    > [!IMPORTANT]  
    >  手順 2. ～ 6. は、イベント セッションの定義を断片的に記述しています。 実際には、すべてのステートメントを単一のクエリ ウィンドウに追加してから実行することになります。 サンプル全体については、このトピックの「使用例」のセクションを参照してください。  
  
    ```  
    CREATE EVENT SESSION session_name   
    ON SERVER  
    ```  
  
3.  監視するイベントを *package_name*.*event_name*の形式で追加します。 各イベントについて、次のような行を追加します。  
  
    ```  
    ADD EVENT package_name.event_name  
    ```  
  
     例 :  
  
    ```  
    ADD EVENT sqlserver.file_read_completed,  
    ADD EVENT sqlserver.file_write_completed  
    ```  
  
4.  (省略可能) イベントを追加すると、実行するアクションを追加できます。 また、述語を追加することもできます。 述語は、イベント情報がどのようなときにターゲットによって消費されるかの基準を確立する目的で使用されます。 アクションは、ACTION 句を使用して追加します。述語は、WHERE 句を使用して追加します。 たとえば、sqlserver.file_read_completed イベントについて、ファイル ID が 1 と等しいときに [!INCLUDE[tsql](../includes/tsql-md.md)] テキストをキャプチャするようなアクションと述語を追加するには、次のステートメントを追加します。  
  
    ```  
    ADD EVENT sqlserver.file_read_completed  
       (ACTION (sqlserver.sql_text)  
       WHERE file_id = 1),  
    ```  
  
    -   利用可能なアクションを表示するには、次のクエリを使用します。  
  
        ```  
        SELECT p.name AS 'package_name', xo.name AS 'action_name', xo.description, xo.object_type  
        FROM sys.dm_xe_objects AS xo  
        JOIN sys.dm_xe_packages AS p  
           ON xo.package_guid = p.guid  
        WHERE xo.object_type = 'action'  
        AND (xo.capabilities & 1 = 0   
        OR xo.capabilities IS NULL)  
        ORDER BY p.name, xo.name  
        ```  
  
    -   イベントに対して利用可能な述語を表示するには、次のクエリを使用します。 *event_name* の部分は、述語の追加対象となるイベントの名前に置き換えてください。  
  
        ```  
        SELECT *  
        FROM sys.dm_xe_object_columns  
        WHERE object_name = 'event_name'  
        AND column_type = 'data'  
        ```  
  
         以下に例を示します。  
  
        ```  
        SELECT *   
        FROM sys.dm_xe_object_columns   
        WHERE object_name = 'file_read_completed'  
        AND column_type = 'data'  
        ```  
  
         グローバル述語ソースを追加することもできます。 グローバル述語ソースは、あらゆる述語式で使用できます。 利用可能なグローバル述語ソースを表示するには、次のクエリを使用します。  
  
        ```  
        SELECT p.name AS package_name, xo.name AS predicate_name  
           , xo.description, xo.object_type  
        FROM sys.dm_xe_objects AS xo  
        JOIN sys.dm_xe_packages AS p  
           ON xo.package_guid = p.guid  
        WHERE xo.object_type = 'pred_source'  
        ORDER BY p.name, xo.name  
        ```  
  
         たとえば、次の述語式を使用すると、最初の 5 回の発生に限定してイベント データを収集することができます。  
  
        ```  
        WHERE package0.counter <= 5  
        ```  
  
5.  適切なターゲットを追加します。イベント データはターゲットで処理され、消費されます。 次の形式を使用します。  
  
    ```  
    ADD TARGET package_name.target_name  
    ```  
  
     次の例では、非同期のファイル ターゲットを追加します。  
  
    ```  
    ADD TARGET package0.asynchronous_file_target  
       (SET filename = 'c:\temp\xelog.xel', metadatafile = 'c:\temp\xelog.xem')  
    ```  
  
     利用可能なターゲットを一覧表示するには、次のクエリを使用します。  
  
    ```  
    SELECT p.name AS 'package_name', xo.name AS 'target_name'  
       , xo.description, xo.object_type   
    FROM sys.dm_xe_objects AS xo  
    JOIN sys.dm_xe_packages AS p  
       ON xo.package_guid = p.guid  
    WHERE xo.object_type = 'target'  
    AND (xo.capabilities & 1 = 0  
    OR xo.capabilities IS NULL)  
    ORDER BY p.name, xo.name  
    ```  
  
    > [!NOTE]  
    >  ターゲットの種類については、「 [SQL Server 拡張イベント ターゲット](../../2014/database-engine/sql-server-extended-events-targets.md)」を参照してください。  
  
6.  他にも必要な構成オプションがあれば、確認して追加します。 たとえば、イベント保存モード、イベントをメモリにバッファリングする時間、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の起動時にイベント セッションを自動的に開始するかどうかなどのオプションを構成することができます。 これらのオプションについては、「[ALTER EVENT SESSION &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-event-session-transact-sql)」のトピックに説明があります。 これらのオプションを指定しなかった場合は、既定値が割り当てられる点に注意してください。  
  
7.  セッションを開始します。  
  
    > [!NOTE]  
    >  セッションの結果を表示する方法の詳細については、オンライン ブックの「 [SQL Server 拡張イベント ターゲット](../../2014/database-engine/sql-server-extended-events-targets.md) 」ノードで、使用しているターゲットの種類に応じたトピックを参照してください。  
  
 次の例では、IOActivity という名前の拡張イベント セッションを作成します。キャプチャする情報は次のとおりです。  
  
-   ファイル読み取り完了イベントのデータ (関連付けられている [!INCLUDE[tsql](../includes/tsql-md.md)] テキストを含む)。ファイル ID が 1 に等しいファイルの読み取りが対象となります。  
  
-   ファイル書き込み完了イベントのデータ。  
  
-   ログ キャッシュ内のデータが物理ログ ファイルに書き込まれたときに発生するイベントのデータ。  
  
 このセッションでは、出力結果がファイル ターゲットに送信されます。  
  
```  
CREATE EVENT SESSION IOActivity  
ON SERVER  
  
ADD EVENT sqlserver.file_read_completed  
   (  
   ACTION (sqlserver.sql_text)  
   WHERE file_id = 1),  
ADD EVENT sqlserver.file_write_completed,  
ADD EVENT sqlserver.databases_log_flush  
  
ADD TARGET package0.asynchronous_file_target   
   (SET filename = 'c:\temp\xelog.xel', metadatafile = 'c:\temp\xelog.xem')  
```  
  
## <a name="see-also"></a>参照  
 [CREATE EVENT SESSION &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-event-session-transact-sql)   
 [SQL Server 拡張イベント ターゲット](../../2014/database-engine/sql-server-extended-events-targets.md)   
 [SQL Server 拡張イベント パッケージ](../relational-databases/extended-events/sql-server-extended-events-packages.md)  
  
  
