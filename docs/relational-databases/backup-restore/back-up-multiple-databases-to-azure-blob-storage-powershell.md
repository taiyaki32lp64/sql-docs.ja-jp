---
title: 複数のデータベースのバックアップ:Azure Blob Storage
titleSuffix: PowerShell
ms.custom: seo-lt-2019
ms.date: 12/17/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: f7008339-e69d-4e20-9265-d649da670460
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: a3e89a3dc9cff58b5ab610f0454217cc3b658dc4
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75247457"
---
# <a name="back-up-multiple-databases-to-azure-blob-storage---powershell"></a>Azure BLOB ストレージへの複数のデータベースのバックアップ - PowerShell

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

このトピックでは、PowerShell コマンドレットを使用して Azure Blob Storage サービスへのバックアップを自動化するために使用できるサンプル スクリプトを提供します。  
  
## <a name="overview-of-powershell-cmdlets-for-backup-and-restore"></a>バックアップと復元用の PowerShell コマンドレットの概要

バックアップ操作と復元操作を行うために使用できる 2 つの主要なコマンドレットは、 **Backup-SqlDatabase** と **Restore-SqlDatabase** です。

また、Windows Azure Blob ストレージへのバックアップを自動化するには、**SqlCredential** コマンドレットのセットなど、他のコマンドレットが必要になることもあります。

利用できるコマンドレットの一覧については、[SqlServer のコマンドレット](/powershell/module/sqlserver)に関するページを参照してください。
  
> [!TIP]  
> **SqlCredential** コマンドレットは、Azure Blob Storage へのバックアップと復元のシナリオで使用します。 資格情報とその使用方法の詳細については、[Microsoft Azure BLOB ストレージ サービスを使用した SQL Server のバックアップと復元](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)に関するページを参照してください。
  
### <a name="powershell-for-multi-database-multi-instance-backup-operations"></a>複数データベース/複数インスタンス バックアップ操作用の PowerShell

以下のセクションでは、SQL Server の複数インスタンスでの SQL 資格情報の作成、特定の SQL Server インスタンスにあるすべてのユーザー データベースのバックアップなど、さまざまな操作用のスクリプトを掲載します。 これらのスクリプトでは、使用している環境の要件に従ってバックアップ操作を自動化またはスケジュールすることができます。 ここに示すスクリプトは例であり、環境に合わせて変更または拡張することができます。  
  
サンプル スクリプトに関する注意点を次に示します。  
  
- SQL Server PowerShell では、PowerShell プロバイダーによってサポートされているオブジェクトの階層を表すパス構造を移動するコマンドレットが実装されています。 そのパス内のノードへ移動したときに、他のコマンドレットを使用して、現在のオブジェクトの基本的な操作を実行することができます。

  詳細については、「 [Navigate SQL Server PowerShell Paths](../../relational-databases/scripting/navigate-sql-server-powershell-paths.md)」をご参照ください。

- **Get-ChildItem** コマンドレット:**Get-ChildItem** から返される情報は、SQL Server PowerShell パス内の場所によって異なります。 たとえば、場所がコンピューター レベルである場合、このコマンドレットはコンピューターにインストールされているすべての SQL Server データベース エンジン インスタンスを返します。 あるいは、場所がデータベースなどのオブジェクト レベルである場合、データベース オブジェクトのリストを返します。 既定では、 **Get-ChildItem** コマンドレットはシステム オブジェクトを返しません。 `–Force` パラメーターを使用すると、システム オブジェクトが表示されます。

- Azure ストレージ アカウントと SQL 資格情報は必須の前提条件であり、Azure Blob ストレージ サービスに対するすべてのバックアップ操作と復元操作を対象とします。
  
### <a name="create-a-sql-credential-on-all-instances-of-sql-server"></a>SQL Server のすべてのインスタンスで SQL 資格情報を作成する

次のスクリプトは、コンピューター上にあるすべての SQL Server インスタンスの包括的 SQL 資格情報を作成する目的で使用できます。 いずれかのコンピューター インスタンス上に同じ名前の資格情報が既に存在する場合、このスクリプトはエラーを表示し、続行します。  
  
```powershell
# load the sqlps module
import-module sqlps  
  
# set parameters
$sqlPath = "sqlserver:\sql\$($env:COMPUTERNAME)"
$storageAccount = "<myStorageAccount>"  
$storageKey = "<myStorageAccessKey>"  
$secureString = ConvertTo-SecureString $storageKey -AsPlainText -Force  
$credentialName = "myCredential-$(Get-Random)"

Write-Host "Generate credential: " $credentialName
  
#cd to sql server and get instances  
cd $sqlPath
$instances = Get-ChildItem

#loop through instances and create a SQL credential, output any errors
foreach ($instance in $instances)  {
    try {
        $path = "$($sqlPath)\$($instance.DisplayName)\credentials"
        New-SqlCredential -Name $credentialName -Identity $storageAccount -Secret $secureString -Path $path -ea Stop | Out-Null
        Write-Host "...generated credential $($path)\$($credentialName)."  }
    catch { Write-Host $_.Exception.Message } }
```

> [!NOTE]
> ステートメント `-ea Stop | Out-Null` はユーザー定義の例外出力に使用されます。 既定の PowerShell エラー メッセージを希望する場合は、このステートメントは削除できます。 

### <a name="remove-a-sql-credential-from-all-instances-of-sql-server"></a>SQL Server のすべてのインスタンスから SQL 資格情報を削除する

次のスクリプトは、コンピューターにインストールされているすべての SQL Server インスタンスから特定の資格情報を削除する場合に使用できます。 特定のインスタンスに資格情報が存在しない場合は、エラー メッセージが表示され、すべてのインスタンスが確認されるまでスクリプトが続行されます。  
  
```powershell
import-module sqlps

$sqlPath = "sqlserver:\sql\$($env:COMPUTERNAME)"
$credentialName = "<myCredential>"

Write-Host "Delete credential: " $credentialName

cd $sqlPath
$instances = Get-ChildItem

#loop through instances and delete a SQL credential
foreach ($instance in $instances)  {
    try {
        $path = "$($sqlPath)\$($instance.DisplayName)\credentials\$($credentialName)"
        Remove-SqlCredential -Path $path -ea Stop | Out-Null
        Write-Host "...deleted credential $($path)."  }
    catch { Write-Host $_.Exception.Message } }
```  
  
### <a name="full-backup-for-all-databases"></a>すべてのデータベースの完全バックアップ

次のスクリプトでは、コンピューター上のすべてのデータベースのバックアップを作成します。 これには、ユーザー データベースと **msdb** システム データベースの両方が含まれます。 スクリプトでは、 **tempdb** システム データベースと **model** システム データベースを除外します。  
  
```powershell
import-module sqlps  

$sqlPath = "sqlserver:\sql\$($env:COMPUTERNAME)"
$storageAccount = "<myStorageAccount>"  
$blobContainer = "<myBlobContainer>"  
$backupUrlContainer = "https://$storageAccount.blob.core.windows.net/$blobContainer/"  
$credentialName = "<myCredential>"

Write-Host "Backup database: " $backupUrlContainer
  
cd $sqlPath
$instances = Get-ChildItem

#loop through instances and backup all databases (excluding tempdb and model)
foreach ($instance in $instances)  {
    $path = "$($sqlPath)\$($instance.DisplayName)\databases"
    $databases = Get-ChildItem -Force -Path $path | Where-object {$_.name -ne "tempdb" -and $_.name -ne "model"}

    foreach ($database in $databases) {
        try {
            $databasePath = "$($path)\$($database.Name)"
            Write-Host "...starting backup: " $databasePath
            Backup-SqlDatabase -Database $database.Name -Path $path -BackupContainer $backupUrlContainer -SqlCredential $credentialName -Compression On
            Write-Host "...backup complete."  }
        catch { Write-Host $_.Exception.Message } } }
```  
  
### <a name="full-backup-for-system-databases-only-on-a-specific-instance-of-sql-server"></a>SQL Server の特定のインスタンス上でのみのシステム データベースの完全バックアップ

次のスクリプトは、SQL Server の名前付きインスタンスの **master** データベースと **msdb** データベースをバックアップするために使用できます。 インスタンス パラメーター値を変更することで同じスクリプトをあらゆるインスタンスに使用できます。 SQL Server の既定のインスタンス名は `DEFAULT` です。
  
```powershell
import-module sqlps  

$sqlPath = "sqlserver:\sql\$($env:COMPUTERNAME)"
$instanceName = "DEFAULT"
$storageAccount = "<myStorageAccount>"  
$blobContainer = "<myBlobContainer>"  
$backupUrlContainer = "https://$storageAccount.blob.core.windows.net/$blobContainer/"  
$credentialName = "<myCredential>"

Write-Host "Backup database: " $instanceName " to " $backupUrlContainer
  
cd "$($sqlPath)\$($instanceName)"

#loop through instance and backup specific databases
$databases = "master", "msdb"  
foreach ($database in $databases) {
    try {
        Write-Host "...starting backup: " $database
        Backup-SqlDatabase -Database $database -BackupContainer $backupUrlContainer -SqlCredential $credentialName -Compression On
        Write-Host "...backup complete." }
    catch { Write-Host $_.Exception.Message } }
```  
  
## <a name="see-also"></a>参照

[Azure Blob Storage サービスを使った SQL Server のバックアップと復元](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)

[SQL Server Backup to URL に関するベスト プラクティスとトラブルシューティング](../../relational-databases/backup-restore/sql-server-backup-to-url-best-practices-and-troubleshooting.md)
