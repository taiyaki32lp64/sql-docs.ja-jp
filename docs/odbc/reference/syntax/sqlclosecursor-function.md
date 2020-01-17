---
title: Sqlcloセキュリティー関数 |Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLCloseCursor
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLCloseCursor
helpviewer_keywords:
- SQLCloseCursor function [ODBC]
ms.assetid: 05b0a054-e28d-4e16-b5b0-07418486b372
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ef336a4deb734c0e44f9c15ae7f9faf0dcb32d93
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/19/2019
ms.locfileid: "68343147"
---
# <a name="sqlclosecursor-function"></a>SQLCloseCursor 関数
**互換性**  
 導入されたバージョン:ODBC 3.0 標準準拠:ISO 92  
  
 **まとめ**  
 **Sqlcloは**、ステートメントで開かれているカーソルを閉じ、保留中の結果を破棄します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLCloseCursor(  
     SQLHSTMT     StatementHandle);  
```  
  
## <a name="arguments"></a>引数  
 *StatementHandle*  
 代入ステートメントハンドル。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR、または SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診断  
 **Sqlcloに**よって SQL_ERROR または SQL_SUCCESS_WITH_INFO が返される場合、SQL_HANDLE_STMT の*Handletype*と*StatementHandle*の*ハンドル*を指定して**SQLGetDiagRec**を呼び出すことによって、関連付けられた SQLSTATE 値を取得できます。 次の表に、 **Sqlcloに**よって一般的に返される SQLSTATE 値の一覧を示し、この関数のコンテキストでそれぞれについて説明します。"(DM)" という表記は、ドライバーマネージャーによって返される SQLSTATEs の説明の前にあります。 特に記載がない限り、各 SQLSTATE 値に関連付けられているリターンコードは SQL_ERROR です。  
  
|SQLSTATE|[エラー]|説明|  
|--------------|-----------|-----------------|  
|01000|一般警告|ドライバー固有の情報メッセージ。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|24000|カーソル状態が無効|*StatementHandle*で開かれているカーソルはありません。 (これは、ODBC 3 によってのみ返されます。*x*ドライバー。)|  
|HY000|一般エラー|特定の SQLSTATE がなく、実装固有の SQLSTATE が定義されていないエラーが発生しました。 Messagetext バッファーの**SQLGetDiagRec によっ**て返されるエラーメッセージには、エラーとその原因が記述されています。  *\**|  
|HY001|メモリ割り当てエラー|ドライバーは、関数の実行または完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY010|関数のシーケンスエラー|(DM) 非同期的に実行する関数が、 *StatementHandle*に関連付けられた接続ハンドルに対して呼び出されましたが、この関数が呼び出されたときにまだ実行されていました。<br /><br /> (DM) 非同期的に実行する関数が*StatementHandle*に対して呼び出されましたが、この関数が呼び出されたときにまだ実行されていました。<br /><br /> (DM) **Sqlexecute**、 **SQLExecDirect**、 **sqlbulkoperations**、または**SQLSetPos**が*StatementHandle*に対して呼び出され、SQL_NEED_DATA が返されました。 この関数は、実行時データのすべてのパラメーターまたは列に対してデータが送信される前に呼び出されました。|  
|HY013|メモリ管理エラー|基になるメモリオブジェクトにアクセスできなかったため、関数呼び出しを処理できませんでした。メモリ不足の状態が原因である可能性があります。|  
|HY117|トランザクションの状態が不明なため、接続が中断されました。 切断と読み取り専用の機能のみが許可されます。|(DM) 中断状態の詳細については、「 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)」を参照してください。|  
|HYT01|接続タイムアウトの期限が切れました|データソースが要求に応答する前に、接続のタイムアウト期間が経過しました。 接続タイムアウト期間は、 **SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT によって設定されます。|  
|IM001|ドライバーはこの機能をサポートしていません|(DM) *StatementHandle*に関連付けられているドライバーでは、関数はサポートされていません。|  
  
## <a name="comments"></a>コメント  
 カーソルが開いていない場合、 **Sqlcloが**24000 返されます。 **Sqlcloを**呼び出すことは、SQL_CLOSE オプションを使用して**SQLFreeStmt**を呼び出すことと同じです。ただし、ステートメント **でカーソルが開かれていない場合、SQLFreeStmt with SQL_CLOSE はアプリケーションに影響しません。Sqlcloは**、SQLSTATE 24000 (無効なカーソル状態) を返します。  
  
> [!NOTE]  
>  ODBC 3 の場合。*x*アプリケーションが ODBC 2 で動作する。*x*ドライバーは**sqlcloを**呼び出します。カーソルが開いていない場合、SQLSTATE 24000 (無効なカーソル状態) は返されません。これは、 ドライバーマネージャーが**sqlcloSQLFreeStmt**を SQL_CLOSE にマップするためです。  
  
 詳細については、「[カーソルを閉じる](../../../odbc/reference/develop-app/closing-the-cursor.md)」を参照してください。  
  
## <a name="code-example"></a>コード例  
 「 [SQLBrowseConnect 関数](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)と[SQLConnect 関数](../../../odbc/reference/syntax/sqlconnect-function.md)」を参照してください。  
  
## <a name="related-functions"></a>関連する関数  
  
|詳細|参照先|  
|---------------------------|---------|  
|ステートメント処理の取り消し|[SQLCancel 関数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|ハンドルの解放|[SQLFreeHandle 関数](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|複数の結果セットの処理|[SQLMoreResults 関数](../../../odbc/reference/syntax/sqlmoreresults-function.md)|  
  
## <a name="see-also"></a>参照  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)
