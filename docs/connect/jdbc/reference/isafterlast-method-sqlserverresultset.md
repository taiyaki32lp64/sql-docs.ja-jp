---
title: isAfterLast メソッド (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.isAfterLast
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 19f9d124-3184-4985-8b97-503a8ab8b4f9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 233599694c4fb4f7764bbb48d5c77e0fcd273340
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67977839"
---
# <a name="isafterlast-method-sqlserverresultset"></a>isAfterLast メソッド (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  カーソルが、[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの最終行の後ろにあるかどうかを取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public boolean isAfterLast()  
```  
  
## <a name="return-value"></a>戻り値  
 カーソルが最後の行の後にある場合は**true** 。 カーソルが他の位置にある場合、または結果セットに行が含まれていない場合は**false** 。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 この isAfterLast メソッドは、java.sql.ResultSet インターフェイスの isAfterLast メソッドで規定されています。  
  
 このメソッドが動的カーソル (順方向専用、読み取り専用カーソルを含む) で使用され、selectMethod 接続プロパティが "cursor" に設定されている場合は、例外が発生します。  
  
## <a name="see-also"></a>参照  
 [SQLServerResultSet のメンバー](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet クラス](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
