---
title: SQLFetch 関数 |Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLFetch
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLFetch
helpviewer_keywords:
- SQLFetch function [ODBC]
ms.assetid: 6c6611d2-bc6a-4390-87c9-1c5dd9cfe07c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5c5d2d14786080f665e488acf2bfa888f09a5df4
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345199"
---
# <a name="sqlfetch-function"></a>SQLFetch 関数
**互換性**  
 導入されたバージョン:ODBC 1.0 標準準拠:ISO 92  
  
 **まとめ**  
 **Sqlfetch**は、結果セットから次の行セットデータをフェッチし、すべてのバインドされた列のデータを返します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLFetch(  
     SQLHSTMT     StatementHandle);  
```  
  
## <a name="arguments"></a>引数  
 *StatementHandle*  
 代入ステートメントハンドル。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_NO_DATA、SQL_STILL_EXECUTING、SQL_ERROR、または SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診断  
 **Sqlfetch**が SQL_ERROR または SQL_SUCCESS_WITH_INFO のいずれかを返す場合、SQL_HANDLE_STMT の*Handletype*と StatementHandle の*ハンドル*を指定して[SQLGetDiagRec Function](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)を呼び出すことによって、関連する SQLSTATE 値を取得できます。 次の表に、 **Sqlfetch**によって通常返される SQLSTATE 値と、この関数のコンテキストでのそれぞれについて説明します。"(DM)" という表記は、ドライバーマネージャーによって返される SQLSTATEs の説明の前にあります。 特に記載がない限り、各 SQLSTATE 値に関連付けられているリターンコードは SQL_ERROR です。 1つの列でエラーが発生した場合は、SQL_DIAG_COLUMN_NUMBER の*DiagIdentifier*を使用して[SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)を呼び出して、エラーが発生した列を特定することができます。と**SQLGetDiagField**は、 *DiagIdentifier*の SQL_DIAG_ROW_NUMBER を使用して呼び出すことで、その列を含む行を特定できます。  
  
 SQL_SUCCESS_WITH_INFO または SQL_ERROR を返すことができるすべての SQLSTATEs (01xxx SQLSTATEs を除く) では、複数行操作のすべての行ではなく、1つ以上の行でエラーが発生すると SQL_SUCCESS_WITH_INFO が返され、エラーが発生した場合は SQL_ERROR が返されます。単一行演算。  
  
|SQLSTATE|[エラー]|説明|  
|--------------|-----------|-----------------|  
|01000|一般警告|ドライバー固有の情報メッセージ。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|01004|文字列データ、右側が切り捨てられました|列に対して返された文字列またはバイナリデータにより、空白以外の文字または NULL 以外のバイナリデータが切り捨てられました。 文字列値の場合は、右側が切り捨てられました。|  
|01S01|行にエラーがあります|1つ以上の行をフェッチ中にエラーが発生しました。<br /><br /> (Odbc*2.x アプリケーションが*odbc*2.x ドライバーで*動作しているときにこの SQLSTATE が返された場合は、無視してかまいません)。|  
|01S07|小数部の切り捨て|列に対して返されたデータが切り捨てられました。 数値データ型の場合、数値の小数部は切り捨てられました。 時刻、タイムスタンプ、および期間のデータ型については、時間部分が含まれていますが、時間の小数部が切り捨てられました。<br /><br /> (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|07006|制限されたデータ型の属性違反|結果セットの列のデータ値を、 **SQLBindCol**の*TargetType*によって指定されたデータ型に変換できませんでした。<br /><br /> 列0は SQL_C_BOOKMARK のデータ型にバインドされており、SQL_ATTR_USE_BOOKMARKS statement 属性は SQL_UB_VARIABLE に設定されていました。<br /><br /> 列0は SQL_C_VARBOOKMARK のデータ型にバインドされていますが、SQL_ATTR_USE_BOOKMARKS statement 属性が SQL_UB_VARIABLE に設定されていません。|  
|07009|無効な記述子のインデックス|ドライバーは、 **SQLExtendedFetch**をサポートしていない ODBC*2.x ドライバーで*、列のバインドに指定された列番号が0でした。<br /><br /> 列0がバインドされ、SQL_ATTR_USE_BOOKMARKS statement 属性が SQL_UB_OFF に設定されました。|  
|08S01|通信リンクの失敗|関数が処理を完了する前に、ドライバーと、ドライバーが接続されていたデータソースとの間の通信リンクが失敗しました。|  
|22001|文字列データ、右側が切り捨てられました|列に対して返された可変長のブックマークが切り捨てられました。|  
|22002|インジケーター変数が必要ですが、指定されていません|NULL データが、 **SQLBindCol**によって設定された*StrLen_or_IndPtr* (または**SQLSetDescField**または**SQLSetDescRec**によって設定された SQL_DESC_INDICATOR_PTR) が null ポインターである列にフェッチされました。|  
|22003|数値が有効範囲にありません|1つ以上のバインドされた列の数値または文字列として数値を返すと、切り捨てられる数値の一部 (小数部分ではなく) が発生する可能性があります。<br /><br /> 詳細については、次を参照してください。[データを SQL から C データ型に変換](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)する付録 D:データ型。|  
|22007|無効な datetime 形式|結果セットの文字列が日付、時刻、またはタイムスタンプ C 構造体にバインドされました。列の値は、それぞれ無効な日付、時刻、またはタイムスタンプです。|  
|22012|0による除算|算術式からの値が返されました。この結果、0による除算が行われました。|  
|22015|間隔フィールドオーバーフロー|数値または期間の SQL 型から範囲 C 型への割り当てにより、先頭のフィールドの有効桁数が失われました。<br /><br /> データを interval C 型にフェッチする場合、interval C 型の SQL 型の値は表現されませんでした。|  
|22018|キャストの指定に無効な文字値があります|結果セットの文字列が文字 C バッファーにバインドされました。この列には、バッファーの文字セットに表現がなかった文字が含まれていました。<br /><br /> C 型は、正確な数値、概数、datetime、または interval データ型でした。列の SQL 型は文字データ型でした。列の値が、バインドされた C 型の有効なリテラルではありませんでした。|  
|24000|カーソル状態が無効|*StatementHandle*は実行状態でしたが、結果セットが*StatementHandle*に関連付けられていませんでした。|  
|40001|シリアル化エラー|フェッチが実行されたトランザクションは、デッドロックを防ぐために終了されました。|  
|40003|ステートメントの完了が不明です|この関数の実行中に関連付けられた接続に失敗しました。トランザクションの状態を確認できません。|  
|HY000|一般エラー|特定の SQLSTATE がなく、実装固有の SQLSTATE が定義されていないエラーが発生しました。 Messagetext バッファーの**SQLGetDiagRec によっ**て返されるエラーメッセージには、エラーとその原因が記述されています。  *\**|  
|HY001|メモリ割り当てエラー|ドライバーは、関数の実行または完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY008|操作が取り消されました|*StatementHandle*に対して非同期処理が有効になりました。 **Sqlfetch**関数が呼び出され、実行が完了する前に、 **SQLCancel**または**sqlcancelhandle**が*StatementHandle*で呼び出されました。 その後、 *StatementHandle*で**sqlfetch**関数が再度呼び出されました。<br /><br /> または、 **Sqlfetch**関数が呼び出され、実行が完了する前に、マルチスレッドアプリケーションの別のスレッドの*StatementHandle*で**SQLCancel**または**sqlcancelhandle**が呼び出されました。|  
|HY010|関数のシーケンスエラー|(DM) 非同期的に実行する関数が、 *StatementHandle*に関連付けられている接続ハンドルに対して呼び出されました。 この非同期関数は、 **Sqlfetch**関数が呼び出されたときにまだ実行されていました。<br /><br /> (DM) **Sqlexecute**、 **SQLExecDirect**、または**Sqlmoreresults**が*STATEMENTHANDLE*に対して呼び出され、SQL_PARAM_DATA_AVAILABLE が返されました。 この関数は、ストリーミングされたすべてのパラメーターのデータが取得される前に呼び出されました。<br /><br /> (DM) 指定された*StatementHandle*は実行状態ではありませんでした。 最初に**SQLExecDirect**、 **sqlexecute** 、または catalog 関数を呼び出さずに関数が呼び出されました。<br /><br /> (DM) 非同期的に実行されている関数 (この1つではない) が*StatementHandle*に対して呼び出され、この関数が呼び出されたときにまだ実行されています。<br /><br /> (DM) **Sqlexecute**、 **SQLExecDirect**、 **sqlbulkoperations**、または**SQLSetPos**が*StatementHandle*に対して呼び出され、SQL_NEED_DATA が返されました。 この関数は、実行時データのすべてのパラメーターまたは列に対してデータが送信される前に呼び出されました。<br /><br /> (DM) **SQLExtendedFetch**が呼び出された後、SQL_CLOSE オプションが呼び出さ**れる前に**、 *StatementHandle*に対して**sqlfetch**が呼び出されました。|  
|HY013|メモリ管理エラー|基になるメモリオブジェクトにアクセスできなかったため、関数呼び出しを処理できませんでした。メモリ不足の状態が原因である可能性があります。|  
|HY090|文字列またはバッファーの長さが無効です|SQL_ATTR_USE_BOOKMARK statement 属性が SQL_UB_VARIABLE に設定されました。列0は、長さがこの結果セットのブックマークの最大長と等しくないバッファーにバインドされています。 (この長さは IRD の SQL_DESC_OCTET_LENGTH フィールドにあり、 **SQLDescribeCol**、 **sqlcolattribute**、または**SQLGetDescField**を呼び出すことによって取得できます)。|  
|HY107|行の値が有効範囲にありません|SQL_ATTR_CURSOR_TYPE statement 属性で指定された値は SQL_CURSOR_KEYSET_DRIVEN でしたが、SQL_ATTR_KEYSET_SIZE statement 属性で指定された値は0より大きく、SQL_ATTR_ROW_ARRAY_ で指定された値よりも小さくなっています。SIZE ステートメントの属性。|  
|HY117|トランザクションの状態が不明なため、接続が中断されました。 切断と読み取り専用の機能のみが許可されます。|(DM) 中断状態の詳細については、「 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)」を参照してください。|  
|HYC00|省略可能な機能は実装されていません|ドライバーまたはデータソースが、 **SQLBindCol**の*TargetType*と対応する列の SQL データ型の組み合わせによって指定された変換をサポートしていません。|  
|HYT00|タイムアウトが発生しました|データソースが要求された結果セットを返す前に、クエリのタイムアウト期間が経過しました。 タイムアウト期間は、SQLSetStmtAttr、SQL_ATTR_QUERY_TIMEOUT によって設定されます。|  
|HYT01|接続タイムアウトの期限が切れました|データソースが要求に応答する前に、接続のタイムアウト期間が経過しました。 接続タイムアウト期間は、 **SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT によって設定されます。|  
|IM001|ドライバーはこの機能をサポートしていません|(DM) *StatementHandle*に関連付けられているドライバーでは、関数はサポートされていません。|  
|IM017|非同期通知モードでは、ポーリングは無効になっています|通知モデルが使用されるたびに、ポーリングは無効になります。|  
|IM018|**Sqlcompleteasync**は、このハンドルで前の非同期操作を完了するために呼び出されていません。|ハンドルに対する前の関数呼び出しで SQL_STILL_EXECUTING が返され、通知モードが有効になっている場合は、処理を完了するために、ハンドルで**Sqlcompleteasync**を呼び出して、操作を完了する必要があります。|  
  
## <a name="comments"></a>コメント  
 **Sqlfetch**は、結果セット内の次の行セットを返します。 結果セットが存在する場合にのみ呼び出すことができます。つまり、結果セットを作成する呼び出しの後、その結果セットのカーソルが閉じられる前に呼び出すことができます。 列がバインドされている場合は、それらの列のデータが返されます。 アプリケーションが、フェッチされた行の数を返す行の状態の配列またはバッファーへのポインターを指定した場合、 **Sqlfetch**はこの情報も返します。 **Sqlfetch**の呼び出しと**sqlfetchscroll**の呼び出しを混在させることはできますが、 **SQLExtendedFetch**の呼び出しと混在させることはできません。 詳細については、「[データ行のフェッチ](../../../odbc/reference/develop-app/fetching-a-row-of-data.md)」を参照してください。  
  
 Odbc*2.x アプリケーションが*odbc*2.x ドライバーで*動作する場合、ドライバーマネージャーは**SQLExtendedFetch**をサポートする odbc*2.X ドライバーの* **sqlfetch**呼び出しを**SQLExtendedFetch**にマップします。 ODBC*2.x ドライバーが* **SQLExtendedFetch**をサポートしていない場合、ドライバーマネージャーは**sqlfetch**呼び出しを odbc*2.x ドライバーの* **sqlfetch**にマップします。これにより、1つの行のみがフェッチされます。  
  
 詳細については、「付録 G:[ブロックカーソル、スクロール可能なカーソル、および旧バージョンとの互換性](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md)」を参照してください。旧バージョンとの互換性のためのドライバーガイドライン。  
  
## <a name="positioning-the-cursor"></a>カーソルの位置を指定する  
 結果セットが作成されると、カーソルが結果セットの先頭の前に配置されます。 **Sqlfetch**は次の行セットをフェッチします。 *Fetchorientation*を SQL_FETCH_NEXT に設定して**sqlfetchscroll**を呼び出すことと同じです。 カーソルの詳細については、「[カーソル](../../../odbc/reference/develop-app/cursors.md)と[ブロックカーソル](../../../odbc/reference/develop-app/block-cursors.md)」を参照してください。  
  
 SQL_ATTR_ROW_ARRAY_SIZE statement 属性は、行セット内の行の数を指定します。 **Sqlfetch**によってフェッチされる行セットが結果セットの末尾と重複する場合、 **sqlfetch**は部分的な行セットを返します。 つまり、S + R-1 が L よりも大きい場合 (S はフェッチされる行セットの開始行、R は行セットのサイズ、L は結果セットの最後の行)、行セットの最初の L-S + 1 行だけが有効です。 残りの行は空で、状態は SQL_ROW_NOROW です。  
  
 **Sqlfetch**が返された後、現在の行が行セットの最初の行になります。  
  
 次の表に示すルールは、このセクションの2番目の表に示す条件に基づいて、 **Sqlfetch**の呼び出し後のカーソル位置を示しています。  
  
|条件|新しい行セットの最初の行|  
|---------------|-----------------------------|  
|開始前|1|  
|*CurrRowsetStart*Lastresultrow-RowsetSize [1] \< = |CurrRowsetStart + *RowsetSize*[2]|  
|CurrRowsetStart > *lastresultrow-RowsetSize*[1]|終了後|  
|終了後|終了後|  
  
 [1] フェッチの間で行セットのサイズが変更された場合、これは前のフェッチで使用された行セットのサイズになります。  
  
 [2] フェッチ間で行セットのサイズが変更された場合、これは新しいフェッチで使用された行セットのサイズです。  
  
|Notation|説明|  
|--------------|-------------|  
|開始前|ブロックカーソルは、結果セットの先頭の前に配置されます。 新しい行セットの最初の行が結果セットの先頭より前にある場合、 **Sqlfetch**は SQL_NO_DATA を返します。|  
|終了後|ブロックカーソルは、結果セットの末尾の後に配置されます。 新しい行セットの最初の行が結果セットの末尾の後にある場合、 **Sqlfetch**は SQL_NO_DATA を返します。|  
|*CurrRowsetStart*|現在の行セットの最初の行の番号。|  
|*LastResultRow*|結果セットの最後の行の番号。|  
|*RowsetSize*|行セットのサイズ。|  
  
 たとえば、結果セットの行数が100で、行セットのサイズが5であるとします。 次の表は、さまざまな開始位置に対して**Sqlfetch**によって返される行セットとリターンコードを示しています。  
  
|現在の行セット|リターン コード|新しい行セット|フェッチされる行の数|  
|--------------------|-----------------|----------------|------------------------|  
|開始前|SQL_SUCCESS|1 ~ 5|5|  
|1 ~ 5|SQL_SUCCESS|6 ~ 10|5|  
|52 ~ 56|SQL_SUCCESS|57 ~ 61|5|  
|91 ~ 95|SQL_SUCCESS|96 ~ 100|5|  
|93 ~ 97|SQL_SUCCESS|98 ~ 100。 行の状態配列の行4および5は、SQL_ROW_NOROW に設定されています。|3|  
|96 ~ 100|SQL_NO_DATA|[なし] :|0|  
|99 ~ 100|SQL_NO_DATA|[なし] :|0|  
|終了後|SQL_NO_DATA|[なし] :|0|  
  
## <a name="returning-data-in-bound-columns"></a>バインドされた列のデータを返す  
 **Sqlfetch**は各行を返すため、その列にバインドされている各列のデータをバッファーに格納します。 列がバインドされていない場合、 **Sqlfetch**はデータを返しませんが、ブロックカーソルを前方に移動します。 **SQLGetData**を使用してデータを取得することもできます。 カーソルが複数行のカーソルの場合 (つまり、SQL_ATTR_ROW_ARRAY_SIZE が1より大きい場合)、 *InfoType*が SQL_GETDATA_EXTENSIONS で呼び出され**たときに**SQL_GD_BLOCK が返された場合にのみ、 **SQLGetData**を呼び出すことができます。 (詳細については、「 [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)」を参照してください)。  
  
 **Sqlfetch**は、行内のバインドされた列ごとに次のことを行います。  
  
1.  長さ/インジケーターバッファーを SQL_NULL_DATA に設定し、データが NULL の場合は次の列に進みます。 データが NULL で、長さ/インジケーターバッファーがバインドされていない場合、 **Sqlfetch**は、行の SQLSTATE 22002 (必要であるが指定されていないインジケーター変数) を返し、次の行に進みます。 長さ/インジケーターバッファーのアドレスを確認する方法の詳細については、 [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)の「buffer Addresses」を参照してください。  
  
     列のデータが NULL でない場合、 **Sqlfetch**は手順2に進みます。  
  
2.  SQL_ATTR_MAX_LENGTH statement 属性が0以外の値に設定されていて、列に文字またはバイナリデータが含まれている場合、データは SQL_ATTR_MAX_LENGTH バイトに切り捨てられます。  
  
    > [!NOTE]  
    >  SQL_ATTR_MAX_LENGTH statement 属性は、ネットワークトラフィックを減らすことを目的としています。 通常、データソースによって実装されます。これにより、データはネットワーク経由で返される前に切り捨てられます。 ドライバーとデータソースは、それをサポートするためには必要ありません。 したがって、データが特定のサイズに切り捨てられることを保証するために、アプリケーションでは、そのサイズのバッファーを割り当て、 **SQLBindCol**の*cbValueMax*引数にサイズを指定する必要があります。  
  
3.  **SQLBindCol**の*TargetType*によって指定された型にデータを変換します。  
  
4.  データが文字やバイナリなどの可変長データ型に変換された場合、 **Sqlfetch**はデータの長さがデータバッファーの長さを超えているかどうかをチェックします。 文字データの長さ (null 終端文字を含む) がデータバッファーの長さを超えている場合、 **Sqlfetch**はデータを null 終端文字の長さより短いデータバッファーの長さに切り捨てます。 その後、データを null で終了します。 バイナリデータの長さがデータバッファーの長さを超える場合、 **Sqlfetch**はそれをデータバッファーの長さに切り捨てます。 データバッファーの長さは、 **SQLBindCol**で*bufferlength*を使用して指定します。  
  
     **Sqlfetch**は、固定長データ型に変換されたデータを切り捨てません。データバッファーの長さがデータ型のサイズであることが常に想定されます。  
  
5.  変換された (場合によっては切り捨てられた) データをデータバッファーに配置します。 データバッファーのアドレスを確認する方法の詳細については、 [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)の「buffer Addresses」を参照してください。  
  
6.  長さ/インジケーターバッファーにデータの長さを格納します。 インジケーターポインターと長さポインターが両方とも ( **SQLBindCol**の呼び出しとして) 同じバッファーに設定されている場合、有効なデータの長さがバッファーに書き込まれ、SQL_NULL_DATA が NULL データ用のバッファーに書き込まれます。 長さ/インジケーターバッファーがバインドされていない場合、 **Sqlfetch**は長さを返しません。  
  
    -   文字またはバイナリデータの場合、これは変換後のデータの長さであり、データバッファーが小さすぎるために切り捨てが行われます。 変換後にドライバーがデータの長さを決定できない場合は、長いデータの場合と同様に、長さを SQL_NO_TOTAL に設定します。 SQL_ATTR_MAX_LENGTH statement 属性によってデータが切り捨てられた場合、この属性の値は実際の長さではなく、長さ/インジケーターバッファーに格納されます。 これは、この属性は変換前にサーバー上のデータを切り捨てるように設計されているため、ドライバーが実際の長さを判断する方法がないためです。  
  
    -   他のすべてのデータ型については、変換後のデータの長さです。つまり、データが変換された型のサイズです。  
  
     長さ/インジケーターバッファーのアドレスを確認する方法の詳細については、 [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)の「buffer Addresses」を参照してください。  
  
7.  データが変換中に切り捨てられ、有効桁数が失われた場合 (たとえば、変換時に実数1.234 が整数1に切り捨てられた場合)、 **Sqlfetch**は SQLSTATE 01S07 (小数の切り捨て) と SQL_SUCCESS_WITH_INFO を返します。 データバッファーの長さが小さすぎるためにデータが切り捨てられた場合 (たとえば、文字列 "abcdef" が4バイトのバッファーに格納されている場合)、 **Sqlfetch**は SQLSTATE 01004 (データが切り捨てられました) と SQL_SUCCESS_WITH_INFO を返します。 SQL_ATTR_MAX_LENGTH statement 属性によってデータが切り捨てられた場合、 **Sqlfetch**は SQL_SUCCESS を返し、sqlstate 01S07 (小数部の切り捨て) または sqlstate 01004 (データの切り捨て) を返しません。 有効桁数の損失による変換中にデータが切り捨てられた場合 (たとえば、10万より大きい SQL_INTEGER 値が SQL_C_TINYINT に変換された場合)、 **Sqlfetch**は SQLSTATE 22003 (数値の範囲外) と SQL_ERROR (行セットのサイズが 1) または SQL_SUCCESS_WITH_INFO (行セットのサイズが1より大きい場合)。  
  
 **Sqlfetch**または**SQLFETCHSCROLL**が SQL_SUCCESS または SQL_SUCCESS_WITH_INFO を返さない場合、バインドされたデータバッファーと長さ/インジケーターバッファーの内容は未定義になります。  
  
## <a name="row-status-array"></a>行の状態の配列  
 行の状態の配列は、行セットの各行の状態を返すために使用されます。 この配列のアドレスは、SQL_ATTR_ROW_STATUS_PTR statement 属性で指定します。 配列は、アプリケーションによって割り当てられ、SQL_ATTR_ROW_ARRAY_SIZE statement 属性で指定された数の要素を持つ必要があります。 この値は、 **Sqlfetch**、 **sqlfetchscroll**、および**Sqlbulkoperations**または**SQLSetPos**によって設定されます (カーソルが**SQLExtendedFetch**によって配置された後に呼び出された場合を除く)。 SQL_ATTR_ROW_STATUS_PTR statement 属性の値が null ポインターの場合、これらの関数は行の状態を返しません。  
  
 **Sqlfetch**または**SQLFETCHSCROLL**が SQL_SUCCESS または SQL_SUCCESS_WITH_INFO を返さない場合、行ステータス配列バッファーの内容は未定義になります。  
  
 次の値が行の状態配列に返されます。  
  
|行の状態の配列値|説明|  
|----------------------------|-----------------|  
|SQL_ROW_SUCCESS|行は正常にフェッチされました。この行は、この結果セットから最後にフェッチされてから変更されていません。|  
|SQL_ROW_SUCCESS_WITH_INFO|行は正常にフェッチされました。この行は、この結果セットから最後にフェッチされてから変更されていません。 ただし、行に関する警告が返されました。|  
|SQL_ROW_ERROR|行のフェッチ中にエラーが発生しました。|  
|SQL_ROW_UPDATED [1]、[2]、[3]|行は正常にフェッチされました。この行は、この結果セットから最後にフェッチされてから変更されています。 行がこの結果セットから再びフェッチされた場合、または**SQLSetPos**によって更新された場合、状態は行の新しい状態に変わります。|  
|SQL_ROW_DELETED[3]|この行は、この結果セットから最後にフェッチされてから削除されています。|  
|SQL_ROW_ADDED[4]|行は**Sqlbulkoperations**によって挿入されました。 行がこの結果セットから再びフェッチされた場合、または**SQLSetPos**によって更新された場合、その状態は SQL_ROW_SUCCESS になります。|  
|SQL_ROW_NOROW|行セットには、結果セットの末尾が重なっています。行の状態配列のこの要素にこれする行は返されませんでした。|  
  
 [1] キーセット、混合、および動的カーソルの場合、キー値が更新されると、データ行は削除され、新しい行が追加されたと見なされます。  
  
 [2] 一部のドライバーがデータの更新を検出できないため、この値を返すことができません。 ドライバーが refetched 行の更新を検出できるかどうかを判断するには、アプリケーションは SQL_ROW_UPDATES オプションを使用して**SQLGetInfo**を呼び出します。  
  
 [3] **Sqlfetch**は、 **sqlfetchscroll**の呼び出しが混在している場合にのみ、この値を返すことができます。 これは、 **Sqlfetch**は結果セットを前方に移動し、排他的に使用されている場合は行を再フェッチません。 行が既にフェッチされていないため、 **Sqlfetch**は以前にフェッチされた行に対して行われた変更を検出しません。 ただし、以前にフェッチされた行と**Sqlfetch**を使用して行をフェッチする前に、 **sqlfetchscroll**がカーソルを移動すると、それらの行に対する変更が**sqlfetch**によって検出されます。  
  
 [4] SQLBulkOperations によってのみ返されます。 **Sqlfetch**または**sqlfetchscroll**では設定されません。  
  
### <a name="rows-fetched-buffer"></a>フェッチされる行のバッファー  
 フェッチされた行数は、フェッチ中にエラーが発生したためにデータが返されなかった行も含めて、フェッチされた行の数を返すために使用されます。 つまり、行の状態配列の値が SQL_ROW_NOROW されていない行の数です。 このバッファーのアドレスは、SQL_ATTR_ROWS_FETCHED_PTR statement 属性で指定します。 バッファーは、アプリケーションによって割り当てられます。 これは**Sqlfetch**および**sqlfetchscroll**によって設定されます。 SQL_ATTR_ROWS_FETCHED_PTR statement 属性の値が null ポインターの場合、これらの関数はフェッチされた行の数を返しません。 アプリケーションでは、結果セット内の現在の行の数を確認するために、SQL_ATTR_ROW_NUMBER 属性を使用して**SQLGetStmtAttr**を呼び出すことができます。  
  
 フェッチされた行の内容は、 **Sqlfetch**または**SQLFETCHSCROLL**が SQL_SUCCESS または SQL_SUCCESS_WITH_INFO を返さない場合には未定義です。ただし、SQL_NO_DATA が返された場合は、フェッチされたバッファーの行の値が0に設定されます。  
  
### <a name="error-handling"></a>エラー処理  
 エラーと警告は、個々の行または関数全体に適用できます。 診断レコードの詳細については、「[診断](../../../odbc/reference/develop-app/diagnostics.md)と[SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)」を参照してください。  
  
#### <a name="errors-and-warnings-on-the-entire-function"></a>関数全体のエラーと警告  
 SQLSTATE HYT00 (タイムアウト期限切れ) や SQLSTATE 24000 (無効なカーソル状態) などの関数全体にエラーが適用された場合、 **Sqlfetch**は SQL_ERROR および該当する sqlstate を返します。 行セットバッファーの内容は未定義で、カーソル位置は変更されません。  
  
 関数全体に警告が適用された場合、 **Sqlfetch**は SQL_SUCCESS_WITH_INFO および該当する SQLSTATE を返します。 関数全体に適用される警告の状態レコードは、個々の行に適用される状態レコードの前に返されます。  
  
#### <a name="errors-and-warnings-in-individual-rows"></a>個々の行のエラーと警告  
 エラー (SQLSTATE 22012 (0 除算) など) または警告 (SQLSTATE 01004 (データの切り捨て) など) が1つの行に適用される場合、 **Sqlfetch**は次のことを行います。  
  
-   行状態配列の対応する要素を SQL_ROW_ERROR に設定します。エラーの場合は SQL_ROW_SUCCESS_WITH_INFO、警告の場合はに設定します。  
  
-   エラーまたは警告の SQLSTATEs を含む0個以上の状態レコードを追加します。  
  
-   状態レコード内の行と列の番号フィールドを設定します。 **Sqlfetch**が行または列の番号を特定できない場合は、その数値を SQL_ROW_NUMBER_UNKNOWN または SQL_COLUMN_NUMBER_UNKNOWN にそれぞれ設定します。 状態レコードが特定の列に適用されない場合、 **Sqlfetch**は列番号を SQL_NO_COLUMN_NUMBER に設定します。  
  
 **Sqlfetch**は、行セット内のすべての行がフェッチされるまで、行のフェッチを続行します。 行セットのすべての行でエラーが発生した場合 (status SQL_ROW_NOROW の行は含まない)、SQL_SUCCESS_WITH_INFO が返されます。この場合、SQL_ERROR が返されます。 特に、行セットのサイズが1で、その行でエラーが発生した場合、 **Sqlfetch**は SQL_ERROR を返します。  
  
 **Sqlfetch**は、行番号の順序で状態レコードを返します。 つまり、不明な行 (存在する場合) のすべての状態レコードが返されます。次に、最初の行 (存在する場合) のすべての状態レコードを返し、2番目の行 (存在する場合) のすべてのステータスレコードを返します。 各行の状態レコードは、ステータスレコードの順序付けに関する通常のルールに従って並べ替えられます。詳細については、 [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)の「状態レコードのシーケンス」を参照してください。  
  
### <a name="descriptors-and-sqlfetch"></a>記述子と SQLFetch  
 以下のセクションでは、 **Sqlfetch**が記述子と対話する方法について説明します。  
  
#### <a name="argument-mappings"></a>引数のマッピング  
 ドライバーは、 **Sqlfetch**の引数に基づいて記述子フィールドを設定しません。  
  
#### <a name="other-descriptor-fields"></a>その他の記述子フィールド  
 **Sqlfetch**では、次の記述子フィールドが使用されます。  
  
|記述子フィールド|順.|のフィールド|設定|  
|----------------------|-----------|--------------|-----------------|  
|SQL_DESC_ARRAY_SIZE|ブロ|項目|SQL_ATTR_ROW_ARRAY_SIZE statement 属性|  
|SQL_DESC_ARRAY_STATUS_PTR|IRD|項目|SQL_ATTR_ROW_STATUS_PTR statement 属性|  
|SQL_DESC_BIND_OFFSET_PTR|ブロ|項目|SQL_ATTR_ROW_BIND_OFFSET_PTR statement 属性|  
|SQL_DESC_BIND_TYPE|ブロ|項目|SQL_ATTR_ROW_BIND_TYPE statement 属性|  
|SQL_DESC_COUNT|ブロ|項目|**SQLBindCol**の*columnnumber*引数|  
|SQL_DESC_DATA_PTR|ブロ|レコード|**SQLBindCol**の*targetvalueptr*引数|  
|SQL_DESC_INDICATOR_PTR|ブロ|レコード|**SQLBindCol**の*StrLen_or_IndPtr*引数|  
|SQL_DESC_OCTET_LENGTH|ブロ|レコード|**SQLBindCol**の*bufferlength*引数|  
|SQL_DESC_OCTET_LENGTH_PTR|ブロ|レコード|**SQLBindCol**の*StrLen_or_IndPtr*引数|  
|SQL_DESC_ROWS_PROCESSED_PTR|IRD|項目|SQL_ATTR_ROWS_FETCHED_PTR statement 属性|  
|SQL_DESC_TYPE|ブロ|レコード|**SQLBindCol**の*TargetType*引数|  
  
 すべての記述子フィールドは、 **SQLSetDescField**を使用して設定することもできます。  
  
#### <a name="separate-length-and-indicator-buffers"></a>長さとインジケーターバッファーを分離する  
 アプリケーションでは、長さとインジケーターの値を保持するために使用できる1つのバッファーまたは2つの個別のバッファーをバインドできます。 アプリケーションが**SQLBindCol**を呼び出すと、ドライバーは、の SQL_DESC_OCTET_LENGTH_PTR および SQL_DESC_INDICATOR_PTR フィールドを同じアドレスに設定します。このアドレスは*StrLen_or_IndPtr*引数で渡されます。 アプリケーションが**SQLSetDescField**または**SQLSetDescRec**を呼び出すと、これらの2つのフィールドを異なるアドレスに設定できます。  
  
 **Sqlfetch**は、アプリケーションで個別の長さとインジケーターバッファーが指定されているかどうかを判断します。 この場合、データが NULL でない場合、 **Sqlfetch**はインジケーターバッファーを0に設定し、長さバッファーの長さを返します。 データが NULL の場合、 **Sqlfetch**はインジケーターバッファーを SQL_NULL_DATA に設定し、長さバッファーを変更しません。  
  
### <a name="code-example"></a>コード例  
 「 [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)、 [sqlcolumns](../../../odbc/reference/syntax/sqlcolumns-function.md)、 [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)、および[sqlcolumns](../../../odbc/reference/syntax/sqlprocedures-function.md)」を参照してください。  
  
### <a name="related-functions"></a>関連する関数  
  
|詳細|参照先|  
|---------------------------|---------|  
|結果セット内の列へのバッファーのバインド|[SQLBindCol 関数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|ステートメント処理の取り消し|[SQLCancel 関数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|結果セットの列に関する情報を返す|[SQLDescribeCol 関数](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|SQL ステートメントの実行|[SQLExecDirect 関数](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|準備された SQL ステートメントの実行|[SQLExecute 関数](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|データのブロックのフェッチまたは結果セットのスクロール|[SQLFetchScroll 関数](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|ステートメントでカーソルを閉じる|[SQLFreeStmt 関数](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|データ列の一部またはすべてをフェッチしています|[SQLGetData 関数](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
|結果セットの列数を返す|[SQLNumResultCols 関数](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
|実行するステートメントの準備|[SQLPrepare 関数](../../../odbc/reference/syntax/sqlprepare-function.md)|  
  
## <a name="see-also"></a>参照  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)
