---
title: SQLServerDataSourceObjectFactory クラス |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b616632b-5987-470d-b36c-b22fa9213145
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cf4c90644282ff420e064e7a7b5b99a93c257194
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67971379"
---
# <a name="sqlserverdatasourceobjectfactory-class"></a>SQLServerDataSourceObjectFactory クラス
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  JNDI (Java Naming and Directory Interface) からのデータ ソースを生成するオブジェクト ファクトリを表します。  
  
 **パッケージ:** com.microsoft.sqlserver.jdbc  
  
 **拡張:** java.lang.Object  
  
 **実装:** javax.naming.spi.ObjectFactory  
  
## <a name="syntax"></a>構文  
  
```  
  
public class SQLServerDataSourceObjectFactory  
```  
  
## <a name="remarks"></a>Remarks  
 このクラスはすべてのデータ ソース クラスに継承されます。 Referenceable インターフェイスのサポートの一部として、[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] では、ObjectFactory を実装するこのクラスが公開されています。 Java アプリケーション サーバーはデータ ソース クラスで getReference を呼び出し、それによって、内部的にクラス名をクラス ファクトリとして使用する Reference オブジェクトが作成されます。  
  
 Java アプリケーションサーバーが参照オブジェクトを逆参照する必要がある場合は、SQLServerDataSourceObjectFactory オブジェクトのインスタンスを作成し、 [Getobjectinstance](../../../connect/jdbc/reference/getobjectinstance-method-sqlserverdatasourceobjectfactory.md)メソッドを呼び出して、参照オブジェクトを渡してデータソースを取得します。instance.  
  
## <a name="see-also"></a>参照  
 [SQLServerDataSourceObjectFactory のメンバー](../../../connect/jdbc/reference/sqlserverdatasourceobjectfactory-members.md)   
 [JDBC Driver API リファレンス](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
