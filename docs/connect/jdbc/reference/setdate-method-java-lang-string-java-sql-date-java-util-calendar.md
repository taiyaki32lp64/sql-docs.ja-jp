---
title: setDate メソッドから date および calendar-string |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.setDate (java.lang.String, java.sql.Date, java.util.Calendar)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: fd152ad6-dd5e-49ef-b166-917371a2cba6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0f986b7fd5faadfbd24708ec9a339d3bd2f104f0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67974585"
---
# <a name="setdate-method-javalangstring-javasqldate-javautilcalendar"></a>setDate (java.lang.String, java.sql.Date, java.util.Calendar) メソッド
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  渡された Calendar オブジェクトを使用して、指定されたパラメーターを、渡された日付の値に設定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public void setDate(java.lang.String sCol,  
                    java.sql.Date x,  
                    java.util.Calendar c)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *n*  
  
 パラメーターの番号を示す **int** です。  
  
 *x*  
  
 Date オブジェクトです。  
  
 *c*  
  
 Calendar オブジェクト。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 この setDate メソッドは、java.sql.CallableStatement インターフェイスの setDate メソッドで規定されています。  
  
## <a name="see-also"></a>参照  
 [SQLServerCallableStatement のメンバー](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement クラス](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
