---
title: Linux および macOS に Microsoft ODBC Driver for SQL Server をインストールする | Microsoft Docs
ms.custom: ''
ms.date: 12/05/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- driver, installing
ms.assetid: f78b81ed-5214-43ec-a600-9bfe51c5745a
author: MightyPen
ms.author: v-jizho2
manager: kenvh
ms.openlocfilehash: 2c71bdf4628b74bd21346f37534339d8d83497b2
ms.sourcegitcommit: f3f83ef95399d1570851cd1360dc2f072736bef6
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 08/13/2019
ms.locfileid: "68984594"
---
# <a name="installing-the-microsoft-odbc-driver-for-sql-server-on-linux-and-macos"></a>Linux および macOS に Microsoft ODBC Driver for SQL Server をインストールする
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

この記事では、Linux と macOS 上の [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のほか、オプションの SQL Server 用コマンドライン ツール (`bcp` と `sqlcmd`) および unixODBC 開発ヘッダーをインストールする方法について説明します。

## <a name="microsoft-odbc-driver-17-for-sql-server"></a>Microsoft ODBC Driver 17 for SQL Server 

> [!IMPORTANT]
> 短期間利用可能だった v17 `msodbcsql` パッケージをインストールしている場合は、`msodbcsql17` パッケージのインストール前に削除する必要があります。 これにより、競合が回避されます。 `msodbcsql17` パッケージは `msodbcsql` v13 パッケージと並行してインストールできます。

### <a name="debian"></a>Debian
```
sudo su 
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -

#Download appropriate package for the OS version
#Choose only ONE of the following, corresponding to your OS version

#Debian 8
curl https://packages.microsoft.com/config/debian/8/prod.list > /etc/apt/sources.list.d/mssql-release.list

#Debian 9
curl https://packages.microsoft.com/config/debian/9/prod.list > /etc/apt/sources.list.d/mssql-release.list

#Debian 10
curl https://packages.microsoft.com/config/debian/10/prod.list > /etc/apt/sources.list.d/mssql-release.list

exit
sudo apt-get update
sudo ACCEPT_EULA=Y apt-get install msodbcsql17
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y apt-get install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo apt-get install unixodbc-dev
```

### <a name="redhat-enterprise-server"></a>RedHat Enterprise Server
```
sudo su

#Download appropriate package for the OS version
#Choose only ONE of the following, corresponding to your OS version

#RedHat Enterprise Server 6
curl https://packages.microsoft.com/config/rhel/6/prod.repo > /etc/yum.repos.d/mssql-release.repo

#RedHat Enterprise Server 7
curl https://packages.microsoft.com/config/rhel/7/prod.repo > /etc/yum.repos.d/mssql-release.repo

#RedHat Enterprise Server 8
curl https://packages.microsoft.com/config/rhel/8/prod.repo > /etc/yum.repos.d/mssql-release.repo

exit
sudo yum remove unixODBC-utf16 unixODBC-utf16-devel #to avoid conflicts
sudo ACCEPT_EULA=Y yum install msodbcsql17
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y yum install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo yum install unixODBC-devel
```

### <a name="suse-linux-enterprise-server"></a>SUSE Linux Enterprise Server

```
sudo su

#Download appropriate package for the OS version
#Choose only ONE of the following, corresponding to your OS version

#SUSE Linux Enterprise Server 11 SP4
#Ensure SUSE Linux Enterprise 11 Security Module has been installed 
zypper ar https://packages.microsoft.com/config/sles/11/prod.repo

#SUSE Linux Enterprise Server 12
zypper ar https://packages.microsoft.com/config/sles/12/prod.repo

#SUSE Linux Enterprise Server 15
zypper ar https://packages.microsoft.com/config/sles/15/prod.repo
#(Only for driver 17.3 and below)
SUSEConnect -p sle-module-legacy/15/x86_64

exit
sudo ACCEPT_EULA=Y zypper install msodbcsql17
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y zypper install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo zypper install unixODBC-devel
``` 

### <a name="ubuntu"></a>Ubuntu
```
sudo su 
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -

#Download appropriate package for the OS version
#Choose only ONE of the following, corresponding to your OS version

#Ubuntu 14.04
curl https://packages.microsoft.com/config/ubuntu/14.04/prod.list > /etc/apt/sources.list.d/mssql-release.list

#Ubuntu 16.04
curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list > /etc/apt/sources.list.d/mssql-release.list

#Ubuntu 18.04
curl https://packages.microsoft.com/config/ubuntu/18.04/prod.list > /etc/apt/sources.list.d/mssql-release.list

#Ubuntu 18.10
curl https://packages.microsoft.com/config/ubuntu/18.10/prod.list > /etc/apt/sources.list.d/mssql-release.list

#Ubuntu 19.04
curl https://packages.microsoft.com/config/ubuntu/19.04/prod.list > /etc/apt/sources.list.d/mssql-release.list

exit
sudo apt-get update
sudo ACCEPT_EULA=Y apt-get install msodbcsql17
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y apt-get install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo apt-get install unixodbc-dev
```
> [!NOTE]
> - Ubuntu 18.04 のサポートには、ドライバー バージョン 17.2 以降が必要です。
> - Ubuntu 18.10 のサポートには、ドライバー バージョン 17.3 以降が必要です。   

### <a name="macos"></a>MacOS

```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew tap microsoft/mssql-release https://github.com/Microsoft/homebrew-mssql-release
brew update
brew install msodbcsql17 mssql-tools
```

## <a name="microsoft-odbc-driver-131-for-sql-server"></a>Microsoft ODBC Driver 13.1 for SQL Server 

### <a name="debian-8"></a>Debian 8
```
sudo su 
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
curl https://packages.microsoft.com/config/debian/8/prod.list > /etc/apt/sources.list.d/mssql-release.list
exit
sudo apt-get update
sudo ACCEPT_EULA=Y apt-get install msodbcsql
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y apt-get install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo apt-get install unixodbc-dev
```

### <a name="redhat-enterprise-server-6"></a>RedHat Enterprise Server 6
```
sudo su
curl https://packages.microsoft.com/config/rhel/6/prod.repo > /etc/yum.repos.d/mssql-release.repo
exit
sudo yum remove unixODBC-utf16 unixODBC-utf16-devel #to avoid conflicts
sudo ACCEPT_EULA=Y yum install msodbcsql
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y yum install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo yum install unixODBC-devel
```

### <a name="redhat-enterprise-server-7"></a>RedHat Enterprise Server 7
```
sudo su
curl https://packages.microsoft.com/config/rhel/7/prod.repo > /etc/yum.repos.d/mssql-release.repo
exit
sudo yum remove unixODBC-utf16 unixODBC-utf16-devel #to avoid conflicts
sudo ACCEPT_EULA=Y yum install msodbcsql
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y yum install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo yum install unixODBC-devel
```

### <a name="suse-linux-enterprise-server-11"></a>SUSE Linux Enterprise Server 11

```
sudo su
zypper ar https://packages.microsoft.com/config/sles/11/prod.repo
exit
sudo ACCEPT_EULA=Y zypper install msodbcsql
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y zypper install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo zypper install unixODBC-devel
``` 

### <a name="suse-linux-enterprise-server-12"></a>SUSE Linux Enterprise Server 12

```
sudo su
zypper ar https://packages.microsoft.com/config/sles/12/prod.repo
exit
sudo ACCEPT_EULA=Y zypper install msodbcsql
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y zypper install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo zypper install unixODBC-devel
``` 

### <a name="ubuntu-1510"></a>Ubuntu 15.10
```
sudo su 
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
curl https://packages.microsoft.com/config/ubuntu/15.10/prod.list > /etc/apt/sources.list.d/mssql-release.list
exit
sudo apt-get update
sudo ACCEPT_EULA=Y apt-get install msodbcsql
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y apt-get install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo apt-get install unixodbc-dev
```

### <a name="ubuntu-1604"></a>Ubuntu 16.04
```
sudo su 
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list > /etc/apt/sources.list.d/mssql-release.list
exit
sudo apt-get update
sudo ACCEPT_EULA=Y apt-get install msodbcsql
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y apt-get install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo apt-get install unixodbc-dev
```

### <a name="ubuntu-1610"></a>Ubuntu 16.10
```
sudo su 
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
curl https://packages.microsoft.com/config/ubuntu/16.10/prod.list > /etc/apt/sources.list.d/mssql-release.list
exit
sudo apt-get update
sudo ACCEPT_EULA=Y apt-get install msodbcsql
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y apt-get install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo apt-get install unixodbc-dev
```

### <a name="os-x-1011-el-capitan-and-macos-1012-sierra"></a>OS X 10.11 (El Capitan) と macOS 10.12 (Sierra)

```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew tap microsoft/mssql-release https://github.com/Microsoft/homebrew-mssql-release
brew update
brew install msodbcsql@13.1.9.2 mssql-tools@14.0.6.0
```

## <a name="microsoft-odbc-driver-13-for-sql-server"></a>Microsoft ODBC Driver 13 for SQL Server

### <a name="redhat-enterprise-server-6"></a>RedHat Enterprise Server 6
```
sudo su
curl https://packages.microsoft.com/config/rhel/6/prod.repo > /etc/yum.repos.d/mssql-release.repo
exit
sudo yum update
sudo yum remove unixODBC #to avoid conflicts
sudo ACCEPT_EULA=Y yum install msodbcsql-13.0.1.0-1 mssql-tools-14.0.2.0-1
sudo yum install unixODBC-utf16-devel #this step is optional but recommended*
#Create symlinks for tools
ln -sfn /opt/mssql-tools/bin/sqlcmd-13.0.1.0 /usr/bin/sqlcmd 
ln -sfn /opt/mssql-tools/bin/bcp-13.0.1.0 /usr/bin/bcp
```

### <a name="redhat-enterprise-server-7"></a>RedHat Enterprise Server 7
```
sudo su
curl https://packages.microsoft.com/config/rhel/7/prod.repo > /etc/yum.repos.d/mssql-release.repo
exit
sudo yum update
sudo yum remove unixODBC #to avoid conflicts
sudo ACCEPT_EULA=Y yum install msodbcsql-13.0.1.0-1 mssql-tools-14.0.2.0-1
sudo yum install unixODBC-utf16-devel #this step is optional but recommended*
#Create symlinks for tools
ln -sfn /opt/mssql-tools/bin/sqlcmd-13.0.1.0 /usr/bin/sqlcmd 
ln -sfn /opt/mssql-tools/bin/bcp-13.0.1.0 /usr/bin/bcp
```

### <a name="ubuntu-1510"></a>Ubuntu 15.10
```
sudo su 
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
curl https://packages.microsoft.com/config/ubuntu/15.10/prod.list > /etc/apt/sources.list.d/mssql-release.list
exit
sudo apt-get update
sudo ACCEPT_EULA=Y apt-get install msodbcsql=13.0.1.0-1 mssql-tools=14.0.2.0-1
sudo apt-get install unixodbc-dev-utf16 #this step is optional but recommended*
#Create symlinks for tools
ln -sfn /opt/mssql-tools/bin/sqlcmd-13.0.1.0 /usr/bin/sqlcmd 
ln -sfn /opt/mssql-tools/bin/bcp-13.0.1.0 /usr/bin/bcp
```

### <a name="ubuntu-1604"></a>Ubuntu 16.04
```
sudo su 
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list > /etc/apt/sources.list.d/mssql-release.list
exit
sudo apt-get update
sudo ACCEPT_EULA=Y apt-get install msodbcsql=13.0.1.0-1 mssql-tools=14.0.2.0-1
sudo apt-get install unixodbc-dev-utf16 #this step is optional but recommended*
#Create symlinks for tools
ln -sfn /opt/mssql-tools/bin/sqlcmd-13.0.1.0 /usr/bin/sqlcmd 
ln -sfn /opt/mssql-tools/bin/bcp-13.0.1.0 /usr/bin/bcp
```

### <a name="suse-linux-enterprise-server-12"></a>SUSE Linux Enterprise Server 12

```
sudo su 
zypper ar https://packages.microsoft.com/config/sles/12/prod.repo 
zypper update 
sudo ACCEPT_EULA=Y zypper install msodbcsql-13.0.1.0-1 mssql-tools-14.0.2.0-1
zypper install unixODBC-utf16-devel
#Create symlinks for tools
ln -sfn /opt/mssql-tools/bin/sqlcmd-13.0.1.0 /usr/bin/sqlcmd 
ln -sfn /opt/mssql-tools/bin/bcp-13.0.1.0 /usr/bin/bcp
```

### <a name="offline-installation"></a>オフライン インストール
インターネット接続なしでコンピューターに [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 13 をインストールする場合は、パッケージの依存関係を手動で解決する必要があります。 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 13 には、次の直接的な依存関係があります。
- Ubuntu: libc6 (>= 2.21)、libstdc++6 (>= 4.9)、libkrb5-3、libcurl3、openssl、debconf (>= 0.5)、unixodbc (>= 2.3.1-1)
- Red Hat: ```glibc, e2fsprogs, krb5-libs, openssl, unixODBC```
- SuSE: ```glibc, libuuid1, krb5, openssl, unixODBC```

これらの各パッケージにはそれぞれ独自の依存関係があり、システムに存在する場合と存在しない場合があります。 この問題の一般的な解決策については、ディストリビューションのパッケージ マネージャーの [Redhat](https://wiki.centos.org/HowTos/CreateLocalRepos)、[Ubuntu](https://unix.stackexchange.com/questions/87130/how-to-quickly-create-a-local-apt-repository-for-random-packages-using-a-debian)、および [SUSE](https://en.opensuse.org/Portal:Zypper) に関するドキュメントを参照してください。

また、すべての従属パッケージを手動でダウンロードし、インストール コンピューターにまとめて配置してから、各パッケージを順に手動でインストールし、[!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 13 パッケージを終了する方法も一般的です。

#### <a name="redhat-linux-enterprise-server-7"></a>Redhat Linux Enterprise Server 7
  - https://packages.microsoft.com/rhel/7/prod/ から最新の `msodbcsql` `.rpm` をダウンロードする
  - 依存関係とドライバーをインストールする
  
```
yum install glibc e2fsprogs krb5-libs openssl unixODBC unixODBC-devel #install dependencies
sudo rpm -i  msodbcsql-13.1.X.X-X.x86_64.rpm #install the Driver
```

#### <a name="ubuntu-1604"></a>Ubuntu 16.04
- https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/msodbcsql/ から最新の `msodbcsql` `.deb` をダウンロードする 
- 依存関係とドライバーをインストールする 

```
sudo apt-get install libc6 libstdc++6 libkrb5-3 libcurl3 openssl debconf unixodbc unixodbc-dev #install dependencies
sudo dpkg -i msodbcsql_13.1.X.X-X_amd64.deb #install the Driver
```

#### <a name="suse-linux-enterprise-server-12"></a>SUSE Linux Enterprise Server 12
- https://packages.microsoft.com/sles/12/prod/ から最新の `msodbcsql` `.rpm` をダウンロードする
- 依存関係とドライバーをインストールする

```
zypper install glibc, libuuid1, krb5, openssl, unixODBC unixODBC-devel #install dependencies
sudo rpm -i  msodbcsql-13.1.X.X-X.x86_64.rpm #install the Driver
```

パッケージのインストールを完了したら、ldd を実行し、不足しているライブラリがないか出力を調べることで、[!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 13 がすべての依存関係を検出できることを確認できます。
```
ldd /opt/microsoft/msodbcsql/lib64/libmsodbcsql-*
```
  
## <a name="microsoft-odbc-driver-11-for-sql-server-on-linux"></a>Linux 上の Microsoft ODBC Driver 11 for SQL Server

ドライバーを使用する前に、unixODBC ドライバー マネージャーをインストールしておく必要があります。 詳細については、「[ドライバー マネージャーのインストール](../../../connect/odbc/linux-mac/installing-the-driver-manager.md)」を参照してください。

**インストール手順**  

> [!IMPORTANT]  
> 次の手順では、Red Hat Linux 用のインストール ファイル `msodbcsql-11.0.2270.0.tar.gz` を参照しています。 Preview for SUSE Linux をインストールする場合のファイル名は `msodbcsql-11.0.2260.0.tar.gz` です。  
  
ドライバーをインストールするには:

1.  ルートのアクセス許可があることを確認します。  

2.  ダウンロードでファイル `msodbcsql-11.0.2270.0.tar.gz` を配置したディレクトリに切り替えます。 使用している Linux のバージョンに対応する \*.tar.gz ファイルがあることを確認します。 ファイルを解凍するには、コマンド `tar xvzf msodbcsql-11.0.2270.0.tar.gz` を実行します。  
  
3.  `msodbcsql-11.0.2270.0` のディレクトリに移動すると、ディレクトリ内に **install.sh** というファイルがあることを確認できます。  
  
4.  使用可能なインストール オプションの一覧を表示するには、コマンド **./install.sh**を実行します。  
  
5.  **odbcinst.ini**のバックアップを作成します。 ドライバーのインストールで、 **odbcinst.ini**を更新します。 odbcinst.ini には、unixODBC ドライバー マネージャーで登録されたドライバーの一覧が含まれます。 コンピューターの odbcinst.ini の場所を検出するには、コマンド ```odbc_config --odbcinstini``` を実行します。  
  
6.  ドライバーをインストールする前に、コマンド `./install.sh verify` を実行します。 Linux で ODBC ドライバーをサポートするためにコンピューターに必要なソフトウェアがある場合、`./install.sh verify` の出力でレポートされます。  
  
7.  Linux に ODBC ドライバーをインストールする準備が整ったら、コマンド `./install.sh install` を実行します。 インストール コマンド (`bin-dir` または `lib-dir`) を指定する必要がある場合は、**install** オプションの後にコマンドを指定してください。  
  
8.  使用許諾契約を確認し、 **YES** と入力してインストールを続行します。  
  
インストールで、ドライバーが `/opt/microsoft/msodbcsql/11.0.2270.0` に配置されます。 `/opt/microsoft/msodbcsql/11.0.2270.0` には、ドライバーとそのサポート ファイルが保存されている必要があります。  
  
Linux の Microsoft ODBC ドライバーが正常に登録されたことを確認するには、コマンド ```odbcinst -q -d -n "ODBC Driver 11 for SQL Server"``` を実行します。  
  
「[Use Existing MSDN C++ ODBC Samples for the ODBC Driver on Linux (Linux の ODBC ドライバーに既存の MSDN C++ ODBC サンプルを使用する)](https://blogs.msdn.com/b/sqlblog/archive/2012/01/26/use-existing-msdn-c-odbc-samples-for-microsoft-linux-odbc-driver.aspx) 」には、Linux の ODBC ドライバーを使用して [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] に接続するコード サンプルが紹介されています。  
  
**アンインストール**  
  
Linux の ODBC ドライバー 11 をアンインストールするには、次のコマンドを実行します。  
  
1.  `rm -f /usr/bin/sqlcmd`
  
2.  `rm -f /usr/bin/bcp`  
  
3.  `rm -rf /opt/microsoft/msodbcsql`  
  
4.  `odbcinst -u -d -n "ODBC Driver 11 for SQL Server"`
  
## <a name="troubleshooting-connection-problems"></a>接続の問題のトラブルシューティング  
ODBC ドライバーを使用して [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] に接続できない場合、次の情報を使用して問題を特定します。  
  
最も一般的な接続の問題は、2 つの UnixODBC ドライバー マネージャーがインストールされている場合です。 /usr で libodbc\*.so\*を検索します。 複数バージョンのファイルがある場合、複数のドライバー マネージャーがインストールされている可能性があります。 また、アプリケーションに不適切なバージョンが使用される可能性があります。
  
これらの項目と共に次のセクションを含めるよう `/etc/odbcinst.ini` ファイルを編集することで、接続ログを有効にします。

```
[ODBC]
Trace = Yes
TraceFile = (path to log file, or /dev/stdout to output directly to the terminal)
```  
  
別の接続エラーが発生し、ログ ファイルが見つからない場合、コンピューターに 2 つのドライバー マネージャーが存在する可能性があります。 それ以外の場合、ログの出力は次のようになります。  
  
```  
[ODBC][28783][1321576347.077780][SQLDriverConnectW.c][290]  
        Entry:  
            Connection = 0x17c858e0  
            Window Hdl = (nil)  
            Str In = [DRIVER={ODBC Driver 13 for SQL Server};SERVER={contoso.com};Trusted_Connection={YES};WSID={mydb.contoso.com};AP...][length = 139 (SQL_NTS)]  
            Str Out = (nil)  
            Str Out Max = 0  
            Str Out Ptr = (nil)  
            Completion = 0  
        UNICODE Using encoding ASCII 'UTF8' and UNICODE 'UTF16LE'  
```  
  
ASCII 文字エンコードが UTF-8 ではない場合の例: 
  
```  
UNICODE Using encoding ASCII 'ISO8859-1' and UNICODE 'UCS-2LE'  
```  
  
複数のドライバー マネージャーがインストールされており、アプリケーションが不適切なドライバー マネージャーを使用しているか、またはライバー マネージャーが正しくビルドされていません。  
  
接続エラーの解決の詳細については、以下を参照してください。  
  
-   [SQL の接続問題のトラブルシューティングの手順](https://blogs.msdn.com/b/sql_protocols/archive/2008/04/30/steps-to-troubleshoot-connectivity-issues.aspx)  
  
-   [SQL Server 2005 Connectivity Issue Troubleshoot - Part I (SQL Server 2005 の接続に関する問題のトラブルシューティング - パート 1)](https://blogs.msdn.com/b/sql_protocols/archive/2005/10/22/sql-server-2005-connectivity-issue-troubleshoot-part-i.aspx)  
  
-   [Connectivity troubleshooting in SQL Server 2008 with the Connectivity Ring Buffer (接続リング バッファーを使用している SQL Server 2008 の接続のトラブルシューティング)](https://blogs.msdn.com/b/sql_protocols/archive/2008/05/20/connectivity-troubleshooting-in-sql-server-2008-with-the-connectivity-ring-buffer.aspx)  
  
-   [SQL Server Authentication Troubleshooter (SQL Server 認証のトラブルシューティング)](https://blogs.msdn.com/b/sqlsecurity/archive/2010/03/29/sql-server-authentication-troubleshooter.aspx)  
  
-   [エラーの詳細 (https://www.microsoft.com/products/ee/transform.aspx?ProdName=Microsoft+SQL+Server&EvtSrc=MSSQLServer&EvtID=11001)](https://www.microsoft.com/products/ee/transform.aspx?ProdName=Microsoft+SQL+Server&EvtSrc=MSSQLServer&EvtID=001)  
  
    URL (11001) に指定するエラー番号は、表示されたエラーに合わせて変更する必要があります。  
  
## <a name="driver-files"></a>ドライバー ファイル
Linux と MacOS 上の ODBC ドライバーは、次のコンポーネントで構成されています。

### <a name="linux"></a>Linux

|コンポーネント|[説明]|  
|---------------|-----------------|  
|libmsodbcsql-17.X.so.X.X または libmsodbcsql-13.X.so.X.X|ドライバーのすべての機能を含む共有オブジェクト (`so`) ダイナミック ライブラリ ファイル。 このファイルは、Driver 17 では `/opt/microsoft/msodbcsql17/lib64/`、Driver 13 では `/opt/microsoft/msodbcsql/lib64/` にインストールされます。|  
|`msodbcsqlr17.rll` または `msodbcsqlr13.rll`|ドライバー ライブラリに付随するリソース ファイル。 このファイルは `[driver .so directory]../share/resources/en_US/` にインストールされます| 
|msodbcsql.h|ドライバーを使用するために必要な新しい定義がすべて含まれているヘッダー ファイル。<br /><br /> **注:**  msodbcsql.h と odbcss.h を同じプログラムで参照することはできません。<br /><br /> msodbcsql.h は、Driver 17 では `/opt/microsoft/msodbcsql17/include/`、Driver 13 では `/opt/microsoft/msodbcsql/include/` にインストールされます。 |
|LICENSE.txt|使用許諾契約書の条項を含むテキスト ファイル。 このファイルは、Driver 17 では `/usr/share/doc/msodbcsql17/`、Driver 13 では `/usr/share/doc/msodbcsql/` に配置されます。|
|RELEASE_NOTES|リリース ノートを含むテキスト ファイル。 このファイルは、Driver 17 では `/usr/share/doc/msodbcsql17/`、Driver 13 では `/usr/share/doc/msodbcsql/` に配置されます。|


### <a name="macos"></a>MacOS

|コンポーネント|[説明]|  
|---------------|-----------------|  
|libmsodbcsql.17.dylib または libmsodbcsql.13.dylib|ドライバーのすべての機能を含むダイナミック ライブラリ (`dylib`) ファイル。 このファイルは `/usr/local/lib/` にインストールされます。|  
|`msodbcsqlr17.rll` または `msodbcsqlr13.rll`|ドライバー ライブラリに付随するリソース ファイル。 このファイルは、Driver 17 では `[driver .dylib directory]../share/msodbcsql17/resources/en_US/`、Driver 13 では `[driver .dylib directory]../share/msodbcsql/resources/en_US/` にインストールされます。 | 
|msodbcsql.h|ドライバーを使用するために必要な新しい定義がすべて含まれているヘッダー ファイル。<br /><br /> **注:**  msodbcsql.h と odbcss.h を同じプログラムで参照することはできません。<br /><br /> msodbcsql.h は、Driver 17 では `/usr/local/include/msodbcsql17/`、Driver 13 では `/usr/local/include/msodbcsql/` にインストールされます。 |
|LICENSE.txt|使用許諾契約書の条項を含むテキスト ファイル。 このファイルは、Driver 17 では `/usr/local/share/doc/msodbcsql17/`、Driver 13 では `/usr/local/share/doc/msodbcsql/` に配置されます。 |
|RELEASE_NOTES|リリース ノートを含むテキスト ファイル。 このファイルは、Driver 17 では `/usr/local/share/doc/msodbcsql17/`、Driver 13 では `/usr/local/share/doc/msodbcsql/` に配置されます。 |

## <a name="resource-file-loading"></a>リソース ファイルの読み込み

ドライバーが機能するには、リソース ファイルを読み込む必要があります。 このファイルは、ドライバーのバージョンに応じて `msodbcsqlr17.rll` または `msodbcsqlr13.rll` という名前になります。 `.rll` ファイルの場所は、上の表に示されているとおり、ドライバー自体の場所 (`so` または `dylib`) に対して相対的です。 バージョン 17.1 の時点で、相対パスからの読み込みが失敗した場合、ドライバーは既定のディレクトリからも `.rll` の読み込みを試みます。 既定のリソース ファイルのパスは次のとおりです。

Linux: `/opt/microsoft/msodbcsql17/share/resources/en_US/`

MacOS: `/usr/local/share/msodbcsql17/resources/en_US/`


  
## <a name="see-also"></a>参照

[ドライバー マネージャーのインストール](../../../connect/odbc/linux-mac/installing-the-driver-manager.md)

[リリース ノート](../../../connect/odbc/linux-mac/release-notes-odbc-sql-server-linux-mac.md)

[システム要件](../../../connect/odbc/linux-mac/system-requirements.md)
