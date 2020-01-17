---
title: カーソルの使用 (ODBC) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 59a7e18c69ffa8d928dc38eaefcaf89249c18b38
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73784080"
---
# <a name="using-cursors-odbc"></a>カーソルの使用 (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  ODBC では、次のことを可能にするカーソル モデルがサポートされます。  
  
-   複数種類のカーソル  
  
-   カーソル内でのスクロールと位置指定  
  
-   複数のコンカレンシー オプション。  
  
-   位置指定更新。  
  
 ODBC アプリケーションでは、カーソルを宣言して開いたり、カーソル関連の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを使用することはほとんどありません。 ODBC では、SQL ステートメントから返されたすべての結果セットに対して自動的にカーソルを開きます。 カーソルの特性は、SQL ステートメントが実行される前に、 [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)で設定されたステートメント属性によって制御されます。 結果セットの処理に使用する ODBC API 関数では、フェッチ、スクロール、位置指定更新など、すべてのカーソル機能がサポートされます。  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] スクリプトと ODBC アプリケーションのカーソル操作の比較を次に示します。  
  
|操作|[!INCLUDE[tsql](../../includes/tsql-md.md)]|ODBC|  
|------------|------------------------|----------|  
|カーソル動作を定義する|DECLARE CURSOR パラメーターによる指定|[SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)を使用してカーソルの属性を設定する|  
|カーソルを開く|カーソルを開く*cursor_name*を宣言|**SQLExecDirect**または**sqlexecute**|  
|行をフェッチする|FETCH|**Sqlfetch**または[sqlfetchscroll](../../relational-databases/native-client-odbc-api/sqlfetchscroll.md)|  
|位置指定更新を行う|UPDATE または DELETE の WHERE CURRENT OF 句|**SQLSetPos**|  
|カーソルを閉じる|割り当て解除*CURSOR_NAME*終了|[SQLCloseCursor](../../relational-databases/native-client-odbc-api/sqlclosecursor.md)|  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に実装されているサーバー カーソルでは、ODBC カーソル モデルの機能がサポートされます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ドライバーでは、サーバー カーソルを使用して ODBC API のカーソル機能がサポートされます。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
-   [カーソルの実装方法](../../relational-databases/native-client-odbc-cursors/implementation/how-cursors-are-implemented.md)  
  
-   [カーソルの種類](../../relational-databases/native-client-odbc-cursors/cursor-types.md)  
  
-   [カーソル動作](../../relational-databases/native-client-odbc-cursors/cursor-behaviors.md)  
  
-   [カーソルのプロパティ](../../relational-databases/native-client-odbc-cursors/properties/cursor-properties.md)  
  
-   [カーソルプログラミングの&#40;詳細 ODBC&#41;](../../relational-databases/native-client-odbc-cursors/programming/cursor-programming-details-odbc.md)  
  
-   [行のスクロールとフェッチ](../../relational-databases/native-client-odbc-cursors/scrolling-and-fetching-rows.md)  
  
-   [位置指定&#40;更新 ODBC&#41;](../../relational-databases/native-client-odbc-cursors/positioned-updates-odbc.md)  
  
## <a name="see-also"></a>参照  
 [ &#40;ODBC&#41; ](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  の SQL Server Native Client  
 [CLOSE &#40;Transact-SQL&#41;](../../t-sql/language-elements/close-transact-sql.md)   
 [カーソル](../../relational-databases/cursors.md)   
 [DEALLOCATE &#40;Transact-SQL&#41;](../../t-sql/language-elements/deallocate-transact-sql.md)   
 [DECLARE CURSOR &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-cursor-transact-sql.md)   
 [FETCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/fetch-transact-sql.md)   
 [OPEN &#40;Transact-SQL&#41;](../../t-sql/language-elements/open-transact-sql.md)  
  
  
