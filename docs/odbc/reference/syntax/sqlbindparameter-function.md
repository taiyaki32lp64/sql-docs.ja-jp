---
title: SQLBindParameter 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLBindParameter
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLBindParameter
helpviewer_keywords:
- SQLBindParameter function [ODBC]
ms.assetid: 38349d4b-be03-46f9-9d6a-e50dd144e225
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 65f6145f0cbfbd59fffb71e030f6427ea1f551c0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68036210"
---
# <a name="sqlbindparameter-function"></a>SQLBindParameter 関数

**準拠**  
 バージョンが導入されました。ODBC 2.0 の規格に準拠します。ODBC  
  
 **概要**  
 **SQLBindParameter**バッファーを SQL ステートメントでパラメーター マーカーにバインドします。 **SQLBindParameter**基になるドライバーが Unicode データをサポートしていない場合でも、Unicode の C データ型へのバインドをサポートしています。  
  
> [!NOTE]  
>  この関数が ODBC 1.0 関数に置き換えられます**SQLSetParam**します。 詳細については、「コメントです。」を参照してください。  
  
## <a name="syntax"></a>構文  
  
```cpp
  
SQLRETURN SQLBindParameter(  
      SQLHSTMT        StatementHandle,  
      SQLUSMALLINT    ParameterNumber,  
      SQLSMALLINT     InputOutputType,  
      SQLSMALLINT     ValueType,  
      SQLSMALLINT     ParameterType,  
      SQLULEN         ColumnSize,  
      SQLSMALLINT     DecimalDigits,  
      SQLPOINTER      ParameterValuePtr,  
      SQLLEN          BufferLength,  
      SQLLEN *        StrLen_or_IndPtr);  
```
  
## <a name="arguments"></a>引数

 *StatementHandle*  
 [入力]ステートメント ハンドルです。  
  
 *ParameterNumber*  
 [入力]パラメーターの数、順序付けられた順番に増加のパラメーターの順序で 1 から始まります。  
  
 *InputOutputType*  
 [入力]パラメーターの型。 詳細については、次を参照してください"*InputOutputType*引数"で"コメントです。"。  
  
 *ValueType*  
 [入力]パラメーターの C データ型。 詳細については、次を参照してください"*ValueType*引数"で"コメントです。"。  
  
 *ParameterType*  
 [入力]パラメーターの SQL データ型。 詳細については、次を参照してください"*ParameterType*引数"で"コメントです。"。  
  
 *ColumnSize*  
 [入力]対応するパラメーター マーカーの式または列のサイズ。 詳細については、次を参照してください"*ColumnSize*引数"で"コメントです。"。  
  
 場合は、64 ビット Windows オペレーティング システムでは、アプリケーションを実行してを参照してください。 [ODBC 64 ビットの情報](../../../odbc/reference/odbc-64-bit-information.md)します。  
  
 *DecimalDigits*  
 [入力]対応するパラメーター マーカーの式または列の 10 進数字。 列のサイズの詳細については、次を参照してください。[列のサイズ、10 進数字、転送オクテット長、および表示サイズ](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)します。  
  
 *ParameterValuePtr*  
 [遅延の入力]パラメーターのデータを格納するバッファーへのポインター。 詳細については、次を参照してください"*ParameterValuePtr*引数"で"コメントです。"。  
  
 *BufferLength*  
 [入力/出力]長さ、 *ParameterValuePtr*バッファー (バイト単位)。 詳細については、次を参照してください"*BufferLength*引数"で"コメントです。"。  
  
 参照してください[ODBC 64 ビットの情報](../../../odbc/reference/odbc-64-bit-information.md)場合、アプリケーションが 64 ビットのオペレーティング システムで実行します。  
  
 *StrLen_or_IndPtr*  
 [遅延の入力]パラメーターの長さを格納するバッファーへのポインター。 詳細については、次を参照してください"*StrLen_or_IndPtr*引数"で"コメントです。"。  
  
## <a name="returns"></a>戻り値

 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR、または SQL_INVALID_HANDLE します。  
  
## <a name="diagnostics"></a>診断

 ときに**SQLBindParameter** SQL_ERROR または SQL_SUCCESS_WITH_INFO、関連付けられている SQLSTATE 値を返しますを呼び出すことによって取得できる**SQLGetDiagRec**で、 *HandleType*のSql_handle_stmt として、*処理*の*StatementHandle*します。 次の表に、によって返される通常の SQLSTATE 値**SQLBindParameter** ; この関数のコンテキストでそれぞれについて説明しますと表記"(DM)"の前にドライバー マネージャーによって返されるについての説明。 SQLSTATE 値ごとに関連付けられているリターン コードは明記しない限り、SQL_ERROR です。  

|SQLSTATE|[エラー]|説明|  
|--------------|-----------|-----------------|  
|01000|一般的な警告|ドライバー固有の情報メッセージです。 (関数は、SQL_SUCCESS_WITH_INFO を返します)。|  
|07006|制限付きのデータ型の属性違反|識別されるデータ型、 *ValueType*で識別されるデータ型に変換できない引数、 *ParameterType*引数。 このエラーは、によって返される可能性がありますに注意してください**SQLExecDirect**、 **SQLExecute**、または**SQLPutData**別ではなく、実行時に**SQLBindParameter**.|  
|07009|無効な記述子のインデックス|引数に指定された値 (DM) *ParameterNumber* 1 より小さいをでした。|  
|HY000|一般的なエラー|これがなかった固有の SQLSTATE とする実装に固有の SQLSTATE が定義されていない、エラーが発生しました。 によって返されるエラー メッセージ**SQLGetDiagRec**で、**MessageText*バッファーは、エラーとその原因について説明します。|  
|HY001|メモリの割り当てエラー|ドライバーは、実行または関数の完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY003|無効なアプリケーション バッファーの種類|引数で指定された値*ValueType*有効な C データ型または SQL_C_DEFAULT ありませんでした。|  
|HY004|無効な SQL データ型|引数が指定された値*ParameterType*が ODBC SQL データ型の有効な識別子でも、ドライバーでサポートされている個々 のドライバーの SQL データ型識別子。|  
|HY009|無効な引数値|(DM) 引数*ParameterValuePtr*が null ポインターの場合、引数*StrLen_or_IndPtr*が null ポインターの場合は、および引数*InputOutputType* SQL_PARAM_ でした出力します。<br /><br /> (DM) SQL_PARAM_OUTPUT、位置引数*ParameterValuePtr*が null ポインターの場合は、C 型が文字またはバイナリ、および、BufferLength (*cbValueMax*) が 0 より大きかった。|  
|HY010|関数のシーケンス エラー|(DM) を非同期的に実行中の関数が呼び出された接続ハンドルに関連付けられているため、 *StatementHandle*します。 この非同期関数ではときに実行されている**SQLBindParameter**が呼び出されました。<br /><br /> (DM) **SQLExecute**、 **SQLExecDirect**、または**SQLMoreResults**に対して呼び出された、 *StatementHandle* SQL_PARAM_DATA_ を返されます。ご利用いただけます。 ストリームのすべてのパラメーターのデータが取得される前に、この関数が呼び出されました。<br /><br /> (DM) を非同期的に実行中の関数が呼び出された、 *StatementHandle*この関数が呼び出されたときに実行されているとします。<br /><br /> (DM) **SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**、または**SQLSetPos**に対して呼び出された、 *StatementHandle* SQL_NEED_DATA が返されます。 すべての実行時データ パラメーターまたは列のデータが送信される前に、この関数が呼び出されました。|  
|HY013|メモリ管理エラー|基になるメモリ オブジェクトにアクセスできませんでした、場合によってメモリ不足が原因であるために、関数呼び出しを処理できませんでした。|  
|HY021|不整合な記述子情報|整合性チェック中にチェックする記述子の情報は、一貫性のあるでした。 (整合性チェック」セクションを参照して**SQLSetDescField**)。<br /><br /> 引数が指定された値*DecimalDigits*がで指定された SQL データ型の列のデータ ソースによってサポートされる値の範囲外の*ParameterType*引数。|  
|HY090|文字列またはバッファーの長さが無効です。|(DM) の値*BufferLength*が 0 未満でした。 (SQL_DESC_DATA_PTR フィールドの説明を参照して**SQLSetDescField**)。|  
|HY104|有効桁数または小数点以下桁数の値が無効です。|引数が指定された値*ColumnSize*または*DecimalDigits*がで指定された SQL データ型の列のデータ ソースによってサポートされる値の範囲外の*ParameterType*引数。|  
|HY105|無効なパラメーターの型|引数に指定された値 (DM) *InputOutputType*が無効です。 (「コメントです」を参照してください)|  
|HY117|不明なトランザクションの状態のため、接続が中断されます。 のみを切断して、読み取り専用の関数が許可されます。|(DM) 中断状態の詳細については、次を参照してください。 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)します。|  
|HYC00|省略可能な機能が実装されていません|ドライバーまたはデータ ソースは、引数に指定された値の組み合わせで指定された変換をサポートしていません*ValueType*引数が指定されたドライバー固有の値と*ParameterType*.<br /><br /> 引数が指定された値*ParameterType* ODBC SQL データ型の有効な識別子が ODBC のバージョンのドライバーをサポートしていますが、ドライバーまたはデータ ソースでサポートされていませんでした。<br /><br /> ドライバーには、ODBC 2 のみがサポートしています。*x*と引数*ValueType*が、次のいずれか。<br /><br /> SQL_C_NUMERIC SQL_C_SBIGINT SQL_C_UBIGINT<br /><br /> 間隔 C のすべてのデータ型と[C データ型](../../../odbc/reference/appendixes/c-data-types.md)付録 d:データ型。<br /><br /> ドライバーのみ、3.50 と引数の前に ODBC バージョンをサポートする*ValueType* SQL_C_GUID でした。|  
|HYT01|接続がタイムアウトしました|データ ソースが要求に応答する前に、接続のタイムアウト期間が終了しました。 によって、接続タイムアウト期間が設定されます**SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT します。|  
|IM001|ドライバーでは、この関数はサポートされていません|(DM) に、ドライバーが関連付けられている、 *StatementHandle*関数をサポートしていません。|  
  
## <a name="comments"></a>コメント

 アプリケーションを呼び出す**SQLBindParameter** SQL ステートメント内の各パラメーター マーカーをバインドします。 バインドは、アプリケーションが有効になります**SQLBindParameter** 、もう一度呼び出す**SQLFreeStmt** SQL_RESET_PARAMS オプション、または呼び出し**SQLSetDescField**にAPD の SQL_DESC_COUNT ヘッダー フィールドを 0 に設定します。  
  
 パラメーターの詳細については、次を参照してください。[ステートメント パラメーター](../../../odbc/reference/develop-app/statement-parameters.md)します。 パラメーターのデータ型とパラメーター マーカーの詳細については、次を参照してください[パラメーターのデータ型](../../../odbc/reference/appendixes/parameter-data-types.md)と[パラメーター マーカー](../../../odbc/reference/appendixes/parameter-markers.md)付録 c:。SQL 文法。  
  
## <a name="parameternumber-argument"></a>ParameterNumber 引数  
 場合*ParameterNumber*への呼び出しで**SQLBindParameter** SQL_DESC_COUNT の値よりも大きい**SQLSetDescField** SQL_DESC_ の価値を高めるために呼び出されるカウント*ParameterNumber*します。  
  
## <a name="inputoutputtype-argument"></a>InputOutputType 引数  
 *InputOutputType*引数のパラメーターの型を指定します。 この引数は、IPD の SQL_DESC_PARAMETER_TYPE フィールドを設定します。 など、プロシージャを呼び出さない SQL ステートメントのすべてのパラメーター**挿入**ステートメント、*入力 * * パラメーター*します。 プロシージャ呼び出しのパラメーター入力として使用できる、入力/出力、または出力パラメーター。 (アプリケーションを呼び出す**SQLProcedureColumns** ; プロシージャ呼び出しでパラメーターの種類を決定するパラメーターの型が決まることはできませんが入力パラメーターであると見なされます)。  
  
 *InputOutputType*引数は、次の値のいずれか。  
  
-   SQL_PARAM_INPUT します。 パラメーターなど、プロシージャを呼び出しませんする SQL ステートメント内のパラメーターをマークする、**挿入**ステートメント、またはそのプロシージャ内の入力パラメーターをマークします。 内のパラメーターなど**従業員の値を挿入 (でしょうか、?、でしょうか。)。** は入力パラメーターでは、パラメーター **{AddEmp を呼び出す (ですか?、ですか?、ですか?)}** できますが、必ずしも、入力パラメーターではありません。  
  
     ステートメントが実行されたときにドライバーが、データ ソースにパラメーターのデータを送信します。\* *ParameterValuePtr*バッファーは有効な入力値を含める必要があります、または **StrLen_or_IndPtr*バッファーが SQL_NULL_DATA、生成される場合、または、SQL_LEN_DATA_AT の結果に含める必要があります_Exec 系マクロです。  
  
     設定されている場合は、プロシージャ呼び出しでパラメーターの型を判断できないのは、アプリケーション、 *InputOutputType* SQL_PARAM_INPUT 以外に、データ ソースは、パラメーターの値を返す場合、ドライバーにそれを廃棄します。  
  
-   SQL_PARAM_INPUT_OUTPUT します。 パラメーターは、プロシージャ内の入力/出力パラメーターをマークします。 内のパラメーターなど、 **{call GetEmpDept(?)}** 入力/出力パラメーターで、従業員の名前を受け取り、従業員の部署の名前を返します。  
  
     ステートメントが実行されたときにドライバーが、データ ソースにパラメーターのデータを送信します。\* *ParameterValuePtr*バッファーは有効な入力値を含める必要がありますまたは\* *StrLen_or_IndPtr* SQL_NULL_DATA、生成される場合、または結果のバッファーを含める必要がありますSQL_LEN_DATA_AT_EXEC マクロです。 ステートメントが実行された後に、ドライバーは、アプリケーション パラメーターのデータを返しますドライバーの設定、データ ソースが、入力/出力パラメーターの値を返さない場合、**StrLen_or_IndPtr* SQL_NULL_DATA をバッファーします。  
  
    > [!NOTE]  
    >  ODBC 1.0 アプリケーションを呼び出すと**SQLSetParam**への呼び出しにこのドライバー マネージャーによって、ODBC 2.0 ドライバーの変換**SQLBindParameter**を*InputOutputType*引数は、SQL_PARAM_INPUT_OUTPUT に設定されます。  
  
-   SQL_PARAM_OUTPUT します。 パラメーターは、プロシージャまたはプロシージャの出力パラメーターの戻り値をマークします。いずれの場合も、これらと呼ばれます。*出力パラメーター*します。 内のパラメーターなど、 **{? = GetNextEmpID を呼び出す}** 出力パラメーターで、[次へ] の従業員 ID を返します。  
  
     しない限り、ドライバーが、アプリケーションに、パラメーターのデータを返します、ステートメントが実行された後、 *ParameterValuePtr*と*StrLen_or_IndPtr*引数は、どちらも null ポインターでは、この場合、ドライバーは、出力値を破棄します。 ドライバーの設定、データ ソースが出力パラメーターの値を返さない場合、**StrLen_or_IndPtr* SQL_NULL_DATA をバッファーします。  
  
-   SQL_PARAM_INPUT_OUTPUT_STREAM します。 入力/出力パラメーターをストリーミングすることを示します。 **SQLGetData**部分のパラメーター値を読み取ることができます。 *BufferLength*バッファーの長さは、の呼び出しで判断するために無視**SQLGetData**します。 値、 *StrLen_or_IndPtr*バッファーが SQL_NULL_DATA、SQL_DEFAULT_PARAM、生成される場合、または SQL_LEN_DATA_AT_EXEC マクロの結果に含める必要があります。 出力にストリーミングされる場合、入力データで実行 (DAE) パラメーターとしてパラメーターをバインドする必要があります。 *ParameterValuePtr*によって返される null 以外のポインター値を指定できます**SQLParamData**トークンの値を持つユーザー定義としてで渡された*ParameterValuePtr*の両方の入力と出力します。 詳細については、次を参照してください。 [SQLGetData を使用して出力パラメーターを取得する](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)します。  
  
-   SQL_PARAM_OUTPUT_STREAM します。 SQL_PARAM_INPUT_OUTPUT_STREAM、出力パラメーターのと同じです。 * *StrLen_or_IndPtr*入力は無視されます。  
  
 次の表に、さまざまな組み合わせの*InputOutputType*と **StrLen_or_IndPtr*:  
  
|*InputOutputType*|**StrLen_or_IndPtr*|結果|ParameterValuePtr をコメントします。|  
|-----------------------|----------------------------|-------------|---------------------------------|  
|SQL_PARAM_INPUT|SQL_LEN_DATA_AT_EXEC (*len*) または SQL_DATA_AT_EXEC|入力のパーツ|*ParameterValuePtr*によって返されるポインター値を指定できます**SQLParamData**トークンの値を持つユーザー定義としてで渡された*ParameterValuePtr*します。|  
|SQL_PARAM_INPUT|いない SQL_LEN_DATA_AT_EXEC (*len*) または SQL_DATA_AT_EXEC|入力バッファーをバインドします。|*ParameterValuePtr*は入力バッファーのアドレスです。|  
|SQL_PARAM_OUTPUT|入力は無視されます。|出力バッファーをバインドします。|*ParameterValuePtr*は出力バッファーのアドレスです。|  
|SQL_PARAM_OUTPUT_STREAM|入力は無視されます。|ストリーミングされる出力|*ParameterValuePtr*によって返される任意のポインター値を指定できます**SQLParamData**トークンの値を持つユーザー定義としてで渡された*ParameterValuePtr*します。|  
|SQL_PARAM_INPUT_OUTPUT|SQL_LEN_DATA_AT_EXEC (*len*) または SQL_DATA_AT_EXEC|部分で入力と出力のバインドされたバッファー|*ParameterValuePtr*によって返されることも、出力バッファーのアドレスは、 **SQLParamData**トークンの値を持つユーザー定義としてで渡された*ParameterValuePtr*します。|  
|SQL_PARAM_INPUT_OUTPUT|いない SQL_LEN_DATA_AT_EXEC (*len*) または SQL_DATA_AT_EXEC|入力は、バッファーと出力のバインドされたバッファーのバインド|*ParameterValuePtr*共有入力/出力バッファーのアドレスです。|
|SQL_PARAM_INPUT_OUTPUT_STREAM|SQL_LEN_DATA_AT_EXEC (*len*) または SQL_DATA_AT_EXEC|入力のパーツとストリーミングされる出力|*ParameterValuePtr*によって返される任意の null 以外のポインター値を指定できます**SQLParamData**トークンの値を持つユーザー定義としてで渡された*ParameterValuePtr*の両方の入力出力します。|  
  
> [!NOTE]  
>  ドライバーは、ストリーム出力パラメーターまたは入出力パラメーターをアプリケーションがバインド時に、どの SQL 型が許可されますを決める必要があります。 ドライバー マネージャーでは、無効な SQL 型のエラーは生成されません。  
  
## <a name="valuetype-argument"></a>ValueType 引数

 *ValueType*引数のパラメーターの C データ型を指定します。 この引数は、APD の SQL_DESC_TYPE、SQL_DESC_CONCISE_TYPE、および SQL_DESC_DATETIME_INTERVAL_CODE フィールドを設定します。 内の値のいずれかにあるこの必要があります、 [C データ型](../../../odbc/reference/appendixes/c-data-types.md)付録 d: のセクションデータ型。  
  
 場合、 *ValueType*引数は、間隔のデータ型の SQL_DESC_TYPE フィールドの 1 つ、 *ParameterNumber* SQL_INTERVAL に APD のレコードが設定されている、APD の SQL_DESC_CONCISE_TYPE フィールドに設定されます簡潔な間隔のデータ型との SQL_DESC_DATETIME_INTERVAL_CODE フィールド、 *ParameterNumber*レコードが特定の間隔のデータ型のサブコードに設定されます。 (を参照してください[付録 d:データ型](../../../odbc/reference/appendixes/appendix-d-data-types.md))。既定の間隔、APD の SQL_DESC_DATETIME_INTERVAL_PRECISION および SQL_DESC_PRECISION のフィールドで設定されている有効桁数 (2) と既定の間隔の秒の有効桁数 (6) をそれぞれ、先頭は、データに使用されます。 いずれかの既定の精度が適切でない場合、アプリケーションする必要があります明示的に設定記述子フィールドへの呼び出しによって**SQLSetDescField**または**SQLSetDescRec**します。  
  
 場合、 *ValueType*引数は、datetime データ型の SQL_DESC_TYPE フィールドの 1 つ、 *ParameterNumber* APD のレコードが SQL_DATETIME、のSQL_DESC_CONCISE_TYPEフィールドに設定されている*ParameterNumber* APD のレコードが、簡潔な datetime C データ型との SQL_DESC_DATETIME_INTERVAL_CODE フィールドに設定されている、 *ParameterNumber*レコードが特定の日時のサブコードに設定されています。データを入力します。 (を参照してください[付録 d:データ型](../../../odbc/reference/appendixes/appendix-d-data-types.md))。  
  
 場合、 *ValueType*引数は SQL_C_NUMERIC データ型、(これは、ドライバーで定義) の既定の精度であり (0)、既定の小数点として、APD の SQL_DESC_PRECISION および SQL_DESC_SCALE のフィールド セットはデータに使用します。 アプリケーションがへの呼び出しで記述子フィールドを設定する必要があります明示的に既定の有効桁数または小数点が適切でない場合**SQLSetDescField**または**SQLSetDescRec**します。  
  
 SQL_C_DEFAULT は、すべてのユーザーを SQL データ型がで指定、既定の C データ型から転送されるパラメーターの値を指定します*ParameterType*します。  
  
 拡張の C データ型を指定することもできます。 詳細については、次を参照してください。 [ODBC における C データ型](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)します。  
  
 詳細については、次を参照してください[C データ型の既定の](../../../odbc/reference/appendixes/default-c-data-types.md)、 [C から SQL データ型への変換データ](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)、および[SQL から C データ型への変換データ](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)付録 d:。データ型。  
  
## <a name="parametertype-argument"></a>ParameterType 引数

 記載した値のいずれかにあるこの必要があります、 [SQL データ型](../../../odbc/reference/appendixes/sql-data-types.md)付録 d: のセクションデータ型、またはそれには、ドライバー固有の値がある場合があります。 この引数は、IPD の SQL_DESC_TYPE、SQL_DESC_CONCISE_TYPE、および SQL_DESC_DATETIME_INTERVAL_CODE フィールドを設定します。  
  
 場合、 *ParameterType*引数は、datetime 識別子のいずれか、SQL_DATETIME に IPD の SQL_DESC_TYPE フィールドが設定されている、IPD の SQL_DESC_CONCISE_TYPE フィールド簡潔な datetime の SQL データ型と、SQL_DESC_ に設定されますDATETIME_INTERVAL_CODE フィールドは、適切な datetime サブコード値に設定されます。  
  
 場合*ParameterType*は 1 つ SQL_INTERVAL に設定されている、IPD の SQL_DESC_TYPE フィールドの間隔の識別子、IPD の SQL_DESC_CONCISE_TYPE フィールド簡潔な SQL interval データ型と、SQL_DESC_DATETIME_ に設定されますIPD の INTERVAL_CODE フィールドは、適切な間隔サブコードに設定されます。 IPD の SQL_DESC_DATETIME_INTERVAL_PRECISION フィールドが間隔の先頭有効桁数に設定され、該当する場合、間隔の秒の有効桁数を SQL_DESC_PRECISION フィールドが設定されます。 アプリケーションが呼び出すことによって明示的に設定 SQL_DESC_DATETIME_INTERVAL_PRECISION または SQL_DESC_PRECISION の既定値が適切でない場合必要があります、 **SQLSetDescField**します。 これらのフィールドのいずれかの詳細については、次を参照してください。 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)します。  
  
 場合、 *ValueType*引数が SQL_NUMERIC データ型、既定の有効桁数 (これは、ドライバーで定義) と既定スケール (0)、IPD の SQL_DESC_PRECISION および SQL_DESC_SCALE のフィールド セットとして、データに使用します。 アプリケーションがへの呼び出しで記述子フィールドを設定する必要があります明示的に既定の有効桁数または小数点が適切でない場合**SQLSetDescField**または**SQLSetDescRec**します。  
  
 データを変換する方法については、次を参照してください[C から SQL データ型への変換データ](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)と[SQL から C データ型への変換データ](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)付録 d:。データ型。  
  
## <a name="columnsize-argument"></a>ColumnSize 引数

 *ColumnSize*引数が列またはパラメーター マーカー、そのデータ、または両方の長さに対応する式のサイズを指定します。 この引数は、SQL データ型に応じて、IPD のさまざまなフィールドを設定します。 (、 *ParameterType*引数)。 このマッピングに、次の規則が適用されます。  
  
-   場合*ParameterType* SQL_CHAR、SQL_VARCHAR、SQL_LONGVARCHAR、SQL_BINARY、SQL_VARBINARY、SQL_LONGVARBINARY、またはの値に設定されている、簡潔なSQLdatetimeまたは間隔、データ型のIPDのSQL_DESC_LENGTHフィールド*ColumnSize*します。 (詳細については、次を参照してください、[列のサイズ、10 進数字、転送オクテット長、および表示サイズ](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)付録 d: セクション。データ型です。)  
  
-   場合*ParameterType* SQL_DECIMAL、SQL_NUMERIC、使用できます、SQL_REAL、または SQL_DOUBLE、IPD の SQL_DESC_PRECISION フィールドの値に設定されます*ColumnSize*します。  
  
-   他のデータ型の*ColumnSize*引数は無視されます。  
  
 詳細については、「パラメーターの値を渡す」と SQL_DATA_AT_EXEC で参照してください"*StrLen_or_IndPtr*引数"。  
  
## <a name="decimaldigits-argument"></a>DecimalDigits 引数

 場合*ParameterType* SQL_TYPE_TIME、SQL_TYPE_TIMESTAMP、SQL_INTERVAL_SECOND、SQL_INTERVAL_DAY_TO_SECOND、SQL_INTERVAL_HOUR_TO_SECOND、または SQL_INTERVAL_MINUTE_TO_SECOND、IPD の SQL_DESC_PRECISION フィールドが設定されます*DecimalDigits*します。 場合*ParameterType* SQL_NUMERIC または SQL_DECIMAL、IPD の SQL_DESC_SCALE フィールドに設定されて*DecimalDigits*します。 その他のすべてのデータ型の*DecimalDigits*引数は無視されます。  
  
## <a name="parametervalueptr-argument"></a>ParameterValuePtr 引数

 *ParameterValuePtr*引数が指すバッファーされるときに、 **SQLExecute**または**SQLExecDirect**を呼び出すと、パラメーターの実際のデータが含まれています。 データがで指定された形式である必要があります、 *ValueType*引数。 この引数は、APD の SQL_DESC_DATA_PTR フィールドを設定します。 アプリケーションで設定でき、 *ParameterValuePtr*引数を null ポインターでは、同じくらい *\*StrLen_or_IndPtr* SQL_NULL_DATA または SQL_DATA_AT_EXEC です。 (これは適用のみを入力パラメーターまたは入力/出力パラメーターです)。  
  
 場合\* *StrLen_or_IndPtr* 、SQL_LEN_DATA_AT_EXEC の結果です (*長さ*) マクロまたは SQL_DATA_AT_EXEC し*ParameterValuePtr*が、パラメーターに関連付けられているアプリケーション定義のポインター値です。 経由でアプリケーションに返される**SQLParamData**します。 たとえば、 *ParameterValuePtr* 0 以外のトークン パラメーターの数、データへのポインター、またはアプリケーションの入力パラメーターをバインドするために使用する構造体へのポインターなどがあります。 ただし、その場合、パラメーターが入力/出力パラメーター、 *ParameterValuePtr*出力値を格納するバッファーへのポインターである必要があります。 SQL_ATTR_PARAMSET_SIZE ステートメント属性の値が 1 より大きい場合は、アプリケーションは、と共に、SQL_ATTR_PARAMS_PROCESSED_PTR ステートメント属性によって示される値を使用できます、 *ParameterValuePtr*引数。 たとえば、 *ParameterValuePtr*値の配列をポイントして、アプリケーションは、SQL_ATTR_PARAMS_PROCESSED_PTR によって示される値を使用して配列から適切な値を取得する可能性があります。 詳細については、このセクションで後で「パラメーター値のを渡す」を参照してください。  
  
 場合、 *InputOutputType*引数が SQL_PARAM_INPUT_OUTPUT または SQL_PARAM_OUTPUT、 *ParameterValuePtr*ドライバーが出力値を返すバッファーを指します。 プロシージャは、1 つまたは複数の結果セットを返す場合、 \* *ParameterValuePtr*バッファーは、すべての結果セットや行のカウントが処理されるまでに設定するのには保証されません。 処理が完了するまで、バッファーが設定されていない場合、出力パラメーターと戻り値を利用できませんまで**SQLMoreResults** sql_no_data が返されます。 呼び出す**SQLCloseCursor**または**SQLFreeStmt**オプションが SQL_CLOSE のではこれらの値が破棄されるが発生します。  
  
 SQL_ATTR_PARAMSET_SIZE ステートメント属性の値が 1 より大きい場合*ParameterValuePtr*配列を指します。 1 つの SQL ステートメントでは、パラメーターまたは入力/出力パラメーターの入力値の完全な配列を処理し、出力パラメーターまたは入力/出力の出力値の配列を返します。  
  
## <a name="bufferlength-argument"></a>BufferLength 引数

 文字やバイナリの C データ、 *BufferLength*引数の長さを指定する、 \* *ParameterValuePtr*バッファー (1 つの要素の場合) または、内の要素の長さ\**ParameterValuePtr* (SQL_ATTR_PARAMSET_SIZE ステートメント属性の値が 1 より大きい場合) の配列。 この引数は、APD の SQL_DESC_OCTET_LENGTH レコードのフィールドを設定します。 アプリケーションでは、複数の値を指定します。 場合*BufferLength*内の値の場所を特定するために使用、**ParameterValuePtr*入力と出力の両方の配列。 入力/出力呼び出し力パラメーターの場合を文字データと出力のバイナリの C データを切り捨てるかどうかを判断に使用されます。  
  
-   返される使用可能なバイト数がより大きいまたは等しい場合は、C の文字データ*BufferLength*、内のデータ\* *ParameterValuePtr*に切り捨てられます*BufferLength* null 終了文字の長さ以下は、ドライバーが null で終わるとします。  
  
-   返される使用可能なバイト数がより大きい場合、バイナリの C データ*BufferLength*、内のデータ\* *ParameterValuePtr*に切り捨てられます*BufferLength*バイト。  
  
 C のデータの他のすべての種類、 *BufferLength*引数は無視されます。 長さ、 \* *ParameterValuePtr*バッファー (1 つの要素の場合) または内の要素の長さ、 \* *ParameterValuePtr*配列 (アプリケーションが呼び出す場合**SQLSetStmtAttr**で、*属性*引数のパラメーターごとに複数の値を指定する SQL_ATTR_PARAMSET_SIZE) C データ型の長さと見なされます。  
  
 ストリーミングされる出力のストリームの入力/出力パラメーター、 *BufferLength*でバッファーの長さが指定された引数は無視されます**SQLGetData**します。  
  
> [!NOTE]  
>  ODBC 1.0 アプリケーションを呼び出すと**SQLSetParam** 、ODBC 3 *。x*ドライバー、ドライバー マネージャーに変換しますこのへの呼び出しに**SQLBindParameter**を*BufferLength*引数が SQL_SETPARAM_VALUE_MAX では常にします。 ドライバー マネージャーは、ODBC 3 の場合はエラーを返します。*x*アプリケーション セット*BufferLength* SQL_SETPARAM_VALUE_MAX、ODBC 3 にします *。x*ドライバーは ODBC 1.0 アプリケーションによって呼び出されたときを決定するこれを使用できます。  
  
> [!NOTE]  
>  **SQLSetParam**、アプリケーションがの長さを指定する方法、**ParameterValuePtr*バッファーの文字またはバイナリ データ、およびアプリケーションを送信する方法、ドライバーを返せるようにします。配列の文字またはドライバーにバイナリ パラメーターの値ではドライバーによって定義されています。  
  
## <a name="strlenorindptr-argument"></a>StrLen_or_IndPtr 引数

 *StrLen_or_IndPtr*引数が指すバッファーされるときに、 **SQLExecute**または**SQLExecDirect**を呼び出すと、次のいずれかが含まれています。 (この引数は、アプリケーション パラメーターのポインターの SQL_DESC_OCTET_LENGTH_PTR と SQL_DESC_INDICATOR_PTR レコード フィールドを設定します)。  
  
-   格納されているパラメーター値の長さ **ParameterValuePtr*します。 これは、文字またはバイナリの C データ以外は無視されます。  
  
-   SQL_NTS します。 パラメーターの値は、null で終わる文字列です。  
  
-   SQL_NULL_DATA します。 パラメーターの値には NULL です。  
  
-   SQL_DEFAULT_PARAM します。 プロシージャでは、アプリケーションから取得した値ではなく、パラメーターの既定値を使用します。 この値は ODBC 標準構文で呼び出されるプロシージャでのみ有効ですし、場合にのみ、 *InputOutputType*引数は SQL_PARAM_INPUT、SQL_PARAM_INPUT_OUTPUT、または SQL_PARAM_INPUT_OUTPUT_STREAM します。 ときに\* *StrLen_or_IndPtr* SQL_DEFAULT_PARAM には、 *ValueType*、 *ParameterType*、 *ColumnSize*、 *DecimalDigits*、 *BufferLength*、および*ParameterValuePtr*引数は、入力パラメーターは無視され、入力、出力パラメーター値の定義にのみ使用/出力パラメーター。  
  
-   結果の SQL_LEN_DATA_AT_EXEC (*長さ*) マクロです。 パラメーターのデータに送信**SQLPutData**します。 場合、 *ParameterType*引数は SQL_LONGVARBINARY、SQL_LONGVARCHAR、または long のデータ ソースに固有のデータ型であり、ドライバーで SQL_NEED_LONG_DATA_LEN 情報の種類に"Y"を返します**SQLGetInfo**、*長さ*; パラメーターに送信されるデータのバイト数は、それ以外の場合、*長さ*負以外の値を指定する必要があり、無視されます。 詳細については、「を渡すパラメーターの値、」このセクションの後半を参照してください。  
  
     たとえば、データのバイト数を 10,000 で送信されることを指定する**SQLPutData** SQL_LONGVARCHAR パラメーターでは、1 つまたは複数の呼び出しでは、アプリケーション設定 **StrLen_or_IndPtr*を SQL_LEN_DATA_AT_EXEC (10000)。  
  
-   SQL_DATA_AT_EXEC です。 パラメーターのデータに送信**SQLPutData**します。 この値は、ODBC 3 の呼び出し時に ODBC 1.0 アプリケーションによって使用されます。*x*ドライバー。 詳細については、「を渡すパラメーターの値、」このセクションの後半を参照してください。  
  
 場合*StrLen_or_IndPtr* null ポインターの場合は、ドライバーには、すべての入力パラメーター値が NULL 以外であると、文字とバイナリ データは、null で終わることが前提としています。 場合*InputOutputType* SQL_PARAM_OUTPUT または SQL_PARAM_OUTPUT_STREAM と*ParameterValuePtr*と*StrLen_or_IndPtr*はどちらも null ポインター、ドライバーの破棄出力値。  
  
> [!NOTE]  
>  アプリケーション開発者は、null ポインターを指定することを強くお勧め*StrLen_or_IndPtr* SQL_C_BINARY パラメーターのデータ型の場合します。 ドライバーが SQL_C_BINARY のデータが予期せず切り捨てますしていないことを確認する*StrLen_or_IndPtr*有効な長さの値へのポインターを含める必要があります。  
  
 場合、 *InputOutputType*引数が SQL_PARAM_INPUT_OUTPUT、SQL_PARAM_OUTPUT、SQL_PARAM_INPUT_OUTPUT_STREAM、または SQL_PARAM_OUTPUT_STREAM、 *StrLen_or_IndPtr*バッファーを指す、ドライバーは SQL_NULL_DATA で返される使用可能なバイト数を返します\* *ParameterValuePtr* (文字データの null 終了バイトを除く)、または SQL_NO_TOTAL (場合に使用できるバイト数戻り値を特定できません)。 プロシージャは、1 つまたは複数の結果セットを返す場合、**StrLen_or_IndPtr*バッファーは、すべての結果がフェッチされるまでに設定するのには保証されません。  
  
 SQL_ATTR_PARAMSET_SIZE ステートメント属性の値が 1 より大きい場合*StrLen_or_IndPtr* SQLLEN 値の配列を指します。 これらは以前に紹介すると、このセクションでは、値のいずれかであり、1 つの SQL ステートメントで処理されます。  
  
## <a name="passing-parameter-values"></a>パラメーター値の受け渡し

 アプリケーションは、パラメーターの値を渡すことができますで、 \* *ParameterValuePtr*バッファーまたは 1 つまたは複数の呼び出しを**SQLPutData**します。 データが渡されたパラメーター **SQLPutData**と呼ばれます*実行時データ*パラメーター。 これらは通常、SQL_LONGVARBINARY データ型と SQL_LONGVARCHAR のパラメーターのデータ送信に使用であり、その他のパラメーターを組み込むことができます。  
  
 パラメーター値を渡すには、アプリケーションは、次の一連の手順を実行します。  
  
1.  呼び出し**SQLBindParameter**パラメーターの値のバッファーをバインドするには、各パラメーターの (*ParameterValuePtr*引数) および長さ/インジケーター (*StrLen_or_IndPtr*引数)。 実行時データ パラメーターで*ParameterValuePtr*パラメーターの数やデータへのポインターなど、アプリケーションで定義されたポインター値です。 値は、後で返され、パラメーターを識別するために使用できます。  
  
2.  入力および入力/出力パラメーターの値を格納、 \* *ParameterValuePtr*と **StrLen_or_IndPtr*バッファー。  
  
    -   アプリケーションの通常のパラメーターでパラメーター値の場所、 \* *ParameterValuePtr*バッファーとその値の長さ、**StrLen_or_IndPtr*バッファー。 詳細については、次を参照してください。[パラメーター値の設定](../../../odbc/reference/develop-app/setting-parameter-values.md)します。  
  
    -   実行時データ パラメーターの場合、アプリケーションが、SQL_LEN_DATA_AT_EXEC の結果を配置 (*長さ*) でのマクロ (ODBC 2.0、ドライバーを呼び出す) 場合、**StrLen_or_IndPtr*バッファー。  
  
3.  呼び出し**SQLExecute**または**SQLExecDirect** SQL ステートメントを実行します。  
  
    -   実行時データ パラメーターがない場合は、プロセスが完了しました。  
  
    -   実行時データ パラメーターがある場合、関数は SQL_NEED_DATA を返します。  
  
4.  呼び出し**SQLParamData**で指定されたアプリケーション定義の値を取得する、 *ParameterValuePtr*の引数**SQLBindParameter**最初の処理する実行時データ パラメーター。 **SQLParamData** SQL_NEED_DATA を返します。  
  
    > [!NOTE]  
    >  値がによって返される実行時データ パラメーターには、実行時データ列が似ています、 **SQLParamData**はそれぞれ異なります。 実行時データ パラメーターは、SQL ステートメントでデータを送信でパラメーター **SQLPutData**でステートメントを実行すると**SQLExecDirect**または**SQLExecute**. バインドされている**SQLBindParameter**します。 によって返される値**SQLParamData**にポインター値が渡される**SQLBindParameter**で、 *ParameterValuePtr*引数。 実行時データ列は列のデータを送信行セットで**SQLPutData**行が更新または追加**SQLBulkOperations**またはで更新された**SQLSetPos**. バインドされている**SQLBindCol**します。 によって返される値**SQLParamData**内の行のアドレスは、**TargetValuePtr*バッファー (への呼び出しで設定 **SQLBindCol** ) が処理されています。  
  
5.  呼び出し**SQLPutData**パラメーターのデータを送信する 1 つ以上の時間。 データ値がより大きい場合は、複数の呼び出しが必要な\* *ParameterValuePtr*で指定されたバッファー **SQLPutData**; を複数回呼び出す**SQLPutData**文字、バイナリ、またはデータのソースに固有のデータ型の列に文字データを送信するときにのみ、または列が文字、バイナリ、C のバイナリ データを送信するときに、同じパラメーターは許可されているか、データ ソースに固有のデータ型します。  
  
6.  呼び出し**SQLParamData**パラメーターのすべてのデータが送信されたことを通知するには、もう一度です。  
  
    -   複数の実行時データ パラメーターがある場合**SQLParamData**処理するには、SQL_NEED_DATA と [次へ] の実行時データ パラメーターのアプリケーション定義の値を返します。 アプリケーションでは、手順 4. と 5. を繰り返します。  
  
    -   これ以上の実行時データ パラメーターがある場合は、プロセスが完了しました。 場合は、ステートメントが正常に実行すると、 **SQLParamData** SQL_SUCCESS、SQL_SUCCESS_WITH_INFO; を返します、実行に失敗しました、SQL_ERROR が返されます。 この時点では、 **SQLParamData**ステートメントの実行に使用される関数によって返される任意の SQLSTATE を返すことができます (**SQLExecDirect**または**SQLExecute**)。  
  
         入力/出力または出力パラメーターの出力値が表示されます、 \* *ParameterValuePtr*と **StrLen_or_IndPtr*バッファーの後、アプリケーションは、すべての結果セットを取得します。ステートメントによって生成されます。  
  
 呼び出す**SQLExecute**または**SQLExecDirect** SQL_NEED_DATA 状態でステートメントを配置します。 この時点では、アプリケーションはのみ呼び出すことができます**SQLCancel**、 **SQLGetDiagField**、 **SQLGetDiagRec**、 **SQLGetFunctions**、 **SQLParamData**、または**SQLPutData**ステートメントを使用して、または*接続ハンドル*ステートメントに関連付けられています。 ステートメントまたはステートメントに関連付けられている接続と共に、他の関数を呼び出してその場合、関数は、SQLSTATE HY010 を返します (関数のシーケンス エラーです)。 状態、SQL_NEED_DATA ステートメント リーフ**SQLParamData**または**SQLPutData**はエラーを返します**SQLParamData** SQL_SUCCESS、SQL_SUCCESS_WITH_INFO を返しますまたはステートメントが取り消されました。  
  
 アプリケーションを呼び出す場合**SQLCancel**ドライバーがステートメントの実行をキャンセルして、ドライバーでは、実行時データ パラメーターのデータが引き続き必要があります、中には、アプリケーションが呼び出すことができますし、 **SQLExecute**または**SQLExecDirect**もう一度です。  
  
## <a name="retrieving-streamed-output-parameters"></a>ストリーミングされる出力パラメーターを取得します。

 アプリケーションの設定と*InputOutputType* SQL_PARAM_INPUT_OUTPUT_STREAM または SQL_PARAM_OUTPUT_STREAM、1 つまたは複数の呼び出しで出力パラメーターの値を取得する必要があります**SQLGetData**します。 ドライバーは、アプリケーションに戻るにストリーミングされる出力パラメーターの値を持つ、ときに、SQL_PARAM_DATA_AVAILABLE を次の関数の呼び出しに応答返します。**SQLMoreResults**、 **SQLExecute**、および**SQLExecDirect**します。 アプリケーションを呼び出す**SQLParamData**パラメーター値が使用可能なを判断します。  
  
 SQL_PARAM_DATA_AVAILABLE とストリーミングされる出力パラメーターの詳細については、次を参照してください。 [SQLGetData を使用して出力パラメーターを取得する](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)します。  
  
## <a name="using-arrays-of-parameters"></a>パラメーターの配列の使用

 アプリケーションでは、パラメーター マーカーとパラメーターの配列でパス ステートメントを準備、ときにこれを実行できる 2 つの方法があります。 1 つの方法は、ドライバー ケース パラメーターの配列をステートメント全体が 1 つのアトミック単位として扱われますが、バック エンドの配列処理機能に依存するためです。 Oracle では、配列の処理機能をサポートするデータ ソースの例を示します。 この機能を実装するために別の方法は、ドライバー SQL ステートメントでは、パラメーター、パラメーター配列内の各セットの 1 つの SQL ステートメントのバッチを生成して、バッチを実行するためです。 パラメーターの配列では使用できません、 **UPDATE WHERE CURRENT OF**ステートメント。  
  
 パラメーターの配列が処理されるときに、個々 の結果セットや行の数 (パラメーターのセットごとに 1 つ) が使用可能または結果セット/行カウントを 1 つにロール アップできます。 オプション、SQL_PARAM_ARRAY_ROW_COUNTS **SQLGetInfo**行カウントが (SQL_PARC_BATCH) のパラメーターのセットごとに利用可能なか、1 つだけの行の数が使用可能な (SQL_PARC_NO_BATCH) かどうかを示します。  
  
 オプション、SQL_PARAM_ARRAY_SELECTS **SQLGetInfo**パラメーター (SQL_PAS_BATCH) のセットごとに結果セットがあるか、1 つの結果セットが使用可能な (SQL_PAS_NO_BATCH) かどうかを示します。 ドライバーがパラメーターの配列を実行するときに、結果セットを生成するステートメントを許可していない場合、SQL_PARAM_ARRAY_SELECTS は SQL_PAS_NO_SELECT を返します。  
  
 詳細については、次を参照してください。 [SQLGetInfo 関数](../../../odbc/reference/syntax/sqlgetinfo-function.md)します。  
  
 パラメーターの配列をサポートするためには、SQL_ATTR_PARAMSET_SIZE ステートメント属性は、各パラメーターの値の数を指定に設定されます。 フィールドが 1 より大きい場合は、APD の SQL_DESC_DATA_PTR、SQL_DESC_INDICATOR_PTR、および SQL_DESC_OCTET_LENGTH_PTR フィールドは配列を指す必要があります。 各配列のカーディナリティは、SQL_ATTR_PARAMSET_SIZE の値と同じです。  
  
 APD の SQL_DESC_ROWS_PROCESSED_PTR フィールドは、処理されて、エラーのセットを含むパラメーターのセットの数を格納しているバッファーを指します。 各パラメーターのセットが処理されると、ドライバーは、バッファーに新しい値を格納します。 これが null ポインターの場合は、数は返されません。 パラメーターの配列を使用している場合は、設定関数によって SQL_ERROR が返される場合でも、APD の SQL_DESC_ROWS_PROCESSED_PTR フィールドによって示される値が設定されます。 SQL_NEED_DATA が返された場合、APD の SQL_DESC_ROWS_PROCESSED_PTR フィールドによって示される値は、処理されているパラメーターのセットに設定されます。  
  
 パラメーターの配列がバインドされている場合、どうなるか**UPDATE WHERE CURRENT OF**ステートメントが実行されるドライバーで定義されます。  
  
## <a name="column-wise-parameter-binding"></a>列方向のパラメーターのバインド

 列方向のバインドでは、アプリケーションは、各パラメーターに個別のパラメーターと長さ/インジケーター配列をバインドします。  
  
 列方向のバインドを使用するには、アプリケーションは最初に sql_param_bind_by_column をそれぞれ、SQL_ATTR_PARAM_BIND_TYPE ステートメント属性を設定します。 (これは、既定値です)。各列にバインドするには、アプリケーションは、次の手順を実行します。  
  
1.  パラメーターのバッファー配列を割り当てます。  
  
2.  長さ/インジケーター バッファーの配列を割り当てます。  
  
    > [!NOTE]  
    >  場合は、アプリケーションは、列方向のバインドを使用する場合に、記述子に直接書き込む、個別の配列の長さとインジケーター データを使用できます。  
  
3.  呼び出し**SQLBindParameter**次の引数で。  
  
    -   *ValueType*パラメーターのバッファー配列内の単一要素の C 型です。  
  
    -   *ParameterType*パラメーターの SQL 型です。  
  
    -   *ParameterValuePtr*パラメーターのバッファー配列のアドレスです。  
  
    -   *BufferLength*パラメーターのバッファー配列内の単一要素のサイズです。 *BufferLength*データが固定長のデータの場合、引数は無視されます。  
  
    -   *StrLen_or_IndPtr*長さ/インジケーター配列のアドレスです。  
  
 この情報を使用する方法の詳細については、「コメント」このセクションの後半の「ParameterValuePtr 引数」を参照してください。 パラメーターの列方向のバインドの詳細については、次を参照してください。[バインド パラメーター配列](../../../odbc/reference/develop-app/binding-arrays-of-parameters.md)します。  
  
## <a name="row-wise-parameter-binding"></a>行方向のパラメーターのバインド

 行方向のバインドでは、アプリケーションは、バインドするには、各パラメーターのパラメーターと長さ/インジケーター バッファーに格納する構造体を定義します。  
  
 行方向のバインドを使用するには、アプリケーションは、次の手順を実行します。  
  
1.  パラメーター (両方のパラメーターと長さ/インジケーター バッファーを含む) の 1 つのセットを保持する構造体を定義し、これらの構造体の配列を割り当てます。  
  
    > [!NOTE]  
    >  場合は、アプリケーションは、行方向のバインドを使用する場合に、記述子に直接書き込む、個別のフィールドの長さとインジケーター データを使用できます。  
  
2.  パラメーターの 1 つのセットを格納する構造体のサイズまたはパラメーターのバインド先のバッファーのインスタンスのサイズには、SQL_ATTR_PARAM_BIND_TYPE ステートメント属性を設定します。 長さは、すべてのバインドされたパラメーターおよび構造体またはバインドされたパラメーターのアドレスが指定した長さでインクリメントされた場合は、結果は内の同じパラメーターの先頭にポイントを確認する、バッファーの埋め込み用の領域を含める必要があります、次の行。 使用すると、 *sizeof* ANSI c 演算子は、この動作が保証されます。  
  
3.  呼び出し**SQLBindParameter**にバインドするには、各パラメーターには、次の引数で。  
  
    -   *ValueType*列にバインドするパラメーターのバッファーのメンバーの種類です。  
  
    -   *ParameterType*パラメーターの SQL 型です。  
  
    -   *ParameterValuePtr*は配列の最初の要素のパラメーター バッファーのメンバーのアドレスです。  
  
    -   *BufferLength*パラメーター バッファーのメンバーのサイズです。  
  
    -   *StrLen_or_IndPtr*はバインドされる長さ/インジケーターのメンバーのアドレスです。  
  
 この情報を使用する方法の詳細については、次を参照してください。"*ParameterValuePtr*引数、"このセクションで後述します。 パラメーターの行方向のバインドの詳細については、次を参照してください。、[バインド パラメーター配列](../../../odbc/reference/develop-app/binding-arrays-of-parameters.md)します。  
  
## <a name="error-information"></a>エラー情報

 ドライバーは、バッチ (SQL_PARAM_ARRAY_ROW_COUNTS オプションは SQL_PARC_NO_BATCH に等しい) としてパラメーター配列を実装していません、エラー状況は、1 つのステートメントが実行されたかのように処理されます。 IPD の SQL_DESC_ARRAY_STATUS_PTR ヘッダー フィールドを使用してアプリケーションが、SQL ステートメントまたはパラメーターの配列にパラメーターが原因のパラメーターを決定する場合は、ドライバーでは、バッチとしてパラメーター配列を実装、 **SQLExecDirect**または**SQLExecute**にエラーが返されます。 このフィールドには、パラメーター値の行ごとの状態情報が含まれています。 フィールドは、エラーが発生したことを示している場合、診断データの構造体のフィールドは失敗したパラメーターの行とパラメーターの数を示します。 配列内の要素の数は、SQL_ATTR_PARAMSET_SIZE ステートメント属性によって設定できる、APD の SQL_DESC_ARRAY_SIZE ヘッダー フィールドによって定義されます。  
  
> [!NOTE]  
>  APD の SQL_DESC_ARRAY_STATUS_PTR ヘッダー フィールドを使用して、パラメーターを無視します。 パラメーターを無視する詳細については、「パラメーターのセットを無視しています」。 次のセクションを参照してください。  
  
 ときに**SQLExecute**または**SQLExecDirect** SQL_PARAM_ERROR、SQL_PARAM_SUCCESS、sql _ を SQL_ERROR を返します、IPD で SQL_DESC_ARRAY_STATUS_PTR フィールドによって示される配列内の要素が含まれますPARAM_SUCCESS_WITH_INFO、SQL_PARAM_UNUSED、または SQL_PARAM_DIAG_UNAVAILABLE します。  
  
 この配列内の各要素に対しては、診断データの構造体には、1 つまたは複数の状態レコードが含まれています。 構造体の SQL_DIAG_ROW_NUMBER フィールドでは、エラーの原因となったパラメーターの値の行番号を示します。 エラーの原因となったパラメーターの行は、特定のパラメーターを特定することである場合、パラメーター数は SQL_DIAG_COLUMN_NUMBER フィールドに入力されます。  
  
 以前のパラメーターで強制的にエラーが発生したため、パラメーターが使用されていないときに、SQL_PARAM_UNUSED が入力された**SQLExecute**または**SQLExecDirect**を中止します。 たとえば、50 のパラメーターがある場合、エラーが発生しました fortieth の原因となったパラメーターのセットを実行中に**SQLExecute**または**SQLExecDirect**中止、SQL_PARAM_UNUSED を入力し、パラメーターを 50 41 の状態の配列。  
  
 SQL_PARAM_DIAG_UNAVAILABLE は、ドライバーは、この個別のパラメーターのレベルのエラー情報によって生成されないように、モノリシックの単位としてパラメーターの配列を扱うときに入力します。  
  
 パラメーターの 1 つのセットの処理のエラーの一部では、停止する配列で、後続のパラメーターのセットの処理が発生します。 その他のエラーは、後続のパラメーターの処理には影響しません。 ドライバーの定義は、どのエラーの処理が停止します。 処理が停止されていない、配列内のすべてのパラメーターの処理、SQL_SUCCESS_WITH_INFO が、エラーの結果として返されるおよび SQL_ATTR_PARAMS_PROCESSED_PTR によって定義されたバッファーが処理されたパラメーターのセットの合計数に設定されている場合 (で定義されている、SQL_ATTR_PARAMSET_SIZE ステートメント属性)、エラーのセットが含まれています。  
  
> [!CAUTION]  
>  パラメーターの配列の処理中にエラーが発生したときに、ODBC の動作では、ODBC 3 で異なります。*x* ODBC 2 の場合よりも *。x*します。 ODBC 2。*x*SQL_ERROR と処理はなく、関数が返されます。 によって示されるバッファー、 *pirow*の引数**SQLParamOptions**エラー行の数に含まれています。 ODBC 3。*x*SQL_SUCCESS_WITH_INFO が返されます、関数、および停止または続行か月を処理します。 問題が解決しない場合は、SQL_ATTR_PARAMS_PROCESSED_PTR で指定したバッファーがでエラーが発生するものも含めすべてのパラメーターの処理の値に設定されます。 この動作の変更の既存のアプリケーションの問題が発生する可能性があります。  
  
 ときに**SQLExecute**または**SQLExecDirect** SQL_ERROR または SQL_NEED_DATA が返されると、状態配列を含むように、パラメーター配列内のすべてのパラメーター セットの処理を完了する前に返します。既に処理されているこれらのパラメーターの状態。 IPD の SQL_DESC_ROWS_PROCESSED_PTR フィールドによって示される場所には、SQL_ERROR または SQL_NEED_DATA エラー コードの原因となったパラメーター配列内の行番号が含まれています。 ドライバーで定義されます。 配列値の状態の可用性は、SELECT ステートメントにパラメーターの配列が送信されると、します。ステートメントが実行されたか、セットのフェッチの結果として、使用可能な必要があります。  
  
## <a name="ignoring-a-set-of-parameters"></a>一連のパラメーターは無視されます。

 (また、SQL_ATTR_PARAM_STATUS_PTR ステートメント属性で設定) として APD の SQL_DESC_ARRAY_STATUS_PTR フィールドを SQL ステートメントにバインドされたパラメーターのセットを無視することを示すために使用できます。 実行時にパラメーターの 1 つまたは複数のセットを無視するドライバーを送信するには、アプリケーションは以下の手順を実行する必要があります。  
  
1.  呼び出す**SQLSetDescField**状態情報が含まれる SQLUSMALLINT 値の配列を指す APD の SQL_DESC_ARRAY_STATUS_PTR ヘッダー フィールドを設定します。 このフィールドを呼び出すことによって設定することもできます。 **SQLSetStmtAttr**で、*属性*、SQL_ATTR_PARAM_OPERATION_PTR アプリケーション記述子ハンドルを取得することなく、フィールドを設定できるのです。  
  
2.  2 つの値のいずれかに APD の SQL_DESC_ARRAY_STATUS_PTR フィールドによって定義された配列の各要素を設定します。  
  
    -   SQL_PARAM_IGNORE を行がステートメントの実行から除外されたことを示します。  
  
    -   SQL_PARAM_PROCEED、ステートメントの実行で、行を含めることを示す。  
  
3.  呼び出す**SQLExecDirect**または**SQLExecute**準備されたステートメントを実行します。  
  
 APD の SQL_DESC_ARRAY_STATUS_PTR フィールドによって定義された配列に、次の規則が適用されます。  
  
-   ポインターの設定を既定で null にします。  
  
-   ポインターが null の場合は、すべてのパラメーターのセットは使用、SQL_ROW_PROCEED にすべての要素が設定された場合と。  
  
-   SQL_PARAM_PROCEED に要素を設定しても、操作がその特定のパラメーターのセットを使用するとは限りません。  
  
-   SQL_PARAM_PROCEED はヘッダー ファイルで 0 として定義されます。  
  
 アプリケーションは、IRD の SQL_DESC_ARRAY_STATUS_PTR フィールドのフィールドと同じ配列を指す APD の指す SQL_DESC_ARRAY_STATUS_PTR を設定できます。 これは、機能は、パラメーターを行のデータにバインドする場合に便利です。 パラメーターは、行データの状態に応じて、無視されます。 SQL_PARAM_IGNORE、だけでなく、次のコードは無視される SQL ステートメントのパラメーターが発生します。SQL_ROW_DELETED、SQL_ROW_UPDATED、および SQL_ROW_ERROR です。 SQL_PARAM_PROCEED、だけでなくは、次のコードは、続行する SQL ステートメントを発生します。SQL_ROW_SUCCESS、SQL_ROW_SUCCESS_WITH_INFO、および SQL_ROW_ADDED です。  
  
## <a name="rebinding-parameters"></a>パラメーターを再バインド

 アプリケーションは、バインディングを変更する 2 つの操作のいずれかを実行できます。  
  
-   呼び出す**SQLBindParameter**は既にバインドされている列の新しいバインディングを指定します。 ドライバーは、新しいで古いバインドを上書きします。  
  
-   バインディングの呼び出しで指定したバッファーのアドレスに追加するオフセットを指定する**SQLBindParameter**します。 詳細については、次のセクションを参照してください「のオフセットを再バインドします」。  
  
## <a name="rebinding-with-offsets"></a>オフセットを持つ再バインド

 アプリケーションのバッファー領域のセットアップへの呼び出しが、多くのパラメーターを含むことのできるパラメーターの再バインドは特に便利です**SQLExecDirect**または**SQLExecute**パラメーターの一部のみを使用します。 バッファー領域の残りの領域は、オフセットで、既存のバインドを変更することで、次のパラメーターのセットを使用できます。  
  
 APD の SQL_DESC_BIND_OFFSET_PTR ヘッダー フィールドは、バインディングのオフセットを指します。 フィールドが null 以外の場合、ドライバー、ポインターを逆参照しの SQL_DESC_DATA_PTR、SQL_DESC_INDICATOR_PTR、および SQL_DESC_OCTET_LENGTH_PTR フィールドの値が null ポインターの場合は、記述子でそれらのフィールドに逆参照された値を追加します。実行時に記録します。 新しいポインター値は、SQL ステートメントが実行されたときに使用されます。 オフセットは、再バインド後に有効です。 SQL_DESC_BIND_OFFSET_PTR 自体、オフセットではなくオフセットへのポインターであるため、変えることができます、オフセットを直接に電話しなくても[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)または[SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)に記述子フィールドを変更します。 ポインターの設定を既定で null にします。 呼び出して、ARD の SQL_DESC_BIND_OFFSET_PTR フィールドを設定することができます[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)またはへの呼び出しによって[SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)で、*された*SQL_ATTR_PARAM_BIND_ のOFFSET_PTR します。  
  
 バインディングのオフセットは常の SQL_DESC_DATA_PTR、SQL_DESC_INDICATOR_PTR、および SQL_DESC_OCTET_LENGTH_PTR フィールドの値に直接追加します。 別の値にオフセットを変更する場合、新しい値は各記述子フィールドの値に直接追加されます。 新しいオフセットは、フィールドの値と、以前のオフセットの合計には追加されません。  
  
## <a name="descriptors"></a>記述子

 パラメーターをバインドする方法については、Apd の Ipd フィールドによって決まります。 引数**SQLBindParameter**これらの記述子フィールドの設定に使用します。 、フィールドを設定することも、 **SQLSetDescField**関数が**SQLBindParameter**は、アプリケーションが呼び出す記述子ハンドルを取得する必要はありませんので、使用する方が効率的**SQLBindParameter**します。  
  
> [!CAUTION]  
>  呼び出す**SQLBindParameter**の 1 つのステートメントの他のステートメントに影響することができます。 これには、ステートメントに関連付けられている ARD が明示的に割り当てられているし、他のステートメントに関連付けられてもときに発生します。 **SQLBindParameter**フィールドを変更します。 この記述子が関連付けられているすべてのステートメントに、APD の変更が適用されます。 呼び出す前に必要な動作でない場合、アプリケーションが、他のステートメントからこの記述子の関連付けを解除する必要があります**SQLBindParameter**します。  
  
 概念的には、 **SQLBindParameter**シーケンスでは、次の手順を実行します。  
  
1.  呼び出し[SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md) APD のハンドルを取得します。  
  
2.  呼び出し[SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md) APD の SQL_DESC_COUNT のフィールドを取得する場合の値、 *ColumnNumber* SQL_DESC_COUNT、呼び出しの引数を超える**SQLSetDescField**に SQL_DESC_COUNT の値を大きく*ColumnNumber*します。  
  
3.  呼び出し[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md) APD の次のフィールドに値を割り当てるを複数回します。  
  
    -   SQL_DESC_TYPE、SQL_DESC_CONCISE_TYPE の値に設定*ValueType*ただし、場合*ValueType*は 1 つ SQL_DESC_TYPE を sql _、datetime または間隔のサブタイプの簡潔な識別子の設定、DATETIME または SQL_INTERVAL の場合はそれぞれ、簡潔な識別子に SQL_DESC_CONCISE_TYPE を設定しを対応する日付時刻または間隔サブコード SQL_DESC_DATETIME_INTERVAL_CODE を設定します。  
  
    -   SQL_DESC_OCTET_LENGTH フィールドの値に設定*BufferLength*します。  
  
    -   SQL_DESC_DATA_PTR フィールドの値に設定*ParameterValue*します。  
  
    -   SQL_DESC_OCTET_LENGTH_PTR フィールドの値に設定*StrLen_or_Ind*します。  
  
    -   値にも、SQL_DESC_INDICATOR_PTR フィールドを設定*StrLen_or_Ind*します。  
  
     *StrLen_or_Ind*パラメーターは、インジケーターの情報と、パラメーター値の長さの両方を指定します。  
  
4.  呼び出し[SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md) IPD ハンドルを取得します。  
  
5.  呼び出し[SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md) IPD の SQL_DESC_COUNT のフィールドを取得する場合の値、 *ColumnNumber* SQL_DESC_COUNT、呼び出しの引数を超える**SQLSetDescField**に SQL_DESC_COUNT の値を大きく*ColumnNumber*します。  
  
6.  呼び出し[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md) IPD の次のフィールドに値を割り当てるを複数回します。  
  
    -   SQL_DESC_TYPE、SQL_DESC_CONCISE_TYPE の値に設定*ParameterType*ことを除いて、場合*ParameterType*は 1 つですが、datetime または間隔のサブタイプの簡潔な識別子の SQL_DESC_TYPE を設定SQL_DATETIME または SQL_INTERVAL の場合は、するには、簡潔な識別子と、対応する datetime 間隔サブコードに SQL_DESC_DATETIME_INTERVAL_CODE を設定する SQL_DESC_CONCISE_TYPE をそれぞれ設定します。  
  
    -   SQL_DESC_LENGTH、SQL_DESC_PRECISION、および、SQL_DESC_DATETIME_INTERVAL_PRECISION の 1 つ以上を設定に適した*ParameterType*します。  
  
    -   SQL_DESC_SCALE の値に設定*DecimalDigits*します。  
  
 場合に呼び出し**SQLBindParameter**失敗、APD の設定は、記述子フィールドの内容は未定義、し、APD の SQL_DESC_COUNT フィールドは変更されません。 さらに、IPD で適切なレコードの SQL_DESC_LENGTH、SQL_DESC_PRECISION、SQL_DESC_SCALE、および SQL_DESC_TYPE フィールドが定義されていると IPD の SQL_DESC_COUNT フィールドは変更されません。  
  
## <a name="conversion-of-calls-to-and-from-sqlsetparam"></a>呼び出しと SQLSetParam の間の変換

 ODBC 1.0 アプリケーションを呼び出すと**SQLSetParam** 、ODBC 3 *。x*ドライバー、ODBC 3 *。x*ドライバー マネージャーは、次の表に示すように呼び出しをマップします。  
  
|ODBC 1.0 アプリケーションを呼び出す|ODBC 3 の呼び出しです。*x*ドライバー|  
|----------------------------------|-------------------------------|  
|SQLSetParam(      StatementHandle,      ParameterNumber,      ValueType,      ParameterType,      LengthPrecision,      ParameterScale,      ParameterValuePtr,      StrLen_or_IndPtr);|SQLBindParameter (StatementHandle、ParameterNumber、SQL_PARAM_INPUT_OUTPUT、ValueType、ParameterType、 *ColumnSize*、 *DecimalDigits*ParameterValuePtr、SQL_SETPARAM_VALUE_MAX、     StrLen_or_IndPtr)。|  
  
## <a name="code-example"></a>コード例  
 次の例では、アプリケーションは、ORDERS テーブルにデータを挿入する SQL ステートメントを準備します。 アプリケーションの呼び出し、ステートメント内の各パラメーター **SQLBindParameter** ODBC C データ型とパラメーターの SQL データ型を指定して、各パラメーターにバッファーをバインドします。 データの行ごとに、アプリケーションは各パラメーターと呼び出しにデータ値を割り当てます**SQLExecute**ステートメントを実行します。  
  
 次の例では、Northwind データベースに関連付けられている Northwind という名前のコンピューターでの ODBC データ ソースがあることを前提としています。  
  
 コード例については、次を参照してください[SQLBulkOperations 関数](../../../odbc/reference/syntax/sqlbulkoperations-function.md)、 [SQLProcedures 関数](../../../odbc/reference/syntax/sqlprocedures-function.md)、 [SQLPutData 関数](../../../odbc/reference/syntax/sqlputdata-function.md)、および[SQLSetPos 関数](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
```cpp
// SQLBindParameter_Function.cpp  
// compile with: ODBC32.lib  
#include <windows.h>  
#include <sqltypes.h>  
#include <sqlext.h>  
  
#define EMPLOYEE_ID_LEN 10  
  
SQLHENV henv = NULL;  
SQLHDBC hdbc = NULL;  
SQLRETURN retcode;  
SQLHSTMT hstmt = NULL;  
SQLSMALLINT sCustID;  
  
SQLCHAR szEmployeeID[EMPLOYEE_ID_LEN];  
SQL_DATE_STRUCT dsOrderDate;  
SQLINTEGER cbCustID = 0, cbOrderDate = 0, cbEmployeeID = SQL_NTS;  
  
int main() {  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
   retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER*)SQL_OV_ODBC3, 0);   
  
   retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);   
   retcode = SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
  
   retcode = SQLConnect(hdbc, (SQLCHAR*) "Northwind", SQL_NTS, (SQLCHAR*) NULL, 0, NULL, 0);  
   retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
  
   retcode = SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, EMPLOYEE_ID_LEN, 0, szEmployeeID, 0, &cbEmployeeID);  
   retcode = SQLBindParameter(hstmt, 2, SQL_PARAM_INPUT, SQL_C_SSHORT, SQL_INTEGER, 0, 0, &sCustID, 0, &cbCustID);  
   retcode = SQLBindParameter(hstmt, 3, SQL_PARAM_INPUT, SQL_C_TYPE_DATE, SQL_TIMESTAMP, sizeof(dsOrderDate), 0, &dsOrderDate, 0, &cbOrderDate);  
  
   retcode = SQLPrepare(hstmt, (SQLCHAR*)"INSERT INTO Orders(CustomerID, EmployeeID, OrderDate) VALUES (?, ?, ?)", SQL_NTS);  
  
   strcpy_s((char*)szEmployeeID, _countof(szEmployeeID), "BERGS");  
   sCustID = 5;  
   dsOrderDate.year = 2006;  
   dsOrderDate.month = 3;  
   dsOrderDate.day = 17;  
  
   retcode = SQLExecute(hstmt);  
}  
```  
  
## <a name="code-example"></a>コード例

 次の例では、アプリケーションは、名前付きパラメーターを使用して、SQL Server のストアド プロシージャを実行します。  
  
```cpp
// SQLBindParameter_Function_2.cpp  
// compile with: ODBC32.lib  
// sample assumes the following stored procedure:  
// use northwind  
// DROP PROCEDURE SQLBindParameter  
// GO  
//   
// CREATE PROCEDURE SQLBindParameter @quote int  
// AS  
// delete from orders where OrderID >= @quote  
// GO  
#include <windows.h>  
#include <sqltypes.h>  
#include <sqlext.h>  
  
SQLHDESC hIpd = NULL;  
SQLHENV henv = NULL;  
SQLHDBC hdbc = NULL;  
SQLRETURN retcode;  
SQLHSTMT hstmt = NULL;  
SQLCHAR szQuote[50] = "100084";  
SQLINTEGER cbValue = SQL_NTS;  
  
int main() {  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
   retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER*)SQL_OV_ODBC3, 0);   
  
   retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);   
   retcode = SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
  
   retcode = SQLConnect(hdbc, (SQLCHAR*) "Northwind", SQL_NTS, (SQLCHAR*) NULL, 0, NULL, 0);  
   retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
  
   retcode = SQLPrepare(hstmt, (SQLCHAR*)"{call SQLBindParameter(?)}", SQL_NTS);  
   retcode = SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, 50, 0, szQuote, 0, &cbValue);  
   retcode = SQLGetStmtAttr(hstmt, SQL_ATTR_IMP_PARAM_DESC, &hIpd, 0, 0);  
   retcode = SQLSetDescField(hIpd, 1, SQL_DESC_NAME, "@quote", SQL_NTS);  
  
   retcode = SQLExecute(hstmt);  
}  
```  
  
## <a name="related-functions"></a>関連する関数  
  
|詳細|解決方法|  
|---------------------------|---------|  
|ステートメント内のパラメーターに関する情報を返す|[SQLDescribeParam 関数](../../../odbc/reference/syntax/sqldescribeparam-function.md)|  
|SQL ステートメントを実行します。|[SQLExecDirect 関数](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|準備された SQL ステートメントを実行します。|[SQLExecute 関数](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|ステートメントでパラメーターのバッファーを解放します。|[SQLFreeStmt 関数](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|ステートメント パラメーターの数を返す|[SQLNumParams 関数](../../../odbc/reference/syntax/sqlnumparams-function.md)|  
|データを送信する次のパラメーターを返す|[SQLParamData 関数](../../../odbc/reference/syntax/sqlparamdata-function.md)|  
|複数のパラメーター値を指定します。|[SQLParamOptions 関数](../../../odbc/reference/syntax/sqlparamoptions-function.md)|  
|実行時にパラメーターのデータを送信します。|[SQLPutData 関数](../../../odbc/reference/syntax/sqlputdata-function.md)|  
  
## <a name="see-also"></a>参照

 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)   
 [SQLGetData を使用した出力パラメーターの取得](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
