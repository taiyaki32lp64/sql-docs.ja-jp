---
title: getMaxColumnsInGroupBy メソッド (SQLServerDatabaseMetaData) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getMaxColumnsInGroupBy
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: a59cfe98-c0f4-46ad-9243-62aa56855f1a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d745712e5a8c4b59ea85c1a9b19c2e247c166be3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67982305"
---
# <a name="getmaxcolumnsingroupby-method-sqlserverdatabasemetadata"></a>getMaxColumnsInGroupBy メソッド (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  データベースで GROUP BY 句に許容される最大の列数を取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public int getMaxColumnsInGroupBy()  
```  
  
## <a name="return-value"></a>戻り値  
 許容される最大の列数を示す **int** です。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 この getMaxColumnsInGroupBy メソッドは、java メタデータインターフェイスの getMaxColumnsInGroupBy メソッドによって指定されます。  
  
## <a name="see-also"></a>参照  
 [SQLServerDatabaseMetaData のメソッド](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData のメンバー](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData クラス](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
