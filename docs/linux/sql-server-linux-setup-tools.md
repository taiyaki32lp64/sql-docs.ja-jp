---
title: Linux に SQL Server コマンドライン ツールをインストールする
titleSuffix: SQL Server
description: この記事では、Linux に SQL Server ツールをインストールする方法について説明します。
author: VanMSFT
ms.author: vanto
ms.date: 06/07/2019
ms.topic: conceptual
ms.prod: sql
ms.custom: sqlfreshmay19
ms.technology: linux
ms.assetid: eff8e226-185f-46d4-a3e3-e18b7a439e63
ms.openlocfilehash: 23610c3144c7cf03a4c93be900bfc60a449448ed
ms.sourcegitcommit: 512acc178ec33b1f0403b5b3fd90e44dbf234327
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/08/2019
ms.locfileid: "72041251"
---
# <a name="install-sqlcmd-and-bcp-the-sql-server-command-line-tools-on-linux"></a>Linux に SQL Server コマンドライン ツール sqlcmd および bcp をインストールする

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

次の手順で、コマンドライン ツール、Microsoft ODBC ドライバー、およびそれらの依存関係をインストールします。 **mssql-tools** パッケージには次のものが含まれます。

- **sqlcmd**:コマンド ライン ユーティリティ
- **bcp**:一括インポート エクスポート ユーティリティ

ご使用のプラットフォームに対応するツールをインストールします。

- [Red Hat Enterprise Linux](#RHEL)
- [Ubuntu](#ubuntu)
- [SUSE Linux Enterprise Server](#SLES)
- [macOS](#macos)
- [Docker](#docker)

この記事では、コマンドライン ツールをインストールする方法について説明します。 **sqlcmd** または **bcp** の使用方法の例を参照するには、トピックの最後にある[リンク](#next-steps)をご覧ください。

## <a name="a-idrhelainstall-tools-on-rhel-7"></a><a id="RHEL"><a/>RHEL 7 にツールをインストールする

次の手順を使用して、Red Hat Enterprise Linux に **mssql-tools** をインストールします。 

1. スーパーユーザー モードにします。

   ```bash
   sudo su
   ```

1. Microsoft Red Hat リポジトリ構成ファイルをダウンロードします。

   ```bash
   curl https://packages.microsoft.com/config/rhel/7/prod.repo > /etc/yum.repos.d/msprod.repo
   ```

1. スーパーユーザー モードを終了します。

   ```bash
   exit
   ```

1. 旧版の **mssql-tools** がインストールされている場合、古い unixODBC パッケージはすべて削除してください。

   ```bash
   sudo yum remove mssql-tools unixODBC-utf16-devel
   ```

1. 次のコマンドを実行し、unixODBC 開発者パッケージと共に **mssql-tools** をインストールします。

   ```bash
   sudo yum install mssql-tools unixODBC-devel
   ```

   > [!Note] 
   > 最新バージョンの **mssql-tools** に更新するには、次のコマンドを実行します。
   >    ```bash
   >   sudo yum check-update
   >   sudo yum update mssql-tools
   >   ```

1. **省略可能**:bash シェルで **PATH** 環境変数に `/opt/mssql-tools/bin/` を追加します。

   ログイン セッション用に bash シェルから **sqlcmd/bcp** にアクセスできるようにするには、次のコマンドで **~/.bash_profile** ファイルの **PATH** を変更します。

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
   ```

   対話型/非ログイン セッション用に bash シェルから **sqlcmd/bcp** にアクセスできるようにするには、次のコマンドで **~/.bashrc** ファイルの **PATH** を変更します。

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
   source ~/.bashrc
   ```

## <a id="ubuntu"></a>Ubuntu 16.04 にツールをインストールする

次の手順を使用して、Ubuntu に **mssql-tools** をインストールします。 

1. パブリック リポジトリの GPG キーをインポートします。

   ```bash
   curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

1. Microsoft Ubuntu リポジトリを登録します。

   ```bash
   curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list | sudo tee /etc/apt/sources.list.d/msprod.list
   ```

1. ソース一覧を更新し、unixODBC 開発者パッケージを使用してインストール コマンドを実行します。

   ```bash
   sudo apt-get update 
   sudo apt-get install mssql-tools unixodbc-dev
   ```

   > [!Note] 
   > 最新バージョンの **mssql-tools** に更新するには、次のコマンドを実行します。
   >    ```bash
   >   sudo apt-get update 
   >   sudo apt-get install mssql-tools 
   >   ```

1. **省略可能**:bash シェルで **PATH** 環境変数に `/opt/mssql-tools/bin/` を追加します。

   ログイン セッション用に bash シェルから **sqlcmd/bcp** にアクセスできるようにするには、次のコマンドで **~/.bash_profile** ファイルの **PATH** を変更します。

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
   ```

   対話型/非ログイン セッション用に bash シェルから **sqlcmd/bcp** にアクセスできるようにするには、次のコマンドで **~/.bashrc** ファイルの **PATH** を変更します。

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
   source ~/.bashrc
   ```

## <a id="SLES"></a>SLES 12 にツールをインストールする

次の手順を使用して、SUSE Linux Enterprise Server に **mssql-tools** をインストールします。 

1. Zypper に Microsoft SQL Server リポジトリを追加します。

   ```bash
   sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/prod.repo 
   sudo zypper --gpg-auto-import-keys refresh
   ```

1. unixODBC 開発者パッケージと共に **mssql-tools** をインストールします。

   ```bash
   sudo zypper install mssql-tools unixODBC-devel
   ```

   > [!Note] 
   > 最新バージョンの **mssql-tools** に更新するには、次のコマンドを実行します。
   >    ```bash
   >   sudo zypper refresh
   >   sudo zypper update mssql-tools
   >   ```

1. **省略可能**:bash シェルで **PATH** 環境変数に `/opt/mssql-tools/bin/` を追加します。

   ログイン セッション用に bash シェルから **sqlcmd/bcp** にアクセスできるようにするには、次のコマンドで **~/.bash_profile** ファイルの **PATH** を変更します。

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
   ```

   対話型/非ログイン セッション用に bash シェルから **sqlcmd/bcp** にアクセスできるようにするには、次のコマンドで **~/.bashrc** ファイルの **PATH** を変更します。

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
   source ~/.bashrc
   ```

## <a id="macos"></a>macOS にツールをインストールする

**sqlcmd** と **bcp** のプレビューが macOS で使用できるようになりました。 詳しくは、[お知らせ](https://blogs.technet.microsoft.com/dataplatforminsider/2017/05/16/sql-server-command-line-tools-for-macos-released/)をご覧ください。

" *[Homebrew](https://brew.sh) をインストールします (まだインストールしていない場合)。* "

        /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

Mac El Capitan および Sierra のツールをインストールするには、次のコマンドを使用します。

```
# brew untap microsoft/mssql-preview if you installed the preview version 
brew tap microsoft/mssql-release https://github.com/Microsoft/homebrew-mssql-release
brew update
brew install mssql-tools
#for silent install: 
#HOMEBREW_NO_ENV_FILTERING=1 ACCEPT_EULA=y brew install mssql-tools
```

## <a id="docker"></a> Docker

[Docker コンテナー内で SQL Server を実行する](quickstart-install-connect-docker.md)場合、SQL Server のコマンドライン ツールは SQL Server Linux コンテナー イメージに既に含まれています。 対話型の Bash シェルで実行中のコンテナーにアタッチする場合は、ツールをローカルで実行できます。

## <a name="offline-installation"></a>オフライン インストール

[!INCLUDE[SQL Server Linux offline package installation](../includes/sql-server-linux-offline-package-install-intro.md)]

1. 最初に、ご使用の Linux ディストリビューション用の **mssql-tools** パッケージを見つけてコピーします。

   | Linux ディストリビューション | **mssql-tools** パッケージの場所 |
   |---|---|
   | Red Hat | [https://packages.microsoft.com/rhel/7.3/prod](https://packages.microsoft.com/rhel/7.3/prod) |
   | SLES | [https://packages.microsoft.com/sles/12/prod](https://packages.microsoft.com/sles/12/prod)|
   | Ubuntu 16.04 | [https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/mssql-tools](https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/mssql-tools) |

1. また、**msodbcsql.h** パッケージも見つけてコピーします。これは依存関係です。 **msodbcsql** パッケージは、**unixODBC-devel** (Red Hat and SLES) または **unixodbc-dev** (Ubuntu) にも依存しています。 **msodbcsql** パッケージの場所を次の表に示します。

   | Linux ディストリビューション | ODBC パッケージの場所 |
   |---|---|
   | Red Hat | [https://packages.microsoft.com/rhel/7.3/prod](https://packages.microsoft.com/rhel/7.3/prod) |
   | SLES | [https://packages.microsoft.com/sles/12/prod](https://packages.microsoft.com/sles/12/prod)|
   | Ubuntu 16.04 | [**msodbcsql**](https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/msodbcsql)<br/>[**unixodbc-dev**](https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/u/unixodbc/) |

1. **ダウンロードしたパッケージを Linux マシンに移動します**。 別のコンピューターを使用してパッケージをダウンロードした場合、パッケージをお使いの Linux コンピューターに移動する 1 つの方法は **scp** コマンドを使用することです。

1. **パッケージをインストールします**。**mssql-tools** および **msodbc** パッケージをインストールします。 依存関係のエラーが発生した場合は無視して次の手順に進みます。

    | プラットフォーム | パッケージのインストール コマンド |
    |-----|-----|
    | Red Hat | `sudo yum localinstall msodbcsql-<version>.rpm`<br/>`sudo yum localinstall mssql-tools-<version>.rpm` |
    | SLES | `sudo zypper install msodbcsql-<version>.rpm`<br/>`sudo zypper install mssql-tools-<version>.rpm` |
    | Ubuntu | `sudo dpkg -i msodbcsql_<version>.deb`<br/>`sudo dpkg -i mssql-tools_<version>.deb` |

1. **不足している依存関係を解決します**。この時点で、依存関係が不足している場合があります。 そうでない場合は、この手順は省略します。 場合によっては、それらの依存関係を手動で見つけてインストールする必要があります。

    RPM パッケージでは、次のコマンドを使用して必要な依存関係を調べることができます。

    ```bash
    rpm -qpR msodbcsql-<version>.rpm
    rpm -qpR mssql-tools-<version>.rpm
    ```

    Debian パッケージでは、それらの依存関係を含む承認されたリポジトリにアクセスできる場合は、**apt-get** コマンドを使用することが最も簡単な解決方法です。

    ```bash
    sudo apt-get -f install
    ```

    > [!NOTE]
    > このコマンドによって、SQL Server パッケージのインストールも完了します。

    ご使用の Debian パッケージでこの方法がうまく行かない場合は、次のコマンドを使用して必要な依存関係を調べることができます。

    ```bash
    dpkg -I msodbcsql_<version>_amd64.deb | grep "Depends:"
    dpkg -I mssql-tools_<version>_amd64.deb | grep "Depends:"
    ```

## <a name="next-steps"></a>次の手順

**sqlcmd** を使用して SQL Server に接続してデータベースを作成する方法の例については、次のクイックスタートのいずれかをご覧ください。

- [Red Hat Enterprise Linux へのインストール](quickstart-install-connect-red-hat.md)
- [SUSE Linux Enterprise Server へのインストール](quickstart-install-connect-suse.md)
- [Ubuntu へのインストール](quickstart-install-connect-ubuntu.md)
- [Docker 上での実行](quickstart-install-connect-ubuntu.md)

**bcp** を使用して、データの一括インポートやエクスポートを行う方法の例については、「[SQL Server on Linux にデータを一括コピーする](sql-server-linux-migrate-bcp.md)」をご覧ください。
