---
title: SQL Server 2017 および 2019 用に Linux リポジトリを構成する
description: Linux 上の SQL Server 2019 および SQL Server 2017 用にソース リポジトリの確認と構成を行います。 このソース リポジトリは、インストールおよびアップグレード中に適用される SQL Server のバージョンに影響します。
author: VanMSFT
ms.author: vanto
ms.date: 01/07/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
zone_pivot_groups: ld2-linux-distribution
ms.openlocfilehash: c1def0c2cfbdc4b3feed191e9eb2673b8e788f82
ms.sourcegitcommit: 76fb3ecb79850a8ef2095310aaa61a89d6d93afd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/09/2020
ms.locfileid: "75776381"
---
# <a name="configure-repositories-for-installing-and-upgrading-sql-server-on-linux"></a>SQL Server on Linux のインストールとアップグレードを行うためのリポジトリを構成する

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

::: zone pivot="ld2-rhel"
この記事では、Linux 上で SQL Server 2017 と SQL Server 2019 のインストールとアップグレードを行うためのリポジトリを正しく構成する方法について説明します。 現在、お客様は **Red Hat (RHEL)** を選択しています (上部)。
::: zone-end

::: zone pivot="ld2-sles"
この記事では、Linux 上で SQL Server 2017 と SQL Server 2019 のインストールとアップグレードを行うためのリポジトリを正しく構成する方法について説明します。 現在、お客様は **SUSE (SLES)** を選択しています (上部)。
::: zone-end

::: zone pivot="ld2-ubuntu"
この記事では、Linux 上で SQL Server 2017 と SQL Server 2019 のインストールとアップグレードを行うためのリポジトリを正しく構成する方法について説明します。 現在、お客様は **Ubuntu** を選択しています (上部)。
::: zone-end

> [!TIP]
> SQL Server 2019 が使用できるようになりました。 お試しになる場合は、この記事を利用して新しい **mssql-server-2019** リポジトリを構成します。 その後、[インストール ガイド](sql-server-linux-setup.md)に記載されている手順に従ってインストールしてください。

## <a id="repositories"></a> リポジトリ

SQL Server on Linux をインストールする場合は、Microsoft リポジトリを構成する必要があります。 このリポジトリを使って、データベース エンジンのパッケージ (**mssql-server**) と、関連する SQL Server のパッケージを入手します。 現在、5 つの主要なリポジトリがあります。

| リポジトリ | Name | [説明] |
|---|---|---|
| **2019** | **mssql-server-2019** | SQL Server 2019 Cumulative Update (CU) リポジトリ。 |
| **2019 GDR** | **mssql-server-2019-gdr** | 重要な更新プログラム専用の SQL Server 2019 GDR リポジトリ。 |
| **2019 Preview** | **mssql-server-preview** | SQL Server 2019 プレビューおよび RC リポジトリ。 |
| **2017** | **mssql-server-2017** | SQL Server 2017 Cumulative Update (CU) リポジトリ。 |
| **2017 GDR** | **mssql-server-2017-gdr** | 重要な更新プログラム専用の SQL Server 2017 GDR リポジトリ。 |

## <a id="cuversusgdr"></a> 累積的な更新プログラムと GDR

各ディストリビューションに対して、主に 2 種類のリポジトリがあることに注意する必要があります。

- **累積的な更新プログラム (CU)** :累積的な更新プログラム (CU) リポジトリには、ベースとなる SQL Server リリースのパッケージと、そのリリース以降のすべてのバグ修正や機能強化が含まれます。 累積的な更新プログラムは、リリース バージョン (SQL Server 2019 など) に固有のものです。 これらは一定の頻度でリリースされます。

- **GDR**:GDR リポジトリには、ベースとなる SQL Server リリースのパッケージと、そのリリース以降の重要な修正とセキュリティ更新プログラムのみが含まれます。 これらの更新プログラムは、次の CU リリースにも追加されます。

CU および GDR の各リリースには、SQL Server の完全なパッケージと、そのリポジトリに対する以前の更新プログラムがすべて含まれています。 SQL Server 用に構成したリポジトリを変更することにより、GDR リリースから CU リリースへの更新がサポートされています。 また、お使いのメジャー バージョン内の任意のリリースに[ダウングレード](sql-server-linux-setup.md#rollback)することもできます (例:2017)。

> [!NOTE]
> リポジトリを変更すれば、GDR リリースから CU リリースにいつでも更新できます。 CU リリースから GDR リリースへの更新はサポートされていません。

## <a name="configure-repositories"></a>リポジトリの構成

::: zone pivot="ld2-rhel"
以下のセクションに記載されている手順に従って、Red Hat Enterprise Server (RHEL) 上でリポジトリを構成します。
::: zone-end

::: zone pivot="ld2-sles"
以下のセクションに記載されている手順に従って、SUSE Linux Enterprise Server (SLES) 上でリポジトリを構成します。
::: zone-end

::: zone pivot="ld2-ubuntu"
以下のセクションに記載されている手順に従って、Ubuntu 上でリポジトリを構成します。
::: zone-end

## <a name="check-for-previously-configured-repositories"></a>以前に構成したリポジトリの確認

<!--RHEL-->
::: zone pivot="ld2-rhel"
まず、SQL Server リポジトリを既に登録しているかどうかを確認します。

1. 次のコマンドを使って、 **/etc/yum.repos.d** ディレクトリ内のファイルを表示します。

   ```bash
   sudo ls /etc/yum.repos.d
   ```

2. SQL Server ディレクトリを構成しているファイルを探します (**mssql-server.repo** など)。

3. そのファイルの内容を出力します。

   ```bash
   sudo cat /etc/yum.repos.d/mssql-server.repo
   ```

4. **name** プロパティが構成されているリポジトリです。 この記事の「[リポジトリ](#repositories)」セクションにある表を使って、それを識別できます。

::: zone-end

<!--SLES-->
::: zone pivot="ld2-sles"
まず、SQL Server リポジトリを既に登録しているかどうかを確認します。

1. **zypper info** を使って、以前に構成したリポジトリに関する情報を取得します。

   ```bash
   sudo zypper info mssql-server
   ```

2. **Repository** プロパティが構成されているリポジトリです。 この記事の「[リポジトリ](#repositories)」セクションにある表を使って、それを識別できます。

::: zone-end

<!--Ubuntu-->
::: zone pivot="ld2-ubuntu"
まず、SQL Server リポジトリを既に登録しているかどうかを確認します。

1. **/etc/apt/sources.list** ファイルの内容を表示します。

   ```bash
   sudo cat /etc/apt/sources.list
   ```

2. mssql-server のパッケージ URL を確認します。 この記事の「[リポジトリ](#repositories)」セクションにある表を使って、それを識別できます。

::: zone-end

## <a name="remove-old-repository"></a>古いリポジトリの削除

<!--RHEL-->
::: zone pivot="ld2-rhel"
必要に応じて、次のコマンドを使って古いリポジトリを削除します。

```bash
sudo rm -rf /etc/yum.repos.d/mssql-server.repo
```

このコマンドでは、前のセクションで識別されたファイルの名前が **mssql-server.repo** であることを仮定しています。

::: zone-end

<!--SLES-->
::: zone pivot="ld2-sles"
必要に応じて、古いリポジトリを削除します。 以前に構成したリポジトリの種類に基づいて、次のいずれかのコマンドを使います。

| リポジトリ | 削除するコマンド |
|---|---|
| **Preview (2019)** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server-preview'` |
| **2019 CU** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server-2019'` |
| **2019 GDR** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server-2019-gdr'`|
| **2017 CU** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server-2017'` |
| **2017 GDR** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server-2017-gdr'`|

::: zone-end

<!--Ubuntu-->
::: zone pivot="ld2-ubuntu"
必要に応じて、古いリポジトリを削除します。 以前に構成したリポジトリの種類に基づいて、次のいずれかのコマンドを使います。

| リポジトリ | 削除するコマンド |
|---|---|
| **Preview (2019)** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview xenial main'` |
| **2019 CU** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019 xenial main'` | 
| **2019 GDR** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019-gdr xenial main'` |
| **2017 CU** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017 xenial main'` | 
| **2017 GDR** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr xenial main'` |

::: zone-end

## <a name="configure-new-repository"></a>新しいリポジトリの構成

<!--RHEL-->
::: zone pivot="ld2-rhel"
SQL Server のインストールとアップグレードのために使用する新しいリポジトリを構成します。 次のコマンドのいずれかを使って、任意のリポジトリを構成します。

> [!NOTE]
> SQL Server 2019 の次のコマンドは、RHEL 8 リポジトリをポイントします。 RHEL 8 は、SQL Server に必要な python2 と共にプレインストールされていません。 詳細については、python2 のインストールと既定のインタープリターとしての構成に関する次のブログを参照してください: https://www.redhat.com/en/blog/installing-microsoft-sql-server-red-hat-enterprise-linux-8-beta 。
>
> RHEL 7 を使用している場合は、次のパスを `/rhel/8` ではなく `/rhel/7` に変更します。

| リポジトリ | Version | command |
|---|---|---|
| **2019 CU** | 2019 | `sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/8/mssql-server-2019.repo` |
| **2019 GDR** | 2019 | `sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/8/mssql-server-2019-gdr.repo` |
| **2017 CU** | 2017 | `sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017.repo` |
| **2017 GDR** | 2017 | `sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017-gdr.repo` |

::: zone-end

<!--SLES-->
::: zone pivot="ld2-sles"
SQL Server のインストールとアップグレードのために使用する新しいリポジトリを構成します。 次のコマンドのいずれかを使って、任意のリポジトリを構成します。

| リポジトリ | Version | command |
|---|---|---|
| **2019 CU** | 2019 | `sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2019.repo` |
| **2019 GDR** | 2019 | `sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2019-gdr.repo` |
| **2017 CU** | 2017 | `sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2017.repo` |
| **2017 GDR** | 2017 | `sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2017-gdr.repo` |

::: zone-end

<!--Ubuntu-->
::: zone pivot="ld2-ubuntu"
SQL Server のインストールとアップグレードのために使用する新しいリポジトリを構成します。

1. パブリック リポジトリの GPG キーをインポートします。

   ```bash
   sudo curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

2. 次のコマンドのいずれかを使って、任意のリポジトリを構成します。

   | リポジトリ | Version | command |
   |---|---|---|
   | **2019 CU** | 2019 | `sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2019.list)"` |
   | **2019 GDR** | 2019 | `sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2019-gdr.list)"` |
   | **2017 CU** | 2017 | `sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017.list)"` |
   | **2017 GDR** | 2017 | `sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017-gdr.list)"` |

3. **apt-get update** を実行します。

   ```bash
   sudo apt-get update
   ```

::: zone-end

## <a name="next-steps"></a>次のステップ

適切なリポジトリを構成したら、新しいリポジトリから、SQL Server と関連パッケージの[インストール](sql-server-linux-setup.md#platforms)や[更新](sql-server-linux-setup.md#upgrade)を始めることができます。

::: zone pivot="ld2-rhel"
> [!IMPORTANT]
> この時点で、[RHEL のクイックスタート](quickstart-install-connect-red-hat.md)を使うことにする場合は、既にターゲット リポジトリを構成してあることを忘れないでください。 チュートリアルに記載されているその手順を繰り返さないでください。 これは、GDR リポジトリを構成する場合に特に当てはまります。クイックスタートでは CU リポジトリが使われるためです。
::: zone-end

::: zone pivot="ld2-sles"
> [!IMPORTANT]
> この時点で、[SLES のクイックスタート](quickstart-install-connect-suse.md)を使うことにする場合は、既にターゲット リポジトリを構成してあることを忘れないでください。 チュートリアルに記載されているその手順を繰り返さないでください。 これは、GDR リポジトリを構成する場合に特に当てはまります。クイックスタートでは CU リポジトリが使われるためです。
::: zone-end

::: zone pivot="ld2-ubuntu"
> [!IMPORTANT]
> この時点で、[Ubuntu のクイックスタート](quickstart-install-connect-ubuntu.md)を使うことにする場合は、既にターゲット リポジトリを構成してあることを忘れないでください。 チュートリアルに記載されているその手順を繰り返さないでください。 これは、GDR リポジトリを構成する場合に特に当てはまります。クイックスタートでは CU リポジトリが使われるためです。
::: zone-end

Linux 上に SQL Server 2017 をインストールする方法について詳しくは、「[Linux 上の SQL Server のインストールのガイダンスについて](sql-server-linux-setup.md)」をご覧ください。
