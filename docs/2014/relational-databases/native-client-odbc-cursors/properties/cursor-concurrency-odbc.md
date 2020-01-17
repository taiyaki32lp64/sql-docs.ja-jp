---
title: カーソルの同時実行 (ODBC)。マイクロソフトのドキュメント
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- concurrency [ODBC]
- cursors [ODBC], concurrency
- ODBC cursors, concurrency
ms.assetid: 68228ece-cbf1-4f19-bfdc-053884c1af48
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3101da05e25cf67fda816bd889393bbebe8be3ac
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62711457"
---
# <a name="cursor-concurrency-odbc"></a>カーソル コンカレンシー (ODBC)
  カーソル操作は、カーソルの種類と同様に、アプリケーションで設定されるコンカレンシー オプションの影響を受けます。 同時実行オプションが設定の SQL_ATTR_CONCURRENCY オプションを使用して[SQLSetStmtAttr](../../native-client-odbc-api/sqlsetstmtattr.md)します。 コンカレンシーの種類は次のとおりです。  
  
-   読み取り専用 (SQL_CONCUR_READONLY)  
  
-   値 (SQL_CONCUR_VALUES)  
  
-   行バージョン (SQL_CONCUR_ROWVER)  
  
-   ロック (SQL_CONCUR_LOCK)  
  
## <a name="see-also"></a>関連項目  
 [カーソルのプロパティ](cursor-properties.md)  
  
  
