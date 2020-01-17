---
title: Microsoft OLE DB Provider for ODBC |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- OLE DB provider for ODBC [ADO]
- providers [ADO], OLE DB provider for ODBC
ms.assetid: 2dc0372d-e74d-4d0f-9c8c-04e5a168c148
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 25db7fdb20ceb2dd24f819e1db7077d40f7e7e3f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67926636"
---
# <a name="microsoft-ole-db-provider-for-odbc-overview"></a>Microsoft OLE DB Provider for ODBC の概要
ADO または RDS プログラマでは、理想的な世界はいずれかを指定すべてのデータ ソースが OLE DB インターフェイスを公開します。 ADO は、データ ソースに直接呼び出すことができるようにします。 ますます多くのデータベース ベンダーは、OLE DB インターフェイスを実装するは、一部のデータ ソースのこの方法はまだ公開されません。 ただし、今日のほとんどの DBMS システムは、ODBC を通じてアクセスできます。

 ODBC ドライバーでは、Oracle などの Microsoft 以外のデータベース製品だけでなく、Microsoft SQL Server、Microsoft Access (Jet データベース エンジン) および Microsoft の FoxPro を含む、現在使用しているすべて主要な DBMS 使用できます。

 ただし、により、Microsoft ODBC プロバイダーを使用すると、任意の ODBC データ ソースに接続するための ADO します。 プロバイダーは、フリー スレッドし、Unicode に対応します。

 プロバイダーは、さまざまな種類のトランザクションのサポートを提供するさまざまな DBMS エンジンのトランザクションをサポートします。 たとえば、Microsoft Access では、5 レベルまで入れ子になったトランザクションをサポートしています。

 これは、ADO の既定のプロバイダーであり、すべてのプロバイダーに依存する ADO プロパティとメソッドがサポートされています。

## <a name="connection-string-parameters"></a>接続文字列パラメーター
 このプロバイダーに接続するには、設定、**プロバイダー =** の引数、 [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)プロパティ。

```
MSDASQL
```

 読み取り、[Provider](../../../ado/reference/ado-api/provider-property-ado.md)プロパティは同様に、この文字列を返します。

## <a name="typical-connection-string"></a>一般的な接続文字列
 このプロバイダーの一般的な接続文字列は次のとおりです。

```
"Provider=MSDASQL;DSN=dsnName;UID=MyUserID;PWD=MyPassword;"
```

 文字列は、これらのキーワードで構成されます。

|Keyword|説明|
|-------------|-----------------|
|**Provider**|OLE DB provider for ODBC を指定します。|
|**DSN**|データ ソース名を指定します。|
|**UID**|ユーザー名を指定します。|
|**PWD**|ユーザーのパスワードを指定します。|
|**URL**|ファイルまたは Web フォルダーに発行されるディレクトリの URL を指定します。|

 省略した場合、ADO の既定のプロバイダーは、このため、**プロバイダー =** ADO 接続文字列のパラメーターはこのプロバイダーへの接続を確立しようとしています。

> [!NOTE]
>  Windows 認証をサポートするデータ ソース プロバイダーに接続するかどうかは、する必要がありますを指定する**Trusted_Connection = yes**または**Integrated Security = SSPI**ユーザー ID とパスワードの代わりに接続文字列の情報です。

 プロバイダーは、ADO で定義されているだけでなく特定の接続パラメーターをサポートしていません。 ただし、プロバイダーは、ODBC ドライバー マネージャーを ADO 非接続パラメーターを渡します。

 省略することができますので、**プロバイダー**パラメーター、ADO 接続文字列を同じデータ ソース用の ODBC 接続文字列と同じであるため作成できます。 同じパラメーター名を使用して (**ドライバー =** 、**データベース =** 、 **DSN =** など)、値とすると構文は、ODBC 接続文字列を作成するとき。 定義済みのデータ ソース名 (DSN) または FileDSN の有無を接続することができます。

## <a name="syntax-with-a-dsn-or-filedsn"></a>DSN、FileDSN の構文:

```
"[Provider=MSDASQL;] { DSN=name | FileDSN=filename } ;
[DATABASE=database;] UID=user; PWD=password"
```

## <a name="syntax-without-a-dsn-dsn-less-connection"></a>DSN (dsn-less connection) を使用しない構文:

```
"[Provider=MSDASQL;] DRIVER=driver; SERVER=server;
DATABASE=database; UID=MyUserID; PWD=MyPassword"
```

## <a name="remarks"></a>コメント
 使用する場合、 **DSN**または**FileDSN**、Windows コントロール パネルの ODBC データ ソース アドミニストレーターを定義する必要があります。 Microsoft Windows 2000 では、odbc データ ソース アドミニストレーターは管理ツールの下にあります。 Windows の以前のバージョンでは、という名前の ODBC アドミニストレーター アイコン**32 ビット ODBC**単**ODBC**します。

 設定する代わりに、 **DSN**、ODBC ドライバーを指定することができます (**ドライバー =** )、"SQL Server;"など、サーバー名 (**SERVER =** ); とデータベース名 (**データベース =** )。

 ユーザー アカウント名を指定することもできます (**UID =** )、およびユーザー アカウントのパスワード (**PWD =** ) ODBC に固有のパラメーターまたは標準の ADO 定義*ユーザー*と*パスワード*パラメーター。

 **DSN**指定できますの定義は既にデータベースを指定して、 *、* *データベース*パラメーターに加え、 **DSN**接続するには別のデータベース。 常に含めることをお勧め *、* *データベース*パラメーターを使用する場合、 **DSN**します。 これは、確認した後、別のユーザーは、既定のデータベース パラメーターを変更する場合は、適切なデータベースに接続することにより、 **DSN**定義します。

## <a name="provider-specific-connection-properties"></a>プロバイダー固有の接続のプロパティ
 OLE DB provider for ODBC をいくつかのプロパティの追加、[プロパティ](../../../ado/reference/ado-api/properties-collection-ado.md)のコレクション、**接続**オブジェクト。 次の表は、かっこ内の対応する OLE DB プロパティ名でこれらのプロパティを一覧表示します。

|プロパティ名|説明|
|-------------------|-----------------|
|アクセス可能な手順 (KAGPROP_ACCESSIBLEPROCEDURES)|ユーザーがストアド プロシージャへのアクセスを持つかどうかを示します。|
|アクセス可能なテーブル (KAGPROP_ACCESSIBLETABLES)|ユーザーがデータベースのテーブルに対して SELECT ステートメントを実行する権限を持つかどうかを示します。|
|アクティブなステートメント (KAGPROP_ACTIVESTATEMENTS)|接続で ODBC ドライバーをサポートできるハンドルの数を示します。|
|ドライバー名 (KAGPROP_DRIVERNAME)|ODBC ドライバーのファイル名を示します。|
|ドライバーの ODBC バージョン (KAGPROP_DRIVERODBCVER)|このドライバーをサポートする ODBC のバージョンを示します。|
|ファイルの使用状況 (KAGPROP_FILEUSAGE)|ドライバーが、データ ソース内のファイルを処理する方法を示しますテーブル、またはカタログとして。|
|Like エスケープ句 (KAGPROP_LIKEESCAPECLAUSE)|ドライバーがパーセント記号 (%) の定義とエスケープ文字の使用をサポートするかどうかを示します下線文字 (_) を WHERE 句の LIKE 述語にします。|
|(KAGPROP_MAXCOLUMNSINGROUPBY) によるグループ内の最大列|SELECT ステートメントの GROUP BY 句を記載されている列の最大数を示します。|
|最大の列インデックス (KAGPROP_MAXCOLUMNSININDEX)|インデックスに含めることができる列の最大数を示します。|
|Order By (KAGPROP_MAXCOLUMNSINORDERBY) で最大の列|SELECT ステートメントの ORDER BY 句を記載されている列の最大数を示します。|
|最大の列で (KAGPROP_MAXCOLUMNSINSELECT) を選択します。|SELECT ステートメントの SELECT 部分を記載されている列の最大数を示します。|
|テーブル (KAGPROP_MAXCOLUMNSINTABLE) の最大列|テーブルで許可されている列の最大数を示します。|
|数値関数 (KAGPROP_NUMERICFUNCTIONS)|数値関数が ODBC ドライバーでサポートされていることを示します。 関数名と、関連するこのビットマスクで使用される値の一覧については、次を参照してください[付録 e:。スカラー関数](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md)ODBC のドキュメントにします。|
|外部結合機能 (KAGPROP_OJCAPABILITY)|プロバイダーでサポートされている外部結合の種類を示します。|
|外部結合 (KAGPROP_OUTERJOINS)|プロバイダーが外部結合をサポートしているかどうかを示します。|
|特殊文字 (KAGPROP_SPECIALCHARACTERS)|ODBC ドライバーの特別な意味を持つ文字を示します。|
|ストアド プロシージャ (KAGPROP_PROCEDURES)|ストアド プロシージャは、この ODBC ドライバーで使用できるかどうかを示します。|
|文字列関数 (KAGPROP_STRINGFUNCTIONS)|文字列関数が ODBC ドライバーでサポートされていることを示します。 関数名と、関連するこのビットマスクで使用される値の一覧については、次を参照してください[付録 e:。スカラー関数](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md)ODBC のドキュメントにします。|
|システム関数 (KAGPROP_SYSTEMFUNCTIONS)|ODBC ドライバーがサポートするシステム関数を示します。 関数名と、関連するこのビットマスクで使用される値の一覧については、次を参照してください[付録 e:。スカラー関数](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md)ODBC のドキュメントにします。|
|日付/時刻関数 (KAGPROP_TIMEDATEFUNCTIONS)|ODBC ドライバーでどの日付と時刻の関数がサポートされていることを示します。 関数名と、関連するこのビットマスクで使用される値の一覧については、次を参照してください[付録 e:。スカラー関数](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md)ODBC のドキュメントにします。|
|SQL 文法のサポート (KAGPROP_ODBCSQLCONFORMANCE)|ODBC ドライバーがサポートする SQL 文法を示します。|

## <a name="provider-specific-recordset-and-command-properties"></a>プロバイダー固有のレコード セットとコマンドのプロパティ
 OLE DB provider for ODBC をいくつかのプロパティの追加、**プロパティ**のコレクション、**レコード セット**と**コマンド**オブジェクト。 次の表は、かっこ内の対応する OLE DB プロパティ名でこれらのプロパティを一覧表示します。

|プロパティ名|説明|
|-------------------|-----------------|
|クエリ ベースの更新/削除/挿入 (KAGPROP_QUERYBASEDUPDATES)|更新、削除、および挿入を SQL クエリを使用して実行できるかどうかを示します。|
|ODBC の同時実行の種類 (KAGPROP_CONCURRENCY)|データ ソースから同時に同じデータにアクセスしようとしています。 2 人のユーザーによって引き起こされる潜在的な問題を軽減するために使用する方法を示します。|
|順方向専用カーソル (KAGPROP_BLOBSONFOCURSOR) での BLOB のユーザー補助|示すかどうか BLOB**フィールド**順方向専用カーソルを使用する場合にアクセスできます。|
|QBU WHERE 句 (KAGPROP_INCLUDENONEXACT) には、使用できます、SQL_DOUBLE、および SQL_REAL|QBU WHERE 句で使用できます、SQL_DOUBLE、SQL_REAL の値を含めることができるかどうかを示します。|
|挿入 (KAGPROP_POSITIONONNEWROW) 後の最後の行の位置|テーブルに新しいレコードが挿入された、テーブルの最後の行があることを示します、現在の行を取得します。|
|IRowsetChangeExtInfo (KAGPROP_IROWSETCHANGEEXTINFO)|示すかどうか、 **IRowsetChange**インターフェイスが拡張情報のサポートを提供します。|
|ODBC カーソルの種類 (KAGPROP_CURSOR)|使用するカーソルの種類を示す、 **Recordset**します。|
|マーシャ リングできる行セットを生成 (KAGPROP_MARSHALLABLE)|ODBC ドライバーがマーシャ リングできるレコード セットを生成することを示します|

## <a name="command-text"></a>コマンド テキスト
 使用する方法、[コマンド](../../../ado/reference/ado-api/command-object-ado.md)オブジェクトは、データ ソースに大きく左右し、受け付けることがクエリまたはコマンドのステートメントの種類。

 ODBC では、ストアド プロシージャの呼び出しを特定の構文を提供します。 [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)のプロパティを**コマンド**オブジェクト、 *CommandText*への引数、 **Execute**メソッドを[接続](../../../ado/reference/ado-api/connection-object-ado.md)オブジェクト、または*ソース*への引数、**オープン**メソッドを[レコード セット](../../../ado/reference/ado-api/recordset-object-ado.md)オブジェクト、この構文を使用して文字列に渡されます。

```
"{ [ ? = ] call procedure [ ( ? [, ? [ , ... ]] ) ] }"
```

 各**でしょうか。** 内のオブジェクトの参照、[パラメーター](../../../ado/reference/ado-api/parameters-collection-ado.md)コレクション。 最初の**でしょうか。** 参照**パラメーター**(0)、[次へ]**でしょうか。** 参照**パラメーター**(1)、という具合です。

 パラメーターの参照はオプションであり、ストアド プロシージャの構造に依存します。 パラメーターを定義していないストアド プロシージャを呼び出す場合は、次のような文字列になります。

```
"{ call procedure }"
```

 2 つのクエリ パラメーターがある場合、文字列は、次のようになります。

```
"{ call procedure ( ?, ? ) }"
```

 ストアド プロシージャは、値を返さない場合、戻り値は、別のパラメーターとして扱われます。 クエリ パラメーターはありませんが、戻り値が場合、文字列は、次のようになります。

```
"{ ? = call procedure }"
```

 最後に、戻り値があり、2 つのクエリ パラメーターの場合、文字列は、次のようになります。

```
"{ ? = call procedure ( ?, ? ) }"
```

## <a name="recordset-behavior"></a>レコード セットの動作
 次の表は、標準の ADO メソッドとプロパティで使用できる、 **Recordset**オブジェクトは、このプロバイダーで開かれました。

 詳細については**Recordset**実行、プロバイダーの構成の動作、[Supports](../../../ado/reference/ado-api/supports-method.md)メソッドを列挙し、**Properties**のコレクション、**Recordset**をプロバイダーに固有の動的なプロパティが存在するかどうかを判断します。

 標準の ADO の可用性**Recordset**プロパティ。

|プロパティ|ForwardOnly|動的|Keyset|スタティック|
|--------------|-----------------|-------------|------------|------------|
|[AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md)|使用できません。|使用できません。|読み取り/書き込み|読み取り/書き込み|
|[AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md)|使用できません。|使用できません。|読み取り/書き込み|読み取り/書き込み|
|[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)|読み取り/書き込み|読み取り/書き込み|読み取り/書き込み|読み取り/書き込み|
|[BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)|読み取り専用|読み取り専用|読み取り専用|読み取り専用|
|[Bookmark](../../../ado/reference/ado-api/bookmark-property-ado.md)|使用できません。|使用できません。|読み取り/書き込み|読み取り/書き込み|
|[CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md)|読み取り/書き込み|読み取り/書き込み|読み取り/書き込み|読み取り/書き込み|
|[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)|読み取り/書き込み|読み取り/書き込み|読み取り/書き込み|読み取り/書き込み|
|[CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md)|読み取り/書き込み|読み取り/書き込み|読み取り/書き込み|読み取り/書き込み|
|[EditMode](../../../ado/reference/ado-api/editmode-property.md)|読み取り専用|読み取り専用|読み取り専用|読み取り専用|
|[Assert](../../../ado/reference/ado-api/filter-property.md)|読み取り/書き込み|読み取り/書き込み|読み取り/書き込み|読み取り/書き込み|
|[LockType](../../../ado/reference/ado-api/locktype-property-ado.md)|読み取り/書き込み|読み取り/書き込み|読み取り/書き込み|読み取り/書き込み|
|[MarshalOptions](../../../ado/reference/ado-api/marshaloptions-property-ado.md)|読み取り/書き込み|読み取り/書き込み|読み取り/書き込み|読み取り/書き込み|
|[MaxRecords](../../../ado/reference/ado-api/maxrecords-property-ado.md)|読み取り/書き込み|読み取り/書き込み|読み取り/書き込み|読み取り/書き込み|
|[PageCount](../../../ado/reference/ado-api/pagecount-property-ado.md)|読み取り/書き込み|使用できません。|読み取り専用|読み取り専用|
|[PageSize](../../../ado/reference/ado-api/pagesize-property-ado.md)|読み取り/書き込み|読み取り/書き込み|読み取り/書き込み|読み取り/書き込み|
|[RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md)|読み取り/書き込み|使用できません。|読み取り専用|読み取り専用|
|[Source](../../../ado/reference/ado-api/source-property-ado-recordset.md)|読み取り/書き込み|読み取り/書き込み|読み取り/書き込み|読み取り/書き込み|
|[State](../../../ado/reference/ado-api/state-property-ado.md)|読み取り専用|読み取り専用|読み取り専用|読み取り専用|
|[Status](../../../ado/reference/ado-api/status-property-ado-recordset.md)|読み取り専用|読み取り専用|読み取り専用|読み取り専用|

 [AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md)と[AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md) ODBC 用の Microsoft OLE DB Provider のバージョン 1.0 で ADO を使用する場合のプロパティは書き込み専用です。

 標準の ADO の可用性**Recordset**メソッド。

|メソッド|ForwardOnly|動的|Keyset|スタティック|
|------------|-----------------|-------------|------------|------------|
|[AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)|[はい]|[はい]|[はい]|はい|
|[Cancel](../../../ado/reference/ado-api/cancel-method-ado.md)|はい|[はい]|[はい]|[はい]|
|[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)|[はい]|[はい]|[はい]|はい|
|[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)|はい|[はい]|[はい]|はい|
|[Clone](../../../ado/reference/ado-api/clone-method-ado.md)|いいえ|いいえ|はい|はい|
|[Close](../../../ado/reference/ado-api/close-method-ado.md)|はい|[はい]|[はい]|はい|
|[削除](../../../ado/reference/ado-api/delete-method-ado-recordset.md)|はい|[はい]|[はい]|[はい]|
|[GetRows](../../../ado/reference/ado-api/getrows-method-ado.md)|はい|[はい]|[はい]|[はい]|
|[Move](../../../ado/reference/ado-api/move-method-ado.md)|はい|[はい]|[はい]|はい|
|[MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|[はい]|[はい]|[はい]|はい|
|[MoveLast](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|いいえ|はい|[はい]|はい|
|[MoveNext](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|はい|[はい]|[はい]|はい|
|[MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|いいえ|はい|[はい]|[はい]|
|[NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)*|はい|[はい]|[はい]|はい|
|[Open](../../../ado/reference/ado-api/open-method-ado-recordset.md)|[はい]|[はい]|[はい]|[はい]|
|[Requery](../../../ado/reference/ado-api/requery-method.md)|はい|[はい]|[はい]|はい|
|[Resync](../../../ado/reference/ado-api/resync-method.md)|いいえ|いいえ|はい|はい|
|[Supports](../../../ado/reference/ado-api/supports-method.md)|はい|[はい]|[はい]|はい|
|[Update](../../../ado/reference/ado-api/update-method.md)|はい|[はい]|[はい]|はい|
|[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)|はい|[はい]|[はい]|はい|

 \* Microsoft Access データベースはサポートされていません。

## <a name="dynamic-properties"></a>動的プロパティ
 Microsoft OLE DB Provider for ODBC にいくつかの動的プロパティの挿入、**プロパティ**、開かれていないのコレクション[接続](../../../ado/reference/ado-api/connection-object-ado.md)、[レコード セット](../../../ado/reference/ado-api/recordset-object-ado.md)、および[コマンド](../../../ado/reference/ado-api/command-object-ado.md)オブジェクト。

 次の表は、ADO および OLE DB 名の各動的プロパティの相互です。 「説明です」という用語を ADO プロパティ名を参照して OLE DB プログラマーズ リファレンス これらのプロパティの詳細については、OLE DB プログラマーズ リファレンスに見つかります。 インデックスの OLE DB プロパティの名前を検索または参照してください[付録 c:OLE DB プロパティ](https://msdn.microsoft.com/deded3ff-f508-4e1b-b2b1-fd9afd3bd292)します。

## <a name="connection-dynamic-properties"></a>接続の動的プロパティ
 次のプロパティに追加されます、**接続**オブジェクトの**プロパティ**コレクション。

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
|Password|DBPROP_AUTH_PASSWORD|
|Ref アクセサーを使って渡す|DBPROP_BYREFACCESSORS|
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
 次のプロパティに追加されます、 **Recordset**オブジェクトの**プロパティ**コレクション。

|ADO のプロパティ名|OLE DB プロパティの名前|
|-----------------------|--------------------------|
|アクセスの順序|DBPROP_ACCESSORDER|
|ブロッキング ストレージ オブジェクト|DBPROP_BLOCKINGSTORAGEOBJECTS|
|ブックマークの種類|DBPROP_BOOKMARKTYPE|
|ブックマークを設定|DBPROP_IROWSETLOCATE|
|挿入行を変更します。|DBPROP_CHANGEINSERTEDROWS|
|列の特権|DBPROP_COLUMNRESTRICT|
|列セットの通知|DBPROP_NOTIFYCOLUMNSET|
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
|IRowsetResynch||
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
|一意の行|DBPROP_UNIQUEROWS|
|更新機能|DBPROP_UPDATABILITY|
|ブックマークを使用します。|DBPROP_BOOKMARKS|

## <a name="command-dynamic-properties"></a>コマンドの動的プロパティ
 次のプロパティに追加されます、**コマンド**オブジェクトの**プロパティ**コレクション。

|ADO のプロパティ名|OLE DB プロパティの名前|
|-----------------------|--------------------------|
|アクセスの順序|DBPROP_ACCESSORDER|
|ブロッキング ストレージ オブジェクト|DBPROP_BLOCKINGSTORAGEOBJECTS|
|ブックマークの種類|DBPROP_BOOKMARKTYPE|
|ブックマークを設定|DBPROP_IROWSETLOCATE|
|挿入行を変更します。|DBPROP_CHANGEINSERTEDROWS|
|列の特権|DBPROP_COLUMNRESTRICT|
|列セットの通知|DBPROP_NOTIFYCOLUMNSET|
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
|IRowsetResynch||
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
|削除されたブックマークをスキップ|DBPROP_BOOKMARKSKIP|
|厳密な行の Id|DBPROP_STRONGIDENTITY|
|更新機能|DBPROP_UPDATABILITY|
|ブックマークを使用します。|DBPROP_BOOKMARKS|

 詳細については、特定の実装と機能について Microsoft OLE DB Provider for ODBC は、次を参照してください。、 [OLE DB プログラマーズ リファレンス](https://msdn.microsoft.com/3c5e2dd5-35e5-4a93-ac3a-3818bb43bbf8)か msdn データ アクセスおよびストレージ デベロッパー センター Web サイトを参照してください。

## <a name="see-also"></a>関連項目
 [コマンド オブジェクト (ADO) を](../../../ado/reference/ado-api/command-object-ado.md) [CommandText プロパティ (ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md) [接続オブジェクト (ADO)](../../../ado/reference/ado-api/connection-object-ado.md) [ConnectionString プロパティ (ADO)](../../../ado/reference/ado-api/connectionstring-property-ado.md) [実行メソッド (ADO Command)](../../../ado/reference/ado-api/execute-method-ado-command.md) [Open メソッド (ADO Recordset)](../../../ado/reference/ado-api/open-method-ado-recordset.md) [Parameters コレクション (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md) [プロパティのコレクション (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md) [プロバイダー プロパティ (ADO)](../../../ado/reference/ado-api/provider-property-ado.md) [レコード セット オブジェクト (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md) [メソッドをサポートしています](../../../ado/reference/ado-api/supports-method.md)
