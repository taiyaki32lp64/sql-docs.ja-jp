---
title: insertRow メソッド (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.insertRow
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 363d1008-1396-4fc0-8e27-c9ba2499e7f1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0f2e6148572d6ec6c7e9b52a704d79e8a9124ccf
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67977884"
---
# <a name="insertrow-method-sqlserverresultset"></a>insertRow メソッド (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  挿入行の内容を [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトとデータベースに追加します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public void insertRow()  
```  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 この insertRow メソッドは、insertRow インターフェイスのメソッドによって指定されます。  
  
 このメソッドを呼び出すときに、カーソルが挿入行にある必要があります。 このメソッドが呼び出された後も、カーソルは挿入行に残り、結果セットは挿入モードのままになります。  
  
## <a name="see-also"></a>参照  
 [SQLServerResultSet のメンバー](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet クラス](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
