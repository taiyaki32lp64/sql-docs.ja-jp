---
title: 暗号化を使用した接続 |Microsoft Docs
ms.custom: ''
ms.date: 09/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: vanto
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ec91fa8a-ab7e-4c1e-a05a-d7951ddf33b1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cff4228404690147d97a44f6f5dd43b1a180153c
ms.sourcegitcommit: fd3e81c55745da5497858abccf8e1f26e3a7ea7d
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 10/01/2019
ms.locfileid: "71713294"
---
# <a name="connecting-with-encryption"></a>暗号化を使用した接続
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  この記事の例では、Java アプリケーションでトランスポート層セキュリティ (TLS) 暗号化を使用できるようにする接続文字列プロパティの使用方法について説明します。 これらの新しい接続文字列プロパティ (**encrypt**、**trustServerCertificate**、**trustStore**、**trustStorePassword**、**hostNameInCertificate** など) の詳細については、「[接続プロパティの設定](../../connect/jdbc/setting-the-connection-properties.md)」を参照してください。  
  
 **encrypt** プロパティが **true** に設定され、**trustServerCertificate** プロパティが **true** に設定されている場合、[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] では [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の TLS 証明書が検証されません。 これは、通常、テスト環境 ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスが自己署名入りの証明書しか備えていない環境など) で接続を許可する場合に必要になります。  
  
 次のコード例では、接続文字列内に **trustServerCertificate** プロパティを設定する方法を示します。  
  
```java
String connectionUrl =   
    "jdbc:sqlserver://localhost:1433;" +  
     "databaseName=AdventureWorks;integratedSecurity=true;" +  
     "encrypt=true;trustServerCertificate=true";  
```  
  
 **encrypt** プロパティが **true** に設定され、**trustServerCertificate** プロパティが **false** に設定されている場合、[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] では [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の TLS 証明書が検証されます。 サーバー証明書の検証は、TLS ハンドシェイクの一部であり、接続先のサーバーが適切なサーバーであることが保証されます。 サーバー証明書を検証するには、**trustStore** 接続プロパティと **trustStorePassword** 接続プロパティを明示的に使用するか、または基になる Java 仮想マシン (JVM) のトラスト ストアを暗黙的に使用して、接続時にトラスト マテリアルを提供する必要があります。  
  
 **trustStore** プロパティでは、証明書の trustStore ファイルへのパス (ファイル名を含む) を指定します。このファイルには、クライアントが信頼する証明書の一覧が含まれています。 **trustStorePassword** プロパティでは、trustStore データの整合性の確認に使用するパスワードを指定します。 JVM の既定のトラストストアの使用方法の詳細については、「[クライアントの暗号化の構成](../../connect/jdbc/configuring-the-client-for-ssl-encryption.md)」を参照してください。  
  
 次のコード例では、接続文字列内に **trustStore** プロパティと **trustStorePassword** プロパティを設定する方法を示します。  
  
```java
String connectionUrl =   
    "jdbc:sqlserver://localhost:1433;" +  
     "databaseName=AdventureWorks;integratedSecurity=true;" +  
     "encrypt=true; trustServerCertificate=false;" +  
     "trustStore=storeName;trustStorePassword=storePassword";  
```  
  
 JDBC Driver には、サーバーのホスト名を指定するための追加プロパティである **hostNameInCertificate** が用意されています。 このプロパティの値は、証明書の subject プロパティと一致する必要があります。  
  
 次のコード例では、接続文字列内で **hostNameInCertificate** プロパティを使用する方法を示します。  
  
```java
String connectionUrl =   
    "jdbc:sqlserver://localhost:1433;" +  
     "databaseName=AdventureWorks;integratedSecurity=true;" +  
     "encrypt=true; trustServerCertificate=false;" +  
     "trustStore=storeName;trustStorePassword=storePassword" +  
     "hostNameInCertificate=hostName";  
```  
  
> [!NOTE]  
>  または、[SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md) クラスによって提供される適切な **setter** メソッドを使用して、接続プロパティの値を設定することもできます。  
  
 **Encrypt**プロパティが**true**に設定され、 **trustservercertificate**プロパティが**false**に設定されていて、接続文字列のサーバー名が TLS 証明書のサーバー名と一致しない場合、次のエラーが発生します。発行済み: `The driver couldn't establish a secure connection to SQL Server by using Secure Sockets Layer (SSL) encryption. Error: "java.security.cert.CertificateException: Failed to validate the server name in a certificate during Secure Sockets Layer (SSL) initialization."`。 バージョン7.2 の場合、ドライバーでは、TLS 証明書のサーバー名の左端のラベルにあるワイルドカードパターンマッチングがサポートされます。

## <a name="see-also"></a>参照

 [暗号化を使用し](../../connect/jdbc/using-ssl-encryption.md)た[JDBC driver アプリケーションのセキュリティ保護](../../connect/jdbc/securing-jdbc-driver-applications.md)