---
title: 可用性グループへのセカンダリ レプリカの参加
description: Transact-SQL (T-SQL)、PowerShell、または SQL Server Management Studio のいずれかを使用して Always On 可用性グループにセカンダリ レプリカを参加させる手順について説明します。
ms.custom: seodec18
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.availabilitygroup.joinreplica.f1
helpviewer_keywords:
- Availability Groups [SQL Server], availability replicas
- Availability Groups [SQL Server], joining
- Availability Groups [SQL Server], configuring
ms.assetid: e5bd2489-097a-490e-8ea1-34fe48378ad1
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 560b808bc22145993ea7ae713ce45d650a0933d0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68003720"
---
# <a name="join-a-secondary-replica-to-an-always-on-availability-group"></a>Always On 可用性グループへのセカンダリ レプリカの参加
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このトピックでは、 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]で [!INCLUDE[tsql](../../../includes/tsql-md.md)]、 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]、または PowerShell を使用して、Always On 可用性グループにセカンダリ レプリカを参加させる方法について説明します。 Always On 可用性グループにセカンダリ レプリカを追加したら、セカンダリ レプリカを可用性グループに参加させる必要があります。 レプリカの参加操作は、セカンダリ レプリカをホストしている [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンス上で実行する必要があります。  

  
##  <a name="Prerequisites"></a> 前提条件  
  
-   可用性グループのプライマリ レプリカが現在オンラインになっている必要があります。    
-   可用性グループへの参加が済んでいないセカンダリ レプリカをホストするサーバー インスタンスに接続されている必要があります。    
-   プライマリ レプリカをホストしているサーバー インスタンスのデータベース ミラーリング エンドポイントに対してローカル サーバー インスタンスが接続できる必要があります。  
  
> [!IMPORTANT]  
>  いずれかの前提条件が満たされていない場合、参加操作は失敗します。 参加操作が失敗した場合は、プライマリ レプリカをホストしているサーバー インスタンスに接続し、セカンダリ レプリカを削除して再度追加した後で、可用性グループに参加させる必要があります。 詳細については、「[可用性グループからのセカンダリ レプリカの削除 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remove-a-secondary-replica-from-an-availability-group-sql-server.md)」および「[可用性グループへのセカンダリ レプリカの追加 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server.md)」を参照してください。  
  
##  <a name="Permissions"></a> Permissions  
 可用性グループの ALTER AVAILABILITY GROUP 権限、CONTROL AVAILABILITY GROUP 権限、ALTER ANY AVAILABILITY GROUP 権限、または CONTROL SERVER 権限が必要です。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
 **可用性グループに可用性レプリカを参加させるには**  
  
1.  オブジェクト エクスプローラーで、セカンダリ レプリカをホストするサーバー インスタンスに接続し、サーバー名をクリックしてサーバー ツリーを展開します。  
  
2.  **[AlwaysOn 高可用性]** ノードと **[可用性グループ]** ノードを展開します。  
  
3.  接続先のセカンダリ レプリカの可用性グループを選択します。  
  
4.  セカンダリ レプリカを右クリックし、 **[可用性グループへの参加]** をクリックします。  
  
5.  これにより、 **[可用性グループへのレプリカの追加]** ダイアログ ボックスが開きます。  
  
6.  セカンダリ レプリカを可用性グループに参加させるには、 **[OK]** をクリックします。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
 **可用性グループに可用性レプリカを参加させるには**  
  
1.  セカンダリ レプリカをホストするサーバー インスタンスに接続します。  
  
2.  [ALTER AVAILABILITY GROUP](../../../t-sql/statements/alter-availability-group-transact-sql.md) ステートメントを使用します。次にその例を示します。  
  
     ALTER AVAILABILITY GROUP *group_name* JOIN  
  
     *group_name* は可用性グループの名前です。  
  
     次の例では、セカンダリ レプリカを `MyAG` 可用性グループに参加させています。  
  
    ```  
    ALTER AVAILABILITY GROUP MyAG JOIN;  
    ```  
  
    > [!NOTE]  
    >  コンテキストで使用するこの [!INCLUDE[tsql](../../../includes/tsql-md.md)] ステートメントを確認するには、「[可用性グループの作成 &#40;Transact-SQL&#41;](../../../database-engine/availability-groups/windows/create-an-availability-group-transact-sql.md)」を参照してください。  
  
##  <a name="PowerShellProcedure"></a> PowerShell の使用  
 **可用性グループに可用性レプリカを参加させるには**  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell プロバイダーで次の操作を行います。  
  
1.  ディレクトリ変更コマンド (**cd**) を使用して、セカンダリ レプリカがホストされているサーバー インスタンスに移動します。  
  
2.  **Join-SqlAvailabilityGroup** コマンドレットに可用性グループの名前を指定して実行し、セカンダリ レプリカを可用性グループに参加させます。  
  
     たとえば、次のコマンドは、指定されたパスにあるサーバー インスタンスによってホストされるセカンダリ レプリカを `MyAg`という名前の可用性グループに参加させます。  このサーバー インスタンスは、この可用性グループ内のセカンダリ レプリカをホストする必要があります。  
  
    ```  
    Join-SqlAvailabilityGroup -Path SQLSERVER:\SQL\SecondaryServer\InstanceName -Name 'MyAg'  
    ```  
  
    > [!NOTE]  
    >  コマンドレットの構文を表示するには、 **PowerShell 環境で** Get-Help [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] コマンドレットを使用します。 詳細については、「 [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md)」を参照してください。  
  
 **SQL Server PowerShell プロバイダーを設定して使用するには**  
  
-   [SQL Server PowerShell プロバイダー](../../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
##  <a name="FollowUp"></a> 補足情報:セカンダリ データベースの構成  
 可用性グループ内のすべてのデータベースには、それぞれ対応するセカンダリ データベースが、セカンダリ レプリカをホストしているサーバー インスタンス上に存在している必要があります。 セカンダリ データベースの構成は、セカンダリ レプリカを可用性グループに参加させる前に行うことも、参加させた後に行うこともできます。  
  
1.  各プライマリ データベースの最新のデータベースとログ バックアップを、セカンダリ レプリカをホストするサーバー インスタンスに復元します。すべての復元操作は RESTORE WITH NORECOVERY で行う必要があります。 詳細については、「 [可用性グループに対するセカンダリ データベースの手動準備 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)、または PowerShell を使用して、AlwaysOn 可用性グループにセカンダリ データベースを参加させる方法について説明します。  
  
2.  各セカンダリ データベースを可用性グループに参加させます。 詳細については、「[可用性グループへのセカンダリ データベースの参加 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-database-to-an-availability-group-sql-server.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [可用性グループの作成と構成 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/creation-and-configuration-of-availability-groups-sql-server.md)   
 [AlwaysOn 可用性グループの概要 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Always On 可用性グループの構成のトラブルシューティング &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/troubleshoot-always-on-availability-groups-configuration-sql-server.md)  
  
  
