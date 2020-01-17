---
title: ISQLServerConnection Interface |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 031c01e2-2c65-4fe4-9700-fdbcc7a39f30
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2fbe3b6c1721720720b06bdcf4122a289589e639
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67977454"
---
# <a name="isqlserverconnection-interface"></a>ISQLServerConnection インターフェイス
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  [!INCLUDE[msCoName](../../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データベースへの JDBC 接続を表します。 このインターフェイスは [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC Driver 3.0 で追加されました。  
  
 **パッケージ:** com.microsoft.sqlserver.jdbc  
  
 **継承:** java.sql.Connection  
  
## <a name="syntax"></a>構文  
  
```  
  
public interface ISQLServerConnection  
```  
  
## <a name="remarks"></a>Remarks  
 このインターフェイスは、 [SQLServerConnection クラス](../../../connect/jdbc/reference/sqlserverconnection-class.md)によって実装されます。  
  
 このインターフェイスでは、次の [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 固有のフィールドが公開されます。  
  
|フィールド|詳細については、「|  
|-----------|-------------------------------|  
|public final static int TRANSACTION_SNAPSHOT|[TRANSACTION_SNAPSHOT](../../../connect/jdbc/reference/transaction-snapshot-field-sqlserverconnection.md)|  
|public UUID getClientConnectionId()|[getClientConnectionID()](../../../connect/jdbc/reference/getclientconnectionid-method-sqlserverconnection.md)|  
  
## <a name="see-also"></a>参照  
 [JDBC Driver API リファレンス](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
