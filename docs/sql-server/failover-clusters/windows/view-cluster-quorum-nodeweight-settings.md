---
title: クラスター クォーラムの NodeWeight 設定を表示 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], WSFC clusters
- quorum [SQL Server], AlwaysOn and WSFC quorum
ms.assetid: b845e73a-bb01-4de2-aac2-8ac12abebc95
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 6d3b98adece53952f72afc999f950c0388b65c96
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67904923"
---
# <a name="view-cluster-quorum-nodeweight-settings"></a>クラスター クォーラムの NodeWeight 設定を表示
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このトピックでは、Windows Server フェールオーバー クラスタリング (WSFC) クラスター内の各メンバー ノードの NodeWeight 設定を表示する方法について説明します。 NodeWeight 設定は、[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]および [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスター インスタンスのディザスター リカバリーとマルチサブネットのシナリオをサポートするためのクォーラムの投票時に使用されます。  
  
-   **開始前の準備:** [前提条件](#Prerequisites)、[セキュリティ](#Security)  
  
-   **クォーラムの NodeWeight 設定を表示する方法:** [Transact-SQL の使用](#TsqlProcedure)、[PowerShell の使用](#PowerShellProcedure)、[Cluster.exe の使用](#CommandPromptProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始前の準備  
  
###  <a name="Prerequisites"></a> 前提条件  
 この機能は [!INCLUDE[firstref_longhorn](../../../includes/firstref-longhorn-md.md)] 以降のバージョンでのみサポートされています。  
  
> [!IMPORTANT]  
>  NodeWeight 設定を使用するには、次の修正プログラムが WSFC クラスターのすべてのサーバーに適用されている必要があります。  
>   
>  [KB2494036](https://support.microsoft.com/kb/2494036):この修正プログラムを使用すると、[!INCLUDE[firstref_longhorn](../../../includes/firstref-longhorn-md.md)] および [!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)] でクォーラムの投票のないクラスター ノードを構成することができます。  
  
> [!TIP]  
>  この修正プログラムがインストールされていない場合、このトピックの例では、NodeWeight に対して空の値または NULL 値が返されます。  
  
###  <a name="Security"></a> セキュリティ  
 ユーザーは、WSFC クラスターの各ノードのローカル Administrators グループのメンバーであるドメイン アカウントを使用する必要があります。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
##### <a name="to-view-nodeweight-settings"></a>NodeWeight 設定を表示するには  
  
1.  クラスター内の任意の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスに接続します。  
  
2.  [sys].[dm_hadr_cluster_members] ビューに対してクエリを実行します。  
  
### <a name="example-transact-sql"></a>例 (Transact-SQL)  
 次の例では、システム ビューに対するクエリを実行して、そのインスタンスのクラスター内のすべてのノードの値を返します。  
  
```sql  
SELECT  member_name, member_state_desc, number_of_quorum_votes  
 FROM   sys.dm_hadr_cluster_members;  
```  
  
##  <a name="PowerShellProcedure"></a> PowerShell の使用  
  
##### <a name="to-view-nodeweight-settings"></a>NodeWeight 設定を表示するには  
  
1.  **[実行管理者として実行]** から高度な権限で Windows PowerShell を起動します。  
  
2.  `FailoverClusters` モジュールをインポートしてクラスター コマンドレットを有効にします。  
  
3.  `Get-ClusterNode` オブジェクトを使用して、クラスター ノード オブジェクトのコレクションを返します。  
  
4.  クラスター ノードのプロパティを判読可能な形式で出力します。  
  
### <a name="example-powershell"></a>例 (PowerShell)  
 次の例では、"Cluster001" というクラスターについて、ノードの一部のプロパティを出力します。  
  
```powershell  
Import-Module FailoverClusters  
  
$cluster = "Cluster001"  
$nodes = Get-ClusterNode -Cluster $cluster  
  
$nodes | Format-Table -property NodeName, State, NodeWeight  
```  
  
##  <a name="CommandPromptProcedure"></a> cluster.exe の使用  
  
> [!NOTE]  
>  cluster.exe ユーティリティは [!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)] リリースでは非推奨とされます。  今後は PowerShell とフェールオーバー クラスタリングを使用してください。  cluster.exe ユーティリティは、Windows Server の次のリリースで削除されます。 詳細については、「 [フェールオーバー クラスターの Windows PowerShell コマンドレットへの Cluster.exe コマンドのマッピング](https://technet.microsoft.com/library/ee619744\(WS.10\).aspx)」を参照してください。  
  
##### <a name="to-view-nodeweight-settings"></a>NodeWeight 設定を表示するには  
  
1.  **[実行管理者として実行]** から高度な権限でコマンド プロンプトを起動します。  
  
2.  **cluster.exe** を使用して、ノードの状態と NodeWeight の値を返します。  
  
### <a name="example-clusterexe"></a>例 (Cluster.exe)  
 次の例では、"Cluster001" というクラスターについて、ノードの一部のプロパティを出力します。  
  
```ms-dos  
cluster.exe Cluster001 node /status /properties  
```  
  
## <a name="see-also"></a>参照  
 [WSFC クォーラム モードと投票の構成 &#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/wsfc-quorum-modes-and-voting-configuration-sql-server.md)   
 [クラスター クォーラムの NodeWeight の設定の構成](../../../sql-server/failover-clusters/windows/configure-cluster-quorum-nodeweight-settings.md)   
 [sys.dm_hadr_cluster_members &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-members-transact-sql.md)   
 [タスク フォーカスによって一覧表示される Windows PowerShell でのフェールオーバー クラスター コマンドレット](https://technet.microsoft.com/library/ee619761\(WS.10\).aspx)  
  
  
