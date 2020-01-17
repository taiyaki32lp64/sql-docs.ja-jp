---
title: ステートメントを使用する (ODBC) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- statements [ODBC]
ms.assetid: f7573f8f-6f21-4e03-8dd5-a5f2ea4878cc
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3624253fa70ca12078a981d694c5e50b5030ce01
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73781177"
---
# <a name="use-a-statement-odbc"></a>ステートメントの使用 (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

    
### <a name="to-use-a-statement"></a>ステートメントを使用するには  
  
1.  [HandleType](https://go.microsoft.com/fwlink/?LinkId=58396) を SQL_HANDLE_STMT として *SQLAllocHandle* を呼び出し、ステートメント ハンドルを割り当てます。  
  
2.  また、[SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) を呼び出してステートメント オプションを設定するか、[SQLGetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlgetstmtattr.md) を呼び出してステートメント属性を取得することもできます。  
  
     サーバー カーソルを使用するには、カーソルの属性を既定値以外の値に設定する必要があります。  
  
3.  また、ステートメントを複数回実行する場合は、[SQLPrepare 関数](https://go.microsoft.com/fwlink/?LinkId=59360)を使用して実行するステートメントを準備します。  
  
4.  ステートメントにバインドされたパラメーター マーカーが含まれている場合は、必要に応じて、[SQLBindParameter](../../../relational-databases/native-client-odbc-api/sqlbindparameter.md) を使用してパラメーター マーカーをプログラム変数にバインドします。 ステートメントが準備されている場合は、[SQLNumParams](https://go.microsoft.com/fwlink/?LinkId=58404) および [SQLDescribeParam](../../../relational-databases/native-client-odbc-api/sqldescribeparam.md) を呼び出して、パラメーターの数と特性を検索できます。  
  
5.  SQLExecDirect を使用してステートメントを直接実行します。  
  
     \- - または -  
  
     ステートメントが準備されている場合は、[SQLExecute](https://go.microsoft.com/fwlink/?LinkId=58400) を使用してそのステートメントを複数回実行します。  
  
     \- - または -  
  
     カタログ関数を呼び出すと、結果が返されます。  
  
6.  結果セット列をプログラム変数にバインドするか、[SQLGetData](../../../relational-databases/native-client-odbc-api/sqlgetdata.md) を使用して結果セット列からプログラム変数にデータを移動するか、あるいはこれらの 2 つの方法を組み合わせて結果を処理します。  
  
     ステートメントの結果セットを一度に 1 行ずつフェッチします。  
  
     \- - または -  
  
     ブロック カーソルを使用して一度に複数行の結果セットをフェッチします。  
  
     \- - または -  
  
     [SQLRowCount](../../../relational-databases/native-client-odbc-api/sqlrowcount.md) を呼び出して、INSERT、UPDATE、または DELETE ステートメントの影響を受ける行数を確認します。  
  
     SQL ステートメントに複数の結果セットが含まれている可能性がある場合は、各結果セットの最後に [SQLMoreResults](../../../relational-databases/native-client-odbc-api/sqlmoreresults.md) を呼び出して、処理する追加の結果セットがあるかどうかを確認します。  
  
7.  結果が処理されたら、ステートメント ハンドルで新しいステートメントを実行できるように、次のアクションが必要な場合があります。  
  
    -   SQL_NO_DATA が返されるまで [SQLMoreResults](../../../relational-databases/native-client-odbc-api/sqlmoreresults.md) を呼び出さなかった場合は、[SQLCloseCursor](../../../relational-databases/native-client-odbc-api/sqlclosecursor.md) を呼び出してカーソルを閉じます。  
  
    -   パラメーター マーカーをプログラム変数にバインドした場合は、[Option](../../../relational-databases/native-client-odbc-api/sqlfreestmt.md) を SQL_RESET_PARAMS に設定して *SQLFreeStmt* を呼び出し、バインドされたパラメーターを解放します。  
  
    -   結果セット列をプログラム変数にバインドした場合は、[Option](../../../relational-databases/native-client-odbc-api/sqlfreestmt.md) を SQL_UNBIND に設定して *SQLFreeStmt* を呼び出し、バインドされた列を解放します。  
  
    -   ステートメント ハンドルを再利用するには、手順 2. に進みます。  
  
8.  [HandleType](../../../relational-databases/native-client-odbc-api/sqlfreehandle.md) を SQL_HANDLE_STMT として *SQLFreeHandle* を呼び出し、ステートメント ハンドルを解放します。  
  
## <a name="see-also"></a>参照  
 [クエリの実行方法に関する&#40;トピック ODBC&#41;](../../../relational-databases/native-client-odbc-how-to/execute-queries/executing-queries-how-to-topics-odbc.md)  
  
  
