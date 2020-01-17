---
title: SQLBulkOperations 関数 |Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLBulkOperations
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLBulkOperations
helpviewer_keywords:
- SQLBulkOperations function [ODBC]
ms.assetid: 7029d0da-b0f2-44e6-9114-50bd96f47196
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 60bcb6851adeba08105dabd6fb0800d2e969a04e
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/19/2019
ms.locfileid: "68343175"
---
# <a name="sqlbulkoperations-function"></a>SQLBulkOperations 関数
**互換性**  
 導入されたバージョン:ODBC 3.0 標準準拠:ODBC  
  
 **まとめ**  
 **Sqlbulkoperations**では、更新、削除、およびブックマークによるフェッチを含む一括挿入操作と一括ブックマーク操作が実行されます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLBulkOperations(  
     SQLHSTMT       StatementHandle,  
     SQLUSMALLINT   Operation);  
```  
  
## <a name="arguments"></a>引数  
 *StatementHandle*  
 代入ステートメントハンドル。  
  
 *操作*  
 代入実行する操作:  
  
 SQL_ADD SQL_UPDATE_BY_BOOKMARK SQL_DELETE_BY_BOOKMARK SQL_FETCH_BY_BOOKMARK  
  
 詳細については、「コメント」を参照してください。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_NEED_DATA、SQL_STILL_EXECUTING、SQL_ERROR、または SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診断  
 **Sqlbulkoperations**が SQL_ERROR または SQL_SUCCESS_WITH_INFO を返すときは、SQL_HANDLE_STMT の*Handletype*と*StatementHandle*の*ハンドル*を指定して**SQLGetDiagRec**を呼び出すことによって、関連する SQLSTATE 値を取得できます. 次の表に、によって通常返される SQLSTATE 値**SQLBulkOperations**ですこの関数のコンテキストでは、各フォルダーについて説明しますと表記"(DM)"の前に、ドライバー マネージャーによって返される SQLSTATEs の説明。 特に記載がない限り、各 SQLSTATE 値に関連付けられているリターンコードは SQL_ERROR です。  
  
 SQL_SUCCESS_WITH_INFO または SQL_ERROR を返すことができるすべての SQLSTATEs (01xxx SQLSTATEs を除く) では、複数行操作のすべての行ではなく、1つ以上の行でエラーが発生すると SQL_SUCCESS_WITH_INFO が返され、エラーが発生した場合は SQL_ERROR が返されます。単一行演算。  
  
|SQLSTATE|[エラー]|説明|  
|--------------|-----------|-----------------|  
|01000|一般警告|ドライバー固有の情報メッセージ。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|01004|文字列データの右側の切り捨て|*操作*引数は SQL_FETCH_BY_BOOKMARK でしたが、データ型が SQL_C_CHAR または SQL_C_BINARY の列に対して返された文字列またはバイナリデータは、空白文字または NULL 以外のバイナリデータの切り捨てになりました。|  
|01S01|行にエラーがあります|*操作*の引数は SQL_ADD でしたが、操作の実行中に1つ以上の行でエラーが発生しましたが、少なくとも1つの行が正常に追加されました。 (関数は SQL_SUCCESS_WITH_INFO を返します)。<br /><br /> (このエラーは、アプリケーションが ODBC 2 で動作している場合にのみ発生します。*x*ドライバー。)|  
|01S07|小数部の切り捨て|*Operation*引数が SQL_FETCH_BY_BOOKMARK でした。アプリケーションバッファーのデータ型が SQL_C_CHAR または SQL_C_BINARY ではないか、または1つ以上の列のアプリケーションバッファーに返されたデータが切り捨てられました。 (数値 C データ型の場合、数値の小数部は切り捨てられました。 時間、タイムスタンプ、および期間の C データ型については、時間部分が含まれている場合、時間の小数部が切り捨てられました。<br /><br /> (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|07006|制限されたデータ型の属性違反|*操作*引数は SQL_FETCH_BY_BOOKMARK でしたが、結果セット内の列のデータ値を、 **SQLBindCol**への呼び出しの*TargetType*引数で指定されたデータ型に変換できませんでした。<br /><br /> *操作*引数が SQL_UPDATE_BY_BOOKMARK または SQL_ADD で、アプリケーションバッファー内のデータ値を結果セットの列のデータ型に変換できませんでした。|  
|07009|無効な記述子のインデックス|引数の*操作*が SQL_ADD ましたが、列の列数が結果セットの列の数を超えています。|  
|21S02|派生テーブルの次数が列の一覧と一致しません|引数*操作*は SQL_UPDATE_BY_BOOKMARK でした。また、すべての列がバインド解除されたか読み取り専用であったか、またはバインドされた長さ/インジケーターバッファーの値が SQL_COLUMN_IGNORE であったため、列は更新できませんでした。|  
|22001|文字列データの右側の切り捨て|結果セットの列に文字またはバイナリ値を代入すると、空白以外の文字 (文字の場合) または null 以外 (バイナリの場合) が切り捨てられます。|  
|22003|数値が有効範囲にありません|*操作*引数が SQL_ADD または SQL_UPDATE_BY_BOOKMARK で、結果セット内の列に数値を代入すると、切り捨てられる数値の一部 (小数部分ではなく) が発生しました。<br /><br /> 引数*操作*は SQL_FETCH_BY_BOOKMARK でしたが、1つ以上のバインドされた列の数値を返すと、有効桁数が失われた可能性があります。|  
|22007|無効な datetime 形式|*操作*引数が SQL_ADD または SQL_UPDATE_BY_BOOKMARK で、日付またはタイムスタンプの値が結果セットの列に割り当てられ、年、月、または日のフィールドが範囲外になっています。<br /><br /> 引数の*操作*が SQL_FETCH_BY_BOOKMARK ましたが、1つ以上のバインドされた列の日付またはタイムスタンプの値が返されたため、年、月、または日のフィールドが範囲外になっていました。|  
|22008|日付/時刻フィールドのオーバーフロー|*Operation*引数が SQL_ADD または SQL_UPDATE_BY_BOOKMARK で、結果セット内の列に送信されるデータに対する datetime 算術演算の結果により、結果の datetime フィールド (年、月、日、時、分、または2つ目のフィールド) が返されました。datetimes のグレゴリオ暦の自然なルールに基づいて、フィールドに許容される値の範囲外にあるか、無効になっています。<br /><br /> *操作*引数は SQL_FETCH_BY_BOOKMARK でしたが、結果セットから取得されるデータに対する datetime 算術演算のパフォーマンスが原因で、結果の datetime フィールド (年、月、日、時、分、または2番目のフィールド) がの外側にあります。datetimes のグレゴリオ暦の自然なルールに基づいて、フィールドに許容される値の範囲を指定するか、無効にします。|  
|22015|間隔フィールドオーバーフロー|*操作*引数が SQL_ADD または SQL_UPDATE_BY_BOOKMARK でしたが、正確な数値または期間 C 型を interval SQL データ型に割り当てているため、有効桁数が失われました。<br /><br /> *Operation*引数が SQL_ADD または SQL_UPDATE_BY_BOOKMARK でした。interval SQL 型にを割り当てる場合、interval SQL 型の C 型の値は表現されませんでした。<br /><br /> *操作*引数は SQL_FETCH_BY_BOOKMARK でしたが、完全な数値または期間の SQL 型から間隔 C 型に割り当てているため、先頭のフィールドの有効桁数が失われました。<br /><br /> *操作*引数は SQL_FETCH_BY_BOOKMARK でした。間隔 C 型にを割り当てる場合、interval C 型の SQL 型の値は表現されませんでした。|  
|22018|キャストの指定に無効な文字値があります|*操作*引数は SQL_FETCH_BY_BOOKMARK でした。C 型は、正確な数値、概数、datetime、または interval データ型でした。列の SQL 型は文字データ型でした。列の値が、バインドされた C 型の有効なリテラルではありませんでした。<br /><br /> 引数の*操作*が SQL_ADD または SQL_UPDATE_BY_BOOKMARK です。SQL 型は、正確な数値、概数、datetime、または interval データ型でした。C 型は SQL_C_CHAR です。列の値が、バインドされた SQL 型の有効なリテラルではありませんでした。|  
|23000|整合性制約違反|*操作*引数が SQL_ADD、SQL_DELETE_BY_BOOKMARK、または SQL_UPDATE_BY_BOOKMARK で、整合性制約に違反しました。<br /><br /> *操作*引数は SQL_ADD でしたが、バインドされていない列は not NULL として定義され、既定値はありません。<br /><br /> *操作*引数が SQL_ADD でした。バインドされた*StrLen_or_IndPtr*バッファーに指定された長さは SQL_COLUMN_IGNORE で、列には既定値がありませんでした。|  
|24000|カーソル状態が無効|*StatementHandle*は実行状態でしたが、結果セットが*StatementHandle*に関連付けられていませんでした。|  
|40001|シリアル化エラー|別のトランザクションでリソースのデッドロックが発生したため、トランザクションがロールバックされました。|  
|40003|ステートメントの完了が不明です|この関数の実行中に関連付けられた接続に失敗しました。トランザクションの状態を確認できません。|  
|42000|構文エラーまたはアクセス違反|*操作*引数で要求された操作を実行するために必要な行をドライバーがロックできませんでした。|  
|44000|WITH CHECK OPTION 違反|*Operation*引数が SQL_ADD または SQL_UPDATE_BY_BOOKMARK で、insert または UPDATE が、 **WITH CHECK OPTION**を指定して作成された、表示されているテーブル (または表示されているテーブルから派生したテーブル) に対して実行されました。このような方法では、1つ以上の行になります。挿入または更新の影響を受けるテーブルには表示されなくなります。|  
|HY000|一般エラー|特定の SQLSTATE がなく、実装固有の SQLSTATE が定義されていないエラーが発生しました。 Messagetext バッファーの**SQLGetDiagRec によっ**て返されるエラーメッセージには、エラーとその原因が記述されています。  *\**|  
|HY001|メモリ割り当てエラー|ドライバーは、関数の実行または完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY008|操作が取り消されました|*StatementHandle*に対して非同期処理が有効になりました。 関数が呼び出され、実行が完了する前に、 **SQLCancel**または**Sqlcancelhandle**が*StatementHandle*で呼び出されました。 次に、 *StatementHandle*で関数が再度呼び出されました。<br /><br /> 関数が呼び出され、実行が完了する前に、マルチスレッドアプリケーションの別のスレッドの*StatementHandle*で**SQLCancel**または**sqlcancelhandle**が呼び出されました。|  
|HY010|関数のシーケンスエラー|(DM) 非同期的に実行する関数が、 *StatementHandle*に関連付けられている接続ハンドルに対して呼び出されました。 この非同期関数は、 **Sqlbulkoperations**関数が呼び出されたときにまだ実行されていました。<br /><br /> (DM) **Sqlexecute**、 **SQLExecDirect**、または**Sqlmoreresults**が*STATEMENTHANDLE*に対して呼び出され、SQL_PARAM_DATA_AVAILABLE が返されました。 この関数は、ストリーミングされたすべてのパラメーターのデータが取得される前に呼び出されました。<br /><br /> (DM) 指定された*StatementHandle*は実行状態ではありませんでした。 最初に**SQLExecDirect**、 **sqlexecute**、またはカタログ関数を呼び出さずに関数が呼び出されました。<br /><br /> (DM) 非同期的に実行されている関数 (この1つではない) が*StatementHandle*に対して呼び出され、この関数が呼び出されたときにまだ実行されています。<br /><br /> (DM) **Sqlexecute**、 **SQLExecDirect**、または**SQLSetPos**が*STATEMENTHANDLE*に対して呼び出され、SQL_NEED_DATA が返されました。 この関数は、実行時データのすべてのパラメーターまたは列に対してデータが送信される前に呼び出されました。<br /><br /> (DM) ドライバーは ODBC 2 でした。**Sqlbulkoperations**または**sqlfetch**が呼び出される前に、 *StatementHandle*に対して*x*ドライバーおよび**sqlbulkoperations**が呼び出されました。<br /><br /> (DM) **Sqlbulkoperations**は、 *StatementHandle*で**SQLExtendedFetch**が呼び出された後に呼び出されました。|  
|HY011|属性を今設定することはできません|(DM) ドライバーは ODBC 2 でした。*x*ドライバーと SQL_ATTR_ROW_STATUS_PTR statement 属性が、 **sqlfetch**または**Sqlfetchscroll**と**sqlbulkoperations**の呼び出しの間に設定されました。|  
|HY013|メモリ管理エラー|基になるメモリオブジェクトにアクセスできなかったため、関数呼び出しを処理できませんでした。メモリ不足の状態が原因である可能性があります。|  
|HY090|文字列またはバッファーの長さが無効です|*Operation*引数が SQL_ADD または SQL_UPDATE_BY_BOOKMARK でした。データ値が null ポインターではありませんでした。C データ型は SQL_C_BINARY または SQL_C_CHAR です。列の長さの値が0未満で、SQL_DATA_AT_EXEC、SQL_COLUMN_IGNORE、SQL_NTS、SQL_NULL_DATA、または SQL_LEN_DATA_AT_EXEC_OFFSET 以下ではありませんでした。<br /><br /> 長さ/インジケーターバッファーの値は SQL_DATA_AT_EXEC でした。SQL 型は、SQL_LONGVARCHAR、SQL_LONGVARBINARY、または long データソース固有のデータ型のいずれかです。**SQLGetInfo**の SQL_NEED_LONG_DATA_LEN 情報型は "Y" でした。<br /><br /> *操作*引数が SQL_ADD で、SQL_ATTR_USE_BOOKMARK statement 属性が SQL_UB_VARIABLE に設定されました。列0は、この結果セットのブックマークの長さが最大値と等しくないバッファーにバインドされています。 (この長さは IRD の SQL_DESC_OCTET_LENGTH フィールドにあり、 **SQLDescribeCol**、 **sqlcolattribute**、または**SQLGetDescField**を呼び出すことによって取得できます)。|  
|HY092|無効な属性識別子|(DM)*操作*引数に指定された値が無効でした。<br /><br /> *操作*引数が SQL_ADD、SQL_UPDATE_BY_BOOKMARK、または SQL_DELETE_BY_BOOKMARK で、SQL_ATTR_CONCURRENCY statement 属性が SQL_CONCUR_READ_ONLY に設定されました。<br /><br /> *操作*引数が SQL_DELETE_BY_BOOKMARK、SQL_FETCH_BY_BOOKMARK、または SQL_UPDATE_BY_BOOKMARK で、BOOKMARK 列がバインドされていないか、SQL_ATTR_USE_BOOKMARKS statement 属性が SQL_UB_OFF に設定されています。|  
|HY117|トランザクションの状態が不明なため、接続が中断されました。 切断と読み取り専用の機能のみが許可されます。|(DM) 中断状態の詳細については、「 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)」を参照してください。|  
|HYC00|省略可能な機能は実装されていません|ドライバーまたはデータソースは、*操作*引数で要求された操作をサポートしていません。|  
|HYT00|タイムアウトが発生しました|データソースから結果セットが返される前に、クエリのタイムアウト期間が経過しました。 タイムアウト期間は、SQL_ATTR_QUERY_TIMEOUT の*属性*引数を使用して**SQLSetStmtAttr**によって設定されます。|  
|HYT01|接続タイムアウトの期限が切れました|データソースが要求に応答する前に、接続のタイムアウト期間が経過しました。 接続タイムアウト期間は、 **SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT によって設定されます。|  
|IM001|ドライバーはこの機能をサポートしていません|(DM) *StatementHandle*に関連付けられているドライバーでは、関数はサポートされていません。|  
|IM017|非同期通知モードでは、ポーリングは無効になっています|通知モデルが使用されるたびに、ポーリングは無効になります。|  
|IM018|**Sqlcompleteasync**は、このハンドルで前の非同期操作を完了するために呼び出されていません。|ハンドルに対する前の関数呼び出しで SQL_STILL_EXECUTING が返され、通知モードが有効になっている場合は、処理を完了するために、ハンドルで**Sqlcompleteasync**を呼び出して、操作を完了する必要があります。|  
  
## <a name="comments"></a>コメント  
  
> [!CAUTION]  
>  **Sqlbulkoperations**を呼び出すことができるステートメントの状態と、ODBC 2 との互換性を確保するために何を行う必要があるかについては、「」を参照してください。*x*アプリケーション、付録 G の[ブロックカーソル、スクロール可能なカーソル、および旧バージョンとの互換性](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md)に関するセクションを参照してください。旧バージョンとの互換性のためのドライバーガイドライン。  
  
 アプリケーションでは、 **Sqlbulkoperations**を使用して、現在のクエリに対応するベーステーブルまたはビューに対して次の操作を実行します。  
  
-   新しい行を追加します。  
  
-   各行がブックマークによって識別される行セットを更新します。  
  
-   各行がブックマークによって識別される行セットを削除します。  
  
-   各行がブックマークによって識別される行セットをフェッチします。  
  
 **Sqlbulkoperations**を呼び出した後、ブロックカーソルの位置は未定義です。 アプリケーションでは、カーソル位置を設定するために**Sqlfetchscroll**を呼び出す必要があります。 アプリケーションで**Sqlfetchscroll**を呼び出す必要があるのは、SQL_FETCH_FIRST、SQL_FETCH_LAST、SQL_FETCH_ABSOLUTE、または SQL_FETCH_BOOKMARK の*fetchorientation*引数を使用した場合のみです。 アプリケーションが SQL_FETCH_PRIOR、SQL_FETCH_NEXT、または SQL_FETCH_RELATIVE の*Fetchorientation*引数を使用して**Sqlfetch**または**sqlfetchscroll**を呼び出すと、カーソルの位置は未定義になります。  
  
 **SQLBindCol**への呼び出しで指定された列の長さ/インジケーターバッファーを SQL_COLUMN_IGNORE に設定することによって、 **sqlbulkoperations**の呼び出しによって実行される一括操作では、列を無視できます。  
  
 この関数で一括操作を実行するときに行を無視することはできないため、 **Sqlbulkoperations**を呼び出すときにアプリケーションで SQL_ATTR_ROW_OPERATION_PTR statement 属性を設定する必要はありません。  
  
 SQL_ATTR_ROWS_FETCHED_PTR statement 属性が指すバッファーには、 **Sqlbulkoperations**の呼び出しによって影響を受ける行の数が含まれます。  
  
 *操作*引数が SQL_ADD または SQL_UPDATE_BY_BOOKMARK で、カーソルに関連付けられているクエリ仕様の選択リストに同じ列への複数の参照が含まれている場合、エラーが生成されたか、またはドライバーは、重複する参照を無視し、要求された操作を実行します。  
  
 **Sqlbulkoperations**の使用方法の詳細については、「 [sqlbulkoperations によるデータの更新](../../../odbc/reference/develop-app/updating-data-with-sqlbulkoperations.md)」を参照してください。  
  
## <a name="performing-bulk-inserts"></a>一括挿入の実行  
 **Sqlbulkoperations**を使用してデータを挿入するために、アプリケーションは次の一連の手順を実行します。  
  
1.  結果セットを返すクエリを実行します。  
  
2.  SQL_ATTR_ROW_ARRAY_SIZE statement 属性を、挿入する行の数に設定します。  
  
3.  **SQLBindCol**を呼び出して、挿入するデータをバインドします。 データは、SQL_ATTR_ROW_ARRAY_SIZE の値と同じサイズの配列にバインドされます。  
  
    > [!NOTE]  
    >  SQL_ATTR_ROW_STATUS_PTR statement 属性が指す配列のサイズは、SQL_ATTR_ROW_ARRAY_SIZE または SQL_ATTR_ROW_STATUS_PTR が null ポインターである必要があります。  
  
4.  **Sqlbulkoperations**(*StatementHandle,* SQL_ADD) を呼び出して、挿入を実行します。  
  
5.  アプリケーションで SQL_ATTR_ROW_STATUS_PTR statement 属性が設定されている場合は、この配列を検査して操作の結果を確認できます。  
  
 SQL_ADD の*操作*引数を使用して**sqlbulkoperations**を呼び出す前に、アプリケーションが列0をバインドした場合、ドライバーは、新しく挿入された行のブックマーク値を使用して、バインドされた列0バッファーを更新します。 これを行うには、ステートメントを実行する前に、アプリケーションで SQL_ATTR_USE_BOOKMARKS statement 属性を SQL_UB_VARIABLE に設定しておく必要があります。 (ODBC 2 では使用できません。*x*ドライバー。)  
  
 SQLBulkOperations および Sqlbulkoperations の呼び出しを使用して、SQLBulkOperations によって部分的に長いデータを追加できます。 詳細については、この関数リファレンスで後ほど説明する「一括挿入と更新に長いデータを提供する」を参照してください。  
  
 **Sqlbulkoperations**を呼び出す前に、アプリケーションが Sqlfetch または**sqlfetchscroll**を呼び出す必要はありません (ODBC 2 に対して実行する場合を除く)。*x*ドライバー;「[下位互換性と標準への準拠」を](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)参照してください)。  
  
 *操作*の引数が SQL_ADD の**sqlbulkoperations**が、重複する列を含むカーソルで呼び出される場合、この動作はドライバーによって定義されます。 ドライバーが定義した SQLSTATE を返したり、結果セットに表示される最初の列にデータを追加したり、ドライバー定義のその他の動作を実行したりすることができます。  
  
## <a name="performing-bulk-updates-by-using-bookmarks"></a>ブックマークを使用した一括更新の実行  
 **Sqlbulkoperations**でブックマークを使用して一括更新を実行する場合、アプリケーションは次の手順を順番に実行します。  
  
1.  SQL_ATTR_USE_BOOKMARKS statement 属性を SQL_UB_VARIABLE に設定します。  
  
2.  結果セットを返すクエリを実行します。  
  
3.  SQL_ATTR_ROW_ARRAY_SIZE statement 属性を、更新する行の数に設定します。  
  
4.  **SQLBindCol**を呼び出して、更新するデータをバインドします。 データは、SQL_ATTR_ROW_ARRAY_SIZE の値と同じサイズの配列にバインドされます。 また、 **SQLBindCol**を呼び出して、列 0 (ブックマーク列) をバインドします。  
  
5.  更新対象の行のブックマークを、列0にバインドされた配列にコピーします。  
  
6.  バインドされたバッファー内のデータを更新します。  
  
    > [!NOTE]  
    >  SQL_ATTR_ROW_STATUS_PTR statement 属性が指す配列のサイズは、SQL_ATTR_ROW_ARRAY_SIZE または SQL_ATTR_ROW_STATUS_PTR が null ポインターである必要があります。  
  
7.  **Sqlbulkoperations**(*StatementHandle,* SQL_UPDATE_BY_BOOKMARK) を呼び出します。  
  
    > [!NOTE]  
    >  アプリケーションで SQL_ATTR_ROW_STATUS_PTR statement 属性が設定されている場合は、この配列を検査して操作の結果を確認できます。  
  
8.  必要に応じて、 **Sqlbulkoperations**(*StatementHandle*, SQL_FETCH_BY_BOOKMARK) を呼び出して、バインドされたアプリケーションバッファーにデータをフェッチし、更新が発生したことを確認します。  
  
9. データが更新されている場合、ドライバーは行の状態配列の値を変更して、適切な行を SQL_ROW_UPDATED に変更します。  
  
 **Sqlbulkoperations**によって実行される一括更新には、 **sqlbulkoperations**および**sqlbulkoperations**の呼び出しを使用して長いデータを含めることができます。 詳細については、この関数リファレンスで後ほど説明する「一括挿入と更新に長いデータを提供する」を参照してください。  
  
 複数のカーソルにまたがってブックマークが保持される場合、アプリケーションは、ブックマークによって更新する前に**sqlfetch**または**sqlfetchscroll**を呼び出す必要はありません。 前のカーソルから格納されているブックマークを使用できます。 ブックマークが複数のカーソルにまたがって保持されていない場合、アプリケーションは**Sqlfetch**または**sqlfetchscroll**を呼び出してブックマークを取得する必要があります。  
  
 *操作*の引数が SQL_UPDATE_BY_BOOKMARK の**sqlbulkoperations**が、重複する列を含むカーソルで呼び出される場合、この動作はドライバーによって定義されます。 ドライバーによって定義された SQLSTATE を返したり、結果セットに表示される最初の列を更新したり、ドライバー定義のその他の動作を実行したりすることができます。  
  
## <a name="performing-bulk-fetches-using-bookmarks"></a>ブックマークを使用した一括フェッチの実行  
 **Sqlbulkoperations**でブックマークを使用して一括フェッチを実行する場合、アプリケーションは次の手順を順番に実行します。  
  
1.  SQL_ATTR_USE_BOOKMARKS statement 属性を SQL_UB_VARIABLE に設定します。  
  
2.  結果セットを返すクエリを実行します。  
  
3.  SQL_ATTR_ROW_ARRAY_SIZE statement 属性を、フェッチする行の数に設定します。  
  
4.  **SQLBindCol**を呼び出して、フェッチするデータをバインドします。 データは、SQL_ATTR_ROW_ARRAY_SIZE の値と同じサイズの配列にバインドされます。 また、 **SQLBindCol**を呼び出して、列 0 (ブックマーク列) をバインドします。  
  
5.  列0にバインドされた配列へのフェッチに関心のある行のブックマークをコピーします。 (これは、アプリケーションが既にブックマークを取得していることを前提としています)。  
  
    > [!NOTE]  
    >  SQL_ATTR_ROW_STATUS_PTR statement 属性が指す配列のサイズは、SQL_ATTR_ROW_ARRAY_SIZE または SQL_ATTR_ROW_STATUS_PTR が null ポインターである必要があります。  
  
6.  **Sqlbulkoperations**(*StatementHandle,* SQL_FETCH_BY_BOOKMARK) を呼び出します。  
  
7.  アプリケーションで SQL_ATTR_ROW_STATUS_PTR statement 属性が設定されている場合は、この配列を検査して操作の結果を確認できます。  
  
 複数のカーソルにまたがってブックマークが保持される場合、アプリケーションは、ブックマークによってフェッチする前に**sqlfetch**または**sqlfetchscroll**を呼び出す必要はありません。 前のカーソルから格納されているブックマークを使用できます。 ブックマークが複数のカーソルにまたがって保持されていない場合、アプリケーションは、ブックマークを取得するために、 **Sqlfetch**または**sqlfetchscroll**を1回呼び出す必要があります。  
  
## <a name="performing-bulk-deletes-using-bookmarks"></a>ブックマークを使用した一括削除の実行  
 **Sqlbulkoperations**でブックマークを使用して一括削除を実行する場合、アプリケーションは次の手順を順番に実行します。  
  
1.  SQL_ATTR_USE_BOOKMARKS statement 属性を SQL_UB_VARIABLE に設定します。  
  
2.  結果セットを返すクエリを実行します。  
  
3.  SQL_ATTR_ROW_ARRAY_SIZE statement 属性を、削除する行の数に設定します。  
  
4.  **SQLBindCol**を呼び出して、列 0 (ブックマーク列) をバインドします。  
  
5.  削除する対象の行のブックマークを、列0にバインドされた配列にコピーします。  
  
    > [!NOTE]  
    >  SQL_ATTR_ROW_STATUS_PTR statement 属性が指す配列のサイズは、SQL_ATTR_ROW_ARRAY_SIZE または SQL_ATTR_ROW_STATUS_PTR が null ポインターである必要があります。  
  
6.  **Sqlbulkoperations**(*StatementHandle,* SQL_DELETE_BY_BOOKMARK) を呼び出します。  
  
7.  アプリケーションで SQL_ATTR_ROW_STATUS_PTR statement 属性が設定されている場合は、この配列を検査して操作の結果を確認できます。  
  
 複数のカーソルにまたがってブックマークが保持される場合、アプリケーションは、ブックマークによって削除する前に**sqlfetch**または**sqlfetchscroll**を呼び出す必要はありません。 前のカーソルから格納されているブックマークを使用できます。 ブックマークが複数のカーソルにまたがって保持されていない場合、アプリケーションは、ブックマークを取得するために、 **Sqlfetch**または**sqlfetchscroll**を1回呼び出す必要があります。  
  
## <a name="providing-long-data-for-bulk-inserts-and-updates"></a>一括挿入と更新に長いデータを提供する  
 **Sqlbulkoperations**を呼び出すことによって実行される一括挿入および更新のために、長いデータを提供できます。 長いデータを挿入または更新するには、このトピックの「一括挿入の実行」と「ブックマークを使用した一括更新の実行」で説明されている手順に加えて、アプリケーションは次の手順を実行します。  
  
1.  **SQLBindCol**を使用してデータをバインドする場合、アプリケーションでは、実行時データ列の *\*targetvalueptr*バッファーに、列番号などのアプリケーション定義の値が配置されます。 この値は、後で列を識別するために使用できます。  
  
     アプリケーションによって、SQL_LEN_DATA_AT_EXEC (*length*) マクロの結果が *\*StrLen_or_IndPtr*バッファーに配置されます。 列の SQL データ型が SQL_LONGVARBINARY、SQL_LONGVARCHAR、または long data source 固有のデータ型で、ドライバーが**SQLGetInfo**の SQL_NEED_LONG_DATA_LEN information 型に対して "Y" を返す場合、 *length*はデータのバイト数です。パラメーターに対して送信されます。それ以外の場合は、負でない値である必要があり、無視されます。  
  
2.  **Sqlbulkoperations**が呼び出されると、実行時データ列がある場合、関数は SQL_NEED_DATA を返し、次の手順3に進みます。 (実行時データ列がない場合、プロセスは完了です)。  
  
3.  アプリケーションは**sqlparamdata**を呼び出して、処理する最初の実行時データ列の *\*targetvalueptr*バッファーのアドレスを取得します。 **Sqlparamdata**は SQL_NEED_DATA を返します。 アプリケーションは、  *\*targetvalueptr*バッファーからアプリケーション定義の値を取得します。  
  
    > [!NOTE]  
    >  実行時データパラメーターは実行時データ列に似ていますが、 **Sqlparamdata**によって返される値はそれぞれ異なっています。  
  
     実行時データ列は、行が更新されたとき、または**Sqlputdata**で挿入されたときに**sqlputdata**と共にデータが送信される行セット内の列です。 これらは**SQLBindCol**にバインドされています。 **Sqlparamdata**によって返される値は、処理される **targetvalueptr*バッファー内の行のアドレスです。  
  
4.  アプリケーションは**Sqlputdata**を1回以上呼び出して、列のデータを送信します。 **Sqlputdata**に指定された *\*targetvalueptr*バッファーにすべてのデータ値を返すことができない場合は、複数の呼び出しが必要です。同じ列に対して複数の**sqlputdata**を呼び出すことは、文字 C データを送信するときにのみ許可されます。文字、バイナリ、またはデータソース固有のデータ型の列、または文字、バイナリ、またはデータソース固有のデータ型を持つ列にバイナリ C データを送信する場合。  
  
5.  アプリケーションは**Sqlparamdata**を再度呼び出して、すべてのデータが列に送信されたことを通知します。  
  
    -   実行時データ列の数が多い場合、 **Sqlparamdata**は SQL_NEED_DATA を返し、処理する次の実行時データ列の*targetvalueptr*バッファーのアドレスを返します。 アプリケーションは、手順4と5を繰り返します。  
  
    -   実行時データ列がない場合は、プロセスが完了します。 ステートメントが正常に実行された場合、 **Sqlparamdata**は SQL_SUCCESS または SQL_SUCCESS_WITH_INFO を返します。実行が失敗した場合は、SQL_ERROR を返します。 この時点で、 **Sqlparamdata**は**sqlparamdata**によって返されるすべての SQLSTATE を返すことができます。  
  
 操作が取り消された場合、または Sqlparamdata**また**は**sqlparamdata**で**sqlparamdata**が SQL_NEED_DATA を返した後にエラーが発生した場合、実行中のすべてのデータ列に対してデータが送信される前に、アプリケーションは SQLCancel のみを呼び出すことができます。 ステートメントまたはステートメントに関連付けられている接続の場合は、、 **SQLGetDiagField**、 **SQLGetDiagRec**、 **sqlgetfunctions**、 **sqlgetfunctions**、または**sqlgetfunctions**を使用します。 ステートメントまたはステートメントに関連付けられている接続に対して他の関数を呼び出すと、関数は SQL_ERROR と SQLSTATE HY010 (関数シーケンスエラー) を返します。  
  
 アプリケーションが**SQLCancel**を呼び出しても、ドライバーが実行時データ列のデータを必要としている場合、ドライバーは操作をキャンセルします。 その後、アプリケーションは**Sqlbulkoperations**を再度呼び出すことができます。取り消すと、カーソルの状態または現在のカーソル位置には影響しません。  
  
## <a name="row-status-array"></a>行の状態の配列  
 行の状態の配列には、 **Sqlbulkoperations**の呼び出し後に行セット内のデータ行ごとに状態値が格納されます。 ドライバーは、 **Sqlfetch**、 **sqlfetchscroll**、 **SQLSetPos**、または**sqlbulkoperations**の呼び出し後に、この配列の状態値を設定します。 **Sqlbulkoperations**の前に sqlfetch または **sqlbulkoperations**が呼び出されていない場合、この配列には、sqlbulkoperations の呼び出しが最初に設定されます。 この配列は、SQL_ATTR_ROW_STATUS_PTR statement 属性によってポイントされます。 行ステータス配列内の要素の数は、SQL_ATTR_ROW_ARRAY_SIZE statement 属性で定義されているように、行セット内の行数と同じである必要があります。 この行の状態の配列の詳細については、「 [Sqlfetch](../../../odbc/reference/syntax/sqlfetch-function.md)」を参照してください。  
  
## <a name="code-example"></a>コード例  
 次の例では、一度に10行のデータを Customers テーブルからフェッチします。 次に、実行する操作をユーザーに求めるメッセージが表示されます。 ネットワークトラフィックを減らすために、この例では、バインドされた配列にローカルに更新、削除、および挿入を行いますが、行セットデータを超えたオフセットを使用します。 ユーザーが更新、削除、および挿入をデータソースに送信することを選択すると、コードはバインドオフセットを適切に設定し、 **Sqlbulkoperations**を呼び出します。 わかりやすくするために、ユーザーは10を超える更新、削除、または挿入をバッファリングできません。  
  
```cpp  
// SQLBulkOperations_Function.cpp  
// compile with: ODBC32.lib  
#include <windows.h>  
#include <sqlext.h>  
#include "stdio.h"  
  
#define UPDATE_ROW 100  
#define DELETE_ROW 101  
#define ADD_ROW 102  
#define SEND_TO_DATA_SOURCE 103  
#define UPDATE_OFFSET 10  
#define INSERT_OFFSET 20  
#define DELETE_OFFSET 30  
  
// Define structure for customer data (assume 10 byte maximum bookmark size).  
typedef struct tagCustStruct {  
   SQLCHAR Bookmark[10];  
   SQLINTEGER BookmarkLen;  
   SQLUINTEGER CustomerID;  
   SQLINTEGER CustIDInd;  
   SQLCHAR CompanyName[51];  
   SQLINTEGER NameLenOrInd;  
   SQLCHAR Address[51];  
   SQLINTEGER AddressLenOrInd;  
   SQLCHAR Phone[11];  
   SQLINTEGER PhoneLenOrInd;  
} CustStruct;  
  
// Allocate 40 of these structures. Elements 0-9 are for the current rowset,  
// elements 10-19 are for the buffered updates, elements 20-29 are for  
// the buffered inserts, and elements 30-39 are for the buffered deletes.  
CustStruct CustArray[40];  
SQLUSMALLINT RowStatusArray[10], Action, RowNum, NumUpdates = 0, NumInserts = 0,  
NumDeletes = 0;  
SQLLEN BindOffset = 0;  
SQLRETURN retcode;  
SQLHENV henv = NULL;  
SQLHDBC hdbc = NULL;  
SQLHSTMT hstmt = NULL;  
  
int main() {  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
   retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER*)SQL_OV_ODBC3, 0);   
  
   retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);   
   retcode = SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
  
   retcode = SQLConnect(hdbc, (SQLCHAR*) "Northwind", SQL_NTS, (SQLCHAR*) NULL, 0, NULL, 0);  
   retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
  
   // Set the following statement attributes:  
   // SQL_ATTR_CURSOR_TYPE:           Keyset-driven  
   // SQL_ATTR_ROW_BIND_TYPE:         Row-wise  
   // SQL_ATTR_ROW_ARRAY_SIZE:        10  
   // SQL_ATTR_USE_BOOKMARKS:         Use variable-length bookmarks  
   // SQL_ATTR_ROW_STATUS_PTR:        Points to RowStatusArray  
   // SQL_ATTR_ROW_BIND_OFFSET_PTR:   Points to BindOffset  
   retcode = SQLSetStmtAttr(hstmt, SQL_ATTR_CURSOR_TYPE, (SQLPOINTER)SQL_CURSOR_KEYSET_DRIVEN, 0);  
   retcode = SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_BIND_TYPE, (SQLPOINTER)sizeof(CustStruct), 0);  
   retcode = SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_ARRAY_SIZE, (SQLPOINTER)10, 0);  
   retcode = SQLSetStmtAttr(hstmt, SQL_ATTR_USE_BOOKMARKS, (SQLPOINTER)SQL_UB_VARIABLE, 0);  
   retcode = SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_STATUS_PTR, RowStatusArray, 0);  
   retcode = SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_BIND_OFFSET_PTR, &BindOffset, 0);  
  
   // Bind arrays to the bookmark, CustomerID, CompanyName, Address, and Phone columns.  
   retcode = SQLBindCol(hstmt, 0, SQL_C_VARBOOKMARK, CustArray[0].Bookmark, sizeof(CustArray[0].Bookmark), &CustArray[0].BookmarkLen);  
   retcode = SQLBindCol(hstmt, 1, SQL_C_ULONG, &CustArray[0].CustomerID, 0, &CustArray[0].CustIDInd);  
   retcode = SQLBindCol(hstmt, 2, SQL_C_CHAR, CustArray[0].CompanyName, sizeof(CustArray[0].CompanyName), &CustArray[0].NameLenOrInd);  
   retcode = SQLBindCol(hstmt, 3, SQL_C_CHAR, CustArray[0].Address, sizeof(CustArray[0].Address), &CustArray[0].AddressLenOrInd);  
   retcode = SQLBindCol(hstmt, 4, SQL_C_CHAR, CustArray[0].Phone, sizeof(CustArray[0].Phone), &CustArray[0].PhoneLenOrInd);  
  
   // Execute a statement to retrieve rows from the Customers table.  
   retcode = SQLExecDirect(hstmt, (SQLCHAR*)"SELECT CustomerID, CompanyName, Address, Phone FROM Customers", SQL_NTS);  
  
   // Fetch and display the first 10 rows.  
   retcode = SQLFetchScroll(hstmt, SQL_FETCH_NEXT, 0);  
   // DisplayCustData(CustArray, 10);  
  
   // Call GetAction to get an action and a row number from the user.  
   // while (GetAction(&Action, &RowNum)) {  
   Action = SQL_FETCH_NEXT;  
   RowNum = 2;  
   switch (Action) {  
      case SQL_FETCH_NEXT:  
      case SQL_FETCH_PRIOR:  
      case SQL_FETCH_FIRST:  
      case SQL_FETCH_LAST:  
      case SQL_FETCH_ABSOLUTE:  
      case SQL_FETCH_RELATIVE:  
         // Fetch and display the requested data.  
         SQLFetchScroll(hstmt, Action, RowNum);  
         // DisplayCustData(CustArray, 10);  
         break;  
  
      case UPDATE_ROW:  
         // Check if we have reached the maximum number of buffered updates.  
         if (NumUpdates < 10) {  
            // Get the new customer data and place it in the next available element of  
            // the buffered updates section of CustArray, copy the bookmark of the row  
            // being updated to the same element, and increment the update counter.  
            // Checking to see we have not already buffered an update for this  
            // row not shown.  
            // GetNewCustData(CustArray, UPDATE_OFFSET + NumUpdates);  
            memcpy(CustArray[UPDATE_OFFSET + NumUpdates].Bookmark,  
               CustArray[RowNum - 1].Bookmark,  
               CustArray[RowNum - 1].BookmarkLen);  
            CustArray[UPDATE_OFFSET + NumUpdates].BookmarkLen =  
               CustArray[RowNum - 1].BookmarkLen;  
            NumUpdates++;  
         } else {  
            printf("Buffers full. Send buffered changes to the data source.");  
         }  
         break;  
      case DELETE_ROW:  
         // Check if we have reached the maximum number of buffered deletes.  
         if (NumDeletes < 10) {  
            // Copy the bookmark of the row being deleted to the next available element  
            // of the buffered deletes section of CustArray and increment the delete  
            // counter. Checking to see we have not already buffered an update for  
            // this row not shown.  
            memcpy(CustArray[DELETE_OFFSET + NumDeletes].Bookmark,  
               CustArray[RowNum - 1].Bookmark,  
               CustArray[RowNum - 1].BookmarkLen);  
  
            CustArray[DELETE_OFFSET + NumDeletes].BookmarkLen =  
               CustArray[RowNum - 1].BookmarkLen;  
  
            NumDeletes++;  
         } else  
            printf("Buffers full. Send buffered changes to the data source.");  
         break;  
  
      case ADD_ROW:  
         // reached maximum number of buffered inserts?  
         if (NumInserts < 10) {  
            // Get the new customer data and place it in the next available element of  
            // the buffered inserts section of CustArray and increment insert counter.  
            // GetNewCustData(CustArray, INSERT_OFFSET + NumInserts);  
            NumInserts++;  
         } else  
            printf("Buffers full. Send buffered changes to the data source.");  
         break;  
  
      case SEND_TO_DATA_SOURCE:  
         // If there are any buffered updates, inserts, or deletes, set the array size  
         // to that number, set the binding offset to use the data in the buffered  
         // update, insert, or delete part of CustArray, and call SQLBulkOperations to  
         // do the updates, inserts, or deletes. Because we will never have more than  
         // 10 updates, inserts, or deletes, we can use the same row status array.  
         if (NumUpdates) {  
            SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_ARRAY_SIZE, (SQLPOINTER)NumUpdates, 0);  
            BindOffset = UPDATE_OFFSET * sizeof(CustStruct);  
            SQLBulkOperations(hstmt, SQL_UPDATE_BY_BOOKMARK);  
            NumUpdates = 0;  
         }  
  
         if (NumInserts) {  
            SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_ARRAY_SIZE, (SQLPOINTER)NumInserts, 0);  
            BindOffset = INSERT_OFFSET * sizeof(CustStruct);  
            SQLBulkOperations(hstmt, SQL_ADD);  
            NumInserts = 0;  
         }  
  
         if (NumDeletes) {  
            SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_ARRAY_SIZE, (SQLPOINTER)NumDeletes, 0);  
            BindOffset = DELETE_OFFSET * sizeof(CustStruct);  
            SQLBulkOperations(hstmt, SQL_DELETE_BY_BOOKMARK);  
            NumDeletes = 0;  
         }  
  
         // If there were any updates, inserts, or deletes, reset the binding offset  
         // and array size to their original values.  
         if (NumUpdates || NumInserts || NumDeletes) {  
            SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_ARRAY_SIZE, (SQLPOINTER)10, 0);  
            BindOffset = 0;  
         }  
         break;  
   }  
   // }  
  
   // Close the cursor.  
   SQLFreeStmt(hstmt, SQL_CLOSE);  
}  
```  
  
## <a name="related-functions"></a>関連する関数  
  
|詳細|参照先|  
|---------------------------|---------|  
|結果セット内の列へのバッファーのバインド|[SQLBindCol 関数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|ステートメント処理の取り消し|[SQLCancel 関数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|データのブロックのフェッチまたは結果セットのスクロール|[SQLFetchScroll 関数](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|記述子の1つのフィールドを取得する|[SQLGetDescField 関数](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|記述子の複数のフィールドを取得する|[SQLGetDescRec 関数](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|記述子の1つのフィールドの設定|[SQLSetDescField 関数](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|記述子の複数のフィールドの設定|[SQLSetDescRec 関数](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
|カーソルの配置、行セット内のデータの更新、または行セット内のデータの更新または削除|[SQLSetPos 関数](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
|ステートメント属性の設定|[SQLSetStmtAttr 関数](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>参照  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)
