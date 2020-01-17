---
title: ブックマーク (ODBC) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], bookmarks
- bookmarks [ODBC]
ms.assetid: 1d7cccc5-f847-4321-b240-28570854ee5c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bab3571ba880658d9f1a2629b899484008428083
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68118786"
---
# <a name="bookmarks-odbc"></a>ブックマーク (ODBC)
ブックマークは、データ行の識別に使われる値です。 ブックマーク値の意味を解釈できるのは、ドライバーまたはデータ ソースのみです。 たとえば、ブックマークは、行番号のような単純な値の場合も、ディスク アドレスのような複雑な値の場合もあります。 ODBC でのブックマークは、実際のブック内のブックマークとは少し異なります。 実際の本のリーダーは特定のページにブックマークを配置し、ページに戻るには、そのブックマークを探します。 ODBC では、アプリケーションが特定の行のブックマークを要求し、これを保存し、カーソルに戻して行に返します。 したがって、ODBC でのブックマークは、記憶して、もう一度ページを検索し、ページ番号を書き留めるリーダーに似ています。  
  
 ブックマークのドライバーのサポートを確認するアプリケーションを呼び出す**SQLGetInfo** SQL_BOOKMARK_PERSISTENCE オプションを使用します。 この値のビットは、どのような操作のブックマーク存続しますが、カーソルが閉じられた後ブックマークがまだ有効にはかどうかなどについて説明します。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [ブックマークの種類](../../../odbc/reference/develop-app/bookmark-types.md)  
  
-   [ブックマークの取得](../../../odbc/reference/develop-app/retrieving-bookmarks.md)  
  
-   [ブックマークによるスクロール](../../../odbc/reference/develop-app/scrolling-by-bookmark.md)  
  
-   [ブックマークによる更新、削除、またはフェッチ](../../../odbc/reference/develop-app/updating-deleting-or-fetching-by-bookmark.md)  
  
-   [ブックマークの比較](../../../odbc/reference/develop-app/comparing-bookmarks.md)
