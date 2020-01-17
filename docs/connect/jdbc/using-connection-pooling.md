---
title: 接続プールを使用する |Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 699d4e8a-34bf-4c60-b0d5-4a10dad6084a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 69aa4d7f29d8c7963f9b300f868bc8265cde2fd0
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2019
ms.locfileid: "69026371"
---
# <a name="using-connection-pooling"></a>接続プールの使用

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] は、Java Platform, Enterprise Edition (Java EE) の接続プールをサポートします。 JDBC ドライバーは、ミドルウェア ベンダーが提供し JDBC 3.0 に準拠する接続プールの実装に参加できるように、JDBC 3.0 に必要なインターフェイスを実装しています。 Java EE アプリケーション サーバーのようなミドルウェアの多くは、準拠した接続プール機能を備えています。 JDBC ドライバーは、これらの環境でプールされた接続に参加します。  
  
> [!NOTE]  
> JDBC ドライバーは Java EE 接続プールをサポートしますが、独自のプール実装は提供しません。 このドライバーでは、接続の管理をサードパーティの Java アプリケーション サーバーに依存しています。  
  
## <a name="remarks"></a>Remarks

接続プールを実装するためのクラスは次のとおりです。  
  
| クラス                                                           | 実装                                                    | [説明]                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| --------------------------------------------------------------- | ------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| com.microsoft.sqlserver.jdbc. SQLServerXADataSource             | javax.sql.ConnectionPoolDataSource および javax.sql.XADataSource | Java EE サーバーはすべての JDBC 3.0 プールおよび XA インターフェイスを実装するので、常に [SQLServerXADataSource](../../connect/jdbc/reference/sqlserverxadatasource-class.md) クラスを使用することをお勧めします。                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| com.microsoft.sqlserver.jdbc. SQLServerConnectionPoolDataSource | javax.sql.ConnectionPoolDataSource                            | このクラスは、Java EE アプリケーション サーバーが物理接続による接続プールを作成するための接続ファクトリです。 Java EE ベンダーの構成で、javax.sql.ConnectionPoolDataSource を実装するクラスが必要な場合は、クラス名に [SQLServerConnectionPoolDataSource](../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md) を指定します。 通常、代わりに [SQLServerXADataSource](../../connect/jdbc/reference/sqlserverxadatasource-class.md) クラスを使用することをお勧めします。このクラスはプールと XA インターフェイスの両方を実装し、多くの Java EE サーバー構成で検証されているためです。 |
  
 JDBC のアプリケーション コードでは、プールの利点を最大限に活かすため、常に接続を明示的に閉じる必要があります。 アプリケーションが接続を明示的に閉じると、プール実装は直ちに接続を再利用することができます。 接続が開いたままの場合、他のアプリケーションはその接続を再利用することができません。 アプリケーションは、`finally` 構文を使用して、例外が発生した場合でもプールされた接続が確実に閉じられるようにします。  
  
> [!NOTE]  
> 現在 JDBC ドライバーは、接続をプールに返すとき sp_reset_connection ストアド プロシージャを呼び出しません。 ただし、接続を元の状態に戻すときは、サードパーティの Java アプリケーション サーバーに依存します。  
  
## <a name="see-also"></a>参照

[JDBC ドライバーによる SQL Server への接続](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)  
