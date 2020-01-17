---
title: SUSE:SQL Server on Linux のインストール
description: このクイックスタートでは、SUSE Linux Enterprise Server に SQL Server 2017 または SQL Server 2019 をインストールしてから、sqlcmd を使用してデータベースを作成してクエリを実行する方法を示します。
author: VanMSFT
ms.author: vanto
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 31ddfb80-f75c-4f51-8540-de6213cb68b8
ms.openlocfilehash: 811438987106a5eb73a914e5d7bbceb139cd5c37
ms.sourcegitcommit: 035ad9197cb9799852ed705432740ad52e0a256d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/31/2019
ms.locfileid: "75558635"
---
# <a name="quickstart-install-sql-server-and-create-a-database-on-suse-linux-enterprise-server"></a>クイック スタート:SUSE Linux Enterprise Server で SQL Server をインストールし、データベースを作成する

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

このクイックスタートでは、SQL Server 2017 または SQL Server 2019 を SUSE Linux Enterprise Server (SLES) v12 SP2 にインストールします。 次に、**sqlcmd** と接続して最初のデータベースを作成し、クエリを実行します。

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

このクイックスタートでは、SQL Server 2019 を SUSE Linux Enterprise Server (SLES) v12 にインストールします。 次に、**sqlcmd** と接続して最初のデータベースを作成し、クエリを実行します。

> [!IMPORTANT]
> SQL Server 2019 は、SUSE Enterprise Linux Server v12 SP2、SP3、または SP4 でサポートされています。

::: moniker-end

> [!TIP]
> このチュートリアルには、ユーザー入力とインターネット接続が必要です。 [無人](sql-server-linux-setup.md#unattended)または[オフライン](sql-server-linux-setup.md#offline)のインストール手順について関心をお持ちの場合は、[SQL Server on Linux のインストール ガイダンス](sql-server-linux-setup.md)に関する記事を参照してください。

## <a name="prerequisites"></a>前提条件

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

SLES v12 SP2 コンピューターには**少なくとも 2 GB** のメモリが必要です。 ファイル システムは **XFS** または **EXT4** である必要があります。 **BTRFS** などの他のファイル システムはサポートされていません。

::: moniker-end

<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

SLES v12 SP2、SP3、または SP4 のコンピューターには、**少なくとも 2 GB** のメモリが必要です。 ファイル システムは **XFS** または **EXT4** である必要があります。 **BTRFS** などの他のファイル システムはサポートされていません。

::: moniker-end

自分のコンピューターに SUSE Linux Enterprise Server をインストールする方法については、[https://www.suse.com/products/server](https://www.suse.com/products/server) にお進みください。 Azure で SLES 仮想マシンを作成することもできます。 「[Azure CLI を使用した Linux VM の作成と管理](https://docs.microsoft.com/azure/virtual-machines/linux/tutorial-manage-vm)」を参照し、`az vm create` の呼び出しで `--image SLES` を使用します。

SQL Server の CTP または RC リリースを以前インストールしている場合、この手順を行う前に、古いリポジトリを削除する必要があります。 詳細は、[SQL Server 2017 と 2019 に Linux リポジトリを構成する](sql-server-linux-change-repo.md)方法に関するページを参照してください。

> [!NOTE]
> 現時点では、Windows 10 用の [Windows Subsystem for Linux](https://msdn.microsoft.com/commandline/wsl/about) はインストール先としてサポートされていません。

他のシステム要件については、[SQL Server on Linux のシステム要件](sql-server-linux-setup.md#system)に関する記事を参照してください。

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

## <a id="install"></a>SQL Server をインストールする

SLES 上で SQL Server を構成するには、ターミナルで次のコマンドを実行して **mssql-server** パッケージをインストールします。

1. Microsoft SQL Server 2017 SLES リポジトリ構成ファイルをダウンロードします。

   ```bash
   sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2017.repo
   ```

   > [!TIP]
   > SQL Server 2019 をインストールする場合は、代わりに SQL Server 2019 リポジトリを登録する必要があります。 SQL Server 2019 のインストールには、次のコマンドを使用します。
   >
   > ```bash
   > sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2019.repo
   > ```

2. リポジトリを最新の情報に更新します。

   ```bash
   sudo zypper --gpg-auto-import-keys refresh 
   ```
   
3. 次のコマンドを実行して SQL Server をインストールします。

   ```bash
   sudo zypper install -y mssql-server
   ```

4. パッケージのインストールが完了したら、**mssql-conf setup** を実行し、プロンプトに従って SA パスワードを設定し、エディションを選択します。

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

   > [!TIP]
   > 次の SQL Server 2017 エディションは無料でライセンスが付与されます。Evaluation、Developer、Express。

   > [!NOTE]
   > SA アカウントには必ず強力なパスワードを指定してください (大文字と小文字、10 進数の数字、英数字以外の記号を含む、最小 8 文字の長さ)。

5. 構成が完了したら、サービスが実行されていることを確認します。

   ```bash
   systemctl status mssql-server
   ```

6. リモート接続を計画している場合は、必要に応じてファイアウォールで SQL Server の TCP ポート (既定値は 1433) も開きます。 SuSE ファイアウォールを使用している場合、 **/etc/sysconfig/SuSEfirewall2** 構成ファイルを編集する必要があります。 **FW_SERVICES_EXT_TCP** エントリを変更し、SQL Server ポート番号を含めます。

   ```
   FW_SERVICES_EXT_TCP="1433"
   ```

この時点で、SQL Server は SLES コンピューター上で動作しており、使用する準備ができています。

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

## <a id="install"></a>SQL Server をインストールする

SLES 上で SQL Server を構成するには、ターミナルで次のコマンドを実行して **mssql-server** パッケージをインストールします。

1. Microsoft SQL Server 2019 SLES リポジトリ構成ファイルをダウンロードします。

   ```bash
   sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2019.repo
   ```

2. リポジトリを最新の情報に更新します。

   ```bash
   sudo zypper --gpg-auto-import-keys refresh 
   ```
   
3. 次のコマンドを実行して SQL Server をインストールします。

   ```bash
   sudo zypper install -y mssql-server
   ```

4. パッケージのインストールが完了したら、**mssql-conf setup** を実行し、プロンプトに従って SA パスワードを設定し、エディションを選択します。

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

   > [!NOTE]
   > SA アカウントには必ず強力なパスワードを指定してください (大文字と小文字、10 進数の数字、英数字以外の記号を含む、最小 8 文字の長さ)。

5. 構成が完了したら、サービスが実行されていることを確認します。

   ```bash
   systemctl status mssql-server
   ```

6. リモート接続を計画している場合は、必要に応じてファイアウォールで SQL Server の TCP ポート (既定値は 1433) も開きます。 SuSE ファイアウォールを使用している場合、 **/etc/sysconfig/SuSEfirewall2** 構成ファイルを編集する必要があります。 **FW_SERVICES_EXT_TCP** エントリを変更し、SQL Server ポート番号を含めます。

   ```
   FW_SERVICES_EXT_TCP="1433"
   ```

この時点で、SQL Server 2019 は SLES コンピューター上で動作しており、使用する準備ができています。

::: moniker-end


## <a id="tools"></a>SQL Server コマンドライン ツールをインストールする

データベースを作成するには、SQL Server 上で Transact-SQL ステートメントを実行できるツールと接続する必要があります。 次の手順で SQL Server コマンドライン ツールの [sqlcmd](../tools/sqlcmd-utility.md) と [bcp](../tools/bcp-utility.md) をインストールします。

1. Zypper に Microsoft SQL Server リポジトリを追加します。

   ```bash
   sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/prod.repo 
   sudo zypper --gpg-auto-import-keys refresh
   ```

1. unixODBC 開発者パッケージと共に **mssql-tools** をインストールします。

   ```bash
   sudo zypper install -y mssql-tools unixODBC-devel
   ```

1. **PATH** 環境変数に `/opt/mssql-tools/bin/` を追加すると便利です。 完全なパスを指定せずにツールを実行できます。 次のコマンドを実行し、ログイン セッションと対話型/非ログイン セッションの両方の **PATH** を変更します。

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
   source ~/.bashrc
   ```

[!INCLUDE [Connect, create, and query data](../includes/sql-linux-quickstart-connect-query.md)]
