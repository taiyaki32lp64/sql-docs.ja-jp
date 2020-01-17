---
title: レポートサーバー間でコンテンツを移行するための rs .exe スクリプトのサンプル Reporting ServicesMicrosoft Docs
ms.custom: ''
ms.date: 07/27/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: d81bb03a-a89e-4fc1-a62b-886fb5338150
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: fa0bfb3087710243c7506aee57af429a10068a66
ms.sourcegitcommit: a165052c789a327a3a7202872669ce039bd9e495
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72783274"
---
# <a name="sample-reporting-services-rsexe-script-to-migrate-content-between-report-servers"></a>レポート サーバー間でコンテンツを移行するサンプル Reporting Services rs.exe スクリプト
  このトピックでは、 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] RS.exe [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] report server to another report server, using the **RS.exe** utility. RS.exe は、ネイティブ モードと SharePoint モードの両方で、 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]と共にインストールされます。 このスクリプトは、 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] アイテム (レポートやサブスクリプションなど) をサーバー間でコピーします。 スクリプトは SharePoint モードとネイティブ モードの両方のレポート サーバーをサポートしています。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] SharePoint モード &#124; [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] ネイティブ モード|  
  
##  <a name="bkmk_top"></a>このトピックの内容:  
  
-   [ssrs_migration.rss スクリプトをダウンロードするには](#bkmk_download_script)  
  
-   [サポートされるシナリオ](#bkmk_supported_scenarios)  
  
-   [スクリプトが移行するアイテムとリソース](#bkmk_what_is_migrated)  
  
-   [必要な権限](#bkmk_required_permissions)  
  
-   [スクリプトの使用方法](#bkmk_how_to_use_the_script)  
  
-   [パラメーターの説明](#bkmk_parameter_description)  
  
-   [その他の例](#bkmk_more_examples)  
  
    -   [ネイティブ モード レポート サーバー間](#bkmk_native_2_native)  
  
    -   [ネイティブモードから SharePoint モード (ルートサイト)](#bkmk_native_2_sharepoint_root)  
  
    -   [ネイティブモードから SharePoint モード ("bi" サイトコレクション)](#bkmk_native_2_sharepoint_with_site)  
  
    -   [SharePoint モードから SharePoint モード ("bi" サイトコレクション)](#bkmk_sharepoint_2_sharepoint)  
  
    -   [ネイティブモードからネイティブモード (Azure 仮想マシン)](#bkmk_native_to_native_Azure_vm)  
  
    -   [SharePoint モード-Azure 仮想マシン上のネイティブモードサーバーへの ' bi ' サイトコレクション](#bkmk_sharepoint_site_to_native_Azure_vm)  
  
-   [検証](#bkmk_verification)  
  
-   [トラブルシューティング](#bkmk_troubleshoot)  
  
##  <a name="bkmk_download_script"></a> ssrs_migration.rss スクリプトをダウンロードするには  
 CodePlex サイト「 [コンテンツを移行する Reporting Services RS.exe スクリプト](https://azuresql.codeplex.com/releases/view/115207) 」からローカル フォルダーにスクリプトをダウンロードします。 詳細については、「 [スクリプトの使用方法](#bkmk_how_to_use_the_script) 」をご覧ください。  
  
##  <a name="bkmk_supported_scenarios"></a> サポートされるシナリオ  
 スクリプトは SharePoint モードとネイティブ モードの両方のレポート サーバーをサポートしています。 また、次のバージョンのレポート サーバーをサポートしています。  
  
-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
  
-   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
  
-   [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)]  
  
 スクリプトは同じモードまたは異なるモードのレポート サーバー間でコンテンツをコピーするために使用できます。 たとえば、スクリプトを実行して [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] ネイティブ モード レポート サーバーから [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] SharePoint モード レポート サーバーにコンテンツをコピーできます。 スクリプトは RS.exe がインストールされているいずれのサーバーからも実行できます。 たとえば、以下の配置では次のことが可能です。  
  
-   サーバー A **上で** RS.exe とスクリプトを実行する  
  
-   サーバー B **から** コンテンツを  
  
-   サーバー C**に** コピーする  
  
|サーバー名|[レポート サーバー モード]|  
|-----------------|------------------------|  
|サーバー A|ネイティブ|  
|コンテンツを|SharePoint|  
|コピーする|SharePoint|  
  
 RS.exe ユーティリティの詳細については、「[RS.exe ユーティリティ &#40;SSRS&#41;](rs-exe-utility-ssrs.md)」をご覧ください。  
  
###  <a name="bkmk_what_is_migrated"></a> スクリプトが移行するアイテムとリソース  
 スクリプトは同じ名前の既存のコンテンツ アイテムを上書きしません。  スクリプトが移行元サーバー上のアイテムと同じ名前のアイテムを移行先サーバーで検出した場合、個々のアイテムについて "FAILURE" メッセージが表示されますが、スクリプトは続行されます。 次の表は、スクリプトを使用して移行先のモードのレポート サーバーに移行できるコンテンツとリソースの種類を示したものです。  
  
|Count|移行対象|SharePoint|[説明]|  
|----------|--------------|----------------|-----------------|  
|パスワード|**いいえ**|**いいえ**|パスワードは移行 **されません** 。 コンテンツ アイテムの移行後、移行先サーバーで資格情報を更新します。 たとえば、保存された資格情報を使用するデータ ソースなどです。|  
|個人用レポート|**いいえ**|**いいえ**|ネイティブ モードの "個人用レポート" 機能は個々のユーザー ログインに基づいているため、スクリプト作成サービスは、rss スクリプトに渡される **-u** パラメーターで指定されていないユーザーの "My Reports" フォルダー内のコンテンツにアクセスすることはできません。 また、"個人用レポート" は [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] SharePoint モードの機能ではなく、フォルダー内のアイテムを SharePoint 環境にコピーすることはできません。 このため、スクリプトは、ソースネイティブモードのレポートサーバー上の "個人用レポート" フォルダーにあるレポートアイテムをコピーしません。 このスクリプトを使用して "個人用レポート" フォルダー内のコンテンツを移行するには、次の手順を実行します。<br /><br /> 1) レポートマネージャーで新しいフォルダーを作成します。 必要に応じて、各ユーザーのフォルダーやサブフォルダーを作成できます。<br /><br /> 2) "個人用レポート" コンテンツを持つユーザーの1人としてログインします。<br /><br /> 3) レポートマネージャーで、**個人用レポート**フォルダーをクリックします。<br /><br /> 4) フォルダーの**詳細**ビューをクリックします。<br /><br /> 5) コピーする各レポートを選択します。<br /><br /> 6) レポートマネージャーツールバーの **[移動]** をクリックします。<br /><br /> 7) 目的の保存先フォルダーを選択します。<br /><br /> 8) 各ユーザーに対して手順2-7 を繰り返します。<br /><br /> 9) スクリプトを実行します。|  
|履歴|**いいえ**|**いいえ**||  
|履歴の設定|はい|はい|履歴の設定は移行されますが、履歴の詳細は移行されません。|  
|スケジュール|可|可|スケジュールを移行するには、SQL Server エージェントがターゲット サーバーで実行されている必要があります。 SQL Server エージェントが移行先で実行されていない場合は、次のエラー メッセージが表示されます。<br /><br /> `Migrating schedules: 1 items found. Migrating schedule: theMondaySchedule ... FAILURE:  The SQL Agent service is not running. This operation requires the SQL Agent service. ---> Microsoft.ReportingServices.Diagnostics.Utilities.SchedulerNotResponding Exception: The SQL Agent service is not running. This operation requires the SQL Agent service.`|  
|ロールとシステム ポリシー|はい|はい|既定では、スクリプトはカスタム権限スキーマをサーバー間でコピーしません。 既定の動作では、"親のアクセス許可を継承する" フラグが TRUE に設定されている移行先サーバーに項目が追加されます。 スクリプトで個々のアイテムの権限をコピーする場合は、SECURITY スイッチを使用します。<br /><br /> ソース サーバーとターゲット サーバーが **同じレポート サーバー モードでない**場合、たとえばネイティブ モードから SharePoint モードへの移行のとき、スクリプトは、「 [Reporting Services のロールおよびタスクと SharePoint のグループおよび権限の比較](../reporting-services-roles-tasks-vs-sharepoint-groups-permissions.md)」トピックで説明している比較に基づいて、既定のロールとグループをマップしようとします。 カスタムのロールとグループは移行先サーバーにコピーされません。<br /><br /> スクリプトが **同じモードの**サーバー間でコピーする場合は、SECURITY スイッチを使用してください。スクリプトは移行先サーバーで新しいロール (ネイティブ モード) またはグループ (SharePoint モード) を作成します。<br /><br /> ロールが移行先サーバーに既に存在する場合、スクリプトは次のような "FAILURE" メッセージを表示し、他のアイテムの移行を続行します。 スクリプトの完了後、移行先サーバー上のロールがニーズを満たすように構成されていることを確認してください。 移行中のロール: 8 項目が見つかりました。<br /><br /> `Migrating role: Browser ... FAILURE: The role 'Browser' already exists and cannot be created. ---> Microsoft.ReportingServices.Diagnostics.Utilities.RoleAlreadyExistsException: The role 'Browser' already exists and cannot be created.`<br /><br /> 詳細については、「[レポート サーバーへのユーザー アクセスを許可する &#40;レポート マネージャー&#41;](../security/grant-user-access-to-a-report-server.md)」を参照してください。<br /><br /> **注:** 移行元サーバー上に存在するユーザーが移行先サーバーに存在しない場合、スクリプトは移行先サーバーでロールの割り当てを適用することはできません。SECURITY スイッチを使用している場合でも同様です。|  
|[共有データ ソース]|はい|はい|スクリプトはターゲット サーバー上の既存のアイテムを上書きしません。 同じ名前のアイテムがターゲット サーバーに既に存在する場合は、次のようなエラー メッセージが表示されます。<br /><br /> `Migrating DataSource: /Data Sources/Aworks2012_oltp ... FAILURE:The item '/Data Sources/Aworks2012_oltp' already exists. ---> Microsoft.ReportingServices.Diagnostics.Utilities.ItemAlreadyExistsException: The item '/Data Source s/Aworks2012_oltp' already exists.`<br /><br /> 資格情報は、データ ソースの一部としてコピー **されません** 。 コンテンツ アイテムの移行後、移行先サーバーで資格情報を更新します。|  
|共有データセット|はい|はい||  
|Restore|はい|はい|スクリプトはターゲット サーバー上の既存のアイテムを上書きしません。 同じ名前のアイテムがターゲット サーバーに既に存在する場合は、次のようなエラー メッセージが表示されます。<br /><br /> `Migrating Folder: /Reports ... FAILURE: The item '/Reports' already exists. ---> Microsoft.ReportingServices.Diagnostics.Utilities.ItemAlreadyExistsException: The item '/Reports' already exists.`|  
|レポート|はい|はい|スクリプトはターゲット サーバー上の既存のアイテムを上書きしません。 同じ名前のアイテムがターゲット サーバーに既に存在する場合は、次のようなエラー メッセージが表示されます。<br /><br /> `Migrating Report: /Reports/testThe item '/Reports/test' already exists. ---> Microsoft.ReportingServices.Diagnostics.Utilities.ItemAlreadyExistsException: The item '/Reports/test' already exists.`|  
|パラメーター|はい|はい||  
|サブスクリプション|はい|はい||  
|履歴の設定|はい|はい|履歴の設定は移行されますが、履歴の詳細は移行されません。|  
|処理オプション|はい|はい||  
|キャッシュ更新オプション|はい|はい|依存設定はカタログ アイテムの一部として移行されます。 次に示しているのは、スクリプトがレポート (.rdl) と関連設定 (キャッシュ更新オプションなど) を移行するときの出力例です。<br /><br /> Migrating parameters for report TitleOnly.rdl 0 items found.<br /><br /> Migrating subscriptions for report TitleOnly.rdl:1 items found.<br /><br /> サブスクリプションを移行すると \\\ ホームに保存します。ブランド<br /><br /> Migrating history settings for report TitleOnly.rdl ...SUCCESS<br /><br /> Migrating processing options for report TitleOnly.rdl ...0 items found.<br /><br /> Migrating cache refresh options for report TitleOnly.rdl ...SUCCESS<br /><br /> Migrating cache refresh plans for report TitleOnly.rdl:1 items found.<br /><br /> Migrating cache refresh plan titleonly_refresh735amM2F ...SUCCESS|  
|キャッシュ更新計画|はい|はい||  
|画像|はい|はい||  
|レポート パーツ|はい|はい||  
  
##  <a name="bkmk_required_permissions"></a> 必要な権限  
 アイテムやリソースの読み書きに必要な権限は、スクリプトで使用されるすべてのメソッドで同じではありません。 次の表は、各アイテムまたはリソースに使用するメソッドをまとめたもので、各メソッドはそれぞれ関連するコンテンツにリンクされています。 必要な権限を表示するには、個々のトピックに移動してください。 たとえば、ListChildren メソッドのトピックでは、必要な権限が次のように示されています。  
  
-   **ネイティブ モードで必要な権限:** アイテムに対する ReadProperties  
  
-   **SharePoint モードで必要な権限:** ViewListItems  
  
|アイテムまたはリソース|ソース|移行先|  
|----------------------|------------|------------|  
|カタログ アイテム|<xref:ReportService2010.ReportingService2010.ListChildren%2A><br /><br /> <xref:ReportService2010.ReportingService2010.GetProperties%2A><br /><br /> <xref:ReportService2010.ReportingService2010.GetItemDataSources%2A><br /><br /> <xref:ReportService2010.ReportingService2010.GetItemReferences%2A><br /><br /> <xref:ReportService2010.ReportingService2010.GetDataSourceContents%2A><br /><br /> <xref:ReportService2010.ReportingService2010.GetItemLink%2A>|<xref:ReportService2010.ReportingService2010.CreateCatalogItem%2A><br /><br /> <xref:ReportService2010.ReportingService2010.SetItemDataSources%2A><br /><br /> <xref:ReportService2010.ReportingService2010.GetItemReferences%2A><br /><br /> <xref:ReportService2010.ReportingService2010.CreateDataSource%2A><br /><br /> <xref:ReportService2010.ReportingService2010.CreateLinkedItem%2A><br /><br /> <xref:ReportService2010.ReportingService2010.CreateFolder%2A>|  
|ロール|<xref:ReportService2010.ReportingService2010.ListRoles%2A><br /><br /> <xref:ReportService2010.ReportingService2010.GetRoleProperties%2A>|<xref:ReportService2010.ReportingService2010.CreateRole%2A>|  
|システム ポリシー|<xref:ReportService2010.ReportingService2010.GetSystemPolicies%2A>|<xref:ReportService2010.ReportingService2010.SetSystemPolicies%2A>|  
|[スケジュール]|<xref:ReportService2010.ReportingService2010.ListSchedules%2A>|<xref:ReportService2010.ReportingService2010.CreateSchedule%2A>|  
|サブスクリプション|<xref:ReportService2010.ReportingService2010.ListSubscriptions%2A><br /><br /> <xref:ReportService2010.ReportingService2010.GetSubscriptionProperties%2A><br /><br /> <xref:ReportService2010.ReportingService2010.GetDataDrivenSubscriptionProperties%2A>|<xref:ReportService2010.ReportingService2010.CreateSubscription%2A><br /><br /> <xref:ReportService2010.ReportingService2010.CreateDataDrivenSubscription%2A>|  
|キャッシュ更新計画|<xref:ReportService2010.ReportingService2010.ListCacheRefreshPlans%2A><br /><br /> <xref:ReportService2010.ReportingService2010.GetCacheRefreshPlanProperties%2A>|<xref:ReportService2010.ReportingService2010.CreateCacheRefreshPlan%2A>|  
|パラメーター|<xref:ReportService2010.ReportingService2010.GetItemParameters%2A>|<xref:ReportService2010.ReportingService2010.SetItemParameters%2A>|  
|実行オプション|<xref:ReportService2010.ReportingService2010.GetExecutionOptions%2A>|<xref:ReportService2010.ReportingService2010.SetExecutionOptions%2A>|  
|[キャッシュ オプション]|<xref:ReportService2010.ReportingService2010.GetCacheOptions%2A>|<xref:ReportService2010.ReportingService2010.SetCacheOptions%2A>|  
|履歴の設定|<xref:ReportService2010.ReportingService2010.GetItemHistoryOptions%2A>|<xref:ReportService2010.ReportingService2010.SetItemHistoryOptions%2A>|  
|アイテム ポリシー|<xref:ReportService2010.ReportingService2010.GetPolicies%2A>|<xref:ReportService2010.ReportingService2010.SetPolicies%2A>|  
  
 詳しくは、「 [Reporting Services のロールおよびタスクと SharePoint のグループおよび権限の比較](../reporting-services-roles-tasks-vs-sharepoint-groups-permissions.md)」をご覧ください。  
  
##  <a name="bkmk_how_to_use_the_script"></a> スクリプトの使用方法  
  
1.  スクリプト ファイルをローカル フォルダー (c: **\rss\ssrs_migration.rss** など) にダウンロードします。  
  
2.  **管理者特権**を使用してコマンド プロンプトを開きます。  
  
3.  ssrs_migration.rss ファイルのあるフォルダーに移動します。  
  
4.  シナリオに適したパラメーターを指定してコマンドを実行します。  
  
 **基本的な例 (ネイティブ モード レポート サーバー間):**  
  
 次の例では、ネイティブ モード **Sourceserver** からネイティブ モード **Targetserver** にコンテンツを移行します。  
  
 ```cmd
rs.exe -i ssrs_migration.rss -e Mgmt2010 -s http://SourceServer/ReportServer -u Domain\User -p password -v ts="http://TargetServer/reportserver" -v tu="Domain\Userser" -v tp="password"
```
  
 **使用に関するメモ:**  
  
-   スクリプトは 2 つのステップで実行されます。  
  
     最初のステップは監査です。移行されるアイテムのリストが返されます。2 番目のステップは移行です。  
  
     移行されるアイテムを一覧表示するのみ、またはパラメーターを変更するのみの場合は、最初の **ステップの後にスクリプトをキャンセル** できます。 依存設定は最初のステップで一覧表示されません。 たとえば、レポートのキャッシュ オプションは一覧表示されません。ただし、レポート自体は一覧表示されます。  
  
    > [!TIP]  
    >  単に 1 つのサーバーを監査する場合は、移行元および移行先として同じサーバーを使用し、ステップ 1 の後にキャンセルします。  
  
     最初のステップで一覧表示される監査情報は、移行元と移行先の両方のネイティブ モード サーバー上の既存のロールを確認するために役立ちます。 次に示しているのは、最初のステップである監査で表示される一覧の例です。 スイッチ -v security="True" を使用したため、一覧に "roles" セクションが含まれています。  
  
    -   `Retrieve and report the list of items that will be migrated. You can cancel the script after step 1 if you do not want to start the actual migration.`  
  
         `Retrieving roles:`  
  
         `Role: Browser`  
  
         `Role: Content Manager`  
  
         `Role: Model Item Browser`  
  
         `Retrieve and report the list of items that will be migrated. You can cancel the script after step 1 if you do not want to start the actual migration.`  
  
         `Retrieving roles:`  
  
         `Role: Browser`  
  
         `Role: Content Manager`  
  
         `Role: CustomRole`  
  
         `Role: Model Item Browser`  
  
         `Role: My Reports`  
  
         `Role: Publisher`  
  
         `Role: Report Builder`  
  
         `Role: System Administrator`  
  
         `Role: System User`  
  
         `Retrieving system policies:`  
  
         `Retrieving system policies:`  
  
         `System policy: BUILTIN\Administrators`  
  
         `System policy: domain\user1`  
  
         `System policy: domain\ueser2`  
  
         `Retrieving schedules:`  
  
         `Schedule: theMondaySchedule`  
  
         `Retrieving catalog items. This may take a while.`  
  
         `Folder: /Data Sources`  
  
         `DataSource: /Data Sources/Aworks2012_oltp`  
  
         `Folder: /images`  
  
         `Resource: /images/Boba Fett.png`  
  
         `Resource: /images/R2-D2.png`  
  
         `Folder: /Reports`  
  
         `Report: /Reports/products`  
  
         `Report: /Reports/test`  
  
         `Report: /Reports/TitleOnly`  
  
-   SOURCE_URL と TARGET_URL は、移行元と移行先の [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] レポート サーバーを参照する有効なレポート サーバー URL であることが必要です。 ネイティブ モードでは、レポート サーバー URL は次のようになります。  
  
    -   `http://servername/reportserver`  
  
     SharePoint モードでは、この URL は次のようになります。  
  
    -   `http://servername/_vti_bin/reportserver`  
  
-   SharePoint でユーザーに表示される仮想フォルダー構造は、基になっている構造と異なる場合があります。 ブラウザーで `http://servername/_vti_bin/reportserver` または `http://servername/sites/site_name/_vti_bin/reportserver` を開き、非仮想フォルダー構造を確認してください。 この情報は、SharePoint モード サーバーの移行元フォルダーと移行先フォルダーを "/" 以外に設定するために役立ちます。  
  
-   パスワードは移行されないため、再入力する必要があります。たとえば、保存された資格情報を使用するデータ ソースなどです。  
  
##  <a name="bkmk_parameter_description"></a> パラメーターの説明  
  
|パラメーター|[説明]|必須|  
|---------------|-----------------|--------------|  
|**-s** Source_URL|移行元レポート サーバーの URL。|はい|  
|**-u** Domain\password **-p** password|移行元サーバーの資格情報。|省略可能。省略した場合は既定の資格情報が使用されます。|  
|**-v st**="SITE"||省略可能。 このパラメーターは SharePoint モード レポート サーバーにのみ使用されます。|  
|**- v f**="SOURCEFOLDER"|すべての移行の場合は "/" に設定し、部分的な移行の場合は "/フォルダー/サブフォルダー" に設定します。 指定したフォルダー内のすべてのコンテンツがコピーされます。|省略可能。既定値は "/" です。|  
|**-v ts**="TARGET_URL"|移行先 RS サーバーの URL。||  
|**-v tu**="domain\username" **-v tp**="password"|ターゲット サーバーの資格情報。|省略可能。省略した場合は既定の資格情報が使用されます。 **注:** ユーザーは共有スケジュールの "作成者" およびレポート アイテムの "変更元" アカウントとしてターゲット サーバーで一覧表示されます。|  
|**-v tst**="SITE"||省略可能。 このパラメーターは SharePoint モード レポート サーバーにのみ使用されます。|  
|**-v tf** ="TARGETFOLDER"|ルート レベルに移行する場合は "/" に設定します。 既存のフォルダーにコピーする場合は "/フォルダー/サブフォルダー" に設定します。 "SOURCEFOLDER" 内のすべてのコンテンツが "TARGETFOLDER" にコピーされます。|省略可能。既定値は "/" です。|  
|**-v security**= "True/False"|"False" に設定した場合、移行先カタログ アイテムには移行先システムの設定に従ってセキュリティ設定が継承されます。 この設定は、ネイティブ モードから SharePoint モードへなど、異なるモードのレポート サーバー間の移行にお勧めします。 "True" に設定した場合、スクリプトはセキュリティ設定を移行しようとします。|省略可能。既定値は "False" です。|  
  
##  <a name="bkmk_more_examples"></a> その他の例  
  
###  <a name="bkmk_native_2_native"></a> ネイティブ モード レポート サーバー間  
 次の例では、ネイティブ モード **Sourceserver** からネイティブ モード **Targetserver** にコンテンツを移行します。  
  
```cmd
rs.exe -i ssrs_migration.rss -e Mgmt2010 -s http://SourceServer/ReportServer -u Domain\User -p password -v ts="http://TargetServer/reportserver" -v tu="Domain\Userser" -v tp="password"  
```  
  
 次の例では、security スイッチを追加します。  
  
```cmd
rs.exe -i ssrs_migration.rss -e Mgmt2010 -s http://SourceServer/ReportServer -u Domain\User -p password -v ts="http://TargetServer/reportserver" -v tu="Domain\Userser" -v tp="password" -v security="True"  
```  
  
###  <a name="bkmk_native_2_sharepoint_root"></a> ネイティブ モードから SharePoint モード (ルート サイト)  
 次の例では、ネイティブ モード **SourceServer** から SharePoint モード サーバー **TargetServer**上の "ルート サイト" にコンテンツを移行します。 ネイティブ モード サーバー上の "Reports" および "Data Sources" フォルダーは SharePoint 配置上の新しいライブラリとして移行されます。  
  
 ![ssrs_rss_migrate_root_site](../media/ssrs-rss-migrate-root-site.gif "ssrs_rss_migrate_root_site")  
  
```cmd
rs.exe -i ssrs_migration.rss -e Mgmt2010 -s http://SourceServer/ReportServer -u Domain\User -p Password -v ts="http://TargetServer/_vti_bin/ReportServer" -v tu="Domain\User" -v tp="Password"  
```  
  
###  <a name="bkmk_native_2_sharepoint_with_site"></a> ネイティブ モードから SharePoint モード ("bi" サイト コレクション)  
 次の例では、ネイティブ モード サーバーから、"sites/bi" サイト コレクションおよび共有ドキュメント ライブラリを含む SharePoint サーバーにコンテンツを移行します。 スクリプトは移行先ドキュメント ライブラリ内にフォルダーを作成します。 たとえば、移行先ドキュメント ライブラリ内に "Reports" および "Data Sources" フォルダーを作成します。  
  
```cmd
rs.exe -i ssrs_migration.rss -e Mgmt2010 -s http://SourceServer/ReportServer -u Domain\User -p Password -v ts="http://TargetServer/sites/bi/_vti_bin/reportserver" -v tst="sites/bi" -v tf="Shared Documents" -v tu="Domain\User" -v tp="Password"  
```  
  
###  <a name="bkmk_sharepoint_2_sharepoint"></a> SharePoint モードから SharePoint モード ("bi" サイト コレクション)  
 この例では、次のようにコンテンツを移行します。  
  
-   "sites/bi" サイト コレクションおよび共有ドキュメント ライブラリを含む SharePoint サーバー **SourceServer** から。  
  
-   "sites/bi" サイト コレクションおよび共有ドキュメント ライブラリを含む SharePoint サーバー **TargetServer** に。  
  
```cmd
rs.exe -i ssrs_migration.rss -e Mgmt2010 -s http://SourceServer/_vti_bin/reportserver -v st="sites/bi" -v f="Shared Documents" -u Domain\User1 -p Password -v ts="http://TargetServer/sites/bi/_vti_bin/reportserver" -v tst="sites/bi" -v tf="Shared Documents" -v tu="Domain\User" -v tp="Password"  
```  
  
###  <a name="bkmk_native_to_native_Azure_vm"></a>ネイティブモードからネイティブモード (Azure 仮想マシン)  
 この例では、次のようにコンテンツを移行します。  
  
-   ネイティブ モード レポート サーバー **SourceServer**から。  
  
-   Azure 仮想マシン上で実行されているネイティブ モード レポート サーバー **TargetServer** に。 **TargetServer は Sourceserver**のドメインに参加しておらず、 **User2**は Azure 仮想マシン**TargetServer**の管理者です。  
  
```cmd
rs.exe -i ssrs_migration.rss -e Mgmt2010 -s http://SourceServer/ReportServer -u Domain\user1 -p Password -v ts="http://ssrsnativeazure.cloudapp.net/ReportServer" -v tu="user2" -v tp="Password2"  
```  
  
> [!TIP]  
>  Windows PowerShell を使用して Azure 仮想マシン上に [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] レポート サーバーを作成する方法については、「[PowerShell を使用したネイティブ モードのレポート サーバーを含む Azure VM の作成](https://msdn.microsoft.com/library/dn449661.aspx)」をご覧ください。  
  
##  <a name="bkmk_sharepoint_site_to_native_Azure_vm"></a>SharePoint モード-Azure 仮想マシン上のネイティブモードサーバーへの ' bi ' サイトコレクション  
 この例では、次のようにコンテンツを移行します。  
  
-   "sites/bi" サイト コレクションおよび共有ドキュメント ライブラリを含む SharePoint モード レポート サーバー **SourceServer** から。  
  
-   Azure 仮想マシン上で実行されているネイティブ モード レポート サーバー **TargetServer** に。 **TargetServer は Sourceserver**のドメインに参加しておらず、 **User2**は Azure 仮想マシン**TargetServer**の管理者です。  
  
```cmd
rs.exe -i ssrs_migration.rss -e Mgmt2010 -s http://uetesta02/_vti_bin/reportserver -u user1 -p Password -v ts="http://ssrsnativeazure.cloudapp.net/ReportServer" -v tu="user2" -v tp="Passowrd2"  
```  
  
##  <a name="bkmk_verification"></a> 検証  
 このセクションは、コンテンツとポリシーが正常に移行されたことを確認するために移行先サーバーで実行する一部の手順をまとめたものです。  
  
### <a name="schedules"></a>スケジュール  
 ターゲット サーバーでスケジュールを確認するには:  
  
 **Native Mode**  
  
1.  移行先サーバーでレポート マネージャーを参照します。  
  
2.  トップ メニューの **[サイトの設定]** をクリックします。  
  
3.  左ペインで **[スケジュール]** をクリックします。  
  
 **SharePoint モード:**  
  
1.  **[サイトの設定]** を参照します。  
  
2.  **[Reporting Services]** グループで、 **[共有スケジュールの管理]** をクリックします。  
  
### <a name="roles-and-groups"></a>ロールとグループ  
 **Native Mode**  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を開き、ネイティブ モード レポート サーバーに接続します。  
  
2.  **オブジェクト エクスプローラー** で **[セキュリティ]** をクリックします。  
  
3.  **[ロール]** をクリックします。  
  
##  <a name="bkmk_troubleshoot"></a> トラブルシューティング  
 より詳細な情報が表示されるようにするには、トレース フラグ **-t** を使用します。 たとえば、スクリプトを実行し、次のようなメッセージが表示されたとします。  
  
-   Could not connect to server: http://\<servername>/ReportServer/ReportService2010.asmx  
  
 **-T**フラグを使用してスクリプトをもう一度実行すると、次のようなメッセージが表示されます。  
  
-   System.Exception: Could not connect to server: http://\<servername>/ReportServer/ReportService2010.asmx ---> System.Net.WebException: **The request failed with HTTP status 401: Unauthorized**.   at System.Web.Services.Protocols.SoapHttpClientProtocol.ReadResponse(SoapClientMessage message, WebResponse response, Stream responseStream, Boolean asyncCall)   at System.Web.Services.Protocols.SoapHttpClientProtocol.Invoke(String methodName, Object[] parameters)   at Microsoft.SqlServer.ReportingServices2010.ReportingService2010.IsSSLRequired()   at Microsoft.ReportingServices.ScriptHost.Management2010Endpoint.PingService(String url, String userName, String password, String domain, Int32 timeout)   at Microsoft.ReportingServices.ScriptHost.ScriptHost.DetermineServerUrlSecurity()   --- End of inner exception stack trace ---  
  
## <a name="see-also"></a>参照  
 [RS.exe ユーティリティ &#40;SSRS&#41;](rs-exe-utility-ssrs.md)   
 [Compare Roles and Tasks in Reporting Services to SharePoint Groups and Permissions](../reporting-services-roles-tasks-vs-sharepoint-groups-permissions.md)  
