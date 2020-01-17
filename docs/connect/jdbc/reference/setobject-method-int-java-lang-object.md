---
title: setObject (int, java.lang.Object) メソッド | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.setObject (int, java.lang.Object)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 61f19faa-3006-4a1c-974c-55951e3b3000
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e4ab210a30080472a777d151695a04ec49ff1041
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67973384"
---
# <a name="setobject-method-int-javalangobject"></a>setObject (int, java.lang.Object) メソッド
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  渡されたオブジェクトを使用して、指定されたパラメーターの値を設定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public final void setObject(int index,  
                            java.lang.Object obj)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *index*  
  
 パラメーターの番号を示す **int** です。  
  
 *obj*  
  
 オブジェクト。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 この setObject メソッドは、java.sql.PreparedStatement インターフェイスの setObject メソッドで指定されています。  
  
 この setObject メソッドを呼び出す前に、指定したパラメーターが次のいずれかのメソッドを使用してアプリケーションで設定されている場合があります。  
  
-   SQLServerPreparedStatement クラスまたは SQLServerCallableStatement クラスの set\<Type> メソッド  
  
-   SQLServerPreparedStatement クラスまたは SQLServerCallableStatement クラスの setNull メソッド  
  
-   SQLServerCallableStatement クラスの[Registeroutparameter](../../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md)メソッド  
  
 このような場合、パラメーターの型が自動的に設定されます。 アプリケーションで obj 値を NULL に設定してこの setObject メソッドを呼び出すと、ドライバーでは、パラメーターの型は以前に呼び出されたメソッドで設定された型であると見なされます。  
  
 obj 値が NULL で、そのパラメーターの型情報を特定できない場合、この setObject メソッドは、指定したパラメーターを CHAR に変換してからデータベースに送信します。  
  
 JDBC Driver 3.0 以降では、このメソッドの動作は **sendTimeAsDatetime** 接続プロパティ ([接続プロパティの設定](../../../connect/jdbc/setting-the-connection-properties.md)) によって変更されます。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [SQLServerDataSource Sqlserverdatasource.setsendtimeasdatetime](../../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md)。  
  
 詳細については、「 [java .sql の時刻値をサーバーに送信する方法の構成](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [setObject メソッド &#40;SQLServerPreparedStatement&#41;](../../../connect/jdbc/reference/setobject-method-sqlserverpreparedstatement.md)   
 [SQLServerPreparedStatement のメンバー](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement クラス](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
