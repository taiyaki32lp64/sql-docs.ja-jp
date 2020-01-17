---
title: AlwaysOn 可用性グループ (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], about
- secondary replicas, see Availability Groups [SQL Server]
- availability [SQL Server]
- AlwaysOn [SQL Server], see Availability Groups [SQL Server]
- Availability Groups [SQL Server]
ms.assetid: aa427606-8422-4656-b205-c9e665ddc8c1
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2e040fb9c05683be9d737ea134710c03d36317cd
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75229008"
---
# <a name="always-on-availability-groups-sql-server"></a>AlwaysOn 可用性グループ (SQL Server)
  
  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 機能は、データベース ミラーリングに代わる、高可用性と災害復旧のためのエンタープライズ レベルのソリューションです。 
  [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]で導入された [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] により、エンタープライズのユーザー データベースの可用性が最大限に高まります。 *可用性グループ*は、相互にフェールオーバーされる個別のユーザーデータベース (*可用性データベース*と呼ばれます) のフェールオーバー環境をサポートします。 可用性グループは、読み取り/書き込みプライマリ データベースのセットをサポートし、1 ～ 8 セットの対応するセカンダリ データベースをサポートします。 必要に応じて、セカンダリ データベースで読み取り専用アクセスまたはいくつかのバックアップ操作を利用できます。  
  
 可用性グループは、可用性レプリカのレベルでフェールオーバーします。 データベースの問題 (たとえば、データ ファイルの損失、データベースの削除、トランザクション ログの破損による障害が疑われる場合など) が発生してもフェールオーバーは行われません。  
  
  
##  <a name="Benefits"></a>効果  
 
  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] には、データベースの可用性を向上し、リソースの使用を改善できる、豊富なオプションのセットが用意されています。 主なコンポーネントは次のとおりです。  
  
-   最大 9 つの可用性レプリカをサポートします。 
  *可用性グループ* は、SQL Server の特定のインスタンスによってホストされ、可用性グループに属する各可用性データベースのローカル コピーを保持します。 各可用性グループは、1 個のプライマリ レプリカと最大 8 個のセカンダリ レプリカをサポートします。 詳細については、「 [Always On 可用性グループの概要 &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)」を参照してください。  
  
    > [!IMPORTANT]  
    >  各可用性レプリカは、単一の Windows Server フェールオーバー クラスタリング (WSFC) クラスターの異なるノード上に存在する必要があります。 可用性グループの前提条件、制限事項、および推奨事項の詳細については、「 [Always On 可用性グループの前提条件、制限事項、および推奨事項」を参照してください。SQL Server;](prereqs-restrictions-recommendations-always-on-availability.md)。  
  
-   次の選択可能な可用性モードをサポートします。  
  
    -   *非同期コミットモード*。 この可用性モードは、距離を隔てて可用性レプリカが分散されている場合に効果的な災害復旧ソリューションです。  
  
    -   *同期コミットモード*。 この可用性モードは、パフォーマンスよりも高可用性とデータ保護が重視され、トランザクションの遅延が増加するのが欠点です。 1 つの可用性グループで、現在のプライマリ レプリカを含む、最大 3 つの同期コミット可用性レプリカをサポートできます。  
  
     詳細については、「可用性モード」を参照してください[。可用性グループを Always On](availability-modes-always-on-availability-groups.md)します。  
  
-   自動フェールオーバー、計画的な手動フェールオーバー (通常は単に "手動フェールオーバー" と呼ばれます)、および強制手動フェールオーバー (通常は単に "強制フェールオーバー" と呼ばれます) の複数の形式の可用性グループ フェールオーバーをサポートします。 詳細については、「[フェールオーバーとフェールオーバーモード」を参照してください。可用性グループを Always On](failover-and-failover-modes-always-on-availability-groups.md)します。  
  
-   次のアクティブ セカンダリ機能の一方または両方をサポートするように指定された可用性レプリカを構成できます。  
  
    -   セカンダリ レプリカとして動作中に、レプリカへの読み取り専用接続でそのデータベースにアクセスして読み込むことができる読み取り専用接続アクセス。 詳細については、「[アクティブなセカンダリ: 読み取り可能なセカンダリレプリカ」を参照してください。Always On 可用性グループ](https://msdn.microsoft.com/library/ff878253.aspx))] を使用します。  
  
    -   セカンダリ レプリカとして動作中に、そのデータベース上でバックアップ操作を実行します。 詳細については、「[アクティブなセカンダリ: セカンダリレプリカでのバックアップ](https://msdn.microsoft.com/library/ff878253.aspx)」を参照してください。  
  
     アクティブ セカンダリ機能を使用して、セカンダリ ハードウェアのリソース使用効率を高めることで、IT の効率性を改善し、コストを低減できます。 また、読み取りを目的としたアプリケーションやバックアップ ジョブをセカンダリ レプリカへとオフロードすることで、プライマリ レプリカのパフォーマンスを改善できます。  
  
-   可用性グループごとに 1 つの可用性グループ リスナーをサポートします。 
  *可用性グループ リスナー* は、AlwaysOn 可用性グループのプライマリ レプリカまたはセカンダリ レプリカ内のデータベースにアクセスするためにクライアントが接続できるサーバー名です。 可用性グループ リスナーは、プライマリ レプリカまたは読み取り専用セカンダリ レプリカに着信接続をダイレクトします。 リスナーは、可用性グループがフェールオーバーした後のアプリケーション フェールオーバーを高速化します。 詳細については、「[可用性グループリスナー、クライアント接続、およびアプリケーションのフェールオーバー」を参照してください。SQL Server;](../../listeners-client-connectivity-application-failover.md)。  
  
-   可用性グループのフェールオーバーを細かく制御する柔軟なフェールオーバー ポリシーをサポートします。 詳細については、「[フェールオーバーとフェールオーバーモード」を参照してください。可用性グループを Always On](failover-and-failover-modes-always-on-availability-groups.md)します。  
  
-   ページ破損に対する保護機能を提供する自動ページ修復をサポートします。 詳細については、「[可用性グループとデータベースミラーリングのためのページの自動修復 &#40;](../../../sql-server/failover-clusters/automatic-page-repair-availability-groups-database-mirroring.md)」を参照してください。  
  
-   安全性とパフォーマンスに優れたトランスポートを実現する、暗号化機能と圧縮機能をサポートします。  
  
-   可用性グループの展開と管理を簡単にするツールの統合セットが用意されています。これには次のツールが含まれます。  
  
    -   
  [!INCLUDE[tsql](../../../includes/tsql-md.md)] DDL ステートメント。 詳細については、「 [Always On 可用性グループの Transact-sql ステートメントの概要」を参照してください。SQL Server;](transact-sql-statements-for-always-on-availability-groups.md)。  
  
    -   
  [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ツール。  
  
        -   
  [!INCLUDE[ssAoNewAgWiz](../../../includes/ssaonewagwiz-md.md)] では、可用性グループの作成と構成を行います。 一部の環境では、このウィザードで、セカンダリ データベースを自動的に準備し、それらの各データベースに対するデータ同期を開始することもできます。 詳細については、「 [[新しい可用性グループ] ダイアログボックスの使用」を参照してください。SQL Server Management Studio;](use-the-new-availability-group-dialog-box-sql-server-management-studio.md)。  
  
        -   
  [!INCLUDE[ssAoAddDbWiz](../../../includes/ssaoadddbwiz-md.md)]では、既存の可用性グループに 1 つ以上のプライマリ データベースを追加できます。 一部の環境では、このウィザードで、セカンダリ データベースを自動的に準備し、それらの各データベースに対するデータ同期を開始することもできます。 詳細については、「 [可用性グループへのデータベース追加ウィザードの使用 (SQLServer)](availability-group-add-database-to-group-wizard.md)」を参照してください。  
  
        -   
  [!INCLUDE[ssAoAddRepWiz](../../../includes/ssaoaddrepwiz-md.md)] では、既存の可用性グループに 1 つ以上のセカンダリ レプリカを追加できます。 一部の環境では、このウィザードで、セカンダリ データベースを自動的に準備し、それらの各データベースに対するデータ同期を開始することもできます。 詳細については、「[可用性グループへのレプリカ追加ウィザードの使用」を参照してください。SQL Server Management Studio;](use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md)。  
  
        -   
  [!INCLUDE[ssAoFoAgWiz](../../../includes/ssaofoagwiz-md.md)]では、可用性グループに対して手動のフェールオーバーを開始できます。 フェールオーバーのターゲットとして指定するセカンダリ レプリカの構成と状態によっては、このウィザードで計画的または強制的な手動フェールオーバーを実行することもできます。 詳細については、[可用性グループのフェールオーバーウィザードの使用に関する説明を参照してください。SQL Server Management Studio;](use-the-fail-over-availability-group-wizard-sql-server-management-studio.md)。  
  
    -   AlwaysOn 可用性グループ、可用性レプリカ、および可用性データベースを監視し、AlwaysOn ポリシーの結果を評価する [!INCLUDE[ssAoDash](../../../includes/ssaodash-md.md)] 。 詳細については、「 [AlwaysOn ダッシュボードの使用」を参照してください。SQL Server Management Studio;](use-the-always-on-dashboard-sql-server-management-studio.md)。  
  
    -   既存の可用性グループに関する基本情報を表示する、[オブジェクト エクスプローラーの詳細] ペイン。 詳細については、「[オブジェクトエクスプローラーの詳細を使用して可用性グループを監視する」を参照してください。SQL Server Management Studio;](use-object-explorer-details-to-monitor-availability-groups.md)。  
  
    -   PowerShell コマンドレット。 詳細については、「 [Always On 可用性グループの PowerShell コマンドレットの概要」を参照してください。SQL は、を提供](overview-of-powershell-cmdlets-for-always-on-availability-groups-sql-server.md)します。  
  
##  <a name="TermsAndDefinitions"></a>用語と定義  
 可用性グループ  
 ひとまとまりでフェールオーバーされるデータベースのセット ( *可用性データベース*) のコンテナー。  
  
 可用性データベース  
 可用性グループに属しているデータベース。 可用性データベースごとに、可用性グループは 1 個の読み取り/書き込み可能なコピー ( *プライマリ データベース*) と 1 ～ 8 個の読み取り専用コピー (*セカンダリ データベース*) を管理します。  
  
 プライマリ サーバー  
 可用性データベースの読み取り/書き込み可能なコピー。  
  
 セカンダリ データベース (secondary database)  
 可用性データベースの読み取り専用コピー。  
  
 可用性グループ  
 可用性グループのインスタンス化。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の特定のインスタンスによってホストされ、可用性グループに属する各可用性データベースのローカル コピーを保持します。 可用性グループには、2 種類の可用性レプリカ ( *プライマリ レプリカ* と 1 ～ 8 個の *セカンダリ レプリカ*) があります。  
  
 プライマリ レプリカ  
 クライアントからプライマリ データベースへの読み取り/書き込み接続を可能にし、各プライマリ データベースのトランザクション ログ レコードをすべてのセカンダリ レプリカに送信する可用性レプリカ。  
  
 セカンダリ レプリカ  
 各可用性データベースのセカンダリ コピーを保持し、可用性グループの潜在的なフェールオーバー ターゲットとして機能する可用性レプリカ。 必要に応じて、セカンダリ レプリカは、セカンダリ データベースへの読み取り専用アクセスと、セカンダリ データベース上でのバックアップの作成をサポートできます。  
  
 可用性グループ リスナー  
 Always On 可用性グループのプライマリ レプリカまたはセカンダリ レプリカ内のデータベースにアクセスするためにクライアントが接続できるサーバー名。 可用性グループ リスナーは、プライマリ レプリカまたは読み取り専用セカンダリ レプリカに着信接続をダイレクトします。  
  
> [!NOTE]  
>  詳細については、「AlwaysOn 可用性グループの概要」を参照してください[。SQL は、を提供](overview-of-always-on-availability-groups-sql-server.md)します。  
  
##  <a name="Interoperability"></a>他のデータベースエンジン機能との相互運用性と共存  
 
  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] は、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]の次の機能またはコンポーネントと共に使用できます。  
  
-   [変更データキャプチャについてSQL Server;](../../../relational-databases/track-changes/about-change-data-capture-sql-server.md)  
  
-   [Change Tracking についてSQL サービス](../../../relational-databases/track-changes/about-change-tracking-sql-server.md)  
  
-   [包含データベース](../../../relational-databases/databases/contained-databases.md)  
  
-   [データベース暗号化](../../../relational-databases/security/encryption/transparent-data-encryption.md)  
  
-   [データベース スナップショット](database-snapshots-with-always-on-availability-groups-sql-server.md)  
  
-   [ストリーム](../../../relational-databases/blob/filestream-sql-server.md)  
  
-   [FileTable](../../../relational-databases/blob/filetables-sql-server.md)  
  
-   [ログ配布](../../log-shipping/about-log-shipping-sql-server.md)  
  
-   [リモート BLOB ストア (RBS)](../../../relational-databases/blob/remote-blob-store-rbs-sql-server.md)  
  
-   [レプリケーション](../../install-windows/install-sql-server-replication.md)  
  
-   [Service Broker](../../configure-windows/sql-server-service-broker.md)  
  
-   [SQL Server エージェント](../../../ssms/agent/sql-server-agent.md)  
  
-   [Reporting Services](reporting-services-with-always-on-availability-groups-sql-server.md)  
  
> [!WARNING]  
>  で[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]他の機能を使用する場合の制限事項と制限事項については、「 [Always On 可用性グループ: 相互運用性」を参照してください。SQL Server;](always-on-availability-groups-interoperability-sql-server.md)。  
  
##  <a name="RelatedTasks"></a>関連タスク  
  
-   [Always On 可用性グループを使用したはじめにSQL Server;](getting-started-with-always-on-availability-groups-sql-server.md)  
  
##  <a name="RelatedContent"></a>関連するコンテンツ  
  
-   **Blog**  
  
     [SQL Server Always On チームのブログ: AlwaysOn チームの公式 SQL Server ブログ](https://blogs.msdn.com/b/sqlalwayson/)  
  
     [CSS SQL Server エンジニアのブログ](https://blogs.msdn.com/b/psssql/)  
  
-   **ビデオ**  
  
     [Microsoft SQL Server コードネーム "Denali" Always On シリーズパート 1: 次世代の高可用性ソリューションの概要](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI302)  
  
     [Microsoft SQL Server コードネーム "Denali" Always On シリーズ第2部: AlwaysOn を使用したミッションクリティカルな高可用性ソリューションの構築](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI404)  
  
-   **ペーパー**  
  
     [高可用性とディザスターリカバリーのための Microsoft SQL Server Always On ソリューションガイド](https://go.microsoft.com/fwlink/?LinkId=227600)  
  
  
  
## <a name="see-also"></a>参照  
 [Always On 可用性グループの概要SQL Server;](overview-of-always-on-availability-groups-sql-server.md)   
 [AlwaysOn 可用性グループ &#40;SQL Server の前提条件、制限事項、推奨事項&#41;](prereqs-restrictions-recommendations-always-on-availability.md)   
 [Always On 可用性グループのためのサーバーインスタンスの構成SQL Server;](always-on-availability-groups-sql-server.md)   
 [可用性グループの作成と構成SQL Server;](creation-and-configuration-of-availability-groups-sql-server.md)   
 [可用性グループの管理SQL Server;](administration-of-an-availability-group-sql-server.md)   
 [可用性グループの監視 &#40;SQL Server&#41;](monitoring-of-availability-groups-sql-server.md)   
 [Always On 可用性グループの Transact-sql ステートメントの概要SQL Server;](transact-sql-statements-for-always-on-availability-groups.md)   
 [AlwaysOn 可用性グループ用の PowerShell コマンドレットの概要SQL Server;](overview-of-powershell-cmdlets-for-always-on-availability-groups-sql-server.md)  
  
