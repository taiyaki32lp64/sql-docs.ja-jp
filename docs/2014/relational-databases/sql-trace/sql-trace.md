---
title: SQL トレース | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: 83c6d1d9-19ce-43fe-be9a-45aaa31f20cb
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a1dd2e117207f3737f54e2cd0269c51918a199f2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63286532"
---
# <a name="sql-trace"></a>SQL トレース (SQL Trace)
  SQL トレースでは、トレース定義に一覧表示されているイベント クラスのインスタンスであるイベントが収集されます。 このようなイベントは、フィルターによってトレースから除外したり、対象のキューに登録したりすることができます。 イベントの対象には、ファイルまたは [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 管理オブジェクト (SMO) を指定できます。SMO では、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]を管理するアプリケーションでトレース情報を使用できます。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 代わりに拡張イベントを使用します。  
  
## <a name="benefits-of-sql-trace"></a>SQL トレースの利点  
 Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] には、 [!INCLUDE[tsql](../../../includes/tsql-md.md)] のインスタンスでトレースを作成するための [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)]システム ストアド プロシージャが用意されています。 これらのシステム ストアド プロシージャを使用して、 [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)]からではなく、ユーザー独自のアプリケーションからトレースを手動で作成することもできます。 これにより、企業のニーズに合わせたカスタム アプリケーションを作成できます。  
  
## <a name="sql-trace-architecture"></a>SQL トレース アーキテクチャ  
 イベント ソースには、 [!INCLUDE[tsql](../../../includes/tsql-md.md)] バッチなどのトレース イベントやデッドロックなどの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] イベントを生成する任意のソースを指定できます。 イベントの詳細については、「 [SQL Server イベント クラスの参照](../event-classes/sql-server-event-class-reference.md)」を参照してください。 イベントの発生後、イベント クラスがトレース定義に含まれている場合は、トレースによってイベント情報が収集されます。 トレース定義に含まれているイベント クラスに対してフィルターが定義されている場合は、フィルターが適用され、トレース イベント情報がキューに渡されます。 キューに登録されたトレース情報は、ファイルに書き込まれるか、または [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)]などのアプリケーションで SMO によって使用されます。 次の図は、トレース中に SQL トレースによってどのようにイベントが収集されるかを示しています。  
  
 ![データベース エンジンのトレース処理](../../database-engine/media/tracarch.gif "データベース エンジンのトレース処理")  
  
## <a name="sql-trace-terminology"></a>SQL トレースの用語  
 次の用語は SQL トレースの主要な概念を示したものです。  
  
 **イベント**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)]のインスタンス内での操作により発生します。  
  
 **データ列**  
 イベントの属性。  
  
 **イベント クラス**  
 トレースできるイベントの種類。 イベント クラスには、イベントから報告できるすべてのデータ列が含まれています。  
  
 **イベント カテゴリ**  
 関連するイベント クラスのグループ。  
  
 **トレース** (名詞)  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]によって返されるイベントやデータのコレクション。  
  
 **トレース** (動詞)  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]のインスタンス内のイベントを収集および監視すること。  
  
 **Tracedefinition**  
 イベント クラス、データ列、およびトレース中に収集されるイベントの種類を識別するフィルターのコレクション。  
  
 **Assert**  
 トレースで収集されるイベントを限定する条件。  
  
 **トレース ファイル**  
 トレースの保存時に作成されるファイル。  
  
 **テンプレート**  
 [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)]では、トレースで収集されるイベント クラスやデータ列を定義するファイル。  
  
 **トレース テーブル**  
 [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)]で、トレースがテーブルに保存されるときに作成されるテーブル。  
  
## <a name="use-data-columns-to-describe-returned-events"></a>データ列による返されたイベントの説明  
 SQL トレースでは、トレース出力のデータ列を使用して、トレースの実行時に返されたイベントが説明されます。 次の表に、 [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] のデータ列を示します。これらのデータ列は、SQL トレースによって使用されるデータ列と同一のデータ列です。また、この表では、既定で選択されているデータ列を示しています。  
  
|データ列|列番号|説明|  
|-----------------|-------------------|-----------------|  
|**ApplicationName** <sup>1</sup>|10|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]のインスタンスへの接続を作成したクライアント アプリケーションの名前。 この列には、プログラム名ではなくアプリケーションによって渡された値が格納されます。|  
|**BigintData1**|52|トレースで指定されているイベント クラスに依存する値 (`bigint` データ型)。|  
|**BigintData2**|53|トレースで指定されているイベント クラスに依存する値 (`bigint` データ型)。|  
|**Binary Data**|2|トレースにキャプチャされるイベント クラスに依存するバイナリ値。|  
|**ClientProcessID** <sup>1</sup>|9|クライアント アプリケーションが実行されているプロセスに対し、ホスト コンピューターによって割り当てられた ID。 クライアントでクライアント プロセス ID が指定されると、このデータ列が作成されます。|  
|**ColumnPermissions**|44|列権限が設定されていたかどうかを示します。 ステートメントのテキストを解析して、どの権限がどの列に適用されていたかを判断できます。|  
|**CPU**|18|イベントで使用された CPU 時間 (ミリ秒)。|  
|**データベース ID** <sup>1</sup>|3|USE *database_name* ステートメントで指定されたデータベースの ID、または特定のインスタンスについて USE *database_name*ステートメントが実行されていない場合は既定のデータベースの ID となります。 [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] では、 **ServerName** データ列がトレースにキャプチャされ、そのサーバーが利用可能な場合、データベースの名前が表示されます。 データベースに対応する値は、DB_ID 関数を使用して特定します。|  
|**DatabaseName**|35|ユーザーのステートメントが実行されているデータベースの名前。|  
|**DBUserName** <sup>1</sup>|40|クライアントの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ユーザー名。|  
|**Duration**|13|イベントの期間 (ミリ秒)。<br /><br /> サーバーはマイクロ秒 (100 万分の 1 (10<sup>-6</sup>) 秒) 単位でのイベント期間、およびイベントにより使用されるミリ秒 (10<sup>-3</sup>秒) 単位での CPU 時間をレポートします。 [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] のグラフィカル ユーザー インターフェイスに、既定ではミリ秒単位で **Duration** 列が表示されますが、トレースがファイルまたはデータベース テーブルに保存されると、 **Duration** 列の値はマイクロ秒単位で記述されます。|  
|**EndTime**|15|イベントが終了した時刻。 **SQL:BatchStarting** や **SP:Starting**などのイベントの開始を示すイベント クラスには、このデータ列は作成されません。|  
|**Error**|31|特定のイベントのエラー番号。 これは多くの場合、 **sysmessages**に格納されたエラー番号です。|  
|**EventClass** <sup>1</sup>|27|キャプチャされるイベント クラスの種類。|  
|**EventSequence**|51|このイベントのシーケンス番号。|  
|**EventSubClass** <sup>1</sup>|21|イベント サブクラスの種類。各イベント クラスに関するより詳細な情報を提供します。 たとえば、 **Execution Warning** イベント クラスのイベント サブクラス値は、以下のような実行の警告の種類を表します。<br /><br /> **1** = クエリの待機。 クエリを実行するには、メモリなど、そのためのリソースが確保されるまで待機しなければなりません。<br /><br /> **2** = クエリのタイムアウト。クエリの実行に必要なリソースが確保されるのを待機していて時間切れになりました。 すべてのイベント クラスに対して、このデータ列が作成されるわけではありません。|  
|**GUID**|54|トレースで指定されているイベント クラスに依存する GUID 値。|  
|**FileName**|36|変更されるファイルの論理名。|  
|**Handle**|33|サーバーとの間で実行を調整するときに ODBC、OLE DB、または DB-Library によって使用される整数。|  
|**HostName** <sup>1</sup>|8|クライアントが実行しているコンピューターの名前。 このデータ列には、クライアントがホスト名を指定している場合にデータが格納されます。 ホスト名を指定するには、HOST_NAME 関数を使用します。|  
|**IndexID**|24|イベントの影響を受けるオブジェクトに付けられたインデックス用の ID。 オブジェクトのインデックス ID を調べるには、 **sysindexes** システム テーブルの **indid** 列を使用します。|  
|**IntegerData**|25|トレースにキャプチャされるイベント クラスに依存する整数値。|  
|**IntegerData2**|55|トレースにキャプチャされるイベント クラスに依存する整数値。|  
|**IsSystem**|60|システム プロセスまたはユーザー プロセスのどちらでイベントが発生したのかを示します。<br /><br /> **1** = システム<br /><br /> **0** = ユーザー|  
|**LineNumber**|5|エラーを含む行の番号が格納されます。 [!INCLUDE[tsql](../../../includes/tsql-md.md)] SP:StmtStarting **のような**ステートメントを含むイベントの場合、 **LineNumber** にはストアド プロシージャまたはバッチでのステートメントの行番号が格納されます。|  
|**LinkedServerName**|45|リンク サーバーの名前|  
|**LoginName**|11|ユーザーのログイン名 (SQL Server セキュリティ ログインまたは DOMAIN\Username の形式の Windows ログイン資格情報)。|  
|**LoginSid** <sup>1</sup>|41|ログイン ユーザーのセキュリティ ID (SID)。 この情報は、 **master** データベースの **sys.server_principals** ビューで参照できます。 サーバーへの各ログインには一意の ID が付けられています。|  
|**MethodName**|47|OLEDB メソッドの名前。|  
|**モード**|32|各種のイベントで要求している状態、または受け取った状態を説明するときに使用される整数。|  
|**NestLevel**|29|@@NESTLEVEL から返されるデータを表す整数。|  
|**NTDomainName** <sup>1</sup>|7|ユーザーが所属する Microsoft Windows ドメイン。|  
|**NTUserName** <sup>1</sup>|6|Windows のユーザー名。|  
|**Exchange Spill**|22|オブジェクトに対してシステムが割り当てた ID。|  
|**ObjectID2**|56|関連するオブジェクトまたはエンティティの ID (使用可能な場合)。|  
|**ObjectName**|34|参照されているオブジェクトの名前。|  
|**ObjectType** <sup>2</sup>|28|イベントに関係するオブジェクトの種類を表す値。 この値は **sysobjects** の **type**列に対応します。|  
|**Offset**|61|ストアド プロシージャまたはバッチ内のステートメントの開始オフセット。|  
|**OwnerID**|58|ロック イベントの場合にのみ該当します。 ロックを所有するオブジェクトの種類。|  
|**OwnerName**|37|オブジェクト所有者のデータベース ユーザー名。|  
|**ParentName**|59|オブジェクトが存在するスキーマ名。|  
|**権限**|19|チェックされた権限の種類を表す整数値。 値は次のとおりです。<br /><br /> **1** = SELECT ALL<br /><br /> **2** = UPDATE ALL<br /><br /> **4** = REFERENCES ALL<br /><br /> **8** = INSERT<br /><br /> **16** = DELETE<br /><br /> **32** = EXECUTE (プロシージャのみ)<br /><br /> **4096** = SELECT ANY (1 列以上)<br /><br /> **8192** = UPDATE ANY<br /><br /> **16384** = REFERENCES ANY|  
|**ProviderName**|46|OLEDB プロバイダーの名前。|  
|**Reads**|16|論理ディスク上の読み取り操作の回数。この操作は、イベントの代わりにサーバーによって実行されます。 これらの読み取り操作には、ステートメントの実行中に行われるテーブルやバッファーからのすべての読み取り操作が含まれます。|  
|**RequestID**|49|ステートメントを含んでいる要求の ID。|  
|**RoleName**|38|有効になっているアプリケーション ロールの名前。|  
|**RowCounts**|48|バッチ内の行数。|  
|**ServerName** <sup>1</sup>|26|トレースしている [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスの名前。|  
|**SessionLoginName**|64|セッションを開始したユーザーのログイン名。 たとえば、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] に **Login1** を使用して接続し、 **Login2**としてステートメントを実行した場合、 **SessionLoginName** には **Login1**が表示され、 **LoginName** には **Login2**が表示されます。 このデータ列には、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ログインと Windows ログインの両方が表示されます。|  
|**Severity**|20|例外イベントの重大度レベル。|  
|**SourceDatabaseID**|62|オブジェクトのソースが存在するデータベースの ID。|  
|**SPID**|12|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] によって割り当てられているサーバー プロセス ID (SPID)。この ID はクライアントに関連付けられています。|  
|**SqlHandle**|63|64 ビット ハッシュ。アドホック クエリやデータベースのテキスト、および SQL オブジェクトのオブジェクト ID に基づいています。 この値を **sys.dm_exec_sql_text()** に渡して、関連付けられている SQL テキストを取得できます。|  
|**StartTime** <sup>1</sup>|14|イベントの開始時刻 (取得できた場合)。|  
|**State**|30|エラー状態コード。|  
|**成功**|23|イベントが正常に終了したかどうかを表します。 値は次のとおりです。<br /><br /> **1** = 成功。<br /><br /> **0** = 失敗。<br /><br /> たとえば、 **1** は、権限チェックの成功を表し、 **0** は失敗を表します。|  
|**TargetLoginName**|42|ログインを対象とする操作 (新規ログインの追加など) の場合の対象ログインの名前。|  
|**TargetLoginSid**|43|ログインを対象とする操作 (新規ログインの追加など) の場合の対象ログインの SID。|  
|**TargetUserName**|39|データベース ユーザーを対象とした操作 (ユーザーへの権限の許可など) を行う場合の対象となるユーザーの名前。|  
|**TextData**|1|トレースにキャプチャされるイベント クラスに依存するテキスト値。 ただし、パラメーター化クエリをトレースする場合は、変数は **TextData** 列のデータ値と共には表示されません。|  
|**Transaction ID**|4|トランザクションに対してシステムが割り当てた ID。|  
|**型**|57|トレースにキャプチャされるイベント クラスに依存する整数値。|  
|**Writes**|17|イベントの代わりにサーバーによって実行される物理ディスクの書き込み操作回数。|  
|**XactSequence**|50|現在のトランザクションを記述するトークン。|  
  
 <sup>1</sup>これらのデータ列がすべてのイベントの既定で設定されます。  
  
 <sup>2</sup>の詳細については、 **ObjectType**データの列を参照してください[ObjectType トレース イベント列](../event-classes/objecttype-trace-event-column.md)します。  
  
## <a name="sql-trace-tasks"></a>SQL トレースのタスク  
  
|タスクの説明|トピック|  
|----------------------|-----------|  
|Transact-SQL ストアド プロシージャを使用してトレースを作成および実行する方法について説明します。|[Transact-SQL ストアド プロシージャを使用したトレースの作成と実行](../sql-trace/create-and-run-traces-using-transact-sql-stored-procedures.md)|  
|[!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)]のインスタンスに対するストアド プロシージャを使用して手動トレースを作成する方法について説明します。|[ストアド プロシージャを使用した手動トレースの作成](../sql-trace/create-manual-traces-using-stored-procedures.md)|  
|トレース結果が書き込まれるファイルにトレース結果を保存する方法について説明します。|[トレース結果のファイルへの保存](../sql-trace/save-trace-results-to-a-file.md)|  
|**temp** ディレクトリの空き領域の使用によってトレース データへのアクセスを向上させる方法について説明します。|[トレース データへのアクセスを向上させる](../sql-trace/improve-access-to-trace-data.md)|  
|ストアド プロシージャを使用してトレースを作成する方法について説明します。|[トレースの作成 &#40;Transact-SQL&#41;](../sql-trace/create-a-trace-transact-sql.md)|  
|ストアド プロシージャを使用して、トレース中のイベントに関して必要な情報のみを取得するフィルターを作成する方法について説明します。|[トレース フィルターの設定 &#40;Transact-SQL&#41;](../../ssms/agent/set-sql-server-alias-for-sql-server-agent-service-ssms.md)|  
|ストアド プロシージャを使用して既存のトレースを変更する方法について説明します。|[既存のトレースの変更 &#40;Transact-SQL&#41;](../sql-trace/modify-an-existing-trace-transact-sql.md)|  
|組み込み関数を使用して、保存されているトレースを表示する方法について説明します。|[保存されているトレースの表示 &#40;Transact-SQL&#41;](../sql-trace/view-a-saved-trace-transact-sql.md)|  
|組み込み関数を使用してトレース フィルター情報を表示する方法について説明します。|[フィルター情報の表示 &#40;Transact-SQL&#41;](../sql-trace/view-filter-information-transact-sql.md)|  
|ストアド プロシージャを使用してトレースを削除する方法について説明します。|[トレースの削除 &#40;Transact-SQL&#41;](../sql-trace/delete-a-trace-transact-sql.md)|  
|トレースによって発生するパフォーマンス コストを最小限に抑える方法について説明します。|[SQL トレースの最適化](../sql-trace/sql-trace.md)|  
|トレース中に発生するオーバーヘッドを最小限にするためにトレースをフィルター処理する方法について説明します。|[トレースへのフィルターの適用](../sql-trace/filter-a-trace.md)|  
|トレースで収集されるデータ量を最小限にする方法について説明します。|[トレース ファイルとテーブル サイズの制限](../sql-trace/limit-trace-file-and-table-sizes.md)|  
|Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]でトレースのスケジュールを設定するための 2 つの方法について説明します。|[トレースのスケジュール設定](../sql-trace/schedule-traces.md)|  
  
## <a name="see-also"></a>参照  
 [SQL Server プロファイラーのテンプレートと権限](../../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)   
 [SQL Server 管理オブジェクト &#40;SMO&#41; プログラミング ガイド](../server-management-objects-smo/sql-server-management-objects-smo-programming-guide.md)  
  
  
