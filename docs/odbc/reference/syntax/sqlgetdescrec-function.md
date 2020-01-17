---
title: SQLGetDescRec 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetDescRec
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetDescRec
helpviewer_keywords:
- SQLGetDescRec function [ODBC]
ms.assetid: 325e0907-8e87-44e8-a111-f39e636a9cbc
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c27b16d8b72e289f66a051cb2710004f72309599
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68103795"
---
# <a name="sqlgetdescrec-function"></a>SQLGetDescRec 関数
**準拠**  
 バージョンが導入されました。ODBC 3.0 規格に準拠します。ISO 92  
  
 **概要**  
 **SQLGetDescRec**現在の設定または記述子レコードの複数のフィールドの値を返します。 返されるフィールドは、名前、データ型、および列またはパラメーターのデータの格納について説明します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLGetDescRec(  
      SQLHDESC        DescriptorHandle,  
      SQLSMALLINT     RecNumber,  
      SQLCHAR *       Name,  
      SQLSMALLINT     BufferLength,  
      SQLSMALLINT *   StringLengthPtr,  
      SQLSMALLINT *   TypePtr,  
      SQLSMALLINT *   SubTypePtr,  
      SQLLEN *        LengthPtr,  
      SQLSMALLINT *   PrecisionPtr,  
      SQLSMALLINT *   ScalePtr,  
      SQLSMALLINT *   NullablePtr);  
```  
  
## <a name="arguments"></a>引数  
 *DescriptorHandle*  
 [入力]記述子ハンドル。  
  
 *RecNumber*  
 [入力]アプリケーションが情報をシークする記述子レコードを示します。 記述子レコードは、レコード番号 0 ブックマーク レコードで 1 から番号が付けられます。 *RecNumber*引数は SQL_DESC_COUNT の値未満である必要があります。 場合*RecNumber* SQL_DESC_COUNT 小さいですが、行に列またはパラメーターへの呼び出しのデータが含まれていない**SQLGetDescRec**はフィールドの既定値を返します。 (詳細については、「記述子フィールドの初期化」を参照してください[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md))。  
  
 *名前*  
 [出力]記述子のレコードの SQL_DESC_NAME フィールドを返すバッファーへのポインター。  
  
 場合*名前*が null の場合、 *StringLengthPtr*はまだ文字 (文字データの null 終端文字を除く) の合計数を返しますが指すバッファーに返される使用可能な*名前*します。  
  
 *BufferLength*  
 [入力]長さ、**名前*文字のバッファー。  
  
 *StringLengthPtr*  
 [出力]返される使用可能なデータの文字数を返すバッファーへのポインター、 \**名前*バッファー、null 終端文字は除きます。 文字の数がより大きいまたは等しいがかどうか*BufferLength*、内のデータ\**名前*に切り捨てられます*BufferLength*の長さマイナス、null 終端文字の場合は、ドライバーが null で終了とします。  
  
 *TypePtr*  
 [出力]記述子レコードの SQL_DESC_TYPE フィールドの値を返すバッファーへのポインター。  
  
 *SubTypePtr*  
 [出力]レコード型を持つが SQL_DATETIME または SQL_INTERVAL、これは SQL_DESC_DATETIME_INTERVAL_CODE フィールドの値を返すバッファーへのポインターです。  
  
 *LengthPtr*  
 [出力]記述子レコードの SQL_DESC_OCTET_LENGTH フィールドの値を返すバッファーへのポインター。  
  
 *PrecisionPtr*  
 [出力]記述子レコードの SQL_DESC_PRECISION フィールドの値を返すバッファーへのポインター。  
  
 *ScalePtr*  
 [出力]記述子レコードの SQL_DESC_SCALE フィールドの値を返すバッファーへのポインター。  
  
 *NullablePtr*  
 [出力]記述子レコードの SQL_DESC_NULLABLE フィールドの値を返すバッファーへのポインター。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR、SQL_NO_DATA、または SQL_INVALID_HANDLE します。  
  
 場合は、SQL_NO_DATA が返されます。 *RecNumber*記述子レコードの現在の数より大きい。  
  
 場合は、SQL_NO_DATA が返されます。 *DescriptorHandle* IRD ハンドルと、ステートメントが準備または実行された状態が関連付けられている開いているカーソルはありませんでした。  
  
## <a name="diagnostics"></a>診断  
 ときに**SQLGetDescRec** SQL_ERROR または SQL_SUCCESS_WITH_INFO、関連付けられている SQLSTATE 値を返しますを呼び出すことによって取得できる**SQLGetDiagRec**で、 *HandleType* sql _ のHANDLE_DESC と*処理*の*DescriptorHandle*します。 次の表に、によって返される通常の SQLSTATE 値**SQLGetDescRec** ; この関数のコンテキストでそれぞれについて説明しますと表記"(DM)"の前にドライバー マネージャーによって返されるについての説明。 SQLSTATE 値ごとに関連付けられているリターン コードは明記しない限り、SQL_ERROR です。  
  
|SQLSTATE|[エラー]|説明|  
|--------------|-----------|-----------------|  
|01000|一般的な警告|ドライバー固有の情報メッセージです。 (関数は、SQL_SUCCESS_WITH_INFO を返します)。|  
|01004|文字列データで、右側が切り捨てられました|バッファー \**名前*全体の記述子フィールドを返すのに十分な大きさがありません。 そのため、フィールドが切り捨てられました。 切り詰められていない記述子フィールドの長さが返される **StringLengthPtr*します。 (関数は、SQL_SUCCESS_WITH_INFO を返します)。|  
|07009|無効な記述子のインデックス|*FieldIdentifier*引数がレコードのフィールド、 *RecNumber*引数が 0 に設定された、 *DescriptorHandle*引数は、IPD ハンドル。<br /><br /> (DM)、 *RecNumber*引数が 0 に設定されており、SQL_ATTR_USE_BOOKMARKS のステートメント属性 SQL_UB_OFF に設定されて、 *DescriptorHandle*引数は、IRD のハンドル。<br /><br /> *RecNumber*引数が 0 未満でした。|  
|08S01|通信リンク エラー|関数が完了した処理の前に、ドライバーとドライバーが接続されているデータ ソース間の通信リンクに失敗しました。|  
|HY000|一般的なエラー|これがなかった固有の SQLSTATE とする実装に固有の SQLSTATE が定義されていない、エラーが発生しました。 によって返されるエラー メッセージ**SQLGetDiagRec**で、  *\*MessageText*バッファーは、エラーとその原因について説明します。|  
|HY001|メモリの割り当てエラー|ドライバーは、実行または関数の完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY007|関連付けられているステートメントが準備されていません|*DescriptorHandle*は、IRD の関連付けと関連付けられているステートメント ハンドルは、準備または実行された状態ではありませんでした。|  
|HY010|関数のシーケンス エラー|(DM) *DescriptorHandle*に関連付けられているが、 *StatementHandle*に (このない) 非同期的に実行中の関数が呼び出されたこの関数が呼び出されたときに実行されています。<br /><br /> (DM) *DescriptorHandle*に関連付けられているが、 *StatementHandle*を**SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**、または**SQLSetPos**が呼び出され、SQL_NEED_DATA が返されます。 すべての実行時データ パラメーターまたは列のデータが送信される前に、この関数が呼び出されました。<br /><br /> (DM) を非同期的に実行中の関数が呼び出された接続ハンドルに関連付けられているため、 *DescriptorHandle*します。 この非同期関数ではときに実行されている**SQLGetDescRec**が呼び出されました。|  
|HY013|メモリ管理エラー|基になるメモリ オブジェクトにアクセスできませんでした、場合によってメモリ不足が原因であるために、関数呼び出しを処理できませんでした。|  
|HY117|不明なトランザクションの状態のため、接続が中断されます。 のみを切断して、読み取り専用の関数が許可されます。|(DM) 中断状態の詳細については、次を参照してください。 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)します。|  
|HYT01|接続がタイムアウトしました|データ ソースが要求に応答する前に、接続のタイムアウト期間が終了しました。 によって、接続タイムアウト期間が設定されます**SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT します。|  
|IM001|ドライバーでは、この関数はサポートされていません|(DM) に、ドライバーが関連付けられている*DescriptorHandle*関数をサポートしていません。|  
  
## <a name="comments"></a>コメント  
 アプリケーションが呼び出すことができます**SQLGetDescRec**次の記述子フィールドの 1 つの列またはパラメーターの値を取得します。  
  
-   SQL_DESC_NAME  
  
-   SQL_DESC_TYPE  
  
-   SQL_DESC_DATETIME_INTERVAL_CODE (の型を持つが SQL_DATETIME または SQL_INTERVAL レコード)  
  
-   SQL_DESC_OCTET_LENGTH  
  
-   SQL_DESC_PRECISION  
  
-   SQL_DESC_SCALE  
  
-   SQL_DESC_NULLABLE  
  
 **SQLGetDescRec**ヘッダー フィールドの値を取得できません。  
  
 アプリケーションでは、null ポインターをフィールドに対応する引数を設定して、戻り値のフィールドの設定を防ぐことができます。  
  
 アプリケーションを呼び出すと**SQLGetDescRec**は特定の記述子の型に対して定義されていないフィールドの値を取得する関数が SQL_SUCCESS を返しますが、フィールドに返される値は定義されません。 たとえば、呼び出し**SQLGetDescRec** APD または ARD の SQL_DESC_NAME または SQL_DESC_NULLABLE フィールドについては、SQL_SUCCESS が未定義のフィールドの値は返します。  
  
 アプリケーションを呼び出すと**SQLGetDescRec**特定の記述子の型に対して定義されているが、既定値を持たないをまだ設定されていないフィールドの値を取得する関数が SQL_SUCCESS を返しますが、返される値フィールドが定義されていません。 詳細については、「記述子フィールドの初期化」を参照してください[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)します。  
  
 フィールドの値が呼び出しによって個別に取得することもできます**SQLGetDescField**します。 記述子のヘッダーまたはレコードのフィールドの説明は、次を参照してください。 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)します。 記述子の詳細については、次を参照してください。[記述子](../../../odbc/reference/develop-app/descriptors.md)します。  
  
## <a name="related-functions"></a>関連する関数  
  
|詳細|参照先|  
|---------------------------|---------|  
|列のバインド|[SQLBindCol 関数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|パラメーターのバインド|[SQLBindParameter 関数](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|記述子フィールドの取得|[SQLGetDescField 関数](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|複数の記述子フィールドの設定|[SQLSetDescRec 関数](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
  
## <a name="see-also"></a>参照  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)
