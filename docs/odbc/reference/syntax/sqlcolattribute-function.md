---
title: SQLColAttribute 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLColAttribute
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLColAttribute
helpviewer_keywords:
- SQLColAttribute function [ODBC]
ms.assetid: 8c45c598-cb01-4789-a571-e93619a18ed9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c4577b97c827d527422fe2448656496d7c196c40
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68118699"
---
# <a name="sqlcolattribute-function"></a>SQLColAttribute 関数
**準拠**  
 バージョンが導入されました。ODBC 3.0 規格に準拠します。ISO 92  
  
 **まとめ**  
 **SQLColAttribute**結果セット内の列の記述子の情報を返します。 記述子の情報は、文字列、記述子に依存する値、または整数値として返されます。  
  
> [!NOTE]  
>  詳細についてはどのようなドライバー マネージャーのときに、ODBC 3 には、この関数にマップします。*x* ODBC 2 を利用するアプリケーション *。x*ドライバーを参照してください[アプリケーションの旧バージョンと互換性のマッピング置換関数](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLColAttribute (  
      SQLHSTMT        StatementHandle,  
      SQLUSMALLINT    ColumnNumber,  
      SQLUSMALLINT    FieldIdentifier,  
      SQLPOINTER      CharacterAttributePtr,  
      SQLSMALLINT     BufferLength,  
      SQLSMALLINT *   StringLengthPtr,  
      SQLLEN *        NumericAttributePtr);  
```  
  
## <a name="arguments"></a>引数  
 *StatementHandle*  
 [入力]ステートメント ハンドルです。  
  
 *ColumnNumber*  
 [入力]フィールドの値の取得元の IRD 内のレコードの数。 この引数は、1 から始まる、増加の列の順序で順番に順序付けの結果データの列番号に対応します。 列は、任意の順序で記述できます。  
  
 列 0 は、この引数で指定できますが、SQL_DESC_TYPE と SQL_DESC_OCTET_LENGTH を除くすべての値は未定義の値を返します。  
  
 *FieldIdentifier*  
 [入力]記述子ハンドル。 このハンドルは、IRD のフィールドは (たとえば、SQL_COLUMN_TABLE_NAME) クエリを実行する必要がありますを定義します。  
  
 *CharacterAttributePtr*  
 [出力]値を返すバッファーへのポインター、 *FieldIdentifier*のフィールド、 *ColumnNumber*フィールドが文字の文字列である場合は、IRD の行。 それ以外の場合、フィールドは使用されません。  
  
 場合*CharacterAttributePtr*が null の場合、 *StringLengthPtr*はバイト (文字データの null 終端文字を除く) の合計数を返しますが、バッファーに返される使用可能な指す*CharacterAttributePtr*します。  
  
 *BufferLength*  
 [入力]場合*FieldIdentifier* ODBC で定義されたフィールドと*CharacterAttributePtr*文字の文字列またはバイナリのバッファーを指す、この引数の長さである必要があります\* *CharacterAttributePtr*します。 場合*FieldIdentifier* ODBC で定義されたフィールドと\* *CharacterAttribute*Ptr が整数では、このフィールドは無視されます。 場合、  *\*CharacterAttributePtr*は Unicode 文字列です (呼び出し時に**SQLColAttributeW**)、 *BufferLength*引数は偶数である必要があります。 場合*FieldIdentifier*ドライバーの定義済みのフィールドでは、アプリケーションでは、フィールドには、ドライバー マネージャーの性質を示しますを設定して、 *BufferLength*引数。 *BufferLength*次の値を持つことができます。  
  
-   場合*CharacterAttributePtr* 、ポインターへのポインターは、 *BufferLength* SQL_IS_POINTER 値でなければなりません。  
  
-   場合*CharacterAttributePtr*文字の文字列へのポインター、 *BufferLength*バッファーの長さです。  
  
-   場合*CharacterAttributePtr*バイナリのバッファー、アプリケーションの場所へのポインター、SQL_LEN_BINARY_ATTR の結果は、(*長さ*) マクロで*BufferLength*します。 これにより、負の値で*BufferLength*します。  
  
-   場合*CharacterAttributePtr*を固定長データ型へのポインターは、 *BufferLength*次のいずれかを指定する必要があります。SQL_IS_INTEGER、SQL_IS_UNINTEGER、SQL_SMALLINT、または SQLUSMALLINT します。  
  
 *StringLengthPtr*  
 [出力]バイト (文字データの null 終了バイトを除く) の合計数を返すバッファーへのポインターで返される使用可能な **CharacterAttributePtr*します。  
  
 返される使用可能なバイト数がより大きいまたは等しい場合は、文字データ*BufferLength*、記述子の情報で\* *CharacterAttributePtr* に切り捨てられます*BufferLength* null 終了文字の長さマイナスはドライバーによって null で終わるとします。  
  
 他のすべての種類の値のデータの*BufferLength*は無視されますと、ドライバーのサイズを想定しています **CharacterAttributePtr*は 32 ビットです。  
  
 *NumericAttributePtr*  
 [出力]値を返す整数バッファーへのポインター、 *FieldIdentifier*のフィールド、 *ColumnNumber*フィールドが SQL_DESC_COLUMN_LENGTH など、数値の記述子の型の場合は、IRD の行。 それ以外の場合、フィールドは使用されません。 一部のドライバーは、下位の 32 ビットを書き込む場合がありますのみまたは 16 ビット バッファーと参加解除の上位ビットに変更されていないことに注意してください。 そのため、アプリケーションでは、この関数を呼び出す前に 0 に値を初期化する必要があります。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_STILL_EXECUTING、SQL_ERROR、または SQL_INVALID_HANDLE します。  
  
## <a name="diagnostics"></a>診断  
 ときに**SQLColAttribute** SQL_ERROR または SQL_SUCCESS_WITH_INFO のいずれかを返します、関連付けられた SQLSTATE 値を呼び出すことによって取得される可能性があります**SQLGetDiagRec**で、 *HandleType*sql_handle_stmt としての*処理*の*StatementHandle*します。 次の表に、一般的にによって返される SQLSTATE 値**SQLColAttribute** ; この関数のコンテキストでそれぞれについて説明しますと表記"(DM)"の前にドライバー マネージャーによって返されるについての説明。 SQLSTATE 値ごとに関連付けられているリターン コードは明記しない限り、SQL_ERROR です。  
  
|SQLSTATE|[エラー]|説明|  
|--------------|-----------|-----------------|  
|01000|一般的な警告|ドライバー固有の情報メッセージです。 (関数は、SQL_SUCCESS_WITH_INFO を返します)。|  
|01004|文字列データで、右側が切り捨てられました|バッファー \* *CharacterAttributePtr*容量が不足すると、文字列全体の値を返すため、文字列値が切り捨てられました。 切り詰められていない文字列値の長さが返される **StringLengthPtr*します。 (関数は、SQL_SUCCESS_WITH_INFO を返します)。|  
|07005|準備されたステートメントがない、*カーソルの指定*|関連付けられているステートメント、 *StatementHandle*結果セットを返さなかったと*FieldIdentifier* SQL_DESC_COUNT でした。 記述する列がありませんでした。|  
|07009|無効な記述子のインデックス|(DM) の指定された値*ColumnNumber*を 0 に等しい、SQL_ATTR_USE_BOOKMARKS ステートメント属性 SQL_UB_OFF のでした。<br /><br /> 引数が指定された値*ColumnNumber*が結果セット内の列の数を超えていました。|  
|HY000|一般的なエラー|これがなかった固有の SQLSTATE とする実装に固有の SQLSTATE が定義されていない、エラーが発生しました。 によって返されるエラー メッセージ**SQLGetDiagField**診断データから、構造体では、エラーとその原因がについて説明します。|  
|HY001|メモリの割り当てエラー|ドライバーは、実行または関数の完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY008|操作が取り消されました|非同期処理が有効に、 *StatementHandle*します。 関数が呼び出された、および実行を完了する前に**SQLCancel**または**SQLCancelHandle**が呼び出されて、 *StatementHandle*します。 後でもう一度関数が呼び出された、 *StatementHandle*します。<br /><br /> 関数が呼び出された、および実行を完了する前に**SQLCancel**または**SQLCancelHandle**が呼び出されて、 *StatementHandle*から別のスレッドで、マルチ スレッド アプリケーションです。|  
|HY010|関数のシーケンス エラー|(DM) を非同期的に実行中の関数が呼び出された接続ハンドルに関連付けられているため、 *StatementHandle*します。 この非同期関数は、SQLColAttribute が呼び出されたときにまだ実行中だった。<br /><br /> (DM) **SQLExecute**、 **SQLExecDirect**、または**SQLMoreResults**に対して呼び出された、 *StatementHandle* SQL_PARAM_DATA_ を返されます。ご利用いただけます。 ストリームのすべてのパラメーターのデータが取得される前に、この関数が呼び出されました。<br /><br /> (DM) 関数が呼び出す前に呼び出された**SQLPrepare**、 **SQLExecDirect**、またはのカタログ関数、 *StatementHandle*します。<br /><br /> (DM) を非同期的に実行中の関数 (いないこの"1") が呼び出された、 *StatementHandle*この関数が呼び出されたときに実行されているとします。<br /><br /> (DM) **SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**、または**SQLSetPos**に対して呼び出された、 *StatementHandle* SQL_NEED_DATA が返されます。 すべての実行時データ パラメーターまたは列のデータが送信される前に、この関数が呼び出されました。|  
|HY013|メモリ管理エラー|基になるメモリ オブジェクトにアクセスできませんでした、場合によってメモリ不足が原因であるために、関数呼び出しを処理できませんでした。|  
|HY090|文字列またはバッファーの長さが無効です。|(DM)  *\*CharacterAttributePtr*文字の文字列と*BufferLength* SQL_NTS 等しくもありませんが、0 より小さいをでした。|  
|HY091|無効な記述子フィールドの識別子|引数が指定された値*FieldIdentifier*が定義されている値のいずれかと、実装定義の値でした。|  
|HY117|不明なトランザクションの状態のため、接続が中断されます。 のみを切断して、読み取り専用の関数が許可されます。|(DM) 中断状態の詳細については、次を参照してください。 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)します。|  
|HYC00|対応していないドライバー|引数が指定された値*FieldIdentifier*ドライバーによってサポートされていませんでした。|  
|HYT01|接続がタイムアウトしました|データ ソースが要求に応答する前に、接続のタイムアウト期間が終了しました。 によって、接続タイムアウト期間が設定されます**SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT します。|  
|IM001|ドライバーでは、この関数はサポートされていません|(DM) に、ドライバーが関連付けられている、 *StatementHandle*関数をサポートしていません。|  
|IM017|非同期通知モードでのポーリングは無効です。|通知のモデルを使用すると、常にポーリングは無効です。|  
|IM018|**SQLCompleteAsync**このハンドルに対する前の非同期操作を完了が呼び出されていません。|通知モードが有効になっている場合、ハンドルでは、前の関数呼び出しに SQL_STILL_EXECUTING が返された場合と**SQLCompleteAsync**後処理を行い、操作を完了するハンドルで呼び出す必要があります。|  
  
 後に呼び出されたときに**SQLPrepare**とする前に**SQLExecute**、 **SQLColAttribute**によって返される任意の SQLSTATE を返すことができます**SQLPrepare**または**SQLExecute**に応じて、データ ソースが SQL ステートメントに関連付けられていると評価される場合、 *StatementHandle*します。  
  
 パフォーマンス上の理由から、アプリケーションを呼び出す必要がありますいない**SQLColAttribute**ステートメントを実行する前にします。  
  
## <a name="comments"></a>コメント  
 アプリケーションがによって返される情報を使用する方法については**SQLColAttribute**を参照してください[結果セットのメタデータ](../../../odbc/reference/develop-app/result-set-metadata.md)します。  
  
 **SQLColAttribute**いずれかの情報を返しますで\* *NumericAttributePtr*または\* *CharacterAttributePtr*します。 整数の情報が返される\* *NumericAttributePtr* SQLLEN 値としては情報の他のすべての形式で返される\* *CharacterAttributePtr*します。 情報が返される場合\* *NumericAttributePtr*、ドライバーを無視*CharacterAttributePtr*、 *BufferLength*、および*StringLengthPtr*します。 情報が返される場合\* *CharacterAttributePtr*、ドライバーを無視*NumericAttributePtr*します。  
  
 **SQLColAttribute** IRD の記述子フィールドの値を返します。 記述子ハンドルではなく、ステートメント ハンドルで呼び出されます。 によって返される値**SQLColAttribute**の*FieldIdentifier*も呼び出すことによってこのセクションの後半に示す値を取得できます**SQLGetDescField**で、適切な IRD ハンドル。  
  
 現在定義されている記述子フィールド、導入されたれ、それらの情報が返されます引数は; このセクションでは後で示されています、ODBC のバージョン記述子の種類の詳細については、さまざまなデータ ソースを活用するためにドライバーが定義できます。  
  
 ODBC 3。*x*ドライバーは、各記述子フィールドの値を返す必要があります。 記述子フィールドは、ドライバーまたはデータ ソースには適用されませんし、ドライバーに 0 を返します、明記しない限り場合\* *StringLengthPtr*または空の文字列で **CharacterAttributePtr*します。  
  
## <a name="backward-compatibility"></a>Backward Compatibility  
 ODBC 3。*x*関数**SQLColAttribute**非推奨の ODBC 2 が置き換えられます *。x*関数**SQLColAttributes**します。 マッピングと**SQLColAttributes**に**SQLColAttribute** (ときに、ODBC 2 *。x*アプリケーションは、ODBC 3 の操作します *。x*ドライバー)、またはマッピング**SQLColAttribute**に**SQLColAttributes** (ときに、ODBC 3 *。x* ODBC 2 を利用するアプリケーション *。x*ドライバー)、ドライバー マネージャーがいずれかの値を渡します*FieldIdentifier*新しい値にマップするか、次のように、エラーが返されます。  
  
> [!NOTE]  
>  使用されるプレフィックス*FieldIdentifier* ODBC 3 の値 *。x*で使用される ODBC 2 から変更されました *。x*します。 新しいプレフィックスが"SQL_DESC";古いプレフィックス"SQL_COLUMN"が発生しました。  
  
-   場合、 **#define** ODBC 2 の値 *。x* *FieldIdentifier*と同じ、 **#define** ODBC 3 の値 *。x* *FieldIdentifier*、関数呼び出しで値が渡されるだけです。  
  
-   **#Define** ODBC 2 の値 *。x* *FieldIdentifiers* SQL_COLUMN_LENGTH、SQL_COLUMN_PRECISION、および SQL_COLUMN_SCALE が異なる、 **#define** ODBC 3 の値 *。x* *FieldIdentifiers* SQL_DESC_PRECISION、SQL_DESC_SCALE、および SQL_DESC_LENGTH します。 ODBC 2。*x*ドライバーでは、ODBC 2 がサポートのみ必要があります *。x*値。 ODBC 3。*x*ドライバーは、これらの 3 つの"SQL_COLUMN"と"SQL_DESC"の両方の値をサポートする必要があります*FieldIdentifiers*します。 有効桁数、小数点、および長さは、ODBC 3 で異なる方法で定義されるため、これらの値が異なります。*x*よりも ODBC 2 *。x*します。 詳細については、次を参照してください。[列のサイズ、10 進数字、転送オクテット長、および表示サイズ](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)します。  
  
-   場合、 **#define** ODBC 2 の値 *。x* *FieldIdentifier*とは異なる、 **#define** ODBC 3 の値 *。x* *FieldIdentifier*、として発生数、名前、および null 許容の値、関数呼び出しで値が対応する値にマップされます。 SQL_COLUMN_COUNT を SQL_DESC_COUNT にマップするなど、あり SQL_DESC_COUNT はマッピングの方向に応じて、SQL_COLUMN_COUNT にマップされます。  
  
-   場合*FieldIdentifier* ODBC 3 内の新しい値です *。x*、これがなかった対応する値では、ODBC 2 の *。x*、ときに、ODBC 3 はマップできません *。x*アプリケーションでの呼び出しで使用**SQLColAttribute** 、ODBC 2 *。x*ドライバー、および呼び出しは SQLSTATE HY091 を返します (無効な記述子フィールド識別子)。  
  
 次の表に、記述子の種類によって返される**SQLColAttribute**します。 型*NumericAttributePtr*値は**SQLLEN \*** します。  
  
|*FieldIdentifier*|[情報]<br /><br /> 返される|説明|  
|-----------------------|---------------------------------|-----------------|  
|SQL_DESC_AUTO_UNIQUE_VALUE (ODBC 1.0)|*NumericAttributePtr*|列が自動増分列の場合は SQL_TRUE にします。<br /><br /> 列が自動増分列ではないかが数値でない場合は SQL_FALSE にします。<br /><br /> このフィールドは数値データ型の列にのみ有効です。 アプリケーションは、[自動増分] 列を含む行に値を挿入することができますが、通常、列の値を更新することはできません。<br /><br /> [自動増分] 列に挿入が行われる挿入時に、一意の値が列に挿入されます。 増分値は定義されていませんがデータ ソースに固有です。 アプリケーションは特定の値によって、特定の時点またはインクリメントで、[自動増分] 列が開始されると想定する必要があります。|  
|SQL_DESC_BASE_COLUMN_NAME (ODBC 3.0)|*CharacterAttributePtr*|結果のベースの列名は、列を設定します。 (式である列の場合) のようにベースの列名が存在しない場合、この変数には、空の文字列が含まれます。<br /><br /> この情報は、IRD の読み取り専用フィールドの SQL_DESC_BASE_COLUMN_NAME レコード フィールドから返されます。|  
|SQL_DESC_BASE_TABLE_NAME (ODBC 3.0)|*CharacterAttributePtr*|列を含むベース テーブルの名前。 ベース テーブルの名前は定義できませんまたは適用可能でないの場合、この変数には、空の文字列が含まれます。<br /><br /> この情報は、IRD の読み取り専用フィールドの SQL_DESC_BASE_TABLE_NAME レコード フィールドから返されます。|  
|SQL_DESC_CASE_SENSITIVE (ODBC 1.0)|*NumericAttributePtr*|SQL_TRUE 場合は、列の照合順序との比較と大文字小文字を区別は処理されます。<br /><br /> 列の照合順序との比較と大文字小文字を区別は扱われませんまたは非文字は sql_false になります。|  
|SQL_DESC_CATALOG_NAME (ODBC 2.0)|*CharacterAttributePtr*|列を含むテーブルのカタログです。 返される値は、実装で定義された列が式の場合、または列がビューの一部である場合です。 データ ソースはカタログをサポートしていないか、カタログ名を特定することはできません、空の文字列が返されます。 この VARCHAR レコードのフィールドでは、128 文字に限定されません。|  
|SQL_DESC_CONCISE_TYPE (ODBC 1.0)|*NumericAttributePtr*|簡潔なデータを入力します。<br /><br /> Datetime と間隔のデータ型は、このフィールドは、簡潔なデータ型を返します。たとえば、SQL_TYPE_TIME または SQL_INTERVAL_YEAR です。 (詳細については、次を参照してください[データ型識別子と記述子](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md)付録 d:。データ型です。)<br /><br /> この情報は、IRD の SQL_DESC_CONCISE_TYPE レコード フィールドから返されます。|  
|SQL_DESC_COUNT (ODBC 1.0)|*NumericAttributePtr*|結果セットで使用できる列の数。 結果セットの列が存在しない場合、0 が返されます。 値、 *ColumnNumber*引数は無視されます。<br /><br /> この情報は、IRD の SQL_DESC_COUNT ヘッダー フィールドから返されます。|  
|SQL_DESC_DISPLAY_SIZE (ODBC 1.0)|*NumericAttributePtr*|列のデータを表示するために必要な文字の最大数。 表示サイズの詳細については、次を参照してください[列のサイズ、10 進数字、転送オクテット長、および表示サイズ](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)付録 d:。データ型。|  
|SQL_DESC_FIXED_PREC_SCALE (ODBC 1.0)|*NumericAttributePtr*|列がデータ ソースに固有である固定有効桁数とスケールを 0 以外の場合は SQL_TRUE にします。<br /><br /> 列にデータ ソースに固有である固定有効桁数とスケールを 0 以外の値がない場合は sql_false になります。|  
|SQL_DESC_LABEL (ODBC 2.0)|*CharacterAttributePtr*|列のラベルまたはタイトル。 たとえば、EmpName という名前の列は従業員名ラベルを付けることがあります。 またはエイリアスを持つという場合があります。<br /><br /> 列がラベルを持たない場合、列名が返されます。 列がラベルが付いていない、名前のない場合は、空の文字列が返されます。|  
|SQL_DESC_LENGTH (ODBC 3.0)|*NumericAttributePtr*|いずれかである数値の値を文字の文字列またはバイナリ データの最大値または実際の文字の長さを入力します。 固定長データ型の場合は、最大文字長または可変長データ型の実際の文字の長さになります。 その値は、常に文字列を終了する null 終了バイトを除外します。<br /><br /> この情報は、IRD の SQL_DESC_LENGTH レコード フィールドから返されます。<br /><br /> 長さの詳細については、次を参照してください[列のサイズ、10 進数字、転送オクテット長、および表示サイズ](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)付録 d:。データ型。|  
|SQL_DESC_LITERAL_PREFIX (ODBC 3.0)|*CharacterAttributePtr*|この varchar (128) レコードのフィールドには、このデータ型のリテラルのプレフィックスとして、ドライバーが認識できる文字が含まれています。 このフィールドには、空の文字列データ型のリテラル プレフィックスは適用されませんが含まれています。 詳細については、次を参照してください。[リテラル プレフィックスおよびサフィックス](../../../odbc/reference/develop-app/literal-prefixes-and-suffixes.md)します。|  
|SQL_DESC_LITERAL_SUFFIX (ODBC 3.0)|*CharacterAttributePtr*|この varchar (128) レコードのフィールドには、このデータ型のリテラルのサフィックスとして、ドライバーが認識できる文字が含まれています。 このフィールドには、空の文字列データ型のリテラル サフィックスは適用されませんが含まれています。 詳細については、次を参照してください。[リテラル プレフィックスおよびサフィックス](../../../odbc/reference/develop-app/literal-prefixes-and-suffixes.md)します。|  
|SQL_DESC_LOCAL_TYPE_NAME (ODBC 3.0)|*CharacterAttributePtr*|この varchar (128) レコードのフィールドには、データ型の正規名と異なる可能性があるデータ型の任意のローカライズされた (ネイティブ言語) 名前が含まれています。 ローカライズされた名前がない場合は、空の文字列が返されます。 このフィールドは、表示目的でのみです。 文字列の文字セットは、ロケールに依存するでは通常、サーバーの既定の文字セット。|  
|SQL_DESC_NAME (ODBC 3.0)|*CharacterAttributePtr*|列の別名、適用される場合。 列の別名が適用されない場合は、列名が返されます。 どちらの場合は、SQL_DESC_UNNAMED ができませんに設定されます。 列名がありませんまたは列の別名がある場合は、空の文字列が返され、SQL_DESC_UNNAMED が SQL_UNNAMED に設定されています。<br /><br /> この情報は、IRD の SQL_DESC_NAME レコード フィールドから返されます。|  
|SQL_DESC_NULLABLE (ODBC 3.0)|*NumericAttributePtr*|Sql _ null 許容列の NULL 値であることができる場合SQL_NO_NULLS 列に NULL 値がない場合または、SQL_NULLABLE_UNKNOWN 列が NULL 値を受け入れるかどうかが不明である場合。<br /><br /> この情報は、IRD の SQL_DESC_NULLABLE レコード フィールドから返されます。|  
|SQL_DESC_NUM_PREC_RADIX (ODBC 3.0)|*NumericAttributePtr*|SQL_DESC_TYPE フィールドでのデータ型が概数データ型の場合は、この SQLINTEGER フィールドには、SQL_DESC_PRECISION フィールドには、ビット数が含まれているために、2 の値が含まれています。 SQL_DESC_TYPE フィールドでのデータ型が真数データ型の場合は、このフィールドには、SQL_DESC_PRECISION フィールドには、10 進数字の数が含まれているために、値 10 にはが含まれています。 このフィールドは、すべての数値以外のデータ型の場合は 0 に設定されます。|  
|SQL_DESC_OCTET_LENGTH (ODBC 3.0)|*NumericAttributePtr*|文字の文字列またはバイナリ データ型の長さ、(バイト単位)。 固定長の文字またはバイナリ型では、これは、実際の長さ (バイト単位)。 可変長の文字またはバイナリ型では、これは、最大長 (バイト単位)。 この値では、null 終端文字は含まれません。<br /><br /> この情報は、IRD の SQL_DESC_OCTET_LENGTH レコード フィールドから返されます。<br /><br /> 長さの詳細については、次を参照してください[列のサイズ、10 進数字、転送オクテット長、および表示サイズ](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)付録 d:。データ型。|  
|SQL_DESC_PRECISION (ODBC 3.0)|*NumericAttributePtr*|数値データ型に適用可能な有効桁数を指定する数値。 型のデータ SQL_TYPE_TIME、sql_type_timestamp 型、型し、その値の時間間隔を表すすべての interval データ型は、秒の小数部のコンポーネントの該当する有効桁数。<br /><br /> この情報は、IRD の SQL_DESC_PRECISION レコード フィールドから返されます。|  
|SQL_DESC_SCALE (ODBC 3.0)|*NumericAttributePtr*|数値データ型の該当する小数点以下桁数を示す数値。 DECIMAL および NUMERIC のデータ型の定義のスケールになります。 場合によっては、その他のすべてのデータ型に定義されていません。<br /><br /> この情報は、IRD のスケールのレコード フィールドから返されます。|  
|SQL_DESC_SCHEMA_NAME (ODBC 2.0)|*CharacterAttributePtr*|列を含むテーブルのスキーマです。 返される値は、実装で定義された列が式の場合、または列がビューの一部である場合です。 データ ソースがスキーマをサポートしていないか、スキーマ名が確認できない、空の文字列が返されます。 この VARCHAR レコードのフィールドでは、128 文字に限定されません。|  
|SQL_DESC_SEARCHABLE (ODBC 1.0)|*NumericAttributePtr*|SQL_PRED_NONE WHERE 句で列を使用できない場合。 (これは ODBC 2 で SQL_UNSEARCHABLE 値と同じです。*x*)。<br /><br /> SQL_PRED_CHAR 場合は、列は、WHERE 句では、LIKE 述語と共にのみ使用できます。 (これは ODBC 2 で SQL_LIKE_ONLY 値と同じです。*x*)。<br /><br /> SQL_PRED_BASIC などを除くすべての比較演算子と共に WHERE 句で列を使用できる場合。 (これは ODBC 2 で SQL_EXCEPT_LIKE 値と同じです。*x*)。<br /><br /> SQL_PRED_SEARCHABLE 場合は、列は、任意の比較演算子と共に WHERE 句で使用できます。<br /><br /> 列は、SQL_LONGVARCHAR と SQL_LONGVARBINARY 戻り値は、通常 SQL_PRED_CHAR を入力します。|  
|SQL_DESC_TABLE_NAME (ODBC 2.0)|*CharacterAttributePtr*|列を含むテーブルの名前です。 返される値は、実装で定義された列が式の場合、または列がビューの一部である場合です。<br /><br /> テーブル名を決定できない場合は、空の文字列が返されます。|  
|SQL_DESC_TYPE (ODBC 3.0)|*NumericAttributePtr*|SQL データ型を指定する数値。<br /><br /> ときに*ColumnNumber*と等しいの可変長のブックマークを 0 に SQL_BINARY が返され、固定長のブックマークの SQL_INTEGER が返されます。<br /><br /> Datetime と間隔のデータ型は、このフィールドは、詳細なデータ型を返します。SQL_DATETIME または SQL_INTERVAL の場合は。 (詳細については、次を参照してください[データ型識別子と記述子](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md)付録 d:。データ型。<br /><br /> この情報は、IRD の SQL_DESC_TYPE レコード フィールドから返されます。 **注:** ODBC 2 に対して作業します。*x*ドライバー、SQL_DESC_CONCISE_TYPE を代わりに使用します。|  
|SQL_DESC_TYPE_NAME (ODBC 1.0)|*CharacterAttributePtr*|データ ソースに依存するデータ型名です。たとえば、"CHAR"、"VARCHAR"、"MONEY"、"LONG VARBINARY"、または「CHAR FOR BIT DATA ()」。<br /><br /> 種類が不明な場合は、空の文字列が返されます。|  
|SQL_DESC_UNNAMED (ODBC 3.0)|*NumericAttributePtr*|できませんまたは SQL_UNNAMED します。 列の別名または列名が、IRD の SQL_DESC_NAME フィールドが含まれる場合はできませんが返されます。 列名または列の別名がない場合は、SQL_UNNAMED が返されます。<br /><br /> この情報は、IRD の SQL_DESC_UNNAMED レコード フィールドから返されます。|  
|SQL_DESC_UNSIGNED (ODBC 1.0)|*NumericAttributePtr*|列が署名されていない (または数値ではありません) の場合は SQL_TRUE にします。<br /><br /> 列が署名されている場合は SQL_FALSE にします。|  
|SQL_DESC_UPDATABLE (ODBC 1.0)|*NumericAttributePtr*|列が定義済みの定数の値について説明します。<br /><br /> SQL_ATTR_READONLY SQL_ATTR_WRITE SQL_ATTR_READWRITE_UNKNOWN<br /><br /> SQL_DESC_UPDATABLE では、ベース テーブルの列ではなく、結果セットの列の更新について説明します。 結果セット列の基になる基本列の更新は、このフィールドの値と異なる可能性があります。 列は更新可能かどうかは、データ型、ユーザーの特権と、結果セット自体の定義に基づくことができます。 明確ではありません、列は更新可能かどうか、SQL_ATTR_READWRITE_UNKNOWN が返されます。|  
  
 **SQLColAttribute**拡張可能な代替です**SQLDescribeCol**します。 **SQLDescribeCol** ANSI 89 SQL ベースの記述子の情報の固定セットを返します。 **SQLColAttribute**より広範な ANSI sql-92 と DBMS ベンダーの拡張機能で使用できる記述子情報にアクセスできるようにします。  
  
## <a name="related-functions"></a>関連する関数  
  
|詳細|参照先|  
|---------------------------|---------|  
|バッファーを結果セット内の列にバインドします。|[SQLBindCol 関数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|ステートメントの処理をキャンセル|[SQLCancel 関数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|結果セット内の列に関する情報を返す|[SQLDescribeCol 関数](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|データのブロックをフェッチしています。 または、結果をスクロールの設定|[SQLFetchScroll 関数](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|複数行のデータをフェッチしています|[SQLFetch 関数](../../../odbc/reference/syntax/sqlfetch-function.md)|  
  
## <a name="example"></a>例  
 次のサンプル コードでは、ハンドルと接続は解放されません。 参照してください[SQLFreeHandle 関数](../../../odbc/reference/syntax/sqlfreehandle-function.md)、 [ODBC のサンプル プログラム](../../../odbc/reference/sample-odbc-program.md)、および[SQLFreeStmt 関数](../../../odbc/reference/syntax/sqlfreestmt-function.md)ハンドルおよびステートメントを解放するコード サンプルについてはします。  
  
```cpp  
// SQLColAttibute.cpp  
// compile with: user32.lib odbc32.lib  
  
#define UNICODE  
  
#include <windows.h>  
#include <sqlext.h>  
#include <strsafe.h>  
  
struct DataBinding {  
   SQLSMALLINT TargetType;  
   SQLPOINTER TargetValuePtr;  
   SQLINTEGER BufferLength;  
   SQLLEN StrLen_or_Ind;  
};  
  
void printStatementResult(SQLHSTMT hstmt) {  
   int bufferSize = 1024, i;  
   SQLRETURN retCode;  
   SQLSMALLINT numColumn = 0, bufferLenUsed;
   
   retCode = SQLNumResultCols(hstmt, &numColumn);  
   
   SQLPOINTER* columnLabels = (SQLPOINTER *)malloc( numColumn * sizeof(SQLPOINTER*) );  
   struct DataBinding* columnData = (struct DataBinding*)malloc( numColumn * sizeof(struct DataBinding) );  
  
   printf( "Columns from that table:\n" );  
   for ( i = 0 ; i < numColumn ; i++ ) {  
      columnLabels[i] = (SQLPOINTER)malloc( bufferSize*sizeof(char) );  
  
      retCode = SQLColAttribute(hstmt, (SQLUSMALLINT)i + 1, SQL_DESC_LABEL, columnLabels[i], (SQLSMALLINT)bufferSize, &bufferLenUsed, NULL);  
      wprintf( L"Column %d: %s\n", i, (wchar_t*)columnLabels[i] );  
   }  
  
   // allocate memory for the binding  
   for ( i = 0 ; i < numColumn ; i++ ) {  
      columnData[i].TargetType = SQL_C_CHAR;  
      columnData[i].BufferLength = (bufferSize+1);  
      columnData[i].TargetValuePtr = malloc( sizeof(unsigned char)*columnData[i].BufferLength );  
   }  
  
   // setup the binding   
   for ( i = 0 ; i < numColumn ; i++ ) {  
      retCode = SQLBindCol(hstmt, (SQLUSMALLINT)i + 1, columnData[i].TargetType,   
         columnData[i].TargetValuePtr, columnData[i].BufferLength, &(columnData[i].StrLen_or_Ind));  
   }  
  
   printf( "Data from that table:\n" );  
   // fetch the data and print out the data  
   for ( retCode = SQLFetch(hstmt) ; retCode == SQL_SUCCESS || retCode == SQL_SUCCESS_WITH_INFO ; retCode = SQLFetch(hstmt) ) {  
      int j;  
      for ( j = 0 ; j < numColumn ; j++ )  
         wprintf( L"%s: %hs\n", columnLabels[j], columnData[j].TargetValuePtr );  
      printf( "\n" );  
   }  
   printf( "\n" );   
}  
  
int main() {  
   int bufferSize = 1024, i, count = 1, numCols = 5;  
   wchar_t firstTableName[1024], * dbName = (wchar_t *)malloc( sizeof(wchar_t)*bufferSize ), * userName = (wchar_t *)malloc( sizeof(wchar_t)*bufferSize );  
   HWND desktopHandle = GetDesktopWindow();   // desktop's window handle  
   SQLWCHAR connStrbuffer[1024];  
   SQLSMALLINT connStrBufferLen, bufferLen;  
   SQLRETURN retCode;  
  
   SQLHENV henv = NULL;   // Environment     
   SQLHDBC hdbc = NULL;   // Connection handle  
   SQLHSTMT hstmt = NULL;   // Statement handle  
  
   struct DataBinding* catalogResult = (struct DataBinding*) malloc( numCols * sizeof(struct DataBinding) );  
   SQLWCHAR* selectAllQuery = (SQLWCHAR *)malloc( sizeof(SQLWCHAR) * bufferSize );  
  
   // connect to database  
   retCode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
   retCode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLCHAR *)(void*)SQL_OV_ODBC3, -1);  
   retCode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);  
   retCode = SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)10, 0);  
   retCode = SQLDriverConnect(hdbc, desktopHandle, L"Driver={SQL Server}", SQL_NTS, connStrbuffer, 1025, &connStrBufferLen, SQL_DRIVER_PROMPT);  
   retCode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
  
   // display the database information  
   retCode = SQLGetInfo(hdbc, SQL_DATABASE_NAME, dbName, (SQLSMALLINT)bufferSize, (SQLSMALLINT *)&bufferLen);  
   retCode = SQLGetInfo(hdbc, SQL_USER_NAME, userName, (SQLSMALLINT)bufferSize, &bufferLen);  
  
   for ( i = 0 ; i < numCols ; i++ ) {  
      catalogResult[i].TargetType = SQL_C_CHAR;  
      catalogResult[i].BufferLength = (bufferSize + 1);  
      catalogResult[i].TargetValuePtr = malloc( sizeof(unsigned char)*catalogResult[i].BufferLength );  
   }  
  
   // Set up the binding. This can be used even if the statement is closed by closeStatementHandle  
   for ( i = 0 ; i < numCols ; i++ )  
      retCode = SQLBindCol(hstmt, (SQLUSMALLINT)i + 1, catalogResult[i].TargetType, catalogResult[i].TargetValuePtr, catalogResult[i].BufferLength, &(catalogResult[i].StrLen_or_Ind));  
  
   retCode = SQLTables( hstmt, (SQLWCHAR*)SQL_ALL_CATALOGS, SQL_NTS, L"", SQL_NTS, L"", SQL_NTS, L"", SQL_NTS );  
   retCode = SQLFreeStmt(hstmt, SQL_CLOSE);  
  
   retCode = SQLTables( hstmt, dbName, SQL_NTS, userName, SQL_NTS, L"%", SQL_NTS, L"TABLE", SQL_NTS );  
  
   for ( retCode = SQLFetch(hstmt) ; retCode == SQL_SUCCESS || retCode == SQL_SUCCESS_WITH_INFO ; retCode = SQLFetch(hstmt), ++count )  
      if ( count == 1 )  
         StringCchPrintfW( firstTableName, 1024, L"%hs", catalogResult[2].TargetValuePtr );  
   retCode = SQLFreeStmt(hstmt, SQL_CLOSE);  
  
   wprintf( L"Select all data from the first table (%s)\n", firstTableName );  
   StringCchPrintfW( selectAllQuery, bufferSize, L"SELECT * FROM %s", firstTableName );  
  
   retCode = SQLExecDirect(hstmt, selectAllQuery, SQL_NTS);  
   printStatementResult(hstmt);  
}  
```  
  
## <a name="see-also"></a>参照  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)   
 [ODBC のサンプル プログラム](../../../odbc/reference/sample-odbc-program.md)
