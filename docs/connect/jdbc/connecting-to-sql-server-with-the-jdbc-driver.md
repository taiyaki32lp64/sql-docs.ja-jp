---
title: JDBC ドライバーによる SQL Server への接続 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 94bcfbe3-f00e-4774-bda8-bb7577518fec
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c8dbf7a415d413e0a9fad431013255ff48417687
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028177"
---
# <a name="connecting-to-sql-server-with-the-jdbc-driver"></a>JDBC ドライバーによる SQL Server への接続
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] を使用して行う最も基本的な操作の 1 つは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースへの接続を確立することです。 データベースとのやり取りは、すべて [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) オブジェクトを介して行われます。JDBC ドライバーのアーキテクチャは非常にフラットであるため、注目に値するほとんどすべての動作が SQLServerConnection オブジェクトに関連します。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が IPv6 ポートのみで待機している場合は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] への接続に IPv4 ではなく IPv6 を使用するために java.net.preferIPv6Addresses システム プロパティを設定します。  
  
```java
System.setProperty("java.net.preferIPv6Addresses", "true");  
```  
  
 このセクションのトピックでは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースへの接続を確立し、操作する方法について説明します。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
|トピック|[説明]|  
|-----------|-----------------|  
|[接続 URL の構築](../../connect/jdbc/building-the-connection-url.md)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースに接続するための接続 URL の作成方法について説明します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースの名前付きインスタンスへの接続についても説明します。|  
|[接続プロパティの設定](../../connect/jdbc/setting-the-connection-properties.md)|さまざまな接続プロパティについて、および [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースに接続する際にそれらをどのように使用するかについて説明します。|  
|[データ ソースのプロパティの設定](../../connect/jdbc/setting-the-data-source-properties.md)|Java Platform, Enterprise Edition (Java EE) 環境でデータ ソースを使用する方法について説明します。|  
|[接続の操作](../../connect/jdbc/working-with-a-connection.md)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースへの接続をインスタンス化するためのさまざまな方法について説明します。|  
|[接続プールの使用](../../connect/jdbc/using-connection-pooling.md)|JDBC ドライバーが接続プールをサポートするしくみについて説明します。|  
|[データベース ミラーリングの使用 &#40;JDBC&#41;](../../connect/jdbc/using-database-mirroring-jdbc.md)|JDBC ドライバーがデータベース ミラーリングの使用をサポートするしくみについて説明します。|  
|[高可用性、ディザスター リカバリーのための JDBC ドライバーのサポート](../../connect/jdbc/jdbc-driver-support-for-high-availability-disaster-recovery.md)|AlwaysOn 可用性グループに接続するアプリケーションの開発方法について説明します。|  
|[Kerberos 統合認証による SQL Server への接続](../../connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server.md)|Kerberos 統合認証を使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースに接続するアプリケーションの Java 実装について説明します。|  
|[Azure SQL Database への接続](../../connect/jdbc/connecting-to-an-azure-sql-database.md)|SQL Azure 上のデータベースに対する接続の問題について説明します。|  
  
## <a name="see-also"></a>参照  
 [JDBC ドライバーの概要](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
