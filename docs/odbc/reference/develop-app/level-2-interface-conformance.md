---
title: レベル 2 インターフェイスの適合性 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interface conformance levels [ODBC]
- level 2 interface conformance levels [ODBC]
- conformance levels [ODBC], interface
ms.assetid: 2dc87840-f2fe-43dd-9d7b-bd95523081d9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 50e74eaed2d651158834a241563d10b3b2e90d5b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67915573"
---
# <a name="level-2-interface-conformance"></a>レベル 2 インターフェイスの適合性
レベル 2 インターフェイスの適合性レベルには、レベル 1 インターフェイスの適合性レベルの機能に加えて、次の機能が含まれています。  
  
|||  
|-|-|  
|201|データベース テーブルとビューの 3 つの部分名を使用します。 (詳細については、2 つの部分で構成名前付けのサポート機能は、101 を参照してください[レベル 1 インターフェイスの適合性](../../../odbc/reference/develop-app/level-1-interface-conformance.md)。)。|  
|202|動的パラメーターを呼び出すことによって記述**SQLDescribeParam**します。|  
|203|だけでなく入力パラメーターですも出力パラメーター、入力/出力パラメーター、およびストアド プロシージャの結果の値を使用します。|  
|204|ブックマークを呼び出すことによって、ブックマークの取得などを使用して**SQLDescribeCol**と**SQLColAttribute**列番号が 0; 呼び出すことによって、ブックマークに基づくフェッチ**SQLFetchScroll**で、 *FetchOrientation* SQL_FETCH_BOOKMARK; に更新プログラム、設定の引数は、削除、および呼び出すことによって、ブックマークの工程でフェッチ**SQLBulkOperations** で*操作*引数 SQL_UPDATE_BY_BOOKMARK、SQL_DELETE_BY_BOOKMARK、または SQL_FETCH_BY_BOOKMARK に設定します。|  
|205|データ辞書についての情報を呼び出すことによって高度な取得**SQLColumnPrivileges**、 **SQLForeignKeys**、および**SQLTablePrivileges**します。|  
|206|SQL ステートメントの代わりに呼び出すことによって、その他のデータベース操作を実行する ODBC 関数を使用して**SQLBulkOperations** SQL_ADD、使用または**SQLSetPos** SQL_DELETE または SQL_UPDATE します。 (サポートへの呼び出しに**SQLSetPos**で、 *LockType* SQL_LOCK_EXCLUSIVE または SQL_LOCK_UNLOCK に設定する引数は、適合性レベルの一部ではありませんが、オプション機能です)。|  
|207|指定された個々 のステートメントの ODBC 関数の非同期実行を有効にします。|  
|208|呼び出すことによって、テーブルの SQL_ROWVER 行を識別する列を取得**SQLSpecialColumns**します。 (詳細については、サポートを参照してください**SQLSpecialColumns**で、 *IdentifierType*引数 SQL_BEST_ROWID 機能の 20 のように設定[Core インターフェイスの適合性](../../../odbc/reference/develop-app/core-interface-conformance.md).)|  
|209|また、ステートメント属性 SQL_ATTR_CONCURRENCY を SQL_CONCUR_READ_ONLY 以外の少なくとも 1 つの値に設定します。|  
|210|ログイン要求のタイムアウトと SQL クエリ (SQL_ATTR_LOGIN_TIMEOUT および SQL_ATTR_QUERY_TIMEOUT) する機能。|  
|211|既定の分離レベルを変更する機能「シリアル化可能な」分離レベルでトランザクションを実行する機能。|
