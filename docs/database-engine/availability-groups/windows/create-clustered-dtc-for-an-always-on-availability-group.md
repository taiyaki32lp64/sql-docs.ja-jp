---
title: 可用性グループ用のクラスター化された DTC リソースを作成する
description: このトピックでは、SQL Server の AlwaysOn 可用性グループのためにクラスター化された DTC を完全に構成する方法について説明します。
ms.custom: seodec18
ms.date: 08/30/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: 0e332aa4-2c48-4bc4-a404-b65735a02cea
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 96c706d58e0f90f4f10b89a724f7d87fa94e41f3
ms.sourcegitcommit: ac90f8510c1dd38d3a44a45a55d0b0449c2405f5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72586765"
---
# <a name="create-clustered-dtc-resource-for-an-always-on-availability-group"></a>Always On 可用性グループ用のクラスター化された DTC リソースを作成する

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

このトピックでは、SQL Server の AlwaysOn 可用性グループのためにクラスター化された DTC を完全に構成する方法について説明します。 完全構成の完了には最大 1 時間かかることがあります。 

このチュートリアルでは、クラスター化された DTC リソースと SQL Server 可用性グループを「[Cluster MSDTC for SQL Server Availability Groups](../../../database-engine/availability-groups/windows/cluster-dtc-for-sql-server-2016-availability-groups.md)」(SQL Server 可用性グループの DTC をクラスター化する) の要件に基づいて作成します。

このチュートリアルでは、PowerShell スクリプトと Transact-SQL (T-SQL) スクリプトが使用されます。  T-SQL スクリプトの多くで **SQLCMD モード** を有効にする必要があります。  **SQLCMD モード**に関する情報については、「 [クエリ エディターで SQLCMD スクリプト操作を有効にする方法](../../../relational-databases/scripting/edit-sqlcmd-scripts-with-query-editor.md)」を参照してください。  PowerShell モジュール **FailoverClusters** をインポートする必要があります。  PowerShell モジュールのインポートに関する詳細については、[PowerShell モジュールのインポート](/powershell/scripting/developer/module/importing-a-powershell-module)に関する記事を参照してください。  このチュートリアルは以下を前提条件とします。
- 「[Always On 可用性グループの前提条件、制限事項、推奨事項 (SQL Server)](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)」の要件をすべて満たしています。  
- ドメインが `contoso.lab`です。
- DTC ネットワーク名リソースが作成される OU でコンピューター オブジェクトを作成する権限がユーザーに与えられています。
- ユーザーがクラスターのあらゆるノードに対して管理者権限が与えられているドメイン ユーザーです。
- `sqlbackups` という名前のファイル共有がバックアップのために作成されています。
- SQL Server の既定のインスタンスが名前付きの `SQLNODE1` と `SQLNODE2`です。
- SQL Server のすべてのインスタンスで同じサービス アカウントが使用されています。
- SQL Server のすべてのインスタンスで、ユーザーが固定の SQL Server ロール sysadmin のメンバーです。
- DTC が解決できないトランザクションの既定の結果が `presume commit`に設定されます。
- ミラーリング エンドポイントでポート `5022`が使用されます。
- 可用性グループやクラスター化された DTC リソースが他に存在しません。
- クラスターの詳細 (既存):
  - 名前: `Cluster`
  - ネットワーク名: `Cluster Network 1`
  - ノード: `SQLNODE1, SQLNODE2`
  - 共有ストレージ:`Cluster Disk 3` (`SQLNODE1` が所有)
- クラスター詳細 (作成予定):
  - ネットワーク名リソース: `DTCnet1`
  - DTC ネットワーク名リソース: `DTC1`
  - DTC 物理ディスク リソース: `DTCDisk1`
  - DTC IP とサブネット リソース: `192.168.2.54`、`255.255.255.0`
  - DTC IP リソース: `DTCIP1`

## <a name="1-check-operating-system"></a>1.オペレーティング システムを確認する
サポートされている分散トランザクションについては、Windows Server 2016 または Windows Server 2012 R2 で [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] を実行する必要があります。  Windows Server 2012 R2 の場合は、[https://support.microsoft.com/kb/3090973](https://support.microsoft.com/kb/3090973) で入手できる KB3090973 の更新プログラムをインストールする必要があります。  このスクリプトはオペレーティング システムのバージョンを確認し、修正プログラム 3090973 をインストールする必要があるかどうかを判断します。  `SQLNODE1` で次の PowerShell スクリプトを実行します。

```powershell  
# A few OS checks

\<#
Script: 
    1) is re-runnable 
    2) will work on any node in the cluster, and 
    3) will execute against every node in the cluster
#>

$nodes = (Get-ClusterNode).Name;
foreach ($node in $nodes) {

    # At least 2012 R2
    $os = (Get-WmiObject -class Win32_OperatingSystem -ComputerName $node).caption;
    IF($os -like "*2012 R2*" -or $os -like "*2016*")
    {
        Write-Host "$os is supported on $node.";
    }
    ELSE
    {
        Write-Host "STOP!  $os is not supported on $node.";
    }
    
    # KB 3090973
    IF($os -like "*2012 R2*")
    {
        $kb = Get-Hotfix -ComputerName $node | Where {$_.HotFixID -eq 'KB3090973'};
        IF($kb)
        {
            Write-Host "KB3090973 is installed on $node."
        }
        ELSE
        {
            Write-Host "HotFixID KB3090973 must be applied on $node.  See https://support.microsoft.com/kb/3090973 for additional information and to download the hotfix.";
        }
    }
    ELSE
    {
        Write-Host "KB3090973 is not applicable to $os on $node."
    }
}
```  
## <a name="2---configure-firewall-rules"></a>2. ファイアウォール規則を構成する
分散トランザクションに関与している他のサーバーと同様に、可用性グループのレプリカをホストしている各 SQL Server で DTC トラフィックを許可するようにこのスクリプトはファイアウォールを構成します。  また、データベース ミラーリング エンドポイントの接続を許可するようにファイアウォールを構成します。  `SQLNODE1` で次の PowerShell スクリプトを実行します。

```powershell  
# Configure Firewall

\<#
Script: 
    1) is re-runnable 
    2) will work on any node in the cluster, and 
    3) will execute against every node in the cluster
#>

$nodes = (Get-ClusterNode).Name;
foreach ($node in $nodes) {
    Get-NetFirewallRule -CimSession $node -DisplayGroup 'Distributed Transaction Coordinator' -Enabled False -ErrorAction SilentlyContinue | Enable-NetFirewallRule;
    New-NetFirewallRule -CimSession $node -DisplayName 'SQL Server Mirroring' -Description 'Port 5022 for SQL Server Mirroring' -Action Allow -Direction Inbound -Protocol TCP -LocalPort 5022 -RemotePort Any -LocalAddress Any -RemoteAddress Any;
    };
```  
## <a name="3--configure-in-doubt-xact-resolution"></a>3.**in-doubt xact resolution** を構成する 
このスクリプトは、不明なトランザクションに対して "コミットを推測する" ように **in-doubt xact resolution** サーバー構成オプションを構成します。  **SQLCMD モード**で `SQLNODE1` に対して SQL Server Management Studio (SSMS) の次の T-SQL スクリプトを実行します。

```sql  
/*******************************************************************
    Execute script in its entirety on SQLNODE1 in SQLCMD mode
*******************************************************************/

-- Configure in-doubt xact resolution on all SQL Server instances to presume commit
IF (SELECT CAST(value_in_use as bit) FROM sys.configurations WITH (NOLOCK) WHERE [name] = N'show advanced options') = 0
BEGIN   
    EXEC sp_configure 'show advanced options', 1;
    RECONFIGURE;
END

-- Configure the server to presume commit for in-doubt transactions.
IF (SELECT CAST(value as bit) FROM sys.configurations WITH (NOLOCK) WHERE [name] = N'in-doubt xact resolution') <> 1
BEGIN   
    EXEC sp_configure 'in-doubt xact resolution', 1;
    RECONFIGURE;
END
GO
-----------------------------------------------------------------------------

:connect SQLNODE2
IF (SELECT CAST(value_in_use as bit) FROM sys.configurations WITH (NOLOCK) WHERE [name] = N'show advanced options') = 0
BEGIN   
    EXEC sp_configure 'show advanced options', 1;
    RECONFIGURE;
END

-- Configure the server to presume commit for in-doubt transactions.
IF (SELECT CAST(value as bit) FROM sys.configurations WITH (NOLOCK) WHERE [name] = N'in-doubt xact resolution') <> 1
BEGIN   
    EXEC sp_configure 'in-doubt xact resolution', 1;
    RECONFIGURE;
END
GO
-----------------------------------------------------------------------------
```

## <a name="4-create-test-databases"></a>4.テスト データベースを作成する
このスクリプトは、`SQLNODE1` で `AG1` という名前のデータベースを作成し、`SQLNODE2` で `dtcDemoAG1` という名前のデータベースを作成します。  **SQLCMD モード**で `SQLNODE1` に対して SSMS の次の T-SQL スクリプトを実行します。

```sql  
/*******************************************************************
    Execute script in its entirety on SQLNODE1 in SQLCMD mode
*******************************************************************/

-- On SQLNODE1 
USE master;
SET NOCOUNT ON;

IF  EXISTS (SELECT * FROM sys.databases WHERE name = N'AG1')
BEGIN
    DROP DATABASE AG1;
END
GO

CREATE DATABASE AG1;
ALTER DATABASE AG1 SET RECOVERY FULL WITH NO_WAIT;
ALTER AUTHORIZATION ON DATABASE::AG1 to sa;
GO

USE AG1;
CREATE TABLE [dbo].[Names] (
        [Name] [varchar](64) NULL,
        [EditDate] datetime
        );

INSERT Names
VALUES ('AG1', GETDATE());
GO


-- Against SQNODE2
:connect SQLNODE2
USE master;
SET NOCOUNT ON;

IF  EXISTS (SELECT * FROM sys.databases WHERE name = N'dtcDemoAG1')
BEGIN
    DROP DATABASE dtcDemoAG1;
END
GO

CREATE DATABASE dtcDemoAG1;
ALTER DATABASE dtcDemoAG1 SET RECOVERY SIMPLE WITH NO_WAIT;
ALTER AUTHORIZATION ON DATABASE::dtcDemoAG1 to sa;
GO

USE dtcDemoAG1;
CREATE TABLE [dbo].[Names] (
        [Name] [varchar](64) NULL,
        [EditDate] datetime
        );
GO    
----------------------------------------------------------------
```
## <a name="5---create-endpoints"></a>5. エンドポイントを作成する
このスクリプトは、TCP ポート `5022` で待機する `AG1_endpoint` という名前のエンドポイントを作成します。  **SQLCMD モード**で `SQLNODE1` に対して SSMS の次の T-SQL スクリプトを実行します。

```sql  
/**********************************************
Execute on SQLNODE1 in SQLCMD mode
**********************************************/

-- Create endpoint on server instance that hosts the primary replica:
IF NOT EXISTS (SELECT * FROM sys.database_mirroring_endpoints)
BEGIN
    CREATE ENDPOINT AG1_endpoint
    AUTHORIZATION [sa]
        STATE=STARTED 
        AS TCP (LISTENER_PORT=5022) 
        FOR DATABASE_MIRRORING (ROLE=ALL);
END
GO
-----------------------------------------------------------------------------

:connect SQLNODE2
IF NOT EXISTS (SELECT * FROM sys.database_mirroring_endpoints)
BEGIN
    CREATE ENDPOINT AG1_endpoint
    AUTHORIZATION [sa]
        STATE=STARTED 
        AS TCP (LISTENER_PORT=5022) 
        FOR DATABASE_MIRRORING (ROLE=ALL);
END
GO
-----------------------------------------------------------------------------
```

## <a name="6---prepare-databases-for-availability-group"></a>6. 可用性グループに使用するデータベースを準備する
このスクリプトは `SQLNODE1` で `AG1` をバックアップし、`SQLNODE2` に復元します。  **SQLCMD モード**で `SQLNODE1` に対して SSMS の次の T-SQL スクリプトを実行します。

```sql  
/*******************************************************************
    Execute script in its entirety on SQLNODE1 in SQLCMD mode
*******************************************************************/

-- Backup database
BACKUP DATABASE AG1 
TO DISK = N'\\sqlnode1\sqlbackups\AG1.bak' 
WITH FORMAT, STATS = 10;

-- Backup transaction log
BACKUP LOG AG1
TO DISK = N'\\sqlnode1\sqlbackups\AG1_Log.bak'
WITH FORMAT, STATS = 10;
GO


-- Restore database and logs on secondary WITH NORECOVERY
:connect SQLNODE2
USE [master]
RESTORE DATABASE AG1 
FROM DISK = N'\\sqlnode1\sqlbackups\AG1.bak' 
WITH NORECOVERY, STATS = 10;

RESTORE LOG AG1 
FROM DISK = N'\\sqlnode1\sqlbackups\AG1_Log.bak'
WITH NORECOVERY, STATS = 10;
GO
```

## <a name="7---create-availability-group"></a>7. 可用性グループを作成する
[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]は、**CREATE AVAILABILITY GROUP** コマンドと **WITH DTC_SUPPORT = PER_DB** 句を使用して作成する必要があります。  現在、既存の可用性グループを変更することはできません。  新しい可用性グループ ウィザードでは、新しい可用性グループに対して DTC サポートを有効にすることができません。  次のスクリプトは新しい可用性グループを作成し、セカンダリを参加させます。  `SQLNODE1` SQLCMD モード **で**に対して SSMS の次の T-SQL スクリプトを実行します。

```sql  
/*******************************************************************
    Execute script in its entirety on SQLNODE1 in SQLCMD mode
*******************************************************************/

--  Create Availability Group on SQLNODE1 
USE master;
CREATE AVAILABILITY GROUP DTCAG1
WITH (DTC_SUPPORT = PER_DB) 
FOR DATABASE AG1
REPLICA ON 
  'SQLNODE1' WITH
     (
     ENDPOINT_URL = 'TCP://SQLNODE1.contoso.lab:5022', 
     AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
     FAILOVER_MODE = MANUAL
     ),
  'SQLNODE2' WITH 
     (
     ENDPOINT_URL = 'TCP://SQLNODE2.contoso.lab:5022',
     AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
     FAILOVER_MODE = MANUAL
     ); 
GO


-- SQLNODE2
-- Join secondary replica to the Availability Group 
:connect SQLNODE2
ALTER AVAILABILITY GROUP DTCag1 JOIN;

-- Join database to the Availability Group
ALTER DATABASE AG1 SET HADR AVAILABILITY GROUP = DTCAG1;
GO
```

> [!IMPORTANT]
> 既存の [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] で DTC を有効にすることはできません。  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] は、既存の可用性グループに対して次の構文を受け取ります。  
> 
> USE master;    
> ALTER AVAILABILITY GROUP \<availability_group\>  
> SET (DTC_Support = Per_DB)  
> 
> ただし、構成変更は実際には行われません。  次の T-SQL クエリで **dtc_support** 構成を確定できます。  
> 
> SELECT name, dtc_support FROM sys.availability_groups  
> 
> 可用性グループで DTC サポートを有効にする唯一の方法は、Transact-SQL を利用して可用性グループを作成することです。
 
## <a name="ClusterDTC"></a>8.クラスター リソースを準備する

このスクリプトは DTC 依存リソース(ディスクと IP) を準備します。  共有ストレージが Windows クラスターに追加されます。  ネットワーク リソースが作成されます。それから DTC が作成され、可用性グループのリソースとなります。  `SQLNODE1` で次の PowerShell スクリプトを実行します。 [Allan Hirt](https://sqlha.com/2013/03/12/how-to-properly-configure-dtc-for-clustered-instances-of-sql-server-with-windows-server-2008-r2/) さんのスクリプトに感謝します。

```powershell  
# Create a clustered Microsoft Distributed Transaction Coordinator properly in the resource group with SQL Server

\<#----------------------------------- Begin User Input -----------------------------------#>
$AGgrp = "DTCag1";                          # Name of the WSFC resource group that will contain the DTC resource

$WSFC = (Get-Cluster).Name;                 # Windows Failover Cluster name
$DTCnetwk = "Cluster Network 1"             # WSFC Network to use for the DTC IP address

$ClusterAvailableDisk = "Cluster Disk 3";   # Designated disk that can support failover clustering and is visible to all nodes, but not yet part of the set of clustered disks
$DTCdisk = "DTCDisk1";                      # Name of the disk to be used with DTC

$DTCipresnm = "DTCIP1";                     # WSFC Friendly Name of the DTC's IP resource 
$DTCipaddr = "192.168.2.54";                # IP address of the DTC resource 
$DTCsubnet = "255.255.255.0";               # Subnet for the DTC IP address 
$DTCnetnm = "DTCNet1";                      # WSFC Friendly Name of the Network Name resource
$DTCresnm = "DTC1";                         # Name of the WSFC DTC Network Name resource; Name must be unique in AD
\<#------------------------------------ End User Input ------------------------------------#>


# Make a new disk available for use in a failover cluster.
Get-ClusterAvailableDisk | Where {$_.Name -eq $ClusterAvailableDisk} | Add-ClusterDisk;

# Rename disk
$resource = Get-ClusterResource $ClusterAvailableDisk; $resource.Name = $DTCdisk;

# Create the IP resource
Add-ClusterResource -Name $DTCipresnm -ResourceType "IP Address" -Group $AGgrp;

# Set the network to use, IP address, and subnet
# All three have to be configured at the same time
$DTCIPres = Get-ClusterResource $DTCipresnm;
$ntwk = New-Object Microsoft.FailoverClusters.PowerShell.ClusterParameter $DTCipres,Network,$DTCnetwk;
$ipaddr = New-Object Microsoft.FailoverClusters.PowerShell.ClusterParameter $DTCipres,Address,$DTCipaddr;
$subnet = New-Object Microsoft.FailoverClusters.PowerShell.ClusterParameter $DTCipres,SubnetMask,$dtcsubnet;

$setdtcipparams = $ntwk,$ipaddr,$subnet;
$setdtcipparams | Set-ClusterParameter;

# Create the Network Name resource
Add-ClusterResource $DTCnetnm -ResourceType "Network Name" -Group $AGgrp;

# Set the value for the Network Name resource
Get-ClusterResource $DTCnetnm | Set-ClusterParameter DnsName $DTCresnm;

# Add the IP address as a depenency of the Network Name resource
Add-ClusterResourceDependency $DTCnetnm $DTCipresnm;

# Create the Distributed Transaction Coordinator resource
Add-ClusterResource $DTCresnm -ResourceType "Distributed Transaction Coordinator" -Group $AGgrp;

# Add the Network Name as a depenency of the DTC resource
Add-ClusterResourceDependency $DTCresnm $DTCnetnm;

# Move the disk into the resource group with SQL Server
Move-ClusterResource -Name $DTCdisk -Group $AGgrp;

# Add the disk as a depenency of the DTC resource
Add-ClusterResourceDependency $DTCresnm $DTCdisk;

# Bring the IP resource online
Start-ClusterResource $DTCipresnm;

# Bring the Network Name resource online
Start-ClusterResource $DTCnetnm;

# Bring the DTC resource online
Start-ClusterResource $DTCresnm;
```  

## <a name="9---enable-network-dtc"></a>9. ネットワーク DTC を有効にする 

次のスクリプトはクラスター化された DTC サービスに対してネットワーク DTC アクセスを有効にし、リモート コンピューターがネットワーク経由で分散トランザクションに参加できるように許可します。  `SQLNODE1` で次の PowerShell スクリプトを実行します。

```powershell  
# Enable Network DTC access for the clustered DTC service

\<#
Script: 
    1) is re-runnable 
    2) will work on any node in the cluster, and 
    3) will execute against every node in the cluster
#>

# Enter Name of DTC resource

$DtcName = "DTC1";
\<# ------- End of User Input ------- #>

[bool]$restart = 0;
$node = (Get-ClusterResource -Name $DtcName).OwnerNode.Name;
$DtcSettings = Get-DtcNetworkSetting -DtcName $DtcName;

IF ($DtcSettings.InboundTransactionsEnabled -eq $false)   
{
    Set-DtcNetworkSetting -CimSession $node -DtcName $DtcName -AuthenticationLevel "Mutual" -InboundTransactionsEnabled $true -Confirm:$false;
    $restart = 1;
}

IF ($DtcSettings.OutboundTransactionsEnabled -eq $false)   
{
    Set-DtcNetworkSetting -CimSession $node -DtcName $DtcName -AuthenticationLevel "Mutual" -OutboundTransactionsEnabled $true -Confirm:$false;
    $restart = 1;
}

IF ($restart -eq 1)
{
    Stop-Dtc -CimSession $node -DtcName $DTCname -Confirm:$false;
    Start-Dtc -CimSession $node -DtcName $DTCname;
}
```  

## <a name="10--disable-and-stop-the-local-dtc-service-on-each-node"></a>10.各ノードでローカル DTC サービスを無効にして停止する

分散トランザクションがクラスター化された DTC リソースを使用することを保証するには、両方のノードでローカルの DTC を無効にします。  次のスクリプトは、各ノードでローカル DTC サービスを無効にして停止します。  `SQLNODE1` で次の PowerShell スクリプトを実行します。
```powershell  
# Disable local DTC service

\<#
Script: 
    1) is re-runnable 
    2) will work on any node in the cluster, and 
    3) will execute against every node in the cluster
#>

$DTCname = 'Local';
$nodes = (Get-ClusterNode).Name;

 foreach ($node in $nodes) {

    $service = Get-WmiObject -class Win32_Service -computername $node -Filter "Name='MSDTC'";
    IF ($service.StartMode -ne 'Disabled')
    {
        $service.ChangeStartMode('Disabled');
    }
    
    IF ($service.State -ne 'Stopped')
    {
        $service.StopService();
    }
}
```  

## <a name="11--cycle-the-includessnoversionincludesssnoversion-mdmd-service-for-each-instance"></a>11.各インスタンスの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サービスを停止し、すぐに起動する

完全に構成されているクラスター化された DTC サービスでは、この DTC サービスを使用するように [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] が登録されていることを確認するために、可用性グループの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の各インスタンスを停止して再起動する必要があります。

最初の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サービスには、分散トランザクションが必要です。この分散トランザクションは DTC サービスに登録されます。 SQL Server サービスでは、再起動されるまで DTC サービスを使用し続けます。 クラスター化された DTC サービスが利用可能な場合は、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] はクラスター化された DTC サービスに登録されます。 クラスター化された DTC サービスが利用できない場合は、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] はローカル DTC サービスに登録されます。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] がクラスター化された DTC サービスに登録されていることを確認するために、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の各インスタンスを停止して再起動します。 

下の T-SQL スクリプトに含まれている手順に従います。
```sql  
/*
Gracefully cycle the SQL Server service and failover the Availability Group
    a.  On SQLNODE2, cycle the SQL Server service from SQL Server Configuration Manger

    b.  On SQLNODE2 failover the Availability Group to SQLNODE2
        Execute T-SQL script, below, on SQLNODE2 (Use Results to Text)

    c.  On SQLNODE1, cycle the SQL Server service from SQL Server Configuration Manger

    d.  On SQLNODE1 failover the Availability Group to SQLNODE1 once the databases are back in sync.
        Execute T-SQL script, below, on SQLNODE1 (Use Results to Text)
*/

SET NOCOUNT ON;

-- Ensure replica is secondary
IF (
SELECT rs.is_primary_replica 
    FROM sys.availability_groups ag
    JOIN sys.dm_hadr_database_replica_states rs
    ON  ag.group_id = rs.group_id
    WHERE ag.name = N'DTCag1'
    AND rs.is_local = 1) = 0
BEGIN
    -- Wait for SYNCHRONIZED state
    DECLARE @ctr tinyint = 0;
    declare @msg varchar(128);
    WHILE (SELECT synchronization_state 
        FROM sys.availability_groups ag
        JOIN sys.dm_hadr_database_replica_states rs
        ON  ag.group_id = rs.group_id
        WHERE ag.name = N'DTCag1'
        AND rs.is_primary_replica = 0
        AND rs.is_local = 1) <> 2
    BEGIN
        WAITFOR DELAY '00:00:01'
        SET @ctr += 1
        SET @msg = 'Waiting for databases to become synchronized. Duration in seconds: ' + cast(@ctr AS varchar(3))
        RAISERROR (@msg, 0, 1) WITH NOWAIT
    END

    ALTER AVAILABILITY GROUP DTCAG1 FAILOVER;
    SELECT 'Failover complete' AS [Sucess]
END
ELSE BEGIN
    SELECT 'This instance is the primary replica.  Connect to the secondary replica and try again.' AS [Error]
END

```

## <a name="12--test-configuration"></a>12.テスト構成

このテストでは、`SQLNODE1` から `SQLNODE2` へのリンク サーバーを使用して、分散トランザクションを作成します。  可用性グループのプライマリ レプリカが `SQLNODE1`にあることを確認します。 構成をテストする目的で、次の操作を行います。

- リンク サーバーを作成する
- 分散トランザクションを実行する

### <a name="create-linked-servers"></a>リンク サーバーを作成する  
次のスクリプトは、 `SQLNODE1`で 2 つのリンク サーバーを作成します。  `SQLNODE1`に対して SSMS の次の T-SQL スクリプトを実行します。

```sql  
-- SQLNODE1
IF NOT EXISTS (SELECT * FROM sys.servers where name = N'SQLNODE1')
BEGIN
    EXEC master.dbo.sp_addlinkedserver @server = N'SQLNODE1';   
END

IF NOT EXISTS (SELECT * FROM sys.servers where name = N'SQLNODE2')
BEGIN
    EXEC master.dbo.sp_addlinkedserver @server = N'SQLNODE2';   
END
 ```

### <a name="execute-a-distributed-transaction"></a>分散トランザクションを実行する
このスクリプトは最初に、現在の DTC トランザクションの統計を返します。  次に、 `SQLNODE1` と `SQLNODE2`でデータベースを活用して分散トランザクションを実行します。  次に、DTC トランザクションの統計をもう一度返します。このとき、数が増えているはずです。  `SQLNODE1` に物理的に接続し、 `SQLNODE1` SQLCMD モード **で**に対して SSMS の次の T-SQL スクリプトを実行します。

```sql  
/*******************************************************************
    Execute script in its entirety on SQLNODE1 in SQLCMD mode
    Must be physically connected to SQLNODE1
*******************************************************************/

USE AG1;
SET NOCOUNT ON;

-- Get Baseline
!! Powershell; $DtcNameC = Get-DtcClusterDefault; Get-DtcTransactionsStatistics -DtcName $DtcNameC;

SET XACT_ABORT ON
BEGIN DISTRIBUTED TRANSACTION
    INSERT INTO SQLNODE1.[AG1].[dbo].[Names] VALUES ('TestValue1', GETDATE());
    INSERT INTO SQLNODE2.[dtcDemoAG1].[dbo].[Names] VALUES ('TestValue2', GETDATE());
COMMIT TRAN
GO

-- Review DTC Transaction Statistics
!! Powershell; $DtcNameC = Get-DtcClusterDefault; Get-DtcTransactionsStatistics -DtcName $DtcNameC;
```

> [!IMPORTANT]
> `USE AG1` ステートメントを実行し、データベース コンテキストを `AG1`に設定する必要があります。  そうしないと、次のエラー メッセージを受け取ります。"トランザクション コンテキストを他のセッションが使用中です。"
