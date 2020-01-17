---
title: 行のスクロールとフェッチ |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9a8c0c0783ff51548143fa7fd670de2502482673
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73784054"
---
# <a name="scrolling-and-fetching-rows"></a>行のスクロールとフェッチ
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  スクロール可能なカーソルを使用するには、ODBC アプリケーションでは次の操作を行う必要があります。  
  
-   [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)を使用してカーソル機能を設定します。  
  
-   **Sqlexecute**または**SQLExecDirect**を使用してカーソルを開きます。  
  
-   **Sqlfetch**または[sqlfetchscroll](../../relational-databases/native-client-odbc-api/sqlfetchscroll.md)を使用して行をスクロールおよびフェッチします。  
  
 **Sqlfetch**と**Sqlfetchsroll**は、同時に行のブロックをフェッチできます。 返される行の数は、SQL_ATTR_ROW_ARRAY_SIZE パラメーターを設定するために**SQLSetStmtAttr**を使用して指定します。  
  
 ODBC アプリケーションでは、 **Sqlfetch**を使用して、順方向専用カーソルを介してフェッチできます。  
  
 カーソルをスクロールするには、 **Sqlfetchscroll**を使用します。 **Sqlfetchscroll**は、相対フェッチ (現在の行セットの先頭から行セット*n*の行をフェッチ) と絶対フェッチ (行*n*で始まる行セットのフェッチ) に加えて、次の行セット、以前の行セット、最初の行セット、および最後の行セットのフェッチをサポートしています。 絶対フェッチで*n*が負の値の場合、行は結果セットの末尾からカウントされます。 たとえば、行 -1 の絶対フェッチは、結果セット内にある最後の行を起点とした行セットをフェッチします。  
  
 レポートなどのブロックカーソル機能に対してのみ**Sqlfetchscroll**を使用するアプリケーションは、次の行セットをフェッチするオプションのみを使用して、結果セットを1回だけ通過する可能性があります。 一方、画面ベースのアプリケーションでは、 **Sqlfetchscroll**のすべての機能を利用できます。 アプリケーションで、行セットのサイズを画面に表示される行数に設定し、画面バッファーを結果セットにバインドすると、スクロールバーの操作を**Sqlfetchscroll**の呼び出しに直接変換できます。  
  
|スクロール バーの操作|SQLFetchScroll のスクロール操作|  
|--------------------------|-------------------------------------|  
|1 画面分上へ移動 (PageUp)|SQL_FETCH_PRIOR|  
|1 画面分下へ移動 (PageDown)|SQL_FETCH_NEXT|  
|1 行上へ移動|FetchOffset が-1 に等しい SQL_FETCH_RELATIVE|  
|1 行下へ移動|FetchOffset に 1 を指定した SQL_FETCH_RELATIVE|  
|スクロール ボックスを先頭に移動|SQL_FETCH_FIRST|  
|スクロール ボックスを末尾に移動|SQL_FETCH_LAST|  
|スクロール ボックスを任意の位置に移動|SQL_FETCH_ABSOLUTE|  
  
## <a name="in-this-section"></a>このセクションの内容  
  
-   [ODBC での行のブックマーク](../../relational-databases/native-client-odbc-cursors/scrolling-and-fetching-rows-bookmarking-rows-in-odbc.md)  
  
## <a name="see-also"></a>参照  
 [カーソル&#40;を使用した ODBC&#41;](../../relational-databases/native-client-odbc-cursors/using-cursors-odbc.md)  
  
  
