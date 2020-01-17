---
title: SQL Server マルチサブネット クラスタリング (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- stretch cluster
- Availability Groups [SQL Server], WSFC clusters
- failover clustering [SQL Server], AlwaysOn Availability Groups
- multi-site failover cluster
- failover clustering [SQL Server]
ms.assetid: cd909612-99cc-4962-a8fb-e9a5b918e221
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: be4125f417b6333bfcb3002b15f1319f484d22a1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63049475"
---
# <a name="sql-server-multi-subnet-clustering-sql-server"></a>SQL Server マルチサブネット クラスタリング (SQL Server)
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] マルチサブネット フェールオーバー クラスターとは、各フェールオーバー クラスター ノードが異なるサブネットに接続されているか、異なるサブネットのセットに接続されている構成のことです。 これらのサブネットには、同じ場所や地理的に分散したサイトを指定できます。 地理的に分散したサイトのクラスタリングは、拡張クラスターと呼ばれることがあります。 すべてのノードがアクセスできる共有ストレージがないため、複数のサブネットのデータ ストレージ間でデータをレプリケートする必要があります。 データをレプリケートすることで、使用可能なデータのコピーが複数存在することになります。 そのため、マルチサブネット フェールオーバー クラスターによって、高可用性に加えてディザスター リカバリー ソリューションも実現します。  
  
 
  
##  <a name="VisualElement"></a> SQL Server マルチサブネット フェールオーバー クラスター (2 ノード、2 サブネット)  
 次の図は、2 ノード、2 サブネットの [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]のフェールオーバー クラスター インスタンス (FCI) を表します。  
  
 ![マルチ サブネット アーキテクチャと MultiSubnetFailover](../../../database-engine/media/multi-subnet-architecture-withmultisubnetfailoverparam.gif "マルチ サブネット アーキテクチャと MultiSubnetFailover")  
  

  
##  <a name="Configurations"></a> マルチサブネット フェールオーバー クラスター インスタンス構成  
 複数のサブネットを使用する [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] FCI の例を次に示します。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] FCI SQLCLUST1 には Node1 および Node2 が含まれます。 Node1 は Subnet1 に接続されています。 Node2 は Subnet2 に接続されています。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Setup ではこの構成をマルチサブネット クラスターと認識し、IP アドレス リソースの依存関係が **OR**に設定されます。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] FCI SQLCLUST1 には Node1、Node2 および Node3 が含まれます。 Node1 および Node2 は Subnet1 に接続されています。 Node 3 は Subnet2 に接続されています。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Setup ではこの構成をマルチサブネット クラスターと認識し、IP アドレス リソースの依存関係が **OR**に設定されます。 Node1 と Node2 が同じサブネット上にあるため、この構成ではローカルでの可用性が強化されます。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] FCI SQLCLUST1 には Node1 および Node2 が含まれます。 Node1 は Subnet1 に接続されています。 Node2 は Subnet1 および Subnet2 に接続されています。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Setup ではこの構成をマルチサブネット クラスターと認識し、IP アドレス リソースの依存関係が **OR**に設定されます。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] FCI SQLCLUST1 には Node1 および Node2 が含まれます。 Node1 は Subnet1 および Subnet2 に接続されています。 Node2 も Subnet1 および Subnet2 に接続されています。 IP アドレス リソースの依存関係は、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Setup によって **AND** に設定されています。  
  
    > [!NOTE]  
    >  クラスター ノードが同じサブネットのセットに含まれているため、この構成はマルチサブネット フェールオーバー クラスター構成と見なされません。  
  
##  <a name="ComponentsAndConcepts"></a> IP アドレス リソースに関する考慮事項  
 マルチサブネット フェールオーバー クラスターの構成では、フェールオーバー クラスター内のすべてのノードが IP アドレスを所有するわけではありません。また、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の起動時に一部のノードがオンラインにならない場合があります。 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]以降では、IP アドレス リソースの依存関係を **OR**に設定することができます。 そのため、バインドできる有効な IP アドレスが少なくとも 1 つ存在していれば、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] をオンラインにすることができます。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] より前のバージョンの [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] では、フェイル オーバー用の単一の IP アドレスをサイト全体に公開するために、マルチサイト クラスター構成で拡張 V-LAN テクノロジを使用していました。 異なるサブネットにわたるノードをクラスター化するための [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の新しい機能を使用することで、拡張 V-LAN テクノロジを実装することなく、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスターを複数のサイトを対象として構成できるようになりました。  
  
### <a name="ip-address-resource-or-dependency-considerations"></a>IP アドレス リソースの OR 依存関係に関する考慮事項  
 IP アドレス リソースの依存関係を **OR**に設定する場合、次のフェールオーバーの動作を考慮してください:  
  
-   現在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] クラスター リソース グループを所有しているノード上の IP アドレスの 1 つが使用不能な場合、そのノード上で有効なすべての IP アドレスが使用不能にならない限り、フェールオーバーが自動的に発生することはありません。  
  
-   フェールオーバーの発生時、現在のノード上で有効な少なくとも 1 つの IP アドレスにバインドできる限り、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] はオンラインになります。 起動時に [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] にバインドされなかった IP アドレスはエラー ログに表示されます。  
  
  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の FCI が [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)]のスタンドアロン インスタンスとサイド バイ サイドでインストールされている場合は、IP アドレスで TCP ポート番号が競合しないように注意してください。 競合は通常、 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] の 2 つのインスタンスが両方とも既定の TCP ポート (1433) を使用するように構成されている場合に発生します。 競合を回避するには、一方のインスタンスが既定以外の固定ポートを使用するように構成します。 通常、固定ポートの構成は、スタンドアロン インスタンスに対して行うのが最も簡単です。 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] で異なるポートが使用されるように構成すると、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の FCI がノードのスタンバイに失敗した場合に、予期しない IP アドレス/TCP ポート競合によってインスタンスの起動がブロックされる問題を回避できます。  
  
##  <a name="DNS"></a> フェールオーバー中のクライアント回復待機時間  
 複数サブネットの FCI 既定で RegisterAllProvidersIP のクラスター リソースのネットワーク名を有効にします。 マルチサブネット構成では、ネットワーク名のオンラインおよびオフライン両方の IP アドレスが DNS サーバーに登録されます。 クライアント アプリケーションは、すべての登録済み IP アドレスを DNS サーバーから取得し、受信した順序または並列で使用してアドレスへの接続を試みます。 つまり、マルチサブネット フェールオーバーのクライアント回復時間は DNS 更新の待機時間に依存しません。 既定では、クライアントは IP アドレスを順番に試行します。 クライアントが新しいオプションの `MultiSubnetFailover=True` パラメーターを接続文字列で使用している場合、IP アドレスを同時に試し、最初に応答したサーバーに接続します。 これにより、フェールオーバー発生時のクライアント回復待機時間を最小限に抑えることができます。 詳細については、次を参照してください。 [AlwaysOn クライアント接続 (SQL Server)](../../../database-engine/availability-groups/windows/always-on-client-connectivity-sql-server.md)と[可用性グループ リスナーの構成を作成または&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)します。  
  
 レガシ クライアント ライブラリまたはサードパーティ データ プロバイダーでは、接続文字列に `MultiSubnetFailover` パラメーターを使用できません。 クライアント アプリケーションが [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]のマルチサブネット FCI と最適な状態で連携して動作するように、クライアント接続文字列の接続タイムアウトを追加の IP アドレスごとに 21 秒で調整を試みてください。 これにより、クライアントの再接続の試みは、マルチサブネット FCI のすべての IP アドレスへの切り替えができるまでタイムアウトしません。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Management Studio および **sqlcmd** の既定のクライアント接続タイムアウト期間は 15 秒です。  
  
 
  
##  <a name="RelatedContent"></a> 関連コンテンツ  
  
|コンテンツの説明|トピック|  
|-------------------------|-----------|  
|SQL Server フェールオーバー クラスターのインストール|[新しい SQL Server フェールオーバー クラスターの作成 &#40;セットアップ&#41;](../install/create-a-new-sql-server-failover-cluster-setup.md)|  
|既存の SQL Server フェールオーバー クラスターのインプレース アップグレード|[SQL Server フェールオーバー クラスター インスタンスのアップグレード &#40;セットアップ&#41;](upgrade-a-sql-server-failover-cluster-instance-setup.md)|  
|既存の SQL Server フェールオーバー クラスターのメンテナンス|[SQL Server フェールオーバー クラスターでのノードの追加または削除 &#40;セットアップ&#41;](../install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)|  
|Windows フェールオーバー クラスタリング|[Microsoft Windows マルチサイト フェールオーバー クラスターのベスト プラクティス](https://secureinfra.blog/2013/11/09/microsoft-windows-multi-site-failover-cluster-best-practices/)|  
|フェールオーバー クラスターの管理スナップインを使用した WSFC のイベントおよびログの表示|[フェールオーバー クラスターのイベントおよびログを表示する](https://technet.microsoft.com/library/cc772342\(WS.10\).aspx)|  
|Windows PowerShell を使用した WSFC フェールオーバー クラスターのすべてのノード (または特定のノード) のログ ファイルの作成|[Get-ClusterLog フェールオーバー クラスター コマンドレット](https://technet.microsoft.com/library/ee461045.aspx)|  
  
 
  
  
