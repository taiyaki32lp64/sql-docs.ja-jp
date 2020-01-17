---
title: getLoginTimeout メソッド (SQLServerDataSource) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getLoginTimeout
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 316f067c-9e08-456a-af19-b80b0bbd4a5c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5fe82d2709aa8efa32408a9d9d86f0f660bed823
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67982548"
---
# <a name="getlogintimeout-method-sqlserverdatasource"></a>getLoginTimeout メソッド (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  接続の試行中に [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) オブジェクトが待機する秒数を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public int getLoginTimeout()  
```  
  
## <a name="return-value"></a>戻り値  
 待機する秒数を表す **int** 値です。  
  
## <a name="remarks"></a>Remarks  
 アプリケーションがタイムアウト値を明示的に指定しない場合、このメソッドは既定値の 15 秒を返します。  
  
 この getLoginTimeout メソッドは、javax.mail インターフェイスの getLoginTimeout メソッドによって指定されます。  
  
## <a name="see-also"></a>参照  
 [SQLServerDataSource のメンバー](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource クラス](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
