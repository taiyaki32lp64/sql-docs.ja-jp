---
title: フェールオーバー クラスター インスタンスと可用性グループ
description: SQL Server フェールオーバー クラスター インスタンスと Always On 可用性グループの機能を組み合わせることで、高可用性とディザスター リカバリーを向上させることができます。
ms.custom: seo-lt-2019
ms.date: 07/02/2017
ms.prod: sql
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
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 62b5f1d23608ce6337befa1e4888ad2cda543dc9
ms.sourcegitcommit: f8cf8cc6650a22e0b61779c20ca7428cdb23c850
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/04/2019
ms.locfileid: "74822254"
---
# <a name="failover-clustering-and-always-on-availability-groups-sql-server"></a>フェールオーバー クラスタリングと Always On 可用性グループ (SQL Server)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

   [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] で導入された [!INCLUDE[sssql11](../../../includes/sssql11-md.md)] (High Availability and Disaster Recovery) ソリューションには、Windows Server フェールオーバー クラスタリング (WSFC) が必要です。 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] フェールオーバー クラスタリングには依存しませんが、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] は、フェールオーバー クラスタリング インスタンス (FCI) を使用して、可用性グループの可用性レプリカをホストすることもできます。 実際に [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 環境を設計する際は、それぞれのクラスタリング テクノロジの役割を知り、注意点を把握しておくことが大切です。  
  
> [!NOTE]  
>  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] の概念については、「[Always On 可用性グループの概要 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)」を参照してください。  
  
  
##  <a name="WSFC"></a> Windows Server フェールオーバー クラスタリングと可用性グループ  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] を配置するには、Windows Server フェールオーバー クラスター (WSFC) が必要です。 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]を有効にするには、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスが WSFC ノード上に存在し、WSFC とノードがオンライン状態である必要があります。 さらに、特定の可用性グループの各可用性レプリカが、同じ WSFC の異なるノード上に存在する必要があります。 唯一の例外は、別の WSFC に移行するときに、可用性グループは一時的に 2 つのクラスターにまたがることができるという点です。  
  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] では、特定の可用性グループに属している可用性レプリカの現在のロールを監視、管理したり、フェールオーバー イベントが可用性レプリカに及ぼす影響を判断したりするために、Windows Server フェールオーバー クラスター (WSFC) が使用されます。 WSFC リソース グループは、作成されたすべての可用性グループに対して作成されます。 WSFC は、このリソース グループを監視して、プライマリ レプリカの正常性を評価します。  
  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] のクォーラムは、クラスター ノードが可用性レプリカをホストしているかどうかに関係なく、WSFC 内のすべてのノードに基づきます。 データベース ミラーリングとは異なり、 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]には監視ロールはありません。  
  
 WSFC の全体的な正常性は、クラスター内のノードのクォーラムの投票によって決定されます。 災害や永続的なハードウェア障害または通信障害が原因で WSFC がオフラインになった場合は、管理操作を手動で行う必要があります。 Windows Server または WSFC の管理者は、クォーラムを強制し、稼動しているクラスター ノードをフォールト トレラントではない構成でオンラインに戻す必要があります。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] レジストリ キーは WSFC のサブキーです。 WSFC を削除してから再作成した場合は、元の WSFC 上の可用性レプリカをホストしていた [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] の各インスタンスについて、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 機能を無効にしてから再度有効にする必要があります。  
  
 WSFC ノードでの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の実行および WSFC クォーラムについては、[Windows Server フェールオーバー クラスタリング &#40;WSFC&#41; と SQL Server](../../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md)に関するページを参照してください。  
  
##  <a name="SQLServerFC"></a> [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスター インスタンス (FCI) と可用性グループ  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] FCI を WSFC と共に実装することにより、サーバー インスタンス レベルで第 2 のフェールオーバー レイヤーをセットアップできます。 可用性レプリカは、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のスタンドアロン インスタンスまたは FCI インスタンスでホストできます。 特定の可用性グループのレプリカをホストできる FCI パートナーは 1 つに限られます。 可用性レプリカが FCI で実行されている場合、可用性グループの有効な所有者の一覧には、アクティブな FCI ノードだけが含まれます。  
  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] は、共有ストレージの形態には依存しません。 ただし、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスター インスタンス (FCI) を使用して 1 つまたは複数の可用性レプリカをホストする場合、各 FCI では標準の SQL Server フェールオーバー クラスター インスタンスのインストールと同様、共有ストレージが必要になります。  
  
 追加の前提条件の詳細については、「[Always On 可用性グループの前提条件、制限事項、および推奨事項 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)」の「SQL Server のフェールオーバー クラスター インスタンス (FCI) を使用して可用性レプリカをホストするための前提条件と制限」を参照してください。  
  
### <a name="comparison-of-failover-cluster-instances-and-availability-groups"></a>フェールオーバー クラスター インスタンスと可用性グループの比較  
 FCI のノードの数に関係なく、FCI 全体は可用性グループ内の 1 つのレプリカをホストします。 次の表に、FCI 内のノードと可用性グループ内のレプリカの概念の違いについて説明します。  
  
||FCI 内のノード|可用性グループ内のレプリカ|  
|-|-------------------------|-------------------------------------------|  
|**WSFC を使用する**|はい|はい|  
|**保護レベル**|インスタンス|データベース|  
|**ストレージの種類**|共有|非共有<br /><br /> 可用性グループ内のレプリカがストレージを共有しない一方、FCI によってホストされるレプリカは、FCI によって必要とされたときに共有ストレージ ソリューションを使用します。 ストレージ ソリューションは、可用性グループのレプリカ間ではなく、FCI 内のノードでのみ共有されます。|  
|**ストレージ ソリューション**|直接接続、SAN、マウント ポイント、SMB|ノードの種類によって異なる|  
|**読み取り可能なセカンダリ**|いいえ*|はい|  
|**該当するフェールオーバー ポリシー設定**|WSFC クォーラム<br /><br /> FCI 固有<br /><br /> 可用性グループ設定**|WSFC クォーラム<br /><br /> 可用性グループの設定|  
|**フェールオーバー リソース**|サーバー、インスタンス、およびデータベース|データベースのみ|  
  
 *可用性グループ内の同期セカンダリ レプリカは、常に対応する [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンス上で実行されていますが、FCI 内のセカンダリ ノードは、実際には対応する [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスを起動していないため、読み取り不可能です。 FCI 内のセカンダリ ノードは、FCI フェールオーバー中にリソース グループの所有権が転送されたときにのみ、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスを起動します。 ただし、アクティブな FCI ノードにおいて、FCI によってホストされるデータベースが可用性グループに属している場合にローカルな可用性グループが読み取り可能なセカンダリ レプリカとして実行されていると、データベースは読み取り可能です。  
  
 **可用性グループのフェールオーバー ポリシー設定は、スタンドアロン インスタンスと FCI インスタンスのどちらでホストされているかに関係なく、すべてのレプリカに適用されます。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]の各エディションにおける FCI 内の**ノード数**および **Always On 可用性グループ**の詳細については、「[SQL Server 2012 の各エディションがサポートする機能](https://go.microsoft.com/fwlink/?linkid=232473)」(https://go.microsoft.com/fwlink/?linkid=232473) を参照してください。  
  
### <a name="considerations-for-hosting-an-availability-replica-on-an-fci"></a>FCI で可用性レプリカをホストする場合の考慮事項  
  
> [!IMPORTANT]  
>  SQL Server フェールオーバー クラスター インスタンス (FCI) で可用性レプリカをホストすることを計画している場合は、Windows Server 2008 ホスト ノードが Always On の前提条件およびフェールオーバー クラスター インスタンス (FCI) の制限を満たしていることを確認してください。 詳細については、「 [Always On 可用性グループの前提条件、制限事項、および推奨事項 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)の構成に関する一般的な問題のトラブルシューティングに役立つ情報を提供します。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスター インスタンス (FCI) は可用性グループによる自動フェールオーバーをサポートしないため、FCI によってホストされる可用性レプリカは手動フェールオーバー用にのみ構成できます。  
  
 場合により、すべてのノードで使用できない共有ディスクを含めるように WSFC を構成する必要があります。 たとえば、3 つのノードを持つ 2 つのデータ センター間の WSFC を検討します。 ノードのうちの 2 つは、プライマリ データ センター内の SQL Server フェールオーバー クラスター インスタンス (FCI) をホストし、同じ共有ディスクにアクセスできます。 3 つ目のノードは、別のデータ センター内の SQL Server のスタンドアロン インスタンスをホストし、プライマリ データ センターの共有ディスクにはアクセスできません。 この WSFC 構成では、FCI でプライマリ レプリカがホストされ、スタンドアロン インスタンスでセカンダリ レプリカがホストされる場合に可用性グループの配置がサポートされます。  
  
 特定の可用性グループの可用性レプリカをホストするために FCI を選択する場合は、FCI フェールオーバーによって 1 つの WSFC ノードで同じ可用性グループの 2 つの可用性レプリカをホストする操作が試行されないように注意してください。  
  
 この構成によってどのような問題が起きるかを次のサンプル シナリオに示します。  
  
 Marcel は、`NODE01` と `NODE02` の 2 つのノードから成る WSFC を構成しています。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスター インスタンス `fciInstance1`は、 `NODE01` と `NODE02` の両方にインストールされています。 `NODE01` の現在の所有者は `fciInstance1`です。  
 Marcel は、 `NODE02`に、別の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]インスタンス `Instance3`をインストールすることにしました。Instance3 はスタンドアロン インスタンスです。  
 Marcel は、 `NODE01`で、fciInstance1 に対する [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]を有効にしました。 `NODE02`では、 `Instance3` に対する [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]を有効にしました。 さらに、可用性グループをセットアップしました。この可用性グループは、 `fciInstance1` がプライマリ レプリカをホストするためだけでなく、 `Instance3` がセカンダリ レプリカをホストするためにも使用されます。  
 あるとき、`fciInstance1` 上の `NODE01` が利用できなくなり、WSFC によって `fciInstance1` が `NODE02` にフェールオーバーされたとします。 フェールオーバー後の `fciInstance1` は、 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]上でプライマリ ロールとして動作する `NODE02`対応のインスタンスです。 しかし、この時点で `Instance3` は、 `fciInstance1`と同じ WSFC ノードに存在します。 これは [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] の制約に違反します。  
 このシナリオで起きる問題を回避するには、スタンドアロン インスタンス ( `Instance3`) が、`NODE01` や `NODE02` と同じ WSFC 内の別のノードに存在している必要があります。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] FCI の詳細については、「[Always On フェールオーバー クラスター インスタンス &#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md)」を参照してください。  
  
##  <a name="FCMrestrictions"></a> WSFC フェールオーバー クラスター マネージャーを使用した可用性グループの操作に関する制限事項  
 フェールオーバー クラスター マネージャーを使用して可用性グループを操作しないでください。次に例を示します。  
  
-   可用性グループのクラスター化されたサービス (リソース グループ) のリソースの追加や削除を行わないでください。  
  
-   可用性グループのプロパティ (たとえば、有効な所有者、優先所有者) を変更しないでください。 これらのプロパティは、可用性グループによって自動的に設定されます。  
  
-   **フェールオーバー クラスター マネージャーを使用して可用性グループを他のノードに移動したり可用性グループをフェールオーバーしたりしないでください。** フェールオーバー クラスターは可用性レプリカの同期状態を認識しないため、そのような操作を行うとダウンタイムが長くなることがあります。 [!INCLUDE[tsql](../../../includes/tsql-md.md)] または [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]を使用する必要があります。  

  >[!WARNING]
  > フェールオーバー クラスター マネージャーを使用して、可用性グループをホストしている*フェールオーバー クラスター インスタンス*を、同じ可用性グループのレプリカを "*すでに*" ホストしているノードに移動すると、可用性グループのレプリカが失われ、それによってターゲット ノード上でオンラインにできなくなる可能性があります。 フェールオーバー クラスターの 1 つのノードでは、同じ可用性グループの複数のレプリカをホストすることはできません。 これがどのように発生し、どのように回復するかの詳細については、ブログ記事の「[Replica unexpectedly dropped in availability group](https://blogs.msdn.microsoft.com/alwaysonpro/2014/02/03/issue-replica-unexpectedly-dropped-in-availability-group/)」(可用性グループでレプリカが予想外に削除される) を参照してください。 
  
##  <a name="RelatedContent"></a> 関連コンテンツ  
  
-   **ブログ:**  
  
     [制限付きセキュリティを使用した SQL Server 用 Windows フェールオーバー クラスタリング (可用性グループまたは FCI) の構成](https://blogs.msdn.microsoft.com/sqlalwayson/2012/06/05/configure-windows-failover-clustering-for-sql-server-availability-group-or-fci-with-limited-security/)  
  
     [SQL Server Always On チーム ブログ:SQL Server Always On チームのオフィシャル ブログ](https://blogs.msdn.microsoft.com/sqlalwayson/)  
  
     [CSS SQL Server エンジニアのブログ](https://blogs.msdn.com/b/psssql/)  
  
-   **ホワイト ペーパー:**  
  
     [Always On アーキテクチャ ガイド:フェールオーバー クラスター インスタンスと可用性グループの使用による高可用性およびディザスター リカバリー ソリューションの構築](https://msdn.microsoft.com/library/jj215886.aspx)  
  
     [高可用性と災害復旧のための Microsoft SQL Server AlwaysOn ソリューション ガイド](https://go.microsoft.com/fwlink/?LinkId=227600)  
  
     [SQL Server 2012 に関する Microsoft ホワイト ペーパー](https://msdn.microsoft.com/library/hh403491.aspx)  
  
     [SQL Server ユーザー諮問チームのホワイト ペーパー](https://techcommunity.microsoft.com/t5/DataCAT/bg-p/DataCAT/)  
  
## <a name="see-also"></a>参照  
 [AlwaysOn 可用性グループの概要 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [AlwaysOn 可用性グループの有効化と無効化 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md)   
 [可用性グループの監視 &#40;Transact-SQL&#41;](../../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [Always On フェールオーバー クラスター インスタンス &#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md)  
  
  
