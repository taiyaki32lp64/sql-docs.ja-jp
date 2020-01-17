---
title: SQLGetDescField 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetDescField
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetDescField
helpviewer_keywords:
- SQLGetDescField function [ODBC]
ms.assetid: f09ff660-1e4a-4370-be85-90d4da0487d3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cdf2990056c297d217248543812e347b61d3486d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68103809"
---
# <a name="sqlgetdescfield-function"></a>SQLGetDescField 関数
**準拠**  
 バージョンが導入されました。ODBC 3.0 規格に準拠します。ISO 92  
  
 **まとめ**  
 **SQLGetDescField**現在の設定または記述子レコードの 1 つのフィールドの値を返します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLGetDescField(  
     SQLHDESC        DescriptorHandle,  
     SQLSMALLINT     RecNumber,  
     SQLSMALLINT     FieldIdentifier,  
     SQLPOINTER      ValuePtr,  
     SQLINTEGER      BufferLength,  
     SQLINTEGER *    StringLengthPtr);  
```  
  
## <a name="arguments"></a>引数  
 *DescriptorHandle*  
 [入力]記述子ハンドル。  
  
 *RecNumber*  
 [入力]アプリケーションが情報をシークする記述子レコードを示します。 記述子のレコードは、レコード番号 0 ブックマーク レコードの中で、0 から番号が付けられます。 場合、 *FieldIdentifier*引数が、ヘッダー フィールドを示します*RecNumber*は無視されます。 場合*RecNumber* SQL_DESC_COUNT 小さいですが、行に列またはパラメーターへの呼び出しのデータが含まれていない**SQLGetDescField**はフィールドの既定値を返します。 (詳細については、「記述子フィールドの初期化」を参照してください[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md))。  
  
 *FieldIdentifier*  
 [入力]値が返される記述子フィールドを示します。 詳細については、次を参照してください。、"*FieldIdentifier*引数"セクション[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)します。  
  
 *ValuePtr*  
 [出力]記述子の情報を返すバッファーへのポインター。 データ型の値に依存*FieldIdentifier*します。  
  
 場合*ValuePtr*が整数型、アプリケーションは sqlulen ですのバッファーを使用する必要があります、およびドライバーによって、この関数を呼び出す前に初期化値を 0 の下位 32 ビットまたは 16 ビットのバッファーを書き込むし、上位のビットのままに可能性がありますのみ変更されていません。  
  
 場合*ValuePtr*が null の場合、 *StringLengthPtr*バイト (文字データの null 終端文字を除く) の合計数を返すはまだが指すバッファーに返される使用可能な*ValuePtr*します。  
  
 *BufferLength*  
 [入力]場合*FieldIdentifier* ODBC で定義されたフィールドと*ValuePtr*文字の文字列またはバイナリのバッファーを指す、この引数の長さである必要があります\* *ValuePtr*. 場合*FieldIdentifier* ODBC で定義されたフィールドと\* *ValuePtr*整数*BufferLength*は無視されます。 場合の値 *\*ValuePtr*が Unicode データ型 (呼び出し時に**SQLGetDescFieldW**)、 *BufferLength*引数は偶数である必要があります。  
  
 場合*FieldIdentifier*ドライバーの定義済みのフィールドでは、アプリケーションでは、フィールドには、ドライバー マネージャーの性質を示しますを設定して、 *BufferLength*引数。 *BufferLength*次の値を持つことができます。  
  
-   場合 *\*ValuePtr*文字の文字列へのポインターは*BufferLength* SQL_NTS または文字列の長さです。  
  
-   場合 *\*ValuePtr* 、SQL_LEN_BINARY_ATTR の結果を配置するアプリケーションが、バイナリ バッファーへのポインター (*長さ*) マクロで*BufferLength*します。 これにより、負の値で*BufferLength*します。  
  
-   場合 *\*ValuePtr*文字の文字列またはバイナリ文字列以外の値へのポインターは*BufferLength* SQL_IS_POINTER 値でなければなりません。  
  
-   場合 *\*ValuePtr*はし、固定長データ型を含む*BufferLength*に応じて SQL_IS_INTEGER、SQL_IS_UINTEGER、SQL_IS_SMALLINT、または SQL_IS_USMALLINT は、します。  
  
 *StringLengthPtr*  
 [出力](Null 終端文字のために必要なバイト数を除く) バイトの合計数を返すバッファーへのポインターで返される使用可能な **ValuePtr*します。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR、SQL_NO_DATA、または SQL_INVALID_HANDLE します。  
  
 場合は、SQL_NO_DATA が返されます。 *RecNumber*記述子レコードの現在の数より大きい。  
  
 場合は、SQL_NO_DATA が返されます。 *DescriptorHandle* IRD ハンドルと、ステートメントが準備または実行された状態が関連付けられている開いているカーソルはありませんでした。  
  
## <a name="diagnostics"></a>診断  
 ときに**SQLGetDescField** SQL_ERROR または SQL_SUCCESS_WITH_INFO、関連付けられている SQLSTATE 値を返しますを呼び出すことによって取得できる**SQLGetDiagRec**で、 *HandleType*のSql_handle_stmt として、*処理*の*StatementHandle*します。 次の表に、一般的にによって返される SQLSTATE 値**SQLGetDescField** ; この関数のコンテキストでそれぞれについて説明しますと表記"(DM)"の前にドライバー マネージャーによって返されるについての説明。 SQLSTATE 値ごとに関連付けられているリターン コードは明記しない限り、SQL_ERROR です。  
  
|SQLSTATE|[エラー]|説明|  
|--------------|-----------|-----------------|  
|01000|一般的な警告|ドライバー固有の情報メッセージです。 (関数は、SQL_SUCCESS_WITH_INFO を返します)。|  
|01004|文字列データで、右側が切り捨てられました|バッファー \* *ValuePtr*フィールドが切り捨てられるため、全体の記述子フィールドを返すのに十分な大きさがありません。 切り詰められていない記述子フィールドの長さが返される **StringLengthPtr*します。 (関数は、SQL_SUCCESS_WITH_INFO を返します)。|  
|07009|無効な記述子のインデックス|(DM)、 *RecNumber*引数が 0 と等しく、SQL_ATTR_USE_BOOKMARK ステートメント属性されました SQL_UB_OFF、および*DescriptorHandle*引数は、IRD のハンドル。 (このエラーは返されますを明示的に割り当てられた記述子の記述子がステートメント ハンドルに関連付けられた場合にのみ。)<br /><br /> *FieldIdentifier*引数がレコードのフィールド、 *RecNumber*引数が 0 の場合、 *DescriptorHandle*引数は、IPD ハンドル。<br /><br /> *RecNumber*引数が 0 未満でした。|  
|08S01|通信リンク エラー|関数が完了した処理の前に、ドライバーとドライバーが接続されているデータ ソース間の通信リンクに失敗しました。|  
|HY000|一般的なエラー|これがなかった固有の SQLSTATE とする実装に固有の SQLSTATE が定義されていない、エラーが発生しました。 によって返されるエラー メッセージ**SQLGetDiagRec**で、  *\*MessageText*バッファーは、エラーとその原因について説明します。|  
|HY001|メモリの割り当てエラー|ドライバーは、実行または関数の完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY007|関連付けられているステートメントが準備されていません|*DescriptorHandle*に関連付けられているが、 *StatementHandle* IRD のと関連付けられているステートメント ハンドルがないされて準備または実行されます。|  
|HY010|関数のシーケンス エラー|(DM) *DescriptorHandle*に関連付けられているが、 *StatementHandle*に (このない) 非同期的に実行中の関数が呼び出されたこの関数が呼び出されたときに実行されています。<br /><br /> (DM) *DescriptorHandle*に関連付けられているが、 *StatementHandle*を**SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**、または**SQLSetPos**が呼び出され、SQL_NEED_DATA が返されます。 すべての実行時データ パラメーターまたは列のデータが送信される前に、この関数が呼び出されました。<br /><br /> (DM) を非同期的に実行中の関数が呼び出された接続ハンドルに関連付けられているため、 *DescriptorHandle*します。 この非同期関数ではときに実行されている、 **SQLGetDescField**関数が呼び出されました。|  
|HY013|メモリ管理エラー|基になるメモリ オブジェクトにアクセスできませんでした、場合によってメモリ不足が原因であるために、関数呼び出しを処理できませんでした。|  
|HY021|不整合な記述子情報|(Apd の標準) は、SQL_DESC_TYPE と SQL_DESC_DATETIME_INTERVAL_CODE フィールドは、有効な ODBC SQL 型、有効なドライバー固有 SQL 型 (Ipd)、または有効な ODBC C データ型は形成してしません。|  
|HY090|文字列またはバッファーの長さが無効です。|(DM)  *\*ValuePtr*された文字の文字列と*BufferLength* 0 未満でした。|  
|HY091|無効な記述子フィールドの識別子|*FieldIdentifier*でした、ODBC で定義されたフィールドとしましたが、実装定義の値でした。<br /><br /> *FieldIdentifier*が undefined を*DescriptorHandle*します。|  
|HY117|不明なトランザクションの状態のため、接続が中断されます。 のみを切断して、読み取り専用の関数が許可されます。|(DM) 中断状態の詳細については、次を参照してください。 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)します。|  
|HYT01|接続がタイムアウトしました|データ ソースが要求に応答する前に、接続のタイムアウト期間が終了しました。 によって、接続タイムアウト期間が設定されます**SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT します。|  
|IM001|ドライバーでは、この関数はサポートされていません|(DM) に、ドライバーが関連付けられている、 *DescriptorHandle*関数をサポートしていません。|  
  
## <a name="comments"></a>コメント  
 アプリケーションが呼び出すことができます**SQLGetDescField**記述子レコードの 1 つのフィールドの値を返します。 呼び出し**SQLGetDescField**ヘッダー フィールド、レコードのフィールド、およびブックマークのフィールドを含む、記述子の型のいずれかのフィールドの設定を返すことができます。 アプリケーションでは、任意の順序で、同じまたは別の記述子の複数のフィールドの設定を繰り返し呼び出すことで取得できます**SQLGetDescField**します。 **SQLGetDescField**ドライバーの定義済みの記述子フィールドを返す呼び出すこともできます。  
  
 パフォーマンス上の理由から、アプリケーションを呼び出す必要がありますいない**SQLGetDescField**ステートメントを実行する前に、IRD の。  
  
 名前、データ型、および列またはパラメーターのデータのストレージを記述する複数のフィールドの設定は、1 回の呼び出しでも取得できます**SQLGetDescRec**します。 **SQLGetStmtAttr**ステートメント属性になっている記述子のヘッダーの 1 つのフィールドの設定を取得するということができます。 **SQLColAttribute**、 **SQLDescribeCol**、および**SQLDescribeParam**ブックマークのレコードまたはフィールドを取得します。  
  
 アプリケーションを呼び出すと**SQLGetDescField**は特定の記述子の型に対して定義されていないフィールドの値を取得する関数が SQL_SUCCESS を返しますが、フィールドに返される値は定義されません。 たとえば、呼び出し**SQLGetDescField** APD または ARD の SQL_DESC_NAME または SQL_DESC_NULLABLE フィールドについては、SQL_SUCCESS が未定義のフィールドの値は返します。  
  
 アプリケーションを呼び出すと**SQLGetDescField**関数は、値が SQL_SUCCESS が返されるを返します特定の記述子の型に対して定義されているが、既定値を持たないをまだ設定されていないフィールドの値を取得するにはフィールドは定義されません。 記述子フィールドとフィールドの説明の初期化の詳細については、「記述子フィールドの初期化」を参照してください[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)します。 記述子の詳細については、次を参照してください。[記述子](../../../odbc/reference/develop-app/descriptors.md)します。  
  
## <a name="related-functions"></a>関連する関数  
  
|詳細|参照先|  
|---------------------------|---------|  
|複数の記述子フィールドの取得|[SQLGetDescRec 関数](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|1 つの記述子フィールドの設定|[SQLSetDescField 関数](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|複数の記述子フィールドの設定|[SQLSetDescRec 関数](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
  
## <a name="see-also"></a>参照  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)
