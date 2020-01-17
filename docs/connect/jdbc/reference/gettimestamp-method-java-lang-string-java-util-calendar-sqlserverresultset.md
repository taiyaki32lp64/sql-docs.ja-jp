---
title: getTimestamp (java.lang.String, java.util.Calendar) メソッド | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getTimestamp (java.lang.String, java.util.Calendar)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 44474000-8951-49ee-93a5-c8cb879eaf55
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 25731d68f767fbdd614525e5a39613fc46ae6206
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67978828"
---
# <a name="gettimestamp-method-javalangstring-javautilcalendar-sqlserverresultset"></a>getTimestamp (java.lang.String, java.util.Calendar) メソッド (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Calendar オブジェクトを使用して、[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの現在の行にある指定された列名の値が Java プログラミング言語の java.sql.Timestamp オブジェクトとして取得されます。  
  
## <a name="syntax"></a>構文  
  
```  
  
public java.sql.Timestamp getTimestamp(java.lang.String colName,  
                                       java.util.Calendar cal)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *colName*  
  
 列名を含む**文字列**です。  
  
 *カレンダー*  
  
 Calendar オブジェクト。  
  
## <a name="return-value"></a>戻り値  
 タイムスタンプオブジェクト。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 この getTimestamp メソッドは、java.sql.ResultSet インターフェイスの getTimestamp メソッドで規定されています。  
  
 このメソッドでは、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の datetime 列と smalldatetime 列からのみ値が返されます。  
  
## <a name="see-also"></a>参照  
 [getTimestamp メソッド &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/gettimestamp-method-sqlserverresultset.md)   
 [SQLServerResultSet のメンバー](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet クラス](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
