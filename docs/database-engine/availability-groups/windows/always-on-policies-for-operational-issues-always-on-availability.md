---
title: ポリシー ベースの管理:可用性グループ
description: Always On 可用性グループの正常性モデルは、定義済みポリシー ベースの管理 (PBM) ポリシーのセットを評価します。 これらのポリシーを使用すると、可用性グループとレプリカおよびデータベースの正常性を SQL Server で表示できます。
ms.custom: seo-lt-2019
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], troubleshooting
- Availability Groups [SQL Server], policies
ms.assetid: afa5289c-641a-4c03-8749-44862384ec5f
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: ac339e638377778065f158b4cbd20280d5d4bb65
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75244061"
---
# <a name="policy-based-management-for-operational-issues-with-always-on-availability-groups"></a>Always On 可用性グループでの運用上の問題に対するポリシー ベースの管理
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Always On 可用性グループの正常性モデルは、定義済みポリシー ベースの管理 (PBM) ポリシーのセットを評価します。 これらのポリシーを使用すると、可用性グループとその可用性レプリカおよびデータベースの正常性を SQL Server で表示できます。  
  
  
##  <a name="TermsAndDefinitions"></a> 用語と定義  
 AlwaysOn の定義済みのポリシー  
 一連の組み込みポリシーであり、データベース管理者はこれらのポリシーを使用して、可用性グループとその可用性レプリカおよびデータベースが AlwaysOn ポリシーで定義されている状態に適合しているかどうかをチェックできます。  
  
 [Always On 可用性グループ](../../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)  
 データベース ミラーリングに代わる、高可用性と災害復旧のためのエンタープライズ レベルのソリューション。  
  
 可用性グループ  
 ひとまとまりでフェールオーバーされる個別のユーザー データベースのセット ( *可用性データベース*) のコンテナー。  
  
 可用性レプリカ  
 可用性グループのインスタンス化。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の特定のインスタンスによってホストされ、可用性グループに属する各可用性データベースのローカル コピーを保持します。 可用性グループには、2 種類の可用性レプリカ ( *プライマリ レプリカ* と 1 ～ 4 つの *セカンダリ レプリカ*) があります。 可用性グループの可用性レプリカをホストするサーバー インスタンスは、同じ Windows Server フェールオーバー クラスタリング (WSFC) クラスター内の別のノードにある必要があります。  
  
 可用性データベース  
 可用性グループに属しているデータベース。 可用性データベースごとに、可用性グループは 1 個の読み取り/書き込み可能なコピー ( *プライマリ データベース*) と 1 ～ 4 個の読み取り専用コピー (*セカンダリ データベース*) を管理します。  
  
 Always On ダッシュボード  
 可用性グループの正常性をひとめで確認できるビューを提供する [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ダッシュボード。 詳細については、このトピックの「 [AlwaysOn ダッシュボード](#Dashboard)」を参照してください。  
  
##  <a name="Always OnPBM"></a> 定義済みのポリシーと問題点  
 次の表は、定義済みのポリシーをまとめたものです。  
  
|ポリシー名|問題|カテゴリ **&#42;**|ファセット|  
|-----------------|-----------|--------------------|-----------|  
|WSFC クラスターの状態|[WSFC クラスター サービスはオフラインです](../../../database-engine/availability-groups/windows/wsfc-cluster-service-is-offline.md)。|Critical|SQL Server のインスタンス|  
|可用性グループのオンライン状態|[可用性グループがオフライン](../../../database-engine/availability-groups/windows/availability-group-is-offline.md)。|Critical|可用性グループ|  
|可用性グループの自動フェールオーバーの準備|[可用性グループの自動フェールオーバーの準備ができていない](../../../database-engine/availability-groups/windows/availability-group-is-not-ready-for-automatic-failover.md)。|Critical|可用性グループ|  
|可用性レプリカのデータ同期状態|[一部の可用性レプリカでデータが同期されない](../../../database-engine/availability-groups/windows/some-availability-replicas-are-not-synchronizing-data.md)。|警告|可用性グループ|  
|同期レプリカのデータの同期状態|[いくつかの同期のレプリカが同期されていません](../../../database-engine/availability-groups/windows/some-synchronous-replicas-are-not-synchronized.md)。|警告|可用性グループ|  
|可用性レプリカのロールの状態|[一部の可用性レプリカに正常なロールがありません](../../../database-engine/availability-groups/windows/some-availability-replicas-do-not-have-a-healthy-role.md)。|警告|可用性グループ|  
|可用性レプリカの接続状態|[いくつかの可用性レプリカが切断されている](../../../database-engine/availability-groups/windows/some-availability-replicas-are-disconnected.md)。|警告|可用性グループ|  
|可用性レプリカのロールの状態|[可用性レプリカに正常なロールがありません](../../../database-engine/availability-groups/windows/availability-replica-does-not-have-a-healthy-role.md)。|Critical|可用性レプリカ|  
|可用性レプリカの接続状態|[可用性レプリカが切断されている](../../../database-engine/availability-groups/windows/availability-replica-is-disconnected.md)。|Critical|可用性レプリカ|  
|可用性レプリカの参加状態|[可用性レプリカが参加していません](../../../database-engine/availability-groups/windows/availability-replica-is-not-joined.md)。|警告|可用性レプリカ|  
|可用性レプリカのデータの同期状態|[一部の可用性データベースのデータ同期状態が正常ではありません](../../../database-engine/availability-groups/windows/data-synchronization-state-of-some-availability-database-is-not-healthy.md)。|警告|可用性レプリカ|  
|可用性データベースの中断状態|[可用性データベースが中断されています](../../../database-engine/availability-groups/windows/availability-database-is-suspended.md)。|警告|可用性データベース|  
|可用性データベースの参加状態|[セカンダリ データベースが参加していません](../../../database-engine/availability-groups/windows/secondary-database-is-not-joined.md)。|警告|可用性データベース|  
|可用性データベースのデータ同期状態|[可用性データベースのデータ同期状態が正常ではありません](../../../database-engine/availability-groups/windows/data-synchronization-state-of-availability-database-is-not-healthy.md)。|警告|可用性データベース|  
  
> [!IMPORTANT]
>  **&#42;** Always On ポリシーでは、カテゴリの名前が ID として使用されます。 AlwaysOn カテゴリの名前を変更すると、正常性評価の機能を使用できなくなります。 このため、AlwaysOn カテゴリの名前は変更しないでください。  
  
##  <a name="Dashboard"></a> AlwaysOn ダッシュボード  
 AlwaysOn ダッシュボードには、可用性グループの正常性を一目で確認できるビューが用意されています。 AlwaysOn ダッシュボードには、次の機能が含まれています。  
  
-   指定された可用性グループ、その可用性レプリカ、およびそのデータベースの詳細情報を簡単に表示できます。  
  
-   主要な状態が視覚的に表示され、データベース管理者は運用上の意思決定を迅速に行うことができます。  
  
-   トラブルシューティング シナリオの開始ポイントを提供します。  
  
-   特定の運用上の問題点について、 **[ポリシー評価の結果]** ダイアログ ボックスに、特定の AlwaysOn 正常性ポリシーの違反に関する情報と、修復のヘルプへのリンクを示します。  
  
-   AlwaysOn 固有の問題の前のイベントを表示する正常性拡張イベント ビューアーを提供します。  
  
-   可用性グループのフェールオーバーで特定の問題を修復できる場合、リンクの開始ポイントである[可用性グループのフェールオーバー ウィザード](../../../database-engine/availability-groups/windows/use-the-fail-over-availability-group-wizard-sql-server-management-studio.md)を提供します。 データベース管理者は、このウィザードを使用して手動フェールオーバー プロセスを実行します。  
  
##  <a name="ExtendHealthModel"></a> AlwaysOn 正常性モデルの拡張  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] の正常性モデルを拡張するには、独自のユーザー定義のポリシーを作成し、監視するオブジェクトの種類に基づいて特定のカテゴリに分類します。  いくつかの設定を変更した後、独自のユーザー定義のポリシーおよび AlwaysOn の定義済みのポリシーが、AlwaysOn ダッシュボードによって自動的に評価されます。  
  
 ユーザー定義ポリシーでは、AlwaysOn の定義済みポリシーで使用されているものを含め、使用可能なすべての PBM ファセットを使用できます (このトピックの「 [定義済みのポリシーと問題点](#Always OnPBM)」を参照してください)。 サーバーのファセットは、[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] の正常性状態の監視用に、**IsHadrEnabled** プロパティおよび **HadrManagerStatus**プロパティを提供します。 サーバーのファセットは、WSFC クラスター構成の監視用に、**ClusterQuorumType** プロパティおよび **ClusterQuorumState** プロパティも提供します。  
  
 詳細については、「 [AlwaysOn の正常性モデル: パート 2: 正常性モデルの拡張](https://blogs.msdn.microsoft.com/sqlalwayson/2012/02/13/the-alwayson-health-model-part-2-extending-the-health-model/) 」を参照してください (SQL Server AlwaysOn チームのブログ)。  
  
##  <a name="RelatedTasks"></a> 関連タスク  
  
-   [Always On ポリシーを使用した可用性グループの正常性の確認 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/use-always-on-policies-to-view-the-health-of-an-availability-group-sql-server.md)  
  
-   [AlwaysOn ダッシュボードの使用 &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
-   [WSFC の強制クォーラムによる災害復旧 &#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/wsfc-disaster-recovery-through-forced-quorum-sql-server.md)  
  
-   [クォーラムを使用せずに WSFC クラスターを強制的に起動する](../../../sql-server/failover-clusters/windows/force-a-wsfc-cluster-to-start-without-a-quorum.md)  
  
-   [可用性グループの強制手動フェールオーバーの実行 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)  
  
-   [失敗したファイルの追加操作のトラブルシューティング &#40;AlwaysOn 可用性グループ&#41;](../../../database-engine/availability-groups/windows/troubleshoot-a-failed-add-file-operation-always-on-availability-groups.md)  
  
##  <a name="RelatedContent"></a> 関連コンテンツ  
  
-   [AlwaysOn の正常性モデル: パート 1: 正常性モデルのアーキテクチャ](https://blogs.msdn.microsoft.com/sqlalwayson/2012/02/08/the-alwayson-health-model-part-1-health-model-architecture/)  
  
-   [AlwaysOn の正常性モデル: パート 2: 正常性モデルの拡張](https://blogs.msdn.microsoft.com/sqlalwayson/2012/02/13/the-alwayson-health-model-part-2-extending-the-health-model/)  
  
-   [高可用性と災害復旧のための Microsoft SQL Server AlwaysOn ソリューション ガイド](https://go.microsoft.com/fwlink/?LinkId=227600)  
  
## <a name="see-also"></a>参照  
 [AlwaysOn 可用性グループ &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [AlwaysOn 可用性グループの概要 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [可用性グループの管理 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/administration-of-an-availability-group-sql-server.md)   
 [可用性グループの監視 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/monitoring-of-availability-groups-sql-server.md)  
  
  
