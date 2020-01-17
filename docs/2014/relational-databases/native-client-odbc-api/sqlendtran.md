---
title: SQLEndTran | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLEndTran function
ms.assetid: 95cff841-c2d5-4e1e-a18d-f3d4696a5b85
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f5425fdc189febd23e9fc61765f4ad56fe484111
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63067594"
---
# <a name="sqlendtran"></a>SQLEndTran
  既定で、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーがステートメントの関連付けられているカーソルを閉じるときに**SQLEndTran**コミットまたはロールバック操作を行います。 サーバー カーソルは、静的カーソルでない限り、閉じられます。 ときに**SQLEndTran**がコミットまたはロールバック操作をステートメントの関連付けられているカーソルの動作はによって設定ドライバー固有のODBC接続属性SQL_COPT_SS_PRESERVE_CURSORSの値によって決まります[SQLSetConnectAttr](sqlsetconnectattr.md)します。  
  
## <a name="see-also"></a>関連項目  
 [ODBC API 実装の詳細](odbc-api-implementation-details.md)   
 [SQLEndTran 関数](https://go.microsoft.com/fwlink/?LinkId=59342)  
  
  
