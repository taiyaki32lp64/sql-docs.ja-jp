---
title: SQLSpecialColumns 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSpecialColumns
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLSpecialColumns
helpviewer_keywords:
- SQLSpecialColumns function [ODBC]
ms.assetid: bb2d9f21-bda0-4e50-a8be-f710db660034
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 15fa1269b733c9adc938b1880735ae2a4e5db731
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68039557"
---
# <a name="sqlspecialcolumns-function"></a>SQLSpecialColumns 関数
**準拠**  
 バージョンが導入されました。ODBC 1.0 規格に準拠します。[グループを開く]  
  
 **まとめ**  
 **SQLSpecialColumns**指定されたテーブル内の列に関する次の情報を取得します。  
  
-   テーブルの行を一意に識別する最適な列のセット。  
  
-   トランザクションによって行の任意の値が更新されたときに自動的に更新される列。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLSpecialColumns(  
     SQLHSTMT      StatementHandle,  
     SQLSMALLINT   IdentifierType,  
     SQLCHAR *     CatalogName,  
     SQLSMALLINT   NameLength1,  
     SQLCHAR *     SchemaName,  
     SQLSMALLINT   NameLength2,  
     SQLCHAR *     TableName,  
     SQLSMALLINT   NameLength3,  
     SQLSMALLINT   Scope,  
     SQLSMALLINT   Nullable);  
```  
  
## <a name="arguments"></a>引数  
 *StatementHandle*  
 [入力]ステートメント ハンドルです。  
  
 *IdentifierType*  
 [入力]返される列の型。 値は次のいずれかを指定する必要があります。  
  
 SQL_BEST_ROWID:最適な列または列または列から値を取得することによって、指定したテーブルを一意に識別できる任意の行を使用する列のセットを返します。 列には設計されています (Oracle ROWID または Ingres TID) ように、この目的または、列またはテーブルの一意のインデックスの列は、擬似列を指定できます。  
  
 SQL_ROWVER:ある SQLBase ROWID または Sybase タイムスタンプ) などのトランザクションによって行の任意の値が更新されたときに、データ ソースによって自動的に更新される場合、指定したテーブルの列または列を返します。  
  
 *カタログ名*  
 [入力]テーブルのカタログ名。 ドライバーは、いくつかのテーブルのドライバーをさまざまな Dbms、空の文字列からデータを取得した場合など、他ではなく、カタログをサポートしている場合 ("") のカタログはありません。 それらのテーブルを表します。 *CatalogName*文字列の検索パターンを含めることはできません。  
  
 SQL_ATTR_METADATA_ID ステートメント属性は、SQL_TRUE に設定されている場合*CatalogName*は識別子として扱われますそのケースは重要ではありません。 場合は sql_false になります、 *CatalogName*は通常の引数です。 文字どおり、扱われ、そのケースは重要では。 詳細については、次を参照してください。[カタログ関数の引数](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)します。  
  
 *NameLength1*  
 [入力]文字の長さ **CatalogName*します。  
  
 *スキーマ名*  
 [入力]テーブルのスキーマ名です。 ドライバーは、ドライバーをさまざまな Dbms、空の文字列からデータを取得した場合など、他ではなく一部のテーブルのスキーマをサポートしている場合 ("") のスキーマはありません。 それらのテーブルを表します。 *SchemaName*文字列の検索パターンを含めることはできません。  
  
 SQL_ATTR_METADATA_ID ステートメント属性は、SQL_TRUE に設定されている場合*SchemaName*は識別子として扱われますそのケースは重要ではありません。 場合は sql_false になります、 *SchemaName*は通常の引数です。 文字どおり、扱われ、そのケースは重要では。  
  
 *NameLength2*  
 [入力]文字の長さ **SchemaName*します。  
  
 *TableName*  
 [入力]テーブル名です。 この引数は、null ポインターにすることはできません。 *TableName*文字列の検索パターンを含めることはできません。  
  
 SQL_ATTR_METADATA_ID ステートメント属性は、SQL_TRUE に設定されている場合*TableName*は識別子として扱われますそのケースは重要ではありません。 場合は sql_false になります、 *TableName*は通常の引数です。 文字どおり、扱われ、そのケースは重要では。  
  
 *NameLength3*  
 [入力]文字の長さ **TableName*します。  
  
 *Scope*  
 [入力]Rowid の最低限必要な範囲です。 大きいスコープの返された rowid があります。 次のいずれかを指定する必要があります。  
  
 SQL_SCOPE_CURROW:Rowid の該当する行に配置されている間のみ有効にすることが保証されます。 行が更新または別のトランザクションによって削除された場合、rowid を使用して、後で再度選択に行が返されません可能性があります。  
  
 SQL_SCOPE_TRANSACTION:Rowid を現在のトランザクションの期間を有効にすることが保証されます。  
  
 SQL_SCOPE_SESSION:Rowid を (複数のトランザクションにまたがって) 有効、セッションの間にすることが保証されます。  
  
 *NULL 値の使用*  
 [入力]特殊な列値は NULL を返すかどうかを決定します。 次のいずれかを指定する必要があります。  
  
 SQL_NO_NULLS:NULL 値は、特別な列を除外します。 一部のドライバーが SQL_NO_NULLS をサポートできないし、これらのドライバーが SQL_NO_NULLS が指定されている場合は、設定、空の結果を返します。 絶対に必要な場合にのみ、このケースと要求 SQL_NO_NULLS アプリケーションを準備する必要があります。  
  
 SQL_NULLABLE:NULL 値があった場合でも、特殊な列を返します。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_STILL_EXECUTING、SQL_ERROR、または SQL_INVALID_HANDLE します。  
  
## <a name="diagnostics"></a>診断  
 ときに**SQLSpecialColumns** SQL_ERROR または SQL_SUCCESS_WITH_INFO、関連付けられている SQLSTATE 値を返しますを呼び出すことによって取得される可能性があります**SQLGetDiagRec**で、 *HandleType*のSql_handle_stmt として、*処理*の*StatementHandle*します。 次の表に、一般的にによって返される SQLSTATE 値**SQLSpecialColumns** ; この関数のコンテキストでそれぞれについて説明しますと表記"(DM)"の前にドライバー マネージャーによって返されるについての説明。 SQLSTATE 値ごとに関連付けられているリターン コードは明記しない限り、SQL_ERROR です。  
  
|SQLSTATE|[エラー]|説明|  
|--------------|-----------|-----------------|  
|01000|一般的な警告|ドライバー固有の情報メッセージです。 (関数は、SQL_SUCCESS_WITH_INFO を返します)。|  
|08S01|通信リンク エラー|関数が完了した処理の前に、ドライバーとドライバーが接続されているデータ ソース間の通信リンクに失敗しました。|  
|24000|カーソル状態が無効|カーソルが開いて、 *StatementHandle*、および**SQLFetch**または**SQLFetchScroll**が呼び出されました。 このエラーが返されますドライバー マネージャーによって**SQLFetch**または**SQLFetchScroll** SQL_NO_DATA が返されなかったと場合、ドライバーによって返される**SQLFetch**または**SQLFetchScroll** SQL_NO_DATA が返されます。<br /><br /> カーソルが開いて、 *StatementHandle*が**SQLFetch**または**SQLFetchScroll**呼び出されていない必要があります。|  
|40001|シリアル化エラー|トランザクションが別のトランザクションでリソース デッドロックによりロールバックされました。|  
|40003|不明なステートメント入力候補|、この関数の実行中に、関連付けられた接続が失敗し、トランザクションの状態を特定できません。|  
|HY000|一般的なエラー|これがなかった固有の SQLSTATE とする実装に固有の SQLSTATE が定義されていない、エラーが発生しました。 によって返されるエラー メッセージ**SQLGetDiagRec**で、  *\*MessageText*バッファーは、エラーとその原因について説明します。|  
|HY001|メモリの割り当てエラー|ドライバーは、実行または関数の完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY008|操作が取り消されました|非同期処理が有効に、 *StatementHandle*します。 関数が呼び出された、および実行を完了する前に**SQLCancel**または**SQLCancelHandle**が呼び出されて、 *StatementHandle*します。 後でもう一度関数が呼び出された、 *StatementHandle*します。<br /><br /> 関数が呼び出された、および実行を完了する前に**SQLCancel**または**SQLCancelHandle**が呼び出されて、 *StatementHandle*から別のスレッドで、マルチ スレッド アプリケーションです。|  
|HY009|無効な null ポインターの使用|*TableName*引数が null ポインター。<br /><br /> SQL_ATTR_METADATA_ID のステートメント属性、SQL_TRUE に設定されて、 *CatalogName*引数が null ポインターの場合は、および、SQL_CATALOG_NAME*情報の種類*カタログ名を返しますがサポートされています。<br /><br /> (DM) SQL_ATTR_METADATA_ID ステートメント属性の SQL_TRUE に設定された、 *SchemaName*引数が null ポインター。|  
|HY010|関数のシーケンス エラー|(DM) を非同期的に実行中の関数が呼び出された接続ハンドルに関連付けられているため、 *StatementHandle*します。 この関数ではときに実行されている**SQLSpecialColumns**が呼び出されました。<br /><br /> (DM) **SQLExecute**、 **SQLExecDirect**、または**SQLMoreResults**に対して呼び出された、 *StatementHandle* SQL_PARAM_DATA_ を返されます。ご利用いただけます。 ストリームのすべてのパラメーターのデータが取得される前に、この関数が呼び出されました。<br /><br /> (DM) を非同期的に実行中の関数 (いないこの"1") が呼び出された、 *StatementHandle*この関数が呼び出されたときに実行されているとします。<br /><br /> (DM) **SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**、または**SQLSetPos**に対して呼び出された、 *StatementHandle* SQL_NEED_DATA が返されます。 すべての実行時データ パラメーターまたは列のデータが送信される前に、この関数が呼び出されました。|  
|HY013|メモリ管理エラー|基になるメモリ オブジェクトにアクセスできませんでした、場合によってメモリ不足が原因であるために、関数呼び出しを処理できませんでした。|  
|HY090|文字列またはバッファーの長さが無効です。|(DM) 長の引数のいずれかの値が 0 未満でしたが、SQL_NTS と等しくありません。<br /><br /> 長の引数のいずれかの値には、対応する名前の最大長の値を超えています。 それぞれの名前の最大長を呼び出すことによって取得できる**SQLGetInfo**で、*情報の種類*値。SQL_MAX_CATALOG_NAME_LEN、SQL_MAX_SCHEMA_NAME_LEN、または SQL_MAX_TABLE_NAME_LEN します。|  
|HY097|範囲外の列の型|(DM)、無効な*IdentifierType*値が指定されました。|  
|HY098|範囲外のスコープの種類|(DM)、無効な*スコープ*値が指定されました。|  
|HY099|範囲外の null 許容型|(DM)、無効な*Nullable*値が指定されました。|  
|HY117|不明なトランザクションの状態のため、接続が中断されます。 のみを切断して、読み取り専用の関数が許可されます。|(DM) 中断状態の詳細については、次を参照してください。 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)します。|  
|HYC00|省略可能な機能が実装されていません|カタログが指定されていると、ドライバーまたはデータ ソースがカタログをサポートしていません。<br /><br /> スキーマが指定されていると、ドライバーまたはデータ ソース スキーマはサポートしません。<br /><br /> SQL_ATTR_CURSOR_TYPE、SQL_ATTR_CONCURRENCY ステートメント属性の現在の設定の組み合わせが、ドライバーまたはデータ ソースでサポートされていません。<br /><br /> SQL_ATTR_USE_BOOKMARKS ステートメント属性は SQL_UB_VARIABLE に設定されており、SQL_ATTR_CURSOR_TYPE ステートメント属性は、ドライバーがブックマークをできません、カーソルの種類に設定されました。|  
|HYT00|タイムアウトが発生しました|クエリのタイムアウト期間は、要求された結果セットが返されるデータ ソースの前に有効期限が切れました。 によって、タイムアウト期間が設定されます**SQLSetStmtAttr**、SQL_ATTR_QUERY_TIMEOUT します。|  
|HYT01|接続がタイムアウトしました|データ ソースが要求に応答する前に、接続のタイムアウト期間が終了しました。 によって、接続タイムアウト期間が設定されます**SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT します。|  
|IM001|ドライバーでは、この関数はサポートされていません|(DM) に、ドライバーが関連付けられている、 *StatementHandle*関数をサポートしていません。|  
|IM017|非同期通知モードでのポーリングは無効です。|通知のモデルを使用すると、常にポーリングは無効です。|  
|IM018|**SQLCompleteAsync**このハンドルに対する前の非同期操作を完了が呼び出されていません。|通知モードが有効になっている場合、ハンドルでは、前の関数呼び出しに SQL_STILL_EXECUTING が返された場合と**SQLCompleteAsync**後処理を行い、操作を完了するハンドルで呼び出す必要があります。|  
  
## <a name="comments"></a>コメント  
 ときに、 *IdentifierType*引数は、SQL_BEST_ROWID **SQLSpecialColumns**列またはテーブル内の各行を一意に識別する列を返します。 これらの列で常に使用できる、*選択リスト*または**WHERE**句。 **SQLColumns**テーブルの列でさまざまな情報を返すために使用するは必ずしも返さない、各行を一意に識別する列またはによって行のいずれかの値に自動的に更新される列を更新します。トランザクションです。 たとえば、 **SQLColumns** Oracle の擬似列 ROWID を返さなかった可能性があります。 これは、ため**SQLSpecialColumns**これらの列を返すために使用します。 詳細については、次を参照してください。[カタログ データの使用](../../../odbc/reference/develop-app/uses-of-catalog-data.md)します。  
  
> [!NOTE]  
>  一般的な使用、引数、および ODBC カタログ関数の返されたデータの詳細については、次を参照してください。[カタログ関数](../../../odbc/reference/develop-app/catalog-functions.md)します。  
  
 場合は、テーブルの各行を一意に識別する列が存在しない**SQLSpecialColumns**行の存在しない行セットを返します後続の呼び出し**SQLFetch**または**SQLFetchScroll**。ステートメント SQL_NO_DATA が返されます。  
  
 場合、 *IdentifierType*、*スコープ*、または*Nullable*引数は、データ ソースでサポートされていない特性を指定**SQLSpecialColumns**空の結果セットを返します。  
  
 SQL_ATTR_METADATA_ID ステートメント属性は、SQL_TRUE に設定されている場合、 *CatalogName*、 *SchemaName*、および*TableName*のための引数は、識別子として扱われます、特定の状況での null ポインターを設定することはできません。 (詳細については、次を参照してください[カタログ関数の引数](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)。)。  
  
 **SQLSpecialColumns**スコープによって順序付けられた、標準的な結果セットとして結果を返します。  
  
 次の列が ODBC の名前が変更された*3.x*します。 列名の変更では、アプリケーションは、列番号でバインドため、旧バージョンとの互換性は影響しません。  
  
|ODBC 2.0 列|ODBC *3.x*列|  
|---------------------|-----------------------|  
|PRECISION|COLUMN_SIZE|  
|LENGTH|BUFFER_LENGTH|  
|SCALE|DECIMAL_DIGITS|  
  
 COLUMN_NAME 列の実際の長さを確認するアプリケーションを呼び出すことができます**SQLGetInfo** SQL_MAX_COLUMN_NAME_LEN オプションを使用します。  
  
 次の表には、結果セット内の列が一覧表示します。 ドライバーでは、8 (PSEUDO_COLUMN) 列を超える追加の列を定義できます。 アプリケーションでは、明示的な序数位置を指定するのではなく、結果セットの末尾からカウント ダウンによって、ドライバー固有の列へのアクセスを得る必要があります。 詳細については、次を参照してください。[カタログ関数によって返されるデータ](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)します。  
  
|列名|列番号|データ型|コメント|  
|-----------------|-------------------|---------------|--------------|  
|スコープ (ODBC 1.0)|1|Smallint|Rowid の実際の範囲。 次の値のいずれかが含まれます。<br /><br /> SQL_SCOPE_CURROW SQL_SCOPE_TRANSACTION SQL_SCOPE_SESSION<br /><br /> NULL が返されます*IdentifierType* SQL_ROWVER です。 各値については、の説明を参照してください。*スコープ*構文では"、"このセクションで前にします。|  
|COLUMN_NAME (ODBC 1.0)|2|NULL 以外の Varchar|列名 ドライバーは、名前がない列の空の文字列を返します。|  
|DATA_TYPE (ODBC 1.0)|3|Smallint (NULL 以外)|SQL データ型です。 これには、ODBC SQL データ型をまたはドライバーに固有の SQL データ型を指定できます。 有効な ODBC SQL データ型の一覧は、次を参照してください。 [SQL データ型](../../../odbc/reference/appendixes/sql-data-types.md)します。 ドライバー固有の SQL データ型については、ドライバーのドキュメントを参照してください。|  
|TYPE_NAME (ODBC 1.0)|4|NULL 以外の Varchar|データ ソースに依存するデータ型名です。たとえば、"CHAR"、"VARCHAR"、"MONEY"、"LONG VARBINARY"、または「CHAR FOR BIT DATA ()」。|  
|COLUMN_SIZE (ODBC 1.0)|5|Integer|データ ソースの列のサイズ。 列のサイズに関する詳細については、次を参照してください。[列のサイズ、10 進数字、転送オクテット長、および表示サイズ](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)します。|  
|BUFFER_LENGTH 列 (ODBC 1.0)|6|Integer|転送されるデータの長さ (バイト単位)、 **SQLGetData**または**SQLFetch** SQL_C_DEFAULT が指定されている場合に操作します。 数値データは、このサイズは、データ ソースに格納されたデータのサイズよりも異なる場合があります。 この値は、文字またはバイナリ データ、COLUMN_SIZE 列の場合と同じです。 詳細については、次を参照してください。[列のサイズ、10 進数字、転送オクテット長、および表示サイズ](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)します。|  
|DECIMAL_DIGITS (ODBC 1.0)|7|Smallint|データ ソースの列の 10 進数字。 10 進数字は適用できないデータ型の NULL を返します。 詳細については 10 進数字、次を参照してください。[列のサイズ、10 進数字、転送オクテット長、および表示サイズ](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)します。|  
|PSEUDO_COLUMN (ODBC 2.0)|8|Smallint|列が Oracle ROWID などの擬似列かどうかを示します。<br /><br /> SQL_PC_UNKNOWN SQL_PC_NOT_PSEUDO SQL_PC_PSEUDO**に注意してください。** 最大の相互運用性の擬似列必要がありますいないは引用符で囲むによって返される引用符文字の識別子を持つ**SQLGetInfo**します。|  
  
 アプリケーションは、SQL_BEST_ROWID の値を取得した後、アプリケーションは、定義されたスコープ内でその行をこれらの値を使用できます。 **選択**ステートメントに行または 1 つの行を返すことが保証されます。  
  
 アプリケーションは、rowid 列に基づいて行を再選択行が見つからない場合は、アプリケーションは、行が削除されたか、rowid 列が変更されたことを想定できます。 逆は true ではありません: rowid が変更されていない場合でも、行の他の列を変更可能性があります。  
  
 SQL_BEST_ROWID は前方スクロールする必要があるアプリケーション、および行のセットから最新のデータを取得する結果セットを以内にもう一度有効な列の型に対して返される列。 Rowid の列は、その行に配置されているときに変更が保証されます。  
  
 カーソルが行に配置されていない場合でもが有効なまま、rowid の列アプリケーションは、結果セットのスコープの列をチェックしてこれを特定できます。  
  
 SQL_ROWVER は rowid を使用して、行が再度選択されるときに、特定の行の任意の列が更新されたかどうかを確認する機能を必要とするアプリケーションに適して列型に対して返される列。 たとえば、rowid を使用して行を再度選択した後、アプリケーションは、SQL_ROWVER 列だけをフェッチするものでは、前の値を比較できます。 SQL_ROWVER 列の値は、前の値と異なる場合、アプリケーションは、表示上のデータが変更されたユーザーに警告できます。  
  
## <a name="code-example"></a>コード例  
 同様の関数のコード例では、次を参照してください。 [SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md)します。  
  
## <a name="related-functions"></a>関連する関数  
  
|詳細|参照先|  
|---------------------------|---------|  
|バッファーを結果セット内の列にバインドします。|[SQLBindCol 関数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|ステートメントの処理をキャンセル|[SQLCancel 関数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|テーブルまたはテーブルの列を返す|[SQLColumns 関数](../../../odbc/reference/syntax/sqlcolumns-function.md)|  
|1 つの行または順方向専用の方向にデータのブロックをフェッチしています|[SQLFetch 関数](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|データのブロックをフェッチしています。 または、結果をスクロールの設定|[SQLFetchScroll 関数](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|主キーの列を返す|[SQLPrimaryKeys 関数](../../../odbc/reference/syntax/sqlprimarykeys-function.md)|  
  
## <a name="see-also"></a>参照  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)
