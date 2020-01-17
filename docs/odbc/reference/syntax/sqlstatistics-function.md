---
title: SQLStatistics 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLStatistics
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLStatistics
helpviewer_keywords:
- SQLStatistics function [ODBC]
ms.assetid: 45210682-cfea-4e5d-9951-bcf1cbe10f41
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ef0f25660a0faa0747752a8ca15c207c1e939669
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68039548"
---
# <a name="sqlstatistics-function"></a>SQLStatistics 関数
**準拠**  
 バージョンが導入されました。ODBC 1.0 規格に準拠します。ISO 92  
  
 **まとめ**  
 **SQLStatistics** 1 つのテーブルとテーブルに関連付けられているインデックスに関する統計情報の一覧を取得します。 ドライバーは、その結果、情報を設定を返します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLStatistics(  
     SQLHSTMT        StatementHandle,  
     SQLCHAR *       CatalogName,  
     SQLSMALLINT     NameLength1,  
     SQLCHAR *       SchemaName,  
     SQLSMALLINT     NameLength2,  
     SQLCHAR *       TableName,  
     SQLSMALLINT     NameLength3,  
     SQLUSMALLINT    Unique,  
     SQLUSMALLINT    Reserved);  
```  
  
## <a name="arguments"></a>引数  
 *StatementHandle*  
 [入力]ステートメント ハンドルです。  
  
 *カタログ名*  
 [入力]カタログの名前。 ドライバーは、いくつかのテーブルのドライバーをさまざまな Dbms、空の文字列からデータを取得した場合など、他ではなく、カタログをサポートしている場合 ("") それらのテーブルのカタログがないことを示します。 *CatalogName*文字列の検索パターンを含めることはできません。  
  
 SQL_ATTR_METADATA_ID ステートメント属性は、SQL_TRUE に設定されている場合*CatalogName*は識別子として扱われますそのケースは重要ではありません。 場合は sql_false になります、 *CatalogName*は通常の引数です。 文字どおり、扱われ、そのケースは重要では。 詳細については、次を参照してください。[カタログ関数の引数](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)します。  
  
 *NameLength1*  
 [入力]文字の長さ **CatalogName*します。  
  
 *スキーマ名*  
 [入力]スキーマ名です。 ドライバーは、ドライバーをさまざまな Dbms、空の文字列からデータを取得した場合など、他ではなく一部のテーブルのスキーマをサポートしている場合 ("") それらのテーブル スキーマがないことを示します。 *SchemaName*文字列の検索パターンを含めることはできません。  
  
 SQL_ATTR_METADATA_ID ステートメント属性は、SQL_TRUE に設定されている場合*SchemaName*は識別子として扱われますそのケースは重要ではありません。 場合は sql_false になります、 *SchemaName*は通常の引数です。 文字どおり、扱われ、そのケースは重要では。  
  
 *NameLength2*  
 [入力]文字の長さ **SchemaName*します。  
  
 *TableName*  
 [入力]テーブル名です。 この引数は、null ポインターにすることはできません。 *SchemaName*文字列の検索パターンを含めることはできません。  
  
 SQL_ATTR_METADATA_ID ステートメント属性は、SQL_TRUE に設定されている場合*TableName*は識別子として扱われますそのケースは重要ではありません。 場合は sql_false になります、 *TableName*は通常の引数です。 文字どおり、扱われ、そのケースは重要では。  
  
 *NameLength3*  
 [入力]文字の長さ **TableName*します。  
  
 *[一意]*  
 [入力]インデックスの種類:SQL_INDEX_UNIQUE または SQL_INDEX_ALL します。  
  
 *Reserved*  
 [入力]結果セットのカーディナリティおよびページの列の重要度を示します。 次のオプションに影響を与える、戻り値のカーディナリティおよびページの列だけです。カーディナリティおよびページが返されない場合でも、インデックスの情報が返されます。  
  
 SQL_ENSURE では、ドライバーが統計を無条件に取得することを要求します。 (ドライバーのみ、Open Group 標準に準拠しているし、ODBC 拡張機能をサポートしていないをできなく SQL_ENSURE をサポートするためにします。)  
  
 SQL_QUICK 要求をサーバーからすぐに使用できる場合に、ドライバーでカーディナリティおよびページを取得します。 この場合、ドライバーで取得される値が最新であるかどうかは保証されません。 (ODBC から SQL_QUICK 動作を常に取得は、Open Group 標準に記述されているアプリケーション*3.x*-準拠のドライバーです)。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_STILL_EXECUTING、SQL_ERROR、または SQL_INVALID_HANDLE します。  
  
## <a name="diagnostics"></a>診断  
 ときに**SQLStatistics** SQL_ERROR または SQL_SUCCESS_WITH_INFO、関連付けられている SQLSTATE 値を返しますを呼び出すことによって取得できる**SQLGetDiagRec**で、 *HandleType* sql _ のHANDLE_STMT と*処理*の*StatementHandle*します。 次の表に、によって返される通常の SQLSTATE 値**SQLStatistics** ; この関数のコンテキストでそれぞれについて説明しますと表記"(DM)"の前にドライバー マネージャーによって返されるについての説明。 SQLSTATE 値ごとに関連付けられているリターン コードは明記しない限り、SQL_ERROR です。  
  
|SQLSTATE|[エラー]|説明|  
|--------------|-----------|-----------------|  
|01000|一般的な警告|ドライバー固有の情報メッセージです。 (関数は、SQL_SUCCESS_WITH_INFO を返します)。|  
|08S01|通信リンク エラー|関数が完了した処理の前に、ドライバーとドライバーが接続されているデータ ソース間の通信リンクに失敗しました。|  
|24000|カーソル状態が無効|カーソルが開いて、 *StatementHandle*、および**SQLFetch**または**SQLFetchScroll**が呼び出されました。 このエラーが返されますドライバー マネージャーによって**SQLFetch**または**SQLFetchScroll** SQL_NO_DATA が返されなかったと場合、ドライバーによって返される**SQLFetch**または**SQLFetchScroll** SQL_NO_DATA が返されます。<br /><br /> カーソルが開いて、 *StatementHandle*が**SQLFetch**または**SQLFetchScroll**呼び出されていない必要があります。|  
|40001|シリアル化エラー|トランザクションが別のトランザクションでリソース デッドロックによりロールバックされました。|  
|40003|不明なステートメント入力候補|、この関数の実行中に、関連付けられた接続が失敗し、トランザクションの状態を特定できません。|  
|HY000|一般的なエラー|これがなかった固有の SQLSTATE とする実装に固有の SQLSTATE が定義されていない、エラーが発生しました。 によって返されるエラー メッセージ**SQLGetDiagRec**で、  *\*MessageText*バッファーは、エラーとその原因について説明します。|  
|HY001|メモリの割り当てエラー|ドライバーは、実行または関数の完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY008|操作が取り消されました|非同期処理が有効に、 *StatementHandle*します。 関数が呼び出された、および実行を完了する前に**SQLCancel**または**SQLCancelHandle**が呼び出されて、 *StatementHandle*関数が呼び出された後、もう一度、 *StatementHandle*します。<br /><br /> 関数が呼び出された、および実行を完了する前に**SQLCancel**または**SQLCancelHandle**が呼び出されて、 *StatementHandle*から別のスレッドで、マルチ スレッド アプリケーションです。|  
|HY009|無効な null ポインターの使用|*TableName*引数が null ポインター。<br /><br /> SQL_ATTR_METADATA_ID のステートメント属性、SQL_TRUE に設定されて、 *CatalogName*引数が null ポインターの場合は、および、SQL_CATALOG_NAME*情報の種類*カタログ名を返しますがサポートされています。<br /><br /> (DM) SQL_ATTR_METADATA_ID ステートメント属性の SQL_TRUE に設定された、 *SchemaName*引数が null ポインター。|  
|HY010|関数のシーケンス エラー|(DM) を非同期的に実行中の関数が呼び出された接続ハンドルに関連付けられているため、 *StatementHandle*します。 この非同期関数ではときに実行されている、 **SQLStatistics**関数が呼び出されました。<br /><br /> (DM) **SQLExecute**、 **SQLExecDirect**、または**SQLMoreResults**に対して呼び出された、 *StatementHandle* SQL_PARAM_DATA_ を返されます。ご利用いただけます。 ストリームのすべてのパラメーターのデータが取得される前に、この関数が呼び出されました。<br /><br /> (DM) を非同期的に実行中の関数 (いないこの"1") が呼び出された、 *StatementHandle*この関数が呼び出されたときに実行されているとします。<br /><br /> (DM) **SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**、または**SQLSetPos**に対して呼び出された、 *StatementHandle* SQL_NEED_DATA が返されます。 すべての実行時データ パラメーターまたは列のデータが送信される前に、この関数が呼び出されました。|  
|HY013|メモリ管理エラー|基になるメモリ オブジェクトにアクセスできませんでした、場合によってメモリ不足が原因であるために、関数呼び出しを処理できませんでした。|  
|HY090|文字列またはバッファーの長さが無効です。|(DM) 名の長の引数のいずれかの値が 0 未満でしたが、SQL_NTS と等しくありません。<br /><br /> 名の長の引数のいずれかの値には、対応する名前の最大長の値を超えています。|  
|HY100|範囲外の一意性オプションの種類|(DM)、無効な*Unique*値が指定されました。|  
|HY101|範囲外の正確性オプションの種類|(DM)、無効な*占有*値が指定されました。|  
|HY117|不明なトランザクションの状態のため、接続が中断されます。 のみを切断して、読み取り専用の関数が許可されます。|(DM) 中断状態の詳細については、次を参照してください。 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)します。|  
|HYC00|省略可能な機能が実装されていません|カタログが指定されていると、ドライバーまたはデータ ソースがカタログをサポートしていません。<br /><br /> スキーマが指定されていると、ドライバーまたはデータ ソース スキーマはサポートしません。<br /><br /> SQL_ATTR_CURSOR_TYPE、SQL_ATTR_CONCURRENCY ステートメント属性の現在の設定の組み合わせが、ドライバーまたはデータ ソースでサポートされていません。<br /><br /> SQL_ATTR_USE_BOOKMARKS ステートメント属性は SQL_UB_VARIABLE に設定されており、SQL_ATTR_CURSOR_TYPE ステートメント属性は、ドライバーがブックマークをできません、カーソルの種類に設定されました。|  
|HYT00|タイムアウトが発生しました|クエリのタイムアウト期間は、要求された結果セットが返されるデータ ソースの前に有効期限が切れました。 によって、タイムアウト期間が設定されます**SQLSetStmtAttr**、SQL_ATTR_QUERY_TIMEOUT します。|  
|HYT01|接続がタイムアウトしました|データ ソースが要求に応答する前に、接続のタイムアウト期間が終了しました。 によって、接続タイムアウト期間が設定されます**SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT します。|  
|IM001|ドライバーでは、この関数はサポートされていません|(DM) に、ドライバーが関連付けられている、 *StatementHandle*関数をサポートしていません。|  
|IM017|非同期通知モードでのポーリングは無効です。|通知のモデルを使用すると、常にポーリングは無効です。|  
|IM018|**SQLCompleteAsync**このハンドルに対する前の非同期操作を完了が呼び出されていません。|通知モードが有効になっている場合、ハンドルでは、前の関数呼び出しに SQL_STILL_EXECUTING が返された場合と**SQLCompleteAsync**後処理を行い、操作を完了するハンドルで呼び出す必要があります。|  
  
## <a name="comments"></a>コメント  
 **SQLStatistics** NON_UNIQUE、型、INDEX_QUALIFIER、INDEX_NAME、および ORDINAL_POSITION 順に並べ、標準的な結果セットとして 1 つのテーブルに関する情報を返します。 結果セットは、統計情報 (結果セットのカーディナリティおよびページの列) 内のテーブルの各インデックスについての情報を結合します。 この情報の用途については、次を参照してください。[カタログ データの使用](../../../odbc/reference/develop-app/uses-of-catalog-data.md)します。  
  
 アプリケーションが呼び出すことができますを TABLE_CAT、TABLE_SCHEM、TABLE_NAME、COLUMN_NAME、列の実際の長さを判断する**SQLGetInfo** SQL_MAX_CATALOG_NAME_LEN、SQL_MAX_SCHEMA_NAME_LEN、SQL_MAX_TABLE_NAME_LEN、および SQL_MAX_COLUMN_NAME_LEN オプション。  
  
> [!NOTE]  
>  一般的な使用、引数、および ODBC カタログ関数の返されたデータの詳細については、次を参照してください。[カタログ関数](../../../odbc/reference/develop-app/catalog-functions.md)します。  
  
 次の列が ODBC の名前が変更された*3.x*します。 列名の変更では、アプリケーションは、列番号でバインドため、旧バージョンとの互換性は影響しません。  
  
|ODBC 2.0 列|ODBC *3.x*列|  
|---------------------|-----------------------|  
|TABLE_QUALIFIER|TABLE_CAT|  
|TABLE_OWNER|TABLE_SCHEM|  
|SEQ_IN_INDEX|ORDINAL_POSITION|  
|COLLATION|ASC_OR_DESC|  
  
 次の表には、結果セット内の列が一覧表示します。 ドライバーでは、列 (FILTER_CONDITION) 13 を超える追加の列を定義できます。 アプリケーションでは、結果の明示的な位置を表す序数を指定する代わりにセットの末尾からカウント ダウンして、ドライバー固有の列へのアクセスを得る必要があります。 詳細については、次を参照してください。[カタログ関数によって返されるデータ](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)します。  
  
|列名|列番号|データ型|コメント|  
|-----------------|-------------------|---------------|--------------|  
|TABLE_CAT (ODBC 1.0)|1|Varchar|統計またはインデックスを適用する; テーブルのカタログ名データ ソースに適用されない場合は NULL です。 ドライバーの空の文字列を返します、ドライバーは、さまざまな Dbms からデータを取得するときなどに、他のユーザーではなく一部のテーブルのカタログをサポートする場合 ("")、それらのテーブルのカタログがないです。|  
|TABLE_SCHEM (ODBC 1.0)|2|Varchar|統計またはインデックスを適用する; テーブルのスキーマ名データ ソースに適用されない場合は NULL です。 ドライバーの空の文字列を返します、ドライバーは、さまざまな Dbms からデータを取得するときなどに、他のユーザーではなく一部のテーブルのスキーマをサポートする場合 ("")、それらのテーブル スキーマがないです。|  
|TABLE_NAME (ODBC 1.0)|3|NULL 以外の Varchar|統計またはインデックスを適用するテーブルのテーブル名です。|  
|NON_UNIQUE (ODBC 1.0)|4|Smallint|インデックスが重複する値を許容しないかどうかを示します。<br /><br /> インデックス値は、一意でない場合は SQL_TRUE にします。<br /><br /> インデックス値は一意である必要がある場合 sql_false になります。<br /><br /> 型が SQL_TABLE_STAT の場合は、NULL が返されます。|  
|INDEX_QUALIFIER (ODBC 1.0)|5|Varchar|インデックスを修飾するために使用される識別子という名前を行う、 **DROP INDEX**;データ ソースでは、インデックスの修飾子はサポートされていない場合、または型が SQL_TABLE_STAT の場合は、NULL が返されます。 この列の null 以外の値が返された場合に、インデックス名を修飾するために使用する必要があります、 **DROP INDEX**ステートメント; インデックス名を修飾するために、TABLE_SCHEM を使用する必要がありますそれ以外の場合、します。|  
|INDEX_NAME (ODBC 1.0)|6|Varchar|インデックス名。型が SQL_TABLE_STAT の場合は、NULL が返されます。|  
|型 (ODBC 1.0)|7|Smallint (NULL 以外)|返される情報の種類です。<br /><br /> SQL_TABLE_STAT では、(カーディナリティやページの列) 内のテーブルの統計情報を示します。<br /><br /> SQL_INDEX_BTREE は B ツリー インデックスを示します。<br /><br /> SQL_INDEX_CLUSTERED では、クラスター化インデックスを示します。<br /><br /> SQL_INDEX_CONTENT では、コンテンツ インデックスを示します。<br /><br /> SQL_INDEX_HASHED では、ハッシュ インデックスを示します。<br /><br /> SQL_INDEX_OTHER では、インデックスの別の種類を示します。|  
|ORDINAL_POSITION (ODBC 1.0)|8|Smallint|(1 から開始)。 インデックス内の列のシーケンス番号型が SQL_TABLE_STAT の場合は、NULL が返されます。|  
|COLUMN_NAME (ODBC 1.0)|9|Varchar|列名 列が式に基づいている場合など、給与 + 特典では、式が返されます。式を決定できない場合は、空の文字列が返されます。 型が SQL_TABLE_STAT の場合は、NULL が返されます。|  
|ASC_OR_DESC (ODBC 1.0)|10|Char (1)|列の並べ替え順序:昇順; の"a"降順以外の場合に、"D"列の並べ替え順序は、データ ソースでサポートされていない場合、または型が SQL_TABLE_STAT の場合は、NULL が返されます。|  
|カーディナリティ (ODBC 1.0)|11|Integer|テーブルまたはインデックスのカーディナリティ型が SQL_TABLE_STAT 以外の場合、テーブル内の行の数型は SQL_TABLE_STAT; がない場合、インデックスの一意の値の数データ ソースから値が使用できない場合は、NULL が返されます。|  
|ページ (ODBC 1.0)|12|Integer|インデックスまたはテーブルを格納するために使用するページ数型が SQL_TABLE_STAT 以外の場合、テーブルのページ数型は SQL_TABLE_STAT; がない場合、インデックスのページ数データ ソースから値が使用できない場合、またはデータ ソースに適用されない場合は、NULL が返されます。|  
|FILTER_CONDITION (ODBC 2.0)|13|Varchar|これは、フィルター条件の給与など、インデックスがフィルター選択されたインデックスの場合は、30000 を >フィルター条件を決定できない場合は、空の文字列になります。<br /><br /> NULL の場合は、インデックスがフィルター選択されたインデックスを特定できないかどうか、インデックスがフィルター選択されたインデックス、または型が SQL_TABLE_STAT。|  
  
 結果セット内の行は、テーブルに対応している場合、ドライバーは種類 SQL_TABLE_STAT を設定し、NON_UNIQUE、INDEX_QUALIFIER、INDEX_NAME、ORDINAL_POSITION、COLUMN_NAME、および ASC_OR_DESC を NULL に設定します。 ページのカーディナリティや利用できない場合、データ ソースから、ドライバーはそれらを NULL に設定します。  
  
## <a name="code-example"></a>コード例  
 同様の関数のコード例では、次を参照してください。 [SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md)します。  
  
## <a name="related-functions"></a>関連する関数  
  
|詳細|参照先|  
|---------------------------|---------|  
|バッファーを結果セット内の列にバインドします。|[SQLBindCol 関数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|ステートメントの処理をキャンセル|[SQLCancel 関数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|1 つの行または順方向専用の方向にデータのブロックをフェッチしています。|[SQLFetch 関数](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|データのブロックをフェッチしています。 または、結果をスクロールの設定|[SQLFetchScroll 関数](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|外部キーの列を返す|[SQLForeignKeys 関数](../../../odbc/reference/syntax/sqlforeignkeys-function.md)|  
|主キーの列を返す|[SQLPrimaryKeys 関数](../../../odbc/reference/syntax/sqlprimarykeys-function.md)|  
  
## <a name="see-also"></a>参照  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)
