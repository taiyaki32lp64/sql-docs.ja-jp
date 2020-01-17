---
title: JDBC ドライバーのシステム要件 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 447792bb-f39b-49b4-9fd0-1ef4154c74ab
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5759a1f9936fdb8a6df4de422ae2ff0542dc63a8
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2019
ms.locfileid: "69027672"
---
# <a name="system-requirements-for-the-jdbc-driver"></a>JDBC ドライバーのシステム要件
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] を使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] のデータにアクセスするには、次のコンポーネントをコンピューターにインストールする必要があります。

- [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] ([ダウンロード](download-microsoft-jdbc-driver-for-sql-server.md))
- Java ランタイム環境

## <a name="java-runtime-environment-requirements"></a>Java Runtime Environment の要件  

 Microsoft JDBC Driver 7.4 for SQL Server 以降で、Java Development Kit (JDK) 12.0 と Java Runtime Environment (JRE) 12.0 がサポートされています。

 Microsoft JDBC Driver 7.2 for SQL Server 以降で、Java Development Kit (JDK) 11.0 と Java Runtime Environment (JRE) 11.0 がサポートされています。
 
 Microsoft JDBC Driver 7.0 for SQL Server 以降で、Java Development Kit (JDK) 10.0 と Java Runtime Environment (JRE) 10.0 がサポートされています。

 Microsoft JDBC Driver 6.4 for SQL Server 以降で、Java Development Kit (JDK) 9.0 と Java Runtime Environment (JRE) 9.0 がサポートされています。

 Microsoft JDBC Driver 4.2 for SQL Server 以降で、Java Development Kit (JDK) 8.0 と Java Runtime Environment (JRE) 8.0 がサポートされています。 Java Database Connectivity (JDBC) Spec API のサポートが拡張され、JDBC 4.1 と 4.2 API が対象になりました。
  
 Microsoft JDBC Driver 4.1 for SQL Server 以降で、Java Development Kit (JDK) 7.0 と Java Runtime Environment (JRE) 7.0 がサポートされています。
  
 [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)] 以降では、JDBC 4.0 API を包含する形で Java Database Connectivity (JDBC) Spec API に対する JDBC ドライバー サポートが拡張されています。 JDBC 4.0 API は、Java Development Kit (JDK) 6.0 および Java Runtime Environment (JRE) 6.0 の一部として導入されました。 JDBC 4.0 は、JDBC 3.0 API のスーパーセットです。
  
 Windows と UNIX オペレーティング システムで [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] を展開する場合、インストール パッケージである *sqljdbc_\<version>_enu.exe* と *sqljdbc_\<version>_enu.tar.gz* をそれぞれ使用する必要があります。 JDBC Driver の展開方法の詳細については、「[JDBC Driver の展開](../../connect/jdbc/deploying-the-jdbc-driver.md)」トピックを参照してください。  

**Microsoft JDBC Driver 7.4 for SQL Server:**  

  JDBC Driver 7.4 の各インストール パッケージには、3 つの JAR クラス ライブラリ (**mssql-jdbc-7.4.1.jre8.jar**、**mssql-jdbc-7.4.1.jre11.jar**、**mssql-jdbc-7.4.1.jre12.jar**) が含まれています。

  JDBC Driver 7.4 は、すべての主要な Java 仮想マシンと連携し、それらでサポートされるように設計されていますが、テストは OpenJDK 1.8、OpenJDK 11.0、OpenJDK 12.0、Azul Zulu JRE 1.8、Azul Zulu JRE 11.0、Azul Zulu JRE 12.0 上でのみ実行されます。
  
  Microsoft JDBC Drivers 7.4 for SQL Server に含まれている 2 つの JAR ファイルによって提供されるサポートの概要を以下に示します。  
  
  |JAR|JDBC バージョン準拠|推奨される Java のバージョン|[説明]|  
|---------|-----------------------------|----------------------|-----------------|   
|mssql-jdbc-7.4.1. jre8|4.2|8|Java Runtime Environment (JRE) 1.8 が必要です。 JRE 1.7 以前を使用すると、例外がスローされます。<br /><br /> 7\.4 の新機能には、JDK 12 のサポート、NTLM 認証、useFmtOnly が含まれます。 |    
|mssql-jdbc-7.4.1. jre11|4.3|11|Java Runtime Environment (JRE) 11.0 が必要です。 JRE 10.0 以前を使用すると、例外がスローされます。<br /><br /> 7\.4 の新機能には、JDK 12 のサポート、NTLM 認証、useFmtOnly が含まれます。 |  
|mssql-jdbc-7.4.1. jre12|4.3|12|Java Runtime Environment (JRE) 12.0 が必要です。 JRE 11.0 以前を使用すると、例外がスローされます。<br /><br /> 7\.4 の新機能には、JDK 12 のサポート、NTLM 認証、useFmtOnly が含まれます。 |   


  JDBC Driver 7.4 は Maven Central Repository でも使用でき、次のコードを POM.XML に追加することで Maven プロジェクトに追加できます。  
  
 ```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>7.4.1.jre11</version>
</dependency>
```

**Microsoft JDBC Driver 7.2 for SQL Server:**  

  JDBC Driver 7.2 の各インストール パッケージには、2 つの JAR クラス ライブラリ (**mssql-jdbc-7.2.2.jre8.jar** および **mssql-jdbc-7.2.2.jre11.jar**) が含まれています。

  JDBC Driver 7.2 は、すべての主要な Java 仮想マシンと連携し、それらでサポートされるように設計されていますが、テストは OpenJDK 8.0、OpenJDK 11.0、Azul Zulu JRE 8.0、および Azul Zulu JRE 11.0 上でのみ実行されます。
  
  Microsoft JDBC Drivers 7.2 for SQL Server に含まれている 2 つの JAR ファイルによって提供されるサポートの概要を以下に示します。  
  
  |JAR|JDBC バージョン準拠|推奨される Java のバージョン|[説明]|  
|---------|-----------------------------|----------------------|-----------------|   
|mssql-jdbc-7.2.2.jre8.jar|4.2|8|Java Runtime Environment (JRE) 8.0 が必要です。 JRE 7.0 以前を使用すると、例外がスローされます。<br /><br /> 7\.2 の新機能には、JDK 11 のサポート、Active Directory マネージド サービス ID (MSI) 認証、OSGi のサポート、SQLServerError API が含まれます。 |    
|mssql-jdbc-7.2.2.jre11.jar|4.3|10|Java Runtime Environment (JRE) 11.0 が必要です。 JRE 10.0 以前を使用すると、例外がスローされます。<br /><br /> 7\.2 の新機能には、JDK 11 のサポート、Active Directory マネージド サービス ID (MSI) 認証、OSGi のサポート、SQLServerError API が含まれます。 |    


  JDBC Driver 7.2 は Maven Central Repository でも使用でき、次のコードを POM.XML に追加することで Maven プロジェクトに追加できます。  
  
 ```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>7.2.2.jre11</version>
</dependency>
```
 
**Microsoft JDBC Driver 7.0 for SQL Server:**  

  JDBC Driver 7.0 の各インストール パッケージには、2 つの JAR クラス ライブラリ (**mssql-jdbc-7.0.0.jre8.jar** および **mssql-jdbc-7.0.0.jre10.jar**) が含まれています。

  JDBC Driver 7.0 は、すべての主要な Java 仮想マシンで操作とサポートができるよう設計されていますが、テストが実行されるのは OpenJDK 8.0 と 10.0 上のみです。
  
  Microsoft JDBC Driver 7.0 for SQL Server に含まれている 2 つの JAR ファイルによって提供されるサポートの概要を以下に示します。  
  
  |JAR|JDBC バージョン準拠|推奨される Java のバージョン|[説明]|  
|---------|-----------------------------|----------------------|-----------------|   
|mssql-jdbc-7.0.0.jre8.jar|4.2|8|Java Runtime Environment (JRE) 8.0 が必要です。 JRE 7.0 以前を使用すると、例外がスローされます。<br /><br /> 7\.0 の新機能には、JDK 10 のサポート、JDBC 4.2 仕様に更新された既定の準拠レベル、空間データ型のサポート、cancelQueryTime 接続プロパティ、要求境界メソッド、useBulkCopyForBatchInsert 接続プロパティ、データ検出および分類情報、UTF-8 機能の拡張、および CityHash のサポートが含まれます。 |    
|mssql-jdbc-7.0.0.jre10.jar|4.3|10|Java Runtime Environment (JRE) 10.0 が必要です。 JRE 9.0 以前を使用すると、例外がスローされます。<br /><br /> 7\.0 の新機能には、JDK 10 のサポート、JDBC 4.2 仕様に更新された既定の準拠レベル、空間データ型のサポート、cancelQueryTime 接続プロパティ、要求境界メソッド、useBulkCopyForBatchInsert 接続プロパティ、データ検出および分類情報、UTF-8 機能の拡張、および CityHash のサポートが含まれます。 |    


  JDBC Driver 7.0 は Maven Central Repository でも使用でき、次のコードを POM.XML に追加することで Maven プロジェクトに追加できます。  
  
 ```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>7.0.0.jre10</version>
</dependency>
```
  
**Microsoft JDBC Driver 6.4 for SQL Server:**  

  JDBC Driver 6.4 の各インストール パッケージには、3 つの JAR クラス ライブラリ (**mssql-jdbc-6.4.0.jre7.jar**、**mssql-jdbc-6.4.0.jre8.jar**、**mssql-jdbc-6.4.0.jre9.jar**) が含まれています。

  JDBC Driver 6.4 は、すべての主要な Java 仮想マシンで操作とサポートができるよう設計されていますが、テストが実行されるのは OpenJDK 7.0、8.0、9.0 上のみです。
  
  Microsoft JDBC Driver 6.4 for SQL Server に含まれている 3 つの JAR ファイルによって提供されるサポートの概要を以下に示します。  
  
  |JAR|JDBC バージョン準拠|推奨される Java のバージョン|[説明]|  
|---------|-----------------------------|----------------------|-----------------|   
|mssql-jdbc-6.4.0.jre7.jar|4.1|7|Java Runtime Environment (JRE) 7.0 が必要です。 JRE 6.0 以前を使用すると、例外がスローされます。<br /><br /> 6\.4 の新機能には、Linux 用の Azure AD 認証、Kerberos でのプリンシパル/パスワードの使用、クロスドメイン認証での SPN 内の REALM の自動検証、Kerberos 制約付き委任、クエリのタイムアウト、ソケットのタイムアウト、および準備されたステートメントのハンドルの再利用が含まれます。 |  
|mssql-jdbc-6.4.0.jre8.jar|4.2|8|Java Runtime Environment (JRE) 8.0 が必要です。 JRE 7.0 以前を使用すると、例外がスローされます。<br /><br /> 6\.4 の新機能には、Linux 用の Azure AD 認証、Kerberos でのプリンシパル/パスワードの使用、クロスドメイン認証での SPN 内の REALM の自動検証、Kerberos 制約付き委任、クエリのタイムアウト、ソケットのタイムアウト、および準備されたステートメントのハンドルの再利用が含まれます。 |    
|mssql-jdbc-6.4.0.jre9.jar|4.3|9|Java Runtime Environment (JRE) 9.0 が必要です。 JRE 8.0 以前を使用すると、例外がスローされます。<br /><br /> 6\.4 の新機能には、Linux 用の Azure AD 認証、Kerberos でのプリンシパル/パスワードの使用、クロスドメイン認証での SPN 内の REALM の自動検証、Kerberos 制約付き委任、クエリのタイムアウト、ソケットのタイムアウト、および準備されたステートメントのハンドルの再利用が含まれます。 |

JDBC Driver 6.4 は Maven Central Repository でも使用でき、次のコードを POM.XML に追加することで Maven プロジェクトに追加できます。 

 ```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>6.4.0.jre9</version>
</dependency>
```

**Microsoft JDBC Driver 6.2 for SQL Server:**  
  
  JDBC Driver 6.2 の各インストール パッケージには、2 つの JAR クラス ライブラリ (**mssql-jdbc-6.2.2.jre7.jar** および **mssql-jdbc-6.2.2.jre8.jar**) が含まれています。 
  
 JDBC Driver 6.2 は、すべての主要な Java 仮想マシンで操作とサポートができるよう設計されていますが、テストが実行されるのは Sun JRE 5.0、6.0、7.0、8.0 上のみです。
  
 Microsoft JDBC Driver 6.0 for SQL Server および Microsoft JDBC Driver 4.2 for SQL Server に含まれている 2 つの JAR ファイルによって提供されるサポートの概要を以下に示します。  
  
|JAR|JDBC バージョン準拠|推奨される Java のバージョン|[説明]|  
|---------|-----------------------------|----------------------|-----------------|
|mssql-jdbc-6.2.2.jre7.jar|4.1|7|Java Runtime Environment (JRE) 7.0 が必要です。 JRE 6.0 以前を使用すると、例外がスローされます。<br /><br /> 6\.2 の新機能には、Linux 用の Azure AD 認証、Kerberos でのプリンシパル/パスワードの方法、クロスドメイン認証での SPN 内の REALM の自動検証、Kerberos 制約付き委任、クエリのタイムアウト、ソケットのタイムアウト、および準備されたステートメントのハンドルの再利用が含まれます。 |  
|mssql-jdbc-6.2.3.jre8.jar|4.2|8|Java Runtime Environment (JRE) 8.0 が必要です。 JRE 7.0 以前を使用すると、例外がスローされます。<br /><br /> 6\.2 の新機能には、Linux 用の Azure AD 認証、Kerberos でのプリンシパル/パスワードの使用、クロスドメイン認証での SPN 内の REALM の自動検証、Kerberos 制約付き委任、クエリのタイムアウト、ソケットのタイムアウト、および準備されたステートメントのハンドルの再利用が含まれます。|    

  JDBC Driver 6.2 は Maven Central Repository でも使用でき、次のコードを POM.XML に追加することで Maven プロジェクトに追加できます。 
  
 ```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>6.2.2.jre8</version>
</dependency>
```    

 **Microsoft JDBC Driver 6.0 for SQL Server および Microsoft JDBC Driver 4.2 for SQL Server:**  
  
  JDBC Drivers 6.0 および 4.2 には、各インストール パッケージに 2 つの JAR クラス ライブラリ (**sqljdbc41.jar** および **sqljdbc42.jar**) が含まれています。 
  
 JDBC Driver 6.0 および 4.2 は、すべての主要な Java 仮想マシンで操作とサポートができるよう設計されていますが、Sun JRE 5.0、6.0、7.0、8.0 のみでテストされます。
  
 Microsoft JDBC Driver 6.0 for SQL Server および Microsoft JDBC Driver 4.2 for SQL Server に含まれている 2 つの JAR ファイルによって提供されるサポートの概要を以下に示します。  
  
|JAR|JDBC バージョン準拠|推奨される Java のバージョン|[説明]|  
|---------|-----------------------------|----------------------|-----------------|   
|sqljdbc41.jar|4.1|7|Java Runtime Environment (JRE) 7.0 が必要です。 JRE 6.0 以前を使用すると、例外がスローされます。<br /><br /> 6\.0 および 4.2 パッケージの新機能には、JDBC 4.1 準拠と一括コピーが含まれます。<br /><br /> さらに、6.0 パッケージのみの新機能として、常時暗号化、テーブル値パラメーター、Azure Active Directory 認証、AlwaysOn 可用性グループへの透過接続、準備されたクエリと国際化ドメイン名 (IDN) でのパラメーターのメタデータ取得の機能強化が含まれます。|  
|sqljdbc42.jar|4.2|8|Java Runtime Environment (JRE) 8.0 が必要です。 JRE 7.0 以前を使用すると、例外がスローされます。<br /><br /> 6\.0 と 4.2 のパッケージの新機能には、JDBC 4.1 準拠、JDBC 4.2 準拠、および一括コピーが含まれます。<br /><br /> さらに、6.0 パッケージのみの新機能として、常時暗号化、テーブル値パラメーター、Azure Active Directory 認証、AlwaysOn 可用性グループへの透過接続、準備されたクエリと国際化ドメイン名 (IDN) でのパラメーターのメタデータ取得の機能強化が含まれます。|  
  
 **Microsoft JDBC Driver 4.1 for SQL Server:**  
  
 JDBC Driver 4.1 には、各インストール パッケージに 1 つの JAR クラス ライブラリ (**sqljdbc41.jar**) が含まれます。  
    
|JAR|[説明]|  
|---------|-----------------|  
|sqljdbc41.jar|**sqljdbc41.jar** クラス ライブラリでは、JDBC 4.0 API のサポートが提供されます。 JDBC 4.0 ドライバーのすべての機能と JDBC 4.0 API メソッドを備えています。 JDBC 4.1 はサポートされていません ("SQLFeatureNotSupportedException" の例外がスローされます)。<br /><br /> **sqljdbc41.jar** クラス ライブラリを使用するには、Java Runtime Environment (JRE) 7.0 が必要です。 JRE 6.0 および 5.0 で **sqljdbc41.jar** を使用すると、例外がスローされます。<br /><br /> 
  
 この JDBC ドライバーは、すべての主要な Java 仮想マシンで操作とサポートができるよう設計されていますが、Sun JRE 5.0、6.0、7.0 でテストされます。
  
 Microsoft JDBC Driver 4.1 for SQL Server に含まれている JAR ファイルによって提供されるサポートの概要を以下に示します。  
  
|JAR|JDBC のバージョン|JRE (実行可能)|JDK (コンパイル可能)|  
|---------|------------------|---------------------|-------------------------|   
|sqljdbc41.jar|4|7|7 6 5|  
  
## <a name="sql-server-requirements"></a>SQL Server 要件  
 JDBC ドライバーは、Azure SQL Database と SQL Server への接続をサポートします。 Microsoft JDBC Driver 4.2 for SQL Server と Microsoft JDBC Driver 4.1 for SQL Server では、SQL Server 2008 以降をサポートします。
  
## <a name="operating-system-requirements"></a>オペレーティング システムの要件  
 JDBC ドライバーは、Java 仮想マシン (JVM) の使用をサポートするすべてのオペレーティング システムで機能するように設計されています。 ただし、公式にテストされているのは、Sun Solaris、SUSE Linux、および Windows オペレーティング システムだけです。  
  
## <a name="supported-languages"></a>サポートされている言語  
 JDBC ドライバーは、すべての [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 列の照合順序をサポートしています。 JDBC ドライバーでサポートされる照合順序の詳細については、「[JDBC Driver の国際化機能](../../connect/jdbc/international-features-of-the-jdbc-driver.md)」をご覧ください。  
  
 照合順序の詳細については、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オンライン ブックの「照合順序の使用」を参照してください。  
  
## <a name="see-also"></a>参照  
 [JDBC ドライバーの概要](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
