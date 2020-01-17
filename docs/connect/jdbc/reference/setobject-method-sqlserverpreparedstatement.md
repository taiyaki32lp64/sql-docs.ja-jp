---
title: setObject メソッド (SQLServerPreparedStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.setObject
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 93a2b22c-82b4-48c7-a428-369ebe98a372
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 27993632c5aa6f1ab334c02c123a1984d3408b6e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67973294"
---
# <a name="setobject-method-sqlserverpreparedstatement"></a>setObject メソッド (SQLServerPreparedStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  渡されたオブジェクトを使用して、指定されたパラメーターの値を設定します。  
  
 JDBC Driver 3.0 以降では、このメソッドの動作は **sendTimeAsDatetime** 接続プロパティ ([接続プロパティの設定](../../../connect/jdbc/setting-the-connection-properties.md)) によって変更されます。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [SQLServerDataSource Sqlserverdatasource.setsendtimeasdatetime](../../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md)。  
  
 詳細については、「 [java .sql の時刻値をサーバーに送信する方法の構成](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md)」を参照してください。  
  
## <a name="overload-list"></a>オーバーロードの一覧  
  
|[オブジェクト名]|[説明]|  
|----------|-----------------|  
|[setObject (int, java.lang.Object)](../../../connect/jdbc/reference/setobject-method-int-java-lang-object.md)|渡されたオブジェクトを使用して、指定されたパラメーターの値を設定します。|  
|[setObject (int, java.lang.Object, int)](../../../connect/jdbc/reference/setobject-method-int-java-lang-object-int.md)|渡されたオブジェクトと変換先の型を使用して、指定されたパラメーターの値が設定されます。|  
|[setObject (int, java.lang.Object, int, int)](../../../connect/jdbc/reference/setobject-method-int-java-lang-object-int-int.md)|渡されたオブジェクト、変換先の型、および小数点以下桁数を使用して、指定されたパラメーターの値が設定されます。|  
  
## <a name="see-also"></a>参照  
 [SQLServerPreparedStatement のメンバー](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement クラス](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
