---
title: Reporting Services Data Alerts | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 8c234077-b670-45c0-803f-51c5a5e0866e
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d5dd8bad47bdbc1faaec1dcb7e9c7e9a05bed548
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66102975"
---
# <a name="reporting-services-data-alerts"></a>Reporting Services のデータ警告
  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] の "データ警告" は、関心のある、または重要なレポート データを適切なタイミングで把握できるよう補助する、データ駆動型の警告ソリューションです。 データ警告を使用することで、情報を探し出す必要がなくなり、情報が自動的に通知されるようになります。  
  
 データ警告メッセージは電子メールで送信されます。 情報の重要性に応じて、メッセージの送信頻度を選択したり、結果が変更された場合にのみメッセージが送信されるようにすることができます。 複数の電子メール受信者を指定して、この方法で他のユーザーに通知し、効率性とコラボレーションを強化することができます。  
  
||  
|-|  
|**[!INCLUDE[applies](../includes/applies-md.md)]**  SharePoint モード|  
  
##  <a name="AlertingWF"></a> データ警告のアーキテクチャとワークフロー  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] データ警告は、大きく次の機能に分けることができます。  
  
-   **データ警告定義の作成と保存**: レポートの実行、注意すべきデータ値を識別するルールの作成、データ警告メッセージを送信する定期的なパターンの定義、警告メッセージの受信者の指定などを行います。  
  
-   **データ警告定義の実行**: 警告サービスは、予定された時刻に警告の定義を処理してレポート データを取得し、警告の定義にあるルールに基づいてデータ警告インスタンスを作成します。  
  
-   **受信者へのデータ警告メッセージの配信**: 警告サービスは、警告のインスタンスを作成し、警告メッセージを電子メールで受信者に送信します。  
  
 さらに、データ警告所有者は、自分の警告に関する情報を表示し、そのデータ警告定義を削除または編集できます。 警告の所有者は 1 人だけで、警告を作成したユーザーが所有者になります。  
  
 SharePoint 警告の管理権限を持つ警告管理者は、サイト レベルでデータ警告を管理できます。 サイト ユーザーごとの警告の一覧表示や、警告の削除を行うことができます。  
  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] のデータ警告は、SharePoint の通知とは異なります。 SharePoint の通知は、レポートを始めとするあらゆる種類のドキュメントに対して定義できます。 SharePoint の通知は、ドキュメントが変更されたときに送信されます。 たとえば、レポート内のテーブルに列を追加した場合などです。 対照的に、データ警告は、レポート内のデータが警告定義内のルールを満たしたときに送信されます。 各ルールは通常、レポートに表示されるデータを参照します。  
  
 レポートに関するデータ警告を作成することによって、自分や他のユーザーが注目すべきデータを定義したルールにレポートのデータが合致した場合に、ビジネス ニーズに応じた間隔で、レポート データ内の変更を監視し、データ警告メッセージを電子メールで送信できます。 データ警告をオンデマンドで実行することもできます。 SharePoint の "警告の作成" 権限を持つユーザーは、自分が表示する権限を持っている任意のレポートに対して警告を作成できます。 レポートには複数の警告を作成することができます。また、1 つのレポートに対し、複数のユーザーが同じ通知を作成することも異なる通知を作成することも可能です。 自分が作成したデータ警告定義内で他のユーザーを警告メッセージの受信者として指定することにより、他のユーザーとのコラボレーションを実現することもできます。  
  
 次の図は、データ警告定義を作成および保存し、データ警告のインスタンスの処理を開始する SQL エージェント ジョブを作成して、警告のトリガーとなったレポート データが含まれるデータ警告メッセージを 1 人または複数の受信者に電子メールで送信するワークフローを示しています。  
  
 ![Reporting Services 警告内のワークフロー](media/rs-alertingworkflow.gif "Reporting Services 警告内のワークフロー")  
  
### <a name="reports-supported-by-data-alerts"></a>データ警告によってサポートされるレポート  
 データ警告は、レポート定義言語 (RDL) で記述され、レポート デザイナーまたはレポート ビルダーで作成された、あらゆる種類の業務用レポートに対して作成できます。 データ領域 (テーブルやグラフなど) を含んだレポート、サブレポートを含んだレポート、さらには、複数のパラレルな列グループと入れ子になったデータ領域を含んだ複雑なレポートがサポートされます。 要件は、レポートに任意の種類のデータ領域が少なくとも 1 つ含まれていることと、レポート データ ソースが保存済みの資格情報を使用するか、または資格情報を使用しないように構成されていることだけです。 データ領域がないレポートに対しては警告を作成できません。  
  
 [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)]で作成されたレポートに対してデータ警告を作成することはできません。  
  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] をネイティブ モードまたは SharePoint モードでインストールするか、またはスタンドアロン バージョンのレポート ビルダーを使用している場合、レポート サーバー、自分のコンピューター、または SharePoint ライブラリに対してレポートを保存できます。 レポートに対してデータ警告を作成するには、レポートを保存するか、SharePoint ライブラリにアップロードする必要があります。 ネイティブ モードのレポート サーバーにもコンピューターにも保存されていないレポートに対して警告を作成することはできません。 また、カスタム アプリケーションに埋め込む形で警告を作成することもできません。  
  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] のレポートでは、さまざまな種類の資格情報がサポートされます。 レポートのデータ ソースに保存済みの資格情報が使用されている場合、または、資格情報が使用されていない場合、レポートに対してデータ警告を作成することができます。 資格情報として統合セキュリティを使用するレポートや、資格情報の入力が求められるレポートに対して警告を作成することはできません。 レポートは、警告の定義の処理の一環として実行されます。資格情報がないと、この処理は失敗します。 詳細については、以下を参照してください。  
  
-   [レポート データ ソースに関する資格情報と接続情報を指定する](report-data/specify-credential-and-connection-information-for-report-data-sources.md)  
  
-   [ロールと権限 &#40;Reporting Services&#41;](security/roles-and-permissions-reporting-services.md)  
  
-   [レポート サーバーでの認証](security/authentication-with-the-report-server.md)  
  
### <a name="run-reports"></a>レポートの実行  
 データ警告定義を作成する最初の手順は、SharePoint ライブラリ内にある目的のレポートの場所を特定し、レポートを実行することです。 レポートを実行するとき、そこにデータがないと、その時点でそのレポートについての警告を作成することはできません。  
  
 レポートがパラメーター化されている場合は、レポートの実行時に使用するパラメーター値を指定します。 パラメーター値は、レポートに対して作成するデータ警告定義内に保存されます。 これらの値は、レポートがデータ警告定義の処理の 1 つの手順として再実行される際に使用されます。 パラメーター値を変更する場合は、それらのパラメーター値を使用してレポートを再実行し、そのバージョンのレポートに対する警告定義を作成する必要があります。  
  
### <a name="create-data-alert-definitions"></a>データ警告定義の作成  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] のデータ警告機能には、データ警告定義を作成するためのデータ警告デザイナーが用意されています。  
  
 データ警告定義を作成するには、レポートを実行し、SharePoint レポート ビューアーの **[アクション]** メニューからデータ警告デザイナーを開きます。 レポートのデータ フィードが生成され、データ警告デザイナーのデータ プレビュー テーブルにデータ フィードの先頭 100 行が表示されます。 レポートから取得されたすべてのデータ フィードは、データ警告デザイナーで警告の定義を行っている間キャッシュされます。 このキャッシュによって、複数のデータ フィードをすばやく切り替えることができます。 データ警告デザイナーで警告の定義を再度開くと、データ フィードが最新の情報に更新されます。  
  
 データ警告定義は、データ警告メッセージをトリガーするためにレポート データが満たす必要のあるルールと句、警告メッセージの送信頻度を定義するスケジュール、警告メッセージの送信開始/終了日 (オプション)、警告メッセージに含める情報 (件名行や説明など)、およびメッセージの受信者で構成されます。 作成した警告の定義は、SQL Server 警告データベースに保存します。  
  
### <a name="save-data-alert-definitions-and-alerting-metadata"></a>データ警告定義と警告メタデータの保存  
 SharePoint モードで [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] をインストールすると、SQL Server 警告データベースが自動的に作成されます。  
  
 データ警告定義と警告メタデータは、警告データベースに保存されます。 このデータベースの既定の名前は ReportingServices\<GUID>_Alerting です。  
  
 データ警告定義を保存すると、警告定義のための SQL Server エージェント ジョブが自動的に作成されます。 このジョブには、ジョブ スケジュールが含まれます。 このスケジュールは、警告定義で定義した定期的なパターンに基づくものです。 ジョブを実行すると、データ警告定義の処理が開始されます。  
  
### <a name="process-data-alert-definitions"></a>データ警告定義の処理  
 SQL Server エージェント ジョブのスケジュールが警告定義の処理を開始すると、レポートが実行されてレポート データ フィードが更新されます。 警告サービスは、データ フィードを読み取り、そのデータ値に対し、データ警告定義によって指定されたルールを適用します。 ルールに合致するデータ値が 1 つでもあった場合は、データ警告インスタンスが作成され、警告結果を含むデータ警告メッセージがすべての受信者に電子メールで送信されます。 結果には、警告インスタンスの作成時点ですべてのルールを満たしていたレポート データの行が含まれます。 同じ結果を含む警告メッセージが複数生成されるのを防ぎたい場合は、結果が変更された場合にのみメッセージが送信されるように指定することもできます。 この場合、警告インスタンスは作成されて警告データベースに保存されますが、警告メッセージは生成されません。 エラーが発生した場合は、やはり警告インスタンスが警告データベースに保存され、エラーの詳細情報を含んだ警告メッセージが受信者に送信されます。 後の「診断とログ」のセクションでは、ログ記録とトラブルシューティングについてより詳しく説明しています。  
  
### <a name="send-data-alert-messages"></a>データ警告メッセージの送信  
 データ警告メッセージは電子メールで送信されます。  
  
 **"差出人"** 行には、 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] の電子メール配信構成によって指定された値が表示されます。 **"宛先"** 行には、データ警告デザイナーで警告を作成するときに指定した一連の受信者が表示されます。  
  
 データ警告メッセージには、データ警告デザイナーで指定する電子メールの "件名" 行に加え、次の情報が含まれます。  
  
-   データ警告定義の作成者の名前。  
  
-   警告定義内に説明を入力した場合は、電子メール テキストの上部に説明が表示されます。  
  
-   警告結果。これは、警告定義で指定したルールを満たすレポート データ フィード内の行で構成されます。  
  
-   警告定義の作成対象のレポートへのリンク。  
  
-   警告定義内のルール。  
  
-   レポートの実行に使用したパラメーターと値。  
  
-   レポート データ領域外にあるレポート アイテムから取得されたコンテキスト値。  
  
 データ警告インスタンスまたはデータ警告メッセージを作成できない場合は、エラー メッセージがすべての受信者に送信されます。 メッセージには、警告結果の代わりにエラーの説明が含められます。  
  
 詳細については、「 [Data Alert Messages](../../2014/reporting-services/data-alert-messages.md)」を参照してください。  
  
##  <a name="InstallAlerting"></a> データ警告のインストール  
 データ警告機能は、SharePoint モードで [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] がインストールされている場合にのみ使用できます。 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] を SharePoint モードでインストールすると、データ警告定義および警告メタデータを格納する警告データベースと、警告を管理するための 2 つの SharePoint ページとがセットアップによって自動的に作成され、SharePoint サイトにデータ警告デザイナーが追加されます。 警告機能に関して、インストール中に設定する特別な手順やオプションはありません。  
  
 SharePoint モードの [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] のインストール ( [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] で新たに導入された [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 共有サービスや、 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 機能を使用する前に作成および構成する必要のある [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] サービス アプリケーションを含む) に関する詳細については、MSDN ライブラリの「 [SharePoint 2010 用 Reporting Services の SharePoint モードのインストール](../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md) 」を参照してください。  
  
 このトピックの冒頭の図に示したように、データ警告には SQL Server エージェント ジョブが使用されます。 このジョブを作成するには、SQL Server エージェントが実行されている必要があります。 SQL Server エージェントは、 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]をインストールした際に、自動的に開始されるよう構成されている可能性があります。 そのように構成されていない場合は、SQL Server エージェントを手動で開始できます。 詳細については、「 [SQL Server エージェントの構成](../ssms/agent/configure-sql-server-agent.md) 」および「 [データベース エンジン、SQL Server エージェント、SQL Server Browser サービスの開始、停止、一時停止、再開、および再起動](../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)」を参照してください。  
  
 SharePoint サーバーの全体管理の **[サブスクリプションと警告の準備]** ページでは、SQL Server エージェントが実行されているかどうかを確認し、SQL Server エージェントへのアクセス権を付与するために実行するカスタムの [!INCLUDE[tsql](../includes/tsql-md.md)] スクリプトを作成およびダウンロードできます。 また、PowerShell を使用して [!INCLUDE[tsql](../includes/tsql-md.md)] スクリプトを生成することもできます。 詳細については、「[SSRS サービス アプリケーションを使用するためのサブスクリプションと警告の準備](install-windows/provision-subscriptions-and-alerts-for-ssrs-service-applications.md)」を参照してください。  
  
##  <a name="ConfigAlert"></a> データ警告の構成  
 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 以降では、 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] を SharePoint モードでインストールする場合は必ず、 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 機能 (データ警告を含む) の設定が、レポート サーバー構成ファイル (rsreportserver.config) と SharePoint 構成データベースの間で分散されます。 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]のインストールおよび構成の 1 つの手順としてサービス アプリケーションを作成すると、SharePoint 構成データベースが自動的に作成されます。 詳細については、次を参照してください。 [RSReportServer Configuration File](report-server/rsreportserver-config-configuration-file.md)と[Reporting Services 構成ファイル](report-server/reporting-services-configuration-files.md)します。  
  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] データ警告の設定には、警告データおよびメタデータのクリーンアップ間隔と、データ警告メッセージを電子メールで送信する際の再試行回数が含まれます。 構成ファイルと構成データベースを更新して、データ警告設定に異なる値を使用することもできます。  
  
 レポート サーバー構成ファイルは直接更新します。 SharePoint 構成データベースは、Windows PowerShell コマンドレットを使用して更新します。  
  
 次の表は、データ警告の構成要素とその既定値、説明、および場所を一覧にしたものです。  
  
|設定|既定値|説明|場所|  
|-------------|-------------------|-----------------|--------------|  
|AlertingCleanupCycleMinutes|20|クリーンアップ サイクルの開始間隔 (分) です。|レポート サーバー構成ファイル|  
|AlertingExecutionLogCleanupMinutes|10080|実行ログのエントリを保持する時間 (分) です。|レポート サーバー構成ファイル|  
|AlertingDataCleanupMinutes|360|一時的なデータを保持する時間 (分) です。|レポート サーバー構成ファイル|  
|AlertingMaxDataRetentionDays|180|警告の実行メタデータ、警告インスタンス、および実行結果が削除されるまでの日数です。|レポート サーバー構成ファイル|  
|MaxRetries|3|データ警告の処理を再試行する回数。|サービス構成データベース|  
|SecondsBeforeRetry|900|各再試行までに待機する秒数。|サービス構成データベース|  
  
 既定では、MaxRetries と SecondsBeforeRetry の設定は、データ警告をトリガーするすべてのイベントに適用されます。 再試行の実行と遅延をより細かく制御したい場合は、異なる MaxRetries 値と SecondsBeforeRetry 値を指定するすべてのイベント ハンドラーに対して要素を追加できます。  
  
### <a name="event-handlers-and-retry"></a>イベント ハンドラーと再試行  
 イベント ハンドラーには次のものがあります。  
  
|イベント ハンドラー|説明|  
|-------------------|-----------------|  
|FireAlert|データ警告マネージャーで **[実行]**  をクリックして、警告定義の処理を直ちに開始します。|  
|FireSchedule|SQL Server エージェントにより、警告定義のジョブ スケジュールが起動されます。|  
|CreateSchedule|データ警告定義を作成すると、警告定義で指定された頻度に基づいて、SQL Server エージェントのジョブ スケジュールが作成されます。|  
|UpdateSchedule|データ警告定義の頻度を更新すると、SQL Server エージェントのジョブ スケジュールが更新されます。|  
|DeleteSchedule|データ警告定義を削除すると、対応する SQL Server エージェント ジョブが削除されます。|  
|GenerateAlert|警告ランタイムが、レポート データ フィードを処理し、データ警告定義で指定されたルールを適用し、データ警告のインスタンスを作成するかどうかを決定して、必要であれば、データ警告のインスタンスを作成します。|  
|DeliverAlert|ランタイムがデータ警告メッセージを作成し、それをすべての受信者に電子メールで送信します。|  
  
 次の表に、イベント ハンドラーと再試行のタイミングをまとめています。  
  
|エラー カテゴリ|<|\<|イベントの種類||>|>|>|  
|--------------------|--------|--------|----------------|-|--------|--------|--------|  
||**FireAlert**|**FireSchedule**|**CreateSchedule**|**UpdateSchedule**|**DeleteSchedule**|**GenerateAlert**|**DeliverAlert**|  
|メモリ不足|x|X|X|X|X|X|x|  
|スレッドの中止|x|X|X|X|X|X|x|  
|SQL エージェントが未実行|x||X|X|x|||  
|一時的。 ほとんどの場合は接続の問題、タイムアウト、およびロックが原因。|x|X|X|X|X|X|×|  
|IOException|||||||x|  
|WebException|||||||x|  
|SocketException|||||||x|  
|SMTPException **(\*)**|||||||x|  
  
 **(\*)** 再試行をトリガーする SMTP エラーは次のとおりです。  
  
-   SmtpStatusCode.ServiceNotAvailable  
  
-   SmtpStatusCode.MailboxBusy  
  
-   SmtpStatusCode.MailboxUnavailable  
  
###  <a name="bkmk_disablealerts"></a> データ警告の無効化  
 データ警告機能を無効にする場合は、構成ファイルの Service セクションを更新します。 次のコードは、構成ファイルの Service セクションを示しています。  
  
 `<Service>`  
  
 `<IsSchedulingService>True</IsSchedulingService>`  
  
 `<IsNotificationService>True</IsNotificationService>`  
  
 `<IsEventService>True</IsEventService>`  
  
 `<IsAlertingService>True</IsAlertingService>`  
  
 `...`  
  
 `</Service>`  
  
 警告機能を無効にするには、 `<IsAlertingService>True</IsAlertingService>`の True を False に変更します。  
  
##  <a name="Permissions"></a> データ警告に対する権限  
 レポートに対するデータ警告を作成するには、レポートを実行して SharePoint サイトに警告を作成するための権限が必要です。 レポートの権限の詳細については、次を参照してください。  
  
-   [複数のレポートからのデータ フィードの生成 &#40;レポート ビルダーおよび SSRS&#41;](report-builder/generating-data-feeds-from-reports-report-builder-and-ssrs.md)  
  
-   [SharePoint サイト上のレポート サーバー アイテムに対する権限の設定 &#40;Reporting Services の SharePoint 統合モード&#41;](security/set-permissions-for-report-server-items-on-a-sharepoint-site.md)  
  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] のデータ警告は、インフォメーション ワーカーと警告管理者という 2 つの権限レベルをサポートします。 次の表は、関連する SharePoint 権限とユーザー タスクの一覧です。  
  
|ユーザーの種類|SharePoint 権限|タスクの説明|  
|---------------|---------------------------|----------------------|  
|インフォメーション ワーカー|アイテムの表示<br /><br /> 警告の作成|レポートなどのアイテムを表示し、レポートに対してデータ警告を作成できます。 警告を編集および削除できます。|  
|警告管理者|警告の管理|SharePoint サイトに保存されたすべてのデータ警告を一覧表示し、通知を削除できます。|  
  
##  <a name="DiagnosticsLogging"></a> 診断とログ  
 データ警告では、インフォメーション ワーカーおよび管理者が、さまざまな方法で警告を追跡し、警告に失敗した理由を特定することができます。また、管理者は、警告メッセージがだれに送信され、警告インスタンスがいくつ送信されたかなどを、ログを使用して把握できます。  
  
### <a name="data-alert-manager"></a>データ警告マネージャー  
 失敗した理由をインフォメーション ワーカーと警告管理者が把握しやすいように、データ警告マネージャーには、警告の定義とエラー情報が一覧表示されます。 エラーの一般的な理由は、次のとおりです。  
  
-   レポート データ フィードが変更され、データ警告定義のルールに使用されていた列が、現在はデータ フィードに存在しない。  
  
-   レポートを表示する権限が取り消された。  
  
-   基になるデータ ソースのデータ型が変更され、警告の定義が無効になった。  
  
### <a name="logs"></a>ログ  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] では、データ警告定義の処理時に実行されるレポートや、作成されるデータ警告インスタンスの詳細を把握するのに役立つ、多数のログが提供されます。 特によく使用されるログは、警告実行ログ、レポート サーバー実行ログ、およびレポート サーバー トレース ログの 3 つです。  
  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] の他のログについては、「 [Reporting Services のログ ファイルとソース](report-server/reporting-services-log-files-and-sources.md)」を参照してください。  
  
#### <a name="alerting-execution-log"></a>警告実行ログ  
 警告機能のランタイム サービスは、警告データベースの ExecutionLogView テーブルにエントリを書き込みます。 このテーブルに対してクエリを実行するか、次のストアド プロシージャを実行すると、警告データベースに保存されたデータ警告に関して、より詳細な診断情報を取得できます。  
  
-   ReadAlertData  
  
-   ReadAlertHistory  
  
-   ReadAlertInstances  
  
-   ReadEventHistory  
  
-   ReadFeedPollHistory  
  
-   ReadFeedPools  
  
-   ReadPollData  
  
-   ReadSentAlerts  
  
 SQL エージェントを使用すると、ストアド プロシージャをスケジュールに従って実行することができます。 詳しくは、「 [SQL Server Agent](../ssms/agent/sql-server-agent.md)」をご覧ください。  
  
#### <a name="report-server-execution-log"></a>レポート サーバー実行ログ  
 レポートは、データ警告定義の作成対象であるデータ フィードを生成するために実行されます。 レポート サーバー データベース内のレポート サーバー実行ログは、レポートが実行されるたびに情報を取得します。 データベース内の ExecutionLog2 ビューに対してクエリを実行し、詳細な情報を取得することもできます。 詳細については、次を参照してください。[レポート サーバー実行ログと ExecutionLog3 ビュー](report-server/report-server-executionlog-and-the-executionlog3-view.md)します。  
  
#### <a name="report-server-trace-log"></a>レポート サーバー トレース ログ  
 レポート サーバーのトレース ログには、レポート サーバー Web サービスおよびバックグラウンド処理によって実行された操作を含め、レポート サーバー サービスの操作に関するきわめて詳細な情報が記録されます。 トレース ログ情報は、レポート サーバーを含むアプリケーションをデバッグしている場合、またはイベント ログや実行ログに書き込まれた特定の問題を調査している場合に役立ちます。 詳細については、「 [Report Server Service Trace Log](report-server/report-server-service-trace-log.md)」を参照してください。  
  
##  <a name="PerformanceCounters"></a> パフォーマンス カウンター  
 データ警告では、独自のパフォーマンス カウンターが提供されます。 警告ランタイム サービスの一部であるイベントに関連するパフォーマンス カウンターは 1 つのみです。 イベント キューに関連するパフォーマンス カウンターは、すべてのアクティブなイベントのキューの長さを知らせます。  
  
|イベントまたはイベント キュー|パフォーマンス カウンター|  
|--------------------------|-------------------------|  
|ALERTINGQUEUESIZE|Alerting: event queue length|  
|FireAlert|Alerting: events processed - FireAlert|  
|FireSchedule|Alerting: events processed - FireSchedule|  
|CreateSchedule|Alerting: events processed - CreateSchedule|  
|UpdateSchedule|Alerting: events processed - UpdateSchedule|  
|DeleteSchedule|Alerting: events processed - DeleteSchedule|  
|GenerateAlert|Alerting: events processed - GenerateAlert|  
|DeliverAlert|Alerting: events processed - DeliverAlert|  
  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] では、その他の [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 機能用のパフォーマンス カウンターも用意されています。 詳細については、次を参照してください[ReportServer:Service と ReportServerSharePoint:Service パフォーマンス オブジェクトのパフォーマンス カウンター](report-server/performance-counters-reportserver-service-performance-objects.md)、 [MSRS 2014 Web Service と MSRS 2014 Windows パフォーマンス カウンター。サービスのパフォーマンス オブジェクト&#40;ネイティブ モード&#41;](report-server/performance-counters-msrs-2011-web-service-performance-objects.md)、および[MSRS 2014 Web Service SharePoint Mode と MSRS 2014 Windows Service SharePoint Mode パフォーマンス オブジェクトのパフォーマンス カウンター &#40;SharePointモード&#41;](report-server/performance-counters-msrs-2011-sharepoint-mode-performance-objects.md)します。  
  
##  <a name="SupportForSSL"></a> SSL のサポート  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] では、HTTP SSL (Secure Sockets Layer) サービスを使用して、レポート サーバーまたは SharePoint サイトへの暗号化接続を確立できます。  
  
 警告ランタイム サービスとデータ警告ユーザー インターフェイスは、SSL をサポートしており、SSL と HTTP のいずれを使用している場合にも同様に機能します。ただし、少しだけ異なる点があります。 データ警告定義が SSL 接続を使用して作成された場合は、データ警告メッセージから SharePoint ライブラリにリンク バックする URL にも、SSL が使用されます。 SSL 接続は、URL に HTTP ではなく HTTPS が使用されているという点で区別できます。 同様に、データ警告定義が HTTP 接続を使用して作成された場合は、SharePoint サイトへのリンク バックに HTTP が使用されます。 警告定義が SSL と HTTP のどちらを使用して作成されたかにかかわらず、データ警告デザイナーやデータ警告マネージャーを使用する際のユーザーと警告管理者のエクスペリエンスは同じです。 警告定義の作成時とその後の更新および再保存時との間で、使用されるプロトコル (HTTP または SSL) が変わった場合、リンク URL では元のプロトコルがそのまま使用されます。  
  
 SSL を使用するように構成された SharePoint サイトにデータ警告定義を作成し、SSL の要件を取り除いた場合、警告はサイトで引き続き機能します。 サイトが削除された場合は、既定のゾーンのサイトが代わりに使用されます。  
  
##  <a name="UserInterface"></a> データ警告のユーザー インターフェイス  
 データ警告では、警告を管理するための SharePoint ページと、データ警告定義の作成と編集を行うためのデザイナーが用意されています。  
  
-   **データ警告デザイナー** は、データ警告定義を作成または編集する際に使用します。 詳細については、「 [データ警告デザイナー](../../2014/reporting-services/data-alert-designer.md)」、「 [データ警告デザイナーでのデータ警告の作成](create-a-data-alert-in-data-alert-designer.md) 」および「 [警告デザイナーでのデータ警告の編集](edit-a-data-alert-in-alert-designer.md)」を参照してください。  
  
-   **データ警告マネージャー** では、データ警告を一覧表示して警告を削除できるほか、警告を開いて編集することができます。 データ警告マネージャーには、2 つのバージョンがあります。1 つはユーザー用です。ユーザーが自分で作成した警告を管理する目的で使用します。もう 1 つは管理者用です。サイト ユーザーが所有する警告を管理者が管理する目的で使用します。  
  
     作成したデータ警告の管理に関する詳細については、「 [SharePoint ユーザー用のデータ警告マネージャー](../../2014/reporting-services/data-alert-manager-for-sharepoint-users.md) 」および「 [データ警告マネージャーでのデータ警告の管理](manage-my-data-alerts-in-data-alert-manager.md)」を参照してください。  
  
     サイト上のすべてのデータ警告の管理に関する詳細については、「 [警告管理者用のデータ警告マネージャー](../../2014/reporting-services/data-alert-manager-for-alerting-administrators.md) 」および「 [データ警告マネージャーで SharePoint サイトのすべてのデータ警告を管理する](manage-all-data-alerts-on-a-sharepoint-site-in-data-alert-manager.md)」を参照してください。  
  
-   **サブスクリプションとデータ警告の準備** では、Reporting Services がデータ警告に SQL Server エージェントを使用できるかどうかを確認したり、SQL Server エージェントへのアクセス権を付与するためのスクリプトをダウンロードすることができます。 詳細については、「[SSRS サービス アプリケーションを使用するためのサブスクリプションと警告の準備](install-windows/provision-subscriptions-and-alerts-for-ssrs-service-applications.md)」を参照してください。  
  
##  <a name="Globalization"></a> データ警告のグローバリゼーション  
 アラビア語やヘブライ語などの特定のスクリプトは、右から左に記述されます。 データ警告では、左から右に記述するスクリプトだけでなく、右から左のスクリプトもサポートされています。 データ警告は、カルチャを検出し、ユーザー インターフェイスの外観と動作、ならびにデータ警告メッセージのレイアウトを必要に応じて変更します。 カルチャは、ユーザーのコンピューター上で稼動しているオペレーティング システムの地域設定から取得されます。 カルチャは、データ警告定義を更新して再保存するたびに更新されます。  
  
 データが警告定義内のルールを満たすかどうかは、警告定義内のカルチャによって影響を受けることがあります。 カルチャ固有のルールによって最もよく影響を受けるのは、文字列比較です。  
  
 レポート データが警告定義内のルールを満たすかどうかは、警告定義内のカルチャによって影響を受けることがあります。 この影響を最もよく受けるのは文字列です。 たとえば、ドイツのカルチャを使用した警告定義では、英語の文字 "o" とドイツ語の文字 "ö" を比較するルールは満たされません。 イギリスのカルチャを使用した同じ警告定義では、このルールは満たされます。  
  
 データの書式設定もまた、警告定義のカルチャに基づきます。 たとえば、ピリオドを小数点区切り文字として使用するカルチャで 45.67 と表示される値は、コンマを小数点区切り文字として使用するカルチャでは、45,67 と表示されます。  
  
 右から左への記述がサポートされるかどうかは、使用するデータ警告ユーザー インターフェイスによって異なります。 データ警告デザイナーでは、テキスト ボックス内で右から左の記述がサポートされますが、デザイナーのレイアウトは右から左にはなりません。 デザイナーのレイアウトは、他のツールと同様に左から右のレイアウトになります。 右から左のテキスト方向で作成された警告定義が左から右の環境で編集された場合、警告定義の保存時には、右から左のテキスト方法が維持されます。 データ警告マネージャーは、SharePoint ページと同様に動作します。 レイアウトは、他の SharePoint ページと同様に、右から左のレイアウトになります。 右から左のデータ警告定義に基づくデータ警告メッセージでは、メッセージは右から左へと表示され、メッセージ レイアウトは左から右となります。  
  
##  <a name="HowTo"></a> 関連タスク  
  
-   [SharePoint ライブラリへのレポートの保存 &#40;レポート ビルダー&#41;](report-builder/save-a-report-to-a-sharepoint-library-report-builder.md)  
  
-   [データ警告デザイナーでのデータ警告の作成](create-a-data-alert-in-data-alert-designer.md)  
  
-   [警告デザイナーでのデータ警告の編集](edit-a-data-alert-in-alert-designer.md)  
  
-   [データ警告マネージャーでのデータ警告の管理](manage-my-data-alerts-in-data-alert-manager.md)  
  
-   [データ警告マネージャーで SharePoint サイトのすべてのデータ警告を管理する](manage-all-data-alerts-on-a-sharepoint-site-in-data-alert-manager.md)  
  
-   [ユーザーおよび警告管理者に権限を付与する](grant-permissions-to-users-and-alerting-administrators.md)  
  
## <a name="see-also"></a>参照  
 [データ警告デザイナー](../../2014/reporting-services/data-alert-designer.md)   
 [警告管理者用のデータ警告マネージャー](../../2014/reporting-services/data-alert-manager-for-alerting-administrators.md)   
 [SharePoint ユーザー用のデータ警告マネージャー](../../2014/reporting-services/data-alert-manager-for-sharepoint-users.md)  
  
  
