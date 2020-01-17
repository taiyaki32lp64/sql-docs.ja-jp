---
title: SQLSetStmtAttr 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSetStmtAttr
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLSetStmtAttr
helpviewer_keywords:
- SQLSetStmtAttr function [ODBC]
ms.assetid: 7abc5260-733a-48d4-9974-2d1a6a9ea5f6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 583639a5cd4680bf6cfcf03bbaf6ee9eb63adba8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68039649"
---
# <a name="sqlsetstmtattr-function"></a>SQLSetStmtAttr 関数
**準拠**  
 バージョンが導入されました。ODBC 3.0 規格に準拠します。ISO 92  
  
 **まとめ**  
 **SQLSetStmtAttr**ステートメントに関連する属性を設定します。  
  
> [!NOTE]
>  どのようなドライバー マネージャーは、ときに、マッピングするには、この関数、ODBC の詳細については*3.x* odbc アプリケーションが動作*2.x*ドライバーを参照してください[後方のマッピング置換関数アプリケーションの互換性を](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLSetStmtAttr(  
     SQLHSTMT      StatementHandle,  
     SQLINTEGER    Attribute,  
     SQLPOINTER    ValuePtr,  
     SQLINTEGER    StringLength);  
```  
  
## <a name="arguments"></a>引数  
 *StatementHandle*  
 [入力]ステートメント ハンドルです。  
  
 *属性*  
 [入力]オプションを設定すると、「コメントです」記載されています。  
  
 *ValuePtr*  
 [入力]関連付けられる値*属性*します。 値に応じて*属性*、 *ValuePtr*次のいずれかになります。  
  
-   ODBC 記述子ハンドル。  
  
-   SQLUINTEGER 値。  
  
-   Sqlulen です値。  
  
-   次のいずれかへのポインター。  
  
    -   Null で終わる文字列。  
  
    -   バイナリのバッファー。  
  
    -   値または SQLLEN、sqlulen です、または SQLUSMALLINT 型の配列。  
  
    -   ドライバーの定義済みの値。  
  
 場合、*属性*引数は、ドライバー固有の値では、 *ValuePtr*符号付き整数である可能性があります。  
  
 *StringLength*  
 [入力]場合*属性*ODBC で定義された属性と*ValuePtr*文字の文字列またはバイナリのバッファーを指す、この引数の長さである必要があります\* *ValuePtr*. 場合*属性*ODBC で定義された属性と*ValuePtr*整数*StringLength*は無視されます。  
  
 場合*属性*ドライバーの定義済みの属性では、アプリケーションを設定して属性をドライバー マネージャーの性質を示します、 *StringLength*引数。 *StringLength*次の値を持つことができます。  
  
-   場合*ValuePtr*文字の文字列へのポインターは*StringLength* SQL_NTS または文字列の長さです。  
  
-   場合*ValuePtr* 、SQL_LEN_BINARY_ATTR の結果を配置するアプリケーションが、バイナリ バッファーへのポインター (*長さ*) マクロで*StringLength*します。 これにより、負の値で*StringLength*します。  
  
-   場合*ValuePtr*文字の文字列またはバイナリ文字列以外の値へのポインターは*StringLength* SQL_IS_POINTER 値でなければなりません。  
  
-   場合*ValuePtr* 、固定長の値を含む*StringLength* SQL_IS_INTEGER または SQL_IS_UINTEGER のいずれかを適切なは。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR、または SQL_INVALID_HANDLE します。  
  
## <a name="diagnostics"></a>診断  
 ときに**SQLSetStmtAttr** SQL_ERROR または SQL_SUCCESS_WITH_INFO、関連付けられている SQLSTATE 値を返しますを呼び出すことによって取得される可能性があります**SQLGetDiagRec**で、 *HandleType* SQL の_HANDLE_STMT と*処理*の*StatementHandle*します。 次の表に、一般的にによって返される SQLSTATE 値**SQLSetStmtAttr** ; この関数のコンテキストでそれぞれについて説明しますと表記"(DM)"の前にドライバー マネージャーによって返されるについての説明。 SQLSTATE 値ごとに関連付けられているリターン コードは明記しない限り、SQL_ERROR です。  
  
|SQLSTATE|[エラー]|説明|  
|--------------|-----------|-----------------|  
|01000|一般的な警告|ドライバー固有の情報メッセージです。 (関数は、SQL_SUCCESS_WITH_INFO を返します)。|  
|01S02|オプション値が変更されました|ドライバーがで指定された値をサポートしていませんでした*ValuePtr*で指定された値または*ValuePtr*が、ドライバーのような値を代入するため、実装の動作状態のため無効です。 (**SQLGetStmtAttr**一時的に置き換えられた値を決定するということができます)。代替値が有効、 *StatementHandle*カーソルが閉じられるまで、ステートメント属性はこの時点で、前の値に元に戻します。 変更可能なステートメント属性は次のとおりです。<br /><br /> SQL _ ATTR_CONCURRENCY SQL _ ATTR_CURSOR_TYPE SQL _ ATTR_KEYSET_SIZE SQL _ ATTR_MAX_LENGTH SQL _ ATTR_MAX_ROWS SQL _ ATTR_QUERY_TIMEOUT SQL_ATTR_ROW_ARRAY_SIZE SQL _ ATTR_SIMULATE_CURSOR<br /><br /> (関数は、SQL_SUCCESS_WITH_INFO を返します)。|  
|08S01|通信リンク エラー|関数が完了した処理の前に、ドライバーとドライバーが接続されているデータ ソース間の通信リンクに失敗しました。|  
|24000|カーソル状態が無効|*属性*SQL_ATTR_CONCURRENCY、SQL_ATTR_CURSOR_TYPE、SQL_ATTR_SIMULATE_CURSOR、または、SQL_ATTR_USE_BOOKMARKS、カーソルが開かれていた。|  
|HY000|一般的なエラー|これがなかった固有の SQLSTATE とする実装に固有の SQLSTATE が定義されていない、エラーが発生しました。 によって返されるエラー メッセージ**SQLGetDiagRec**で、  *\*MessageText*バッファーは、エラーとその原因について説明します。|  
|HY001|メモリの割り当てエラー|ドライバーは、実行または関数の完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY009|無効な null ポインターの使用|*属性*引数が文字列の属性を必要とするステートメント属性を識別し、 *ValuePtr*引数が null ポインター。|  
|HY010|関数のシーケンス エラー|(DM) を非同期的に実行中の関数が呼び出された接続ハンドルに関連付けられているため、 *StatementHandle*します。 この非同期関数ではときに実行されている、 **SQLSetStmtAttr**関数が呼び出されました。<br /><br /> (DM) **SQLExecute**、 **SQLExecDirect**、または**SQLMoreResults**に対して呼び出された、 *StatementHandle* SQL_PARAM_DATA_ を返されます。ご利用いただけます。 ストリームのすべてのパラメーターのデータが取得される前に、この関数が呼び出されました。<br /><br /> (DM) を非同期的に実行中の関数が呼び出された、 *StatementHandle*この関数が呼び出されたときに実行されているとします。<br /><br /> (DM) **SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**、または**SQLSetPos**に対して呼び出された、 *StatementHandle* SQL_NEED_DATA が返されます。 すべての実行時データ パラメーターまたは列のデータが送信される前に、この関数が呼び出されました。|  
|HY011|属性を設定できません。|*属性*が SQL_ATTR_CONCURRENCY、sql _ ATTR_CURSOR_TYPE、sql _ ATTR_SIMULATE_CURSOR、または sql _ ATTR_USE_BOOKMARKS、およびステートメントが準備されています。|  
|HY013|メモリ管理エラー|基になるメモリ オブジェクトにアクセスできませんでした、場合によってメモリ不足が原因であるために、関数呼び出しを処理できませんでした。|  
|HY017|無効な自動的に割り当てられた記述子ハンドルの使用|(DM)、*属性*SQL_ATTR_IMP_ROW_DESC または SQL_ATTR_IMP_PARAM_DESC 引数がでした。<br /><br /> (DM)、*属性*引数が SQL_ATTR_APP_ROW_DESC または SQL_ATTR_APP_PARAM_DESC、および値*ValuePtr*当初は、ハンドル以外、暗黙的に割り当てられた記述子ハンドルARD または APD に対して割り当てられます。|  
|HY024|無効な属性値|指定した*属性*値、無効な値に指定されました*ValuePtr*します。 (ドライバー マネージャーは、接続とステートメント属性 SQL_ATTR_ACCESS_MODE や sql _ ATTR_ASYNC_ENABLE などの値の個別セットをそのまま使用するには、この SQLSTATE を返します。 ドライバーの他のすべての接続とステートメント属性で指定された値を確認する必要があります*ValuePtr*)。<br /><br /> *属性*引数が SQL_ATTR_APP_ROW_DESC または SQL_ATTR_APP_PARAM_DESC、および*ValuePtr*と同じ接続ではないに明示的に割り当てられた記述子ハンドルが、 *StatementHandle*引数。|  
|HY090|文字列またはバッファーの長さが無効です。|(DM)  *\*ValuePtr*文字の文字列と*StringLength*引数は SQL_NTS が 0 未満でした。|  
|HY092|無効な属性またはオプション識別子|引数に指定された値 (DM)*属性*ODBC ドライバーでサポートされているのバージョンには無効です。<br /><br /> 引数に指定された値 (DM)*属性*読み取り専用属性されました。|  
|HY117|不明なトランザクションの状態のため、接続が中断されます。 のみを切断して、読み取り専用の関数が許可されます。|(DM) 中断状態の詳細については、次を参照してください。 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)します。|  
|HYC00|省略可能な機能が実装されていません|引数が指定された値*属性*有効な ODBC ステートメント属性が ODBC のバージョンのドライバーでサポートされているが、ドライバーによってサポートされていませんでした。<br /><br /> *属性*引数が呼び出すと、SQL_ATTR_ASYNC_ENABLE **SQLGetInfo**で、*情報の種類*SQL_ASYNC_MODE の SQL_AM_CONNECTION を返します。<br /><br /> *属性*引数が SQL_ATTR_ENABLE_AUTO_IPD、および SQL_ATTR_AUTO_IPD 接続属性の値が sql_false になります。|  
|HYT01|接続がタイムアウトしました|データ ソースが要求に応答する前に、接続のタイムアウト期間が終了しました。 によって、接続タイムアウト期間が設定されます**SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT します。|  
|IM001|ドライバーでは、この関数はサポートされていません|(DM) に、ドライバーが関連付けられている、 *StatementHandle*関数をサポートしていません。|  
|S1118|ドライバーが非同期通知をサポートしていません|呼び出す場合**SQLSetStmtAttr** SQL_ATTR_ASYNC_STMT_EVENT; を設定する非同期の通知は、ドライバーによってサポートされていません。|  
  
## <a name="comments"></a>コメント  
 別の呼び出しによって変更されるまで、ステートメントのステートメント属性は有効**SQLSetStmtAttr**を呼び出して、ステートメントが削除されるまで、または**SQLFreeHandle**します。 呼び出す**SQLFreeStmt** SQL_CLOSE、SQL_UNBIND、または SQL_RESET_PARAMS オプションはリセットされませんステートメント属性。  
  
 いくつかのステートメント属性は、データ ソースがで指定された値をサポートしていない場合のような値の置換をサポート*ValuePtr*します。 このような場合、ドライバーは SQL_SUCCESS_WITH_INFO と SQLSTATE 01S02 を返します (オプションの値が変更されました)。 たとえば場合、*属性*SQL_ATTR_CONCURRENCY、および*ValuePtr* SQL_CONCUR_ROWVER があり、データ ソースがこれにもできない場合、ドライバー SQL_CONCUR_VALUES に置換されますを返す sql _SUCCESS_WITH_INFO します。 置き換えられた値を決定するアプリケーションを呼び出す**SQLGetStmtAttr**します。  
  
 情報の形式設定*ValuePtr*に指定した依存*属性*します。 **SQLSetStmtAttr**属性情報を 2 つの異なる形式のいずれかで受け取り: 文字の文字列または整数値。 それぞれの形式は、属性の説明に記録されます。 内の各属性に対して返される情報をこの形式を適用**SQLGetStmtAttr**します。 文字列の指す、 *ValuePtr*の引数**SQLSetStmtAttr**長さ*StringLength*します。  
  
> [!NOTE]
>  ステートメント属性を呼び出すことで、接続レベルで設定できる**SQLSetConnectAttr** ODBC では非推奨*3.x*します。 ODBC *3.x*アプリケーションは接続レベルでステートメント属性を設定しない必要があります。 ODBC *3.x*で、これは、接続属性とステートメントの属性の両方を指定できます、SQL_ATTR_METADATA_ID および SQL_ATTR_ASYNC_ENABLE 属性を除く、接続レベルでのステートメント属性を設定することはできません接続レベルまたはステートメント レベルのいずれかに設定します。  
> 
> [!NOTE]
>  ODBC *3.x* ODBC 協力する場合、ドライバーはこの機能をサポートのみ必要*2.x*セット ODBC アプリケーション*2.x*接続レベルでステートメントのオプション。 詳細については、「設定ステートメント オプションで、接続レベル」を参照してください[SQLSetConnectOption のマッピング](../../../odbc/reference/appendixes/sqlsetconnectoption-mapping.md)で付録 g:。旧バージョンとの互換性のためのガイドラインをドライバーです。  
  
## <a name="statement-attributes-that-set-descriptor-fields"></a>記述子フィールドの設定を与えるステートメント属性  
 多くのステートメント属性は、記述子のヘッダー フィールドに対応します。 記述子フィールドの設定でこれらの属性に実際に結果を設定します。 フィールドの設定への呼び出しによって**SQLSetStmtAttr**なく**SQLSetDescField**記述子ハンドルが関数呼び出しを取得する必要はありません利点があります。  
  
> [!CAUTION]  
>  呼び出す**SQLSetStmtAttr**の 1 つのステートメントの他のステートメントに影響することができます。 これには、明示的に割り当てられているし、その他のステートメントに関連付けられても APD または ARD ステートメントに関連付けられているときに発生します。 **SQLSetStmtAttr** APD または ARD、変更、変更がこの記述子が関連付けられているすべてのステートメントに適用されます。 アプリケーションが、他のステートメントからこの記述子の関連付けを解除する必要があります、必要な動作でない場合 (呼び出して**SQLSetStmtAttr** SQL_ATTR_APP_ROW_DESC または SQL_ATTR_APP_PARAM_DESC フィールド別に設定するには記述子ハンドル) 呼び出す前に**SQLSetStmtAttr**もう一度です。  
  
 識別されるステートメントに現在関連付けられている適用可能な記述子に対してのみ、フィールドを設定する記述子フィールドが設定されている対応するステートメント属性の結果として設定されている場合、 *StatementHandle*引数と属性の設定、将来そのステートメントに関連付けられている可能性のある任意の記述子は影響しません。 呼び出してステートメント属性でもある記述子フィールドを設定すると**SQLSetDescField**、対応するステートメント属性を設定します。 場合は、明示的に割り当てられた記述子は、ステートメントから関連付け解除、ヘッダー フィールドに対応するステートメント属性は、暗黙的に割り当てられた記述子フィールドの値に戻ります。  
  
 ステートメントが割り当てられます (を参照してください[SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md))、4 つの記述子ハンドルが自動的に割り当てられ、ステートメントに関連付けられています。 明示的に割り当てられた記述子ハンドルは、呼び出すことによって、ステートメントと関連付けができる**SQLAllocHandle**で、 *fHandleType*記述子ハンドルおよび呼び出しますを割り当てるSQL_HANDLE_DESCの**SQLSetStmtAttr**ステートメントと記述子ハンドルを関連付ける。  
  
 次の表に、ステートメント属性は、記述子のヘッダー フィールドに対応します。  
  
|ステートメント属性|ヘッダー フィールド|Desc です。|  
|-------------------------|------------------|-----------|  
|SQL_ATTR_PARAM_BIND_OFFSET_PTR|SQL_DESC_BIND_OFFSET_PTR|APD|  
|SQL_ATTR_PARAM_BIND_TYPE|SQL_DESC_BIND_TYPE|APD|  
|SQL_ATTR_PARAM_OPERATION_PTR|SQL_DESC_ARRAY_STATUS_PTR|APD|  
|SQL_ATTR_PARAM_STATUS_PTR|SQL_DESC_ARRAY_STATUS_PTR|IPD|  
|SQL_ATTR_PARAMS_PROCESSED_PTR|SQL_DESC_ROWS_PROCESSED_PTR|IPD|  
|SQL_ATTR_PARAMSET_SIZE|SQL_DESC_ARRAY_SIZE|APD|  
|SQL_ATTR_ROW_ARRAY_SIZE|SQL_DESC_ARRAY_SIZE|ARD|  
|SQL_ATTR_ROW_BIND_OFFSET_PTR|SQL_DESC_BIND_OFFSET_PTR|ARD|  
|SQL_ATTR_ROW_BIND_TYPE|SQL_DESC_BIND_TYPE|ARD|  
|SQL_ATTR_ROW_OPERATION_PTR|SQL_DESC_ARRAY_STATUS_PTR|ARD|  
|SQL_ATTR_ROW_STATUS_PTR|SQL_DESC_ARRAY_STATUS_PTR|IRD|  
|SQL_ATTR_ROWS_FETCHED_PTR|SQL_DESC_ROWS_PROCESSED_PTR|IRD|  
  
## <a name="statement-attributes"></a>ステートメント属性  
 現在定義されている属性とが導入されました ODBC のバージョンが次の表に示すように多くの属性をさまざまなデータ ソースを活用するためにドライバーを定義することが期待されます。 属性の範囲は ODBC; によって予約されていますドライバー開発者向けには、Open Group から個々 のドライバーの使用するための値を予約する必要があります。 詳細については、次を参照してください。[ドライバー固有のデータ型、記述子の種類、情報の種類、診断型、および属性](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md)します。  
  
|属性|*ValuePtr*内容|  
|---------------|-------------------------|  
|SQL_ATTR_APP_PARAM_DESC (ODBC 3.0)|APD の後続の呼び出しを識別するハンドル**SQLExecute**と**SQLExecDirect**ステートメント ハンドルでします。 この属性の初期値には、暗黙的に割り当て、ステートメントが最初に割り当てられるときに、記述子です。 この属性の値が SQL_NULL_DESC または最初に割り当てられた記述子ハンドルに設定されている場合、ステートメント ハンドルに以前関連付けられていた APD ハンドルを明示的に割り当てられたがそこから関連付け解除し、に、ステートメント ハンドルを元に戻します、APD のハンドルを暗黙的に割り当てられます。<br /><br /> または、同じステートメントに暗黙的に設定された別の記述子ハンドルを別のステートメントを暗黙的に割り当てられた記述子ハンドルには、この属性を設定することはできません。暗黙的に割り当てられた記述子ハンドルは、1 つ以上のステートメントまたは記述子ハンドルに関連付けすることはできません。|  
|SQL_ATTR_APP_ROW_DESC (ODBC 3.0)|ステートメント ハンドルで以降のフェッチの ARD へのハンドル。 この属性の初期値には、暗黙的に割り当て、ステートメントが最初に割り当てられるときに、記述子です。 この属性の値が SQL_NULL_DESC または最初に割り当てられた記述子ハンドルに設定されている場合、ステートメント ハンドルに以前関連付けられていた ARD ハンドルを明示的に割り当てられたがそこから関連付け解除し、に、ステートメント ハンドルを元に戻します、ARD ハンドルを暗黙的に割り当てられます。<br /><br /> または、同じステートメントに暗黙的に設定された別の記述子ハンドルを別のステートメントを暗黙的に割り当てられた記述子ハンドルには、この属性を設定することはできません。暗黙的に割り当てられた記述子ハンドルは、1 つ以上のステートメントまたは記述子ハンドルに関連付けすることはできません。|  
|SQL_ATTR_ASYNC_ENABLE (ODBC 1.0)|指定されたステートメントで呼び出される関数が非同期的に実行するかどうかを指定する sqlulen です値:<br /><br /> SQL_ASYNC_ENABLE_OFF = 無効にするステートメント レベルの非同期実行のサポート (既定)。<br /><br /> SQL_ASYNC_ENABLE_ON = ステートメント レベルの非同期実行のサポートを有効にします。<br /><br /> 詳細については、次を参照してください。[非同期実行 (ポーリング メソッド)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)します。<br /><br /> ステートメント レベルの非同期実行のサポートとドライバーは、ステートメント属性 SQL_ATTR_ASYNC_ENABLE は読み取り専用です。 その値は、ステートメント ハンドルの割り当て時に同じ名前の接続レベルの属性の値として同じです。<br /><br /> 呼び出す**SQLSetStmtAttr** SQL_ATTR_ASYNC_ENABLE を設定するときに、SQL_ASYNC_MODE*情報の種類*SQL_AM_CONNECTION 返します SQLSTATE HYC00 を返します (省略可能な機能が実装されていません)。 詳細については、次を参照してください。 [SQLSetConnectAttr 関数](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)詳細についてはします。|  
|SQL_ATTR_ASYNC_STMT_EVENT (ODBC 3.8)|イベント ハンドルである SQLPOINTER 値。<br /><br /> 呼び出して非同期関数の完了の通知が有効になっている**SQLSetStmtAttr**を設定する、 **SQL_ATTR_ASYNC_STMT_EVENT**属性し、イベント ハンドルを指定します。|  
|SQL_ATTR_ASYNC_STMT_PCALLBACK (ODBC 3.8)|非同期のコールバック関数への SQLPOINTER。<br /><br /> ドライバー マネージャーがドライバーを呼び出すことができますのみ**SQLSetStmtAttr**この属性を持つ関数です。|  
|SQL_ATTR_ASYNC_STMT_PCONTEXT (ODBC 3.8)|Context 構造体への SQLPOINTER<br /><br /> ドライバー マネージャーがドライバーを呼び出すことができますのみ**SQLSetStmtAttr**この属性を持つ関数です。|  
|SQL_ATTR_CONCURRENCY (ODBC 2.0)|カーソルの同時実行を示す sqlulen です値を指定します。<br /><br /> SQL_CONCUR_READ_ONLY = カーソルは読み取り専用です。 更新は許可されません。<br /><br /> SQL_CONCUR_LOCK カーソルは、行を更新することを確認するための十分なロックの最も低いレベルを = です。<br /><br /> SQL_CONCUR_ROWVER SQLBase ROWID または Sybase タイムスタンプなどの行のバージョンを比較する、カーソルはオプティミスティック同時実行制御を = です。<br /><br /> SQL_CONCUR_VALUES 値を比較する、カーソルはオプティミスティック同時実行制御を = です。<br /><br /> SQL_ATTR_CONCURRENCY に既定値は、SQL_CONCUR_READ_ONLY です。<br /><br /> この属性は、開いているカーソルに指定できません。 詳細については、次を参照してください。[同時実行の種類](../../../odbc/reference/develop-app/concurrency-types.md)します。<br /><br /> 場合、SQL_ATTR_CURSOR_TYPE*属性*が変更された実行時間、および警告を発行するとでも、SQL_ATTR_CONCURRENCYの値を変更SQL_ATTR_CONCURRENCYの現在の値をサポートしていない型に**SQLExecDirect**または**SQLPrepare**が呼び出されます。<br /><br /> ドライバーがサポートしている場合、 **SELECT FOR UPDATE** SQL_CONCUR_READ_ONLY に SQL_ATTR_CONCURRENCY の値が設定されているステートメントと、このようなステートメントが実行されるが、エラーが返されます。 実行時および SQLSTATE 01S02 に SQL_ATTR_CURSOR_TYPE の値は変更 SQL_ATTR_CONCURRENCY の値は、ドライバーは、SQL_ATTR_CURSOR_TYPE の現在の値ではなく SQL_ATTR_CURSOR_TYPE のいくつかの値をサポートする値を変更する場合(オプションの値が変更された) が発行された**SQLExecDirect**または**SQLPrepare**が呼び出されます。<br /><br /> ドライバーが別の同時実行に置き換えられ、SQLSTATE 01S02 を返す場合は、データ ソースでは、指定した同時実行はサポートされていない、(オプションの値が変更されました)。 置き換えます SQL_CONCUR_ROWVER、SQL_CONCUR_VALUES、ドライバー、またはその逆です。 SQL_CONCUR_LOCK、ドライバーに置き換えます、SQL_CONCUR_ROWVER、SQL_CONCUR_VALUES またはの順序で。 置換された値の有効性は、実行時までは確認されません。<br /><br /> SQL_ATTR_CONCURRENCY と他のカーソルの属性間のリレーションシップの詳細については、次を参照してください。[カーソルの特性とカーソルの種類](../../../odbc/reference/develop-app/cursor-characteristics-and-cursor-type.md)します。|  
|SQL_ATTR_CURSOR_SCROLLABLE (ODBC 3.0)|アプリケーションに必要なサポートのレベルを示す sqlulen です値を指定します。 この属性を設定する後続の呼び出しに影響を与えます**SQLExecDirect**と**SQLExecute**します。<br /><br /> SQL_NONSCROLLABLE = Scrollable カーソルは、ステートメント ハンドルでは必要ありません。 アプリケーションを呼び出す場合**SQLFetchScroll**の唯一の有効な値は、このハンドルで*FetchOrientation* SQL_FETCH_NEXT が。 既定値です。<br /><br /> SQL_SCROLLABLE = Scrollable カーソルは、ステートメント ハンドルで必要です。 呼び出すときに**SQLFetchScroll**、アプリケーションの有効な値を指定できます*FetchOrientation*、シーケンシャル モード以外のモードでのカーソルの配置を実現します。<br /><br /> スクロール可能なカーソルの詳細については、次を参照してください。[スクロール可能なカーソル](../../../odbc/reference/develop-app/scrollable-cursors.md)します。 SQL_ATTR_CURSOR_SCROLLABLE と他のカーソルの属性間のリレーションシップの詳細については、次を参照してください[カーソルの特性とカーソルの種類。](../../../odbc/reference/develop-app/cursor-characteristics-and-cursor-type.md)|  
|SQL_ATTR_CURSOR_SENSITIVITY (ODBC 3.0)|ステートメント ハンドルでカーソルが表示されるようにするかどうかを示す sqlulen です値を結果に加えられた変更を別のカーソルでに設定します。 この属性を設定する後続の呼び出しに影響を与えます**SQLExecDirect**と**SQLExecute**します。 アプリケーションは、アプリケーションでこの属性を取得する初期状態または状態として最も最近の値が設定戻る読み込むことができます。<br /><br /> SQL_UNSPECIFIED = 指定されていない、カーソルの種類し、かどうかのカーソル ステートメント ハンドルに表示されるように別のカーソルが結果セットに加えられた変更します。 ステートメント ハンドルでカーソルが表示されるようになしでは、このようないくつか、またはすべての変更。 既定値です。<br /><br /> SQL_INSENSITIVE = その他のすべてのカーソルでステートメント ハンドルを表示する結果セットのことに加えられた変更を反映せず、すべてのカーソル。 Insensitive カーソルは読み取り専用です。 これは、読み取り専用である同時実行が静的カーソルに対応します。<br /><br /> SQL_SENSITIVE = すべてのカーソルで、ステートメント ハンドル表示結果に加えられたすべての変更が別のカーソルを設定します。<br /><br /> SQL_ATTR_CURSOR_SENSITIVITY と他のカーソルの属性間のリレーションシップの詳細については、次を参照してください。[カーソルの特性とカーソルの種類](../../../odbc/reference/develop-app/cursor-characteristics-and-cursor-type.md)します。|  
|SQL_ATTR_CURSOR_TYPE (ODBC 2.0)|カーソルの種類を指定する sqlulen です値:<br /><br /> SQL_CURSOR_FORWARD_ONLY = カーソルだけスクロール転送します。<br /><br /> SQL_CURSOR_STATIC = データ結果セットが静的です。<br /><br /> SQL_CURSOR_KEYSET_DRIVEN = ドライバーの保存と SQL_ATTR_KEYSET_SIZE ステートメントの属性で指定された行の数のキーを使用します。<br /><br /> SQL_CURSOR_DYNAMIC = ドライバーの保存と、行セット内の行キーのみを使用します。<br /><br /> 既定値は、SQL_CURSOR_FORWARD_ONLY です。 SQL ステートメントが準備された後、この属性は指定できません。<br /><br /> ドライバーが別のカーソルの種類に置き換えられ、SQLSTATE 01S02 を返します、指定したカーソルの種類が、データ ソースでサポートされていない場合 (オプションの値が変更されました)。 混合または動的カーソルの場合、ドライバーに置換されます、キーセット ドリブンまたは静的カーソルの順序で。 キーセット ドリブン カーソルの場合は、ドライバーには、静的カーソルが置換されます。<br /><br /> スクロール可能なカーソルの種類の詳細については、次を参照してください。[スクロール可能なカーソルの種類](../../../odbc/reference/develop-app/scrollable-cursor-types.md)します。 SQL_ATTR_CURSOR_TYPE およびその他のカーソルの属性間のリレーションシップの詳細については、次を参照してください。[カーソルの特性とカーソルの種類](../../../odbc/reference/develop-app/cursor-characteristics-and-cursor-type.md)します。|  
|SQL_ATTR_ENABLE_AUTO_IPD (ODBC 3.0)|IPD の自動作成を実行するかどうかを示す sqlulen です値:<br /><br /> SQL_TRUE に呼び出しの後に、IPD の自動作成 = **SQLPrepare**します。 SQL_FALSE = 呼び出しの後に、IPD の自動作成をオフに**SQLPrepare**します。 (アプリケーションでは IPD フィールド情報を呼び出すことによっても取得できます**SQLDescribeParam**サポートされている場合)。ステートメント属性 SQL_ATTR_ENABLE_AUTO_IPD の既定値は、sql_false になります。 詳細については、次を参照してください。 [、IPD の自動作成](../../../odbc/reference/develop-app/automatic-population-of-the-ipd.md)です。|  
|SQL_ATTR_FETCH_BOOKMARK_PTR (ODBC 3.0)|SQLLEN\*バイナリのブックマークの値を指します。 ときに**SQLFetchScroll**を使用して呼び出した*fFetchOrientation*ブックマーク値をこのフィールドから SQL_FETCH_BOOKMARK 等しい、ドライバーを取得します。 このフィールドの既定値は null ポインターです。 詳細については、次を参照してください。[ブックマークによるスクロール](../../../odbc/reference/develop-app/scrolling-by-bookmark.md)します。<br /><br /> このフィールドによって示される値はブックマークで delete は使用されません、ブックマークを更新またはでブックマーク操作によってフェッチ**SQLBulkOperations**ブックマーク行セットのバッファーにキャッシュを使用します。|  
|SQL_ATTR_IMP_PARAM_DESC (ODBC 3.0)|IPD のハンドルです。 この属性の値は、ステートメントが最初に割り当てられるときに割り当てられた記述子です。 アプリケーションでは、この属性を設定できません。<br /><br /> この属性への呼び出しで取得できる**SQLGetStmtAttr**への呼び出しで設定されていないが、 **SQLSetStmtAttr**します。|  
|SQL_ATTR_IMP_ROW_DESC (ODBC 3.0)|IRD のハンドルです。 この属性の値は、ステートメントが最初に割り当てられるときに割り当てられた記述子です。 アプリケーションでは、この属性を設定できません。<br /><br /> この属性への呼び出しで取得できる**SQLGetStmtAttr**への呼び出しで設定されていないが、 **SQLSetStmtAttr**します。|  
|SQL_ATTR_KEYSET_SIZE (ODBC 2.0)|キーセット ドリブン カーソルのキーセット内の行の数を示す sqlulen です。 キーセットのサイズが 0 (既定値) の場合は、完全にキーセット ドリブン カーソルのです。 キーセットのサイズが 0 より大きい場合は、カーソルを混合 (キーセット ドリブンのキーセット内と動的、キーセットの外部で)。 既定のキーセットのサイズは 0 です。 キーセット ドリブン カーソルの詳細については、次を参照してください。[キーセット ドリブン カーソル](../../../odbc/reference/develop-app/keyset-driven-cursors.md)します。<br /><br /> ドライバーがそのサイズに置き換えられ、SQLSTATE 01S02 を返します、指定されたサイズが最大キーセットのサイズを超える場合 (オプションの値が変更されました)。<br /><br /> **SQLFetch**または**SQLFetchScroll**キーセットのサイズが 0 より大きいと、行セット サイズよりも小さい場合はエラーを返します。|  
|SQL_ATTR_MAX_LENGTH (ODBC 1.0)|ドライバーが文字またはバイナリの列から返されるデータの最大量を示す sqlulen です値を指定します。 場合*ValuePtr*が、使用可能なデータの長さより小さい**SQLFetch**または**SQLGetData**データが切り捨てられるし、関係なく SQL_SUCCESS を返します。 場合*ValuePtr*が 0 (既定値) の場合、ドライバーが利用可能なすべてのデータを返そうとします。<br /><br /> 指定された長さがデータ ソースを返すことができるデータの最小量よりも少ない場合またはデータ ソースが返すことができます、ドライバーの代替値を返す SQLSTATE 01S02 データの最大量よりも大きい (オプションの値が変更されました)。<br /><br /> この属性の値は、開いているカーソル; に設定できます。ただし、設定がすぐに反映されませんである場合、ドライバーは SQLSTATE 01S02 を返します (オプションの値の変更) 元の値に属性をリセットします。<br /><br /> この属性は、ネットワーク トラフィックを削減するためのものがあり、複数層のドライバー (ドライバー) ではなく、データ ソースで実装できる場合にのみサポートされている必要があります。 データの切り捨てをアプリケーションでこのメカニズムが使用しない必要があります。アプリケーションを受信したデータを切り捨てるで最大のバッファーの長さを指定する必要があります、 *BufferLength*引数**SQLBindCol**または**SQLGetData**します。|  
|SQL_ATTR_MAX_ROWS (ODBC 1.0)|アプリケーションに返される行の最大数に対応する sqlulen です値を**選択**ステートメント。 場合\* *ValuePtr*が 0 (既定値) と等しい、ドライバーは、すべての行を返します。<br /><br /> この属性は、ネットワーク トラフィックを削減するものです。 結果セットが作成され、結果セットは、最初に制限の適用概念的には、 *ValuePtr*行。 結果セット内の行の数がより大きいかどうか*ValuePtr*、結果セットが切り詰められています。<br /><br /> SQL_ATTR_MAX_ROWS が上すべての結果セットに適用されます、*ステートメント*、カタログ関数によって返されるものなどです。 SQL_ATTR_MAX_ROWS は、カーソル行の数の値の最大値を確立します。<br /><br /> ドライバーがの SQL_ATTR_MAX_ROWS 動作をエミュレートする必要がありますいない**SQLFetch**または**SQLFetchScroll** (かどうかは結果セットのサイズ制限実装できない、データ ソース) が保証できない場合その SQL_ATTRMAX_ROWS は適切に実装します。<br /><br /> ドライバー定義 SQL_ATTR_MAX_ROWS を (カタログ関数の場合) などの SELECT ステートメント以外のステートメントに適用するかどうか。<br /><br /> この属性の値は、開いているカーソル; に設定できます。ただし、設定がすぐに反映されませんである場合、ドライバーは SQLSTATE 01S02 を返します (オプションの値の変更) 元の値に属性をリセットします。|  
|SQL_ATTR_METADATA_ID (ODBC 3.0)|カタログ関数の文字列引数の処理方法を決定する sqlulen です値。<br /><br /> 場合は SQL_TRUE、カタログ関数の文字列引数は、識別子として扱われます。 大文字と小文字は大きくありません。 規格文字列の場合、ドライバーは、末尾のスペースを削除および文字列が大文字に折りたたまれません。 区切られた文字列の場合、ドライバーは、先頭または末尾のスペースを削除しは文字どおり、区切り記号の間は。 返しますが SQL_ERROR と SQLSTATE HY009 null ポインターにこれらの引数のいずれかに設定されている場合 (null ポインターの無効な使用)。<br /><br /> 場合は sql_false になります、カタログ関数の文字列引数は、識別子としては扱われません。 大文字と小文字は重要です。 か、含めることができます、文字列の検索パターンまたはそうでない引数に応じて。<br /><br /> 既定値は、sql_false になります。<br /><br /> *TableType*の引数**SQLTables**、この属性を受けませんが、値の一覧を受け取ります。<br /><br /> SQL_ATTR_METADATA_ID は接続レベルの設定もできます。 (SQL_ATTR_ASYNC_ENABLE し、接続属性にもなる唯一のステートメント属性)。<br /><br /> 詳細については、次を参照してください。[カタログ関数の引数](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)します。|  
|SQL_ATTR_NOSCAN (ODBC 1.0)|ドライバーが SQL 文字列のエスケープ シーケンスをスキャンするかどうかを示す sqlulen です値:<br /><br /> SQL_NOSCAN_OFF ドライバー スキャン (既定値) のエスケープ シーケンスの SQL 文字列を = です。<br /><br /> SQL_NOSCAN_ON = ドライバーは SQL 文字列のエスケープ シーケンスをスキャンしません。 代わりに、ドライバーは、データ ソースへの直接のステートメントを送信します。<br /><br /> 詳細については、次を参照してください。 [odbc エスケープ シーケンス](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md)します。|  
|SQL_ATTR_PARAM_BIND_OFFSET_PTR (ODBC 3.0)|Sqlulen です * 動的パラメーターのバインドを変更へのポインターに追加のオフセットを示す値。 ドライバーにポインターを逆参照し、遅延のフィールド (SQL_DESC_DATA_PTR、SQL_DESC_INDICATOR_PTR、および SQL_DESC_OCTET_LENGTH_PTR) の記述子レコードのそれぞれに逆参照された値を追加し、新しいポインター値を使用してこのフィールドが null 以外の場合は、バインドするときにします。 設定されている既定では null にします。<br /><br /> バインドのオフセットは常に、SQL_DESC_DATA_PTR、SQL_DESC_INDICATOR_PTR、および SQL_DESC_OCTET_LENGTH_PTR フィールドに直接追加します。 オフセットが別の値に変更されると、新しい値は、記述子フィールドの値に直接追加されます。 新しいオフセットは、フィールドの値と、以前のオフセットには追加されません。<br /><br /> 詳細については、次を参照してください。[パラメーター バインド オフセット](../../../odbc/reference/develop-app/parameter-binding-offsets.md)します。<br /><br /> このステートメント属性を設定すると、APD ヘッダーで SQL_DESC_BIND_OFFSET_PTR フィールドが設定されます。|  
|SQL_ATTR_PARAM_BIND_TYPE (ODBC 3.0)|動的パラメーターに使用するバインディングの方向を示す sqlulen です値を指定します。<br /><br /> このフィールドは、列方向のバインドを選択する sql_param_bind_by_column です (既定値) に設定されます。<br /><br /> 行方向のバインドを選択するには、このフィールドは構造体、または一連の動的パラメーターにバインドされるバッファーのインスタンスの長さに設定されます。 この長さは、すべてのバインドされたパラメーターおよび構造体またはバインドされたパラメーターのアドレスが指定した長さでインクリメントされた場合は、結果は、次に、同じパラメーターの先頭にポイントすることを確認するバッファーの埋め込み用の領域を含める必要があります。パラメーターのセット。 使用する場合、 *sizeof* ANSI c 演算子は、この動作が保証されます。<br /><br /> 詳細については、次を参照してください。[パラメーターの配列のバインド](../../../odbc/reference/develop-app/binding-arrays-of-parameters.md)します。<br /><br /> このステートメント属性を設定すると、APD ヘッダーで SQL_DESC_ BIND_TYPE フィールドが設定されます。|  
|SQL_ATTR_PARAM_OPERATION_PTR (ODBC 3.0)|SQLUSMALLINT \* SQLUSMALLINT 値の配列を指す値を SQL ステートメントの実行中にパラメーターを無視するために使用します。 各値は、(実行のパラメーター) に対して SQL_PARAM_PROCEED または SQL_PARAM_IGNORE (のパラメーターが無視される) のいずれかに設定されます。<br /><br /> SQL_PARAM_IGNORE に APD の SQL_DESC_ARRAY_STATUS_PTR が指す配列で、状態値を設定して、処理中に一連のパラメーターを無視できます。 SQL_PARAM_PROCEED にその状態値が設定されている場合、または配列内の要素が設定されていない場合は、パラメーターのセットが処理されます。<br /><br /> このステートメント属性は、する場合、ドライバーは返しませんパラメーター状態値、null ポインターを設定できます。 この属性は、いつでも設定できますが、新しい値は、次の時間までは使用されません**SQLExecDirect**または**SQLExecute**が呼び出されます。<br /><br /> バインドされたパラメーターがない場合、この属性は無視されます。<br /><br /> 詳細については、次を参照してください。[パラメーターの配列を使用して](../../../odbc/reference/develop-app/using-arrays-of-parameters.md)します。<br /><br /> このステートメント属性を設定すると、APD ヘッダーで SQL_DESC_ARRAY_STATUS_PTR フィールドが設定されます。|  
|SQL_ATTR_PARAM_STATUS_PTR (ODBC 3.0)|SQLUSMALLINT\*値 SQLUSMALLINT の配列を指す値が呼び出しの後にパラメーター値の行ごとに状態情報を含む**SQLExecute**または**SQLExecDirect**します。 このフィールドは、PARAMSET_SIZE が 1 より大きい場合にのみ必要です。<br /><br /> 状態値は、次の値を含めることができます。<br /><br /> SQL_PARAM_SUCCESS:SQL ステートメントは、このパラメーターのセットを正常に実行されました。<br /><br /> SQL_PARAM_SUCCESS_WITH_INFO:SQL ステートメントがこのパラメーターのセットを正常に実行ただし、警告情報は、診断データの構造体で使用できます。<br /><br /> SQL_PARAM_ERROR:このパラメーターのセットの処理中にエラーが発生しました。 追加のエラー情報は、診断データの構造体で使用できます。<br /><br /> SQL_PARAM_UNUSED:このパラメーターのセットでしたに使用される、可能性があるためという事実にいくつか前のパラメーター セットには、さらに処理を中止エラーが発生しました。 または、SQL_ATTR_PARAM_OPERATION_PTR で指定された配列内のパラメーターのセットの SQL_PARAM_IGNORE が設定されているためです。<br /><br /> SQL_PARAM_DIAG_UNAVAILABLE:ドライバーは、モノリシックな単位としてパラメーターの配列を処理し、そのためこのレベルのエラー情報を生成しません。<br /><br /> このステートメント属性は、する場合、ドライバーは返しませんパラメーター状態値、null ポインターを設定できます。 この属性は、いつでも設定できますが、新しい値は、次の時間までは使用されません**SQLExecute**または**SQLExecDirect**が呼び出されます。 この属性の設定は影響、ドライバーによって実装されている出力パラメーターの動作に注意してください。<br /><br /> 詳細については、次を参照してください。[パラメーターの配列を使用して](../../../odbc/reference/develop-app/using-arrays-of-parameters.md)します。<br /><br /> このステートメント属性を設定すると、IPD ヘッダーで SQL_DESC_ARRAY_STATUS_PTR フィールドが設定されます。|  
|SQL_ATTR_PARAMS_PROCESSED_PTR (ODBC 3.0)|Sqlulen です\*で処理されて、エラーのセットを含むパラメーターのセットの数を返すバッファーを指すレコードのフィールド。 これが null ポインターの場合は、数は返されません。<br /><br /> このステートメント属性を設定すると、IPD ヘッダーで SQL_DESC_ROWS_PROCESSED_PTR フィールドが設定されます。<br /><br /> 場合に呼び出し**SQLExecDirect**または**SQLExecute**をこの属性によって指し示されるバッファー内の塗りつぶしが SQL_SUCCESS または sql_success_with_info が返されません、バッファーの内容は未定義です。<br /><br /> 詳細については、次を参照してください。[パラメーターの配列を使用して](../../../odbc/reference/develop-app/using-arrays-of-parameters.md)します。|  
|SQL_ATTR_PARAMSET_SIZE (ODBC 3.0)|各パラメーターの値の数を示す sqlulen です値を指定します。 SQL_ATTR_PARAMSET_SIZE が 1 より大きい場合は、SQL_DESC_DATA_PTR、SQL_DESC_INDICATOR_PTR、および、APD の SQL_DESC_OCTET_LENGTH_PTR 配列をポイントします。 各配列のカーディナリティは、このフィールドの値と同じです。<br /><br /> バインドされたパラメーターがない場合、この属性は無視されます。<br /><br /> 詳細については、次を参照してください。[パラメーターの配列を使用して](../../../odbc/reference/develop-app/using-arrays-of-parameters.md)します。<br /><br /> このステートメント属性を設定すると、APD ヘッダーで SQL_DESC_ARRAY_SIZE フィールドが設定されます。|  
|SQL_ATTR_QUERY_TIMEOUT (ODBC 1.0)|アプリケーションに返す前に実行する SQL ステートメントを待機する秒数に対応する sqlulen です値。 場合*ValuePtr*は 0 (既定値) に等しいか、タイムアウトはありません。<br /><br /> 指定したタイムアウトがデータ ソースのタイムアウトの最大値を超えていますまたは最小のタイムアウトよりも小さい場合**SQLSetStmtAttr**その値に置き換えられ、SQLSTATE 01S02 を返します (オプションの値が変更されました)。<br /><br /> アプリケーションを呼び出す必要はありませんので注意**SQLCloseCursor**場合、ステートメントを再利用する、**選択**ステートメントがタイムアウトしました。<br /><br /> このステートメント属性クエリ タイムアウトは、同期および非同期モードでは無効です。|  
|SQL_ATTR_RETRIEVE_DATA (ODBC 2.0)|Sqlulen です値の場合:<br /><br /> SQL_RD_ON = **SQLFetchScroll**と ODBC *3.x*、 **SQLFetch**指定した場所にカーソルを配置した後にデータを取得します。 既定値です。<br /><br /> SQL_RD_OFF = **SQLFetchScroll**と ODBC *3.x*、 **SQLFetch**カーソルを配置した後にデータを取得できません。<br /><br /> SQL_RETRIEVE_DATA SQL_RD_OFF に設定してアプリケーションは、行が存在するか、行が取得されるオーバーヘッドを発生させずに、行のブックマークを取得することを確認できます。 詳細については、次を参照してください。[のスクロールとフェッチ行](../../../odbc/reference/develop-app/scrolling-and-fetching-rows-odbc.md)します。<br /><br /> この属性の値は、開いているカーソル; に設定できます。ただし、設定がすぐに反映されませんである場合、ドライバーは SQLSTATE 01S02 を返します (オプションの値の変更) 元の値に属性をリセットします。|  
|SQL_ATTR_ROW_ARRAY_SIZE (ODBC 3.0)|各呼び出しによって返される行の数を示す sqlulen です値**SQLFetch**または**SQLFetchScroll**します。 一括ブックマーク操作で使用されるブックマーク配列内の行の数も**SQLBulkOperations**します。 既定値は 1 です。<br /><br /> ドライバーがその値に置き換えられ、SQLSTATE 01S02 を返します、指定した行セット サイズがデータ ソースでサポートされる最大の行セットのサイズを超える場合 (オプションの値が変更されました)。<br /><br /> 詳細については、次を参照してください。[行セット サイズ](../../../odbc/reference/develop-app/rowset-size.md)します。<br /><br /> このステートメント属性を設定すると、ARD ヘッダーで SQL_DESC_ARRAY_SIZE フィールドが設定されます。|  
|SQL_ATTR_ROW_BIND_OFFSET_PTR (ODBC 3.0)|Sqlulen です * 列のデータのバインドを変更へのポインターに追加のオフセットを示す値。 ドライバーにポインターを逆参照し、遅延のフィールド (SQL_DESC_DATA_PTR、SQL_DESC_INDICATOR_PTR、および SQL_DESC_OCTET_LENGTH_PTR) の記述子レコードのそれぞれに逆参照された値を追加し、新しいポインター値を使用してこのフィールドが null 以外の場合は、バインドするときにします。 設定されている既定では null にします。<br /><br /> このステートメント属性を設定すると、ARD ヘッダーで SQL_DESC_BIND_OFFSET_PTR フィールドが設定されます。|  
|SQL_ATTR_ROW_BIND_TYPE (ODBC 1.0)|バインディングの方向を設定する sqlulen です値ときに使用する**SQLFetch**または**SQLFetchScroll**が関連付けられているステートメントで呼び出されます。 値を SQL_BIND_BY_COLUMN に設定して、列方向のバインドが選択されます。 構造体または結果列のバインド先のバッファーのインスタンスの長さに値を設定して、行方向のバインドが選択されます。<br /><br /> すべてのバインドされた列および構造体またはバインドされた列のアドレスが指定した長さでインクリメントされた場合に、結果は番目の同じ列の先頭にポイントさせるバッファーの埋め込み用の領域を含める必要があります、長さが指定されている場合次の行の電子メール。 使用する場合、 **sizeof**構造体または共用体では、ANSI C 演算子は、この動作が保証されます。<br /><br /> 既定のバインディングの方向は、列方向のバインド**SQLFetch**と**SQLFetchScroll**します。<br /><br /> 詳細については、次を参照してください。[ブロック カーソルで使用するための列のバインド](../../../odbc/reference/develop-app/binding-columns-for-use-with-block-cursors.md)します。<br /><br /> このステートメント属性を設定すると、ARD ヘッダーで SQL_DESC_BIND_TYPE フィールドが設定されます。|  
|SQL_ATTR_ROW_NUMBER (ODBC 2.0)|全体の結果の現在の行の数をある sqlulen です値を設定します。 現在の行の数を特定できない、または現在の行がない、ドライバーは、0 を返します。<br /><br /> この属性への呼び出しで取得できる**SQLGetStmtAttr**への呼び出しで設定されていないが、 **SQLSetStmtAttr**します。|  
|SQL_ATTR_ROW_OPERATION_PTR (ODBC 3.0)|SQLUSMALLINT \* SQLUSMALLINT 値の配列を指す値を使用して一括操作中に行を無視するために使用**SQLSetPos**します。 各値は、(一括操作に含まれる行) の SQL_ROW_PROCEED または SQL_ROW_IGNORE (の一括操作から除外する行) のいずれかに設定されます。 (呼び出し中に、この配列を使用して行を無視できない**SQLBulkOperations**)。<br /><br /> このステートメント属性は、行の状態値は、ドライバーの場合に返されません、null ポインターを設定できます。 この属性は、いつでも設定できますが、新しい値は、次の時間までは使用されません**SQLSetPos**が呼び出されます。<br /><br /> 詳細については、次を参照してください。 [SQLSetPos による行セット内の行の更新](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md)と[SQLSetPos による行セットの行を削除する](../../../odbc/reference/develop-app/deleting-rows-in-the-rowset-with-sqlsetpos.md)します。<br /><br /> このステートメント属性を設定するで、ARD SQL_DESC_ARRAY_STATUS_PTR フィールドが設定されます。|  
|SQL_ATTR_ROW_STATUS_PTR (ODBC 3.0)|SQLUSMALLINT\*値 SQLUSMALLINT の配列を指す値が呼び出しの後に行の状態値を含む**SQLFetch**または**SQLFetchScroll**します。 配列には、行セット内の行がある多くの要素があります。<br /><br /> このステートメント属性は、行の状態値は、ドライバーの場合に返されません、null ポインターを設定できます。 この属性は、いつでも設定できますが、新しい値は、次の時間までは使用されません**SQLBulkOperations**、 **SQLFetch**、 **SQLFetchScroll**、または**SQLSetPos**が呼び出されます。<br /><br /> 詳細については、次を参照してください。[フェッチされた行の数と状態](../../../odbc/reference/develop-app/number-of-rows-fetched-and-status.md)します。<br /><br /> このステートメント属性を設定すると、IRD のヘッダーで SQL_DESC_ARRAY_STATUS_PTR フィールドが設定されます。<br /><br /> この属性は、ODBC によってマップされて*2.x*ドライバー、 *rgbRowStatus*配列への呼び出しで**SQLExtendedFetch**します。|  
|SQL_ATTR_ROWS_FETCHED_PTR (ODBC 3.0)|Sqlulen です\*呼び出しの後にフェッチされた行の数を返す先のバッファーを指す値**SQLFetch**または**SQLFetchScroll**; 実行一括操作によって影響を受ける行の数呼び出して**SQLSetPos**で、*操作*SQL_REFRESH; またはを実行する一括操作によって影響を受ける行の数の引数**SQLBulkOperations**. この数値には、エラー行が含まれます。<br /><br /> 詳細については、次を参照してください。[フェッチされた行の数と状態](../../../odbc/reference/develop-app/number-of-rows-fetched-and-status.md)します。<br /><br /> このステートメント属性を設定すると、IRD のヘッダーで SQL_DESC_ROWS_PROCESSED_PTR フィールドが設定されます。<br /><br /> 場合に呼び出し**SQLFetch**または**SQLFetchScroll**をこの属性によって指し示されるバッファー内の塗りつぶしが SQL_SUCCESS または sql_success_with_info が返されません、バッファーの内容は未定義です。|  
|SQL_ATTR_SIMULATE_CURSOR (ODBC 2.0)|配置をシミュレートするドライバーが update および delete ステートメントであるかどうかを示す sqlulen です値をこのようなステートメントが 1 つだけの単一行に影響することを保証します。<br /><br /> ほとんどのドライバーを作成、検索結果を位置指定更新をシミュレートし、delete ステートメント、**更新**または**削除**ステートメントを含む、**場所**句を指定する、現在の行の各列の値。 これらの列は、一意のキーを構成、しない限り、このようなステートメントは、複数の行に影響します。<br /><br /> このようなステートメントに 1 行のみが影響を確実には、ドライバーは、一意のキーで列を決定し、結果セットにこれらの列を追加します。 アプリケーションが結果セット内の列が一意のキーを構成することを保証する場合、ドライバーはこれを行うには必要ありません。 これにより、実行時間が減少する可能性があります。<br /><br /> SQL_SC_NON_UNIQUE = ドライバーはシミュレートされた保証しない更新または位置指定 delete ステートメントが 1 つだけ行に影響を与えるそのためには、アプリケーションの役目です。 ステートメントが 1 つ以上の行に影響する場合**SQLExecute**、 **SQLExecDirect**、または**SQLSetPos** SQLSTATE 01001 (カーソル操作の競合) を返します。<br /><br /> SQL_SC_TRY_UNIQUE = シミュレートされた更新プログラムを配置することを保証するドライバー試行またはステートメントの影響の 1 つだけ行を削除します。 ドライバーは、このようなステートメントを常に実行する場合など、複数の行に影響を与える可能性がある場合でも一意のキーはありません。 ステートメントが 1 つ以上の行に影響する場合**SQLExecute**、 **SQLExecDirect**、または**SQLSetPos** SQLSTATE 01001 (カーソル操作の競合) を返します。<br /><br /> SQL_SC_UNIQUE =、位置指定更新をシミュレートするドライバーの保証またはステートメントの影響の 1 つだけ行を削除します。 ドライバーは、特定のステートメントにこれを保証できない場合**SQLExecDirect**または**SQLPrepare**はエラーを返します。<br /><br /> データ ソースは、ドライバーは、カーソルをシミュレートしませんし、ネイティブ SQL が位置指定更新のサポート、および delete ステートメントを提供する場合は、SQL_SIMULATE_CURSOR の SQL_SC_UNIQUE が要求されたときに SQL_SUCCESS が返されます。 SQL_SC_TRY_UNIQUE または SQL_SC_NON_UNIQUE が要求された場合、SQL_SUCCESS_WITH_INFO が返されます。 データ ソースが SQL_SC_TRY_UNIQUE レベルのサポートを提供し、ドライバーは、SQL_SC_NON_UNIQUE の SQL_SC_TRY_UNIQUE、SQL_SUCCESS_WITH_INFO が返されますの SQL_SUCCESS が返されます。<br /><br /> ドライバーがさまざまなシミュレーションの種類に置き換えられ、SQLSTATE 01S02 を返します、指定したカーソルのシミュレーションの種類が、データ ソースでサポートされていない場合 (オプションの値が変更されました)。 SQL_SC_UNIQUE、ドライバーに置き換えます、SQL_SC_TRY_UNIQUE または SQL_SC_NON_UNIQUE の順序で。 SQL_SC_TRY_UNIQUE、ドライバーは SQL_SC_NON_UNIQUE を置き換えます。<br /><br /> 既定では SQL_SC_UNIQUE です。<br /><br /> 詳細については、次を参照してください。[をシミュレートする配置の更新と削除ステートメント](../../../odbc/reference/develop-app/simulating-positioned-update-and-delete-statements.md)します。|  
|SQL_ATTR_USE_BOOKMARKS (ODBC 2.0)|アプリケーションがブックマークを使用してカーソルがあるかどうかを示す sqlulen です値:<br /><br /> SQL_UB_OFF = Off (既定)<br /><br /> SQL_UB_VARIABLE = アプリケーションでは、ブックマークを使用して、カーソルでは、サポートされている場合にドライバーが可変長のブックマークを提供します。 ODBC SQL_UB_FIXED は非推奨*3.x*します。 ODBC *3.x* ODBC を使って作業する場合でも、アプリケーションは可変長のブックマークの使用をして常に*2.x*ドライバー (これだけの 4 バイトの固定長のブックマークがサポートされています)。 これは、固定長のブックマークが可変長のブックマークの特殊なケースだけであるためです。 ODBC を使用する場合*2.x*ドライバー、ドライバー マネージャーで、SQL_UB_FIXED に SQL_UB_VARIABLE がマップされます。<br /><br /> カーソルでブックマークを使用するには、アプリケーションする必要がありますこの属性を指定 SQL_UB_VARIABLE 値を持つ、カーソルを開く前にします。<br /><br /> 詳細については、次を参照してください。[を取得するブックマーク](../../../odbc/reference/develop-app/retrieving-bookmarks.md)します。|  
  
 [1] にはこれらの関数は、記述子が、実装の記述子アプリケーション記述子ではない場合にのみ、非同期的に呼び出すことができます。  
  
 参照してください[列方向のバインド](../../../odbc/reference/develop-app/column-wise-binding.md)と[行方向のバインド](../../../odbc/reference/develop-app/row-wise-binding.md)します。  
  
## <a name="related-functions"></a>関連する関数  
  
|詳細|参照先|  
|---------------------------|---------|  
|ステートメントの処理をキャンセル|[SQLCancel 関数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|接続属性の設定を返す|[SQLGetConnectAttr 関数](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|ステートメント属性の設定を返す|[SQLGetStmtAttr 関数](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)|  
|接続属性の設定|[SQLSetConnectAttr 関数](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|記述子の 1 つのフィールドを設定|[SQLSetDescField 関数](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
  
## <a name="see-also"></a>参照  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)
