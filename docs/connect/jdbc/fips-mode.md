---
title: JDBC | の FIPS モードMicrosoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: genemi
ms.technology: connectivity
ms.topic: conceptual
author: MikeRayMSFT
ms.author: mikeray
manager: kenvh
ms.openlocfilehash: 63681ee474d4993e248bf02dcabd9065317ffa39
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028064"
---
# <a name="fips-mode"></a>FIPS モード

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Microsoft JDBC Driver for SQL Server は、 *FIPS 140 準拠*として構成された jvm での実行をサポートしています。

#### <a name="prerequisites"></a>Prerequisites

- FIPS 構成 JVM
- 適切な SSL 証明書
- 適切なポリシーファイル
- 適切な構成パラメーター

## <a name="fips-configured-jvm"></a>FIPS 構成 JVM

一般に、アプリケーションは FIPS `java.security`準拠の暗号化プロバイダーを使用するようにファイルを構成できます。 FIPS 140 準拠の構成方法については、JVM に固有のドキュメントを参照してください。

FIPS 構成の承認済みモジュールを表示するには、[暗号化モジュール検証プログラムの検証済みモジュール](https://csrc.nist.gov/Projects/cryptographic-module-validation-program/Validated-Modules)を参照してください。

ベンダーには、FIPS で JVM を構成するための追加の手順が含まれる場合があります。

## <a name="appropriate-ssl-certificate"></a>適切な SSL 証明書
FIPS モードで SQL Server に接続するには、有効な SSL 証明書が必要です。 FIPS が有効になっているクライアントコンピューター (JVM) の Java キーストアにインストールまたはインポートします。

### <a name="importing-ssl-certificate-in-java-keystore"></a>Java キーストアに SSL 証明書をインポートする
FIPS では、ほとんどの場合、PKCS またはプロバイダー固有の形式で証明書 (cert) をインポートする必要があります。
次のスニペットを使用して、SSL 証明書をインポートし、適切なキーストア形式を使用して作業ディレクトリに保存します。 _信頼\_ストア\_パスワード_は、Java キーストアのパスワードです。

```java
public void saveGenericKeyStore(
        String provider,
        String trustStoreType,
        String certName,
        String certPath
        ) throws KeyStoreException, CertificateException,
            NoSuchAlgorithmException, NoSuchProviderException,
            IOException
{
    KeyStore ks = KeyStore.getInstance(trustStoreType, provider);
    FileOutputStream os = new FileOutputStream("./MyTrustStore_" + trustStoreType);
    ks.load(null, null);
    ks.setCertificateEntry(certName, getCertificate(certPath));
    ks.store(os, TRUST_STORE_PASSWORD.toCharArray());
    os.flush();
    os.close();
}

private Certificate getCertificate(String pathName)
        throws FileNotFoundException, CertificateException
{
    FileInputStream fis = new FileInputStream(pathName);
    CertificateFactory cf = CertificateFactory.getInstance("X.509");
    return cf.generateCertificate(fis);
}
```

次の例では、BouncyCastle プロバイダーを使用して、Azure SSL 証明書を PKCS12 形式でインポートしています。 証明書は、次のスニペットを使用して、 _MyTrustStore\_PKCS12_という名前の作業ディレクトリにインポートされます。

`saveGenericKeyStore(BCFIPS, PKCS12, "SQLAzure SSL Certificate Name", "SQLAzure.cer");`

## <a name="appropriate-policy-files"></a>適切なポリシーファイル
一部の FIPS プロバイダーでは、無制限のポリシー jar が必要です。 このような場合は、Sun/Oracle の場合、 [jre 8](https://www.oracle.com/technetwork/java/javase/downloads/jce8-download-2133166.html)または[Jre 7](https://www.oracle.com/technetwork/java/javase/downloads/jce-7-download-432124.html)の Java Cryptography Extension (Jce) 無制限の防衛法ポリシーファイルをダウンロードします。 

## <a name="appropriate-configuration-parameters"></a>適切な構成パラメーター
FIPS 準拠モードで JDBC Driver を実行するには、次の表に示すように接続プロパティを構成します。 

#### <a name="properties"></a>Properties 

|プロパティ|型|既定|[説明]|注|
|---|---|---|---|---|
|encrypt|boolean ["true / false"]|"false"|FIPS が有効になっている JVM の暗号化プロパティは**true**にする必要があります||
|TrustServerCertificate|boolean ["true / false"]|"false"|FIPS の場合、ユーザーは証明書チェーンを検証する必要があるため、ユーザーはこのプロパティに **"false"** 値を使用する必要があります。 ||
|trustStore|String|null|証明書をインポートした Java キーストアファイルのパス。 システムに証明書をインストールする場合は、何も渡す必要はありません。 ドライバーは、cacerts ファイルまたは jssecacerts ファイルを使用します。||
|trustStorePassword|String|null|trustStore データの整合性を確認するために使用するパスワードです。||
|fips|boolean ["true / false"]|"false"|FIPS が有効になっている JVM の場合、このプロパティは**true**である必要があります|6\.1.4 で追加 (安定リリース 6.2.2)||
|fipsProvider|String|null|JVM で構成された FIPS プロバイダー。 例: BCFIPS または SunPKCS11-NSS |6\.1.2 (Stable release 6.2.2) で追加されました。 v6.4.0 では非推奨となりました。詳細については、[こちら](https://github.com/Microsoft/mssql-jdbc/pull/460)を参照してください。|
|trustStoreType|String|JKS|FIPS モードの場合は、トラストストアの種類として「PKCS12」または「FIPS プロバイダーで定義された種類」を設定します |6\.1.2 で追加 (安定リリース 6.2.2)||
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |
