---
title: Always On フェールオーバー クラスター インスタンス (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- clustering [SQL Server]
- high availability [SQL Server], failover clustering
- virtual servers [SQL Server], about virtual servers
- clusters [SQL Server]
- servers [SQL Server], failover clustering
- resource groups [SQL Server]
- availability [SQL Server]
- failover clustering [SQL Server]
- AlwaysOn [SQL Server], see failover clustering [SQL Server]
ms.assetid: 86a15b33-4d03-4549-8ea2-b45e4f1baad7
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: feceb314570449173b5ffc03869e5e3ad06906d9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68063802"
---
# <a name="always-on-failover-cluster-instances-sql-server"></a>Always On フェールオーバー クラスター インスタンス (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Always On 製品の一部として、Always On フェールオーバー クラスター インスタンスでは、Windows Server フェールオーバー クラスタリング (WSFC) の機能を活用して、サーバー インスタンス レベル (*フェールオーバー クラスター インスタンス* (FCI)) での冗長性によるローカル高可用性を実現します。 FCI は、Windows Server フェールオーバー クラスタリング (WSFC) ノード全体、場合によっては複数のサブネットにインストールされる [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の単一インスタンスです。 FCI は、ネットワーク上では 1 台のコンピューターで実行されている [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスのように見えますが、現在のノードが使用できなくなった場合には、1 つの WSFC ノードから別の WSFC ノードにフェールオーバーする機能を備えています。  
  
 FCI は、[可用性グループ](../../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)を活用して、データベース レベルでのリモートのディザスター リカバリーを実現します。 詳細については、「[Failover Clustering and Always On Availability Groups (SQL Server) (フェールオーバー クラスタリングと可用性グループ &#40;SQL Server&#41;)](../../../database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server.md)」をご覧ください。  
 
 > [!NOTE]  
 > Windows Server 2016 Datacenter Edition には、記憶域スペース ダイレクト (S2D) のサポートが導入されています。 SQL Server フェールオーバー クラスター インスタンスは、クラスター ストレージ リソース向けの S2D をサポートしています。 詳細については、「[Windows Server 2016 の記憶域スペース ダイレクト](https://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview)」を参照してください。
 > 
 >フェールオーバー クラスター インスタンスは、クラスター化共有ボリューム (CSV) もサポートしています。 詳細については、「 [フェールオーバー クラスターのクラスターの共有ボリュームについて](https://technet.microsoft.com/library/dd759255.aspx)」を参照してください。 
   
 **このトピックの内容**  
  
-   [利点](#Benefits)  
  
-   [推奨事項](#Recommendations)  
  
-   [フェールオーバー クラスター インスタンスの概要](#Overview)  
  
-   [フェールオーバー クラスター インスタンスの構成要素](#FCIelements)  
  
-   [SQL Server フェールオーバーの概念とタスク](#ConceptsAndTasks)  
  
-   [関連項目](#RelatedTopics)  
  
##  <a name="Benefits"></a> フェールオーバー クラスター インスタンスの利点  
 サーバーのハードウェアまたはソフトウェアに障害が発生すると、そのサーバーに接続しているアプリケーションまたはクライアントで、ダウンタイムが発生します。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスが (スタンドアロン インスタンスではなく) FCI として構成されている場合、その [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスの高可用性は、FCI の冗長ノードの存在によって保護されます。 一度に FCI 内のノードの 1 つだけが WSFC リソース グループを所有します。 障害 (ハードウェア、オペレーティング システム、アプリケーション、サービスなどの障害) が発生した場合や計画していたアップグレードが行われる場合は、リソース グループの所有権が別の WSFC ノードに移動します。 この処理は、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] に接続しているクライアントまたはアプリケーションに認識されることなく実行され、これによって障害発生中のアプリケーションおよびクライアントのダウンタイムを最小限に抑えることができます。 次の一覧は、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスター インスタンスの主な利点を示しています。  
  
-   冗長性によるインスタンス レベルの保護  
  
-   障害 (ハードウェア、オペレーティング システム、アプリケーション、サービスなどの障害) 発生時の自動フェールオーバー  
  
    > [!IMPORTANT]  
    >  可用性グループでは、FCI から可用性グループ内の他のノードへの自動フェールオーバーはサポートされていません。 このため、自動フェールオーバーが高可用性ソリューションの重要なコンポーネントである場合は、FCI とスタンドアロン ノードを 1 つの可用性グループ内で組み合わせて使用することはできません。 ただし、*ディザスター リカバリー* ソリューションではこの組み合わせを使用できます。  
  
-   WSFC クラスター ディスク (iSCSI、ファイバー チャネルなど) やサーバー メッセージ ブロック (SMB) ファイル共有などのさまざまなストレージ ソリューションのサポート。  
  
-   マルチサブネット FCI を使用している、または FCI によってホストされるデータベースを可用性グループ内で実行している災害復旧ソリューション。 [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]の新しいマルチサブネット サポートでは、マルチサブネット FCI に仮想 LAN が不要になり、マルチサブネット FCI の管理性とセキュリティが向上します。  
  
-   フェールオーバー時にアプリケーションとクライアントの再構成が不要  
  
-   自動フェールオーバーの詳細なトリガー イベント用の柔軟なフェールオーバー ポリシー  
  
-   専用接続および永続接続を使用した定期的および詳細な正常性状態の検出による信頼性の高いフェールオーバー  
  
-   間接バックグラウンド チェックポイントによりフェールオーバー時に構成と予測が可能  
  
-   フェールオーバー時のリソース使用状況を調整  
  
##  <a name="Recommendations"></a> 推奨事項  
 実稼働環境では、静的 IP アドレスをフェールオーバー クラスター インスタンスの仮想 IP アドレスと組み合わせて使用することをお勧めします。  実稼働環境で DHCP を使用することはお勧めしません。 ダウンタイムが発生した場合に DHCP の IP リース期限が切れると、DNS 名に関連付けられている新しい DHCP IP アドレスの再登録に余分な時間がかかります。  
  
##  <a name="Overview"></a> フェールオーバー クラスター インスタンスの概要  
 FCI は、1 つ以上の WSFC ノードのある WSFC リソース グループで実行します。 FCI が起動すると、ノードの 1 つがリソース グループの所有権を引き受け、その [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスをオンラインにします。 このノードが所有するリソースは次のとおりです。  
  
-   ネットワーク名  
  
-   IP アドレス (IP address)  
  
-   共有ディスク  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データベース エンジン サービス  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] エージェント サービス  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Analysis Service サービス (インストールされている場合)  
  
-   1 つのファイル共有リソース (FILESTREAM 機能がインストールされている場合)  
  
 任意の時点で、リソース グループ所有者だけがリソース グループ内のそれぞれの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サービスを実行しています (FCI の他のノードでは実行されません)。 フェールオーバーが発生すると、それが自動フェールオーバーと計画的フェールオーバーのいずれであるかにかかわらず、次の一連のイベントが発生します。  
  
1.  ハードウェアまたはシステムの障害が発生しない限り、バッファー キャッシュ内のすべてのダーティ ページがディスクに書き込まれます。  
  
2.  リソース グループ内のそれぞれの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サービスが、すべてアクティブ ノードで停止されます。  
  
3.  リソース グループの所有権が FCI の別のノードに転送されます。  
  
4.  新しいリソース グループ所有者が [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サービスを開始します。  
  
5.  クライアント アプリケーション接続要求が、同じ仮想ネットワーク名 (VNN) を使用して新しいアクティブ ノードに自動的に送られます。  
  
 FCI は、基になる WSFC クラスターが正常なクォーラム状態にある限りオンラインになります (クォーラム WSFC ノードの大半は、自動フェールオーバー ターゲットとして使用できます)。 WSFC クラスターがクォーラムを失うと、その原因がハードウェア、ソフトウェア、ネットワーク障害であるか、不適切なクォーラム構成であるかにかかわらず、WSFC クラスター全体が FCI と共にオフラインになります。 この予定外のフェールオーバー シナリオでは、WSFC クラスターと FCI をオンラインに戻すために、手動介入によって残りの使用可能ノードでクォーラムを再確立する必要があります。 詳細については、「[WSFC クォーラム モードと投票の構成 &#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/wsfc-quorum-modes-and-voting-configuration-sql-server.md)」をご覧ください。  
  
### <a name="predictable-failover-time"></a>予測可能なフェールオーバー時間  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスがチェックポイント操作を最後に行った時期によっては、バッファー キャッシュ内のダーティ ページが大量になることがあります。 このため、フェールオーバーは、残りのダーティ ページをディスクに書き込むまで継続し、フェールオーバー時間が長く予測不能になる場合があります。 [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]からは、FCI は間接チェックポイントを使用して、バッファー キャッシュに保持されるダーティ ページの量を調整します。 これにより、通常の作業負荷ではリソースの消費が増えますが、フェールオーバー時間の予測や構成が可能になります。 これは、組織内のサービス レベル契約で、高可用性ソリューションの目標復旧時間 (RTO) を指定する場合に非常に役立ちます。 間接的なチェックポイントの詳細については、「 [Indirect Checkpoints](../../../relational-databases/logs/database-checkpoints-sql-server.md#IndirectChkpt)」を参照してください。  
  
### <a name="reliable-health-monitoring-and-flexible-failover-policy"></a>信頼性の高い正常性監視と柔軟なフェールオーバー ポリシー  
 FCI が正常に開始した後で、WSFC サービスは基になる WSFC クラスターの正常性と [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスの正常性の両方を監視します。 [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]からは、WSFC サービスは専用接続を使用して、アクティブな [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスにシステム ストアド プロシージャを通じて詳細コンポーネント診断をポーリングします。 これには 3 つの影響があります。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスへの専用接続により、FCI が非常に高負荷の場合でも、コンポーネント診断を常に確実にポーリングできます。 これにより、高負荷状態のシステムと、実際に障害条件が発生しているシステムを区別できるため、誤ったフェールオーバーなどの問題を回避できます。  
  
-   詳細コンポーネント診断により、より柔軟なフェールオーバー ポリシーを構成できるため、フェールオーバーをトリガーする障害条件とトリガーしない障害条件を選択できます。  
  
-   詳細コンポーネント診断により、自動フェールオーバーをさかのぼってトラブルシューティングすることもできます。 診断情報がログ ファイルに格納され、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] エラー ログと併置されます。 これらをログ ファイル ビューアーに読み込んで、そのフェールオーバーの原因を判断するためにフェールオーバーの発生までのコンポーネント状態を調査できます。  
  
 詳細については、「 [Failover Policy for Failover Cluster Instances](../../../sql-server/failover-clusters/windows/failover-policy-for-failover-cluster-instances.md)」をご覧ください。  
  
##  <a name="FCIelements"></a> フェールオーバー クラスター インスタンスの構成要素  
 FCI は、類似するハードウェア構成と同一のソフトウェア構成 (オペレーティング システムのバージョンとパッチ レベル、および [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のバージョン、パッチ レベル、コンポーネント、インスタンス名など) を含む物理サーバー (ノード) のセットから構成されます。 同一のソフトウェア構成は、ノード間でフェールオーバーする際に FCI が完全に機能できるようにするために必要です。  
  
 WSFC リソース グループ  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] FCI は、WSFC リソース グループで実行されます。 リソース グループ内の各ノードは、構成設定の同期されたコピーおよびチェックポイントが設定されたレジストリ キーを保持して、フェールオーバー後に FCI が完全に機能し、一度にクラスター内の 1 つのノード (アクティブ ノード) だけがリソース グループを所有するようにします。 WSFC サービスは、サーバー クラスター、クォーラム構成、フェールオーバー ポリシー、およびフェールオーバー操作に加え、FCI の VNN および仮想 IP アドレスを管理します。 障害 (ハードウェア、オペレーティング システム、アプリケーション、サービスなどの障害) が発生した場合や計画していたアップグレードが行われる場合は、リソース グループの所有権が FCI 内の別のノードに移動します。WSFC リソース グループでサポートされるノード数は、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] エディションによって決まります。 また、CPU、メモリ、ディスク数などのハードウェア容量に応じて、同じ WSFC クラスターが複数の FCI (複数のリソース グループ) を実行できます。  
  
 SQL Server バイナリ  
 製品バイナリは FCI の各ノードにローカルにインストールされます。これは、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] スタンドアロン インストールと同様のプロセスです。 ただし、スタートアップ時にサービスが自動的に開始されることはなく、WSFC によって管理されます。  
  
 ストレージ  
 可用性グループとは対照的に、FCI は FCI のすべてのノード間でデータベースとログの格納に共有ストレージを使用する必要があります。 共有ストレージは、WSFC クラスター ディスク、SAN 上のディスク、記憶域スペース ダイレクト (S2D)、または SMB 上のファイル共有の形式にすることができます。 このようにして、フェールオーバーの発生時に、FCI のすべてのノードがインスタンス データについて同じビューを持ちます。 ただし、これは共有ストレージに単一障害点が生じる可能性があり、FCI が基になるストレージ ソリューションに依存してデータ保護を行うことを意味します。  
  
 ネットワーク名  
 FCI の VNN は、FCI に統一された接続ポイントを提供します。 これにより、アプリケーションは、現在アクティブなノードを知らなくても VNN に接続できます。 フェールオーバーが発生した場合、VNN は開始後に新しいアクティブ ノードに登録されます。 この処理は、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] に接続しているクライアントまたはアプリケーションに認識されることなく実行され、これによって障害発生中のアプリケーションおよびクライアントのダウンタイムを最小限に抑えることができます。  
  
 仮想 IP  
 マルチサブネット FCI の場合、FCI の各サブネットに仮想 IP アドレスが割り当てられます。 フェールオーバー時に、DNS サーバー上の VNN は、それぞれのサブネットの仮想 IP アドレスを指すように更新されます。 アプリケーションとクライアントは、マルチサブネット フェールオーバー後に同じ VNN を使用して FCI に接続できます。  
  
##  <a name="ConceptsAndTasks"></a> SQL Server フェールオーバーの概念とタスク  
  
|概念とタスク|トピック|  
|------------------------|-----------|  
|障害検出メカニズムと柔軟なフェールオーバー ポリシーについて説明します。|[Failover Policy for Failover Cluster Instances](../../../sql-server/failover-clusters/windows/failover-policy-for-failover-cluster-instances.md)|  
|FCI の管理とメンテナンスの概念について説明します。|[フェールオーバー クラスター インスタンスの管理とメンテナンス](../../../sql-server/failover-clusters/windows/failover-cluster-instance-administration-and-maintenance.md)|  
|マルチサブネットの構成と概念について説明します。|[SQL Server マルチサブネット クラスタリング &#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/sql-server-multi-subnet-clustering-sql-server.md)|  
  
##  <a name="RelatedTopics"></a> 関連項目  
  
|**トピックの説明**|**トピック**|  
|----------------------------|---------------|  
|新しい [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] FCI のインストール方法について説明します。|[新しい SQL Server フェールオーバー クラスターの作成 &#40;セットアップ&#41;](../../../sql-server/failover-clusters/install/create-a-new-sql-server-failover-cluster-setup.md)|  
|[!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] フェールオーバー クラスターにアップグレードする方法について説明します。|[SQL Server フェールオーバー クラスター インスタンスのアップグレード](../../../sql-server/failover-clusters/windows/upgrade-a-sql-server-failover-cluster-instance.md)|  
|Windows フェールオーバー クラスタリングの概念について説明し、Windows フェールオーバー クラスタリングに関連するタスクへのリンクを示します。|[!INCLUDE[nextref_longhorn](../../../includes/nextref-longhorn-md.md)]: [フェールオーバー クラスターの概要](https://go.microsoft.com/fwlink/?LinkId=177878)<br /><br /> [!INCLUDE[nextref_longhorn](../../../includes/nextref-longhorn-md.md)] R2: [フェールオーバー クラスターの概要](https://go.microsoft.com/fwlink/?LinkId=177879)|  
|FCI 内のノードと可用性グループ内のレプリカの概念の違いと、FCI を使用して可用性グループのレプリカをホストする場合の考慮事項について説明します。|[フェールオーバー クラスタリングと可用性グループ &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server.md)|  
  
  
