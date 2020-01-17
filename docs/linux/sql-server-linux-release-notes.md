---
title: Linux 上の SQL Server 2017 のリリース ノート
description: この記事には、Linux で実行されている SQL Server 2017 のリリース ノートとサポートされている機能が含まれています。 リリース ノートは、最新のリリースと以前のいくつかのリリースに含まれています。
author: VanMSFT
ms.author: vanto
ms.date: 10/10/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 1314744f-fcaf-46db-800e-2918fa7e1b6c
ms.openlocfilehash: 839d789e633e8f8794ec6fde70980e6c1a43ce91
ms.sourcegitcommit: 39630fddc69141531eddca2a3c156ccf8536f49c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72930485"
---
# <a name="release-notes-for-sql-server-2017-on-linux"></a>Linux 上の SQL Server 2017 のリリース ノート

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

次のリリース ノートは、Linux で実行されている [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] に適用されます。 この記事は、リリースごとのセクションに分けられています。 GA リリースには、詳細なサポートと既知の問題が記載されています。 更新累積プログラム (CU) または一般配布リリース (GDR) のそれぞれには、Linux パッケージのダウンロードへのリンクに加えて、CU の変更について説明するサポート記事へのリンクが含まれています。

> [!TIP]
> これらのリリース ノートは、特に [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] リリースを対象としています。 新しい [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] の詳細については、[Linux 上の SQL Server 2019 プレビューのリリース ノート](sql-server-linux-release-notes-2019.md?view=sql-server-ver15)を参照してください。

## <a name="supported-platforms"></a>サポートされているプラットフォーム

| プラットフォーム | [ファイル システム] | インストール ガイド |
|-----|-----|-----|
| Red Hat Enterprise Linux 7.3、7.4、7.5、または 7.6 Server | XFS または EXT4 | [インストール ガイド](quickstart-install-connect-red-hat.md) | 
| SUSE Enterprise Linux Server v12 SP2 | XFS または EXT4 | [インストール ガイド](quickstart-install-connect-suse.md) |
| Ubuntu 16.04LTS | XFS または EXT4 | [インストール ガイド](quickstart-install-connect-ubuntu.md) | 
| Windows、Mac、または Linux 上の Docker エンジン 1.8+ | なし | [インストール ガイド](quickstart-install-connect-docker.md) | 

> [!TIP]
> 詳細については、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] on Linux の[システム要件](sql-server-linux-setup.md#system)を確認してください。 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] の最新のサポート ポリシーについては、「[Microsoft SQL Server のテクニカル サポート ポリシー](https://support.microsoft.com/help/4047326/support-policy-for-microsoft-sql-server)」を参照してください。

## <a name="tools"></a>ツール

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] を対象とする既存のクライアント ツールの多くは、Linux で実行されている [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] をシームレスにターゲットにすることができます。 一部のツールには、Linux で適切に動作させるための特定のバージョン要件がある場合があります。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ツールの完全な一覧については、[SQL Server 用の SQL ツールとユーティリティ](../tools/overview-sql-tools.md)に関するページを参照してください。

## <a name="release-history"></a>リリース履歴

[!INCLUDE[ssSQL17](../includes/sssql17-md.md)] のリリース履歴の一覧を次の表に示します。

| リリース               | Version       | リリース日 |
|-----------------------|---------------|--------------|
| [CU17](#CU17)         | 14.0.3238.1   | 2019-10-08   |
| [CU16](#CU16)         | 14.0.3223.3   | 2019-08-01   |
| [CU15](#CU15)         | 14.0.3162.1   | 2019-05-23   |
| [CU14](#CU14)         | 14.0.3076.1   | 2019-03-25   |
| [CU13](#CU13)         | 14.0.3048.4   | 2018-12-18   |
| [CU12](#CU12)         | 14.0.3045.24  | 2018-10-24   |
| [CU11](#CU11)         | 14.0.3038.14  | 2018-09-20   |
| [CU10](#CU10)         | 14.0.3037.1   | 2018-08-27   |
| [CU9-GDR2](#CU9-GDR2) | 14.0.3035.2   | 2018-08-18   |
| [GDR2](#GDR2)         | 14.0.2002.14  | 2018-08-18   |
| [CU9](#CU9)           | 14.0.3030.27  | 2018-07-18   |
| [CU8](#CU8)           | 14.0.3029.16  | 2018-06-21   |
| [CU7](#CU7)           | 14.0.3026.27  | 2018-05-24   |
| [CU6](#CU6)           | 14.0.3025.34  | 2018-04-19   |
| [CU5](#CU5)           | 14.0.3023.8   | 2018-03-20   |
| [CU4](#CU4)           | 14.0.3022.28  | 2018-02-20   |
| [CU3](#CU3)           | 14.0.3015.40  | 2018-01-03   |
| [GDR1](#GDR1)         | 14.0.2000.63  | 2018-01-03   |
| [CU2](#CU2)           | 14.0.3008.27  | 2017-11-28   |
| [CU1](#CU1)           | 14.0.3006.16  | 2017-10-24   |
| [GA](#GA)             | 14.0.1000.169 | 2017-10-02   |

## <a id="cuinstall"></a>更新プログラムのインストール方法

CU リポジトリ (**mssql-server-2017**) を構成済みの場合は、新規インストールを実行すると [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] パッケージの最新の CU を取得します。 この CU リポジトリは、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] on Linux 用のすべてのパッケージ インストールに関する記事の既定値です。 GDR リポジトリ (**mssql-server-2017-GDR**) を構成済みの場合は、GA 以降にリリースされた重要なセキュリティ更新プログラムのみを取得します。 Docker コンテナー CU または GDR 更新プログラムが必要な場合は、[Docker エンジン用の Microsoft SQL Server on Linux](https://hub.docker.com/r/microsoft/mssql-server) の公式イメージを参照してください。 リポジトリ構成の詳細については、[SQL Server on Linux 用のリポジトリの構成](sql-server-linux-change-repo.md)に関するページを参照してください。

既存の [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] パッケージを更新する場合は、パッケージごとに適切な更新コマンドを実行して、最新の CU を取得します。 各パッケージの特定の更新手順については、次のインストール ガイドを参照してください。

- [SQL Server パッケージのインストール](sql-server-linux-setup.md#upgrade)
- [フルテキスト検索パッケージのインストール](sql-server-linux-setup-full-text-search.md)
- [SQL Server Integration Services のインストール](sql-server-linux-setup-ssis.md)
- [SQL Server エージェントの有効化](sql-server-linux-setup-sql-agent.md)

## <a id="CU17"></a> CU17 (2019 年 10 月)

これは、[!INCLUDE[ssSQL17](../includes/sssql17-md.md)] の Cumulative Update 17 (CU17) リリースです。 このリリースの [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] のバージョンは 14.0.3238.1 です。 このリリースの修正プログラムと機能強化の詳細については、[https://support.microsoft.com/en-us/help/4498951](https://support.microsoft.com/en-us/help/4515579) を参照してください。

### <a name="package-details"></a>パッケージの詳細

手動またはオフラインのパッケージ インストールの場合は、次の表の情報を使用して RPM と Debian のパッケージをダウンロードすることができます。

| [パッケージ] | パッケージ バージョン | ダウンロード |
|-----|-----|-----|
| Red Hat RPM パッケージ | 14.0.3238.1-19 | [エンジン RPM パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3238.1-19.x86_64.rpm)</br>[高可用性 RPM パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3238.1-19.x86_64.rpm)</br>[フルテキスト検索 RPM パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3238.1-19.x86_64.rpm)</br>[SSIS パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM パッケージ | 14.0.3238.1-19 | [mssql-server エンジン RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3238.1-19.x86_64.rpm)</br>[高可用性 RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3238.1-19.x86_64.rpm)</br>[フルテキスト検索 RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3238.1-19.x86_64.rpm) | 
| Ubuntu 16.04 Debian パッケージ | 14.0.3238.1-19 | [エンジン Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3238.1-19_amd64.deb)</br>[高可用性 Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3238.1-19_amd64.deb)</br>[フルテキスト検索 Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3238.1-19_amd64.deb)<br/>[SSIS パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU16"></a> CU16 (2019 年 8 月)

これは、[!INCLUDE[ssSQL17](../includes/sssql17-md.md)] の Cumulative Update 16 (CU16) リリースです。 このリリースの [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] バージョンは 14.0.3223.3 です。 このリリースの修正プログラムと機能強化の詳細については、[https://support.microsoft.com/en-us/help/4508218](https://support.microsoft.com/en-us/help/4508218) を参照してください。

### <a name="whats-new"></a>新機能

|新機能または更新 | 詳細 |
|:---|:---|
| MSDTC のサポート | SQL Server 2017 の Microsoft 分散トランザクション コーディネーター (MSDTC) のサポートです。 詳細については、「[Linux で Microsoft 分散トランザクション コーディネーター (MSDTC) を構成する方法](sql-server-linux-configure-msdtc.md)」をご覧ください。 |

### <a name="package-details"></a>パッケージの詳細

手動またはオフラインのパッケージ インストールの場合は、次の表の情報を使用して RPM と Debian のパッケージをダウンロードすることができます。

| [パッケージ] | パッケージ バージョン | ダウンロード |
|-----|-----|-----|
| Red Hat RPM パッケージ | 14.0.3223.3-15 | [エンジン RPM パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3223.3-15.x86_64.rpm)</br>[高可用性 RPM パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3223.3-15.x86_64.rpm)</br>[フルテキスト検索 RPM パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3223.3-15.x86_64.rpm)</br>[SSIS パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM パッケージ | 14.0.3223.3-15 | [mssql-server エンジン RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3223.3-15.x86_64.rpm)</br>[高可用性 RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3223.3-15.x86_64.rpm)</br>[フルテキスト検索 RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3223.3-15.x86_64.rpm) | 
| Ubuntu 16.04 Debian パッケージ | 14.0.3223.3-15 | [エンジン Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3223.3-15_amd64.deb)</br>[高可用性 Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3223.3-15_amd64.deb)</br>[フルテキスト検索 Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3223.3-15_amd64.deb)<br/>[SSIS パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU15"></a> CU15 (2019 年 5 月)

これは、[!INCLUDE[ssSQL17](../includes/sssql17-md.md)] の Cumulative Update 15 (CU15) リリースです。 このリリースの [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] バージョンは 14.0.3162.1 です。 このリリースの修正プログラムと機能強化の詳細については、[https://support.microsoft.com/en-us/help/4498951](https://support.microsoft.com/en-us/help/4498951) を参照してください。

### <a name="package-details"></a>パッケージの詳細

手動またはオフラインのパッケージ インストールの場合は、次の表の情報を使用して RPM と Debian のパッケージをダウンロードすることができます。

| [パッケージ] | パッケージ バージョン | ダウンロード |
|-----|-----|-----|
| Red Hat RPM パッケージ | 14.0.3162.1-1 | [エンジン RPM パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3162.1-1.x86_64.rpm)</br>[高可用性 RPM パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3162.1-1.x86_64.rpm)</br>[フルテキスト検索 RPM パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3162.1-1.x86_64.rpm)</br>[SSIS パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM パッケージ | 14.0.3162.1-1 | [mssql-server エンジン RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3162.1-1.x86_64.rpm)</br>[高可用性 RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3162.1-1.x86_64.rpm)</br>[フルテキスト検索 RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3162.1-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian パッケージ | 14.0.3162.1-1 | [エンジン Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3162.1-1_amd64.deb)</br>[高可用性 Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3162.1-1_amd64.deb)</br>[フルテキスト検索 Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3162.1-1_amd64.deb)<br/>[SSIS パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU14"></a> CU14 (2019 年 3 月)

これは、[!INCLUDE[ssSQL17](../includes/sssql17-md.md)] の Cumulative Update 14 (CU14) リリースです。 このリリースの [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] バージョンは 14.0.3076.1 です。 このリリースの修正プログラムと機能強化の詳細については、[https://support.microsoft.com/help/4484710](https://support.microsoft.com/help/4484710) を参照してください。

### <a name="package-details"></a>パッケージの詳細

手動またはオフラインのパッケージ インストールの場合は、次の表の情報を使用して RPM と Debian のパッケージをダウンロードすることができます。

| [パッケージ] | パッケージ バージョン | ダウンロード |
|-----|-----|-----|
| Red Hat RPM パッケージ | 14.0.3076.1-2 | [エンジン RPM パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3076.1-2.x86_64.rpm)</br>[高可用性 RPM パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3076.1-2.x86_64.rpm)</br>[フルテキスト検索 RPM パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3076.1-2.x86_64.rpm)</br>[SSIS パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM パッケージ | 14.0.3076.1-2 | [mssql-server エンジン RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3076.1-2.x86_64.rpm)</br>[高可用性 RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3076.1-2.x86_64.rpm)</br>[フルテキスト検索 RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3076.1-2.x86_64.rpm) | 
| Ubuntu 16.04 Debian パッケージ | 14.0.3076.1-2 | [エンジン Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3076.1-2_amd64.deb)</br>[高可用性 Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3076.1-2_amd64.deb)</br>[フルテキスト検索 Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3076.1-2_amd64.deb)<br/>[SSIS パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU13"></a> CU13 (2018 年 12 月)

これは、[!INCLUDE[ssSQL17](../includes/sssql17-md.md)] の Cumulative Update 13 (CU13) リリースです。 このリリースの [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] バージョンは 14.0.3048.4 です。 このリリースの修正プログラムと機能強化の詳細については、[https://support.microsoft.com/help/4466404](https://support.microsoft.com/help/4466404) を参照してください。

### <a name="package-details"></a>パッケージの詳細

手動またはオフラインのパッケージ インストールの場合は、次の表の情報を使用して RPM と Debian のパッケージをダウンロードすることができます。

| [パッケージ] | パッケージ バージョン | ダウンロード |
|-----|-----|-----|
| Red Hat RPM パッケージ | 14.0.3048.4-1 | [エンジン RPM パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3048.4-1.x86_64.rpm)</br>[高可用性 RPM パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3048.4-1.x86_64.rpm)</br>[フルテキスト検索 RPM パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3048.4-1.x86_64.rpm)</br>[SSIS パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM パッケージ | 14.0.3048.4-1 | [mssql-server エンジン RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3048.4-1.x86_64.rpm)</br>[高可用性 RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3048.4-1.x86_64.rpm)</br>[フルテキスト検索 RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3048.4-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian パッケージ | 14.0.3048.4-1 | [エンジン Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3048.4-1_amd64.deb)</br>[高可用性 Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3048.4-1_amd64.deb)</br>[フルテキスト検索 Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3048.4-1_amd64.deb)<br/>[SSIS パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU12"></a> CU12 (2018 年 10 月)

これは、[!INCLUDE[ssSQL17](../includes/sssql17-md.md)] の Cumulative Update 12 (CU12) リリースです。 このリリースの [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] バージョンは 14.0.3045.24 です。 このリリースの修正プログラムと機能強化の詳細については、[https://support.microsoft.com/help/4464082](https://support.microsoft.com/help/4464082) を参照してください。

### <a name="package-details"></a>パッケージの詳細

手動またはオフラインのパッケージ インストールの場合は、次の表の情報を使用して RPM と Debian のパッケージをダウンロードすることができます。

| [パッケージ] | パッケージ バージョン | ダウンロード |
|-----|-----|-----|
| Red Hat RPM パッケージ | 14.0.3045.24-1 | [エンジン RPM パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3045.24-1.x86_64.rpm)</br>[高可用性 RPM パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3045.24-1.x86_64.rpm)</br>[フルテキスト検索 RPM パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3045.24-1.x86_64.rpm)</br>[SSIS パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM パッケージ | 14.0.3045.24-1 | [mssql-server エンジン RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3045.24-1.x86_64.rpm)</br>[高可用性 RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3045.24-1.x86_64.rpm)</br>[フルテキスト検索 RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3045.24-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian パッケージ | 14.0.3045.24-1 | [エンジン Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3045.24-1_amd64.deb)</br>[高可用性 Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3045.24-1_amd64.deb)</br>[フルテキスト検索 Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3045.24-1_amd64.deb)<br/>[SSIS パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU11"></a> CU11 (2018 年 9 月)

これは、[!INCLUDE[ssSQL17](../includes/sssql17-md.md)] の Cumulative Update 11 (CU11) リリースです。 このリリースの [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] バージョンは 14.0.3038.14 です。 このリリースの修正プログラムと機能強化の詳細については、[https://support.microsoft.com/help/4462262](https://support.microsoft.com/help/4462262) を参照してください。

### <a name="package-details"></a>パッケージの詳細

手動またはオフラインのパッケージ インストールの場合は、次の表の情報を使用して RPM と Debian のパッケージをダウンロードすることができます。

| [パッケージ] | パッケージ バージョン | ダウンロード |
|-----|-----|-----|
| Red Hat RPM パッケージ | 14.0.3038.14-2 | [エンジン RPM パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3038.14-2.x86_64.rpm)</br>[高可用性 RPM パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3038.14-2.x86_64.rpm)</br>[フルテキスト検索 RPM パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3038.14-2.x86_64.rpm)</br>[SSIS パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM パッケージ | 14.0.3038.14-2 | [mssql-server エンジン RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3038.14-2.x86_64.rpm)</br>[高可用性 RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3038.14-2.x86_64.rpm)</br>[フルテキスト検索 RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3038.14-2.x86_64.rpm) | 
| Ubuntu 16.04 Debian パッケージ | 14.0.3038.14-2 | [エンジン Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3038.14-2_amd64.deb)</br>[高可用性 Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3038.14-2_amd64.deb)</br>[フルテキスト検索 Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3038.14-2_amd64.deb)<br/>[SSIS パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU10"></a> CU10 (2018 年 8 月)

これは、[!INCLUDE[ssSQL17](../includes/sssql17-md.md)] の Cumulative Update 10 (CU10) リリースです。 このリリースの [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] バージョンは 14.0.3037.1 です。 このリリースの修正プログラムと機能強化の詳細については、[https://support.microsoft.com/help/4342123](https://support.microsoft.com/help/4342123) を参照してください。

### <a name="package-details"></a>パッケージの詳細

手動またはオフラインのパッケージ インストールの場合は、次の表の情報を使用して RPM と Debian のパッケージをダウンロードすることができます。

| [パッケージ] | パッケージ バージョン | ダウンロード |
|-----|-----|-----|
| Red Hat RPM パッケージ | 14.0.3037.1-2 | [エンジン RPM パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3037.1-2.x86_64.rpm)</br>[高可用性 RPM パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3037.1-2.x86_64.rpm)</br>[フルテキスト検索 RPM パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3037.1-2.x86_64.rpm)</br>[SSIS パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM パッケージ | 14.0.3037.1-2 | [mssql-server エンジン RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3037.1-2.x86_64.rpm)</br>[高可用性 RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3037.1-2.x86_64.rpm)</br>[フルテキスト検索 RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3037.1-2.x86_64.rpm) | 
| Ubuntu 16.04 Debian パッケージ | 14.0.3037.1-2 | [エンジン Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3037.1-2_amd64.deb)</br>[高可用性 Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3037.1-2_amd64.deb)</br>[フルテキスト検索 Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3037.1-2_amd64.deb)<br/>[SSIS パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU9-GDR2"></a> CU9-GDR2 (2018 年 8 月)

これは、[!INCLUDE[ssSQL17](../includes/sssql17-md.md)] 用に以前にリリースされた CU (CU9) も含まれているセキュリティ更新プログラムです。 このリリースの [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] バージョンは 14.0.3035.2 です。 このリリースの修正プログラムと機能強化の詳細については、[https://support.microsoft.com/help/4293805](https://support.microsoft.com/help/4293805) を参照してください。

### <a name="package-details"></a>パッケージの詳細

手動またはオフラインのパッケージ インストールの場合は、次の表の情報を使用して RPM と Debian のパッケージをダウンロードすることができます。

| [パッケージ] | パッケージ バージョン | ダウンロード |
|-----|-----|-----|
| Red Hat RPM パッケージ | 14.0.3035.2-1 | [エンジン RPM パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3035.2-1.x86_64.rpm)</br>[高可用性 RPM パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3035.2-1.x86_64.rpm)</br>[フルテキスト検索 RPM パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3035.2-1.x86_64.rpm)| 
| SLES RPM パッケージ | 14.0.3035.2-1 | [mssql-server エンジン RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3035.2-1.x86_64.rpm)</br>[高可用性 RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3035.2-1.x86_64.rpm)</br>[フルテキスト検索 RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3035.2-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian パッケージ | 14.0.3035.2-1 | [エンジン Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3035.2-1_amd64.deb)</br>[高可用性 Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3035.2-1_amd64.deb)</br>[フルテキスト検索 Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3035.2-1_amd64.deb)<br/> |

## <a id="GDR2"></a> GDR2 (2018 年 8 月)

これは、[!INCLUDE[ssSQL17](../includes/sssql17-md.md)] の GDR2 (および GDR1) セキュリティ修正プログラムのみが含まれるセキュリティ更新プログラムです。  このリリースの [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] バージョンは 14.0.2002.14 です。 このリリースの修正プログラムと機能強化の詳細については、[https://support.microsoft.com/help/4293803](https://support.microsoft.com/help/4293803) を参照してください。

### <a name="package-details"></a>パッケージの詳細

手動またはオフラインのパッケージ インストールの場合は、次の表の情報を使用して RPM と Debian のパッケージをダウンロードすることができます。

| [パッケージ] | パッケージ バージョン | ダウンロード |
|-----|-----|-----|
| Red Hat RPM パッケージ | 14.0.2002.14-1 | [エンジン RPM パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-14.0.2002.14-1.x86_64.rpm)</br>[高可用性 RPM パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-ha-14.0.2002.14-1.x86_64.rpm)</br>[フルテキスト検索 RPM パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-fts-14.0.2002.14-1.x86_64.rpm) | 
| SLES RPM パッケージ | 14.0.2002.14-1 | [mssql-server エンジン RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-14.0.2002.14-1.x86_64.rpm)</br>[高可用性 RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-ha-14.0.2002.14-1.x86_64.rpm)</br>[フルテキスト検索 RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-fts-14.0.2002.14-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian パッケージ | 14.0.2002.14-1 | [エンジン Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server/mssql-server_14.0.2002.14-1_amd64.deb)</br>[高可用性 Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.2002.14-1_amd64.deb)</br>[フルテキスト検索 Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.2002.14-1_amd64.deb) |

## <a id="CU9"></a> CU9 (2018 年 7 月)

これは、[!INCLUDE[ssSQL17](../includes/sssql17-md.md)] の Cumulative Update 9 (CU9) リリースです。 このリリースの [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] バージョンは 14.0.3030.27 です。 このリリースの修正プログラムと機能強化の詳細については、[https://support.microsoft.com/help/4341265](https://support.microsoft.com/help/4341265) を参照してください。

### <a name="package-details"></a>パッケージの詳細

手動またはオフラインのパッケージ インストールの場合は、次の表の情報を使用して RPM と Debian のパッケージをダウンロードすることができます。

| [パッケージ] | パッケージ バージョン | ダウンロード |
|-----|-----|-----|
| Red Hat RPM パッケージ | 14.0.3030.27-1 | [エンジン RPM パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3030.27-1.x86_64.rpm)</br>[高可用性 RPM パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3030.27-1.x86_64.rpm)</br>[フルテキスト検索 RPM パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3030.27-1.x86_64.rpm)</br>[SSIS パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM パッケージ | 14.0.3030.27-1 | [mssql-server エンジン RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3030.27-1.x86_64.rpm)</br>[高可用性 RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3030.27-1.x86_64.rpm)</br>[フルテキスト検索 RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3030.27-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian パッケージ | 14.0.3030.27-1 | [エンジン Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3030.27-1_amd64.deb)</br>[高可用性 Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3030.27-1_amd64.deb)</br>[フルテキスト検索 Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3030.27-1_amd64.deb)<br/>[SSIS パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU8"></a> CU8 (2018 年 6 月)

これは、[!INCLUDE[ssSQL17](../includes/sssql17-md.md)] の Cumulative Update 8 (CU8) リリースです。 このリリースの [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] バージョンは 14.0.3029.16 です。 このリリースの修正プログラムと機能強化の詳細については、[https://support.microsoft.com/help/4338363](https://support.microsoft.com/help/4338363) を参照してください。

### <a name="package-details"></a>パッケージの詳細

手動またはオフラインのパッケージ インストールの場合は、次の表の情報を使用して RPM と Debian のパッケージをダウンロードすることができます。

| [パッケージ] | パッケージ バージョン | ダウンロード |
|-----|-----|-----|
| Red Hat RPM パッケージ | 14.0.3029.16-1 | [エンジン RPM パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3029.16-1.x86_64.rpm)</br>[高可用性 RPM パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3029.16-1.x86_64.rpm)</br>[フルテキスト検索 RPM パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3029.16-1.x86_64.rpm)</br>[SSIS パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM パッケージ | 14.0.3029.16-1 | [mssql-server エンジン RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3029.16-1.x86_64.rpm)</br>[高可用性 RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3029.16-1.x86_64.rpm)</br>[フルテキスト検索 RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3029.16-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian パッケージ | 14.0.3029.16-1 | [エンジン Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3029.16-1_amd64.deb)</br>[高可用性 Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3029.16-1_amd64.deb)</br>[フルテキスト検索 Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3029.16-1_amd64.deb)<br/>[SSIS パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU7"></a> CU7 (2018 年 5 月)

これは、[!INCLUDE[ssSQL17](../includes/sssql17-md.md)] の Cumulative Update 7 (CU7) リリースです。 このリリースの [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] バージョンは 14.0.3026.27 です。 このリリースの修正プログラムと機能強化の詳細については、[https://support.microsoft.com/help/4229789](https://support.microsoft.com/help/4229789) を参照してください。

### <a name="package-details"></a>パッケージの詳細

手動またはオフラインのパッケージ インストールの場合は、次の表の情報を使用して RPM と Debian のパッケージをダウンロードすることができます。

| [パッケージ] | パッケージ バージョン | ダウンロード |
|-----|-----|-----|
| Red Hat RPM パッケージ | 14.0.3026.27-2 | [エンジン RPM パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3026.27-2.x86_64.rpm)</br>[高可用性 RPM パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3026.27-2.x86_64.rpm)</br>[フルテキスト検索 RPM パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3026.27-2.x86_64.rpm)</br>[SSIS パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM パッケージ | 14.0.3026.27-2 | [mssql-server エンジン RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3026.27-2.x86_64.rpm)</br>[高可用性 RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3026.27-2.x86_64.rpm)</br>[フルテキスト検索 RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3026.27-2.x86_64.rpm) | 
| Ubuntu 16.04 Debian パッケージ | 14.0.3026.27-2 | [エンジン Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3026.27-2_amd64.deb)</br>[高可用性 Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3026.27-2_amd64.deb)</br>[フルテキスト検索 Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3026.27-2_amd64.deb)<br/>[SSIS パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU6"></a> CU6 (2018 年 4 月)

これは、[!INCLUDE[ssSQL17](../includes/sssql17-md.md)] の Cumulative Update 6 (CU6) リリースです。 このリリースの [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] バージョンは 14.0.3025.34 です。 このリリースの修正プログラムと機能強化の詳細については、[https://support.microsoft.com/help/4101464](https://support.microsoft.com/help/4101464) を参照してください。

### <a name="package-details"></a>パッケージの詳細

手動またはオフラインのパッケージ インストールの場合は、次の表の情報を使用して RPM と Debian のパッケージをダウンロードすることができます。

| [パッケージ] | パッケージ バージョン | ダウンロード |
|-----|-----|-----|
| Red Hat RPM パッケージ | 14.0.3025.34-3 | [エンジン RPM パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3025.34-3.x86_64.rpm)</br>[高可用性 RPM パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3025.34-3.x86_64.rpm)</br>[フルテキスト検索 RPM パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3025.34-3.x86_64.rpm)</br>[SSIS パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM パッケージ | 14.0.3025.34-3 | [mssql-server エンジン RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3025.34-3.x86_64.rpm)</br>[高可用性 RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3025.34-3.x86_64.rpm)</br>[フルテキスト検索 RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3025.34-3.x86_64.rpm) | 
| Ubuntu 16.04 Debian パッケージ | 14.0.3025.34-3 | [エンジン Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3025.34-3_amd64.deb)</br>[高可用性 Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3025.34-3_amd64.deb)</br>[フルテキスト検索 Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3025.34-3_amd64.deb)<br/>[SSIS パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU5"></a> CU5 (2018 年 3 月)

これは、[!INCLUDE[ssSQL17](../includes/sssql17-md.md)] の Cumulative Update 5 (CU5) リリースです。 このリリースの [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] バージョンは 14.0.3023.8 です。 このリリースの修正プログラムと機能強化の詳細については、[https://support.microsoft.com/help/4092643](https://support.microsoft.com/help/4092643) を参照してください。

### <a name="known-upgrade-issue"></a>アップグレードに関する既知の問題

以前のリリースから CU5 にアップグレードすると、次のエラーが発生して [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] を起動できないことがあります。

```
Error: 4860, Severity: 16, State: 1.
Cannot bulk load. The file "C:\Install\SqlTraceCollect.dtsx" does not exist or you don't have file access rights.
Error: 912, Severity: 21, State: 2.
Script level upgrade for database 'master' failed because upgrade step 'msdb110_upgrade.sql' encountered error 200, state
```

このエラーを解決するには、SQL Server エージェントを有効にし、次のコマンドを使用して [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] を再起動します。

```bash
sudo /opt/mssql/bin/mssql-conf set sqlagent.enabled true
sudo systemctl start mssql-server
```

### <a name="package-details"></a>パッケージの詳細

手動またはオフラインのパッケージ インストールの場合は、次の表の情報を使用して RPM と Debian のパッケージをダウンロードすることができます。

| [パッケージ] | パッケージ バージョン | ダウンロード |
|-----|-----|-----|
| Red Hat RPM パッケージ | 14.0.3023.8-5 | [エンジン RPM パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3023.8-5.x86_64.rpm)</br>[高可用性 RPM パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3023.8-5.x86_64.rpm)</br>[フルテキスト検索 RPM パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3023.8-5.x86_64.rpm)</br>[SSIS パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM パッケージ | 14.0.3023.8-5 | [mssql-server エンジン RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3023.8-5.x86_64.rpm)</br>[高可用性 RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3023.8-5.x86_64.rpm)</br>[フルテキスト検索 RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3023.8-5.x86_64.rpm) | 
| Ubuntu 16.04 Debian パッケージ | 14.0.3023.8-5 | [エンジン Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3023.8-5_amd64.deb)</br>[高可用性 Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3023.8-5_amd64.deb)</br>[フルテキスト検索 Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3023.8-5_amd64.deb)<br/>[SSIS パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU4"></a> CU4 (2018 年 2 月)

これは、[!INCLUDE[ssSQL17](../includes/sssql17-md.md)] の Cumulative Update 4 (CU4) リリースです。 このリリースの [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] バージョンは 14.0.3022.28 です。 このリリースの修正プログラムと機能強化の詳細については、[https://support.microsoft.com/help/4056498](https://support.microsoft.com/help/4056498) を参照してください。

### <a name="package-details"></a>パッケージの詳細

手動またはオフラインのパッケージ インストールの場合は、次の表の情報を使用して RPM と Debian のパッケージをダウンロードすることができます。

> [!NOTE]
> CU4 より、SQL Server エージェントは別のパッケージとしてインストールされなくなりました。 これはエンジン パッケージと共にインストールされ、使用するには有効にする必要があります。

| [パッケージ] | パッケージ バージョン | ダウンロード |
|-----|-----|-----|
| Red Hat RPM パッケージ | 14.0.3022.28-2 | [エンジン RPM パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3022.28-2.x86_64.rpm)</br>[高可用性 RPM パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3022.28-2.x86_64.rpm)</br>[フルテキスト検索 RPM パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3022.28-2.x86_64.rpm)</br>[SSIS パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM パッケージ | 14.0.3022.28-2 | [mssql-server エンジン RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3022.28-2.x86_64.rpm)</br>[高可用性 RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3022.28-2.x86_64.rpm)</br>[フルテキスト検索 RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3022.28-2.x86_64.rpm) | 
| Ubuntu 16.04 Debian パッケージ | 14.0.3022.28-2 | [エンジン Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3022.28-2_amd64.deb)</br>[高可用性 Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3022.28-2_amd64.deb)</br>[フルテキスト検索 Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3022.28-2_amd64.deb)<br/>[SSIS パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="GDR1"></a> GDR1 (2018 年 1 月)

これは、[!INCLUDE[ssSQL17](../includes/sssql17-md.md)] の GDR1 セキュリティ修正プログラムのみが含まれるセキュリティ更新プログラムです。 このリリースの [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] バージョンは 14.0.2000.63 です。 このリリースの修正プログラムと機能強化の詳細については、[https://support.microsoft.com/help/4057122](https://support.microsoft.com/help/4057122) を参照してください。

### <a name="package-details"></a>パッケージの詳細

手動またはオフラインのパッケージ インストールの場合は、次の表の情報を使用して RPM と Debian のパッケージをダウンロードすることができます。

| [パッケージ] | パッケージ バージョン | ダウンロード |
|-----|-----|-----|
| Red Hat RPM パッケージ | 14.0.2000.63-3 | [エンジン RPM パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-14.0.2000.63-3.x86_64.rpm)</br>[高可用性 RPM パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-ha-14.0.2000.63-3.x86_64.rpm)</br>[フルテキスト検索 RPM パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-fts-14.0.2000.63-3.x86_64.rpm) | 
| SLES RPM パッケージ | 14.0.2000.63-3 | [mssql-server エンジン RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-14.0.2000.63-3.x86_64.rpm)</br>[高可用性 RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-ha-14.0.2000.63-3.x86_64.rpm)</br>[フルテキスト検索 RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-fts-14.0.2000.63-3.x86_64.rpm) | 
| Ubuntu 16.04 Debian パッケージ | 14.0.2000.63-3 | [エンジン Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server/mssql-server_14.0.2000.63-3_amd64.deb)</br>[高可用性 Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.2000.63-3_amd64.deb)</br>[フルテキスト検索 Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.2000.63-3_amd64.deb) |

## <a id="CU3"></a> CU3 (2018 年 1 月)

これは、[!INCLUDE[ssSQL17](../includes/sssql17-md.md)] の Cumulative Update 3 (CU3) リリースです。 このリリースの [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] バージョンは 14.0.3015.40 です。 このリリースの修正プログラムと機能強化の詳細については、[https://support.microsoft.com/help/4052987](https://support.microsoft.com/help/4052987) を参照してください。

### <a name="package-details"></a>パッケージの詳細

手動またはオフラインのパッケージ インストールの場合は、次の表の情報を使用して RPM と Debian のパッケージをダウンロードすることができます。

| [パッケージ] | パッケージ バージョン | ダウンロード |
|-----|-----|-----|
| Red Hat RPM パッケージ | 14.0.3015.40-1 | [エンジン RPM パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3015.40-1.x86_64.rpm)</br>[高可用性 RPM パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3015.40-1.x86_64.rpm)</br>[フルテキスト検索 RPM パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3015.40-1.x86_64.rpm)</br>[SQL Server エージェント RPM パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3015.40-1.x86_64.rpm)</br>[SSIS パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM パッケージ | 14.0.3015.40-1 | [mssql-server エンジン RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3015.40-1.x86_64.rpm)</br>[高可用性 RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3015.40-1.x86_64.rpm)</br>[フルテキスト検索 RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3015.40-1.x86_64.rpm)</br>[SQL Server エージェント RPM パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3015.40-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian パッケージ | 14.0.3015.40-1 | [エンジン Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3015.40-1_amd64.deb)</br>[高可用性 Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3015.40-1_amd64.deb)</br>[フルテキスト検索 Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3015.40-1_amd64.deb)</br>[SQL Server エージェント Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.3015.40-1_amd64.deb)<br/>[SSIS パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU2"></a> CU2 (2017 年 11 月)

これは、[!INCLUDE[ssSQL17](../includes/sssql17-md.md)] の Cumulative Update 2 (CU2) リリースです。 このリリースの [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] バージョンは 14.0.3008.27 です。 このリリースの修正プログラムと機能強化の詳細については、[https://support.microsoft.com/help/4052574](https://support.microsoft.com/help/4052574) を参照してください。

### <a name="package-details"></a>パッケージの詳細

手動またはオフラインのパッケージ インストールの場合は、次の表の情報を使用して RPM と Debian のパッケージをダウンロードすることができます。

| [パッケージ] | パッケージ バージョン | ダウンロード |
|-----|-----|-----|
| Red Hat RPM パッケージ | 14.0.3008.27-1 | [エンジン RPM パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3008.27-1.x86_64.rpm)</br>[高可用性 RPM パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3008.27-1.x86_64.rpm)</br>[フルテキスト検索 RPM パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3008.27-1.x86_64.rpm)</br>[SQL Server エージェント RPM パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3008.27-1.x86_64.rpm)</br>[SSIS パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM パッケージ | 14.0.3008.27-1 | [mssql-server エンジン RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3008.27-1.x86_64.rpm)</br>[高可用性 RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3008.27-1.x86_64.rpm)</br>[フルテキスト検索 RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3008.27-1.x86_64.rpm)</br>[SQL Server エージェント RPM パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3008.27-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian パッケージ | 14.0.3008.27-1 | [エンジン Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3008.27-1_amd64.deb)</br>[高可用性 Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3008.27-1_amd64.deb)</br>[フルテキスト検索 Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3008.27-1_amd64.deb)</br>[SQL Server エージェント Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.3008.27-1_amd64.deb)<br/>[SSIS パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU1"></a> CU1 (2017 年 10 月)

これは、[!INCLUDE[ssSQL17](../includes/sssql17-md.md)] の Cumulative Update 1 (CU1) リリースです。 このリリースの [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] バージョンは 14.0.3006.16 です。 このリリースの修正プログラムと機能強化の詳細については、[https://support.microsoft.com/help/KB4053439](https://support.microsoft.com/help/4038634) を参照してください。

### <a name="package-details"></a>パッケージの詳細

手動またはオフラインのパッケージ インストールの場合は、次の表の情報を使用して RPM と Debian のパッケージをダウンロードすることができます。

| [パッケージ] | パッケージ バージョン | ダウンロード |
|-----|-----|-----|
| Red Hat RPM パッケージ | 14.0.3006.16-3 | [エンジン RPM パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3006.16-3.x86_64.rpm)</br>[高可用性 RPM パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3006.16-3.x86_64.rpm)</br>[フルテキスト検索 RPM パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3006.16-3.x86_64.rpm)</br>[SQL Server エージェント RPM パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3006.16-3.x86_64.rpm)</br>[SSIS パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM パッケージ | 14.0.3006.16-3 | [mssql-server エンジン RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3006.16-3.x86_64.rpm)</br>[高可用性 RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3006.16-3.x86_64.rpm)</br>[フルテキスト検索 RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3006.16-3.x86_64.rpm)</br>[SQL Server エージェント RPM パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3006.16-3.x86_64.rpm) | 
| Ubuntu 16.04 Debian パッケージ | 14.0.3006.16-3 | [エンジン Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3006.16-3_amd64.deb)</br>[高可用性 Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3006.16-3_amd64.deb)</br>[フルテキスト検索 Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3006.16-3_amd64.deb)</br>[SQL Server エージェント Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.3006.16-3_amd64.deb)<br/>[SSIS パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="GA"></a> GA (2017 年 10 月)

これは [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] の一般公開 (GA) リリースです。 このリリースの [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] バージョンは 14.0.1000.169 です。

### <a name="package-details"></a>パッケージの詳細

次の表に、RPM パッケージと Debian パッケージのパッケージの詳細とダウンロード場所を示します。 次のインストール ガイドに記載されている手順を使用する場合は、これらのパッケージを直接ダウンロードする必要はありません。

- [SQL Server パッケージのインストール](sql-server-linux-setup.md)
- [フルテキスト検索パッケージのインストール](sql-server-linux-setup-full-text-search.md)
- [SQL Server エージェント パッケージのインストール](sql-server-linux-setup-sql-agent.md)
- [SQL Server Integration Services のインストール](sql-server-linux-setup-ssis.md)

| [パッケージ] | パッケージ バージョン | ダウンロード |
|-----|-----|-----|
| Red Hat RPM パッケージ | 14.0.1000.169-2 | [エンジン RPM パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.1000.169-2.x86_64.rpm)</br>[高可用性 RPM パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.1000.169-2.x86_64.rpm)</br>[フルテキスト検索 RPM パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.1000.169-2.x86_64.rpm)</br>[SQL Server エージェント RPM パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.1000.169-2.x86_64.rpm)</br>[SSIS パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM パッケージ | 14.0.1000.169-2 | [mssql-server エンジン RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.1000.169-2.x86_64.rpm)</br>[高可用性 RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.1000.169-2.x86_64.rpm)</br>[フルテキスト検索 RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.1000.169-2.x86_64.rpm)</br>[SQL Server エージェント RPM パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.1000.169-2.x86_64.rpm) | 
| Ubuntu 16.04 Debian パッケージ | 14.0.1000.169-2 | [エンジン Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.1000.169-2_amd64.deb)</br>[高可用性 Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.1000.169-2_amd64.deb)</br>[フルテキスト検索 Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.1000.169-2_amd64.deb)</br>[SQL Server エージェント Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.1000.169-2_amd64.deb)<br/>[SSIS パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a name="known-issues"></a>既知の問題

以下のセクションでは、Linux 上の [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] の一般公開 (GA) リリースに関する既知の問題について説明します。

#### <a name="general"></a>全般

- [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] がインストールされているホスト名の長さは 15 文字以下でなければなりません。 

    - **解決方法**:/etc/hostname の名前を 15 文字以下に変更します。

- システム時刻を手動で過去の時間に戻して設定すると、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] は [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 内の内部システム時刻の更新を停止します。

    - **解決方法**:[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]を再起動します。

- サポートされているのは単一インスタンスのインストールのみです。

    - **解決方法**:特定のホストに複数のインスタンスが必要な場合は、VM または Docker コンテナーの使用を検討してください。 

- [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Configuration Manager は [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] on Linux には接続できません。

- **sa** ログインの既定の言語は English (英語) です。

    - **解決方法**:**ALTER LOGIN** ステートメントを使用して **sa** ログインの言語を変更します。

#### <a name="databases"></a>データベース

- mssql-conf ユーティリティを使って master データベースを移動することはできません。 他のシステム データベースは mssql-conf で移動できます。

- Windows 上の [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] にバックアップされたデータベースを復元する場合は、Transact-SQL ステートメントで **WITH MOVE** 句を使用する必要があります。

- トランスポート層セキュリティ (TLS) の特定のアルゴリズム (暗号スイート) は、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] on Linux では正常に機能しません。 この結果、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] に接続しようとすると接続エラーが発生し、高可用性グループのレプリカ間の接続を確立する際に問題が発生します。

   - **解決方法**:次の手順を実行して、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] on Linux 用の **mssql.conf** 構成スクリプトを変更して、問題のある暗号スイートを無効にします。

      1. /var/opt/mssql/mssql.conf に次の内容を追加します。

      ```
      [network]
      tlsciphers= AES256-GCM-SHA384:AES128-GCM-SHA256:AES256-SHA256:AES128-SHA256:AES256-SHA:AES128-SHA:!ECDHE-RSA-AES128-GCM-SHA256:!ECDHE-RSA-AES256-GCM-SHA384:!ECDHE-ECDSA-AES256-GCM-SHA384:!ECDHE-ECDSA-AES128-GCM-SHA256:!ECDHE-ECDSA-AES256-SHA384:!ECDHE-ECDSA-AES128-SHA256:!ECDHE-ECDSA-AES256-SHA:!ECDHE-ECDSA-AES128-SHA:!ECDHE-RSA-AES256-SHA384:!ECDHE-RSA-AES128-SHA256:!ECDHE-RSA-AES256-SHA:!ECDHE-RSA-AES128-SHA:!DHE-RSA-AES256-GCM-SHA384:!DHE-RSA-AES128-GCM-SHA256:!DHE-RSA-AES256-SHA:!DHE-RSA-AES128-SHA:!DHE-DSS-AES256-SHA256:!DHE-DSS-AES128-SHA256:!DHE-DSS-AES256-SHA:!DHE-DSS-AES128-SHA:!DHE-DSS-DES-CBC3-SHA:!NULL-SHA256:!NULL-SHA
      ```

         >[!NOTE]
         >In the preceding code, `!` negates the expression. This tells OpenSSL to not use the following cipher suite.  

      1. 次のコマンドを使用して [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] を再起動します。

      ```bash
      sudo systemctl restart mssql-server
      ```

- インメモリ OLTP を使用する Windows 上の [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] データベースは、Linux 上の [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] では復元できません。 インメモリ OLTP を使用する [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] データベースを復元するには、最初に Windows 上でデータベースを [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] または [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] にアップグレードしてから、バックアップ/復元またはデタッチ/アタッチを使用して [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] on Linux に移動します。

- ユーザー権限 **ADMINISTER BULK OPERATIONS** は、現時点で Linux ではサポートされていません。

#### <a name="networking"></a>ネットワーク

リンク サーバーや可用性グループなど、sqlservr プロセスからの送信 TCP 接続に関連する機能は、次の両方の条件が満たされている場合は動作しない可能性があります。

1. ターゲット サーバーは、IP アドレスではなくホスト名として指定されます。

1. カーネルでは、ソース インスタンスの IPv6 が無効になっています。 システムのカーネルで IPv6 が有効になっているかどうかを確認するには、次のすべてのテストに合格する必要があります。

   - `cat /proc/cmdline` は、現在のカーネルのブート コマンドラインを出力します。 この出力に `ipv6.disable=1` を含めることはできません。
   - /proc/sys/net/ipv6/ ディレクトリが存在している必要があります。
   - `socket(AF_INET6, SOCK_STREAM, IPPROTO_IP)` を呼び出す C プログラムが成功する必要があります。syscall は、fd! =-1 を返して EAFNOSUPPORT で失敗しない必要があります。

正確なエラーは、機能によって異なります。 リンク サーバーの場合、これはログイン タイムアウト エラーとして現れます。 可用性グループの場合、セカンダリの `ALTER AVAILABILITY GROUP JOIN` DDL は 5 分後に失敗し、ダウンロード構成のタイムアウト エラーが発生します。

この問題を回避するには、次のいずれかのようにします。

1. ホスト名ではなく IP を使用して、TCP 接続のターゲットを指定します。

1. ブート コマンドラインから `ipv6.disable=1` を削除して、カーネルで IPv6 を有効にします。 これを行う方法は、Linux ディストリビューションとブートローダー (grub など) によって異なります。 IPv6 を無効にする場合でも、`sysctl` 構成 (たとえば、`/etc/sysctl.conf`) で `net.ipv6.conf.all.disable_ipv6 = 1` を設定することによって無効にすることもできます。 この場合も、システムのネットワーク アダプターが IPv6 アドレスを取得できませんが、sqlservr の機能を使用できるようになります。

#### <a name="network-file-system-nfs"></a>Network File System (NFS)
運用環境で **Network File System (NFS)** のリモート共有を使用する場合は、次のサポート要件に注意してください。

- NFS バージョン **4.2 以上**を使用してください。 前のバージョンの NFS では、最新のファイル システムに共通する、fallocate やスパース ファイルの作成などの必要な機能がサポートされていません。
- NFS マウント上の **/var/opt/mssql** ディレクトリのみが検索されます。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] システム バイナリなどの他のファイルはサポートされていません。
- リモート共有をマウントするときに NFS クライアントが 'nolock' オプションを使用していることを確認してください。

#### <a name="localization"></a>ローカリゼーション

- セットアップ時にロケールが英語 (en_us) でない場合は、bash セッション/ターミナルで UTF-8 エンコードを使用する必要があります。 ASCII エンコードを使用すると、次のようなエラーが表示される場合があります。

   ```
   UnicodeEncodeError: 'ascii' codec can't encode character u'\xf1' in position 8: ordinal not in range(128)
   ```

   UTF-8 エンコードを使用できない場合は、MSSQL_LCID 環境変数を使用してセットアップを実行し、使用する言語選択を指定します。

   ```bash
   sudo MSSQL_LCID=<LcidValue> /opt/mssql/bin/mssql-conf setup
   ```

- mssql-conf セットアップを実行していて、英語以外の [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のインストールを実行すると、ローカライズされたテキストの後に "SQL Server を構成中..." という不適切な拡張文字が表示されます。 または、ラテン語以外のインストールの場合、文が完全に欠落する可能性があります。 欠落している文には、次のローカライズされた文字列が表示される必要があります。"ライセンス PID は正常に処理されました。 新しいエディションは [\<Name\> edition] です。" この文字列は情報提供のみを目的とした出力であり、次の [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 累積更新プログラムでは、すべての言語でこの値に対応します。 これは、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の正常なインストールには影響しません。 

#### <a name="full-text-search"></a>フルテキスト検索

- このリリースでは、Office ドキュメントのフィルターを含め、すべてのフィルターが使用できるわけではありません。 サポートされているフィルターの一覧については、[Linux への SQL Server フルテキスト検索のインストール](sql-server-linux-setup-full-text-search.md#filters)に関するページを参照してください。

#### <a id="ssis"></a> SQL Server Integration Services (SSIS)

- **mssql-server-is** パッケージは、このリリースの SUSE ではサポートされていません。 現時点では、Ubuntu と Red Hat Enterprise Linux (RHEL) でサポートされています。

- Linux CTP 2.1 Refresh 以降の [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] の場合、[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] パッケージでは、Linux で ODBC 接続を使用できます。 この機能は [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] と MySQL ODBC ドライバーでテストされていますが、ODBC 仕様に準拠するあらゆる Unicode ODBC ドライバーでも動作することが予想されます。 デザイン時、DSN または接続文字列を指定し、ODBC データに接続できます。Windows 認証を使用することもできます。 詳細については、[Linux での ODBC サポートの告知ブログ記事](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/)を参照してください。

- Linux 上で SSIS パッケージを実行する場合、このリリースでは次の機能はサポートされていません。
  - [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] カタログ データベース
  - SQL エージェントでスケジュールされたパッケージの実行
  - [Windows 認証]
  - サードパーティ コンポーネント
  - 変更データ キャプチャ (CDC)
  - [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] スケール アウト
  - SSIS 用の Azure Feature Pack
  - Hadoop と HDFS のサポート
  - Microsoft Connector for SAP BW

現在サポートされていない、または制限付きでサポートされている組み込み SSIS コンポーネントの一覧については、[Linux の SSIS の制限事項と既知の問題](sql-server-linux-ssis-known-issues.md#components)に関するページを参照してください。

Linux の SSIS の詳細については、次の記事を参照してください。
-   [SSIS の Linux サポートをお知らせするブログ記事](https://blogs.msdn.microsoft.com/ssis/2017/05/17/ssis-helsinki-is-available-in-sql-server-vnext-ctp2-1/)。
-   [Linux に SQL Server Integration Services (SSIS) をインストールする](sql-server-linux-setup-ssis.md)
-   [SSIS で Linux 上のデータの抽出、変換、読み込みを行う](sql-server-linux-migrate-ssis.md)

#### <a id="ssms"></a> SQL Server Management Studio (SSMS)

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] on Linux に接続されている Windows の [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] には、次の制限事項が適用されます。

- メンテナンス プランはサポートされていません。

- [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] の管理データ ウェアハウス (MDW) とデータ コレクターはサポートされていません。 

- Windows 認証または Windows イベント ログ オプションを備えた [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] の UI コンポーネントは、Linux では機能しません。 これらの機能は、SQL ログインなどの他のオプションと共に引き続き使用できます。 

- 保持するログ ファイルの数は変更できません。

## <a name="next-steps"></a>次の手順

作業を開始するには、次のクイック スタートを参照してください。

- [Red Hat Enterprise Linux へのインストール](quickstart-install-connect-red-hat.md)
- [SUSE Linux Enterprise Server へのインストール](quickstart-install-connect-suse.md)
- [Ubuntu へのインストール](quickstart-install-connect-ubuntu.md)
- [Docker 上での実行](quickstart-install-connect-ubuntu.md)
- [Azure での SQL VM プロビジョニング](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=/sql/toc/toc.json)
- [実行と接続 - クラウド](quickstart-install-connect-clouds.md)

よく寄せられる質問に対する回答については、[SQL Server on Linux に関してよく寄せられる質問](sql-server-linux-faq.md)に関するページを参照してください。
