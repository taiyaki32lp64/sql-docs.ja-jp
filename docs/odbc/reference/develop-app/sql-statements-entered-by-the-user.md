---
title: SQL ステートメントが、ユーザーが入力した |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- user-entered SQL statements [ODBC]
- SQL statements [ODBC], constructing
- SQL statements [ODBC], entered by user
ms.assetid: 109af162-93ba-425a-8fe5-49c7dc7cc784
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 78a1653df60b21cde772cbe32a688b3fdef80a42
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68086072"
---
# <a name="sql-statements-entered-by-the-user"></a>ユーザーが入力した SQL ステートメント
よくアド ホック分析を実行するアプリケーションでは、SQL ステートメントを直接入力するユーザーを許可します。 以下に例を示します。  
  
```  
SQLCHAR *     Statement, SqlState[6], Msg[SQL_MAX_MESSAGE_LENGTH];  
SQLSMALLINT   i, MsgLen;  
SQLINTEGER    NativeError;  
SQLRETURN     rc1, rc2;  
  
// Prompt user for SQL statement.  
GetSQLStatement(Statement);  
  
// Execute the statement directly. Because it will be executed only once,  
// do not prepare it.  
rc1 = SQLExecDirect(hstmt, Statement, SQL_NTS);  
  
// Process any errors or returned information.  
if ((rc1 == SQL_ERROR) || rc1 == SQL_SUCCESS_WITH_INFO) {  
   i = 1;  
   while ((rc2 = SQLGetDiagRec(SQL_HANDLE_STMT, hstmt, i, SqlState, &NativeError,  
         Msg, sizeof(Msg), &MsgLen)) != SQL_NO_DATA) {  
      DisplayError(SqlState, NativeError, Msg, MsgLen);  
      i++;  
   }  
}  
```  
  
 この手法はアプリケーションのコーディングを簡略化します。アプリケーションでは、SQL ステートメントを作成しているユーザーに対する、ステートメントの有効性をチェックするデータ ソースに依存しています。 SQL の複雑な作業を適切に公開するグラフィカル ユーザー インターフェイスを記述するため、SQL ステートメントのテキストを入力するユーザーに依頼するだけと、ことをお勧めの代替可能性があります。 ただし、SQL だけでなく、クエリ対象のデータ ソースのスキーマを把握するユーザーが必要です。 一部のアプリケーションは、ユーザーが基本的な SQL ステートメントを作成しが、ユーザーが変更できるテキスト インターフェイスを提供するグラフィカル ユーザー インターフェイスを提供します。
