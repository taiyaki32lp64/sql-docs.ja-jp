---
title: PowerShell を使用して複数のデータベースを Azure Blob Storage サービスにバックアップする |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: f7008339-e69d-4e20-9265-d649da670460
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 701928a722e14cf3eb5c1e678a1dd764597f46ec
ms.sourcegitcommit: a165052c789a327a3a7202872669ce039bd9e495
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72783084"
---
# <a name="use-powershell-to-backup-multiple-databases-to-azure-blob-storage-service"></a>PowerShell を使った Azure Blob Storage サービスへの複数データベースのバックアップ
  このトピックでは、PowerShell コマンドレットを使用して Azure Blob Storage サービスへのバックアップを自動化するために使用できるサンプル スクリプトを提供します。  
  
## <a name="overview-of-powershell-cmdlets-for-backup-and-restore"></a>バックアップと復元用の PowerShell コマンドレットの概要  
 バックアップ操作と復元操作を行うために使用できる 2 つの主要なコマンドレットは、`Backup-SqlDatabase` と `Restore-SqlDatabase` です。 さらに、一連の **SqlCredential** コマンドレットのように、Azure Blob Storage へのバックアップを自動化するために必要な他のコマンドレットもあります。バックアップおよび復元操作用として [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] に用意されている PowerShell コマンドレットを次に示します。  
  
 Backup-SqlDatabase  
 このコマンドレットは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] バックアップを作成するために使用します。  
  
 Restore-SqlDatabase  
 データベースを復元するために使用します。  
  
 New-SqlCredential  
 このコマンドレットは、Azure Storage の SQL Server バックアップに使用する SQL 資格情報を作成するために使用します。 SQL Server のバックアップと復元における資格情報とその使用方法の詳細については、「 [Azure Blob Storage サービスを使用したバックアップと復元の SQL Server](sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)」を参照してください。  
  
 Get-SqlCredential  
 このコマンドレットは、資格情報オブジェクトとそのプロパティを取得するために使用します。  
  
 Remove-SqlCredential  
 SQL 資格情報オブジェクトを削除します。  
  
 Set-SqlCredential  
 このコマンドレットは、SQL 資格情報オブジェクトのプロパティを変更または設定するために使用します。  
  
> [!TIP]  
>  Credential コマンドレットは、Azure Blob Storage へのバックアップと復元のシナリオで使用します。  
  
### <a name="powershell-for-multi-database-multi-instance-backup-operations"></a>複数データベース/複数インスタンス バックアップ操作用の PowerShell  
 以下のセクションでは、SQL Server の複数インスタンスでの SQL 資格情報の作成、特定の SQL Server インスタンスにあるすべてのユーザー データベースのバックアップなど、さまざまな操作用のスクリプトを掲載します。 これらのスクリプトでは、使用している環境の要件に従ってバックアップ操作を自動化またはスケジュールすることができます。 ここに示すスクリプトは例であり、環境に合わせて変更または拡張することができます。  
  
 サンプル スクリプトに関する注意点を次に示します。  
  
1.  **SQL Server PowerShell パスの移動:** Windows PowerShell では、コマンドレットを実装して、PowerShell プロバイダーによりサポートされるオブジェクトの階層を表すパス構造を移動できます。 そのパス内のノードへ移動したときに、他のコマンドレットを使用して、現在のオブジェクトの基本的な操作を実行することができます。  
  
2.  `Get-ChildItem` コマンドレット: `Get-ChildItem` から返される情報は、SQL Server PowerShell パス内の場所によって異なります。 たとえば、場所がコンピューター レベルである場合、このコマンドレットはコンピューターにインストールされているすべての SQL Server データベース エンジン インスタンスを返します。 もう 1 つの例として、場所がデータベースなどのオブジェクト レベルである場合、このコマンドレットはデータベース オブジェクトのリストを返します。  既定では、`Get-ChildItem` コマンドレットはシステム オブジェクトを返しません。  -Force パラメーターを使用すると、システム オブジェクトを表示できます。  
  
     詳細については、「 [Navigate SQL Server PowerShell Paths](../../powershell/navigate-sql-server-powershell-paths.md)」をご参照ください。  
  
3.  各コード サンプルは変数値を変更して個別に試すことができますが、Azure ストレージ アカウントおよび SQL 資格情報の作成が前提条件であり、Azure Blob Storage サービスへのすべてのバックアップ操作と復元操作に必要です。  
  
### <a name="create-a-sql-credential-on-all-the-instances-of-sql-server"></a>SQL Server のすべてのインスタンスで SQL 資格情報を作成する  
 2 種類のサンプル スクリプトがあり、いずれもコンピューター上のすべての SQL Server インスタンスで SQL 資格情報 "mybackupToURL" を作成します。 最初の例では単純に資格情報を作成し、例外をトラップしません。  たとえば、コンピューター上のいずれかのインスタンスに同じ名前の資格情報が既に存在する場合、このスクリプトは失敗します。 2 番目の例ではエラーをトラップし、スクリプトを続行できます。  
  
```powershell
import-module sqlps  
  
# create variables  
$storageAccount = "mystorageaccount"  
$storageKey = "<storageaccesskeyvalue>"  
$secureString = ConvertTo-SecureString $storageKey  -asplaintext -force  
$credentialName = "mybackuptoURL"  
  
#cd to computer level  
cd sqlserver:\sql\COMPUTERNAME  
# get the list of instances  
$instances = Get-ChildItem  
#pipe the instances to new-sqlcredentail cmdlet to create SQL credential  
$instances | New-SqlCredential -Name $credentialName -Identity $storageAccount -Secret $secureString  
```  
  
```powershell
import-module sqlps  
  
# set the parameter values
$storageAccount = "mystorageaccount"  
$storageKey = "<storageaccesskeyvalue>"  
$secureString = ConvertTo-SecureString $storageKey  -asplaintext -force  
$credentialName = "mybackuptoURL"  
  
#cd to computer level  
cd sqlserver:\sql\COMPUTERNAME  
# get the list of instances  
$instances = Get-ChildItem  
#loop through instances and create a SQL credential, output any errors  
ForEach ($instance In $instances)  
{  
    Try  
{  
     New-SqlCredential -Name $credentialName -path "SQLServer:\SQL\$($instance.name)" -Identity $storageAccount -Secret $secureString -ea Stop
}  
Catch [Exception]  
    {
            Write-Host "instance - $($instance.name): "$_.Exception.Message
    }
 }
```  
  
### <a name="remove-a-sql-credential-from-all-the-instances-of-sql-server"></a>SQL Server のすべてのインスタンスから SQL 資格情報を削除する  
 このスクリプトは、コンピューターにインストールされているすべての SQL Server インスタンスから特定の資格情報を削除する場合に使用できます。 特定のインスタンスに資格情報オブジェクトが存在しない場合は、エラー メッセージが表示され、すべてのインスタンスが確認されるまでスクリプトが続行されます。  
  
```powershell
import-module sqlps  
  
cd SQLServer:\SQL\COMPUTERNAME  
$credentialName = "mybackuptoURL"  
  
$instances = Get-ChildItem  
  
ForEach ($instance In $instances)  
   {
    Try  
        {  
            $path = "SQLServer:\SQL\$($instance.name)\credentials\$credentialName"   
            Remove-SqlCredential -Path $path -ea stop   
         }  
         Catch [Exception]  
         {  
            Write-Host $_.Exception.Message
        }
    }  
```  
  
### <a name="full-database-backup-for-all-databases-including-system-databases"></a>すべてのデータベース (システム データベースを含む) の完全バックアップ  
 次のスクリプトでは、コンピューター上のすべてのデータベースのバックアップを作成します。 これには、ユーザー データベースと **msdb** システム データベースの両方が含まれます。 スクリプトでは、 **tempdb** システム データベースと **model** システム データベースを除外します。  
  
```powershell
import-module sqlps  
# set the parameter values  
$storageAccount = "mystorageaccount"  
$blobContainer = "privatecontainertest"  
$backupUrlContainer = "https://$storageAccount.blob.core.windows.net/$blobContainer/"  
$credentialName = "mybackuptoURL"  
  
# cd to computer level
cd SQLServer:\SQL\COMPUTERNAME  
$instances = Get-ChildItem
# loop through each instances and backup up all the  databases -filter out tempdb and model databases  
  
 ForEach ($instance In $instances)  
 {  
   $path = "sqlserver:\sql\$($instance.name)\databases"  
   $alldatabases = Get-ChildItem -Force -path $path | Where-Object {$_.name -ne "tempdb" -and $_.name -ne "model"}   
   $alldatabases | Backup-SqlDatabase -BackupContainer $backupUrlContainer -SqlCredential $credentialName -Compression On -script   
 }
```  
  
### <a name="full-database-backup-for-all-user-databases"></a>すべてのユーザー データベースの完全バックアップ  
 次のスクリプトは、コンピューター上にあるすべての SQL Server インスタンスのユーザー データベースをすべてバックアップするために使用できます。  
  
```powershell
import-module sqlps
  
$storageAccount = "mystorageaccount"  
$blobContainer = "privatecontainertest"  
$backupUrlContainer = "https://$storageAccount.blob.core.windows.net/$blobContainer/"  
$credentialName = "mybackuptoURL"  
  
# cd to computer level
cd SQLServer:\SQL\COMPUTERNAME  
$instances = Get-ChildItem
# loop through each instances and backup up all the user databases  
 ForEach ($instance In $instances)  
 {  
    $databases = dir "sqlserver:\sql\$($instance.name)\databases"  
    $databases | Backup-SqlDatabase -BackupContainer $backupUrlContainer -SqlCredential $credentialName -Compression On
 }  
```  
  
### <a name="full-database-backup-for-master-and-msdb-system-databases-on-all-the-instances-of-sql-server"></a>すべての SQL Server インスタンスの master と msdb (システム データベース) の完全バックアップ  
 次のスクリプトは、コンピューター上にインストールされているすべての SQL Server インスタンスの **master** データベースと **msdb** データベースをバックアップするために使用できます。  
  
```powershell
import-module sqlps  
  
$storageAccount = "mystorageaccount"  
$blobContainer = "privatecontainertest"  
$backupUrlContainer = "https://$storageAccount.blob.core.windows.net/$blobContainer/"  
$credentialName = "mybackupToUrl"  
$sysDbs = "master", "msdb"  
  
#cd to computer level  
cd sqlserver:\sql\COMPUTERNAME  
$instances = Get-ChildItem
ForEach ($instance In $instances)  
 {  
      ForEach ($s In $sysdbs)  
     {  
        Backup-SqlDatabase -Database $s -path "sqlserver:\sql\$($instance.name)" -BackupContainer  $backupUrlContainer -SqlCredential $credentialName -Compression On   
}
 } 
```  
  
### <a name="full-database-backup-for-all-user-databases-on-an-instance-of-sql-server"></a>SQL Server インスタンスのすべてのユーザー データベースの完全バックアップ  
 次のスクリプトは、SQL Server の名前付きインスタンスで使用可能なユーザー データベースのみをバックアップするために使用します。 $srvPath パラメーターの値を変更することで、同じスクリプトをコンピューター上の既定インスタンスに使用することもできます。  
  
```powershell
import-module sqlps  
  
$storageAccount = "mystorageaccount"  
$blobContainer = "privatecontainertest"  
$backupUrlContainer = "https://$storageAccount.blob.core.windows.net/$blobContainer/"  
$srvPath = "SQLServer:\SQL\COMPUTERNAME\INSTANCENAME"  # for default instance, the $srvpath variable is "SQLSERVER:\SQL\COMPUTERNAME\DEFAULT"  
$credentialName = "mybackupToUrl"  
  
#cd to computer level  
cd sqlserver:\sql\COMPUTERNAME  
  
#retrieves the database objects for a specific instance  
$databases = dir $srvPath\databases  
  
#backup all the user databases  
$databases | Backup-SqlDatabase -BackupContainer $backupUrlContainer -SqlCredential $credentialName -Compression On  
```  
  
### <a name="full-database-backup-for-only-system-databases-master-and-msdb-on-an-instance-of-sql-server"></a>SQL Server インスタンスのシステム データベース (master と msdb) のみの完全バックアップ  
 次のスクリプトは、SQL Server の名前付きインスタンスの **master** データベースと **msdb** データベースをバックアップするために使用できます。 $srvPath パラメーターの値を変更することで、同じスクリプトをコンピューター上の既定インスタンスに使用することもできます。  
  
```powershell
import-module sqlps  
  
$storageAccount = "mystorageaccount"  
$blobContainer = "privatecontainertest"  
$backupUrlContainer = "https://$storageAccount.blob.core.windows.net/$blobContainer/"  
$srvPath = "SQLServer:\SQL\COMPUTERNAME\INSTANCENAME" # for default instance, the $srvpath variable is "SQLSERVER:\SQL\COMPUTERNAME\DEFAULT"  
$credentialName = "mybackupToUrl"  
  
#navigate to instance level  
cd $srvPath  
  
$sysDbs = "master", "msdb"  
ForEach ($s In $sysDbs)
{  
Backup-SqlDatabase -Database $s -BackupContainer $backupUrlContainer -SqlCredential $credentialName -Compression On  
}
```  
  
## <a name="see-also"></a>「
 [Azure Blob Storage サービスを使用したバックアップと復元の SQL Server SQL Server の](sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md) [URL に関するベストプラクティスとトラブルシューティング](sql-server-backup-to-url-best-practices-and-troubleshooting.md)  
