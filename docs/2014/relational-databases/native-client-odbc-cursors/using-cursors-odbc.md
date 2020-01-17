---
title: カーソルの使用 (ODBC) |マイクロソフトのドキュメント
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, cursors
- ODBC cursors, about ODBC cursors
- ODBC applications, cursors
- cursors [ODBC]
- ODBC cursors
ms.assetid: 51322f92-0d76-44c9-9c33-9223676cf1d3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bc53253c93f5f52c6bbe00941eadbf14b65d5f64
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68206822"
---
# <a name="using-cursors-odbc"></a>カーソルの使用 (ODBC)
  ODBC では、次のことを可能にするカーソル モデルがサポートされます。  
  
-   複数種類のカーソル  
  
-   カーソル内でのスクロールと位置指定  
  
-   複数のコンカレンシー オプション。  
  
-   位置指定更新します。  
  
 ODBC アプリケーションでは、カーソルを宣言して開いたり、カーソル関連の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを使用することはほとんどありません。 ODBC では、SQL ステートメントから返されたすべての結果セットに対して自動的にカーソルを開きます。 カーソルの特性を設定するステートメント属性によって制御されます[SQLSetStmtAttr](../native-client-odbc-api/sqlsetstmtattr.md) SQL する前にステートメントが実行されます。 結果セットの処理に使用する ODBC API 関数では、フェッチ、スクロール、位置指定更新など、すべてのカーソル機能がサポートされます。  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] スクリプトと ODBC アプリケーションのカーソル操作の比較を次に示します。  
  
|操作|[!INCLUDE[tsql](../../includes/tsql-md.md)]|ODBC|  
|------------|------------------------|----------|  
|カーソル動作を定義する|DECLARE CURSOR パラメーターによる指定|使用してカーソルの属性を設定[SQLSetStmtAttr](../native-client-odbc-api/sqlsetstmtattr.md)|  
|カーソルを開く|開いているカーソルの宣言*cursor_name*|**SQLExecDirect**または**SQLExecute**|  
|行をフェッチする|FETCH|**SQLFetch**または[SQLFetchScroll](../native-client-odbc-api/sqlfetchscroll.md)|  
|位置指定更新を行う|UPDATE または DELETE の WHERE CURRENT OF 句|**SQLSetPos**|  
|カーソルを閉じる|閉じる*cursor_name* DEALLOCATE|[SQLCloseCursor](../native-client-odbc-api/sqlclosecursor.md)|  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に実装されているサーバー カーソルでは、ODBC カーソル モデルの機能がサポートされます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ドライバーでは、サーバー カーソルを使用して ODBC API のカーソル機能がサポートされます。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
-   [カーソルの実装方法](implementation/how-cursors-are-implemented.md)  
  
-   [カーソルの種類](cursor-types.md)  
  
-   [カーソル動作](cursor-behaviors.md)  
  
-   [カーソルのプロパティ](properties/cursor-properties.md)  
  
-   [カーソル プログラミングの詳細&#40;ODBC&#41;](programming/cursor-programming-details-odbc.md)  
  
-   [行のスクロールとフェッチ](../native-client-ole-db-rowsets/fetching-rows.md)  
  
-   [位置指定更新&#40;ODBC&#41;](positioned-updates-odbc.md)  
  
## <a name="see-also"></a>関連項目  
 [SQL Server Native Client &#40;ODBC&#41;](../native-client/odbc/sql-server-native-client-odbc.md)   
 [CLOSE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/close-transact-sql)   
 [カーソル](../../relational-databases/cursors.md)   
 [DEALLOCATE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/deallocate-transact-sql)   
 [DECLARE CURSOR &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/declare-cursor-transact-sql)   
 [FETCH &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/fetch-transact-sql)   
 [OPEN &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/open-transact-sql)  
  
  
