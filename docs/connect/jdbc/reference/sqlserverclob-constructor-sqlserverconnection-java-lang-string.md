---
title: SQLServerClob コンストラクター (SQLServerConnection, java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.SQLServerClob (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7058f4f7-ef3e-4d62-90d1-79299708b1eb
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7a539ef893788be9e0200b9f412f8c3ed7652b26
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67971802"
---
# <a name="sqlserverclob-constructor-sqlserverconnection-javalangstring"></a>SQLServerClob (SQLServerConnection, java.lang.String) コンストラクター
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) オブジェクトとデータの文字列が渡されたときに、[SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-class.md) クラスの新しいインスタンスを初期化します。  
  
> [!NOTE]  
>  このメソッドは、JDBC Driver Version 2.0 では非推奨とされました。 代わりに、[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) クラスの [createClob](../../../connect/jdbc/reference/createclob-method-sqlserverconnection.md) メソッドを使用してください。  
  
## <a name="syntax"></a>構文  
  
```  
  
public SQLServerClob(SQLServerConnection connection,  
                     java.lang.String data)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *connection*  
  
 SQLServerConnection オブジェクト。  
  
 *data*  
  
 CLOB データです。  
  
## <a name="see-also"></a>参照  
 [SQLServerClob のコンストラクター](../../../connect/jdbc/reference/sqlserverclob-constructors.md)   
 [SQLServerClob メンバー](../../../connect/jdbc/reference/sqlserverclob-members.md)   
 [SQLServerClob クラス](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  
