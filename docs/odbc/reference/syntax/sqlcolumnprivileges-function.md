---
title: SQLColumnPrivileges 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLColumnPrivileges
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLColumnPrivileges
helpviewer_keywords:
- SQLColumnPrivileges function [ODBC]
ms.assetid: ef233d9a-6ed5-4986-9d42-5e0b1a79fb6e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5e3c54e0e2eb4ad633d35159e1ff010c9388f5d3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68118713"
---
# <a name="sqlcolumnprivileges-function"></a>SQLColumnPrivileges 関数
**準拠**  
 バージョンが導入されました。ODBC 1.0 規格に準拠します。ODBC  
  
 **まとめ**  
 **SQLColumnPrivileges**列と指定したテーブルに関連付けられている権限の一覧を返します。 ドライバーは結果セットとして、指定した情報を返します*StatementHandle*します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLColumnPrivileges(  
     SQLHSTMT      StatementHandle,  
     SQLCHAR *     CatalogName,  
     SQLSMALLINT   NameLength1,  
     SQLCHAR *     SchemaName,  
     SQLSMALLINT   NameLength2,  
     SQLCHAR *     TableName,  
     SQLSMALLINT   NameLength3,  
     SQLCHAR *     ColumnName,  
     SQLSMALLINT   NameLength4);  
```  
  
## <a name="arguments"></a>引数  
 *StatementHandle*  
 [入力]ステートメント ハンドルです。  
  
 *カタログ名*  
 [入力]カタログの名前。 ドライバーは、ドライバーをさまざまな Dbms、空の文字列からデータを取得した場合など、他ではなく一部のカタログの名前をサポートしている場合 ("") の名前を持たないフルテキスト カタログを表します。 *CatalogName*文字列の検索パターンを含めることはできません。  
  
 SQL_ATTR_METADATA_ID ステートメント属性は、SQL_TRUE に設定されている場合*CatalogName*は識別子として扱われますそのケースは重要ではありません。 場合は sql_false になります、 *CatalogName*は通常の引数です。 文字どおり、扱われ、そのケースは重要では。 詳細については、次を参照してください。[カタログ関数の引数](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)します。  
  
 *NameLength1*  
 [入力]文字の長さ **CatalogName*します。  
  
 *スキーマ名*  
 [入力]スキーマ名です。 ドライバーは、ドライバーをさまざまな Dbms、空の文字列からデータを取得した場合など、他ではなく一部のテーブルのスキーマをサポートしている場合 ("") のスキーマはありません。 それらのテーブルを表します。 *SchemaName*文字列の検索パターンを含めることはできません。  
  
 SQL_ATTR_METADATA_ID ステートメント属性は、SQL_TRUE に設定されている場合*SchemaName*は識別子として扱われます。 場合は sql_false になります、 *SchemaName*は通常の引数です。 文字どおり、扱われ、そのケースは重要では。  
  
 *NameLength2*  
 [入力]文字の長さ **SchemaName*します。  
  
 *TableName*  
 [入力]テーブル名です。 この引数は、null ポインターにすることはできません。 *TableName*文字列の検索パターンを含めることはできません。  
  
 SQL_ATTR_METADATA_ID ステートメント属性は、SQL_TRUE に設定されている場合*TableName*は識別子として扱われますそのケースは重要ではありません。 場合は sql_false になります、 *TableName*は通常の引数です。 文字どおり、扱われ、そのケースは重要では。  
  
 *NameLength3*  
 [入力]文字の長さ **TableName*します。  
  
 *[ColumnName]*  
 [入力]列名の文字列の検索パターン。  
  
 SQL_ATTR_METADATA_ID ステートメント属性は、SQL_TRUE に設定されている場合*ColumnName*は識別子として扱われますそのケースは重要ではありません。 場合は sql_false になります、 *ColumnName*パターン引数の値は、; 文字どおり、扱われ、そのケースは重要です。  
  
 *NameLength4*  
 [入力]文字の長さ **ColumnName*します。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_STILL_EXECUTING、SQL_ERROR、または SQL_INVALID_HANDLE します。  
  
## <a name="diagnostics"></a>診断  
 ときに**SQLColumnPrivileges** SQL_ERROR または SQL_SUCCESS_WITH_INFO、関連付けられている SQLSTATE 値を返しますを呼び出すことによって取得される可能性があります**SQLGetDiagRec**で、 *HandleType*sql_handle_stmt としての*処理*の*StatementHandle*します。 次の表に、一般的にによって返される SQLSTATE 値**SQLColumnPrivileges** ; この関数のコンテキストでそれぞれについて説明しますと表記"(DM)"の前に、ドライバーによって返されるについての説明マネージャー。 SQLSTATE 値ごとに関連付けられているリターン コードは明記しない限り、SQL_ERROR です。  
  
|SQLSTATE|[エラー]|説明|  
|--------------|-----------|-----------------|  
|01000|一般的な警告|ドライバー固有の情報メッセージです。 (関数は、SQL_SUCCESS_WITH_INFO を返します)。|  
|08S01|通信リンク エラー|関数が完了した処理の前に、ドライバーとドライバーが接続されているデータ ソース間の通信リンクに失敗しました。|  
|24000|カーソル状態が無効|カーソルが開いて、 *StatementHandle、* と**SQLFetch**または**SQLFetchScroll**が呼び出されました。 このエラーが返されますドライバー マネージャーによって**SQLFetch**または**SQLFetchScroll** 、SQL_NO_DATA が返されなかったと場合、ドライバーによって返される**SQLFetch**または**SQLFetchScroll** SQL_NO_DATA が返されます。<br /><br /> カーソルが開いて、 *StatementHandle*が**SQLFetch**または**SQLFetchScroll**呼び出されていない必要があります。|  
|40001|シリアル化エラー|トランザクションが別のトランザクションでリソース デッドロックによりロールバックされました。|  
|40003|不明なステートメント入力候補|、この関数の実行中に、関連付けられた接続が失敗し、トランザクションの状態を特定できません。|  
|HY000|一般的なエラー|これがなかった固有の SQLSTATE とする実装に固有の SQLSTATE が定義されていない、エラーが発生しました。 によって返されるエラー メッセージ**SQLGetDiagRec**で、  *\*MessageText*バッファーは、エラーとその原因について説明します。|  
|HY001|メモリの割り当てエラー|ドライバーは、実行または関数の完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY008|操作が取り消されました|非同期処理が有効に、 *StatementHandle*します。 関数が呼び出された、および実行を完了する前に**SQLCancel**または**SQLCancelHandle**が呼び出されて、 *StatementHandle*します。 後でもう一度関数が呼び出された、 *StatementHandle*します。<br /><br /> 関数が呼び出された、および実行を完了する前に**SQLCancel**または**SQLCancelHandle**が呼び出されて、 *StatementHandle*から別のスレッドで、マルチ スレッド アプリケーションです。|  
|HY009|無効な null ポインターの使用|*TableName*引数が null ポインター。<br /><br /> SQL_ATTR_METADATA_ID のステートメント属性、SQL_TRUE に設定されて、 *CatalogName*引数が null ポインターの場合は、および、SQL_CATALOG_NAME*情報の種類*カタログ名を返しますがサポートされています。<br /><br /> (DM) SQL_ATTR_METADATA_ID ステートメント属性の SQL_TRUE に設定された、 *SchemaName*または*ColumnName*引数が null ポインター。|  
|HY010|関数のシーケンス エラー|(DM) を非同期的に実行中の関数が呼び出された接続ハンドルに関連付けられているため、 *StatementHandle*します。 この非同期関数は、この関数が呼び出されたときにまだ実行中だった。<br /><br /> (DM) **SQLExecute**、 **SQLExecDirect**、または**SQLMoreResults**に対して呼び出された、 *StatementHandle* SQL_PARAM_DATA_ を返されます。ご利用いただけます。 ストリームのすべてのパラメーターのデータが取得される前に、この関数が呼び出されました。<br /><br /> (DM) を非同期的に実行中の関数 (いないこの"1") が呼び出された、 *StatementHandle*この関数が呼び出されたときに実行されているとします。<br /><br /> (DM) **SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**、または**SQLSetPos**に対して呼び出された、 *StatementHandle* SQL_NEED_DATA が返されます。 すべての実行時データ パラメーターまたは列のデータが送信される前に、この関数が呼び出されました。|  
|HY013|メモリ管理エラー|基になるメモリ オブジェクトにアクセスできませんでした、場合によってメモリ不足が原因であるために、関数呼び出しを処理できませんでした。|  
|HY090|文字列またはバッファーの長さが無効です。|(DM) 名の長の引数のいずれかの値が 0 未満でしたが、SQL_NTS と等しくありません。|  
|||名の長の引数のいずれかの値には、対応する名前の最大長の値を超えています。 (「コメントです」を参照してください)|  
|HY117|不明なトランザクションの状態のため、接続が中断されます。 のみを切断して、読み取り専用の関数が許可されます。|(DM) 中断状態の詳細については、次を参照してください。 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)します。|  
|HYC00|省略可能な機能が実装されていません|カタログ名が指定されました、およびドライバーまたはデータ ソースがカタログをサポートしていません。<br /><br /> スキーマ名を指定してから、およびドライバーまたはデータ ソースがスキーマをサポートしていません。<br /><br /> 文字列の検索パターンが、列名の指定され、データ ソースがその引数の検索パターンをサポートしていません。<br /><br /> SQL_CONCURRENCY と SQL_CURSOR_TYPE ステートメント属性の現在の設定の組み合わせが、ドライバーまたはデータ ソースでサポートされていません。<br /><br /> SQL_ATTR_USE_BOOKMARKS ステートメント属性は SQL_UB_VARIABLE に設定されており、SQL_ATTR_CURSOR_TYPE ステートメント属性は、ドライバーがブックマークをできません、カーソルの種類に設定されました。|  
|HYT00|タイムアウトが発生しました|データ ソースには、結果セットが返される前に、クエリのタイムアウト期間が終了しました。 によって、タイムアウト期間が設定されます**SQLSetStmtAttr**、SQL_ATTR_QUERY_TIMEOUT します。|  
|HYT01|接続がタイムアウトしました|データ ソースが要求に応答する前に、接続のタイムアウト期間が終了しました。 によって、接続タイムアウト期間が設定されます**SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT します。|  
|IM001|ドライバーでは、この関数はサポートされていません|(DM) に、ドライバーが関連付けられている、 *StatementHandle*関数をサポートしていません。|  
|IM017|非同期通知モードでのポーリングは無効です。|通知のモデルを使用すると、常にポーリングは無効です。|  
|IM018|**SQLCompleteAsync**このハンドルに対する前の非同期操作を完了が呼び出されていません。|通知モードが有効になっている場合、ハンドルでは、前の関数呼び出しに SQL_STILL_EXECUTING が返された場合と**SQLCompleteAsync**後処理を行い、操作を完了するハンドルで呼び出す必要があります。|  
  
## <a name="comments"></a>コメント  
 **SQLColumnPrivileges** TABLE_CAT、TABLE_SCHEM、TABLE_NAME、COLUMN_NAME、および特権を並べ、標準的な結果セットとして結果を返します。  
  
> [!NOTE]  
>  **SQLColumnPrivileges**のすべての列の特権を返さなかった可能性があります。 たとえば、ドライバーでは、Oracle ROWID などの擬似列の権限に関する情報が返されません可能性があります。 アプリケーションがによって返されるかどうかにかかわらず、任意の有効な列を使用できます**SQLColumnPrivileges**します。  
  
 VARCHAR 列の長さは、テーブルには表示されません。実際の長さは、データ ソースに依存します。 CATALOG_NAME、SCHEMA_NAME、TABLE_NAME、COLUMN_NAME、列の実際の長さを決定するには、アプリケーションを呼び出すことができます**SQLGetInfo** SQL_MAX_CATALOG_NAME_LEN、SQL_MAX_SCHEMA_NAME_LEN、SQL_MAX_TABLE_NAME_ でLEN、および SQL_MAX_COLUMN_NAME_LEN オプション。  
  
> [!NOTE]  
>  一般的な使用、引数、および ODBC カタログ関数の返されたデータの詳細については、次を参照してください。[カタログ関数](../../../odbc/reference/develop-app/catalog-functions.md)します。  
  
 次の列は、ODBC 3 の名前に変更されています。*x*します。 列名の変更では、アプリケーションは、列番号でバインドため、旧バージョンとの互換性は影響しません。  
  
|ODBC 2.0 列|ODBC 3。*x*列|  
|---------------------|-----------------------|  
|TABLE_QUALIFIER|TABLE_CAT|  
|TABLE_OWNER|TABLE_SCHEM|  
  
 次の表には、結果セット内の列が一覧表示します。 ドライバーでは、8 (IS_GRANTABLE) 列を超える追加の列を定義できます。 アプリケーションでは、明示的な序数位置を指定するのではなく、結果セットの末尾からカウント ダウンによって、ドライバー固有の列へのアクセスを得る必要があります。 詳細については、次を参照してください。[カタログ関数によって返されるデータ](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)します。  
  
|列名|列番号|データ型|コメント|  
|-----------------|-------------------|---------------|--------------|  
|TABLE_CAT (ODBC 1.0)|1|Varchar|カタログの識別子。データ ソースに適用されない場合は NULL です。 ドライバーの空の文字列を返します、ドライバーは、さまざまな Dbms からデータを取得するときなどに、他のユーザーではなく一部のテーブルのカタログをサポートする場合 ("")、それらのテーブルのカタログがないです。|  
|TABLE_SCHEM (ODBC 1.0)|2|Varchar|スキーマ識別子。データ ソースに適用されない場合は NULL です。 ドライバーの空の文字列を返します、ドライバーは、さまざまな Dbms からデータを取得するときなどに、他のユーザーではなく一部のテーブルのスキーマをサポートする場合 ("")、それらのテーブル スキーマがないです。|  
|TABLE_NAME (ODBC 1.0)|3|NULL 以外の Varchar|テーブルの識別子です。|  
|COLUMN_NAME (ODBC 1.0)|4|NULL 以外の Varchar|列名 ドライバーは、名前がない列の空の文字列を返します。|  
|権限の許可者 (ODBC 1.0)|5|Varchar|特権を付与したユーザーの名前データ ソースに適用されない場合は NULL です。<br /><br /> 権限付与対象ユーザーの列の値をオブジェクトの所有者であるすべての行、GRANTOR 列は「(_s)」になります。|  
|権限付与対象ユーザー (ODBC 1.0)|6|NULL 以外の Varchar|ユーザーに権限を与えられたユーザーの名前。|  
|特権 (ODBC 1.0)|7|NULL 以外の Varchar|列の特権を識別します。 次のいずれかを指定することがあります (ソース データでサポートされている他のユーザーまたは実装で定義された)。<br /><br /> 選択します。列のデータを取得する、権限付与対象ユーザーが許可されます。<br /><br /> 挿入します。関連付けられているテーブルに挿入された新しい行に列のデータを提供する、権限付与対象ユーザーが許可されます。<br /><br /> 更新プログラム:列のデータを更新する権限が許可されます。<br /><br /> 参照:制約内で列を参照する、権限付与対象ユーザーが許可されている (たとえば、一意、参照、またはテーブルが check 制約)。|  
|IS_GRANTABLE (ODBC 1.0)|8|Varchar|他のユーザーに、特権を付与する権限が許可されたかどうかを示します"YES"、"NO"、または不明またはデータ ソースに適用されない場合は"NULL"です。<br /><br /> 特権はどちらかです付与できるまたは付与禁止両方は必要ありません。 によって返される結果セット**SQLColumnPrivileges** IS_GRANTABLE 列を除くすべての列が同じ値を含めることが 2 つの行が含まれません。|  
  
## <a name="code-example"></a>コード例  
 同様の関数のコード例では、次を参照してください。 [SQLColumns 関数](../../../odbc/reference/syntax/sqlcolumns-function.md)します。  
  
## <a name="related-functions"></a>関連する関数  
  
|詳細|参照先|  
|---------------------------|---------|  
|バッファーを結果セット内の列にバインドします。|[SQLBindCol 関数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|ステートメントの処理をキャンセル|[SQLCancel 関数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|テーブルまたはテーブルの列を返す|[SQLColumns 関数](../../../odbc/reference/syntax/sqlcolumns-function.md)|  
|データのブロックをフェッチしています。 または、結果をスクロールの設定|[SQLFetchScroll 関数](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|複数行のデータをフェッチしています|[SQLFetch 関数](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|テーブルまたはテーブルに対する権限を返す|[SQLTablePrivileges 関数](../../../odbc/reference/syntax/sqltableprivileges-function.md)|  
|データ ソース内のテーブルの一覧を返す|[SQLTables 関数](../../../odbc/reference/syntax/sqltables-function.md)|  
  
## <a name="see-also"></a>参照  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)
