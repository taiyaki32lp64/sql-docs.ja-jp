---
title: RHEL に SQL Server を無人インストールする
titleSuffix: SQL Server
description: SQL Server スクリプト サンプル - Red Hat Enterprise Linux への無人インストール (RHEL)
ms.custom: seo-lt-2019
author: VanMSFT
ms.author: vanto
ms.date: 10/02/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: dc37a110b82113f2a96bd46be914c06a43c1a0ea
ms.sourcegitcommit: 035ad9197cb9799852ed705432740ad52e0a256d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/31/2019
ms.locfileid: "75558647"
---
# <a name="sample-unattended-sql-server-installation-script-for-red-hat-enterprise-linux"></a>サンプル:Red Hat Enterprise Linux 用の無人 SQL Server インストール スクリプト

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

このサンプル Bash スクリプトでは、対話式の入力なしで Red Hat Enterprise Linux (RHEL) に SQL Server 2017 をインストールします。 データベース エンジン、SQL Server コマンドライン ツール、SQL Server エージェントのインストール例を示し、インストール後の手順を行います。 必要に応じてフルテキスト検索をインストールして管理ユーザーを作成することができます。

> [!TIP]
> 無人インストール スクリプトが不要な場合は、SQL Server をインストールする最も簡単な方法は [Red Hat のクイックスタート](quickstart-install-connect-red-hat.md)に従うことです。 その他の設定情報については、[SQL Server on Linux のインストール ガイダンス](sql-server-linux-setup.md)を参照してください。

## <a name="prerequisites"></a>前提条件

- SQL Server on Linux を実行するには、少なくとも 2 GB のメモリが必要です。
- ファイル システムは **XFS** または **EXT4** である必要があります。 **BTRFS** などの他のファイル システムはサポートされていません。
- 他のシステム要件については、[SQL Server on Linux のシステム要件](sql-server-linux-setup.md#system)に関する記事を参照してください。

## <a name="sample-script"></a>サンプル スクリプト
サンプル スクリプトをファイルに保存し、カスタマイズするには、スクリプト内の変数値を置き換えます。 スクリプト ファイルから削除するのであれば、スクリプト変数を環境変数として設定することもできます。

```bash
#!/bin/bash -e

# Use the following variables to control your install:

# Password for the SA user (required)
MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>'

# Product ID of the version of SQL server you're installing
# Must be evaluation, developer, express, web, standard, enterprise, or your 25 digit product key
# Defaults to developer
MSSQL_PID='evaluation'

# Install SQL Server Agent (recommended)
SQL_ENABLE_AGENT='y'

# Install SQL Server Full Text Search (optional)
# SQL_INSTALL_FULLTEXT='y'

# Create an additional user with sysadmin privileges (optional)
# SQL_INSTALL_USER='<Username>'
# SQL_INSTALL_USER_PASSWORD='<YourStrong!Passw0rd>'

if [ -z $MSSQL_SA_PASSWORD ]
then
  echo Environment variable MSSQL_SA_PASSWORD must be set for unattended install
  exit 1
fi

echo Adding Microsoft repositories...
sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017.repo
sudo curl -o /etc/yum.repos.d/msprod.repo https://packages.microsoft.com/config/rhel/7/prod.repo

echo Installing SQL Server...
sudo yum install -y mssql-server

echo Running mssql-conf setup...
sudo MSSQL_SA_PASSWORD=$MSSQL_SA_PASSWORD \
     MSSQL_PID=$MSSQL_PID \
     /opt/mssql/bin/mssql-conf -n setup accept-eula

echo Installing mssql-tools and unixODBC developer...
sudo ACCEPT_EULA=Y yum install -y mssql-tools unixODBC-devel

# Add SQL Server tools to the path by default:
echo Adding SQL Server tools to your path...
echo PATH="$PATH:/opt/mssql-tools/bin" >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc

# Optional Enable SQL Server Agent :
if [ ! -z $SQL_ENABLE_AGENT ]
then
  echo Enable SQL Server Agent...
  sudo /opt/mssql/bin/mssql-conf set sqlagent.enabled true
  sudo systemctl restart mssql-server
fi

# Optional SQL Server Full Text Search installation:
if [ ! -z $SQL_INSTALL_FULLTEXT ]
then
    echo Installing SQL Server Full-Text Search...
    sudo yum install -y mssql-server-fts
fi

# Configure firewall to allow TCP port 1433:
echo Configuring firewall to allow traffic on port 1433...
sudo firewall-cmd --zone=public --add-port=1433/tcp --permanent
sudo firewall-cmd --reload

# Example of setting post-installation configuration options
# Set trace flags 1204 and 1222 for deadlock tracing:
#echo Setting trace flags...
#sudo /opt/mssql/bin/mssql-conf traceflag 1204 1222 on

# Restart SQL Server after making configuration changes:
echo Restarting SQL Server...
sudo systemctl restart mssql-server

# Connect to server and get the version:
counter=1
errstatus=1
while [ $counter -le 5 ] && [ $errstatus = 1 ]
do
  echo Waiting for SQL Server to start...
  sleep 5s
  /opt/mssql-tools/bin/sqlcmd \
    -S localhost \
    -U SA \
    -P $MSSQL_SA_PASSWORD \
    -Q "SELECT @@VERSION" 2>/dev/null
  errstatus=$?
  ((counter++))
done

# Display error if connection failed:
if [ $errstatus = 1 ]
then
  echo Cannot connect to SQL Server, installation aborted
  exit $errstatus
fi

# Optional new user creation:
if [ ! -z $SQL_INSTALL_USER ] && [ ! -z $SQL_INSTALL_USER_PASSWORD ]
then
  echo Creating user $SQL_INSTALL_USER
  /opt/mssql-tools/bin/sqlcmd \
    -S localhost \
    -U SA \
    -P $MSSQL_SA_PASSWORD \
    -Q "CREATE LOGIN [$SQL_INSTALL_USER] WITH PASSWORD=N'$SQL_INSTALL_USER_PASSWORD', DEFAULT_DATABASE=[master], CHECK_EXPIRATION=ON, CHECK_POLICY=ON; ALTER SERVER ROLE [sysadmin] ADD MEMBER [$SQL_INSTALL_USER]"
fi

echo Done!
```

## <a name="running-the-script"></a>スクリプトの実行

スクリプトを実行するには

1. サンプルを任意のテキスト エディターに貼り付けて、`install_sql.sh` のように覚えやすい名前で保存します。

1. `MSSQL_SA_PASSWORD`、`MSSQL_PID`、その他の変更する他の変数をカスタマイズします。

1. スクリプトを実行可能としてマークする

   ```bash
   chmod +x install_sql.sh
   ```

1. スクリプトを実行する

   ```bash
   ./install_sql.sh
   ```

## <a name="understanding-the-script"></a>スクリプトの概要

Bash スクリプトで最初に実行されることは、いくつかの変数の設定です。  これらは、サンプルなどのスクリプト変数、または環境変数です。  変数 `MSSQL_SA_PASSWORD` は SQL Server のインストールに**必要**です。その他はスクリプト用に作成されたカスタム変数です。  サンプル スクリプトは次の手順を行います。

1. 公開 Microsoft GPG キーをインポートします。

1. SQL Server とコマンドライン ツール用の Microsoft リポジトリを登録します。

1. ローカル リポジトリを更新する

1. SQL Server をインストールする

1. ```MSSQL_SA_PASSWORD``` を使用して SQL Server を構成し、エンドユーザー使用許諾契約に自動的に同意します。

1. SQL Server コマンドライン ツールのエンドユーザー使用許諾契約に自動的に同意し、インストールして、unixodbc-dev パッケージをインストールします。

1. 使いやすいように SQL Server のコマンドライン ツールをパスに追加します。

1. 既定でスクリプト変数 ```SQL_INSTALL_AGENT``` が設定されている場合は、SQL Server エージェントをインストールします。

1. 変数 ```SQL_INSTALL_FULLTEXT``` が設定されている場合は、必要に応じて SQL Server フルテキスト検索をインストールします。

1. システム ファイアウォールで、別のシステムから SQL Server に接続するために必要な TCP 用のポート 1433 のブロックを解除します。

1. 必要に応じて、デッドロック トレース用にトレース フラグを設定します (行をコメント解除する必要があります)。

1. SQL Server がインストールされたので、動作するようにプロセスを再起動します。

1. エラー メッセージを非表示にして、SQL Server が適切にインストールされていることを確認します。

1. ```SQL_INSTALL_USER``` と ```SQL_INSTALL_USER_PASSWORD``` の両方が設定されている場合は、新しいサーバー管理者ユーザーを作成します。

## <a name="next-steps"></a>次のステップ

複数の無人インストールを簡略化し、適切な環境変数を設定するスタンドアロンの Bash スクリプトを作成します。  サンプル スクリプトが使用している変数を削除して、それらを独自の Bash スクリプトに含めることができます。

```bash
#!/bin/bash
export MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>'
export MSSQL_PID='evaluation'
export SQL_INSTALL_AGENT='y'
export SQL_INSTALL_USER='<Username>'
export SQL_INSTALL_USER_PASSWORD='<YourStrong!Passw0rd>'
export SQL_INSTALL_AGENT='y'
```

次に、Bash スクリプトを次のように実行します。
```bash
. ./my_script_name.sh
```

SQL Server on Linux の詳細については、[Live Share の概要](sql-server-linux-overview.md)に関する記事を参照してください。
