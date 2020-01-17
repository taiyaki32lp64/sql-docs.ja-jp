---
title: SQLGetCursorName |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLGetCursorName function
ms.assetid: 3a427a23-28ef-49aa-b9ec-6cab0914bdf3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 603a2b5be4ca75495f094aa838d0373a9689a523
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62657781"
---
# <a name="sqlgetcursorname"></a>SQLGetCursorName
  アプリケーションが、カーソル名を指定しない場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーでは、カーソルの生成時にアプリケーションに 1 つが生成されます。 アプリケーションが使用できる**SQLGetCursorName**位置指定の UPDATE および DELETE ステートメントのドライバー定義カーソル名を取得します。 アプリケーションが呼び出す必要はありません**SQLSetCursorName**活用するために、データ操作ステートメントを配置します。  
  
## <a name="see-also"></a>参照  
 [SQLGetCursorName 関数](https://go.microsoft.com/fwlink/?LinkId=59349)   
 [ODBC API 実装の詳細](odbc-api-implementation-details.md)  
  
  
