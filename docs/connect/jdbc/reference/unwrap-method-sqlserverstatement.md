---
title: ラップ解除メソッド (SQLServerStatement) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ce680176-ef04-4e44-bb6c-ec50bd06e7e6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d9b57c0d984198a40e04c1dfe6eeb6ce946d2d13
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67985605"
---
# <a name="unwrap-method-sqlserverstatement"></a>unwrap メソッド (SQLServerStatement)
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
 [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md) メソッドは、JDBC 4.0 仕様で導入された java.sql.Wrapper インターフェイスで定義されています。  
  
 アプリケーションは [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] に固有の JDBC API 拡張機能にアクセスする必要がある場合があります。 unwrap メソッドは、クラスがベンダー拡張を公開する場合、このオブジェクトが拡張するパブリック クラスへのアンラッピングをサポートします。  
  
 このメソッドが呼び出されると、オブジェクトは [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) クラスにアンラップされます。  
  
 コード例については、「[大きなデータサンプルの更新](../../../connect/jdbc/updating-large-data-sample.md)」または「 [ &#40;メソッド SQLServerCallableStatement&#41;のラップ](../../../connect/jdbc/reference/unwrap-method-sqlservercallablestatement.md)解除」を参照してください。  
  
 詳細については、「[ラッパーとインターフェイス](../../../connect/jdbc/wrappers-and-interfaces.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [isWrapperFor メソッド &#40;SQLServerStatement&#41;](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverstatement.md)   
 [SQLServerStatement のメンバー](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement クラス](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
