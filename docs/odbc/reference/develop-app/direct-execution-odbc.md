---
title: 直接実行 ODBC |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], direct execution
- direct execution [ODBC]
- SQL statements [ODBC], executing
ms.assetid: dd00a535-b136-494f-913b-410838e3de7e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 72d9222be541a8d41b5b9935ac7cbbcfde4da19c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68039797"
---
# <a name="direct-execution-odbc"></a>直接実行 (ODBC)
直接実行は、ステートメントを実行する最も簡単な方法です。 実行するため、ステートメントが送信されると、データ ソース アクセス プランにコンパイルし、しアクセス計画を実行します。  
  
 直接実行は、ビルドおよび実行時にステートメントを実行する汎用アプリケーションで通常使用されます。 たとえば、次のコードでは、SQL ステートメントを構築し、1 回実行します。  
  
```  
SQLCHAR *SQLStatement;  
  
// Build an SQL statement.  
BuildStatement(SQLStatement);  
  
// Execute the statement.  
SQLExecDirect(hstmt, SQLStatement, SQL_NTS);  
```  
  
 直接実行は 1 回実行されるステートメントに最適です。 その主な欠点は、それが実行されるたびに、SQL ステートメントを解析します。 さらに、アプリケーションがステートメントによって作成された、(ある場合) まで、ステートメントが実行した後、結果セットに関する情報を取得できません。ステートメントが準備され、別の 2 つの手順で実行された場合、可能です。  
  
 ステートメントを実行するには、直接アプリケーションを実行、次の操作します。  
  
1.  パラメーターの値を設定します。 詳細については、次を参照してください。[ステートメント パラメーター](../../../odbc/reference/develop-app/statement-parameters.md)、このセクションで後述します。  
  
2.  呼び出し**SQLExecDirect**し、SQL ステートメントを含む文字列を渡します。  
  
3.  ときに**SQLExecDirect**を呼び出すと、ドライバー。  
  
    -   ステートメントを解析することがなく、データ ソースの SQL 文法を使用する SQL ステートメントを変更します。これで説明されているエスケープ シーケンスを置き換えるが含まれています。 [odbc エスケープ シーケンス](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md)します。 アプリケーションが呼び出すことによって、SQL ステートメントの変更されたフォームを取得できます**SQLNativeSql**します。 SQL_ATTR_NOSCAN ステートメントの属性が設定されている場合、エスケープ シーケンスは置き換えられません。  
  
    -   現在のパラメーター値を取得し、必要に応じてそれらを変換します。 詳細については、次を参照してください。[ステートメント パラメーター](../../../odbc/reference/develop-app/statement-parameters.md)、このセクションで後述します。  
  
    -   ステートメントと変換されたパラメーターの値を実行するためのデータ ソースに送信します。  
  
    -   すべてのエラーを返します。 シーケンス処理または SQLSTATE 24000 など状態診断 (無効なカーソル状態)、SQLSTATE 42000 (構文エラーまたはアクセス違反、) などの構文エラーとセマンティック エラー SQLSTATE 42S02 などが含まれます (ベース テーブルまたはビューが見つかりません)。
