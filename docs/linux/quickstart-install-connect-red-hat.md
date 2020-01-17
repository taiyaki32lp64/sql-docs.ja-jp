---
title: RHEL:Linux 上に SQL Server をインストールする
titleSuffix: SQL Server
description: このクイックスタートでは、Red Hat Enterprise Linux (RHEL) に SQL Server 2017 または SQL Server 2019 をインストールしてから、sqlcmd を使用してデータベースを作成してクエリを実行する方法を示します。
author: VanMSFT
ms.custom: seo-lt-2019
ms.author: vanto
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 92503f59-96dc-4f6a-b1b0-d135c43e935e
ms.openlocfilehash: b93ea834e890981d3fd45fd999a05ae5b2b68042
ms.sourcegitcommit: 035ad9197cb9799852ed705432740ad52e0a256d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/31/2019
ms.locfileid: "75558439"
---
# <a name="quickstart-install-sql-server-and-create-a-database-on-red-hat"></a>クイック スタート:Red Hat に SQL Server をインストールし、データベースを作成する

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

このクイックスタートでは、Red Hat Enterprise Linux (RHEL) に SQL Server 2017 または SQL Server 2019 をインストールします。 次に、**sqlcmd** と接続して最初のデータベースを作成し、クエリを実行します。

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

このクイックスタートでは、Red Hat Enterprise Linux (RHEL) 7.3+ に SQL Server 2019 をインストールします。 次に、**sqlcmd** と接続して最初のデータベースを作成し、クエリを実行します。

::: moniker-end

> [!TIP]
> このチュートリアルには、ユーザー入力とインターネット接続が必要です。 [無人](sql-server-linux-setup.md#unattended)または[オフライン](sql-server-linux-setup.md#offline)のインストール手順について関心をお持ちの場合は、[SQL Server on Linux のインストール ガイダンス](sql-server-linux-setup.md)に関する記事を参照してください。

## <a name="prerequisites"></a>前提条件

RHEL 7.3、7.4、7.5、7.6 コンピューターには**少なくとも 2 GB** のメモリが必要です。

自分のコンピューターに Red Hat Enterprise Linux をインストールする方法については、[https://access.redhat.com/products/red-hat-enterprise-linux/evaluation](https://access.redhat.com/products/red-hat-enterprise-linux/evaluation) にお進みください。 Azure で RHEL 仮想マシンを作成することもできます。 「[Azure CLI を使用した Linux VM の作成と管理](https://docs.microsoft.com/azure/virtual-machines/linux/tutorial-manage-vm)」を参照し、`az vm create` の呼び出しで `--image RHEL` を使用します。

SQL Server の CTP または RC リリースを以前インストールしている場合、この手順を行う前に、古いリポジトリを削除する必要があります。 詳細は、[SQL Server 2017 と 2019 に Linux リポジトリを構成する](sql-server-linux-change-repo.md)方法に関するページを参照してください。

他のシステム要件については、[SQL Server on Linux のシステム要件](sql-server-linux-setup.md#system)に関する記事を参照してください。

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

## <a id="install"></a>SQL Server をインストールする

RHEL 上で SQL Server を構成するには、ターミナルで次のコマンドを実行して **mssql-server** パッケージをインストールします。

1. Microsoft SQL Server 2017 Red Hat リポジトリ構成ファイルをダウンロードします。

   ```bash
   sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017.repo
   ```

   > [!TIP]
   > SQL Server 2019 をインストールする場合は、代わりに SQL Server 2019 リポジトリを登録する必要があります。 SQL Server 2019 のインストールには、次のコマンドを使用します。
   >
   > ```bash
   > sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2019.repo
   > ```

2. 次のコマンドを実行して SQL Server をインストールします。

   ```bash
   sudo yum install -y mssql-server
   ```

3. パッケージのインストールが完了したら、**mssql-conf setup** を実行し、プロンプトに従って SA パスワードを設定し、エディションを選択します。

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

   > [!TIP]
   > 次の SQL Server 2017 エディションは無料でライセンスが付与されます。Evaluation、Developer、Express。

   > [!NOTE]
   > SA アカウントには必ず強力なパスワードを指定してください (大文字と小文字、10 進数の数字、英数字以外の記号を含む、最小 8 文字の長さ)。

4. 構成が完了したら、サービスが実行されていることを確認します。

   ```bash
   systemctl status mssql-server
   ```

5. リモート接続を許可するには、RHEL のファイアウォールで SQL Server ポートを開きます。 既定の SQL Server ポートは TCP 1433 です。 ファイアウォールに **FirewallD** を使用している場合、次のコマンドを使用できます。

   ```bash
   sudo firewall-cmd --zone=public --add-port=1433/tcp --permanent
   sudo firewall-cmd --reload
   ```

この時点で、SQL Server は RHEL コンピューター上で動作しており、使用する準備ができています。

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

## <a id="install"></a>SQL Server をインストールする

RHEL 上で SQL Server を構成するには、ターミナルで次のコマンドを実行して **mssql-server** パッケージをインストールします。

1. Microsoft SQL Server 2019 Red Hat リポジトリ構成ファイルをダウンロードします。

   ```bash
   sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2019.repo
   ```

2. 次のコマンドを実行して SQL Server をインストールします。

   ```bash
   sudo yum install -y mssql-server
   ```

3. パッケージのインストールが完了したら、**mssql-conf setup** を実行し、プロンプトに従って SA パスワードを設定し、エディションを選択します。

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

   > [!NOTE]
   > SA アカウントには必ず強力なパスワードを指定してください (大文字と小文字、10 進数の数字、英数字以外の記号を含む、最小 8 文字の長さ)。

4. 構成が完了したら、サービスが実行されていることを確認します。

   ```bash
   systemctl status mssql-server
   ```

5. リモート接続を許可するには、RHEL のファイアウォールで SQL Server ポートを開きます。 既定の SQL Server ポートは TCP 1433 です。 ファイアウォールに **FirewallD** を使用している場合、次のコマンドを使用できます。

   ```bash
   sudo firewall-cmd --zone=public --add-port=1433/tcp --permanent
   sudo firewall-cmd --reload
   ```

この時点で、SQL Server 2019 は RHEL コンピューター上で動作しており、使用する準備ができています。

::: moniker-end

## <a id="tools"></a>SQL Server コマンドライン ツールをインストールする

データベースを作成するには、SQL Server 上で Transact-SQL ステートメントを実行できるツールと接続する必要があります。 次の手順で SQL Server コマンドライン ツールの [sqlcmd](../tools/sqlcmd-utility.md) と [bcp](../tools/bcp-utility.md) をインストールします。

1. Microsoft Red Hat リポジトリ構成ファイルをダウンロードします。

   ```bash
   sudo curl -o /etc/yum.repos.d/msprod.repo https://packages.microsoft.com/config/rhel/7/prod.repo
   ```

1. 旧版の **mssql-tools** がインストールされている場合、古い unixODBC パッケージはすべて削除してください。

   ```bash
   sudo yum remove unixODBC-utf16 unixODBC-utf16-devel
   ```

1. 次のコマンドを実行し、unixODBC 開発者パッケージと共に **mssql-tools** をインストールします。

   ```bash
   sudo yum install -y mssql-tools unixODBC-devel
   ```

1. **PATH** 環境変数に `/opt/mssql-tools/bin/` を追加すると便利です。 完全なパスを指定せずにツールを実行できます。 次のコマンドを実行し、ログイン セッションと対話型/非ログイン セッションの両方の **PATH** を変更します。

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
   source ~/.bashrc
   ```

[!INCLUDE [Connect, create, and query data](../includes/sql-linux-quickstart-connect-query.md)]
