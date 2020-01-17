---
title: Linux に SQL Server Machine Learning Services (Python、R) をインストールする
description: Linux に SQL Server Machine Learning Services (Python と R) をインストールする方法を説明します:(Red Hat、Ubuntu、SUSE)。
author: dphansen
ms.author: davidph
ms.reviewer: vanto
manager: cgronlun
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: machine-learning
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 4f32f4219e438a3f6dc390d11b50e6487c47ee49
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/04/2019
ms.locfileid: "73531247"
---
# <a name="install-sql-server-machine-learning-services-python-and-r-on-linux"></a>Linux に SQL Server Machine Learning Services (Python と R) をインストールする

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

この記事では、Linux に [SQL Server Machine Learning Services](../advanced-analytics/index.yml) をインストールする方法について説明します。 Machine Learning Services を使用して、データベース内で Python または R スクリプトを実行できます。

次の Linux ディストリビューションがサポートされています。

- Red Hat Enterprise Linux (RHEL)
- SUSE Linux Enterprise Server (SLES)
- Ubuntu

Machine Learning Services は、データベース エンジンのアドオン機能です。 [データベース エンジンと Machine Learning Services を同時にインストールする](#install-all)ことは可能ですが、コンポーネントを追加する前に問題を解決できるように、まずは SQL Server データベースエンジンをインストールして構成することをお勧めします。 

Python と R の拡張機能のパッケージは、SQL Server Linux ソース リポジトリに配置されています。 データベース エンジンのインストール用にソース リポジトリを既に構成している場合は、同じリポジトリ登録を使用して **mssql-mlservices** パッケージ インストール コマンドを実行できます。

Machine Learning Services は Linux コンテナーでもサポートされています。 Machine Learning Services は、ビルド済みのコンテナーに付属していませんが、[GitHub 上で入手できるサンプル テンプレート](https://github.com/Microsoft/mssql-docker/tree/master/linux/preview/examples/mssql-mlservices)を使用して、SQL Server コンテナーから作成できます。

Machine Learning Services は、SQL Server ビッグ データ クラスターに既定でインストールされています。この場合、手順に従う必要はありません。 詳細については、[ビッグ データ クラスターでの Machine Learning Services (Python および R) の使用](../big-data-cluster/machine-learning-services.md)に関するページを参照してください。

## <a name="uninstall-preview-release"></a>プレビューリリースをアンインストールする

プレビュー リリース (Community Technical Preview (CTP) またはリリース候補) をインストールしている場合は、SQL Server 2019 をインストールする前に、このバージョンをアンインストールして以前のすべてのパッケージを削除することをお勧めします。 複数のバージョンのサイド バイ サイド インストールはサポートされていません。また、パッケージ一覧は、最新のいくつかのプレビュー (CTP/RC) リリースで変更されています。

### <a name="1-confirm-package-installation"></a>1.パッケージのインストールを確認する

最初の手順として、状況に応じて以前のインストールの存在をチェックします。 次のファイルは既存のインストールを示します。checkinstallextensibility.sh、exthost、launchpad です。

```bash
ls /opt/microsoft/mssql/bin
```

### <a name="2-uninstall-ctprc-packages"></a>2.CTP/RC パッケージをアンインストールする

最下位のパッケージ レベルでアンインストールを行います。 より下位のパッケージに依存しているアップストリーム パッケージが、自動的にアンインストールされます。

  + R 統合の場合は、**microsoft-r-open*** を削除します
  + Python 統合の場合は、**mssql-mlservices-python** を削除します

次の表に、パッケージを削除するためのコマンドを示します。

| プラットフォーム  | パッケージの削除コマンド | 
|-----------|----------------------------|
| Red Hat   | `sudo yum remove microsoft-r-open-mro-3.4.4`<br/>`sudo yum remove msssql-mlservices-python` |
| SUSE  | `sudo zypper remove microsoft-r-open-mro-3.4.4`<br/>`sudo zypper remove msssql-mlservices-python` |
| Ubuntu    | `sudo apt-get remove microsoft-r-open-mro-3.4.4`<br/>`sudo apt-get remove msssql-mlservices-python`|

> [!Note]
> Microsoft R Open 3.4.4 は、以前にインストールした CTP リリースに応じて、2 つのパッケージで構成されています。 (foreachiterators パッケージは、CTP 2.2 のメインの mro パッケージに結合されました。)microsoft-r-open-mro-3.4.4 を削除した後にこれらのパッケージのいずれかが残っている場合は、それらを個別に削除する必要があります。
> ```
> microsoft-r-open-foreachiterators-3.4.4
> microsoft-r-open-mkl-3.4.4
> microsoft-r-open-mro-3.4.4
> ```

### <a name="3-proceed-with-install"></a>3.インストールを続行する

この記事の手順を使用して、お使いのオペレーティング システムに最上位のパッケージ レベルでインストールを行います。

OS 固有の一連のインストール手順ごとに、"*最上位のパッケージ レベル*" は、完全なパッケージ セットに対応した **例 1 - 完全なインストール**か、実行可能なインストールに必要なパッケージの最小数に対応した**例 2 - 最小限のインストール**のどちらかになります。

1. R 統合の場合は、[MRO](#mro) から開始します。これが前提条件であるためです。 R 統合はこれなしではインストールされません。

2. オペレーティング システムのパッケージ マネージャーと構文を使用して、インストール コマンドを実行します。 

   + [Red Hat](#RHEL)
   + [Ubuntu](#ubuntu)
   + [SUSE](#suse)

## <a name="prerequisites"></a>Prerequisites

+ Linux バージョンは、必ず [SQL Server によってサポートされます](sql-server-linux-release-notes-2019.md#supported-platforms)が、Docker エンジンは含まれていません。 サポートされているバージョンは次のとおりです。

   + [Red Hat Enterprise Linux (RHEL)](quickstart-install-connect-red-hat.md)

   + [SUSE Enterprise Linux Server](quickstart-install-connect-suse.md)

   + [Ubuntu](quickstart-install-connect-ubuntu.md)

+ (R のみ) [Microsoft R Open](#mro) は、SQL Server の R 機能用の基本 R ディストリビューションを提供します

+ T-SQL コマンドを実行するためのツールを用意しておく必要があります。 インストール後の構成および検証には、クエリ エディターが必要です。 Linux 上で実行される無料ダウンロードの [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/download?view=sql-server-2017#get-azure-data-studio-for-linux) をお勧めします。

<a name="mro"></a>

### <a name="microsoft-r-open-mro-installation"></a>Microsoft R Open (MRO) のインストール

Microsoft の R の基本ディストリビューションは、RevoScaleR、MicrosoftML、および Machine Learning Services と共にインストールされるその他の R パッケージを使用するための前提条件です。

必要なバージョンは MRO 3.5.2 です。

MRO をインストールするには、次の 2 つのアプローチを使用します。

+ MRAN から MRO tarball をダウンロードし、展開して、その install.sh スクリプトを実行します。 このアプローチを使用する場合は、[MRAN のインストール手順](https://mran.microsoft.com/releases/3.5.2)に従うことができます。

+ または、以下の説明に従って **packages.microsoft.com** リポジトリを登録して、MRO ディストリビューション (microsoft-r-open-mro と microsoft-r-open-mkl) を構成する 2 つのパッケージをインストールします。 

次のコマンドは、MRO を提供するリポジトリを登録します。 登録後、他の R パッケージをインストールするためのコマンド (mssql-mlservices-mml など) には、パッケージの依存関係として MRO が自動的に含まれます。

#### <a name="mro-on-ubuntu"></a>Ubuntu での MRO

```bash
# Install as root
sudo su

# Optionally, if your system does not have the https apt transport option
apt-get install apt-transport-https

# Set the location of the package repo the "prod" directory containing the distribution.
# This example specifies 16.04. Replace with 14.04 if you want that version
wget https://packages.microsoft.com/config/ubuntu/16.04/packages-microsoft-prod.deb

# Register the repo
dpkg -i packages-microsoft-prod.deb

# Update packages on your system (required), including MRO installation
sudo apt-get update
```

#### <a name="mro-on-red-hat"></a>Red Hat での MRO

```bash
# Import the Microsoft repository key
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc


# Set the location of the package repo at the "prod" directory
# The following command is for version 7.x
# For 6.x, replace 7 with 6 to get that version
rpm -Uvh https://packages.microsoft.com/config/rhel/7/packages-microsoft-prod.rpm

# Update packages on your system (optional)
yum update
```

#### <a name="mro-on-suse"></a>SUSE での MRO

```bash
# Install as root
sudo su

# Set the location of the package repo at the "prod" directory containing the distribution
# This example is for SLES12, the only supported version of SUSE in Machine Learning Server
zypper ar -f https://packages.microsoft.com/sles/12/prod packages-microsoft-com

# Update packages on your system (optional)
zypper update
```

## <a name="package-list"></a>パッケージ一覧

インターネットに接続されたデバイス上で、各オペレーティング システム用のパッケージ インストーラーを使用して、パッケージがデータベース エンジンとは別個にダウンロードおよびインストールされます。 次の表では、使用可能なすべてのパッケージについて説明します。ただし、R および Python の場合は、完全な機能のインストールまたは最小限の機能のインストールを提供するパッケージを指定します。

| パッケージ名 | 適用先 | [説明] |
|--------------|----------|-------------|
|mssql-server-extensibility  | All | R および Python コードを実行するために使用される拡張機能のフレームワーク。 |
| microsoft-openmpi  | Python、R | Linux での並列化用に Revo* ライブラリによって使用されるメッセージ パッシング インターフェイス。 |
| mssql-mlservices-python | Python | Anaconda と Python のオープンソース ディストリビューション。 |
|mssql-mlservices-mlm-py  | Python | *完全インストール*。 イメージの特性付けとテキストのセンチメント分析のための、revoscalepy、microsoftml、事前トレーニング済みのモデルを提供します。| 
|mssql-mlservices-packages-py  | Python | *最小インストール*。 revoscalepy と microsoftml を提供します。 <br/>事前トレーニング済みモデルは除外されます。 | 
| [microsoft-r-open*](#mro) | R | R のオープンソース ディストリビューション。3 つのパッケージで構成されています。 |
|mssql-mlservices-mlm-r  | R | *完全インストール*。 イメージの特性付けとテキストのセンチメント分析のための、RevoScaleR、MicrosoftML、sqlRUtils、olapR、事前トレーニング済みのモデルを提供します。| 
|mssql-mlservices-packages-r  | R | *最小インストール*。 RevoScaleR、sqlRUtils、MicrosoftML、olapR を提供します。 <br/>事前トレーニング済みモデルは除外されます。 | 

<a name="RHEL"></a>

## <a name="redhat-commands"></a>RedHat コマンド

言語サポートは、必要な任意の組み合わせ (1 つまたは複数の言語) でインストールできます。 R と Python では、2 つのパッケージから選択できます。 1 つは、*完全インストール*として機能するすべての利用可能な機能を提供します。 もう 1 つの選択肢では、事前トレーニング済みの機械学習モデルが除外され、*最小インストール*と見なされます。

> [!Tip]
> 可能であれば、`yum clean all` を実行して、インストールの前にシステム上のパッケージを更新しておきます。

### <a name="example-1----full-installation"></a>例 1 - 完全インストール 

オープンソースの R と Python、拡張機能のフレームワーク、microsoft openmpi、拡張機能 (R、Python)、R および Python 用の機械学習ライブラリと 事前トレーニング済みモデルが含まれています。 

```bash
# Install as root or sudo
# Add everything (all R, Python)
# Be sure to include -9.4.7* in mlsservices package names
sudo yum install mssql-mlservices-mlm-py-9.4.7*
sudo yum install mssql-mlservices-mlm-r-9.4.7* 
```

### <a name="example-2---minimum-installation"></a>例 2 - 最小インストール 

オープンソースの R と Python、拡張機能のフレームワーク、microsoft openmpi、コア Revo* ライブラリ、R および Python 用の機械学習ライブラリが含まれています。 事前トレーニング済みモデルは除外されます。

```bash
# Install as root or sudo
# Minimum install of R, Python extensions
# Be sure to include -9.4.6* in mlsservices package names
sudo yum install mssql-mlservices-packages-py-9.4.7*
sudo yum install mssql-mlservices-packages-r-9.4.7*
```

<a name="ubuntu"></a>

## <a name="ubuntu-commands"></a>Ubuntu コマンド

言語サポートは、必要な任意の組み合わせ (1 つまたは複数の言語) でインストールできます。 R と Python では、2 つのパッケージから選択できます。 1 つは、*完全インストール*として機能するすべての利用可能な機能を提供します。 もう 1 つの選択肢では、事前トレーニング済みの機械学習モデルが除外され、*最小インストール*と見なされます。

> [!Tip]
> 可能であれば、`apt-get update` を実行して、インストールの前にシステム上のパッケージを更新しておきます。 また、Ubuntu の一部の Docker イメージには、https apt transport オプションが含まれていない場合があります。 インストールするには、`apt-get install apt-transport-https` を使用します。

### <a name="example-1----full-installation"></a>例 1 - 完全インストール 

オープンソースの R と Python、拡張機能のフレームワーク、microsoft openmpi、拡張機能 (R、Python)、R および Python 用の機械学習ライブラリと 事前トレーニング済みモデルが含まれています。 

```bash
# Install as root or sudo
# Add everything (all R, Python)
# There is no asterisk in this full install
sudo apt-get install mssql-mlservices-mlm-py 
sudo apt-get install mssql-mlservices-mlm-r 
```

### <a name="example-2---minimum-installation"></a>例 2 - 最小インストール 

オープンソースの R と Python、拡張機能のフレームワーク、microsoft openmpi、コア Revo* ライブラリ、R および Python 用の機械学習ライブラリが含まれています。 事前トレーニング済みモデルは除外されます。 

```bash
# Install as root or sudo
# Minimum install of R, Python
# No aasterisk
sudo apt-get install mssql-mlservices-packages-py
sudo apt-get install mssql-mlservices-packages-r
```

<a name="suse"></a>

## <a name="suse-commands"></a>SUSE コマンド

言語サポートは、必要な任意の組み合わせ (1 つまたは複数の言語) でインストールできます。 R と Python では、2 つのパッケージから選択できます。 1 つは、*完全インストール*として機能するすべての利用可能な機能を提供します。 もう 1 つの選択肢では、事前トレーニング済みの機械学習モデルが除外され、*最小インストール*と見なされます。

### <a name="example-1----full-installation"></a>例 1 - 完全インストール 

オープンソースの R と Python、拡張機能のフレームワーク、microsoft openmpi、拡張機能 (R、Python)、R および Python 用の機械学習ライブラリと 事前トレーニング済みモデルが含まれています。 

```bash
# Install as root or sudo
# Add everything (all R, Python)
# Be sure to include -9.4.7* in mlsservices package names
sudo zypper install mssql-mlservices-mlm-py-9.4.7*
sudo zypper install mssql-mlservices-mlm-r-9.4.7* 
```

### <a name="example-2---minimum-installation"></a>例 2 - 最小インストール 

オープンソースの R と Python、拡張機能のフレームワーク、microsoft openmpi、コア Revo* ライブラリ、R および Python 用の機械学習ライブラリが含まれています。 事前トレーニング済みモデルは除外されます。 

```bash
# Install as root or sudo
# Minimum install of R, Python extensions
# Be sure to include -9.4.6* in mlsservices package names
sudo zypper install mssql-mlservices-packages-py-9.4.7*
sudo zypper install mssql-mlservices-packages-r-9.4.7*
```

## <a name="post-install-config-required"></a>インストール後の構成 (必須)

追加の構成には、主に [mssql-conf ツール](sql-server-linux-configure-mssql-conf.md)を利用します。


1. SQL Server サービスの実行に使用する mssql ユーザー アカウントを追加します。 事前にセットアップを実行していない場合、これは必須です。

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

2. オープンソースの R および Python のライセンス契約に同意します。 これにはいくつかの方法があります。 以前に SQL Server のライセンスを同意していて、この時点で R または Python の拡張機能を追加する場合は、次のコマンドで条項に同意したことになります。

   ```bash
   # Run as SUDO or root
   # Use set + EULA 
   sudo /opt/mssql/bin/mssql-conf set EULA accepteulaml Y
   ```

   もう 1 つのワークフローとして、SQL Server データベース エンジンのライセンス契約にまだ同意していない場合は、mssql-mlservices パッケージが検出され、`mssql-conf setup` の実行時に EULA の同意を求めるメッセージが表示されます。 EULA パラメーターの詳細については、[mssql-conf ツールを使用した SQL Server の構成](sql-server-linux-configure-mssql-conf.md#mlservices-eula)に関するページを参照してください。

3. 送信ネットワーク アクセスを有効にします。 既定では、送信ネットワーク アクセスは無効になっています。 送信要求を有効にするには、mssql-conf ツールを使用して "outboundnetworkaccess" ブール型プロパティを設定します。 詳しくは、「[mssql-conf ツールを利用して SQL Server on Linux を構成する](sql-server-linux-configure-mssql-conf.md#mlservices-outbound-access)」をご覧ください。

   ```bash
   # Run as SUDO or root
   # Enable outbound requests over the network
   sudo /opt/mssql/bin/mssql-conf set extensibility outboundnetworkaccess 1
   ```

4. R 機能の統合のみの場合、**MKL_CBWR** 環境変数を設定して、Intel Math Kernel Library (MKL) 計算からの[一貫した出力を保証](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr)します。

   + ユーザーのホーム ディレクトリで **bash_profile** という名前のファイルを編集または作成し、行 `export MKL_CBWR="AUTO"` をファイルに追加します。

   + bash コマンド プロンプトで「`source .bash_profile`」と入力して、このファイルを実行します。

5. SQL Server Launchpad サービスとデータベース エンジン インスタンスを再起動して、INI ファイルから更新後の値を読み込みます。 拡張機能に関連する設定が変更されるたびに、再起動を促すメッセージが表示されます。  

   ```bash
   systemctl restart mssql-launchpadd

   systemctl restart mssql-server.service
   ```

6. Azure Data Studio または Transact-SQL を実行する SQL Server Management Studio (Windows のみ) などの別のツールを使用して、外部スクリプトの実行を有効にします。 

   ```bash
   EXEC sp_configure 'external scripts enabled', 1 
   RECONFIGURE WITH OVERRIDE 
   ```

7. スタート パッド サービスをもう一度再起動します。

## <a name="verify-installation"></a>インストールの確認

R ライブラリ (MicrosoftML、RevoScaleR など) については、`/opt/mssql/mlservices/libraries/RServer` を参照してください。

Python ライブラリ (microsoftml および revoscalepy) については、`/opt/mssql/mlservices/libraries/PythonServer` を参照してください。

インストールを確認するには、R または Python を起動するシステム ストアド プロシージャが実行される T-SQL スクリプトを実行します。 このタスクには、クエリ ツールが必要になります。 Azure Data Studio が適しています。 SQL Server Management Studio や PowerShell など、一般的に使用されるその他のツールは Windows 限定です。 これらのツールを利用する Windows コンピューターがある場合は、それを使用してデータベース エンジンの Linux インストールに接続します。

次の SQL コマンドを実行して、SQL Server で R の実行をテストします。 スクリプトが実行されない場合は、サービスを再起動する `sudo systemctl restart mssql-server.service` を試してください。

```r
EXEC sp_execute_external_script   
@language =N'R', 
@script=N' 
OutputDataSet <- InputDataSet', 
@input_data_1 =N'SELECT 1 AS hello' 
WITH RESULT SETS (([hello] int not null)); 
GO 
```
 
次の SQL コマンドを実行して、SQL Server で Python の実行をテストします。 
 
```python
EXEC sp_execute_external_script  
@language =N'Python', 
@script=N' 
OutputDataSet = InputDataSet; 
', 
@input_data_1 =N'SELECT 1 AS hello' 
WITH RESULT SETS (([hello] int not null)); 
GO 
```

<a name="install-all"></a>

## <a name="chained-combo-install"></a>チェーンされた "コンボ" インストール

データベース エンジンをインストールするコマンドに R または Python のパッケージとパラメーターを付加すると、1 つの手順でデータベース エンジンと Machine Learning Services をインストールして構成することができます。 

1. R 統合の場合は、前提条件として [Microsoft R Open](#mro) をインストールします。 R 機能をインストールしない場合は、この手順をスキップしてください。

2. データベース エンジンに加えて、言語拡張機能を含めたコマンド ラインを指定します。

  データベース エンジンのインストールには、Python 統合などの 1 つの機能を追加できます。

  ```bash
  sudo yum install -y mssql-server mssql-mlservices-packages-r-9.4.7* 
  ```

  または、両方の拡張機能 (R、Python) を追加します。

  ```bash
  sudo yum install -y mssql-server mssql-mlservices-packages-r-9.4.7* mssql-mlservices-packages-py-9.4.7*
  ```

3. ライセンス契約に同意し、インストール後の構成を完了します。 このタスクには、**mssql-conf** ツールを使用します。

  ```bash
  sudo /opt/mssql/bin/mssql-conf setup
  ```

  データベース エンジンのライセンス契約に同意し、エディションを選択して、管理者パスワードを設定するように求められます。 また、Machine Learning Services のライセンス契約への同意も求められます。

4. 求められた場合は、サービスを再起動します。

  ```bash
  sudo systemctl restart mssql-server.service
  ```

## <a name="unattended-installation"></a>無人インストール

データベース エンジンの[無人インストール](https://docs.microsoft.com/sql/linux/sql-server-linux-setup?view=sql-server-2017#unattended)を使用して、mssql-mlservices と EULA を追加します。

セットアップまたは mssql-conf ツールでライセンス契約への同意を求めるメッセージが表示されます。 SQL Server データベース エンジンが既に構成されていて、EULA に同意している場合は、オープンソースの R および Python ディストリビューションに対して mlservices 固有の EULA パラメーターのいずれかを使用します。

```bash
sudo /opt/mssql/bin/mssql-conf setup accept-eula-ml
```

EULA の同意に関するすべての可能な順列は、「[Configure SQL Server on Linux with the mssql-conf tool](sql-server-linux-configure-mssql-conf.md#mlservices-eula)」(mssql-conf ツールを使用して SQL Server on Linux を構成する) に記載されています。

## <a name="offline-installation"></a>オフライン インストール

パッケージをインストールする手順については、[オフライン インストール](sql-server-linux-setup.md#offline)の手順に従います。 ダウンロード サイトを検索し、以下のパッケージ一覧を使用して特定のパッケージをダウンロードします。

> [!Tip]
> いくつかのパッケージ管理ツールには、パッケージの依存関係を判断するのに役立つコマンドが用意されています。 yum の場合は、`sudo yum deplist [package]` を使用します。 Ubuntu の場合は、`sudo apt-get install --reinstall --download-only [package name]` の後に `dpkg -I [package name].deb` を続けて使用します。


#### <a name="download-site"></a>ダウンロード サイト

[https://packages.microsoft.com/](https://packages.microsoft.com/) からパッケージをダウンロードできます。 R および Python 用の mlservices パッケージはすべて、データベース エンジン パッケージと併置されています。 mlservices パッケージの基本バージョンは、9.4.6 です。 microsoft-r-open パッケージが[別のリポジトリ](#mro)にあることを思い出してください。

#### <a name="rhel7-paths"></a>RHEL/7 パス

|||
|--|----|
| mssql/mlservices パッケージ | [https://packages.microsoft.com/rhel/7/mssql-server-preview/](https://packages.microsoft.com/rhel/7/mssql-server-preview/) |
| microsoft-r-open パッケージ | [https://packages.microsoft.com/rhel/7/prod/](https://packages.microsoft.com/rhel/7/prod/) | 


#### <a name="ubuntu1604-paths"></a>Ubuntu/16.04 パス

|||
|--|----|
| mssql/mlservices パッケージ | [https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/) |
| microsoft-r-open パッケージ | [https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/](https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/) | 

#### <a name="sles12-paths"></a>SLES/12 パス

|||
|--|----|
| mssql/mlservices パッケージ | [https://packages.microsoft.com/sles/12/mssql-server-preview/](https://packages.microsoft.com/sles/12/mssql-server-preview/) |
| microsoft-r-open パッケージ | [https://packages.microsoft.com/sles/12/prod/](https://packages.microsoft.com/sles/12/prod/) | 

#### <a name="package-list"></a>パッケージ一覧

使用する拡張機能に応じて、特定の言語に必要なパッケージをダウンロードします。 正確なファイル名にはサフィックス内のプラットフォーム情報が含まれますが、以下のファイル名では、取得するファイルを十分に判断できる程度に近いものにしておく必要があります。

```
# Core packages 
mssql-server-15.0.1000
mssql-server-extensibility-15.0.1000

# R
microsoft-openmpi-3.0.0
microsoft-r-open-mkl-3.5.2
microsoft-r-open-mro-3.5.2
mssql-mlservices-packages-r-9.4.7.64
mssql-mlservices-mlm-r-9.4.7.64


# Python
microsoft-openmpi-3.0.0
mssql-mlservices-python-9.4.7.64
mssql-mlservices-packages-py-9.4.7.64
mssql-mlservices-mlm-py-9.4.7.64
```

## <a name="add-more-rpython-packages"></a>その他の Python パッケージを追加する 
 
その他の R および Python パッケージをインストールし、SQL Server 2019 で実行されるスクリプトで使用することができます。

### <a name="r-packages"></a>R パッケージ 
 
1. R セッションを開始します。

   ```r
   # sudo /opt/mssql/mlservices/bin/R/R 
   ```

2. [glue](https://mran.microsoft.com/package/glue) という R パッケージをインストールして、パッケージのインストールをテストします。

   ```r
   # install.packages("glue",lib="/opt/mssql/mlservices/libraries/RServer") 
   ```
   または、コマンド ラインから R パッケージをインストールすることもできます 

   ```r
   # sudo /opt/mssql/mlservices/bin/R/R CMD INSTALL -l /opt/mssql/mlservices/libraries/RServer glue_1.1.1.tar.gz 
   ```

3. R パッケージを [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) にインストールします。

   ```r
   EXEC sp_execute_external_script  
   @language = N'R', 
   @script = N'library(glue)' 
   ```

### <a name="python-packages"></a>Python パッケージ 
 
1. pip を使用して [httpie](https://httpie.org/) という名前の Python パッケージをインストールします。 

   ```python
   # sudo /opt/mssql/mlservices/bin/python/python -m pip install httpie 
   ``` 

2. Python パッケージを [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) にインポートします。
 
   ```python
   EXEC sp_execute_external_script  
   @language = N'Python',  
   @script = N'import httpie' 
   ```

## <a name="run-in-a-container"></a>コンテナー内で実行する

下記の手順に従い、Docker コンテナー内で SQL Server Machine Learning Services をビルドして実行します。 詳細については、「[Docker で SQL Server コンテナーイメージを構成する](sql-server-linux-configure-docker.md)」を参照してください。

### <a name="prerequisites"></a>Prerequisites

- Git のコマンド ライン インターフェイス。
- サポートされているいずれかの Linux ディストリビューションの Docker エンジン 1.8 以降 または Mac/Windows 用 Docker。 詳細については、「[Install Docker](https://docs.docker.com/engine/installation/)」(Docker をインストールする) を参照してください。
- 2 ギガバイト (GB) 以上のディスク領域。
- 2 GB 以上の RAM。
- [SQL Server on Linux のシステム要件](sql-server-linux-setup.md#system)。

### <a name="clone-the-mssql-docker-repository"></a>mssql-docker リポジトリをクローンする

1. Linux または Mac で Bash ターミナルを開くか、または Windows で WSL ターミナルを開きます。

1. mssql-docker リポジトリのローカル コピーを保持するローカル ディレクトリを作成します。

1. git clone コマンドを実行して、mssql-docker リポジトリを複製します。

    ```bash
    git clone https://github.com/microsoft/mssql-docker mssql-docker
    ```

### <a name="build-a-sql-server-linux-container-image-with-machine-learning-services"></a>Machine Learning Services を使用して SQL Server Linux コンテナー イメージをビルドする

1. ディレクトリを mssql-mlservices ディレクトリに変更します。

    ```bash
    cd mssql-docker/linux/preview/examples/mssql-mlservices
    ```

1. build.sh スクリプトを実行します。

   ```bash
   ./build.sh
   ```

   > [!NOTE]
   > Docker イメージをビルドするには、サイズが数 GB のパッケージをいくつかインストールする必要があります。 このスクリプトは、ネットワークの帯域幅によって、完了までに最大 20 分かかります。

### <a name="run-the-sql-server-linux-container-image-with-machine-learning-services"></a>Machine Learning Services を使用して SQL Server Linux コンテナー イメージを実行する

1. コンテナーを実行する前に環境変数を設定します。 PATH_TO_MSSQL 環境変数をホスト ディレクトリに設定します。

   ```bash
    export MSSQL_PID='Developer'
    export ACCEPT_EULA='Y'
    export ACCEPT_EULA_ML='Y'
    export PATH_TO_MSSQL='/home/mssql/'
   ```

1. run.sh スクリプトを実行します。

   ```bash
   ./run.sh
   ```

   このコマンドでは、Developer エディション (既定) を使用して、Machine Learning Services を含む SQL Server コンテナーが作成されます。 SQL Server のポート **1433** は、ホスト上ではポート **1401** として公開されています。

   > [!NOTE]
   > SQL Server の実稼働エディションをコンテナーで実行するプロセスは、若干異なります。 詳細については、「[Docker で SQL Server コンテナーイメージを構成する](sql-server-linux-configure-docker.md)」を参照してください。 同じコンテナー名とポートを使う場合でも、このチュートリアルの残りの部分は実稼働のコンテナーで機能します。

1. Docker コンテナーを表示するには、`docker ps` コマンドを実行します。

   ```bash
   sudo docker ps -a
   ```

1. **[STATUS]** 列に表示されている状態が **[Up]** の場合、SQL Server はコンテナーで実行されており、 **[PORTS]** 列で指定されているポートでリッスンしています。 SQL Server コンテナーの **[STATUS]** 列に **[Exited]** と表示されている場合は、[構成ガイドのトラブルシューティングのセクション](sql-server-linux-configure-docker.md#troubleshooting)を参照してください。

   ```bash
   $ sudo docker ps -a
   ```

    出力結果: 
    
    ```
    CONTAINER ID        IMAGE                          COMMAND                  CREATED             STATUS              PORTS                    NAMES
    941e1bdf8e1d        mcr.microsoft.com/mssql/server/mssql-server-linux   "/bin/sh -c /opt/m..."   About an hour ago   Up About an hour     0.0.0.0:1401->1433/tcp   sql1
    ```

## <a name="next-steps"></a>次の手順

R 開発者はいくつかの簡単な例を試して、SQL Server での R の動作方法の基本を確認できます。 次の手順については、以下のリンクをご覧ください。

+ [チュートリアル: T-SQL での R の実行](../advanced-analytics/tutorials/quickstart-r-create-script.md)
+ [チュートリアル: R 開発者向けのデータベース内分析](../advanced-analytics/tutorials/sqldev-in-database-r-for-sql-developers.md)

Python 開発者は、次のチュートリアルに従って、SQL Server で Python を使用する方法を学習できます。

+ [チュートリアル: T-SQL での Python の実行](../advanced-analytics/tutorials/run-python-using-t-sql.md)
+ [チュートリアル: Python 開発者向けのデータベース内分析](../advanced-analytics/tutorials/sqldev-in-database-python-for-sql-developers.md)

実際のシナリオに基づいた機械学習の例については、[機械学習のチュートリアル](../advanced-analytics/tutorials/machine-learning-services-tutorials.md)を参照してください。
