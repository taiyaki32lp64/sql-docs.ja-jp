---
title: Microsoft JDBC Driver for SQL Server の機能の依存関係 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 939a8773-2583-49a4-bf00-6b892fbe39dc
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7abf0d389217535292260b6a5b055697eb4b19df
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028089"
---
# <a name="feature-dependencies-of-the-microsoft-jdbc-driver-for-sql-server"></a>Microsoft JDBC Driver for SQL Server の機能の依存関係

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

この記事では、Microsoft JDBC Driver for SQL Server が依存しているライブラリを示します。 プロジェクトには、次の依存関係があります。

## <a name="compile-time"></a>コンパイル時間

 - `com.microsoft.azure:azure-keyvault` : Always Encrypted Azure Key Vault 機能用 Azure Key Vault Provider (省略可能)
 - `com.microsoft.azure:adal4j` : Azure Active Directory 認証機能および Azure Key Vault 機能用 Azure Active Directory Library for Java (省略可能)
 - `com.microsoft.rest:client-runtime` : Azure Active Directory 認証機能および Azure Key Vault 機能用 Azure Active Directory Library for Java (省略可能)
 - `org.antlr:antlr4-runtime`: ANTLR 4 Runtime for useFmtOnly 機能 (省略可能)
 - `org.osgi:org.osgi.core` : OSGi Framework をサポートするための OSGi Core ライブラリ
 - `org.osgi:org.osgi.compendium` : OSGi Framework をサポートするための OSGi Compendium ライブラリ

## <a name="test-time"></a>テスト時

前述の機能のいずれかを必要とするプロジェクトでは、該当する依存関係を POM ファイルに明示的に宣言する必要があります。

**例:** を再宣言する必要があります、Azure Active Directory 認証機能を使用しているときに、`adal4j`プロジェクトの POM ファイルに依存関係。 次のスニペットを参照してください。

```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>7.4.1.jre11</version>
    <scope>compile</scope>
</dependency>

<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>adal4j</artifactId>
    <version>1.6.4</version>
</dependency>

<dependency>
    <groupId>com.microsoft.rest</groupId>
    <artifactId>client-runtime</artifactId>
    <version>1.6.10</version>
</dependency>
```

**例:** Azure Key Vault 機能を使用している場合は、再宣言する必要があります。、`azure-keyvault`依存関係と`adal4j`プロジェクトの POM ファイルに依存関係。 次のスニペットを参照してください。

```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>7.4.1.jre11</version>
    <scope>compile</scope>
</dependency>

<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>adal4j</artifactId>
    <version>1.6.4</version>
</dependency>

<dependency>
    <groupId>com.microsoft.rest</groupId>
    <artifactId>client-runtime</artifactId>
    <version>1.6.10</version>
</dependency>

<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-keyvault</artifactId>
    <version>1.2.1</version>
</dependency>
```

## <a name="dependency-requirements-for-the-jdbc-driver"></a>JDBC ドライバーの依存関係の要件

### <a name="working-with-the-azure-key-vault-provider"></a>Azure Key Vault プロバイダーの操作:

- JDBC ドライバー バージョン 7.4.1 - 依存関係バージョン: Azure-Keyvault (バージョン 1.2.1)、Adal4j (バージョン 1.6.4)、Client-Runtime-for-AutoRest (1.6.10)、およびそれらの依存関係 ([サンプル アプリケーション](../../connect/jdbc/azure-key-vault-sample-version-7.0.md))
- JDBC ドライバー バージョン 7.2.2 - 依存関係バージョン: Azure-Keyvault (バージョン 1.2.0)、Azure-Keyvault-Webkey (バージョン 1.2.0)、Adal4j (バージョン 1.6.3)、Client-Runtime-for-AutoRest (1.6.5)、およびそれらの依存関係 ([サンプル アプリケーション](../../connect/jdbc/azure-key-vault-sample-version-7.0.md))
- JDBC ドライバー バージョン 7.0.0 - 依存関係バージョン: Azure-Keyvault (バージョン 1.0.0)、Adal4j (バージョン 1.6.0)、およびそれらの依存関係 ([サンプル アプリケーション](../../connect/jdbc/azure-key-vault-sample-version-7.0.md))
- JDBC ドライバー バージョン 6.4.0 - 依存関係バージョン: Azure-Keyvault (バージョン 1.0.0)、Adal4j (バージョン 1.4.0)、およびそれらの依存関係 ([サンプル アプリケーション](../../connect/jdbc/azure-key-vault-sample-version-6.2.2.md))
- JDBC ドライバー バージョン 6.2.2 - 依存関係バージョン: Azure-Keyvault (バージョン 1.0.0)、Adal4j (バージョン 1.4.0)、およびそれらの依存関係 ([サンプル アプリケーション](../../connect/jdbc/azure-key-vault-sample-version-6.2.2.md))
- JDBC ドライバー バージョン 6.0.0 - 依存関係バージョン: Azure-Keyvault (バージョン 0.9.7)、Adal4j (バージョン 1.3.0)、およびそれらの依存関係 ( [サンプル アプリケーション](../../connect/jdbc/azure-key-vault-sample-version-6.0.0.md))

> [!NOTE]
> ドライバーの 6.2.2 および 6.4.0 バージョンでは、azure-keyvault-java の依存関係がバージョン 1.0.0 に更新されています。 ただし、新しいバージョンは前のバージョン (0.9.7) と互換性がないため、ドライバー内の既存の実装は破壊されます。 ドライバーの新しい実装では API を変更する必要があり、これにより、Azure Key Vault Provider を使用しているクライアント プログラムが破壊されます。
>
> この問題は、最新バージョンのドライバー (7.0.0 以降) では解決されています。 認証コールバック メカニズムを使用していた削除済みのコンストラクターは、下位互換性を保つために Azure Key Vault Provider に戻されています。

### <a name="working-with-azure-active-directory-authentication"></a>Azure Active Directory 認証の操作:

- JDBC Driver バージョン 7.4.1 - 依存関係バージョン: Adal4j (バージョン 1.6.4)、Client-Runtime-for-AutoRest (1.6.10)、およびそれらの依存関係
- JDBC Driver バージョン 7.2.2 - 依存関係バージョン: Adal4j (バージョン 1.6.3)、Client-Runtime-for-AutoRest (1.6.5)、およびそれらの依存関係
- JDBC Driver バージョン 7.0.0 - 依存関係バージョン: Adal4j (バージョン 1.6.0) およびそれらの依存関係
- JDBC Driver バージョン 6.4.0 - 依存関係バージョン: Adal4j (バージョン 1.4.0) およびそれらの依存関係
- JDBC Driver バージョン 6.2.2 - 依存関係バージョン: Adal4j (バージョン 1.4.0) およびそれらの依存関係
- JDBC Driver バージョン 6.0.0 - 依存関係バージョン: Adal4j (バージョン 1.3.0) およびそれらの依存関係 このバージョンのドライバーでは、Windows オペレーティング システム上で _ActiveDirectoryIntegrated_ 認証モードのみで sqljdbc_auth.dll と SQL Server 用 Active Directory 認証ライブラリ (ADALSQL.DLL) を使用して接続できます。

ドライバーのバージョン 6.4.0 以降、アプリケーションでは、Windows オペレーティング システム上で ADALSQL.DLL を必ず使用する必要はありません。 *Windows 以外のオペレーティング システム*では、ActiveDirectoryIntegrated 認証を機能させるには、ドライバーで Kerberos チケットが必要です。 Kerberos を使用して Active Directory に接続する方法の詳細については、「[Set Kerberos ticket on Windows, Linux, and Mac (Windows、Linux、および Mac で Kerberos チケットを設定する)](https://docs.microsoft.com/sql/connect/jdbc/connecting-using-azure-active-directory-authentication#set-kerberos-ticket-on-windows-linux-and-mac)」を参照してください。

*Windows オペレーティング システム*では、ドライバーは、既定で sqljdbc_auth.dll が検索され、Kerberos チケットの設定も Azure ライブラリの依存関係も必要ありません。 sqljdbc_auth.dll を使用できない場合、ドライバーでは、他のオペレーティング システムと同じように、Active Directory への認証用の Kerberos チケットが検索されます。

この機能を使用している[サンプル アプリケーション](../../connect/jdbc/connecting-using-azure-active-directory-authentication.md)を取得できます。

## <a name="see-also"></a>参照

[JDBC Driver GitHub リポジトリ](https://github.com/microsoft/mssql-jdbc)  
[JDBC Driver API リファレンス](../../connect/jdbc/reference/jdbc-driver-api-reference.md)
