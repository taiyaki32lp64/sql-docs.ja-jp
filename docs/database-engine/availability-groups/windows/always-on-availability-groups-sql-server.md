---
title: '可用性グループ: 高可用性とディザスター リカバリーのソリューション'
description: Always On 可用性グループは SQL Server の高可用性/ディザスター リカバリー ソリューションであり、データベース ミラーリングに代わる機能をエンタープライズレベルで提供します。 この機能の基本と実用性について説明します。
ms.custom: seodec18
ms.date: 04/23/2019
ms.prod: sql
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
ms.openlocfilehash: 6eae33bebd834a79a62bd94c5dbe75f4c431b0ba
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68014819"
---
# <a name="always-on-availability-groups-a-high-availability-and-disaster-recovery-solution"></a>Always On 可用性グループ: 高可用性とディザスター リカバリーのソリューション
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 機能は、データベース ミラーリングに代わる、高可用性と災害復旧のためのエンタープライズ レベルのソリューションです。 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]で導入された [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] により、エンタープライズのユーザー データベースの可用性が最大限に高まります。 *可用性グループ* は、 *可用性データベース*として知られる、ひとまとまりでフェールオーバーされる個別のユーザー データベースのセットのためのフェールオーバー環境をサポートします。 可用性グループは、読み取り/書き込みプライマリ データベースのセットをサポートし、1 ～ 8 セットの対応するセカンダリ データベースをサポートします。 必要に応じて、セカンダリ データベースで読み取り専用アクセスまたはいくつかのバックアップ操作を利用できます。  
  
 可用性グループは、可用性レプリカのレベルでフェールオーバーします。 データベースの問題 (たとえば、データ ファイルの損失、データベースの削除、トランザクション ログの破損による障害が疑われる場合など) が発生してもフェールオーバーは行われません。  
 
 >[!NOTE]
 >Always On 可用性グループは、この可用性機能の完全な正式名称です。 省略形は、AOAG または AAG ではなく、AG です。 
  
##  <a name="Benefits"></a> 利点  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] には、データベースの可用性を向上し、リソースの使用を改善できる、豊富なオプションのセットが用意されています。 主なコンポーネントは次のとおりです。  
  
-   最大 9 つの可用性レプリカをサポートします。 *可用性グループ* は、SQL Server の特定のインスタンスによってホストされ、可用性グループに属する各可用性データベースのローカル コピーを保持します。 各可用性グループは、1 個のプライマリ レプリカと最大 8 個のセカンダリ レプリカをサポートします。 詳細については、「 [Always On 可用性グループの概要 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)」を参照してください。  
  
    > [!IMPORTANT]  
    >  各可用性レプリカは、単一の Windows Server フェールオーバー クラスタリング (WSFC) クラスターの異なるノード上に存在する必要があります。 可用性グループの前提条件、制限事項、推奨事項の詳細については、「 [Always On 可用性グループの前提条件、制限事項、および推奨事項 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)」を参照してください。  
  
-   次の選択可能な可用性モードをサポートします。  
  
    -   *非同期コミット モード*。 この可用性モードは、距離を隔てて可用性レプリカが分散されている場合に効果的な災害復旧ソリューションです。  
  
    -   *同期コミット モード*。 この可用性モードは、パフォーマンスよりも高可用性とデータ保護が重視され、トランザクションの遅延が増加するのが欠点です。 1 つの可用性グループで、現在のプライマリ レプリカを含む、最大 3 つの同期コミット可用性レプリカをサポートできます。  
  
     詳細については、「[可用性モード &#40;Always On 可用性グループ&#41;](../../../database-engine/availability-groups/windows/availability-modes-always-on-availability-groups.md)」を参照してください。 

     [!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)] では 3 つであった同期レプリカの最大数が、[!INCLUDE[ssSQL17](../../../includes/sssql17-md.md)] では 5 つに増加します。 この 5 つのレプリカのグループを、グループ内で自動フェールオーバーするように構成できます。 1 つのプライマリ レプリカと、4 つの同期セカンダリ レプリカがあります。
  
-   自動フェールオーバー、計画的な手動フェールオーバー (通常は単に "手動フェールオーバー" と呼ばれます)、および強制手動フェールオーバー (通常は単に "強制フェールオーバー" と呼ばれます) の複数の形式の可用性グループ フェールオーバーをサポートします。 詳細については、「 [フェールオーバーとフェールオーバー モード &#40;AlwaysOn 可用性グループ&#41;](../../../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md)、または PowerShell を使用して、AlwaysOn 可用性グループ上で計画的な手動フェールオーバーまたは強制手動フェールオーバー (強制フェールオーバー) を実行する方法について説明します。  
  
-   次のアクティブ セカンダリ機能の一方または両方をサポートするように指定された可用性レプリカを構成できます。  
  
    -   セカンダリ レプリカとして動作中に、レプリカへの読み取り専用接続でそのデータベースにアクセスして読み込むことができる読み取り専用接続アクセス。 詳細については、「[アクティブなセカンダリ:読み取り可能なセカンダリ レプリカ &#40;Always On 可用性グループ&#41;](../../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)」を参照してください。  
  
    -   セカンダリ レプリカとして動作中に、そのデータベース上でバックアップ操作を実行します。 詳細については、「[アクティブなセカンダリ:セカンダリ レプリカでのバックアップ &#40;Always On 可用性グループ&#41;](../../../database-engine/availability-groups/windows/active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md)」を参照してください。  
  
     アクティブ セカンダリ機能を使用して、セカンダリ ハードウェアのリソース使用効率を高めることで、IT の効率性を改善し、コストを低減できます。 また、読み取りを目的としたアプリケーションやバックアップ ジョブをセカンダリ レプリカへとオフロードすることで、プライマリ レプリカのパフォーマンスを改善できます。  
  
-   可用性グループごとに 1 つの可用性グループ リスナーをサポートします。 *可用性グループ リスナー* は、Always On 可用性グループのプライマリ レプリカまたはセカンダリ レプリカ内のデータベースにアクセスするためにクライアントが接続できるサーバー名です。 可用性グループ リスナーは、プライマリ レプリカまたは読み取り専用セカンダリ レプリカに着信接続をダイレクトします。 リスナーは、可用性グループがフェールオーバーした後のアプリケーション フェールオーバーを高速化します。 詳細については、「 [可用性グループ リスナー、クライアント接続、およびアプリケーションのフェールオーバー &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md)での 1 つ以上の可用性グループの構成と管理において重要です。  
  
-   可用性グループのフェールオーバーを細かく制御する柔軟なフェールオーバー ポリシーをサポートします。 詳細については、「[フェールオーバーとフェールオーバー モード &#40;Always On 可用性グループ&#41;](../../../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md)」を参照してください。  
  
-   ページ破損に対する保護機能を提供する自動ページ修復をサポートします。 詳細については、「[ページの自動修復 &#40;可用性グループ:データベース ミラーリング&#41;](../../../sql-server/failover-clusters/automatic-page-repair-availability-groups-database-mirroring.md)」を参照してください。  
  
-   安全性とパフォーマンスに優れたトランスポートを実現する、暗号化機能と圧縮機能をサポートします。  
  
-   可用性グループの展開と管理を簡単にするツールの統合セットが用意されています。これには次のツールが含まれます。  
  
    -   [!INCLUDE[tsql](../../../includes/tsql-md.md)] DDL ステートメント。 詳細については、「 [Always On 可用性グループの Transact-SQL ステートメントの概要 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/transact-sql-statements-for-always-on-availability-groups.md)」を参照してください。  
  
    -   [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ツール。  
  
        -   [!INCLUDE[ssAoNewAgWiz](../../../includes/ssaonewagwiz-md.md)] では、可用性グループの作成と構成を行います。 一部の環境では、このウィザードで、セカンダリ データベースを自動的に準備し、それらの各データベースに対するデータ同期を開始することもできます。 詳細については、「[新しい可用性グループ ダイアログ ボックスの使用 &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-new-availability-group-dialog-box-sql-server-management-studio.md)」を参照してください。  
  
        -   [!INCLUDE[ssAoAddDbWiz](../../../includes/ssaoadddbwiz-md.md)]では、既存の可用性グループに 1 つ以上のプライマリ データベースを追加できます。 一部の環境では、このウィザードで、セカンダリ データベースを自動的に準備し、それらの各データベースに対するデータ同期を開始することもできます。 詳細については、「 [可用性グループへのデータベース追加ウィザードの使用 (SQLServer)](../../../database-engine/availability-groups/windows/availability-group-add-database-to-group-wizard.md)」を参照してください。  
  
        -   [!INCLUDE[ssAoAddRepWiz](../../../includes/ssaoaddrepwiz-md.md)] では、既存の可用性グループに 1 つ以上のセカンダリ レプリカを追加できます。 一部の環境では、このウィザードで、セカンダリ データベースを自動的に準備し、それらの各データベースに対するデータ同期を開始することもできます。 詳細については、「[可用性グループへのレプリカ追加ウィザードの使用 &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md) を参照してください。  
  
        -   [!INCLUDE[ssAoFoAgWiz](../../../includes/ssaofoagwiz-md.md)]では、可用性グループに対して手動のフェールオーバーを開始できます。 フェールオーバーのターゲットとして指定するセカンダリ レプリカの構成と状態によっては、このウィザードで計画的または強制的な手動フェールオーバーを実行することもできます。 詳細については、「[可用性グループのフェールオーバー ウィザードの使用 &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-fail-over-availability-group-wizard-sql-server-management-studio.md)」を参照してください。  
  
    -   Always On 可用性グループ、可用性レプリカ、および可用性データベースを監視し、Always On ポリシーの結果を評価する [!INCLUDE[ssAoDash](../../../includes/ssaodash-md.md)]。 詳細については、「[Always On ダッシュボードの使用 &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)」を参照してください。  
  
    -   既存の可用性グループに関する基本情報を表示する、[オブジェクト エクスプローラーの詳細] ペイン。 詳細については、「[[オブジェクト エクスプローラーの詳細] を使用した可用性グループの監視 &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-object-explorer-details-to-monitor-availability-groups.md) を参照してください。  
  
    -   PowerShell コマンドレット。 詳細については、「 [Always On 可用性グループの PowerShell コマンドレットの概要 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-powershell-cmdlets-for-always-on-availability-groups-sql-server.md)」を参照してください。  
  
##  <a name="TermsAndDefinitions"></a> 用語と定義  
 **可用性グループ**  
 ひとまとまりでフェールオーバーされるデータベースのセット ( *可用性データベース*) のコンテナー。  
  
 **可用性データベース**  
 可用性グループに属しているデータベース。 可用性データベースごとに、可用性グループは 1 個の読み取り/書き込み可能なコピー ( *プライマリ データベース*) と 1 ～ 8 個の読み取り専用コピー (*セカンダリ データベース*) を管理します。  
  
 **プライマリ データベース**  
 可用性データベースの読み取り/書き込み可能なコピー。  
  
 **セカンダリ データベース**  
 可用性データベースの読み取り専用コピー。  
  
 **可用性レプリカ**  
 可用性グループのインスタンス化。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の特定のインスタンスによってホストされ、可用性グループに属する各可用性データベースのローカル コピーを保持します。 可用性グループには、2 種類の可用性レプリカ ( *プライマリ レプリカ* と 1 ～ 8 個の *セカンダリ レプリカ*) があります。  
  
 **プライマリ レプリカ**  
 クライアントからプライマリ データベースへの読み取り/書き込み接続を可能にし、各プライマリ データベースのトランザクション ログ レコードをすべてのセカンダリ レプリカに送信する可用性レプリカ。  
  
 **セカンダリ レプリカ**  
 各可用性データベースのセカンダリ コピーを保持し、可用性グループの潜在的なフェールオーバー ターゲットとして機能する可用性レプリカ。 必要に応じて、セカンダリ レプリカは、セカンダリ データベースへの読み取り専用アクセスと、セカンダリ データベース上でのバックアップの作成をサポートできます。  
  
 **可用性グループ リスナー**  
 Always On 可用性グループのプライマリ レプリカまたはセカンダリ レプリカ内のデータベースにアクセスするためにクライアントが接続できるサーバー名。 可用性グループ リスナーは、プライマリ レプリカまたは読み取り専用セカンダリ レプリカに着信接続をダイレクトします。  
  
> [!NOTE]  
>  詳細については、「 [Always On 可用性グループの概要 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)」を参照してください。  
  
##  <a name="Interoperability"></a> その他のデータベース エンジン機能との相互運用性と共存  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] は、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]の次の機能またはコンポーネントと共に使用できます。  
  
-   [変更データ キャプチャについて &#40;SQL Server&#41;](../../../relational-databases/track-changes/about-change-data-capture-sql-server.md)  
  
-   [変更の追跡について &#40;SQL Server&#41;](../../../relational-databases/track-changes/about-change-tracking-sql-server.md)  
  
-   [包含データベース](../../../relational-databases/databases/contained-databases.md)  
  
-   [データベース暗号化](../../../relational-databases/security/encryption/transparent-data-encryption.md)  
  
-   [データベース スナップショット](../../../database-engine/availability-groups/windows/database-snapshots-with-always-on-availability-groups-sql-server.md)  
  
-   [FILESTREAM](../../../relational-databases/blob/filestream-sql-server.md)  
  
-   [FileTable](../../../relational-databases/blob/filetables-sql-server.md)  
  
-   [ログ配布](../../../database-engine/log-shipping/about-log-shipping-sql-server.md)  
  
-   [リモート BLOB ストア (RBS)](../../../relational-databases/blob/remote-blob-store-rbs-sql-server.md)  
  
-   [レプリケーション](../../../relational-databases/replication/sql-server-replication.md)  
  
-   [Service Broker](../../../database-engine/configure-windows/sql-server-service-broker.md)  
  
-   [SQL Server エージェント](../../../ssms/agent/sql-server-agent.md)  
  
-   [Reporting Services](../../../database-engine/availability-groups/windows/reporting-services-with-always-on-availability-groups-sql-server.md)  
  
> [!WARNING]  
>  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] で他の機能を使用する場合の制限事項については、「[Always On 可用性グループ: 相互運用性 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-availability-groups-interoperability-sql-server.md)」を参照してください。  
  
##  <a name="RelatedTasks"></a> 関連タスク  
  
-   [Always On 可用性グループの概要 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/getting-started-with-always-on-availability-groups-sql-server.md)  
  
##  <a name="RelatedContent"></a> 関連コンテンツ  
  
-   **ブログ:**  
  
     [SQL Server Always On チーム ブログ:SQL Server Always On チームのオフィシャル ブログ](https://blogs.msdn.microsoft.com/sqlalwayson/)  
  
     [CSS SQL Server エンジニアのブログ](https://blogs.msdn.com/b/psssql/)  
  
-   **ビデオ:**  
  
     [Microsoft SQL Server コードネーム "Denali" Always On シリーズ パート 1: 次世代高可用性ソリューションの概要](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI302)  
  
     [Microsoft SQL Server コードネーム "Denali" Always On シリーズ パート 2: Always On を使用したミッション クリティカルな高可用性ソリューションの構築](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI404)  
  
-   **ホワイト ペーパー:**  
  
     [高可用性と災害復旧のための Microsoft SQL Server AlwaysOn ソリューション ガイド](https://go.microsoft.com/fwlink/?LinkId=227600)  
  
     [SQL Server 2012 に関する Microsoft ホワイト ペーパー](https://msdn.microsoft.com/library/hh403491.aspx)  
  
     [SQL Server ユーザー諮問チームのホワイト ペーパー](https://techcommunity.microsoft.com/t5/DataCAT/bg-p/DataCAT/)  
  
## <a name="see-also"></a>参照  
 [AlwaysOn 可用性グループの概要 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [AlwaysOn 可用性グループの前提条件、制限事項、および推奨事項 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)   
 [Always On 可用性グループのためのサーバー インスタンスの構成 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configuration-of-a-server-instance-for-always-on-availability-groups-sql-server.md)   
 [可用性グループの作成と構成 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/creation-and-configuration-of-availability-groups-sql-server.md)   
 [可用性グループの管理 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/administration-of-an-availability-group-sql-server.md)   
 [可用性グループの監視 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/monitoring-of-availability-groups-sql-server.md)   
 [Always On 可用性グループの Transact-SQL ステートメントの概要 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/transact-sql-statements-for-always-on-availability-groups.md)   
 [Always On 可用性グループの PowerShell コマンドレットの概要 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-powershell-cmdlets-for-always-on-availability-groups-sql-server.md)  
  
  
