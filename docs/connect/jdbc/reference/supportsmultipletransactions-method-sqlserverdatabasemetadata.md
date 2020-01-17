---
title: supportsMultipleTransactions メソッド (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.supportsMultipleTransactions
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 34ff8dcb-5487-46d1-a4c1-25e33eb3eee4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e16b4f5590057424cfe67491cf4943399d54c01c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67969184"
---
# <a name="supportsmultipletransactions-method-sqlserverdatabasemetadata"></a>supportsMultipleTransactions メソッド (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  データベースが、異なる接続で複数のトランザクションを同時に開くことができるかどうかを取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public boolean supportsMultipleTransactions()  
```  
  
## <a name="return-value"></a>戻り値  
 サポートされている場合は**true** 。 それ以外の場合は、 **false**です。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 この Supports多重トランザクションメソッドは、java メタデータインターフェイスの Supports多重トランザクションメソッドによって指定されます。  
  
## <a name="see-also"></a>参照  
 [SQLServerDatabaseMetaData のメソッド](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData のメンバー](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData クラス](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
