---
title: Reporting Services と AlwaysOn 可用性グループ (SQL Server) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Reporting Services, AlwaysOn Availability Groups
- Availability Groups [SQL Server], interoperability
ms.assetid: edeb5c75-fb13-467e-873a-ab3aad88ab72
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8fef73519d067218a152e35bad2db9e1bae3372c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62789238"
---
# <a name="reporting-services-with-alwayson-availability-groups-sql-server"></a>Reporting Services と AlwaysOn 可用性グループ (SQL Server)
  このトピックでは、 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] の [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] (AG) と [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]を組み合わせて利用する方法について説明します。 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] と [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] を使用するデータベースのシナリオとしては、レポート データ ソース、レポート サーバー データベース、レポート デザインの 3 つが考えられます。 3 つのシナリオでは、それぞれサポートされる機能と必要な構成が異なります。  
  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] データ ソースで [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] を使用する大きな利点は、プライマリ データベースのフェールオーバー機能としての読み取り可能なセカンダリ レプリカをレポート データ ソースとしても利用できることです。  
  
 に関する一般情報について[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]を参照してください[SQL Server 2012 の AlwaysOn に関する FAQ (https://msdn.microsoft.com/sqlserver/gg508768)](https://msdn.microsoft.com/sqlserver/gg508768)します。  
  
   
  
##  <a name="bkmk_requirements"></a> Reporting Services と AlwaysOn 可用性グループを使用するための要件  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]  [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]を使用するためには、.Net 3.5 SP1 の修正プログラムをダウンロードしてインストールする必要があります。 この修正プログラムを適用すると、AG 機能を使う SQL クライアントが新たにサポートされ、さらに、接続文字列プロパティとして **ApplicationIntent** および **MultiSubnetFailover**がサポートされます。 レポート サーバーをホストする各コンピューターにこの修正プログラムがインストールされていない場合、ユーザーがレポートをプレビューしようとすると、以下のようなエラー メッセージが表示され、レポート サーバーのトレース ログに記録されます。  
  
> **エラー メッセージ:** "キーワードはサポートされていません:'applicationintent'"  
  
 このメッセージは、 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] の接続文字列に [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] のプロパティが含まれているとき、そのプロパティをサーバー側が認識できなかった場合に生成されます。 レポート サーバー側でリモート エラーが有効にされている場合、[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] のユーザー インターフェイスで [接続テスト] ボタンをクリックしたときや、レポートをプレビューしたときにこのエラー メッセージが表示されます。  
  
 必要な修正プログラムの詳細については、「 [KB 2654347 - .NET Framework 3.5 SP1 に SQL Server 2012 の AlwaysOn 機能のサポートを導入する修正プログラム](https://go.microsoft.com/fwlink/?LinkId=242896)」をご覧ください。  
  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] のその他の要件については、「[AlwaysOn 可用性グループの前提条件、制限事項、および推奨事項 &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md)」を参照してください。  
  
> [!NOTE]  
>  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] の機能がサポートする範囲に、[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] の構成ファイル (**RSreportserver.config** など) は含まれません。 いずれかのレポート サーバーの構成ファイルに手動で変更を加えた場合は、そのレプリカを手動で更新する必要があります。  
  
##  <a name="bkmk_reportdatasources"></a> レポート データ ソースと可用性グループ  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] を使用した [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] データ ソースの動作は、AG 環境の構成内容によって異なります。  
  
 レポート データ ソースに [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] を利用するには、可用性グループ " *リスナーの DNS 名*" を使用するようにレポート データ ソースの接続文字列を構成する必要があります。 サポートされているデータ ソースは次のとおりです。  
  
-   SQL Native Client を使用した ODBC データ ソース。  
  
-   SQL クライアント (レポート サーバーには .Net の修正プログラムを適用)。  
  
 接続文字列には、セカンダリ レプリカを使って読み取り専用レポートを生成するようにレポート クエリ要求を構成する、AlwaysOn の新しい接続プロパティを含めることもできます。 レポート要求にセカンダリ レプリカを使うことによって、読み取り/書き込み可能なプライマリ レプリカへの負荷を軽減することができます。 次の図は、3 つのレプリカから成る AG 構成の例です。 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] データ ソースの接続文字列は ApplicationIntent=ReadOnly で構成されています。 この例のレポート クエリ要求はセカンダリ レプリカに送信され、プライマリ レプリカには送信されません。  
  
 ![AG グループを使用する SSRS データソース](../../media/rs-alwayson-basic.gif "AG グループを使用する SSRS データソース")  
  
 次に接続文字列の例を示します。[AvailabilityGroupListenerName] は、レプリカの作成時に構成された **"リスナーの DNS 名"** です。  
  
 `Data Source=[AvailabilityGroupListenerName];Initial Catalog = AdventureWorks2008R2; ApplicationIntent=ReadOnly`  
  
 **のユーザー インターフェイスにある** [接続テスト] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] ボタンでは、接続が確立可能であるかどうかは検証されますが、AG の構成は検証されません。 たとえば、AG に属していないサーバーへの接続文字列に ApplicationIntent を含めても、このパラメーターは無視されます。 **[接続テスト]** ボタンによって検証されるのは、指定されたサーバーへの接続が確立可能であるかどうか、という点のみです。  
  
 接続文字列の編集方法は、レポートの作成方法とパブリッシュ方法によって異なります。  
  
-   **ネイティブ モード:** 共有データ ソースとは、既にネイティブ モードのレポート サーバーにパブリッシュされたレポートのレポート マネージャーを使用します。  
  
-   **SharePoint モード:** 既に SharePoint サーバーにパブリッシュされたレポートには、ドキュメント ライブラリ内の SharePoint 構成ページを使用します。  
  
-   **レポート デザイン:** [!INCLUDE[ssRBDenali](../../../includes/ssrbdenali-md.md)] または [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] when you are creating new repまたはts. 詳細については、このトピックのレポート デザインに関するセクションを参照してください。  
  
 **その他のリソース:**  
  
-   [レポート データ ソースを管理する](../../../reporting-services/report-data/manage-report-data-sources.md)  
  
-   使用できる接続文字列プロパティの詳細については、「 [Using Connection String Keywords with SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)」をご覧ください。  
  
-   可用性グループ リスナーに関する必須情報については、「[可用性グループ リスナーの作成または構成 &#40;SQL Server&#41;](create-or-configure-an-availability-group-listener-sql-server.md)」を参照してください。  
  
 **注意点 :** 通常、セカンダリ レプリカがプライマリ レプリカからデータの変更を受け取るまでには時間差が生じます。 プライマリ レプリカとセカンダリ レプリカ間に生じる更新の時間差は、次の要因によって変動します。  
  
-   セカンダリ レプリカの数。 セカンダリ レプリカが 1 つ構成に追加されるごとに時間差は大きくなります。  
  
-   プライマリ レプリカとセカンダリ レプリカの地理的な位置と両者の距離。 たとえば、セカンダリ レプリカとプライマリ レプリカが同じ建物内に存在した場合と比べ、異なるデータ センターに存在している方が通常は時間差が大きくなります。  
  
-   各レプリカの可用性モードの構成。 プライマリ レプリカは、セカンダリ レプリカがディスクにトランザクションを書き込むまで、データベースに対するトランザクションをコミットせずに待機する場合があります。待機するかどうかを決めるのが可用性モードです。 詳細については、の「可用性モード」を参照してください。 [AlwaysOn 可用性グループの概要&#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)します。  
  
 読み取り専用のセカンダリ レプリカを [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] のデータ ソースとして使用する場合は、データ更新の時間差が、レポート ユーザーの想定を越えることのないように注意してください。  
  
##  <a name="bkmk_reportdesign"></a> レポート デザインと可用性グループ  
 [!INCLUDE[ssRBDenali](../../../includes/ssrbdenali-md.md)] または [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]のレポート プロジェクトでレポートをデザインする際、ユーザーは、レポート データ ソースの接続文字列に、 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]の新しい接続プロパティを含めることができます。 新しい接続プロパティのサポート状況は、ユーザーがどこでレポートをプレビューするかによって異なります。  
  
-   **ローカル プレビュー:** [!INCLUDE[ssRBDenali](../../../includes/ssrbdenali-md.md)] と [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] use the .Net framework 4.0 と support [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] の接続文字列プロパティがサポートされます。  
  
-   **リモートまたはサーバー モード プレビュー:** [!INCLUDE[ssRBDenali](../../../includes/ssrbdenali-md.md)]でレポートをプレビューするか、レポート サーバーに対してレポートをパブリッシュした後、次のようなエラーが表示された場合、プレビュー対象となるレポートのレポート サーバーに [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]用の .Net Framework 3.5 SP1 修正プログラムがインストールされていません。  
  
> **エラー メッセージ:** "キーワードはサポートされていません:'applicationintent'"  
  
##  <a name="bkmk_reportserverdatabases"></a> レポート サーバー データベースと可用性グループ  
 Reporting Services は、レポート サーバー データベースへの [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] の使用をサポートしていますが、これには一定の制限があります。 レポート サーバー データベースをレプリカの一部として AG 内に構成することはできますが、フェールオーバーが発生しても、 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] は、レポート サーバー データベースに対して別のレプリカを自動的には使用しません。  
  
 フェールオーバーと復旧を完了させるには、手動でのアクションまたはカスタム オートメーション スクリプトが必要です。 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] のフェールオーバー後は、これらのアクションが完了するまで、レポート サーバーの機能が正常に動作しない可能性があります。  
  
> [!NOTE]  
>  レポート サーバー データベースに対するフェールオーバーと災害復旧を検討している場合は、レポート サーバーの暗号化キーのコピーを必ずバックアップするようにお勧めします。  
  
###  <a name="bkmk_differences_in_server_mode"></a> SharePoint モードとネイティブ モード間の違い  
 このセクションでは、 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]との連携の観点から、SharePoint モードのレポート サーバーとネイティブ モードのレポート サーバーの違いについて説明します。  
  
 SharePoint レポート サーバーでは、作成した **サービス アプリケーションごとに** 3 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] つのデータベースが作成されます。 SharePoint モードのレポート サーバー データベースへの接続は、サービス アプリケーションを作成するときに、SharePoint サーバーの全体管理で構成します。 データベースの既定の名前には、サービス アプリケーションに関連付けられた GUID が含まれます。 SharePoint モードのレポート サーバーのデータベース名の例を次に示します。  
  
-   ReportingService_85c08ac3c8e64d3cb400ad06ed5da5d6  
  
-   ReportingService_85c08ac3c8e64d3cb400ad06ed5da5d6TempDB  
  
-   ReportingService_85c08ac3c8e64d3cb400ad06ed5da5d6_Alerting  
  
 ネイティブ モードのレポート サーバーでは、 **2** つのデータベースを使用します。 ネイティブ モードのレポート サーバーのデータベース名の例を次に示します。  
  
-   ReportServer  
  
-   ReportServerTempDB  
  
 Alerting データベースとそれに関連する機能は、ネイティブ モードではサポートされず、使用されません。 ネイティブ モードのレポート サーバーの構成は、 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 構成マネージャーで行います。 SharePoint モードの「クライアント アクセス ポイント」SharePoint の構成の一部として作成した名前を指定するサービス アプリケーション データベースの名前を構成できます。 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]を使用して SharePoint を構成する方法については、[「Configure and manage SQL Server availability groups for SharePoint Server」(SharePoint Server の SQL Server 可用性グループの構成と管理) (https://go.microsoft.com/fwlink/?LinkId=245165)](https://go.microsoft.com/fwlink/?LinkId=245165) を参照してください。  
  
> [!NOTE]
>  SharePoint モードのレポート サーバーでは、 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] サービス アプリケーション データベースと SharePoint コンテンツ データベースの同期処理が行われます。 レポート サーバー データベースとコンテンツ データベースは一体で管理することが大切です。 1 つのまとまりとしてフェールオーバーと復元を行うことができるよう、同じ可用性グループで構成することを検討してください。 次のシナリオを考えてみましょう。  
> 
>  -   コンテンツ データベースを復元またはフェールオーバーします。差し替わるコンテンツ データベースのコピーには、レポート サーバー データベースに対する直近の変更が反映されていません。  
> -   [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] の同期処理で、コンテンツ データベースとレポート サーバー データベース内の一連の項目について両者の相違点が検出されます。  
> -   同期処理では、コンテンツ データベース内の項目が削除または更新されます。  
  
###  <a name="bkmk_prepare_databases"></a> 可用性グループに使用するレポート サーバー データベースの準備  
 以下に示したのは、レポート サーバー データベースを準備して [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]に追加する基本的な手順です。  
  
-   可用性グループを作成し、 *リスナーの DNS 名*を構成します。  
  
-   **プライマリ レプリカ:** レポート サーバー データベースが 1 つの可用性グループの一部になるように構成し、すべてのレポート サーバー データベースを含んだプライマリ レプリカを作成します。  
  
-   **セカンダリ レプリカ:** 1 つまたは複数のセカンダリ レプリカを作成します。 プライマリ レプリカからセカンダリ レプリカへとデータベースをコピーする際は、'RESTORE WITH NORECOVERY' を使って、セカンダリ レプリカごとにデータベースを復元するのが一般的です。 セカンダリ レプリカの作成およびデータの同期動作の検証の詳細については、「[AlwaysOn セカンダリ データベース上のデータ移動の開始 &#40;SQL Server&#41;](start-data-movement-on-an-always-on-secondary-database-sql-server.md)」を参照してください。  
  
-   **レポート サーバーの資格情報:** プライマリに対して作成したセカンダリ レプリカ上に、レポート サーバーの適切な資格情報を作成する必要があります。 実際の手順は、[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 環境で使用する認証の種類 (Window [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] サービス アカウント、Windows ユーザー アカウント、SQL Server 認証) によって異なります。 詳細については、「[レポート サーバー データベース接続の構成 &#40;SSRS 構成マネージャー&#41;](../../../sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)」を参照してください。  
  
-   リスナーの DNS 名を使用するようにデータベース接続を更新します。 ネイティブ モードのレポート サーバーの場合、 **構成マネージャーで** [レポート サーバー データベース名] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] を変更します。 SharePoint モードの場合、 **サービス アプリケーションの** データベース サーバー名 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] を変更します。  
  
###  <a name="bkmk_steps_to_complete_failover"></a> レポート サーバー データベースのディザスター リカバリーの手順  
 次の手順は、セカンダリ レプリカへの [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] フェールオーバー後に実施する必要があります。  
  
1.  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] のデータベースをホストするプライマリ データベース エンジンによって使用されている SQL エージェント サービスのインスタンスを停止します。  
  
2.  新しいプライマリ レプリカとなるコンピューター上の SQL エージェント サービスを開始します。  
  
3.  レポート サーバー サービスを停止します。  
  
     レポート サーバーがネイティブ モードの場合、 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 構成マネージャーを使用して、レポート サーバーの Windows サーバーを停止します。  
  
     レポート サーバーが SharePoint モードで構成されている場合、SharePoint サーバーの全体管理で [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 共有サービスを停止します。  
  
4.  レポート サーバー サービスまたは [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] SharePoint サービスを開始します。  
  
5.  新しいプライマリ レプリカに対してレポートを実行できることを確認します。  
  
###  <a name="bkmk_failover_behavior"></a> フェールオーバー時のレポート サーバーの動作  
 レポート サーバー データベースのフェールオーバーが発生した後は、新しいプライマリ レプリカを使用するようにレポート サーバー環境を更新することになりますが、このとき、フェールオーバーと復旧処理に起因する運用上の問題がいくつか生じます。 この問題の影響は、フェールオーバー時の [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] の負荷に加え、 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] がセカンダリ レプリカへのフェールオーバーに要した時間、さらには、レポート サーバー管理者が新しいプライマリ レプリカを使うようにレポート環境を更新するのにかかった時間によって変動します。  
  
-   バックグラウンド処理が繰り返し実行される場合があります。これは、再試行ロジックが作動しても、フェールオーバー中は、スケジューリングされている作業をレポート サーバーが完了済みとしてマークできないためです。  
  
-   SQL Server エージェントがレポート サーバー データベースにデータを書き込むことができず、そのデータが新しいプライマリ レプリカと同期されないために、通常ならフェールオーバー中にトリガーされるバックグラウンド処理が実行されません。  
  
-   データベースのフェールオーバーが完了し、レポート サーバー サービスが再開されると、その後、SQL Server エージェント ジョブが自動的に再作成されます。 SQL エージェント ジョブが再作成されるまで、SQL Server エージェント ジョブに関連するバックグラウンド処理は一切実行されません。 これには、 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] サブスクリプション、スケジュール、スナップショットなどが該当します。  
  
## <a name="see-also"></a>参照  
 [SQL Server Native Client の HADR サポート](../../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)   
  [AlwaysOn 可用性グループ (SQL Server)](always-on-availability-groups-sql-server.md) [AlwaysOn 可用性グループの概要&#40;SQL Server&#41;](getting-started-with-always-on-availability-groups-sql-server.md)   
 [SQL Server Native Client での接続文字列キーワードの使用](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)   
 [SQL Server Native Client の HADR サポート](../../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)   
 [可用性レプリカに対するクライアント接続アクセスについて &#40;SQL Server&#41;](about-client-connection-access-to-availability-replicas-sql-server.md)  
  
  
