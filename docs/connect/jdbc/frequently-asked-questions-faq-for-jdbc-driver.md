---
title: JDBC ドライバーのよくあるご質問 (FAQ) | Microsoft Docs
ms.custom: ''
ms.date: 10/28/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: cbc0e397-ecf2-4494-87b2-a492609bceae
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 37f644b07b02c90e74b0b4fe4e0d5215f5efa298
ms.sourcegitcommit: 4fb6bc7c81a692a2df706df063d36afad42816af
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 10/29/2019
ms.locfileid: "73049818"
---
# <a name="frequently-asked-questions-faq-for-jdbc-driver"></a>JDBC ドライバーのよくあるご質問 (FAQ)

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

このページでは、Microsoft SQL Server 用 JDBC Driver についてよく寄せられる質問に対する回答をご紹介します。

## <a name="frequently-asked-questions"></a>よく寄せられる質問

**JDBC ドライバーの機能強化を支援するにはどうすればよいですか。**  
JDBC Driver はオープンソースであり、[GitHub](https://github.com/microsoft/mssql-jdbc) でソース コードを確認できます。 問題を指摘したり、コード ベースに投稿したりすることで、ドライバーの機能強化を支援できます。

**ドライバーはどのバージョンの SQL Server と Java をサポートしていますか。**  
詳細については、「[Microsoft SQL Server 用 JDBC Driver のサポート表](../../connect/jdbc/microsoft-jdbc-driver-for-sql-server-support-matrix.md)」をご覧ください。

**Microsoft ダウンロード センターで入手できる JDBC ドライバー パッケージと GitHub で入手できる JDBC ドライバーは何が違いますか。**  
Microsoft JDBC ドライバー用の GitHub リポジトリで入手できる JDBC ドライバー ファイルは JDBC ドライバーの中核であり、リポジトリに示されているオープンソース ライセンスの対象です。 Microsoft ダウンロード センターのドライバー パッケージには、Windows に統合された認証と JDBC ドライバーとの XA トランザクションを可能にするための追加ライブラリが含まれています。 これらの追加ライブラリは、ダウンロード可能パッケージに含まれているライセンスの対象です。

**ドライバーをアップグレードする場合に知っておく必要があることは何ですか。**  
Microsoft JDBC Driver 7.4 では、DBC 4.2 および 4.3 (一部) 仕様がサポートされ、インストール パッケージには次に示す 3 つの JAR クラス ライブラリが含まれます。

| JAR                        | JDBC 仕様            | JDK のバージョン |
| -------------------------- | ----------------------------- | ----------- |
| mssql-jdbc-7.4.1. jre12 | JDBC 4.3 (一部) および 4.2 | JDK 12.0    |
| mssql-jdbc-7.4.1. jre11 | JDBC 4.3 (一部) および 4.2 | JDK 11.0    |
| mssql-jdbc-7.4.1. jre8  | JDBC 4.2                      | JDK 8.0     |
| &nbsp;                     | &nbsp;                        | &nbsp;      |

Microsoft JDBC Driver 7.2 では、JDBC 4.2 および 4.3 (一部) の仕様がサポートされ、インストール パッケージには次に示す 2 つの JAR クラス ライブラリが含まれます。

| JAR                        | JDBC 仕様            | JDK のバージョン |
| -------------------------- | ----------------------------- | ----------- |
| mssql-jdbc-7.2.2.jre11.jar | JDBC 4.3 (一部) および 4.2 | JDK 11.0    |
| mssql-jdbc-7.2.2.jre8.jar  | JDBC 4.2                      | JDK 8.0     |
| &nbsp;                     | &nbsp;                        | &nbsp;      |

Microsoft JDBC Driver 7.0 では、JDBC 4.2 および 4.3 (一部) 仕様がサポートされ、インストール パッケージには次に示す 2 つの JAR クラス ライブラリが含まれます。

| JAR                        | JDBC 仕様            | JDK のバージョン |
| -------------------------- | ----------------------------- | ----------- |
| mssql-jdbc-7.0.0.jre10.jar | JDBC 4.3 (一部) および 4.2 | JDK 10.0    |
| mssql-jdbc-7.0.0.jre8.jar  | JDBC 4.2                      | JDK 8.0     |
| &nbsp;                     | &nbsp;                        | &nbsp;      |

Microsoft JDBC Driver 6.4 では、DBC 4.1、4.2、および 4.3 (一部) 仕様がサポートされ、インストール パッケージには次に示す 3 つの JAR クラス ライブラリが含まれます。

| JAR                       | JDBC 仕様                 | JDK のバージョン |
| ------------------------- | ---------------------------------- | ----------- |
| mssql-jdbc-6.4.0.jre9.jar | JDBC 4.3 (一部)、4.2、4.1 | JDK 9.0     |
| mssql-jdbc-6.4.0.jre8.jar | JDBC 4.2、4.1                  | JDK 8.0     |
| mssql-jdbc-6.4.0.jre7.jar | JDBC 4.1                           | JDK 7.0     |
| &nbsp;                    | &nbsp;                             | &nbsp;      |

Microsoft JDBC Driver 6.2 では、DBC 4.0、4.1、および 4.2 仕様がサポートされ、インストール パッケージには次に示す 2 つの JAR クラス ライブラリが含まれます。

| JAR                       | JDBC 仕様     | JDK のバージョン |
| ------------------------- | ---------------------- | ----------- |
| mssql-jdbc-6.2.2.jre8.jar | JDBC 4.2、4.1、4.0 | JDK 8.0     |
| mssql-jdbc-6.2.2.jre7.jar | JDBC 4.1、4.0       | JDK 7.0     |
| &nbsp;                    | &nbsp;                 | &nbsp;      |

Microsoft JDBC Drivers 6.0 および 4.2 for SQL Server では、DBC 4.0、4.1、および 4.2 仕様がサポートされ、インストール パッケージには次に示す 2 つの JAR クラス ライブラリが含まれます。

| JAR           | JDBC 仕様     | JDK のバージョン |
| ------------- | ---------------------- | ----------- |
| sqljdbc42.jar | JDBC 4.2、4.1、4.0 | JDK 8.0     |
| sqljdbc41.jar | JDBC 4.1、4.0       | JDK 7.0     |
| &nbsp;        | &nbsp;                 | &nbsp;      |

Microsoft JDBC Driver 4.1 for SQL Server では、DBC 4.0 仕様がサポートされ、インストール パッケージには次に示す 1 つの JAR クラス ライブラリが含まれます。

| JAR           | JDBC 仕様 | JDK のバージョン     |
| ------------- | ------------------ | --------------- |
| sqljdbc41.jar | JDBC 4.0           | JDK 7.0、6.0 |
| &nbsp;        | &nbsp;             | &nbsp;      |

**既存の SQL Server のバージョンで最新のドライバーを使用するには、アプリケーションのコードを変更する必要がありますか。**  
通常、ドライバーは下位互換性を持つよう設計されているため、ドライバーをアップグレードする際に既存のアプリケーションを変更する必要はありません。 ドライバーの新しいバージョンに破壊的変更が導入された場合は、「[Microsoft JDBC Driver のリリース ノート](../../connect/jdbc/release-notes-for-the-jdbc-driver.md)」セクションに、変更に関する詳細と既存のアプリケーションへの影響が記載されます。 さらに、そのリリースと既知の問題で修正されたバグの一覧については、ドライバーに付属のリリース ノートをご覧ください。

**ドライバーの料金はいくらですか。**  
Microsoft SQL Server 用 JDBC Driver は、追加料金なしでご利用いただけます。

**ドライバーを個人で再配布できますか。**  
JDBC Driver 6.0、6.2、6.4、および 7.0 は再配布可能です。 ライセンス契約の「再頒布可能コード」の条項を見直してください。

**ドライバーを使用して Linux コンピューターから Microsoft SQL Server にアクセスできますか。**  
はい。 ドライバーを使用して、Linux、Unix、他の Windows 以外のプラットフォームから SQL Server にアクセスできます。 詳細については、「[Microsoft SQL Server 用 JDBC Driver のサポート表](../../connect/jdbc/microsoft-jdbc-driver-for-sql-server-support-matrix.md)」をご覧ください。

**ドライバーは Secure Sockets Layer (SSL) 暗号化をサポートしていますか。**  
バージョン 1.2 以降のドライバーは、Secure Sockets Layer (SSL) 暗号化をサポートしています。 詳細については、「[SSL 暗号化の使用](../../connect/jdbc/using-ssl-encryption.md)」をご覧ください。

**Microsoft SQL Server 用 JDBC Driver ではどのような認証がサポートされていますか。**  
次の表は、使用可能な認証オプションを示しています。 4\.0 リリース以降のドライバーでは、ピュア Java Kerberos 認証が使用可能です。

| プラットフォーム    | 認証                        |
| ----------- | ------------------------------------- |
| Windows 以外 | ピュア Java Kerberos                    |
| Windows 以外 | SQL Server                            |
| Windows 以外 | Azure Active Directory 認証 |
| Windows     | ピュア Java Kerberos                    |
| Windows     | SQL Server                            |
| Windows     | Kerberos と NTLM バックアップ             |
| Windows     | NTLM                                  |
| Windows     | Azure Active Directory 認証 |
| &nbsp;      | &nbsp;                                |

**ドライバーは、インターネット プロトコル バージョン 6 (IPv6) のアドレスをサポートしていますか。**  
可能。 ドライバーでは、IPv6 アドレスの使用がサポートされます。 接続プロパティのコレクションと serverName 接続文字列のプロパティを使用します。 詳細については、「[接続 URL の構築](../../connect/jdbc/building-the-connection-url.md)」をご覧ください。

**アダプティブ バッファリングとは何ですか。**  
アダプティブ バッファリングは、Microsoft SQL Server 2005 JDBC Driver バージョン 1.2 から導入されました。 これは、サーバー カーソルのオーバーヘッドを発生させることなく、あらゆる種類の大きな値のデータを取得できるように設計されています。 Microsoft SQL Server JDBC Driver のアダプティブ バッファリング機能には接続文字列プロパティ responseBuffering があり、これを "adaptive" または "full" に設定できます。 バージョン 1.2 リリースでは、"full" が既定のバッファリング モードであるため、アプリケーションから明示的にアダプティブ バッファリング モードを設定する必要があります。 JDBC Driver 2.0 以降では、ドライバーの既定の動作は "adaptive" です。 したがって、アプリケーションから明示的に要求しなくても、アダプティブ バッファリングの動作が適用されます。 詳細については、「[アダプティブ バッファリングの使用](../../connect/jdbc/using-adaptive-buffering.md)」とブログ「[What is adaptiveresponse buffering and why should I use it?](https://go.microsoft.com/fwlink/?LinkId=111575)」 (アダプティブ レスポンス バッファリングの概要とこれを使用する理由) を参照してください。

**ドライバーで接続プールがサポートされますか。**  
ドライバーは、Java Platform, Enterprise Edition 5 (Java EE 5) の接続プールをサポートしています。 ドライバーは、ミドルウェア アプリケーション サーバー ベンダーが提供するあらゆる接続プールの実装に参加できるように、JDBC 3.0 に必要なインターフェイスを実装しています。 このドライバーは、これらの環境でプールされた接続に参加します。 詳細については、「 [Using Connection Pooling](../../connect/jdbc/using-connection-pooling.md)」をご覧ください。 ドライバーは独自のプール実装を提供せず、むしろサードパーティの Java アプリケーション サーバーに依存しています。

**ドライバーのサポートを利用できますか。**  
さまざまなサポート オプションをご利用いただけます。 Microsoft が監視している [GitHub リポジトリ](https://github.com/microsoft/mssql-jdbc)に質問や問題を投稿できます。 [フォーラム](https://go.microsoft.com/fwlink/?LinkID=246673)は、Microsoft、MVP、およびコミュニティによって監視されています。 マイクロソフト カスタマー サポートにお問い合わせいただくこともできます。 開発チームは、サードパーティのアプリケーション サーバーの外部で問題の再現をお客様にお願いする場合があります。 ホストしている Java コンテナー環境の外部で問題を再現できない場合は、チームが引き続きお客様を支援できるよう、関連するサードパーティを介入させる必要があります。 チームは、Windows などのオペレーティング システムで問題を再現することをお客様にお願いする場合もあります。

**ドライバーは、サードパーティのアプリケーション サーバーでの使用が認定されていますか。**  
ドライバーは、IBM WebSphere、SAP NetWeaver などのさまざまなアプリケーション サーバーに対してテスト済みです。

**どのようにしてトレースを有効にできますか。**  
ドライバーはトレース (またはログ記録) の使用をサポートしているため、アプリケーションで使用するときに JDBC Driver で発生した問題の解決に役立てることができます。 クライアント側の JAR のトレースの使用を有効にするため、JDBC Driver は java.util.logging でログ記録 API を使用しています。 詳細については、「[ドライバー操作のトレース](../../connect/jdbc/tracing-driver-operation.md)」を参照してください。 サーバー側の XA のトレースについては、「 [Data Access Tracing in SQL Server (SQL Server でのデータ アクセスのトレース)](https://go.microsoft.com/fwlink/?LinkId=248705)」をご覧ください。

**古いバージョンのドライバー (SQL Server 2000 JDBC ドライバー、2005 ドライバー、1.0、1.1、1.2 ドライバーなど) はどこでダウンロードできますか。**  
これらのバージョンのドライバーはサポートされていないため、ダウンロードできません。 Microsoft は Java 接続のサポートの向上を継続的に進めています。 そのため、最新バージョンの Microsoft JDBC ドライバーを使用することを強くおすすめします。

**JRE 1.4 を使用しています。JRE 1.4 と互換性があるのはどのドライバーですか。**  
SAP 製品を使用していて JRE 1.4 のサポートが必要なお客様は、 [SAPService Marketplace](https://service.sap.com/) にお問い合わせの上、1.2 Microsoft JDBC ドライバーを入手してください。

**ドライバーは FIPS 検証済みのアルゴリズムを使用して通信できますか。**  
Microsoft JDBC Driver には暗号化アルゴリズムが含まれていません。 お客様が、Federal Information Processing Standards (FIPS) に準拠していると見なされるオペレーティング システム、アプリケーション、JVM アルゴリズムを活用して、これらのアルゴリズムを使用するドライバーを構成する場合、ドライバーは指定されたアルゴリズムのみを通信に使用します。

## <a name="see-also"></a>参照

[JDBC ドライバーの概要](../../connect/jdbc/overview-of-the-jdbc-driver.md)
