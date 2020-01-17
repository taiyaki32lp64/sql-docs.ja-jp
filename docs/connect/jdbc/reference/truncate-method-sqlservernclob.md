---
title: truncate メソッド (SQLServerNClob) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b7e8210d-a724-4bae-832a-ae4c63031c9c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f9ed19679cb1a173d015152a006f55660fe9f826
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67968464"
---
# <a name="truncate-method-sqlservernclob"></a>truncate メソッド (SQLServerNClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  **NCLOB** を指定された長さに切り捨てます。  
  
## <a name="syntax"></a>構文  
  
```  
  
public void truncate(long len)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *len*  
  
 **NCLOB** 値を切り捨てた後に残す長さ (文字数) です。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 この truncate メソッドは、java.sql.NClob インターフェイスの truncate メソッドで規定されています。  
  
## <a name="see-also"></a>参照  
 [SQLServerNClob のメソッド](../../../connect/jdbc/reference/sqlservernclob-methods.md)   
 [SQLServerNClob のメンバー](../../../connect/jdbc/reference/sqlservernclob-members.md)   
 [SQLServerNClob クラス](../../../connect/jdbc/reference/sqlservernclob-class.md)  
  
  
