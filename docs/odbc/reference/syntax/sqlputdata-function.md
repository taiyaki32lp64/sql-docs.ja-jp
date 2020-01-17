---
title: SQLPutData 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLPutData
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLPutData
helpviewer_keywords:
- SQLPutData function [ODBC]
ms.assetid: 9a60f004-1477-4c54-a20c-7378e1116713
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 676f9fb526996e96b27bb758a7343c86afaac460
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68053650"
---
# <a name="sqlputdata-function"></a>SQLPutData 関数
**準拠**  
 バージョンが導入されました。ODBC 1.0 規格に準拠します。ISO 92  
  
 **まとめ**  
 **SQLPutData**により、ステートメントの実行時にドライバーをパラメーターまたは列のデータを送信するアプリケーション。 この関数は、部分の文字、バイナリ、またはデータ ソースに固有のデータ型 (たとえば、SQL_LONGVARBINARY、SQL_LONGVARCHAR または型のパラメーター) の列に文字またはバイナリ データ値を送信する使用できます。 **SQLPutData**基になるドライバーが Unicode データをサポートしていない場合でも、Unicode の C データ型へのバインドをサポートしています。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLPutData(  
      SQLHSTMT     StatementHandle,  
      SQLPOINTER   DataPtr,  
      SQLLEN       StrLen_or_Ind);  
```  
  
## <a name="arguments"></a>引数  
 *StatementHandle*  
 [入力]ステートメント ハンドルです。  
  
 *DataPtr*  
 [入力]パラメーターまたは列の実際のデータを格納するバッファーへのポインター。 データがで指定された C データ型である必要があります、 *ValueType*の引数**SQLBindParameter** (のパラメーターのデータ)、または*TargetType*の引数**SQLBindCol** (の列のデータ)。  
  
 *StrLen_or_Ind*  
 [入力]長さ\* *DataPtr*します。 呼び出しに送信されるデータ量を指定します**SQLPutData**します。 データの量は、指定されたパラメーターまたは列の各呼び出しで異なります。 *StrLen_or_Ind*次の条件のいずれかを満たしていない場合は無視されます。  
  
-   *StrLen_or_Ind*は SQL_NTS、SQL_NULL_DATA、または SQL_DEFAULT_PARAM します。  
  
-   C データ型がで指定された**SQLBindParameter**または**SQLBindCol** SQL_C_CHAR または SQL_C_BINARY です。  
  
-   C データ型は SQL_C_DEFAULT、および指定した SQL データ型の既定の C データ型は、SQL_C_CHAR または SQL_C_BINARY します。  
  
 他のすべての種類を C のデータの場合*StrLen_or_Ind* SQL_NULL_DATA または SQL_DEFAULT_PARAM ではないことが前提とドライバーのサイズ、 \* *DataPtr*バッファーが指定された C データ型のサイズ*ValueType*または*TargetType*データ値全体を送信します。 詳細については、次を参照してください[C から SQL データ型への変換データ](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)付録 d:。データ型。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_STILL_EXECUTING、SQL_ERROR、または SQL_INVALID_HANDLE します。  
  
## <a name="diagnostics"></a>診断  
 ときに**SQLPutData** SQL_ERROR または SQL_SUCCESS_WITH_INFO、関連付けられている SQLSTATE 値を返しますを呼び出すことによって取得できる**SQLGetDiagRec**で、 *HandleType* sql _ のHANDLE_STMT と*処理*の*StatementHandle*します。 次の表に、一般的にによって返される SQLSTATE 値**SQLPutData** ; この関数のコンテキストでそれぞれについて説明しますと表記"(DM)"の前にドライバー マネージャーによって返されるについての説明。 SQLSTATE 値ごとに関連付けられているリターン コードは明記しない限り、SQL_ERROR です。  
  
|SQLSTATE|[エラー]|説明|  
|--------------|-----------|-----------------|  
|01000|一般的な警告|ドライバー固有の情報メッセージです。 (関数は、SQL_SUCCESS_WITH_INFO を返します)。|  
|01004|文字列データで、右側が切り捨てられました|文字列またはバイナリ データが出力パラメーターに対して返される空白文字または NULL 以外のバイナリ データの切り捨てが発生しました。 文字列値がいた場合は、右側から切り捨てられますことでした。 (関数は、SQL_SUCCESS_WITH_INFO を返します)。|  
|07006|制限付きのデータ型の属性違反|識別されるデータ値、 *ValueType*引数**SQLBindParameter**のバインドされたパラメーターがで識別されるデータ型に変換できませんでした、 *ParameterType*引数**SQLBindParameter**します。|  
|07S01|既定のパラメーターの使い方が正しくありません。|パラメーターの値の設定で**SQLBindParameter**が SQL_DEFAULT_PARAM、および対応するパラメーターは、既定値はありませんでした。|  
|08S01|通信リンク エラー|関数が完了した処理の前に、ドライバーとドライバーが接続されているデータ ソース間の通信リンクに失敗しました。|  
|22001|文字列データの右側が切り捨てられました|文字値または列にバイナリ値の割り当ては、空白 (文字) または null 以外 (バイナリ) の文字またはバイトの切り捨てが発生しました。<br /><br /> SQL_NEED_LONG_DATA_LEN 情報の種類で**SQLGetInfo**が"Y"と指定された以外 (データ型は SQL_LONGVARCHAR、SQL_LONGVARBINARY、または長い形式のデータ ソースに固有のデータ型)、long 型パラメーターのより多くのデータが送信されました。*StrLen_or_IndPtr*引数**SQLBindParameter**します。<br /><br /> SQL_NEED_LONG_DATA_LEN 情報の種類で**SQLGetInfo** "Y"で指定された数より長い列 (データ型は SQL_LONGVARCHAR、SQL_LONGVARBINARY、または長い形式のデータ ソースに固有のデータ型) のより多くのデータが送信された、追加または更新されたデータの行の列に対応する長バッファー **SQLBulkOperations**またはで更新された**SQLSetPos**します。|  
|22003|数値が範囲外|列に関連付けられているテーブル列に割り当てられたときに切り詰められる数値の (ではなく小数部) 全体の一部が原因となったまたはバインドされている数値パラメーターのデータが送信されます。<br /><br /> 1 つまたは複数の入力/出力または出力パラメーター (数値または文字列) としての数値の値が返される原因となる (ではなく小数部) 整数部分が切り捨てられる数値。|  
|22007|無効な datetime 形式|それぞれ、無効な日付、時刻、またはタイムスタンプ パラメーターまたは列の日付、時刻、またはタイムスタンプの構造体にバインドされた送信されるデータがでした。<br /><br /> または入力/出力の出力パラメーターは、日付、時刻、またはタイムスタンプ C 構造体にバインドされていたし、返されるパラメーターの値が、それぞれ、無効な日付、時刻、またはタイムスタンプ。 (関数は、SQL_SUCCESS_WITH_INFO を返します)。|  
|22008|Datetime フィールド オーバーフロー|Datetime 式が入力/出力の計算または出力パラメーターの日付、時刻、または無効なタイムスタンプ C の構造体が発生しました。|  
|22012|0 による除算|算術式の入力/出力の計算または 0 による除算で出力パラメーターが発生しました。|  
|22015|Interval フィールド オーバーフロー|間隔 SQL データ型にパラメーターの有効桁数が失われる原因となったまたは正確な数値または間隔の列のデータが送信されます。<br /><br /> データは、間隔の列または複数のフィールドを持つパラメーターの送信された、数値データ型に変換された、および数値データ型の表現がなかった。<br /><br /> 列に送信されるデータまたはパラメーターのデータは、SQL 型、期間に割り当てられたし、SQL の種類の間隔で C 型の値の表現はありませんでした。<br /><br /> 正確な numeric または間隔 C 列またはパラメーター C の間隔の種類を送信するデータには、有効桁数の損失が発生します。<br /><br /> 列に送信されるデータまたはパラメーターのデータは、間隔 C 構造体に割り当てられたし、間隔のデータ構造内のデータの表現はありませんでした。|  
|22018|キャストの無効な文字の値|C 型は、真数または概数の数値、datetime、またはデータ間隔の種類。列の SQL 型が文字データ型。列またはパラメーターの値がバインドされた C 型の有効なリテラルではありませんでした。<br /><br /> SQL 型が、真数または概数の数値、datetime、またはデータ間隔の種類。C 型が SQL_C_CHAR;列またはパラメーターの値がバインドされた SQL 型の有効なリテラルではありませんでした。|  
|HY000|一般的なエラー|これがなかった固有の SQLSTATE とする実装に固有の SQLSTATE が定義されていない、エラーが発生しました。 によって返されるエラー メッセージ**SQLGetDiagRec**で、  *\*MessageText*バッファーは、エラーとその原因について説明します。|  
|HY001|メモリの割り当てエラー|ドライバーは、実行または関数の完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY008|操作が取り消されました|非同期処理が有効に、 *StatementHandle*します。 関数が呼び出された、および実行を完了する前に**SQLCancel**または**SQLCancelHandle**が呼び出されて、 *StatementHandle*します。 後でもう一度関数が呼び出された、 *StatementHandle*します。<br /><br /> 関数が呼び出された、および実行を完了する前に**SQLCancel**または**SQLCancelHandle**が呼び出されて、 *StatementHandle*から別のスレッドで、マルチ スレッド アプリケーションです。|  
|HY009|無効な null ポインターの使用|(DM) 引数*DataPtr*が null ポインターの場合は、および引数*StrLen_or_Ind*でした SQL_DEFAULT_PARAM、または SQL_NULL_DATA は 0。|  
|HY010|関数のシーケンス エラー|(DM) 前の関数呼び出しはへの呼び出しではない**SQLPutData**または**SQLParamData**します。<br /><br /> (DM) を非同期的に実行中の関数が呼び出された接続ハンドルに関連付けられているため、 *StatementHandle*します。 この非同期関数は、SQLPutData 関数が呼び出されたときにまだ実行中だった。<br /><br /> (DM) **SQLExecute**、 **SQLExecDirect**、または**SQLMoreResults**に対して呼び出された、 *StatementHandle* SQL_PARAM_DATA_ を返されます。ご利用いただけます。 ストリームのすべてのパラメーターのデータが取得される前に、この関数が呼び出されました。<br /><br /> (DM) を非同期的に実行中の関数 (いないこの"1") が呼び出された、 *StatementHandle*この関数が呼び出されたときに実行されているとします。|  
|HY013|メモリ管理エラー|基になるメモリ オブジェクトにアクセスできませんでした、場合によってメモリ不足が原因であるために、関数呼び出しを処理できませんでした。|  
|HY019|部分で送信される文字またはバイナリ以外のデータ|**SQLPutData**が呼び出された複数の 1 回のパラメーターまたは列、およびそれが使用されていない文字、バイナリ、またはデータのソースに固有のデータ型の列に文字データを送信する、または文字の列にバイナリの C データを送信するには、バイナリ、またはデータ ソースに固有のデータ型。|  
|HY020|Null 値を連結しようとしてください。|**SQLPutData** 、SQL_NEED_DATA が返されますの呼び出し後、これらの呼び出しのいずれかで複数回呼び出された、 *StrLen_or_Ind* SQL_NULL_DATA または SQL_DEFAULT_PARAM 引数が含まれています。|  
|HY090|文字列またはバッファーの長さが無効です。|引数*DataPtr*が null ポインターの場合は、および引数*StrLen_or_Ind* SQL_NTS または SQL_NULL_DATA 等しくありませんが、0 より小さいをでした。|  
|HY117|不明なトランザクションの状態のため、接続が中断されます。 のみを切断して、読み取り専用の関数が許可されます。|(DM) 中断状態の詳細については、次を参照してください。 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)します。|  
|HYT01|接続がタイムアウトしました|データ ソースが要求に応答する前に、接続のタイムアウト期間が終了しました。 によって、接続タイムアウト期間が設定されます**SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT します。|  
|IM001|ドライバーでは、この関数はサポートされていません|(DM) に、ドライバーが関連付けられている、 *StatementHandle*関数をサポートしていません。|  
|IM017|非同期通知モードでのポーリングは無効です。|通知のモデルを使用すると、常にポーリングは無効です。|  
|IM018|**SQLCompleteAsync**このハンドルに対する前の非同期操作を完了が呼び出されていません。|通知モードが有効になっている場合、ハンドルでは、前の関数呼び出しに SQL_STILL_EXECUTING が返された場合と**SQLCompleteAsync**後処理を行い、操作を完了するハンドルで呼び出す必要があります。|  
  
 場合**SQLPutData**と呼ばれますが、SQL ステートメントでパラメーターのデータを送信中に、ステートメントを実行すると呼ばれる関数によって返される任意の SQLSTATE を返すこと (**SQLExecute**または**SQLExecDirect**)。 列のデータを送信中に呼び出された場合更新または追加**SQLBulkOperations**で更新されているまたは**SQLSetPos**、によって返される任意の SQLSTATE を返すことができます**SQLBulkOperations**または**SQLSetPos**します。  
  
## <a name="comments"></a>コメント  
 **SQLPutData**実行時のデータのデータを 2 つの使用を提供するということができますパラメーターのデータへの呼び出しで使用される**SQLExecute**または**SQLExecDirect**、または行が更新されたときに使用される列のデータ。呼び出しで追加または**SQLBulkOperations**への呼び出しによって更新または**SQLSetPos**します。  
  
 アプリケーションを呼び出すと**SQLParamData**データを決定する送信先と、ドライバーは、アプリケーションは、パラメーター データを送信する決定に使用できる、または列のデータがあるインジケーターを返します。 また、インジケーターを呼び出す必要があるアプリケーションには、SQL_NEED_DATA を返します**SQLPutData**データを送信します。 *DataPtr*引数**SQLPutData**、アプリケーション パラメーターまたは列の実際のデータを格納するバッファーへのポインターを渡します。  
  
 ドライバーに関係なく SQL_SUCCESS を返しますと**SQLPutData**、アプリケーション呼び出し**SQLParamData**もう一度です。 **SQLParamData** SQL_NEED_DATA より多くのデータを送信する必要がある場合は、アプリケーションが返されます**SQLPutData**もう一度です。 実行時のデータのすべてのデータが送信された場合は関係なく SQL_SUCCESS を返します。 その後、アプリケーションを呼び出す**SQLParamData**もう一度です。 ドライバーが SQL_NEED_DATA とで別のインジケーターを返す場合 *\*ValuePtrPtr*、もう 1 つのパラメーターまたは列にデータを必要と**SQLPutData**が再度呼び出されます。 データが送信され、SQL ステートメントを実行することができる場合ドライバー SQL_SUCCESS を返します、し、すべての実行時データまたは**SQLBulkOperations**または**SQLSetPos**呼び出しを処理できます。  
  
 方法の実行時データ パラメーターのデータの詳細については、ステートメントの実行時に渡されるを参照してください「パラメーターの値を渡す」で[SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)と[長い形式のデータを送信する](../../../odbc/reference/develop-app/sending-long-data.md)します。 詳細については、方法、実行時データ列のデータが更新または追加を参照してください"を使用して SQLSetPos" [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)、「を実行する一括更新プログラムを使用してブックマーク」で[SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)と[長い形式のデータ、SQLSetPos および SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)します。  
  
> [!NOTE]  
>  アプリケーションで使用できます**SQLPutData**文字、バイナリ、またはデータのソースに固有のデータ型の列に文字データを送信するときにのみ、または列が文字、バイナリ、C のバイナリ データを送信するときに、部分のデータまたはデータを送信するにはソースに固有のデータを入力します。 場合**SQLPutData**というが複数回、他の条件下で SQL_ERROR と返す SQLSTATE HY019 (文字またはバイナリ以外のデータが分割されて送信されました)。  
  
## <a name="example"></a>例  
 次の例は、テストと呼ばれるデータ ソース名を想定しています。 関連付けられているデータベースには、次のように、作成できるテーブルが必要です。  
  
```sql  
CREATE TABLE emp4 (NAME char(30), AGE int, BIRTHDAY datetime, Memo1 text)  
```  
  
```cpp  
// SQLPutData.cpp  
// compile with: odbc32.lib user32.lib  
#include <stdio.h>  
#include <windows.h>  
#include <sqlext.h>  
#include <odbcss.h>  
  
#define TEXTSIZE  12000  
#define MAXBUFLEN 256  
  
SQLHENV henv = SQL_NULL_HENV;  
SQLHDBC hdbc1 = SQL_NULL_HDBC;       
SQLHSTMT hstmt1 = SQL_NULL_HSTMT;  
  
void Cleanup() {  
   if (hstmt1 != SQL_NULL_HSTMT)  
      SQLFreeHandle(SQL_HANDLE_STMT, hstmt1);  
  
   if (hdbc1 != SQL_NULL_HDBC) {  
      SQLDisconnect(hdbc1);  
      SQLFreeHandle(SQL_HANDLE_DBC, hdbc1);  
   }  
  
   if (henv != SQL_NULL_HENV)  
      SQLFreeHandle(SQL_HANDLE_ENV, henv);  
}  
  
int main() {  
   RETCODE retcode;  
  
   // SQLBindParameter variables.  
   SQLLEN cbTextSize, lbytes;  
  
   // SQLParamData variable.  
   PTR pParmID;  
  
   // SQLPutData variables.  
   UCHAR  Data[] =   
      "abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz"  
      "abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz"  
      "abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz"  
      "abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz"  
      "abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz"  
      "abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz"  
      "abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz"  
      "abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz"  
      "abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz"  
      "abcdefghijklmnopqrstuvwxyz";  
  
   SDWORD cbBatch = (SDWORD)sizeof(Data) - 1;  
  
   // Allocate the ODBC environment and save handle.  
   retcode = SQLAllocHandle (SQL_HANDLE_ENV, NULL, &henv);  
   if ( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLAllocHandle(Env) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Notify ODBC that this is an ODBC 3.0 app.  
   retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER) SQL_OV_ODBC3, SQL_IS_INTEGER);  
   if ( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLSetEnvAttr(ODBC version) Failed\n\n");  
      Cleanup();  
      return(9);      
   }  
  
   // Allocate ODBC connection handle and connect.  
   retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc1);  
   if ( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLAllocHandle(hdbc1) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Sample uses Integrated Security, create SQL Server DSN using Windows NT authentication.   
   retcode = SQLConnect(hdbc1, (UCHAR*)"Test", SQL_NTS, (UCHAR*)"",SQL_NTS, (UCHAR*)"", SQL_NTS);  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLConnect() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Allocate statement handle.  
   retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc1, &hstmt1);  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLAllocHandle(hstmt1) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Set parameters based on total data to send.  
   lbytes = (SDWORD)TEXTSIZE;  
   cbTextSize = SQL_LEN_DATA_AT_EXEC(lbytes);  
  
   // Bind the parameter marker.  
   retcode = SQLBindParameter (hstmt1,           // hstmt  
                               1,                // ipar  
                               SQL_PARAM_INPUT,  // fParamType  
                               SQL_C_CHAR,       // fCType  
                               SQL_LONGVARCHAR,  // FSqlType  
                               lbytes,           // cbColDef  
                               0,                // ibScale  
                               (VOID *)1,        // rgbValue  
                               0,                // cbValueMax  
                               &cbTextSize);     // pcbValue  
  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLBindParameter Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Execute the command.  
   retcode =   
      SQLExecDirect(hstmt1, (UCHAR*)"INSERT INTO emp4 VALUES('Paul Borm', 46,'1950-11-12 00:00:00', ?)", SQL_NTS);  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_NEED_DATA) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLExecDirect Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Check to see if NEED_DATA; if yes, use SQLPutData.  
   retcode = SQLParamData(hstmt1, &pParmID);  
   if (retcode == SQL_NEED_DATA) {  
      while (lbytes > cbBatch) {  
         SQLPutData(hstmt1, Data, cbBatch);  
         lbytes -= cbBatch;  
      }  
      // Put final batch.  
      retcode = SQLPutData(hstmt1, Data, lbytes);   
   }  
  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLParamData Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Make final SQLParamData call.  
   retcode = SQLParamData(hstmt1, &pParmID);  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("Final SQLParamData Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Clean up.  
   SQLFreeHandle(SQL_HANDLE_STMT, hstmt1);  
   SQLDisconnect(hdbc1);  
   SQLFreeHandle(SQL_HANDLE_DBC, hdbc1);  
   SQLFreeHandle(SQL_HANDLE_ENV, henv);  
}  
```  
  
## <a name="related-functions"></a>関連する関数  
  
|詳細|参照先|  
|---------------------------|---------|  
|バッファーをパラメーターにバインドします。|[SQLBindParameter 関数](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|ステートメントの処理をキャンセル|[SQLCancel 関数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|SQL ステートメントを実行します。|[SQLExecDirect 関数](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|準備された SQL ステートメントを実行します。|[SQLExecute 関数](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|データを送信する次のパラメーターを返す|[SQLParamData 関数](../../../odbc/reference/syntax/sqlparamdata-function.md)|  
  
## <a name="see-also"></a>参照  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)
