---
title: SQL Server の言語拡張を Linux にインストールする
titleSuffix: ''
description: Red Hat、Ubuntu、SUSE 上に SQL Server の言語拡張をインストールする方法について説明します。
author: dphansen
ms.author: davidph
ms.reviewer: vanto
manager: cgronlun
ms.date: 11/05/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: language-extensions
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 2b5a8c83f827f574698d2e9b37a19cdb29e1ba80
ms.sourcegitcommit: baa40306cada09e480b4c5ddb44ee8524307a2ab
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/06/2019
ms.locfileid: "73660778"
---
# <a name="install-sql-server-language-extensions-on-linux"></a>SQL Server の言語拡張を Linux にインストールする

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

言語拡張は、データベース エンジンに対するアドオンです。 [データベース エンジンと言語拡張を同時にインストールする](#install-all)ことは可能ですが、コンポーネントを追加する前に問題を解決できるように、まずは SQL Server データベースエンジンをインストールして構成することをお勧めします。 

この記事の手順に従って、Java の言語拡張をインストールします。

Java 拡張機能のパッケージは、SQL Server Linux ソース リポジトリに配置されています。 データベース エンジンのインストールのためにソース リポジトリを既に構成している場合は、同じリポジトリ登録を使用して **mssql-server-extensibility-java** パッケージ インストール コマンドを実行できます。

また、言語拡張は Linux コンテナー上でもサポートされます。 言語拡張には、ビルド済みのコンテナーは付属していませんが、[GitHub 上で入手できるサンプル テンプレート](https://github.com/Microsoft/mssql-docker/tree/master/linux/preview/examples/mssql-mlservices)を使用して、SQL Server コンテナーから作成できます。

言語拡張と [Machine Learning Services](../advanced-analytics/index.yml) は、既定では、SQL Server ビッグ データ クラスターにインストールされます。 ビッグ データ クラスターを使用する場合、この記事の手順を行う必要はありません。 詳細については、[ビッグ データ クラスターでの Machine Learning Services (Python および R) の使用](../big-data-cluster/machine-learning-services.md)に関するページを参照してください。

## <a name="uninstall-preview-version"></a>プレビュー バージョンをアンインストールする

プレビュー リリース (Community Technical Preview (CTP) またはリリース候補 (RC)) をインストールしている場合は、SQL Server 2019 をインストールする前に、このバージョンをアンインストールして以前のすべてのパッケージを削除することをお勧めします。 複数のバージョンのサイド バイ サイド インストールはサポートされていません。また、パッケージ一覧は、最新のいくつかのプレビュー (CTP/RC) リリースで変更されています。

### <a name="1-confirm-package-installation"></a>1.パッケージのインストールを確認する

最初の手順として、状況に応じて以前のインストールの存在をチェックします。 次のファイルは既存のインストールを示します。checkinstallextensibility.sh、exthost、launchpad です。

```bash
ls /opt/microsoft/mssql/bin
```

### <a name="2-uninstall-previous-ctprc-packages"></a>2.以前の CTP/RC パッケージをアンインストールする

最下位のパッケージ レベルでアンインストールを行います。 より下位のパッケージに依存しているアップストリーム パッケージがすべて、自動的にアンインストールされます。

  + Java 統合の場合、**mssql-server-extensibility-java** を削除します。

次の表に、パッケージを削除するためのコマンドを示します。

| プラットフォーム  | パッケージの削除コマンド | 
|-----------|----------------------------|
| RHEL  | `sudo yum remove msssql-server-extensibility-java` |
| SLES  | `sudo zypper remove msssql-server-extensibility-java` |
| Ubuntu    | `sudo apt-get remove msssql-server-extensibility-java`|

### <a name="3-install-sql-server-2019"></a>3.SQL Server 2019 をインストールする

この記事の手順を使用して、お使いのオペレーティング システムに最上位のパッケージ レベルでインストールを行います。

OS 固有の一連のインストール手順ごとに、"*最上位のパッケージ レベル*" は、完全なパッケージ セットに対応した**例 1 - 完全なインストール**か、実行可能なインストールに必要なパッケージの最小数に対応した**例 2 - 最小限のインストール**のどちらかになります。

1. Linux ディストリビューション用のパッケージ マネージャーと構文を使用して、インストール コマンドを実行します。 

   + [RedHat](#RHEL)
   + [Ubuntu](#ubuntu)
   + [SUSE](#suse)

## <a name="prerequisites"></a>Prerequisites

+ Linux バージョンは、必ず [SQL Server によってサポートされます](sql-server-linux-release-notes-2019.md#supported-platforms)が、Docker エンジンは含まれていません。 サポートされているバージョンは次のとおりです。

   + [Red Hat Enterprise Linux (RHEL)](quickstart-install-connect-red-hat.md)

   + [SUSE Enterprise Linux Server](quickstart-install-connect-suse.md)

   + [Ubuntu](quickstart-install-connect-ubuntu.md)

+ T-SQL コマンドを実行するためのツールを用意しておく必要があります。 インストール後の構成および検証には、クエリ エディターが必要です。 Linux 上で実行される無料ダウンロードの [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/download?view=sql-server-2017#get-azure-data-studio-for-linux) をお勧めします。

## <a name="package-list"></a>パッケージ一覧

インターネットに接続されたデバイス上で、各オペレーティング システム用のパッケージ インストーラーを使用して、パッケージがデータベース エンジンとは別個にダウンロードされてインストールされます。 次の表に、使用可能な全パッケージについて説明します。

| パッケージ名 | 適用先 | [説明] |
|--------------|----------|-------------|
|mssql-server-extensibility  | すべての言語 | Java 言語拡張機能に使用される拡張性フレームワーク |
|mssql-server-extensibility-java | Java | Java 言語拡張機能に使用され、サポートされている Java ランタイムが含まれる拡張性フレームワーク |

<a name="RHEL"></a>

## <a name="install-language-extensions"></a>言語拡張をインストールする

**mssql-server-extensibility-java** をインストールすることによって、Linux 上に言語拡張と Java をインストールできます。 **mssql-server-extensibility-java** をインストールすると、JRE 11 がまだインストールされていない場合は、パッケージによって自動的にインストールされます。 また、JVM パスが JRE_HOME という環境変数に追加されます。

> [!Note]
> インターネットに接続されたサーバー上では、パッケージの依存関係がダウンロードされ、メイン パッケージのインストールの一部としてインストールされます。 サーバーがインターネットに接続されていない場合は、[オフライン セットアップ](#offline-install)に関するページで詳細を確認してください。

### <a name="redhat-install-command"></a>RedHat インストール コマンド

以下のコマンドを使用して、RedHat 上に Java 用の言語拡張をインストールできます。

> [!Tip]
> 可能であれば、`yum clean all` を実行して、インストールの前にシステム上のパッケージを更新しておきます。

```bash
# Install as root or sudo
sudo yum install mssql-server-extensibility-java
```

<a name="ubuntu"></a>

### <a name="ubuntu-install-command"></a>Ubuntu インストール コマンド

以下のコマンドを使用して、Ubuntu 上に Java 用の言語拡張をインストールできます。

> [!Tip]
> 可能であれば、`apt-get update` を実行して、インストールの前にシステム上のパッケージを更新しておきます。 また、Ubuntu の一部の Docker イメージには、https apt transport オプションが含まれていない場合があります。 インストールするには、`apt-get install apt-transport-https` を使用します。

```bash
# Install as root or sudo
sudo apt-get install mssql-server-extensibility-java
```

<a name="suse"></a>

### <a name="suse-install-command"></a>SUSE インストール コマンド

以下のコマンドを使用して、SUSE 上に Java 用の言語拡張をインストールできます。

```bash
# Install as root or sudo
sudo zypper install mssql-server-extensibility-java
```

## <a name="post-install-config-required"></a>インストール後の構成 (必須)

1. Linux 上でのアクセス許可を付与します

    外部ライブラリを使用している場合は、この手順を実行する必要はありません。 外部ライブラリを使用して作業することをお勧めします。 jar ファイルから外部ライブラリを作成する方法については、「[CREATE EXTERNAL LIBRARY](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql)」をご覧ください。

    外部ライブラリを使用しない場合は、jar 内の Java クラスを実行するための権限を SQL Server に付与する必要があります。

    jar ファイルに対する読み取りと実行のアクセス権を付与するには、jar ファイルに次の **chmod** コマンドを実行します。 SQL Server を操作するときは、常にクラス ファイルを jar 内に配置することをお勧めします。 jar の作成方法については、[jar ファイルを作成する方法](https://docs.microsoft.com/sql/language-extensions/how-to/create-a-java-jar-file-from-class-files)に関するページをご覧ください。

    ```cmd
    chmod ug+rx <MyJarFile.jar>
    ```

    また、jar ファイルへの読み取り/実行の mssql_satellite 権限を付与する必要があります。

    ```cmd
    chown mssql_satellite:mssql_satellite <MyJarFile.jar>
    ```

    追加の構成には、主に[ mssql-conf ツール](sql-server-linux-configure-mssql-conf.md)を利用します。

2. SQL Server サービスの実行に使用する mssql ユーザー アカウントを追加します。 事前にセットアップを実行していない場合、これは必須です。

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

3. 送信ネットワーク アクセスを有効にします。 既定では、送信ネットワーク アクセスは無効になっています。 送信要求を有効にするには、mssql-conf ツールを使用して "outboundnetworkaccess" ブール型プロパティを設定します。 詳しくは、「[mssql-conf ツールを利用して Linux 上で SQL Server を構成する](sql-server-linux-configure-mssql-conf.md#mlservices-outbound-access)」をご覧ください。

   ```bash
   # Run as SUDO or root
   # Enable outbound requests over the network
   sudo /opt/mssql/bin/mssql-conf set extensibility outboundnetworkaccess 1
   ```

4. SQL Server Launchpad サービスとデータベース エンジン インスタンスを再起動して、INI ファイルから更新後の値を読み込みます。 拡張機能に関連する設定が変更されるたびに、再起動を促すメッセージが表示されます。  

   ```bash
   systemctl restart mssql-launchpadd

   systemctl restart mssql-server.service
   ```

5. Azure Data Studio または Transact-SQL を実行する SQL Server Management Studio (Windows のみ) などの別のツールを使用して、外部スクリプトの実行を有効にします。

   ```bash
   EXEC sp_configure 'external scripts enabled', 1
   RECONFIGURE WITH OVERRIDE
   ```

6. もう一度、`mssql-launchpadd` サービスを再起動します。

7. 言語拡張を利用する各データベースには、[CREATE EXTERNAL LANGUAGE](https://docs.microsoft.com/sql/t-sql/statements/create-external-language-transact-sql) を使って外部言語を登録する必要があります。

## <a name="register-external-language"></a>外部言語を登録する

言語拡張を利用する各データベースには、[CREATE EXTERNAL LANGUAGE](https://docs.microsoft.com/sql/t-sql/statements/create-external-language-transact-sql) を使って外部言語を登録する必要があります。

次の例では、Linux にある SQL Server 上のデータベースに、Java という名前の外部言語を追加しています。

```SQL
CREATE EXTERNAL LANGUAGE Java
FROM (CONTENT = N'<path-to-tar.gz>', FILE_NAME = 'javaextension.so');
GO
```

詳しくは、「[CREATE EXTERNAL LANGUAGE](https://docs.microsoft.com/sql/t-sql/statements/create-external-language-transact-sql)」をご覧ください。

## <a name="verify-installation"></a>インストールの確認

Java 機能の統合には、ライブラリは含まれませんが、`grep -r JRE_HOME /etc` を実行して JAVA_HOME 環境変数の作成を確認することができます。

インストールを確認するには、Java を起動するシステム ストアド プロシージャが実行される T-SQL スクリプトを実行します。 このタスクには、クエリ ツールが必要になります。 Azure Data Studio が適しています。 SQL Server Management Studio や PowerShell など、一般的に使用されるその他のツールは Windows 限定です。 これらのツールを利用する Windows コンピューターがある場合は、それを使用してデータベース エンジンの Linux インストールに接続します。

<a name="install-all"></a>

## <a name="full-install-of-sql-server-and-language-extensions"></a>SQL Server および言語拡張の完全なインストール

データベース エンジンをインストールするコマンドに Java パッケージとパラメーターを付加すると、1 つの手順でデータベース エンジンと言語拡張をインストールして構成できます。

1. データベース エンジンに加えて、言語拡張機能を含めたコマンド ラインを指定します。

  Java 拡張機能は、データベース エンジンのインストールに追加できます。

  ```bash
  sudo yum install -y mssql-server mssql-server-extensibility-java 
  ```

3. 使用許諾契約書に同意し、インストール後の構成を完了します。 このタスクには、**mssql-conf** ツールを使用します。

  ```bash
  sudo /opt/mssql/bin/mssql-conf setup
  ```

  データベース エンジンの使用許諾契約書に同意し、エディションを選択して、管理者パスワードを設定するように求められます。 

4. 求められた場合は、サービスを再起動します。

  ```bash
  sudo systemctl restart mssql-server.service
  ```

## <a name="unattended-installation"></a>無人インストール

データベース エンジンの[無人インストール](https://docs.microsoft.com/sql/linux/sql-server-linux-setup#unattended)を使用して、mssql-server-extensibility-java 用のパッケージを追加します。

<a name="offline-install"></a>


## <a name="offline-installation"></a>オフライン インストール

パッケージをインストールする手順については、[オフライン インストール](sql-server-linux-setup.md#offline)の手順に従います。 ダウンロード サイトを検索し、以下のパッケージ一覧を使用して特定のパッケージをダウンロードします。

> [!Tip]
> いくつかのパッケージ管理ツールには、パッケージの依存関係を判断するのに役立つコマンドが用意されています。 yum の場合は、`sudo yum deplist [package]` を使用します。 Ubuntu の場合は、`sudo apt-get install --reinstall --download-only [package name]` の後に `dpkg -I [package name].deb` を続けて使用します。

#### <a name="download-site"></a>ダウンロード サイト

[https://packages.microsoft.com/](https://packages.microsoft.com/) からパッケージをダウンロードできます。 Java 用のパッケージはすべて、データベース エンジンのパッケージと併置されています。 

#### <a name="redhat7-paths"></a>RedHat/7 パス

|||
|--|----|
| mssql/extensibility-java パッケージ | [https://packages.microsoft.com/rhel/7/mssql-server-preview/](https://packages.microsoft.com/rhel/7/mssql-server-preview/) |

#### <a name="ubuntu1604-paths"></a>Ubuntu/16.04 パス

|||
|--|----|
| mssql/extensibility-java パッケージ | [https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/) |

#### <a name="suse12-paths"></a>SUSE/12 パス

|||
|--|----|
| mssql/extensibility-java パッケージ | [https://packages.microsoft.com/sles/12/mssql-server-preview/](https://packages.microsoft.com/sles/12/mssql-server-preview/) |

#### <a name="package-list"></a>パッケージ一覧

使用する拡張機能に応じて、特定の言語に必要なパッケージをダウンロードします。 正確なファイル名にはサフィックス内のプラットフォーム情報が含まれますが、以下のファイル名では、取得するファイルを十分に判断できる程度に近いものにしておく必要があります。

```
# Core packages 
mssql-server-15.0.1000
mssql-server-extensibility-15.0.1000

# Java
mssql-server-extensibility-java-15.0.1000
```

## <a name="limitations"></a>制限事項

+ 現時点では、暗黙の認証は Linux 上では使用できません。つまり、データやその他のリソースにアクセスするために、実行中の Java からサーバーへ接続することはできません。

### <a name="resource-governance"></a>リソース管理

外部リソース プールに対する[リソースのガバナンス](../t-sql/statements/create-external-resource-pool-transact-sql.md)では、Linux と Windows 間に一致がありますが、[sys.dm_resource_governor_external_resource_pools](../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pools.md) の統計では、現在は Linux 上に異なるユニットがあります。 
 
| 列名   | [説明] | Linux 上の値 | 
|---------------|--------------|---------------|
|peak_memory_kb | リソース プールに使用されているメモリの最大量。 | Linux では、この統計は CGroups メモリ サブシステムから提供され、値は memory.max_usage_in_bytes になります |
|write_io_count | Resource Governor の統計がリセットされてから発行された書き込み IO の合計。 | Linux では、この統計は CGroups blkio サブシステムから提供され、書き込み行での値は blkio.throttle.io_serviced になります | 
|read_io_count | Resource Governor の統計がリセットされてから発行された読み取り IO の合計。 | Linux では、この統計は CGroups blkio サブシステムから提供され、読み取り行での値は blkio.throttle.io_serviced になります | 
|total_cpu_kernel_ms | Resource Governor の統計がリセットされてからの累積 CPU ユーザー カーネル時間 (ミリ秒単位)。 | Linux では、この統計は CGroups cpuacct サブシステムから提供され、ユーザー行での値は cpuacct.stat になります |  
|total_cpu_user_ms | Resource Governor の統計がリセットされてからの累積 CPU ユーザー時間 (ミリ秒単位)。| Linux では、この統計は CGroups cpuacct サブシステムから提供され、システム行での値は cpuacct.stat になります | 
|active_processes_count | 要求の時点で実行されている外部プロセスの数。| Linux では、この統計は CGroups pids サブシステムから提供され、値は pids.current になります | 

## <a name="next-steps"></a>次の手順

Java 開発者はいくつかの簡単な例を試して、SQL Server での Java の動作方法の基本を確認できます。 次の手順については、以下のリンクを参照してください。

+ [チュートリアル: Java での正規表現](../language-extensions/tutorials/search-for-string-using-regular-expressions-in-java.md)