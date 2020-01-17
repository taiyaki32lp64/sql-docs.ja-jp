---
title: フェールオーバー クラスタ リングと AlwaysOn 可用性グループ (SQL Server) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- clustering [SQL Server]
- Availability Groups [SQL Server], WSFC clusters
- Failover Cluster Instances [SQL Server], see failover clustering [SQL Server]
- quorum [SQL Server]
- failover clustering [SQL Server], AlwaysOn Availability Groups
- Availability Groups [SQL Server], Failover Cluster Instances
ms.assetid: 613bfbf1-9958-477b-a6be-c6d4f18785c3
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e8d4858d55d9c37529e44cdf7759bf9fe6ce2630
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62792005"
---
# <a name="failover-clustering-and-alwayson-availability-groups-sql-server"></a>フェールオーバー クラスタリングと AlwaysOn 可用性グループ (SQL Server)
  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] で導入された[!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]高可用性ディザスター リカバリー ソリューションには、Windows Server フェールオーバー クラスタリング (WSFC) が必要です。 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] フェールオーバー クラスタリングには依存しませんが、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] は、フェールオーバー クラスタリング インスタンス (FCI) を使用して、可用性グループの可用性レプリカをホストすることもできます。 実際に [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 環境を設計する際は、それぞれのクラスタリング テクノロジの役割を知り、注意点を把握しておくことが大切です。  
  
> [!NOTE]  
>  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] の概念については、「[AlwaysOn 可用性グループの概要 &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)」を参照してください。  
  

  
##  <a name="WSFC"></a> Windows Server フェールオーバー クラスタリングと可用性グループ  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] を配置するには、Windows Server フェールオーバー クラスタリング (WSFC) クラスターが必要です。 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]を有効にするには、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスが WSFC ノード上に存在し、WSFC クラスターとノードがオンライン状態である必要があります。 さらに、特定の可用性グループの各可用性レプリカが、同じ WSFC クラスターの異なるノード上に存在する必要があります。 唯一の例外は、別の WSFC クラスターに移行するときに、可用性グループは一時的に 2 つのクラスターにまたがることができるという点です。  
  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 特定の可用性グループに属している可用性レプリカの現在のロールを監視、管理したり、フェールオーバー イベントが可用性レプリカに及ぼす影響を判断したりするために、では Windows Server フェールオーバー クラスタリング (WSFC) クラスターが使用されます。 WSFC リソース グループは、作成されたすべての可用性グループに対して作成されます。 WSFC クラスターは、このリソース グループを監視して、プライマリ レプリカの正常性を評価します。  
  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] のクォーラムは、クラスター ノードが可用性レプリカをホストしているかどうかに関係なく、WSFC クラスター内のすべてのノードに基づきます。 データベース ミラーリングとは異なり、 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]には監視ロールはありません。  
  
 WSFC クラスターの全体的な正常性は、クラスター内のノードのクォーラムの投票によって決定されます。 災害や永続的なハードウェア障害または通信障害が原因で WSFC クラスターがオフラインになった場合は、管理操作を手動で行う必要があります。 Windows Server または WSFC クラスターの管理者は、クォーラムを強制し、稼動しているクラスター ノードをフォールト トレラントではない構成でオンラインに戻す必要があります。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] レジストリ キーは WSFC クラスターのサブキーです。 WSFC クラスターを削除してから再作成した場合は、元の WSFC クラスター上の可用性レプリカをホストしていた [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] の各インスタンスについて、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 機能を無効にしてから再度有効にする必要があります。  
  
 Windows Server フェールオーバー クラスタリング (WSFC) ノードでの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の実行および WSFC クォーラムについては、「[Windows Server フェールオーバー クラスタリング &#40;WSFC&#41;  と SQL Server](../../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md)」を参照してください。  
  
### <a name="cross-cluster-migration-of-alwayson-availability-groups-for-os-upgrade"></a>OS アップグレードのための AlwaysOn 可用性グループのクラスター間での移行  
 [!INCLUDE[ssSQL11SP1](../../../includes/sssql11sp1-md.md)] から、[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]では、新しい Windows Server フェールオーバー クラスタリング (WSFC) クラスターに配置するために行う可用性グループのクラスター間での移行が新たにサポートされています。 クラスター間の移行では、ダウンタイムを最小限に抑えながら、1 つの可用性グループを (または複数の可用性グループを一括して) 新しい移行先 WSFC クラスターに移行します。 クラスター間の移行プロセスを使用すると、 [!INCLUDE[win8srv](../../../includes/win8srv-md.md)] クラスターへのアップグレード時にサービス レベル契約 (SLA) を維持できます。 移行先の WSFC クラスターに [!INCLUDE[ssSQL11SP1](../../../includes/sssql11sp1-md.md)] (またはそれ以降のバージョン) をインストールし、AlwaysOn 用に有効にする必要があります。 クラスター間での移行を成功させるには、移行先 WSFC クラスターを綿密に計画し、準備することが必要です。  
  
 詳細については、「[OS アップグレードのための AlwaysOn 可用性グループのクラスター間での移行](https://msdn.microsoft.com/library/jj873730.aspx)」を参照してください。  
  
##  <a name="SQLServerFC"></a> [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスター インスタンス (FCI) と可用性グループ  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスタリングを WSFC クラスターと共に実装することにより、サーバー インスタンス レベルで第 2 のフェールオーバー レイヤーをセットアップできます。 可用性レプリカは、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のスタンドアロン インスタンスまたは FCI インスタンスでホストできます。 特定の可用性グループのレプリカをホストできる FCI パートナーは 1 つに限られます。 可用性レプリカが FCI で実行されている場合、可用性グループの有効な所有者の一覧には、アクティブな FCI ノードだけが含まれます。  
  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] は、共有ストレージの形態には依存しません。 ただし、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスター インスタンス (FCI) を使用して 1 つまたは複数の可用性レプリカをホストする場合、各 FCI では標準の SQL Server フェールオーバー クラスター インスタンスのインストールと同様、共有ストレージが必要になります。  
  
 追加の前提条件の詳細については、「[AlwaysOn 可用性グループの前提条件、制限事項、および推奨事項 &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md)」の「SQL Server のフェールオーバー クラスター インスタンス (FCI) を使用して可用性レプリカをホストするための前提条件と制限」を参照してください。  
  
### <a name="comparison-of-failover-cluster-instances-and-availability-groups"></a>フェールオーバー クラスター インスタンスと可用性グループの比較  
 FCI のノードの数に関係なく、FCI 全体は可用性グループ内の 1 つのレプリカをホストします。 次の表に、FCI 内のノードと可用性グループ内のレプリカの概念の違いについて説明します。  
  
||FCI 内のノード|可用性グループ内のレプリカ|  
|-|-------------------------|-------------------------------------------|  
|**WSFC クラスターを使用する**|はい|はい|  
|**保護レベル**|Instance|[データベース]|  
|**ストレージの種類**|Shared|非共有<br /><br /> 可用性グループ内のレプリカがストレージを共有しない一方、FCI によってホストされるレプリカは、FCI によって必要とされたときに共有ストレージ ソリューションを使用することに注意してください。 ストレージ ソリューションは、可用性グループのレプリカ間ではなく、FCI 内のノードでのみ共有されます。|  
|**ストレージ ソリューション**|直接接続、SAN、マウント ポイント、SMB|ノードの種類によって異なる|  
|**読み取り可能なセカンダリ**|なし*|はい|  
|**該当するフェールオーバー ポリシー設定**|WSFC クォーラム<br /><br /> FCI 固有<br /><br /> 可用性グループ設定**|WSFC クォーラム<br /><br /> 可用性グループ設定|  
|**フェールオーバー リソース**|サーバー、インスタンス、およびデータベース|データベースのみ|  
  
 *可用性グループ内の同期セカンダリ レプリカは、常に対応する [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンス上で実行されていますが、FCI 内のセカンダリ ノードは、実際には対応する [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスを起動していないため、読み取り不可能です。 FCI 内のセカンダリ ノードは、FCI フェールオーバー中にリソース グループの所有権が転送されたときにのみ、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスを起動します。 ただし、アクティブな FCI ノードにおいて、FCI によってホストされるデータベースが可用性グループに属している場合にローカルな可用性グループが読み取り可能なセカンダリ レプリカとして実行されていると、データベースは読み取り可能です。  
  
 **可用性グループのフェールオーバー ポリシー設定は、スタンドアロン インスタンスと FCI インスタンスのどちらでホストされているかに関係なく、すべてのレプリカに適用されます。  
  
> [!NOTE]  
>  詳細については**ノード数**フェールオーバー クラスタ リング内と**AlwaysOn 可用性グループ**の各エディションの[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]を参照してください[でサポートされる機能、SQL Server 2012 の各エディション](https://go.microsoft.com/fwlink/?linkid=232473)(https://go.microsoft.com/fwlink/?linkid=232473) します。  
  
### <a name="considerations-for-hosting-an-availability-replica-on-an-fci"></a>FCI で可用性レプリカをホストする場合の考慮事項  
  
> [!IMPORTANT]  
>  SQL Server フェールオーバー クラスター インスタンス (FCI) で可用性レプリカをホストすることを計画している場合は、Windows Server 2008 ホスト ノードが AlwaysOn の前提条件およびフェールオーバー クラスター インスタンス (FCI) の制限を満たしていることを確認してください。 詳細については、「[AlwaysOn 可用性グループの前提条件、制限事項、および推奨事項 &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md)」を参照してください。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスター インスタンス (FCI) は可用性グループによる自動フェールオーバーをサポートしないため、FCI によってホストされる可用性レプリカは手動フェールオーバー用にのみ構成できます。  
  
 場合により、すべてのノードで使用できな共有ディスクを含めるように Windows Server フェールオーバー クラスタリング (WSFC) クラスターを構成する必要があります。 たとえば、3 つのノードを持つ 2 つのデータ センター間の WSFC クラスターを検討します。 ノードのうちの 2 つは、プライマリ データ センター内の SQL Server フェールオーバー クラスタリング インスタンス (FCI) をホストし、同じ共有ディスクにアクセスできます。 3 つ目のノードは、別のデータ センター内の SQL Server のスタンドアロン インスタンスをホストし、プライマリ データ センターの共有ディスクにはアクセスできません。 この WSFC クラスター構成では、FCI でプライマリ レプリカがホストされ、スタンドアロン インスタンスでセカンダリ レプリカがホストされる場合に可用性グループの配置がサポートされます。  
  
 特定の可用性グループの可用性レプリカをホストするために FCI を選択する場合は、FCI フェールオーバーによって 1 つの WSFC ノードで同じ可用性グループの 2 つの可用性レプリカをホストする操作が試行されないように注意してください。  
  
 この構成によってどのような問題が起きるかを次のサンプル シナリオに示します。  
  
 Marcel は、 `NODE01` と `NODE02`の 2 つのノードから成る WSFC クラスターを構成しています。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスター インスタンス `fciInstance1`は、 `NODE01` と `NODE02` の両方にインストールされています。 `NODE01` の現在の所有者は `fciInstance1`です。  
 Marcel は、 `NODE02`に、別の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]インスタンス `Instance3`をインストールすることにしました。Instance3 はスタンドアロン インスタンスです。  
 Marcel は、 `NODE01`で、fciInstance1 に対する [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]を有効にしました。 `NODE02`では、 `Instance3` に対する [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]を有効にしました。 さらに、可用性グループをセットアップしました。この可用性グループは、 `fciInstance1` がプライマリ レプリカをホストするためだけでなく、 `Instance3` がセカンダリ レプリカをホストするためにも使用されます。  
 あるとき、 `fciInstance1` 上の `NODE01`が利用できなくなり、WSFC クラスターによって、 `fciInstance1` が `NODE02`にフェールオーバーされたとします。 フェールオーバー後の `fciInstance1` は、 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]上でプライマリ ロールとして動作する `NODE02`対応のインスタンスです。 しかし、この時点で `Instance3` は、 `fciInstance1`と同じ WSFC ノードに存在します。 これは [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] の制約に違反します。  
 このシナリオで起きる問題を回避するには、スタンドアロン インスタンス (`Instance3`) が、`NODE01` や `NODE02` と同じ WSFC クラスター内の別のノードに存在している必要があります。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスタリングの詳細については、「[AlwaysOn フェールオーバー クラスター インスタンス &#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md)」を参照してください。  
  
##  <a name="FCMrestrictions"></a> WSFC フェールオーバー クラスター マネージャーを使用した可用性グループの操作に関する制限事項  
 フェールオーバー クラスター マネージャーを使用して可用性グループを操作しないでください。次に例を示します。  
  
-   可用性グループのクラスター化されたサービス (リソース グループ) のリソースの追加や削除を行わないでください。  
  
-   可用性グループのプロパティ (たとえば、有効な所有者、優先所有者) を変更しないでください。 これらのプロパティは、可用性グループによって自動的に設定されます。  
  
-   フェールオーバー クラスター マネージャーを使用して可用性グループを他のノードに移動したり可用性グループをフェールオーバーしたりしないでください。 フェールオーバー クラスターは可用性レプリカの同期状態を認識しないため、そのような操作を行うとダウンタイムが長くなることがあります。 [!INCLUDE[tsql](../../../includes/tsql-md.md)] または [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]を使用する必要があります。  
  
##  <a name="RelatedContent"></a> 関連コンテンツ  
  
-   **ブログ:**  
  
     [制限付きセキュリティを使用した SQL Server 用 Windows フェールオーバー クラスタリング (可用性グループまたは FCI) の構成](https://blogs.msdn.com/b/sqlalwayson/archive/2012/06/05/configure-windows-failover-clustering-for-sql-server-availability-group-or-fci-with-limited-security.aspx)  
  
     [SQL Server AlwaysOn チームのブログ:SQL Server AlwaysOn チームのオフィシャル ブログ](https://blogs.msdn.com/b/sqlalwayson/)  
  
     [CSS SQL Server エンジニアのブログ](https://blogs.msdn.com/b/psssql/)  
  
-   **ホワイト ペーパー:**  
  
     [AlwaysOn アーキテクチャ ガイド:フェールオーバー クラスター インスタンスと可用性グループの使用による高可用性およびディザスター リカバリー ソリューションの構築](https://msdn.microsoft.com/library/jj215886.aspx)  
  
     [Microsoft SQL Server AlwaysOn ソリューション ガイド高可用性とディザスター リカバリー](https://go.microsoft.com/fwlink/?LinkId=227600)  
  
     [SQL Server 2012 に関する Microsoft ホワイト ペーパー](https://msdn.microsoft.com/library/hh403491.aspx)  
  
     [SQL Server ユーザー諮問チームのホワイト ペーパー](http://sqlcat.com/)  
  
## <a name="see-also"></a>参照  
 [AlwaysOn 可用性グループの概要&#40;SQL Server&#41; ](overview-of-always-on-availability-groups-sql-server.md) [を有効にして、AlwaysOn 可用性グループを無効にする&#40;SQL Server&#41; ](enable-and-disable-always-on-availability-groups-sql-server.md) [&#40;TRANSACT-SQL&#41;](monitor-availability-groups-transact-sql.md)  
 [AlwaysOn フェールオーバー クラスター インスタンス&#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md) 
  
  
