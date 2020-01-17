---
title: cancelRowUpdates メソッド (SQLServerResultSet) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.cancelRowUpdates
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 2ecacca4-f7bc-4f5d-886a-da7747fdccae
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d1598bca994ae41ccee56ca68e12e74e8d18fd0c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67955798"
---
# <a name="cancelrowupdates-method-sqlserverresultset"></a>cancelRowUpdates メソッド (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの現在の行に対する更新を取り消します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public void cancelRowUpdates()  
```  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 この cancelRowUpdates メソッドは、java. ResultSet インターフェイスの cancelRowUpdates メソッドによって指定されます。  
  
 updater メソッドを呼び出した後、[updateRow](../../../connect/jdbc/reference/updaterow-method-sqlserverresultset.md) メソッドを呼び出す前にこのメソッドを呼び出して、行に加えた更新をロールバックできます。 更新が行われていない場合、または updateRow が既に呼び出されている場合、このメソッドは無効です。  
  
## <a name="see-also"></a>参照  
 [SQLServerResultSet のメンバー](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet クラス](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
