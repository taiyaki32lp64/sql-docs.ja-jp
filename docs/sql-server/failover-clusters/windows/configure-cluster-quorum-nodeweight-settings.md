---
title: クラスター クォーラムの NodeWeight の設定の構成 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], WSFC clusters
- quorum [SQL Server], AlwaysOn and WSFC quorum
ms.assetid: cb3fd9a6-39a2-4e9c-9157-619bf3db9951
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: c42abb37423cd03b4c0233ac44244cdea00708a7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68063779"
---
# <a name="configure-cluster-quorum-nodeweight-settings"></a>クラスター クォーラムの NodeWeight の設定の構成
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このトピックでは、Windows Server フェールオーバー クラスタリング (WSFC) クラスター内のメンバー ノードに NodeWeight 設定を構成する方法について説明します。 NodeWeight 設定は、[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]および [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスター インスタンスのディザスター リカバリーとマルチサブネットのシナリオをサポートするためのクォーラムの投票時に使用されます。  
  
-   **開始前の準備:** [前提条件](#Prerequisites)、[セキュリティ](#Security)  
  
-   **クォーラムの NodeWeight 設定を表示する方法:** [Powershell の使用](#PowerShellProcedure)、[Cluster.exe の使用](#CommandPromptProcedure)  
  
-   [関連コンテンツ](#RelatedContent)  
  
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
  
##  <a name="PowerShellProcedure"></a> PowerShell の使用  
  
##### <a name="to-configure-nodeweight-settings"></a>NodeWeight 設定を構成するには  
  
1.  **[実行管理者として実行]** から高度な権限で Windows PowerShell を起動します。  
  
2.  `FailoverClusters` モジュールをインポートしてクラスター コマンドレットを有効にします。  
  
3.  `Get-ClusterNode` オブジェクトを使用して、クラスター内の各ノードに `NodeWeight` プロパティを設定します。  
  
4.  クラスター ノードのプロパティを判読可能な形式で出力します。  
  
### <a name="example-powershell"></a>例 (PowerShell)  
 次の例では、NodeWeight 設定を "AlwaysOnSrv1" ノードのクォーラムの投票を削除するように変更して、クラスター内のすべてのノードに設定を出力します。  
  
```powershell  
Import-Module FailoverClusters  
  
$node = "AlwaysOnSrv1"  
(Get-ClusterNode $node).NodeWeight = 0  
  
$cluster = (Get-ClusterNode $node).Cluster  
$nodes = Get-ClusterNode -Cluster $cluster  
  
$nodes | Format-Table -property NodeName, State, NodeWeight  
```  
  
##  <a name="CommandPromptProcedure"></a> cluster.exe の使用  
  
> [!NOTE]  
>  cluster.exe ユーティリティは [!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)] リリースでは非推奨とされます。  今後は PowerShell とフェールオーバー クラスタリングを使用してください。  cluster.exe ユーティリティは、Windows Server の次のリリースで削除されます。 詳細については、「 [フェールオーバー クラスターの Windows PowerShell コマンドレットへの Cluster.exe コマンドのマッピング](https://technet.microsoft.com/library/ee619744\(WS.10\).aspx)」を参照してください。  
  
##### <a name="to-configure-nodeweight-settings"></a>NodeWeight 設定を構成するには  
  
1.  **[実行管理者として実行]** から高度な権限でコマンド プロンプトを起動します。  
  
2.  **cluster.exe** を使用して、 `NodeWeight` 値を設定します。  
  
### <a name="example-clusterexe"></a>例 (Cluster.exe)  
 次の例では、NodeWeight の値を "Cluster001" クラスターで "AlwaysOnSrv1" ノードのクォーラムの投票を削除するように変更します。  
  
```ms-dos  
cluster.exe Cluster001 node AlwaysOnSrv1 /prop NodeWeight=0  
```  
  
##  <a name="RelatedContent"></a> 関連コンテンツ  
  
-   [フェールオーバー クラスターのイベントおよびログを表示する](https://technet.microsoft.com/library/cc772342\(WS.10\).aspx)  
  
-   [Get-ClusterLog フェールオーバー クラスター コマンドレット](https://technet.microsoft.com/library/ee461045.aspx)  
  
## <a name="see-also"></a>参照  
 [WSFC クォーラム モードと投票の構成 &#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/wsfc-quorum-modes-and-voting-configuration-sql-server.md)   
 [クラスター クォーラムの NodeWeight 設定を表示](../../../sql-server/failover-clusters/windows/view-cluster-quorum-nodeweight-settings.md)   
 [タスク フォーカスによって一覧表示される Windows PowerShell でのフェールオーバー クラスター コマンドレット](https://technet.microsoft.com/library/ee619761\(WS.10\).aspx)  
  
  
