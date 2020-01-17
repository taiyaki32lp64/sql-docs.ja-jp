---
title: SQLSetDescField 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSetDescField
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLSetDescField
helpviewer_keywords:
- SQLSetDescField function [ODBC]
ms.assetid: 8c544388-fe9d-4f94-a0ac-fa0b9c9c88a5
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4cca223510ebb6838048e3babbf8fdcada42f87a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68039740"
---
# <a name="sqlsetdescfield-function"></a>SQLSetDescField 関数

**準拠**  
 バージョンが導入されました。ODBC 3.0 規格に準拠します。ISO 92  
  
 **まとめ**  
 **Sqlsetdescfield による**記述子レコードの 1 つのフィールドの値を設定します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
SQLRETURN SQLSetDescField(  
     SQLHDESC      DescriptorHandle,  
     SQLSMALLINT   RecNumber,  
     SQLSMALLINT   FieldIdentifier,  
     SQLPOINTER    ValuePtr,  
     SQLINTEGER    BufferLength);  
```  
  
## <a name="arguments"></a>引数  
 *DescriptorHandle*  
 [入力]記述子ハンドル。  
  
 *RecNumber*  
 [入力]記述子レコードのフィールドを設定しようとするアプリケーションを含むことを示します。 記述子のレコードは、レコード番号 0 ブックマーク レコードの中で、0 から番号が付けられます。 *RecNumber*ヘッダー フィールドの引数は無視されます。  
  
 *FieldIdentifier*  
 [入力]値を設定するが、記述子フィールドを示します。 詳細については、次を参照してください。"*FieldIdentifier*引数"、"コメント"セクションでします。  
  
 *ValuePtr*  
 [入力]記述子の情報または整数値を格納するバッファーへのポインター。 データ型の値に依存*FieldIdentifier*します。 場合*ValuePtr*整数値です (SQLLEN) は 8 バイト、4 バイト (SQLINTEGER) またはの値に応じて 2 バイト (SQLSMALLINT) と見なすことが、 *FieldIdentifier*引数。  
  
 *BufferLength*  
 [入力]場合*FieldIdentifier* ODBC で定義されたフィールドと*ValuePtr*文字の文字列またはバイナリのバッファーを指す、この引数の長さである必要があります **ValuePtr*します。 文字の文字列データでは、この引数は、文字列のバイト数を含める必要があります。  
  
 場合*FieldIdentifier* ODBC で定義されたフィールドと*ValuePtr*整数*BufferLength*は無視されます。  
  
 場合*FieldIdentifier*ドライバーの定義済みのフィールドでは、アプリケーションでは、フィールドには、ドライバー マネージャーの性質を示しますを設定して、 *BufferLength*引数。 *BufferLength*次の値を持つことができます。  
  
-   場合*ValuePtr*文字の文字列へのポインターは*BufferLength* SQL_NTS または文字列の長さです。  
  
-   場合*ValuePtr* 、SQL_LEN_BINARY_ATTR の結果を配置するアプリケーションが、バイナリ バッファーへのポインター (*長さ*) マクロで*BufferLength*します。 これにより、負の値で*BufferLength*します。  
  
-   場合*ValuePtr*文字の文字列またはバイナリ文字列以外の値へのポインターは*BufferLength* SQL_IS_POINTER 値でなければなりません。  
  
-   場合*ValuePtr* 、固定長の値を含む*BufferLength*に応じて SQL_IS_INTEGER、SQL_IS_UINTEGER、SQL_IS_SMALLINT、または SQL_IS_USMALLINT は、します。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR、または SQL_INVALID_HANDLE します。  
  
## <a name="diagnostics"></a>診断  
 ときに**SQLSetDescField** SQL_ERROR または SQL_SUCCESS_WITH_INFO、関連付けられている SQLSTATE 値を返しますを呼び出すことによって取得できる**SQLGetDiagRec**で、 *HandleType*のSQL_HANDLE_DESC と*処理*の*DescriptorHandle*します。 次の表に、一般的にによって返される SQLSTATE 値**SQLSetDescField** ; この関数のコンテキストでそれぞれについて説明します"(DM)"の表記の前にドライバー マネージャーによって返されるについての説明。 SQLSTATE 値ごとに関連付けられているリターン コードは明記しない限り、SQL_ERROR です。  
  
|SQLSTATE|[エラー]|説明|  
|--------------|-----------|-----------------|  
|01000|一般的な警告|ドライバー固有の情報メッセージです。 (関数は、SQL_SUCCESS_WITH_INFO を返します)。|  
|01S02|オプション値が変更されました|ドライバーがで指定された値をサポートしていませんでした *\*ValuePtr* (場合*ValuePtr*ポインター) の値または*ValuePtr* (場合*ValuePtr*された整数値です)、または *\*ValuePtr*が、ドライバーのような値を代入するため、実装の動作状態のため無効です。 (関数は、SQL_SUCCESS_WITH_INFO を返します)。|  
|07009|無効な記述子のインデックス|*FieldIdentifier*引数がレコードのフィールド、 *RecNumber*引数が 0 の場合、 *DescriptorHandle* IPD ハンドルへの引数と呼ばれます。<br /><br /> *RecNumber*引数が 0 未満、 *DescriptorHandle* ARD したり、APD 引数と呼ばれます。<br /><br /> *RecNumber*引数が列またはデータ ソースをサポートできますが、パラメーターの最大数よりも大きいと*DescriptorHandle* APD または ARD に引数と呼ばれます。<br /><br /> (DM)、 *FieldIdentifier*引数が SQL_DESC_COUNT、および *\*ValuePtr*引数が 0 未満でした。<br /><br /> *RecNumber*引数が 0 に等しいと*DescriptorHandle*引数は、暗黙的に割り当てられた APD 呼ばれます。 (これを明示的に割り当てられたアプリケーション記述子を使用してエラーが発生しないを明示的に割り当てられたアプリケーション記述子は、APD またはまで ARD かどうかが不明のために実行されます。)|  
|08S01|通信リンク エラー|関数が完了した処理の前に、ドライバーとドライバーが接続されているデータ ソース間の通信リンクに失敗しました。|  
|22001|文字列データで、右側が切り捨てられました|*FieldIdentifier*引数は、SQL_DESC_NAME と*BufferLength*引数が SQL_MAX_IDENTIFIER_LEN より大きい値です。|  
|HY000|一般的なエラー|これがなかった固有の SQLSTATE とする実装に固有の SQLSTATE が定義されていない、エラーが発生しました。 によって返されるエラー メッセージ**SQLGetDiagRec**で、  *\*MessageText*バッファーは、エラーとその原因について説明します。|  
|HY001|メモリの割り当てエラー|ドライバーは、実行または関数の完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY010|関数のシーケンス エラー|(DM)、 *DescriptorHandle*に関連付けられているが、 *StatementHandle*に (このない) 非同期的に実行中の関数が呼び出されたこの関数が呼び出されたときに実行されています。<br /><br /> (DM) **SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**、または**SQLSetPos**に対して呼び出された、 *StatementHandle*られて、 *DescriptorHandle*が関連付けられているし、SQL_NEED_DATA が返されます。 すべての実行時データ パラメーターまたは列のデータが送信される前に、この関数が呼び出されました。<br /><br /> (DM) を非同期的に実行中の関数が呼び出された接続ハンドルに関連付けられているため、 *DescriptorHandle*します。 この非同期関数ではときに実行されている、 **SQLSetDescField**関数が呼び出されました。<br /><br /> (DM) **SQLExecute**、 **SQLExecDirect**、または**SQLMoreResults**に関連付けられているステートメント ハンドルのいずれかが呼び出された、 *DescriptorHandle* SQL_PARAM_DATA_AVAILABLE が返されます。 ストリームのすべてのパラメーターのデータが取得される前に、この関数が呼び出されました。|  
|HY013|メモリ管理エラー|基になるメモリ オブジェクトにアクセスできませんでした、場合によってメモリ不足が原因であるために、関数呼び出しを処理できませんでした。|  
|HY016|実装行記述子は変更できません。|*DescriptorHandle*引数は、IRD に関連付けられていたと*FieldIdentifier* SQL_DESC_ARRAY_STATUS_PTR または SQL_DESC_ROWS_PROCESSED_PTR 引数がありませんでした。|  
|HY021|不整合な記述子情報|(Apd の標準) は、SQL_DESC_TYPE と SQL_DESC_DATETIME_INTERVAL_CODE フィールドは、有効な ODBC SQL 型または (Ipd) の有効なドライバー固有の SQL 型または有効な ODBC C データ型は形成してしません。<br /><br /> 整合性チェック中にチェック記述子の情報は、一貫性のあるでした。 (で「整合性チェック」を参照してください**SQLSetDescRec**。)。|  
|HY090|文字列またはバッファーの長さが無効です。|(DM)  *\*ValuePtr*文字の文字列と*BufferLength*がゼロ未満が SQL_NTS と等しくありませんでした。<br /><br /> (DM) ドライバーが、ODBC 2 *.x*ドライバー、記述子の ARD、 *ColumnNumber*引数が 0、および引数が指定された値に設定された*BufferLength*されました4 と等しくありません。|  
|HY091|無効な記述子フィールドの識別子|指定された値、 *FieldIdentifier*引数が、ODBC で定義されたフィールドとしましたが、実装定義の値でした。<br /><br /> *FieldIdentifier*引数は有効ですが、 *DescriptorHandle*引数。<br /><br /> *FieldIdentifier*引数が ODBC で定義された、読み取り専用フィールド。|  
|HY092|無効な属性またはオプション識別子|値 *\*ValuePtr*は無効です、 *FieldIdentifier*引数。<br /><br /> *FieldIdentifier*引数が SQL_DESC_UNNAMED、および*ValuePtr*できませんでした。|  
|HY105|無効なパラメーターの型|(DM) SQL_DESC_PARAMETER_TYPE フィールドに指定された値が無効です。 (詳細については、次を参照してください、"*InputOutputType*引数"セクション**SQLBindParameter**。)。|  
|HY117|不明なトランザクションの状態のため、接続が中断されます。 のみを切断して、読み取り専用の関数が許可されます。|(DM) 中断状態の詳細については、次を参照してください。[で ODBC 3.8 新](../../../odbc/reference/what-s-new-in-odbc-3-8.md)します。|  
|HYT01|接続がタイムアウトしました|データ ソースが要求に応答する前に、接続のタイムアウト期間が終了しました。 によって、接続タイムアウト期間が設定されます**SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT します。|  
|IM001|ドライバーでは、この関数はサポートされていません|(DM) に、ドライバーが関連付けられている、 *DescriptorHandle*関数をサポートしていません。|  
  
## <a name="comments"></a>コメント  
 アプリケーションが呼び出すことができます**SQLSetDescField**一度に 1 つの記述子フィールドを設定します。 1 回の呼び出しに**SQLSetDescField**記述子を 1 つで 1 つのフィールドを設定します。 この関数は、記述子の型のいずれかのフィールドを設定すると呼ばれる、フィールドを設定することができますを提供できます。 (このセクションの後半の表を参照してください)。  
  
> [!NOTE]  
>  呼び出し**SQLSetDescField**で識別される記述子レコードの内容は、失敗、 *RecNumber*引数が定義されていません。  
  
 他の関数は、関数の単一の呼び出しで複数の記述子フィールドを設定すると呼ばれることができます。 **SQLSetDescRec**列またはパラメーター (、SQL_DESC_TYPE SQL_DESC_DATETIME_INTERVAL_CODE、SQL_DESC_OCTET_LENGTH、SQL_DESC_PRECISION sql _ にバインドされているデータ型とバッファーに影響するさまざまなフィールドを設定する関数DESC_SCALE、SQL_DESC_DATA_PTR、SQL_DESC_OCTET_LENGTH_PTR、および SQL_DESC_INDICATOR_PTR フィールド)。 **SQLBindCol**または**SQLBindParameter**列またはパラメーターのバインディングの完全な仕様を作成するために使用できます。 これらの関数は、1 つの関数呼び出しの記述子フィールドの特定のグループを設定します。  
  
 **Sqlsetdescfield による**呼び出すバインド バッファーを変更するには、バインドのポインター (SQL_DESC_DATA_PTR、SQL_DESC_INDICATOR_PTR、または SQL_DESC_OCTET_LENGTH_PTR) にオフセットを追加することができます。 バインドのバッファーを呼び出さずにこの変更**SQLBindCol**または**SQLBindParameter**アプリケーションを SQL_DESC_DATA_ などの他のフィールドを変更することがなく SQL_DESC_DATA_PTR を変更することができます入力します。  
  
 アプリケーションを呼び出す場合**SQLSetDescField** SQL_DESC_COUNT 以外の任意のフィールドまたは SQL_DESC_DATA_PTR、SQL_DESC_INDICATOR_PTR、SQL_DESC_OCTET_LENGTH_PTR、遅延のフィールドを設定するには、レコードがバインドされていません。  
  
 記述子のヘッダー フィールドを呼び出すことによって設定が**SQLSetDescField**と適切な*FieldIdentifier*します。 多くのヘッダー フィールドではもステートメントの属性への呼び出しで設定することも**SQLSetStmtAttr**します。 これにより、アプリケーションを最初に記述子ハンドルを取得することがなく、記述子フィールドを設定できます。 ときに**SQLSetDescField**が呼び出され、ヘッダー フィールドを設定する、 *RecNumber*引数は無視されます。  
  
 A *RecNumber* 0 のブックマークのフィールドを設定に使用されます。  
  
> [!NOTE]  
>  ステートメント属性 SQL_ATTR_USE_BOOKMARKS は常に設定する呼び出しの前に**SQLSetDescField**ブックマーク フィールドを設定します。 これは必須ではありません、中に強くお勧めします。  
  
## <a name="sequence-of-setting-descriptor-fields"></a>一連の記述子フィールドの設定  
 記述子フィールドを呼び出すことによって設定するときに**SQLSetDescField**アプリケーションが特定の順序に従う必要があります。  
  
1.  アプリケーションでは、SQL_DESC_TYPE、SQL_DESC_CONCISE_TYPE、または SQL_DESC_DATETIME_INTERVAL_CODE フィールドをまず設定する必要があります。  
  
2.  これらのフィールドのいずれかが設定された後に、アプリケーションは、データ型の属性を設定でき、ドライバーはデータ型の適切な既定値をデータ型に属性フィールドを設定します。 型の属性フィールドの既定の自動により、記述子が、アプリケーションのデータ型が指定した後で使用する準備が常にあります。 アプリケーションは、データ型の属性を明示的に設定する場合、に、既定の属性をオーバーライドします。  
  
3.  手順 1 で示されているフィールドのいずれかが設定されているし、データ型の属性が設定されている、アプリケーションは、SQL_DESC_DATA_PTR を設定できます。 これには、記述子フィールドの整合性チェックが求められます。 アプリケーションは、SQL_DESC_DATA_PTR フィールドを設定した後、データ型または属性を変更する場合、ドライバーは、null ポインターの場合、レコードをバインド解除する SQL_DESC_DATA_PTR を設定します。 これにより、記述子レコードが使用する前に、シーケンスで適切な手順を実行するアプリケーションです。  
  
## <a name="initialization-of-descriptor-fields"></a>記述子フィールドの初期化  
 記述子が割り当てられるの記述子フィールドは既定値に初期化することができます、既定値のない初期化するか、記述子の種類に対して定義できません。 次の表では、"D"は、既定値、フィールドが初期化されていることを示すと、"ND"は、既定値なし、フィールドが初期化されていることを示す、記述子の種類ごとに各フィールドの初期化を示します。 数値が表示されている場合、フィールドの既定値はその数にします。 テーブルは、フィールドが (R/W) の読み取り/書き込みまたは読み取り専用 (R) であるかどうかも示します。  
  
 ステートメント ハンドルまたは記述子が割り当てられたときではなく、IRD に設定されてと、ステートメントが準備または実行後にのみ、ird フィールドは既定値を持ちます。 IRD が作成されるまで、ird フィールドにアクセスしようとするとはエラーを返します。  
  
 記述子の種類 (標準と IRDs、および Apd と Ipd) のすべてではありませんが、1 つまたは複数をいくつかの記述子フィールドが定義されます。 フィールドは、記述子の型に対して定義されているが、ときに、その記述子を使用する関数のいずれかでは必要ありません。  
  
 によってアクセスできるフィールド**SQLGetDescField**必ずしも設定することはできません**SQLSetDescField**します。 設定できるフィールド**SQLSetDescField**次の表に記載されています。  
  
 ヘッダー フィールドの初期化は、次の表に記載されています。  
  
|ヘッダー フィールドの名前|型|R/W|既定値|  
|-----------------------|----------|----------|-------------|  
|SQL_DESC_ALLOC_TYPE|SQLSMALLINT|ARD:R APD:R IRD:R の IPD:R|ARD:SQL_DESC_ALLOC_AUTO の暗黙の SQL_DESC_ALLOC_USER または明示的な<br /><br /> APD:SQL_DESC_ALLOC_AUTO の暗黙の SQL_DESC_ALLOC_USER または明示的な<br /><br /> IRD:SQL_DESC_ALLOC_AUTO<br /><br /> IPD:SQL_DESC_ALLOC_AUTO|  
|SQL_DESC_ARRAY_SIZE|SQLULEN です。|ARD:APD の読み取り/書き込みです。R/W IRD:未使用の IPD:未使用|ARD: [1] APD: [1] IRD:未使用の IPD:未使用|  
|SQL_DESC_ARRAY_STATUS_PTR|SQLUSMALLINT *|ARD:APD の読み取り/書き込みです。R/W IRD:IPD の読み取り/書き込みです。R/W|ARD:APD の ptr は null します。Ptr IRD は null します。Null ptr IPD:Null ptr|  
|SQL_DESC_BIND_OFFSET_PTR|SQLLEN *|ARD:APD の読み取り/書き込みです。R/W IRD:未使用の IPD:未使用|ARD:APD の ptr は null します。Ptr IRD は null します。未使用の IPD:未使用|  
|SQL_DESC_BIND_TYPE|SQLINTEGER|ARD:APD の読み取り/書き込みです。R/W IRD:未使用の IPD:未使用|ARD:SQL_BIND_BY_COLUMN<br /><br /> APD:SQL_BIND_BY_COLUMN<br /><br /> IRD:未使用<br /><br /> IPD:未使用|  
|SQL_DESC_COUNT|SQLSMALLINT|ARD:APD の読み取り/書き込みです。R/W IRD:R の IPD:R/W|ARD:APD の 0:0 IRD:IPD の D:0|  
|SQL_DESC_ROWS_PROCESSED_PTR|SQLULEN です *|ARD:未使用の APD:未使用の IRD:IPD の読み取り/書き込みです。R/W|ARD:未使用の APD:未使用の IRD:Null ptr IPD:Null ptr|  
  
 [1] フィールドは、IPD をドライバーが自動的に作成する場合にのみ定義されます。 ない場合は、定義はありません。 アプリケーションが、これらのフィールド、SQLSTATE HY091 を設定しようとしています。 場合 (無効な記述子フィールド識別子) が返されます。  
  
 レコードのフィールドの初期化は、次の表に示すようにします。  
  
|レコード フィールド名|型|R/W|既定値|  
|-----------------------|----------|----------|-------------|  
|SQL_DESC_AUTO_UNIQUE_VALUE|SQLINTEGER|ARD:未使用の APD:未使用の IRD:R の IPD:未使用|ARD:未使用の APD:未使用の IRD:IPD の D:未使用|  
|SQL_DESC_BASE_COLUMN_NAME|SQLCHAR *|ARD:未使用の APD:未使用の IRD:R の IPD:未使用|ARD:未使用の APD:未使用の IRD:IPD の D:未使用|  
|SQL_DESC_BASE_TABLE_NAME|SQLCHAR *|ARD:未使用の APD:未使用の IRD:R の IPD:未使用|ARD:未使用の APD:未使用の IRD:IPD の D:未使用|  
|SQL_DESC_CASE_SENSITIVE|SQLINTEGER|ARD:未使用の APD:未使用の IRD:R の IPD:R|ARD:未使用の APD:未使用の IRD:IPD の D:D [1]|  
|SQL_DESC_CATALOG_NAME|SQLCHAR *|ARD:未使用の APD:未使用の IRD:R の IPD:未使用|ARD:未使用の APD:未使用の IRD:IPD の D:未使用|  
|SQL_DESC_CONCISE_TYPE|SQLSMALLINT|ARD:APD の読み取り/書き込みです。R/W IRD:R の IPD:R/W|ARD:SQL_C_ 既定 APD:SQL_C_ 既定 IRD:IPD の D:ND|  
|SQL_DESC_DATA_PTR|SQLPOINTER|ARD:APD の読み取り/書き込みです。R/W IRD:未使用の IPD:未使用|ARD:APD の ptr は null します。Ptr IRD は null します。未使用の IPD:未使用 [2]|  
|SQL_DESC_DATETIME_INTERVAL_CODE|SQLSMALLINT|ARD:APD の読み取り/書き込みです。R/W IRD:R の IPD:R/W|ARD:ND APD:ND IRD:IPD の D:ND|  
|SQL_DESC_DATETIME_INTERVAL_PRECISION|SQLINTEGER|ARD:APD の読み取り/書き込みです。R/W IRD:R の IPD:R/W|ARD:ND APD:ND IRD:IPD の D:ND|  
|SQL_DESC_DISPLAY_SIZE|SQLLEN|ARD:未使用の APD:未使用の IRD:R の IPD:未使用|ARD:未使用の APD:未使用の IRD:IPD の D:未使用|  
|SQL_DESC_FIXED_PREC_SCALE|SQLSMALLINT|ARD:未使用の APD:未使用の IRD:R の IPD:R|ARD:未使用の APD:未使用の IRD:IPD の D:D [1]|  
|SQL_DESC_INDICATOR_PTR|SQLLEN *|ARD:APD の読み取り/書き込みです。R/W IRD:未使用の IPD:未使用|ARD:APD の ptr は null します。Ptr IRD は null します。未使用の IPD:未使用|  
|SQL_DESC_LABEL|SQLCHAR *|ARD:未使用の APD:未使用の IRD:R の IPD:未使用|ARD:未使用の APD:未使用の IRD:IPD の D:未使用|  
|SQL_DESC_LENGTH|SQLULEN です。|ARD:APD の読み取り/書き込みです。R/W IRD:R の IPD:R/W|ARD:ND APD:ND IRD:IPD の D:ND|  
|SQL_DESC_LITERAL_PREFIX|SQLCHAR *|ARD:未使用の APD:未使用の IRD:R の IPD:未使用|ARD:未使用の APD:未使用の IRD:IPD の D:未使用|  
|SQL_DESC_LITERAL_SUFFIX|SQLCHAR *|ARD:未使用の APD:未使用の IRD:R の IPD:未使用|ARD:未使用の APD:未使用の IRD:IPD の D:未使用|  
|SQL_DESC_LOCAL_TYPE_NAME|SQLCHAR *|ARD:未使用の APD:未使用の IRD:R の IPD:R|ARD:未使用の APD:未使用の IRD:IPD の D:D [1]|  
|SQL_DESC_NAME|SQLCHAR *|ARD:未使用の APD:未使用の IRD:R の IPD:R/W|ARD:ND APD:ND IRD:IPD の D:ND|  
|SQL_DESC_NULLABLE|SQLSMALLINT|ARD:未使用の APD:未使用の IRD:R の IPD:R|ARD:ND APD:ND IRD:IPD の D:ND|  
|SQL_DESC_NUM_PREC_RADIX|SQLINTEGER|ARD:APD の読み取り/書き込みです。R/W IRD:R の IPD:R/W|ARD:ND APD:ND IRD:IPD の D:ND|  
|SQL_DESC_OCTET_LENGTH|SQLLEN|ARD:APD の読み取り/書き込みです。R/W IRD:R の IPD:R/W|ARD:ND APD:ND IRD:IPD の D:ND|  
|SQL_DESC_OCTET_LENGTH_PTR|SQLLEN *|ARD:APD の読み取り/書き込みです。R/W IRD:未使用の IPD:未使用|ARD:APD の ptr は null します。Ptr IRD は null します。未使用の IPD:未使用|  
|SQL_DESC_PARAMETER_TYPE|SQLSMALLINT|ARD:未使用の APD:未使用の IRD:未使用の IPD:R/W|ARD:未使用の APD:未使用の IRD:未使用の IPD:D = SQL_PARAM_INPUT|  
|SQL_DESC_PRECISION|SQLSMALLINT|ARD:APD の読み取り/書き込みです。R/W IRD:R の IPD:R/W|ARD:ND APD:ND IRD:IPD の D:ND|  
|SQL_DESC_ROWVER|SQLSMALLINT|ARD:未使用<br /><br /> APD:未使用<br /><br /> IRD:R<br /><br /> IPD:R|ARD:未使用<br /><br /> APD:未使用<br /><br /> IRD:ND<br /><br /> IPD:ND|  
|SQL_DESC_SCALE|SQLSMALLINT|ARD:APD の読み取り/書き込みです。R/W IRD:R の IPD:R/W|ARD:ND APD:ND IRD:IPD の D:ND|  
|SQL_DESC_SCHEMA_NAME|SQLCHAR *|ARD:未使用の APD:未使用の IRD:R の IPD:未使用|ARD:未使用の APD:未使用の IRD:IPD の D:未使用|  
|SQL_DESC_SEARCHABLE|SQLSMALLINT|ARD:未使用の APD:未使用の IRD:R の IPD:未使用|ARD:未使用の APD:未使用の IRD:IPD の D:未使用|  
|SQL_DESC_TABLE_NAME|SQLCHAR *|ARD:未使用の APD:未使用の IRD:R の IPD:未使用|ARD:未使用の APD:未使用の IRD:IPD の D:未使用|  
|SQL_DESC_TYPE|SQLSMALLINT|ARD:APD の読み取り/書き込みです。R/W IRD:R の IPD:R/W|ARD:SQL_C_DEFAULT APD:SQL_C_DEFAULT IRD:IPD の D:ND|  
|SQL_DESC_TYPE_NAME|SQLCHAR *|ARD:未使用の APD:未使用の IRD:R の IPD:R|ARD:未使用の APD:未使用の IRD:IPD の D:D [1]|  
|SQL_DESC_UNNAMED|SQLSMALLINT|ARD:未使用の APD:未使用の IRD:R の IPD:R/W|ARD:ND APD:ND IRD:IPD の D:ND|  
|SQL_DESC_UNSIGNED|SQLSMALLINT|ARD:未使用の APD:未使用の IRD:R の IPD:R|ARD:未使用の APD:未使用の IRD:IPD の D:D [1]|  
|SQL_DESC_UPDATABLE|SQLSMALLINT|ARD:未使用の APD:未使用の IRD:R の IPD:未使用|ARD:未使用の APD:未使用の IRD:IPD の D:未使用|  
  
 [1] フィールドは、IPD をドライバーが自動的に作成する場合にのみ定義されます。 ない場合は、定義はありません。 アプリケーションが、これらのフィールド、SQLSTATE HY091 を設定しようとしています。 場合 (無効な記述子フィールド識別子) が返されます。  
  
 [2]、IPD で SQL_DESC_DATA_PTR フィールドは、整合性チェックを強制的に設定できます。 後続の呼び出しで**SQLGetDescField**または**SQLGetDescRec**ドライバーは、SQL_DESC_DATA_PTR に設定された値を返す必要はありません。  
  
## <a name="fieldidentifier-argument"></a>FieldIdentifier 引数  
 *FieldIdentifier*記述子フィールドを設定するかを指定します。 記述子が含まれています、*記述子のヘッダー、* 、次のセクション、「ヘッダー フィールド」と 0 個以上で説明するヘッダー フィールドから成る*記述子レコード、* レコード フィールドから成る「ヘッダー フィールド」セクションを次のセクションで説明します。  
  
## <a name="header-fields"></a>ヘッダー フィールド  
 各記述子では、次のフィールドで構成されたヘッダーがあります。  
  
 **[すべて] SQL_DESC_ALLOC_TYPE**  
 この読み取り専用 SQLSMALLINT ヘッダー フィールドでは、ドライバーによって、またはアプリケーションによって明示的に、記述子の割り当てられた自動的に設定するかどうかを指定します。 アプリケーションは、取得、このフィールドは変更されません。 フィールドは、記述子がドライバーによって自動的に割り当てられている場合、ドライバーによって SQL_DESC_ALLOC_AUTO に設定されます。 記述子は、アプリケーションによって明示的に割り当てられた場合、ドライバーによって SQL_DESC_ALLOC_USER に設定にされます。  
  
 **SQL_DESC_ARRAY_SIZE [アプリケーション記述子]**  
 標準では、この sqlulen ですヘッダー フィールドは、行セット内の行の数を指定します。 これへの呼び出しによって返される行の番号**SQLFetch**または**SQLFetchScroll**またはへの呼び出しで操作する**SQLBulkOperations**または**SQLSetPos**.  
  
 Apd では、この sqlulen ですヘッダー フィールドは、各パラメーターの値の数を指定します。  
  
 このフィールドの既定値は 1 です。 SQL_DESC_ARRAY_SIZE が 1 より大きい場合は、SQL_DESC_DATA_PTR、SQL_DESC_INDICATOR_PTR、および ARD または APD の SQL_DESC_OCTET_LENGTH_PTR 配列をポイントします。 各配列のカーディナリティは、このフィールドの値と同じです。  
  
 ARD でこのフィールドを呼び出すことによって設定することもできます。 **SQLSetStmtAttr** SQL_ATTR_ROW_ARRAY_SIZE 属性を持つ。 APD でこのフィールドを呼び出すことによって設定することもできます。 **SQLSetStmtAttr** SQL_ATTR_PARAMSET_SIZE 属性を持つ。  
  
 **[すべて] SQL_DESC_ARRAY_STATUS_PTR**  
 記述子種類ごとに、この SQLUSMALLINT の * SQLUSMALLINT 値の配列へのヘッダー フィールドのポインター。 これらのアレイが次のように名前付き: 状態配列 (IRD)、パラメーター状態配列 (IPD)、行操作配列 (ARD)、およびパラメーターの操作の配列 (APD) の行。  
  
 このヘッダー フィールドが呼び出しの後に状態の値を含む行の状態配列を指す、ird **SQLBulkOperations**、 **SQLFetch**、 **SQLFetchScroll**、または**SQLSetPos**します。 配列には、行セット内の行がある多くの要素があります。 アプリケーションは、SQLUSMALLINTs の配列を割り当てるし、配列をポイントするには、このフィールドを設定する必要があります。 フィールドは、既定で null ポインターに設定されます。 状態値は生成されません後者を null ポインターの場合は、SQL_DESC_ARRAY_STATUS_PTR フィールドが設定され、配列が設定されていない、ドライバーは、配列を設定します。  
  
> [!CAUTION]  
>  アプリケーションは、IRD の SQL_DESC_ARRAY_STATUS_PTR フィールドによって示される行の状態の配列の要素を設定する場合、ドライバーの動作は未定義です。  
  
 呼び出して、配列の初期値は**SQLBulkOperations**、 **SQLFetch**、 **SQLFetchScroll**、または**SQLSetPos**します。 呼び出しに SQL_SUCCESS または SQL_SUCCESS_WITH_INFO を返さなかった場合にこのフィールドによって示される配列の内容は未定義です。 配列内の要素は、次の値を含めることができます。  
  
-   SQL_ROW_SUCCESS:行が正常にフェッチされたれ、最後にフェッチした後は変更されていません。  
  
-   SQL_ROW_SUCCESS_WITH_INFO:行が正常にフェッチされたれ、最後にフェッチした後は変更されていません。 ただし、行の詳細については、警告が返されました。  
  
-   SQL_ROW_ERROR:行のフェッチ中にエラーが発生しました。  
  
-   SQL_ROW_UPDATED:行は正常にフェッチされ、が最後にフェッチされた以降に更新されました。 行を再度フェッチすると、その状態は SQL_ROW_SUCCESS が。  
  
-   SQL_ROW_DELETED になります。最後にフェッチしたため、行が削除されました。  
  
-   SQL_ROW_ADDED:行が挿入された**SQLBulkOperations**します。 行を再度フェッチすると、その状態は SQL_ROW_SUCCESS が。  
  
-   SQL_ROW_NOROW であって:行セットには、結果セットの末尾がオーバー ラップされ、この要素の行の状態配列に対応する行が返されません。  
  
 IRD では、このフィールドを呼び出すことによって設定することもできます。 **SQLSetStmtAttr**し、SQL_ATTR_ROW_STATUS_PTR 属性を持つ。  
  
 IRD の SQL_DESC_ARRAY_STATUS_PTR フィールドは SQL_SUCCESS または SQL_SUCCESS_WITH_INFO が返された後にのみ有効です。 場合は、リターン コードは、次のいずれかではない、SQL_DESC_ROWS_PROCESSED_PTR が指す位置は定義されません。  
  
 このヘッダー フィールドが呼び出しの後にパラメーター値の各セットの状態情報を含むパラメーター状態配列を指す、IPD で**SQLExecute**または**SQLExecDirect**します。 場合に呼び出し**SQLExecute**または**SQLExecDirect** SQL_SUCCESS または sql_success_with_info が、このフィールドによって示される配列の内容は定義されていないが返されませんでした。 アプリケーションは、SQLUSMALLINTs の配列を割り当てるし、配列をポイントするには、このフィールドを設定する必要があります。 状態値は生成されません後者を null ポインターの場合は、SQL_DESC_ARRAY_STATUS_PTR フィールドが設定され、配列が設定されていない、ドライバーは、配列を設定します。 配列内の要素は、次の値を含めることができます。  
  
-   SQL_PARAM_SUCCESS:SQL ステートメントは、このパラメーターのセットを正常に実行されました。  
  
-   SQL_PARAM_SUCCESS_WITH_INFO:SQL ステートメントがこのパラメーターのセットを正常に実行ただし、警告情報は、診断データの構造体で使用できます。  
  
-   SQL_PARAM_ERROR:このパラメーターのセットの処理中にエラーが発生しました。 追加のエラー情報は、診断データの構造体で使用できます。  
  
-   SQL_PARAM_UNUSED:このパラメーターが設定されたに使用される、可能性があるいくつか前のパラメーター セットには、さらに処理を中止エラーが発生しました。 という事実が原因、または一連の SQL_DESC_ARRAY_STATUS_PTR フィールドで指定された配列内のパラメーターの SQL_PARAM_IGNORE が設定されているためAPD します。  
  
-   SQL_PARAM_DIAG_UNAVAILABLE:診断情報は、ご利用いただけません。 この例としてはこのレベルのエラー情報によって生成されないようにと場合、ドライバーは、モノリシックな単位としてパラメーターの配列を扱います。  
  
 IPD でこのフィールドを呼び出すことによって設定することもできます。 **SQLSetStmtAttr** SQL_ATTR_PARAM_STATUS_PTR 属性を持つ。  
  
 このヘッダー フィールドがこの行が無視するかどうかを示すために、アプリケーションによって設定できる値の行操作配列を指す、ARD で**SQLSetPos**操作。 配列内の要素は、次の値を含めることができます。  
  
-   SQL_ROW_PROCEED:一括操作を使用して、行が含まれている**SQLSetPos**します。 (この設定は保証されません、操作は、行で実行すること。 行 SQL_ROW_ERROR IRD 行の状態配列内の状態にある場合、ドライバーできないことがあります、行の操作を実行します。)  
  
-   SQL_ROW_IGNORE:一括操作を使用して、行を除外する**SQLSetPos**します。  
  
 配列の要素が設定されていない場合は、一括操作ですべての行が含まれます。 一括操作ですべての行を含む、ARD の SQL_DESC_ARRAY_STATUS_PTR フィールドの値が null ポインターの場合解釈は、有効な配列を指すポインター、配列のすべての要素が SQL_ROW_PROCEED 場合と同じです。 配列内の要素が SQL_ROW_IGNORE に設定されている場合、無視された行の行の状態配列内の値は変更されません。  
  
 ARD でこのフィールドを呼び出すことによって設定することもできます。 **SQLSetStmtAttr** SQL_ATTR_ROW_OPERATION_PTR 属性を持つ。  
  
 このヘッダー フィールドがこのパラメーターのセットがあるかどうかを示すために、アプリケーションによって設定できる値の操作パラメーター配列を指す、APD のするときに無視**SQLExecute**または**SQLExecDirect**が呼び出されます。 配列内の要素は、次の値を含めることができます。  
  
-   SQL_PARAM_PROCEED:パラメーターのセットが含まれている、 **SQLExecute**または**SQLExecDirect**呼び出します。  
  
-   SQL_PARAM_IGNORE:パラメーターのセットはから除外されて、 **SQLExecute**または**SQLExecDirect**呼び出します。  
  
 すべての配列内のパラメーターのセットを使用する配列の要素が設定されていない場合、 **SQLExecute**または**SQLExecDirect**呼び出し。 APD の SQL_DESC_ARRAY_STATUS_PTR フィールドの値が null ポインターの場合は、すべてのパラメーターのセットが使用されます。解釈は、有効な配列を指すポインター、配列のすべての要素が SQL_PARAM_PROCEED 場合と同じです。  
  
 APD でこのフィールドを呼び出すことによって設定することもできます。 **SQLSetStmtAttr** SQL_ATTR_PARAM_OPERATION_PTR 属性を持つ。  
  
 **SQL_DESC_BIND_OFFSET_PTR [アプリケーション記述子]**  
 この SQLLEN * ヘッダー フィールドがポイントするバインディングのオフセット。 既定で null ポインターに設定されます。 このフィールドが null ポインターでない場合は、ドライバーは、ポインターを逆参照しの各フィールド (SQL_DESC_DATA_PTR、SQL_DESC_INDICATOR_PTR、および SQL_DESC_OCTET_LENGTH_PTR) の記述子レコードで、null 以外の値を持つ遅延を逆参照された値を追加します。バインドするときに時間と使用して、新しいポインター値をフェッチします。  
  
 バインディングのオフセットは常の SQL_DESC_DATA_PTR、SQL_DESC_INDICATOR_PTR、および SQL_DESC_OCTET_LENGTH_PTR フィールドの値に直接追加します。 別の値にオフセットを変更する場合、新しい値は各記述子フィールドの値に直接追加されます。 新しいオフセットは、以前の任意のオフセットを加えたフィールド値には追加されません。  
  
 このフィールドは、*遅延フィールド*:設定されているが、データ バッファーのアドレスを確認する必要があるときに、ドライバーでの後で使用される時点では使用されません。  
  
 ARD でこのフィールドを呼び出すことによって設定することもできます。 **SQLSetStmtAttr** SQL_ATTR_ROW_BIND_OFFSET_PTR 属性を持つ。 ARD でこのフィールドを呼び出すことによって設定することもできます。 **SQLSetStmtAttr** SQL_ATTR_PARAM_BIND_OFFSET_PTR 属性を持つ。  
  
 詳細については、行方向のバインドでの説明を参照してください。 [SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)と[SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)します。  
  
 **SQL_DESC_BIND_TYPE [アプリケーション記述子]**  
 この SQLUINTEGER ヘッダー フィールドでは、列またはパラメーターをバインドするために使用するバインディングの方向を設定します。  
  
 このフィールドがバインディングの方向を指定する標準、ときに**SQLFetchScroll**または**SQLFetch**が関連付けられているステートメント ハンドルで呼び出されます。  
  
 列の列方向のバインドを選択するには、このフィールドは、(既定値) を SQL_BIND_BY_COLUMN に設定されます。  
  
 ARD でこのフィールドを呼び出すことによって設定することもできます。 **SQLSetStmtAttr** 、SQL_ATTR_ROW_BIND_TYPE を*属性*します。  
  
 Apd では、このフィールドは、動的パラメーターに使用するバインディングの方向を指定します。  
  
 パラメーターの列方向のバインドを選択するには、このフィールドは、(既定値) を SQL_BIND_BY_COLUMN に設定されます。  
  
 APD でこのフィールドを呼び出すことによって設定することもできます。 **SQLSetStmtAttr** 、SQL_ATTR_PARAM_BIND_TYPE を*属性*します。  
  
 **[すべて] SQL_DESC_COUNT**  
 この SQLSMALLINT ヘッダー フィールドには、データを格納する番号が最大のレコードの 1 から始まるインデックスを指定します。 ドライバーが、記述子のデータ構造を設定すると、重要なレコードの数を表示する SQL_DESC_COUNT フィールドも設定があります。 アプリケーションがこのデータ構造体のインスタンスを割り当てるときの部屋を予約するレコードの数を指定することはありません。 アプリケーションでは、レコードの内容を指定します、記述子ハンドルが適切なサイズのデータ構造体を指すことを確認するための必要な操作の実行、ドライバー。  
  
 SQL_DESC_COUNT は (フィールドが、ARD の場合) にバインドされているすべてのデータ列の場合、または (フィールドが、APD の場合) にバインドされた、すべてのパラメーターの数ではありませんが番号が最大のレコードの数。 番号が最大の列またはパラメーターがバインドされている場合、SQL_DESC_COUNT は、[次へ] の番号が最大の列またはパラメーターの数に変更されます。 列または番号を持つパラメーターが小さいかどうか、最も高い数字列の数がバインドされているよりも (呼び出して**SQLBindCol**で、 *TargetValuePtr*引数に null ポインター、または設定**SQLBindParameter**で、 *ParameterValuePtr*引数が null ポインターに設定)、SQL_DESC_COUNT は変更されません。 追加の列またはパラメーターがデータを格納する番号が最大レコードよりも大きい番号にバインドされている場合、ドライバーは SQL_DESC_COUNT フィールドの値を自動的に増加します。 呼び出すことによってすべての列がバインドされていない場合**SQLFreeStmt** SQL_UNBIND オプション、SQL_DESC_COUNT ARD および IRD フィールドが 0 に設定されます。 場合**SQLFreeStmt**と呼ばれるは、SQL_RESET_PARAMS オプションと、APD と IPD SQL_DESC_COUNT フィールドが 0 に設定されます。  
  
 SQL_DESC_COUNT 値明示的に設定できますアプリケーションで呼び出すことによって**SQLSetDescField**します。 SQL_DESC_COUNT の値が明示的に低下している SQL_DESC_COUNT に新しい値よりも大きい番号を持つすべてのレコードが効果的に削除されます。 SQL_DESC_COUNT の値が明示的に 0 に設定し、フィールドが、ARD である場合は、バインドされたブックマーク列を除くすべてのデータ バッファーが解放されます。  
  
 ARD のこのフィールドにレコード カウントでは、バインドされたブックマーク列は含まれません。 ブックマーク列をバインド解除する唯一の方法では、SQL_DESC_DATA_PTR フィールドに null ポインターを設定します。  
  
 **SQL_DESC_ROWS_PROCESSED_PTR [実装記述子]**  
 IRD のこの sqlulen です\*呼び出しの後にフェッチされた行の数を格納するバッファーへのヘッダー フィールドがポイント**SQLFetch**または**SQLFetchScroll**、または一括操作に影響を受けた行の数呼び出しによって実行される**SQLBulkOperations**または**SQLSetPos**エラー行を含むです。  
  
 IPD では、この SQLUINTEGER * 処理されて、エラーのセットを含むパラメーターのセットの数を格納するバッファーへのヘッダー フィールドがポイントです。 これが null ポインターの場合は、数は返されません。  
  
 SQL_DESC_ROWS_PROCESSED_PTR が有効では呼び出しの後に関係なく SQL_SUCCESS または SQL_SUCCESS_WITH_INFO が返された後にのみ**SQLFetch**または**SQLFetchScroll** (の IRD フィールド) または**SQLExecute**、 **SQLExecDirect**、または**SQLParamData** (の IPD フィールド)。 によって示されるバッファーに表示される呼び出し場合は、このフィールドが SQL_SUCCESS または sql_success_with_info が返されません、バッファーの内容は 0 に設定されている場合、バッファー内の値を sql_no_data が返されるしない限り、定義されています。  
  
 ARD でこのフィールドを呼び出すことによって設定することもできます。 **SQLSetStmtAttr** SQL_ATTR_ROWS_FETCHED_PTR 属性を持つ。 APD でこのフィールドを呼び出すことによって設定することもできます。 **SQLSetStmtAttr** SQL_ATTR_PARAMS_PROCESSED_PTR 属性を持つ。  
  
 このフィールドで指し示されるバッファーは、アプリケーションによって割り当てられます。 ドライバーによって設定される遅延出力バッファーになります。 既定で null ポインターに設定されます。  
  
## <a name="record-fields"></a>レコードのフィールド  
 各記述子には、列のデータまたは記述子の種類に応じて、動的パラメーターのいずれかを定義するフィールドから成る 1 つまたは複数のレコードが含まれています。 各レコードは、1 つの列またはパラメーターの完全な定義です。  
  
 **SQL_DESC_AUTO_UNIQUE_VALUE [IRDs]**  
 この読み取り専用 SQLINTEGER のレコードのフィールドには、列が自動インクリメント列ではない場合、列が自動インクリメントの列の場合、または SQL_FALSE 場合 SQL_TRUE が含まれています。 このフィールドは読み取り専用ですが、基になる自動インクリメント列がないと、読み取り専用とは限りません。  
  
 **SQL_DESC_BASE_COLUMN_NAME [IRDs]**  
 この読み取り専用の SQLCHAR * 結果セット列のレコードのフィールドにベースの列名が含まれます。 (式である列の場合) のようにベースの列名が存在しない場合、この変数には、空の文字列が含まれています。  
  
 **SQL_DESC_BASE_TABLE_NAME [IRDs]**  
 この読み取り専用の SQLCHAR * 結果セット列のレコードのフィールドがベース テーブル名を格納します。 ベース テーブルの名前は定義できませんまたは適用可能でない、この変数には、空の文字列が含まれています。  
  
 **SQL_DESC_CASE_SENSITIVE [実装記述子]**  
 この読み取り専用 SQLINTEGER のレコードのフィールドが含まれる SQL_TRUE 列またはパラメーターが扱わ照合順序との比較、または SQL_FALSE と大文字小文字を区別、文字である場合または場合は、列に照合順序との比較と大文字小文字を区別は扱われません列です。  
  
 **SQL_DESC_CATALOG_NAME [IRDs]**  
 この読み取り専用の SQLCHAR * レコード フィールドに列を含むベース テーブルのカタログが含まれています。 戻り値にはドライバーによって異なりますが、列が式の場合、または列がビューの一部である場合です。 データ ソースはカタログをサポートしない、またはカタログを特定できない、この変数には、空の文字列が含まれています。  
  
 **[すべて] SQL_DESC_CONCISE_TYPE**  
 この SQLSMALLINT ヘッダー フィールドには、簡潔なデータ型 datetime と間隔のデータ型を含む、すべてのデータ型を指定します。  
  
 SQL_DESC_CONCISE_TYPE、SQL_DESC_TYPE、および SQL_DESC_DATETIME_INTERVAL_CODE フィールドの値は相互に依存します。 毎回、フィールドのいずれかが設定されている、他の設定も必要があります。 呼び出しで設定できる SQL_DESC_CONCISE_TYPE **SQLBindCol**または**SQLBindParameter**、または**SQLSetDescField**します。 呼び出しで設定できる SQL_DESC_TYPE **SQLSetDescField**または**SQLSetDescRec**します。  
  
 SQL_DESC_CONCISE_TYPE が期間または日時のデータ型以外の簡潔なデータ型に設定されている場合は、SQL_DESC_TYPE フィールドが同じ値に設定されているし、SQL_DESC_DATETIME_INTERVAL_CODE フィールドが 0 に設定します。  
  
 SQL_DESC_CONCISE_TYPE が、簡潔なデータ型 datetime または間隔に設定されている場合は、SQL_DESC_TYPE フィールドが対応する詳細な型 (SQL_DATETIME または SQL_INTERVAL) に設定されているされ、適切なサブコードに SQL_DESC_DATETIME_INTERVAL_CODE フィールドが設定されます。  
  
 **[アプリケーション記述子と Ipd] SQL_DESC_DATA_PTR**  
 この SQLPOINTER レコード フィールドは、(Apd) のパラメーター値または (標準) の列の値を含む変数を指します。 このフィールドは、*遅延フィールド*します。 設定されているデータの取得には後で、ドライバーによって使用時に使用されません。  
  
 場合、ARD の SQL_DESC_DATA_PTR フィールドで指定された列のバインドが、 *TargetValuePtr*への呼び出しで引数**SQLBindCol** null ポインターか、ARD を設定する場合は、SQL_DESC_DATA_PTR フィールドに、呼び出す**SQLSetDescField**または**SQLSetDescRec**を null ポインター。 その他のフィールドは、SQL_DESC_DATA_PTR フィールドが null ポインターに設定されている場合に影響しません。  
  
 場合に呼び出し**SQLFetch**または**SQLFetchScroll**をこのフィールドで指し示されるバッファー内の塗りつぶしを返しませんでした SQL_SUCCESS または SQL_SUCCESS_WITH_INFO、バッファーの内容は未定義です。  
  
 ARD、または IPD APD の SQL_DESC_DATA_PTR フィールドが設定されている場合、ドライバー SQL_DESC_TYPE フィールドの値が有効な ODBC C データ型またはドライバーに固有のデータ型のいずれかが含まれていると、データ型に影響を与える他のすべてのフィールドに整合性があることを確認します。 整合性チェックの入力を求めるは、のみ、IPD の SQL_DESC_DATA_PTR フィールドの使用です。 具体的には、アプリケーションが、IPD と以降の呼び出しの SQL_DESC_DATA_PTR フィールドを設定するかどうかは**SQLGetDescField**をこのフィールドでが必ずしも返されないことが設定された値。 詳細についてを参照してください「整合性チェック」 [SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)します。  
  
 **[すべて] SQL_DESC_DATETIME_INTERVAL_CODE**  
 この SQLSMALLINT レコード フィールドには、SQL_DESC_TYPE フィールドが SQL_DATETIME または SQL_INTERVAL の特定の日付時刻または間隔のデータ型のサブコードが含まれています。 これは、SQL と C# の両方のデータ型の場合は true。 コードは、"CODE"(datetime 型の場合) の"TYPE"または"C_TYPE"のいずれかの代わりに使用または"CODE"(間隔の種類) の"INTERVAL"または"C_INTERVAL"の代わりに使用したデータ型名で構成されます。  
  
 SQL_DESC_TYPE、SQL_DESC_CONCISE_TYPE なアプリケーション記述子では SQL_C_DEFAULT に設定されており、記述子は、ステートメント ハンドルに関連付けられたが場合、SQL_DESC_DATETIME_INTERVAL_CODE の内容は未定義です。  
  
 このフィールドは、次の表に、datetime データ型に対して設定できます。  
  
|Datetime 型|DATETIME_INTERVAL_CODE|  
|--------------------|------------------------------|  
|SQL_TYPE_DATE/SQL_C_TYPE_DATE|SQL_CODE_DATE|  
|SQL_TYPE_TIME/SQL_C_TYPE_TIME|SQL_CODE_TIME|  
|SQL_TYPE_TIMESTAMP/SQL_C_TYPE_TIMESTAMP|SQL_CODE_TIMESTAMP|  
  
 このフィールドは、次の表に、interval データ型を設定できます。  
  
|[間隔の種類]|DATETIME_INTERVAL_CODE|  
|-------------------|------------------------------|  
|SQL_INTERVAL_DAY/SQL_C_INTERVAL_DAY|SQL_CODE_DAY|  
|SQL_INTERVAL_DAY_TO_HOUR/SQL_C_INTERVAL_DAY_TO_HOUR|SQL_CODE_DAY_TO_HOUR|  
|SQL_INTERVAL_DAY_TO_MINUTE/SQL_C_INTERVAL_DAY_TO_MINUTE|SQL_CODE_DAY_TO_MINUTE|  
|SQL_INTERVAL_DAY_TO_SECOND/SQL_C_INTERVAL_DAY_TO_SECOND|SQL_CODE_DAY_TO_SECOND|  
|SQL_INTERVAL_HOUR/SQL_C_INTERVAL_HOUR|SQL_CODE_HOUR|  
|SQL_INTERVAL_HOUR_TO_MINUTE/SQL_C_INTERVAL_HOUR_TO_MINUTE|SQL_CODE_HOUR_TO_MINUTE|  
|SQL_INTERVAL_HOUR_TO_SECOND/SQL_C_INTERVAL_HOUR_TO_SECOND|SQL_CODE_HOUR_TO_SECOND|  
|SQL_INTERVAL_MINUTE/SQL_C_INTERVAL_MINUTE|SQL_CODE_MINUTE|  
|SQL_INTERVAL_MINUTE_TO_SECOND/SQL_C_INTERVAL_MINUTE_TO_SECOND|SQL_CODE_MINUTE_TO_SECOND|  
|SQL_INTERVAL_MONTH/SQL_C_INTERVAL_MONTH|SQL_CODE_MONTH|  
|SQL_INTERVAL_SECOND/SQL_C_INTERVAL_SECOND|SQL_CODE_SECOND|  
|SQL_INTERVAL_YEAR/SQL_C_INTERVAL_YEAR|SQL_CODE_YEAR|  
|SQL_INTERVAL_YEAR_TO_MONTH/SQL_C_INTERVAL_YEAR_TO_MONTH|SQL_CODE_YEAR_TO_MONTH|  
  
 データの間隔と、このフィールドの詳細については、次を参照してください。[データ型識別子と記述子](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md)します。  
  
 **[すべて] SQL_DESC_DATETIME_INTERVAL_PRECISION**  
 この SQLINTEGER レコード フィールドには、先頭の有効桁数 SQL_DESC_TYPE フィールドが SQL_INTERVAL の場合、間隔が含まれています。 SQL_DESC_DATETIME_INTERVAL_CODE フィールドが間隔のデータ型に設定されている場合、このフィールドは、先頭の有効桁数の既定の間隔に設定されます。  
  
 **SQL_DESC_DISPLAY_SIZE [IRDs]**  
 この読み取り専用 SQLINTEGER のレコードのフィールドには、列からデータを表示するために必要な文字の最大数が含まれています。  
  
 **SQL_DESC_FIXED_PREC_SCALE [実装記述子]**  
 この読み取り専用 SQLSMALLINT のレコードのフィールドは、列が固定有効桁数と小数点が正確な数値列ではない場合が正確な数値列であり、固定有効桁数と小数点以下桁数を 0 以外の場合に、列の場合は SQL_TRUE、sql_false になります設定されます。  
  
 **SQL_DESC_INDICATOR_PTR [アプリケーション記述子]**  
 標準では、この SQLLEN で * インジケーター変数が指すフィールドを記録します。 この変数は、列の値が NULL の場合、SQL_NULL_DATA を格納します。 Apd のインジケーター変数は、NULL 動的引数を指定する SQL_NULL_DATA に設定されます。 それ以外の場合、変数は、(SQL_DESC_INDICATOR_PTR、および SQL_DESC_OCTET_LENGTH_PTR の値は、ポインターと同じ) しない限り、0 です。  
  
 ARD SQL_DESC_INDICATOR_PTR フィールドが null ポインターの場合、ドライバーは、列が NULL かどうかに関する情報を返すできなくなります。 列が NULL の場合 SQL_DESC_INDICATOR_PTR が null ポインター、SQLSTATE 22002 (インジケーター変数に必要なが指定されていません) が返されます、ドライバーが呼び出しの後にバッファーに格納しようとしたときと**SQLFetch**または**SQLFetchScroll**します。 場合に呼び出し**SQLFetch**または**SQLFetchScroll** SQL_SUCCESS または SQL_SUCCESS_WITH_INFO、バッファーの内容は定義されていないが返されませんでした。  
  
 SQL_DESC_INDICATOR_PTR フィールドは、SQL_DESC_OCTET_LENGTH_PTR によって示されるフィールドが設定されているかどうかを判断します。 列のデータ値が NULL の場合、ドライバーは SQL_NULL_DATA をインジケーター変数を設定します。 SQL_DESC_OCTET_LENGTH_PTR によって示されるフィールドはありませんが設定されます。 NULL 値がフェッチ中に発生しない場合は、SQL_DESC_INDICATOR_PTR によって指し示されるバッファーが 0 に設定されているし、SQL_DESC_OCTET_LENGTH_PTR によって指し示されるバッファーが、データの長さに設定されています。  
  
 APD の SQL_DESC_INDICATOR_PTR フィールドが null ポインターの場合、アプリケーションは、NULL 引数を指定するこの記述子のレコードを使用することはできません。  
  
 このフィールドは、*遅延フィールド*:時に設定されているが、使用は後で、ドライバーによって (標準) を null 値許容属性を示す、または (Apd) の null 値許容属性を確認するには使用されません。  
  
 **SQL_DESC_LABEL [IRDs]**  
 この読み取り専用の SQLCHAR * レコード フィールドには、列のラベルまたはタイトルが含まれています。 列がラベルを持たない場合、この変数には、列名が含まれています。 列が名前のない、ラベルが付いていない場合は、この変数には、空の文字列が含まれています。  
  
 **[すべて] SQL_DESC_LENGTH**  
 Sqlulen ですレコード フィールドは、文字の文字列の最大値または実際の長さまたはバイトのバイナリ データ型のいずれかです。 固定長データ型の最大長または可変長データ型の実際の長さになります。 常に、その値には、文字の文字列を終了する null 終了文字が含まれません。 型が SQL_TYPE_DATE、SQL_TYPE_TIME、sql_type_timestamp 型、または SQL の interval データ型のいずれかの値は、このフィールドに、長さは、datetime または間隔の値の文字の文字列表現の文字。  
  
 このフィールドの値が""として定義されている長さ ODBC 2 の値と異なる場合があります *.x*します。 詳細については、次を参照してください[付録 d:。データ型](../../../odbc/reference/appendixes/appendix-d-data-types.md)します。  
  
 **SQL_DESC_LITERAL_PREFIX [IRDs]**  
 この読み取り専用の SQLCHAR * レコード フィールドには、このデータ型のリテラルのプレフィックスとして、ドライバーが認識できる文字が含まれています。 この変数には、空の文字列データ型のリテラル プレフィックスは適用されませんが含まれています。  
  
 **SQL_DESC_LITERAL_SUFFIX [IRDs]**  
 この読み取り専用の SQLCHAR * レコード フィールドには、このデータ型のリテラルのサフィックスとして、ドライバーが認識できる文字が含まれています。 この変数には、空の文字列データ型のリテラル サフィックスは適用されませんが含まれています。  
  
 **SQL_DESC_LOCAL_TYPE_NAME [実装記述子]**  
 この読み取り専用の SQLCHAR * レコード フィールドにはデータ型の正規名と異なる可能性があるデータ型の任意のローカライズされた (ネイティブ言語) 名前が含まれています。 ローカライズされた名前がない場合は、空の文字列が返されます。 このフィールドは、表示目的でのみです。  
  
 **SQL_DESC_NAME [実装記述子]**  
 この SQLCHAR * 行記述子のレコードのフィールドが適用される場合に、列の別名では、含まれています。 列の別名が適用されない場合は、列名が返されます。 どちらの場合、ドライバーは、SQL_DESC_NAME フィールドを設定するときにできません SQL_DESC_UNNAMED フィールドを設定します。 列名がありませんまたは列の別名がある場合、ドライバーは、SQL_DESC_NAME フィールド内の空の文字列を返し、SQL_UNNAMED を SQL_DESC_UNNAMED フィールドを設定します。  
  
 アプリケーションでは、パラメーター名または名前でストアド プロシージャのパラメーターを指定するエイリアスに、IPD の SQL_DESC_NAME フィールドを設定できます。 (詳細については、次を参照してください[(名前付きパラメーター) の名前によるパラメーターのバインド](../../../odbc/reference/develop-app/binding-parameters-by-name-named-parameters.md)。)。IRD の SQL_DESC_NAME フィールドは読み取り専用フィールドです。SQLSTATE HY091 アプリケーション設定を試みる場合 (無効な記述子フィールド識別子) が返されます。  
  
 これをドライバーが名前付きパラメーターをサポートしていない場合は、このフィールドは定義されません。 ドライバーは、名前付きパラメーターをサポートし、パラメーターを記述するには、このフィールドに、パラメーター名が返されます。  
  
 **SQL_DESC_NULLABLE [実装記述子]**  
 IRDs、この読み取り専用 SQLSMALLINT のレコードのフィールドは SQL_NULLABLE 場合は、列が NULL 値を受け入れるかどうかが不明である場合、列は SQL_NO_NULLS 列には、NULL 値がない場合または SQL_NULLABLE_UNKNOWN、NULL 値を持つことができます。 このフィールドは、基本列ではなく、結果セット列に関連します。  
  
 、Ipd でこのフィールドは常に設定 SQL_NULLABLE のため動的パラメーターは常に null を許容し、アプリケーションによって設定することはできません。  
  
 **[すべて] SQL_DESC_NUM_PREC_RADIX**  
 この SQLINTEGER フィールドに値が 2 の SQL_DESC_TYPE フィールドでのデータ型が、おおよその数値データ型の場合 SQL_DESC_PRECISION フィールドには、ビット数が含まれています。 このフィールドに値を 10 SQL_DESC_TYPE フィールドでのデータ型が、正確な数値データ型の場合 SQL_DESC_PRECISION フィールドには、10 進数字の数が含まれています。 このフィールドは、すべての数値以外のデータ型の場合は 0 に設定されます。  
  
 **[すべて] SQL_DESC_OCTET_LENGTH**  
 この SQLLEN レコード フィールドには、文字の文字列またはバイナリ データ型の長さ、(バイト単位) が含まれています。 固定長の文字またはバイナリ型では、これは、実際の長さ (バイト単位)。 可変長の文字またはバイナリ型では、これは、最大長 (バイト単位)。 この値は、実装記述子の null 終端文字のための領域を常に除外され、アプリケーション記述子の null 終端文字のための領域を常に含まれます。 アプリケーションのデータは、このフィールドには、バッファーのサイズが含まれています。 Apd の場合、このフィールドは、出力または入力/出力パラメーターに対してのみ定義されます。  
  
 **SQL_DESC_OCTET_LENGTH_PTR [アプリケーション記述子]**  
 この SQLLEN * フィールドがポイントするか (行記述子) のバインドされた列の値の (パラメーター記述子) の動的引数の合計長 (バイト単位) を格納する変数を記録します。  
  
 文字の文字列とバイナリを除くすべての引数の APD のこの値が無視されます。このフィールドは、SQL_NTS をポイントしている場合、null で終わる動的引数がある必要があります。 バインドされたパラメーターは、実行時データ パラメーターになることは、アプリケーションこのフィールドを設定、APD のレコードの適切な変数にすることを示します、実行時では、値 SQL_DATA_AT_EXEC または SQL_LEN_DATA_AT_EXEC マクロの結果を含む. このような 1 つ以上のフィールドがある場合、パラメーターが要求されている特定のアプリケーションに役立つ、SQL_DESC_DATA_PTR をパラメーターを一意に識別する値に設定できます。  
  
 ARD OCTET_LENGTH_PTR フィールドが null ポインターの場合、ドライバーは、列の長さの情報を返しません。 APD の SQL_DESC_OCTET_LENGTH_PTR フィールドが null ポインターの場合、ドライバーでは、文字の文字列とバイナリ値が null で終わる前提としています。 (バイナリ値は null で終了することはできませんが、長さの切り捨てを回避するために指定する必要があります)。  
  
 場合に呼び出し**SQLFetch**または**SQLFetchScroll**をこのフィールドで指し示されるバッファー内の塗りつぶしを返しませんでした SQL_SUCCESS または SQL_SUCCESS_WITH_INFO、バッファーの内容は未定義です。 このフィールドは、*遅延フィールド*します。 設定されているを確認したり、データのオクテットの長さを示すために後で、ドライバーによって使用時に使用されません。  
  
 **SQL_DESC_PARAMETER_TYPE [Ipd]**  
 この SQLSMALLINT レコード フィールドが入力パラメーターの入力/出力パラメーター、出力パラメーター、入力/出力ストリームのパラメーターの SQL_PARAM_INPUT_OUTPUT_STREAM または sql _ の SQL_PARAM_OUTPUT SQL_PARAM_INPUT_OUTPUT SQL_PARAM_INPUT を設定します。ストリーミングされた出力パラメーターの PARAM_OUTPUT_STREAM します。 既定では SQL_PARAM_INPUT に設定されます。  
  
 IPD では、フィールドは SQL_PARAM_INPUT を既定で設定 (SQL_ATTR_ENABLE_AUTO_IPD ステートメント属性は sql_false になります)、ドライバーでは、IPD が自動的に設定されていない場合。 アプリケーションでは、入力パラメーターのないパラメーターがの IPD でこのフィールドを設定する必要があります。  
  
 **[すべて] SQL_DESC_PRECISION**  
 この SQLSMALLINT レコード フィールドには、正確な数値型 (バイナリ精度) が、概数型の仮数部のビット数または SQL_TYPE_TIME、SQL_TYPE の秒の小数部のコンポーネントの桁の数字の桁数が含まれています_TIMESTAMP、または SQL_INTERVAL_SECOND データを入力します。 このフィールドは、他のすべてのデータ型に定義されていません。  
  
 このフィールドの値は"precision"として ODBC 2 で定義されているの値と異なる場合があります *.x*します。 詳細については、次を参照してください[付録 d:。データ型](../../../odbc/reference/appendixes/appendix-d-data-types.md)します。  
  
 **SQL_DESC_ROWVER [実装記述子]**  
 この SQLSMALLINTrecord フィールドは、(たとえば、SQL Server では、"timestamp"型の列)、行が更新されたときに、列が自動的に、DBMS によって変更するかどうかを示します。 このレコード フィールドの値は、それ以外の場合に列が、行のバージョン管理の列の場合は SQL_TRUE および SQL_FALSE に設定されます。 この列の属性は、呼び出しに似ています**SQLSpecialColumns** IdentifierType の SQL_ROWVER 列が自動的に更新されているかどうかを判断するとします。  
  
 **[すべて] SQL_DESC_SCALE**  
 この SQLSMALLINT レコード フィールドには、decimal および numeric のデータ型の定義のスケールが含まれています。 フィールドは、その他のすべてのデータ型に定義されていません。  
  
 このフィールドの値は、ODBC 2 で定義されている"scale"の値と異なる場合があります *.x*します。 詳細については、次を参照してください[付録 d:。データ型](../../../odbc/reference/appendixes/appendix-d-data-types.md)します。  
  
 **SQL_DESC_SCHEMA_NAME [IRDs]**  
 この読み取り専用の SQLCHAR * レコード フィールドに列を含むベース テーブルのスキーマ名が含まれています。 戻り値にはドライバーによって異なりますが、列が式の場合、または列がビューの一部である場合です。 データ ソースがスキーマをサポートしていない、またはスキーマ名が確認できない、この変数には、空の文字列が含まれています。  
  
 **SQL_DESC_SEARCHABLE [IRDs]**  
 この読み取り専用 SQLSMALLINT のレコードのフィールドは、次の値のいずれかに設定されます。  
  
-   SQL_PRED_NONE で列を使用できない場合、**WHERE**句。 (これは、ODBC 2 で SQL_UNSEARCHABLE 値として同じ *.x*)。  
  
-   SQL_PRED_CHAR 列で使用できる場合は、**WHERE**しかない句、**LIKE**述語。 (これは、ODBC 2 で SQL_LIKE_ONLY 値として同じ *.x*)。  
  
-   SQL_PRED_BASIC 列で使用できる場合は、**WHERE**を除くすべての比較演算子を含む句**LIKE**します。 (これは、ODBC 2 で SQL_EXCEPT_LIKE 値として同じ *.x*)。  
  
-   SQL_PRED_SEARCHABLE 列で使用できる場合は、**WHERE**任意の比較演算子を含む句。  
  
 **SQL_DESC_TABLE_NAME [IRDs]**  
 この読み取り専用の SQLCHAR * レコード フィールドには、この列を格納するベース テーブルの名前が含まれています。 戻り値にはドライバーによって異なりますが、列が式の場合、または列がビューの一部である場合です。  
  
 **[すべて] SQL_DESC_TYPE**  
 この SQLSMALLINT レコード フィールドには、datetime と間隔のデータ型を除くすべてのデータ型の簡潔な SQL または C データ型を指定します。 Datetime と間隔のデータ型で、このフィールドが SQL_DATETIME または SQL_INTERVAL 詳細データの種類を指定します。  
  
 このフィールドには、SQL_DATETIME または SQL_INTERVAL が含まれています、たびに SQL_DESC_DATETIME_INTERVAL_CODE フィールドは簡潔な型の適切なサブコードを含める必要があります。 Datetime データ型の SQL_DESC_TYPE には、sql_datetime 型が含まれています、SQL_DESC_DATETIME_INTERVAL_CODE フィールドにはサブコード特定の datetime データ型にはが含まれています。 Interval データ型では、SQL_DESC_TYPE が SQL_INTERVAL に含み、SQL_DESC_DATETIME_INTERVAL_CODE フィールドには、特定の間隔のデータ型のサブコードが含まれています。  
  
 SQL_DESC_TYPE、SQL_DESC_CONCISE_TYPE フィールドの値は相互に依存します。 毎回、フィールドのいずれかが設定されている、他の設定も必要があります。 呼び出しで設定できる SQL_DESC_TYPE **SQLSetDescField**または**SQLSetDescRec**します。 呼び出しで設定できる SQL_DESC_CONCISE_TYPE **SQLBindCol**または**SQLBindParameter**、または**SQLSetDescField**します。  
  
 SQL_DESC_TYPE が期間または日時のデータ型以外の簡潔なデータ型に設定されている場合は、SQL_DESC_CONCISE_TYPE フィールドが同じ値に設定されているし、SQL_DESC_DATETIME_INTERVAL_CODE フィールドが 0 に設定します。  
  
 詳細の datetime 型または interval データ型 (SQL_DATETIME または SQL_INTERVAL) SQL_DESC_TYPE が設定されているし、適切なサブコードに SQL_DESC_DATETIME_INTERVAL_CODE フィールドが設定されている、SQL_DESC_CONCISE 型フィールドは、対応する簡潔な型に設定されます。 SQL_DESC_TYPE を簡潔な datetime または間隔の種類のいずれかに設定しようとすると、SQLSTATE HY021 が返されます (不整合な記述子情報)。  
  
 呼び出しで SQL_DESC_TYPE フィールドを設定すると**SQLBindCol**、 **SQLBindParameter**、または**SQLSetDescField**、次のフィールドは、次の既定値に設定されます次の表に示す。 同じレコードの残りのフィールドの値は未定義です。  
  
|SQL_DESC_TYPE の値|その他のフィールドが暗黙的に設定します。|  
|------------------------------|---------------------------------|  
|SQL_CHAR、SQL_VARCHAR、SQL_C_CHAR、SQL_C_VARCHAR|SQL_DESC_LENGTH は 1 に設定されます。 SQL_DESC_PRECISION は 0 に設定されます。|  
|SQL_DATETIME|SQL_CODE_DATE または SQL_CODE_TIME SQL_DESC_DATETIME_INTERVAL_CODE を設定すると、ときに、SQL_DESC_PRECISION は 0 に設定されます。 SQL_DESC_TIMESTAMP に設定されている場合は、SQL_DESC_PRECISION が 6 に設定されます。|  
|SQL_DECIMAL、SQL_NUMERIC、SQL_C_NUMERIC|SQL_DESC_SCALE は 0 に設定されます。 SQL_DESC_PRECISION は、それぞれのデータ型の実装で定義された有効桁数に設定されます。<br /><br /> 参照してください[SQL c: から数値](../../../odbc/reference/appendixes/sql-to-c-numeric.md)SQL_C_NUMERIC 値を手動でバインドする方法についてはします。|  
|使用できます、SQL_C_FLOAT|SQL_DESC_PRECISION は、使用できますの実装で定義された既定の精度に設定されます。|  
|SQL_INTERVAL|間隔のデータ型に SQL_DESC_DATETIME_INTERVAL_CODE を設定すると、SQL_DESC_DATETIME_INTERVAL_PRECISION 2 (既定の間隔先頭の有効桁数) に設定されます。 間隔の秒の部分は、ときに、SQL_DESC_PRECISION は 6 (既定の間隔 (秒) 精度) に設定されます。|  
  
 アプリケーションを呼び出すと**SQLSetDescField**の呼び出しではなく、記述子フィールドを設定する**SQLSetDescRec**アプリケーションがまずデータ型を宣言する必要があります。 このとき、前の表に示されているその他のフィールドが暗黙的に設定します。 かどうか、値のいずれかに暗黙的にセット許容されない、アプリケーションを呼び出して**SQLSetDescField**または**SQLSetDescRec**不正な値を明示的に設定します。  
  
 **SQL_DESC_TYPE_NAME [実装記述子]**  
 この読み取り専用の SQLCHAR * レコード フィールドには、データ ソースに依存する型の名前 (たとえば、"CHAR"、"VARCHAR"、およびなど) が含まれています。 データ型の名前が不明な場合は、この変数には、空の文字列が含まれています。  
  
 **SQL_DESC_UNNAMED [実装記述子]**  
 この行記述子の SQLSMALLINT レコード フィールドは、SQL_DESC_NAME フィールドを設定するとき、できませんまたは SQL_UNNAMED にドライバーによって設定されます。 SQL_DESC_NAME フィールドには、列の別名が含まれている場合、または列の別名が適用されない場合は、ドライバーはできませんを SQL_DESC_UNNAMED フィールドを設定します。 アプリケーションは、パラメーター名またはエイリアスを IPD の SQL_DESC_NAME フィールドを設定する場合、ドライバーは、IPD の SQL_DESC_UNNAMED フィールドをできませんに設定します。 列名がありませんまたは列の別名がある場合、ドライバーは SQL_UNNAMED を SQL_DESC_UNNAMED フィールドを設定します。  
  
 アプリケーションでは、SQL_UNNAMED を IPD の SQL_DESC_UNNAMED フィールドを設定できます。 ドライバーは SQLSTATE HY091 を返します (無効な記述子フィールド識別子) 場合、アプリケーションは、IPD の SQL_DESC_UNNAMED フィールドできませんに設定しようとしています。 IRD の SQL_DESC_UNNAMED フィールドは読み取り専用です。SQLSTATE HY091 アプリケーション設定を試みる場合 (無効な記述子フィールド識別子) が返されます。  
  
 **SQL_DESC_UNSIGNED [実装記述子]**  
 この読み取り専用 SQLSMALLINT のレコードのフィールドは、列の型が署名されている場合、列の型が符号なしまたは数値以外の場合は SQL_TRUE または SQL_FALSE に設定されます。  
  
 **SQL_DESC_UPDATABLE [IRDs]**  
 この読み取り専用 SQLSMALLINT のレコードのフィールドは、次の値のいずれかに設定されます。  
  
-   SQL_ATTR_READ_ONLY 場合は、結果セット列とは、読み取り専用です。  
  
-   SQL_ATTR_WRITE 結果セット列の場合は、読み取り/書き込みです。  
  
-   SQL_ATTR_READWRITE_UNKNOWN 結果セット列であるかどうかが不明である場合は更新可能でかどうか。  
  
 SQL_DESC_UPDATABLE では、ベース テーブルの列ではなく、結果セットの列の更新について説明します。 この結果セット列の基になるベース テーブル内の列の更新は、このフィールドの値と異なる可能性があります。 列は更新可能かどうかは、データ型、ユーザーの特権と、結果セット自体の定義に基づくことができます。 明確ではありません、列は更新可能かどうか、SQL_ATTR_READWRITE_UNKNOWN が返されます。  
  
## <a name="consistency-checks"></a>整合性チェック  
 ARD、APD、または IPD の SQL_DESC_DATA_PTR フィールドの値で、アプリケーションに合格するたびに、整合性チェックは、ドライバーによって自動的に実行します。 任意のフィールドが、他のフィールドと一致しない場合**SQLSetDescField** SQLSTATE HY021 が返されます (不整合な記述子情報)。 詳細についてを参照してください「整合性チェック」 [SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)します。  
  
## <a name="related-functions"></a>関連する関数  
  
|詳細|参照先|  
|---------------------------|---------|  
|列のバインド|[SQLBindCol 関数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|パラメーターのバインド|[SQLBindParameter 関数](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|記述子フィールドの取得|[SQLGetDescField 関数](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|複数の記述子フィールドの取得|[SQLGetDescRec 関数](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|複数の記述子フィールドの設定|[SQLSetDescRec 関数](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
  
## <a name="see-also"></a>参照  
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)   
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)
