---
title: getCursorName メソッド (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getCursorName
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e5b3af67-423a-4551-a4c6-a4bc076bd504
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a4f57b300cb402f422b92330bfe33f1e3c61cf4f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67984191"
---
# <a name="getcursorname-method-sqlserverresultset"></a>getCursorName メソッド (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトによって使用される SQL カーソルの名前を取得します。  
  
> [!NOTE]  
>  このメソッドは、現在 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] ではサポートされていません。 このメソッドを呼び出すと、例外がスローされます。  
  
## <a name="syntax"></a>構文  
  
```  
  
public java.lang.String getCursorName()  
```  
  
## <a name="return-value"></a>戻り値  
 カーソル名を含む **String** です。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 この Getカーソル名メソッドは、java. ResultSet インターフェイスの Getカーソル名メソッドによって指定されます。  
  
## <a name="see-also"></a>参照  
 [SQLServerResultSet のメンバー](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet クラス](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
