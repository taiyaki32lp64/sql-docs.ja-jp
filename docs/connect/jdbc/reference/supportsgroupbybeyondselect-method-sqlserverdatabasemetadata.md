---
title: supportsGroupByBeyondSelect メソッド (SQLServerDatabaseMetaData) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.supportsGroupByBeyondSelect
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: eadd2c37-d9ec-4b47-a91e-ed90b1eaf4b4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c38f17451149e9206cf12329e5ffef314eac7480
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67969385"
---
# <a name="supportsgroupbybeyondselect-method-sqlserverdatabasemetadata"></a>supportsGroupByBeyondSelect メソッド (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  SELECT ステートメント内のすべての列が GROUP BY 句に含まれる場合に、データベースが GROUP BY 句で SELECT ステートメントに含まれていない列の使用をサポートするかどうかを取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public boolean supportsGroupByBeyondSelect()  
```  
  
## <a name="return-value"></a>戻り値  
 サポートされている場合は**true** 。 それ以外の場合は、 **false**です。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 この supportsGroupByBeyondSelect メソッドは、supportsGroupByBeyondSelect メソッドによって、java メタデータインターフェイスで指定されます。  
  
## <a name="see-also"></a>参照  
 [SQLServerDatabaseMetaData のメソッド](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData のメンバー](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData クラス](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
