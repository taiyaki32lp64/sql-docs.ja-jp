---
title: getArray メソッド (int) (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getArray (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 377746c7-8c9c-41f5-8490-ca0dd56fd57a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ff7355a5d63d5f6335612d2bf5de5131f23cab96
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67954385"
---
# <a name="getarray-method-int-sqlserverresultset"></a>getArray (int) メソッド (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの現在の行にある指定された列インデックスの値が、Array オブジェクトとして取得されます。  
  
## <a name="syntax"></a>構文  
  
```  
  
public java.sql.Array getArray(int i)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *i*  
  
 列インデックスを示す **int** です。  
  
## <a name="return-value"></a>戻り値  
 Array オブジェクトです。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 この getArray メソッドは、java.sql.ResultSet インターフェイスの getArray メソッドで規定されています。  
  
## <a name="see-also"></a>参照  
 [getArray メソッド &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getarray-method-sqlserverresultset.md)   
 [SQLServerResultSet のメンバー](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet クラス](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
