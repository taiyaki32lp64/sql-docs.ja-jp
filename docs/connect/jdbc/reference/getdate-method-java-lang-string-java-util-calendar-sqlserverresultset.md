---
title: getDate メソッド (java. util. Calendar) column |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getDate (java.lang.String, java.util.Calendar)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 3fa2a72a-7499-44ec-8f76-a8e646e0190c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 36c1a84fe690760d6eeda6b43fb59a5d0268696c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67983996"
---
# <a name="getdate-method-javalangstring-javautilcalendar-sqlserverresultset"></a>getDate (java.lang.String, java.util.Calendar) メソッド (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  この [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの現在の行にある指定された列名の値を、渡された Calendar オブジェクトを使用し、Java プログラミング言語の java.sql.Date オブジェクトとして取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public java.sql.Date getDate(java.lang.String colName,  
                             java.util.Calendar cal)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *colName*  
  
 列名を含む**文字列**です。  
  
 *カレンダー*  
  
 Calendar オブジェクト。  
  
## <a name="return-value"></a>戻り値  
 Date オブジェクトです。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 この getDate メソッドは、java.sql.ResultSet インターフェイスの getDate メソッドで規定されています。  
  
 このメソッドは、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] datetime または smalldatetime データ型の有効な日付部分が返されます。時刻部分は、指定されたカレンダーのタイムゾーンにおける Java のベースラインの時刻である 00:00 (午前 0 時) に設定されます。  
  
## <a name="see-also"></a>参照  
 [getDate メソッド &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getdate-method-sqlserverresultset.md)   
 [SQLServerResultSet のメンバー](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet クラス](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
