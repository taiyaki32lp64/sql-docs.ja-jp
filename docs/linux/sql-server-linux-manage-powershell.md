---
title: PowerShell で SQL Server on Linux を管理する
description: この記事では、Windows 上の PowerShell を SQL Server on Linux で使う方法の概要を説明します。
author: VanMSFT
ms.author: vanto
ms.date: 10/02/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: a3492ce1-5d55-4505-983c-d6da8d1a94ad
ms.openlocfilehash: 52db0986bb6af34e1dc034d95146a96d3fdcf246
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/25/2019
ms.locfileid: "68000120"
---
# <a name="use-powershell-on-windows-to-manage-sql-server-on-linux"></a>Windows 上の PowerShell を使用して SQL Server on Linux を管理する

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

この記事では、[SQL Server PowerShell](../powershell/sql-server-powershell.md) を紹介し、それを SQL Server on Linux で使う方法について、いくつかの手順例を示します。 PowerShell による SQL Server のサポートは、現在、Windows、MacOS、Linux で使用できます。 この記事では、Windows コンピューターを使って Linux 上のリモート SQL Server インスタンスに接続する手順について説明します。

## <a name="install-the-newest-version-of-sql-powershell-on-windows"></a>Windows に最新バージョンの SQL PowerShell をインストールする

Windows 上の [SQL PowerShell](../powershell/download-sql-server-ps-module.md) は、PowerShell ギャラリーで提供されています。 SQL Server を使用するとき、常に最新版の SqlServer PowerShell モジュールを使用してください。

## <a name="before-you-begin"></a>アンインストールの準備

SQL Server on Linux の[既知の問題](sql-server-linux-release-notes.md)を参照してください。

## <a name="launch-powershell-and-import-the-sqlserver-module"></a>PowerShell を起動して *sqlserver* モジュールをインポートする

最初に、Windows 上で PowerShell を起動しましょう。 Windows コンピューターで <kbd>Win</kbd> + <kbd>R</kbd> キーを押し、「**PowerShell**」と入力して、新しい windows PowerShell セッションを起動します。

```
PowerShell
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

Windows 上の PowerShell を使用して Linux 上の SQL Server インスタンスに接続し、サーバーのプロパティをいくつか表示してみましょう。

次のコマンドをコピーして PowerShell プロンプトに貼り付けます。 これらのコマンドを実行すると、PowerShell では、次のことが行われます。
- インスタンスのホスト名または IP アドレスの入力を求めるダイアログが表示されます
- *[Windows PowerShell 資格情報の要求]* ダイアログが表示され、資格情報の入力を求められます。 "*SQL ユーザー名*" と "*SQL パスワード*" を使って、Linux 上の SQL Server インスタンスに接続できます
- **Get-SqlInstance** コマンドレットを使用して **Server** に接続し、いくつかのプロパティを表示します

必要に応じて、`$serverInstance` 変数をお使いの SQL Server インスタンスの IP アドレスまたはホスト名に置き換えることができます。

```powershell
# Prompt for instance & credentials to login into SQL Server
$serverInstance = Read-Host "Enter the name of your instance"
$credential = Get-Credential

# Connect to the Server and get a few properties
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

SQL Server インスタンスに接続するもう 1 つの方法は、[SQL Server PowerShell プロバイダー](https://docs.microsoft.com/sql/powershell/sql-server-powershell-provider)を使用することです。  このプロバイダーを使用すると、オブジェクト エクスプローラーのツリー構造の中を移動するように (ただし、コマンド ラインで) SQL Server インスタンスの中を移動できます。  既定では、このプロバイダーは `SQLSERVER:\` という名前の PSDrive として表示されます。これを使用し、ドメイン アカウントでアクセスできる SQL Server インスタンスを接続し、その中を移動できます。  SQL Server on Linux 用に Active Directory 認証を設定する方法については、「[構成手順](https://docs.microsoft.com/sql/linux/sql-server-linux-active-directory-auth-overview#configuration-steps)」を参照してください。

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

出力は次のようになります。  出力は Databases ノードでの SSMS の出力に似ていることに気付くかもしれません。  ユーザー データベースが表示されますが、システムデータ ベースは表示されません。

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

インスタンス上のすべてのデータベースを表示する必要がある場合、1 つの方法は [Get-SqlDatabase](https://docs.microsoft.com/powershell/module/sqlserver/Get-SqlDatabase) コマンドレットを使うことです。

## <a name="examine-sql-server-error-logs"></a>SQL Server エラー ログを調べる

次の手順では、Windows 上の PowerShell を使って、Linux 上の SQL Server インスタンスで接続されているエラー ログを調べます。 また、**Out-GridView** コマンドレットを使って、エラー ログの情報をグリッド ビューに表示します。

次のコマンドをコピーして PowerShell プロンプトに貼り付けます。 実行に数分かかる場合があります。 これらのコマンドでは次のことが行われます。
- インスタンスのホスト名または IP アドレスの入力を求めるダイアログが表示されます
- *[Windows PowerShell 資格情報の要求]* ダイアログが表示され、資格情報の入力を求められます。 "*SQL ユーザー名*" と "*SQL パスワード*" を使って、Linux 上の SQL Server インスタンスに接続できます
- **Get-SqlErrorLog** コマンドレットを使用して Linux 上の SQL Server インスタンスに接続し、**昨日**以降のエラー ログを取得します
- 出力が **Out-GridView** コマンドレットにパイプされます

必要に応じて、`$serverInstance` 変数をお使いの SQL Server インスタンスの IP アドレスまたはホスト名に置き換えることができます。

```powershell
# Prompt for instance & credentials to login into SQL Server
$serverInstance = Read-Host "Enter the name of your instance"
$credential = Get-Credential

# Retrieve error logs since yesterday
Get-SqlErrorLog -ServerInstance $serverInstance -Credential $credential -Since Yesterday | Out-GridView
# done
```
## <a name="see-also"></a>参照
- [SQL Server PowerShell](../relational-databases/scripting/sql-server-powershell.md)
- [SqlServer のコマンドレット](https://docs.microsoft.com/powershell/module/sqlserver)
