---
title: SQLGetData 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetData
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetData
helpviewer_keywords:
- SQLGetData function [ODBC]
ms.assetid: e3c1356a-5db7-4186-85fd-8b74633317e8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f33d55cc8ac5dab37ce200a5a654bcb4be7cc9ad
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67911361"
---
# <a name="sqlgetdata-function"></a>SQLGetData 関数
**準拠**  
 バージョンが導入されました。ODBC 1.0 規格に準拠します。ISO 92  
  
 **まとめ**  
 **SQLGetData**結果セット内の 1 つの列または後に 1 つのパラメーターのデータを取得します。 **SQLParamData** SQL_PARAM_DATA_AVAILABLE を返します。 呼び出せる複数回パーツ内の可変長データを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLGetData(  
      SQLHSTMT       StatementHandle,  
      SQLUSMALLINT   Col_or_Param_Num,  
      SQLSMALLINT    TargetType,  
      SQLPOINTER     TargetValuePtr,  
      SQLLEN         BufferLength,  
      SQLLEN *       StrLen_or_IndPtr);  
```  
  
## <a name="arguments"></a>引数  
 *StatementHandle*  
 [入力]ステートメント ハンドルです。  
  
 *Col_or_Param_Num*  
 [入力]列のデータを取得するには、データを返す対象の列の数になります。 結果セットの列は、列の昇順に 1 から始まる番号が付けられます。 ブックマーク列は、列番号が 0 になります。これは、ブックマークが有効になっているかどうかにのみ指定します。  
  
 パラメーターのデータを取得するには、1 から始まりますパラメーターの序数です。  
  
 *TargetType*  
 [入力]C データ型の型の識別子、**TargetValuePtr*バッファー。 有効な C データ型と型識別子の一覧は、次を参照してください、 [C データ型](../../../odbc/reference/appendixes/c-data-types.md)付録 d: セクション。データ型。  
  
 場合*TargetType* SQL_ARD_TYPE、型識別子が、ARD の SQL_DESC_CONCISE_TYPE フィールドで指定されたドライバーの使用です。 場合*TargetType*は SQL_APD_TYPE、 **SQLGetData**で指定されている同じの C データ型を使用して、 **SQLBindParameter**します。 C データ型がで指定された場合は、 **SQLGetData**で指定された C データ型をオーバーライド**SQLBindParameter**します。 SQL_C_DEFAULT がの場合、ドライバーは、ソースの SQL データ型に基づいて既定の C データ型を選択します。  
  
 拡張の C データ型を指定することもできます。 詳細については、次を参照してください。 [ODBC における C データ型](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)します。  
  
 *TargetValuePtr*  
 [出力]データを返すバッファーへのポインター。  
  
 *TargetValuePtr* NULL にすることはできません。  
  
 *BufferLength*  
 [入力]長さ、**TargetValuePtr*バッファー (バイト単位)。  
  
 ドライバーを使用して*BufferLength*の末尾を越えて書き込みを回避するために、 \* *TargetValuePtr*文字またはバイナリ データなどの可変長データを返すときのバッファーします。 文字データを返すときに、ドライバーが、null 終了文字をカウントことに注意してください。 \* *TargetValuePtr*します。 **TargetValuePtr* null 終端文字用の領域を含める必要がありますので、ドライバーには、データが切り捨てられますか。  
  
 ドライバーには整数、日付構造体などの固定長データが返されるときに、ドライバーは無視されます*BufferLength*バッファーが、データを保持するのに十分な大きさを前提としています。 固定長のデータを十分な大きさのバッファーを割り当て、アプリケーションにとって重要ではそのため、または、ドライバーは、バッファーの末尾を越えて書き込み。  
  
 **SQLGetData** SQLSTATE HY090 が返されます (無効な文字列長またはバッファー長) と*BufferLength*が 0 未満の値がときではなく*BufferLength*は 0 です。  
  
 *StrLen_or_IndPtr*  
 [出力]長さまたはインジケーターの値を返すバッファーへのポインター。 これが null ポインターである場合は、長さまたはインジケーターの値は返されません。 フェッチされるデータが NULL の場合、エラーが返されます。  
  
 **SQLGetData**長さ/インジケーター バッファーでは、次の値を返すことができます。  
  
-   返される使用可能なデータの長さ  
  
-   SQL_NO_TOTAL  
  
-   SQL_NULL_DATA  
  
 詳細については、次を参照してください。[長さ/インジケーターの値を使用して](../../../odbc/reference/develop-app/using-length-and-indicator-values.md)とこのトピックでは、"コメント"。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_NO_DATA、SQL_STILL_EXECUTING、SQL_ERROR、または SQL_INVALID_HANDLE します。  
  
## <a name="diagnostics"></a>診断  
 ときに**SQLGetData** SQL_ERROR または SQL_SUCCESS_WITH_INFO のいずれかを返します呼び出すことによって、関連付けられた SQLSTATE 値を取得できる**SQLGetDiagRec**で、 *HandleType*のSql_handle_stmt として、*処理*の*StatementHandle*します。 次の表に、一般的にによって返される SQLSTATE 値**SQLGetData** ; この関数のコンテキストでそれぞれについて説明しますと表記"(DM)"の前にドライバー マネージャーによって返されるについての説明。 SQLSTATE 値ごとに関連付けられているリターン コードは明記しない限り、SQL_ERROR です。  
  
|SQLSTATE|[エラー]|説明|  
|--------------|-----------|-----------------|  
|01000|一般的な警告|ドライバー固有の情報メッセージです。 (関数は、SQL_SUCCESS_WITH_INFO を返します)。|  
|01004|文字列データで、右側が切り捨てられました|指定した列のデータかを満たさない*Col_or_Param_Num*関数は、1 回の呼び出しで取得される可能性があります。 SQL_NO_TOTAL を現在の呼び出しの前に指定された列の残りのデータの長さまたは**SQLGetData**で返される\* *StrLen_or_IndPtr*します。 (関数は、SQL_SUCCESS_WITH_INFO を返します)。<br /><br /> 複数の呼び出しを使用しての詳細については**SQLGetData** 1 つの列「コメントです。」を参照してください。|  
|01S07|分数が切り捨てられました|1 つまたは複数の列に対して返されるデータが切り捨てられました。 数値データ型、数値の小数部が切り捨てられました。 時刻、タイムスタンプ、および時間コンポーネントを含む interval データ型の場合は、時間の小数部が切り捨てられました。<br /><br /> (関数は、SQL_SUCCESS_WITH_INFO を返します)。|  
|07006|制限付きのデータ型の属性違反|結果セット内の列のデータ値は、引数で指定された C データ型に変換できません*TargetType*します。|  
|07009|無効な記述子のインデックス|引数が指定された値*Col_or_Param_Num* 0 の場合、SQL_UB_OFF に SQL_ATTR_USE_BOOKMARKS ステートメントの属性が設定されました。<br /><br /> 引数が指定された値*Col_or_Param_Num*が結果セット内の列の数を超えていました。<br /><br /> *Col_or_Param_Num*値が使用できるパラメーターの序数と等しくありませんでした。<br /><br /> (DM) 指定された列にバインドされました。 この説明は、ドライバーの SQL_GETDATA_EXTENSIONS オプション SQL_GD_BOUND ビットマスクを返すには適用されません**SQLGetInfo**します。<br /><br /> (DM) 指定された列の数が、最高のバインドされた列の数以下が。 この説明は、ドライバーの SQL_GETDATA_EXTENSIONS オプション SQL_GD_ANY_COLUMN ビットマスクを返すには適用されません**SQLGetInfo**します。<br /><br /> (DM)、アプリケーションが既に呼び出されて**SQLGetData**は現在の行の現在の呼び出しで指定された列の数が上記の呼び出しで指定された列の数よりも小さいと、ドライバーでは、sql _ が返されませんSQL_GETDATA_EXTENSIONS オプションのビットマスクを GD_ANY_ORDER **SQLGetInfo**します。<br /><br /> (DM)、 *TargetType*引数が SQL_ARD_TYPE、および*Col_or_Param_Num*記述子レコード、ARD で整合性チェックに失敗しました。<br /><br /> (DM)、 *TargetType*引数 SQL_ARD_TYPE、ARD の SQL_DESC_COUNT フィールドの値より小さい*Col_or_Param_Num*引数。|  
|08S01|通信リンク エラー|関数が完了した処理の前に、ドライバーとドライバーが接続されているデータ ソース間の通信リンクに失敗しました。|  
|22002|インジケーター変数が必要ですが、指定されていません|*StrLen_or_IndPtr* null ポインター、NULL データを取得します。|  
|22003|数値が範囲外|(数値または文字列) として、列の数値の値を取得する原因となる (ではなく小数部) 整数部分が切り捨てられる数値。<br /><br /> 詳細については、次を参照してください[付録 d:。データ型](../../../odbc/reference/appendixes/appendix-d-data-types.md)します。|  
|22007|無効な datetime 形式|結果セット内の文字の列 C 日付、時刻、またはタイムスタンプの構造体にバインドされましたし、列の値が無効な日付、時間、またはタイムスタンプ、それぞれします。 詳細については、次を参照してください[付録 d:。データ型](../../../odbc/reference/appendixes/appendix-d-data-types.md)します。|  
|22012|0 による除算|0 による除算の結果が算術式の値が返されました。|  
|22015|Interval フィールド オーバーフロー|真数型または interval SQL 型から C の間隔の種類への割り当てと、先頭のフィールドに有効桁数の損失が発生します。<br /><br /> C の間隔の種類にデータを返すときに C の間隔の種類の SQL 型の値の表現はありませんでした。|  
|22018|キャストの無効な文字の値|C 文字バッファーに返された結果セット内の文字の列と列には、対象のバッファーの文字セットで表現がない文字が含まれています。<br /><br /> C 型は、真数または概数の数値、datetime、またはデータ間隔の種類。列の SQL 型が文字データ型。列の値がバインドされた C 型の有効なリテラルではありませんでした。|  
|24000|カーソル状態が無効|(DM) 最初に呼び出さず、関数が呼び出された**SQLFetch**または**SQLFetchScroll**に必要なデータの行にカーソルを移動します。<br /><br /> (DM)、 *StatementHandle* 、実行の状態でしたが、結果セットが関連付けられていない、 *StatementHandle*します。<br /><br /> カーソルが開いて、 *StatementHandle*と**SQLFetch**または**SQLFetchScroll**が呼び出された、または後に、結果セットの開始前に、カーソルが配置されたが、結果セットの末尾。|  
|HY000|一般的なエラー|これがなかった固有の SQLSTATE とする実装に固有の SQLSTATE が定義されていない、エラーが発生しました。 によって返されるエラー メッセージ**SQLGetDiagRec**で、 *MessageText*バッファーは、エラーとその原因について説明します。|  
|HY001|メモリの割り当てエラー|ドライバーは、実行または関数の完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY003|範囲外のプログラムの種類|(DM) 引数*TargetType*が有効なデータ型、SQL_C_DEFAULT、SQL_ARD_TYPE (列のデータを取得する) の場合、または SQL_APD_TYPE (パラメーターのデータの取得) の場合。<br /><br /> (DM) 引数*Col_or_Param_Num*が 0、および引数*TargetType*可変長のブックマークに対して、SQL_C_BOOKMARK 固定長のブックマークまたは SQL_C_VARBOOKMARK にしました。|  
|HY008|操作が取り消されました|非同期処理が有効に、 *StatementHandle*します。 関数が呼び出された、および実行を完了する前に**SQLCancel**または**SQLCancelHandle**が呼び出されて、 *StatementHandle*関数が呼び出された後、もう一度、 *StatementHandle*します。<br /><br /> 関数が呼び出された、および実行を完了する前に**SQLCancel**または**SQLCancelHandle**が呼び出されて、 *StatementHandle*から別のスレッドで、マルチ スレッド アプリケーションは、し、関数で再度呼び出さ、 *StatementHandle*します。|  
|HY009|無効な null ポインターの使用|(DM) 引数*TargetValuePtr*が null ポインター。|  
|HY010|関数のシーケンス エラー|(DM)、指定した*StatementHandle*実行の状態ではありませんでした。 最初に呼び出さず、関数が呼び出された**SQLExecDirect**、 **SQLExecute**またはカタログ関数。<br /><br /> (DM) を非同期的に実行中の関数が呼び出された接続ハンドルに関連付けられているため、 *StatementHandle*します。 この非同期関数ではときに実行されている、 **SQLGetData**関数が呼び出されました。<br /><br /> (DM) を非同期的に実行中の関数 (いないこの"1") が呼び出された、 *StatementHandle*この関数が呼び出されたときに実行されているとします。<br /><br /> (DM) **SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**、または**SQLSetPos**に対して呼び出された、 *StatementHandle* SQL_NEED_DATA が返されます。 すべての実行時データ パラメーターまたは列のデータが送信される前に、この関数が呼び出されました。<br /><br /> (DM)、 *StatementHandle* 、実行の状態でしたが、結果セットが関連付けられていない、 *StatementHandle*します。<br /><br /> 呼び出し**SQLExeceute**、 **SQLExecDirect**、または**SQLMoreResults** SQL_PARAM_DATA_AVAILABLE が返されますが、 **SQLGetData**が呼び出されました、の代わりに**SQLParamData**します。|  
|HY013|メモリ管理エラー|基になるメモリ オブジェクトにアクセスできませんでした、場合によってメモリ不足が原因であるために、関数呼び出しを処理できませんでした。|  
|HY090|文字列またはバッファーの長さが無効です。|引数に指定された (DM) 値*BufferLength*が 0 未満でした。<br /><br /> 引数に指定された値*BufferLength*が 4 未満、 *Col_or_Param_Num*引数が 0 の場合に設定されており、ドライバーが、ODBC 2 *.x*ドライバー。|  
|HY109|無効なカーソルの位置|カーソルの位置が (によって**SQLSetPos**、 **SQLFetch**、 **SQLFetchScroll**、または**SQLBulkOperations**) が削除された行またはをフェッチできませんでした。<br /><br /> カーソルが順方向専用カーソルでは、および行セットのサイズが 1 より大きかった。|  
|HY117|不明なトランザクションの状態のため、接続が中断されます。 のみを切断して、読み取り専用の関数が許可されます。|(DM) 中断状態の詳細については、次を参照してください。 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)します。|  
|HYC00|省略可能な機能が実装されていません|ドライバーまたはデータ ソースは、の使用をサポートしていない**SQLGetData**で複数の行で**SQLFetchScroll**します。 この説明は、ドライバーの SQL_GETDATA_EXTENSIONS オプション SQL_GD_BLOCK ビットマスクを返すには適用されません**SQLGetInfo**します。<br /><br /> ドライバーまたはデータ ソースの組み合わせで指定された変換をサポートしていません、 *TargetType*引数と対応する列の SQL データ型。 このエラーは、列の SQL データ型は、ドライバー固有の SQL データ型にマップされていた場合にのみ適用されます。<br /><br /> ドライバーには、ODBC 2 のみがサポートしている *.x*、および引数*TargetType*が、次のいずれか。<br /><br /> SQL_C_NUMERIC SQL_C_SBIGINT SQL_C_UBIGINT<br /><br /> 間隔の C データ型のいずれかと[C データ型](../../../odbc/reference/appendixes/c-data-types.md)付録 d:データ型。<br /><br /> ドライバーのみ、3.50 と引数の前に ODBC バージョンをサポートする*TargetType* SQL_C_GUID でした。|  
|HYT01|接続がタイムアウトしました|データ ソースが要求に応答する前に、接続のタイムアウト期間が終了しました。 によって、接続タイムアウト期間が設定されます**SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT します。|  
|IM001|ドライバーでは、この関数はサポートされていません|(DM) に対応するドライバー、 *StatementHandle*関数をサポートしていません。|  
|IM017|非同期通知モードでのポーリングは無効です。|通知のモデルを使用すると、常にポーリングは無効です。|  
|IM018|**SQLCompleteAsync**このハンドルに対する前の非同期操作を完了が呼び出されていません。|通知モードが有効になっている場合、ハンドルでは、前の関数呼び出しに SQL_STILL_EXECUTING が返された場合と**SQLCompleteAsync**後処理を行い、操作を完了するハンドルで呼び出す必要があります。|  
  
## <a name="comments"></a>コメント  
 **SQLGetData**指定された列のデータを返します。 **SQLGetData**ごとに結果セットから 1 つまたは複数の行がフェッチ後にのみ呼び出すことができます**SQLFetch**、 **SQLFetchScroll**、または**SQLExtendedFetch**します。 可変長のデータが大きすぎて単一の呼び出しで返される場合**SQLGetData** (の制限により、アプリケーションで)、 **SQLGetData**部分で取得できます。 行と呼び出しで一部の列をバインドすることは**SQLGetData**それ以外の場合がいくつかの制限を受けます。 詳細については、次を参照してください。[長い形式のデータを取得する](../../../odbc/reference/develop-app/getting-long-data.md)します。  
  
 使用方法について**SQLGetData**ストリーミングされる出力パラメーターで、次を参照してください。 [SQLGetData を使用して出力パラメーターを取得する](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)します。  
  
## <a name="using-sqlgetdata"></a>SQLGetData を使用します。  
 ドライバーでの拡張機能がサポートされていない場合**SQLGetData**関数は、データを返す数がバインドされていない列に対してのみその最後のバインドされた列の値より大きい。 さらに、データの値の行内の*Col_or_Param_Num*への各呼び出しで引数**SQLGetData**の値以上にする必要があります*Col_or_Param_Num*; 前の呼び出しでつまり、列番号の昇順でデータを取得する必要があります。 最後に拡張機能がサポートされていない場合、 **SQLGetData**行セットのサイズが 1 より大きい場合に呼び出すことはできません。  
  
 ドライバーは、これらの制限のいずれかを緩和できます。 ドライバーの制限を緩和制限を確認するアプリケーションを呼び出す**SQLGetInfo** SQL_GETDATA_EXTENSIONS の次のオプションのいずれかで。  
  
-   SQL_GD_OUTPUT_PARAMS = **SQLGetData**出力パラメーターの値を返すを呼び出すことができます。 詳細については、次を参照してください。 [SQLGetData を使用して出力パラメーターを取得する](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)します。  
  
-   SQL_GD_ANY_COLUMN します。 このオプションが返された場合**SQLGetData**最後の列をバインドする前に含めて、任意のバインドされていない列を呼び出すことができます。  
  
-   SQL_GD_ANY_ORDER します。 このオプションが返された場合**SQLGetData**任意の順序でバインドされていない列を呼び出すことができます。  
  
-   SQL_GD_BLOCK します。 このオプションは、によって返される場合**SQLGetInfo** SQL_GETDATA_EXTENSIONS 情報の種類は、ドライバーへの呼び出しをサポートしています**SQLGetData**行セットのサイズが 1 より大きいと、アプリケーションがを呼び出すことができます **。SQLSetPos**呼び出す前に適切な行にカーソルを配置することも SQL_POSITION **SQLGetData します。**  
  
-   SQL_GD_BOUND します。 このオプションが返された場合**SQLGetData**バインドされた列に対して呼び出すこととしてバインドされていない列。  
  
 これらの制限事項とそれらを緩和するドライバーの機能に 2 つの例外があります。 まず、 **SQLGetData**呼び出さないで順方向専用カーソルの行セットのサイズが 1 より大きい場合。 第 2 に、ドライバーは、ブックマークをサポートする場合する必要があります常にサポートを呼び出す機能**SQLGetData**列 0 を呼び出すアプリケーションを許可しない場合でも**SQLGetData**の他の列の最後より前に、バインドされた列です。 (ODBC 2 で、アプリケーションが動作するときに *.x*ドライバー、 **SQLGetData**で呼び出されたときにブックマークが正常に返されます*Col_or_Param_Num*呼び出しの後に 0 に等しい**SQLFetch**ため、 **SQLFetch** ODBC 3 によってマップされた *.x*をドライバー マネージャー **SQLExtendedFetch** で*FetchOrientation* sql_fetch_next、および**SQLGetData**で、 *Col_or_Param_Num* ODBC 3 によって 0 にマップされて *.x*をドライバー マネージャー**SQLGetStmtOption**で、 *fOption* SQL_GET_BOOKMARK の)。  
  
 **SQLGetData**だけ呼び出すことによって挿入された行のブックマークを取得するのには使用できません**SQLBulkOperations** SQL_ADD オプションでは、カーソルが行に配置されていないためです。 アプリケーションは、呼び出す前に、バインド列 0 でこのような行のブックマークを取得することができます**SQLBulkOperations**である場合、SQL_ADD で**SQLBulkOperations**バインドされたバッファー内のブックマークを返します。 **SQLFetchScroll**し、その行にカーソルの位置を変更する SQL_FETCH_BOOKMARK を呼び出すことができます。  
  
 場合、 *TargetType*引数の SQL_DESC_DATETIME_INTERVAL_PRECISION および SQL_DESC_PRECISION のフィールド セットとして、interval データ型を既定の間隔の主要な精度 (2) と既定の間隔 (秒) の有効桁数 (6) は、それぞれ、ARD データに使用されます。 場合、 *TargetType*引数、SQL_C_NUMERIC データ型を (ドライバー定義) の既定の精度は、および、ARD の SQL_DESC_PRECISION および SQL_DESC_SCALE フィールドで設定されている既定のスケール (0)、データに使用されます。 呼び出して場合、アプリケーションで明示的に適切な記述子フィールドを設定、既定の有効桁数または小数点が適切でない場合**SQLSetDescField**または**SQLSetDescRec**します。 SQL_C_NUMERIC と呼び出しに SQL_DESC_CONCISE_TYPE フィールドを設定できます**SQLGetData**で、 *TargetType* SQL_ARD_TYPE と、記述子フィールドの有効桁数と小数点の値の引数使用します。  
  
> [!NOTE]
>  ODBC 2 *.x*、アプリケーション セット*TargetType*を示すために、SQL_C_DATE、SQL_C_TIME、または SQL_C_TIMESTAMP \* *TargetValuePtr*日付、時刻、またはタイムスタンプの構造体。 ODBC 3 *.x*、アプリケーション セット*TargetType* SQL_C_TYPE_DATE、SQL_C_TYPE_TIME、SQL_C_TYPE_TIMESTAMP したりします。 ドライバー マネージャーで適切なマッピングに基づき、必要な場合、アプリケーションとドライバーのバージョン。  
  
## <a name="retrieving-variable-length-data-in-parts"></a>部分の可変長データを取得します。  
 **SQLGetData**が SQL_CHAR、SQL_VARCHAR、SQL_LONGVARCHAR、SQL_WCHAR、SQL_WVARCHAR、sql _、列の SQL データ型の識別子は、要素の可変長データを格納する列からデータを取得するために使用できますWLONGVARCHAR、SQL_BINARY、SQL_VARBINARY、SQL_LONGVARBINARY、または可変長型のドライバー固有の識別子。  
  
 アプリケーションを呼び出す部分内の列からデータを取得する**SQLGetData**複数回、同じ列に連続でします。 各呼び出しで**SQLGetData**データの次の部分を返します。 文字データの中間部分から、null 終了文字を削除してください、パーツを再構成するため、アプリケーションの責任です。 多くのデータを返すか、終端文字用に十分なバッファーが割り当てられた場合**SQLGetData** SQL_SUCCESS_WITH_INFO と SQLSTATE 01004 (データが切り捨てられます) を返します。 データの最後の部分が返されるとき**SQLGetData** SQL_SUCCESS を返します。 ブックをいないため、アプリケーションは、アプリケーションのバッファー内のデータの量が有効かを知る方法 SQL_NO_TOTAL もゼロを列からデータを取得する有効な最後の呼び出しで返されることができます。 場合**SQLGetData**と呼ばれるは、その後、sql_no_data します。 詳細については、次のセクションでは、「SQLGetData を取得するデータ。」を参照してください。  
  
 可変長のブックマークでの部分で返される**SQLGetData**します。 その他のデータへの呼び出しと同様**SQLGetData**パーツ内の可変長のブックマークから返されるより多くのデータがある場合に、SQLSTATE 01004 (文字列データの右側が切り捨てられました) と SQL_SUCCESS_WITH_INFO を返すが戻ります。 これは、可変長のブックマークがへの呼び出しによって切り捨てられる場合とは異なる**SQLFetch**または**SQLFetchScroll**SQL_ERROR と SQLSTATE 22001 (文字列データの右側が切り捨てられました) が返されます。  
  
 **SQLGetData**部分に固定長データを返すには使用できません。 場合**SQLGetData**は行内の 1 回以上呼び出されると、固定長のデータを含んでいる列の sql_no_data が返されるすべての呼び出しに対して、最初より後です。  
  
## <a name="retrieving-streamed-output-parameters"></a>ストリーミングされる出力パラメーターを取得します。  
 アプリケーションが呼び出すことができる場合、ドライバーは、ストリーミングされる出力パラメーターをサポートする**SQLGetData**小規模な大きなパラメーター値を取得する回数をバッファーします。 ストリーミングされる出力パラメーターの詳細については、次を参照してください。 [SQLGetData を使用して出力パラメーターを取得する](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)します。  
  
## <a name="retrieving-data-with-sqlgetdata"></a>SQLGetData によるデータの取得  
 指定した列のデータを返す**SQLGetData**は、次の一連の手順を実行します。  
  
1.  既にが返すすべての列のデータの場合は、SQL_NO_DATA を返します。  
  
2.  セット\* *StrLen_or_IndPtr* SQL_NULL_DATA データが NULL の場合にします。 データが NULL の場合と*StrLen_or_IndPtr*が null ポインターの場合は、 **SQLGetData** SQLSTATE 22002 (インジケーター変数に必要なが指定されていません) を返します。  
  
     列のデータが NULL でない場合**SQLGetData**手順 3. に進みます。  
  
3.  文字またはバイナリ データは、列が含まれている場合、0 以外の値に SQL_ATTR_MAX_LENGTH ステートメントの属性が設定されている場合、 **SQLGetData**が既に呼び出されていないに SQL_ATTR_MAX_LENGTH を列のデータが切り捨てられますバイト数。  
  
    > [!NOTE]  
    >  SQL_ATTR_MAX_LENGTH ステートメント属性は、ネットワーク トラフィックを削減するものです。 一般に、ネットワーク経由で返す前に、データが切り捨てられますデータ ソースによって実装されます。 ドライバーとデータ ソースは、それをサポートする必要はありません。 そのため、データが特定のサイズに切り捨てられたことを確実に、アプリケーションする必要がありますそのサイズのバッファーを割り当てるし、サイズで指定、 *BufferLength*引数。  
  
4.  指定された種類のデータを変換*TargetType*します。 データはそのデータ型、既定の有効桁数と小数点指定します。 場合*TargetType* SQL_ARD_TYPE、データは、ARD の SQL_DESC_CONCISE_TYPE フィールドの型を使用します。 場合*TargetType* SQL_ARD_TYPE にも、データがで指定された有効桁数と小数点 SQL_DESC_DATETIME_INTERVAL_PRECISION、SQL_DESC_PRECISION、SQL_DESC_CONCISE でのデータに応じて、ARD SQL_DESC_SCALE フィールドを入力フィールドの種類 (_t)。 呼び出して場合、アプリケーションで明示的に適切な記述子フィールドを設定、既定の有効桁数または小数点が適切でない場合**SQLSetDescField**または**SQLSetDescRec**します。  
  
5.  データが文字またはバイナリなどの可変長データ型に変換された場合**SQLGetData**データ長を超えているかどうかを確認します。 *BufferLength*します。 (Null 終了文字を含む) の文字データの長さを超えた場合*BufferLength*、 **SQLGetData**にデータが切り捨てられます*BufferLength*長さ未満null 終了文字です。 Null 終端データ。 バイナリ データのデータ バッファーの長さを超えている場合**SQLGetData**まで切り捨てます*BufferLength*バイト。  
  
     Null 終了文字を保持するためには、指定されたデータ バッファーが小さすぎる場合**SQLGetData** SQL_SUCCESS_WITH_INFO と SQLSTATE 01004 を返します。  
  
     **SQLGetData**切り捨てますしない固定長データ型に変換されたデータは常に想定するの長さ **TargetValuePtr*データ型のサイズです。  
  
6.  変換された (および切り捨てられる可能性があります) のデータを配置\* *TargetValuePtr*します。 なお**SQLGetData**行からデータを返すことはできません。  
  
7.  配置内のデータの長さ\* *StrLen_or_IndPtr*します。 場合*StrLen_or_IndPtr*が null ポインターの場合は、 **SQLGetData**長さは返されません。  
  
    -   文字またはバイナリ データは、これは、データの長さの変換後と理由のための切り捨て前に、 *BufferLength*します。 場合は、ドライバーは長い形式のデータの場合、変換後、データの長さを決定することはできません、SQL_SUCCESS_WITH_INFO が返されます、長 SQL_NO_TOTAL に設定します。 (最後の呼び出し**SQLGetData** 0 または SQL_NO_TOTAL ではない、データの長さを常に返す必要があります)。実際の長さではなく、この属性の値を配置、SQL_ATTR_MAX_LENGTH ステートメント属性によりデータが切り捨てられる場合\* *StrLen_or_IndPtr*します。 これは、この属性は、ドライバーはどのような実際の長さを判断する方法を持たないため、変換前に、サーバー上のデータを切り捨てるに設計されているためにです。 ときに**SQLGetData**を連続して複数回呼び出されると、同じ列に、これは、現在の呼び出しの開始時に使用可能なデータの長さは、後続の呼び出しごとでは、長さが減ります。  
  
    -   その他のすべてのデータ型の変換後、データの長さは、このこれは、データが変換される型のサイズがあります。  
  
8.  変換中に有意性を失うことがなく、データを切り捨てるかどうか (たとえば、実数 1.234 は切り捨てられます 1 の整数に変換される) ため、または*BufferLength*が小さすぎる (たとえば、文字列"abcdef"を配置4 バイト バッファー) で**SQLGetData** SQLSTATE 01004 (データが切り捨てられました) と、SQL_SUCCESS_WITH_INFO を返します。 SQL_ATTR_MAX_LENGTH ステートメント属性のための有効桁数を失うことがなくデータが切り捨てられる場合**SQLGetData** SQL_SUCCESS を返し、SQLSTATE 01004 (データが切り捨てられます) は返されません。  
  
 バインドされたデータ バッファーの内容 (場合**SQLGetData**がバインドされた列で呼び出されます) および長さ/インジケーター バッファーは定義されていない場合は**SQLGetData** SQL_SUCCESS または SQL_SUCCESS_WITH_INFO が返されません。  
  
 連続して呼び出す**SQLGetData**要求された最後の列からデータが取得されます。 以前のオフセットが無効になります。 たとえば、ときに、次のシーケンスは実行されます。  
  
```cpp  
SQLGetData(icol=n), SQLGetData(icol=m), SQLGetData(icol=n)  
```  
  
 SQLGetData(icol=n) の 2 番目の呼び出しは、n 個の列の先頭からのデータを取得します。 以前の呼び出しによるデータの任意のオフセット**SQLGetData**列が有効ではなくなりました。  
  
## <a name="descriptors-and-sqlgetdata"></a>記述子および SQLGetData  
 **SQLGetData**任意の記述子フィールドと直接対話しません。  
  
 場合*TargetType* SQL_ARD_TYPE、データは、ARD の SQL_DESC_CONCISE_TYPE フィールドの型を使用します。 場合*TargetType* SQL_ARD_TYPE または SQL_C_DEFAULT は、データがで指定された有効桁数と小数点 SQL_DESC_DATETIME_INTERVAL_PRECISION、SQL_DESC_PRECISION、および種類のデータに応じて、ARD SQL_DESC_SCALE フィールドSQL_DESC_CONCISE_TYPE フィールド。  
  
## <a name="code-example"></a>コード例  
 次の例では、アプリケーションを実行、**選択**ステートメントを Id、名、顧客の結果セットを返すし、電話番号の名前、ID、および電話番号で並べ替えられます。 データの各行に対して呼び出す**SQLFetch**に次の行にカーソルを移動します。 呼び出す**SQLGetData**取得するへの呼び出しで、フェッチされたデータは、データと返されたバイト数のバッファーを指定します。 **SQLGetData**します。 最後に、各従業員の名前、ID、および電話番号を印刷します。  
  
```cpp  
#define NAME_LEN 50  
#define PHONE_LEN 50  
  
SQLCHAR      szName[NAME_LEN], szPhone[PHONE_LEN];  
SQLINTEGER   sCustID, cbName, cbAge, cbBirthday;  
SQLRETURN    retcode;  
SQLHSTMT     hstmt;  
  
retcode = SQLExecDirect(hstmt,  
   "SELECT CUSTID, NAME, PHONE FROM CUSTOMERS ORDER BY 2, 1, 3",  
   SQL_NTS);  
  
if (retcode == SQL_SUCCESS) {  
   while (TRUE) {  
      retcode = SQLFetch(hstmt);  
      if (retcode == SQL_ERROR || retcode == SQL_SUCCESS_WITH_INFO) {  
         show_error();  
      }  
      if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO){  
  
         /* Get data for columns 1, 2, and 3 */  
  
         SQLGetData(hstmt, 1, SQL_C_ULONG, &sCustID, 0, &cbCustID);  
         SQLGetData(hstmt, 2, SQL_C_CHAR, szName, NAME_LEN, &cbName);  
         SQLGetData(hstmt, 3, SQL_C_CHAR, szPhone, PHONE_LEN,  
            &cbPhone);  
  
         /* Print the row of data */  
  
         fprintf(out, "%-5d %-*s %*s", sCustID, NAME_LEN-1, szName,   
            PHONE_LEN-1, szPhone);  
      } else {  
         break;  
      }  
   }  
}  
```  
  
## <a name="related-functions"></a>関連する関数  
  
|詳細|参照先|  
|---------------------------|---------|  
|結果セット内の列のストレージの割り当てください。|[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|ブロック カーソルの位置に関係なく一括操作を実行します。|[SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|ステートメントの処理をキャンセル|[SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|SQL ステートメントを実行します。|[SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|準備された SQL ステートメントを実行します。|[SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|データのブロックをフェッチしています。 または、結果をスクロールの設定|[SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|1 行のデータまたは順方向専用の方向にデータのブロックをフェッチしています|[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|実行時にパラメーターのデータを送信します。|[SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)|  
|カーソルを配置するか、行セットでデータを更新、更新、または行セット内のデータを削除します。|[SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
  
## <a name="see-also"></a>参照  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)   
 [SQLGetData を使用した出力パラメーターの取得](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
