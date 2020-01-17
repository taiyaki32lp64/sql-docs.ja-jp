---
title: SQLServerResultSet Members |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 2a438d5d-2d6a-46a0-a2ae-f35fbae4a472
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fed1b515d6e003f00cebbaf3f3a9306572e2ad2b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67970562"
---
# <a name="sqlserverresultset-members"></a>SQLServerResultSet のメンバー
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  次の表は、[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) クラスによって公開されるメンバーを示しています。  
  
## <a name="constructors"></a>コンストラクター  
 [なし] :  
  
## <a name="fields"></a>フィールド  
  
|[オブジェクト名]|[説明]|  
|----------|-----------------|  
|[CONCUR_SS_OPTIMISTIC_CC](../../../connect/jdbc/reference/concur-ss-optimistic-cc-field-sqlserverresultset.md)|行ロックを使用しない [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 読み取り/書き込みのオプティミスティック同時実行制御の種類を指定する場合に使用します。|  
|[CONCUR_SS_OPTIMISTIC_CCVAL](../../../connect/jdbc/reference/concur-ss-optimistic-ccval-field-sqlserverresultset.md)|行ロックを使用しない [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 読み取り/書き込みのオプティミスティック同時実行制御の種類を指定する場合に使用します。|  
|[CONCUR_SS_SCROLL_LOCKS](../../../connect/jdbc/reference/concur-ss-scroll-locks-field-sqlserverresultset.md)|行ロックを使用する [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 読み取り/書き込みのオプティミスティック コンカレンシーの種類を指定する場合に使用します。|  
|[TYPE_SS_DIRECT_FORWARD_ONLY](../../../connect/jdbc/reference/type-ss-direct-forward-only-field-sqlserverresultset.md)|カーソルの種類を、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の高速順方向専用かつ読み取り専用カーソルに指定する場合に使用します。|  
|[TYPE_SS_SCROLL_DYNAMIC](../../../connect/jdbc/reference/type-ss-scroll-dynamic-field-sqlserverresultset.md)|カーソルの種類を、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 動的カーソルに指定する場合に使用します。|  
|[TYPE_SS_SCROLL_KEYSET](../../../connect/jdbc/reference/type-ss-scroll-keyset-field-sqlserverresultset.md)|カーソルの種類を、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] キーセット カーソルに指定する場合に使用します。|  
|[TYPE_SS_SCROLL_STATIC](../../../connect/jdbc/reference/type-ss-scroll-static-field-sqlserverresultset.md)|カーソルの種類を、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 静的カーソルに指定する場合に使用します。|  
|[TYPE_SS_SERVER_CURSOR_FORWARD_ONLY](../../../connect/jdbc/reference/type-ss-server-cursor-forward-only-field-sqlserverresultset.md)|カーソルの種類を、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の高速順方向専用かつ読み取り専用カーソルに指定する場合に使用します。|  
  
## <a name="inherited-fields"></a>継承されたフィールド  
  
|継承元のクラス|[説明]|  
|---------------------------|-----------------|  
|java.sql.ResultSet|CLOSE_CURSORS_AT_COMMIT、CONCUR_READ_ONLY、CONCUR_UPDATABLE、FETCH_FORWARD、FETCH_REVERSE、FETCH_UNKNOWN、HOLD_CURSORS_OVER_COMMIT、TYPE_FORWARD_ONLY、TYPE_SCROLL_INSENSITIVE、TYPE_SCROLL_SENSITIVE|  
  
## <a name="methods"></a>メソッド  
  
|[オブジェクト名]|[説明]|  
|----------|-----------------|  
|[absolute](../../../connect/jdbc/reference/absolute-method-sqlserverresultset.md)|[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトで指定した行にカーソルを移動します。|  
|[afterLast](../../../connect/jdbc/reference/afterlast-method-sqlserverresultset.md)|[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの最終行の後ろにカーソルを移動します。|  
|[beforeFirst](../../../connect/jdbc/reference/beforefirst-method-sqlserverresultset.md)|[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの先頭行の前にカーソルを移動します。|  
|[cancelRowUpdates](../../../connect/jdbc/reference/cancelrowupdates-method-sqlserverresultset.md)|[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの現在の行に対する更新を取り消します。|  
|[clearWarnings](../../../connect/jdbc/reference/clearwarnings-method-sqlserverresultset.md)|[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトについて報告されたすべての警告をクリアします。|  
|[close](../../../connect/jdbc/reference/close-method-sqlserverresultset.md)|[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトのデータベースと JDBC リソースを、オブジェクトが自動的に閉じるときに解放されるのを待機しないで直ちに解放します。|  
|[deleteRow](../../../connect/jdbc/reference/deleterow-method-sqlserverresultset.md)|[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトから、および基になるデータベースから、現在の行を削除します。|  
|[finalize](../../../connect/jdbc/reference/finalize-method-sqlserverresultset.md)|[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトを明示的に閉じます。|  
|[findColumn](../../../connect/jdbc/reference/findcolumn-method-sqlserverresultset.md)|[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの指定された列名に一致する、最初の列のインデックスを取得します。|  
|[first](../../../connect/jdbc/reference/first-method-sqlserverresultset.md)|[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの先頭行にカーソルを移動します。|  
|[getArray](../../../connect/jdbc/reference/getarray-method-sqlserverresultset.md)|[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの現在の行にある指定された列の値が、Array オブジェクトとして取得されます。|  
|[getAsciiStream](../../../connect/jdbc/reference/getasciistream-method-sqlserverresultset.md)|[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの現在の行にある指定された列の値が、ASCII 文字のストリームとして取得されます。|  
|[getBigDecimal](../../../connect/jdbc/reference/getbigdecimal-method-sqlserverresultset.md)|[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの現在の行にある指定された列インデックスの値を、java.math.BigDecimal として取得します。|  
|[getBinaryStream](../../../connect/jdbc/reference/getbinarystream-method-sqlserverresultset.md)|[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの現在の行にある指定された列の値が、未解釈のバイトのバイナリ ストリームとして取得されます。|  
|[getBlob](../../../connect/jdbc/reference/getblob-method-sqlserverresultset.md)|[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの現在の行にある指定された列の値が、Java プログラミング言語の BLOB オブジェクトとして取得されます。|  
|[getBoolean](../../../connect/jdbc/reference/getboolean-method-sqlserverresultset.md)|[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの現在の行にある指定された列の値が、Java プログラミング言語の **boolean** として取得されます。|  
|[getByte](../../../connect/jdbc/reference/getbyte-method-sqlserverresultset.md)|[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの現在の行にある指定された列の値が、Java プログラミング言語の **byte** として取得されます。|  
|[getBytes](../../../connect/jdbc/reference/getbytes-method-sqlserverresultset.md)|[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの現在の行にある指定された列の値が、Java プログラミング言語の **byte** 配列として取得されます。|  
|[getCharacterStream](../../../connect/jdbc/reference/getcharacterstream-method-sqlserverresultset.md)|[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの現在の行にある指定された列の値が、java.io.Reader オブジェクトとして取得されます。|  
|[getClob](../../../connect/jdbc/reference/getclob-method-sqlserverresultset.md)|[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの現在の行にある指定された列の値が、Java プログラミング言語の CLOB オブジェクトとして取得されます。|  
|[getConcurrency](../../../connect/jdbc/reference/getconcurrency-method-sqlserverresultset.md)|[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの同時実行モードを取得します。|  
|[getCursorName](../../../connect/jdbc/reference/getcursorname-method-sqlserverresultset.md)|[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトによって使用される SQL カーソルの名前を取得します。|  
|[getDate](../../../connect/jdbc/reference/getdate-method-sqlserverresultset.md)|[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの現在の行にある指定された列の値が、Java プログラミング言語の java.sql.Date オブジェクトとして取得されます。|  
|[getDateTimeOffset](../../../connect/jdbc/reference/getdatetimeoffset-sqlserverresultset.md)|指定された列の値を[DateTimeOffset クラス](../../../connect/jdbc/reference/datetimeoffset-class.md)オブジェクトとして取得します。|  
|[getDouble](../../../connect/jdbc/reference/getdouble-method-sqlserverresultset.md)|[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの現在の行にある指定された列の値が、Java プログラミング言語の **double** として取得されます。|  
|[getFetchDirection](../../../connect/jdbc/reference/getfetchdirection-method-sqlserverresultset.md)|[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトのフェッチ方向を取得します。|  
|[getFetchSize](../../../connect/jdbc/reference/getfetchsize-method-sqlserverresultset.md)|[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトのフェッチ サイズを取得します。|  
|[getFloat](../../../connect/jdbc/reference/getfloat-method-sqlserverresultset.md)|[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの現在の行にある指定された列の値が、Java プログラミング言語の **float** として取得されます。|  
|[getHoldability](../../../connect/jdbc/reference/getholdability-method-sqlserverresultset.md)|[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの保持機能を取得します。|  
|[getInt](../../../connect/jdbc/reference/getint-method-sqlserverresultset.md)|[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの現在の行にある指定された列の値が、Java プログラミング言語の **int** として取得されます。|  
|[getLong](../../../connect/jdbc/reference/getlong-method-sqlserverresultset.md)|[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの現在の行にある指定された列の値が、Java プログラミング言語の **long** として取得されます。|  
|[getMetaData](../../../connect/jdbc/reference/getmetadata-method-sqlserverresultset.md)|[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの列の数、型、およびプロパティを取得します。|  
|[getNCharacterStream](../../../connect/jdbc/reference/getncharacterstream-method-sqlserverresultset.md)|[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの現在の行にある指定された列の値が、Reader オブジェクトとして取得されます。|  
|[getNClob](../../../connect/jdbc/reference/getnclob-method-sqlserverresultset.md)|[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの現在の行にある指定された列の値が、Java プログラミング言語の **NClob** オブジェクトとして取得されます。|  
|[getNString](../../../connect/jdbc/reference/getnstring-method-sqlserverresultset.md)|[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの現在の行にある指定された列の値が、Java プログラミング言語の String として取得されます。|  
|[getObject](../../../connect/jdbc/reference/getobject-method-sqlserverresultset.md)|[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの現在の行にある指定された列の値が、Java プログラミング言語のオブジェクトとして取得されます。|  
|[getRef](../../../connect/jdbc/reference/getref-method-sqlserverresultset.md)|[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの現在の行にある指定された列の値が、Java プログラミング言語の Ref オブジェクトとして取得されます。|  
|[getRow](../../../connect/jdbc/reference/getrow-method-sqlserverresultset.md)|現在の行番号を取得します。|  
|[getShort](../../../connect/jdbc/reference/getshort-method-sqlserverresultset.md)|[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの現在の行にある指定された列の値が、Java プログラミング言語の **short** として取得されます。|  
|[getStatement](../../../connect/jdbc/reference/getstatement-method-sqlserverresultset.md)|[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトを生成した [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) オブジェクトを取得します。|  
|[getString](../../../connect/jdbc/reference/getstring-method-sqlserverresultset.md)|[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの現在の行にある指定された列の値が、Java プログラミング言語の **String** として取得されます。|  
|[getSQLXML](../../../connect/jdbc/reference/getsqlxml-method-sqlserverresultset.md)|[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの現在の行にある指定された列の値が、**SQLXML** オブジェクトとして取得されます。|  
|[getTime](../../../connect/jdbc/reference/gettime-method-sqlserverresultset.md)|[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの現在の行にある指定された列の値が、Java プログラミング言語の java.sql.Time オブジェクトとして取得されます。|  
|[getTimestamp](../../../connect/jdbc/reference/gettimestamp-method-sqlserverresultset.md)|[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの現在の行にある指定された列の値が、Java プログラミング言語の java.sql.Timestamp オブジェクトとして取得されます。|  
|[getType](../../../connect/jdbc/reference/gettype-method-sqlserverresultset.md)|[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトのカーソルの種類を取得します。|  
|[getUnicodeStream](../../../connect/jdbc/reference/getunicodestream-method-sqlserverresultset.md)|[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの現在の行にある指定された列の値が、Unicode 文字のストリームとして取得されます。|  
|[getURL](../../../connect/jdbc/reference/geturl-method-sqlserverresultset.md)|[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの現在の行にある指定された列の値が、URL オブジェクトとして取得されます。|  
|[getWarnings](../../../connect/jdbc/reference/getwarnings-method-sqlserverresultset.md)|[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトでの呼び出しによって報告された最初の警告を取得します。|  
|[insertRow](../../../connect/jdbc/reference/insertrow-method-sqlserverresultset.md)|挿入行の内容を [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトとデータベースに挿入します。|  
|[isAfterLast](../../../connect/jdbc/reference/isafterlast-method-sqlserverresultset.md)|カーソルが、[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの最終行の後ろにあるかどうかを取得します。|  
|[isBeforeFirst](../../../connect/jdbc/reference/isbeforefirst-method-sqlserverresultset.md)|カーソルが、[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの先頭行の前にあるかどうかを取得します。|  
|[isClosed](../../../connect/jdbc/reference/isclosed-method-sqlserverresultset.md)|[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトが閉じられているかどうかを示します。|  
|[isFirst](../../../connect/jdbc/reference/isfirst-method-sqlserverresultset.md)|カーソルが、この [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの先頭行にあるかどうかを取得します。|  
|[isLast](../../../connect/jdbc/reference/islast-method-sqlserverresultset.md)|カーソルが、[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの最終行にあるかどうかを取得します。|  
|[last](../../../connect/jdbc/reference/last-method-sqlserverresultset.md)|[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの最終行にカーソルを移動します。|  
|[moveToCurrentRow](../../../connect/jdbc/reference/movetocurrentrow-method-sqlserverresultset.md)|記憶されているカーソル位置 (通常は現在の行) に、カーソルを移動します。|  
|[moveToInsertRow](../../../connect/jdbc/reference/movetoinsertrow-method-sqlserverresultset.md)|カーソルを挿入行に移動します。|  
|[next](../../../connect/jdbc/reference/next-method-sqlserverresultset.md)|カーソルを現在の位置から 1 行下に移動します。|  
|[previous](../../../connect/jdbc/reference/previous-method-sqlserverresultset.md)|[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの前の行にカーソルを移動します。|  
|[refreshRow](../../../connect/jdbc/reference/refreshrow-method-sqlserverresultset.md)|データベース内の最新の値を使用して、現在の行を更新します。|  
|[relative](../../../connect/jdbc/reference/relative-method-sqlserverresultset.md)|カーソルを指定された行数分、現在の行を基準に正または負の方向に移動します。|  
|[rowDeleted](../../../connect/jdbc/reference/rowdeleted-method-sqlserverresultset.md)|行が削除されたかどうかを取得します。|  
|[rowInserted](../../../connect/jdbc/reference/rowinserted-method-sqlserverresultset.md)|現在の行に挿入があったかどうかを取得します。|  
|[rowUpdated](../../../connect/jdbc/reference/rowupdated-method-sqlserverresultset.md)|現在の行が更新されたかどうかを取得します。|  
|[setFetchDirection](../../../connect/jdbc/reference/setfetchdirection-method-sqlserverresultset.md)|[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの行を処理する方向についてのヒントを示します。|  
|[setFetchSize](../../../connect/jdbc/reference/setfetchsize-method-sqlserverresultset.md)|[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトにさらに行が必要な場合にデータベースからフェッチする必要がある行数について、JDBC ドライバーにヒントを示します。|  
|[updateArray](../../../connect/jdbc/reference/updatearray-method-sqlserverresultset.md)|指定された列を Array オブジェクトで更新します。|  
|[updateAsciiStream](../../../connect/jdbc/reference/updateasciistream-method-sqlserverresultset.md)|指定された列を ASCII ストリーム値で更新します。|  
|[updateBigDecimal](../../../connect/jdbc/reference/updatebigdecimal-method-sqlserverresultset.md)|指定された列を BigDecimal オブジェクトで更新します。|  
|[updateBinaryStream](../../../connect/jdbc/reference/updatebinarystream-method-sqlserverresultset.md)|指定された列をバイナリ ストリーム値で更新します。|  
|[updateBlob](../../../connect/jdbc/reference/updateblob-method-sqlserverresultset.md)|指定された列を java.sql.Blob 値で更新します。|  
|[updateBoolean](../../../connect/jdbc/reference/updateboolean-method-sqlserverresultset.md)|指定された列を **boolean** 値で更新します。|  
|[updateByte](../../../connect/jdbc/reference/updatebyte-method-sqlserverresultset.md)|指定された列を **byte** 値で更新します。|  
|[updateBytes](../../../connect/jdbc/reference/updatebytes-method-sqlserverresultset.md)|指定された列を **byte** 値の配列で更新します。|  
|[updateCharacterStream](../../../connect/jdbc/reference/updatecharacterstream-method-sqlserverresultset.md)|指定された列を文字ストリームの値で更新します。|  
|[updateClob](../../../connect/jdbc/reference/updateclob-method-sqlserverresultset.md)|指定された列を java.sql.Clob 値で更新します。|  
|[updateDate](../../../connect/jdbc/reference/updatedate-method-sqlserverresultset.md)|指定された列を日付の値で更新します。|  
|[updateDateTimeOffset](../../../connect/jdbc/reference/updatedatetimeoffset-sqlserverresultset.md)|[DateTimeOffset クラス](../../../connect/jdbc/reference/datetimeoffset-class.md)列を更新します。|  
|[updateDouble](../../../connect/jdbc/reference/updatedouble-method-sqlserverresultset.md)|指定された列を **double** 値で更新します。|  
|[updateFloat](../../../connect/jdbc/reference/updatefloat-method-sqlserverresultset.md)|指定された列を **float** 値で更新します。|  
|[updateInt](../../../connect/jdbc/reference/updateint-method-sqlserverresultset.md)|指定された列を **int** 値で更新します。|  
|[updateLong](../../../connect/jdbc/reference/updatelong-method-sqlserverresultset.md)|指定された列を **long** 値で更新します。|  
|[updateNCharacterStream](../../../connect/jdbc/reference/updatencharacterstream-method-sqlserverresultset.md)|指定された列を文字ストリームの値で更新します。|  
|[updateNClob](../../../connect/jdbc/reference/updatenclob-method-sqlserverresultset.md)|指定された列を指定されたオブジェクト値で更新します。|  
|[updateNString](../../../connect/jdbc/reference/updatenstring-method-sqlserverresultset.md)|指定された列を**文字列**の値で更新します。|  
|[updateNull](../../../connect/jdbc/reference/updatenull-method-sqlserverresultset.md)|指定された列を null 値で更新します。|  
|[updateObject](../../../connect/jdbc/reference/updateobject-method-sqlserverresultset.md)|指定した列を **Object** 値で更新します。|  
|[updateRef](../../../connect/jdbc/reference/updateref-method-sqlserverresultset.md)|指定された列を java.sql.Ref 値で更新します。|  
|[updateRow](../../../connect/jdbc/reference/updaterow-method-sqlserverresultset.md)|基になるデータベースを [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの現在の行に含まれる新しい内容で更新します。|  
|[updateShort](../../../connect/jdbc/reference/updateshort-method-sqlserverresultset.md)|指定された列を **short** 値で更新します。|  
|[updateString](../../../connect/jdbc/reference/updatestring-method-sqlserverresultset.md)|指定された列を**文字列**の値で更新します。|  
|[updateSQLXML](../../../connect/jdbc/reference/updatesqlxml-method-sqlserverresultset.md)|指定された列を **SQLXML** 値で更新します。|  
|[updateTime](../../../connect/jdbc/reference/updatetime-method-sqlserverresultset.md)|指定された列を時刻の値で更新します。|  
|[updateTimestamp](../../../connect/jdbc/reference/updatetimestamp-method-sqlserverresultset.md)|指定された列をタイムスタンプ値で更新します。|  
|[wasNull](../../../connect/jdbc/reference/wasnull-method-sqlserverresultset.md)|最後に読み取られた値が null 値かどうかを確認します。|  
  
## <a name="inherited-methods"></a>継承されたメソッド  
  
|継承元のクラス|メソッド|  
|---------------------------|-------------|  
|java.lang.Object|clone、equals、getClass、hashCode、notify、notifyAll、toString、wait|  
|java.sql.Wrapper|isWrapperFor、unwrap|  
  
## <a name="see-also"></a>参照  
 [SQLServerResultSet クラス](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
