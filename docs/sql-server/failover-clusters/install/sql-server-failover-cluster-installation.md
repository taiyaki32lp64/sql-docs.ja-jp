---
title: SQL Server フェールオーバー クラスターのインストール | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: c0e75a7c-85c5-423c-a218-77247bf071aa
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: cdc11ab9550b0faaf1fcdc9aa3ba5d7d3fe09eaf
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68063870"
---
# <a name="sql-server-failover-cluster-installation"></a>SQL Server フェールオーバー クラスターのインストール
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のフェールオーバー クラスターをインストールするには、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] セットアップを実行してフェールオーバー クラスター インスタンスを作成し、構成する必要があります。  
  
## <a name="installing-a-failover-cluster"></a>フェールオーバー クラスターのインストール  
 フェールオーバー クラスターをインストールするには、ローカル管理者権限、サービスとしてログオンする権限、およびフェールオーバー クラスター内にあるすべてのノード上のオペレーティング システムの一部として動作する権限を持つドメイン アカウントを使用する必要があります。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] セットアップ プログラムを使用してフェールオーバー クラスターをインストールするには、次の手順を実行します。  
  
1.  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスターをインストール、構成、および管理するには、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] セットアップを使用します。  
  
    -   フェールオーバー クラスター インスタンスの作成に必要な情報 (クラスター ディスク リソース、IP アドレス、ネットワーク名など)、およびフェールオーバーで利用できるノードを確認します。 詳細:  
  
        -   [フェールオーバー クラスタリングをインストールする前に](../../../sql-server/failover-clusters/install/before-installing-failover-clustering.md)  
  
        -   [SQL Server インストールにおけるセキュリティの考慮事項](../../../sql-server/install/security-considerations-for-a-sql-server-installation.md)  
  
    -   これらの構成手順は、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] セットアップ プログラムを実行する前に行う必要があります。Windows のクラスター アドミニストレーターを使用して、手順を実行してください。構成するフェールオーバー クラスター インスタンスごとに 1 つの WSFC グループが必要です。  
  
    -   システムが最小要件を満たしていることを確認する必要があります。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスターに関する特定の要件の詳細については、「 [フェールオーバー クラスタリングをインストールする前に](../../../sql-server/failover-clusters/install/before-installing-failover-clustering.md)」を参照してください。  
  
2.  他のクラスター ノードに影響を与えずに、フェールオーバー クラスター構成からノードを追加または削除します。 詳細については、「[SQL Server フェールオーバー クラスターでのノードの追加または削除 &#40;セットアップ&#41;](../../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)」を参照してください。  
  
    -   フェールオーバー クラスター内のすべてのノードは、32 ビットまたは 64 ビットのいずれかの同一プラットフォームで構成され、エディションおよびバージョンが同じオペレーティング システムを実行している必要があります。 また、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の 64 ビット エディションは、64 ビット版の Windows オペレーティング システムを実行する 64 ビット ハードウェアにインストールする必要があります。 このリリースのフェールオーバー クラスタリングでは、WOW64 がサポートされません。  
  
3.  フェールオーバー クラスター インスタンスごとに複数の IP アドレスを指定します。 各サブネットに複数の IP アドレスを指定することができます。 同じサブネットに複数の IP アドレスがある場合、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] セットアップは依存関係を AND に設定します。 複数のサブネットにわたってノードをクラスター化している場合、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] セットアップは依存関係を OR に設定します。  

4.  SQL Server フェールオーバー クラスター インスタンス (FCI) では、クラスター ノードをドメイン参加させる必要があります。 次の構成は**サポートされていません**。
    - ワークグループ クラスター上の SQL FCI。 
    - マルチドメイン クラスター上の SQL FCI。   
    - ドメイン + ワークグループ クラスター上の SQL FCI。 

## <a name="includessnoversionincludesssnoversion-mdmd-failover-cluster-installation-options"></a>[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスター インストール オプション  
  
##### <a name="option-1-integrated-installation-with-add-node"></a>オプション 1:ノードの追加を伴う統合インストール  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 統合フェールオーバー クラスター インストールは、次の 2 つの手順で構成されています。  
  
1.  単一ノードの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスター インスタンスを作成および構成します。 ノードの構成が正常に完了すると、完全に機能するフェールオーバー クラスター インスタンスが完成します。 フェールオーバー クラスターには 1 つのノードしかないので、この時点では高可用性は備わっていません。  
  
2.  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスターに追加する各ノードで、セットアップを実行し、ノードの追加機能を使用して、ノードを追加します。  
  
##### <a name="option-2-advancedenterprise-installation"></a>オプション 2:高度/エンタープライズ インストール  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 高度/エンタープライズ フェールオーバー クラスター インストールは、次の 2 つの手順で構成されています。  
  
1.  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスターの一部となる各ノードで、セットアップを実行し、フェールオーバー クラスターの準備機能を使用します。 この手順ではノードのクラスター化の準備を行いますが、この手順が終了しても [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスは操作できません。  
  
2.  ノードのクラスター化の準備が整ったら、共有ディスクを所有するノードでセットアップを実行し、フェールオーバー クラスターの実行機能を使用します。 この手順で、フェールオーバー クラスター インスタンスを構成し、完了します。 この手順が完了すると、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスター インスタンスが操作可能になります。  
  
    > [!NOTE]  
    >  マルチノード [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスターのインストールでは、いずれのインストール オプションも使用できます。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスターを作成した後、いずれのオプションでもノードの追加機能を使用してさらにノードを追加することができます。  
  
    > [!IMPORTANT]  
    >  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインストール場所に使用されているオペレーティング システムのドライブ文字は、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスターに追加されるすべてのノードで一致している必要があります。  
  
#### <a name="ip-address-configuration-during-setup"></a>セットアップ中の IP アドレスの構成  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] セットアップでは、次の操作中に、IP リソースの依存関係の設定を指定したり、変更したりできます。  
  
-   統合インストール - [新しい SQL Server フェールオーバー クラスターの作成 &#40;セットアップ&#41;](../../../sql-server/failover-clusters/install/create-a-new-sql-server-failover-cluster-setup.md)  
  
-   CompleteFailoverCluster (詳細インストール) - [新しい SQL Server フェールオーバー クラスターの作成 &#40;セットアップ&#41;](../../../sql-server/failover-clusters/install/create-a-new-sql-server-failover-cluster-setup.md)  
  
-   ノードの追加 - [SQL Server フェールオーバー クラスターでのノードの追加または削除 &#40;セットアップ&#41;](../../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)  
  
-   ノードの削除 - [SQL Server フェールオーバー クラスターでのノードの追加または削除 &#40;セットアップ&#41;](../../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)  
  
 **注** IPv6 IP アドレスがサポートされています。  IPv4 と IPv6 の両方を構成すると、それぞれ異なるサブネットとして扱われ、IPV6 がまずオンラインになることが想定されます。  
  
##### <a name="includessnoversionincludesssnoversion-mdmd-multi-subnet-failover-cluster"></a>[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] マルチサブネット フェールオーバー クラスター  
 クラスター上のノードが別々のサブネットにある場合、OR 依存関係を設定できます。 ただし、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] マルチサブネット フェールオーバー クラスターの各ノードが、指定されている 1 つ以上の IP アドレスの実行可能な所有者である必要があります。  
  
## <a name="see-also"></a>参照  
 [フェールオーバー クラスタリングをインストールする前に](../../../sql-server/failover-clusters/install/before-installing-failover-clustering.md)   
 [新しい SQL Server フェールオーバー クラスターの作成 &#40;セットアップ&#41;](../../../sql-server/failover-clusters/install/create-a-new-sql-server-failover-cluster-setup.md)   
 [コマンド プロンプトからの SQL Server 2016 のインストール](../../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)   
 [SQL Server フェールオーバー クラスター インスタンスのアップグレード](../../../sql-server/failover-clusters/windows/upgrade-a-sql-server-failover-cluster-instance.md)  
  
  
