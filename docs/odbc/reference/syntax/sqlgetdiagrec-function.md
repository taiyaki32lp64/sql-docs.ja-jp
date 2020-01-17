---
title: SQLGetDiagRec 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetDiagRec
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetDiagRec
helpviewer_keywords:
- SQLGetDiagRec function [ODBC]
ms.assetid: ebdbac93-3d68-438f-8416-ef1f08e04269
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c404cbb1f29adbdcb49ef6bed8bb57a047f64f3b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67911315"
---
# <a name="sqlgetdiagrec-function"></a>SQLGetDiagRec 関数
**準拠**  
 バージョンが導入されました。ODBC 3.0 規格に準拠します。ISO 92  
  
 **まとめ**  
 **SQLGetDiagRec**エラー、警告、およびステータス情報を含む診断レコードの複数のフィールドの現在の値を返します。 異なり**SQLGetDiagField**、呼び出しごとに 1 つの診断フィールドを返す**SQLGetDiagRec**いくつかのよく使用される、SQLSTATE、ネイティブ エラー コードを含む、診断レコードのフィールドを返しますと診断メッセージのテキスト。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLGetDiagRec(  
     SQLSMALLINT     HandleType,  
     SQLHANDLE       Handle,  
     SQLSMALLINT     RecNumber,  
     SQLCHAR *       SQLState,  
     SQLINTEGER *    NativeErrorPtr,  
     SQLCHAR *       MessageText,  
     SQLSMALLINT     BufferLength,  
     SQLSMALLINT *   TextLengthPtr);  
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
 [入力]アプリケーションが情報をシークする元の状態レコードを示します。 状態レコードは、1 から番号が付けられます。  
  
 *SQLState*  
 [出力]診断レコードの 5 文字の SQLSTATE コード (および終端の NULL) を返すバッファーへのポインター *RecNumber*します。 最初の 2 つの文字は、クラスを示します。次の 3 つは、サブクラスを示します。 この情報は、SQL_DIAG_SQLSTATE 診断フィールドに含まれます。 詳細については、次を参照してください。 [SQLSTATEs](../../../odbc/reference/develop-app/sqlstates.md)します。  
  
 *NativeErrorPtr*  
 [出力]データ ソースに固有のネイティブ エラー コードを返すバッファーへのポインター。 この情報は、SQL_DIAG_NATIVE 診断フィールドに含まれます。  
  
 *[MessageText]*  
 [出力]診断メッセージのテキスト文字列を返すバッファーへのポインター。 この情報は、SQL_DIAG_MESSAGE_TEXT 診断フィールドに含まれます。 文字列の形式では、次を参照してください。[診断メッセージ](../../../odbc/reference/develop-app/diagnostic-messages.md)します。  
  
 場合*MessageText*が null の場合、 *TextLengthPtr*はまだ文字 (文字データの null 終端文字を除く) の合計数を返しますが指すバッファーに返される使用可能な*MessageText*します。  
  
 *BufferLength*  
 [入力]長さ、**MessageText*文字バッファー。 診断メッセージのテキストの最大長はありません。  
  
 *TextLengthPtr*  
 [出力]文字 (null 終端文字のために必要な文字の数を除く) の合計数を返すバッファーへのポインターで返される使用可能な *\*MessageText*します。 返される使用できる文字数がより大きい場合*BufferLength*、診断メッセージのテキストで *\*MessageText*に切り捨てられます*BufferLength* null 終了文字の長さマイナスです。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR、または SQL_INVALID_HANDLE します。  
  
## <a name="diagnostics"></a>診断  
 **SQLGetDiagRec**自体の診断レコードは通知されません。 次の戻り値を使用して、独自の実行の結果を報告します。  
  
-   SQL_SUCCESS:関数には、診断情報が正常に返されます。  
  
-   SQL_SUCCESS_WITH_INFO:\* *MessageText*バッファーが小さすぎるため、要求された診断メッセージを保持します。 診断レコードは生成されませんでした。 切り捨てが発生したことは、アプリケーションを比較する必要がありますを決定する*BufferLength*実際に記述されている、使用可能なバイト数へ **StringLengthPtr*します。  
  
-   SQL_INVALID_HANDLE:によって示されるハンドル*HandleType*と*処理*が有効なハンドル。  
  
-   SQL_ERROR:次のいずれかが発生しました。  
  
    -   *RecNumber*が負または 0。  
  
    -   *BufferLength* 0 未満でした。  
  
    -   非同期通知を使用する場合、ハンドルに対して非同期操作は完了しませんでした。  
  
-   SQL_NO_DATA:*RecNumber*診断レコードで指定したハンドルに存在していた数よりも大きかった*を処理します。* 関数が SQL_NO_DATA を任意の正のも返します*RecNumber*に対する診断レコードがない場合*処理*します。  
  
## <a name="comments"></a>コメント  
 アプリケーションを呼び出す通常**SQLGetDiagRec** SQL_ERROR または sql_success_with_info が以前の ODBC 関数呼び出しが返される場合。 ただし、任意の ODBC 関数では、それが呼び出されるたびに 0 個以上の診断レコードを投稿できます、ため、アプリケーションを呼び出せる**SQLGetDiagRec**任意の ODBC 関数呼び出しの後にします。 アプリケーションが呼び出すことができます**SQLGetDiagRec**診断データの構造の一部またはすべてのレコードを返すを複数回です。 ODBC では、いつでも格納できる診断レコードの数に制限はありません。  
  
 **SQLGetDiagRec**診断データの構造体のヘッダーからフィールドを返すには使用できません。 (、 *RecNumber*引数は、0 より大きくなければなりません)。アプリケーションを呼び出す必要があります**SQLGetDiagField**この目的のためです。  
  
 **SQLGetDiagRec**最も最近の指定したハンドルに関連付けられている診断情報だけを取得、*処理*引数。 アプリケーションが別の ODBC 関数を呼び出す場合を除く**SQLGetDiagRec**、 **SQLGetDiagField**、または**SQLError**、前の呼び出しから診断情報がすべて、同じハンドルが失われます。  
  
 アプリケーションをスキャンできます診断のすべてのレコードをループしてインクリメント*RecNumber*限り**SQLGetDiagRec** SQL_SUCCESS を返します。 呼び出す**SQLGetDiagRec**ヘッダーとレコードのフィールドを非破壊的なは。 アプリケーションを呼び出して**SQLGetDiagRec**を除くその他の関数の限りレコードからフィールドを取得するには、後でもう一度**SQLGetDiagRec**、 **SQLGetDiagField**、または**SQLError**がそれまでの間で呼び出されました。 呼び出すことによって、アプリケーションで使用できる診断レコードの合計数のカウントが取得できますも**SQLGetDiagField** SQL_DIAG_NUMBER のフィールドと、呼び出し元の値を取得する**SQLGetDiagRec**その回数だけです。  
  
 診断データの構造体のフィールドの説明は、次を参照してください。 [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)します。 詳細については、次を参照してください。[を使用して SQLGetDiagRec および SQLGetDiagField](../../../odbc/reference/develop-app/using-sqlgetdiagrec-and-sqlgetdiagfield.md)と[実装 SQLGetDiagRec および SQLGetDiagField](../../../odbc/reference/develop-app/implementing-sqlgetdiagrec-and-sqlgetdiagfield.md)します。  
  
 HY010 が生成されますが、非同期的に実行されているものと異なる API を呼び出す「関数のシーケンス エラーです」。 ただし、非同期操作が完了する前に、エラー レコードを取得できません。  
  
## <a name="handletype-argument"></a>HandleType 引数  
 各ハンドル型には、関連付けられている診断情報を持つことができます。 *HandleType*引数のハンドル型を示します、*処理*引数。  
  
 いくつかのヘッダーとレコード フィールドは、環境、接続、ステートメント、および記述子ハンドル返されることはできません。 フィールドが適用されていないそれらのハンドルが「ヘッダー フィールド」と「レコードのフィールド」のセクションで示される[SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)します。  
  
 呼び出し**SQLGetDiagRec**場合 SQL_INVALID_HANDLE が返さ*HandleType*は SQL_HANDLE_SENV で、共有環境ハンドルを表します。 ただし場合、 *HandleType* sql_handle_env としてでは、*処理*共有または共有されていない環境ハンドルのいずれかにすることができます。  
  
## <a name="related-functions"></a>関連する関数  
  
|詳細|参照先|  
|---------------------------|---------|  
|診断レコードのフィールドまたは診断のヘッダーのフィールドを取得します。|[SQLGetDiagField 関数](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)|  
  
## <a name="see-also"></a>参照  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)   
 [ODBC のサンプル プログラム](../../../odbc/reference/sample-odbc-program.md)
