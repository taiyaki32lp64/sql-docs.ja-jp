---
title: ラッパーとインターフェイス |Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 27fc9b72-9f21-4728-abcb-5c015f28a6ab
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3a74f5ccd8a36527dd7c37fc02150d11be632ba9
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2019
ms.locfileid: "69025579"
---
# <a name="wrappers-and-interfaces"></a>ラッパーとインターフェイス

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] は、クラスのプロキシを作成できるインターフェイスと、[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] に固有の JDBC API 拡張機能に対し、プロキシ インターフェイス経由でアクセスするためのラッパーをサポートします。

## <a name="wrappers"></a>ラッパー

[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] は、java.sql.Wrapper インターフェイスをサポートします。 このインターフェイスには、[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] に固有の JDBC API 拡張機能に対し、プロキシ インターフェイス経由でアクセスするためのメカニズムが備わっています。

**IsWrapperFor インターフェイスでは、2つのメソッドが定義され**て**います。これは、** とラップ解除です。 **isWrapperFor** は、指定された入力オブジェクトに、このインターフェイスが実装されているかどうかをチェックするメソッドです。 **unwrap** メソッドは、このインターフェイスを実装するオブジェクトを返します。このメソッドから返されたオブジェクトを使用することで、[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 固有のメソッドにアクセスできます。

**isWrapperFor**メソッドと**ラップ**解除メソッドは次のように公開されます。

- [isWrapperFor メソッド &#40;SQLServerCallableStatement&#41;](../../connect/jdbc/reference/iswrapperfor-method-sqlservercallablestatement.md)

- [unwrap メソッド &#40;SQLServerCallableStatement&#41;](../../connect/jdbc/reference/unwrap-method-sqlservercallablestatement.md)

- [isWrapperFor メソッド &#40;SQLServerConnectionPoolDataSource&#41;](../../connect/jdbc/reference/iswrapperfor-method-sqlserverconnectionpooldatasource.md)

- [unwrap メソッド &#40;SQLServerConnectionPoolDataSource&#41;](../../connect/jdbc/reference/unwrap-method-sqlserverconnectionpooldatasource.md)

- [isWrapperFor メソッド &#40;SQLServerDataSource&#41;](../../connect/jdbc/reference/iswrapperfor-method-sqlserverdatasource.md)

- [SQLServerDataSource メソッド&#40;のラップ解除&#41;](../../connect/jdbc/reference/unwrap-method-sqlserverdatasource.md)

- [isWrapperFor メソッド &#40;SQLServerPreparedStatement&#41;](../../connect/jdbc/reference/iswrapperfor-method-sqlserverpreparedstatement.md)

- [unwrap メソッド &#40;SQLServerPreparedStatement&#41;](../../connect/jdbc/reference/unwrap-method-sqlserverpreparedstatement.md)

- [isWrapperFor メソッド &#40;SQLServerStatement&#41;](../../connect/jdbc/reference/iswrapperfor-method-sqlserverstatement.md)

- [SQLServerStatement メソッド&#40;のラップ解除&#41;](../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md)

- [isWrapperFor メソッド &#40;SQLServerXADataSource&#41;](../../connect/jdbc/reference/iswrapperfor-method-sqlserverxadatasource.md)

- [SQLServerXADataSource メソッド&#40;のラップ解除&#41;](../../connect/jdbc/reference/unwrap-method-sqlserverxadatasource.md)

## <a name="interfaces"></a>インターフェイス

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] JDBC Driver 3.0 以降では、関連付けられたクラスからドライバー固有のメソッドにアクセスするアプリケーション サーバーでインターフェイスを使用できます。 アプリケーション サーバーでは、プロキシを作成し、インターフェイスから [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 固有の機能を公開することで、クラスをラップできます。 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] では、アプリケーション サーバーがクラスのプロキシを作成できるように、[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 固有のメソッドと定数を持つインターフェイスをサポートします。

このインターフェイスは標準の Java インターフェイスから派生するため、オブジェクトをアンラップしてドライバー固有の機能または汎用 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 機能にアクセスした後で、同じオブジェクトを使用できます。

次のインターフェイスが追加されています。

- [ISQLServerCallableStatement](../../connect/jdbc/reference/isqlservercallablestatement-interface.md)

- [ISQLServerConnection](../../connect/jdbc/reference/isqlserverconnection-interface.md)

- [ISQLServerDataSource](../../connect/jdbc/reference/isqlserverdatasource-interface.md)

- [ISQLServerPreparedStatement](../../connect/jdbc/reference/isqlserverpreparedstatement-interface.md)

- [ISQLServerResultSet](../../connect/jdbc/reference/isqlserverresultset-interface.md)

- [ISQLServerStatement](../../connect/jdbc/reference/isqlserverstatement-interface.md)

## <a name="example"></a>例

### <a name="description"></a>[説明]

このサンプルは、DataSource オブジェクトから [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 固有の関数にアクセスする方法を示しています。 この DataSource クラスはアプリケーション サーバーによってラップされた可能性があります。 JDBC Driver 固有の関数または定数にアクセスするには、データソースを ISQLServerDataSource インターフェイスにアンラップし、このインターフェイスで宣言された関数を使用できます。

### <a name="code"></a>コード

```java
import javax.sql.*;  
import java.sql.*;  
import com.microsoft.sqlserver.jdbc.*;  

public class UnWrapTest {  
   public static void main(String[] args) {  
      // This is a test.  This DataSource object could be something from an appserver
      // which has wrapped the real SQLServerDataSource with its own wrapper  
      SQLServerDataSource ds = new SQLServerDataSource();  
      checkSendStringParametersAsUnicode(ds);  
   }  

   // Unwrap to the ISQLServerDataSource interface to access the getSendStringParametersAsUnicode function  
   static void checkSendStringParametersAsUnicode(DataSource ds) {  
      try {  
         final ISQLServerDataSource sqlServerDataSource = ds.unwrap(ISQLServerDataSource.class);  
         boolean sendStringParametersAsUnicode = sqlServerDataSource.getSendStringParametersAsUnicode();  

         System.out.println("Send string as parameter value is:-" + sendStringParametersAsUnicode);  

      } catch (SQLException sqlE) {  
         System.out.println("Exception:-" + sqlE);  
      }  
   }  
}  
```

## <a name="see-also"></a>参照

[JDBC ドライバーのデータ型について](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)
