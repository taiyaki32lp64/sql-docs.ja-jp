---
title: setLoginTimeout メソッド (SQLServerDataSource) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setLoginTimeout
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b63d1cf4-dc1b-4e35-9a56-50436642eaaf
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a64bc643e8d5a9d820b2bcd9cd307f033a869d7c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67974088"
---
# <a name="setlogintimeout-method-sqlserverdatasource"></a>setLoginTimeout メソッド (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  接続の試行中に [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) オブジェクトが待機する秒数を設定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public void setLoginTimeout(int loginTimeout)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *loginTimeout*  
  
 待機する秒数を表す **int** 値です。 0 は、タイムアウトが既定のシステム タイムアウトであることを示します。既定のシステム タイムアウトは、既定では 15 秒に指定されています。  
  
## <a name="remarks"></a>Remarks  
 この setLoginTimeout メソッドは、javax.mail インターフェイスの setLoginTimeout メソッドによって指定されます。  
  
## <a name="see-also"></a>参照  
 [SQLServerDataSource のメンバー](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource クラス](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
