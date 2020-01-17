---
title: システム設定 (マスター データ サービス) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- Master Data Services, system settings
- system settings [Master Data Services]
ms.assetid: 83075cdf-f059-4646-8ba2-19be8202f130
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 2384d6fa7831c38ff68f495485555701f2a1f7ba
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68085597"
---
# <a name="system-settings-master-data-services"></a>システム設定 (マスター データ サービス)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  任意の [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] データベースに関連付けられているすべての Web アプリケーションおよび Web サービスについて、システム設定を構成できます。  
  
 これらの設定の多くは、 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] の **[データベース]** ページで構成できます。 その他の設定は、 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] データベースの System Settings テーブル (mdm.tblSystemSetting) で構成できます。  
  
 設定は次のカテゴリに分類できます。  
  
-   [全般設定](#General)  
  
-   [バージョン管理設定](#Versions)  
  
-   [ステージング設定](#Staging)  
  
-   [エクスプローラー設定](#Explorer)  
  
-   [Excel 設定用アドイン](#xls)  
  
-   [ビジネス ルール設定](#BusinessRules)  
  
-   [通知設定](#Notifications)  
  
-   [セキュリティ設定](#Security)  
  
-   [未使用](#NotUsed)  
  
##  <a name="General"></a> 全般設定  
  
|構成マネージャーの設定|システム設定|説明|  
|-----------------------------------|--------------------|-----------------|  
|**[データベース接続のタイムアウト]**|**DatabaseConnectionTimeOut**|[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] データベースで接続が完了するまでに許容される秒数。 この時間内に接続が完了しない場合、接続が取り消されエラーが返されます。 既定値は **60** 秒 (1 分) です。|  
|**[データベース コマンドのタイムアウト]**|**DatabaseCommandTimeOut**|[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] データベースでコマンドが完了するまでに許容される秒数。 この時間内にコマンドが完了しない場合、コマンドは取り消されエラーが返されます。 既定値は **3600** 秒 (60 分) です。|  
|**[Web サービスのタイムアウト]**|**ServerTimeOut**|ASP.NET で [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] ページの要求を完了するまでに許容される秒数。 この時間内に要求を完了しない場合、要求はキャンセルされエラーが返されます。 既定値は **120000** 秒 (2000 分) です。|  
|**[クライアントのタイムアウト]**|**ClientTimeOut**|[!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] がホーム ページに戻るまでの非アクティブ期間 (秒数)。 既定値は **300** 秒 (5 分) です。|  
|**[バッチごとの行数]**|**RowsPerBatch**|Web サービスによって各バッチで取得するレコード数。 既定値は **50**です。|  
||**ApplicationName**|イベント ログに表示されるテキスト。 既定値は **MDM**です。|  
||**SiteTitle**|[!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web ブラウザーのタイトル バーに表示されるテキスト。 既定値は **[マスター データ マネージャー]** です。|  
|**[ログ保有期間日数]**|**LogRentionDays**|ログが削除されるまでの日数。 既定値は -1 で、ログ テーブルが消去されないことを示します。<br /><br /> 値が 0 の場合、ログ テーブルには当日のデータのみが保持されます。 前の日のデータのログは切り捨てられます。<br /><br /> 値が 0 より大きい場合、ログ データは値で指定した日数保持されます。|  
  
##  <a name="Versions"></a> バージョン管理設定  
  
|構成マネージャーの設定|システム設定|説明|  
|-----------------------------------|--------------------|-----------------|  
|**[コミット済みのバージョンだけをコピーする]**|**CopyOnlyCommittedVersion**|[!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]で、ユーザーがコピーできるモデル バージョンは、状態が **[コミット済み]** のバージョンであるか、またはすべての状態のバージョンであるかを示します。 既定値は **[はい]** または **1**で、ユーザーが **[コミット済み]** バージョンのみをコピーできることを示します。 値を **[いいえ]** または **2** に変更すると、ユーザーはすべてのバージョンをコピーできます。|  
  
 詳細については、「[バージョン (マスター データ サービス)](../master-data-services/versions-master-data-services.md)」を参照してください。  
  
##  <a name="Staging"></a> ステージング設定  
  
|構成マネージャーの設定|システム設定|説明|  
|-----------------------------------|--------------------|-----------------|  
|**[すべてのステージング トランザクションをログに記録]**|**StagingTransactionLogging**|SQL Server 2008 R2 だけに適用されます。 ステージング レコードが [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] データベースに読み込まれるときにトランザクションをログに記録するかどうかを示します。 既定値は **[オフ]** または **2**です。 値を **[オン]** または **1** に変更すると、ログ記録が有効になります。|  
|**[ステージング バッチの間隔]**|**StagingBatchInterval**|[!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] **[統合管理]** 機能領域で、 **[バッチの開始]** をクリックしてからバッチが処理されるまでの秒数を示します。 既定値は **60** 秒 (1 分) です。|  
  
 詳細については、「[概要:テーブルからデータをインポートする &#40;マスター データ サービス&#41;](../master-data-services/overview-importing-data-from-tables-master-data-services.md)」を参照してください。  
  
##  <a name="Explorer"></a> エクスプローラー設定  
  
|構成マネージャーの設定|システム設定|説明|  
|-----------------------------------|--------------------|-----------------|  
|**[既定で階層内のメンバーの数]**|**HierarchyChildNodeLimit**|[!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] の **[エクスプローラー]** 機能領域で、 **[詳細]** が表示されるまでに、各階層ノードに表示されるメンバーの最大数を示します。 **[詳細]** をクリックすると、次のメンバーのグループを表示できます。 既定値は **50**です。|  
|**[既定で階層内の名前を表示する]**|**ShowNamesInHierarchy**|[!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] **[エクスプローラー]** 機能領域で、階層を表示する場合に選択する既定の設定を示します。<br /><br /> 既定値は **[はい]** または **1**で、各メンバーの名前とコードが表示されることを示します。 値を **[いいえ]** または **2** に変更すると、コードのみが表示されます。|  
|**[一覧内のドメインベースの属性数]**|**DBAListRowLimit**|[!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] **[エクスプローラー]** 機能領域で、グリッド内のドメインベースの属性値をダブルクリックするときに一覧に表示される属性の数を示します。 既定値は **50**です。 メンバー数が 50 を超える場合は、検索可能なダイアログが代わりに表示されます。|  
||**GridFilterDefaultFuzzySimilarityLevel**|[!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] **[エクスプローラー]** 機能領域で、 **[次と一致する]** フィルター条件を使用している場合に使用される類似性のレベルを示します。 既定値は、 **0.3**です。 **1** に近い値を設定すると、検索条件に近い一致が返されます。 完全一致を検索するには **1** に設定します。|  
  
##  <a name="xls"></a> Excel 設定用アドイン  
  
|構成マネージャーの設定|システム設定|説明|  
|-----------------------------------|--------------------|-----------------|  
|[Web サイト ホーム ページで Excel テキスト用アドインを表示]|ShowAddInText|[!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] ホーム ページで、 [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)]をダウンロードするためのリンクを表示します。|  
|[Web サイト ホーム ページでの Excel 用アドインのインストール パス]|AddInURL|[!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] ホーム ページで [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)] へのリンクが表示される場合に、ユーザーがリンクをクリックした場合の移動先となる場所。|  
  
##  <a name="BusinessRules"></a> ビジネス ルール設定  
  
|構成マネージャーの設定|システム設定|説明|  
|-----------------------------------|--------------------|-----------------|  
|**[新しいビジネス ルールの増分数]**|**BusinessRuleDefaultPriorityIncrement**|[!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] **[システム管理]** 機能領域で、新しい各ビジネス ルールの優先度の増分数を示します。 既定値は **10**です。|  
|**[ビジネス ルールを適用するメンバーの数]**|**BusinessRuleRealtimeMemberCount**|[!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] **[エクスプローラー]** 機能領域で、ビジネス ルールを適用するグリッド内のメンバーの最大数を示します。 [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)]では、ビジネス ルールを適用するアクティブなワークシート内のメンバーの最大数を示します。 既定値は **10000**です。|  
|**[Business Rule User Script Execute First]\(ビジネス ルール ユーザー スクリプトを最初に実行\)**|**BusinessRuleUserScriptExecuteFirst**|通常、ビジネス ルール アクションは、"既定値"、"値の変更"、"検証"、"外部アクション"、"ユーザー定義アクション スクリプト" の順に実行します。 この設定が **1** に変更されると、"ユーザー定義アクション スクリプト" がビジネス ルール アクションの最初に実行される手順になります。 この設定は、非表示の設定です。 既定値は **0**です。|  
  
 詳細については、「[ビジネス ルール (マスター データ サービス)](../master-data-services/business-rules-master-data-services.md)」を参照してください。  
  
##  <a name="Notifications"></a> 通知設定  
  
|構成マネージャーの設定|システム設定|説明|  
|-----------------------------------|--------------------|-----------------|  
|**[通知に対するマスター データ マネージャーの URL]**|**MDMRootURL**|電子メール通知のリンクで使用される [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web アプリケーションの URL (`https://constoso/mds` など)。|  
|**[通知電子メールの送信間隔]**|**NotificationInterval**|電子メール通知を送信する頻度 (秒数)。 既定値は **120** 秒 (2 分) です。|  
|**[電子メールごとの通知の数]**|**NotificationsPerEmail**|単一の電子メールに記載される検証の問題の最大数。 これを超える数の問題が存在しても、電子メールには含まれません (ただし、 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]では確認できます)。|  
|**[既定の電子メールの形式]**|**EmailFormat**|すべての電子メール通知の形式。 既定値は **[HTML]** または **1**です。 データベース設定値 **2** は、 **テキスト**を意味します。<br /><br /> 注:この設定は、ユーザーごとにオーバーライドすることができます。オーバーライドするには、[!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]で、ユーザーの **[全般]** タブの **[電子メールの形式]** を変更して保存します。|  
|**[電子メール アドレスの正規表現]**|**EmailRegExPattern**|[!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] **[ユーザー/グループの権限]** 機能領域で、ユーザーの **[電子メールの形式]** を変更して保存します。正規表現の詳細については、MSDN ライブラリの「 [正規表現言語要素](https://go.microsoft.com/fwlink/?LinkId=164401) 」を参照してください。|  
|**[データベース メール アカウント]**|**EmailProfilePrincipalAccount**|電子メール通知を送信するときに使用するデータベース メール アカウントを表示します。 既定のプロファイルは **mds_email_user**です。|  
|**[データベース メール プロファイル]**|**DatabaseMailProfile**|電子メール通知を送信するときに使用するデータベース メール プロファイル。 既定値は空白です。|  
||**ValidationIssueHTML**|HTML 形式で、ビジネス ルールによる検証が失敗したときに電子メール ユーザーが取得するテキストを示します。|  
||**ValidationIssueText**|プレーンテキスト形式で、ビジネス ルールによる検証が失敗したときに電子メール ユーザーが取得するテキストを示します。|  
||**VersionStatusChangeText**|プレーンテキスト形式で、バージョンの状態が変更するときにユーザーが取得する電子メールのテキストを示します。 この電子メールを受信するのは、モデル全体に対する **[更新]** 権限を持つユーザーのみです。|  
||**VersionStatusChangeHTML**|HTML 形式で、バージョンの状態が変更するときにユーザーが取得する電子メールのテキストを示します。 この電子メールを受信するのは、モデル全体に対する **[更新]** 権限を持つユーザーのみです。|  
  
 詳細については、「[通知 (マスター データ サービス)](../master-data-services/notifications-master-data-services.md)」を参照してください。  
  
##  <a name="Security"></a> セキュリティ設定  
  
|構成マネージャーの設定|システム設定|説明|  
|-----------------------------------|--------------------|-----------------|  
||**SecurityMemberProcessInterval**|[!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] **[ユーザー/グループの権限]** 機能領域で、 **[階層メンバー]** タブで設定したユーザーとグループの権限が適用される頻度 (秒数) を示します。 既定値は **3600** 秒 (60 分) です。|  

##  <a name="Performance"></a> パフォーマンス設定  

|構成マネージャーの設定|システム設定|説明|  
|-----------------------------------|--------------------|-----------------|  
|**Enable performance improvement setting (パフォーマンス向上の設定を有効にする)**|**PerformanceImprovementEnable**|読み込みアクセス許可関連のページのパフォーマンスがよくなるこの設定は既定で有効になります (**1 に設定**)。 ただし、この状況では、エンティティ、属性、ユーザー、またはグループの作成/変更はパフォーマンスが低下します。 これを回避するには、この設定を無効にできます (**0 に設定**)。 この設定を変更した後。 コマンド "**EXEC [mdm].[udpPerformanceToggleSwitch];** " を実行して、ビューとデータが正しいことを確認する必要があります。|  
  
 詳細については、「[メンバー権限を直ちに適用する (マスター データ サービス)](../master-data-services/immediately-apply-member-permissions-master-data-services.md)」を参照してください。  
  
##  <a name="NotUsed"></a> 未使用  
 System Settings テーブルの次の設定は、使用されません。  
  
-   **SecurityMode**  
  
-   **MDSHubName**  
  
-   **ApplicationLogging**  
  
-   **ReportServer**  
  
-   **ReportDirectory**  
  
-   **BusinessRuleEngineIterationLimit**  
  
-   **BusinessRuleExtensibility**  
  
-   **AttributeExplorerMarkAllActionMemberCount**  
  
## <a name="see-also"></a>関連項目  
 [データベース オブジェクト セキュリティ (マスター データ サービス)](../master-data-services/database-object-security-master-data-services.md)  
  
  
