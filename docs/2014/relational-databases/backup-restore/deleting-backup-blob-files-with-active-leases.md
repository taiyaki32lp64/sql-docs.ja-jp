---
title: アクティブなリースを保持しているバックアップ BLOB ファイルの削除 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: 13a8f879-274f-4934-a722-b4677fc9a782
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 663bab775aff9a04a4a9d93f2bcbd0e193b18f37
ms.sourcegitcommit: a165052c789a327a3a7202872669ce039bd9e495
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72783062"
---
# <a name="deleting-backup-blob-files-with-active-leases"></a>アクティブなリースを保持しているバックアップ BLOB ファイルの削除
  Azure storage との間でバックアップまたは復元を行う場合、SQL Server は blob への排他アクセスをロックするために無限リースを取得します。 バックアップまたは復元プロセスが正常に完了すると、リースは解放されます。 バックアップまたは復元に失敗すると、バックアップ プロセスは無効な BLOB のクリーンアップを試みます。 ただし、バックアップの失敗の原因が長期的または持続的なネットワーク接続エラーの場合は、バックアップ プロセスは BLOB にアクセスできず、BLOB は孤立したままになる可能性があります。 つまり、リースが解放されるまで、BLOB を書き込むことも削除することもできません。 このトピックでは、リースを解放する方法と BLOB の削除について説明します。  
  
 リースの種類の詳細については、こちらの [記事](https://go.microsoft.com/fwlink/?LinkId=275664)をご覧ください。  
  
 バックアップ操作が失敗すると、無効なバックアップ ファイルが生成されます。  また、バックアップ BLOB ファイルでは、削除や上書きを防ぐためにアクティブなリースを保持する場合もあります。  BLOB を削除または上書きするには、最初にリースを終了する必要があります。バックアップ障害が発生した場合は、リースをクリーンアップして BLOB を削除することをお勧めします。 また、ストレージ管理タスクの一部としてクリーンアップを定期的に選択することもできます。  
  
 復元エラーが発生した場合、後続の復元はブロックされないため、アクティブなリースは問題にならないことがあります。 リースを終了する必要があるのは、BLOB を上書きまたは削除する場合だけです。  
  
## <a name="managing-orphaned-blobs"></a>孤立した BLOB の管理  
 次の手順では、バックアップ動作または復元動作の失敗後にクリーンアップする方法について説明します。 すべての手順は、PowerShell スクリプトを使用して実行することもできます。 コード例については、次のセクションに示します。  
  
1.  **リースを保持している BLOB の識別:** バックアップ プロセスを実行するスクリプトまたはプロセスがあると、スクリプトまたはプロセス内のエラーをキャプチャし、それを使用して BLOB をクリーンアップできる場合があります。   また、LeaseStats プロパティと LeastState プロパティを使用して、それらのプロパティに対してリースを保持している BLOB を識別することもできます。 BLOB を識別したら、一覧を確認し、BLOB を削除する前にバックアップ ファイルが有効かどうかを確認することをお勧めします。  
  
2.  **リースの終了:** 承認された要求では、リース ID を指定せずにリースを終了できます。 詳細については、 [こちら](https://go.microsoft.com/fwlink/?LinkID=275664) をご覧ください。  
  
    > [!TIP]  
    >  SQL Server は、復元操作中にリース ID を発行して排他アクセスを確立します。 復元のリース ID は BAC2BAC2BAC2BAC2BAC2BAC2BAC2BAC2 です。  
  
3.  **BLOB の削除:** アクティブなリースを保持している BLOB を削除するには、最初にリースを終了する必要があります。  
  
###  <a name="Code_Example"></a> PowerShell スクリプトの例  
 **\* \* 重要な \* \*** PowerShell 2.0 を実行している場合は、Microsoft Windowsazure.servicebus アセンブリの読み込みで問題が発生する可能性があります。 この問題を解決するには、PowerShell 3.0 にアップグレードすることをお勧めします。 また、PowerShell 2.0 では次の回避策を使用することもできます。  
  
-   次のスクリプトを使用して実行時に .NET 2.0 アセンブリと .NET 4.0 アセンブリを読み込むように powershell.exe.config ファイルを作成または変更する:  
  
    ```xml
    <?xml version="1.0"?>
    <configuration>
        <startup useLegacyV2RuntimeActivationPolicy="true">
            <supportedRuntime version="v4.0.30319"/>
            <supportedRuntime version="v2.0.50727"/>
        </startup>
    </configuration>
    ```  
  
 次の例は、アクティブなリースを保持している BLOB を識別してから、アクティブなリースを終了する方法を示しています。 この例は、リリースのリース ID をフィルター選択する方法も示します。  
  
 このスクリプトの実行に関するヒント  
  
> [!WARNING]  
>  Azure Blob ストレージサービスへのバックアップがこのスクリプトと同時に実行されている場合、バックアップは失敗する可能性があります。これは、このスクリプトによって、バックアップが同時に取得しようとしているリースが解除されるためです。 このスクリプトは、保守期間中またはバックアップの実行が予期されていないときに実行することをお勧めします。  
  
1.  このスクリプトを実行すると、ストレージアカウント、ストレージキー、コンテナー、Azure ストレージアセンブリのパスと名前のパラメーターの値を入力するように求められます。 ストレージ アセンブリのパスは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インスタンスのインストール ディレクトリです。 ストレージ アセンブリのファイル名は Microsoft.WindowsAzure.Storage.dll です。 次に、入力するプロンプトと値の例を示します。  
  
    ```  
    cmdlet  at command pipeline position 1  
    Supply values for the following parameters:  
    storageAccount: mycloudstorageaccount  
    storageKey: 0BopKY7eEha3gBnistYk+904nf  
    blobContainer: mycontainer   
    storageAssemblyPath: C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Binn\Microsoft.WindowsAzure.Storage.dll  
    ```  
  
2.  リースがロックされている BLOB がない場合は、次のメッセージが表示されます。  
  
     **ロックされたリースの状態の BLOB はありません**  
  
     リースがロックされている BLOB がある場合は、次のメッセージが表示されます。  
  
     **リースを終了しています**  
  
     **\<BLOB の URL> のリースは復元リースです。このメッセージが表示されるのは、まだアクティブな復元リースを保持している BLOB がある場合のみです。**  
  
     **\<BLOB の URL> のリースは復元リースではありません。\<BLOB の URL>** のリースを終了しています。  
  
```powershell
param(  
       [Parameter(Mandatory=$true)]  
       [string]$storageAccount,  
       [Parameter(Mandatory=$true)]  
       [string]$storageKey,  
       [Parameter(Mandatory=$true)]  
       [string]$blobContainer,  
       [Parameter(Mandatory=$true)]  
       [string]$storageAssemblyPath  
)  
  
# Well known Restore Lease ID  
$restoreLeaseId = "BAC2BAC2BAC2BAC2BAC2BAC2BAC2BAC2"  
  
# Load the storage assembly without locking the file for the duration of the PowerShell session  
$bytes = [System.IO.File]::ReadAllBytes($storageAssemblyPath)  
[System.Reflection.Assembly]::Load($bytes)  
  
$cred = New-Object 'Microsoft.WindowsAzure.Storage.Auth.StorageCredentials' $storageAccount, $storageKey  
$client = New-Object 'Microsoft.WindowsAzure.Storage.Blob.CloudBlobClient' "https://$storageAccount.blob.core.windows.net", $cred  
$container = $client.GetContainerReference($blobContainer)  
  
#list all the blobs  
$allBlobs = $container.ListBlobs()
  
$lockedBlobs = @()  
# filter blobs that are have Lease Status as "locked"  
foreach($blob in $allBlobs)  
{  
    $blobProperties = $blob.Properties
    if($blobProperties.LeaseStatus -eq "Locked")  
    {  
        $lockedBlobs += $blob  
    }  
}  
  
if ($lockedBlobs.Count -eq 0)  
{
    Write-Host " There are no blobs with locked lease status"  
}

if($lockedBlobs.Count -gt 0)  
{  
    Write-Host "Breaking leases"  
    foreach($blob in $lockedBlobs )
    {  
        try  
        {  
            $blob.AcquireLease($null, $restoreLeaseId, $null, $null, $null)  
            Write-Host "The lease on $($blob.Uri) is a restore lease"  
        }  
        catch [Microsoft.WindowsAzure.Storage.StorageException]  
        {  
            if($_.Exception.RequestInformation.HttpStatusCode -eq 409)  
            {  
                Write-Host "The lease on $($blob.Uri) is not a restore lease"  
            }  
        }  
  
        Write-Host "Breaking lease on $($blob.Uri)"  
        $blob.BreakLease($(New-TimeSpan), $null, $null, $null) | Out-Null  
    }  
}
```  
  
## <a name="see-also"></a>「  
 [SQL Server Backup to URL Best Practices and Troubleshooting (SQL Server Backup to URL に関するベスト プラクティスとトラブルシューティング)](sql-server-backup-to-url-best-practices-and-troubleshooting.md)  
