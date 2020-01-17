---
title: ADO Dynamic プロパティ インデックス |Microsoft Docs
ms.prod: sql
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- dynamic properties [ADO], index
ms.assetid: 80d389dd-46ef-459f-b0d4-6f712fc4f32d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9eb88905f56abf9c1c702f5fd73cbe61a1bcde3d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67921083"
---
# <a name="ado-dynamic-property-index"></a>ADO Dynamic プロパティ インデックス
データ プロバイダー、サービス プロバイダー、およびサービス コンポーネントが動的プロパティを追加、**プロパティ**、開かれていないのコレクション[接続](../../../ado/reference/ado-api/connection-object-ado.md)と[Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)オブジェクト。 指定されたプロバイダーは、これらのオブジェクトが開かれたときに、追加のプロパティを挿入も可能性があります。 これらのプロパティのいくつか記載されている、 [ADO の動的プロパティ](../../../ado/reference/ado-api/ado-dynamic-properties.md)セクション。 特定のプロバイダーの詳細に表示される、[付録 a:プロバイダー](../../../ado/guide/appendixes/appendix-a-providers.md)セクション。  
  
 次の表は、各標準 OLE DB プロバイダー動的プロパティ用の ADO および OLE DB 名の cross-indexes です。 プロバイダーは、ここで表示されているより多くのプロパティを追加できます。 プロバイダー固有の動的プロパティに関する特定の情報をプロバイダーのドキュメントを参照してください。  
  
 「説明です」という用語 ADO プロパティ名を参照して OLE DB プログラマーズ リファレンス これらの標準プロパティの詳細については、検索または参照内のインデックス、 [OLE DB のドキュメント](https://msdn.microsoft.com/library/windows/desktop/ms722784.aspx)の OLE DB プロパティの名前をします。  
  
## <a name="connection-dynamic-properties"></a>接続の動的プロパティ  
  
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
|Location|DBPROP_INIT_LOCATION|  
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
|OLE DB サービス|DBPROP_INIT_OLEDBSERVICES|  
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
 なお、**動的プロパティ**の**レコード セット**オブジェクト (使用できなくなります) とスコープ外に移動して、**レコード セット**が閉じられました。  
  
|ADO のプロパティ名|OLE DB プロパティの名前|  
|-----------------------|--------------------------|  
|IAccessor|DBPROP_IACCESSOR|  
|IChapteredRowset||  
|IColumnsInfo|DBPROP_ICOLUMNSINFO|  
|IColumnsRowset|DBPROP_ICOLUMNSROWSET|  
|IConnectionPointContainer|DBPROP_ICONNECTIONPOINTCONTAINER|  
|IConvertType||  
|ILockBytes|DBPROP_ILOCKBYTES|  
|IRowset|DBPROP_IROWSET|  
|IDBAsynchStatus|DBPROP_IDBASYNCHSTATUS|  
|IParentRowset||  
|IRowsetChange|DBPROP_IROWSETCHANGE|  
|IRowsetExactScroll||  
|IRowsetFind|DBPROP_IROWSETFIND|  
|IRowsetIdentity|DBPROP_IROWSETIDENTITY|  
|IRowsetInfo|DBPROP_IROWSETINFO|  
|IRowsetLocate|DBPROP_IROWSETLOCATE|  
|IRowsetRefresh|DBPROP_IROWSETREFRESH|  
|IRowsetResynch||  
|IRowsetScroll|DBPROP_IROWSETSCROLL|  
|IRowsetUpdate|DBPROP_IROWSETUPDATE|  
|IRowsetView|DBPROP_IROWSETVIEW|  
|IRowsetIndex|DBPROP_IROWSETINDEX|  
|ISequentialStream|DBPROP_ISEQUENTIALSTREAM|  
|IStorage|DBPROP_ISTORAGE|  
|IStream|DBPROP_ISTREAM|  
|ISupportErrorInfo|DBPROP_ISUPPORTERRORINFO|  
|アクセスの順序|DBPROP_ACCESSORDER|  
|追加専用の行セット|DBPROP_APPENDONLY|  
|非同期の行セットの処理|DBPROP_ROWSET_ASYNCH|  
|自動再計算|DBPROP_ADC_AUTORECALC|  
|バック グラウンド フェッチ サイズ|DBPROP_ASYNCHFETCHSIZE|  
|バックグラウンド スレッド優先順位|DBPROP_ASYNCHTHREADPRIORITY|  
|バッチ サイズ|DBPROP_ADC_BATCHSIZE|  
|ブロッキング ストレージ オブジェクト|DBPROP_BLOCKINGSTORAGEOBJECTS|  
|ブックマークの種類|DBPROP_BOOKMARKTYPE|  
|ブックマークを設定|DBPROP_IROWSETLOCATE|  
|ブックマークの順序指定|DBPROP_ORDEREDBOOKMARKS|  
|子の行をキャッシュします。|DBPROP_ADC_CACHECHILDROWS|  
|キャッシュ列の遅延|DBPROP_CACHEDEFERRED|  
|挿入行を変更します。|DBPROP_CHANGEINSERTEDROWS|  
|列の特権|DBPROP_COLUMNRESTRICT|  
|列セットの通知|DBPROP_NOTIFYCOLUMNSET|  
|書き込み可能な列|DBPROP_MAYWRITECOLUMN|  
|コマンド タイムアウト|DBPROP_COMMANDTIMEOUT|  
|カーソル エンジンのバージョン|DBPROP_ADC_CEVER|  
|列を遅延します。|DBPROP_DEFERRED|  
|ストレージ オブジェクトの更新を遅延|DBPROP_DELAYSTORAGEOBJECTS|  
|後方のフェッチします。|DBPROP_CANFETCHBACKWARDS|  
|操作をフィルター処理します。|DBPROP_FILTERCOMPAREOPS|  
|検索操作|DBPROP_FINDCOMPAREOPS|  
|非表示の列 (数)|DBPROP_HIDDENCOLUMNS|  
|行を保持します。|DBPROP_CANHOLDROWS|  
|固定行|DBPROP_IMMOBILEROWS|  
|最初のフェッチ サイズ|DBPROP_ASYNCHPREFETCHSIZE|  
|リテラル ブックマーク|DBPROP_LITERALBOOKMARKS|  
|リテラル行の Id|DBPROP_LITERALIDENTITY|  
|状態の変更を管理します。|DBPROP_ADC_MAINTAINCHANGESTATUS|  
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
|Private1||  
|クイック再起動|DBPROP_QUICKRESTART|  
|再入イベント|DBPROP_REENTRANTEVENTS|  
|削除された行を削除します。|DBPROP_REMOVEDELETED|  
|複数の変更を報告します。|DBPROP_REPORTMULTIPLECHANGES|  
|名前を変更します。|DBPROP_ADC_RESHAPENAME|  
|再同期コマンド|DBPROP_ADC_CUSTOMRESYNCH|  
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
|削除されたブックマークをスキップ|DBPROP_BOOKMARKSKIPPED|  
|厳密な行の Id|DBPROP_STRONGIDENTITY|  
|一意のカタログ|DBPROP_ADC_UNIQUECATALOG|  
|一意の行|DBPROP_UNIQUEROWS|  
|一意のスキーマ|DBPROP_ADC_UNIQUESCHEMA|  
|Unique Table|DBPROP_ADC_UNIQUETABLE|  
|更新機能|DBPROP_UPDATABILITY|  
|更新基準|DBPROP_ADC_UPDATECRITERIA|  
|更新プログラムの再同期|DBPROP_ADC_UPDATERESYNC|  
|ブックマークを使用します。|DBPROP_BOOKMARKS|
