---
title: カーソルの動作 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- scrollable cursors [SQL Server]
- SQL Server Native Client ODBC driver, cursors
- version-based optimistic concurrency
- cursors [ODBC], cursor behaviors
- ODBC applications, cursors
- SQL_ATTR_CURSOR_SENSITIVITY option
- SQL_ATTR_CURSOR_SCROLLABLE option
- sensitivity behavior of cursor
- ODBC cursors, cursor behaviors
ms.assetid: 742ddcd2-232b-4aa1-9212-027df120ad35
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6c5ded9f42da267cfd137f0adfd4465d965d9a06
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63188564"
---
# <a name="cursor-behaviors"></a>カーソル動作
  ODBC では、カーソルのスクロールの可否と感度を設定することでカーソル動作を指定する、ISO オプションがサポートされます。 これらの動作は、SQL_ATTR_CURSOR_SCROLLABLE と SQL_ATTR_CURSOR_SENSITIVITY オプションへの呼び出しでの設定で指定された[SQLSetStmtAttr](../native-client-odbc-api/sqlsetstmtattr.md)します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーでは、次の特性を持つサーバー カーソルを要求して、これらのオプションを実装します。  
  
|カーソル動作の設定|要求されるサーバー カーソルの特性|  
|------------------------------|---------------------------------------------|  
|SQL_SCROLLABLE と SQL_SENSITIVE|キーセット ドリブン カーソルとバージョンに基づくオプティミスティック コンカレンシー|  
|SQL_SCROLLABLE と SQL_INSENSITIVE|静的カーソルと読み取り専用コンカレンシー|  
|SQL_SCROLLABLE と SQL_UNSPECIFIED|静的カーソルと読み取り専用コンカレンシー|  
|SQL_NONSCROLLABLE と SQL_SENSITIVE|順方向専用カーソルとバージョンに基づくオプティミスティック コンカレンシー|  
|SQL_NONSCROLLABLE と SQL_INSENSITIVE|既定の結果セット (順方向専用、読み取り専用)|  
|SQL_NONSCROLLABLE と SQL_UNSPECIFIED|既定の結果セット (順方向専用、読み取り専用)|  
  
 バージョンに基づくオプティミスティック同時実行制御が必要です、**タイムスタンプ**基になるテーブル内の列。 バージョンに基づくオプティミスティック同時実行制御がないテーブルで要求された場合、**タイムスタンプ**列に、サーバー使用の値に基づくオプティミスティック同時実行制御。  
  
## <a name="scrollability"></a>スクロール可能  
 SQL_ATTR_CURSOR_SCROLLABLE が SQL_SCROLLABLE に設定されている場合、カーソルはのすべての異なる値をサポートしています、 *FetchOrientation*パラメーターの[SQLFetchScroll](../native-client-odbc-api/sqlfetchscroll.md)します。 SQL_ATTR_CURSOR_SCROLLABLE が SQL_NONSCROLLABLE に設定されている場合、カーソルのみをサポートする*FetchOrientation* SQL_FETCH_NEXT の値。  
  
## <a name="sensitivity"></a>感度  
 SQL_ATTR_CURSOR_SENSITIVITY が SQL_SENSITIVE に設定されているとき、現在のユーザーが行ったデータ変更または他のユーザーがコミットしたデータ変更がカーソルに反映されます。 SQL_ATTR_CURSOR_SENSITIVITY が SQL_INSENSITIVE に設定されているときは、データ変更がカーソルに反映されません。  
  
## <a name="see-also"></a>参照  
 [カーソルを使用して&#40;ODBC&#41;](using-cursors-odbc.md)  
  
  
