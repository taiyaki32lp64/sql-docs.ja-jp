---
title: SQLCompleteAsync 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
f1_keywords:
- SQLCompleteAsync
helpviewer_keywords:
- SQLCompleteAsync function [ODBC]
ms.assetid: 1b97c46a-d2e5-4540-8239-9d975e5321c6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5e50e8128bb80b290e7610d9cc846dd3e148e398
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68118629"
---
# <a name="sqlcompleteasync-function"></a>SQLCompleteAsync 関数
**準拠**  
 バージョンが導入されました。ODBC 3.8  
  
 標準への準拠:なし  
  
 **概要**  
 **SQLCompleteAsync**非同期関数のいずれかの通知またはポーリング ベースの処理を使用して完了時に決定するために使用できます。 非同期操作の詳細については、次を参照してください。[非同期実行](../../../odbc/reference/develop-app/asynchronous-execution.md)します。  
  
 **SQLCompleteAsync**は、ODBC ドライバー マネージャーでのみ実装します。  
  
 通知ベースの非同期処理モードで**SQLCompleteAsync**ドライバー マネージャーが通知に使用されるイベント オブジェクトを生成した後に呼び出す必要があります。 **SQLCompleteAsync**完了、非同期処理と非同期関数は、リターン コードが生成されます。  
  
 ポーリング ベースの非同期処理モードで**SQLCompleteAsync**代替は、元の非同期関数呼び出しで引数を指定することがなく、元の非同期関数を呼び出すことです。 **SQLCompleteAsync** ODBC カーソル ライブラリが有効になっているかどうかに関係なく使用できます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLCompleteAsync(  
      SQLSMALLINT HandleType,  
      SQLHANDLE   Handle,  
      RETCODE *   AsyncRetCodePtr);  
```  
  
## <a name="arguments"></a>引数  
 *HandleType*  
 [入力]非同期を完了するためのハンドルの型を処理します。 有効な値は sql_handle_dbc としてまたは sql_handle_stmt として。  
  
 *Handle*  
 [入力]非同期を完了するためのハンドルを処理します。 場合*処理*で指定された型の有効なハンドルではありません*HandleType*、 **SQLCompleteAsync** SQL_INVALID_HANDLE が返されます。  
  
 場合*処理*で指定された型の有効なハンドルではありません*HandleType*、 **SQLCompleteAsync** SQL_INVALID_HANDLE が返されます。  
  
 *AsyncRetCodePtr*  
 [出力]非同期 API のリターン コードを格納するバッファーへのポインター。 場合*AsyncRetCodePtr*が null の場合、 **SQLCompleteAsync** SQL_ERROR を返します。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_ERROR、SQL_NO_DATA、または SQL_INVALID_HANDLE します。  
  
## <a name="diagnostics"></a>診断  
 場合**SQLCompleteAsync**返します SQL_SUCCESS、アプリケーションは、によって指し示されるバッファーから非同期関数のリターン コードを取得する必要があります*AsyncRetCodePtr*します。 関連付けられている SQLSTATE、存在する場合、取得できますを呼び出して**SQLGetDiagRec**で、 *HandleType* sql_handle_stmt としてのステートメント ハンドルまたは*HandleType* sql _ のHANDLE_DBC との接続を処理します。 これらの診断レコードがこれではない非同期の関数に関連付けられた**SQLCompleteAsync**関数。  
  
 **SQLCompleteAsync**ことを示す SQL_SUCCESS 以外のコードを返します**SQLCompleteAsync**は正しく呼び出されません。 **SQLCompleteAsync**任意の診断レコードをここで投稿されます。 リターン コードは次のとおりです。  
  
-   SQL_INVALID_HANDLE:によって示されるハンドル*HandleType*と*処理*有効なハンドルではありません。  
  
-   SQL_ERROR:*AsyncRetCodePtr*が NULL またはハンドルの非同期処理が有効になっていません。  
  
-   SQL_NO_DATA:通知モードでは、非同期の操作が進行中またはドライバー マネージャーが、アプリケーションが通知されません。 ポーリング モードで、非同期操作は進行中です。  
  
## <a name="comments"></a>コメント  
 ポーリング ベースの非同期処理モードで*AsyncRetCodePtr* SQL_STILL_EXECUTING がありますと**SQLCompleteAsync** SQL_SUCCESS を返します。 アプリケーションはまでポーリングを保持する必要があります*AsyncRetCodePtr* SQL_STILL_EXECUTING ではありません。 通知ベースの非同期処理モードで*AsyncRetCodePtr* SQL_STILL_EXECUTING ものではありません。  
  
## <a name="see-also"></a>参照  
 [非同期実行 (ポーリング メソッド)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
