---
title: インストール:PowerShell Desired State Configuration
description: PowerShell Desired State Configuration (DSC) を使用して SQL Server をインストールする方法について説明します。
ms.custom: seo-lt-2019
ms.date: 12/13/2019
ms.devlang: PowerShell
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
author: randomnote1
ms.author: dareist
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 7e7b3f2d8673972100e01413e5688353cb7c87a6
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75258984"
---
# <a name="install-sql-server-with-powershell-desired-state-configuration"></a>PowerShell Desired State Configuration での SQL Server をインストールする

見直すこともなく、同じボタンを選択し、同じ情報を入力するだけで SQL Server のインストール インターフェイスを済ませたことはありますか。 インストールは完了しましたが、**sysadmin** ロールで DBA グループを指定するのを忘れていました。 このような場合、次の操作を実行する必要があります。
* シングルユーザー モードを開始します。
* 適切なユーザーまたはグループを追加します。
* マルチユーザー モードで SQL Server をバックアップします。
* テストします。 

さらに悪いことは、インストール全体への信頼が揺らぐことです。 "他に何か忘れていないか?" 自問するのではないでしょうか。

[PowerShell Desired State Configuration (DSC)](/powershell/scripting/dsc/overview/overview) に関するページを参照してください。 DSC を使用して、数百、数千のサーバーで再利用できる 1 つの構成テンプレートをビルドします。 ビルドによっては、いくつかの設定パラメーターを調整する必要があります。 ただし、すべての標準設定を適切に維持できるため、これは重要な問題ではありません。 この場合、重要なパラメーターの入力を忘れるという可能性は排除されます。

この記事では、**SqlServerDsc** DSC リソースを使用して、Windows Server 2016 上の SQL Server 2017 のスタンドアロン インスタンスの初期設定を参照します。 DSC がどのように動作するかを調べないときは、いくつかの DSC の予備知識があると役立ちます。

このチュートリアルには、次のアイテムが必須です。

- Windows Server 2016 を実行しているマシン。
- SQL Server 2017 のインストール メディア。
- **SqlServerDsc** DSC リソース。

## <a name="prerequisites"></a>前提条件

ほとんどの場合、DSC を使用して前提条件が処理されます。 ただし、このデモの目的のため、ここでは前提条件を手動で処理します。

## <a name="install-the-sqlserverdsc-dsc-resource"></a>SqlServerDsc DSC リソースのインストール

[SqlServerDsc](https://www.powershellgallery.com/packages/SqlServerDsc) DSC リソースは、[Install-Module](https://docs.microsoft.com/powershell/module/powershellget/Install-Module?view=powershell-5.1) コマンドレットを使用して [PowerShell Gallery](https://www.powershellgallery.com/) からダウンロードします。 

> [!NOTE]
> このモジュールをインストールするには、PowerShell が**管理者として**実行されていることを確認します。

```PowerShell
Install-Module -Name SqlServerDsc
```

### <a name="get-the-sql-server-2017-installation-media"></a>SQL Server 2017 のインストール メディアを取得する
SQL Server 2017 のインストール メディアをサーバーにダウンロードします。 Visual Studio サブスクリプションから SQL Server 2017 Enterprise をダウンロードして、ISO を `C:\en_sql_server_2017_enterprise_x64_dvd_11293666.iso` にコピーしました。

ここで、ISO はディレクトリに抽出される必要があります。

```PowerShell
New-Item -Path C:\SQL2017 -ItemType Directory
$mountResult = Mount-DiskImage -ImagePath 'C:\en_sql_server_2017_enterprise_x64_dvd_11293666.iso' -PassThru
$volumeInfo = $mountResult | Get-Volume
$driveInfo = Get-PSDrive -Name $volumeInfo.DriveLetter
Copy-Item -Path ( Join-Path -Path $driveInfo.Root -ChildPath '*' ) -Destination C:\SQL2017\ -Recurse
Dismount-DiskImage -ImagePath 'C:\en_sql_server_2017_enterprise_x64_dvd_11293666.iso'
```

## <a name="create-the-configuration"></a>構成の作成

### <a name="configuration"></a>構成

[管理オブジェクト フォーマット (MOF)](https://docs.microsoft.com/windows/desktop/WmiSdk/managed-object-format--mof-) ドキュメントを生成するために呼び出される構成関数を作成します。

```PowerShell
Configuration SQLInstall
{...}
```

### <a name="modules"></a>モジュール

モジュールを現在のセッションにインポートします。 このようなモジュールで、構成ドキュメントに MOF ドキュメントの作成方法を指示します。 また、DSC エンジンに MOF ドキュメントをサーバーに適用する方法も指示します。

```PowerShell
Import-DscResource -ModuleName SqlServerDsc
```

### <a name="resources"></a>リソース

#### <a name="net-framework"></a>.NET Framework

SQL Server は .NET Framework に依存しています。 そのため、それがインストールされていることを確認してから、SQL Server をインストールする必要があります。 **WindowsFeature** リソースは、**Net-Framework-45-Core** の Windows 機能のインストールに使用されます。

```PowerShell
WindowsFeature 'NetFramework45'
{
     Name = 'Net-Framework-45-Core'
     Ensure = 'Present'
}
```

#### <a name="sqlsetup"></a>SqlSetup

DSC に SQL Server をインストールする方法を指示するために、**SqlSetup** リソースが使用されます。 基本的なインストールに必要なパラメーターは次のとおりです。

- **InstanceName**。 インスタンスの名前。 既定のインスタンスには **MSSQLSERVER** を使用します。
- **Features**。 インストールする機能。 この例では、**SQLEngine** 機能のみをインストールします。
- **SourcePath**。 SQL インストール メディアへのパス。 この例では、SQL インストール メディアを `C:\SQL2017` に格納しました。 ネットワーク共有によって、サーバー上で使用される領域を最小限に抑えることができます。
- **SQLSysAdminAccounts**。 **sysadmin** ロールのメンバーになるユーザーまたはグループ。 この例では、ローカルの Administrators グループに **sysadmin** アクセス権を付与します。 

> [!NOTE]
> 高度なセキュリティ環境では、この構成は推奨されません。

**SqlSetup** で利用できるパラメーターの完全な一覧と説明は、[SqlServerDsc GitHub リポジトリ](https://github.com/PowerShell/SqlServerDsc/tree/master#sqlsetup)で入手できます。

**SqlSetup** リソースでは、SQL Server のみがインストールされ、適用される設定は**保持されません**。 例として、インストール時に **SQLSysAdminAccounts** を指定した場合があります。 管理者は **sysadmin** ロールのサインインの追加または削除することができます。 ただし、**SqlSetup** リソースは影響を受けません。 DSC に **sysadmin** ロールのメンバーシップを適用する必要がある場合は、[SqlServerRole](https://github.com/PowerShell/SqlServerDsc/tree/master#sqlserverrole) リソースを使用します。

#### <a name="finish-configuration"></a>構成の完了

```PowerShell
Configuration SQLInstall
{
     Import-DscResource -ModuleName SqlServerDsc

     node localhost
     {
          WindowsFeature 'NetFramework45'
          {
               Name   = 'NET-Framework-45-Core'
               Ensure = 'Present'
          }

          SqlSetup 'InstallDefaultInstance'
          {
               InstanceName        = 'MSSQLSERVER'
               Features            = 'SQLENGINE'
               SourcePath          = 'C:\SQL2017'
               SQLSysAdminAccounts = @('Administrators')
               DependsOn           = '[WindowsFeature]NetFramework45'
          }
     }
}
```

## <a name="build-and-deploy"></a>ビルドとデプロイ

### <a name="compile-the-configuration"></a>構成のコンパイル

構成スクリプトのドット ソース:

```PowerShell
. .\SQLInstallConfiguration.ps1
```

構成関数の実行:

```PowerShell
SQLInstall
```

**SQLInstall** というディレクトリが作業ディレクトリに作成されます。 これには **localhost.mof** というファイルが含まれています。 MOF のコンテンツを確認します。これにより、コンパイルされた DSC 構成が表示されます。

### <a name="deploy-the-configuration"></a>構成の配置

SQL Server の DSC 配置を開始するには、**Start-DscConfiguration** コマンドレットを呼び出します。 コマンドレットには次のパラメーターが指定されます。

- **Path**。 配置する MOF ドキュメントを含むフォルダーへのパスです。 たとえば `C:\SQLInstall` です。
- **Wait**。 構成ジョブが完了するまで待機します。
- **Force**。 任意の既存の DSC 構成をオーバーライドします。
- **Verbose**。 詳細の出力を表示します。 トラブルシューティングに役立てるために、最初に構成をプッシュするときに便利です。

```PowerShell
Start-DscConfiguration -Path C:\SQLInstall -Wait -Force -Verbose
```

構成が適用されると、詳細な出力に状況が表示されます。 エラー (赤いテキスト) がスローされない限り、画面上に "**操作 'Invoke CimMethod' が完了しました**" が表示されたら SQL Server をインストールするようにします。

## <a name="validate-installation"></a>インストールの検証

### <a name="dsc"></a>DSC

[Test-DscConfiguration](https://docs.microsoft.com/powershell/module/psdesiredstateconfiguration/test-dscconfiguration) コマンドレットによって、サーバーの現在の状態が目的の状態を満たしているかどうかを判断できます。 この場合は SQL Server のインストールです。 **Test-DscConfiguration** の結果は **True** になります。

```PowerShell
PS C:\> Test-DscConfiguration
True
```

### <a name="services"></a>サービス

サービスの一覧で SQL Server サービスが返されるようになります。

```PowerShell
PS C:\> Get-Service -Name *SQL*
Status  Name           DisplayName
------  ----           -----------
Running MSSQLSERVER    SQL Server (MSSQLSERVER)
Stopped SQLBrowser     SQL Server Browser
Running SQLSERVERAGENT SQL Server Agent (MSSQLSERVER)
Running SQLTELEMETRY   SQL Server CEIP service (MSSQLSERVER)
Running SQLWriter      SQL Server VSS Writer
```

### <a name="sql-server"></a>SQL Server

```PowerShell
PS C:\> & sqlcmd -S $env:COMPUTERNAME
1> SELECT @@SERVERNAME
2> GO
1> quit
```

## <a name="see-also"></a>参照

[Windows PowerShell Desired State Configuration の概要](/powershell/scripting/dsc/overview/overview)

[コマンド プロンプトからの SQL Server のインストール](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)

[構成ファイルを使用した SQL Server のインストール](../../database-engine/install-windows/install-sql-server-using-a-configuration-file.md)
