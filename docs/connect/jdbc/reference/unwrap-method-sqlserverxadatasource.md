---
title: ラップ解除メソッド (SQLServerXADataSource) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d97c99b3-2224-4abb-8b32-40aff49fe759
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3f7406bce05278cad83b28b14f95a241b3eff026
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67986047"
---
# <a name="unwrap-method-sqlserverxadatasource"></a>unwrap メソッド (SQLServerXADataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  指定されたインターフェイスを実装するオブジェクトを返します。このメソッドから返されたオブジェクトを使用することで、[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 固有のメソッドにアクセスできます。  
  
## <a name="syntax"></a>構文  
  
```  
  
public <T> T unwrap(Class<T> iface)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *iface*  
  
 インターフェイスを定義する **T** 型のクラスです。  
  
## <a name="return-value"></a>戻り値  
 指定されたインターフェイスを実装するオブジェクトです。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverxadatasource.md) メソッドは、JDBC 4.0 仕様で導入された java.sql.Wrapper インターフェイスで定義されています。  
  
 アプリケーションは [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] に固有の JDBC API 拡張機能にアクセスする必要がある場合があります。 unwrap メソッドは、クラスがベンダー拡張を公開する場合、このオブジェクトが拡張するパブリック クラスへのアンラッピングをサポートします。  
  
 [SQLServerXADataSource](../../../connect/jdbc/reference/sqlserverxadatasource-class.md) クラスは、[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) クラスから拡張された [SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md) クラスを拡張します。 このメソッドが呼び出されると、オブジェクトは [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)、[SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md)、および [SQLServerXADataSource](../../../connect/jdbc/reference/sqlserverxadatasource-class.md) の各クラスにアンラップされます。  
  
 詳細については、「[ラッパーとインターフェイス](../../../connect/jdbc/wrappers-and-interfaces.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [SQLServerXADataSource のメソッド](../../../connect/jdbc/reference/sqlserverxadatasource-methods.md)   
 [SQLServerXADataSource のメンバー](../../../connect/jdbc/reference/sqlserverxadatasource-members.md)   
 [SQLServerXADataSource クラス](../../../connect/jdbc/reference/sqlserverxadatasource-class.md)  
  
  
