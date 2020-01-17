---
title: SQLDescribeCol 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLDescribeCol
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLDescribeCol
helpviewer_keywords:
- SQLDescribeCol function [ODBC]
ms.assetid: eddef353-83f3-4a3c-8f24-f9ed888890a4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 63982d87f0dbbe0c8ab1a540185e298d9943f630
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68104789"
---
# <a name="sqldescribecol-function"></a>SQLDescribeCol 関数
**準拠**  
 バージョンが導入されました。ODBC 1.0 規格に準拠します。ISO 92  
  
 **まとめ**  
 **SQLDescribeCol**結果セットの 1 つの列に列名、型、列のサイズ、10 進数字、および null 値の許容 - 結果記述子を返します。 この情報もは、ird フィールドにします。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLDescribeCol(  
      SQLHSTMT       StatementHandle,  
      SQLUSMALLINT   ColumnNumber,  
      SQLCHAR *      ColumnName,  
      SQLSMALLINT    BufferLength,  
      SQLSMALLINT *  NameLengthPtr,  
      SQLSMALLINT *  DataTypePtr,  
      SQLULEN *      ColumnSizePtr,  
      SQLSMALLINT *  DecimalDigitsPtr,  
      SQLSMALLINT *  NullablePtr);  
```  
  
## <a name="arguments"></a>引数  
 *StatementHandle*  
 [入力]ステートメント ハンドルです。  
  
 *ColumnNumber*  
 [入力]結果のデータの列数は、1 から始まる、増加の列の順序で順番に順序付けします。 *ColumnNumber*ブックマーク列を記述する引数が 0 に設定することもできます。  
  
 *[ColumnName]*  
 [出力]列名を取得するための null で終わるバッファーへのポインター。 この値は、IRD の SQL_DESC_NAME フィールドから読み取られます。 列が名前付きか、列名が確認できない場合、ドライバーは、空の文字列を返します。  
  
 場合*ColumnName*が null の場合、 *NameLengthPtr*はまだ文字 (文字データの null 終端文字を除く) の合計数を返しますが指すバッファーに返される使用可能な*ColumnName*します。  
  
 *BufferLength*  
 [入力]長さ、**ColumnName*文字のバッファー。  
  
 *NameLengthPtr*  
 [出力]文字 (終端の null を除く) の合計数を返すバッファーへのポインターで返される使用可能な\* *ColumnName*します。 返すに使用できる文字数がより大きいかに等しい場合*BufferLength*、内の列名\* *ColumnName*に切り捨てられます*BufferLength*null 終了文字の長さマイナスです。  
  
 *DataTypePtr*  
 [出力]列の SQL データ型を返すバッファーへのポインター。 この値は、IRD の SQL_DESC_CONCISE_TYPE フィールドから読み取られます。 内の値の 1 つ[SQL データ型](../../../odbc/reference/appendixes/sql-data-types.md)、またはドライバーに固有の SQL データ型。 データ型を決定できない場合、ドライバーは SQL_UNKNOWN_TYPE を返します。  
  
 ODBC 3。*x*、SQL_TYPE_DATE、SQL_TYPE_TIME、または SQL_TYPE_TIMESTAMP がで返される *\*DataTypePtr*の日付、時刻、またはタイムスタンプ データ、ODBC 2 にそれぞれ;.*x*SQL_DATE、SQL_TIME、または SQL_TIMESTAMP が返されます。 ドライバー マネージャーは、ODBC 2 時に、必要なマッピングを実行します。*x*アプリケーションは、ODBC 3 の操作します *。x*ドライバーまたはとき、ODBC 3 *。x* ODBC 2 を利用するアプリケーション *。x*ドライバー。  
  
 ときに*ColumnNumber*と等しいで返される SQL_BINARY (ブックマーク列) を 0 に *\*DataTypePtr*の可変長のブックマーク。 (SQL_INTEGER は ODBC の 3 つのブックマークを使用する場合に返されます。*x* ODBC 2 を使用するアプリケーション *。x*ドライバーまたは ODBC 2 *。x*アプリケーションは、ODBC 3 の操作します *。x*ドライバー)。  
  
 これらのデータ型の詳細については、次を参照してください[SQL データ型](../../../odbc/reference/appendixes/sql-data-types.md)付録 d:。データ型。 ドライバー固有の SQL データ型については、ドライバーのドキュメントを参照してください。  
  
 *ColumnSizePtr*  
 [出力]データ ソースの列の文字) 単位でサイズを返すバッファーへのポインター。 列のサイズを決定できない場合、ドライバーは、0 を返します。 列のサイズの詳細については、次を参照してください[列のサイズ、10 進数字、転送オクテット長、および表示サイズ](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)付録 d:。データ型。  
  
 *DecimalDigitsPtr*  
 [出力]データ ソースの列の 10 進数字の数を返すバッファーへのポインター。 10 進数字の数が特定できないまたは適用可能でない、ドライバーは 0 を返します。 10 進数字の詳細については、次を参照してください[列のサイズ、10 進数字、転送オクテット長、および表示サイズ](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)付録 d:。データ型。  
  
 *NullablePtr*  
 [出力]列が NULL 値を許容するかどうかを示す値を返すバッファーへのポインター。 この値は、IRD の SQL_DESC_NULLABLE フィールドから読み取られます。 値は次のいずれかになります。  
  
 SQL_NO_NULLS:その列には NULL 値が許容されていません。  
  
 SQL_NULLABLE:列が NULL 値を許容します。  
  
 SQL_NULLABLE_UNKNOWN:列が NULL 値を許容するかどうか、ドライバーを特定できません。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_STILL_EXECUTING、SQL_ERROR、または SQL_INVALID_HANDLE します。  
  
## <a name="diagnostics"></a>診断  
 ときに**SQLDescribeCol** SQL_ERROR または SQL_SUCCESS_WITH_INFO のいずれかを返します呼び出すことによって、関連付けられた SQLSTATE 値を取得できる**SQLGetDiagRec**で、 *HandleType*sql_handle_stmt としての*処理*の*StatementHandle*します。 次の表に、一般的にによって返される SQLSTATE 値**SQLDescribeCol** ; この関数のコンテキストでそれぞれについて説明しますと表記"(DM)"の前にドライバー マネージャーによって返されるについての説明。 SQLSTATE 値ごとに関連付けられているリターン コードは明記しない限り、SQL_ERROR です。  
  
|SQLSTATE|[エラー]|説明|  
|--------------|-----------|-----------------|  
|01000|一般的な警告|ドライバー固有の情報メッセージです。 (関数は、SQL_SUCCESS_WITH_INFO を返します)。|  
|01004|文字列データで、右側が切り捨てられました|バッファー \* *ColumnName*を列名は切り詰められましたように列全体の名前を返すのに十分な大きさがありません。 切り詰められていない列名の長さが返される **NameLengthPtr*します。 (関数は、SQL_SUCCESS_WITH_INFO を返します)。|  
|07005|準備されたステートメントがない、*カーソルの指定*|関連付けられているステートメント、 *StatementHandle*結果セットを返しませんでした。 記述する列がありませんでした。|  
|07009|無効な記述子のインデックス|引数に指定された (DM) 値*ColumnNumber*を 0 に等しい、SQL_ATTR_USE_BOOKMARKS ステートメントのオプションが SQL_UB_OFF をでした。<br /><br /> 引数が指定された値*ColumnNumber*が結果セット内の列の数を超えていました。|  
|08S01|通信リンク エラー|関数が完了した処理の前に、ドライバーとドライバーが接続されているデータ ソース間の通信リンクに失敗しました。|  
|HY000|一般的なエラー|これがなかった固有の SQLSTATE とする実装に固有の SQLSTATE が定義されていない、エラーが発生しました。 によって返されるエラー メッセージ**SQLGetDiagRec**で、  *\*MessageText*バッファーは、エラーとその原因について説明します。|  
|HY001|メモリ割り当てに失敗しました|ドライバーは、実行または関数の完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY008|操作が取り消されました|非同期処理が有効に、 *StatementHandle*します。 関数が呼び出された、および実行を完了する前に**SQLCancel**または**SQLCancelHandle**が呼び出されて、 *StatementHandle*します。 後でもう一度関数が呼び出された、 *StatementHandle*します。<br /><br /> 関数が呼び出された、および実行を完了する前に**SQLCancel**または**SQLCancelHandle**が呼び出されて、 *StatementHandle*から別のスレッドで、マルチ スレッド アプリケーションです。|  
|HY010|関数のシーケンス エラー|(DM) を非同期的に実行中の関数が呼び出された接続ハンドルに関連付けられているため、 *StatementHandle*します。 この非同期関数ではときに実行されている**SQLDescribeCol**が呼び出されました。<br /><br /> (DM) **SQLExecute**、 **SQLExecDirect**、または**SQLMoreResults**に対して呼び出された、 *StatementHandle* SQL_PARAM_DATA_ を返されます。ご利用いただけます。 ストリームのすべてのパラメーターのデータが取得される前に、この関数が呼び出されました。<br /><br /> (DM) を非同期的に実行中の関数 (いないこの"1") が呼び出された、 *StatementHandle*この関数が呼び出されたときに実行されているとします。<br /><br /> (DM) 関数が呼び出す前に呼び出された**SQLPrepare**、 **SQLExecute**、またはステートメント ハンドルでのカタログ関数。<br /><br /> (DM) **SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**、または**SQLSetPos**に対して呼び出された、 *StatementHandle* SQL_NEED_DATA が返されます。 すべての実行時データ パラメーターまたは列のデータが送信される前に、この関数が呼び出されました。|  
|HY013|メモリ管理エラー|基になるメモリ オブジェクトにアクセスできませんでした、場合によってメモリ不足が原因であるために、関数呼び出しを処理できませんでした。|  
|HY090|文字列またはバッファーの長さが無効です。|引数に指定された (DM) 値*BufferLength*が 0 未満でした。|  
|HY117|不明なトランザクションの状態のため、接続が中断されます。 のみを切断して、読み取り専用の関数が許可されます。|(DM) 中断状態の詳細については、次を参照してください。 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)します。|  
|HYT01|接続がタイムアウトしました|データ ソースが要求に応答する前に、接続のタイムアウト期間が終了しました。 によって、接続タイムアウト期間が設定されます**SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT します。|  
|IM001|ドライバーでは、この関数はサポートされていません|(DM) に、ドライバーが関連付けられている、 *StatementHandle*関数をサポートしていません。|  
|IM017|非同期通知モードでのポーリングは無効です。|通知のモデルを使用すると、常にポーリングは無効です。|  
|IM018|**SQLCompleteAsync**このハンドルに対する前の非同期操作を完了が呼び出されていません。|通知モードが有効になっている場合、ハンドルでは、前の関数呼び出しに SQL_STILL_EXECUTING が返された場合と**SQLCompleteAsync**後処理を行い、操作を完了するハンドルで呼び出す必要があります。|  
  
 **SQLDescribeCol**によって返される任意の SQLSTATE を返すことができます**SQLPrepare**または**SQLExecute**後に呼び出されたときに**SQLPrepare** 前**SQLExecute**にデータ ソースが、ステートメント ハンドルに関連付けられている SQL ステートメントを評価するときに依存します。  
  
 パフォーマンス上の理由から、アプリケーションを呼び出す必要がありますいない**SQLDescribeCol**ステートメントを実行する前にします。  
  
## <a name="comments"></a>コメント  
 アプリケーションを呼び出す通常**SQLDescribeCol**呼び出しの後に**SQLPrepare**の前に、または後に関連付けられている呼び出し**SQLExecute**します。 アプリケーションを呼び出すことも**SQLDescribeCol**呼び出しの後に**SQLExecDirect**します。 詳細については、次を参照してください。[結果セットのメタデータ](../../../odbc/reference/develop-app/result-set-metadata.md)します。  
  
 **SQLDescribeCol**列名、型、およびによって生成される長さを取得、**選択**ステートメント。 列が式の場合 **ColumnName*が空の文字列またはドライバーの定義の名前。  
  
> [!NOTE]  
>  ODBC では、Open Group と SQL アクセス グループ呼び出しレベル インターフェイス仕様のオプションを指定しない場合でも、拡張機能として SQL_NULLABLE_UNKNOWN をサポート**SQLDescribeCol**します。  
  
## <a name="related-functions"></a>関連する関数  
  
|詳細|参照先|  
|---------------------------|---------|  
|バッファーを結果セット内の列にバインドします。|[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|ステートメントの処理をキャンセル|[SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|結果セット内の列に関する情報を返す|[SQLColAttribute](../../../odbc/reference/syntax/sqlcolattribute-function.md)|  
|複数行のデータをフェッチしています|[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|結果の数を返すセットの列|[SQLNumResultCols](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
|実行するステートメントを準備します。|[SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)|  
  
## <a name="see-also"></a>参照  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)
