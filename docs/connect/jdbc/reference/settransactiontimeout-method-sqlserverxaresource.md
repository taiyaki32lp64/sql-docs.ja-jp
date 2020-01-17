---
title: setTransactionTimeout メソッド (SQLServerXAResource) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerXAResource.setTransactionTimeout
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 38bf4a1a-6ad3-437c-b9ed-8792ab6dde7e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 481843393f15998df059bb7a732c64010b2c8bf0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67972281"
---
# <a name="settransactiontimeout-method-sqlserverxaresource"></a>setTransactionTimeout Method メソッド (SQLServerXAResource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  [SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md) オブジェクトの現在のトランザクション タイムアウト値を設定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public boolean setTransactionTimeout(int seconds)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *seconds*  
  
 **Int**値。  
  
## <a name="return-value"></a>戻り値  
 タイムアウトが正常に設定された場合は **true** です。 それ以外の場合は、 **false**です。  
  
## <a name="exceptions"></a>例外  
 javax.transaction.xa.XAException  
  
## <a name="remarks"></a>Remarks  
 この setTransactionTimeout メソッドは、javax.mail インターフェイスの setTransactionTimeout メソッドによって指定されます。  
  
## <a name="see-also"></a>参照  
 [SQLServerXAResource のメソッド](../../../connect/jdbc/reference/sqlserverxaresource-methods.md)   
 [SQLServerXAResource のメンバー](../../../connect/jdbc/reference/sqlserverxaresource-members.md)   
 [SQLServerXAResource クラス](../../../connect/jdbc/reference/sqlserverxaresource-class.md)  
  
  
