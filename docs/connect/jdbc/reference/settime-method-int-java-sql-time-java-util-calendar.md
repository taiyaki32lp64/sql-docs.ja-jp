---
title: setTime (int, java.sql.Time, java.util.Calendar) メソッド | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.setTime (int, java.sql.Time, java.lang.Calendar)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 79ff6eef-6ad7-4e33-95be-c2d552c65546
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c6388ea031c6cbd5c492b5af03bd37a091592868
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67972564"
---
# <a name="settime-method-int-javasqltime-javautilcalendar"></a>setTime (int, java.sql.Time, java.util.Calendar) メソッド
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  渡された Calendar オブジェクトを使用して、指定されたパラメーターを、渡された時刻の値に設定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public final void setTime(int n,  
                          java.sql.Time x,  
                          java.util.Calendar cal)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *n*  
  
 パラメーターの番号を示す **int** です。  
  
 *x*  
  
 時刻オブジェクト。  
  
 *カレンダー*  
  
 Calendar オブジェクト。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 この setTime メソッドは、java.sql.PreparedStatement インターフェイスの setTime メソッドで規定されています。  
  
 JDBC Driver 3.0 以降では、このメソッドの動作は **sendTimeAsDatetime** 接続プロパティ ([接続プロパティの設定](../../../connect/jdbc/setting-the-connection-properties.md)) によって変更されます。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [SQLServerDataSource Sqlserverdatasource.setsendtimeasdatetime](../../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md)。  
  
 詳細については、「 [java .sql の時刻値をサーバーに送信する方法の構成](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [setTime メソッド &#40;SQLServerPreparedStatement&#41;](../../../connect/jdbc/reference/settime-method-sqlserverpreparedstatement.md)   
 [SQLServerPreparedStatement のメンバー](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement クラス](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
