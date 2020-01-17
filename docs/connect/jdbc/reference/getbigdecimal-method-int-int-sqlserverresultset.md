---
title: getBigDecimal メソッド (int, int) (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getBigDecimal (int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: c99d0772-b26c-492c-a643-2813b5429993
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 15991cb98860ccc471229ae3abb8e3b24e35c799
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67954012"
---
# <a name="getbigdecimal-method-int-int-sqlserverresultset"></a>getBigDecimal (int, int) メソッド (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの現在の行にある指定された列インデックスの値を、渡された小数点以下桁数を使用して取得します。  
  
> [!NOTE]  
>  このメソッドは、JDBC 仕様では非推奨とされました。 代わりに、[getBigDecimal (int)](../../../connect/jdbc/reference/getbigdecimal-method-int-sqlserverresultset.md) メソッドを使用してください。  
  
## <a name="syntax"></a>構文  
  
```  
  
public java.math.BigDecimal getBigDecimal(int columnIndex,  
                                          int scale)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *columnIndex*  
  
 列インデックスを示す **int** です。  
  
 *scale*  
  
 小数点以下の桁数を示す **int** です。  
  
## <a name="return-value"></a>戻り値  
 BigDecimal オブジェクト。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 この getBigDecimal メソッドは、java. ResultSet インターフェイスの getBigDecimal メソッドによって指定されます。  
  
## <a name="see-also"></a>参照  
 [getBigDecimal メソッド &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getbigdecimal-method-sqlserverresultset.md)   
 [SQLServerResultSet のメンバー](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet クラス](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
