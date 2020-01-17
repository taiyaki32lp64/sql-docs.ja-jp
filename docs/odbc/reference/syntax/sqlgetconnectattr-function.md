---
title: SQLGetConnectAttr 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetConnectOption
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetConnectAttr
helpviewer_keywords:
- SQLGetConnectAttr function [ODBC]
ms.assetid: 2cb4ffa8-19d3-4664-8c2f-6682cdcc3f33
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 06c158c49c0ce175204bc9738a4f4136db7fe344
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68006215"
---
# <a name="sqlgetconnectattr-function"></a>SQLGetConnectAttr 関数
**準拠**  
 バージョンが導入されました。ODBC 3.0 規格に準拠します。ISO 92  
  
 **まとめ**  
 **SQLGetConnectAttr**接続属性の現在の設定を返します。  
  
> [!NOTE]
>  どのようなドライバー マネージャーは、ときに、マッピングするには、この関数、ODBC 3 の詳細については *.x*アプリケーションの操作は、ODBC 2 *.x*ドライバーを参照してください[後方のマッピング置換関数アプリケーションの互換性を](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLGetConnectAttr(  
     SQLHDBC        ConnectionHandle,  
     SQLINTEGER     Attribute,  
     SQLPOINTER     ValuePtr,  
     SQLINTEGER     BufferLength,  
     SQLINTEGER *   StringLengthPtr);  
```  
  
## <a name="arguments"></a>引数  
 *ConnectionHandle*  
 [入力] 接続ハンドル。  
  
 *属性*  
 [入力]取得する属性。  
  
 *ValuePtr*  
 [出力]指定された属性の現在の値を返すメモリへのポインター*属性*します。 整数型の属性の下位 32 ビットのみ書き込むことによってドライバーまたは 16 ビット バッファーと参加解除の上位ビットに変更されていません。 そのため、アプリケーションは sqlulen ですのバッファーを使用し、この関数を呼び出す前に、値を 0 を初期化する必要があります。  
  
 場合*ValuePtr*が null の場合、 *StringLengthPtr*バイト (文字データの null 終端文字を除く) の合計数を返すはまだが指すバッファーに返される使用可能な*ValuePtr*します。  
  
 *BufferLength*  
 [入力]場合*属性*ODBC で定義された属性と*ValuePtr*文字の文字列またはバイナリのバッファーを指す、この引数の長さである必要があります\* *ValuePtr*. 場合*属性*ODBC で定義された属性と\* *ValuePtr*整数*BufferLength*は無視されます。 場合の値 *\*ValuePtr*は Unicode 文字列です (呼び出し時に**SQLGetConnectAttrW**)、 *BufferLength*引数は偶数である必要があります。  
  
 場合*属性*ドライバーの定義済みの属性では、アプリケーションを設定して属性をドライバー マネージャーの性質を示します、 *BufferLength*引数。 *BufferLength*次の値を持つことができます。  
  
-   場合 *\*ValuePtr*文字の文字列へのポインターは、 *BufferLength*文字列の長さです。  
  
-   場合 *\*ValuePtr*バイナリのバッファー、アプリケーションの場所へのポインター、SQL_LEN_BINARY_ATTR の結果は、(*長さ*) マクロで*BufferLength*します。 これにより、負の値で*BufferLength*します。  
  
-   場合 *\*ValuePtr*文字の文字列またはバイナリ文字列以外の値へのポインターは、 *BufferLength* SQL_IS_POINTER 値でなければなりません。  
  
-   場合 *\*ValuePtr* 、固定長データ型を含む*BufferLength* SQL_IS_INTEGER または SQL_IS_UINTEGER のいずれかを適切なは。  
  
 *StringLengthPtr*  
 [出力] (Null 終了文字を除く) バイトの合計数を返すバッファーへのポインターで返される使用可能な\* *ValuePtr*します。 場合\* *ValuePtr* null ポインターの場合は、長さは返されません。 属性値が文字の文字列と、返される使用可能なバイト数がより大きい場合*BufferLength* null 終了文字のデータの長さマイナス *\*ValuePtr*に切り捨てられます*BufferLength* null 終了文字の長さマイナスはドライバーによって null で終わるとします。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_NO_DATA、SQL_ERROR、または SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診断  
 ときに**SQLGetConnectAttr** SQL_ERROR または SQL_SUCCESS_WITH_INFO、関連付けられている SQLSTATE 値を返しますは、呼び出すことによって、診断データの構造から取得できます**SQLGetDiagRec** 、で *。HandleType* sql_handle_dbc としての*処理*の*ConnectionHandle*します。 次の表に、によって返される通常の SQLSTATE 値**SQLGetConnectAttr** ; この関数のコンテキストでそれぞれについて説明しますと表記"(DM)"の前にドライバー マネージャーによって返されるについての説明. SQLSTATE 値ごとに関連付けられているリターン コードは明記しない限り、SQL_ERROR です。  
  
|SQLSTATE|[エラー]|説明|  
|--------------|-----------|-----------------|  
|01000|一般的な警告|ドライバー固有の情報メッセージです。 (関数は、SQL_SUCCESS_WITH_INFO を返します)。|  
|01004|文字列データで、右側が切り捨てられました|返されるデータ\* *ValuePtr*に切り詰められました*BufferLength* null 終了文字の長さマイナスです。 切り詰められていない文字列値の長さが返される **StringLengthPtr*します。 (関数は、SQL_SUCCESS_WITH_INFO を返します)。|  
|08003|接続は開いていません|(DM)、*属性*に対して開いている接続に必要な値が指定されました。|  
|08S01|通信リンク エラー|関数が完了した処理の前に、ドライバーとドライバーが接続されているデータ ソース間の通信リンクに失敗しました。|  
|HY000|一般的なエラー|これがなかった固有の SQLSTATE とする実装に固有の SQLSTATE が定義されていない、エラーが発生しました。 引数で診断データの構造からエラー メッセージが返される*MessageText*で**SQLGetDiagField**エラーとその原因について説明します。|  
|HY001|メモリの割り当てエラー|ドライバーは、実行または関数の完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY010|関数のシーケンス エラー|(DM) **SQLBrowseConnect**に対して呼び出された、 *ConnectionHandle* SQL_NEED_DATA が返されます。 この関数が呼び出されました**SQLBrowseConnect** SQL_SUCCESS_WITH_INFO または SQL_SUCCESS が返されます。<br /><br /> (DM) **SQLExecute**、 **SQLExecDirect**、または**SQLMoreResults**に対して呼び出された、 *ConnectionHandle* SQL_PARAM_DATA_ を返されます。ご利用いただけます。 ストリームのすべてのパラメーターのデータが取得される前に、この関数が呼び出されました。|  
|HY013|メモリ管理エラー|基になるメモリ オブジェクトにアクセスできませんでした、場合によってメモリ不足が原因であるために、関数呼び出しを処理できませんでした。|  
|HY090|文字列またはバッファーの長さが無効です。|(DM)  *\*ValuePtr*文字の文字列し、BufferLength は SQL_NTS 等しくもありませんが、0 より小さいをでした。|  
|HY092|無効な属性またはオプション識別子|引数が指定された値*属性*ODBC ドライバーでサポートされているのバージョンには無効です。|  
|HY114|ドライバーは接続レベルの非同期関数の実行をサポートしていません|(DM) アプリケーションは、非同期接続の操作をサポートしていないドライバーの SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE を使用した非同期関数の実行を有効にしようとしました。|  
|HY117|不明なトランザクションの状態のため、接続が中断されます。 のみを切断して、読み取り専用の関数が許可されます。|(DM) 中断状態の詳細については、次を参照してください。 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)します。|  
|HYC00|省略可能な機能が実装されていません|引数が指定された値*属性*有効な ODBC 接続属性が ODBC のバージョンのドライバーでサポートされていますが、ドライバーによってサポートされていませんでした。|  
|HYT01|接続がタイムアウトしました|データ ソースが要求に応答する前に、接続のタイムアウト期間が終了しました。 によって、接続タイムアウト期間が設定されます**SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT します。|  
|IM001|ドライバーでは、この関数はサポートされていません|(DM) に対応するドライバー、 *ConnectionHandle*関数をサポートしていません。|  
  
## <a name="comments"></a>コメント  
 接続属性については、次を参照してください。[接続属性](../../../odbc/reference/develop-app/connection-attributes.md)します。  
  
 設定可能な属性の一覧は、次を参照してください。 [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)します。 その場合に注意してください*属性*、文字列を返す属性を指定します*ValuePtr*の文字列バッファーへのポインターである必要があります。 Null 終了文字を含む、返される文字列の最大長*BufferLength*バイト。  
  
 属性によってアプリケーションが呼び出す前に接続を確立する**SQLGetConnectAttr**します。 ただし場合、 **SQLGetConnectAttr**と呼ばれる、指定した属性は、既定値はなく、前回の呼び出しが設定されていないと**SQLSetConnectAttr**、 **SQLGetConnectAttr**SQL_NO_DATA が返されます。  
  
 場合*属性*SQL_ATTR トレースまたは SQL_ATTR トレースファイル*ConnectionHandle*が無効になると**SQLGetConnectAttr** SQL_ERROR または sql _ は返されませんINVALID_HANDLE 場合*ConnectionHandle*が無効です。 これらの属性は、すべての接続に適用されます。 **SQLGetConnectAttr**もう 1 つの引数が有効でない場合、SQL_ERROR または SQL_INVALID_HANDLE を返します。  
  
 アプリケーションを使用してステートメント属性を設定することもできます**SQLSetConnectAttr**、アプリケーションが使用できない**SQLGetConnectAttr**値ステートメント属性を取得するには、呼び出す必要があります**SQLGetStmtAttr**ステートメント属性の設定を取得します。  
  
 SQL_ATTR_AUTO_IPD と SQL_ATTR_CONNECTION_DEAD の両方の接続属性への呼び出しによって返される**SQLGetConnectAttr**への呼び出しで設定することはできませんが、 **SQLSetConnectAttr**します。  
  
> [!NOTE]  
>  非同期サポートはありません**SQLGetConnectAttr**します。 実装するときに**SQLGetConnectAttr**ドライバーは、情報の送信や、サーバーから要求された回数を最小限に抑えることでパフォーマンスを向上できます。  
  
## <a name="related-functions"></a>関連する関数  
  
|詳細|参照先|  
|---------------------------|---------|  
|ステートメント属性の設定を返す|[SQLGetStmtAttr 関数](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)|  
|接続属性の設定|[SQLSetConnectAttr 関数](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|環境属性を設定|[SQLSetEnvAttr 関数](../../../odbc/reference/syntax/sqlsetenvattr-function.md)|  
|ステートメント属性を設定|[SQLSetStmtAttr 関数](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>参照  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)
