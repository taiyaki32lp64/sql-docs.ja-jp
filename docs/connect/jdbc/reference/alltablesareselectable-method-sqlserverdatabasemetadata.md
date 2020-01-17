---
title: AllSQLServerDatabaseMetaData (選択可能) メソッド () |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.allTablesAreSelectable
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: eb340450-45a7-49c8-84bc-1b9dd5ee842f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f2fa61d7239858cb3479e7eeaa730e4197bf6bc5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67955867"
---
# <a name="alltablesareselectable-method-sqlserverdatabasemetadata"></a>allTablesAreSelectable メソッド (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  現在のユーザーが、[getTables](../../../connect/jdbc/reference/gettables-method-sqlserverdatabasemetadata.md) メソッドで返されたすべてのテーブルを SELECT ステートメントで使用するアクセス許可を持っているかどうかを取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public boolean allTablesAreSelectable()  
```  
  
## <a name="return-value"></a>戻り値  
 ユーザーがすべてのテーブルを使用するためのアクセス許可を持っている場合は **true** です。 それ以外の場合は、 **false**です。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 この Alltablesareselectable 可能なメソッドは、java メタデータインターフェイスの allTablesAreSelectable 可能なメソッドによって指定されます。  
  
## <a name="see-also"></a>参照  
 [SQLServerDatabaseMetaData のメソッド](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData のメンバー](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData クラス](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
