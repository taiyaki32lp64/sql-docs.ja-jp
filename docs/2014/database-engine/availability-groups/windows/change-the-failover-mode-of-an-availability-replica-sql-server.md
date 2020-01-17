---
title: 可用性レプリカのフェールオーバー モードの変更 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 6750456d708d68e57aadd4b1139f6e108a93b9ba
ms.sourcegitcommit: a165052c789a327a3a7202872669ce039bd9e495
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72783014"
---
# <a name="change-the-failover-mode-of-an-availability-replica-sql-server"></a>可用性レプリカのフェールオーバー モードの変更 (SQL Server)
  このトピックでは、 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 、 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]、または PowerShell を使用して、 [!INCLUDE[tsql](../../../includes/tsql-md.md)]の AlwaysOn 可用性グループでの可用性レプリカのフェールオーバー モードを変更する方法について説明します。 フェールオーバー モードは、同期コミット可用性モードで実行されるレプリカのフェールオーバー モードを決定するレプリカ プロパティです。 詳細については、「[フェールオーバーとフェールオーバー モード &#40;AlwaysOn 可用性グループ&#41;](failover-and-failover-modes-always-on-availability-groups.md)」および「[可用性モード &#40;AlwaysOn 可用性グループ&#41;](availability-modes-always-on-availability-groups.md)」を参照してください。  
  

  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Prerequisites"></a> 前提条件と制限  
  
-   このタスクは、プライマリ レプリカ上でのみサポートされます。 プライマリ レプリカをホストするサーバー インスタンスに接続されている必要があります。  
  
-   SQL Server フェールオーバー クラスター インスタンス (FCI) は可用性グループによる自動フェールオーバーをサポートしないため、FCI によってホストされる可用性レプリカは手動フェールオーバー用にのみ構成できます。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> アクセス許可  
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
  
2.  [ALTER AVAILABILITY GROUP](/sql/t-sql/statements/alter-availability-group-transact-sql) ステートメントを使用します。次にその例を示します。  
  
     ALTER AVAILABILITY GROUP *group_name* MODIFY REPLICA ON '*server_name*'  
  
     WITH ( {  
  
     AVAILABILITY_MODE = { SYNCHRONOUS_COMMIT | ASYNCHRONOUS_COMMIT }  
  
     | FAILOVER_MODE = { AUTOMATIC | MANUAL }  
  
     }  )  
  
     パラメーターの説明  
  
    -   *group_name* は、可用性グループの名前です。  
  
    -   { '*system_name*[\\*instance_name*]' | '*FCI_network_name*[\\*instance_name*]' }  
  
         変更する可用性レプリカをホストする [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスのアドレスを指定します。 このアドレスの構成要素は次のとおりです。  
  
         *system_name*  
         スタンドアロン サーバー インスタンスが存在するコンピューター システムの NetBIOS 名です。  
  
         *FCI_network_name*  
         ターゲット サーバー インスタンスが [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー パートナー (FCI) である [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスターにアクセスするために使用されるネットワーク名です。  
  
         *instance_name*  
         ターゲットの可用性レプリカをホストする [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスの名前です。 既定のサーバー インスタンスの場合、 *instance_name* は省略可能です。  
  
     これらのパラメーターの詳細については、「[ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-availability-group-transact-sql)」を参照してください。  
  
     次の例は、 *MyAG* 可用性グループのプライマリ レプリカで実行すると、 *COMPUTER01*という名前のコンピューター上の既定のサーバー インスタンスにある可用性レプリカで、フェールオーバー モードが自動フェールオーバーに変更されます。  
  
    ```  
    ALTER AVAILABILITY GROUP MyAG MODIFY REPLICA ON 'COMPUTER01' WITH  
       (FAILOVER_MODE = AUTOMATIC);  
    ```  
  
##  <a name="PowerShellProcedure"></a> PowerShell の使用  

### <a name="to-change-the-failover-mode-of-an-availability-replica"></a>可用性レプリカのフェールオーバー モードを変更するには
  
1.  プライマリ レプリカをホストするサーバー インスタンスにディレクトリを変更 (`cd`) します。  
  
2.  `Set-SqlAvailabilityReplica` パラメーターを指定して `FailoverMode` コマンドレットを使用します。 レプリカを自動フェールオーバーに設定するときは、`AvailabilityMode` パラメーターを使用して、レプリカを同期コミット可用性モードに変更しなければならない場合があります。  
  
     たとえば、次のコマンドは、可用性グループ `MyReplica` のレプリカ `MyAg` を、同期コミット可用性モードを使用し、自動フェールオーバーをサポートするように変更します。  
  
    ```powershell
    Set-SqlAvailabilityReplica -AvailabilityMode "SynchronousCommit" -FailoverMode "Automatic" `
     -Path SQLSERVER:\Sql\PrimaryServer\InstanceName\AvailabilityGroups\MyAg\Replicas\MyReplica  
    ```  
  
    > [!NOTE]  
    >  コマンドレットの構文を表示するには、`Get-Help` PowerShell 環境で [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] コマンドレットを使用します。 詳細については、「 [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md)」を参照してください。  
  
SQL Server PowerShell プロバイダーを設定して使用する方法については、「 [SQL Server PowerShell プロバイダー](../../../powershell/sql-server-powershell-provider.md)」を参照してください。
  
## <a name="see-also"></a>参照  
 [AlwaysOn 可用性グループ&#40;SQL Server の概要&#41;](overview-of-always-on-availability-groups-sql-server.md)  
 [可用性モード&#40;AlwaysOn 可用性グループ&#41; ](availability-modes-always-on-availability-groups.md)   
 [フェールオーバーとフェール&#40;オーバーモード AlwaysOn 可用性グループ&#41;](failover-and-failover-modes-always-on-availability-groups.md) 
