---
title: スクロールとフェッチ行 |マイクロソフトのドキュメント
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- scrollable cursors [SQL Server]
- SQL Server Native Client ODBC driver, cursors
- SQLFetchScroll function
- ODBC applications, cursors
- cursors [ODBC], fetching rows
- ODBC cursors, fetching rows
- cursors [ODBC], scrolling rows
- fetching [ODBC]
- ODBC cursors, scrolling rows
ms.assetid: 9109f10d-326b-4a6d-8c97-831f60da8c4c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a0c0f7f2cad7eaecc212e2283fab7fc7d69f2ee7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63207124"
---
# <a name="scrolling-and-fetching-rows"></a>行のスクロールとフェッチ
  スクロール可能なカーソルを使用するには、ODBC アプリケーションでは次の操作を行う必要があります。  
  
-   設定を使用してカーソル機能[SQLSetStmtAttr](../native-client-odbc-api/sqlsetstmtattr.md)します。  
  
-   使用して、カーソルを開く**SQLExecute**または**SQLExecDirect**します。  
  
-   使用して行のスクロールとフェッチ**SQLFetch**または[SQLFetchScroll](../native-client-odbc-api/sqlfetchscroll.md)します。  
  
 両方**SQLFetch**と**SQLFetchSroll**行のブロックを一度にフェッチできます。 指定された行の数が返される**SQLSetStmtAttr** SQL_ATTR_ROW_ARRAY_SIZE パラメーターを設定します。  
  
 ODBC アプリケーションで使用できる**SQLFetch**順方向専用カーソルを介してフェッチを実行します。  
  
 **SQLFetchScroll**カーソルの周囲をスクロールするために使用します。 **SQLFetchScroll** 、次のフェッチをサポートしているだけでなく相対フェッチ前に、最初と最後の行セット (行セットをフェッチ*n*現在の行セットの先頭からの行) と絶対フェッチ (行セットのフェッチ行から始まる*n*)。 場合*n*は行が結果セットの最後から数えられます絶対フェッチで負の値。 たとえば、行 -1 の絶対フェッチは、結果セット内にある最後の行を起点とした行セットをフェッチします。  
  
 使用するアプリケーション**SQLFetchScroll**ブロックに対してのみ、レポートなどのカーソル機能は、一度に 1 つを結果セットを通過する可能性がありますオプションのみを使用して、次の行セットをフェッチします。 スクリーン ベースのアプリケーションでは、その一方で、活用することのすべての機能**SQLFetchScroll**します。 スクロール バーの操作への呼び出しを直接変換できる場合は、アプリケーションでは、行セットのサイズを画面に表示される行の数に設定し、結果セットに、画面バッファーをバインドする、 **SQLFetchScroll**します。  
  
|スクロール バーの操作|SQLFetchScroll のスクロール操作|  
|--------------------------|-------------------------------------|  
|1 画面分上へ移動 (PageUp)|SQL_FETCH_PRIOR|  
|1 画面分下へ移動 (PageDown)|SQL_FETCH_NEXT|  
|1 行上へ移動|指定したを-1 に FetchOffset SQL_FETCH_RELATIVE|  
|1 行下へ移動|FetchOffset に 1 を指定した SQL_FETCH_RELATIVE|  
|スクロール ボックスを先頭に移動|SQL_FETCH_FIRST|  
|スクロール ボックスを末尾に移動|SQL_FETCH_LAST|  
|スクロール ボックスを任意の位置に移動|SQL_FETCH_ABSOLUTE|  
  
## <a name="in-this-section"></a>このセクションの内容  
  
-   [ODBC での行のブックマーク](scrolling-and-fetching-rows-bookmarking-rows-in-odbc.md)  
  
## <a name="see-also"></a>参照  
 [カーソルを使用して&#40;ODBC&#41;](using-cursors-odbc.md)  
  
  
