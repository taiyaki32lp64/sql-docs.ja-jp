---
title: カーソルの行セットのサイズ。マイクロソフトのドキュメント
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- cursors [ODBC], rowset size
- ODBC cursors, rowset size
- rowsets [ODBC]
ms.assetid: 2febe2ae-fdc1-490e-a79f-c516bc8e7c3f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bff145e7e3c6e429ca0877c81c5188b02e428809
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63207166"
---
# <a name="cursor-rowset-size"></a>カーソルの行セット サイズ
  ODBC カーソルでは、一度にフェッチできる行数は制限されません。 呼び出すたびに複数の行を取得することができます**SQLFetch**または[SQLFetchScroll](../../native-client-odbc-api/sqlfetchscroll.md)。 Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のようなクライアント/サーバー型のデータベースで作業しているときは、1 回に複数行を取得する方が効率的です。 フェッチで返される行の数が行セットのサイズという名前の SQL_ATTR_ROW_ARRAY_SIZE を使用して指定されて[SQLSetStmtAttr](../../native-client-odbc-api/sqlsetstmtattr.md)します。  
  
```  
SQLUINTEGER uwRowsize;  
SQLSetStmtAttr(m_hstmt, SQL_ATTR_ROW_ARRAY_SIZE, (SQLPOINTER)uwRowsetSize, SQL_IS_UINTEGER);  
```  
  
 行セット サイズが 2 以上のカーソルをブロック カーソルと呼びます。  
  
 ブロック カーソルの結果セット列は、次の 2 つの方法でバインドできます。  
  
-   列方向のバインド  
  
     各列が変数の配列にバインドされます。 各配列には行セット サイズと同じ数の要素が含まれます。  
  
-   行方向のバインド  
  
     1 行のすべての列のデータとインジケーターが含まれる構造体を使用して配列が構築されます。 この配列には行セット サイズと同じ数の構造体が含まれます。  
  
 列方向または行方向のバインドを使用する場合、各呼び出し**SQLFetch**または**SQLFetchScroll**バインド配列を取得した行セットからのデータを入力します。  
  
 [SQLGetData](../../native-client-odbc-api/sqlgetdata.md)ブロック カーソルの列のデータを取得する場合にも使用することができます。 **SQLGetData** 、一度に 1 つの行の動作**SQLSetPos**呼び出しの前に現在の行として行セット内の特定の行を設定するのには呼び出す必要があります**SQLGetData**。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]ネイティブ クライアントの ODBC ドライバーは、設定を簡単に全体の結果を取得する行セットを使用して最適化を提供しています。 このような最適化を使用するには、カーソルの属性を既定値に設定 (順方向専用、読み取り専用、行セット サイズ = 1) に**される**または**SQLExecute**と呼ばれます。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]ネイティブ クライアントの ODBC ドライバーは、既定の結果セットを設定します。 スクロールを使用しないでクライアントに結果を送信する場合は、既定の結果セットの方がサーバー カーソルよりも効率的です。 ステートメントを実行後、行セット サイズを増やし、列方向のバインドか行方向のバインドを使用します。 これにより、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]の結果行を効率的にクライアントに送信するのには既定の結果セットのセットを使用中に、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]ネイティブ クライアントの ODBC ドライバーは、クライアントのネットワーク バッファーから行を取得する継続的にします。  
  
## <a name="see-also"></a>関連項目  
 [カーソルのプロパティ](cursor-properties.md)  
  
  
