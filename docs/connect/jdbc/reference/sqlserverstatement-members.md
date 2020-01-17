---
title: SQLServerStatement Members |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 828cbaa9-ea7a-4986-95c3-5ba0d7d01d83
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 72eededd01cd61d6845cc92bbdfbfd073668dd76
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67970353"
---
# <a name="sqlserverstatement-members"></a>SQLServerStatement のメンバー
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  次の表は、[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) クラスによって公開されるメンバーを示しています。  
  
## <a name="constructors"></a>コンストラクター  
 [なし] :  
  
## <a name="fields"></a>フィールド  
 [なし] :  
  
## <a name="inherited-fields"></a>継承されたフィールド  
  
|[オブジェクト名]|[説明]|  
|----------|-----------------|  
|java.sql.Statement|CLOSE_ALL_RESULTS、CLOSE_CURRENT_RESULT、EXECUTE_FAILED、KEEP_CURRENT_RESULT、NO_GENERATED_KEYS、RETURN_GENERATED_KEYS、SUCCESS_NO_INFO|  
  
## <a name="methods"></a>メソッド  
  
|[オブジェクト名]|[説明]|  
|----------|-----------------|  
|[addBatch](../../../connect/jdbc/reference/addbatch-method-sqlserverstatement.md)|渡された SQL コマンドを、[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) オブジェクトの現在のコマンド一覧に追加します。|  
|[cancel](../../../connect/jdbc/reference/cancel-method-sqlserverstatement.md)|[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) オブジェクトによって現在実行されている SQL ステートメントを取り消します。|  
|[clearBatch](../../../connect/jdbc/reference/clearbatch-method-sqlserverstatement.md)|[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) オブジェクトに対する SQL コマンドの現在の一覧を空にします。|  
|[clearWarnings](../../../connect/jdbc/reference/clearwarnings-method-sqlserverstatement.md)|[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) オブジェクトについて報告されたすべての警告をクリアします。|  
|[close](../../../connect/jdbc/reference/close-method-sqlserverstatement.md)|[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) オブジェクトのデータベースと JDBC リソースを、自動的に解放されるまで待たずに直ちに解放します。|  
|[execute](../../../connect/jdbc/reference/execute-method-sqlserverstatement.md)|渡された SQL ステートメントを実行します。このステートメントは、複数の結果を返す場合があります。|  
|[executeBatch](../../../connect/jdbc/reference/executebatch-method-sqlserverstatement.md)|実行するコマンド バッチをデータベースに送信します。 すべてのコマンドが正常に実行されている場合は、更新数の配列が返されます。|  
|[executeQuery](../../../connect/jdbc/reference/executequery-method-sqlserverstatement.md)|渡された SQL ステートメントを実行し、1 つの [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトを返します。|  
|[executeUpdate](../../../connect/jdbc/reference/executeupdate-method-sqlserverstatement.md)|渡された SQL ステートメントを実行します。ステートメントは INSERT、UPDATE、MERGE、DELETE、または SQL DDL ステートメントのような何も返さない SQL ステートメントが可能です。|  
|[getConnection](../../../connect/jdbc/reference/getconnection-method-sqlserverstatement.md)|[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) オブジェクトを生成した [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) オブジェクトを取得します。|  
|[getFetchDirection](../../../connect/jdbc/reference/getfetchdirection-method-sqlserverstatement.md)|行をフェッチする方向をデータベース テーブルから取得します。この方向は、[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) オブジェクトから生成される結果セットの既定の方向となります。|  
|[getFetchSize](../../../connect/jdbc/reference/getfetchsize-method-sqlserverstatement.md)|結果セットの行数を取得します。この行数は、[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) オブジェクトから生成される結果セット オブジェクトの既定のフェッチ サイズとなります。|  
|[getGeneratedKeys](../../../connect/jdbc/reference/getgeneratedkeys-method-sqlserverstatement.md)|[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) オブジェクトを実行した結果作成される自動生成キーを取得します。|  
|[getMaxFieldSize](../../../connect/jdbc/reference/getmaxfieldsize-method-sqlserverstatement.md)|[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) オブジェクトによって生成される [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの文字列やバイナリ列の値に対して返すことができる最大バイト数を取得します。|  
|[getMaxRows](../../../connect/jdbc/reference/getmaxrows-method-sqlserverstatement.md)|[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) オブジェクトによって生成される [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトが含むことのできる最大行数を取得します。|  
|[getMoreResults](../../../connect/jdbc/reference/getmoreresults-method-sqlserverstatement.md)|[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) オブジェクトの次の結果に移動します。|  
|[getQueryTimeout](../../../connect/jdbc/reference/getquerytimeout-method-sqlserverstatement.md)|[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] が [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) オブジェクトの実行を待つ秒数を取得します。|  
|[getResponseBuffering](../../../connect/jdbc/reference/getresponsebuffering-method-sqlserverstatement.md)|[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) オブジェクトの応答バッファリング モードを取得します。|  
|[getResultSet](../../../connect/jdbc/reference/getresultset-method-sqlserverstatement.md)|現在の結果を [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトとして取得します。|  
|[getResultSetConcurrency](../../../connect/jdbc/reference/getresultsetconcurrency-method-sqlserverstatement.md)|[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) オブジェクトによって生成された [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの結果セットのコンカレンシーを取得します。|  
|[getResultSetHoldability](../../../connect/jdbc/reference/getresultsetholdability-method-sqlserverstatement.md)|[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) オブジェクトによって生成された [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの結果セットの保持機能を取得します。|  
|[getResultSetType](../../../connect/jdbc/reference/getresultsettype-method-sqlserverstatement.md)|[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) オブジェクトによって生成された [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの結果セットの種類を取得します。|  
|[getUpdateCount](../../../connect/jdbc/reference/getupdatecount-method-sqlserverstatement.md)|現在の結果を更新数として取得します。|  
|[getWarnings](../../../connect/jdbc/reference/getwarnings-method-sqlserverstatement.md)|[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) オブジェクトでの呼び出しによって報告された最初の警告を取得します。|  
|[isClosed](../../../connect/jdbc/reference/isclosed-method-sqlserverstatement.md)|[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) オブジェクトが閉じられているかどうかを示します。|  
|[isPoolable](../../../connect/jdbc/reference/ispoolable-method-sqlserverstatement.md)|ユーザー指定のステートメント プールにステートメントを追加できるかどうかを示す値を返します。|  
|[isWrapperFor](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverstatement.md)|ステートメント オブジェクトが指定されたインターフェイスのラッパーであるかどうかを示します。|  
|[setCursorName](../../../connect/jdbc/reference/setcursorname-method-sqlserverstatement.md)|SQL カーソル名を、渡された文字列に設定します。この文字列は、後に続く実行 (execute) メソッドによって使用されます。|  
|[setEscapeProcessing](../../../connect/jdbc/reference/setescapeprocessing-method-sqlserverstatement.md)|エスケープの処理モードを設定します。|  
|[setFetchDirection](../../../connect/jdbc/reference/setfetchdirection-method-sqlserverstatement.md)|結果セットの行を処理する方向についてのヒントを JDBC ドライバーに示します。|  
|[setFetchSize](../../../connect/jdbc/reference/setfetchsize-method-sqlserverstatement.md)|さらに行が必要な場合にデータベースからフェッチする必要がある行数について、JDBC ドライバーにヒントを示します。|  
|[setMaxFieldSize](../../../connect/jdbc/reference/setmaxfieldsize-method-sqlserverstatement.md)|文字またはバイナリ値を格納する [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 列の最大バイト数の制限を、渡されたバイト数に設定します。|  
|[setMaxRows](../../../connect/jdbc/reference/setmaxrows-method-sqlserverstatement.md)|任意の [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトが含むことのできる最大行数の制限が、渡された数値に設定されます。|  
|[setPoolable](../../../connect/jdbc/reference/setpoolable-method-sqlserverstatement.md)|ステートメントをプールすること、またはプールしないことを要求します。|  
|[setQueryTimeout](../../../connect/jdbc/reference/setquerytimeout-method-sqlserverstatement.md)|[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) オブジェクトの実行が完了するのをドライバーが待つ秒数を、渡された秒数に設定します。|  
|[setResponseBuffering](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md)|[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) オブジェクトの応答バッファリング モードを **String full** または **adaptive** に設定します。これらのモードの文字列では、大文字と小文字のどちらも使用できます。|  
|[unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md)|指定されたインターフェイスを実装するオブジェクトを返します。このメソッドから返されたオブジェクトを使用することで、[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 固有のメソッドにアクセスできます。|  
  
## <a name="inherited-methods"></a>継承されたメソッド  
  
|継承元のクラス|メソッド|  
|---------------------------|-------------|  
|java.lang.Object|clone、equals、getClass、hashCode、notify、notifyAll、toString、wait|  
|java.sql.Wrapper|isWrapperFor、unwrap|  
  
## <a name="see-also"></a>参照  
 [SQLServerStatement クラス](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
