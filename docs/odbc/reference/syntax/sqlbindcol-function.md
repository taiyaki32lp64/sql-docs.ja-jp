---
title: SQLBindCol 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLBindCol
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLBindCol
helpviewer_keywords:
- SQLBindCol function [ODBC]
ms.assetid: 41a37655-84cd-423f-9daa-e0b47b88dc54
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c1c89ff79ee0fcac37f7b6e231e957e051c9db2e
ms.sourcegitcommit: 43c3d8939f6f7b0ddc493d8e7a643eb7db634535
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2019
ms.locfileid: "72289287"
---
# <a name="sqlbindcol-function"></a>SQLBindCol 関数
**互換性**  
 導入されたバージョン: ODBC 1.0 標準準拠: ISO 92  
  
 **概要**  
 **SQLBindCol**は、アプリケーションデータバッファーを結果セットの列にバインドします。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLBindCol(  
      SQLHSTMT       StatementHandle,  
      SQLUSMALLINT   ColumnNumber,  
      SQLSMALLINT    TargetType,  
      SQLPOINTER     TargetValuePtr,  
      SQLLEN         BufferLength,  
      SQLLEN *       StrLen_or_Ind);  
```  
  
## <a name="arguments"></a>引数  
 *StatementHandle*  
 代入ステートメントハンドル。  
  
 *ColumnNumber*  
 代入バインドする結果セット列の番号。 列には、列の順序が0から始まるように番号が付けられます。ここで、column 0 はブックマーク列です。 ブックマークが使用されていない場合 (つまり、SQL_ATTR_USE_BOOKMARKS statement 属性が SQL_UB_OFF に設定されている場合、列番号は1から始まります。  
  
 *TargetType*  
 代入\**Targetvalueptr*バッファーの C データ型の識別子。 データソースから**Sqlfetch**、 **sqlfetchscroll**、 **Sqlbulkoperations**、または**SQLSetPos**を使用してデータを取得する場合、ドライバーはデータをこの型に変換します。**Sqlbulkoperations**または**SQLSetPos**を使用してデータをデータソースに送信すると、ドライバーはこの型からデータを変換します。 有効な C データ型と型識別子の一覧については、「付録 D: データ型」の「 [c データ型](../../../odbc/reference/appendixes/c-data-types.md)」を参照してください。  
  
 *TargetType*引数が interval データ型の場合、既定の間隔の有効桁数 (2) と既定の間隔の秒の有効桁数 (6) が、それぞれのの SQL_DESC_DATETIME_INTERVAL_PRECISION および SQL_DESC_PRECISION の各フィールドに設定されています。 *TargetType*引数が SQL_C_NUMERIC 場合は、既定の有効桁数 (ドライバー定義) と既定の小数点以下桁数 (0) が使用されます。この値は、SQL_DESC_PRECISION および SQL_DESC_SCALE のフィールドで設定されます。 既定の有効桁数または小数点以下桁数が適切でない場合、アプリケーションは、 **SQLSetDescField**または**SQLSetDescRec**の呼び出しによって適切な記述子フィールドを明示的に設定する必要があります。  
  
 拡張 C データ型を指定することもできます。 詳細については、「 [ODBC の C データ型](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)」を参照してください。  
  
 *TargetValuePtr*  
 [遅延入力/出力]列にバインドするデータバッファーへのポインター。 **Sqlfetch**および**sqlfetchscroll**は、このバッファー内のデータを返します。 **Sqlbulkoperations**は、*操作*が SQL_FETCH_BY_BOOKMARK 場合にこのバッファーのデータを返します。*操作*が SQL_ADD または SQL_UPDATE_BY_BOOKMARK たときに、このバッファーからデータを取得します。 **SQLSetPos**は、*操作*が SQL_REFRESH 場合にこのバッファー内のデータを返します。*操作*が SQL_UPDATE されたときに、このバッファーからデータを取得します。  
  
 *Targetvalueptr*が null ポインターの場合、ドライバーは列のデータバッファーをバインド解除します。 アプリケーションでは、SQL_UNBIND オプションを指定して**SQLFreeStmt**を呼び出すことによって、すべての列のバインドを解除できます。 **SQLBindCol**への呼び出しの*targetvalueptr*引数が null ポインターでも、 *StrLen_or_IndPtr*引数が有効な値である場合、アプリケーションは、列のデータバッファーのバインドを解除できますが、長さ/インジケーターバッファーが列にバインドされていてもかまいません。  
  
 *BufferLength*  
 代入\**Targetvalueptr*バッファーの長さ (バイト単位)。  
  
 ドライバーを使用して*BufferLength*の末尾を越えて書き込みを回避するために、 \* *TargetValuePtr* 文字またはバイナリ データなどの可変長データが返されるときにバッファーします。 ドライバーが文字データが返されるときに、null 終端文字がカウントされることを確認\* *TargetValuePtr* します。 \**TargetValuePtr* スペースを含める必要がありますので、null 終了文字またはドライバーにデータを切り捨てるの。  
  
 ドライバーが整数や日付構造などの固定長データを返す場合、ドライバーは*Bufferlength*を無視し、バッファーがデータを保持するのに十分な大きさであると想定します。 このため、アプリケーションで固定長データ用に十分な大きさのバッファーを割り当てることが重要です。または、ドライバーがバッファーの末尾を越えて書き込みを行います。  
  
 *Bufferlength が 0*未満の場合、 **SQLBINDCOL**は SQLSTATE HY090 (無効な文字列またはバッファー長) を返しますが、 *bufferlength*が0のときは返されません。 ただし、 *TargetType*が文字型を指定する場合は、アプリケーションで*bufferlength*を0に設定しないでください。この場合、ISO CLI 準拠のドライバーは SQLSTATE HY090 (無効な文字列またはバッファー長) を返します。  
  
 *StrLen_or_IndPtr*  
 [遅延入力/出力]列にバインドする長さ/インジケーターバッファーへのポインター。 **Sqlfetch**および**sqlfetchscroll**は、このバッファー内の値を返します。 **Sqlbulkoperations** *操作*が SQL_ADD、SQL_UPDATE_BY_BOOKMARK、または SQL_DELETE_BY_BOOKMARK の場合、このバッファーから値を取得します。 *操作*が SQL_FETCH_BY_BOOKMARK されると、 **sqlbulkoperations**はこのバッファー内の値を返します。 **SQLSetPos**は、*操作*が SQL_REFRESH 場合にこのバッファー内の値を返します。*操作*が SQL_UPDATE 場合、このバッファーから値を取得します。  
  
 **Sqlfetch**、 **sqlfetchscroll**、 **Sqlbulkoperations**、および**SQLSetPos**は、長さ/インジケーターバッファー内の次の値を返すことができます。  
  
-   返すことができるデータの長さ  
  
-   SQL_NO_TOTAL  
  
-   SQL_NULL_DATA  
  
 アプリケーションでは、 **Sqlbulkoperations**または**SQLSetPos**で使用するために、長さ/インジケーターバッファーに次の値を配置できます。  
  
-   送信されるデータの長さ  
  
-   SQL_NTS  
  
-   SQL_NULL_DATA  
  
-   SQL_DATA_AT_EXEC  
  
-   SQL_LEN_DATA_AT_EXEC マクロの結果  
  
-   SQL_COLUMN_IGNORE  
  
 インジケーターバッファーと長さバッファーが個別のバッファーの場合、インジケーターバッファーは SQL_NULL_DATA のみを返すことができますが、長さのバッファーは他のすべての値を返すことができます。  
  
 詳細については、次を参照してください[SQLBulkOperations 関数](../../../odbc/reference/syntax/sqlbulkoperations-function.md)、 [SQLFetch 関数](../../../odbc/reference/syntax/sqlfetch-function.md)、 [SQLSetPos 関数](../../../odbc/reference/syntax/sqlsetpos-function.md)、および[長さ/インジケーター値を使用する](../../../odbc/reference/develop-app/using-length-and-indicator-values.md)。  
  
 *StrLen_or_IndPtr*が null ポインターの場合、長さまたはインジケーターの値は使用されません。 これはデータをフェッチするときにエラーになり、データは NULL になります。  
  
 アプリケーションが64ビットのオペレーティングシステムで実行される場合は、「 [ODBC 64 ビット情報](../../../odbc/reference/odbc-64-bit-information.md)」を参照してください。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR、または SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診断  
 **SQLBindCol**が SQL_ERROR または SQL_SUCCESS_WITH_INFO を返す場合、関連付けられた SQLSTATE 値を取得するには、 *Handletype* SQL_HANDLE_STMT と*StatementHandle*の*ハンドル*を指定して**SQLGetDiagRec**を呼び出します。 次の表に、 **SQLBindCol**によって通常返される SQLSTATE 値と、この関数のコンテキストでのそれぞれについて説明します。"(DM)" という表記は、ドライバーマネージャーによって返される SQLSTATEs の説明の前にあります。 特に記載がない限り、各 SQLSTATE 値に関連付けられているリターンコードは SQL_ERROR ます。  
  
|SQLSTATE|エラー|[説明]|  
|--------------|-----------|-----------------|  
|01000|一般警告|ドライバー固有の情報メッセージ。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|07006|制限されたデータ型の属性違反|(DM) *Columnnumber*引数が0で、 *TargetType*引数が SQL_C_BOOKMARK または SQL_C_VARBOOKMARK ではありませんでした。|  
|07009|無効な記述子のインデックス|引数*Columnnumber*に指定された値が、結果セット内の列の最大数を超えました。|  
|HY000|一般エラー|特定の SQLSTATE がなく、実装固有の SQLSTATE が定義されていないエラーが発生しました。 *\*MessageText*バッファー内の**SQLGetDiagRec**によって返されるエラーメッセージには、エラーとその原因が記述されています。|  
|HY001|メモリ割り当てエラー|ドライバーは、関数の実行または完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY003|アプリケーションバッファーの種類が無効です|引数*TargetType*は、有効なデータ型でも SQL_C_DEFAULT でもありませんでした。|  
|HY010|関数のシーケンスエラー|(DM) 非同期的に実行する関数が、 *StatementHandle*に関連付けられている接続ハンドルに対して呼び出されました。 この非同期関数は、 **SQLBindCol**が呼び出されたときにまだ実行されていました。<br /><br /> (DM) **Sqlexecute**、 **SQLExecDirect**、または**Sqlmoreresults**が*StatementHandle*に対して呼び出され、SQL_PARAM_DATA_AVAILABLE が返されました。 この関数は、ストリーミングされたすべてのパラメーターのデータが取得される前に呼び出されました。<br /><br /> (DM) 非同期的に実行する関数が*StatementHandle*に対して呼び出されましたが、この関数が呼び出されたときにまだ実行されていました。<br /><br /> (DM) **Sqlexecute**、 **SQLExecDirect**、 **Sqlbulkoperations**、 **SQLSetPos**が*StatementHandle*に対して呼び出され、SQL_NEED_DATA が返されました。 この関数は、実行時データのすべてのパラメーターまたは列に対してデータが送信される前に呼び出されました。|  
|HY013|メモリ管理エラー|基になるメモリオブジェクトにアクセスできなかったため、関数呼び出しを処理できませんでした。メモリ不足の状態が原因である可能性があります。|  
|HY090|文字列またはバッファーの長さが無効です|(DM) 引数*Bufferlength*に指定された値が0未満でした。<br /><br /> (DM) ドライバーは ODBC 2 でした。*x*ドライバー、 *columnnumber*引数が0に設定されています。また、引数*bufferlength*に指定された値が4ではありませんでした。|  
|HY117|トランザクションの状態が不明なため、接続が中断されました。 切断と読み取り専用の機能のみが許可されます。|(DM) 中断状態の詳細については、「 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)」を参照してください。|  
|HYC00|省略可能な機能は実装されていません|ドライバーまたはデータソースが、 *TargetType*引数と、対応する列のドライバー固有の SQL データ型の組み合わせによって指定された変換をサポートしていません。<br /><br /> 引数*Columnnumber*が0で、ドライバーがブックマークをサポートしていません。<br /><br /> ドライバーは ODBC 2 だけをサポートします。*x*と引数*TargetType*は、次のいずれかでした。<br /><br /> SQL_C_NUMERIC SQL_C_SBIGINT SQL_C_UBIGINT<br /><br /> また、「付録 D: データ型」の[c データ型](../../../odbc/reference/appendixes/c-data-types.md)に示されているすべての interval c データ型についても説明します。<br /><br /> ドライバーがサポートしているのは3.50 より前のバージョンの ODBC のみで、引数*TargetType*は SQL_C_GUID。|  
|HYT01|接続タイムアウトの期限が切れました|データソースが要求に応答する前に、接続のタイムアウト期間が経過しました。 接続タイムアウト期間は、 **SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT によって設定されます。|  
|IM001|ドライバーはこの機能をサポートしていません|(DM) *StatementHandle*に関連付けられているドライバーでは、関数はサポートされていません。|  
  
## <a name="comments"></a>コメント  
 **SQLBindCol**は、結果セット内の列を、アプリケーションのデータバッファーと長さ/インジケーターバッファーに関連付ける、または*バインド*するために使用されます。 アプリケーションが**Sqlfetch**、 **sqlfetchscroll**、または**SQLSetPos**を呼び出してデータをフェッチすると、ドライバーは、指定されたバッファー内のバインドされた列のデータを返します。詳細については、「 [Sqlfetch 関数](../../../odbc/reference/syntax/sqlfetch-function.md)」を参照してください。 アプリケーションが**Sqlbulkoperations**を呼び出して行を更新または挿入する**ときに行**を更新する場合、ドライバーは、指定されたバッファーからバインドされた列のデータを取得します。詳細については、「 [Sqlbulkoperations 関数](../../../odbc/reference/syntax/sqlbulkoperations-function.md)」または「 [SQLSetPos 関数](../../../odbc/reference/syntax/sqlsetpos-function.md)」を参照してください。 バインディングの詳細については、「[結果の取得 (基本)](../../../odbc/reference/develop-app/retrieving-results-basic.md)」を参照してください。  
  
 列からデータを取得するために、列をバインドする必要はないことに注意してください。 アプリケーションでは、 **SQLGetData**を呼び出して列からデータを取得することもできます。 行の一部の列をバインドし、他の列に対して**SQLGetData**を呼び出すこともできますが、これにはいくつかの制限があります。 詳細については、「 [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)」を参照してください。  
  
## <a name="binding-unbinding-and-rebinding-columns"></a>列のバインド、バインド解除、および再バインド  
 データが結果セットからフェッチされた後でも、いつでも列をバインド、バインド解除、または再バインドできます。 新しいバインドは、次にバインドを使用する関数が呼び出されたときに有効になります。 たとえば、アプリケーションが結果セットの列をバインドし、 **Sqlfetch**を呼び出すとします。 ドライバーは、バインドされたバッファー内のデータを返します。 ここで、アプリケーションが列を別のバッファーのセットにバインドするとします。 ドライバーは、新しくバインドされたバッファーにのみ、フェッチされた行のデータを格納しません。 代わりに、 **Sqlfetch**が再度呼び出されるまで待機し、次の行のデータを新たにバインドされたバッファーに配置します。  
  
> [!NOTE]  
>  ステートメント属性 SQL_ATTR_USE_BOOKMARKS は、列を列0にバインドする前に常に設定する必要があります。 これは必須ではありませんが、強くお勧めします。  
  
## <a name="binding-columns"></a>バインディング列  
 列をバインドするには、アプリケーションは**SQLBindCol**を呼び出し、データバッファーの列番号、型、アドレス、および長さと、長さ/インジケーターバッファーのアドレスを渡します。 これらのアドレスの使用方法の詳細については、このセクションの後の「バッファーアドレス」を参照してください。 列のバインドの詳細については、「 [Using SQLBindCol](../../../odbc/reference/develop-app/using-sqlbindcol.md)」を参照してください。  
  
 これらのバッファーの使用は遅延されます。つまり、アプリケーションは**SQLBindCol**でそれらをバインドしますが、ドライバーは他の機能 ( **sqlbulkoperations**、 **sqlfetch**、 **sqlbulkoperations**、 **SQLSetPos**) からそれらにアクセスします。 **SQLBindCol**で指定されたポインターが有効なままであることを確認する必要があります。 アプリケーションでこれらのポインターが無効になることが許可されている場合 (たとえば、バッファーを解放し、それらのポインターが有効であると想定している関数を呼び出す場合)、結果は未定義になります。 詳細については、「[遅延バッファー](../../../odbc/reference/develop-app/deferred-buffers.md)」を参照してください。  
  
 バインドは、新しいバインドによって置き換えられるか、列がバインド解除されるか、ステートメントが解放されるまで有効です。  
  
## <a name="unbinding-columns"></a>列のバインド解除  
 1つの列のバインドを解除するには、アプリケーションは*Columnnumber*をその列の数に設定し、 *targetvalueptr*を null ポインターに設定して**SQLBindCol**を呼び出します。 *Columnnumber*がバインドされていない列を参照している場合、 **SQLBindCol**は引き続き SQL_SUCCESS を返します。  
  
 すべての列のバインドを解除するために、アプリケーションは*Foption*を SQL_UNBIND に設定して**SQLFreeStmt**を呼び出します。 これは、の [SQL_DESC_COUNT] フィールドをゼロに設定することによっても実現できます。  
  
## <a name="rebinding-columns"></a>列の再バインド  
 アプリケーションでは、次の2つの操作のいずれかを実行して、バインドを変更できます。  
  
-   **SQLBindCol**を呼び出して、既にバインドされている列の新しいバインドを指定します。 ドライバーは、古いバインディングを新しいもので上書きします。  
  
-   **SQLBindCol**へのバインド呼び出しで指定されたバッファーアドレスに追加するオフセットを指定します。 詳細については、次のセクション「バインドオフセット」を参照してください。  
  
## <a name="binding-offsets"></a>バインド (オフセットを)  
 バインドオフセットは、逆参照される前に、( *Targetvalueptr*および*StrLen_or_IndPtr*引数で指定された) データと長さ/インジケーターバッファーのアドレスに追加される値です。 オフセットが使用されている場合、バインドはアプリケーションのバッファーのレイアウト方法の "テンプレート" です。アプリケーションは、オフセットを変更することによって、この "テンプレート" を別のメモリ領域に移動できます。 各バインドの各アドレスに同じオフセットが追加されるため、異なる列のバッファー間の相対オフセットは、バッファーの各セット内で同じである必要があります。 これは、行方向のバインドを使用する場合は常に true です。列方向のバインドが使用されている場合は、アプリケーションでバッファーを十分にレイアウトする必要があります。  
  
 バインドオフセットを使用すると、 **SQLBindCol**を呼び出すことによって列を再バインドするのと基本的に同じ効果があります。 違いは、 **SQLBindCol**への新しい呼び出しによって、データバッファーと長さ/インジケーターバッファーの新しいアドレスが指定されるのに対し、バインドオフセットを使用してもアドレスは変更されませんが、オフセットが追加されるだけです。 アプリケーションでは、必要に応じて新しいオフセットを指定できます。このオフセットは常に、最初にバインドされたアドレスに追加されます。 特に、オフセットが0に設定されている場合、またはステートメント属性が null ポインターに設定されている場合、ドライバーは最初にバインドされたアドレスを使用します。  
  
 バインドオフセットを指定するために、アプリケーションは SQL_ATTR_ROW_BIND_OFFSET_PTR statement 属性を SQLINTEGER バッファーのアドレスに設定します。 バインドを使用する関数をアプリケーションが呼び出す前に、このバッファーにバイト単位のオフセットを挿入します。 使用するバッファーのアドレスを決定するために、ドライバーはバインド内のアドレスにオフセットを追加します。 アドレスとオフセットの合計は有効なアドレスである必要がありますが、オフセットが追加されるアドレスが有効である必要はありません。 バインドオフセットの使用方法の詳細については、このセクションの後の「バッファーアドレス」を参照してください。  
  
## <a name="binding-arrays"></a>配列のバインド  
 行セットのサイズ (SQL_ATTR_ROW_ARRAY_SIZE statement 属性の値) が1より大きい場合、アプリケーションは単一バッファーではなくバッファーの配列をバインドします。 詳細については、「[ブロックカーソル](../../../odbc/reference/develop-app/block-cursors.md)」を参照してください。  
  
 このアプリケーションでは、次の2つの方法で配列をバインドできます。  
  
-   各列に配列をバインドします。 各データ構造 (配列) には1つの列のデータが含まれているため、これは*列方向のバインド*と呼ばれます。  
  
-   行全体のデータを保持する構造体を定義し、これらの構造体の配列をバインドします。 各データ構造体には1つの行のデータが含まれているため、これは行方向の*バインド*と呼ばれます。  
  
 バッファーの各配列には、少なくとも行セットのサイズと同じ数の要素が必要です。  
  
> [!NOTE]  
>  アプリケーションでアラインメントが有効であることを確認する必要があります。 配置に関する考慮事項の詳細については、「[アラインメント](../../../odbc/reference/develop-app/alignment.md)」を参照してください。  
  
## <a name="column-wise-binding"></a>列方向のバインド  
 列方向のバインドでは、アプリケーションによって、個別のデータと長さ/インジケーター配列が各列にバインドされます。  
  
 列方向のバインドを使用するには、まず、アプリケーションで SQL_ATTR_ROW_BIND_TYPE statement 属性を SQL_BIND_BY_COLUMN に設定します。 (これが既定値です)。バインドされる各列に対して、アプリケーションは次の手順を実行します。  
  
1.  データバッファー配列を割り当てます。  
  
2.  長さ/インジケーターバッファーの配列を割り当てます。  
  
    > [!NOTE]  
    >  列方向のバインドを使用するときにアプリケーションが記述子に直接書き込む場合は、長さとインジケーターデータに個別の配列を使用できます。  
  
3.  次の引数を使用して**SQLBindCol**を呼び出します。  
  
    -   *TargetType*は、データバッファー配列内の1つの要素の型です。  
  
    -   *Targetvalueptr*は、データバッファー配列のアドレスです。  
  
    -   *Bufferlength*は、データバッファー配列内の1つの要素のサイズです。 *Bufferlength*引数は、データが固定長データの場合は無視されます。  
  
    -   *StrLen_or_IndPtr*は、長さ/インジケーター配列のアドレスです。  
  
 この情報の使用方法の詳細については、このセクションで後述する「バッファーアドレス」を参照してください。 列方向のバインドの詳細については、「[列方向のバインド](../../../odbc/reference/develop-app/column-wise-binding.md)」を参照してください。  
  
## <a name="row-wise-binding"></a>行方向のバインド  
 行方向のバインドでは、バインドされる各列のデータと長さ/インジケーターバッファーを含む構造体を定義します。  
  
 行方向のバインドを使用するために、アプリケーションは次の手順を実行します。  
  
1.  1行のデータ (データと長さ/インジケーターバッファーを含む) を保持する構造体を定義し、これらの構造体の配列を割り当てます。  
  
    > [!NOTE]  
    >  行方向のバインドを使用するときにアプリケーションが記述子に直接書き込む場合は、長さとインジケーターデータに個別のフィールドを使用できます。  
  
2.  SQL_ATTR_ROW_BIND_TYPE ステートメントの属性を、1行のデータを含む構造体のサイズ、または結果の列がバインドされるバッファーのインスタンスのサイズに設定します。 長さには、すべてのバインドされた列の領域と、構造体またはバッファーの埋め込みが含まれる必要があります。これにより、バインドされた列のアドレスが指定された長さでインクリメントされると、結果は次の行の同じ列の先頭を指します。 ANSI C で*sizeof*演算子を使用すると、この動作は保証されます。  
  
3.  は、バインドされる各列に対して次の引数を使用して**SQLBindCol**を呼び出します。  
  
    -   *TargetType*は、列にバインドされるデータバッファーメンバーの種類です。  
  
    -   *Targetvalueptr*は、最初の配列要素のデータバッファーメンバーのアドレスです。  
  
    -   *Bufferlength*は、データバッファーメンバーのサイズです。  
  
    -   *StrLen_or_IndPtr*は、バインドされる長さ/インジケーターメンバーのアドレスです。  
  
 この情報の使用方法の詳細については、このセクションで後述する「バッファーアドレス」を参照してください。 列方向のバインドの詳細については、「行方向の[バインド](../../../odbc/reference/develop-app/row-wise-binding.md)」を参照してください。  
  
## <a name="buffer-addresses"></a>バッファーアドレス  
 *バッファーアドレス*は、データまたは長さ/インジケーターバッファーの実際のアドレスです。 ドライバーは、バッファーに書き込む直前 (フェッチ時など) に、バッファーアドレスを計算します。 次の式から計算されます。これは、 *Targetvalueptr*と*StrLen_or_IndPtr*引数に指定されたアドレス、バインドオフセット、および行番号を使用します。  
  
 バインドされた*アドレス* + *バインドオフセット*+ ((*行番号*-1) x*要素サイズ*)  
  
 ここでは、次の表に示すように、数式の変数を定義します。  
  
|変数|[説明]|  
|--------------|-----------------|  
|*バインドされたアドレス*|データバッファーの場合は、 **SQLBindCol**の*targetvalueptr*引数で指定されたアドレス。<br /><br /> 長さ/インジケーターバッファーの場合、 **SQLBindCol**の*StrLen_or_IndPtr*引数で指定されたアドレス。 詳細については、「記述子と SQLBindCol」セクションの「その他のコメント」を参照してください。<br /><br /> バインドされたアドレスが0の場合、前の数式で計算されたアドレスが0以外の場合でも、データ値は返されません。|  
|*バインドオフセット*|行方向のバインドを使用する場合は、SQL_ATTR_ROW_BIND_OFFSET_PTR statement 属性で指定したアドレスに格納されている値。<br /><br /> 列方向のバインドが使用されている場合、または SQL_ATTR_ROW_BIND_OFFSET_PTR statement 属性の値が null ポインターの場合、*バインドオフセット*は0になります。|  
|*行番号*|行セット内の行の1から始まる番号。 単一行フェッチ (既定値) の場合、これは1です。|  
|*要素のサイズ*|バインドされた配列内の要素のサイズ。<br /><br /> 列方向のバインドが使用されている場合、長さ/インジケーターバッファーには**sizeof (SQLINTEGER)** が使用されます。 データバッファーの場合は、データ型が可変長の場合は**SQLBindCol**の*bufferlength*引数の値、データ型が固定長の場合はデータ型のサイズになります。<br /><br /> 行方向のバインドを使用する場合、これはデータと長さ/インジケーターバッファーの両方の SQL_ATTR_ROW_BIND_TYPE statement 属性の値になります。|  
  
## <a name="descriptors-and-sqlbindcol"></a>記述子と SQLBindCol  
 次のセクションでは、 **SQLBindCol**が記述子と対話する方法について説明します。  
  
> [!CAUTION]  
>  あるステートメントに対して**SQLBindCol**を呼び出すと、他のステートメントに影響を与える可能性があります。 このエラーは、ステートメントに関連付けられているが明示的に割り当てられ、他のステートメントにも関連付けられている場合に発生します。 **SQLBindCol**は記述子を変更するため、この記述子が関連付けられているすべてのステートメントに変更が適用されます。 これが必要な動作でない場合、アプリケーションは、 **SQLBindCol**を呼び出す前に、他のステートメントとこの記述子の関連付けを解除する必要があります。  
  
## <a name="argument-mappings"></a>引数のマッピング  
 概念的には、 **SQLBindCol**は次の手順を順番に実行します。  
  
1.  **SQLGetStmtAttr**を呼び出して、そのハンドルを取得します。  
  
2.  **SQLGetDescField**を呼び出してこの記述子の SQL_DESC_COUNT フィールドを取得します。 *columnnumber*引数の値が SQL_DESC_COUNT の値を超えている場合は、 **SQLSetDescField**を呼び出して、SQL_DESC_COUNT の値を*columnnumber*に増やします。  
  
3.  **SQLSetDescField**を複数回呼び出して、の次のフィールドに値を割り当てます。  
  
    -   SQL_DESC_TYPE と SQL_DESC_CONCISE_TYPE を*targettype*の値に設定します。ただし、 *targettype*が datetime または interval サブタイプの簡潔な識別子の1つである場合、SQL_DESC_TYPE はそれぞれ SQL_DATETIME または SQL_INTERVAL に設定されます。SQL_DESC_CONCISE_TYPE を簡潔な識別子に設定します。とは、対応する DATETIME または INTERVAL サブコードに SQL_DESC_DATETIME_INTERVAL_CODE を設定します。  
  
    -   *TargetType*に応じて、SQL_DESC_LENGTH、SQL_DESC_PRECISION、SQL_DESC_SCALE、および SQL_DESC_DATETIME_INTERVAL_PRECISION の1つ以上を設定します。  
  
    -   SQL_DESC_OCTET_LENGTH フィールドを*Bufferlength*の値に設定します。  
  
    -   SQL_DESC_DATA_PTR フィールドを*targetvalue*の値に設定します。  
  
    -   SQL_DESC_INDICATOR_PTR フィールドを*StrLen_or_Ind*の値に設定します。 (次の段落を参照してください)。  
  
    -   SQL_DESC_OCTET_LENGTH_PTR フィールドを*StrLen_or_Ind*の値に設定します。 (次の段落を参照してください)。  
  
 *StrLen_or_Ind*引数が参照する変数は、インジケーターと長さの両方の情報に使用されます。 フェッチで列に null 値が検出された場合、この変数には SQL_NULL_DATA が格納されます。それ以外の場合は、この変数にデータ長を格納します。 Null ポインターを*StrLen_or_Ind*として渡すと、フェッチ操作によってデータ長が返されますが、null 値が検出され、SQL_NULL_DATA を返すことができない場合、フェッチは失敗します。  
  
 **SQLBindCol**への呼び出しが失敗した場合、通常は設定されていた記述子フィールドの内容が未定義になり、の SQL_DESC_COUNT フィールドの値は変更されません。  
  
## <a name="implicit-resetting-of-count-field"></a>カウントフィールドの暗黙的なリセット  
 **SQLBindCol**は、SQL_DESC_COUNT の値が増加する場合にのみ、 *columnnumber*引数の値に SQL_DESC_COUNT を設定します。 *Targetvalueptr*引数の値が null ポインターであり、 *columnnumber*引数の値が SQL_DESC_COUNT と等しい場合 (つまり、最大バインド列のバインドを解除した場合)、SQL_DESC_COUNT は、残りの最大のバインド列の数に設定されます。  
  
## <a name="cautions-regarding-sql_default"></a>SQL_DEFAULT に関する注意事項  
 列データを正常に取得するには、アプリケーションがアプリケーションバッファー内のデータの長さと開始位置を正しく確認する必要があります。 アプリケーションが明示的な*TargetType*を指定すると、アプリケーション誤解が簡単に検出されます。 ただし、アプリケーションで SQL_DEFAULT の*TargetType*が指定されている場合、メタデータへの変更、または別の列へのコードの適用によって、アプリケーションで想定されているものとは異なるデータ型の列に**SQLBindCol**を適用できます。 この場合、アプリケーションは、フェッチされた列データの先頭または長さを常に判断するとは限りません。 これにより、データエラーやメモリ違反が報告される可能性があります。  
  
## <a name="code-example"></a>コード例  
 次の例では、アプリケーションは Customers テーブルに対して**select**ステートメントを実行し、名前で並べ替えられた顧客 id、名前、および電話番号の結果セットを返します。 次に、 **SQLBindCol**を呼び出して、データの列をローカルバッファーにバインドします。 最後に、アプリケーションは**Sqlfetch**を使用してデータの各行をフェッチし、各顧客の名前、ID、および電話番号を出力します。  
  
 コード例については、次を参照してください[SQLBulkOperations 関数](../../../odbc/reference/syntax/sqlbulkoperations-function.md)、 [SQLColumns 関数](../../../odbc/reference/syntax/sqlcolumns-function.md)、 [SQLFetchScroll 関数](../../../odbc/reference/syntax/sqlfetchscroll-function.md)、および[SQLSetPos 関数](../../../odbc/reference/syntax/sqlsetpos-function.md)。  
  
```cpp  
// SQLBindCol_ref.cpp  
// compile with: odbc32.lib  
#include <windows.h>  
#include <stdio.h>  
  
#define UNICODE  
#include <sqlext.h>  
  
#define NAME_LEN 50  
#define PHONE_LEN 20  
  
void show_error() {  
   printf("error\n");  
}  
  
int main() {  
   SQLHENV henv;  
   SQLHDBC hdbc;  
   SQLHSTMT hstmt = 0;  
   SQLRETURN retcode;  
   SQLWCHAR szName[NAME_LEN], szPhone[PHONE_LEN], sCustID[NAME_LEN];  
   SQLLEN cbName = 0, cbCustID = 0, cbPhone = 0;  
  
   // Allocate environment handle  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
  
   // Set the ODBC version environment attribute  
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
      retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER*)SQL_OV_ODBC3, 0);   
  
      // Allocate connection handle  
      if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
         retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);  
  
         // Set login timeout to 5 seconds  
         if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
            SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
  
            // Connect to data source  
            retcode = SQLConnect(hdbc, (SQLWCHAR*) L"NorthWind", SQL_NTS, (SQLWCHAR*) NULL, 0, NULL, 0);  
  
            // Allocate statement handle  
            if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {   
               retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);   
  
               retcode = SQLExecDirect(hstmt, (SQLWCHAR *) L"SELECT CustomerID, ContactName, Phone FROM CUSTOMERS ORDER BY 2, 1, 3", SQL_NTS);  
               if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
  
                  // Bind columns 1, 2, and 3  
                  retcode = SQLBindCol(hstmt, 1, SQL_C_CHAR, &sCustID, 100, &cbCustID);  
                  retcode = SQLBindCol(hstmt, 2, SQL_C_CHAR, szName, NAME_LEN, &cbName);  
                  retcode = SQLBindCol(hstmt, 3, SQL_C_CHAR, szPhone, PHONE_LEN, &cbPhone);   
  
                  // Fetch and print each row of data. On an error, display a message and exit.  
                  for (i ; ; i++) {  
                     retcode = SQLFetch(hstmt);  
                     if (retcode == SQL_ERROR || retcode == SQL_SUCCESS_WITH_INFO)  
                        show_error();  
                     if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO)  
                        wprintf(L"%d: %S %S %S\n", i + 1, sCustID, szName, szPhone);  
                     else  
                        break;  
                  }  
               }  
  
               // Process data  
               if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
                  SQLCancel(hstmt);  
                  SQLFreeHandle(SQL_HANDLE_STMT, hstmt);  
               }  
  
               SQLDisconnect(hdbc);  
            }  
  
            SQLFreeHandle(SQL_HANDLE_DBC, hdbc);  
         }  
      }  
      SQLFreeHandle(SQL_HANDLE_ENV, henv);  
   }  
}  
```  
  
 「[サンプル ODBC プログラム](../../../odbc/reference/sample-odbc-program.md)」も参照してください。  
  
## <a name="related-functions"></a>関連する関数  
  
|詳細|参照先|  
|---------------------------|---------|  
|結果セットの列に関する情報を返す|[SQLDescribeCol 関数](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|データのブロックのフェッチまたは結果セットのスクロール|[SQLFetchScroll 関数](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|複数行のデータのフェッチ|[SQLFetch 関数](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|ステートメントで列バッファーを解放しています|[SQLFreeStmt 関数](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|データ列の一部またはすべてをフェッチしています|[SQLGetData 関数](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
|結果セットの列数を返す|[SQLNumResultCols 関数](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
  
## <a name="see-also"></a>参照  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)
