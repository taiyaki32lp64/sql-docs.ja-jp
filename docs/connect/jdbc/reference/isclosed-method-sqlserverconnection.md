---
title: isClosed メソッド (SQLServerConnection) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.isClosed
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 3560ab18-4350-4d02-9716-439f0c2f7142
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 45e56a0a5ddb7cf8aece6813d421b7ebb1685408
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67977710"
---
# <a name="isclosed-method-sqlserverconnection"></a>isClosed メソッド (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) オブジェクトが閉じられているかどうかを示します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public boolean isClosed()  
```  
  
## <a name="return-value"></a>戻り値  
 接続が閉じている場合は**true** 、それ以外の場合は**false** 。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 この isClosed メソッドは、java. .sql. 接続インターフェイスの isClosed メソッドによって指定されます。  
  
 呼び出された SQLServerConnection オブジェクトの状態を検証します。 接続に対して [close](../../../connect/jdbc/reference/close-method-sqlserverconnection.md) メソッドが既に呼び出されている場合、または特定の致命的なエラーが発生した場合、接続は閉じられています。 このメソッドが **true** を返すのは、close メソッドが呼び出された後に呼び出された場合だけです。  
  
## <a name="see-also"></a>参照  
 [SQLServerConnection のメンバー](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection クラス](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
