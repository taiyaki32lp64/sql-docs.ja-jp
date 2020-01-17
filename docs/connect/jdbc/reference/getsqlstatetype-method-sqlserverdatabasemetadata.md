---
title: getSQLStateType メソッド (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getSQLStateType
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ee4d6751-68a3-4d04-831c-e6d704c59e63
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 76faa3bcaccac4f75d95dc49276c669a5631b5a8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67979731"
---
# <a name="getsqlstatetype-method-sqlserverdatabasemetadata"></a>getSQLStateType メソッド (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  SQLException.getSQLState メソッドによって返される SQLSTATE が、X/Open (現在は Open Group)、SQL CLI、SQL99 (JDBC 3.0)、SQL:2003 (JDBC 4.0) のいずれであるかを示します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public int getSQLStateType()  
```  
  
## <a name="return-value"></a>戻り値  
 SQLSTATE の種類を示す **int** です。次のいずれかの値になります。  
  
-   Java Runtime Environment バージョン5.0 の場合: **xopenStates**接続プロパティが**true**に設定されている場合、このメソッドは Databasemetadata. sqlstatexopen を返します。 それ以外の場合は、sqlStateSQL99 です。  
  
-   Java Runtime Environment バージョン6.0 の場合: **xopenStates**接続プロパティが**true**に設定されている場合、このメソッドは Databasemetadata. sqlstatexopen を返します。 それ以外の場合、DatabaseMetaData。 sqlStateSQL。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 この getSQLStateType メソッドは、java メタデータインターフェイスの getSQLStateType メソッドによって指定されます。  
  
## <a name="see-also"></a>参照  
 [SQLServerDatabaseMetaData のメソッド](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData のメンバー](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData クラス](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
