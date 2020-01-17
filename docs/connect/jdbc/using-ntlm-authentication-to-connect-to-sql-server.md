---
title: NTLM 認証を使用して SQL Server | に接続するMicrosoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: lilgreenbird
ms.author: v-susanh
manager: kenvh
ms.openlocfilehash: 2fab4794544ada07e0bf5e690da35b72ad6b7421
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2019
ms.locfileid: "69026102"
---
# <a name="using-ntlm-authentication-to-connect-to-sql-server"></a>NTLM 認証を使用して SQL Server に接続する

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

を[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]使用すると、アプリケーションは**authenticationscheme**接続プロパティを使用して、NTLM v2 認証を使用してデータベースに接続することを示すことができます。 

NTLM 認証にも、次のプロパティが使用されます。

- **domain = domainName**optional
- **user = ユーザー名**
- **password = password**
- **統合 Atedsecurity = true**

**ドメイン**以外のプロパティは必須です。 **NTLM** authenticationscheme プロパティが使用されているときに、ドライバーが不足している場合は、エラーがスローされます。 

接続プロパティの詳細については、「[接続プロパティの設定](../../connect/jdbc/setting-the-connection-properties.md)」を参照してください。 Microsoft NTLM 認証プロトコルの詳細については、「 [MICROSOFT ntlm](https://docs.microsoft.com/windows/desktop/SecAuthN/microsoft-ntlm)」を参照してください。

## <a name="remarks"></a>Remarks

NTLM 認証の動作を制御する SQL server 設定の説明については、「[ネットワークセキュリティ: LAN Manager の認証レベル](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/network-security-lan-manager-authentication-level)」を参照してください。 

## <a name="logging"></a>ログ記録

NTLM 認証をサポートするために、新しいロガー com.microsoft.sqlserver.jdbc.internals.NTLMAuthentication が追加されました。 詳細については、「[ドライバー操作のトレース](../../connect/jdbc/tracing-driver-operation.md)」を参照してください。

## <a name="datasource"></a>DataSource

データソースを使用して接続を作成する場合は、 **Setauthenticationscheme**、 **setdomain**、および (必要に応じて) **setauthenticationscheme**を使用して、NTLM のプロパティをプログラムで設定できます。

```java
SQLServerDataSource ds = new SQLServerDataSource();
ds.setServerName("<server>");
ds.setPortNumber(1433); // change if necessary
ds.setIntegratedSecurity(true);
ds.setAuthenticationScheme("NTLM");
ds.setDomain("<domainName>");
ds.setUser("<userName>");
ds.setPassword("<password>");
ds.setDatabaseName("<database>");
ds.setServerSpn("<serverSpn");

try (Connection c = ds.getConnection(); Statement s = c.createStatement();
        ResultSet rs = s.executeQuery("select auth_scheme from sys.dm_exec_connections where session_id=@@spid")) {
    while (rs.next()) {
        System.out.println("Authentication Scheme: " + rs.getString(1));
    }
}
```

## <a name="service-principal-names"></a>サービス プリンシパル名

サービス プリンシパル名 (SPN) は、クライアントがサービスのインスタンスを一意に識別するための名前です。

**serverSpn** 接続プロパティを使用して SPN を指定できますが、ドライバーで自動的に作成することもできます (既定)。 このプロパティの形式は "MSSQLSvc/fqdn:port\@REALM" です。ここで、fqdn は完全修飾ドメイン名、port はポート番号、REALM は大文字で表記された SQL Server の領域です。 既定の領域はサーバーの領域と同じであるため、このプロパティの領域部分は省略可能です。

たとえば、SPN は次のようになります。 "MSSQLSvc/some: 1433" のようになります。

サービス プリンシパル名 (SPN) の詳細については、以下を参照してください。

- [クライアント接続でのサービス プリンシパル名 (SPN) のサポート](https://docs.microsoft.com/sql/relational-databases/native-client/features/service-principal-name-spn-support-in-client-connections?view=sql-server-2017)

> [!NOTE]  
> serverSpn 接続属性は、Microsoft JDBC Driver 4.2 以降でのみサポートされています。

> JDBC driver の6.2 リリースの前に、 **Serverspn**を明示的に設定する必要があります。 6\.2 リリースの場合、ドライバーは既定で **Serverspn** を構築でき ますが、 **serverspn**を明示的に使用することもできます。

## <a name="security-risks"></a>セキュリティ リスク

NTLM プロトコルは、さまざまな脆弱性を持つ古い認証プロトコルであり、セキュリティ上のリスクがあります。 これは比較的弱い暗号方式に基づいており、さまざまな攻撃に対して脆弱です。 これは Kerberos に置き換えられ、より安全であり、推奨されます。 NTLM 認証は、セキュリティで保護された信頼できる環境でのみ使用するか、Kerberos を使用できないようにする必要があります。

は[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] NTLM v2 のみをサポートしており、元の v1 プロトコルよりもセキュリティが強化されています。 また、セキュリティ強化のために SSL 暗号化を使用することもお勧めします。 

拡張保護を有効にする方法の詳細については、以下を参照してください。

- [拡張保護を使用したデータベース エンジンへの接続](../../database-engine/configure-windows/connect-to-the-database-engine-using-extended-protection.md)

SSL 暗号化を使用した接続の詳細については、以下を参照してください。

- [SSL 暗号化を使用した接続](../../connect/jdbc/connecting-with-ssl-encryption.md)

> [!NOTE]
> 7\.4 リリースでは、拡張保護と暗号化の**両方**を有効にすることはサポートされていません。

## <a name="see-also"></a>参照

[JDBC ドライバーによる SQL Server への接続](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)
