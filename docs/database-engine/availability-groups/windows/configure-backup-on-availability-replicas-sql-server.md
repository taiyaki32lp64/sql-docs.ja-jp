---
title: 可用性グループのセカンダリ レプリカのバックアップの構成
description: Transact-SQL (T-SQL)、PowerShell、または SQL Server Management Studio のいずれかを使用して Always On 可用性グループのセカンダリ レプリカのバックアップを構成する方法を説明します。
ms.custom: seodec18
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- backup priority
- backup on secondary replicas
- Availability Groups [SQL Server], availability replicas
- Availability Groups [SQL Server], backup on secondary replicas
- active secondary replicas [SQL Server], backup on
- automated backup preference
- Availability Groups [SQL Server], active secondary replicas
ms.assetid: 74bc40bb-9f57-44e4-8988-1d69c0585eb6
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: a2a3258dfa0fbb234cf4f888e4ae98f27c215993
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67988519"
---
# <a name="configure-backups-on-secondary-replicas-of-an-always-on-availability-group"></a>Always On 可用性グループのセカンダリ レプリカのバックアップの構成
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このトピックでは、 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]で [!INCLUDE[tsql](../../../includes/tsql-md.md)]、 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]、または PowerShell を使用して、Always On 可用性グループのセカンダリ レプリカでバックアップを構成する方法について説明します。  
  
> [!NOTE]  
>  セカンダリ レプリカのバックアップの概要については、「[アクティブなセカンダリ:セカンダリ レプリカでのバックアップ &#40;Always On 可用性グループ&#41;](../../../database-engine/availability-groups/windows/active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md)」を参照してください。  
  
##  <a name="Prerequisites"></a> 前提条件  
 プライマリ レプリカをホストするサーバー インスタンスに接続されている必要があります。  
  
  
##  <a name="Permissions"></a> Permissions  
  
|タスク|アクセス許可|  
|----------|-----------------|  
|可用性グループの作成時にセカンダリ レプリカでバックアップを構成するには|**sysadmin** 固定サーバー ロールのメンバーシップと、CREATE AVAILABILITY GROUP サーバー権限、ALTER ANY AVAILABILITY GROUP 権限、CONTROL SERVER 権限のいずれかが必要です。|  
|可用性グループまたは可用性レプリカを変更するには|可用性グループの ALTER AVAILABILITY GROUP 権限、CONTROL AVAILABILITY GROUP 権限、ALTER ANY AVAILABILITY GROUP 権限、または CONTROL SERVER 権限が必要です。|  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
 **セカンダリ レプリカでバックアップを構成するには**  
  
1.  オブジェクト エクスプローラーで、プライマリ レプリカをホストするサーバー インスタンスに接続し、サーバー名をクリックしてサーバー ツリーを展開します。  
  
2.  **[AlwaysOn 高可用性]** ノードと **[可用性グループ]** ノードを展開します。  
  
3.  バックアップ優先設定を構成する可用性グループをクリックし、 **[プロパティ]** をクリックします。  
  
4.  **[可用性グループのプロパティ]** ダイアログ ボックスで、 **[バックアップの設定]** ページをクリックします。  
  
5.  **[バックアップを実行する場所]** パネルで、可用性グループの自動バックアップ設定を選択します。次のいずれかを選択できます。  
  
     **[セカンダリを優先]**  
     オンラインのレプリカがプライマリ レプリカのみである場合を除き、セカンダリ レプリカでバックアップを実行することを指定します。 オンラインのレプリカがプライマリ レプリカのみである場合は、プライマリ レプリカでバックアップを実行する必要があります。 既定のオプションです。  
  
     **[セカンダリのみ]**  
     バックアップをプライマリ レプリカでは実行しないことを指定します。 オンラインのレプリカがプライマリ レプリカだけの場合、バックアップは実行されません。  
  
     **プライマリ**  
     バックアップを常にプライマリ レプリカで実行することを指定します。 このオプションは、差分バックアップの作成など、バックアップがセカンダリ レプリカで実行されたときにはサポートされないバックアップ機能が必要な場合に役に立ちます。  
  
    > [!IMPORTANT]  
    >  ログ配布を使用して可用性グループのセカンダリ データベースを準備する場合は、すべてのセカンダリ データベースの準備が完了し、それらを可用性グループに参加させるまで、自動バックアップ設定を **[プライマリ]** に設定します。  
  
     **[任意のレプリカ]**  
     バックアップを実行するレプリカを選択するときにバックアップ ジョブが可用性レプリカのロールを無視するように指定します。 バックアップ ジョブは、動作状態および接続状態と組み合わせて、各可用性レプリカのバックアップ優先順位などの他の要素を評価する場合があります。  
  
    > [!IMPORTANT]  
    >  自動バックアップ設定の適用はありません。 この優先設定の解釈は、特定の可用性グループのデータベースに対するバックアップ ジョブのスクリプトでのロジックに依存します (ロジックが存在する場合)。 自動バックアップ設定はアドホック バックアップには影響しません。 詳細については、このトピックで後述する「[補足情報:セカンダリ レプリカでバックアップを構成した後](#FollowUp)」を参照してください。  
  
6.  **[レプリカのバックアップの優先順位]** グリッドを使用して、可用性レプリカのバックアップの優先順位を変更します。 このグリッドには、可用性グループのレプリカをホストする各サーバー インスタンスの現在のバックアップの優先順位が表示されます。 グリッドの列は次のとおりです。  
  
     **サーバー インスタンス**  
     可用性レプリカをホストする [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスの名前。  
  
     **[バックアップ優先度 (最小 = 1、最高 = 100)]**  
     同じ可用性グループ内の他のレプリカと比較して、このレプリカでバックアップを実行する優先順位を指定します。 値は 0 ～ 100 の範囲の整数です。 1 は最も低い優先順位を示し、100 は最も高い優先順位を示します。 たとえば、 **Backup Priority** = 1 の場合、現在使用可能な可用性レプリカにそれより高い優先順位のものがない場合にのみ、その可用性レプリカがバックアップの実行に対して選択されます。  
  
     **[レプリカの除外]**  
     バックアップの実行時にこの可用性レプリカを選択しない場合に選択します。 これは、たとえば、バックアップをフェールオーバーすることがないリモート可用性レプリカのような場合に便利です。  
  
7.  変更をコミットするには、 **[OK]** をクリックします。  
  
 **別の方法で [バックアップの設定] ページにアクセスする**  
  
-   [[新しい可用性グループ] ダイアログ ボックスの使用 &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [可用性グループへのレプリカ追加ウィザードの使用 &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md)  
  
-   [[新しい可用性グループ] ダイアログ ボックスの使用 &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
 **セカンダリ レプリカでバックアップを構成するには**  
  
1.  プライマリ レプリカをホストするサーバー インスタンスに接続します。  
  
2.  新しい可用性グループの場合は、[CREATE AVAILABILITY GROUP&#40;Transact-SQL&#41;](../../../t-sql/statements/create-availability-group-transact-sql.md) ステートメントを使用します。 既存の可用性グループを変更する場合は、[ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-availability-group-transact-sql.md) ステートメントを使用します。  
  
##  <a name="PowerShellProcedure"></a> PowerShell の使用  
 **セカンダリ レプリカでバックアップを構成するには**  
  
1.  既定 (**cd**) を、プライマリ レプリカをホストするサーバー インスタンスに設定します。  
  
2.  必要に応じて、追加または変更する各可用性レプリカのバックアップの優先順位を構成します。 この優先順位は、プライマリ レプリカをホストするサーバー インスタンスによって使用され、可用性グループ内のデータベースで自動バックアップ要求を処理するレプリカを決定します (優先順位の高いレプリカが選択されます)。 この優先順位には、0 ～ 100 の数値を指定できます。 優先順位が 0 の場合は、レプリカがバックアップ要求を処理する対象と見なされないことを示します。  既定の設定は 50 です。  
  
     可用性グループに可用性レプリカを追加する場合は、 **New-SqlAvailabilityReplica** コマンドレットを使用します。 既存の可用性レプリカを変更する場合は、 **Set-SqlAvailabilityReplica** コマンドレットを使用します。 どちらの場合も **BackupPriority**_n_ パラメーターを使用します。 *n* は 0 ～ 100 の値です。  
  
     たとえば、次のコマンドは、可用性レプリカ `MyReplica` のバックアップの優先順位を **60**に設定します。  
  
    ```  
    Set-SqlAvailabilityReplica -BackupPriority 60 `  
    -Path SQLSERVER:\Sql\Computer\Instance\AvailabilityGroups\MyAg\AvailabilityReplicas\MyReplica  
    ```  
  
3.  必要に応じて、作成または変更している可用性グループの自動バックアップ設定を構成します。 この優先設定は、バックアップを実行する場所を選択するときにバックアップ ジョブがプライマリ レプリカを評価する方法を指定します。 既定の設定では、セカンダリ レプリカが優先されます。  
  
     可用性グループを作成する場合は、 **New-SqlAvailabilityGroup** コマンドレットを使用します。 既存の可用性グループを変更する場合は、 **Set-SqlAvailabilityGroup** コマンドレットを使用します。 どちらの場合も **AutomatedBackupPreference** パラメーターを指定します。  
  
     パラメーターの説明  
  
     **プライマリ**  
     バックアップを常にプライマリ レプリカで実行することを指定します。 このオプションは、差分バックアップの作成など、バックアップがセカンダリ レプリカで実行されたときにはサポートされないバックアップ機能が必要な場合に役に立ちます。  
  
    > [!IMPORTANT]  
    >  ログ配布を使用して可用性グループのセカンダリ データベースを準備する場合は、すべてのセカンダリ データベースの準備が完了し、それらを可用性グループに参加させるまで、自動バックアップ設定を **[プライマリ]** に設定します。  
  
     **SecondaryOnly**  
     バックアップをプライマリ レプリカでは実行しないことを指定します。 オンラインのレプリカがプライマリ レプリカだけの場合、バックアップは実行されません。  
  
     **セカンダリ**  
     オンラインのレプリカがプライマリ レプリカのみである場合を除き、セカンダリ レプリカでバックアップを実行することを指定します。 オンラインのレプリカがプライマリ レプリカのみである場合は、プライマリ レプリカでバックアップを実行する必要があります。 これは既定の動作です。  
  
     **なし**  
     バックアップを実行するレプリカを選択するときにバックアップ ジョブが可用性レプリカのロールを無視するように指定します。 バックアップ ジョブは、動作状態および接続状態と組み合わせて、各可用性レプリカのバックアップ優先順位などの他の要素を評価する場合があります。  
  
    > [!IMPORTANT]  
    >  **AutomatedBackupPreference**は適用されません。 この優先設定の解釈は、特定の可用性グループのデータベースに対するバックアップ ジョブのスクリプトでのロジックに依存します (ロジックが存在する場合)。 自動バックアップ設定はアドホック バックアップには影響しません。 詳細については、このトピックで後述する「[補足情報:セカンダリ レプリカでバックアップを構成した後](#FollowUp)」を参照してください。  
  
     たとえば、次のコマンドは、可用性グループ **の** AutomatedBackupPreference `MyAg` プロパティを **SecondaryOnly**に設定します。 この可用性グループ内のデータベースの自動バックアップはプライマリ レプリカでは行われませんが、バックアップの優先度設定が最も高いセカンダリ レプリカにリダイレクトされます。  
  
    ```  
    Set-SqlAvailabilityGroup `  
    -Path SQLSERVER:\Sql\PrimaryServer\InstanceName\AvailabilityGroups\MyAg `  
    -AutomatedBackupPreference SecondaryOnly  
    ```  
  
> [!NOTE]  
>  コマンドレットの構文を表示するには、 **PowerShell 環境で** Get-Help [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] コマンドレットを使用します。 詳細については、「 [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md)」を参照してください。  
  
 **SQL Server PowerShell プロバイダーを設定して使用するには**  
  
-   [SQL Server PowerShell プロバイダー](../../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
-   [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md)  
  
##  <a name="FollowUp"></a> 補足情報:セカンダリ レプリカでバックアップを構成した後  
 特定の可用性グループの自動バックアップ設定を考慮に入れるには、バックアップ優先度が 0 を超える (>0) 可用性レプリカをホストする各サーバー インスタンスで、可用性グループのデータベースのバックアップ ジョブを実行するスクリプトを作成する必要があります。 現在のレプリカが優先バックアップ レプリカかどうかを確認すには、バックアップ スクリプトで [sys.fn_hadr_backup_is_preferred_replica](../../../relational-databases/system-functions/sys-fn-hadr-backup-is-preferred-replica-transact-sql.md) 関数を使用します。 現在のサーバー インスタンスでホストされている可用性レプリカがバックアップ用の優先レプリカである場合、この関数は 1 を返します。 そうでない場合、関数は 0 を返します。 この関数に対してクエリを実行する各可用性レプリカを対象にしてシンプルなスクリプトを実行することによって、特定のバックアップ ジョブの実行に適したレプリカを特定できます。 たとえば、バックアップ ジョブ スクリプトの典型的なスニペットは次のようになります。  
  
```  
IF (NOT sys.fn_hadr_backup_is_preferred_replica(@DBNAME))  
BEGIN  
      Select 'This is not the preferred replica, exiting with success';  
      RETURN 0 - This is a normal, expected condition, so the script returns success  
END  
BACKUP DATABASE @DBNAME TO DISK=<disk>  
   WITH COPY_ONLY;  
```  
  
 このロジックを使用してバックアップ ジョブのスクリプトを作成することにより、各可用性レプリカで同じスケジュールでジョブを実行できるようになります。 これらの各ジョブは同じデータを参照してジョブを実行する必要があるかどうかを判断するので、実際にバックアップ ステージに進むことができるのは、スケジュールされているジョブのうち 1 つだけです。  フェールオーバーが発生した場合に、どのスクリプトやジョブも変更する必要はありません。 また、可用性グループを再構成して可用性レプリカを追加する場合、バックアップ ジョブの管理で必要な操作は、バックアップ ジョブのコピーまたはスケジュールのみです。 可用性レプリカを削除する場合は、レプリカをホストするサーバー インスタンスからバックアップ ジョブを削除する操作のみです。  
  
> [!TIP]  
>  [メンテナンス プラン ウィザード](../../../relational-databases/maintenance-plans/use-the-maintenance-plan-wizard.md)を使用してバックアップ ジョブを作成すると、 **sys.fn_hadr_backup_is_preferred_replica** 関数の呼び出しと確認を行うスクリプト作成ロジックがそのジョブに自動的に含まれます。 ただし、バックアップ ジョブによって、"これは優先レプリカではありません" というメッセージが返されることはありません。可用性グループの可用性レプリカをホストする各サーバー インスタンスで、各可用性データベースのジョブを必ず作成します。  
  
##  <a name="ForInfoAboutBuPref"></a> バックアップ優先設定に関する情報を取得するには  
 次の表は、セカンダリでのバックアップに関連する情報を取得するのに役立ちます。  
  
|表示|[情報]|関連する列|  
|----------|-----------------|----------------------|  
|[sys.fn_hadr_backup_is_preferred_replica](../../../relational-databases/system-functions/sys-fn-hadr-backup-is-preferred-replica-transact-sql.md)|現在のレプリカが優先されるバックアップ レプリカであるかどうか|該当なし。|  
|[sys.availability_groups](../../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md)|自動バックアップ設定|**automated_backup_preference**<br /><br /> **automated_backup_preference_desc**|  
|[sys.availability_replicas](../../../relational-databases/system-catalog-views/sys-availability-replicas-transact-sql.md)|指定された可用性レプリカのバックアップの優先順位|**backup_priority**|  
|[sys.dm_hadr_availability_replica_states](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-states-transact-sql.md)|レプリカがこのサーバー インスタンスにローカルであるかどうか<br /><br /> 現在のロール<br /><br /> 運用状態<br /><br /> 接続状態<br /><br /> 可用性レプリカの同期の正常性|**is_local**<br /><br /> **ロール**, 、 **role_desc**<br /><br /> **operational_state**、 **operational_state_desc**<br /><br /> **connected_state**、 **connected_state_desc**<br /><br /> **synchronization_health**、 **synchronization_health_desc**|  
  
##  <a name="RelatedContent"></a> 関連コンテンツ  
  
-   [高可用性と災害復旧のための Microsoft SQL Server AlwaysOn ソリューション ガイド](https://go.microsoft.com/fwlink/?LinkId=227600)  
  
-   [SQL Server Always On チーム ブログ:SQL Server Always On チームのオフィシャル ブログ](https://blogs.msdn.microsoft.com/sqlalwayson/)  
  
## <a name="see-also"></a>参照  
 [AlwaysOn 可用性グループの概要 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [アクティブなセカンダリ:セカンダリ レプリカでのバックアップ &#40;Always On 可用性グループ&#41;](../../../database-engine/availability-groups/windows/active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md)  
  
  
