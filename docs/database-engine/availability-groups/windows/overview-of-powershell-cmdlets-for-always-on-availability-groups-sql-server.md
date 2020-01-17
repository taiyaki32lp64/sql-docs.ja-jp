---
title: 可用性グループの PowerShell コマンドレット
description: 'Always On 可用性グループの管理に利用できるさまざまな PowerShell コマンドレットの参照。 '
ms.custom: seo-lt-2019
ms.date: 08/30/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], PowerShell cmdlets
- Availability Groups [SQL Server], about
- PowerShell [SQL Server], cmdlets
ms.assetid: b3fef0d5-b6d7-4386-a0f0-d06c165ad4de
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 8aac669c8e7b2f43666a43c26a8040c3658c560c
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75236092"
---
# <a name="overview-of-powershell-cmdlets-for-always-on-availability-groups"></a>Always On 可用性グループの PowerShell コマンドレットの概要
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] PowerShell は、特にシステム管理用に設計されている、タスク ベースのコマンド ライン シェルとスクリプト言語です。 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] は、 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] で一連の PowerShell コマンドレットを提供しており、それらを使用すると可用性グループ、可用性レプリカ、および可用性データベースの配置、管理、および監視ができます。  
  
> [!NOTE]  
>  PowerShell コマンドレットは、アクションを正常に開始した時点で完了できます。 つまり、目的の操作 (可用性グループのフェールオーバーなど) の完了を示すわけではありません。 一連の操作をスクリプト化している場合は、アクションの状態を確認し、完了するまで待機しなければならないことがあります。  
  
> [!NOTE]  
>  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]のタスクを実行するコマンドレットの使用方法を説明している [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] オンライン ブックのトピックの一覧については、「[Always On 可用性グループ &#40;SQL Server&#41 の概要](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)」の「関連タスク」を参照してください。  
  
##  <a name="ConfiguringServerInstance"></a> Always On 可用性グループのサーバー インスタンスの構成  
  
|コマンドレット|[説明]|サポート対象|  
|-------------|-----------------|------------------|
|[**Disable-SqlAlwaysOn**](/powershell/module/sqlserver/disable-sqlalwayson)|サーバー インスタンス上の [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 機能を無効にします。|**Path**、 **InputObject**、または **Name** パラメーターによって指定されるサーバー インスタンス。 ( [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] をサポートしている [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]のエディションである必要があります)。|  
|[**Enable-SqlAlwaysOn**](/powershell/module/sqlserver/enable-sqlalwayson)|[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 機能をサポートしている [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] のインスタンス上で [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] を有効化します。 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] のサポートの詳細については、「[Always On 可用性グループの前提条件、制限事項、および推奨事項 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)」を参照してください。|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] をサポートしている [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]の任意のエディション。|  
|[**New-SqlHadrEndPoint**](/powershell/module/sqlserver/new-sqlhadrendpoint)|サーバー インスタンス上に新しいデータベース ミラーリング エンドポイントを作成します。 このエンドポイントは、プライマリ データベースとセカンダリ データベース間のデータ移動のために必要です。|の任意のインスタンス [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]|  
|[**Set-SqlHadrEndpoint**](/powershell/module/sqlserver/set-sqlhadrendpoint)|既存のデータベース ミラーリング エンドポイントの名前、状態、認証などのプロパティを変更します。|[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] をサポートしていて、データベース ミラーリング エンドポイントが存在しないサーバー インスタンス。|  

  
##  <a name="BnRcmdlets"></a> バックアップおよびデータベースとトランザクション ログを復元します。  
  
|コマンドレット|[説明]|サポート対象|  
|-------------|-----------------|------------------|  
|[**Backup-SqlDatabase**](/powershell/module/sqlserver/backup-sqldatabase)|データまたはログ バックアップを作成します。|任意のオンライン データベース ( [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]の場合、プライマリ レプリカをホストしているサーバー インスタンス上のデータベース)|  
|[**Restore-SqlDatabase**](/powershell/module/sqlserver/restore-sqldatabase)|バックアップを復元します。|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の任意のインスタンス ( [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]の場合、セカンダリ レプリカをホストしているサーバー インスタンス)<br /><br />

  >[!Important]
  >セカンダリ データベースを準備している場合は、すべての **Restore-SqlDatabase** コマンドで **-NoRecovery** パラメーターを使用する必要があります。 
  
 これらのコマンドレッドを使用してセカンダリ データベースを準備する方法の詳細については、「[可用性グループに対するセカンダリ データベースの手動準備 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)」を参照してください。  
  
##  <a name="DeployManageAGs"></a> 作成して、可用性グループの管理  
  
|コマンドレット|[説明]|サポート対象|  
|-------------|-----------------|------------------|  
|[**New-SqlAvailabilityGroup**](/powershell/module/sqlserver/new-sqlavailabilitygroup)|新しい可用性グループを作成します。|プライマリ レプリカをホストするサーバー インスタンス|  
|[**Remove-SqlAvailabilityGroup**](/powershell/module/sqlserver/remove-sqlavailabilitygroup)|可用性グループを削除します。|HADR 対応のサーバー インスタンス|  
|[**Set-SqlAvailabilityGroup**](/powershell/module/sqlserver/set-sqlavailabilitygroup)|可用性グループのプロパティを設定します。可用性グループをオンライン/オフラインにします。|プライマリ レプリカをホストするサーバー インスタンス|  
|[**Switch-SqlAvailabilityGroup**](/powershell/module/sqlserver/switch-sqlavailabilitygroup)|以下のいずれかの形式のフェールオーバーを開始します。<br /><br /> 可用性グループの強制フェールオーバー (データ損失の可能性あり)。<br /><br /> 可用性グループの手動フェールオーバー。|対象のセカンダリ レプリカをホストするサーバー インスタンス|  
  
##  <a name="AGlisteners"></a> 作成して、可用性グループ リスナーの管理  
  
|コマンドレット|[説明]|サポート対象|  
|------------|-----------------|------------------|  
|[**New-SqlAvailabilityGroupListener**](/powershell/module/sqlserver/new-sqlavailabilitygrouplistener)|新しい可用性グループ リスナーを作成して、既存の可用性グループにアタッチします。|プライマリ レプリカをホストするサーバー インスタンス|  
|[**Set-SqlAvailabilityGroupListener**](/powershell/module/sqlserver/set-sqlavailabilitygrouplistener)|既存の可用性グループ リスナーのポート設定を変更します。|プライマリ レプリカをホストするサーバー インスタンス|  
|[**Add-SqlAvailabilityGroupListenerStaticIp**](/powershell/module/sqlserver/add-sqlavailabilitygrouplistenerstaticip)|既存の可用性グループ リスナー構成に静的 IP アドレスを追加します。 IP アドレスには、サブネットを含む IPv4 アドレス、または IPv6 アドレスを指定できます。|プライマリ レプリカをホストするサーバー インスタンス|  
  
##  <a name="DeployManageARs"></a> 作成して、可用性レプリカの管理  
  
|コマンドレット|[説明]|サポート対象|  
|-------------|-----------------|------------------|  
|[**New-SqlAvailabilityReplica**](/powershell/module/sqlserver/new-sqlavailabilityreplica)|新しい可用性レプリカを作成します。 **-AsTemplate** パラメーターを使用すると、新しい可用性レプリカごとにインメモリの可用性レプリカ オブジェクトを作成できます。|プライマリ レプリカをホストするサーバー インスタンス|  
|[**Join-SqlAvailabilityGroup**](/powershell/module/sqlserver/join-sqlavailabilitygroup)|セカンダリ レプリカを可用性グループに参加させます。|セカンダリ レプリカをホストするサーバー インスタンス|  
|[**Remove-SqlAvailabilityReplica**](/powershell/module/sqlserver/remove-sqlavailabilityreplica)|可用性レプリカを削除します。|プライマリ レプリカをホストするサーバー インスタンス|  
|[**Set-SqlAvailabilityReplica**](/powershell/module/sqlserver/set-sqlavailabilityreplica)|可用性レプリカのプロパティを設定します。|プライマリ レプリカをホストするサーバー インスタンス|  
  
##  <a name="DeployManageDbs"></a> 追加して、可用性データベースの管理  
  
|コマンドレット|[説明]|サポート対象|  
|-------------|-----------------|------------------|  
|[**Add-SqlAvailabilityDatabase**](/powershell/module/sqlserver/add-sqlavailabilitydatabase)|プライマリ レプリカ上で、データベースを可用性グループに追加します。<br /><br /> セカンダリ レプリカ上で、セカンダリ データベースを可用性グループに参加させます。|可用性レプリカをホストする任意のサーバー インスタンス (レプリカがプライマリかセカンダリかで動作が異なります)|  
|[**Remove-SqlAvailabilityDatabase**](/powershell/module/sqlserver/remove-sqlavailabilitydatabase)|プライマリ レプリカ上で、可用性グループからデータベースを削除します。<br /><br /> セカンダリ レプリカ上で、ローカル セカンダリ データベースをローカル セカンダリ レプリカから削除します。|可用性レプリカをホストする任意のサーバー インスタンス (レプリカがプライマリかセカンダリかで動作が異なります)|  
|[**Resume-SqlAvailabilityDatabase**](/powershell/module/sqlserver/resume-sqlavailabilitydatabase)|中断されている可用性データベースのデータ移動を再開します。|データベースが中断されたサーバー インスタンス|  
|[**Suspend-SqlAvailabilityDatabase**](/powershell/module/sqlserver/suspend-sqlavailabilitydatabase)|可用性データベースのデータ移動を中断します。|可用性レプリカをホストする任意のサーバー インスタンス|  
  
##  <a name="MonitorTblshtAGs"></a> 可用性グループの正常性の監視  
 以下の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] コマンドレットを使用すると、可用性グループとそのレプリカおよびデータベースの正常性を監視できます。  
  
> [!IMPORTANT]  
>  これらのコマンドレットを実行するには、CONNECT、VIEW SERVER STATE、および VIEW ANY DEFINITION 権限が必要です。  
  
|コマンドレット|[説明]|サポート対象|  
|------------|-----------------|------------------|  
|[**Test-SqlAvailabilityGroup**](/powershell/module/sqlserver/test-sqlavailabilitygroup)|SQL Server のポリシー ベースの管理 (PBM) のポリシーを評価することによって、可用性グループの正常性を査定します。|可用性レプリカをホストする任意のサーバー インスタンス。*|  
|[**Test-SqlAvailabilityReplica**](/powershell/module/sqlserver/test-sqlavailabilityreplica)|SQL Server のポリシー ベースの管理 (PBM) のポリシーを評価することによって、可用性レプリカの正常性を査定します。|可用性レプリカをホストする任意のサーバー インスタンス。*|  
|[**Test-SqlDatabaseReplicaState**](/powershell/module/sqlserver/test-sqldatabasereplicastate)|SQL Server のポリシー ベースの管理 (PBM) のポリシーを評価することによって、参加しているすべての可用性レプリカ上の可用性データベースの正常性を査定します。|可用性レプリカをホストする任意のサーバー インスタンス。*|  
  
 \* 可用性グループ内のすべての可用性レプリカについての情報を表示するには、プライマリ レプリカをホストするサーバー インスタンスを使用してください。  
  
 詳細については、「[Always On ポリシーを使用した可用性グループの正常性の確認 &#40;SQL Server&#41](../../../database-engine/availability-groups/windows/use-always-on-policies-to-view-the-health-of-an-availability-group-sql-server.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [AlwaysOn 可用性グループの概要 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md)  
  
  
