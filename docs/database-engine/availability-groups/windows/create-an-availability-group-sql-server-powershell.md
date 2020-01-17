---
title: PowerShell による可用性グループの作成
description: PowerShell を使用して Always On 可用性グループを作成する手順です。
ms.custom: seodec18
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], creating
ms.assetid: bc69a7df-20fa-41e1-9301-11317c5270d2
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 9b307c932925331fc28473186f120b2d05cc09c5
ms.sourcegitcommit: 8732161f26a93de3aa1fb13495e8a6a71519c155
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/01/2019
ms.locfileid: "71708413"
---
# <a name="create-an-always-on-availability-group-using-powershell"></a>PowerShell による Always On 可用性グループの作成
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このトピックでは、 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]の Always On 可用性グループを PowerShell コマンドレットで作成および構成する方法について説明します。 *可用性グループ* は、1 つのまとまりとしてフェールオーバーする一連のユーザー データベースと、フェールオーバーをサポートする一連のフェールオーバー パートナー ( *可用性レプリカ*) を定義します。  
  
> [!NOTE]  
> 可用性グループの概要については、「 [Always On 可用性グループの概要 &#40;SQL Server&#41;](~/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)の Always On 可用性グループを PowerShell コマンドレットで作成および構成する方法について説明します。  
  
> [!NOTE]  
> PowerShell のコマンドレットの代わりに、可用性グループの作成ウィザードや [!INCLUDE[tsql](../../../includes/tsql-md.md)]を使用する方法もあります。 詳細については、「[[新しい可用性グループ] ダイアログ ボックスの使用 &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-new-availability-group-dialog-box-sql-server-management-studio.md)」または「[可用性グループの作成 &#40;Transact-SQL&#41;](../../../database-engine/availability-groups/windows/create-an-availability-group-transact-sql.md)」を参照してください。  

## <a name="before-you-begin"></a>はじめに
### <a name="PrerequisitesRestrictions"></a> 前提条件、制限事項、および推奨事項  

- 可用性グループを作成する前に、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の各ホスト インスタンスが、同じ Windows Server Failover Clustering (WSFC) フェールオーバー クラスタリングのそれぞれ異なる WSFC ノードに存在していることを確認します。 また、使用するサーバー インスタンスが、他のサーバー インスタンスの前提条件を満たしていることと、他の [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]の要件がすべて満たされていること、さらに、自分自身も推奨事項を認識していることを確認してください。 詳細については、「[Always On 可用性グループの前提条件、制限事項、および推奨事項 &#40;SQL Server&#41;](~/database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)」を参照することを強くお勧めします。  

### <a name="Permissions"></a> Permissions  
 **sysadmin** 固定サーバー ロールのメンバーシップと、CREATE AVAILABILITY GROUP サーバー権限、ALTER ANY AVAILABILITY GROUP 権限、CONTROL SERVER 権限のいずれかが必要です。  

## <a name="PowerShellProcedure"></a> PowerShell を使用した可用性グループの作成と構成  
 
次の表は、可用性グループの構成に伴う基本的な作業の一覧です。一覧には PowerShell コマンドレットによってサポートされる作業が示されています。 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] に関連したこれらの作業は、この表に示されている順に実行する必要があります。  
  
|タスク|PowerShell コマンドレット (利用可能な場合) または Transact SQL ステートメント|タスクを実行する場所|  
|----------|--------------------------------------------------------------------|---------------------------------|  
|データベース ミラーリング エンドポイントを作成する ( [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスごとに 1 回)|**New-SqlHadrEndPoint**|データベース ミラーリング エンドポイントが欠落している各サーバー インスタンスで実行します。<br /><br />既存のデータベース ミラーリング エンドポイントに変更を加えるには、**Set-SqlHadrEndpoint** を使用します。|  
|可用性グループを作成する|まず、 **New-SqlAvailabilityReplica** コマンドレットに **-AsTemplate** パラメーターを指定し、可用性グループに追加する予定の 2 つの可用性レプリカのそれぞれについて、インメモリの可用性レプリカ オブジェクトを作成します。<br /><br /> 次に、 **New-SqlAvailabilityGroup** コマンドレットを使用し、可用性レプリカ オブジェクトを参照して、可用性グループを作成します。|初期プライマリ レプリカをホストするサーバー インスタンスで実行します。|  
|セカンダリ レプリカを可用性グループに参加させる|**Join-SqlAvailabilityGroup**|セカンダリ レプリカをホストする各サーバー インスタンスで実行します。|  
|セカンダリ データベースを準備する|**Backup-SqlDatabase** と **Restore-SqlDatabase**|プライマリ レプリカをホストするサーバー インスタンスでバックアップを作成します。<br /><br /> セカンダリ レプリカをホストする各サーバー インスタンス上で、 **NoRecovery** 復元パラメーターを使用してバックアップを復元します。 プライマリ レプリカをホストするコンピューターとターゲット セカンダリ レプリカをホストするコンピューターとでファイル パスが異なる場合は、 **RelocateFile** 復元パラメーターも使用します。|  
|各セカンダリ データベースを可用性グループに参加させてデータ同期を開始する|**Add-SqlAvailabilityDatabase**|セカンダリ レプリカをホストする各サーバー インスタンスで実行します。|  
  
> [!NOTE]
> 特定のタスクを実行するには、示されているサーバー インスタンス (1 つまたは複数) にディレクトリを変更します (**cd**)。  

## <a name="using-powershell"></a>PowerShell の使用

[SQL Server PowerShell プロバイダー](../../../relational-databases/scripting/sql-server-powershell-provider.md)を設定して使用します。 

> [!NOTE]  
> 特定のコマンドレットの構文や例を表示するには、 **PowerShell 環境で** Get-Help [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] コマンドレットを使用します。 詳細については、「 [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md)」を参照してください。  

1. プライマリ レプリカをホストするサーバー インスタンスにディレクトリを変更 (**cd**) します。  
  
1. プライマリ レプリカのインメモリの可用性レプリカ オブジェクトを作成します。  
  
1. セカンダリ レプリカごとにインメモリの可用性レプリカ オブジェクトを作成します。  
  
1. 可用性グループを作成します。  
  
    > [!NOTE]  
    > 可用性グループ名の最大文字数は 128 文字です。  

1. 新しいセカンダリ レプリカを、可用性グループに参加させます。[可用性グループへのセカンダリ レプリカの参加 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-replica-to-an-availability-group-sql-server.md) に関する記事を参照してください。  
  
1. 可用性グループ内の各データベースについて、セカンダリ データベースを作成します。これは、プライマリ データベースの最新のバックアップを、RESTORE WITH NORECOVERY で復元することによって行います。  
  
1. すべての新しいセカンダリ データベースを、可用性グループに参加させます。[可用性グループへのセカンダリ レプリカの参加 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-replica-to-an-availability-group-sql-server.md) に関する記事を参照してください。  
  
1. (省略可能) Windows の **dir** コマンドを使用して、新しい可用性グループの内容を確認します。  
  
> [!NOTE]  
> 複数のサーバー インスタンスの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サービス アカウントが、それぞれ異なるドメイン ユーザー アカウントで実行されている場合、それぞれのサーバー インスタンス上に、もう一方のサーバー インスタンス用のログインを作成し、そのログインにローカルのデータベース ミラーリング エンドポイントへの CONNECT 権限を付与します。  

### <a name="ExampleConfigureGroup"></a> 例
以下の PowerShell スクリプトは、2 つの可用性レプリカと 1 つの可用性データベースから成る `<myAvailabilityGroup>` という名前の単純な可用性グループを作成、構成する例です。 この例では、次の処理を実行します。  

1. `<myDatabase>` とそのトランザクション ログをバックアップします。  

1. `<myDatabase>` とそのトランザクション ログを **-NoRecovery** オプションを使用して復元します。  

1. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のローカル インスタンス (名前は `PrimaryComputer\Instance`) によってホストされるプライマリ レプリカのメモリ内表現を作成します。  

1. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンス (名前は `SecondaryComputer\Instance`) によってホストされるセカンダリ レプリカのメモリ内表現を作成します。  

1. `<myAvailabilityGroup>`という名前の可用性グループを作成します。  

1. セカンダリ レプリカを可用性グループに参加させます。  

1. セカンダリ データベースを可用性グループに参加させます。  

```powershell
# Backup my database and its log on the primary  
Backup-SqlDatabase `  
    -Database "<myDatabase>" `  
    -BackupFile "\\share\backups\<myDatabase>.bak" `  
    -ServerInstance "PrimaryComputer\Instance"  
  
Backup-SqlDatabase `  
    -Database "<myDatabase>" `  
    -BackupFile "\\share\backups\<myDatabase>.log" `  
    -ServerInstance "PrimaryComputer\Instance" `  
    -BackupAction Log   
  
# Restore the database and log on the secondary (using NO RECOVERY)  
Restore-SqlDatabase `  
    -Database "<myDatabase>" `  
    -BackupFile "\\share\backups\<myDatabase>.bak" `  
    -ServerInstance "SecondaryComputer\Instance" `  
    -NoRecovery  
  
Restore-SqlDatabase `  
    -Database "<myDatabase>" `  
    -BackupFile "\\share\backups\<myDatabase>.log" `  
    -ServerInstance "SecondaryComputer\Instance" `  
    -RestoreAction Log `  
    -NoRecovery  
  
# Create an in-memory representation of the primary replica.  
$primaryReplica = New-SqlAvailabilityReplica `  
    -Name "PrimaryComputer\Instance" `  
    -EndpointURL "TCP://PrimaryComputer.domain.com:5022" `  
    -AvailabilityMode "SynchronousCommit" `  
    -FailoverMode "Automatic" `  
    -Version 12 `  
    -AsTemplate  
  
# Create an in-memory representation of the secondary replica.  
$secondaryReplica = New-SqlAvailabilityReplica `  
    -Name "SecondaryComputer\Instance" `  
    -EndpointURL "TCP://SecondaryComputer.domain.com:5022" `  
    -AvailabilityMode "SynchronousCommit" `  
    -FailoverMode "Automatic" `  
    -Version 12 `  
    -AsTemplate  
  
# Create the availability group  
New-SqlAvailabilityGroup `  
    -Name "<myAvailabilityGroup>" `  
    -Path "SQLSERVER:\SQL\PrimaryComputer\Instance" `  
    -AvailabilityReplica @($primaryReplica,$secondaryReplica) `  
    -Database "<myDatabase>"  
  
# Join the secondary replica to the availability group.  
Join-SqlAvailabilityGroup -Path "SQLSERVER:\SQL\SecondaryComputer\Instance" -Name "<myAvailabilityGroup>"  
  
# Join the secondary database to the availability group.  
Add-SqlAvailabilityDatabase -Path "SQLSERVER:\SQL\SecondaryComputer\Instance\AvailabilityGroups\<myAvailabilityGroup>" -Database "<myDatabase>"  
```  
  
## <a name="RelatedTasks"></a> 関連タスク  
 **Always On 可用性グループのサーバー インスタンスを構成するには**  
  
- [Always On 可用性グループの有効化と無効化 &#40;SQL Server&#41;](~/database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md)  
  
- [AlwaysOn 可用性グループのデータベース ミラーリング エンドポイントの作成 &#40;SQL Server PowerShell&#41;](~/database-engine/availability-groups/windows/database-mirroring-always-on-availability-groups-powershell.md)  
  
 **可用性グループおよびレプリカのプロパティを構成するには**  
  
- [可用性レプリカの可用性モードの変更 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/change-the-availability-mode-of-an-availability-replica-sql-server.md)  
  
- [可用性レプリカのフェールオーバー モードの変更 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/change-the-failover-mode-of-an-availability-replica-sql-server.md)  
  
- [可用性グループ リスナーの作成または構成 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)  
  
- [自動フェールオーバーの条件を制御する柔軟なフェールオーバー ポリシーの構成 &#40;Always On 可用性グループ&#41;](~/database-engine/availability-groups/windows/configure-flexible-automatic-failover-policy.md)  
  
- [可用性レプリカを追加または変更する場合のエンドポイント URL の指定 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/specify-endpoint-url-adding-or-modifying-availability-replica.md)  
  
- [可用性レプリカでのバックアップの構成 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-backup-on-availability-replicas-sql-server.md)  
  
- [可用性レプリカでの読み取り専用アクセスの構成 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-access-on-an-availability-replica-sql-server.md)  
  
- [可用性グループの読み取り専用ルーティングの構成 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md)  
  
- [可用性レプリカのセッション タイムアウト期間の変更 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/change-the-session-timeout-period-for-an-availability-replica-sql-server.md)  
  
 **可用性グループの構成を完了するには**  
  
- [可用性グループへのセカンダリ レプリカの参加 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
- [可用性グループに対するセカンダリ データベースの手動準備 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)  
  
- [可用性グループへのセカンダリ データベースの参加 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-database-to-an-availability-group-sql-server.md)  
  
- [可用性グループ リスナーの作成または構成 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)  
  
 **別の方法で可用性グループを作成する**  
  
- [可用性グループ ウィザードの使用 &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio.md)  
  
- [[新しい可用性グループ] ダイアログ ボックスの使用 &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
- [可用性グループの作成 &#40;Transact-SQL&#41;](../../../database-engine/availability-groups/windows/create-an-availability-group-transact-sql.md)  
  
 **Always On 可用性グループの構成のトラブルシューティング方法**  
  
- [Always On 可用性グループの構成のトラブルシューティング &#40;SQL Server&#41;](~/database-engine/availability-groups/windows/troubleshoot-always-on-availability-groups-configuration-sql-server.md)  
  
- [失敗したファイルの追加操作のトラブルシューティング &#40;AlwaysOn 可用性グループ&#41;](~/database-engine/availability-groups/windows/troubleshoot-a-failed-add-file-operation-always-on-availability-groups.md)  
  
## <a name="RelatedContent"></a> 関連コンテンツ  
  
- **ブログ:**  
  
     [Always On - HADRON 学習シリーズ:HADRON 対応データベースでのワーカー プールの使用](https://blogs.msdn.com/b/psssql/archive/2012/05/17/Always%20On-hadron-learning-series-worker-pool-usage-for-hadron-enabled-databases.aspx)  
  
     [SQL Server PowerShell を使用した Always On の構成](https://blogs.msdn.microsoft.com/sqlalwayson/2012/02/03/configuring-alwayson-with-sql-server-powershell/)  
  
     [SQL Server Always On チーム ブログ:SQL Server Always On チームのオフィシャル ブログ](https://blogs.msdn.microsoft.com/sqlalwayson/)  
  
     [CSS SQL Server エンジニアのブログ](https://blogs.msdn.com/b/psssql/)  
  
- **ビデオ:**  
  
     [Microsoft SQL Server コードネーム "Denali" Always On シリーズ パート 1: 次世代高可用性ソリューションの概要](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI302)  
  
     [Microsoft SQL Server コードネーム "Denali" Always On シリーズ パート 2: Always On を使用したミッション クリティカルな高可用性ソリューションの構築](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI404)  
  
- **ホワイト ペーパー:**  
  
     [高可用性と災害復旧のための Microsoft SQL Server AlwaysOn ソリューション ガイド](https://go.microsoft.com/fwlink/?LinkId=227600)  
  
     [SQL Server 2012 に関する Microsoft ホワイト ペーパー](https://msdn.microsoft.com/library/hh403491.aspx)  
  
     [SQL Server ユーザー諮問チームのホワイト ペーパー](https://techcommunity.microsoft.com/t5/DataCAT/bg-p/DataCAT/)  
  
## <a name="see-also"></a>参照  
 [データベース ミラーリング エンドポイント &#40;SQL Server&#41;](../../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)   
 [Always On 可用性グループの概要 &#40;SQL Server&#41;](~/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)
