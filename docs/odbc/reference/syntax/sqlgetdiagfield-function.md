---
title: SQLGetDiagField 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetDiagField
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetDiagField
helpviewer_keywords:
- SQLGetDiagField function [ODBC]
ms.assetid: 1dbc4398-97a8-4585-bb77-1f7ea75e24c4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 620ccce9a035139482b2d9b4630bb2242f720af8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68103774"
---
# <a name="sqlgetdiagfield-function"></a>SQLGetDiagField 関数

**準拠**  
 バージョンが導入されました。ODBC 3.0 規格に準拠します。ISO 92  
  
 **まとめ**  
 **SQLGetDiagField**エラー、警告、およびステータス情報を含む診断データ構造 (指定したハンドルに関連付けられている) のレコードのフィールドの現在の値を返します。  
  
## <a name="syntax"></a>構文  
  
```cpp

SQLRETURN SQLGetDiagField(  
     SQLSMALLINT     HandleType,  
     SQLHANDLE       Handle,  
     SQLSMALLINT     RecNumber,  
     SQLSMALLINT     DiagIdentifier,  
     SQLPOINTER      DiagInfoPtr,  
     SQLSMALLINT     BufferLength,  
     SQLSMALLINT *   StringLengthPtr);  
```  
  
## <a name="arguments"></a>引数  
 *HandleType*  
 [入力]診断が必要なハンドルの型を記述するハンドル型の識別子です。 次のいずれかを指定する必要があります。  
  
-   SQL_HANDLE_DBC として  
  
-   SQL_HANDLE_DBC_INFO_TOKEN  
  
-   SQL_HANDLE_DESC  
  
-   SQL_HANDLE_ENV として  
  
-   SQL_HANDLE_STMT として  
  
 SQL_HANDLE_DBC_INFO_TOKEN ハンドルは、ドライバー マネージャーとドライバーでのみ使用されます。 アプリケーションでは、この種類のハンドルは使用しないでください。 SQL_HANDLE_DBC_INFO_TOKEN の詳細については、次を参照してください。 [ODBC ドライバーで接続プールの認識を開発](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)します。  
  
 *Handle*  
 [入力]診断データの構造で示される型のハンドルを*HandleType*します。 場合*HandleType* sql_handle_env としてでは、*処理*共有または共有されていない環境ハンドルのいずれかにすることができます。  
  
 *RecNumber*  
 [入力]アプリケーションが情報をシークする元の状態レコードを示します。 状態レコードは、1 から番号が付けられます。 場合、 *DiagIdentifier*引数が、診断ヘッダーのすべてのフィールドを示します*RecNumber*は無視されます。 ない場合は、0 以上である必要があります。  
  
 *DiagIdentifier*  
 [入力]値が返される診断フィールドを示します。 詳細については、次を参照してください、"*DiagIdentifier*引数"セクション"コメントです。"。  
  
 *DiagInfoPtr*  
 [出力]診断情報を返すバッファーへのポインター。 データ型の値に依存*DiagIdentifier*します。 場合*DiagInfoPtr*は整数型には、アプリケーションは sqlulen ですのバッファーを使用する必要があります、および、値をいくつかのドライバーとして、この関数を呼び出す前に 0 がのみが初期化下位 32 ビットまたは 16 ビットのバッファーを書き込むし、上位のままにしますビットが変更されていません。  
  
 場合*DiagInfoPtr*が null の場合、 *StringLengthPtr*バイト (文字データの null 終端文字を除く) の合計数を返すはまだが指すバッファーに返される使用可能な*DiagInfoPtr*します。  
  
 *BufferLength*  
 [入力]場合*DiagIdentifier*は、ODBC で定義された診断と*DiagInfoPtr*文字の文字列またはバイナリのバッファーを指す、この引数の長さである必要があります\* *DiagInfoPtr*. 場合*DiagIdentifier* ODBC で定義されたフィールドと\* *DiagInfoPtr*整数*BufferLength*は無視されます。 場合の値 *\*DiagInfoPtr*は Unicode 文字列です (呼び出し時に**SQLGetDiagFieldW**)、 *BufferLength*引数は偶数である必要があります。  
  
 場合*DiagIdentifier*ドライバーの定義済みのフィールドでは、アプリケーションでは、フィールドには、ドライバー マネージャーの性質を示しますを設定して、 *BufferLength*引数。 *BufferLength*次の値を持つことができます。  
  
-   場合*DiagInfoPtr*文字の文字列へのポインターは、 *BufferLength* SQL_NTS または文字列の長さです。  
  
-   場合*DiagInfoPtr*バイナリのバッファー、アプリケーションの場所へのポインター、SQL_LEN_BINARY_ATTR の結果は、(*長さ*) マクロで*BufferLength*します。 これにより、負の値で*BufferLength*します。  
  
-   場合*DiagInfoPtr*文字の文字列またはバイナリ文字列以外の値へのポインターは、 *BufferLength* SQL_IS_POINTER 値でなければなりません。  
  
-   場合 *\*DiagInfoPtr* 、固定長データ型を含む*BufferLength*に応じて SQL_IS_INTEGER、SQL_IS_UINTEGER、SQL_IS_SMALLINT、または SQL_IS_USMALLINT は、します。  
  
 *StringLengthPtr*  
 [出力](Null 終端文字のために必要なバイト数を除く) バイトの合計数を返すバッファーへのポインターで返される使用可能な\* *DiagInfoPtr*、文字データ。 返される使用可能なバイト数がより大きいかに等しい場合*BufferLength*、内のテキスト\* *DiagInfoPtr*に切り捨てられます*BufferLength*マイナスnull 終了文字の長さ。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR、SQL_INVALID_HANDLE、または SQL_NO_DATA します。  
  
## <a name="diagnostics"></a>診断  
 **SQLGetDiagField**自体の診断レコードは通知されません。 次の戻り値を使用して、独自の実行の結果を報告します。  
  
-   SQL_SUCCESS:関数には、診断情報が正常に返されます。  
  
-   SQL_SUCCESS_WITH_INFO:\**DiagInfoPtr*が要求された診断フィールドを保持するためには小さすぎます。 そのため、診断フィールドのデータが切り捨てられました。 切り捨てが発生したことは、アプリケーションを比較する必要がありますを決定する*BufferLength*実際に記述されている、使用可能なバイト数へ **StringLengthPtr*します。  
  
-   SQL_INVALID_HANDLE:によって示されるハンドル*HandleType*と*処理*が有効なハンドル。  
  
-   SQL_ERROR:次のいずれかが発生しました。  
  
    -   *DiagIdentifier*引数が有効な値のいずれか。  
  
    -   *DiagIdentifier*引数が SQL_DIAG_CURSOR_ROW_COUNT、SQL_DIAG_DYNAMIC_FUNCTION、SQL_DIAG_DYNAMIC_FUNCTION_CODE、または、SQL_DIAG_ROW_COUNT が*処理*がステートメント ハンドルではありません。 (ドライバー マネージャーを診断します。)  
  
    -   *RecNumber*引数が負または 0 とき*DiagIdentifier*診断レコードからフィールドを指定します。 *RecNumber*ヘッダー フィールドは無視されます。  
  
    -   要求された値が文字の文字列と*BufferLength* 0 未満でした。  
  
    -   非同期通知を使用する場合、ハンドルに対して非同期操作は完了しませんでした。  
  
-   SQL_NO_DATA:*RecNumber*診断レコードで指定したハンドルに存在していた数よりも大きかった*を処理します。* 関数が SQL_NO_DATA を任意の正のも返します*RecNumber*に対する診断レコードがない場合*処理*します。  
  
## <a name="comments"></a>コメント  
 アプリケーションを呼び出す通常**SQLGetDiagField** 3 つの目標の 1 つを実行します。  
  
1.  関数呼び出しが SQL_ERROR または sql_success_with_info が返されるときに、特定のエラーまたは警告情報を取得する (またはの SQL_NEED_DATA、 **SQLBrowseConnect**関数)。  
  
2.  呼び出して、insert、delete、または更新操作が実行されたときの影響を受けたデータ ソース内の行の数を決定する**SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**、または**SQLSetPos** (SQL_DIAG_ROW_COUNT ヘッダー フィールドから)、または、ドライバーは、この情報を提供できる場合は、現在開いているカーソル内に存在する行の数を決定する (から、SQL_DIAG_CURSOR_ROW_COUNT ヘッダー フィールド)。  
  
3.  呼び出しによってどの関数が実行されたかを判断する**SQLExecDirect**または**SQLExecute** (から SQL_DIAG_DYNAMIC_FUNCTION と SQL_DIAG_DYNAMIC_FUNCTION_CODE ヘッダー フィールド)。  
  
 ODBC 関数できますを投稿 0 個以上の診断レコードことが呼び出されるたびにアプリケーションを呼び出すことができます**SQLGetDiagField**任意の ODBC 関数呼び出しの後にします。 いつでも格納できる診断レコードの数に制限はありません。 **SQLGetDiagField**最後に指定された診断データの構造体に関連付けられている診断情報だけを取得、*処理*引数。 アプリケーションが他にも ODBC 関数を呼び出す場合**SQLGetDiagField**または**SQLGetDiagRec**、同じハンドルを使用して前の呼び出しから診断情報は失われます。  
  
 アプリケーションが増分することですべての診断レコードをスキャンできます*RecNumber*限り**SQLGetDiagField** SQL_SUCCESS を返します。 SQL_DIAG_NUMBER ヘッダー フィールドには、状態レコードの数が示されます。 呼び出す**SQLGetDiagField**ヘッダーとレコードのフィールドを非破壊的なは。 アプリケーションが呼び出すことができます**SQLGetDiagField**後でもう一度間に、同じハンドルにレコードを投稿すると、診断関数以外の関数が呼び出されていない限り、レコードからフィールドを取得します。  
  
 アプリケーションが呼び出すことができます**SQLGetDiagField** SQL_DIAG_CURSOR_ROW_COUNT または SQL_DIAG_ROW_COUNT、SQL_ERROR が返されます場合を除き、いつでも任意の診断フィールドを返す*処理*されませんが、ステートメント ハンドルです。 その他の診断フィールドが定義されていない場合への呼び出し**SQLGetDiagField** (提供される他の診断が出現しない) に関係なく SQL_SUCCESS を返します、フィールド、未定義の値が返されます。  
  
 詳細については、次を参照してください。[を使用して SQLGetDiagRec および SQLGetDiagField](../../../odbc/reference/develop-app/using-sqlgetdiagrec-and-sqlgetdiagfield.md)と[実装 SQLGetDiagRec および SQLGetDiagField](../../../odbc/reference/develop-app/implementing-sqlgetdiagrec-and-sqlgetdiagfield.md)します。  
  
 HY010 が生成されますが、非同期的に実行されているものと異なる API を呼び出す「関数のシーケンス エラーです」。 ただし、非同期操作が完了する前に、エラー レコードを取得できません。  
  
## <a name="handletype-argument"></a>HandleType 引数  
 各ハンドル型には、関連付けられている診断情報を持つことができます。 *HandleType*引数のハンドルの種類を示す*処理*します。  
  
 いくつかのヘッダーとレコード フィールドは、環境、接続、ステートメント、および記述子ハンドル返されることはできません。 続く「ヘッダー フィールド」と「レコードのフィールド」セクションでは、フィールドが適用されていないそれらのハンドルが示されます。  
  
 場合*HandleType* sql_handle_env としてでは、*処理*共有または共有されていない環境ハンドルのいずれかであることができます。  
  
 環境ハンドルを関連付けることはドライバー固有のヘッダーの診断フィールドはありません。  
  
 記述子ハンドルに対して定義されている診断のみヘッダー フィールドとは、SQL_DIAG_NUMBER および SQL_DIAG_RETURNCODE です。  
  
## <a name="diagidentifier-argument"></a>DiagIdentifier 引数  
 この引数は、診断データの構造から必要なフィールドの識別子を示します。 場合*RecNumber*がより大きい、フィールド内のデータ説明関数によって返される診断情報を 1 に等しいか、または。 場合*RecNumber*が 0 のフィールドが診断データの構造体のヘッダー内で診断の情報を特定の情報が返される関数呼び出しに関連するデータを含んでいます場合、。  
  
 ドライバーは、診断データの構造体で、ドライバー固有のヘッダーとレコードのフィールドを定義できます。  
  
 ODBC 3 *.x*アプリケーションは、ODBC 2 *.x*を呼び出すことがドライバー **SQLGetDiagField**でのみ、 *DiagIdentifier*SQL_DIAG_CLASS_ORIGIN、SQL_DIAG_CLASS_SUBCLASS_ORIGIN、SQL_DIAG_CONNECTION_NAME、SQL_DIAG_MESSAGE_TEXT、SQL_DIAG_NATIVE、SQL_DIAG_NUMBER、SQL_DIAG_RETURNCODE、SQL_DIAG_SERVER_NAME、または SQL_DIAG_SQLSTATE の引数です。 その他のすべての診断フィールドには、SQL_ERROR が返されます。  
  
## <a name="header-fields"></a>ヘッダー フィールド  
 次の表に示されているヘッダー フィールドに含まれる、 *DiagIdentifier*引数。  
  
|DiagIdentifier|の戻り値の型 :|戻り値|  
|--------------------|-----------------|-------------|  
|SQL_DIAG_CURSOR_ROW_COUNT|SQLLEN|このフィールドには、カーソル内の行の数が含まれています。 そのセマンティクスが異なります、 **SQLGetInfo** SQL_DYNAMIC_CURSOR_ATTRIBUTES2、SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2、SQL_KEYSET_CURSOR_ATTRIBUTES2、および SQL_STATIC_CURSOR_ATTRIBUTES2、いることを示す情報の種類行カウントは各カーソルの種類 (SQL_CA2_CRC_EXACT と SQL_CA2_CRC_APPROXIMATE ビット) で使用できます。<br /><br /> ステートメント ハンドルののみとにした場合のみ、このフィールドの内容が定義された**SQLExecute**、 **SQLExecDirect**、または**SQLMoreResults**が呼び出されました。 呼び出す**SQLGetDiagField**で、 *DiagIdentifier*ハンドルには、ステートメント以外で SQL_DIAG_CURSOR_ROW_COUNT の SQL_ERROR が返されます。|  
|SQL_DIAG_DYNAMIC_FUNCTION|SQLCHAR *|これは、基になる関数が実行される SQL ステートメントを記述する文字列です。 (特定の値をこのセクションで後で「動的関数のフィールドの値」を参照してください)。ステートメント ハンドルとへの呼び出し後にのみ、このフィールドの内容が定義された**SQLExecute**、 **SQLExecDirect**、または**SQLMoreResults**します。 呼び出す**SQLGetDiagField**で、 *DiagIdentifier*ハンドルには、ステートメント以外で SQL_DIAG_DYNAMIC_FUNCTION の SQL_ERROR が返されます。 呼び出す前にこのフィールドの値は未定義**SQLExecute**または**SQLExecDirect**します。|  
|SQL_DIAG_DYNAMIC_FUNCTION_CODE|SQLINTEGER|これは、基になる関数によって実行された SQL ステートメントを表す数値コードです。 (特定の値に対して「値の動的関数フィールドの」このセクションの後半を参照してください)。ステートメント ハンドルとへの呼び出し後にのみ、このフィールドの内容が定義された**SQLExecute**、 **SQLExecDirect**、または**SQLMoreResults**します。 呼び出す**SQLGetDiagField**で、 *DiagIdentifier*ハンドルには、ステートメント以外で SQL_DIAG_DYNAMIC_FUNCTION_CODE の SQL_ERROR が返されます。 呼び出す前にこのフィールドの値は未定義**SQLExecute**または**SQLExecDirect**します。|  
|SQL_DIAG_NUMBER|SQLINTEGER|指定したハンドルの使用可能な状態レコードの数。|  
|SQL_DIAG_RETURNCODE|SQLRETURN|関数によって返されるリターン コード。 リターン コードの一覧は、次を参照してください。[リターン コード](../../../odbc/reference/develop-app/return-codes-odbc.md)します。 ドライバーは SQL_DIAG_RETURNCODE; を実装する必要はありません。ドライバー マネージャーによって常に実装されます。 関数がまだ呼び出されていないの場合、*処理*、SQL_DIAG_RETURNCODE SQL_SUCCESS が返されます。|  
|SQL_DIAG_ROW_COUNT|SQLLEN|Insert、delete、またはによって実行された更新によって影響を受ける行の数**SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**、または**SQLSetPos**. ドライバー定義後に、*カーソル仕様*が実行されました。 このフィールドの内容は、ステートメント ハンドルに対してのみ定義されます。 呼び出す**SQLGetDiagField**で、 *DiagIdentifier*ハンドルには、ステートメント以外で SQL_DIAG_ROW_COUNT の SQL_ERROR が返されます。 このフィールドのデータが返されることも、 *RowCountPtr*の引数**SQLRowCount**します。 によって返される行の数は、このフィールドのデータがすべて nondiagnostic 関数の呼び出し後にリセットされます**SQLRowCount**ステートメントが準備済みまたは割り当て済みの状態に戻してまで同じままになります。|  
  
## <a name="record-fields"></a>レコードのフィールド  
 次の表に示されているレコード フィールドに含まれる、 *DiagIdentifier*引数。  
  
|DiagIdentifier|の戻り値の型 :|戻り値|  
|--------------------|-----------------|-------------|  
|SQL_DIAG_CLASS_ORIGIN|SQLCHAR *|このレコードの SQLSTATE 値のクラス部分を定義するドキュメントを示す文字列。 その値が、Open Group と ISO コールレベル インターフェイスによって定義されたすべての SQLSTATEs"ISO 9075"。 (これらすべてが SQLSTATE クラスは、"IM") に固有の ODBC SQLSTATEs、その値は"ODBC 3.0" です。|  
|SQL_DIAG_COLUMN_NUMBER|SQLINTEGER|SQL_DIAG_ROW_NUMBER フィールドが、行セットまたは一連のパラメーターの有効な行番号の場合は、このフィールドには、結果セット内の列番号またはパラメーターのセット内のパラメーター数を表す値が含まれています。 結果セット列の番号は常に 1 から開始この状態レコードは、ブックマーク列に関係している場合、フィールドは 0 にすることができます。 パラメーター番号は、1 から始まります。 値 SQL_NO_COLUMN_NUMBER 状態レコードは、列の数またはパラメーターの番号に関連付けられていない場合があります。 ドライバーが、列の数またはこのレコードが関連付けられているパラメーターの数を判別できない場合、このフィールドは SQL_COLUMN_NUMBER_UNKNOWN 値を持ちます。<br /><br /> このフィールドの内容は、ステートメント ハンドルに対してのみ定義されます。|  
|SQL_DIAG_CONNECTION_NAME|SQLCHAR *|診断レコードに関連する接続の名前を示す文字列。 このフィールドは、ドライバーの定義です。 環境ハンドルに関連付けられている診断データの構造とすべての接続に関係しない診断では、このフィールドは、長さ 0 の文字列です。|  
|SQL_DIAG_MESSAGE_TEXT|SQLCHAR *|エラーまたは警告の情報メッセージです。 このフィールドは」の説明に従って書式設定された[診断メッセージ](../../../odbc/reference/develop-app/diagnostic-messages.md)します。 診断メッセージのテキストの最大長はありません。|  
|SQL_DIAG_NATIVE|SQLINTEGER|ドライバー/データ ソース固有のネイティブ エラー コード。 ネイティブ エラー コードがない場合、ドライバーは、0 を返します。|  
|SQL_DIAG_ROW_NUMBER|SQLLEN|このフィールドには、行セットの行番号または状態レコードが関連付けられているパラメーターのセット内のパラメーター数が含まれています。 行番号およびパラメーターの番号は、1 から始まります。 このフィールドは、この状態レコードは、行番号またはパラメーターの番号に関連付けられていない場合、SQL_NO_ROW_NUMBER 値を持ちます。 ドライバーが、行番号またはこのレコードが関連付けられているパラメーターの数を判別できない場合、このフィールドは SQL_ROW_NUMBER_UNKNOWN 値を持ちます。<br /><br /> このフィールドの内容は、ステートメント ハンドルに対してのみ定義されます。|  
|SQL_DIAG_SERVER_NAME|SQLCHAR *|診断レコードに関連するサーバー名を示す文字列。 これはへの呼び出しに返される値と同じ**SQLGetInfo** SQL_DATA_SOURCE_NAME オプションを使用します。 環境ハンドルに関連付けられている診断データの構造と任意のサーバーに関係しない診断では、このフィールドは、長さ 0 の文字列です。|  
|SQL_DIAG_SQLSTATE|SQLCHAR *|5 文字の SQLSTATE 診断コード。 詳細については、次を参照してください。 [SQLSTATEs](../../../odbc/reference/develop-app/sqlstates.md)します。|  
|SQL_DIAG_SUBCLASS_ORIGIN|SQLCHAR *|SQL_DIAG_CLASS_ORIGIN、SQLSTATE コードのサブクラスの一部の定義の部分を識別すると同じ形式と有効な値を含む文字列。 "ODBC 3.0"が返される ODBC 固有について、次のとおりです。<br /><br /> 01S00、01S01、01S02、01S06、01S07、07S01、08S01、21S01、21S02、25S01、25S02、25S03、42S01、42S02、42S11、42S12、42S21、42S22、HY095、HY097、HY098、HY099、HY100、HY101、HY105、HY107、HY109、HY110、HY111、HYT00、HYT01、IM001、IM002、IM003、IM004、IM005、IM006、IM007、IM008、IM010、IM011、IM012 します。|  
  
## <a name="values-of-the-dynamic-function-fields"></a>動的関数のフィールドの値  
 次の表に、SQL_DIAG_DYNAMIC_FUNCTION と SQL_DIAG_DYNAMIC_FUNCTION_CODE の値への呼び出しによって実行された SQL ステートメントの種類ごとに適用される**SQLExecute**または**SQLExecDirect**. ドライバーは、記載されているドライバーの定義済みの値を追加できます。  
  
|SQL ステートメント (SQL statement)<br /><br /> 実行|値<br /><br /> SQL_DIAG_DYNAMIC_FUNCTION|値<br /><br /> SQL_DIAG_DYNAMIC_FUNCTION_CODE|  
|--------------------------------|-----------------------------------------------|-----------------------------------------------------|  
|*alter ドメイン ステートメント*|「ALTER ドメイン」|SQL_DIAG_ALTER_DOMAIN|  
|*alter table ステートメント*|"ALTER TABLE"|SQL_DIAG_ALTER_TABLE|  
|*アサーション定義*|「アサーションの作成」|SQL_DIAG_CREATE_ASSERTION|  
|*文字セットの定義*|"文字セットの作成|SQL_DIAG_CREATE_CHARACTER_SET|  
|*照合順序定義*|「照合順序の作成」|SQL_DIAG_CREATE_COLLATION|  
|*domainn 定義*|「ドメインの作成」|SQL_DIAG_CREATE_DOMAIN|
|*create index ステートメント*|「インデックスの作成」|SQL_DIAG_CREATE_INDEX|  
|*create table ステートメント*|「テーブルの作成」|SQL_DIAG_CREATE_TABLE|  
|*create view ステートメント*|「ビューの作成」|SQL_DIAG_CREATE_VIEW|  
|*カーソルの指定*|"カーソルの選択|SQL_DIAG_SELECT_CURSOR|  
|*delete-statement-positioned*|"動的な削除の CURSOR"|SQL_DIAG_DYNAMIC_DELETE_CURSOR|  
|*delete ステートメントの検索*|[場所の削除]|SQL_DIAG_DELETE_WHERE|  
|*drop アサーションのステートメント*|「ドロップ アサーション」|SQL_DIAG_DROP_ASSERTION|  
|*ドロップ文字セット stmt*|「ドロップ文字セット」|SQL_DIAG_DROP_CHARACTER_SET|  
|*drop の照合順序-ステートメント*|「照合順序をドロップ」|SQL_DIAG_DROP_COLLATION|  
|*drop ドメイン-ステートメント*|「ドロップ ドメイン」|SQL_DIAG_DROP_DOMAIN|  
|*drop index-ステートメント*|"DROP INDEX"|SQL_DIAG_DROP_INDEX|  
|*drop schema のステートメント*|"DROP SCHEMA"|SQL_DIAG_DROP_SCHEMA|  
|*drop-テーブル-ステートメント*|"DROP TABLE"|SQL_DIAG_DROP_TABLE|  
|*drop-変換-ステートメント*|「変換してドロップ」|SQL_DIAG_DROP_TRANSLATION|  
|*drop-ビュー-ステートメント*|"DROP VIEW"|SQL_DIAG_DROP_VIEW|  
|*grantstatement*|「許可」|SQL_DIAG_GRANT|
|*insert ステートメント*|"INSERT"|SQL_DIAG_INSERT|  
|*ODBC の手順-拡張機能*|"CALL"|SQL_DIAG_ 呼び出し|  
|*revoke-statement*|"REVOKE"|SQL_DIAG_REVOKE|  
|*スキーマ定義*|「スキーマの作成」|SQL_DIAG_CREATE_SCHEMA|  
|*翻訳の定義*|「翻訳の作成」|SQL_DIAG_CREATE_TRANSLATION|  
|*update-statement-positioned*|「動的な更新カーソル」|SQL_DIAG_DYNAMIC_UPDATE_CURSOR|  
|*update-statement-searched*|「場所の更新」|SQL_DIAG_UPDATE_WHERE|  
|Unknown|*空の文字列*|SQL_DIAG_UNKNOWN_STATEMENT|  

<!--
These two malformed table rows were fixed by educated GUESS only.
Each pair starts with the original flawed row.
Flawed because treated as only two cells by HTML render,
and because missing info anyway.
Also, these flawed rows lacked '|' as their first nonWhitespace character (although markdown technically allows this omission, unfortunately).
Arguably the following SQL.H file shows the sequence of the flawed rows in the table was suboptimal also.

ftp://www.fpc.org/fpc32/VS6Disk1/VC98/INCLUDE/SQL.H

GeneMi , 2019/01/19
- - - - - - - - - - - - - -

n-definition*|"CREATE DOMAIN"|SQL_DIAG_CREATE_DOMAIN|  

|*domain-definition*|"CREATE DOMAIN"|SQL_DIAG_CREATE_DOMAIN|

-statement*|"GRANT"|SQL_DIAG_GRANT|  

|*grant-statement*|"GRANT"|SQL_DIAG_GRANT|

-->

## <a name="sequence-of-status-records"></a>状態レコードのシーケンス

 状態レコードは、行番号と診断の種類に基づいてシーケンス内に配置されます。 ドライバー マネージャーは、最終的な順序で生成される状態レコードが返されるを決定します。 ドライバーは、最終的な順序で生成される状態レコードが返されるを決定します。  
  
 診断レコードは、ドライバー マネージャーとドライバーの両方によって投稿されたは場合、ドライバー マネージャーが順序付ける責任を負います。  
  
 2 つ以上の状態レコードがある場合、行番号によってレコードのシーケンスが最初に決定されます。 診断レコードのシーケンスを決定する行ごとに、次の規則が適用されます。  
  
-   任意の行に対応していないレコードには-1 SQL_NO_ROW_NUMBER が定義されているために、特定の行に対応するレコードの前に表示されます。  
  
-   SQL_ROW_NUMBER_UNKNOWN が-2 に定義されているため、他のすべてのレコードの前に対象の行番号が不明のレコードが表示されます。  
  
-   特定の行に関連するすべてのレコードのレコードは SQL_DIAG_ROW_NUMBER フィールドの値によって並べ替えられます。 すべてのエラーと影響を受けた最初の行の警告が表示され、すべてのエラーと警告は、次の行の影響を受けるとします。  
  
> [!NOTE]
>  ODBC 3 *.x*場合、ドライバー マネージャーが診断のキューの状態レコードを注文しない SQLSTATE 01S01 (行内のエラー) が、ODBC 2 によって返される *.x*ドライバーまたは SQLSTATE 01S01 ODBC によって (行内のエラー) が返されます3 *.x*ドライバーと**SQLExtendedFetch**と呼びますまたは**SQLSetPos**に位置付けられているカーソルで呼び出される**SQLExtendedFetch**.  
  
 内での行ごとに、またはこれらすべてのレコードが行番号が不明、または行に対応していないまたは SQL_NO_ROW_NUMBER と等しい行番号は、これらすべてのレコードについて、表示されている最初のレコードは、並べ替え規則のセットを使用して決定されます。 最初のレコードの後の行に影響を与える、他のレコードの順序は定義されません。 アプリケーションは、警告のエラーは、最初のレコードの後に前に限りません。 アプリケーションでは、完全な関数呼び出しが失敗した情報を入手する完全な診断データの構造をスキャンする必要があります。  
  
 次の規則は、行内の最初のレコードの確認に使用されます。 最高のランクを持つレコードは、最初のレコードです。 (ドライバー マネージャー、ドライバー、ゲートウェイ、およびなど) のレコードのソースとは見なされませんときにレコードを順位付けします。  
  
-   **エラー**最高ランクであるエラーを記述した状態レコード。 エラーを並べ替えるには、次の規則が適用されます。  
  
    -   トランザクションの失敗または可能なトランザクションの失敗を示すレコードは、その他のすべてのレコードを outrank します。  
  
    -   2 つまたは複数のレコードには、同じエラー条件について説明します場合、SQLSTATEs 開いてグループ CLI 仕様 (HZ で使用するクラス 03) で定義された outrank SQLSTATEs の ODBC およびドライバーの定義とします。  
  
-   **データ値の No の実装で定義された**No Data 値 (クラス 02) のドライバーの定義を記述する状態レコードがある 2 番目の最高ランク。  
  
-   **警告**警告 (クラス 01) を示す状態レコード最低ランクであります。 2 つまたは複数のレコード SQLSTATEs 開いてグループ CLI 仕様によって定義されているを警告し、同じ警告の状態を記述する場合は、ODBC で定義され、ドライバーの定義についてを outrank します。  
  
## <a name="related-functions"></a>関連する関数  
  
|詳細|参照先|  
|---------------------------|---------|  
|診断データの構造体の複数のフィールドを取得します。|[SQLGetDiagRec 関数](sqlgetdiagrec-function.md)|  
  
## <a name="see-also"></a>参照  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)
