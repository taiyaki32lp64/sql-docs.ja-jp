---
title: AlwaysOn 可用性グループを使用したはじめに (SQL Server) |Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], deploying
- Availability Groups [SQL Server], about
ms.assetid: 33f2f2d0-79e0-4107-9902-d67019b826aa
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2e809d84071089ce57c66bc8f9a388203923fe66
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75228763"
---
# <a name="getting-started-with-alwayson-availability-groups-sql-server"></a>AlwaysOn 可用性グループの概要 (SQL Server)
  このトピックでは、 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] をサポートするように [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] のインスタンスを構成する手順と可用性グループを作成、管理、および監視する手順について説明します。  
  
  
##  <a name="BeforeYouBegin"></a>開始する前に  
  
###  <a name="RecommendedReading"></a>推奨資料  
 可用性グループを初めて作成する場合は、あらかじめ次のトピックに目を通しておくことをお勧めします。  
  
-   [AlwaysOn 可用性グループ &#40;SQL Server の概要&#41;](overview-of-always-on-availability-groups-sql-server.md)  
  
-   [AlwaysOn 可用性グループ &#40;SQL Server の前提条件、制限事項、推奨事項&#41;](prereqs-restrictions-recommendations-always-on-availability.md)  
  
##  <a name="ConfigSI"></a>AlwaysOn 可用性グループをサポートするための SQL Server のインスタンスの構成  
  
||手順|リンク|  
|------|----------|-----------|  
|![Checkbox](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|**を[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]有効にします。** 可用性グループに参加する [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] のすべてのインスタンスで [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 機能を有効にする必要があります。<br /><br /> **前提条件:** ホストコンピューターは、Windows Server フェールオーバークラスタリング (WSFC) ノードである必要があります。<br /><br /> その他の前提条件については、「[AlwaysOn 可用性グループの前提条件、制限事項、および推奨事項 &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md)」の「SQL Server インスタンスの前提条件と制限」を参照してください。|[AlwaysOn 可用性グループを有効または無効にする](enable-and-disable-always-on-availability-groups-sql-server.md)|  
|![Checkbox](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|**データベースミラーリングエンドポイントを作成します (存在しない場合)。** 各サーバー インスタンスに、 [データベース ミラーリング エンドポイント](../../database-mirroring/the-database-mirroring-endpoint-sql-server.md)が存在することを確認します。 サーバー インスタンスでは、このエンドポイントを使用して、他のサーバー インスタンスから [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] の接続を受信します。|データベース ミラーリング エンドポイントが存在するかどうかを確認するには、次のカタログ ビューを使用します。 [sys.database_mirroring_endpoints](/sql/relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql)<br /><br /> **Windows 認証の場合:** 以下を使用してデータベースミラーリングエンドポイントを作成するには:<br /><br /> [新しい可用性グループ ウィザード](use-the-availability-group-wizard-sql-server-management-studio.md)<br /><br /> [Transact-sql](../../database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)<br /><br /> [SQL Server PowerShell](database-mirroring-always-on-availability-groups-powershell.md)<br /><br /> **証明書認証の場合:** を使用してデータベースミラーリングエンドポイントを作成するには <br />                    [Transact-sql](../../database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)|  
  
##  <a name="ConfigAG"></a>新しい可用性グループの作成と構成  
  
||手順|リンク|  
|------|----------|-----------|  
|![Checkbox](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|**可用性グループを作成します。** 可用性グループに追加するデータベースをホストする [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスで可用性グループを作成します。<br /><br /> 可用性グループを作成する [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスで、少なくとも初期プライマリ レプリカを作成します。 1 ～ 4 個のセカンダリ レプリカを指定できます。 可用性グループとレプリカのプロパティについては、「[CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-availability-group-transact-sql)」をご覧ください。<br /><br /> 
  [可用性グループ リスナー](../../listeners-client-connectivity-application-failover.md)を作成することを強くお勧めします。<br /><br /> **前提条件:** 特定の可用性[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]グループの可用性レプリカをホストするのインスタンスは、1つの WSFC クラスターの別々のノードに存在する必要があります。 唯一の例外は、別の WSFC クラスターに移行するときに、可用性グループは一時的に 2 つのクラスターにまたがることができるという点です。<br /><br /> その他の前提条件については、「[AlwaysOn 可用性グループの前提条件、制限事項、推奨事項 &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md)」の「可用性グループの前提条件と制限」、「可用性データベースの前提条件と制限」、および「SQL Server インスタンスの前提条件と制限」を参照してください。|可用性グループを作成する場合は、次のツールを使用できます。<br /><br /> [新しい可用性グループ ウィザード](use-the-availability-group-wizard-sql-server-management-studio.md)<br /><br /> [Transact-sql](create-an-availability-group-transact-sql.md)<br /><br /> [SQL Server PowerShell](create-an-availability-group-transact-sql.md)|  
|![Checkbox](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|**セカンダリレプリカを可用性グループに参加させます。** セカンダリ レプリカをホストしている [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] の各インスタンスに接続し、ローカル セカンダリ レプリカを可用性グループに参加させます。|[可用性グループにセカンダリレプリカを参加させる](join-a-secondary-replica-to-an-availability-group-sql-server.md)<br /><br /> ヒント: 新しい可用性グループ ウィザードを使用すると、この手順が自動化されます。|  
|![Checkbox](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|**セカンダリデータベースを準備します。** セカンダリ レプリカをホストしている各サーバー インスタンスで、RESTORE WITH NORECOVERY を使用してプライマリ データベースのバックアップを復元します。|[セカンダリデータベースを手動で準備する](manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)<br /><br /> ヒント: 新しい可用性グループ ウィザードを使用して、セカンダリ データベースを自動的に準備できます。 詳細については、「[[最初のデータの同期を選択] ページ &#40;AlwaysOn 可用性グループ ウィザード&#41;](select-initial-data-synchronization-page-always-on-availability-group-wizards.md)」の「初期データの完全同期を使用するための前提条件」を参照してください。|  
|![Checkbox](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|**セカンダリデータベースを可用性グループに参加させます。** セカンダリ レプリカをホストしている各サーバー インスタンスで、各ローカル セカンダリ データベースを可用性グループに参加させます。 可用性グループに参加すると、セカンダリ データベースは対応するプライマリ データベースとのデータ同期を開始します。|[可用性グループへのセカンダリデータベースの参加](join-a-secondary-database-to-an-availability-group-sql-server.md)<br /><br /> ヒント: 各セカンダリ レプリカにそれぞれセカンダリ データベースが存在する場合は、新しい可用性グループ ウィザードでこの手順を実行できます。|  
||**可用性グループリスナーを作成します。**  可用性グループ リスナーをまだ作成していない場合、可用性グループを作成するときにこの手順を実行する必要があります。|[可用性グループリスナー &#40;SQL Server を作成または構成&#41;](create-or-configure-an-availability-group-listener-sql-server.md)|  
|![Checkbox](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|**アプリケーション開発者にリスナーの DNS ホスト名を指定します。**  開発者は、可用性グループ リスナーに接続要求を送信するために、接続文字列でこの DNS 名を指定する必要があります。 詳細については、「 [可用性グループ リスナー、クライアント接続、およびアプリケーションのフェールオーバー &#40;SQL Server&#41;](../../listeners-client-connectivity-application-failover.md)での 1 つ以上の可用性グループの構成と管理において重要です。|「 [可用性グループ リスナーの作成または構成 &#40;SQL Server&#41;](create-or-configure-an-availability-group-listener-sql-server.md)|  
|![Checkbox](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|**バックアップジョブをどこで構成するかを設定します。**  セカンダリ データベースでバックアップを実行する場合は、自動バックアップ設定を考慮に入れてバックアップ ジョブのスクリプトを作成する必要があります。 可用性グループの可用性レプリカをホストする各サーバー インスタンスで、可用性グループのデータベースごとにスクリプトを作成します。|「[可用性レプリカでのバックアップの構成 &#40;SQLServer&#41;](configure-backup-on-availability-replicas-sql-server.md)」の「補足情報: セカンダリ レプリカでバックアップを構成した後」|  
  
##  <a name="ManageAGsEtc"></a>可用性グループ、レプリカ、およびデータベースの管理  
  
> [!NOTE]  
>  可用性グループとレプリカのプロパティについては、「[CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-availability-group-transact-sql)」をご覧ください。  
  
 既存の可用性グループの管理には、次のタスクが 1 つ以上含まれます。  
  
|タスク|Link|  
|----------|----------|  
|可用性グループの [柔軟なフェールオーバー ポリシー](flexible-automatic-failover-policy-availability-group.md) を変更して、自動フェールオーバーを実行する条件を制御します。 このポリシーは、自動フェールオーバーが可能な場合にのみ関係します。|[可用性グループの柔軟なフェールオーバーポリシーを構成する](configure-flexible-automatic-failover-policy.md)|  
|計画的な手動フェールオーバーか、 *強制フェールオーバー*と通常呼ばれる強制手動フェールオーバー (データ損失の可能性あり) を実行します。 詳細については、「[フェールオーバーとフェールオーバー モード &#40;AlwaysOn 可用性グループ&#41;](failover-and-failover-modes-always-on-availability-groups.md)」を参照してください。|[計画的な手動フェールオーバーを実行する](perform-a-planned-manual-failover-of-an-availability-group-sql-server.md)<br /><br /> [強制手動フェールオーバーを実行する](perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)|  
|一連の定義済みポリシーを使用して、可用性グループとレプリカおよびデータベースの正常性を表示します。|[ポリシーベースの管理を使用して可用性グループの正常性を表示する](use-always-on-policies-to-view-the-health-of-an-availability-group-sql-server.md)<br /><br /> [AlwaysOn グループ ダッシュボードの使用](use-the-always-on-dashboard-sql-server-management-studio.md)|  
|セカンダリ レプリカを追加または削除します。|[セカンダリレプリカの追加](add-a-secondary-replica-to-an-availability-group-sql-server.md)<br /><br /> [セカンダリレプリカの削除](remove-a-secondary-replica-from-an-availability-group-sql-server.md)|  
|可用性データベースを中断または再開します。 セカンダリ データベースを中断すると、データベースを再開するまで現在の状態が維持されます。|[データベースを中断する](suspend-an-availability-database-sql-server.md)<br /><br /> [データベースの再開](resume-an-availability-database-sql-server.md)|  
|データベースを追加または削除します。|[データベースを追加する](availability-group-add-a-database.md)<br /><br /> [セカンダリ データベースの削除](remove-a-secondary-database-from-an-availability-group-sql-server.md)<br /><br /> [プライマリデータベースを削除する](remove-a-primary-database-from-an-availability-group-sql-server.md)|  
|可用性グループ リスナーを再構成または作成します。|[可用性グループリスナーの作成または構成](create-or-configure-an-availability-group-listener-sql-server.md)|  
|可用性グループを削除します。|[可用性グループの削除](remove-an-availability-group-sql-server.md)|  
|ファイルの追加操作のトラブルシューティングを行います。 これは、プライマリ データベースとセカンダリ データベースのファイル パスが異なる場合に必要となります。|[失敗したファイルの追加操作のトラブルシューティング](troubleshoot-a-failed-add-file-operation-always-on-availability-groups.md)|  
|可用性レプリカのプロパティを変更します。|[可用性モードの変更](change-the-availability-mode-of-an-availability-replica-sql-server.md)<br /><br /> [フェールオーバーモードの変更](change-the-failover-mode-of-an-availability-replica-sql-server.md)<br /><br /> [バックアップの優先順位を構成する (および自動バックアップ設定)](configure-backup-on-availability-replicas-sql-server.md)<br /><br /> [読み取り専用アクセスの構成](configure-read-only-access-on-an-availability-replica-sql-server.md)<br /><br /> [読み取り専用ルーティングの構成](configure-read-only-routing-for-an-availability-group-sql-server.md)<br /><br /> [セッションタイムアウト期間の変更](change-the-session-timeout-period-for-an-availability-replica-sql-server.md)|  
  
##  <a name="MonitorAGsEtc"></a>可用性グループの監視  
 AlwaysOn 可用性グループのプロパティと状態を監視するには、次のツールを使用します。  
  
|ツール|簡単な説明|リンク|  
|----------|-----------------------|-----------|  
|System Center Monitoring pack for SQL Server|Monitoring pack for SQL Server (SQLMP) は、可用性グループ、可用性レプリカ、および可用性データベースを IT 管理者が監視するための推奨ソリューションです。 
  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] に特に関連する監視機能は次のとおりです。<br /><br /> 可用性グループ、可用性レプリカ、および可用性データベースを多数のコンピューターから自動検出する機能。 これにより、 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] の在庫を簡単に追跡できます。<br /><br /> System Center Operations Manager (SCOM) の完全な警告機能とチケット機能。 これらの機能は、問題の早期解決を可能にする詳細な情報を提供します。<br /><br /> ポリシー ベースの管理 (PBM) を使用した AlwaysOn 正常性状態の監視のカスタム拡張機能。<br /><br /> 正常性状態は、可用性データベースから可用性レプリカにロールアップされます。<br /><br /> System Center Operations Manager コンソールから [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] を管理するカスタム タスク。|監視パック (SQLServerMP.msi) および *SQL Server Management Pack Guide for System Center Operations Manager* (SQLServerMPGuide.doc) をダウンロードするには、以下を参照してください。<br /><br /> [SQL Server 用 System Center 監視パック](https://www.microsoft.com/download/details.aspx?displaylang=en&id=10631)|  
|[!INCLUDE[tsql](../../../includes/tsql-md.md)]|
  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] のカタログ ビューと動的管理ビューは、可用性グループとそのレプリカ、データベース、リスナー、および WSFC クラスター環境に関する豊富な情報を提供します。|[Transact-sql&#41;&#40;可用性グループの監視](monitor-availability-groups-transact-sql.md)|  
|[!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]|
  **[オブジェクト エクスプローラーの詳細]** ペインには、接続先の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスでホストされている可用性グループの基本情報が表示されます。<br /><br /> ヒント: このペインを使用して、複数の可用性グループ、レプリカ、またはデータベースを選択し、選択したオブジェクトで一般的な管理タスク (可用性グループからの複数の可用性レプリカまたはデータベースの削除など) を実行します。|[オブジェクトエクスプローラーの詳細を使用して可用性グループを監視する](use-object-explorer-details-to-monitor-availability-groups.md)|  
|[!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]|[**プロパティ**] ダイアログボックスを使用すると、可用性グループ、レプリカ、またはリスナーのプロパティを表示できます。また、場合によっては、値を変更することもできます。|[可用性グループのプロパティ](view-availability-group-properties-sql-server.md)<br /><br /> [可用性レプリカのプロパティ](view-availability-replica-properties-sql-server.md)<br /><br /> [可用性グループリスナーのプロパティ](view-availability-group-listener-properties-sql-server.md)|  
|システム モニター|
  **SQLServer:Availability Replica** パフォーマンス オブジェクトには、可用性レプリカに関する情報を報告するパフォーマンス カウンターが含まれています。|[SQL Server、可用性レプリカ](../../../relational-databases/performance-monitor/sql-server-availability-replica.md)|  
|システム モニター|
  **SQLServer:Database Replica** パフォーマンス オブジェクトには、特定のセカンダリ レプリカのセカンダリ データベースに関する情報を報告するパフォーマンス カウンターが含まれています。<br /><br /> SQL Server の **SQLServer:Databases** オブジェクトには、トランザクション ログの利用状況などを監視するパフォーマンス カウンターが含まれています。 可用性データベースでのトランザクション ログの利用状況の監視に関連性が高いカウンターは、 **[Log Flush Write Time (ms)]**、 **[Log Flushes/sec]**、 **[Log Pool Cache Misses/sec]**、 **[Log Pool Disk Reads/sec]**、および **[Log Pool Requests/sec]** です。|[SQL Server、データベースレプリカ](../../../relational-databases/performance-monitor/sql-server-database-replica.md)<br /><br /> [SQL Server、Databases オブジェクト](../../../relational-databases/performance-monitor/sql-server-databases-object.md)|  
  
##  <a name="RelatedContent"></a>関連するコンテンツ  
  
-   **ビデオ-alwayson の概要:**  [Microsoft SQL Server コードネーム "Denali" alwayson シリーズパート 1: 次世代の高可用性ソリューションの概要](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI302)  
  
-   **ビデオ-Alwayson の詳細:**  [Microsoft SQL Server コードネーム "Denali" alwayson シリーズパート 2: Alwayson を使用したミッションクリティカルな高可用性ソリューションの構築](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI404)  
  
-   **ホワイトペーパー:**  [高可用性とディザスターリカバリーのための AlwaysOn ソリューションガイドの Microsoft SQL Server](https://go.microsoft.com/fwlink/?LinkId=227600)  
  
-   **ブログ:**  [SQL Server Alwayson チームのブログ: alwayson チームの公式 SQL Server のブログ](https://blogs.msdn.com/b/sqlalwayson/)  
  
## <a name="see-also"></a>参照  
 [AlwaysOn 可用性グループ &#40;SQL Server&#41;](always-on-availability-groups-sql-server.md)   
 [AlwaysOn 可用性グループ &#40;SQL Server の概要&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [AlwaysOn 可用性グループ &#40;SQL Server のサーバーインスタンスの構成&#41;](configuration-of-a-server-instance-for-always-on-availability-groups-sql-server.md)   
 [可用性グループの作成と構成 &#40;SQL Server&#41;](creation-and-configuration-of-availability-groups-sql-server.md)   
 [可用性グループの監視 &#40;SQL Server&#41;](monitoring-of-availability-groups-sql-server.md)   
 [AlwaysOn 可用性グループ &#40;SQL Server の Transact-sql ステートメントの概要&#41;](transact-sql-statements-for-always-on-availability-groups.md)   
 [AlwaysOn 可用性グループ &#40;SQL Server の PowerShell コマンドレットの概要&#41;](overview-of-powershell-cmdlets-for-always-on-availability-groups-sql-server.md)  
  
