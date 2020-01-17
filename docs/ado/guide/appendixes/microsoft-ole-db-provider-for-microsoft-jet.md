---
title: Microsoft OLE DB Provider for Microsoft Jet |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Jet provider for OLE DB [ADO]
- providers [ADO], OLE DB provider for Microsoft Jet
- OLE DB provider for Microsoft Jet [ADO]
ms.assetid: fd956da1-5203-40af-aa7e-fc13a6c6581f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 69d88aebe25f6cfa5490cce736c05780b87eee6e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67926644"
---
# <a name="microsoft-ole-db-provider-for-microsoft-jet-overview"></a>Microsoft OLE DB Provider for Jet の概要
OLE DB Provider For Microsoft Jet を使うと、ADOで Microsoft Jet データベースにアクセスできます。

## <a name="connection-string-parameters"></a>接続文字列パラメーター
 このプロバイダーに接続するには、[ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) プロパティの *Provider* 引数を以下のように設定します。 

```vb
Microsoft.Jet.OLEDB.4.0
```

[Provider](../../../ado/reference/ado-api/provider-property-ado.md)プロパティを読み出すとこの文字列を返します。

## <a name="typical-connection-string"></a>一般的な接続文字列
 このプロバイダーの一般的な接続文字列は次のとおりです。

```vb
"Provider=Microsoft.Jet.OLEDB.4.0;Data Source=databaseName;User ID=MyUserID;Password=MyPassword;"
```

 接続文字列は、以下のようなキーワードで構成されます。

|Keyword|説明|
|-------------|-----------------|
|**Provider**|OLE DB Proider For Microsoft Jet を指定します。|
|**Data Source**|データベースのパスとファイル名を指定します (たとえば `c:\Northwind.mdb`)。|
|**User ID**|ユーザー名を指定します。 このキーワードが指定されていない場合、文字列"`admin`" が既定で使用されます。|
|**Password**|ユーザーのパスワードを指定します。 このキーワードが指定されていない場合、空の文字列 ("") が既定で使用されます。|

> [!NOTE]
>  Windows 認証をサポートするデータ ソース プロバイダーに接続する場合は、ユーザー ID とパスワードの代わりに **Trusted_Connection = yes**または**Integrated Security = SSPI** を指定する必要があります。

## <a name="provider-specific-connection-parameters"></a>プロバイダー固有の接続パラメーター
 OLE DB Provide For Microsoft Jet は、ADO で定義されているものに加えて、いくつかのプロバイダー固有の動的プロパティをサポートします。 他のすべての **Connection** パラメータと同様に、**Connection** オブジェクトの **Propaties** コレクション、または接続文字列の一部として指定できます。

 次の表は、これらのプロパティの一覧です。かっこ内には対応する OLE DB プロパティ名を表示しています。

|パラメーター|説明|
|---------------|-----------------|
|Jet OLEDB:Compact 解放された領域の容量 (DBPROP_JETOLEDB_COMPACTFREESPACESIZE)|データベースの最適化で再利用できるをバイト単位での領域の量の推定値を示します。 この値は、データベース接続が確立された後にのみ有効です。|
|Jet OLEDB:Connection コントロール (DBPROP_JETOLEDB_CONNECTIONCONTROL)|ユーザーがデータベースに接続できるかどうかを示します。|
|Jet OLEDB: システム データベース (DBPROP_JETOLEDB_CREATESYSTEMDATABASE) の作成|新しいデータ ソースを作成するときにシステム データベースを作成するかどうかを示します。|
|Jet oledb: データベースのロック モード (DBPROP_JETOLEDB_DATABASELOCKMODE)|このデータベースのロック モードを示します。 最初のユーザー データベースを開くには、データベースが開いている間に使用するモードを決定します。|
|Jet oledb: データベースのパスワード (DBPROP_JETOLEDB_DATABASEPASSWORD)|データベースのパスワードを示します。|
|Jet OLEDB: Compact (DBPROP_JETOLEDB_COMPACT_DONTCOPYLOCALE) のロケールはコピーしません|データベースを圧縮する場合に、Jet がロケール情報をコピーするかどうかを示します。|
|Jet OLEDB: データベース (DBPROP_JETOLEDB_ENCRYPTDATABASE) の暗号化|最適化されたデータベースを暗号化するかどうかを示します。 このプロパティが設定されていない場合は、元のデータベースは暗号化もされている場合、圧縮されたデータベースが暗号化されます。|
|Jet OLEDB:Engine 型 (DBPROP_JETOLEDB_ENGINE)|現在のデータ ストアにアクセスするために使用するストレージ エンジンを示します。|
|Jet OLEDB:Exclusive 非同期遅延 (DBPROP_JETOLEDB_EXCLUSIVEASYNCDELAY)|時間 (ミリ秒)、データベースが排他的に開かれるときにディスクに非同期の書き込み遅延の最大長を示します。<br /><br /> しない限り、このプロパティは無視されます**Jet OLEDB:Flush トランザクション タイムアウト**は 0 に設定します。|
|Jet OLEDB:Flush トランザクションのタイムアウト (DBPROP_JETOLEDB_FLUSHTRANSACTIONTIMEOUT)|非同期書き込みのためのキャッシュに格納されたデータが実際に書き込まれる前に待機する時間の割合をディスクにします。 この設定の値をオーバーライドする**Jet OLEDB: 共有非同期遅延**と**Jet OLEDB:Exclusive 非同期遅延**します。|
|Jet OLEDB: グローバル一括トランザクション (DBPROP_JETOLEDB_GLOBALBULKNOTRANSACTIONS)|SQL 一括トランザクションが処理されるかどうかを示します。|
|Jet OLEDB: グローバルの部分的な一括操作 (DBPROP_JETOLEDB_GLOBALBULKPARTIAL)|データベースを開くために使用するパスワードを示します。|
|Jet OLEDB: 暗黙的なコミットの同期 (DBPROP_JETOLEDB_IMPLICITCOMMITSYNC)|内部の暗黙的なトランザクションで加えられた変更が同期または非同期モードで記述されたかどうかを示します。|
|Jet OLEDB:Lock 遅延 (DBPROP_JETOLEDB_LOCKDELAY)|前回の試みが失敗した後、ロックの取得を試みる前に待機するミリ秒数を示します。|
|Jet OLEDB:Lock 再試行 (DBPROP_JETOLEDB_LOCKRETRY)|ロックされたページにアクセスしようが繰り返される回数を示します。|
|Jet OLEDB:Max バッファー サイズ (DBPROP_JETOLEDB_MAXBUFFERSIZE)|最大容量を示しますメモリ、キロバイト単位で Jet を使用できるの変更をディスクにフラッシュする前にします。|
|ファイル (DBPROP_JETOLEDB_MAXLOCKSPERFILE) ごとの jet OLEDB:Max ロック|データベースに配置できるロックの最大数を示します。 既定値は、9500 です。|
|Jet OLEDB: 新しいデータベースのパスワード (DBPROP_JETOLEDB_NEWDATABASEPASSWORD)|このデータベース用に設定する新しいパスワードを示します。 古いパスワードが保存される**Jet oledb: データベース パスワード**します。|
|Jet OLEDB:ODBC コマンド タイムアウト (DBPROP_JETOLEDB_ODBCCOMMANDTIMEOUT)|リモート Jet から ODBC クエリまでのミリ秒数がタイムアウトになることを示します。|
|テーブル ロック (DBPROP_JETOLEDB_PAGELOCKSTOTABLELOCK) に jet OLEDB:Page をロックします。|ページ数は、Jet テーブル ロックにロックを昇格しようとする前に、トランザクション内でロック必要があることを示します。 この値が 0 の場合、ロックは昇格されません。|
|Jet OLEDB:Page タイムアウト (DBPROP_JETOLEDB_PAGETIMEOUT)|Jet は、キャッシュがデータベース ファイルを使用して最新でないかどうかを確認する前に待機するミリ秒数を示します。|
|Jet OLEDB:Recycle 時間の長い値を持つページ (DBPROP_JETOLEDB_RECYCLELONGVALUEPAGES)|Jet は解放されるときに、BLOB のページを再利用する積極的に試みるかどうかを示します。|
|Jet OLEDB:Registry パス (DBPROP_JETOLEDB_REGPATH)|Jet データベース エンジンの値を含む Windows レジストリ キーを示します。|
|Jet OLEDB:Reset ISAM Stats (DBPROP_JETOLEDB_RESETISAMSTATS)|示すかどうか、スキーマ**レコード セット**DBSCHEMA_JETOLEDB_ISAMSTATS はパフォーマンス情報が返された後、パフォーマンス カウンターをリセットする必要があります。|
|Jet OLEDB: 非同期遅延 (DBPROP_JETOLEDB_SHAREDASYNCDELAY) を共有|最大容量を示します Jet の時間 (ミリ秒)、マルチ ユーザー モードでデータベースを開くときにディスクへの非同期書き込みを遅らせることができます。|
|Jet OLEDB:System Database (DBPROP_JETOLEDB_SYSDBPATH)|ワークグループ情報ファイル (システム データベース) のパスとファイル名を示します。|
|Jet OLEDB:Transaction コミット モード (DBPROP_JETOLEDB_TXNCOMMITMODE)|Jet が同期的にディスクにデータを書き込むかどうかまたは非同期的にトランザクションがコミットされたことを示します。|
|Jet OLEDB:User コミット同期 (DBPROP_JETOLEDB_USERCOMMITSYNC)|同期または非同期モードでのトランザクションで加えられた変更を書き込むかどうかを示します。|

## <a name="provider-specific-recordset-and-command-properties"></a>プロバイダー固有のレコード セットとコマンドのプロパティ
 Jet プロバイダーは、プロバイダーに固有のいくつかもサポートしています。 **Recordset**と**コマンド**プロパティ。 これらのプロパティにアクセスして、設定、**プロパティ**のコレクション、 **Recordset**または**コマンド**オブジェクト。 テーブルには、ADO のプロパティ名とかっこで囲まれた対応する OLE DB プロパティ名が一覧表示します。

|プロパティ名|説明|
|-------------------|-----------------|
|Jet OLEDB:Bulk トランザクション (DBPROP_JETOLEDB_BULKNOTRANSACTIONS)|SQL 一括操作が処理されるかどうかを示します。 リソースの遅延のため、トランザクションと、大規模な一括操作が失敗することがあります。|
|Jet OLEDB:Enable Fat カーソル (DBPROP_JETOLEDB_ENABLEFATCURSOR)|リモート行ソースのレコード セットを設定するときに、複数の行をキャッシュするかどうかを示します。|
|Jet OLEDB:Fat カーソルのキャッシュ サイズ (DBPROP_JETOLEDB_FATCURSORMAXROWS)|リモート データ ストアの行のキャッシュを使用する場合は、キャッシュする行の数を示します。 しない限り、この値は無視されます**Jet OLEDB:Enable Fat カーソル**は True です。|
|Jet OLEDB: 一貫性のない (DBPROP_JETOLEDB_INCONSISTENT)|クエリの結果が一貫性のない更新を許可するかどうかを示します。|
|Jet OLEDB: ロック粒度 (DBPROP_JETOLEDB_LOCKGRANULARITY)|行レベルのロックを使用して、テーブルを開くかどうかを示します。|
|Jet OLEDB:ODBC パススルー ステートメント (DBPROP_JETOLEDB_ODBCPASSTHROUGH)|Jet が内の SQL テキストを渡すことを示します、**コマンド**オブジェクトをそのままバックエンドにします。|
|Jet OLEDB:Partial 一括 Ops (DBPROP_JETOLEDB_BULKPARTIAL)|SQL DML 操作が失敗したときに、Jet の動作を示します。|
|Jet OLEDB:Pass クエリ一括 Op (DBPROP_JETOLEDB_PASSTHROUGHBULKOP) 経由|かどうかクエリを実行しないことを示します。 を返す、**レコード セット**データ ソースに変更されていないに渡されます。|
|Jet OLEDB:Pass クエリからの接続文字列 (DBPROP_JETOLEDB_ODBCPASSTHROUGHCONNECTSTRING)|使用する Jet の接続文字列を示しますリモート データ ストアに接続します。 しない限り、この値は無視されます**Jet OLEDB:ODBC パススルー ステートメント**は True です。|
|Jet OLEDB: クエリ (DBPROP_JETOLEDB_STOREDQUERY) が格納されています。|コマンド テキストを SQL コマンドではなくストアド クエリとして解釈するかどうかを示します。|
|Jet OLEDB: 規則セット (DBPROP_JETOLEDB_VALIDATEONSET) での検証|列のデータが設定されている場合、または変更をデータベースにコミットするときに、Jet の検証規則が評価されるかどうかを示します。|

 既定では、for Microsoft Jet OLE DB プロバイダーは、Microsoft Jet データベースを読み取り/書き込みモードで開きます。 読み取り専用モードでデータベースを開く、設定、[モード](../../../ado/reference/ado-api/mode-property-ado.md)プロパティ、ADO を**接続**オブジェクトを**adModeRead**。

## <a name="command-object-usage"></a>コマンド オブジェクトの使用方法
 コマンドのテキスト、[コマンド](../../../ado/reference/ado-api/command-object-ado.md)オブジェクトが、Microsoft Jet SQL 言語を使用します。 コマンド テキストで行を返すクエリ、操作クエリ、およびテーブル名を指定することができます。ただし、ストアド プロシージャはサポートされていません、指定されていない必要があります。

## <a name="recordset-behavior"></a>レコード セットの動作
 Microsoft Jet データベース エンジンは、動的カーソルをサポートしていません。 したがって、for Microsoft Jet OLE DB プロバイダーはできません、 **adLockDynamic**カーソルの種類。 動的カーソルが要求されたときに、プロバイダーは、キーセット カーソルを返すし、リセット、 [CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md)プロパティの種類を示す[Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)が返されます。 さらに、更新可能な場合**Recordset**が要求された (**LockType**は**adLockOptimistic**、 **adLockBatchOptimistic**、または**adLockPessimistic**) また、プロバイダー、キーセット カーソルを返すし、リセット、 **CursorType**プロパティ。

## <a name="dynamic-properties"></a>動的プロパティ
 For Microsoft Jet OLE DB Provider にいくつかの動的プロパティの挿入、**プロパティ**、開かれていないのコレクション[接続](../../../ado/reference/ado-api/connection-object-ado.md)、 [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)、および[コマンド](../../../ado/reference/ado-api/command-object-ado.md)オブジェクト。

 次の表は、ADO および OLE DB 名の各動的プロパティの相互です。 「説明です」という用語を ADO プロパティ名を参照して OLE DB プログラマーズ リファレンス これらのプロパティの詳細については、OLE DB プログラマーズ リファレンスに見つかります。

## <a name="connection-dynamic-properties"></a>接続の動的プロパティ
 次のプロパティに追加されます、**プロパティ**のコレクション、**接続**オブジェクト。

|ADO のプロパティ名|OLE DB プロパティの名前|
|-----------------------|--------------------------|
|Active sessions|DBPROP_ACTIVESESSIONS|
|非同期で起こる中止|DBPROP_ASYNCTXNABORT|
|非同期のコミット|DBPROP_ASYNCTNXCOMMIT|
|自動コミット分離レベル|DBPROP_SESS_AUTOCOMMITISOLEVELS|
|カタログの場所|DBPROP_CATALOGLOCATION|
|カタログ用語|DBPROP_CATALOGTERM|
|列の定義|DBPROP_COLUMNDEFINITION|
|現在のカタログ|DBPROP_CURRENTCATALOG|
|[データ ソース]|DBPROP_INIT_DATASOURCE|
|Data Source Name|DBPROP_DATASOURCENAME|
|データ ソース オブジェクト スレッド モデル|DBPROP_DSOTHREADMODEL|
|DBMS 名|DBPROP_DBMSNAME|
|DBMS バージョン|DBPROP_DBMSVER|
|GROUP BY をサポート|DBPROP_GROUPBY|
|異なるテーブルのサポート|DBPROP_HETEROGENEOUSTABLES|
|識別子の大文字と小文字の区別|DBPROP_IDENTIFIERCASE|
|分離レベル|DBPROP_SUPPORTEDTXNISOLEVELS|
|分離の保持|DBPROP_SUPPORTEDTXNISORETAIN|
|[Locale Identifier]|DBPROP_INIT_LCID|
|インデックスの最大サイズ|DBPROP_MAXINDEXSIZE|
|行の最大サイズ|DBPROP_MAXROWSIZE|
|最大行サイズには、BLOB が含まれています。|DBPROP_MAXROWSIZEINCLUDESBLOB|
|SELECT の最大のテーブル|DBPROP_MAXTABLESINSELECT|
|モード|DBPROP_INIT_MODE|
|複数のパラメーター セット|DBPROP_MULTIPLEPARAMSETS|
|複数の結果|DBPROP_MULTIPLERESULTS|
|複数のストレージ オブジェクト|DBPROP_MULTIPLESTORAGEOBJECTS|
|複数のテーブルの更新|DBPROP_MULTITABLEUPDATE|
|NULL 照合順序|DBPROP_NULLCOLLATION|
|NULL 連続動作|DBPROP_CONCATNULLBEHAVIOR|
|OLE DB バージョン|DBPROP_PROVIDEROLEDBVER|
|OLE オブジェクトのサポート|DBPROP_OLEOBJECTS|
|開いている行セットのサポート|DBPROP_OPENROWSETSUPPORT|
|選択リストの ORDER BY 列|DBPROP_ORDERBYCOLUMNSINSELECT|
|出力パラメーターの使用状況|DBPROP_OUTPUTPARAMETERAVAILABILITY|
|Ref アクセサーを使って渡す|DBPROP_BYREFACCESSORS|
|パスワード|DBPROP_AUTH_PASSWORD|
|永続的な ID の種類|DBPROP_PERSISTENTIDTYPE|
|中止動作を準備します。|DBPROP_PREPAREABORTBEHAVIOR|
|コミット動作を準備します。|DBPROP_PREPARECOMMITBEHAVIOR|
|プロシージャ用語|DBPROP_PROCEDURETERM|
|[プロンプト]|DBPROP_INIT_PROMPT|
|プロバイダーの表示名|DBPROP_PROVIDERFRIENDLYNAME|
|Provider Name|DBPROP_PROVIDERFILENAME|
|プロバイダーのバージョン|DBPROP_PROVIDERVER|
|読み取り専用データ ソース|DBPROP_DATASOURCEREADONLY|
|行セットの変換|DBPROP_ROWSETCONVERSIONSONCOMMAND|
|スキーマ用語|DBPROP_SCHEMATERM|
|スキーマの使用|DBPROP_SCHEMAUSAGE|
|SQL のサポート|DBPROP_SQLSUPPORT|
|構造化ストレージ|DBPROP_STRUCTUREDSTORAGE|
|サブクエリのサポート|DBPROP_SUBQUERIES|
|テーブル用語|DBPROP_TABLETERM|
|トランザクション DDL|DBPROP_SUPPORTEDTXNDDL|
|[ユーザー ID]|DBPROP_AUTH_USERID|
|[ユーザー名]|DBPROP_USERNAME|
|ウィンドウ ハンドル|DBPROP_INIT_HWND|

## <a name="recordset-dynamic-properties"></a>レコード セットの動的プロパティ
 次のプロパティに追加されます、**プロパティ**のコレクション、 **Recordset**オブジェクト。

|ADO のプロパティ名|OLE DB プロパティの名前|
|-----------------------|--------------------------|
|アクセスの順序|DBPROP_ACCESSORDER|
|追加専用の行セット|DBPROP_APPENDONLY|
|ブロッキング ストレージ オブジェクト|DBPROP_BLOCKINGSTORAGEOBJECTS|
|ブックマークの種類|DBPROP_BOOKMARKTYPE|
|ブックマークを設定|DBPROP_IROWSETLOCATE|
|ブックマークの順序指定|DBPROP_ORDEREDBOOKMARKS|
|キャッシュ列の遅延|DBPROP_CACHEDEFERRED|
|挿入行を変更します。|DBPROP_CHANGEINSERTEDROWS|
|列の特権|DBPROP_COLUMNRESTRICT|
|列セットの通知|DBPROP_NOTIFYCOLUMNSET|
|書き込み可能な列|DBPROP_MAYWRITECOLUMN|
|列を遅延します。|DBPROP_DEFERRED|
|ストレージ オブジェクトの更新を遅延|DBPROP_DELAYSTORAGEOBJECTS|
|後方のフェッチします。|DBPROP_CANFETCHBACKWARDS|
|行を保持します。|DBPROP_CANHOLDROWS|
|IAccessor|DBPROP_IAccessor|
|IColumnsInfo|DBPROP_IColumnsInfo|
|IColumnsRowset|DBPROP_IColumnsRowset|
|IConnectionPointContainer|DBPROP_IConnectionPointContainer|
|IConvertType|DBPROP_IConvertType|
|ILockBytes|DBPROP_ILockBytes|
|固定行|DBPROP_IMMOBILEROWS|
|IRowset|DBPROP_IRowset|
|IRowsetChange|DBPROP_IRowsetChange|
|IRowsetIdentity|DBPROP_IRowsetIdentity|
|IRowsetIndex|DBPROP_IRowsetIndex|
|IRowsetInfo|DBPROP_IRowsetInfo|
|IRowsetLocate|DBPROP_IRowsestLocate|
|IRowsetResynch||
|IRowsetScroll|DBPROP_IRowsetScroll|
|IRowsetUpdate|DBPROP_IRowsetUpdate|
|ISequentialStream|DBPROP_ISequentialStream|
|IStorage|DBPROP_IStorage|
|IStream|DBPROP_IStream|
|ISupportErrorInfo|DBPROP_ISupportErrorInfo|
|リテラル ブックマーク|DBPROP_LITERALBOOKMARKS|
|リテラル行の Id|DBPROP_LITERALIDENTITY|
|開いている行の最大数|DBPROP_MAXOPENROWS|
|保留中の行の最大数|DBPROP_MAXPENDINGROWS|
|行の最大数|DBPROP_MAXROWS|
|メモリ使用量|DBPROP_MEMORYUSAGE|
|通知の粒度|DBPROP_NOTIFICATIONGRANULARITY|
|通知フェーズ|DBPROP_NOTIFICATIONPHASES|
|トランザクション化されたオブジェクト|DBPROP_TRANSACTEDOBJECT|
|その他の変更の表示|DBPROP_OTHERUPDATEDELETE|
|他のユーザーの挿入を可視化|DBPROP_OTHERINSERT|
|独自の変更の表示|DBPROP_OWNUPDATEDELETE|
|独自の挿入を可視化|DBPROP_OWNINSERT|
|中止時に保存します。|DBPROP_ABORTPRESERVE|
|コミット時に保存します。|DBPROP_COMMITPRESERVE|
|クイック再起動|DBPROP_QUICKRESTART|
|再入イベント|DBPROP_REENTRANTEVENTS|
|削除された行を削除します。|DBPROP_REMOVEDELETED|
|複数の変更を報告します。|DBPROP_REPORTMULTIPLECHANGES|
|保留中の挿入を返す|DBPROP_RETURNPENDINGINSERTS|
|行の削除通知|DBPROP_NOTIFYROWDELETE|
|行の最初の変更通知|DBPROP_NOTIFYROWFIRSTCHANGE|
|行の挿入通知|DBPROP_NOTIFYROWINSERT|
|行の特権|DBPROP_ROWRESTRICT|
|行の再同期の通知|DBPROP_NOTIFYROWRESYNCH|
|行のスレッド モデル|DBPROP_ROWTHREADMODEL|
|行の変更の取り消し通知|DBPROP_NOTIFYROWUNDOCHANGE|
|行の削除の取り消し通知|DBPROP_NOTIFYROWUNDODELETE|
|行の挿入の取り消し通知|DBPROP_NOTIFYROWUNDOINSERT|
|行の更新通知|DBPROP_NOTIFYROWUPDATE|
|行セットのフェッチ位置の変更通知|DBPROP_NOTIFYROWSETFETCHPOSISIONCHANGE|
|行セットの解放通知|DBPROP_NOTIFYROWSETRELEASE|
|逆にスクロールします。|DBPROP_CANSCROLLBACKWARDS|
|削除されたブックマークをスキップ|DBPROP_BOOKMARKSKIPPED|
|厳密な行の Id|DBPROP_STRONGITDENTITY|
|更新機能|DBPROP_UPDATABILITY|
|ブックマークを使用します。|DBPROP_BOOKMARKS|

## <a name="command-dynamic-properties"></a>コマンドの動的プロパティ
 次のプロパティに追加されます、**プロパティ**のコレクション、**コマンド**オブジェクト。

|ADO のプロパティ名|OLE DB プロパティの名前|
|-----------------------|--------------------------|
|アクセスの順序|DBPROP_ACCESSORDER|
|追加専用の行セット|DBPROP_APPENDONLY|
|ブロッキング ストレージ オブジェクト|DBPROP_BLOCKINGSTORAGEOBJECTS|
|ブックマークの種類|DBPROP_BOOKMARKTYPE|
|ブックマークを設定|DBPROP_IROWSETLOCATE|
|挿入行を変更します。|DBPROP_CHANGEINSERTEDROWS|
|列の特権|DBPROP_COLUMNRESTRICT|
|列セットの通知|DBPROP_NOTIFYCOLUMNSET|
|列を遅延します。|DBPROP_DEFERRED|
|ストレージ オブジェクトの更新を遅延|DBPROP_DELAYSTORAGEOBJECTS|
|後方のフェッチします。|DBPROP_CANFETCHBACKWARDS|
|行を保持します。|DBPROP_CANHOLDROWS|
|IAccessor|DBPROP_IAccessor|
|IColumnsInfo|DBPROP_IColumnsInfo|
|IColumnsRowset|DBPROP_IColumnsRowset|
|IConnectionPointContainer|DBPROP_IConnectionPointContainer|
|IConvertType|DBPROP_IConvertType|
|ILockBytes|DBPROP_ILockBytes|
|固定行|DBPROP_IMMOBILEROWS|
|IRowset|DBPROP_IRowset|
|IRowsetChange|DBPROP_IRowsetChange|
|IRowsetIdentity|DBPROP_IRowsetIdentity|
|IRowsetIndex|DBPROP_IRowsetIndex|
|IRowsetInfo|DBPROP_IRowsetInfo|
|IRowsetLocate|DBPROP_IRowsetLocate|
|IRowsetResynch||
|IRowsetScroll|DBPROP_IRowsetScroll|
|IRowsetUpdate|DBPROP_IRowsetUpdate|
|ISequentialStream|DBPROP_ISequentialStream|
|IStorage|DBPROP_IStorage|
|IStream|DBPROP_IStream|
|ISupportErrorInfo|DBPROP_ISupportErrorInfo|
|リテラル ブックマーク|DBPROP_LITERALBOOKMARKS|
|リテラル行の Id|DBPROP_LITERALIDENTITY|
|ロック モード|DBPROP_LOCKMODE|
|開いている行の最大数|DBPROP_MAXOPENROWS|
|保留中の行の最大数|DBPROP_MAXPENDINGROWS|
|行の最大数|DBPROP_MAXROWS|
|通知の粒度|DBPROP_NOTIFICATIONGRANULARITY|
|通知フェーズ|DBPROP_NOTIFICATIONPHASES|
|トランザクション化されたオブジェクト|DBPROP_TRANSACTEDOBJECT|
|その他の変更の表示|DBPROP_OTHERUPDATEDELETE|
|他のユーザーの挿入を可視化|DBPROP_OTHERINSERT|
|独自の変更の表示|DBPROP_OWNUPDATEDELETE|
|独自の挿入を可視化|DBPROP_OWNINSERT|
|中止時に保存します。|DBPROP_ABORTPRESERVE|
|コミット時に保存します。|DBPROP_COMMITPRESERVE|
|クイック再起動|DBPROP_QUICKRESTART|
|再入イベント|DBPROP_REENTRANTEVENTS|
|削除された行を削除します。|DBPROP_REMOVEDELETED|
|複数の変更を報告します。|DBPROP_REPORTMULTIPLECHANGES|
|保留中の挿入を返す|DBPROP_RETURNPENDINGINSERTS|
|行の削除通知|DBPROP_NOTIFYROWDELETE|
|行の最初の変更通知|DBPROP_NOTIFYROWFIRSTCHANGE|
|行の挿入通知|DBPROP_NOTIFYROWINSERT|
|行の特権|DBPROP_ROWRESTRICT|
|行の再同期の通知|DBPROP_NOTIFYROWRESYNCH|
|行のスレッド モデル|DBPROP_ROWTHREADMODEL|
|行の変更の取り消し通知|DBPROP_NOTIFYROWUNDOCHANGE|
|行の削除の取り消し通知|DBPROP_NOTIFYROWUNDODELETE|
|行の挿入の取り消し通知|DBPROP_NOTIFYROWUNDOINSERT|
|行の更新通知|DBPROP_NOTIFYROWUPDATE|
|行セットのフェッチ位置の変更通知|DBPROP_NOTIFYROWSETFETCHPOSITIONCHANGE|
|行セットの解放通知|DBPROP_NOTIFYROWSETRELEASE|
|逆にスクロールします。|DBPROP_CANSCROLLBACKWARDS|
|サーバーのデータを挿入|DBPROP_SERVERDATAONINSERT|
|削除されたブックマークをスキップ|DBPROP_BOOKMARKSKIP|
|厳密な行の Id|DBPROP_STRONGIDENTITY|
|更新機能|DBPROP_UPDATABILITY|
|ブックマークを使用します。|DBPROP_BOOKMARKS|

 特定の実装の詳細と for Microsoft Jet OLE DB プロバイダーの機能については、次を参照してください。 [Jet プロバイダー](https://msdn.microsoft.com/library/windows/desktop/ms722791.aspx) OLE DB のドキュメント。
