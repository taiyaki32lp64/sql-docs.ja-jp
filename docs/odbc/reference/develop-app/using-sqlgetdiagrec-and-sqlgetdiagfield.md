---
title: SQLGetDiagRec および SQLGetDiagField の使用 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], SqlGetDiagField
- SQLGetDiagField function [ODBC], and SQLGetDiagRec
- SQLGetDiagRec function [ODBC], and SQLGetDiagField
- diagnostic information [ODBC], SqlGetDiagRec
- retrieving diagnostic information [ODBC]
ms.assetid: 4f486bb1-fad8-4064-ac9d-61f2de85b68b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 23b7539c32b6cb675f8616d9b8ec9db89be1208b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68022153"
---
# <a name="using-sqlgetdiagrec-and-sqlgetdiagfield"></a>SQLGetDiagRec および SQLGetDiagField の使用
アプリケーション呼び出し**SQLGetDiagRec**または**SQLGetDiagField**診断情報を取得します。 これらの関数は、環境、接続、ステートメント、または記述子ハンドルをそのまま使用し、最後にそのハンドルを使用した関数から診断を返します。 特定のハンドルをログに記録する診断は、そのハンドルを使用して新しい関数が呼び出されたときに破棄されます。 関数には、複数の診断レコードが返されると複数回; に、アプリケーション呼び出しがこれらの関数状態レコードの合計数が呼び出すことによって取得**SQLGetDiagField** SQL_DIAG_NUMBER オプションを使用してヘッダー レコード (レコード 0)。  
  
 アプリケーションが呼び出すことで個々 の診断フィールドを取得**SQLGetDiagField**し取得するフィールドを指定します。 特定の診断フィールドには、特定の種類のハンドルのすべての意味はありません。 診断フィールドとその意味の一覧は、次を参照してください。、 [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)関数の説明。  
  
 アプリケーションを呼び出す、SQLSTATE、ネイティブ エラー コード、および 1 回の呼び出しで診断メッセージを取得する**SQLGetDiagRec**;**SQLGetDiagRec**ヘッダー レコードから情報を取得するのには使用できません。  
  
 たとえば、次のコードでは、SQL ステートメントのユーザーに求め、それを実行します。 呼び出すすべての診断情報が返された場合**SQLGetDiagField**状態レコードの数を取得し、 **SQLGetDiagRec**ものから、SQLSTATE、ネイティブ エラー コード、および診断メッセージを取得するにはレコードがあります。  
  
```  
SQLCHAR       SqlState[6], SQLStmt[100], Msg[SQL_MAX_MESSAGE_LENGTH];  
SQLINTEGER    NativeError;  
SQLSMALLINT   i, MsgLen;  
SQLRETURN     rc1, rc2;  
SQLHSTMT      hstmt;  
  
// Prompt the user for an SQL statement.  
GetSQLStmt(SQLStmt);  
  
// Execute the SQL statement and return any errors or warnings.  
rc1 = SQLExecDirect(hstmt, SQLStmt, SQL_NTS);  
if ((rc1 == SQL_SUCCESS_WITH_INFO) || (rc1 == SQL_ERROR)) {
   SQLLEN numRecs = 0;
   SQLGetDiagField(SQL_HANDLE_STMT, hstmt, 0, SQL_DIAG_NUMBER, &numRecs, 0, 0);
   // Get the status records.
   i = 1;  
   while (i <= numRecs && (rc2 = SQLGetDiagRec(SQL_HANDLE_STMT, hstmt, i, SqlState, &NativeError,  
            Msg, sizeof(Msg), &MsgLen)) != SQL_NO_DATA) {  
      DisplayError(SqlState,NativeError,Msg,MsgLen);  
      i++;  
   }  
}  
  
if ((rc1 == SQL_SUCCESS) || (rc1 == SQL_SUCCESS_WITH_INFO)) {  
   // Process statement results, if any.  
}  
```
