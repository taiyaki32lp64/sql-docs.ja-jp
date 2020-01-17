---
title: PowerShell Core で SQL Server on Linux を管理する
description: この記事では、SQL Server on Linux で PowerShell Core を使用する方法の概要を提供します。
ms.date: 04/22/2019
ms.prod: sql
ms.technology: linux
ms.topic: conceptual
author: SQLvariant
ms.author: aanelson
ms.reviewer: vanto
ms.openlocfilehash: e37237224dd9e8a6b44b913914c43d29cbc25d21
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028724"
---
# <a name="manage-sql-server-on-linux-with-powershell-core"></a>PowerShell Core で SQL Server on Linux を管理する

この記事では [SQL Server PowerShell](../powershell/sql-server-powershell.md) を紹介します。また、macOS と Linux で PowerShell Core (PS Core) を使用する方法について、例をいくつか紹介します。 PowerShell Core は [GitHub](https://github.com/powershell/powershell) のオープン ソース プロジェクトになりました。

## <a name="cross-platform-editor-options"></a>クロスプラットフォーム エディター オプション

下の PowerShell Core の手順はすべて、通常のターミナルで動作します。あるいは、VS Code または Azure Data Studio 内のターミナルから実行できます。  VS Code と Azure Data Studio のいずれも macOS と Linux で利用できます。  Azure Data Studio の詳細は、[このクイックスタート](https://docs.microsoft.com/sql/azure-data-studio/quickstart-sql-server)を参照してください。  [PowerShell 拡張機能](https://docs.microsoft.com/sql/azure-data-studio/powershell-extension)の使用もお勧めします。

## <a name="installing-powershell-core"></a>PowerShell Core のインストール

サポートされているさまざまな実験用プラットフォームで PowerShell Core をインストールする方法については、次の記事を参照してください。

- [Windows に PowerShell Core をインストールする](https://docs.microsoft.com/powershell/scripting/install/installing-powershell-core-on-windows?view=powershell-6)
- [Linux に PowerShell Core をインストールする](https://docs.microsoft.com/powershell/scripting/install/installing-powershell-core-on-linux?view=powershell-6)
- [macOS に PowerShell Core をインストールする](https://docs.microsoft.com/powershell/scripting/install/installing-powershell-core-on-macos?view=powershell-6)
- [ARM に PowerShell Core をインストールする](https://docs.microsoft.com/powershell/scripting/install/powershell-core-on-arm?view=powershell-6)

## <a name="install-the-sqlserver-module"></a>SqlServer モジュールをインストールする

`SqlServer` モジュールは [PowerShell ギャラリー](https://www.powershellgallery.com/packages/SqlServer/)で保守管理されます。 SQL Server を使用するとき、常に最新版の SqlServer PowerShell モジュールを使用してください。

SqlServer モジュールをインストールするには、PowerShell Core セッションを開き、次のコードを実行します。

```powerhsell
Install-Module -Name SqlServer
```

PowerShell ギャラリーから SqlServer モジュールをインストールする方法については、この[ページ](../powershell/download-sql-server-ps-module.md)を参照してください。

## <a name="using-the-sqlserver-module"></a>SqlServer モジュールを使用する

まず、PowerShell Core を起動してみましょう。  macOS または Linux を使用している場合、コンピューターで*ターミナル セッション*を開き、「**pwsh**」と入力すると、新しい PowerShell Core セッションが起動します。  Windows の場合、<kbd>Win</kbd>+<kbd>R</kbd> を使用し、「`pwsh`」と入力すると、新しい PowerShell Core セッションが起動します。

```
pwsh
```

SQL Server からは、**SqlServer** という名前の PowerShell モジュールが提供されます。 **SqlServer** モジュールを使用し、SQL Server コンポーネント (SQL Server プロバイダーとコマンドレット) を PowerShell 環境またはスクリプトにインポートできます。

現在の PowerShell セッションに **SqlServer** モジュールをインポートするには、次のコマンドをコピーして PowerShell プロンプトに貼り付けます。

```powershell
Import-Module SqlServer
```

**SqlServer** モジュールが正しくインポートされたことを確認するには、PowerShell プロンプトで次のコマンドを入力します。

```powershell
Get-Module -Name SqlServer
```

PowerShell には、次の出力のような情報が表示されるはずです。

```
ModuleType Version    Name          ExportedCommands
---------- -------    ----          ----------------
Script     21.1.18102 SqlServer     {Add-SqlAvailabilityDatabase, Add-SqlAvailabilityGroupList...
```

## <a name="connect-to-sql-server-and-get-server-information"></a>SQL Server に接続し、サーバー情報を取得する

次の手順では、PowerShell Core を使用して Linux 上の SQL Server インスタンスに接続し、いくつかのサーバー プロパティを表示します。

PowerShell プロンプトで次のコマンドをコピーして貼り付けます。 これらのコマンドを実行すると、PowerShell では、次のことが行われます。
- インスタンスのホスト名または IP アドレスの入力を求めるダイアログが表示されます
- *[PowerShell 資格情報の要求]* ダイアログが表示され、資格情報の入力が求められます。 *SQL ユーザー名*と *SQL パスワード*を使用し、Linux 上の SQL Server インスタンスに接続できます
- **Get-SqlInstance** コマンドレットを使用して **Server** に接続し、いくつかのプロパティを表示します

必要に応じて、`$serverInstance` 変数をお使いの SQL Server インスタンスの IP アドレスまたはホスト名に置き換えることができます。

```powershell
# Prompt for instance & credentials to login into SQL Server
$serverInstance = Read-Host "Enter the name of your instance"
$credential = Get-Credential

# Connect to the Server and return a few properties
Get-SqlInstance -ServerInstance $serverInstance -Credential $credential
# done
```

PowerShell には、次の出力のような情報が表示されるはずです。

```
Instance Name                   Version    ProductLevel UpdateLevel  HostPlatform HostDistribution
-------------                   -------    ------------ -----------  ------------ ----------------
your_server_instance            14.0.3048  RTM          CU13         Linux        Ubuntu
```

> [!NOTE]
> これらの値に対して何も表示されない場合、ターゲット SQL Server インスタンスへの接続に失敗した可能性があります。 同じ接続情報を使用して SQL Server Management Studio から接続できることを確認してください。 次に、[接続のトラブルシューティングに関する推奨事項](sql-server-linux-troubleshooting-guide.md#connection)を確認します。

## <a name="using-the-sql-server-powershell-provider"></a>SQL Server PowerShell プロバイダーの使用

SQL Server インスタンスに接続するもう 1 つの方法は、[SQL Server PowerShell プロバイダー](https://docs.microsoft.com/sql/powershell/sql-server-powershell-provider)を使用することです。  プロバイダーを使用すると、オブジェクト エクスプローラーのツリー構造の中を移動するように SQL Server インスタンスの中を移動できます (ただし、コマンドラインで)。  既定では、このプロバイダーは `SQLSERVER:\` という名前の PSDrive として表示されます。これを使用し、ドメイン アカウントでアクセスできる SQL Server インスタンスを接続し、その中を移動できます。  SQL Server on Linux 用に Active Directory 認証を設定する方法については、「[構成手順](https://docs.microsoft.com/sql/linux/sql-server-linux-active-directory-auth-overview#configuration-steps)」を参照してください。

SQL Server PowerShell プロバイダーで SQL 認証を使用することもできます。 これを行うには、`New-PSDrive` コマンドレットを使用して新しい PSDrive を作成し、正しい資格情報を指定して接続します。

下の例では、SQL 認証を使用し、新しい PSDrive を作成する方法を確認できます。

```powershell
# NOTE: We are reusing the values saved in the $credential variable from the above example.

New-PSDrive -Name SQLonDocker -PSProvider SqlServer -Root 'SQLSERVER:\SQL\localhost,10002\Default\' -Credential $credential
```

`Get-PSDrive` コマンドレットを実行すると、ドライブが作成されたことを確認できます。

```powershell
Get-PSDrive
```

新しい PSDrive が作成されたら、その中での移動を開始できます。

```powershell
dir SQLonDocker:\Databases
```

出力は次のようになります。  この出力は Databases ノードでの SSMS の出力に似ていることに気付くかもしれません。  ユーザー データベースが表示されますが、システムデータ ベースは表示されません。

```powershell
Name                 Status           Size     Space  Recovery Compat. Owner
                                            Available  Model     Level
----                 ------           ---- ---------- -------- ------- -----
AdventureWorks2016   Normal      209.63 MB    1.31 MB Simple       130 sa
AdventureWorksDW2012 Normal      167.00 MB   32.47 MB Simple       110 sa
AdventureWorksDW2014 Normal      188.00 MB   78.10 MB Simple       120 sa
AdventureWorksDW2016 Normal      172.00 MB   74.76 MB Simple       130 sa
AdventureWorksDW2017 Normal      208.00 MB   40.57 MB Simple       140 sa
```

インスタンス上のすべてのデータベースを表示する必要がある場合、`Get-SqlDatabase` コマンドレットを使用する方法があります。

## <a name="get-databases"></a>データベースを取得する

知っておくべき重要なコマンドレットに `Get-SqlDatabase` があります。  データベースが関係するさまざまな操作に対して、あるいはデータベース内のオブジェクトに対して `Get-SqlDatabase` コマンドレットを使用できます。  `-ServerInstance` パラメーターと `-Database` パラメーターの両方に値を提供する場合、その 1 つのデータベース オブジェクトだけが取得されます。  ただし、`-ServerInstance` パラメーターのみを指定した場合、そのインスタンス上のすべてのデータベースの完全な一覧が返されます。

```powershell
# NOTE: We are reusing the values saved in the $credential variable from the above example.

# Connect to the Instance and retrieve all databases
Get-SqlDatabase -ServerInstance ServerB -Credential $credential
```

上の Get-SqlDatabase コマンドからは次のようなものが返されます。

```powershell
Name                 Status           Size     Space  Recovery Compat. Owner
                                            Available  Model     Level
----                 ------           ---- ---------- -------- ------- -----
AdventureWorks2016   Normal      209.63 MB    1.31 MB Simple       130 sa
AdventureWorksDW2012 Normal      167.00 MB   32.47 MB Simple       110 sa
AdventureWorksDW2014 Normal      188.00 MB   78.10 MB Simple       120 sa
AdventureWorksDW2016 Normal      172.00 MB   74.88 MB Simple       130 sa
AdventureWorksDW2017 Normal      208.00 MB   40.63 MB Simple       140 sa
master               Normal        6.00 MB  600.00 KB Simple       140 sa
model                Normal       16.00 MB    5.70 MB Full         140 sa
msdb                 Normal       15.50 MB    1.14 MB Simple       140 sa
tempdb               Normal       16.00 MB    5.49 MB Simple       140 sa

```

## <a name="examine-sql-server-error-logs"></a>SQL Server エラー ログを調べる

次の手順では、PowerShell Core を使用し、Linux 上の SQL Server インスタンスで接続されているエラー ログを調べます。

PowerShell プロンプトで次のコマンドをコピーして貼り付けます。 実行に数分かかる場合があります これらのコマンドで次の手順が実行されます。
- インスタンスのホスト名または IP アドレスの入力を求めるダイアログが表示されます
- *[PowerShell 資格情報の要求]* ダイアログが表示され、資格情報の入力が求められます。 *SQL ユーザー名*と *SQL パスワード*を使用し、Linux 上の SQL Server インスタンスに接続できます
- **Get-SqlErrorLog** コマンドレットを使用して Linux 上の SQL Server インスタンスに接続し、**昨日**以降のエラー ログを取得します。

任意で、`$serverInstance` 変数を SQL Server インスタンスの IP アドレスまたはホスト名と置換できます。

```powershell
# Prompt for instance & credentials to login into SQL Server
$serverInstance = Read-Host "Enter the name of your instance"
$credential = Get-Credential

# Retrieve error logs since yesterday
Get-SqlErrorLog -ServerInstance $serverInstance -Credential $credential -Since Yesterday
# done
```

## <a name="explore-cmdlets-currently-available-in-ps-core"></a>PS Core で現在利用できるコマンドレットを試す
SqlServer モジュールには現在、Windows PowerShell で利用できるコマンドレットが 109 個用意されていますが、109 個のうちの 62 個だけが PSCore で利用できます。 現在利用できる 59 個のコマンドレットの完全な一覧は以下のようになります。  SqlServer モジュールの全コマンドレットを詳しく記録したものが必要な場合、SqlServer [コマンドレット リファレンス](https://docs.microsoft.com/powershell/module/sqlserver/)を参照してください。

次のコマンドでは、お使いのバージョンの PowerShell で利用できるすべてのコマンドレットが表示されます。

```powershell
Get-Command -Module SqlServer -CommandType Cmdlet |
SORT -Property Noun |
SELECT Name
```

- ConvertFrom-EncodedSqlName
- ConvertTo-EncodedSqlName
- Get-SqlAgent
- Get-SqlAgentJob
- Get-SqlAgentJobHistory
- Get-SqlAgentJobSchedule
- Get-SqlAgentJobStep
- Get-SqlAgentSchedule
- Invoke-SqlAssessment
- Get-SqlAssessmentItem
- Remove-SqlAvailabilityDatabase
- Resume-SqlAvailabilityDatabase
- Add-SqlAvailabilityDatabase
- Suspend-SqlAvailabilityDatabase
- New-SqlAvailabilityGroup
- Set-SqlAvailabilityGroup
- Remove-SqlAvailabilityGroup
- Switch-SqlAvailabilityGroup
- Join-SqlAvailabilityGroup
- Revoke-SqlAvailabilityGroupCreateAnyDatabase
- Grant-SqlAvailabilityGroupCreateAnyDatabase
- New-SqlAvailabilityGroupListener
- Set-SqlAvailabilityGroupListener
- Add-SqlAvailabilityGroupListenerStaticIp
- Set-SqlAvailabilityReplica
- Remove-SqlAvailabilityReplica
- New-SqlAvailabilityReplica
- Set-SqlAvailabilityReplicaRoleToSecondary
- New-SqlBackupEncryptionOption
- Get-SqlBackupHistory
- Invoke-Sqlcmd
- New-SqlCngColumnMasterKeySettings
- Remove-SqlColumnEncryptionKey
- Get-SqlColumnEncryptionKey
- Remove-SqlColumnEncryptionKeyValue
- Add-SqlColumnEncryptionKeyValue
- Get-SqlColumnMasterKey
- Remove-SqlColumnMasterKey
- New-SqlColumnMasterKey
- Get-SqlCredential
- Set-SqlCredential
- New-SqlCredential
- Remove-SqlCredential
- New-SqlCspColumnMasterKeySettings
- Get-SqlDatabase
- Restore-SqlDatabase
- Backup-SqlDatabase
- Set-SqlErrorLog
- Get-SqlErrorLog
- New-SqlHADREndpoint
- Set-SqlHADREndpoint
- Get-SqlInstance
- Add-SqlLogin
- Remove-SqlLogin
- Get-SqlLogin
- Set-SqlSmartAdmin
- Get-SqlSmartAdmin
- Read-SqlTableData
- Write-SqlTableData
- Read-SqlViewData
- Read-SqlXEvent
- Convert-UrnToPath

## <a name="see-also"></a>参照
- [SQL Server PowerShell](../relational-databases/scripting/sql-server-powershell.md)
