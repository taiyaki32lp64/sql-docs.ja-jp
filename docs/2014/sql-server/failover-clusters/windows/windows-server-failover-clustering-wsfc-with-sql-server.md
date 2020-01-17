---
title: Windows Server フェールオーバー クラスタリング (WSFC) と SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], WSFC clusters
- Windows Server Failover Clustering (WSFC), with SQL Server
- WSFC, with SQL Server
- quorum [SQL Server]
- failover clustering [SQL Server], AlwaysOn Availability Groups
ms.assetid: 79d2ea5a-edd8-4b3b-9502-96202057b01a
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f39911901b6ab729382c2e08b34c3452d4ec65cd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63246032"
---
# <a name="windows-server-failover-clustering-wsfc-with-sql-server"></a>Windows Server フェールオーバー クラスタリング (WSFC) と SQL Server
  *Windows Server フェールオーバー クラスタリング* (WSFC) クラスターは、アプリケーションとサービスの可用性を高めるために連携する独立したサーバーのグループです。 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] は、WSFC サービスと機能を活用して [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] と [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスター インスタンスをサポートします。  
  
 
  
##  <a name="TermsAndDefs"></a> 用語と定義  
 WSFC クラスター  
 Windows Server フェールオーバー クラスタリング (WSFC) クラスターは、アプリケーションとサービスの可用性を高めるために連携する独立したサーバーのグループです。  
  
 フェールオーバー クラスター インスタンス  
 1 つ以上のアプリケーションまたはサービスを実行するために必要となる、IP アドレス リソース、ネットワーク名リソース、その他のリソースを管理する Windows サービスのインスタンスです。 クライアントは、コンピューター名を使用して物理サーバーのサービスにアクセスする場合と同様に、ネットワーク名を使用してグループ内のリソースにアクセスできます。 ただし、フェールオーバー クラスター インスタンスはグループであるため、基になる名前またはアドレスに影響を与えることなく他のノードにフェールオーバーできます。  
  
 ノード  
 サーバー クラスターのアクティブまたは非アクティブなメンバーである Microsoft Windows サーバー システムです。  
  
 クラスター リソース  
 物理的または論理的エンティティです。ノードによる所有、オンライン化またはオフライン化、ノード間での移動、クラスター オブジェクトとしての管理が可能です。 特定の時点でクラスター リソースを所有できるのは 1 つのノードのみです。  
  
 リソース グループ  
 単一クラスター オブジェクトとして管理されるクラスター リソースのコレクションです。 通常、リソース グループには、特定のアプリケーションまたはサービスを実行するために必要なすべてのクラスター リソースが含まれます。 フェールオーバーとフェールバックは常にリソース グループ上で行われます。  
  
 リソースの依存関係  
 他のリソースが依存するリソースです。 リソース A がリソース B に依存している場合、B は A の依存関係です。  
  
 ネットワーク名リソース  
 クラスター リソースとして管理されている論理サーバーの名前です。 ネットワーク名リソースは、IP アドレス リソースと共に使用する必要があります。  
  
 優先所有者  
 リソース グループの実行が優先されるノードです。 各リソース グループには、優先順に並べられた優先所有者のリストが関連付けられています。 自動フェールオーバー中に、リソース グループは、優先所有者リスト内の次の優先ノードに移動します。  
  
 実行可能な所有者  
 リソースを実行できるセカンダリ ノードです。 各リソース グループには、実行可能な所有者のリストが関連付けられています。 リソース グループは、実行可能な所有者としてリストされているノードにのみフェールオーバーできます。  
  
 クォーラム モード  
 クラスターが維持できるノード障害の数を決定するフェールオーバー クラスター内のクォーラム構成です。  
  
 強制されたクォーラム  
 クォーラムに必要な少数の要素のみが通信しているときでもクラスターを開始するためのプロセスです。  
  
 詳細については、以下をご覧ください。[フェールオーバー クラスター用語集](/previous-versions/windows/desktop/MsCS/server-cluster-glossary)  
  
##  <a name="Overview"></a> Windows Server フェールオーバー クラスタリングの概要  
 Windows Server フェールオーバー クラスタリングは、Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] や Microsoft Exchange などのホストされるサーバー アプリケーションの高可用性とディザスター リカバリー シナリオをサポートするインフラストラクチャ機能を提供します。 クラスター ノードまたはサービスに障害が発生すると、そのノードでホストされていたサービスは自動的に、または手動で、他の可用性ノードに転送されます。このプロセスを *フェールオーバー*と呼びます。  
  
 WSFC クラスター内のノードは連携して、次のような機能を提供します。  
  
-   **分散メタデータと通知。** WSFC サービスとホストされるアプリケーション メタデータは、クラスター内の各ノードで維持されます。 このメタデータには、ホストされるアプリケーションの設定に加え、WSFC 構成と状態が含まれます。 ノードのメタデータまたは状態の変更は、クラスター内の他のノードに自動的に反映されます。  
  
-   **リソース管理。** クラスター内の各ノードは、直接アタッチされたストレージ、ネットワーク インターフェイス、共有ディスク ストレージへのアクセスなどの物理的リソースを提供する場合があります。 ホストされるアプリケーション自体もクラスター リソースとして登録されます。また、他のリソース上でスタートアップと正常性依存関係を構成する場合があります。  
  
-   **正常性状態の監視。** ノード間およびプライマリ ノードの正常性状態の検出は、ハートビート ネットワーク通信およびリソース監視の組み合わせによって行われます。 クラスターの全体的な正常性状態は、クラスター内のノードのクォーラムの投票によって決定されます。  
  
-   **フェールオーバーの調整。** 各リソースはプライマリ ノードでホストされるように構成され、それぞれ自動的に、または手動で 1 つ以上のセカンダリ ノードに転送されます。 正常性ベースのフェールオーバー ポリシーによって、ノード間でのリソース所有権の自動転送が制御されます。 フェールオーバーが発生すると、適切に対応できるように、ノードおよびホストされているアプリケーションに通知されます。  
  
 詳細については、以下をご覧ください。[Windows Server 2008 R2 のフェールオーバー クラスター](https://technet.microsoft.com/library/ff182338\(WS.10\).aspx)  
  
##  <a name="AlwaysOnWsfcTech"></a> SQL Server AlwaysOn テクノロジと WSFC  
 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] *AlwaysOn*は、新しい高可用性とディザスター リカバリー ソリューションの WSFC を利用します。 AlwaysOn は、アプリケーションの可用性を高め、ハードウェア投資の回収率を上げ、高可用性配置と管理を簡素化する、統合された柔軟なソリューションを提供します。  
  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] と AlwaysOn フェールオーバー クラスター インスタンスのどちらも WSFC をプラットフォーム テクノロジとして使用して、コンポーネントとしてを WSFC クラスター リソースとして登録します。  関連するリソースは *リソース グループ*としてまとめられ、他の WSFC クラスター リソースに依存するように設定できます。 これによって、WSFC クラスター サービスは、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスを再起動する必要がある場合はこれを検出して通知したり、WSFC クラスター内の他のサーバー ノードに自動的にフェールオーバーしたりします。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] AlwaysOn テクノロジの利点を完全に活かすには、WSFC 関連のいくつかの前提条件を適用する必要があります。  
>   
>  詳細については、以下をご覧ください。[前提条件、制限事項、および AlwaysOn 可用性グループの推奨事項&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)  
  
### <a name="instance-level-high-availability-with-alwayson-failover-cluster-instances"></a>AlwaysOn フェールオーバー クラスター インスタンスとインスタンス レベルの高可用性  
 AlwaysOn *フェールオーバー クラスター インスタンス* (FCI) は、WSFC クラスター内のノードにまたがってインストールされた [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスです。 この種類のインスタンスには、共有ディスク ストレージ (ファイバー チャネルまたは iSCSI SAN 経由) および仮想ネットワーク名に対してリソース依存関係があります。 仮想ネットワーク名には、それぞれが異なるサブネットに存在する 1 つ以上の仮想 IP アドレスに対してリソース依存関係があります。 SQL Server サービスおよび SQL Server エージェント サービスはリソースとして登録され、どちらも仮想ネットワーク名リソースに依存します。  
  
 フェールオーバーが発生した場合、WSFC サービスはインスタンスのリソース所有権を指定されたフェールオーバー ノードに転送します。 その後、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスは、フェールオーバー ノードで再起動され、データベースが通常どおり復元されます。 特定の時点で、FCI と基になるリソースをホストできるのは、クラスター内の 1 つのノードのみです。  
  
> [!NOTE]  
>  AlwaysOn フェールオーバー クラスター インスタンスには、ストレージ エリア ネットワーク (SAN)、SMB ファイル共有などの対称的な共有ディスク ストレージが必要です。  共有ディスク ストレージ ボリュームは、WSFC クラスター内のすべてのフェールオーバー ノードで使用できる必要があります。  
  
 詳細については、以下をご覧ください。[AlwaysOn フェールオーバー クラスター インスタンス](always-on-failover-cluster-instances-sql-server.md)  
  
### <a name="database-level-high-availability-with-includesshadrincludessshadr-mdmd"></a>データベース レベルの高可用性 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]  
 *可用性グループ* は、共にフェールオーバーするユーザー データベースのセットです。 可用性グループは、1 つのプライマリ *可用性レプリカ* と、共有ストレージを必要としないデータ保護のために SQL Server ログに基づくデータ移動を介して維持される 1 ～ 4 個のセカンダリ レプリカから構成されます。 各レプリカは、WSFC クラスターの別々のノードにある [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスによってホストされます。 可用性グループとこれに対応する仮想ネットワーク名は、WSFC クラスターのリソースとして登録されます。  
  
 プライマリ レプリカのノード上の *可用性グループ リスナー* は、受信クライアント要求に応答し、仮想ネットワーク名に接続します。そして、接続文字列の属性に基づいて各要求を適切な [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスにリダイレクトします。  
  
 フェールオーバーが発生した場合は、共有物理リソースの所有権を他のノードに転送する代わりに、WSFC を利用して他の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンス上でセカンダリ レプリカを再構成し、可用性グループのプライマリ レプリカにします。 その後、可用性グループの仮想ネットワーク名リソースが、そのインスタンスに転送されます。  
  
 特定の時点で、可用性グループ データベースのプライマリ レプリカをホストできるのは、1 つの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスのみです。また、関連付けられたすべてのセカンダリ レプリカは別々のインスタンスに存在する必要があり、各インスタンスは別々の物理ノードに存在する必要があります。  
  
> [!NOTE]  
>  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]ではフェールオーバー クラスター インスタンスを配置する必要はありません。また、対称共有ストレージ (SAN または SMB) を使用する必要もありません。  
>   
>  フェールオーバー クラスター インスタンス (FCI) を可用性グループと共に使用することによって、可用性レプリカの可用性を高めることができます。 ただし、WSFC クラスター内での競合状態の発生を回避するため、FCI 上でホストされる可用性レプリカとの間の可用性グループの自動フェールオーバーはサポートされていません。  
  
 詳細については、以下をご覧ください。[AlwaysOn 可用性グループの概要&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
  
##  <a name="AlwaysOnWsfcHealth"></a> WSFC の正常性監視とフェールオーバー  
 AlwaysOn ソリューションの高可用性は、物理的および論理的 WSFC クラスター リソースのプロアクティブな正常性状態の監視と、冗長ハードウェアでの自動フェールオーバーおよび再構成によって実現します。  また、システム管理者は、可用性グループまたはノード間での *インスタンスの* 手動フェールオーバー [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] を開始できます。  
  
### <a name="failover-policies-for-nodes-failover-cluster-instances-and-availability-groups"></a>ノード、フェールオーバー クラスター インスタンス、可用性グループのフェールオーバー ポリシー  
 *フェールオーバー ポリシー* は、WSFC クラスター ノード、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスター インスタンス (FCI)、および可用性グループのレベルで構成されます。  これらのポリシーは、クラスター リソースの異常な状態の重大度、期間、頻度とノードの応答時間に基づいたもので、サービスの再起動のトリガー、ノード間でのクラスター リソースの *自動フェールオーバー* のトリガー、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンス間での可用性グループ プライマリ レプリカの移動のトリガーを行うことができます。  
  
 可用性グループ レプリカのフェールオーバーは、基になる [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスに影響しません。  FCI のフェールオーバーでは、ホストされている可用性グループ レプリカとインスタンスが移動します。  
  
 詳細については、以下をご覧ください。[Failover Policy for Failover Cluster Instances](failover-policy-for-failover-cluster-instances.md)  
  
### <a name="wsfc-resource-health-detection"></a>WSFC リソースの正常性の検出  
 WSFC クラスター ノード内の各リソースの状態と正常性は、定期的または要求時に報告されます。 リソースの障害を示す状況としては、電源障害、ディスクまたはメモリのエラー、ネットワーク通信エラー、応答しないサービスなどがあります。  
  
 ネットワーク、ストレージ、サービスなどの WSFC クラスター リソースは、互いに依存するように構成できます。 リソースの累積正常性は、リソース依存関係の正常性で正常性を連続的にロール アップすることで決定されます。  
  
### <a name="wsfc-inter-node-health-detection-and-quorum-voting"></a>WSFC ノード間の正常性の検出とクォーラム投票  
 WSFC クラスター内の各ノードは、定期的なハートビート通信に参加し、ノードの正常性状態を他のノードと共有します。 応答しないノードは、エラー状態であると見なされます。  
  
 *クォーラム* ノード セットは、WSFC クラスター内の大多数の投票ノードおよび監視サーバーです。 WSFC クラスターの全体的な正常性と状態は、定期的な *クォーラムの投票*によって決定されます。 クォーラムの存在は、クラスターが正常であり、ノード レベルのフォールト トレランスを提供できることを表します。  
  
 *クォーラム モード* は、WSFC クラスター レベルで構成され、クォーラム投票の方法、および自動フェールオーバーを実行するタイミングまたはクラスターをオフラインにするタイミングを指定します。  
  
> [!TIP]  
>  WSFC クラスターのクォーラム投票の数は、常に奇数にすることをお勧めします。  クォーラム投票のために、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] をクラスター内のすべてのノードにインストールする必要はありません。 追加サーバーはクォーラム メンバーとして機能できます。また、リモート ファイル共有を決定機構として使用するように WSFC クォーラム モデルを構成することもできます。  
>   
>  詳細については、以下をご覧ください。[WSFC クォーラム モードと投票の構成 &#40;SQL Server&#41;](wsfc-quorum-modes-and-voting-configuration-sql-server.md)  
  
### <a name="disaster-recovery-through-forced-quorum"></a>強制されたクォーラムによる災害復旧  
 実際の運用状況と WSFC クラスター構成に応じて、自動フェールオーバーと手動フェールオーバーの両方を使用できます。これによって、堅牢でフォールト トレランスな [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] AlwaysOn ソリューションを維持できます。 ただし、WSFC クラスター内の投票ノードのクォーラムが相互に通信できない場合、または WSFC クラスターがこれ以外の理由で正常性の検証に失敗する場合は、WSFC クラスターがオフラインになる場合があります。  
  
 災害や、永続的なハードウェア障害または通信障害が原因で WSFC クラスターがオフラインになった場合は、手動で管理操作を実行して、 *クォーラムを強制* し、稼働しているクラスター ノードを非フォールト トレラント構成でオンラインに戻す必要があります。  
  
 その後、WSFC クラスターを再構成し、影響を受けたデータベース レプリカを復元し、新しいクォーラムを再構築するという一連の手順を実行する必要があります。  
  
 詳細については、以下をご覧ください。[WSFC の強制クォーラムによる災害復旧 &#40;SQL Server&#41;](wsfc-disaster-recovery-through-forced-quorum-sql-server.md)  
  
##  <a name="AlwaysOnWsfcRelationship"></a> SQL Server AlwaysOn コンポーネントと WSFC との関係  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] AlwaysOn と WSFC の機能およびコンポーネント間には、いくつかのリレーションシップの層が存在します。  
  
 AlwaysOn 可用性グループは、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスでホストされています。  
 クライアントは、可用性グループ リスナーの論理ネットワーク名を指定してプライマリまたはセカンダリ データベースに接続することを要求します。この要求は、基になる [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスまたは [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスター インスタンス (FCI) の適切なインスタンス ネットワーク名にリダイレクトされます。  
  
 SQL サーバー インスタンスは、1 つのノード上でアクティブにホストされています。  
 スタンドアロンの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスが存在する場合は、静的なインスタンス ネットワーク名で、常に 1 つのノードにあります。  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] FCI が存在する場合は、1 つの仮想インスタンス ネットワーク名で、2 つ以上のフェールオーバー ノードの中の 1 つのノードでアクティブになります。  
  
 ノードは、WSFC クラスターのメンバーです。  
 すべてのノードの WSFC 構成メタデータと状態は、各ノードに保存されます。 各サーバーは、ユーザーまたはシステム データベースに対して非対称ストレージまたは共有ストレージ (SAN) ボリュームを提供できます。 各サーバーには、1 つまたは複数のサブネット上に少なくとも 1 つの物理ネットワーク インターフェイスがあります。  
  
 WSFC サービスは、サーバー グループの正常性を監視し、構成を管理します。  
 Windows Server フェールオーバー クラスター (WSFC) サービスは、WSFC 構成メタデータへの変更とその状態を、クラスター内のすべてのノードに反映します。 一部のメタデータと状態が、WSFC クォーラム監視リモート ファイル共有に保存されることもあります。 2 つ以上のアクティブなノードまたは監視サーバーによって、WSFC クラスターの正常性について投票するクォーラムが構成されます。  
  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] レジストリ キーは WSFC クラスターのサブキーです。  
 WSFC クラスターを削除してから再作成した場合は、 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] を有効にしていた、元の WSFC クラスター上の各サーバー インスタンスについて、 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 機能を無効にしてから再度有効にする必要があります。 詳細については、「[AlwaysOn 可用性グループの有効化と無効化 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md)」を参照してください。  
  
 ![SQL Server AlwaysOn コンポーネント コンテキストの図](../../../database-engine/media/alwaysoncomponentcontextdiagram.gif "SQL Server AlwaysOn コンポーネント コンテキストの図")  
  
##  <a name="RelatedTasks"></a> 関連タスク  
  
-   [クラスター クォーラムの NodeWeight 設定を表示](view-cluster-quorum-nodeweight-settings.md)  
  
-   [クラスター クォーラムの NodeWeight の設定の構成](configure-cluster-quorum-nodeweight-settings.md)  
  
-   [クォーラムを使用せずに WSFC クラスターを強制的に起動する](force-a-wsfc-cluster-to-start-without-a-quorum.md)  
  
##  <a name="RelatedContent"></a> 関連コンテンツ  
  
-   [Windows Server テクノロジ:フェールオーバー クラスター](https://technet.microsoft.com/library/cc732488\(v=WS.10\).aspx)  
  
-   [Windows Server 2008 R2 のフェールオーバー クラスター](https://technet.microsoft.com/library/ff182338\(WS.10\).aspx)  
  
-   [フェールオーバー クラスターのイベントおよびログを表示する](https://technet.microsoft.com/library/cc772342\(WS.10\).aspx)  
  
-   [Get-ClusterLog フェールオーバー クラスター コマンドレット](https://technet.microsoft.com/library/ee461045.aspx)  
  
## <a name="see-also"></a>参照  
 [AlwaysOn フェールオーバー クラスター インスタンス (SQL Server)](always-on-failover-cluster-instances-sql-server.md)   
 [AlwaysOn 可用性グループの概要&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [WSFC クォーラム モードと投票の構成 &#40;SQL Server&#41;](wsfc-quorum-modes-and-voting-configuration-sql-server.md)   
 [フェールオーバー クラスター インスタンスのフェールオーバー ポリシー](failover-policy-for-failover-cluster-instances.md)   
 [WSFC の強制クォーラムによる災害復旧 &#40;SQL Server&#41;](wsfc-disaster-recovery-through-forced-quorum-sql-server.md)  
  
  
