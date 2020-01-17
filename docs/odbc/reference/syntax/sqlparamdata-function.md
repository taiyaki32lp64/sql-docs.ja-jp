---
title: SQLParamData 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLParamData
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLParamData
helpviewer_keywords:
- SQLParamData function [ODBC]
ms.assetid: 68fe010d-9539-4e5b-a260-c8d32423b1db
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 41cb718b5425315856fe4db27658cce873f90e6b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68018944"
---
# <a name="sqlparamdata-function"></a>SQLParamData 関数
**準拠**  
 バージョンが導入されました。ODBC 1.0 規格に準拠します。ISO 92  
  
 **まとめ**  
 **SQLParamData**と共に使用**SQLPutData**パラメーターのデータと、ステートメントの実行時に提供する**SQLGetData**ストリーミングされる出力パラメーターのデータを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLParamData(  
     SQLHSTMT       StatementHandle,  
     SQLPOINTER *   ValuePtrPtr);  
```  
  
## <a name="arguments"></a>引数  
 *StatementHandle*  
 [入力]ステートメント ハンドルです。  
  
 *ValuePtrPtr*  
 [出力]アドレスを返すバッファーへのポインター、 *ParameterValuePtr*で指定されたバッファー **SQLBindParameter** (のパラメーターのデータ) のアドレス、または、 *TargetValuePtr*で指定されたバッファー **SQLBindCol** (データ)、列の SQL_DESC_DATA_PTR 記述子レコードのフィールドに含まれているとします。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_NEED_DATA、SQL_NO_DATA、SQL_STILL_EXECUTING、SQL_ERROR、SQL_INVALID_HANDLE、または SQL_PARAM_DATA_AVAILABLE  
  
## <a name="diagnostics"></a>診断  
 ときに**SQLParamData** SQL_ERROR または SQL_SUCCESS_WITH_INFO、関連付けられている SQLSTATE 値を返しますを呼び出すことによって取得できる**SQLGetDiagRec**で、 *HandleType* sql _ のHANDLE_STMT と*処理*の*StatementHandle*します。 次の表に、によって返される通常の SQLSTATE 値**SQLParamData** ; この関数のコンテキストでそれぞれについて説明しますと表記"(DM)"の前にドライバー マネージャーによって返されるについての説明。 SQLSTATE 値ごとに関連付けられているリターン コードは明記しない限り、SQL_ERROR です。  
  
|SQLSTATE|[エラー]|説明|  
|--------------|-----------|-----------------|  
|01000|一般的な警告|ドライバー固有の情報メッセージです。 (関数は、SQL_SUCCESS_WITH_INFO を返します)。|  
|07006|制限付きのデータ型の属性違反|識別されるデータ値、 *ValueType*引数**SQLBindParameter**のバインドされたパラメーターがで識別されるデータ型に変換できませんでした、 *ParameterType*引数**SQLBindParameter**します。<br /><br /> SQL_PARAM_INPUT_OUTPUT または SQL_PARAM_OUTPUT で識別されるデータ型に変換しないとしてバインドされたパラメーターのデータ値が返される、 *ValueType*引数**SQLBindParameter**します。<br /><br /> (1 つまたは複数の行のデータ値を変換できませんでした、1 つまたは複数の行が正常に返された場合は、この関数を返します SQL_SUCCESS_WITH_INFO。)|  
|08S01|通信リンク エラー|関数が完了した処理の前に、ドライバーとドライバーが接続されているデータ ソース間の通信リンクに失敗しました。|  
|22026|文字列データの長さが合致しません|SQL_NEED_LONG_DATA_LEN 情報の種類で**SQLGetInfo**が"Y"と指定された以外 (データ型は SQL_LONGVARCHAR、SQL_LONGVARBINARY、または長い形式のデータ ソースに固有のデータ型)、long 型パラメーターの低いデータが送信されました。*StrLen_or_IndPtr*引数**SQLBindParameter**します。<br /><br /> SQL_NEED_LONG_DATA_LEN 情報の種類で**SQLGetInfo** "Y"で指定された数より長い列 (データ型は SQL_LONGVARCHAR、SQL_LONGVARBINARY、または長い形式のデータ ソースに固有のデータ型) の低いデータが送信された、追加または更新されたデータの行の列に対応する長バッファー **SQLBulkOperations**またはで更新された**SQLSetPos**します。|  
|40001|シリアル化エラー|トランザクションが別のトランザクションでリソース デッドロックによりロールバックされました。|  
|40003|不明なステートメント入力候補|、この関数の実行中に、関連付けられた接続が失敗し、トランザクションの状態を特定できません。|  
|HY000|一般的なエラー|これがなかった固有の SQLSTATE とする実装に固有の SQLSTATE が定義されていない、エラーが発生しました。 によって返されるエラー メッセージ**SQLGetDiagRec**で、  *\*MessageText*バッファーは、エラーとその原因について説明します。|  
|HY001|メモリの割り当てエラー|ドライバーは、実行または関数の完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY008|操作が取り消されました|非同期処理が有効に、 *StatementHandle*します。 関数が呼び出された、および前に、実行を完了**SQLCancel**または**SQLCancelHandle**が呼び出されて、 *StatementHandle*; で、関数が再度呼び出されましたし*StatementHandle*します。<br /><br /> 関数が呼び出された、および実行を完了する前に**SQLCancel**または**SQLCancelHandle**が呼び出されて、 *StatementHandle*から別のスレッドで、マルチ スレッド アプリケーションです。|  
|HY010|関数のシーケンス エラー|(DM) 前の関数呼び出しはへの呼び出しではない**SQLExecDirect**、 **SQLExecute**、 **SQLBulkOperations**、または**SQLSetPos**場所、コードは SQL_NEED_DATA、または前の関数呼び出しがへの呼び出しを返す**SQLPutData**します。<br /><br /> 前の関数呼び出しがへの呼び出し**SQLParamData**します。<br /><br /> (DM) を非同期的に実行中の関数が呼び出された接続ハンドルに関連付けられているため、 *StatementHandle*します。 この非同期関数ではときに実行されている、 **SQLParamData**関数が呼び出されました。<br /><br /> (DM) を非同期的に実行中の関数 (いないこの"1") が呼び出された、 *StatementHandle*この関数が呼び出されたときに実行されているとします。<br /><br /> **SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**、または**SQLSetPos**に対して呼び出された、 *StatementHandle*と返された SQL_NEED_DATA します。 **SQLCancel**すべての実行時データ パラメーターまたは列のデータが送信される前に呼び出されました。|  
|HY013|メモリ管理エラー|基になるメモリ オブジェクトにアクセスできませんでした、場合によってメモリ不足が原因であるために、関数呼び出しを処理できませんでした。|  
|HY117|不明なトランザクションの状態のため、接続が中断されます。 のみを切断して、読み取り専用の関数が許可されます。|(DM) 中断状態の詳細については、次を参照してください。 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)します。|  
|HYT01|接続がタイムアウトしました|データ ソースが要求に応答する前に、接続のタイムアウト期間が終了しました。 によって、接続タイムアウト期間が設定されます**SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT します。|  
|IM001|ドライバーでは、この関数はサポートされていません|(DM) に対応するドライバー、 *StatementHandle*関数をサポートしていません。|  
|IM017|非同期通知モードでのポーリングは無効です。|通知のモデルを使用すると、常にポーリングは無効です。|  
|IM018|**SQLCompleteAsync**このハンドルに対する前の非同期操作を完了が呼び出されていません。|通知モードが有効になっている場合、ハンドルでは、前の関数呼び出しに SQL_STILL_EXECUTING が返された場合と**SQLCompleteAsync**後処理を行い、操作を完了するハンドルで呼び出す必要があります。|  
  
 場合**SQLParamData**と呼ばれますが、SQL ステートメントでパラメーターのデータを送信中に、ステートメントを実行すると呼ばれる関数によって返される任意の SQLSTATE を返すこと (**SQLExecute**または**SQLExecDirect**)。 列のデータを送信中に呼び出された場合更新または追加**SQLBulkOperations**で更新されているまたは**SQLSetPos**、によって返される任意の SQLSTATE を返すことができます**SQLBulkOperations**または**SQLSetPos**します。  
  
## <a name="comments"></a>コメント  
 **SQLParamData**実行時のデータのデータを 2 つの使用を提供するということができます: パラメーターのデータへの呼び出しで使用される**SQLExecute**または**SQLExecDirect**、または列のデータとなる場合に使用されます行が更新またはへの呼び出しによって追加**SQLBulkOperations**への呼び出しによって更新または**SQLSetPos**します。 実行時に、 **SQLParamData**インジケーター データのドライバーで必要なアプリケーションに返します。  
  
 アプリケーションを呼び出すと**SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**、または**SQLSetPos**ドライバーは SQL_NEED_ を返します実行時のデータのデータが必要がある場合は、データ。 その後、アプリケーションを呼び出す**SQLParamData**に送信するデータを決定します。 ドライバーは、パラメーターのデータを必要とする場合、ドライバーを返します、  *\*ValuePtrPtr*出力バッファーの行セットのバッファーでアプリケーションを配置する値。 アプリケーションでは、ドライバーが要求しているパラメーター データを決定するのに、この値を使用できます。 ドライバーは、列のデータを必要とする場合、ドライバーを返します、  *\*ValuePtrPtr*バッファーの列が最初にバインドされている、次のように、アドレス。  
  
 *アドレスをバインド* + *オフセットをバインド*+ ((*行数*- 1) x*要素のサイズ*)  
  
 変数が定義されて次の表に記載されています。  
  
|変数|説明|  
|--------------|-----------------|  
|*アドレスをバインドします。*|指定したアドレス、 *TargetValuePtr*引数**SQLBindCol**します。|  
|*バインディングのオフセット*|SQL_ATTR_ROW_BIND_OFFSET_PTR ステートメント属性で指定されたアドレスに格納された値。|  
|*行番号*|1 から始まる行セットの行の数。 単一行のフェッチは、既定値は、これは 1 です。|  
|*要素のサイズ*|両方のデータと長さ/インジケーター バッファーの SQL_ATTR_ROW_BIND_TYPE ステートメント属性の値。|  
  
 また、インジケーターを呼び出す必要があるアプリケーションには、SQL_NEED_DATA を返します**SQLPutData**データを送信します。  
  
 アプリケーション呼び出し**SQLPutData**列またはパラメーターの実行時のデータのデータを送信するために必要な回数だけです。 列またはパラメーターのすべてのデータが送信された後、アプリケーションを呼び出す**SQLParamData**もう一度です。 場合**SQLParamData** SQL_NEED_DATA を返しますがもう 1 つのパラメーターまたは列のデータを送信する必要があります。 そのため、もう一度アプリケーションを呼び出す**SQLPutData**します。 実行時のデータのすべてのデータがすべてのパラメーターまたは列の送信された場合**SQLParamData** SQL_SUCCESS または SQL_SUCCESS_WITH_INFO の値を返します *\*ValuePtrPtr*は定義されていませんSQL ステートメントを実行して、または**SQLBulkOperations**または**SQLSetPos**呼び出しを処理できます。  
  
 場合**SQLParamData**を検索対象の提供が終了パラメーターのデータを更新または delete の各データ ソースへの呼び出しですべての行には影響しませんステートメント**SQLParamData** sql_no_data が返されます。  
  
 方法の実行時データ パラメーターのデータの詳細については、ステートメントの実行時に渡されるを参照してください「パラメーターの値を渡す」で[SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)と[長い形式のデータを送信する](../../../odbc/reference/develop-app/sending-long-data.md)します。 更新や追加方法 - 実行時データ列のデータに関する詳細についてを参照してください"を使用して SQLSetPos" [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)、「を実行する一括更新プログラムを使用してブックマーク」で[SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)、[長い形式のデータ、SQLSetPos および SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)します。  
  
 **SQLParamData**ストリーミングされる出力パラメーターを取得するということができます。 ときに**SQLMoreResults**、 **SQLExecute**、 **SQLGetData**、または**SQLExecDirect**返します SQL_PARAM_DATA_AVAILABLE、呼び出す**SQLParamData**パラメーターが使用可能な値を判別します。 SQL_PARAM_DATA_AVAILABLE とストリーミングされる出力パラメーターの詳細については、次を参照してください。 [SQLGetData を使用して出力パラメーターを取得する](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)します。  
  
## <a name="code-example"></a>コード例  
 参照してください[SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)します。  
  
## <a name="related-functions"></a>関連する関数  
  
|詳細|参照先|  
|---------------------------|---------|  
|バッファーをパラメーターにバインドします。|[SQLBindParameter 関数](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|ステートメントの処理をキャンセル|[SQLCancel 関数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|ステートメント内のパラメーターに関する情報を返す|[SQLDescribeParam 関数](../../../odbc/reference/syntax/sqldescribeparam-function.md)|  
|SQL ステートメントを実行します。|[SQLExecDirect 関数](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|準備された SQL ステートメントを実行します。|[SQLExecute 関数](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|実行時にパラメーターのデータを送信します。|[SQLPutData 関数](../../../odbc/reference/syntax/sqlputdata-function.md)|  
  
## <a name="see-also"></a>参照  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)   
 [SQLGetData を使用した出力パラメーターの取得](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
