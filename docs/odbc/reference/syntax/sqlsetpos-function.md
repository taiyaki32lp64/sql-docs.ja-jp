---
title: SQLSetPos 関数 |Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSetPos
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLSetPos
helpviewer_keywords:
- SQLSetPos function [ODBC]
ms.assetid: 80190ee7-ae3b-45e5-92a9-693eb558f322
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 80f14b99d2c7dac91116186fdcf53ff77ee6c2c0
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/19/2019
ms.locfileid: "68343065"
---
# <a name="sqlsetpos-function"></a>SQLSetPos 関数
**互換性**  
 導入されたバージョン:ODBC 1.0 標準準拠:ODBC  
  
 **まとめ**  
 **SQLSetPos**は、行セット内のカーソル位置を設定し、アプリケーションが行セット内のデータを更新したり、結果セット内のデータを更新または削除したりできるようにします。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLSetPos(  
      SQLHSTMT        StatementHandle,  
      SQLSETPOSIROW   RowNumber,  
      SQLUSMALLINT    Operation,  
      SQLUSMALLINT    LockType);  
```  
  
## <a name="arguments"></a>引数  
 *StatementHandle*  
 代入ステートメントハンドル。  
  
 *RowNumber*  
 代入*操作*引数で指定された操作を実行する行セット内の行の位置。 *RowNumber*が0の場合、操作は行セットのすべての行に適用されます。  
  
 詳細については、「コメント」を参照してください。  
  
 *操作*  
 代入実行する操作:  
  
 SQL_POSITION SQL_REFRESH SQL_UPDATE SQL_DELETE  
  
> [!NOTE]
>  *Operation*引数の SQL_ADD 値は *、ODBC 3.x*では非推奨とされました。 ODBC *3.x*ドライバーは、旧バージョンとの互換性のために SQL_ADD をサポートする必要があります。 この機能は、SQL_ADD*操作*を使用した**sqlbulkoperations**の呼び出しに置き換えられました。 Odbc *2.x アプリケーションが*odbc *2.x ドライバーで*動作する場合、ドライバーマネージャーは、SQL_ADD の*操作*によって、SQL_ADD の*操作*で**sqlbulkoperations**への呼び出しを**SQLSetPos**にマップします。  
  
 詳細については、「コメント」を参照してください。  
  
 *LockType*  
 代入*操作*引数で指定された操作を実行した後に、行をロックする方法を指定します。  
  
 SQL_LOCK_NO_CHANGE SQL_LOCK_EXCLUSIVE SQL_LOCK_UNLOCK  
  
 詳細については、「コメント」を参照してください。  
  
 **型**  
  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_NEED_DATA、SQL_STILL_EXECUTING、SQL_ERROR、または SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診断  
 **SQLSetPos**が SQL_ERROR または SQL_SUCCESS_WITH_INFO を返す場合、SQL_HANDLE_STMT の*Handletype*と*StatementHandle*の*ハンドル*を指定して**SQLGetDiagRec**を呼び出すことによって、関連する SQLSTATE 値を取得できます。 次の表に、 **SQLSetPos**によって一般的に返される SQLSTATE 値を示し、この関数のコンテキストでそれぞれについて説明します。"(DM)" という表記は、ドライバーマネージャーによって返される SQLSTATEs の説明の前にあります。 特に記載がない限り、各 SQLSTATE 値に関連付けられているリターンコードは SQL_ERROR です。  
  
 SQL_SUCCESS_WITH_INFO または SQL_ERROR を返すことができるすべての SQLSTATEs (01xxx SQLSTATEs を除く) では、複数行操作のすべての行ではなく、1つ以上の行でエラーが発生すると SQL_SUCCESS_WITH_INFO が返され、エラーが発生した場合は SQL_ERROR が返されます。単一行演算。  
  
|SQLSTATE|[エラー]|説明|  
|--------------|-----------|-----------------|  
|01000|一般警告|ドライバー固有の情報メッセージ。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|01001|カーソル操作の競合|*操作*引数が SQL_DELETE または SQL_UPDATE で、行または複数の行が削除または更新されていません。 (複数の行の更新の詳細については、 **SQLSetStmtAttr**の SQL_ATTR_SIMULATE_CURSOR*属性*の説明を参照してください。)(関数は SQL_SUCCESS_WITH_INFO を返します)。<br /><br /> *操作*引数が SQL_DELETE または SQL_UPDATE で、オプティミスティック同時実行制御のため、操作に失敗しました。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|01004|文字列データの右側の切り捨て|*操作*引数は SQL_REFRESH でしたが、データ型が SQL_C_CHAR または SQL_C_BINARY の列に対して返された文字列またはバイナリデータは、空白文字または NULL 以外のバイナリデータの切り捨てになりました。|  
|01S01|行にエラーがあります|*RowNumber*引数が0で、*操作*引数で指定された操作の実行中に1つ以上の行でエラーが発生しました。<br /><br /> (SQL_SUCCESS_WITH_INFO は、1行の操作でエラーが発生した場合に、複数行の操作のすべての行ではなく、1つ以上の行でエラーが発生した場合に返されます。<br /><br /> (この SQLSTATE は、ドライバー*が ODBC 2.x*ドライバーであり、カーソルライブラリが使用されていない場合に、 **SQLExtendedFetch**の後に**SQLSetPos**が呼び出されたときにのみ返されます)。|  
|01S07|小数部の切り捨て|*Operation*引数が SQL_REFRESH でした。アプリケーションバッファーのデータ型が SQL_C_CHAR または SQL_C_BINARY ではないか、または1つ以上の列のアプリケーションバッファーに返されたデータが切り捨てられました。 数値データ型の場合、数値の小数部は切り捨てられました。 時間、タイムスタンプ、および期間のデータ型については、時刻の部分が切り捨てられました。<br /><br /> (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|07006|制限されたデータ型の属性違反|結果セットの列のデータ値を、 **SQLBindCol**の呼び出しで*TargetType*によって指定されたデータ型に変換できませんでした。|  
|07009|無効な記述子のインデックス|引数の*操作*が SQL_REFRESH または SQL_UPDATE で、列の列数が結果セットの列の数を超えています。|  
|21S02|派生テーブルの次数が列の一覧と一致しません|引数*操作*は SQL_UPDATE でしたが、列が更新可能ではありませんでした。すべての列がバインド解除されたか、読み取り専用であったか、またはバインドされた長さ/インジケーターバッファーの値が SQL_COLUMN_IGNORE でした。|  
|22001|文字列データ、右切り捨て|*操作*引数が SQL_UPDATE ましたが、列への文字またはバイナリ値の割り当てにより、空白以外の文字 (文字の場合) または null 以外 (バイナリ) の文字またはバイトが切り捨てられました。|  
|22003|数値が有効範囲にありません|引数*操作*は SQL_UPDATE でしたが、結果セット内の列に数値を割り当てると、切り捨てられる数値の一部 (小数部分ではなく) が発生しました。<br /><br /> 引数*操作*は SQL_REFRESH でしたが、1つ以上のバインドされた列の数値を返すと、有効桁数が失われた可能性があります。|  
|22007|無効な datetime 形式|引数の*操作*が SQL_UPDATE ましたが、日付またはタイムスタンプの値が結果セットの列に割り当てられ、年、月、または日のフィールドが範囲外になっています。<br /><br /> 引数の*操作*が SQL_REFRESH ましたが、1つ以上のバインドされた列の日付またはタイムスタンプの値が返されたため、年、月、または日のフィールドが範囲外になっていました。|  
|22008|日付/時刻フィールドのオーバーフロー|*操作*引数は SQL_UPDATE でしたが、結果セット内の列に送信されるデータに対する datetime 算術演算のパフォーマンスが原因で、結果が許容範囲外になったことを表す datetime フィールド (年、月、日、時、分、または2番目のフィールド) が返されました。フィールドの値の範囲です。または、グレゴリオ暦の datetimes の自然な規則に基づいて無効になっています。<br /><br /> *操作*引数は SQL_REFRESH でしたが、結果セットから取得されるデータに対する datetime 算術演算のパフォーマンスにより、結果が許容範囲外であることを表す datetime フィールド (年、月、日、時、分、または2番目のフィールド) が返されました。フィールドの値の範囲です。または、グレゴリオ暦の datetimes の自然な規則に基づいて無効になっています。|  
|22015|間隔フィールドオーバーフロー|*操作*引数は SQL_UPDATE でしたが、真数または interval C 型を interval SQL データ型に割り当てた結果、有効桁数が失われました。<br /><br /> *操作*引数は SQL_UPDATE でした。interval SQL 型にを割り当てる場合、interval SQL 型の C 型の値は表現されませんでした。<br /><br /> *操作*引数は SQL_REFRESH でしたが、完全な数値または期間の SQL 型から間隔 C 型に割り当てているため、先頭のフィールドの有効桁数が失われました。<br /><br /> *Operation*引数が SQL_ REFRESH でした。間隔 C 型にを割り当てる場合、interval C 型の SQL 型の値は表現されませんでした。|  
|22018|キャストの指定に無効な文字値があります|*操作*引数は SQL_REFRESH でした。C 型は、正確な数値、概数、datetime、または interval データ型でした。列の SQL 型は文字データ型でした。列の値が、バインドされた C 型の有効なリテラルではありませんでした。<br /><br /> 引数*操作*は SQL_UPDATE でした。SQL 型は、正確な数値、概数、datetime、または interval データ型でした。C 型は SQL_C_CHAR です。列の値が、バインドされた SQL 型の有効なリテラルではありませんでした。|  
|23000|整合性制約違反|引数の*操作*が SQL_DELETE または SQL_UPDATE で、整合性の制約に違反しました。|  
|24000|カーソル状態が無効|*StatementHandle*は実行状態でしたが、結果セットが*StatementHandle*に関連付けられていませんでした。<br /><br /> (DM) *StatementHandle*でカーソルが開いていましたが、 **sqlfetch**または**sqlfetchscroll**は呼び出されませんでした。<br /><br /> *StatementHandle*でカーソルが開かれましたが、 **Sqlfetch**または**sqlfetchscroll**が呼び出されましたが、カーソルが結果セットの先頭より前、または結果セットの末尾の後に配置されました。<br /><br /> 引数の*操作*が SQL_DELETE、SQL_REFRESH、または SQL_UPDATE で、カーソルが結果セットの先頭の前、または結果セットの末尾の後に配置されました。|  
|40001|シリアル化エラー|リソースが別のトランザクションでデッドロックしているため、トランザクションがロールバックされました。|  
|40003|ステートメントの完了が不明です|この関数の実行中に関連付けられた接続に失敗しました。トランザクションの状態を確認できません。|  
|42000|構文エラーまたはアクセス違反|ドライバーは、引数*操作*で要求された操作を実行するために必要に応じて行をロックできませんでした。<br /><br /> ドライバーは、引数*LockType*に要求された行をロックできませんでした。|  
|44000|WITH CHECK OPTION 違反|*Operation*引数は SQL_UPDATE でしたが、この更新は、表示されているテーブルまたは表示されているテーブルから派生したテーブルに対して実行されました。この場合、 **WITH CHECK OPTION**を指定することで、更新プログラムの影響を受ける1つ以上の行が削除されます。表示されているテーブルに存在します。|  
|HY000|一般エラー|特定の SQLSTATE がなく、実装固有の SQLSTATE が定義されていないエラーが発生しました。 Messagetext バッファーの**SQLGetDiagRec によっ**て返されるエラーメッセージには、エラーとその原因が記述されています。  *\**|  
|HY001|メモリ割り当てエラー|ドライバーは、関数の実行または完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY008|操作が取り消されました|*StatementHandle*に対して非同期処理が有効になりました。 関数が呼び出され、実行が完了する前に、 **SQLCancel**または**Sqlcancelhandle**が*StatementHandle*で呼び出された後、 *StatementHandle*で関数が再度呼び出されました。<br /><br /> 関数が呼び出され、実行が完了する前に、マルチスレッドアプリケーションの別のスレッドの*StatementHandle*で**SQLCancel**または**sqlcancelhandle**が呼び出されました。|  
|HY010|関数のシーケンスエラー|(DM) 非同期的に実行する関数が、 *StatementHandle*に関連付けられている接続ハンドルに対して呼び出されました。 この非同期関数は、SQLSetPos 関数が呼び出されたときにまだ実行されていました。<br /><br /> (DM) 指定された*StatementHandle*は実行状態ではありませんでした。 最初に**SQLExecDirect**、 **sqlexecute**、またはカタログ関数を呼び出さずに関数が呼び出されました。<br /><br /> (DM) 非同期的に実行されている関数 (この1つではない) が*StatementHandle*に対して呼び出され、この関数が呼び出されたときにまだ実行されています。<br /><br /> (DM) **Sqlexecute**、 **SQLExecDirect**、 **sqlbulkoperations**、または**SQLSetPos**が*StatementHandle*に対して呼び出され、SQL_NEED_DATA が返されました。 この関数は、実行時データのすべてのパラメーターまたは列に対してデータが送信される前に呼び出されました。<br /><br /> (DM) ドライバー*は ODBC 2.x*ドライバーで、 **sqlfetch**が呼び出された後に*StatementHandle*に対して**SQLSetPos**が呼び出されました。|  
|HY011|属性を今設定することはできません|(DM) ドライバー*は ODBC 2.x*ドライバーでした。SQL_ATTR_ROW_STATUS_PTR statement 属性が設定されました。次に、 **Sqlfetch**、 **sqlfetchscroll**、または**SQLExtendedFetch**が呼び出される前に**SQLSetPos**が呼び出されました。|  
|HY013|メモリ管理エラー|基になるメモリオブジェクトにアクセスできなかったため、関数呼び出しを処理できませんでした。メモリ不足の状態が原因である可能性があります。|  
|HY090|文字列またはバッファーの長さが無効です|*操作*引数が SQL_UPDATE で、データ値が null ポインターで、列の長さの値が0、SQL_DATA_AT_EXEC、SQL_COLUMN_IGNORE、SQL_NULL_DATA、または SQL_LEN_DATA_AT_EXEC_OFFSET 以下でした。<br /><br /> *操作*引数は SQL_UPDATE でした。データ値が null ポインターではありませんでした。C データ型は SQL_C_BINARY または SQL_C_CHAR です。列の長さの値が0未満で、SQL_DATA_AT_EXEC、SQL_COLUMN_IGNORE、SQL_NTS、SQL_NULL_DATA、または SQL_LEN_DATA_AT_EXEC_OFFSET 以下ではありませんでした。<br /><br /> 長さ/インジケーターバッファーの値は SQL_DATA_AT_EXEC でした。SQL 型は、SQL_LONGVARCHAR、SQL_LONGVARBINARY、または long データソース固有のデータ型のいずれかです。**SQLGetInfo**の SQL_NEED_LONG_DATA_LEN 情報型は "Y" でした。|  
|HY092|無効な属性識別子|(DM)*操作*引数に指定された値が無効でした。<br /><br /> (DM) *LockType*引数に指定された値が無効でした。<br /><br /> *操作*引数が SQL_UPDATE または SQL_DELETE で、SQL_ATTR_CONCURRENCY statement 属性が SQL_ATTR_CONCUR_READ_ONLY でした。|  
|HY107|行の値が有効範囲にありません|引数*RowNumber*に指定された値が、行セット内の行数を超えています。|  
|HY109|カーソル位置が無効です|*StatementHandle*に関連付けられているカーソルは順方向専用として定義されているため、カーソルを行セット内に配置できませんでした。 **SQLSetStmtAttr**の SQL_ATTR_CURSOR_TYPE 属性の説明を参照してください。<br /><br /> *操作*引数が SQL_UPDATE、SQL_DELETE、または SQL_REFRESH で、 *RowNumber*引数によって識別される行が削除されたか、またはフェッチされませんでした。<br /><br /> (DM) *RowNumber*引数が0で、*操作*の引数が SQL_POSITION でした。<br /><br /> **SQLSetPos**は**sqlbulkoperations**が呼び出された後、 **Sqlbulkoperations**または**sqlfetch**が呼び出される前に呼び出されました。|  
|HY117|トランザクションの状態が不明なため、接続が中断されました。 切断と読み取り専用の機能のみが許可されます。|(DM) 中断状態の詳細については、「 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)」を参照してください。|  
|HYC00|省略可能な機能は実装されていません|ドライバーまたはデータソースが、*操作*引数または*LockType*引数で要求された操作をサポートしていません。|  
|HYT00|タイムアウトが発生しました|データソースから結果セットが返される前に、クエリのタイムアウト期間が経過しました。 タイムアウト期間は、SQL_ATTR_QUERY_TIMEOUT の*属性*を使用して**SQLSetStmtAttr**によって設定されます。|  
|HYT01|接続タイムアウトの期限が切れました|データソースが要求に応答する前に、接続のタイムアウト期間が経過しました。 接続タイムアウト期間は、 **SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT によって設定されます。|  
|IM001|ドライバーはこの機能をサポートしていません|(DM) *StatementHandle*に関連付けられているドライバーでは、関数はサポートされていません。|  
|IM017|非同期通知モードでは、ポーリングは無効になっています|通知モデルが使用されるたびに、ポーリングは無効になります。|  
|IM018|**Sqlcompleteasync**は、このハンドルで前の非同期操作を完了するために呼び出されていません。|ハンドルに対する前の関数呼び出しで SQL_STILL_EXECUTING が返され、通知モードが有効になっている場合は、処理を完了するために、ハンドルで**Sqlcompleteasync**を呼び出して、操作を完了する必要があります。|  
  
## <a name="comments"></a>コメント  
  
> [!CAUTION]
>  **SQLSetPos**を呼び出すことができるステートメントの状態と *、ODBC 2.x*アプリケーションとの互換性を確保するために必要な操作の詳細については、「[ブロックカーソル、スクロール可能なカーソル、および下位互換性](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md)」を参照してください。  
  
## <a name="rownumber-argument"></a>RowNumber 引数  
 *RowNumber*引数は、*操作*引数で指定された操作を実行する行セット内の行の番号を指定します。 *RowNumber*が0の場合、操作は行セットのすべての行に適用されます。 *RowNumber*には、0から行セット内の行数までの値を指定する必要があります。  
  
> [!NOTE]  
>  C 言語では、配列は0から始まるので、 *RowNumber*引数は1から始まるものです。 たとえば、行セットの5番目の行を更新する場合、アプリケーションは配列インデックス4の行セットバッファーを変更しますが、 *RowNumber*は5に指定します。  
  
 すべての操作は、 *RowNumber*によって指定された行にカーソルを置きます。 次の操作にはカーソル位置が必要です。  
  
-   位置指定の update および delete ステートメント。  
  
-   **SQLGetData**を呼び出します。  
  
-   SQL_DELETE、SQL_REFRESH、および SQL_UPDATE オプションを使用して**SQLSetPos**を呼び出します。  
  
 たとえば、RowNumber が2の*操作* **で SQL_DELETE**を呼び出す場合、 *RowNumber*が2の場合、カーソルは行セットの2番目の行に配置され、その行は削除されます。 2番目の行の実装行ステータス配列 (SQL_ATTR_ROW_STATUS_PTR statement 属性が指す) のエントリが SQL_ROW_DELETED に変更されます。  
  
 アプリケーションで**SQLSetPos**を呼び出すと、カーソル位置を指定できます。 通常は、位置指定の update または delete ステートメントを実行する前にカーソルを移動するか、 **SQLGetData**を呼び出すために、SQL_POSITION または SQL_REFRESH 操作を使用して**SQLSetPos**を呼び出します。  
  
## <a name="operation-argument"></a>Operation 引数  
 *Operation*引数は、次の操作をサポートしています。 アプリケーションは、データソースでサポートされているオプションを特定するために、SQL_DYNAMIC_CURSOR_ATTRIBUTES1、SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1、SQL_KEYSET_CURSOR_ATTRIBUTES1、または SQL_STATIC_CURSOR_ATTRIBUTES1 を使用して**SQLGetInfo**を呼び出します。情報の種類 (カーソルの種類によって異なります)。  
  
|*操作*<br /><br /> 引数 (argument)|操作|  
|------------------------------|---------------|  
|SQL_POSITION|このドライバーは、 *RowNumber*によって指定された行にカーソルを置きます。<br /><br /> SQL_ATTR_ROW_OPERATION_PTR statement 属性が指す行ステータス配列の内容は、SQL_POSITION*操作*では無視されます。|  
|SQL_REFRESH|ドライバーは、 *RowNumber*によって指定された行にカーソルを置いて、その行の行セットバッファー内のデータを更新します。 ドライバーが行セットバッファー内のデータを返す方法の詳細については、 **SQLBindCol**の行方向と列方向のバインドに関する記述を参照してください。<br /><br /> **SQLSetPos**で SQL_REFRESH を*操作*すると、現在フェッチされている行セット内の行の状態と内容が更新されます。 これには、ブックマークの更新も含まれます。 バッファー内のデータは更新されますが、refetched されていないため、行セットのメンバーシップは固定されています。 これは、 *Fetchorientation*を SQL_FETCH_RELATIVE に設定し、 *RowNumber*を0に等しい値を指定して**sqlfetchscroll**を呼び出すことによって行われる更新とは異なります。これは、結果セットから行セットを refetches して、追加されたデータを表示したり、削除したりすることができます。これらの操作がドライバーとカーソルによってサポートされている場合は、データを削除します。<br /><br /> **SQLSetPos**を正常に更新しても、SQL_ROW_DELETED の行の状態は変わりません。 行セット内の削除された行は、次のフェッチまで削除済みとしてマークされ続けます。 カーソルでパッキングがサポートされている場合、次のフェッチ時に行が非表示になります (以降の**Sqlfetch**または**sqlfetchscroll**は、削除された行を返しません)。<br /><br /> 追加された行は、 **SQLSetPos**を使用した更新が実行されるときには表示されません。 この動作は**Sqlfetchscroll**とは異なり、 *FetchType*は SQL_FETCH_RELATIVE で、 *RowNumber*は0に等しくなります。これにより、現在の行セットも更新されますが、追加されたレコードが表示されますが、これらの操作がカーソルによってサポートされます。<br /><br /> **SQLSetPos**を正常に更新すると、SQL_ROW_ADDED の行の状態が SQL_ROW_SUCCESS に変更されます (行の状態の配列が存在する場合)。<br /><br /> **SQLSetPos**を正常に更新すると、行の状態が SQL_ROW_UPDATED に変更されます (行の状態の配列が存在する場合)。<br /><br /> 行の**SQLSetPos**操作でエラーが発生した場合、行の状態は SQL_ROW_ERROR (行の状態の配列が存在する場合) に設定されます。<br /><br /> SQL_CONCUR_ROWVER または SQL_CONCUR_VALUES の SQL_ATTR_CONCURRENCY statement 属性で開かれたカーソルについては、 **SQLSetPos**を使用して更新すると、データソースによって使用されるオプティミスティック同時実行制御の値が更新され、行が変更されたことが検出されることがあります。 この場合、カーソルの同時実行を確実にするために使用される行のバージョンまたは値は、サーバーから行セットバッファーが更新されるたびに更新されます。 このエラーは、更新された行ごとに発生します。<br /><br /> SQL_ATTR_ROW_OPERATION_PTR statement 属性が指す行ステータス配列の内容は、SQL_REFRESH*操作*では無視されます。|  
|SQL_UPDATE|ドライバーは、 *RowNumber*によって指定された行にカーソルを置き、行セットバッファーの値 ( **SQLBindCol**の*targetvalueptr*引数) を使用してデータの基になる行を更新します。 長さ/インジケーターバッファー ( **SQLBindCol**の*StrLen_or_IndPtr*引数) からデータの長さを取得します。 列の長さが SQL_COLUMN_IGNORE の場合、列は更新されません。 行を更新すると、ドライバーは行の状態の配列の対応する要素を SQL_ROW_UPDATED または SQL_ROW_SUCCESS_WITH_INFO に変更します (行の状態の配列が存在する場合)。<br /><br /> SQL_UPDATE の*操作*引数を持つ**SQLSetPos**が、重複する列を含むカーソルで呼び出された場合の動作は、ドライバーによって定義されています。 ドライバーがドライバーで定義した SQLSTATE を返すことができます。また、結果セットに表示される最初の列を更新したり、ドライバーによって定義されたその他の動作を実行したりすることができます。<br /><br /> SQL_ATTR_ROW_OPERATION_PTR statement 属性が指す行演算配列は、一括更新中に現在の行セットの行を無視することを示すために使用できます。 詳細については、後の「状態と操作の配列」を参照してください。|  
|SQL_DELETE|ドライバーは、 *RowNumber*によって指定された行にカーソルを置いて、データの基になる行を削除します。 このメソッドは、行状態配列の対応する要素を SQL_ROW_DELETED に変更します。 行が削除された後、行に対しては、update ステートメントと delete ステートメントの位置を指定すると、 **SQLGetData**を呼び出すことができます。また、*操作*が SQL_POSITION 以外に設定されている場合は、 **SQLSetPos**の呼び出しも無効になります。 パッキングをサポートするドライバーでは、データソースから新しいデータを取得するときに、行がカーソルから削除されます。<br /><br /> 行が表示されたままであるかどうかは、カーソルの種類によって異なります。 たとえば、削除された行は静的カーソルやキーセットドリブンカーソルに対して表示されますが、動的カーソルには見えません。<br /><br /> SQL_ATTR_ROW_OPERATION_PTR statement 属性によってポイントされている行操作配列は、一括削除中に現在の行セットの行を無視することを示すために使用できます。 詳細については、後の「状態と操作の配列」を参照してください。|  
  
## <a name="locktype-argument"></a>LockType 引数  
 *LockType*引数は、アプリケーションで同時実行を制御する方法を提供します。 ほとんどの場合、同時実行レベルとトランザクションをサポートするデータソースでは、 *LockType*引数の SQL_LOCK_NO_CHANGE 値のみがサポートされます。 *LockType*引数は、一般にファイルベースのサポートにのみ使用されます。  
  
 *LockType*引数は、 **SQLSetPos**が実行された後の行のロック状態を指定します。 ドライバーが、要求された操作を実行するために、または*LockType*引数を満たすために行をロックできない場合は、SQL_ERROR と SQLSTATE 42000 (構文エラーまたはアクセス違反) が返されます。  
  
 1つのステートメントに対して*LockType*引数が指定されていますが、このロックは、接続上のすべてのステートメントに対して同じ特権を accords します。 特に、ある接続で1つのステートメントによって取得されたロックを、同じ接続上の別のステートメントによってロック解除することができます。  
  
 **Sqlsetpos**によってロックされている行は、アプリケーションが*LockType*を SQL_LOCK_UNLOCK に設定されている行に対して**sqlsetpos**を呼び出すか、またはアプリケーションがステートメントまたは SQLFreeStmt の**sqlfreehandle**を呼び出すまでロックされたままになります。SQL_CLOSE オプションを使用します。 トランザクションをサポートするドライバーの場合、アプリケーションが**SQLEndTran**を呼び出して、接続でトランザクションをコミットまたはロールバックすると、そのトランザクションがコミットまたはロールバックされるときに、ロックが解除されます (トランザクションのコミットまたはロールバック時にカーソルが閉じられた場合)。**SQLGetInfo**によって返される SQL_CURSOR_COMMIT_BEHAVIOR および SQL_CURSOR_ROLLBACK_BEHAVIOR 情報の種類によって示されます。  
  
 *LockType*引数では、次の種類のロックがサポートされています。 アプリケーションは、データソースでサポートされているロックを特定するために、SQL_DYNAMIC_CURSOR_ATTRIBUTES1、SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1、SQL_KEYSET_CURSOR_ATTRIBUTES1、または SQL_STATIC_CURSOR_ATTRIBUTES1 を使用して**SQLGetInfo**を呼び出します。情報の種類 (カーソルの種類によって異なります)。  
  
|*LockType*引数|ロックの種類|  
|-------------------------|---------------|  
|SQL_LOCK_NO_CHANGE|ドライバーまたはデータソースは、 **SQLSetPos**が呼び出される前と同じロックまたはロック解除された状態になっていることを確認します。 この値の*LockType*を使用すると、行レベルの明示的ロックをサポートしていないデータソースで、現在の同時実行レベルとトランザクション分離レベルで必要なロックを使用できます。|  
|SQL_LOCK_EXCLUSIVE|ドライバーまたはデータソースは、行を排他的にロックします。 別の接続または別のアプリケーションのステートメントを使用して、行のロックを取得することはできません。|  
|SQL_LOCK_UNLOCK|ドライバーまたはデータソースによって行のロックが解除されます。|  
  
 ドライバーが SQL_LOCK_EXCLUSIVE をサポートしているが SQL_LOCK_UNLOCK をサポートしていない場合は、前の段落で説明した関数呼び出しのいずれかが発生するまで、ロックされている行がロックされたままになります。  
  
 ドライバーが SQL_LOCK_EXCLUSIVE をサポートしていても、SQL_LOCK_UNLOCK をサポートしていない場合、ロックされている行は、アプリケーションがステートメントまたは SQL_CLOSE オプションを使用して**SQLFreeStmt**の**sqlfreehandle**を呼び出すまでロックされたままになります。 ドライバーがトランザクションをサポートし、トランザクションのコミットまたはロールバック時にカーソルを閉じると、アプリケーションは**SQLEndTran**を呼び出します。  
  
 **SQLSetPos**の update 操作と delete 操作の場合、アプリケーションは次のように*LockType*引数を使用します。  
  
-   取得した行が変更されないことを保証するために、アプリケーションは、 *Operation*を SQL_REFRESH に設定し、 *LockType*を SQL_LOCK_EXCLUSIVE に設定して、 **SQLSetPos**を呼び出します。  
  
-   アプリケーションが*LockType*を SQL_LOCK_NO_CHANGE に設定した場合、ドライバーは、アプリケーションが SQL_ATTR_CONCURRENCY statement 属性に SQL_CONCUR_LOCK を指定した場合にのみ、更新操作または削除操作が成功することを保証します。  
  
-   アプリケーションで SQL_ATTR_CONCURRENCY statement 属性に SQL_CONCUR_ROWVER または SQL_CONCUR_VALUES を指定した場合、ドライバーは行のバージョンまたは値を比較し、アプリケーションが行をフェッチした後に行が変更された場合は操作を拒否します。  
  
-   アプリケーションで SQL_ATTR_CONCURRENCY statement 属性に SQL_CONCUR_READ_ONLY が指定されている場合、ドライバーは更新操作または削除操作を拒否します。  
  
 SQL_ATTR_CONCURRENCY statement 属性の詳細については、「 [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)」を参照してください。  
  
## <a name="status-and-operation-arrays"></a>状態と操作の配列  
 **SQLSetPos**を呼び出すと、次の状態と操作の配列が使用されます。  
  
-   行の状態の配列 (IRD と SQL_ATTR_ROW_STATUS_ARRAY statement 属性の SQL_DESC_ARRAY_STATUS_PTR フィールドによって示される) には、行セット内の各データ行の状態値が含まれています。 ドライバーは、 **Sqlfetch**、 **sqlfetchscroll**、 **sqlbulkoperations**、 **SQLSetPos**の呼び出し後に、この配列の状態値を設定します。 この配列は、SQL_ATTR_ROW_STATUS_PTR statement 属性によってポイントされます。  
  
-   行の操作配列 (SQL_DESC_ARRAY_STATUS_PTR フィールドと SQL_ATTR_ROW_OPERATION_ARRAY statement 属性で参照される) には、一括操作の**SQLSetPos**の呼び出しがあるかどうかを示す行セットの各行の値が含まれています。は無視されるか、実行されます。 配列の各要素は、SQL_ROW_PROCEED (既定値) または SQL_ROW_IGNORE に設定されます。 この配列は、SQL_ATTR_ROW_OPERATION_PTR statement 属性によってポイントされます。  
  
 状態と操作の配列内の要素の数は、SQL_ATTR_ROW_ARRAY_SIZE statement 属性で定義されているように、行セット内の行数と同じである必要があります。  
  
 行の状態の配列の詳細については、「 [Sqlfetch](../../../odbc/reference/syntax/sqlfetch-function.md)」を参照してください。 行操作配列の詳細については、このセクションの後の「一括操作での行の無視」を参照してください。  
  
## <a name="using-sqlsetpos"></a>SQLSetPos の使用  
 アプリケーションは**SQLSetPos**を呼び出す前に、次の一連の手順を実行する必要があります。  
  
1.  アプリケーションで、 *Operation*を SQL_UPDATE に設定して**SQLSetPos**を呼び出す場合は、各列に対して**SQLBindCol** (または**SQLSetDescRec**) を呼び出して、列のデータと長さのデータ型とバインドバッファーを指定します。  
  
2.  アプリケーションが SQL_DELETE または SQL_UPDATE に設定された*操作*を使用して**SQLSetPos**を呼び出す場合は、 **sqlcolattribute**を呼び出して、削除または更新する列が更新可能であることを確認します。  
  
3.  結果セットを作成するには、 **SQLExecDirect**、 **sqlexecute**、または catalog 関数を呼び出します。  
  
4.  データを取得するには、 **Sqlfetch**または**sqlfetchscroll**を呼び出します。  
  
 **Sqlsetpos**の使用方法の詳細については、「 [sqlsetpos を使用したデータの更新](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md)」を参照してください。  
  
## <a name="deleting-data-using-sqlsetpos"></a>SQLSetPos を使用したデータの削除  
 **Sqlsetpos**を使用してデータを削除するには、アプリケーションは、 *RowNumber*を、削除する行の番号に設定し、*操作*を SQL_DELETE に設定して**sqlsetpos**を呼び出します。  
  
 データが削除されると、ドライバーは、適切な行の実装行状態配列の値を SQL_ROW_DELETED (または SQL_ROW_ERROR) に変更します。  
  
## <a name="updating-data-using-sqlsetpos"></a>SQLSetPos を使用したデータの更新  
 アプリケーションは、バインドされたデータバッファーまたは**Sqlputdata**の1つ以上の呼び出しに列の値を渡すことができます。 データが**Sqlputdata**で渡される列は、*実行時データ* *列*と呼ばれます。 これらは、SQL_LONGVARBINARY 列と SQL_LONGVARCHAR 列のデータを送信するために一般的に使用され、他の列と混在させることができます。  
  
#### <a name="to-update-data-with-sqlsetpos-an-application"></a>SQLSetPos を使用してデータを更新するには、次のようにします。  
  
1.  **SQLBindCol**でバインドされたデータと長さ/インジケーターバッファーに値を配置します。  
  
    -   通常の列の場合、アプリケーションは、新しい列の値 *\*を targetvalueptr*バッファーに、  *\** その値の長さを StrLen_or_IndPtr バッファーに配置します。 行を更新しない場合、アプリケーションは行操作配列のその行の要素に SQL_ROW_IGNORE を配置します。  
  
    -   実行時データ列の場合、アプリケーションは、列番号などのアプリケーション定義の値を *\*targetvalueptr*バッファーに配置します。 この値は、後で列を識別するために使用できます。  
  
         アプリケーションによって、SQL_LEN_DATA_AT_EXEC (*length*) マクロの結果が **StrLen_or_IndPtr*バッファーに配置されます。 列の SQL データ型が SQL_LONGVARBINARY、SQL_LONGVARCHAR、または long data source 固有のデータ型で、ドライバーが**SQLGetInfo**の SQL_NEED_LONG_DATA_LEN information 型に対して "Y" を返す場合、 *length*はデータのバイト数です。パラメーターに対して送信されます。それ以外の場合は、負でない値である必要があり、無視されます。  
  
2.  *操作*の引数を SQL_UPDATE に設定して**SQLSetPos**を呼び出し、データ行を更新します。  
  
    -   実行時データ列がない場合は、処理が完了します。  
  
    -   実行時データ列がある場合、関数は SQL_NEED_DATA を返し、手順3に進みます。  
  
3.  **Sqlparamdata**を呼び出して、処理する最初の実行時データ列の *\*targetvalueptr*バッファーのアドレスを取得します。 **Sqlparamdata**は SQL_NEED_DATA を返します。 アプリケーションは、  *\*targetvalueptr*バッファーからアプリケーション定義の値を取得します。  
  
    > [!NOTE]  
    >  実行時データパラメーターは実行時データ列に似ていますが、 **Sqlparamdata**によって返される値はそれぞれ異なっています。  
  
    > [!NOTE]  
    >  実行時データパラメーターは、 **SQLExecDirect**または**sqlexecute**を使用してステートメントを実行するときに、 **sqlputdata**を使用してデータを送信する SQL ステートメントのパラメーターです。 **SQLBindParameter**にバインドされているか、 **SQLSetDescRec**で記述子を設定します。 **Sqlparamdata**によって返される値は、 *parametervalueptr*引数の**SQLBindParameter**に渡される32ビット値です。  
  
    > [!NOTE]  
    >  実行時データ列は、行が**SQLSetPos**で更新されたときに**sqlputdata**を使用してデータが送信される行セット内の列です。 これらは**SQLBindCol**にバインドされています。 **Sqlparamdata**によって返される値は、処理される **targetvalueptr*バッファー内の行のアドレスです。  
  
4.  **Sqlputdata**を1回以上呼び出して、列のデータを送信します。 **Sqlputdata**に指定された *\*targetvalueptr*バッファーにすべてのデータ値を返すことができない場合は、複数の呼び出しが必要です。同じ列に対して複数の**sqlputdata**を呼び出すことは、文字 C データを送信するときにのみ許可されます。文字、バイナリ、またはデータソース固有のデータ型の列、または文字、バイナリ、またはデータソース固有のデータ型を持つ列にバイナリ C データを送信する場合。  
  
5.  **Sqlparamdata**を再度呼び出して、すべてのデータが列に送信されたことを通知します。  
  
    -   実行時データ列の数が多い場合、 **Sqlparamdata**は SQL_NEED_DATA を返し、処理する次の実行時データ列の*targetvalueptr*バッファーのアドレスを返します。 アプリケーションは、手順4と5を繰り返します。  
  
    -   実行時データ列がない場合は、プロセスが完了します。 ステートメントが正常に実行された場合、 **Sqlparamdata**は SQL_SUCCESS または SQL_SUCCESS_WITH_INFO を返します。実行が失敗した場合は、SQL_ERROR を返します。 この時点で、 **Sqlparamdata**は**SQLSetPos**で返すことができる SQLSTATE を返すことができます。  
  
 データが更新されている場合、ドライバーは、該当する行の実装行の状態配列の値を SQL_ROW_UPDATED に変更します。  
  
 操作が取り消された場合、または**Sqlparamdata**または**sqlparamdata**でエラーが発生した場合、 **SQLSetPos**が SQL_NEED_DATA を返し、実行中のすべての列のデータが送信される前に、アプリケーションは**SQLCancel**のみを**呼び出すことができます。** ステートメントまたはステートメントに関連付けられている接続の SQLGetDiagField、 **SQLGetDiagRec**、 **sqlgetfunctions**、 **Sqlgetfunctions**、または**sqlgetfunctions** 。 ステートメントまたはステートメントに関連付けられている接続に対して他の関数を呼び出すと、関数は SQL_ERROR と SQLSTATE HY010 (関数シーケンスエラー) を返します。  
  
 アプリケーションが**SQLCancel**を呼び出しても、ドライバーが実行時データ列のデータを必要としている場合、ドライバーは操作をキャンセルします。 その後、アプリケーションは**SQLSetPos**を再度呼び出すことができます。取り消すと、カーソルの状態または現在のカーソル位置には影響しません。  
  
 カーソルに関連付けられているクエリ仕様の選択リストに同じ列への複数の参照が含まれている場合、エラーが生成されたか、ドライバーが重複した参照を無視し、要求された操作を実行した場合、ドライバーが定義されます。  
  
## <a name="performing-bulk-operations"></a>一括操作の実行  
 *RowNumber*引数が0の場合、ドライバーは、SQL_ATTR_ROW_OPERATION_PTR によってポイントされている行操作配列のフィールドの値が SQL_ROW_PROCEED の行セット内のすべての行に対して、 *operation*引数で指定された操作を実行します。statement 属性。 これは、SQL_DELETE、SQL_REFRESH、または SQL_UPDATE の*操作*引数の*RowNumber*引数の有効な値ですが、SQL_POSITION は使用できません。 SQL_POSITION の*操作*と*RowNumber*が0の場合、 **SQLSetPos**は SQLSTATE HY109 (無効なカーソル位置) を返します。  
  
 SQLSTATE HYT00 (タイムアウト期限切れ) など、行セット全体に関連するエラーが発生した場合、ドライバーは SQL_ERROR と適切な SQLSTATE を返します。 行セットバッファーの内容は未定義で、カーソル位置は変更されません。  
  
 1つの行に関連するエラーが発生した場合、ドライバーは次のようになります。  
  
-   SQL_ATTR_ROW_STATUS_PTR statement 属性が指す行ステータス配列の行の要素を SQL_ROW_ERROR に設定します。  
  
-   エラーキューにエラーの追加の SQLSTATEs を1つ以上ポストし、診断データ構造の SQL_DIAG_ROW_NUMBER フィールドを設定します。  
  
 エラーまたは警告が処理された後、ドライバーが行セット内の残りの行に対して操作を完了すると、SQL_SUCCESS_WITH_INFO が返されます。 このため、エラーが返された行ごとに、0個以上の追加の SQLSTATEs がエラーキューに含まれています。 エラーまたは警告の処理後にドライバーが操作を停止した場合は、SQL_ERROR が返されます。  
  
 ドライバーから SQLSTATE 01004 (データが切り捨てられました) などの警告が返された場合、特定の行に適用されるエラー情報が返される前に、行セット全体または行セット内の不明な行に適用される警告が返されます。 特定の行に関する警告と、それらの行に関する他のエラー情報が返されます。  
  
 *RowNumber*が0の場合、*操作*が SQL_UPDATE、SQL_REFRESH、または SQL_DELETE の場合、 **SQLSetPos**が動作している行の数は SQL_ATTR_ROWS_FETCHED_PTR statement 属性によって示されます。  
  
 *RowNumber*が0で、*操作*が SQL_DELETE、SQL_REFRESH、または SQL_UPDATE の場合、操作の後の現在の行は、操作の前の現在の行と同じになります。  
  
## <a name="ignoring-a-row-in-a-bulk-operation"></a>一括操作での行の無視  
 行操作の配列を使用して、 **SQLSetPos**を使用した一括操作中に、現在の行セットの行を無視することを示すことができます。 一括操作中に1つ以上の行を無視するようにドライバーに指示するには、アプリケーションで次の手順を実行する必要があります。  
  
1.  **SQLSetStmtAttr**を呼び出して、SQL_ATTR_ROW_OPERATION_PTR statement 属性が Sqlus悪意 lints の配列を指すように設定します。 このフィールドは、 **SQLSetDescField**を呼び出して設定することもできます。この場合、アプリケーションは記述子ハンドルを取得する必要があるため、SQL_DESC_ARRAY_STATUS_PTR ヘッダーフィールドを設定します。  
  
2.  行操作配列の各要素を次の2つの値のいずれかに設定します。  
  
    -   SQL_ROW_IGNORE は、行が一括操作に対して除外されることを示します。  
  
    -   SQL_ROW_PROCEED は、行が一括操作に含まれることを示します。 (これは既定値です)。  
  
3.  **SQLSetPos**を呼び出して、一括操作を実行します。  
  
 行操作配列には、次の規則が適用されます。  
  
-   SQL_ROW_IGNORE と SQL_ROW_PROCEED は、SQL_DELETE または SQL_UPDATE の*操作*で**SQLSetPos**を使用した一括操作にのみ影響します。 SQL_REFRESH または SQL_POSITION の*操作*によって**SQLSetPos**への呼び出しには影響しません。  
  
-   既定では、ポインターは null に設定されています。  
  
-   ポインターが null の場合は、すべての要素が SQL_ROW_PROCEED に設定されているかのようにすべての行が更新されます。  
  
-   要素を SQL_ROW_PROCEED に設定しても、その特定の行で操作が行われることは保証されません。 たとえば、行セット内の特定の行にステータス SQL_ROW_ERROR がある場合、そのアプリケーションが SQL_ROW_PROCEED を指定したかどうかに関係なく、ドライバーはその行を更新できない可能性があります。 アプリケーションでは、行の状態の配列を常に確認して、操作が成功したかどうかを確認する必要があります。  
  
-   SQL_ROW_PROCEED は、ヘッダーファイルで0として定義されています。 アプリケーションでは、すべての行を処理するために、行操作配列を0に初期化できます。  
  
-   行操作配列の要素番号 "n" が SQL_ROW_IGNORE に設定されていて、 **sqlsetpos**が呼び出されて一括更新または削除操作を実行する場合、行セットの n 番目の行は**SQLSetPos**の呼び出し後も変更されません。  
  
-   アプリケーションでは、読み取り専用の列を自動的に SQL_ROW_IGNORE に設定する必要があります。  
  
## <a name="ignoring-a-column-in-a-bulk-operation"></a>一括操作での列の無視  
 1つ以上の読み取り専用列に対する更新によって生成された不要な処理診断を回避するために、アプリケーションでは、バインドされた長さ/インジケーターバッファーの値を SQL_COLUMN_IGNORE に設定できます。 詳細については、「 [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)」を参照してください。  
  
## <a name="code-example"></a>コード例  
 次の例では、ユーザーが ORDERS テーブルを参照して注文ステータスを更新できるようにします。 カーソルは、行セットサイズが20のキーセットドリブンであり、オプティミスティック同時実行制御を使用して行バージョンを比較しています。 各行セットがフェッチされると、アプリケーションによって出力され、ユーザーは注文の状態を選択して更新できるようになります。 アプリケーションは**SQLSetPos**を使用して、選択された行にカーソルを置き、行の位置指定更新を実行します。 (わかりやすくするために、エラー処理は省略されています)。  
  
```cpp  
#define ROWS 20  
#define STATUS_LEN 6  
  
SQLCHAR        szStatus[ROWS][STATUS_LEN], szReply[3];  
SQLINTEGER     cbStatus[ROWS], cbOrderID;  
SQLUSMALLINT   rgfRowStatus[ROWS];  
SQLUINTEGER    sOrderID, crow = ROWS, irow;  
SQLHSTMT       hstmtS, hstmtU;  
  
SQLSetStmtAttr(hstmtS, SQL_ATTR_CONCURRENCY, (SQLPOINTER) SQL_CONCUR_ROWVER, 0);  
SQLSetStmtAttr(hstmtS, SQL_ATTR_CURSOR_TYPE, (SQLPOINTER) SQL_CURSOR_KEYSET_DRIVEN, 0);  
SQLSetStmtAttr(hstmtS, SQL_ATTR_ROW_ARRAY_SIZE, (SQLPOINTER) ROWS, 0);  
SQLSetStmtAttr(hstmtS, SQL_ATTR_ROW_STATUS_PTR, (SQLPOINTER) rgfRowStatus, 0);  
SQLSetCursorName(hstmtS, "C1", SQL_NTS);  
SQLExecDirect(hstmtS, "SELECT ORDERID, STATUS FROM ORDERS ", SQL_NTS);  
  
SQLBindCol(hstmtS, 1, SQL_C_ULONG, &sOrderID, 0, &cbOrderID);  
SQLBindCol(hstmtS, 2, SQL_C_CHAR, szStatus, STATUS_LEN, &cbStatus);  
  
while ((retcode == SQLFetchScroll(hstmtS, SQL_FETCH_NEXT, 0)) != SQL_ERROR) {  
   if (retcode == SQL_NO_DATA_FOUND)  
      break;  
   for (irow = 0; irow < crow; irow++) {  
      if (rgfRowStatus[irow] != SQL_ROW_DELETED)  
         printf("%2d %5d %*s\n", irow+1, sOrderID, NAME_LEN-1, szStatus[irow]);  
   }  
   while (TRUE) {  
      printf("\nRow number to update?");  
      gets_s(szReply, 3);  
      irow = atoi(szReply);  
      if (irow > 0 && irow <= crow) {  
         printf("\nNew status?");  
         gets_s(szStatus[irow-1], (ROWS * STATUS_LEN));  
         SQLSetPos(hstmtS, irow, SQL_POSITION, SQL_LOCK_NO_CHANGE);  
         SQLPrepare(hstmtU,  
          "UPDATE ORDERS SET STATUS=? WHERE CURRENT OF C1", SQL_NTS);  
         SQLBindParameter(hstmtU, 1, SQL_PARAM_INPUT,  
            SQL_C_CHAR, SQL_CHAR,  
            STATUS_LEN, 0, szStatus[irow], 0, NULL);  
         SQLExecute(hstmtU);  
      } else if (irow == 0) {  
         break;  
      }  
   }  
}  
```  
  
 その他の例については、「配置された[Update および Delete ステートメント](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md)」および「 [SQLSetPos による行セットの行の更新](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md)」を参照してください。  
  
## <a name="related-functions"></a>関連する関数  
  
|詳細|参照先|  
|---------------------------|---------|  
|結果セット内の列へのバッファーのバインド|[SQLBindCol 関数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|ブロックカーソル位置に関係のない一括操作の実行|[SQLBulkOperations 関数](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|ステートメント処理の取り消し|[SQLCancel 関数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|データのブロックのフェッチまたは結果セットのスクロール|[SQLFetchScroll 関数](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|記述子の1つのフィールドを取得する|[SQLGetDescField 関数](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|記述子の複数のフィールドを取得する|[SQLGetDescRec 関数](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|記述子の1つのフィールドの設定|[SQLSetDescField 関数](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|記述子の複数のフィールドの設定|[SQLSetDescRec 関数](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
|ステートメント属性の設定|[SQLSetStmtAttr 関数](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>参照  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)
