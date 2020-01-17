---
title: getPooledConnection メソッド () |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnectionPoolDataSource.getPooledConnection ()
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: aad6c325-3398-462c-aa6e-201dc89fa5ef
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 89b0379d9708a0f0d8809362afed6e64fe19f052
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67980822"
---
# <a name="getpooledconnection-method-"></a>getPooledConnection () メソッド
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  プールされた接続として使用できる物理データベース接続の確立を試みます。  
  
## <a name="syntax"></a>構文  
  
```  
  
public javax.sql.PooledConnection getPooledConnection()  
```  
  
## <a name="return-value"></a>戻り値  
 [SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md) オブジェクトです。  
  
## <a name="exceptions"></a>例外  
 java.sql.SQLException  
  
## <a name="remarks"></a>Remarks  
 この getPooledConnection メソッドは、javax.mail インターフェイスの getPooledConnection メソッドによって指定されます。  
  
## <a name="see-also"></a>参照  
 [getPooledConnection](../../../connect/jdbc/reference/getpooledconnection-method-sqlserverconnectionpooldatasource.md)   
 [SQLServerConnectionPoolDataSource のメソッド](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-methods.md)   
 [SQLServerConnectionPoolDataSource のメンバー](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-members.md)   
 [SQLServerConnectionPoolDataSource クラス](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md)  
  
  
