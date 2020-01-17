---
title: SQLServerCallableStatement Members |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apitype: Assembly
ms.assetid: 5ebdc186-e50f-4d14-bbf4-95af5051e4a4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 69a12437e3b1e611cf9e48d60c9fd77cd02f63bc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67971867"
---
# <a name="sqlservercallablestatement-members"></a>SQLServerCallableStatement のメンバー
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  次の表では、[SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md) クラスによって公開されるメンバーを示します。  
  
## <a name="constructors"></a>コンストラクター  
 [なし] :  
  
## <a name="fields"></a>フィールド  
  
|継承元のクラス|メソッド|  
|---------------------------|-------------|  
|java.sql.Statement|CLOSE_ALL_RESULTS、CLOSE_CURRENT_RESULT、EXECUTE_FAILED、KEEP_CURRENT_RESULT、NO_GENERATED_KEYS、RETURN_GENERATED_KEYS、SUCCESS_NO_INFO|  
  
## <a name="inherited-fields"></a>継承されたフィールド  
 [なし] :  
  
## <a name="methods"></a>メソッド  
  
|[オブジェクト名]|[説明]|  
|----------|-----------------|  
|[addBatch](../../../connect/jdbc/reference/addbatch-method-sqlserverpreparedstatement.md)|([SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) から継承されます) この CallableStatement オブジェクトのコマンド バッチにパラメーターのセットを追加します。|  
|[cancel](../../../connect/jdbc/reference/cancel-method-sqlserverstatement.md)|([SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) から継承されます) CallableStatement オブジェクトによって現在実行されている SQL ステートメントを取り消します。|  
|[clearBatch](../../../connect/jdbc/reference/clearbatch-method-sqlserverpreparedstatement.md)|([SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) から継承されます) CallableStatement オブジェクトに対する SQL コマンドの現在の一覧を空にします。|  
|[clearParameters](../../../connect/jdbc/reference/clearparameters-method-sqlserverpreparedstatement.md)|([SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) から継承されます) 現在のパラメーター値を直ちにクリアします。|  
|[clearWarnings](../../../connect/jdbc/reference/clearwarnings-method-sqlserverstatement.md)|([SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) から継承されます) CallableStatement オブジェクトについて報告されたすべての警告をクリアします。|  
|[close](../../../connect/jdbc/reference/close-method-sqlserverpreparedstatement.md)|([SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) から継承されます) CallableStatement オブジェクトのデータベースと JDBC リソースを、自動的に解放されるまで待たずに直ちに解放します。|  
|[execute](../../../connect/jdbc/reference/execute-method-sqlserverpreparedstatement.md)|([SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) から継承されます) CallableStatement オブジェクトの SQL ステートメントを実行します。すべての種類の SQL ステートメントを実行できます。|  
|[executeBatch](../../../connect/jdbc/reference/executebatch-method-sqlserverpreparedstatement.md)|([SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) から継承されます) 実行するコマンド バッチをデータベースに送信します。 すべてのコマンドが正常に実行されている場合は、更新数の配列が返されます。|  
|[executeQuery](../../../connect/jdbc/reference/executequery-method-sqlserverpreparedstatement.md)|([SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) から継承されます) CallableStatement オブジェクトの SQL クエリを実行し、クエリによって生成される [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトを返します。|  
|[executeUpdate](../../../connect/jdbc/reference/executeupdate-method-sqlserverpreparedstatement.md)|([SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) から継承されます) CallableStatement オブジェクトの SQL ステートメントを実行します。SQL ステートメントは、SQL INSERT、UPDATE、MERGE、または DELETE ステートメントであるか、DDL ステートメントなどのような何も返さない SQL ステートメントであることが必要です。|  
|[getConnection](../../../connect/jdbc/reference/getconnection-method-sqlserverstatement.md)|([SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) から継承されます) CallableStatement オブジェクトを生成した [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) オブジェクトを取得します。|  
|[getDateTimeOffset](../../../connect/jdbc/reference/getdatetimeoffset-method-sqlservercallablestatement.md)|指定された列の値を[DateTimeOffset クラス](../../../connect/jdbc/reference/datetimeoffset-class.md)オブジェクトとして取得します。|  
|[getFetchDirection](../../../connect/jdbc/reference/getfetchdirection-method-sqlserverstatement.md)|([SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) から継承されます) 行をフェッチする方向をデータベース テーブルから取得します。この方向は、CallableStatement オブジェクトから生成される結果セットの既定の方向となります。|  
|[getFetchSize](../../../connect/jdbc/reference/getfetchsize-method-sqlserverstatement.md)|([SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) から継承されます) 結果セットの行数を取得します。この行数は、CallableStatement オブジェクトから生成される結果セット オブジェクトの既定のフェッチ サイズとなります。|  
|[getGeneratedKeys](../../../connect/jdbc/reference/getgeneratedkeys-method-sqlserverstatement.md)|([SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) から継承されます) CallableStatement オブジェクトを実行した結果作成される自動生成キーを取得します。|  
|[getMaxFieldSize](../../../connect/jdbc/reference/getmaxfieldsize-method-sqlserverstatement.md)|([SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) から継承されます) CallableStatement オブジェクトによって生成される [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの文字およびバイナリの列値に対して返される最大バイト数を取得します。|  
|[getMaxRows](../../../connect/jdbc/reference/getmaxrows-method-sqlserverstatement.md)|([SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) から継承されます) CallableStatement オブジェクトによって生成される [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトが含むことのできる最大行数を取得します。|  
|[getMetaData](../../../connect/jdbc/reference/getmetadata-method-sqlserverpreparedstatement.md)|([SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) から継承されます) [SQLServerResultSetMetaData クラス](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md)のオブジェクトを取得します。このオブジェクトには、CallableStatement オブジェクトの実行時に返される [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの列に関する情報が含まれます。|  
|[getMoreResults](../../../connect/jdbc/reference/getmoreresults-method-sqlserverstatement.md)|([SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) から継承されます) この CallableStatement オブジェクトの次の結果に移動します。|  
|[getParameterMetaData](../../../connect/jdbc/reference/getparametermetadata-method-sqlserverpreparedstatement.md)|([SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) から継承されます) CallableStatement オブジェクトのパラメーターの数、型、およびプロパティを取得します。|  
|[getArray](../../../connect/jdbc/reference/getarray-method-sqlservercallablestatement.md)|指定されたパラメーターの値を Array オブジェクトとして取得します。|  
|[getAsciiStream](../../../connect/jdbc/reference/getasciistream-method-sqlservercallablestatement.md)|指定されたパラメーターの値を **ASCII** 文字のストリームとして取得します。|  
|[getBigDecimal](../../../connect/jdbc/reference/getbigdecimal-method-sqlservercallablestatement.md)|指定されたパラメーターの値を java.math.BigDecimal として取得します。|  
|[getBinaryStream](../../../connect/jdbc/reference/getbinarystream-method-sqlservercallablestatement.md)|指定されたパラメーターの値を連続するバイトのバイナリ ストリームとして取得します。|  
|[getBlob](../../../connect/jdbc/reference/getblob-method-sqlservercallablestatement.md)|指定された JDBC Blob パラメーターの値を Java プログラミング言語の Blob オブジェクトとして取得します。|  
|[getboolean](../../../connect/jdbc/reference/getboolean-method-sqlservercallablestatement.md)|指定されたパラメーターの値を **Boolean** 値として取得します。|  
|[getByte](../../../connect/jdbc/reference/getbyte-method-sqlservercallablestatement.md)|指定されたパラメーターの値を **byte** 値として取得します。|  
|[getBytes](../../../connect/jdbc/reference/getbytes-method-sqlservercallablestatement.md)|指定されたパラメーターの値を byte 配列として取得します。|  
|[getCharacterStream](../../../connect/jdbc/reference/getcharacterstream-method-sqlservercallablestatement.md)|指定されたパラメーターの値を java.io.Reader オブジェクトとして取得します。|  
|[getClob](../../../connect/jdbc/reference/getclob-method-sqlservercallablestatement.md)|指定された JDBC Blob パラメーターの値を Java プログラミング言語の Clob オブジェクトとして取得します。|  
|[getDate](../../../connect/jdbc/reference/getdate-method-sqlservercallablestatement.md)|指定されたパラメーターの値を Java プログラミング言語の java.sql.Date オブジェクトとして取得します。|  
|[getDateTimeOffset](../../../connect/jdbc/reference/getdatetimeoffset-method-sqlservercallablestatement.md)|指定された列の値を[DateTimeOffset クラス](../../../connect/jdbc/reference/datetimeoffset-class.md)オブジェクトとして取得します。|  
|[getDouble](../../../connect/jdbc/reference/getdouble-method-sqlservercallablestatement.md)|指定されたパラメーターの値を Java プログラミング言語の **double** として取得します。|  
|[getFloat](../../../connect/jdbc/reference/getfloat-method-sqlservercallablestatement.md)|指定されたパラメーターの値を Java プログラミング言語の **float** として取得します。|  
|[getInt](../../../connect/jdbc/reference/getint-method-sqlservercallablestatement.md)|指定されたパラメーターの値を Java プログラミング言語の **int** として取得します。|  
|[getLong](../../../connect/jdbc/reference/getlong-method-sqlservercallablestatement.md)|指定されたパラメーターの値を Java プログラミング言語の **long** として取得します。|  
|[getNCharacterStream](../../../connect/jdbc/reference/getncharacterstream-method-sqlservercallablestatement.md)|指定されたパラメーターの値を Reader オブジェクトとして取得します。|  
|[getNClob](../../../connect/jdbc/reference/getnclob-method-sqlservercallablestatement.md)|指定された JDBC **NCLOB** パラメーターの値を Java プログラミング言語の **NClob** オブジェクトとして取得します。|  
|[getNString](../../../connect/jdbc/reference/getnstring-method-sqlservercallablestatement.md)|指定された**NCHAR**、 **NVARCHAR** 、または**LONGNVARCHAR**パラメーターの値を Java プログラミング言語の文字列として取得します。|  
|[getObject](../../../connect/jdbc/reference/getobject-method-sqlservercallablestatement.md)|指定されたパラメーターの値を Java プログラミング言語のオブジェクトとして取得します。|  
|[getQueryTimeout](../../../connect/jdbc/reference/getquerytimeout-method-sqlserverstatement.md)|([SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) から継承されます) [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] が CallableStatement オブジェクトの実行を待つ秒数を取得します。|  
|[getRef](../../../connect/jdbc/reference/getref-method-sqlservercallablestatement.md)|指定されたパラメーターの値を Java プログラミング言語の Ref オブジェクトとして取得します。|  
|[getResponseBuffering](../../../connect/jdbc/reference/getresponsebuffering-method-sqlserverstatement.md)|([SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) から継承されます) [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) オブジェクトの応答バッファリング モードを取得します。|  
|[getResultSet](../../../connect/jdbc/reference/getresultset-method-sqlserverstatement.md)|([SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) から継承されます) 現在の結果を [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトとして取得します。|  
|[getResultSetConcurrency](../../../connect/jdbc/reference/getresultsetconcurrency-method-sqlserverstatement.md)|([SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) から継承されます) CallableStatement オブジェクトによって生成された [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの結果セットのコンカレンシーを取得します。|  
|[getResultSetHoldability](../../../connect/jdbc/reference/getresultsetholdability-method-sqlserverstatement.md)|([SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) から継承されます) CallableStatement オブジェクトによって生成された [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの結果セットの保持機能を取得します。|  
|[getResultSetType](../../../connect/jdbc/reference/getresultsettype-method-sqlserverstatement.md)|([SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) から継承されます) CallableStatement オブジェクトによって生成された [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの結果セットの種類を取得します。|  
|[getShort](../../../connect/jdbc/reference/getshort-method-sqlservercallablestatement.md)|指定されたパラメーターの値を Java プログラミング言語の **short** として取得します。|  
|[getString](../../../connect/jdbc/reference/getstring-method-sqlservercallablestatement.md)|指定されたパラメーターの値を Java プログラミング言語の**文字列**として取得します。|  
|[getSQLXML](../../../connect/jdbc/reference/getsqlxml-method-sqlservercallablestatement.md)|指定されたパラメーターの値を java.sql.SQLXML オブジェクトとして取得します。|  
|[getTime](../../../connect/jdbc/reference/gettime-method-sqlservercallablestatement.md)|指定されたパラメーターの値を Java プログラミング言語の java.sql.Time オブジェクトとして取得します。|  
|[getTimestamp](../../../connect/jdbc/reference/gettimestamp-method-sqlservercallablestatement.md)|指定されたパラメーターの値を Java プログラミング言語の java.sql.Timestamp オブジェクトとして取得します。|  
|[getUpdateCount](../../../connect/jdbc/reference/getupdatecount-method-sqlserverstatement.md)|([SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) から継承されます) 現在の結果を更新数として取得します。|  
|[getURL](../../../connect/jdbc/reference/geturl-method-sqlservercallablestatement.md)|指定されたパラメーターの値を Java プログラミング言語の URL オブジェクトとして取得します。|  
|[getWarnings](../../../connect/jdbc/reference/getwarnings-method-sqlserverstatement.md)|([SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) から継承されます) CallableStatement オブジェクトでの呼び出しによって報告された最初の警告を取得します。|  
|[isClosed](../../../connect/jdbc/reference/isclosed-method-sqlserverstatement.md)|([SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) から継承されます) この Statement オブジェクトが閉じられているかどうかを示します。|  
|[isPoolable](../../../connect/jdbc/reference/ispoolable-method-sqlserverstatement.md)|([SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) から継承されます) ユーザー指定のステートメント プールにステートメントを追加できるかどうかを示す値を返します。|  
|[isWrapperFor](../../../connect/jdbc/reference/iswrapperfor-method-sqlservercallablestatement.md)|ステートメント オブジェクトが指定されたインターフェイスのラッパーであるかどうかを示します。|  
|[registerOutParameter](../../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md)|OUT パラメーターを登録します。|  
|[setArray](../../../connect/jdbc/reference/setarray-method-sqlserverpreparedstatement.md)|([SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) から継承されます) 指定されたパラメーターの番号を、渡された Array オブジェクトに設定します。|  
|[setAsciiStream](../../../connect/jdbc/reference/setasciistream-sqlservercallablestatement.md)|指定されたパラメーターを、渡された入力ストリームに設定します。|  
|[setBigDecimal](../../../connect/jdbc/reference/setbigdecimal-method-sqlservercallablestatement.md)|指定されたパラメーターの番号を、渡された BigDecimal オブジェクトに設定します。|  
|[setBinaryStream](../../../connect/jdbc/reference/setbinarystream-sqlservercallablestatement.md)|指定されたパラメーターを、指定された入力ストリームに設定します。|  
|[setBlob](../../../connect/jdbc/reference/setblob-method-sqlserverpreparedstatement.md)|([SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) から継承されます) 指定されたパラメーターを、渡された Blob オブジェクトに設定します。|  
|[setboolean](../../../connect/jdbc/reference/setboolean-method-sqlservercallablestatement.md)|指定されたパラメーターを、渡された **Boolean** 値に設定します。|  
|[setByte](../../../connect/jdbc/reference/setbyte-method-sqlservercallablestatement.md)|指定されたパラメーターを、渡された **byte** 値に設定します。|  
|[setBytes](../../../connect/jdbc/reference/setbytes-method-sqlservercallablestatement.md)|指定されたパラメーターを、渡された**バイト**値に設定します。|  
|[setCharacterStream](../../../connect/jdbc/reference/setcharacterstream-method-sqlservercallablestatement.md)|指定されたパラメーターを、渡された Reader オブジェクトに設定します。|  
|[setClob](../../../connect/jdbc/reference/setclob-method-sqlservercallablestatement.md)|([SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) から継承されます) 指定されたパラメーターを、指定されたオブジェクトに設定します。|  
|[setCursorName](../../../connect/jdbc/reference/setcursorname-method-sqlserverstatement.md)|([SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) から継承されます) SQL カーソル名を、渡された文字列に設定します。この文字列は、後に続く実行 (execute) メソッドによって使用されます。|  
|[setDate](../../../connect/jdbc/reference/setdate-method-sqlservercallablestatement.md)|指定されたパラメーターを、渡された日付の値に設定します。|  
|[setDateTimeOffset](../../../connect/jdbc/reference/setdatetimeoffset-method-sqlservercallablestatement.md)|指定された列の値を[DateTimeOffset クラス](../../../connect/jdbc/reference/datetimeoffset-class.md)の値に設定します。|  
|[setDouble](../../../connect/jdbc/reference/setdouble-method-sqlservercallablestatement.md)|指定されたパラメーターを、渡された **double** 値に設定します。|  
|[setEscapeProcessing](../../../connect/jdbc/reference/setescapeprocessing-method-sqlserverstatement.md)|([SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) から継承されます) エスケープの処理モードを設定します。|  
|[setFetchDirection](../../../connect/jdbc/reference/setfetchdirection-method-sqlserverstatement.md)|([SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) から継承されます) 結果セットの行を処理する方向についてのヒントを JDBC ドライバーに示します。|  
|[setFetchSize](../../../connect/jdbc/reference/setfetchsize-method-sqlserverstatement.md)|([SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) から継承されます) さらに行が必要な場合にデータベースからフェッチする必要がある行数について、JDBC ドライバーにヒントを示します。|  
|[setFloat](../../../connect/jdbc/reference/setfloat-method-sqlservercallablestatement.md)|指定されたパラメーターを、指定された **float** の値に設定します。|  
|[setInt](../../../connect/jdbc/reference/setint-method-sqlservercallablestatement.md)|指定されたパラメーターを、指定された **int** の値に設定します。|  
|[setLong](../../../connect/jdbc/reference/setlong-method-sqlservercallablestatement.md)|指定されたパラメーターを、指定された **long** の値に設定します。|  
|[setMaxFieldSize](../../../connect/jdbc/reference/setmaxfieldsize-method-sqlserverstatement.md)|([SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) から継承されます) 文字またはバイナリ値を格納する [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 列の最大バイト数の制限を、指定されたバイト数に設定します。|  
|[setMaxRows](../../../connect/jdbc/reference/setmaxrows-method-sqlserverstatement.md)|([SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) から継承されます) 任意の [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトが含むことのできる最大行数の制限を、指定された数値に設定します。|  
|[setNCharacterStream](../../../connect/jdbc/reference/setncharacterstream-method-sqlservercallablestatement.md)|指定されたパラメーターを、指定された Reader オブジェクトに設定します。|  
|[setNClob](../../../connect/jdbc/reference/setnclob-method-sqlservercallablestatement.md)|指定されたパラメーターを、指定されたオブジェクトに設定します。|  
|[setNString](../../../connect/jdbc/reference/setnstring-method-sqlservercallablestatement.md)|指定されたパラメーターを、指定された String オブジェクトに設定します。|  
|[setNull](../../../connect/jdbc/reference/setnull-method-sqlservercallablestatement.md)|渡されたパラメーターの型で、指定されたパラメーターを null 値に設定します。|  
|[setObject](../../../connect/jdbc/reference/setobject-method-sqlservercallablestatement.md)|渡されたオブジェクトを使用して、指定されたパラメーターの値が設定されます。|  
|[setPoolable](../../../connect/jdbc/reference/setpoolable-method-sqlserverstatement.md)|([SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) から継承されます) ステートメントをプールすること、またはプールしないことを要求します。 既定では、SQLServerCallableStatement オブジェクトは作成時にプールされます。|  
|[setQueryTimeout](../../../connect/jdbc/reference/setquerytimeout-method-sqlserverstatement.md)|([SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) から継承されます) CallableStatement オブジェクトの実行をドライバーが待つ秒数を、指定された秒数に設定します。|  
|[setRef](../../../connect/jdbc/reference/setref-method-sqlserverpreparedstatement.md)|([SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) から継承されます) 指定されたパラメーターを、指定された Ref オブジェクトに設定します。|  
|[setResponseBuffering](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md)|([SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) から継承されます) [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) オブジェクトの応答バッファリング モードを **String full** または **adaptive** に設定します。これらのモードの文字列では、大文字と小文字のどちらも使用できます。|  
|[setShort](../../../connect/jdbc/reference/setshort-method-sqlservercallablestatement.md)|指定されたパラメーターを、指定された **short** 値に設定します。|  
|[setString](../../../connect/jdbc/reference/setstring-method-sqlservercallablestatement.md)|指定されたパラメーターを、指定された Java **String** 値に設定します。|  
|[setSQLXML](../../../connect/jdbc/reference/setsqlxml-method-sqlservercallablestatement.md)|指定されたパラメーターを、指定された **SQLXML** オブジェクトに設定します。|  
|[setTime](../../../connect/jdbc/reference/settime-method-sqlservercallablestatement.md)|指定されたパラメーターを、指定された時刻の値に設定します。|  
|[setTimestamp](../../../connect/jdbc/reference/settimestamp-method-sqlservercallablestatement.md)|指定されたパラメーターを、指定されたタイムスタンプ値に設定します。|  
|[setUnicodeStream](../../../connect/jdbc/reference/setunicodestream-method-sqlserverpreparedstatement.md)|([SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) から継承されます) 指定されたパラメーターの番号を、渡された入力ストリームに設定します。入力ストリームは、指定されたバイト数を持ちます。|  
|[setURL](../../../connect/jdbc/reference/seturl-method-sqlservercallablestatement.md)|指定されたパラメーターを、指定された URL 値に設定します。|  
|[unwrap](../../../connect/jdbc/reference/unwrap-method-sqlservercallablestatement.md)|指定されたインターフェイスを実装するオブジェクトを返します。このメソッドから返されたオブジェクトを使用することで、[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 固有のメソッドにアクセスできます。|  
|[wasNull](../../../connect/jdbc/reference/wasnull-method-sqlservercallablestatement.md)|最後に読み取られた OUT パラメーターが SQL NULL かどうかを取得します。|  
  
## <a name="inherited-methods"></a>継承されたメソッド  
  
|継承元のクラス|メソッド|  
|---------------------------|-------------|  
|com.microsoft.sqlserver.jdbc.SQLServerPreparedStatement|addBatch、clearBatch、clearParameters、close、execute、executeBatch、executeQuery、executeUpdate、getMetaData、getParameterMetaData、setArray、setAsciiStream、setBigDecimal、setBinaryStream、setBlob、setboolean、setByte、setBytes、setCharacterStream、setClob、setDate、setDouble、setFloat、setInt、setLong、setNull、setObject、setRef、setShort、setString、setTime、setTimestamp、setUnicodeStream、setURL|  
|com.microsoft.sqlserver.jdbc.SQLServerStatement|cancel、clearWarnings、execute、executeUpdate、getConnection、getFetchDirection、getFetchSize、getGeneratedKeys、getMaxFieldSize、getMaxRows、getMoreResults、getQueryTimeout、getResultSet、getResultSetConcurrency、getResultSetHoldability、getResultSetType、getUpdateCount、getWarnings、isPoolable、setCursorName、setEscapeProcessing、setFetchDirection、setFetchSize、setMaxFieldSize、setMaxRows、setPoolable、setQueryTimeout|  
|class java.lang.Object|clone、equals、finalize、getClass、hashCode、notify、notifyAll、toString、wait|  
|java.sql.PreparedStatement|addBatch、clearParameters、execute、executeQuery、executeUpdate、getMetaData、getParameterMetaData、getSQLXML、setArray、setAsciiStream、setBigDecimal、setBinaryStream、setBlob、setboolean、setByte、setBytes、setCharacterStream、setClob、setDate、setDate、setDouble、setFloat、setInt、setLong、setNull、setObject、setRef、setShort、setString、setSQLXML、setTime、setTimestamp、setUnicodeStream、setURL|  
|java.sql.Statement|addBatch、cancel、clearBatch、clearWarnings、close、execute、executeBatch、executeQuery、executeUpdate、getConnection、getFetchDirection、getFetchSize、getGeneratedKeys、getMaxFieldSize、getMaxRows、getMoreResults、getQueryTimeout、getResultSet、getResultSetConcurrency、getResultSetHoldability、getResultSetType、getUpdateCount、getWarnings、setCursorName、setEscapeProcessing、setFetchDirection、setFetchSize、setMaxFieldSize、setMaxRows、setQueryTimeout|  
|java.sql.Wrapper|isWrapperFor、unwrap|  
  
## <a name="see-also"></a>参照  
 [SQLServerCallableStatement クラス](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
