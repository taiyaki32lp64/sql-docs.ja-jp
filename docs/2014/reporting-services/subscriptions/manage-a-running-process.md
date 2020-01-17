---
title: 実行中の処理を管理する | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- report processing [Reporting Services], status information
- jobs [Reporting Services]
- viewing jobs
- canceling jobs
- user jobs [Reporting Services]
- system jobs [Reporting Services]
- report processing [Reporting Services], managing running processes
- processes [Reporting Services]
- scanning processes [Reporting Services]
- status information [Reporting Services]
- report processing [Reporting Services]
- canceling subscriptions
- report servers [Reporting Services], jobs
- data-driven subscriptions
- displaying jobs
- subscriptions [Reporting Services], running processes
ms.assetid: 473e574e-f1ff-4ef9-bda6-7028b357ac42
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f0c465a50547d8ca45947dc5db5c56221a8a4538
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66100821"
---
# <a name="manage-a-running-process"></a>Manage a Running Process
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] では、レポート サーバーで実行中のジョブの状態を監視します。 レポート サーバーは、一定の間隔で、実行中のジョブをスキャンし、レポート サーバー データベース (SharePoint モードの場合はサービス アプリケーション データベース) に状態情報を書き込みます。 リモートまたはローカル データベース サーバーでのクエリの実行、レポート処理、およびレポート表示のいずれかが行われている場合、ジョブは実行中です。  
  
 *ユーザー ジョブ* と *システム ジョブ*の両方を管理できます。  
  
-   ユーザー ジョブは、各ユーザーまたはサブスクリプションによって開始されます。 このジョブには、要求時のレポートの実行、レポート履歴スナップショットの要求、レポート スナップショットの手動作成、および標準のサブスクリプションの処理が含まれます。  
  
-   システム ジョブは、レポート サーバーによって開始されます。 システム ジョブには、スケジュールされたレポート実行スナップショット、スケジュールされたレポート履歴スナップショット、およびデータ ドリブン サブスクリプションが含まれます。  
  
 レポートの処理時間およびリソースの使用は、レポート、クエリの複雑さ、データ量、およびレポートに対して指定された表示形式により、大きく異なります。 ローカル データ ソースに対する単純なクエリを有するレポートは、通常、ミリ秒単位で完了し、管理または調整の必要はありません。 これに対し、PDF または Excel で表示されるサイズの大きいレポートでは、ハードウェア リソース、配信オプション、および並行して他の処理が実行されているかどうかにより、相当な処理時間を要する場合があります。 レポート サーバーでは、時間のかかる処理の多くは、レポートの表示操作処理と、クエリ処理の完了を待機している処理です。 コンピューターをオフラインにしたり、完了までに長時間かかっている実行中のジョブを停止する場合、レポート処理を取り消すことが必要になる場合があります。  
  
 キャンセルできる処理は次のとおりです。  
  
-   オンデマンドのレポート処理。  
  
-   スケジュールされたレポート処理。  
  
-   個々のユーザーが所有する標準サブスクリプション。  
  
 ジョブのキャンセルでは、レポート サーバーで実行中の処理だけが取り消されます。 レポート サーバーは、他のコンピューター上のデータ処理を管理しないため、他のシステム上で孤立したそれ以降のクエリ処理については、手動で取り消す必要があります。 実行に長時間かかるクエリが自動的にシャットダウンされるようなクエリのタイムアウト値を指定することを検討してください。 詳細については、「[レポートおよび共有データセット処理のタイムアウト値の設定 (SSRS)](../report-server/setting-time-out-values-for-report-and-shared-dataset-processing-ssrs.md)」を参照してください。 レポートの一時停止の詳細については、次を参照してください。 [Pause Report and Subscription Processing](disable-or-pause-report-and-subscription-processing.md)します。  
  
> [!NOTE]  
>  まれに、サーバーを再起動して処理を取り消す必要が生じる場合があります。 SharePoint モードの場合、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サービス アプリケーションをホストしているアプリケーション プールの再起動が必要になる場合があります。 詳細については、「 [レポート サーバー サービスの開始と停止](../report-server/start-and-stop-the-report-server-service.md)」を参照してください。  
  
 このトピックの内容  
  
-   [ジョブの表示とキャンセル (ネイティブ モード)](#bkmk_native)  
  
-   [ジョブの表示とキャンセル (SharePoint モード)](#bkmk_sharepoint)  
  
-   [プログラムによるジョブの管理](#bkmk_programmatically)  
  
##  <a name="bkmk_native"></a> ジョブの表示とキャンセル (ネイティブ モード)  
 レポート サーバーで実行中のジョブは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] を使用して表示したり取り消したりできます。 現在実行中のジョブの一覧を取得したり、最新のジョブ ステータスをレポート サーバー データベースから取得したりするには、ページを更新する必要があります。 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]からレポート サーバーに接続する際、[ジョブ] フォルダーを開くと、現在レポート サーバー コンピューターで処理中のレポートを一覧表示できます。 [ジョブのプロパティ] ページに、各ジョブのステータス情報が表示されます。 [レポート サーバー ジョブのキャンセル] ダイアログ ボックスを開くことによって、すべてのジョブのステータス情報を確認できます。  
  
 レポート サーバーで実行中のジョブは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] を使用して表示したり取り消したりできます。 現在実行中のジョブの一覧を取得したり、最新のジョブ ステータスをレポート サーバー データベースから取得したりするには、ページを更新する必要があります。 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]からレポート サーバーに接続する際、[ジョブ] フォルダーを開くと、現在レポート サーバー コンピューターで処理中のレポートを一覧表示できます。 [ジョブのプロパティ] ページに、各ジョブのステータス情報が表示されます。 [レポート サーバー ジョブのキャンセル] ダイアログ ボックスを開くことによって、すべてのジョブのステータス情報を確認できます。  
  
 モデルの生成、モデルの処理、またはデータ ドリブン サブスクリプションについては、 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] で一覧表示したり取り消したりすることはできません。 モデルの生成またはモデルの処理を取り消す手段は、Reporting Services には用意されていません。 ただし、このトピックで紹介している手順に従うことによって、データ ドリブン サブスクリプションをキャンセルできます。  
  
### <a name="how-to-cancel-report-processing-or-subscription"></a>レポート処理またはサブスクリプションを取り消す方法  
  
1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]からレポート サーバーに接続します。 詳細については、「 [Management Studio でレポート サーバーに接続する方法](../tools/connect-to-a-report-server-in-management-studio.md)」を参照してください。  
  
2.  **[ジョブ]** フォルダーを開きます。  
  
3.  レポートを右クリックし、 **[ジョブの取り消し]** をクリックします。  
  
### <a name="how-to-cancel-a-data-driven-subscription"></a>データ ドリブン サブスクリプションを取り消す方法  
  
1.  テキスト エディターで RSReportServer.config ファイルを開きます。  
  
2.  `IsNotificationService` を探します。  
  
3.  `False` に設定します。  
  
4.  ファイルを保存します。  
  
5.  レポート マネージャーで、レポートの [サブスクリプション] タブまたは **[個人用サブスクリプション]** からデータ ドリブン サブスクリプションを削除します。  
  
6.  サブスクリプションを削除したら、RSReportServer.config ファイルで `IsNotificationService` を探し、`True` に設定します。  
  
7.  ファイルを保存します。  
  
### <a name="configuring-frequency-settings-for-retrieving-job-status"></a>ジョブ ステータスの取得間隔の設定  
 実行中のジョブは、レポート サーバーの一時データベースに格納されます。 RSReportServer.config ファイルで構成設定を変更し、レポート サーバーによる実行中のジョブをスキャンする頻度と実行ジョブの状態を新規から実行中に変更するまでの間隔を制御できます。 `RunningRequestsDbCycle` 設定では、レポート サーバーによって実行中である処理のスキャンの頻度を指定します。 既定では、状態情報は 60 秒ごとに記録されます。 `RunningRequestsAge` 設定では、ジョブが新規から実行中に遷移するまでの間隔を指定します。  
  
##  <a name="bkmk_sharepoint"></a> ジョブの表示とキャンセル (SharePoint モード)  
 SharePoint モードでの配置のジョブの管理は、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サービス アプリケーションごとに、SharePoint サーバーの全体管理を使用して行います。  
  
#### <a name="to-manage-jobs-in-sharepoint-mode"></a>SharePoint モードでジョブを管理するには  
  
1.  SharePoint サーバーの全体管理で **[サービス アプリケーションの管理]** をクリックします。  
  
2.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サービス アプリケーションの名前を見つけてクリックし、アプリケーションの管理ページを開きます。  
  
3.  **[ジョブの管理]** をクリックします。  
  
4.  **[ジョブ ID]** をクリックして、ジョブの詳細を表示します。  
  
5.  または、ジョブのボックスをクリックして **[削除]** をクリックし、ジョブをキャンセルします。 ジョブを削除しても、サブスクリプションは削除されません。  
  
##  <a name="bkmk_programmatically"></a> プログラムによるジョブの管理  
 ジョブは、プログラムまたはスクリプトを使用して管理できます。 詳細については、「 <xref:ReportService2010.ReportingService2010.ListJobs%2A>」と「 <xref:ReportService2010.ReportingService2010.CancelJob%2A>の両方を管理できます。  
  
## <a name="see-also"></a>参照  
 [[レポート サーバー ジョブのキャンセル] (Management Studio)](../tools/cancel-report-server-jobs-management-studio.md)   
 [[ジョブのプロパティ] (Management Studio)](../tools/job-properties-management-studio.md)   
 [Reporting Services の構成ファイル &#40;RSreportserver.config&#41; の変更](../report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)   
 [RSReportServer 構成ファイル](../report-server/rsreportserver-config-configuration-file.md)   
 [レポート マネージャー &#40;SSRS ネイティブ モード&#41;](../report-manager-ssrs-native-mode.md)   
 [レポート サーバーのパフォーマンスの監視](../report-server/monitoring-report-server-performance.md)  
  
  
