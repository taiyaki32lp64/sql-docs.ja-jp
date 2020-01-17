---
title: PowerShell を使用して SSIS プロジェクトを配置する | Microsoft Docs
ms.date: 05/21/2018
ms.topic: quickstart
ms.prod: sql
ms.prod_service: integration-services
ms.custom: ''
ms.technology: integration-services
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 108331bfdff6734b7f5a8d64a4983f2c54490ec5
ms.sourcegitcommit: ef830f565ee07dc7d4388925cc3c86c5d2cfb4c7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/09/2019
ms.locfileid: "74947114"
---
# <a name="deploy-an-ssis-project-with-powershell"></a>PowerShell を使用して SSIS プロジェクトを配置する

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


このクイックスタートでは、PowerShell スクリプトを使用してデータベース サーバーに接続し、SSIS プロジェクトを SSIS カタログに配置する方法を示します。

## <a name="prerequisites"></a>前提条件

Azure SQL Database サーバーは、ポート 1433 でリッスンします。 企業のファイアウォール内から Azure SQL Database サーバーに接続しようとする場合、正常に接続するには、このポートを企業のファイアウォールで開ける必要があります。

## <a name="supported-platforms"></a>サポートされているプラットフォーム

このクイックスタートの情報を利用し、次のプラットフォームに SSIS プロジェクトをデプロイできます。

-   SQL Server on Windows。

-   Azure SQL Database。 Azure でパッケージをデプロイし、実行する方法については、「[SQL Server Integration Services ワークロードをクラウドにリフト アンド シフトする](lift-shift/ssis-azure-lift-shift-ssis-packages-overview.md)」を参照してください。

SQL Server on Linux に SSIS パッケージをデプロイする場合は、このクイックスタートの情報を使用できません。 Linux でパッケージを実行する方法については、[SSIS を使用し、Linux でデータの抽出、変換、読み込みを行う](../linux/sql-server-linux-migrate-ssis.md)方法に関するページを参照してください。

## <a name="for-azure-sql-database-get-the-connection-info"></a>Azure SQL Database の場合の接続情報の取得

プロジェクトを Azure SQL Database にデプロイするには、SSIS カタログ データベース (SSISDB) に接続するために必要な接続情報を取得します。 次の手順では、完全修飾サーバー名とログイン情報が必要です。

1. [Azure portal](https://portal.azure.com/) にサインインする
2. 左側のメニューから **[SQL Databases]** を選択し、 **[SQL データベース]** ページで SSISDB データベースを選びます。 
3. データベースの **[概要]** ページで、完全修飾サーバー名を確認します。 **[クリックしてコピー]** オプションを表示するには、サーバー名にマウス ポインターを移動します。 
4. Azure SQL Database サーバーのログイン情報を忘れた場合は、[SQL Database サーバー] ページに移動し、サーバーの管理者名を表示します。 必要に応じて、パスワードをリセットできます。
5. **[データベース接続文字列の表示]** をクリックします。
6. 完全な **ADO.NET** 接続文字列を確認します。

## <a name="supported-authentication-method"></a>サポートされている認証方法

[デプロイの認証方法](ssis-quickstart-deploy-ssms.md#authentication-methods-for-deployment)を参照してください。

## <a name="ssis-powershell-provider"></a>SSIS PowerShell プロバイダー
次のスクリプトの一番上で変数の適切な値を指定し、スクリプトを実行して SSIS プロジェクトを配置します。

> [!NOTE]
> 次の例では、Windows 認証を使用してオンプレミスの SQL Server に配置します。 SQL Server 認証を使用して接続を確立するには、`New-PSDive` コマンドレットを使用します。 Azure SQL Database サーバーに接続する場合、Windows 認証を使用できません。

```powershell
# Variables
$TargetInstanceName = "localhost\default"
$TargetFolderName = "Project1Folder"
$ProjectFilePath = "C:\Projects\Integration Services Project1\Integration Services Project1\bin\Development\Integration Services Project1.ispac"
$ProjectName = "Integration Services Project1"

# Get the Integration Services catalog
$catalog = Get-Item SQLSERVER:\SSIS\$TargetInstanceName\Catalogs\SSISDB\

# Create the target folder
New-Object "Microsoft.SqlServer.Management.IntegrationServices.CatalogFolder" ($catalog, 
$TargetFolderName,"Folder description") -OutVariable folder
$folder.Create()

# Read the project file and deploy it
[byte[]] $projectFile = [System.IO.File]::ReadAllBytes($ProjectFilePath)
$folder.DeployProject($ProjectName, $projectFile)

# Verify packages were deployed.
dir "$($catalog.PSPath)\Folders\$TargetFolderName\Projects\$ProjectName\Packages" | 
SELECT Name, DisplayName, PackageId
```

## <a name="powershell-script"></a>PowerShell スクリプト
次のスクリプトの一番上で変数の適切な値を指定し、スクリプトを実行して SSIS プロジェクトを配置します。

> [!NOTE]
> 次の例では、Windows 認証を使用してオンプレミスの SQL Server に配置します。 SQL Server 認証を使用するには、`Integrated Security=SSPI;` 引数を `User ID=<user name>;Password=<password>;` に置き換えます。 Azure SQL Database サーバーに接続する場合、Windows 認証を使用できません。

```powershell
# Variables
$SSISNamespace = "Microsoft.SqlServer.Management.IntegrationServices"
$TargetServerName = "localhost"
$TargetFolderName = "Project1Folder"
$ProjectFilePath = "C:\Projects\Integration Services Project1\Integration Services Project1\bin\Development\Integration Services Project1.ispac"
$ProjectName = "Integration Services Project1"

# Load the IntegrationServices assembly
$loadStatus = [System.Reflection.Assembly]::Load("Microsoft.SQLServer.Management.IntegrationServices, "+
    "Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91, processorArchitecture=MSIL")

# Create a connection to the server
$sqlConnectionString = `
    "Data Source=" + $TargetServerName + ";Initial Catalog=master;Integrated Security=SSPI;"
$sqlConnection = New-Object System.Data.SqlClient.SqlConnection $sqlConnectionString

# Create the Integration Services object
$integrationServices = New-Object $SSISNamespace".IntegrationServices" $sqlConnection

# Get the Integration Services catalog
$catalog = $integrationServices.Catalogs["SSISDB"]

# Create the target folder
$folder = New-Object $SSISNamespace".CatalogFolder" ($catalog, $TargetFolderName,
    "Folder description")
$folder.Create()

Write-Host "Deploying " $ProjectName " project ..."

# Read the project file and deploy it
[byte[]] $projectFile = [System.IO.File]::ReadAllBytes($ProjectFilePath)
$folder.DeployProject($ProjectName, $projectFile)

Write-Host "Done."
```

## <a name="next-steps"></a>次のステップ
- パッケージを配置する他の方法を検討します。
    - [SSMS を使用して SSIS パッケージを配置する](./ssis-quickstart-deploy-ssms.md)
    - [Transact-SQL (SSMS) を使用して SSIS パッケージを配置する](./ssis-quickstart-deploy-tsql-ssms.md)
    - [Transact-SQL (VS Code) を使用して SSIS パッケージを配置する](ssis-quickstart-deploy-tsql-vscode.md)
    - [コマンド プロンプトから SSIS パッケージを配置する](./ssis-quickstart-deploy-cmdline.md)
    - [C# を使用して SSIS パッケージを配置する](./ssis-quickstart-deploy-dotnet.md) 
- 配置されたパッケージを実行します。 パッケージを実行するには、いくつかのツールおよび言語から選択することができます。 詳細については、次の記事を参照してください。
    - [SSMS を使用して SSIS パッケージを実行する](./ssis-quickstart-run-ssms.md)
    - [Transact-SQL (SSMS) を使用して SSIS パッケージを実行する](./ssis-quickstart-run-tsql-ssms.md)
    - [Transact-SQL (VS Code) を使用して SSIS パッケージを実行する](ssis-quickstart-run-tsql-vscode.md)
    - [コマンド プロンプトから SSIS パッケージを実行する](./ssis-quickstart-run-cmdline.md)
    - [PowerShell を使用して SSIS パッケージを実行する](ssis-quickstart-run-powershell.md)
    - [C# を使用して SSIS パッケージを実行する](./ssis-quickstart-run-dotnet.md) 
