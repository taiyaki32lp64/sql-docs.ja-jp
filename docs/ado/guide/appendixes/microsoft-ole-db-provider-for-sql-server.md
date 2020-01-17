---
title: Microsoft OLE DB Provider for SQL Server |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- providers [ADO], OLE DB provider for SQL Server
- OLE DB provider for SQL Server [ADO]
- SQLOLEDB [ADO]
ms.assetid: 99bc40c4-9181-4ca1-a06f-9a1a914a0b7b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bd28ece0e82c4551409920c876d54fbd7dc501ff
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67926612"
---
# <a name="microsoft-ole-db-provider-for-sql-server-overview"></a>Microsoft OLE DB Provider for SQL Server の概要
Microsoft OLE DB Provider for SQL Server、SQLOLEDB には、Microsoft SQL Server にアクセスする ADO ができます。

> [!IMPORTANT]
> Microsoft OLE DB Provider for SQL Server (SQLOLEDB) は非推奨と、新しい開発作業で使用するには使用しないでいます。 代わりに、新しい使用[Microsoft OLE DB Driver for SQL Server](../../../connect/oledb/oledb-driver-for-sql-server.md) (MSOLEDBSQL) server の最新の機能と更新されます。

## <a name="connection-string-parameters"></a>接続文字列パラメーター
 このプロバイダーに接続するには、設定、*プロバイダー*への引数、 [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)プロパティ。

```vb
SQLOLEDB
```

 この値も設定またはを使用して読み取る、[プロバイダー](../../../ado/reference/ado-api/provider-property-ado.md)プロパティ。

## <a name="typical-connection-string"></a>一般的な接続文字列
 このプロバイダーの一般的な接続文字列は次のとおりです。

```vb
"Provider=SQLOLEDB;Data Source=serverName;"
Initial Catalog=databaseName;
User ID=MyUserID;Password=MyPassword;"
```

 文字列は、これらのキーワードで構成されます。

|Keyword|説明|
|-------------|-----------------|
|**Provider**|OLE DB Provider for SQL Server を指定します。|
|**Data Source**または**Server**|サーバーの名前を指定します。|
|**Initial Catalog**または**データベース**|サーバー上のデータベースの名前を指定します。|
|**User ID**または**uid**|(SQL Server 認証) のユーザー名を指定します。|
|**Password**または**pwd**|(SQL Server 認証) のユーザーのパスワードを指定します。|

> [!NOTE]
>  Windows 認証をサポートするデータ ソース プロバイダーに接続するかどうかは、する必要がありますを指定する**Trusted_Connection = yes**または**Integrated Security = SSPI**ユーザー ID とパスワードの代わりに接続文字列の情報です。

## <a name="provider-specific-connection-parameters"></a>プロバイダー固有の接続パラメーター
 プロバイダーは、ADO で定義されているだけでなく、いくつかのプロバイダーに固有の接続パラメーターをサポートします。 ADO 接続のプロパティを持つこれらのプロバイダーに固有のプロパティを設定してを使用して、[プロパティ](../../../ado/reference/ado-api/properties-collection-ado.md)のコレクション、[接続](../../../ado/reference/ado-api/connection-object-ado.md)の一部として設定できますまたは、 **ConnectionString**。

|パラメーター|説明|
|---------------|-----------------|
|Trusted_Connection|ユーザーの認証モードを示します。 これに設定することができます**はい**または**いいえ**します。 既定値は**いいえ**します。 このプロパティ設定されている場合**はい**、SQLOLEDB では、Microsoft Windows NT の認証モードを使用して、ユーザーによって指定された SQL Server データベースへのアクセスを承認します、**場所**と[データソース](../../../ado/reference/ado-api/datasource-property-ado.md)プロパティの値。 このプロパティ設定されている場合**いいえ**SQLOLEDB が混在モードを使用して、SQL Server データベースへのユーザー アクセスを承認するためにします。 SQL Server ログインとパスワードが指定されて、**ユーザー Id**と**パスワード**プロパティ。|
|[現在の言語]|SQL Server の言語名を示します。 システム メッセージの選択や書式設定に使われる言語を示します。 SQL Server で言語をインストールする必要がありますそれ以外の場合の開始が、接続は失敗します。|
|[ネットワーク アドレス]|指定された SQL Server のネットワーク アドレスを示します、**場所**プロパティ。|
|ネットワーク ライブラリ|SQL Server との通信に使用されるネットワーク ライブラリ (DLL) の名前を示します。 この名前には、パスやファイル拡張子 (.dll) は含めません。 既定値は、SQL Server クライアントの構成によって提供されます。|
|準備手順を使用します。|コマンドを準備するときに、SQL Server が一時ストアド プロシージャを作成するかどうかを決定します (によって、**準備**プロパティ)。|
|自動変換します。|OEM/ANSI 文字を変換するかどうかを示します。 このプロパティに設定できます**True**または**False**します。 既定値は **True**です。 このプロパティ設定されている場合**True**、マルチバイト文字の文字列から取得したまたは SQL Server に送信されるときに、SQLOLEDB が OEM/ANSI 文字変換を実行します。 このプロパティ設定されている場合**False**SQLOLEDB がマルチバイト文字の文字列データで OEM/ANSI 文字変換を実行できません。|
|Packet Size|ネットワーク パケット サイズ (バイト単位) を示します。 パケット サイズ プロパティの値は 512 ~ 32767 の間にある必要があります。 SQLOLEDB ネットワーク パケット サイズを既定値は、4096 です。|
|Application Name|クライアント アプリケーションの名前を示します。|
|[ワークステーション ID]|ワークステーションを識別する文字列。|

## <a name="command-object-usage"></a>コマンド オブジェクトの使用方法
 SQLOLEDB では、有効な構文として、ODBC、ANSI、および SQL Server に固有の TRANSACT-SQL の融合を受け取ります。 たとえば、次の SQL ステートメントでは、ODBC SQL のエスケープ シーケンスを使用して、LCASE 文字列関数を指定しています。

```sql
SELECT customerid={fn LCASE(CustomerID)} FROM Customers

```

 LCASE 関数は、大文字をすべて小文字に変換した文字列を返します。 ANSI SQL の文字列関数下は、次の SQL ステートメントは、ANSI の前に示した ODBC ステートメントと等価ですに同じ操作を実行します。

```sql
SELECT customerid=LOWER(CustomerID) FROM Customers

```

 SQLOLEDB では、コマンドのテキストとして指定するステートメントのいずれかの形式が正常に処理します。

## <a name="stored-procedures"></a>ストアド プロシージャ
 SQL Server を実行すると、SQLOLEDB コマンドを使用してプロシージャが格納されている、ときに、コマンド テキストで ODBC プロシージャ呼び出しのエスケープ シーケンスを使用します。 SQLOLEDB は、SQL Server のリモート プロシージャ コールのメカニズムを使用してコマンドの処理を最適化します。 たとえば、次の ODBC SQL ステートメントは、TRANSACT-SQL フォーム上の推奨されるコマンド テキストを示します。

## <a name="odbc-sql"></a>ODBC SQL

```vb
{call SalesByCategory('Produce', '1995')}

```

## <a name="transact-sql"></a>Transact-SQL

```sql
EXECUTE SalesByCategory 'Produce', '1995'

```

## <a name="sql-server-features"></a>SQL Server の機能
 ADO SQL server での XML を使用できます**コマンド**の入力や結果ではなく XML ストリームの形式で取得**Recordset**オブジェクト。 詳細については、次を参照してください。[コマンド入力を使用してストリーム](../../../ado/guide/data/command-streams.md)と[ストリームに結果セットを取得する](../../../ado/guide/data/retrieving-resultsets-into-streams.md)します。

### <a name="accessing-sqlvariant-data-using-mdac-27-mdac-28-or-windows-dac-60"></a>MDAC 2.7、MDAC 2.8、または Windows DAC 6.0 を使用して、sql_variant データにアクセスします。
 Microsoft SQL Server がというデータ型を**sql_variant**します。 OLE DB のような**DBTYPE_VARIANT**、 **sql_variant**データ型は、さまざまな種類のデータを格納できます。 ただしのいくつかの主な違いがある**DBTYPE_VARIANT**と**sql_variant**します。 ADO として格納されているデータも処理を**sql_variant**値の他のデータ型を処理する方法とは異なります。 次のとおりに、型の列に格納されている SQL Server データにアクセスするときに考慮すべき問題**sql_variant**します。

-   MDAC 2.7、MDAC 2.8、および Windows Data Access Components (Windows DAC) 6.0 では、OLE DB Provider for SQL Server をサポート、 **sql_variant**型。 OLE DB Provider for ODBC は提供されません。

-   **Sql_variant**型が一致しないと一致、 **DBTYPE_VARIANT**データ型。  **Sql_variant**型のサポートでサポートされていないいくつかの新しいサブタイプ**DBTYPE_VARIANT、** など**GUID**、 **ANSI** (UNICODE 以外の)文字列、および**BIGINT**します。 サブタイプを以外を使用して前に示した正しく機能します。

-   **Sql_variant**サブタイプ**数値**と一致しません、 **DBTYPE_DECIMAL**サイズ。

-   複数のデータ型の強制変換は、一致しない型になります。 たとえば、強制型変換を**sql_variant**のサブタイプで**GUID**を**DBTYPE_VARIANT**のサブタイプになります**safearray**(バイト). この種類の変換を**sql_variant**の新しいサブタイプになります**配列**(バイト単位)。

-   **レコード セット**フィールドが含まれている**sql_variant**データは、リモート処理ができる (マーシャ リング) または永続化された場合にのみ、 **sql_variant**特定のサブタイプが含まれています。 リモートしようとしてまたはサポートされていない次のデータを永続化のサブタイプには、Microsoft の永続化プロバイダー (MSPersist) から、実行時エラー (サポートされていない変換) が発生します。**VT_VARIANT**、 **VT_RECORD**、 **VT_ILLEGAL**、 **VT_UNKNOWN**、 **VT_BSTR**、および**VT_DISPATCH します。**

-   MDAC 2.7、MDAC 2.8、および Windows DAC 6.0 での SQL サーバーの OLE DB プロバイダーがという名前の動的プロパティ**ネイティブ バリアントを許可する**、名前が示すように、開発が可能にアクセスする、 **sql_variant**でネイティブ形式ではなく、 **DBTYPE_VARIANT**します。 このプロパティを設定して、 **Recordset**は、クライアント カーソル エンジンによって開かれます (**adUseClient**)、 **Recordset.Open**呼び出しは失敗します。 このプロパティが設定されている場合、 **Recordset**サーバー カーソルを開くと (**adUseServer**)、 **Recordset.Open**呼び出しが成功すると、型の列へのアクセスが、**sql_variant**エラーが発生します。

-   MDAC の 2.5 を使用するクライアント アプリケーションで**sql_variant** Microsoft SQL Server に対するクエリでデータを使用することができます。 ただしの値、 **sql_variant**データが文字列として扱われます。 このようなクライアント アプリケーションは、MDAC 2.7、MDAC 2.8、または Windows DAC 6.0 にアップグレードする必要があります。

## <a name="recordset-behavior"></a>レコード セットの動作
 SQLOLEDB では、多くのコマンドによって生成される複数の結果をサポートするために、SQL Server カーソルを使用できません。 コンシューマーは、SQL Server カーソルのサポートを必要とするレコード セットを要求している場合、結果として使用するコマンド テキストが 1 つのレコード セットよりも多くが生成する場合にエラーが発生します。

 SQLOLEDB のスクロール可能なレコード セットは、SQL Server カーソルでサポートされます。 SQL Server は、機密性の高いデータベースの他のユーザーによって加えられた変更をカーソルでの制限を適用します。 具体的には、一部のカーソル内の行を並べ替えられることはできず、SQL の ORDER BY 句を含むコマンドを使用してレコード セットを作成しようとして失敗することができます。

## <a name="dynamic-properties"></a>動的プロパティ
 Microsoft OLE DB Provider for SQL Server にいくつかの動的プロパティの挿入、**プロパティ**、開かれていないのコレクション[接続](../../../ado/reference/ado-api/connection-object-ado.md)、 [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)、および[コマンド](../../../ado/reference/ado-api/command-object-ado.md)オブジェクト。

 次の表は、ADO および OLE DB 名の各動的プロパティの相互です。 「説明です」という用語 ADO プロパティ名を参照して OLE DB プログラマーズ リファレンス これらのプロパティの詳細については、OLE DB プログラマーズ リファレンスに見つかります。 インデックスの OLE DB プロパティの名前を検索または参照してください[付録 c:OLE DB プロパティ](https://msdn.microsoft.com/deded3ff-f508-4e1b-b2b1-fd9afd3bd292)します。

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
|Connect Timeout|DBPROP_INIT_TIMEOUT|
|現在のカタログ|DBPROP_CURRENTCATALOG|
|[データ ソース]|DBPROP_INIT_DATASOURCE|
|Data Source Name|DBPROP_DATASOURCENAME|
|データ ソース オブジェクト スレッド モデル|DBPROP_DSOTHREADMODEL|
|DBMS 名|DBPROP_DBMSNAME|
|DBMS バージョン|DBPROP_DBMSVER|
|Extended Properties|DBPROP_INIT_PROVIDERSTRING|
|GROUP BY をサポート|DBPROP_GROUPBY|
|異なるテーブルのサポート|DBPROP_HETEROGENEOUSTABLES|
|識別子の大文字と小文字の区別|DBPROP_IDENTIFIERCASE|
|Initial Catalog|DBPROP_INIT_CATALOG|
|分離レベル|DBPROP_SUPPORTEDTXNISOLEVELS|
|分離の保持|DBPROP_SUPPORTEDTXNISORETAIN|
|[Locale Identifier]|DBPROP_INIT_LCID|
|インデックスの最大サイズ|DBPROP_MAXINDEXSIZE|
|行の最大サイズ|DBPROP_MAXROWSIZE|
|最大行サイズには、BLOB が含まれています。|DBPROP_MAXROWSIZEINCLUDESBLOB|
|SELECT の最大のテーブル|DBPROP_MAXTABLESINSELECT|
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
|Persist Security Info|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|
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
|ブロッキング ストレージ オブジェクト|DBPROP_BLOCKINGSTORAGEOBJECTS|
|ブックマークの種類|DBPROP_BOOKMARKTYPE|
|ブックマークを設定|DBPROP_IROWSETLOCATE|
|挿入行を変更します。|DBPROP_CHANGEINSERTEDROWS|
|列の特権|DBPROP_COLUMNRESTRICT|
|列セットの通知|DBPROP_NOTIFYCOLUMNSET|
|コマンド タイムアウト|DBPROP_COMMANDTIMEOUT|
|列を遅延します。|DBPROP_DEFERRED|
|ストレージ オブジェクトの更新を遅延|DBPROP_DELAYSTORAGEOBJECTS|
|後方のフェッチします。|DBPROP_CANFETCHBACKWARDS|
|行を保持します。|DBPROP_CANHOLDROWS|
|IAccessor|DBPROP_IAccessor|
|IColumnsInfo|DBPROP_IColumnsInfo|
|IColumnsRowset|DBPROP_IColumnsRowset|
|IConnectionPointContainer|DBPROP_IConnectionPointContainer|
|IConvertType|DBPROP_IConvertType|
|固定行|DBPROP_IMMOBILEROWS|
|IRowset|DBPROP_IRowset|
|IRowsetChange|DBPROP_IRowsetChange|
|IRowsetIdentity|DBPROP_IRowsetIdentity|
|IRowsetInfo|DBPROP_IRowsetInfo|
|IRowsetLocate|DBPROP_IRowsestLocate|
|IRowsetResynch||
|IRowsetScroll|DBPROP_IRowsetScroll|
|IRowsetUpdate|DBPROP_IRowsetUpdate|
|ISequentialStream|DBPROP_ISequentialStream|
|ISupportErrorInfo|DBPROP_ISupportErrorInfo|
|リテラル ブックマーク|DBPROP_LITERALBOOKMARKS|
|リテラル行の Id|DBPROP_LITERALIDENTITY|
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
|行セットのフェッチ位置の変更通知|DBPROP_NOTIFYROWSETFETCHPOSISIONCHANGE|
|行セットの解放通知|DBPROP_NOTIFYROWSETRELEASE|
|逆にスクロールします。|DBPROP_CANSCROLLBACKWARDS|
|サーバー カーソル|DBPROP_SERVERCURSOR|
|削除されたブックマークをスキップ|DBPROP_BOOKMARKSKIPPED|
|厳密な行の Id|DBPROP_STRONGITDENTITY|
|一意の行|DBPROP_UNIQUEROWS|
|更新機能|DBPROP_UPDATABILITY|
|ブックマークを使用します。|DBPROP_BOOKMARKS|

## <a name="command-dynamic-properties"></a>コマンドの動的プロパティ
 次のプロパティに追加されます、**プロパティ**のコレクション、**コマンド**オブジェクト。

|ADO のプロパティ名|OLE DB プロパティの名前|
|-----------------------|--------------------------|
|アクセスの順序|DBPROP_ACCESSORDER|
|基本パス|SSPROP_STREAM_BASEPATH|
|ブロッキング ストレージ オブジェクト|DBPROP_BLOCKINGSTORAGEOBJECTS|
|ブックマークの種類|DBPROP_BOOKMARKTYPE|
|ブックマークを設定|DBPROP_IROWSETLOCATE|
|挿入行を変更します。|DBPROP_CHANGEINSERTEDROWS|
|列の特権|DBPROP_COLUMNRESTRICT|
|列セットの通知|DBPROP_NOTIFYCOLUMNSET|
|コンテンツの種類|SSPROP_STREAM_CONTENTTYPE|
|カーソル自動のフェッチ|SSPROP_CURSORAUTOFETCH|
|列を遅延します。|DBPROP_DEFERRED|
|準備コマンドの遅延送信|SSPROP_DEFERPREPARE|
|ストレージ オブジェクトの更新を遅延|DBPROP_DELAYSTORAGEOBJECTS|
|後方のフェッチします。|DBPROP_CANFETCHBACKWARDS|
|行を保持します。|DBPROP_CANHOLDROWS|
|IAccessor|DBPROP_IAccessor|
|IColumnsInfo|DBPROP_IColumnsInfo|
|IColumnsRowset|DBPROP_IColumnsRowset|
|IConnectionPointContainer|DBPROP_IConnectionPointContainer|
|IConvertType|DBPROP_IConvertType|
|固定行|DBPROP_IMMOBILEROWS|
|IRowset|DBPROP_IRowset|
|IRowsetChange|DBPROP_IRowsetChange|
|IRowsetIdentity|DBPROP_IRowsetIdentity|
|IRowsetInfo|DBPROP_IRowsetInfo|
|IRowsetLocate|DBPROP_IRowsetLocate|
|IRowsetResynch|DBPROP_IRowsetResynch|
|IRowsetScroll|DBPROP_IRowsetScroll|
|IRowsetUpdate|DBPROP_IRowsetUpdate|
|ISequentialStream|DBPROP_ISequentialStream|
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
|出力エンコードのプロパティ|DBPROP_OUTPUTENCODING|
|Output Stream プロパティ|DBPROP_OUTPUTSTREAM|
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
|サーバー カーソル|DBPROP_SERVERCURSOR|
|サーバーのデータを挿入|DBPROP_SERVERDATAONINSERT|
|削除されたブックマークをスキップ|DBPROP_BOOKMARKSKIP|
|厳密な行の Id|DBPROP_STRONGIDENTITY|
|更新機能|DBPROP_UPDATABILITY|
|ブックマークを使用します。|DBPROP_BOOKMARKS|
|XML のルート|SSPROP_STREAM_XMLROOT|
|XSL (XSL)|SSPROP_STREAM_XSL|

 特定の実装の詳細と、Microsoft SQL Server OLE DB プロバイダーの機能については、次を参照してください。、 [SQL Server プロバイダー](https://msdn.microsoft.com/adf1d6c4-5930-444a-9248-ff1979729635)します。

## <a name="see-also"></a>参照
 [ConnectionString プロパティ (ADO)](../../../ado/reference/ado-api/connectionstring-property-ado.md) [プロバイダー プロパティ (ADO)](../../../ado/reference/ado-api/provider-property-ado.md) [レコード セット オブジェクト (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
