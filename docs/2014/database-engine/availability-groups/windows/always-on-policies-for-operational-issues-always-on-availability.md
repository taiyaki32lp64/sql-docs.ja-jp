---
title: Always On Always On 可用性グループ (SQL Server) 運用上の問題のポリシー |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], troubleshooting
- Availability Groups [SQL Server], policies
ms.assetid: afa5289c-641a-4c03-8749-44862384ec5f
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 815f549cf9ab6dd7fe748c08ae7f32683c9d8551
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62815757"
---
# <a name="always-on-policies-for-operational-issues-with-always-on-availability-groups-sql-server"></a>AlwaysOn 可用性グループでの運用上の問題のポリシー ベースの管理 (SQL Server)
  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] の正常性モデルは、定義済みポリシー ベースの管理 (PBM) ポリシーのセットを評価します。 これらのポリシーを使用すると、可用性グループとその可用性レプリカおよびデータベースの正常性を [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]で表示できます。  
  
 
  
##  <a name="TermsAndDefinitions"></a> 用語と定義  
 AlwaysOn の定義済みのポリシー  
 一連の組み込みポリシーを使用して、データベース管理者は可用性グループとその可用性レプリカおよびデータベースが AlwaysOn ポリシーで定義されている状態に適合しているかどうかをチェックできます。  
  
 [AlwaysOn 可用性グループ](always-on-availability-groups-sql-server.md)高可用性とディザスター リカバリーのソリューションで、データベース ミラーリングにエンタープライズ レベルの代替を提供します。  
  
 可用性グループ  
 ひとまとまりでフェールオーバーされる個別のユーザー データベースのセット ( *可用性データベース*) のコンテナー。  
  
 可用性レプリカ  
 可用性グループのインスタンス化。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の特定のインスタンスによってホストされ、可用性グループに属する各可用性データベースのローカル コピーを保持します。 可用性グループには、2 種類の可用性レプリカ ( *プライマリ レプリカ* と 1 ～ 4 つの *セカンダリ レプリカ*) があります。 可用性グループの可用性レプリカをホストするサーバー インスタンスは、同じ Windows Server フェールオーバー クラスタリング (WSFC) クラスター内の別のノードにある必要があります。  
  
 可用性データベース  
 可用性グループに属しているデータベース。 可用性データベースごとに、可用性グループは 1 個の読み取り/書き込み可能なコピー (*プライマリ データベース*) と 1 ～ 4 個の読み取り専用コピー (*セカンダリ データベース*) を管理します。  
  
 AlwaysOn ダッシュボード  
 可用性グループの正常性をひとめで確認できるビューを提供する [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ダッシュボード。 詳細については、このトピックの「 [AlwaysOn ダッシュボード](#Dashboard)」を参照してください。  
  
##  <a name="AlwaysOnPBM"></a> 定義済みのポリシーと問題点  
 次の表は、定義済みのポリシーをまとめたものです。  
  
|ポリシー名|問題点|カテゴリ**<sup>*</sup>**|ファセット|  
|-----------------|-----------|------------------------------|-----------|  
|WSFC クラスターの状態|[WSFC クラスター サービスはオフラインです](wsfc-cluster-service-is-offline.md)。|重大|SQL Server のインスタンス|  
|可用性グループのオンライン状態|[可用性グループがオフライン](availability-group-is-offline.md)。|重大|可用性グループ|  
|可用性グループの自動フェールオーバーの準備|[可用性グループの自動フェールオーバーの準備ができていない](availability-group-is-not-ready-for-automatic-failover.md)。|重大|可用性グループ|  
|可用性レプリカのデータ同期状態|[一部の可用性レプリカでデータが同期されない](some-availability-replicas-are-not-synchronizing-data.md)。|警告|可用性グループ|  
|同期レプリカのデータの同期状態|[いくつかの同期のレプリカが同期されていません](some-synchronous-replicas-are-not-synchronized.md)。|警告|可用性グループ|  
|可用性レプリカのロールの状態|[一部の可用性レプリカに正常なロールがありません](some-availability-replicas-do-not-have-a-healthy-role.md)。|警告|可用性グループ|  
|可用性レプリカの接続状態|[いくつかの可用性レプリカが切断されている](some-availability-replicas-are-disconnected.md)。|警告|可用性グループ|  
|可用性レプリカのロールの状態|[可用性レプリカに正常なロールがありません](availability-replica-does-not-have-a-healthy-role.md)。|重大|可用性レプリカ|  
|可用性レプリカの接続状態|[可用性レプリカが切断されている](availability-replica-is-disconnected.md)。|重大|可用性レプリカ|  
|可用性レプリカの参加状態|[可用性レプリカが参加していません](availability-replica-is-not-joined.md)。|警告|可用性レプリカ|  
|可用性レプリカのデータの同期状態|[一部の可用性データベースのデータ同期状態が正常ではありません](data-synchronization-state-of-some-availability-database-is-not-healthy.md)。|警告|可用性レプリカ|  
|可用性データベースの中断状態|[可用性データベースが中断されています](availability-database-is-suspended.md)。|警告|可用性データベース|  
|可用性データベースの参加状態|[セカンダリ データベースが参加していません](secondary-database-is-not-joined.md)。|警告|可用性データベース|  
|可用性データベースのデータ同期状態|[可用性データベースのデータ同期状態が正常ではありません](data-synchronization-state-of-availability-database-is-not-healthy.md)。|警告|可用性データベース|  
  
> [!IMPORTANT]  
>  **<sup>*</sup>**  AlwaysOn ポリシーでは、カテゴリ名が Id として使用されます。 AlwaysOn カテゴリの名前を変更すると、正常性評価の機能を使用できなくなります。 このため、AlwaysOn カテゴリの名前は変更しないでください。  
  
##  <a name="Dashboard"></a> AlwaysOn ダッシュ ボード  
 AlwaysOn ダッシュボードには、可用性グループの正常性をひとめで確認できるビューが用意されています。 AlwaysOn ダッシュボードには、次の機能が含まれています。  
  
-   指定された可用性グループ、その可用性レプリカ、およびそのデータベースの詳細情報を簡単に表示できます。  
  
-   主要な状態が視覚的に表示され、データベース管理者は運用上の意思決定を迅速に行うことができます。  
  
-   トラブルシューティング シナリオの開始ポイントを提供します。  
  
-   特定の運用上の問題点について、 **[ポリシー評価の結果]** ダイアログ ボックスに、特定の AlwaysOn 正常性ポリシーの違反に関する情報と、修復のヘルプへのリンクを示します。  
  
-   AlwaysOn 固有の問題の前のイベントを表示する正常性拡張イベント ビューアーを提供します。  
  
-   可用性グループのフェールオーバーで特定の問題を修復できる場合、リンクの開始ポイントである[可用性グループのフェールオーバー ウィザード](use-the-fail-over-availability-group-wizard-sql-server-management-studio.md)を提供します。 データベース管理者は、このウィザードを使用して手動フェールオーバー プロセスを実行します。  
  
##  <a name="ExtendHealthModel"></a> AlwaysOn の正常性モデルの拡張  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] の正常性モデルを拡張するには、独自のユーザー定義のポリシーを作成し、監視するオブジェクトの種類に基づいて特定のカテゴリに分類します。  いくつかの設定を変更した後、独自のユーザー定義のポリシーおよび AlwaysOn の定義済みのポリシーが、AlwaysOn ダッシュボードによって自動的に評価されます。  
  
 ユーザー定義ポリシーでは、AlwaysOn の定義済みポリシーで使用されているものを含め、使用可能なすべての PBM ファセットを使用できます (このトピックの「[定義済みのポリシーと問題点](#AlwaysOnPBM)」を参照してください)。 サーバーのファセットは、[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] の正常性状態の監視用に、`IsHadrEnabled` プロパティおよび `HadrManagerStatus` プロパティを提供します。 サーバーのファセットは、WSFC クラスター構成の監視用に、`ClusterQuorumType` プロパティおよび `ClusterQuorumState` プロパティも提供します。  
  
 詳細については、「[AlwaysOn の正常性モデル: パート 2: 正常性モデルの拡張](https://blogs.msdn.com/b/sqlalwayson/archive/2012/02/13/extending-the-alwayson-health-model.aspx)」を参照してください (SQL Server AlwaysOn チームのブログ)。  
  
##  <a name="RelatedTasks"></a> 関連タスク  
  
-   [AlwaysOn ポリシーを使用して、可用性グループのヘルスを表示する&#40;SQL Server&#41;](use-always-on-policies-to-view-the-health-of-an-availability-group-sql-server.md)  
  
-   [AlwaysOn ダッシュボードの使用 &#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
-   [WSFC の強制クォーラムによる災害復旧 &#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/wsfc-disaster-recovery-through-forced-quorum-sql-server.md)  
  
-   [クォーラムを使用せずに WSFC クラスターを強制的に起動する](../../../sql-server/failover-clusters/windows/force-a-wsfc-cluster-to-start-without-a-quorum.md)  
  
-   [可用性グループの強制手動フェールオーバーの実行 &#40;SQL Server&#41;](perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)  
  
-   [ファイル追加失敗の操作のトラブルシューティング&#40;AlwaysOn 可用性グループ&#41;](troubleshoot-a-failed-add-file-operation-always-on-availability-groups.md)  
  
##  <a name="RelatedContent"></a> 関連コンテンツ  
  
-   [AlwaysOn の正常性モデル: パート 1: 正常性モデルのアーキテクチャ](https://blogs.msdn.com/b/sqlalwayson/archive/2012/02/13/extending-the-alwayson-health-model.aspx)  
  
-   [AlwaysOn の正常性モデル: パート 2: 正常性モデルの拡張](https://blogs.msdn.com/b/sqlalwayson/archive/2012/02/13/extending-the-alwayson-health-model.aspx)  
  
-   [Microsoft SQL Server AlwaysOn ソリューション ガイド高可用性とディザスター リカバリー](https://go.microsoft.com/fwlink/?LinkId=227600)  
  
## <a name="see-also"></a>関連項目  
 [AlwaysOn 可用性グループ (SQL Server)](always-on-availability-groups-sql-server.md)   
 [AlwaysOn 可用性グループの概要&#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [可用性グループの管理 &#40;SQL Server&#41;](administration-of-an-availability-group-sql-server.md)   
 [可用性グループの監視 &#40;SQL Server&#41;](monitoring-of-availability-groups-sql-server.md)  
  
  
