---
title: SQLGetStmtAttr 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetStmtAttr
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetStmtAttr
helpviewer_keywords:
- SQLGetStmtAttr function [ODBC]
ms.assetid: e321d460-e997-4527-aee6-207cf5a498e9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 31ddab7291807222882050233715d3ad61e25124
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68061464"
---
# <a name="sqlgetstmtattr-function"></a>SQLGetStmtAttr 関数
**準拠**  
 バージョンが導入されました。ODBC 3.0 規格に準拠します。ISO 92  
  
 **まとめ**  
 **SQLGetStmtAttr**ステートメント属性の現在の設定を返します。  
  
> [!NOTE]  
>  詳細についてはどのようなドライバー マネージャーのときに、ODBC 3 には、この関数にマップします。*x* ODBC 2 を利用するアプリケーション *。x*ドライバーを参照してください[アプリケーションの旧バージョンと互換性のマッピング置換関数](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLGetStmtAttr(  
     SQLHSTMT        StatementHandle,  
     SQLINTEGER      Attribute,  
     SQLPOINTER      ValuePtr,  
     SQLINTEGER      BufferLength,  
     SQLINTEGER *    StringLengthPtr);  
```  
  
## <a name="arguments"></a>引数  
 *StatementHandle*  
 [入力]ステートメント ハンドルです。  
  
 *属性*  
 [入力]取得する属性。  
  
 *ValuePtr*  
 [出力]指定された属性の値を返すバッファーへのポインター*属性*します。  
  
 場合*ValuePtr*が null の場合、 *StringLengthPtr*バイト (文字データの null 終端文字を除く) の合計数を返すはまだが指すバッファーに返される使用可能な*ValuePtr*します。  
  
 *BufferLength*  
 [入力]場合*属性*ODBC で定義された属性と*ValuePtr*文字の文字列またはバイナリのバッファーを指す、この引数の長さである必要があります\* *ValuePtr*. 場合*属性*ODBC で定義された属性と\* *ValuePtr*整数*BufferLength*は無視されます。 値が返される場合 *\*ValuePtr*は Unicode 文字列です (呼び出し時に**SQLGetStmtAttrW**)、 *BufferLength*引数は偶数である必要があります。  
  
 場合*属性*ドライバーの定義済みの属性では、アプリケーションを設定して属性をドライバー マネージャーの性質を示します、 *BufferLength*引数。 *BufferLength*次の値を持つことができます。  
  
-   場合 *\*ValuePtr*文字の文字列へのポインターは*BufferLength* SQL_NTS または文字列の長さです。  
  
-   場合 *\*ValuePtr* 、SQL_LEN_BINARY_ATTR の結果を配置するアプリケーションが、バイナリ バッファーへのポインター (*長さ*) マクロで*BufferLength*します。 これにより、負の値で*BufferLength*します。  
  
-   場合 *\*ValuePtr*文字の文字列またはバイナリ文字列以外の値へのポインターは*BufferLength* SQL_IS_POINTER 値でなければなりません。  
  
-   場合 *\*ValuePtr*ですし、固定長データ型が含まれています*BufferLength* SQL_IS_INTEGER または SQL_IS_UINTEGER のいずれかを適切なは。  
  
 *StringLengthPtr*  
 [出力] (Null 終了文字を除く) バイトの合計数を返すバッファーへのポインターで返される使用可能な *\*ValuePtr*します。 場合*ValuePtr* null ポインターの場合は、長さは返されません。 属性値が文字の文字列と、返される使用可能なバイト数がより大きいまたは等しい場合*BufferLength*、内のデータ *\*ValuePtr* に切り捨てられます*BufferLength* null 終了文字の長さマイナスはドライバーによって null で終わるとします。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR、または SQL_INVALID_HANDLE します。  
  
## <a name="diagnostics"></a>診断  
 ときに**SQLGetStmtAttr** SQL_ERROR または SQL_SUCCESS_WITH_INFO、関連付けられている SQLSTATE 値を返しますを呼び出すことによって取得される可能性があります**SQLGetDiagRec**で、 *HandleType* SQL の_HANDLE_STMT と*処理*の*StatementHandle*します。 次の表に、一般的にによって返される SQLSTATE 値**SQLGetStmtAttr** ; この関数のコンテキストでそれぞれについて説明しますと表記"(DM)"の前にドライバー マネージャーによって返されるについての説明。 SQLSTATE 値ごとに関連付けられているリターン コードは明記しない限り、SQL_ERROR です。  
  
|SQLSTATE|[エラー]|説明|  
|--------------|-----------|-----------------|  
|01000|一般的な警告|ドライバー固有の情報メッセージです。 (関数は、SQL_SUCCESS_WITH_INFO を返します)。|  
|01004|文字列データで、右側が切り捨てられました|返されるデータ *\*ValuePtr*に切り詰められました*BufferLength* null 終了文字の長さマイナスです。 切り詰められていない文字列値の長さが返される **StringLengthPtr*します。 (関数は、SQL_SUCCESS_WITH_INFO を返します)。|  
|24000|カーソル状態が無効|引数*属性*SQL_ATTR_ROW_NUMBER がや、カーソルが開いていない、カーソルが結果セットの場合、または結果セットの終了後に開始する前に配置されました。|  
|HY000|一般的なエラー|これがなかった固有の SQLSTATE とする実装に固有の SQLSTATE が定義されていない、エラーが発生しました。 によって返されるエラー メッセージ**SQLGetDiagRec**引数*MessageText*エラーとその原因について説明します。|  
|HY001|メモリの割り当てエラー|ドライバーは、実行または関数の完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY010|関数のシーケンス エラー|(DM) を非同期的に実行中の関数が呼び出された接続ハンドルに関連付けられているため、 *StatementHandle*します。 この非同期関数ではときに実行されている、 **SQLGetStmtAttr**関数が呼び出されました。<br /><br /> (DM) を非同期的に実行中の関数が呼び出された、 *StatementHandle*この関数が呼び出されたときに実行されているとします。<br /><br /> (DM) **SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**、または**SQLSetPos**に対して呼び出された、 *StatementHandle* SQL_NEED_DATA が返されます。 すべての実行時データ パラメーターまたは列のデータが送信される前に、この関数が呼び出されました。|  
|HY013|メモリ管理エラー|基になるメモリ オブジェクトにアクセスできませんでした、場合によってメモリ不足が原因であるために、関数呼び出しを処理できませんでした。|  
|HY090|文字列またはバッファーの長さが無効です。|*(DM) \*ValuePtr*文字の文字列し、BufferLength は SQL_NTS に等しくないが、0 より小さいをでした。|  
|HY092|無効な属性またはオプション識別子|引数が指定された値*属性*ODBC ドライバーでサポートされているのバージョンには無効です。|  
|HY109|無効なカーソルの位置|*属性*引数が SQL_ATTR_ROW_NUMBER と行に削除されたかをフェッチできませんでした。|  
|HY117|不明なトランザクションの状態のため、接続が中断されます。 のみを切断して、読み取り専用の関数が許可されます。|(DM) 中断状態の詳細については、次を参照してください。 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)します。|  
|HYC00|省略可能な機能が実装されていません|引数が指定された値*属性*有効な ODBC ステートメント属性が ODBC のバージョンのドライバーでサポートされていますが、ドライバーによってサポートされていませんでした。|  
|HYT01|接続がタイムアウトしました|データ ソースが要求に応答する前に、接続のタイムアウト期間が終了しました。 によって、接続タイムアウト期間が設定されます**SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT します。|  
|IM001|ドライバーでは、この関数はサポートされていません|(DM) に対応するドライバー、 *StatementHandle*関数をサポートしていません。|  
  
## <a name="comments"></a>コメント  
 ステートメント属性については、次を参照してください。[ステートメント属性](../../../odbc/reference/develop-app/statement-attributes.md)します。  
  
 呼び出し**SQLGetStmtAttr**で返します *\*ValuePtr*で指定されたステートメント属性の値*属性*します。 その値は sqlulen です値または null で終わる文字の文字列にもできます。 Sqlulen です値の場合、一部のドライバーは、下位の 32 ビットを書き込む場合がありますのみまたは 16 ビット バッファーと参加解除の上位ビットに変更されていません。 そのため、アプリケーションは sqlulen ですのバッファーを使用し、この関数を呼び出す前に、値を 0 を初期化する必要があります。 また、 *BufferLength*と*StringLengthPtr*引数は使用されません。 アプリケーションが内の文字列の最大長を指定して、値が null で終わる文字列の場合は、 *BufferLength*引数と、ドライバーでは、その文字列の長さを返します、  *\*StringLengthPtr*バッファー。  
  
 呼び出すアプリケーションを許可する**SQLGetStmtAttr** ODBC 2 を使用する *。x*ドライバーへの呼び出し**SQLGetStmtAttr**をドライバー マネージャーではマップ**SQLGetStmtOption**します。  
  
 次のステートメント属性は読み取り専用を取得できるように**SQLGetStmtAttr**で設定されていないが、 **SQLSetStmtAttr**:  
  
-   SQL_ATTR_IMP_PARAM_DESC  
  
-   SQL_ATTR_IMP_ROW_DESC  
  
-   SQL_ATTR_ROW_NUMBER  
  
 設定し、取得が可能な属性の一覧は、次を参照してください。 [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)します。  
  
## <a name="related-functions"></a>関連する関数  
  
|詳細|参照先|  
|---------------------------|---------|  
|接続属性の設定を返す|[SQLGetConnectAttr 関数](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|接続属性の設定|[SQLSetConnectAttr 関数](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|ステートメント属性を設定|[SQLSetStmtAttr 関数](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>参照  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)
