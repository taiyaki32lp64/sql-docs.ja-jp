---
title: Power BI Report Server の統合 (構成マネージャー) | Microsoft Docs
author: maggiesMSFT
ms.author: maggies
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
ms.date: 09/17/2017
ms.openlocfilehash: c2013e99f5e222c50d954e292cbc0b48b39cb7c9
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68265644"
---
# <a name="power-bi-report-server-integration-configuration-manager"></a>Power BI レポート サーバーの統合 (構成マネージャー)

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成マネージャーの **[Power BI 統合]** ページを使用して、レポート サーバーを目的の Azure Active Directory (AD) 管理対象テナントに登録すると、レポート サーバーのユーザーはサポートされるレポート アイテムを [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] ダッシュボードにピン留めできるようになります。 ピン留めできるサポートされているアイテムの一覧については、「 [Power BI ダッシュボードへの Reporting Services のアイテムのピン留め](../../reporting-services/pin-reporting-services-items-to-power-bi-dashboards.md)」を参照してください。

## <a name="bkmk_requirements"></a> Power BI 統合の要件

[!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] サービスを参照できるようにするためのアクティブなインターネット接続に加え、 [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)]統合を完了するには次の要件があります。

- **Azure Active Directory:** 組織で Azure Active Directory を使用する必要があります。Azure Active Directory では、Azure サービスと Web アプリケーションのディレクトリと ID を管理できます。 詳細については、「 [Azure Active Directory とは](https://azure.microsoft.com/documentation/articles/active-directory-whatis/)」を参照してください。

- **管理対象テナント:** レポート アイテムをピン留めする [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] ダッシュボードは、Azure AD 管理対象テナントに属している必要があります。  管理対象テナントは、組織が Office 365 や Microsoft Intune などの Azure サービスに初めてサブスクライブしたときに自動的に作成されます。   バイラル テナントは現在サポートされていません。  詳細については、「 [Azure AD ディレクトリとは](https://msdn.microsoft.com/library/azure/jj573650.aspx#BKMK_WhatIsAnAzureADTenant)」の「Azure AD テナントとは」および「Azure AD ディレクトリを取得する方法」を参照してください。

- [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] 統合を実行するユーザーは、Azure AD テナントのメンバーで、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] システム管理者であり、ReportServer カタログ データベースのシステム管理者でもある必要があります。

- [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] 統合を実行するユーザーは、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のインストールに使用するアカウントまたは [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]サービスが実行されているアカウントで [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成マネージャーを起動する必要があります

- ピン留めするレポートでは、保存された資格情報を使用する必要があります。 これは [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] 統合自体の要件ではありませんが、ピン留めされたアイテムの更新プロセスの要件となっています。  レポート アイテムのピン留め操作により、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] でのタイルの更新スケジュールを管理する [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)]サブスクリプションが作成されます。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サブスクリプションでは、保存された資格情報が必要です。 レポートで保存された資格情報を使用していない場合、ユーザーは引き続きレポート アイテムをピン留めできますが、関連付けられたサブスクリプションが [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)]でデータを更新しようとすると、 **[個人用サブスクリプション]** ページに次のようなエラー メッセージが表示されます。

    PowerBI 配信エラー: ダッシュ ボード: IT 支払い分析のサンプル、ビジュアル: Chart2、エラー: 現在のアクションを完了できません。 ユーザー データ ソースの資格情報が、このレポートまたは共有データセットを実行するための要件を満たしていません。 ユーザー データ ソースの資格情報が.

資格情報を保存する方法の詳細については、「 [Reporting Services データ ソースに資格情報を保存する](../../reporting-services/report-data/store-credentials-in-a-reporting-services-data-source.md)」の「レポート固有のデータ ソース用の保存された資格情報を構成する」を参照してください。

管理者は、  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のログ ファイルで詳細を確認できます。  次のようなメッセージが表示されます。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のログ ファイルを確認および監視する優れた方法として、ファイルに対して [!INCLUDE[msCoName](../../includes/msconame-md.md)] Power Query を使用します。  詳細情報と短いビデオについては、「 [レポート サーバー サービスのトレース ログ](../../reporting-services/report-server/report-server-service-trace-log.md)」を参照してください。

- subscription!WindowsService_1!1458!09/24/2015-00:09:27:: e ERROR: PowerBI 配信エラー: ダッシュ ボード: IT 支払い分析のサンプル、ビジュアル: Chart2、エラー: 現在のアクションを完了できません。 ユーザー データ ソースの資格情報が、このレポートまたは共有データセットを実行するための要件を満たしていません。 ユーザー データ ソースの資格情報がレポート サーバー データベースに格納されていないか、ユーザー データ ソースが、資格情報を要求しないように構成されているにもかかわらず、自動実行アカウントが指定されていません。

- notification!WindowsService_1!1458!09/24/2015-00:09:27:: e ERROR: Error occurred processing subscription fcdb8581-d763-4b3b-ba3e-8572360df4f9: PowerBI 配信エラー: ダッシュ ボード: IT 支払い分析のサンプル、ビジュアル: Chart2、エラー: 現在のアクションを完了できません。 ユーザー データ ソースの資格情報が、このレポートまたは共有データセットを実行するための要件を満たしていません。 ユーザー データ ソースの資格情報がレポート サーバー データベースに格納されていないか、ユーザー データ ソースが、資格情報を要求しないように構成されているにもかかわらず、自動実行アカウントが指定されていません。

## <a name="bkmk_steps2integrate"></a> レポート サーバーを統合および登録するには

[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成マネージャーで次の手順を完了します。 詳細については、「[Reporting Services 構成マネージャー](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)」を参照してください。

1. [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] 統合ページを選択します。

2. **[Power BI に登録]** を選択します。

    >[!Note]
    > ポート 443 がブロックされていないことを確認してください。

3. [!INCLUDE[msCoName](../../includes/msconame-md.md)] サインイン ダイアログで、 [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)]へのサインインに使用する資格情報を入力します。

4. 登録が完了すると、 **[Power BI の登録の詳細]** セクションに Azure テナント ID とリダイレクト URL が示されます。  この URL は、 [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] ダッシュボードが登録済みのレポート サーバーと通信するためのサインインおよび通信プロセスの中で使用されます。

5. **[結果]** ウィンドウの **[コピー]** ボタンをクリックして、登録の詳細を Windows クリップボードにコピーし、後で参照できるように保存します。

## <a name="bkmk_unregister"></a> Power BI への登録の解除

**登録解除:** Azure Active Directory からレポート サーバーの登録を解除すると、次のようになります。

- Web ポータルのメニュー バーに **[個人用設定]** リンクが表示されなくなります。

- 既にピン留めされているレポート アイテムはダッシュボードに引き続きピン留めされますが、ダッシュボードでタイルが更新されなくなります。

- タイルを更新していた [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サブスクリプションはレポート サーバー上に引き続き存在しますが、構成済みのスケジュールでサブスクリプションが実行されると、次のようなエラー メッセージが表示されます。

    **このサブスクリプションの配信拡張機能を読み込めませんでした。**

構成マネージャーの **Power BI** ページで、 **[Power BI への登録を解除]** を選択します。

##  <a name="bkmk_updateregistration"></a> 登録の更新

レポート サーバーの構成を変更した場合は、 **[登録の更新]** を使用します。 たとえば、ユーザーが [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)]を参照する際に使用する URL を追加または削除する場合は、次の手順を実行します。

- [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成マネージャーで、 **Web ポータルの URL** を選択します。

     **[詳細設定]** を選択します。

- **[追加]** を選択して、 [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] の新しい HTTP ID を追加し、 **[OK]** を選択します。

     [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] アイコンが変更され、サーバー構成が変更されたことが示されます。  ![ssrs_powebi_icon_warning](../../reporting-services/install-windows/media/ssrs-powebi-icon-warning.png "ssrs_powebi_icon_warning")

- **[Power BI 統合]** ページで、 **[登録の更新]** を選択します。

     Azure AD へのログインを求められます。 ページが更新され、 **[リダイレクト URL]** に新しい URL が表示されます。

##  <a name="bkmk_integration_process"></a> Power BI の統合とピン留めのプロセスの概要

ここでは、レポート サーバーを [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] と統合し、レポート アイテムをダッシュボードにピン留めするときの基本的な手順と関連するテクノロジの概要を説明します。

 **統合:**

1. 構成マネージャーで、 **[Power BI に登録]** をクリックすると、Azure Active Directory へのサインインを求められます。

2. [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] クライアント アプリが管理対象テナントに登録されます。

3. Azure Active Directory 内で管理されるテナントで Power BI クライアント アプリが作成されます。

4. 登録には、ユーザーがレポート サーバーからサインインするときに使用されるリダイレクト URL が含まれます。  アプリ ID と URL が ReportServer データベースに保存されます。 リダイレクト URL は、Azure への認証要求からレポート サーバーに制御を戻すことができるように、認証要求時に使用されます。 たとえば、ユーザーがサインインするときやアイテムをダッシュボードにピン留めするときに使用されます。

5. 構成マネージャーにアプリ ID と URL が表示されます。

 ![ssrs_pbiflow_integration](../../reporting-services/install-windows/media/ssrs-pbiflow-integration.png "ssrs_pbiflow_integration")

 **ユーザーがレポート アイテムをダッシュボードにピン留めする場合:**

1. ユーザーが [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] でレポートをプレビューし、 [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)]でレポート アイテムをクリックして初めてピン留めすると、

2. Azure AD サインイン ページにリダイレクトされます。 ユーザーは、 [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] **My Settings** page. ユーザーが Azure 管理対象テナントにサインインすると、Azure アカウントと [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のアクセス許可の間に関係が確立されます。  詳細については、「 [Power BI 統合の個人用設定 &#40;Web ポータル&#41;](../my-settings-for-power-bi-integration-web-portal.md)」を参照してください。

3. ユーザーのセキュリティ トークンがレポート サーバーに返されます。

4. ユーザーのセキュリティ トークンが ReportServer データベースに保存されます。

5. [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] サービスから、そのユーザーがアクセスできるグループとダッシュボードの一覧が取得されます。  ユーザーは、ピン留め先のグループとダッシュボードを選択し、 [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] タイルのデータの更新頻度を構成します。

6. レポート アイテムがダッシュボードにピン留めされます。

7. ダッシュボード タイルのレポート アイテムのスケジュールされた更新を管理するために、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サブスクリプションが作成されます。 サブスクリプションでは、ユーザーがサインインしたときに作成されたセキュリティ トークンを使用します。

     トークンの有効期間は **90 日間**です。有効期間を過ぎたら、ユーザーはもう一度サインインして新しいユーザー トークンを作成する必要があります。 トークンの有効期限が切れても、ピン留めされたタイルはダッシュボードに引き続き表示されますが、データは更新されなくなります。  新しいユーザー トークンが作成されるまで、ピン留めされたアイテムに使用される [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サブスクリプションでエラーが発生します。 「 [Power BI 統合の個人用設定 &#40;Web ポータル&#41;](../my-settings-for-power-bi-integration-web-portal.md)」を参照してください。 」を参照してください。

ユーザーが 2 回目にアイテムをピン留めするときは、手順 1 ～ 4 がスキップされます。代わりに、ReportServer データベースからアプリ ID と URL が取得され、手順 5 からフローが続行されます。

![ssRS-pin-to-powerbi-flow](../../reporting-services/install-windows/media/ssrs-pin-to-powerbi-flow.png)

 **サブスクリプションが起動してダッシュボード タイルを更新する場合:**

1. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サブスクリプションが起動すると、レポートが表示されます。

2. ユーザー トークンが ReportServer データベースから取得されます。

3. トークンと共に、レポート アイテムの状態とデータが [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)]サービスに送信されます。

4. トークンが Azure AD に送信され、検証されます。 トークンが有効な場合、レポート アイテムのデータがダッシュボード タイルに送信され、タイルの日付プロパティが更新されます。

5. トークンが無効な場合は、エラーが返され、レポート サーバーでログに記録されます。  状態などの情報はダッシュボードに送信されません。

![ssRS-subscription-to-powerbi-flow](../../reporting-services/install-windows/media/ssrs-subscription-to-powerbi-flow.png)

   <iframe width="560" height="315" src="https://www.youtube.com/embed/QhPQObqmMPc" frameborder="0" allowfullscreen></iframe>

## <a name="considerations-and-limitations"></a>注意点と制限事項

* バイラルおよび政府用テナントはサポートされていません。

## <a name="next-steps"></a>次の手順

[Power BI 統合の個人用設定 &#40;Web ポータル&#41;](../my-settings-for-power-bi-integration-web-portal.md)  
[Power BI ダッシュボードへの Reporting Services のアイテムのピン留め](../../reporting-services/pin-reporting-services-items-to-power-bi-dashboards.md)
[Power BI のダッシュボード](https://powerbi.microsoft.com/documentation/powerbi-service-dashboards/)  

その他の質問 [Reporting Services のフォーラムに質問してみてください](https://go.microsoft.com/fwlink/?LinkId=620231)
