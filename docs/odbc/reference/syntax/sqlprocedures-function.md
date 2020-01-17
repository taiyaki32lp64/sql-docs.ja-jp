---
title: SQLProcedures 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLProcedures
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLProcedures
helpviewer_keywords:
- SQLProcedures function [ODBC]
ms.assetid: d0d9ef10-2fd4-44a5-9334-649f186f4ba0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1bdaf63313a339d2b25ca6648ad25c1b4466b3f8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68005733"
---
# <a name="sqlprocedures-function"></a>SQLProcedures 関数
**準拠**  
 バージョンが導入されました。ODBC 1.0 規格に準拠します。ODBC  
  
 **まとめ**  
 **SQLProcedures**特定のデータ ソースに格納されているプロシージャ名の一覧を返します。 *プロシージャ*記述に使用される一般的な用語には、*実行可能オブジェクト*、または入力と出力パラメーターを使用して呼び出すことができる名前付きエンティティ。 手順の詳細については、次を参照してください。、[プロシージャ](../../../odbc/reference/develop-app/procedures-odbc.md)します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLProcedures(  
     SQLHSTMT       StatementHandle,  
     SQLCHAR *      CatalogName,  
     SQLSMALLINT    NameLength1,  
     SQLCHAR *      SchemaName,  
     SQLSMALLINT    NameLength2,  
     SQLCHAR *      ProcName,  
     SQLSMALLINT    NameLength3);  
```  
  
## <a name="arguments"></a>引数  
 *StatementHandle*  
 [入力]ステートメント ハンドルです。  
  
 *カタログ名*  
 [入力]プロシージャのカタログです。 ドライバーは、いくつかのテーブルのドライバーをさまざまな Dbms、空の文字列からデータを取得した場合など、他ではなく、カタログをサポートしている場合 ("") のカタログはありません。 それらのテーブルを表します。 *CatalogName*文字列の検索パターンを含めることはできません。  
  
 SQL_ATTR_METADATA_ID ステートメント属性は、SQL_TRUE に設定されている場合*CatalogName*は識別子として扱われますそのケースは重要ではありません。 場合は sql_false になります、 *CatalogName*は通常の引数です。 文字どおり、扱われ、そのケースは重要では。 詳細については、次を参照してください。[カタログ関数の引数](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)します。  
  
 *NameLength1*  
 [入力]文字の長さ **CatalogName*します。  
  
 *スキーマ名*  
 [入力]プロシージャのスキーマ名の文字列の検索パターン。 ドライバーをドライバーがさまざまな Dbms、空の文字列からデータを取得する場合など、他ではなく一部のプロシージャのスキーマをサポートしている場合 ("") のスキーマはありません。 それらの手順を示します。  
  
 SQL_ATTR_METADATA_ID ステートメント属性は、SQL_TRUE に設定されている場合*SchemaName*は識別子として扱われますそのケースは重要ではありません。 場合は sql_false になります、 *SchemaName*パターン引数の値は、; 文字どおり、扱われ、そのケースは重要です。  
  
 *NameLength2*  
 [入力]文字の長さ **SchemaName*します。  
  
 *ProcName*  
 [入力]プロシージャ名の文字列の検索パターン。  
  
 SQL_ATTR_METADATA_ID ステートメント属性は、SQL_TRUE に設定されている場合*ProcName*は識別子として扱われますそのケースは重要ではありません。 場合は sql_false になります、 *ProcName*パターン引数の値は、; 文字どおり、扱われ、そのケースは重要です。  
  
 *NameLength3*  
 [入力]文字の長さ **ProcName*します。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_STILL_EXECUTING、SQL_ERROR、または SQL_INVALID_HANDLE します。  
  
## <a name="diagnostics"></a>診断  
 ときに**SQLProcedures** SQL_ERROR または SQL_SUCCESS_WITH_INFO、関連付けられている SQLSTATE 値を返しますを呼び出すことによって取得できる**SQLGetDiagRec**で、 *HandleType* sql _ のHANDLE_STMT と*処理*の*StatementHandle*します。 次の表に、一般的にによって返される SQLSTATE 値**SQLProcedures** ; この関数のコンテキストでそれぞれについて説明しますと表記"(DM)"の前にドライバー マネージャーによって返されるについての説明。 SQLSTATE 値ごとに関連付けられているリターン コードは明記しない限り、SQL_ERROR です。  
  
|SQLSTATE|[エラー]|説明|  
|--------------|-----------|-----------------|  
|01000|一般的な警告|ドライバー固有の情報メッセージです。 (関数は、SQL_SUCCESS_WITH_INFO を返します)。|  
|08S01|通信リンク エラー|関数が完了した処理の前に、ドライバーとドライバーが接続されているデータ ソース間の通信リンクに失敗しました。|  
|24000|カーソル状態が無効|カーソルが開いて、 *StatementHandle*、および**SQLFetch**または**SQLFetchScroll**が呼び出されました。 このエラーが返されますドライバー マネージャーによって**SQLFetch**または**SQLFetchScroll** 、SQL_NO_DATA が返されなかったと場合、ドライバーによって返される**SQLFetch**または**SQLFetchScroll** SQL_NO_DATA が返されます。<br /><br /> カーソルが開いて、 *StatementHandle*が**SQLFetch**または**SQLFetchScroll**呼び出されていない必要があります。|  
|40001|シリアル化エラー|トランザクションが別のトランザクションでリソース デッドロックによりロールバックされました。|  
|40003|不明なステートメント入力候補|、この関数の実行中に、関連付けられた接続が失敗し、トランザクションの状態を特定できません。|  
|HY000|一般的なエラー|これがなかった固有の SQLSTATE とする実装に固有の SQLSTATE が定義されていない、エラーが発生しました。 によって返されるエラー メッセージ**SQLGetDiagRec**で、  *\*MessageText*バッファーは、エラーとその原因について説明します。|  
|HY001|メモリの割り当てエラー|ドライバーは、実行または関数の完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY008|操作が取り消されました|非同期処理が有効に、 *StatementHandle*します。 関数が呼び出された、および実行を完了する前に**SQLCancel**または**SQLCancelHandle**が呼び出されて、 *StatementHandle*します。 後でもう一度関数が呼び出された、 *StatementHandle*します。<br /><br /> 関数が呼び出された、および実行を完了する前に**SQLCancel**または**SQLCancelHandle**が呼び出されて、 *StatementHandle*から別のスレッドで、マルチ スレッド アプリケーションです。|  
|HY009|無効な null ポインターの使用|SQL_ATTR_METADATA_ID のステートメント属性、SQL_TRUE に設定されて、 *CatalogName*引数が null ポインターの場合は、および、SQL_CATALOG_NAME*情報の種類*カタログ名を返しますがサポートされています。<br /><br /> (DM) SQL_ATTR_METADATA_ID ステートメント属性の SQL_TRUE に設定された、 *SchemaName*または*ProcName*引数が null ポインター。|  
|HY010|関数のシーケンス エラー|(DM) を非同期的に実行中の関数が呼び出された接続ハンドルに関連付けられているため、 *StatementHandle*します。 この非同期関数は、この関数が呼び出されたときにまだ実行中だった。<br /><br /> (DM) **SQLExecute**、 **SQLExecDirect**、または**SQLMoreResults**に対して呼び出された、 *StatementHandle* SQL_PARAM_DATA_ を返されます。ご利用いただけます。 ストリームのすべてのパラメーターのデータが取得される前に、この関数が呼び出されました。<br /><br /> (DM) を非同期的に実行中の関数 (いないこの"1") が呼び出された、 *StatementHandle*この関数が呼び出されたときに実行されているとします。<br /><br /> (DM) **SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**、または**SQLSetPos**に対して呼び出された、 *StatementHandle* SQL_NEED_DATA が返されます。 すべての実行時データ パラメーターまたは列のデータが送信される前に、この関数が呼び出されました。|  
|HY013|メモリ管理エラー|基になるメモリ オブジェクトにアクセスできませんでした、場合によってメモリ不足が原因であるために、関数呼び出しを処理できませんでした。|  
|HY090|文字列またはバッファーの長さが無効です。|(DM) 名の長の引数のいずれかの値が 0 未満でしたが、SQL_NTS と等しくありません。<br /><br /> 名の長の引数のいずれかの値には、対応する名前の最大長の値を超えています。|  
|HY117|不明なトランザクションの状態のため、接続が中断されます。 のみを切断して、読み取り専用の関数が許可されます。|(DM) 中断状態の詳細については、次を参照してください。 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)します。|  
|HYC00|省略可能な機能が実装されていません|プロシージャのカタログが指定されていると、ドライバーまたはデータ ソースがカタログをサポートしていません。<br /><br /> プロシージャのスキーマが指定されていると、ドライバーまたはデータ ソース スキーマはサポートしません。<br /><br /> プロシージャのスキーマまたはプロシージャ名、文字列の検索パターンが指定されて、データ ソースがこれらの引数の 1 つ以上の検索パターンをサポートしていません。<br /><br /> SQL_ATTR_CURSOR_TYPE、SQL_ATTR_CONCURRENCY ステートメント属性の現在の設定の組み合わせが、ドライバーまたはデータ ソースでサポートされていません。<br /><br /> SQL_ATTR_USE_BOOKMARKS ステートメント属性は SQL_UB_VARIABLE に設定されており、SQL_ATTR_CURSOR_TYPE ステートメント属性は、ドライバーがブックマークをできません、カーソルの種類に設定されました。|  
|HYT00|タイムアウトが発生しました|クエリのタイムアウト期間は、要求された結果セットが返されるデータ ソースの前に有効期限が切れました。 によって、タイムアウト期間が設定されます**SQLSetStmtAttr**、SQL_ATTR_QUERY_TIMEOUT します。|  
|HYT01|接続がタイムアウトしました|データ ソースが要求に応答する前に、接続のタイムアウト期間が終了しました。 によって、接続タイムアウト期間が設定されます**SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT します。|  
|IM001|ドライバーでは、この関数はサポートされていません|(DM) に、ドライバーが関連付けられている、 *StatementHandle*この関数をサポートしていません。|  
|IM017|非同期通知モードでのポーリングは無効です。|通知のモデルを使用すると、常にポーリングは無効です。|  
|IM018|**SQLCompleteAsync**このハンドルに対する前の非同期操作を完了が呼び出されていません。|通知モードが有効になっている場合、ハンドルでは、前の関数呼び出しに SQL_STILL_EXECUTING が返された場合と**SQLCompleteAsync**後処理を行い、操作を完了するハンドルで呼び出す必要があります。|  
  
## <a name="comments"></a>コメント  
 **SQLProcedures**要求された範囲内のすべての手順を示します。 ユーザーにもこれらの手順を実行する権限がない可能性があります。 アクセシビリティを確認するアプリケーションを呼び出すことができます**SQLGetInfo** SQL_ACCESSIBLE_PROCEDURES 情報の値を確認します。 それ以外の場合、アプリケーションは、ユーザーが、プロシージャが実行できないことを選択した状況に対処できる必要があります。 この情報の用途については、次を参照してください。[プロシージャ](../../../odbc/reference/develop-app/procedures-odbc.md)します。  
  
> [!NOTE]  
>  一般的な使用、引数、および ODBC カタログ関数の返されたデータの詳細については、次を参照してください。[カタログ関数](../../../odbc/reference/develop-app/catalog-functions.md)します。  
  
 **SQLProcedures** PROCEDURE_CAT、PROCEDURE_SCHEMA、PROCEDURE_NAME、順序付けられた、標準的な結果セットとして結果を返します。  
  
> [!NOTE]  
>  **SQLProcedures**のすべてのプロシージャを返さなかった可能性があります。 アプリケーションがによって返されるかどうかに関係なく、任意の有効なプロシージャを使用できます**SQLProcedures**します。  
  
 次の列が ODBC 3 の名前が変更された *.x*します。 列名の変更では、アプリケーションは、列番号でバインドため、旧バージョンとの互換性は影響しません。  
  
|ODBC 2.0 列|ODBC 3 *.x*列|  
|---------------------|-----------------------|  
|PROCEDURE_QUALIFIER|PROCEDURE_CAT|  
|プロシージャ _OWNER|プロシージャ _SCHEM|  
  
 アプリケーションが呼び出すことができますを PROCEDURE_CAT、PROCEDURE_SCHEM、PROCEDURE_NAME 列の実際の長さを判断する**SQLGetInfo** SQL_MAX_CATALOG_NAME_LEN、SQL_MAX_SCHEMA_NAME_LEN、SQL_MAX_PROCEDURE_ とNAME_LEN オプション。  
  
 次の表には、結果セット内の列が一覧表示します。 ドライバーでは、8 (PROCEDURE_TYPE) 列を超える追加の列を定義できます。 アプリケーションでは、明示的な序数位置を指定するのではなく、結果セットの末尾からカウント ダウンによって、ドライバー固有の列へのアクセスを得る必要があります。 詳細については、次を参照してください。[カタログ関数によって返されるデータ](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)します。  
  
|列名|列番号|データ型|コメント|  
|-----------------|-------------------|---------------|--------------|  
|PROCEDURE_CAT (ODBC 2.0)|1|Varchar|プロシージャのカタログの識別子。データ ソースに適用されない場合は NULL です。 ドライバーの空の文字列を返します、ドライバーは、さまざまな Dbms からデータを取得するときなどに、他のユーザーではなく一部のプロシージャのカタログをサポートする場合 ("") のカタログはありません。 それらの手順。|  
|PROCEDURE_SCHEM (ODBC 2.0)|2|Varchar|プロシージャのスキーマの識別子。データ ソースに適用されない場合は NULL です。 ドライバーの空の文字列を返します、ドライバーは、さまざまな Dbms からデータを取得するときなどに、他のユーザーではなく一部のプロシージャのスキーマをサポートする場合 ("") のスキーマはありません。 それらの手順。|  
|PROCEDURE_NAME (ODBC 2.0)|3|NULL 以外の Varchar|プロシージャの識別子です。|  
|NUM_INPUT_PARAMS (ODBC 2.0)|4|なし|将来使用するために予約されています。 アプリケーションは、これらの結果の列で返されるデータに依存させないでください。|  
|NUM_OUTPUT_PARAMS (ODBC 2.0)|5|なし|将来使用するために予約されています。 アプリケーションは、これらの結果の列で返されるデータに依存させないでください。|  
|NUM_RESULT_SETS (ODBC 2.0)|6|なし|将来使用するために予約されています。 アプリケーションは、これらの結果の列で返されるデータに依存させないでください。|  
|「解説」(ODBC 2.0)|7|Varchar|プロシージャの説明です。|  
|PROCEDURE_TYPE (ODBC 2.0)|8|Smallint|プロシージャの種類を定義します。<br /><br /> SQL_PT_UNKNOWN:プロシージャが値を返すかどうかを特定できません。<br /><br /> SQL_PT_PROCEDURE:返されるオブジェクトはプロシージャです。つまり、戻り値はありません。<br /><br /> :返されるオブジェクトが関数です。つまり、戻り値があります。|  
  
 *SchemaName*と*ProcName*引数は、検索パターンをそのまま使用します。 有効な検索パターンの詳細については、次を参照してください。[パターン値の引数](../../../odbc/reference/develop-app/pattern-value-arguments.md)します。  
  
## <a name="code-example"></a>コード例  
 参照してください[プロシージャ呼び出し](../../../odbc/reference/develop-app/procedure-calls.md)します。  
  
## <a name="related-functions"></a>関連する関数  
  
|詳細|参照先|  
|---------------------------|---------|  
|バッファーを結果セット内の列にバインドします。|[SQLBindCol 関数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|ステートメントの処理をキャンセル|[SQLCancel 関数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|1 つの行または順方向専用の方向にデータのブロックをフェッチしています|[SQLFetch 関数](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|データのブロックをフェッチしています。 または、結果をスクロールの設定|[SQLFetchScroll 関数](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|ドライバーまたはデータ ソースに関する情報を返す|[SQLGetInfo 関数](../../../odbc/reference/syntax/sqlgetinfo-function.md)|  
|プロシージャの列に設定されたパラメーターと結果を返す|[SQLProcedureColumns 関数](../../../odbc/reference/syntax/sqlprocedurecolumns-function.md)|  
|ストアド プロシージャを呼び出すための構文|[ステートメントの実行](../../../odbc/reference/develop-app/executing-statements-odbc.md)|  
  
## <a name="see-also"></a>参照  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)
