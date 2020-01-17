---
title: SQLForeignKeys 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLForeignKeys
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLForeignKeys
helpviewer_keywords:
- SQLForeignKeys function [ODBC]
ms.assetid: 07f3f645-f643-4d39-9a10-70a72f24e608
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 58f69b9f3088c063faa39da677f2865abdfc6476
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68003011"
---
# <a name="sqlforeignkeys-function"></a>SQLForeignKeys 関数
**準拠**  
 バージョンが導入されました。ODBC 1.0 規格に準拠します。ODBC  
  
 **まとめ**  
 **SQLForeignKeys**返すことができます。  
  
-   指定されたテーブル (列指定されたテーブル内の他のテーブルの主キーを参照する) の外部キーの一覧。  
  
-   指定したテーブルの主キーを参照するその他のテーブルの外部キーの一覧。  
  
 ドライバーは、結果セットとして指定されたステートメントの各リストを返します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLForeignKeys(  
     SQLHSTMT       StatementHandle,  
     SQLCHAR *      PKCatalogName,  
     SQLSMALLINT    NameLength1,  
     SQLCHAR *      PKSchemaName,  
     SQLSMALLINT    NameLength2,  
     SQLCHAR *      PKTableName,  
     SQLSMALLINT    NameLength3,  
     SQLCHAR *      FKCatalogName,  
     SQLSMALLINT    NameLength4,  
     SQLCHAR *      FKSchemaName,  
     SQLSMALLINT    NameLength5,  
     SQLCHAR *      FKTableName,  
     SQLSMALLINT    NameLength6);  
```  
  
## <a name="arguments"></a>引数  
 *StatementHandle*  
 [入力]ステートメント ハンドルです。  
  
 *PKCatalogName*  
 [入力]主キー テーブルのカタログ名。 ドライバーは、いくつかのテーブルのドライバーをさまざまな Dbms、空の文字列からデータを取得した場合など、他ではなく、カタログをサポートしている場合 ("") のカタログはありません。 それらのテーブルを表します。 *PKCatalogName*文字列の検索パターンを含めることはできません。  
  
 SQL_ATTR_METADATA_ID ステートメント属性は、SQL_TRUE に設定されている場合*PKCatalogName*は識別子として扱われますそのケースは重要ではありません。 場合は sql_false になります、 *PKCatalogName*は通常の引数です。 文字どおり、扱われ、そのケースは重要では。 詳細については、次を参照してください。[カタログ関数の引数](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)します。  
  
 *NameLength1*  
 [入力]長さ **PKCatalogName*、文字数。  
  
 *PKSchemaName*  
 [入力]主キー テーブルのスキーマ名。 ドライバーは、ドライバーをさまざまな Dbms、空の文字列からデータを取得した場合など、他ではなく一部のテーブルのスキーマをサポートしている場合 ("") のスキーマはありません。 それらのテーブルを表します。 *PKSchemaName*文字列の検索パターンを含めることはできません。  
  
 SQL_ATTR_METADATA_ID ステートメント属性は、SQL_TRUE に設定されている場合*PKSchemaName*は識別子として扱われますそのケースは重要ではありません。 場合は sql_false になります、 *PKSchemaName*は通常の引数です。 文字どおり、扱われ、そのケースは重要では。  
  
 *NameLength2*  
 [入力]長さ **PKSchemaName*、文字数。  
  
 *PKTableName*  
 [入力]主キー テーブルの名前。 *PKTableName*文字列の検索パターンを含めることはできません。  
  
 SQL_ATTR_METADATA_ID ステートメント属性は、SQL_TRUE に設定されている場合*PKTableName*は識別子として扱われますそのケースは重要ではありません。 場合は sql_false になります、 *PKTableName*は通常の引数です。 文字どおり、扱われ、そのケースは重要では。  
  
 *NameLength3*  
 [入力]長さ **PKTableName*、文字数。  
  
 *FKCatalogName*  
 [入力]外部キー テーブルのカタログ名。 ドライバーは、いくつかのテーブルのドライバーをさまざまな Dbms、空の文字列からデータを取得した場合など、他ではなく、カタログをサポートしている場合 ("") のカタログはありません。 それらのテーブルを表します。 *FKCatalogName*文字列の検索パターンを含めることはできません。  
  
 SQL_ATTR_METADATA_ID ステートメント属性は、SQL_TRUE に設定されている場合*FKCatalogName*は識別子として扱われますそのケースは重要ではありません。 場合は sql_false になります、 *FKCatalogName*は通常の引数です。 文字どおり、扱われ、そのケースは重要では。  
  
 *NameLength4*  
 [入力]長さ **FKCatalogName*、文字数。  
  
 *FKSchemaName*  
 [入力]外部キー テーブルのスキーマ名。 ドライバーは、ドライバーをさまざまな Dbms、空の文字列からデータを取得した場合など、他ではなく一部のテーブルのスキーマをサポートしている場合 ("") のスキーマはありません。 それらのテーブルを表します。 *FKSchemaName*文字列の検索パターンを含めることはできません。  
  
 SQL_ATTR_METADATA_ID ステートメント属性は、SQL_TRUE に設定されている場合*FKSchemaName*は識別子として扱われますそのケースは重要ではありません。 場合は sql_false になります、 *FKSchemaName*は通常の引数です。 文字どおり、扱われ、そのケースは重要では。  
  
 *NameLength5*  
 [入力]長さ **FKSchemaName*、文字数。  
  
 *FKTableName*  
 [入力]外部キー テーブルの名前。 *FKTableName*文字列の検索パターンを含めることはできません。  
  
 SQL_ATTR_METADATA_ID ステートメント属性は、SQL_TRUE に設定されている場合*FKTableName*は識別子として扱われますそのケースは重要ではありません。 場合は sql_false になります、 *FKTableName*は通常の引数です。 文字どおり、扱われ、そのケースは重要では。  
  
 *NameLength6*  
 [入力]長さ **FKTableName*、文字数。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_STILL_EXECUTING、SQL_ERROR、または SQL_INVALID_HANDLE します。  
  
## <a name="diagnostics"></a>診断  
 ときに**SQLForeignKeys** SQL_ERROR または SQL_SUCCESS_WITH_INFO、関連付けられている SQLSTATE 値を返しますを呼び出すことによって取得できる**SQLGetDiagRec**で、 *HandleType* SQL の_HANDLE_STMT と*処理*の*StatementHandle*します。 次の表に、によって返される通常の SQLSTATE 値**SQLForeignKeys** ; この関数のコンテキストでそれぞれについて説明しますと表記"(DM)"の前にドライバー マネージャーによって返されるについての説明。 SQLSTATE 値ごとに関連付けられているリターン コードは明記しない限り、SQL_ERROR です。  
  
|SQLSTATE|[エラー]|説明|  
|--------------|-----------|-----------------|  
|01000|一般的な警告|ドライバー固有の情報メッセージです。 (関数は、SQL_SUCCESS_WITH_INFO を返します)。|  
|08S01|通信リンク エラー|関数が完了した処理の前に、ドライバーとドライバーが接続されているデータ ソース間の通信リンクに失敗しました。|  
|24000|カーソル状態が無効|カーソルが開いて、 *StatementHandle*、および**SQLFetch**または**SQLFetchScroll**が呼び出されました。 このエラーが返されますドライバー マネージャーによって**SQLFetch**または**SQLFetchScroll** 、SQL_NO_DATA が返されなかったと場合、ドライバーによって返される**SQLFetch**または**SQLFetchScroll** SQL_NO_DATA が返されます。<br /><br /> カーソルが開いて、 *StatementHandle*が**SQLFetch**または**SQLFetchScroll**呼び出されていない必要があります。|  
|40001|シリアル化エラー|トランザクションが別のトランザクションでリソース デッドロックによりロールバックされました。|  
|40003|不明なステートメント入力候補|、この関数の実行中に、関連付けられた接続が失敗し、トランザクションの状態を特定できません。|  
|HY000|一般的なエラー|これがなかった固有の SQLSTATE とする実装に固有の SQLSTATE が定義されていない、エラーが発生しました。 によって返されるエラー メッセージ**SQLGetDiagRec**で、  *\*MessageText*バッファーは、エラーとその原因について説明します。|  
|HY001|メモリの割り当てエラー|ドライバーは、実行または関数の完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY008|操作が取り消されました|非同期処理が有効に、 *StatementHandle*します。 関数が呼び出された、および実行を完了する前に**SQLCancel**または**SQLCancelHandle**が呼び出されて、 *StatementHandle*関数が呼び出された後、もう一度、 *StatementHandle*します。<br /><br /> 関数が呼び出された、および実行を完了する前に**SQLCancel**または**SQLCancelHandle**が呼び出されて、 *StatementHandle*から別のスレッドで、マルチ スレッド アプリケーションです。|  
|HY009|無効な null ポインターの使用|(DM) 引数*PKTableName*と*FKTableName*が両方とも null ポインター。<br /><br /> SQL_ATTR_METADATA_ID のステートメント属性、SQL_TRUE に設定されて、 *FKCatalogName*または*PKCatalogName*引数が null ポインターの場合は、および、SQL_CATALOG_NAME*情報の種類*カタログ名を返しますがサポートされています。<br /><br /> (DM) SQL_ATTR_METADATA_ID ステートメント属性の SQL_TRUE に設定された、 *FKSchemaName*、 *PKSchemaName*、 *FKTableName*、または*PKTableName*引数が null ポインター。|  
|HY010|関数のシーケンス エラー|(DM) を非同期的に実行中の関数が呼び出された接続ハンドルに関連付けられているため、 *StatementHandle*します。 SQLForeignKeys 関数が呼び出されたときにも、この非同期関数が実行されました。<br /><br /> (DM) **SQLExecute**、 **SQLExecDirect**、または**SQLMoreResults**に対して呼び出された、 *StatementHandle* SQL_PARAM_DATA_ を返されます。ご利用いただけます。 ストリームのすべてのパラメーターのデータが取得される前に、この関数が呼び出されました。<br /><br /> (DM) を非同期的に実行中の関数 (いないこの"1") が呼び出された、 *StatementHandle*この関数が呼び出されたときに実行されているとします。<br /><br /> (DM) **SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**、または**SQLSetPos**に対して呼び出された、 *StatementHandle* SQL_NEED_DATA が返されます。 すべての実行時データ パラメーターまたは列のデータが送信される前に、この関数が呼び出されました。|  
|HY013|メモリ管理エラー|基になるメモリ オブジェクトにアクセスできませんでした、場合によってメモリ不足が原因であるために、関数呼び出しを処理できませんでした。|  
|HY090|文字列またはバッファーの長さが無効です。|(DM) 名の長の引数のいずれかの値が 0 未満でしたが、SQL_NTS と等しくありません。|  
|||名の長の引数のいずれかの値には、対応する名前の最大長の値を超えています。 (「コメントです」を参照してください)|  
|HY117|不明なトランザクションの状態のため、接続が中断されます。 のみを切断して、読み取り専用の関数が許可されます。|(DM) 中断状態の詳細については、次を参照してください。 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)します。|  
|HYC00|省略可能な機能が実装されていません|カタログ名が指定されました、およびドライバーまたはデータ ソースがカタログをサポートしていません。<br /><br /> スキーマ名を指定してから、およびドライバーまたはデータ ソースがスキーマをサポートしていません。|  
|||SQL_ATTR_CURSOR_TYPE、SQL_ATTR_CONCURRENCY ステートメント属性の現在の設定の組み合わせが、ドライバーまたはデータ ソースでサポートされていません。<br /><br /> SQL_ATTR_USE_BOOKMARKS ステートメント属性は SQL_UB_VARIABLE に設定されており、SQL_ATTR_CURSOR_TYPE ステートメント属性は、ドライバーがブックマークをできません、カーソルの種類に設定されました。|  
|HYT00|タイムアウトが発生しました|データ ソースには、結果セットが返される前に、クエリのタイムアウト期間が終了しました。 によって、タイムアウト期間が設定されます**SQLSetStmtAttr**、SQL_ATTR_QUERY_TIMEOUT します。|  
|HYT01|接続がタイムアウトしました|データ ソースが要求に応答する前に、接続のタイムアウト期間が終了しました。 によって、接続タイムアウト期間が設定されます**SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT します。|  
|IM001|ドライバーでは、この関数はサポートされていません|(DM) に、ドライバーが関連付けられている、 *StatementHandle*関数をサポートしていません。|  
|IM017|非同期通知モードでのポーリングは無効です。|通知のモデルを使用すると、常にポーリングは無効です。|  
|IM018|**SQLCompleteAsync**このハンドルに対する前の非同期操作を完了が呼び出されていません。|通知モードが有効になっている場合、ハンドルでは、前の関数呼び出しに SQL_STILL_EXECUTING が返された場合と**SQLCompleteAsync**後処理を行い、操作を完了するハンドルで呼び出す必要があります。|  
  
## <a name="comments"></a>コメント  
 この関数によって返される情報の使用方法については、次を参照してください。[カタログ データの使用](../../../odbc/reference/develop-app/uses-of-catalog-data.md)します。  
  
 場合\* *PKTableName* 、テーブル名を含む**SQLForeignKeys**指定したテーブルの主キーとそれを参照するすべての外部キーを含む結果セットを返します。 その他のテーブルの外部キーの一覧では、指定したテーブルの unique 制約をポイントする外部キーは含まれません。  
  
 場合\* *FKTableName* 、テーブル名を含む**SQLForeignKeys**を他のテーブルの主キーを指す指定のテーブル内のすべての外部キーを含む結果セットを返しますと参照されている他のテーブルの主キー。 指定したテーブルの外部キーの一覧では、他のテーブルで unique 制約を参照する外部キーは含まれません。  
  
 両方\* *PKTableName*と\* *FKTableName* 、テーブル名を含む**SQLForeignKeys**指定されたテーブルの外部キーを返します\* *FKTableName*で指定したテーブルの主キーを参照する **PKTableName*します。 1 つのキーは、最大でこのする必要があります。  
  
> [!NOTE]  
>  一般的な使用、引数、および ODBC カタログ関数の返されたデータの詳細については、次を参照してください。[カタログ関数](../../../odbc/reference/develop-app/catalog-functions.md)します。  
  
 **SQLForeignKeys**結果の標準的な結果セットとして返します。 主キーに関連付けられている外部キーが要求される場合、結果セットは FKTABLE_CAT や FKTABLE_SCHEM、FKTABLE_NAME、KEY_SEQ で並べ替えられます。 外部キーに関連付けられている主キーが要求される場合、結果セットは PKTABLE_CAT、PKTABLE_SCHEM、PKTABLE_NAME、および KEY_SEQ で並べ替えられます。 次の表には、結果セット内の列が一覧表示します。  
  
 VARCHAR 列の長さは、テーブルには表示されません。実際の長さは、データ ソースに依存します。 PKTABLE_CAT または FKTABLE_CAT、PKTABLE_SCHEM または FKTABLE_SCHEM の実際の長さを確認するのに PKTABLE_NAME または FKTABLE_NAME、および PKCOLUMN_NAME FKCOLUMN_NAME 列では、アプリケーションを呼び出すことができます**SQLGetInfo** SQL_MAX_ でCATALOG_NAME_LEN、SQL_MAX_SCHEMA_NAME_LEN、SQL_MAX_TABLE_NAME_LEN、および SQL_MAX_COLUMN_NAME_LEN オプション。  
  
 次の列が ODBC 3 の名前が変更された *。 x。* 列名の変更では、アプリケーションは、列番号でバインドため、旧バージョンとの互換性は影響しません。  
  
|ODBC 2.0 列|ODBC 3 *.x*列|  
|---------------------|-----------------------|  
|PKTABLE_QUALIFIER|PKTABLE_CAT|  
|PKTABLE_OWNER|PKTABLE_SCHEM|  
|FKTABLE_QUALIFIER|FK_TABLE_CAT|  
|FKTABLE_OWNER|FKTABLE_SCHEM|  
  
 次の表には、結果セット内の列が一覧表示します。 ドライバーでは、列 (注釈) の 14 を超える追加の列を定義できます。 アプリケーションでは、結果の明示的な位置を表す序数を指定する代わりにセットの末尾からカウント ダウンして、ドライバー固有の列へのアクセスを得る必要があります。 詳細については、次を参照してください。[カタログ関数によって返されるデータ](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)します。  
  
|列名|列番号|データ型|コメント|  
|-----------------|-------------------|---------------|--------------|  
|PKTABLE_CAT (ODBC 1.0)|1|Varchar|主キー テーブルのカタログ名。データ ソースに適用されない場合は NULL です。 ドライバーの空の文字列を返します、ドライバーは、さまざまな Dbms からデータを取得するときなどに、他のユーザーではなく一部のテーブルのカタログをサポートする場合 ("")、それらのテーブルのカタログがないです。|  
|PKTABLE_SCHEM (ODBC 1.0)|2|Varchar|主キー テーブルのスキーマ名。データ ソースに適用されない場合は NULL です。 ドライバーの空の文字列を返します、ドライバーは、さまざまな Dbms からデータを取得するときなどに、他のユーザーではなく一部のテーブルのスキーマをサポートする場合 ("")、それらのテーブル スキーマがないです。|  
|PKTABLE_NAME (ODBC 1.0)|3|NULL 以外の Varchar|主キー テーブルの名前。|  
|PKCOLUMN_NAME (ODBC 1.0)|4|NULL 以外の Varchar|主キー列の名前。 ドライバーは、名前がない列の空の文字列を返します。|  
|FKTABLE_CAT (ODBC 1.0)|5|Varchar|外部キー テーブルのカタログ名。データ ソースに適用されない場合は NULL です。 ドライバーの空の文字列を返します、ドライバーは、さまざまな Dbms からデータを取得するときなどに、他のユーザーではなく一部のテーブルのカタログをサポートする場合 ("")、それらのテーブルのカタログがないです。|  
|FKTABLE_SCHEM (ODBC 1.0)|6|Varchar|外部キー テーブルのスキーマ名。データ ソースに適用されない場合は NULL です。 ドライバーの空の文字列を返します、ドライバーは、さまざまな Dbms からデータを取得するときなどに、他のユーザーではなく一部のテーブルのスキーマをサポートする場合 ("")、それらのテーブル スキーマがないです。|  
|FKTABLE_NAME (ODBC 1.0)|7|NULL 以外の Varchar|外部キー テーブルの名前。|  
|FKCOLUMN_NAME (ODBC 1.0)|8|NULL 以外の Varchar|外部キー列の名前。 ドライバーは、名前がない列の空の文字列を返します。|  
|KEY_SEQ (ODBC 1.0)|9|Smallint (NULL 以外)|(1 から始まる) キーの列のシーケンス番号。|  
|UPDATE_RULE (ODBC 1.0)|10|Smallint|SQL の操作時に、外部キーに適用されるアクション**UPDATE**します。 次の値のいずれかのことができます。 (参照先のテーブルが主キーを持つテーブルは、参照元のテーブルが外部キーを持つテーブル)。<br /><br /> SQL_CASCADE:参照先のテーブルの主キーが更新されたときに、参照元テーブルの外部キーも更新されます。<br /><br /> SQL_NO_ACTION:参照先のテーブルの主キーの更新により、参照元テーブル「未解決の参照」が生じる可能性があるかどうか (つまり、参照元のテーブル内の行がないの対応する参照先のテーブルで)、更新が拒否されました。 参照元のテーブルの外部キーの更新プログラムは、参照先のテーブルの主キーの値として存在しない値を発生させることは、更新プログラムが拒否されます。 (このアクションは、ODBC 2 SQL_RESTRICT アクションと同じ *.x*)。<br /><br /> SQL_SET_NULL:すべての外部キー参照テーブルの主キーの変更されたコンポーネントに対応するコンポーネントを NULL に設定されます、主キーの 1 つまたは複数のコンポーネントが変更されているように参照先のテーブル内 1 つまたは複数の行が更新されると、参照元のテーブルの一致する行。<br /><br /> SQL_SET_DEFAULT:主キーの変更されたコンポーネントに対応する外部キー参照テーブルのコンポーネントは、applicab に設定方法の主キーの 1 つまたは複数のコンポーネントが変更されたことで、参照されるテーブルの 1 つまたは複数の行が更新されると、参照元のテーブルのすべての一致する行の le 既定値。<br /><br /> データ ソースに適用されない場合は NULL です。|  
|DELETE_RULE (ODBC 1.0)|11|Smallint|SQL の操作時に、外部キーに適用されるアクション**削除**します。 次の値のいずれかのことができます。 (参照先のテーブルが主キーを持つテーブルは、参照元のテーブルが外部キーを持つテーブル)。<br /><br /> SQL_CASCADE:参照先のテーブルの行が削除されると、参照元のテーブルで一致するすべての行も削除されます。<br /><br /> SQL_NO_ACTION:参照先のテーブル内の行の削除により、参照元テーブル「未解決の参照」が生じる可能性があるかどうか (つまり、参照元のテーブル内の行がないの対応する参照先のテーブルで)、更新が拒否されました。 (このアクションは、ODBC 2 SQL_RESTRICT アクションと同じ *.x*)。<br /><br /> SQL_SET_NULL:参照先のテーブル内 1 つまたは複数の行が削除されると、参照元のテーブルの外部キーの各コンポーネントは、参照元のテーブルのすべての一致する行に NULL に設定されます。<br /><br /> SQL_SET_DEFAULT:参照先のテーブル内 1 つまたは複数の行が削除されると、参照元のテーブルの外部キーの各コンポーネントは、参照元のテーブルのすべての一致する行の該当する既定値に設定されます。<br /><br /> データ ソースに適用されない場合は NULL です。|  
|FK_NAME (ODBC 2.0)|12|Varchar|外部キーの名前。 データ ソースに適用されない場合は NULL です。|  
|PK_NAME (ODBC 2.0)|13|Varchar|プライマリ キーの名前。 データ ソースに適用されない場合は NULL です。|  
|遅延 (ODBC 3.0)|14|Smallint|度を SQL_NOT_DEFERRABLE します。|  
  
## <a name="code-example"></a>コード例  
 次の表のように、この例は、注文、線、および顧客をという名前の 3 つのテーブルを使用します。  
  
|ORDERS|行|顧客|  
|------------|-----------|---------------|  
|ORDERID|ORDERID|CUSTID|  
|CUSTID|行|NAME|  
|OPENDATE|PARTID|アドレス|  
|営業担当者|数量|電話|  
|STATUS|||  
  
 ORDERS テーブルでは、CUSTID は、販売の行われた先顧客を識別します。 CUSTOMERS テーブルで CUSTID を参照する外部キーになります。  
  
 行の表では、ORDERID は、行項目が関連付けられている販売注文を識別します。 ORDERS テーブルの ORDERID を参照する外部キーになります。  
  
 この例では**SQLPrimaryKeys**を ORDERS テーブルの主キーを取得します。 結果セットは 1 つの行になります重要な列は、次の表に表示されます。  
  
|TABLE_NAME|COLUMN_NAME|KEY_SEQ|  
|-----------------|------------------|--------------|  
|ORDERS|ORDERID|1|  
  
 例では次に、 **SQLForeignKeys**を ORDERS テーブルの主キーを参照する他のテーブルの外部キーを取得します。 結果セットは 1 つの行になります重要な列は、次の表に表示されます。  
  
|PKTABLE_NAME|PKCOLUMN_NAME|FKTABLE_NAME|FKCOLUMN_NAME|KEY_SEQ|  
|-------------------|--------------------|-------------------|--------------------|--------------|  
|ORDERS|CUSTID|行|CUSTID|1|  
  
 例では最後に、 **SQLForeignKeys**を他のテーブルの主キーを参照する ORDERS テーブルの外部キーを取得します。 結果セットは 1 つの行になります重要な列は、次の表に表示されます。  
  
|PKTABLE_NAME|PKCOLUMN_NAME|FKTABLE_NAME|FKCOLUMN_NAME|KEY_SEQ|  
|-------------------|--------------------|-------------------|--------------------|--------------|  
|顧客|CUSTID|ORDERS|CUSTID|1|  
  
```cpp  
#define TAB_LEN SQL_MAX_TABLE_NAME_LEN + 1  
#define COL_LEN SQL_MAX_COLUMN_NAME_LEN + 1  
  
LPSTR   szTable;              /* Table to display */  
  
UCHAR szPkTable[TAB_LEN];   /* Primary key table name */  
UCHAR szFkTable[TAB_LEN];   /* Foreign key table name */  
UCHAR szPkCol[COL_LEN];     /* Primary key column */  
UCHAR szFkCol[COL_LEN];     /* Foreign key column */  
  
SQLHSTMT      hstmt;  
SQLINTEGER    cbPkTable, cbPkCol, cbFkTable, cbFkCol, cbKeySeq;  
SQLSMALLINT   iKeySeq;  
SQLRETURN     retcode;  
  
// Bind the columns that describe the primary and foreign keys.  
// Ignore the table schema, name, and catalog for this example.  
  
SQLBindCol(hstmt, 3, SQL_C_CHAR, szPkTable, TAB_LEN, &cbPkTable);  
SQLBindCol(hstmt, 4, SQL_C_CHAR, szPkCol, COL_LEN, &cbPkCol);  
SQLBindCol(hstmt, 5, SQL_C_SSHORT, &iKeySeq, TAB_LEN, &cbKeySeq);  
SQLBindCol(hstmt, 7, SQL_C_CHAR, szFkTable, TAB_LEN, &cbFkTable);  
SQLBindCol(hstmt, 8, SQL_C_CHAR, szFkCol, COL_LEN, &cbFkCol);  
  
strcpy_s(szTable, sizeof(szTable), "ORDERS");  
  
/* Get the names of the columns in the primary key. */  
  
retcode = SQLPrimaryKeys(hstmt,  
         NULL, 0,             /* Catalog name */  
         NULL, 0,             /* Schema name */  
         szTable, SQL_NTS);   /* Table name */  
  
while ((retcode == SQL_SUCCESS) || (retcode == SQL SUCCESS_WITH_INFO)) {  
  
   /* Fetch and display the result set. This will be a list of the */  
   /* columns in the primary key of the ORDERS table. */  
  
   retcode = SQLFetch(hstmt);  
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO)  
      fprintf(out, "Table: %s Column: %s Key Seq: %hd \n", szPkTable, szPkCol,  
      iKeySeq);  
}  
  
/* Close the cursor (the hstmt is still allocated). */  
  
SQLFreeStmt(hstmt, SQL_CLOSE);  
  
/* Get all the foreign keys that refer to ORDERS primary key.*/   
  
retcode = SQLForeignKeys(hstmt,  
         NULL, 0,            /* Primary catalog */  
         NULL, 0,            /* Primary schema */  
         szTable, SQL_NTS,   /* Primary table */  
         NULL, 0,            /* Foreign catalog */  
         NULL, 0,            /* Foreign schema */  
         NULL, 0);           /* Foreign table */  
  
while ((retcode == SQL_SUCCESS) || (retcode == SQL_SUCCESS_WITH_INFO)) {  
  
/* Fetch and display the result set. This will be all of the */  
/* foreign keys in other tables that refer to the ORDERS */  
/* primary key. */  
  
   retcode = SQLFetch(hstmt);  
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO)  
      fprintf(out, "%-s ( %-s ) <-- %-s ( %-s )\n", szPkTable,  
               szPkCol, szFkTable, szFkCol);  
}  
  
/* Close the cursor (the hstmt is still allocated). */  
  
SQLFreeStmt(hstmt, SQL_CLOSE);  
  
/* Get all the foreign keys in the ORDERS table. */  
  
retcode = SQLForeignKeys(hstmt,  
         NULL, 0,             /* Primary catalog */  
         NULL, 0,             /* Primary schema */  
         NULL, 0,             /* Primary table */  
         NULL, 0,             /* Foreign catalog */  
         NULL, 0,             /* Foreign schema */  
         szTable, SQL_NTS);   /* Foreign table */  
  
while ((retcode == SQL_SUCCESS) || (retcode == SQL_SUCCESS_WITH_INFO)) {  
  
/* Fetch and display the result set. This will be all of the */  
/* primary keys in other tables that are referred to by foreign */  
/* keys in the ORDERS table. */  
  
   retcode = SQLFetch(hstmt);  
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO)  
      fprintf(out, "%-s ( %-s )--> %-s ( %-s )\n", szFkTable, szFkCol, szPkTable, szPkCol);  
}  
  
/* Free the hstmt. */  
SQLFreeStmt(hstmt, SQL_DROP);  
```  
  
## <a name="related-functions"></a>関連する関数  
  
|詳細|参照先|  
|---------------------------|---------|  
|バッファーを結果セット内の列にバインドします。|[SQLBindCol 関数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|ステートメントの処理をキャンセル|[SQLCancel 関数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|1 つの行または順方向専用の方向にデータのブロックをフェッチしています|[SQLFetch 関数](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|データのブロックをフェッチしています。 または、結果をスクロールの設定|[SQLFetchScroll 関数](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|主キーの列を返す|[SQLPrimaryKeys 関数](../../../odbc/reference/syntax/sqlprimarykeys-function.md)|  
|テーブルの統計情報とインデックスを返す|[SQLStatistics 関数](../../../odbc/reference/syntax/sqlstatistics-function.md)|  
  
## <a name="see-also"></a>参照  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)
