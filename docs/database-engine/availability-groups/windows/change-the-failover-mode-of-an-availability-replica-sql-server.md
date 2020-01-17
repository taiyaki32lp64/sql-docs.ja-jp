---
title: 可用性グループのレプリカ フェールオーバー モードの変更
description: Transact-SQL (T-SQL)、PowerShell、または SQL Server Management Studio を使用して Always On 可用性グループ内のレプリカのフェールオーバー モードを変更する方法を説明します。
ms.custom: seo-lt-2019
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- failover modes [SQL Server]
- Availability Groups [SQL Server], deploying
- Availability Groups [SQL Server], failover modes
- Availability Groups [SQL Server], configuring
ms.assetid: 619a826f-8e65-48eb-8c34-39497d238279
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 4dd7de6af88d6fe5955c03f611a593869e19cfc0
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75241819"
---
# <a name="change-the-failover-mode-for-a-replica-within-an-always-on-availability-group"></a>Always On 可用性グループ内のレプリカのフェールオーバー モードの変更
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このトピックでは、 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 、 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]または PowerShell を使用して、 [!INCLUDE[tsql](../../../includes/tsql-md.md)]の Always On 可用性グループでの可用性レプリカのフェールオーバー モードを変更する方法について説明します。 フェールオーバー モードは、同期コミット可用性モードで実行されるレプリカのフェールオーバー モードを決定するレプリカ プロパティです。 詳細については、「 [フェールオーバーとフェールオーバー モード &#40;Always On 可用性グループ&#41;](../../../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md) 」および「 [可用性モード &#40;Always On 可用性グループ&#41;](../../../database-engine/availability-groups/windows/availability-modes-always-on-availability-groups.md)」を参照してください。  
  
## <a name="Prerequisites"></a> 前提条件と制限  
  
-   このタスクは、プライマリ レプリカ上でのみサポートされます。 プライマリ レプリカをホストするサーバー インスタンスに接続されている必要があります。  
  
-   SQL Server フェールオーバー クラスター インスタンス (FCI) は可用性グループによる自動フェールオーバーをサポートしないため、FCI によってホストされる可用性レプリカは手動フェールオーバー用にのみ構成できます。  
  

##  <a name="Permissions"></a> Permissions  
 可用性グループの ALTER AVAILABILITY GROUP 権限、CONTROL AVAILABILITY GROUP 権限、ALTER ANY AVAILABILITY GROUP 権限、または CONTROL SERVER 権限が必要です。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
 **可用性レプリカのフェールオーバー モードを変更するには**  
  
1.  オブジェクト エクスプローラーで、プライマリ レプリカをホストするサーバー インスタンスに接続し、サーバー ツリーを展開します。  
  
2.  **[AlwaysOn 高可用性]** ノードと **[可用性グループ]** ノードを展開します。  
  
3.  変更するレプリカが含まれる可用性グループをクリックします。  
  
4.  レプリカを右クリックし、 **[プロパティ]** をクリックします。  
  
5.  **[可用性レプリカ プロパティ]** ダイアログ ボックスで **[フェールオーバー モード]** ボックスの一覧を使用して、このレプリカのフェールオーバー モードを変更します。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
 **可用性レプリカのフェールオーバー モードを変更するには**  
  
1.  プライマリ レプリカをホストするサーバー インスタンスに接続します。  
  
2.  [ALTER AVAILABILITY GROUP](../../../t-sql/statements/alter-availability-group-transact-sql.md) ステートメントを使用します。次にその例を示します。

   ```Transact-SQL
   ALTER AVAILABILITY GROUP *group_name* MODIFY REPLICA ON '*server_name*'  
      WITH ( {  
           AVAILABILITY_MODE = { SYNCHRONOUS_COMMIT | ASYNCHRONOUS_COMMIT }
              | FAILOVER_MODE = { AUTOMATIC | MANUAL }
            }  )
   ```

   前述のスクリプトでは、

      - *group_name* は、可用性グループの名前です。  
  
      - *server_name* はコンピューター名またはフェールオーバー クラスターのネットワーク名です。 名前付きインスタンスの場合は、`\instance_name' を追加します。 変更するレプリカをホストする名前を使用します。
  
   これらのパラメーターの詳細については、「[ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-availability-group-transact-sql.md)」を参照してください。  
  
   次の例は、 *MyAG* 可用性グループのプライマリ レプリカで実行すると、 *COMPUTER01*という名前のコンピューター上の既定のサーバー インスタンスにある可用性レプリカで、フェールオーバー モードが自動フェールオーバーに変更されます。  
  
    ```  
    ALTER AVAILABILITY GROUP MyAG MODIFY REPLICA ON 'COMPUTER01' WITH  
       (FAILOVER_MODE = AUTOMATIC);  
    ```  
  
##  <a name="PowerShellProcedure"></a> PowerShell の使用  
 **可用性レプリカのフェールオーバー モードを変更するには**  
  
1.  プライマリ レプリカをホストするサーバー インスタンスにディレクトリを変更 (**cd**) します 。  
  
2.  **FailoverMode** パラメーターを指定して **Set-SqlAvailabilityReplica** コマンドレットを使用します。 レプリカを自動フェールオーバーに設定するときは、 **AvailabilityMode** パラメーターを使用して、レプリカを同期コミット可用性モードに変更しなければならない場合があります。  
  
     たとえば、次のコマンドは、可用性グループ `MyReplica` のレプリカ `MyAg` を、同期コミット可用性モードを使用し、自動フェールオーバーをサポートするように変更します。  
  
    ```  
    Set-SqlAvailabilityReplica -AvailabilityMode "SynchronousCommit" -FailoverMode "Automatic" `   
    -Path SQLSERVER:\Sql\PrimaryServer\InstanceName\AvailabilityGroups\MyAg\Replicas\MyReplica  
    ```  
  
    > [!NOTE]  
    >  コマンドレットの構文を表示するには、 **PowerShell 環境で** Get-Help [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] コマンドレットを使用します。 詳細については、「 [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md)」を参照してください。  
  
 **SQL Server PowerShell プロバイダーを設定して使用するには**  
  
-   [SQL Server PowerShell プロバイダー](../../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
## <a name="see-also"></a>参照  
 [AlwaysOn 可用性グループの概要 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [可用性モード &#40;AlwaysOn 可用性グループ&#41;](../../../database-engine/availability-groups/windows/availability-modes-always-on-availability-groups.md)   
 [フェールオーバーとフェールオーバー モード &#40;Always On 可用性グループ&#41;](../../../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md)  
  
  
