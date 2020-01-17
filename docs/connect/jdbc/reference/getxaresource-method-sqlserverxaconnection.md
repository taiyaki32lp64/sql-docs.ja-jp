---
title: getXAResource メソッド (SQLServerXAConnection) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerXAConnection.getXAResource
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e1d2828f-fd20-44b0-b796-dc70f77c5b03
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c3d4b2132c3bbcf5612faa5f319a5358f158e2b7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67977978"
---
# <a name="getxaresource-method-sqlserverxaconnection"></a>getXAResource メソッド (SQLServerXAConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  [SQLServerXAConnection](../../../connect/jdbc/reference/sqlserverxaconnection-class.md) オブジェクトの分散トランザクションへの参加を管理するため、トランザクション マネージャーが使用する [SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md) オブジェクトを取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public javax.transaction.xa.XAResource getXAResource()  
```  
  
## <a name="return-value"></a>戻り値  
 XAResource オブジェクト。  
  
## <a name="exceptions"></a>例外  
 java.sql.SQLException  
  
## <a name="remarks"></a>Remarks  
 この getXAResource メソッドは、Javax.sql.xaconnection インターフェイスの getXAResource メソッドによって指定されます。  
  
## <a name="see-also"></a>参照  
 [SQLServerXAConnection のメソッド](../../../connect/jdbc/reference/sqlserverxaconnection-methods.md)   
 [SQLServerXAConnection のメンバー](../../../connect/jdbc/reference/sqlserverxaconnection-members.md)   
 [SQLServerXAConnection クラス](../../../connect/jdbc/reference/sqlserverxaconnection-class.md)  
  
  
