---
title: sp_trace_setevent (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_trace_setevent_TSQL
- sp_trace_setevent
dev_langs:
- TSQL
helpviewer_keywords:
- sp_trace_setevent
ms.assetid: 7662d1d9-6d0f-443a-b011-c901a8b77a44
author: stevestein
ms.author: sstein
ms.openlocfilehash: f622f7d7097afd66a87b8ad90280e19ac3ea40de
ms.sourcegitcommit: 43c3d8939f6f7b0ddc493d8e7a643eb7db634535
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2019
ms.locfileid: "72305303"
---
# <a name="sp_trace_setevent-transact-sql"></a>sp_trace_setevent (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  トレースに対して、イベントまたはイベント列を追加または削除します。 **sp_trace_setevent**は、停止している既存のトレースに対してのみ実行できます (*状態*は**0**)。 このストアドプロシージャが存在しないトレースまたは*状態*が**0**以外のトレースで実行されると、エラーが返されます。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 代わりに拡張イベントを使用します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_trace_setevent [ @traceid = ] trace_id   
          , [ @eventid = ] event_id  
          , [ @columnid = ] column_id  
          , [ @on = ] on  
```  
  
## <a name="arguments"></a>引数  
`[ @traceid = ] trace_id` は、変更するトレースの ID です。 *trace_id*は**int**,、既定値はありません。 ユーザーは、この*trace_id*値を採用して、トレースの識別、変更、および制御を行います。  
  
`[ @eventid = ] event_id` は、有効にするイベントの ID です。 *event_id*は**int**,、既定値はありません。  
  
 次の表は、トレースに対して追加または削除できるイベントの一覧です。  
  
|イベント番号|イベント名|[説明]|  
|------------------|----------------|-----------------|  
|0-9|予約済み。|予約済み。|  
|10|RPC:Completed|リモートプロシージャコール (RPC) が完了したときに発生します。|  
|11|RPC:Starting|RPC が開始したときに発生します。|  
|12|SQL:BatchCompleted|[!INCLUDE[tsql](../../includes/tsql-md.md)] バッチが完了したときに発生します。|  
|13|SQL:BatchStarting|[!INCLUDE[tsql](../../includes/tsql-md.md)] バッチが開始したときに発生します。|  
|14|Audit Login|ユーザーが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に正常にログオンしたときに発生します。|  
|15|Audit Logout|ユーザーが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] からログアウトしたときに発生します。|  
|16|Attention|クライアントの割り込み要求やクライアント接続の切断などのアテンションイベントが発生したときに発生します。|  
|17|ExistingConnection|トレースの開始前から [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続しているユーザーのすべての利用状況を検出します。|  
|18|Audit Server Starts and Stops|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスの状態が変更されたときに発生します。|  
|19|DTCTransaction|複数のデータベース間で、[!INCLUDE[msCoName](../../includes/msconame-md.md)] 分散トランザクション コーディネーター (MS DTC) によってコーディネートされたトランザクションを追跡します。|  
|20|ログインの監査に失敗しました|クライアントから [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] へのログイン試行が失敗したことを示します。|  
|21|EventLog|イベントが Windows アプリケーション ログに記録されたことを示します。|  
|22|ErrorLog|エラー イベントが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラー ログに記録されたことを示します。|  
|23|Lock:Released|ページなどのリソースのロックが解除されたことを示します。|  
|24|Lock:Acquired|データ ページなどのリソースのロックが取得されたことを示します。|  
|25|Lock:Deadlock|は、他のトランザクションが所有するリソースに対して互換性のないロックを取得しようとすることで、2つの同時実行トランザクションが相互にデッドロックすることを示します。|  
|26|Lock:Cancel|リソースのロックの取得がキャンセルされたことを示します (たとえば、デッドロックが原因で)。|  
|27|Lock:Timeout|ページなどのリソースのロックが要求されたが、他のトランザクションによってそのリソースのブロッキング ロックが保持されているため、要求がタイムアウトになったことを示します。 タイムアウトは @@LOCK_TIMEOUT 関数によって決定され、SET LOCK_TIMEOUT ステートメントを使用して設定できます。|  
|28|Degree of Parallelism Event (7.0 Insert)|SELECT、INSERT、または UPDATE ステートメントが実行される前に発生します。|  
|29-31|予約済み。|代わりにイベント 28 を使用してください。|  
|32|予約済み。|予約済み。|  
|33|例外|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]で例外が発生したことを示します。|  
|34|SP:CacheMiss|ストアドプロシージャがプロシージャキャッシュ内に見つからないことを示します。|  
|35|SP: CacheInsert|項目がプロシージャキャッシュに挿入された時点を示します。|  
|36|SP: CacheRemove|プロシージャ キャッシュからアイテムが削除されたことを示します。|  
|37|SP: Recompile|ストアド プロシージャが再コンパイルされたことを示します。|  
|38|SP:CacheHit|ストアド プロシージャがプロシージャ キャッシュ内にあることを示します。|  
|39|非推奨|非推奨|  
|40|SQL:StmtStarting|[!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントが開始されたときに発生します。|  
|41|SQL:StmtCompleted|[!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントが完了したときに発生します。|  
|42|SP:Starting|ストアドプロシージャが開始された時点を示します。|  
|43|SP:Completed|ストアド プロシージャが完了したことを示します。|  
|44|SP:StmtStarting|ストアドプロシージャ内の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントの実行が開始されたことを示します。|  
|45|SP:StmtCompleted|ストアド プロシージャ内の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントの実行が完了したことを示します。|  
|46|オブジェクト: Created|CREATE INDEX、CREATE TABLE、CREATE DATABASE などのステートメントで、オブジェクトが作成されたことを示します。|  
|47|Object:Deleted|DROP INDEX や DROP TABLE などのステートメントで、オブジェクトが削除されたことを示します。|  
|48|予約済み。||  
|49|予約済み。||  
|50|SQL トランザクション|BEGIN、COMMIT、SAVE、および ROLLBACK TRANSACTION ステートメント [!INCLUDE[tsql](../../includes/tsql-md.md)] を追跡します。|  
|51|スキャン: 開始|テーブル スキャンまたはインデックス スキャンが開始されたことを示します。|  
|52|スキャン: 停止|テーブル スキャンまたはインデックス スキャンが停止したことを示します。|  
|53|CursorOpen|[!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントで、ODBC、OLE DB、または DB-Library によりカーソルがオープンされたことを示します。|  
|54|TransactionLog|トランザクションがいつトランザクション ログに書き込まれるかを追跡します。|  
|55|ハッシュの警告|バッファー パーティション上で処理されていないハッシュ演算 (ハッシュ結合、ハッシュ集計、ハッシュ ユニオン、ハッシュ識別など) が代替プランに変更されたことを示します。 これは、再帰の深さ、データスキュー、トレースフラグ、またはビットカウントが原因で発生する可能性があります。|  
|56-57|予約済み。||  
|58|Auto Stats|インデックス統計の自動更新が実行されたことを示します。|  
|59|Lock:Deadlock Chain|デッドロックにつながる各イベントに対して生成されます。|  
|60|Lock:Escalation|ページ ロックが TABLE ロックまたは HoBT ロックにエスカレートまたは変換された場合など、細かい単位のロックが大きな単位のロックに変換されたことを示します。|  
|61|OLE DB Errors|OLE DB エラーが発生したことを示します。|  
|62-66|予約済み。||  
|67|Execution Warnings|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ステートメントまたはストアド プロシージャの実行中に発生した警告を示します。|  
|68|Showplan Text (Unencoded)|実行された [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントのプラン ツリーを表示します。|  
|69|Sort Warnings|メモリに合わない並べ替え操作を示します。 インデックスの作成に関連する並べ替え操作は対象になりません。SELECT ステートメントで使用される ORDER BY 句など、クエリ内の並べ替え操作のみが対象になります。|  
|70|CursorPrepare|[!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントのカーソルが、ODBC、OLE DB、または DB-LIBRARY で使用できるように準備された時点を示します。|  
|71|Prepare SQL|ODBC、OLE DB、または DB-LIBRARY では、使用する [!INCLUDE[tsql](../../includes/tsql-md.md)] のステートメントが準備されています。|  
|72|Exec Prepared SQL|ODBC、OLE DB、または DB-Library によって、準備された 1 つ以上の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントが実行されたことを示します。|  
|73|Unprepare SQL|ODBC、OLE DB、または DB-LIBRARY が、準備された [!INCLUDE[tsql](../../includes/tsql-md.md)] のステートメントを準備解除 (削除) しました。|  
|74|CursorExecute|[!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントで ODBC、OLE DB、または DB-Library によって準備されたカーソルが実行されたことを示します。|  
|75|CursorRecompile|[!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントで ODBC または DB-Library によってオープンされていたカーソルが、直接再コンパイルされたか、またはスキーマが変更されたために再コンパイルされたことを示します。<br /><br /> ANSI および ANSI 以外のカーソルに対してトリガーされます。|  
|76|CursorImplicitConversion|[!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントのカーソルは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって1つの型から別の型に変換されます。<br /><br /> ANSI および ANSI 以外のカーソルに対してトリガーされます。|  
|77|CursorUnprepare|[!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントで準備されたカーソルが、ODBC、OLE DB、または DB-Library によって削除されたことを示します。|  
|78|CursorClose|ODBC、OLE DB、または DB-LIBRARY によって [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントで以前に開かれたカーソルは閉じられています。|  
|79|列の統計情報がありません|オプティマイザーに有効な列の統計が利用できません。|  
|80|Missing Join Predicate|結合述語がないクエリが実行されています。 クエリの終了に時間がかかる可能性があります。|  
|81|Server Memory Change|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] メモリ使用量の増加または減少は、1メガバイト (MB) または最大サーバーメモリの5% のどちらか大きい方になります。|  
|82-91|ユーザーが構成可能 (0-9)|ユーザーが定義したイベントデータ。|  
|92|データファイルの自動拡張|データファイルがサーバーによって自動的に拡張されたことを示します。|  
|93|Log File Auto Grow|ログ ファイルがサーバーによって自動的に拡張されたことを示します。|  
|94|Data File Auto Shrink|データ ファイルがサーバーによって自動的に圧縮されたことを示します。|  
|95|ログファイルの自動圧縮|ログファイルがサーバーによって自動的に圧縮されたことを示します。|  
|96|Showplan Text|クエリ オプティマイザーの SQL ステートメントのクエリ プラン ツリーを表示します。 **TextData**列には、このイベントの Showplan が含まれていないことに注意してください。|  
|97|Showplan All|実行された SQL ステートメントのコンパイル時の完全な詳細を含むクエリプランを表示します。 **TextData**列には、このイベントの Showplan が含まれていないことに注意してください。|  
|98|Showplan Statistics Profile|実行された SQL ステートメントの実行時の完全な詳細を含むクエリプランを表示します。 **TextData**列には、このイベントの Showplan が含まれていないことに注意してください。|  
|99|予約済み。||  
|100|RPC Output Parameter|各 RPC に対して、パラメーターの出力値を生成します。|  
|101|予約済み。||  
|102|監査データベーススコープ GDR|データベースに対する権限の許可などのデータベース限定の操作時に、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の任意のユーザーがステートメント権限の GRANT、DENY、REVOKE を実行するたびに発生します。|  
|103|Audit Object GDR イベント|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の任意のユーザーがオブジェクト権限の GRANT、DENY、REVOKE を実行するたびに発生します。|  
|104|Audit AddLogin イベント|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインが追加または削除されたときに発生します。**sp_addlogin**と**sp_droplogin**の場合。|  
|105|Audit Login GDR Event|Windows ログイン権限が追加または削除されたときに発生します。**sp_grantlogin**、 **sp_revokelogin**、 **sp_denylogin**。|  
|106|Audit Login Change Property Event|パスワード以外のログインのプロパティが変更された場合に発生します。**sp_defaultdb**と**sp_defaultlanguage**の場合。|  
|107|Audit Login Change Password イベント|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインパスワードが変更されたときに発生します。<br /><br /> パスワードは記録されません。|  
|108|Audit Add Login to Server Role イベント|固定サーバーロールに対してログインが追加または削除されたときに発生します。**sp_addsrvrolemember**の場合は、 **sp_dropsrvrolemember**の場合はです。|  
|109|Audit Add DB User Event|データベースユーザー (Windows または [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]) としてログインが追加または削除されたときに発生します。**sp_grantdbaccess**、 **sp_revokedbaccess**、 **sp_adduser**、および**sp_dropuser**。|  
|110|Audit Add Member to DB ロールイベント|データベースに対してデータベースユーザー (固定またはユーザー定義) としてログインが追加または削除されたときに発生します。**sp_addrolemember**、 **sp_droprolemember**、 **sp_changegroup**。|  
|111|Audit Add Role イベント|データベースにデータベースユーザーとしてログインが追加または削除されたときに発生します。**sp_addrole**と**sp_droprole**の場合。|  
|112|Audit App Role Change Password Event|アプリケーションロールのパスワードが変更されたときに発生します。|  
|113|Audit Statement Permission Event|CREATE TABLE などのステートメント権限が使用されたときに発生します。|  
|114|Audit Schema Object Access Event|SELECT などのオブジェクト権限が使用されたときに、それが成功したかどうかに関係なく発生します。|  
|115|バックアップ/復元イベントの監査|BACKUP または RESTORE コマンドが実行されたときに発生します。|  
|116|Audit DBCC Event|DBCC コマンドが発行されたときに発生します。|  
|117|Audit Change Audit Event|監査トレースが変更されたときに発生します。|  
|118|Audit Object Derived Permission Event|CREATE、ALTER、および DROP オブジェクトコマンドが発行されたときに発生します。|  
|119|OLEDB 呼び出しイベント|分散クエリとリモート ストアド プロシージャに対して、OLE DB プロバイダー呼び出しが行われたときに発生します。|  
|120|OLEDB QueryInterface Event|分散クエリとリモートストアドプロシージャに対して OLE DB **QueryInterface**呼び出しが行われたときに発生します。|  
|121|OLEDB DataRead Event|OLE DB プロバイダーに対して、データ要求の呼び出しが行われたときに発生します。|  
|122|Showplan XML|SQL ステートメントの実行時に発生します。 プラン表示操作を識別するには、このイベントを含めます。 各イベントは、整形式の XML ドキュメントに格納されます。 このイベントの**バイナリ**列には、エンコードされたプラン表示が含まれていることに注意してください。 トレースを開いて Showplan を表示するには、SQL Server プロファイラーを使用します。|  
|123|SQL: FullTextQuery|フルテキスト クエリが実行されたときに発生します。|  
|124|Broker:Conversation|[!INCLUDE[ssSB](../../includes/sssb-md.md)] メッセージ交換の進行状況を報告します。|  
|125|廃止に関するお知らせ|将来のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]から削除される機能を使用すると発生します。|  
|126|Deprecation Final Support|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の次の主要なリリースで削除される予定の機能を使用したときに発生します。|  
|127|交換書き込みイベント|並列クエリプランの通信バッファーが**tempdb**データベースに一時的に書き込まれたときに発生します。|  
|128|Audit Database Management イベント|データベースが作成、変更、または削除されたときに発生します。|  
|129|Audit Database Object Management イベント|CREATE、ALTER、または DROP ステートメントがスキーマなどのデータベースオブジェクトで実行されるときに発生します。|  
|130|Audit Database Principal Management Event|ユーザーなどのプリンシパルがデータベースで作成、変更、または削除されるときに発生します。|  
|131|監査スキーマオブジェクト管理イベント|サーバーオブジェクトが作成、変更、または削除されるときに発生します。|  
|132|Audit Server Principal Impersonation Event|サーバー スコープ内で、EXECUTE AS LOGIN などの権限借用があるときに発生します。|  
|133|Audit Database Principal Impersonation Event|EXECUTE AS USER や SETUSER など、データベーススコープ内で権限の借用が発生したときに発生します。|  
|134|監査サーバーオブジェクトの所有権の取得イベント|サーバースコープ内のオブジェクトの所有者が変更されたときに発生します。|  
|135|Audit Database オブジェクトの所有権の取得イベント|データベーススコープ内のオブジェクトの所有者が変更したときに発生します。|  
|136|Broker:Conversation Group|[!INCLUDE[ssSB](../../includes/sssb-md.md)] によって、新しいメッセージ交換グループが作成されたか、既存のメッセージ交換グループが削除されたときに発生します。|  
|137|Blocked Process Report|指定された時間を超えてプロセスがブロックされた場合に発生します。 システム プロセスや、デッドロックを検出できないリソースで待機しているプロセスはこの対象外です。 **Sp_configure**を使用して、レポートが生成されるしきい値と頻度を構成します。|  
|138|Broker:Connection|[!INCLUDE[ssSB](../../includes/sssb-md.md)] によって管理される転送接続の状態をレポートします。|  
|139|Broker: 転送されたメッセージを転送しました|[!INCLUDE[ssSB](../../includes/sssb-md.md)] によってメッセージが転送されたときに発生します。|  
|140|Broker:Forwarded Message Dropped|[!INCLUDE[ssSB](../../includes/sssb-md.md)] によって転送予定のメッセージが削除されたときに発生します。|  
|141|Broker:Message Classify|[!INCLUDE[ssSB](../../includes/sssb-md.md)] でメッセージのルーティングが決定されたときに発生します。|  
|142|Broker:Transmission|[!INCLUDE[ssSB](../../includes/sssb-md.md)] トランスポート層でエラーが発生したことを示します。 エラー番号と状態の値で、エラーの原因を確認できます。|  
|143|Broker: キューが無効です|[!INCLUDE[ssSB](../../includes/sssb-md.md)] キューに連続して5つのトランザクションロールバックがあったため、有害メッセージが検出されたことを示します。 イベントには、有害メッセージを含むキューのデータベース ID とキュー ID が含まれます。|  
|144-145|予約済み。||  
|146|Showplan XML Statistics Profile|SQL ステートメントの実行時に発生します。 Showplan 操作を識別し、コンパイル時の完全なデータを表示します。 このイベントの**バイナリ**列には、エンコードされたプラン表示が含まれていることに注意してください。 トレースを開いて Showplan を表示するには、SQL Server プロファイラーを使用します。|  
|148|Deadlock Graph|試行がデッドロックの一部であり、デッドロックの対象として選択されたために、ロックを取得しようとしたときに発生します。 デッドロックについての XML の説明が提供されます。|  
|149|Broker: リモートメッセージの受信確認|[!INCLUDE[ssSB](../../includes/sssb-md.md)] によってメッセージの受信確認が送信または受信されたときに発生します。|  
|150|トレースファイルの終了|トレースファイルのロールオーバー中にトレースファイルが閉じたときに発生します。|  
|151|予約済み。||  
|152|Audit Change Database Owner|ALTER AUTHORIZATION を使用してデータベースの所有者を変更し、権限をチェックするときに発生します。|  
|153|監査スキーマオブジェクトの所有権の取得イベント|ALTER AUTHORIZATION を使用してオブジェクトに所有者を割り当て、アクセス許可がチェックされるときに発生します。|  
|154|予約済み。||  
|155|FT: クロールを開始しました|フルテキストのクロール (カタログ作成) が開始したときに発生します。 クロール要求がワーカータスクによって選択されているかどうかを確認するには、を使用します。|  
|156|FT:Crawl Stopped|フルテキストのクロール (カタログ作成) が停止したときに発生します。 クロールが正常に完了するか、致命的なエラーが発生すると、停止します。|  
|157|FT:Crawl Aborted|フルテキストクロール中に例外が発生した場合に発生します。 通常、これによってフルテキストのクロールは停止します。|  
|158|Audit Broker Conversation|[!INCLUDE[ssSB](../../includes/sssb-md.md)] ダイアログセキュリティに関連する監査メッセージを報告します。|  
|159|Audit Broker Login|[!INCLUDE[ssSB](../../includes/sssb-md.md)] トランスポートセキュリティに関連する監査メッセージを報告します。|  
|160|Broker: メッセージを配信できませんでした|サービスに配信される必要がある受信メッセージを [!INCLUDE[ssSB](../../includes/sssb-md.md)] が保持できない場合に発生します。|  
|161|Broker:Corrupted Message|[!INCLUDE[ssSB](../../includes/sssb-md.md)] が破損したメッセージを受信したときに発生します。|  
|162|User Error Message|エラーや例外が発生したときにユーザーに表示されるエラー メッセージを表示します。|  
|163|Broker: アクティブ化|キュー モニターによって、アクティブ化ストアド プロシージャの開始や QUEUE_ACTIVATION 通知の送信が行われたときに発生します。またはキュー モニターが終了してアクティブ化ストアド プロシージャが開始したときに発生します。|  
|164|Object:Altered|データベースオブジェクトが変更されたときに発生します。|  
|165|Performance statistics|コンパイル済みのクエリプランが初めてキャッシュされたとき、再コンパイルされたとき、またはプランキャッシュから削除されたときに発生します。|  
|166|SQL:StmtRecompile|ステートメントレベルの再コンパイルが発生したときに発生します。|  
|167|データベースミラーリングの状態の変更|ミラー化データベースの状態が変更されたときに発生します。|  
|168|Showplan XML For Query Compile|SQL ステートメントのコンパイル時に発生します。 コンパイル時の完全なデータが表示されます。 このイベントの**バイナリ**列には、エンコードされたプラン表示が含まれていることに注意してください。 トレースを開いて Showplan を表示するには、SQL Server プロファイラーを使用します。|  
|169|Showplan All For Query Compile|SQL ステートメントのコンパイル時に発生します。 コンパイル時の完全なデータを表示します。 プラン表示演算子を識別するために使用します。|  
|170|Audit Server Scope GDR イベント|ログインの作成など、サーバースコープの権限に対して grant、deny、または revoke イベントが発生したことを示します。|  
|171|Audit Server Object GDR イベント|テーブルや関数などのスキーマオブジェクトに対して grant、deny、または revoke イベントが発生したことを示します。|  
|172|Audit Database Object GDR Event|アセンブリやスキーマなどのデータベース オブジェクトに対して、付与、拒否、または取り消しのイベントが発生したことを示します。|  
|173|サーバー操作の監査イベント|設定、リソース、外部アクセス、または承認の変更などのセキュリティ監査操作が使用されるときに発生します。|  
|175|Audit Server Alter Trace イベント|ステートメントが ALTER TRACE 権限をチェックするときに発生します。|  
|176|Audit Server Object Management イベント|サーバーオブジェクトが作成、変更、または削除されるときに発生します。|  
|177|監査サーバープリンシパル管理イベント|サーバー プリンシパルが作成、変更、または削除されたときに発生します。|  
|178|データベースの監査操作イベント|チェックポイントやクエリ通知のサブスクライブなど、データベース操作が行われたときに発生します。|  
|180|Audit Database Object Access Event|スキーマなどのデータベースオブジェクトがアクセスされたときに発生します。|  
|181|TM: Begin Tran starting|BEGIN TRANSACTION 要求が開始されたときに発生します。|  
|182|TM: Begin Tran completed|BEGIN TRANSACTION 要求が完了したときに発生します。|  
|183|TM: トランザクションの昇格を開始します|トランザクションの昇格要求が開始されたときに発生します。|  
|184|TM: トランザクションの昇格が完了しました|PROMOTE TRANSACTION 要求が完了したときに発生します。|  
|185|TM: Commit Tran starting|COMMIT TRANSACTION 要求が開始されたときに発生します。|  
|186|TM: Commit Tran completed|COMMIT TRANSACTION 要求が完了したときに発生します。|  
|187|TM: Rollback Tran starting|ROLLBACK TRANSACTION 要求が開始されたときに発生します。|  
|188|TM: Rollback Tran completed|ROLLBACK TRANSACTION 要求が完了したときに発生します。|  
|189|Lock: Timeout (タイムアウト > 0)|ページなどのリソースのロック要求がタイムアウトしたときに発生します。|  
|190|進行状況レポート: オンラインインデックス操作|ビルドプロセスの実行中に、オンラインのインデックス構築操作の進行状況を報告します。|  
|191|TM: Save Tran starting|SAVE TRANSACTION 要求が開始されたときに発生します。|  
|192|TM: Save Tran completed|SAVE TRANSACTION 要求が完了したときに発生します。|  
|193|バックグラウンドジョブエラー|バックグラウンド ジョブが異常終了したときに発生します。|  
|194|OLEDB Provider Information|分散クエリが実行され、プロバイダー接続に対応する情報が収集されるときに発生します。|  
|195|Mount Tape|テープ マウント要求を受け取ったときに発生します。|  
|196|Assembly Load|CLR アセンブリの読み込み要求が発生したときに発生します。|  
|197|予約済み。||  
|198|XQuery Static Type|XQuery 式が実行されるときに発生します。 このイベント クラスでは静的な XQuery 式が提供されます。|  
|199|全: サブスクリプション|クエリの登録をサブスクライブできない場合に発生します。 **TextData**列には、イベントに関する情報が含まれています。|  
|200|: パラメーターテーブル|アクティブなサブスクリプションに関する情報は、内部パラメーター テーブルに格納されます。 このイベント クラスは、パラメーター テーブルが作成または削除されたときに発生します。 通常これらのテーブルは、データベースを再起動したときに作成または削除されます。 **TextData**列には、イベントに関する情報が含まれています。|  
|201|QN: template|クエリ テンプレートによって、サブスクリプション クエリのクラスが表されます。 通常、同じクラスにあるクエリは、パラメーター値を除いてすべて同じになります。 このイベント クラスは、新しいサブスクリプション要求が、既存のクラス (一致したクラス)、新しいクラス (作成)、または削除するクラスに分類されたときに発生します。これは、アクティブなサブスクリプションが含まれていないクエリ クラスのテンプレートをクリーンアップすることを示します。 **TextData**列には、イベントに関する情報が含まれています。|  
|202|全: dynamics|クエリ通知の内部アクティビティを追跡します。 **TextData**列には、イベントに関する情報が含まれています。|  
|212|ビットマップの警告|クエリでビットマップフィルターが無効になっていることを示します。|  
|213|Database Suspect Data Page|**Msdb**の**suspect_pages**テーブルにページがいつ追加されるかを示します。|  
|214|CPU Threshold Exceeded|クエリが CPU のしきい値 (REQUEST_MAX_CPU_TIME_SEC) を超えたことを Resource Governor が検出したことを示します。|  
|215|PreConnect:Starting|LOGON トリガーまたは Resource Governor 分類子関数の実行が開始されたことを示します。|  
|216|PreConnect: 完了|LOGON トリガーまたは Resource Governor 分類子関数の実行が完了したことを示します。|  
|217|Plan Guide Successful|SQL Server でプラン ガイドを含むクエリまたはバッチの実行プランが正常に生成されたことを示します。|  
|218|Plan Guide Unsuccessful|SQL Server でプラン ガイドを含むクエリまたはバッチの実行プランを生成できなかったことを示します。 プランガイドを適用せずにこのクエリまたはバッチの実行プランを生成しようとしました SQL Server。 無効なプランガイドがこの問題の原因である可能性があります。 プランガイドを検証するには、fn_validate_plan_guide システム関数を使用します。|  
|235|Audit Fulltext||  
  
`[ @columnid = ] column_id` には、イベントに追加する列の ID を指定します。 *column_id*は**int**,、既定値はありません。  
  
 次の表に、イベントに追加できる列を示します。  
  
|列番号|列名|[説明]|  
|-------------------|-----------------|-----------------|  
|@shouldalert|**TextData**|トレースでキャプチャされるイベントクラスに依存するテキスト値。|  
|2|**BinaryData**|トレースでキャプチャされたイベント クラスに依存するバイナリ値。|  
|3|**DatabaseID**|USE *database*ステートメントで指定されたデータベースの ID、または特定の接続に対して use *database*ステートメントが実行されていない場合は既定のデータベースの ID となります。<br /><br /> データベースの値は、DB_ID 関数を使用して決定できます。|  
|4|**TransactionID**|システムによって割り当てられたトランザクション ID。|  
|5|**LineNumber**|エラーを含む行の番号が格納されます。 [!INCLUDE[tsql](../../includes/tsql-md.md)] SP:StmtStarting **のような**ステートメントを含むイベントの場合、 **LineNumber** にはストアド プロシージャまたはバッチでのステートメントの行番号が格納されます。|  
|6|**NTUserName**|[!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows のユーザー名。|  
|7|**NTDomainName**|ユーザーが所属する Windows ドメイン。|  
|8|**HostName**|要求を生成したクライアント コンピューターの名前。|  
|9|**ClientProcessID**|クライアントアプリケーションが実行されているプロセスにクライアントコンピューターによって割り当てられた ID。|  
|10|**ApplicationName**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスへの接続を作成したクライアント アプリケーションの名前。 この列には、プログラムの表示名ではなく、アプリケーションによって渡された値が格納されます。|  
|11|**LoginName**|クライアントのログイン名を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] します。|  
|12|**SPID**|クライアントに関連付けられているプロセスに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって割り当てられたサーバープロセス ID。|  
|13|**Duration**|イベントにかかった経過時間 (マイクロ秒)。 このデータ列は、Hash Warning イベントによって設定されません。|  
|14|**StartTime**|イベントの開始時刻 (取得できた場合)。|  
|15|**EndTime**|イベントの終了時刻。 **SQL:BatchStarting** や **SP:Starting**などの開始イベント クラスについては、この列に値が格納されません。 また、 **Hash Warning**イベントによって設定されることもありません。|  
|16|**Reads**|イベントの代わりにサーバーによって実行される、論理ディスク読み取り回数。 この列は、 **Lock: Released**イベントによって設定されません。|  
|17|**Writes**|イベントの代わりにサーバーによって実行される、物理ディスクの書き込み回数。|  
|18|**CPU**|イベントに使用された CPU 時間 (ミリ秒単位)。|  
|19|**Permissions**|アクセス許可のビットマップを表します。セキュリティ監査によって使用されます。|  
|20|**Severity**|例外の重大度レベル。|  
|21|**EventSubClass**|イベント サブクラスの種類。 すべてのイベント クラスに対して、このデータ列が作成されるわけではありません。|  
|22|**Exchange Spill**|システムによって割り当てられたオブジェクト ID。|  
|23|**成功**|アクセス許可の使用が成功しました。監査に使用されます。<br /><br /> **1** = 成功**0** = 失敗|  
|24|**IndexID**|イベントの影響を受けるオブジェクトに付けられたインデックス用の ID。 オブジェクトのインデックス ID を調べるには、 **indid** システム テーブルの **sysindexes** 列を使用します。|  
|25|**IntegerData**|トレースでキャプチャされたイベント クラスに依存する整数値。|  
|26|**ServerName**|トレースされている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスの名前 ( *servername*または*servername\instancename*)。|  
|27|**EventClass**|記録されるイベント クラスの種類。|  
|28|**ObjectType**|テーブル、関数、ストアドプロシージャなどのオブジェクトの型。|  
|29|**NestLevel**|このストアドプロシージャが実行されている入れ子レベルです。 参照してください[@@NESTLEVEL&#40;Transact-SQL&#41;](../../t-sql/functions/nestlevel-transact-sql.md).|  
|30|**状態**|サーバーの状態 (エラーが発生した場合)。|  
|31|**[エラー]**|エラー番号。|  
|32|**モード**|取得したロックのロックモード。 この列は、 **Lock: Released**イベントによって設定されません。|  
|33|**Handle**|イベントで参照されているオブジェクトのハンドル。|  
|34|**ObjectName**|アクセスされるオブジェクトの名前。|  
|35|**DatabaseName**|USE *database*ステートメントで指定されたデータベースの名前。|  
|36|**FileName**|変更されたファイル名の論理名。|  
|37|**OwnerName**|参照先オブジェクトの所有者名。|  
|38|**RoleName**|ステートメントの対象となっているデータベースまたはサーバー全体のロールの名前。|  
|39|**TargetUserName**|アクションの対象のユーザー名。|  
|40|**DBUserName**|クライアントの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベース ユーザー名。|  
|41|**LoginSid**|ログインしたユーザーのセキュリティ識別子 (SID)。|  
|42|**TargetLoginName**|アクションの対象となるログイン名。|  
|43|**TargetLoginSid**|アクションの対象となるログインの SID。|  
|44|**ColumnPermissions**|列レベルの権限の状態です。セキュリティ監査によって使用されます。|  
|45|**LinkedServerName**|リンク サーバーの名前|  
|46|**ProviderName**|OLE DB プロバイダーの名前です。|  
|47|**MethodName**|OLE DB メソッドの名前。|  
|48|**RowCounts**|バッチに含まれる行数。|  
|49|**RequestID**|ステートメントが含まれている要求の ID。|  
|50|**XactSequence**|現在のトランザクションを記述するトークン。|  
|51|**EventSequence**|このイベントのシーケンス番号。|  
|52|**BigintData1**|**bigint**値。トレースでキャプチャされたイベントクラスに依存します。|  
|53|**BigintData2**|**bigint**値。トレースでキャプチャされたイベントクラスに依存します。|  
|54|**GUID**|トレースでキャプチャされたイベント クラスに依存する GUID 値。|  
|55|**IntegerData2**|トレースでキャプチャされたイベントクラスに依存する整数値。|  
|56|**ObjectID2**|関連するオブジェクトまたはエンティティの ID (使用可能な場合)。|  
|57|**種類**|トレースでキャプチャされたイベントクラスに依存する整数値。|  
|58|**OwnerID**|ロックを所有するオブジェクトの種類。 ロック イベントの場合にのみ該当します。|  
|59|**ParentName**|オブジェクトが存在するスキーマの名前。|  
|60|**IsSystem**|イベントがシステム プロセスとユーザー プロセスのどちらで発生したか。<br /><br /> **1** = システム<br /><br /> **0** = ユーザー。|  
|61|**Offset**|ストアド プロシージャ内またはバッチ内のステートメントの開始オフセット。|  
|62|**SourceDatabaseID**|オブジェクトのソースが存在するデータベースの ID。|  
|63|**SqlHandle**|64 ビット ハッシュ。アドホック クエリやデータベースのテキスト、および SQL オブジェクトのオブジェクト ID に基づいています。 この値を **sys.dm_exec_sql_text()** に渡して、関連付けられている SQL テキストを取得できます。|  
|64|**SessionLoginName**|セッションを開始したユーザーのログイン名。 たとえば、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に **Login1** を使用して接続し、 **Login2**としてステートメントを実行した場合、 **SessionLoginName** には **Login1**が表示され、 **LoginName** には **Login2**が表示されます。 このデータ列には、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインと Windows ログインの両方が表示されます。|  
  
 **[ @on=]** *on*  
 このイベントを ON (1) にするか OFF (0) にするかを指定します。 *で* は **ビット**, 、既定値はありません。  
  
 *On*が**1**に設定されていて*column_id*が NULL の場合、イベントは on に設定され、すべての列がクリアされます。 *Column_id*が null でない場合は、そのイベントに対して列が ON に設定されます。  
  
 *On*が**0**に設定されていて*column_id*が NULL の場合、イベントはオフになり、すべての列がクリアされます。 *Column_id*が null でない場合、列は無効になります。  
  
 次の表は、 **\@** と **\@columnid**間の相互作用を示しています。  
  
|@on|@columnid|結果|  
|---------|---------------|------------|  
|ON (**1**)|NULL|イベントは ON になります。<br /><br /> すべての列が消去されます。|  
||NOT NULL|指定されたイベントに対して列が有効になっています。|  
|OFF (**0**)|NULL|イベントは無効になっています。<br /><br /> すべての列が消去されます。|  
||NOT NULL|指定されたイベントに対して列は OFF になります。|  
  
## <a name="return-code-values"></a>リターン コードの値  
 次の表は、このストアド プロシージャの完了時に返されるコード値を示しています。  
  
|リターン コード|[説明]|  
|-----------------|-----------------|  
|0|エラーなし。|  
|@shouldalert|原因不明のエラーです。|  
|2|トレースは現在実行中です。 この時点でトレースを変更すると、エラーが発生します。|  
|3|指定されたイベントは無効です。 イベントが存在しないか、またはストアドプロシージャに対して適切ではありません。|  
|4|指定した列は無効です。|  
|9|指定されたトレースハンドルは無効です。|  
|11|指定された列は内部で使用されているため、削除できません。|  
|13|メモリ不足。 指定されたアクションを実行するのに十分なメモリがない場合に返されます。|  
|16|関数は、このトレースに対して無効です。|  
  
## <a name="remarks"></a>Remarks  
 **sp_trace_setevent**では、以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]で使用できる拡張ストアドプロシージャによって以前に実行された操作の多くが実行されます。 次の代わりに**sp_trace_setevent**を使用します。  
  
-   **xp_trace_addnewqueue**  
  
-   **xp_trace_eventclassrequired**  
  
-   **xp_trace_seteventclassrequired**  
  
 ユーザーは、各イベントに追加された各列に対して**sp_trace_setevent**を実行する必要があります。 を実行するたびに **\@on**が**1**に設定されている場合、 **sp_trace_setevent**は、指定されたイベントをトレースのイベントの一覧に追加します。 **\@** が**0**に設定されている場合、 **sp_trace_setevent**指定されたイベントを一覧から削除します。  
  
 すべての SQL トレースストアドプロシージャ (**sp_trace_xx**) のパラメーターは厳密に型指定されます。 これらのパラメーターを、引数の説明で指定されている正しいデータ型で指定しないと、このストアド プロシージャではエラーが返されます。  
  
 トレース ストアド プロシージャを使用した例については、「[トレースの作成 &#40;Transact-SQL&#41;](../../relational-databases/sql-trace/create-a-trace-transact-sql.md)」を参照してください。  
  
## <a name="permissions"></a>アクセス許可  
 ユーザーは ALTER TRACE 権限を持っている必要があります。  
  
## <a name="see-also"></a>参照  
 [fn_trace_geteventinfo &#40;transact-sql&#41; ](../../relational-databases/system-functions/sys-fn-trace-geteventinfo-transact-sql.md)   
 [sys.fn_trace_getinfo &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-getinfo-transact-sql.md)   
 [transact-sql &#40;  の&#41; sp_trace_generateevent](../../relational-databases/system-stored-procedures/sp-trace-generateevent-transact-sql.md)  
 [SQL Server イベント クラスの参照](../../relational-databases/event-classes/sql-server-event-class-reference.md)   
 [SQL トレース](../../relational-databases/sql-trace/sql-trace.md)  
  
  
