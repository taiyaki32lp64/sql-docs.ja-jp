---
title: truncate メソッド (SQLServerBlob) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerBlob.truncate
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ef181e04-003a-442a-9b7e-0c508a7cc873
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3195b0eafb5eb48f7ec6b159fef05036d6efd7df
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67968491"
---
# <a name="truncate-method-sqlserverblob"></a>truncate メソッド (SQLServerBlob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  BLOB を指定された長さに切り捨てます。  
  
## <a name="syntax"></a>構文  
  
```  
  
public void truncate(long len)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *len*  
  
 BLOB の新しい長さです。  
  
## <a name="exceptions"></a>例外  
 java.sql.SQLException  
  
## <a name="remarks"></a>Remarks  
 この truncate メソッドは、java.sql.Blob インターフェイスの truncate メソッドで規定されています。  
  
## <a name="see-also"></a>参照  
 [SQLServerBlob のメソッド](../../../connect/jdbc/reference/sqlserverblob-methods.md)   
 [SQLServerBlob のメンバー](../../../connect/jdbc/reference/sqlserverblob-members.md)   
 [SQLServerBlob クラス](../../../connect/jdbc/reference/sqlserverblob-class.md)  
  
  
