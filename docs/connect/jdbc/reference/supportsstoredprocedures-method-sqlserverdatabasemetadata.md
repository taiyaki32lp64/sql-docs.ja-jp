---
title: supportsStoredProcedures メソッド |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.supportsStoredProcedures
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 776ff53a-8bf3-4864-a7b7-170fdef1a87b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: dd3c71aa058534342ddd70fdf1ae5256fb75e708
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67968766"
---
# <a name="supportsstoredprocedures-method-sqlserverdatabasemetadata"></a>supportsStoredProcedures メソッド (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  データベースがストアド プロシージャのエスケープ構文を使用するストアド プロシージャの呼び出しをサポートするかどうかを取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public boolean supportsStoredProcedures()  
```  
  
## <a name="return-value"></a>戻り値  
 サポートされている場合は**true** 。 それ以外の場合は、 **false**です。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 この supportsStoredProcedures メソッドは、supportsStoredProcedures メソッドによって、java メタデータインターフェイスで指定されます。  
  
## <a name="see-also"></a>参照  
 [SQLServerDatabaseMetaData のメソッド](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData のメンバー](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData クラス](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
