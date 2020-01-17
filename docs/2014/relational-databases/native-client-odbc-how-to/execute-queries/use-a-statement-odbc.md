---
title: ステートメントの使用 (ODBC) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- statements [ODBC]
ms.assetid: f7573f8f-6f21-4e03-8dd5-a5f2ea4878cc
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 842e862dff7eca85a05df0222989c6ee6390ab89
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63200329"
---
# <a name="use-a-statement-odbc"></a>ステートメントの使用 (ODBC)
    
### <a name="to-use-a-statement"></a>ステートメントを使用するには  
  
1.  *HandleType* を SQL_HANDLE_STMT として [SQLAllocHandle](https://go.microsoft.com/fwlink/?LinkId=58396) を呼び出し、ステートメント ハンドルを割り当てます。  
  
2.  また、[SQLSetStmtAttr](../../native-client-odbc-api/sqlsetstmtattr.md) を呼び出してステートメント オプションを設定するか、[SQLGetStmtAttr](../../native-client-odbc-api/sqlgetstmtattr.md) を呼び出してステートメント属性を取得することもできます。  
  
     サーバー カーソルを使用するには、カーソルの属性を既定値以外の値に設定する必要があります。  
  
3.  また、ステートメントを複数回実行する場合は、[SQLPrepare 関数](https://go.microsoft.com/fwlink/?LinkId=59360)を使用して実行するステートメントを準備します。  
  
4.  ステートメントにバインドされたパラメーター マーカーが含まれている場合は、必要に応じて、[SQLBindParameter](../../native-client-odbc-api/sqlbindparameter.md) を使用してパラメーター マーカーをプログラム変数にバインドします。 ステートメントが準備されている場合は、[SQLNumParams](https://go.microsoft.com/fwlink/?LinkId=58404) および [SQLDescribeParam](../../native-client-odbc-api/sqldescribeparam.md) を呼び出して、パラメーターの数と特性を検索できます。  
  
5.  SQLExecDirect を使用してステートメントを直接実行します。  
  
     \- - または -  
  
     ステートメントが準備されている場合は、[SQLExecute](https://go.microsoft.com/fwlink/?LinkId=58400) を使用してそのステートメントを複数回実行します。  
  
     \- - または -  
  
     カタログ関数を呼び出すと、結果が返されます。  
  
6.  結果セット列をプログラム変数にバインドするか、[SQLGetData](../../native-client-odbc-api/sqlgetdata.md) を使用して結果セット列からプログラム変数にデータを移動するか、あるいはこれらの 2 つの方法を組み合わせて結果を処理します。  
  
     ステートメントの結果セットを一度に 1 行ずつフェッチします。  
  
     \- - または -  
  
     ブロック カーソルを使用して一度に複数行の結果セットをフェッチします。  
  
     \- - または -  
  
     [SQLRowCount](../../native-client-odbc-api/sqlrowcount.md) を呼び出して、INSERT、UPDATE、または DELETE ステートメントの影響を受ける行数を確認します。  
  
     SQL ステートメントに複数の結果セットが含まれている可能性がある場合は、各結果セットの最後に [SQLMoreResults](../../native-client-odbc-api/sqlmoreresults.md) を呼び出して、処理する追加の結果セットがあるかどうかを確認します。  
  
7.  結果が処理されたら、ステートメント ハンドルで新しいステートメントを実行できるように、次のアクションが必要な場合があります。  
  
    -   SQL_NO_DATA が返されるまで [SQLMoreResults](../../native-client-odbc-api/sqlmoreresults.md) を呼び出さなかった場合は、[SQLCloseCursor](../../native-client-odbc-api/sqlclosecursor.md) を呼び出してカーソルを閉じます。  
  
    -   パラメーター マーカーをプログラム変数にバインドした場合は、*Option* を SQL_RESET_PARAMS に設定して [SQLFreeStmt](../../native-client-odbc-api/sqlfreestmt.md) を呼び出し、バインドされたパラメーターを解放します。  
  
    -   結果セット列をプログラム変数にバインドした場合は、*Option* を SQL_UNBIND に設定して [SQLFreeStmt](../../native-client-odbc-api/sqlfreestmt.md) を呼び出し、バインドされた列を解放します。  
  
    -   ステートメント ハンドルを再利用するには、手順 2. に進みます。  
  
8.  *HandleType* を SQL_HANDLE_STMT として [SQLFreeHandle](../../native-client-odbc-api/sqlfreehandle.md) を呼び出し、ステートメント ハンドルを解放します。  
  
## <a name="see-also"></a>参照  
 [クエリを実行方法に関するトピック&#40;ODBC&#41;](executing-queries-how-to-topics-odbc.md)  
  
  
