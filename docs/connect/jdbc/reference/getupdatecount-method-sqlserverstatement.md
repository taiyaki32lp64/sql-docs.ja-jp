---
title: getUpdateCount メソッド (SQLServerStatement) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.getUpdateCount
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e9570228-4500-44b6-b2f1-84ac050b5112
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e319f5f924fc82b3b7dfac31d5d64d8ea15ee3ab
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67978390"
---
# <a name="getupdatecount-method-sqlserverstatement"></a>getUpdateCount メソッド (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  現在の結果を更新数として取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public final int getUpdateCount()  
```  
  
## <a name="return-value"></a>戻り値  
 更新数を含む **int** です。 返された結果が結果セット オブジェクトである場合、または結果がなくなった場合は、-1 が返されます。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 この getUpdateCount メソッドは、java. .sql. ステートメントインターフェイスの getUpdateCount メソッドによって指定されます。  
  
## <a name="see-also"></a>参照  
 [SQLServerStatement のメンバー](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement クラス](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
