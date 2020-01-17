---
title: SQLDataSources 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLDataSources
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLDataSources
helpviewer_keywords:
- SQLDataSources function [ODBC]
ms.assetid: 3f63b1b4-e70e-44cd-96c6-6878d50d0117
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 28fcf56293516937455afc387a8d478734f5b006
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68121378"
---
# <a name="sqldatasources-function"></a>SQLDataSources 関数
**準拠**  
 バージョンが導入されました。ODBC 1.0 規格に準拠します。ISO 92  
  
 **まとめ**  
 **SQLDataSources**データ ソースに関する情報を返します。 この関数は、ドライバー マネージャーによってのみ実装されます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLDataSources(  
     SQLHENV          EnvironmentHandle,  
     SQLUSMALLINT     Direction,  
     SQLCHAR *        ServerName,  
     SQLSMALLINT      BufferLength1,  
     SQLSMALLINT *    NameLength1Ptr,  
     SQLCHAR *        Description,  
     SQLSMALLINT      BufferLength2,  
     SQLSMALLINT *    NameLength2Ptr);  
```  
  
## <a name="arguments"></a>引数  
 *EnvironmentHandle*  
 [入力]環境ハンドル。  
  
 *[方向]*  
 [入力]データ ソースをドライバー マネージャーに関する情報を返しますを決定します。 次の値をとります。  
  
 SQL_FETCH_NEXT (一覧で、[次へ] のデータ ソース名を取得) を SQL_FETCH_FIRST (リストの先頭からのフェッチ) を (最初のフェッチのユーザーに DSN)、SQL_FETCH_FIRST_USER または SQL_FETCH_FIRST_SYSTEM (最初のシステム DSN のフェッチ) にします。  
  
 ときに*方向*SQL_FETCH_FIRST、後続の呼び出しに設定されている**SQLDataSources**で*方向*リターン ユーザーとシステム Dsn を前方に設定します。 ときに*方向*SQL_FETCH_FIRST_USER、後続のすべての呼び出しに設定されている**SQLDataSources**で*方向*リターン ユーザー Dsn だけを前方に設定します。 ときに*方向*SQL_FETCH_FIRST_SYSTEM、後続のすべての呼び出しに設定されている**SQLDataSources**で*方向*リターン システム Dsn だけを前方に設定します。  
  
 *ServerName*  
 [出力]データ ソース名を返すバッファーへのポインター。  
  
 場合*ServerName*が null の場合、 *NameLength1Ptr*はまだ文字 (文字データの null 終端文字を除く) の合計数を返しますが指すバッファーに返される使用可能な*ServerName*します。  
  
 *BufferLength1*  
 [入力]長さ、**ServerName*文字で、バッファー; SQL_MAX_DSN_LENGTH と null 終端文字以内であるこの必要はありません。  
  
 *NameLength1Ptr*  
 [出力]文字 (null 終了文字を除く) の合計数を返すバッファーへのポインターで返される使用可能な\* *ServerName*します。 返すに使用できる文字数がより大きいかに等しい場合*BufferLength1*、内のデータ ソース名\* *ServerName*に切り捨てられます*BufferLength1* null 終了文字の長さマイナスです。  
  
 *[説明]*  
 [出力]データ ソースに関連付けられているドライバーの説明を返すバッファーへのポインター。 たとえば、dBASE ファイルまたは SQL Server。  
  
 場合*説明*が null の場合、 *NameLength2Ptr*はまだ文字 (文字データの null 終端文字を除く) の合計数を返しますが指すバッファーに返される使用可能な*説明*します。  
  
 *BufferLength2*  
 [入力]文字の長さ、**説明*バッファー。  
  
 *NameLength2Ptr*  
 [出力]文字 (null 終了文字を除く) の合計数を返すバッファーへのポインターで返される使用可能な\**説明*します。 返すに使用できる文字数がより大きいかに等しい場合*BufferLength2*、ドライバーの説明で\**説明*に切り捨てられます*BufferLength2* null 終了文字の長さマイナスです。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_NO_DATA、SQL_ERROR、または SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診断  
 ときに**SQLDataSources** SQL_ERROR または SQL_SUCCESS_WITH_INFO のいずれかを返します呼び出すことによって、関連付けられた SQLSTATE 値を取得できる**SQLGetDiagRec**で、 *HandleType*sql_handle_env としての*処理*の*EnvironmentHandle*します。 次の表に、によって返される通常の SQLSTATE 値**SQLDataSources** ; この関数のコンテキストでそれぞれについて説明しますと表記"(DM)"の前にドライバー マネージャーによって返されるについての説明。 SQLSTATE 値ごとに関連付けられているリターン コードは明記しない限り、SQL_ERROR です。  
  
|SQLSTATE|[エラー]|説明|  
|--------------|-----------|-----------------|  
|01000|一般的な警告|(DM) ドライバー マネージャーに固有の情報メッセージ。 (関数は、SQL_SUCCESS_WITH_INFO を返します)。|  
|01004|文字列データで、右側が切り捨てられました|(DM) バッファー \* *ServerName*完全なデータ ソース名を取得するのに十分な大きさがありません。 そのため、名前が切り捨てられました。 全体のデータ ソース名の長さが返される\* *NameLength1Ptr*します。 (関数は、SQL_SUCCESS_WITH_INFO を返します)。<br /><br /> (DM) バッファー \**説明*を完全なドライバーの説明を返すのに十分な大きさがありません。 そのため、説明が切り捨てられました。 切り詰められていないデータ ソースの説明の長さが返される **NameLength2Ptr*します。 (関数は、SQL_SUCCESS_WITH_INFO を返します)。|  
|HY000|一般的なエラー|(DM) エラーが発生する固有の SQLSTATE がなかったし、対象の実装に固有の SQLSTATE が定義されていません。 によって返されるエラー メッセージ**SQLGetDiagRec**で、  *\*MessageText*バッファーは、エラーとその原因について説明します。|  
|HY001|メモリの割り当てエラー|(DM)、ドライバー マネージャーは、実行または関数の完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY010|関数のシーケンス エラー|(DM) **SQLExecute**、 **SQLExecDirect**、または**SQLMoreResults**に対して呼び出された、 *StatementHandle* SQL_PARAM_DATA_ を返されます。ご利用いただけます。 ストリームのすべてのパラメーターのデータが取得される前に、この関数が呼び出されました。|  
|HY013|メモリ管理エラー|基になるメモリ オブジェクトにアクセスできませんでした、場合によってメモリ不足が原因であるために、関数呼び出しを処理できませんでした。|  
|HY090|文字列またはバッファーの長さが無効です。|引数に指定された (DM) 値*BufferLength1*が 0 未満でした。<br /><br /> 引数に指定された (DM) 値*BufferLength2*が 0 未満でした。|  
|HY103|無効な取得コード|引数に指定された値 (DM)*方向*SQL_FETCH_FIRST、SQL_FETCH_FIRST_USER、SQL_FETCH_FIRST_SYSTEM、または SQL_FETCH_NEXT でした。|  
|HY117|不明なトランザクションの状態のため、接続が中断されます。 のみを切断して、読み取り専用の関数が許可されます。|(DM) 中断状態の詳細については、次を参照してください。 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)します。|  
  
## <a name="comments"></a>コメント  
 **SQLDataSources**は実装されてドライバー マネージャーでの特定のドライバーの標準への準拠に関係なくすべてのドライバーでサポートされています。  
  
 アプリケーションが呼び出すことができます**SQLDataSources**すべてのデータ ソース名を取得する回数します。 ドライバー マネージャーは、システム情報からこの情報を取得します。 ない多くのデータ ソース名が存在する場合、ドライバー マネージャーは SQL_NO_DATA を返します。 場合**SQLDataSources**は、SQL_NO_DATA が返された後、最初のデータ ソース名が返されます。 すぐに SQL_FETCH_NEXT で呼び出されます。 アプリケーションがによって返される情報を使用する方法については**SQLDataSources**を参照してください[データ ソースまたはドライバーを選択する](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)します。  
  
 SQL_FETCH_NEXT が渡された場合**SQLDataSources**初めて呼び出されると、最初のデータ ソースの名前を返します。  
  
 ドライバーは、データ ソース名を実際のデータ ソースにマップする方法を決定します。  
  
## <a name="related-functions"></a>関連する関数  
  
|詳細|参照先|  
|---------------------------|---------|  
|検出とデータ ソースに接続するために必要な値を一覧表示します。|[SQLBrowseConnect 関数](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|  
|データ ソースへの接続|[SQLConnect 関数](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|接続文字列またはダイアログ ボックスを使用してデータ ソースへの接続|[SQLDriverConnect 関数](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|ドライバーの説明と属性を返す|[SQLDrivers 関数](../../../odbc/reference/syntax/sqldrivers-function.md)|  
  
## <a name="see-also"></a>参照  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)
