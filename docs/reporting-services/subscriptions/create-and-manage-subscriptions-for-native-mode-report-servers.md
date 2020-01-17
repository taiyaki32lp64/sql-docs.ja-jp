---
title: ネイティブ モード レポート サーバーのサブスクリプションの作成と管理 | Microsoft Docs
ms.date: 05/28/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: subscriptions
ms.topic: conceptual
helpviewer_keywords:
- standard subscriptions [Reporting Services]
- subscriptions [Reporting Services], standard
ms.assetid: 5ab1c661-9bfa-434a-b315-faac34ed12b1
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 69cc078dc5ce605f1d7bf55d872c2a4629eb3301
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66403253"
---
# <a name="create-and-manage-subscriptions-for-native-mode-report-servers"></a>ネイティブ モード レポート サーバーのサブスクリプションの作成と管理
  標準のサブスクリプションは、電子メールまたは共有フォルダーを使用してレポートを配信する個々のユーザーによって作成されるサブスクリプションです。 このトピックでは、個別のユーザーが作成および管理する標準のサブスクリプションに関する情報を記載しています。 データ ドリブン サブスクリプションについては、必要条件および手順が異なるため、別のトピックで説明します。 詳細については、「 [データ ドリブン サブスクリプションを作成、変更、および削除する](../../reporting-services/subscriptions/create-modify-and-delete-data-driven-subscriptions.md)」を参照してください。  
  
 **この記事の内容:**  
  
-   [サブスクリプションの一般的な要件](#bkmk_create_subscription)  
  
-   [ファイル共有サブスクリプションを作成するには](#bkmk_create_fileshare_subscription)  
  
-   [電子メール サブスクリプションを作成するには](#bkmk_create_email_subscription)  
  
-   [サブスクリプションを変更するには](#bkmk_modify_subscription)  
  
-   [サブスクリプションを削除するには](#bkmk_delete_subscription)  
  
##  <a name="bkmk_create_subscription"></a> サブスクリプションの一般的な要件  
 この記事では、[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の Web ポータルを使って、ネイティブ モードのレポート サーバー上にサブスクリプションを作成する方法について説明します。 サブスクリプションを定義した後は、Web ポータルの [個人用サブスクリプション] ページか、特定のレポートの **[サブスクリプション]** タブを使用してそれにアクセスできます。  
  
 SharePoint モード レポート サーバーのレポートを、SharePoint サイトのアプリケーション ページを使用してサブスクライブする方法については、「[SharePoint モード レポート サーバーのサブスクリプションの作成と管理](../../reporting-services/subscriptions/create-and-manage-subscriptions-for-sharepoint-mode-report-servers.md) 」を参照してください。  
  
-   電子メール配信を使用する場合は、サブスクリプションを作成する前に、SMTP サーバーまたはゲートウェイ接続用にレポート サーバーを構成する必要があります。 詳細については、「 [Reporting Services の電子メール配信](../../reporting-services/subscriptions/e-mail-delivery-in-reporting-services.md)」を参照してください。  
  
-   ファイル共有配信を使用するには、あらかじめ対象フォルダーを定義しておく必要があります。 詳細については、「[サブスクリプション設定とファイル共有アカウント (構成マネージャー)](../install-windows/subscription-settings-and-a-file-share-account-configuration-manager.md)」をご覧ください。  
  
 レポートをサブスクライブするには、保存された資格情報を使用するか、資格情報を使用しないように、レポートのデータ ソースを構成しておく必要があります。 詳細については、「 [Reporting Services データ ソースに資格情報を保存する](../../reporting-services/report-data/store-credentials-in-a-reporting-services-data-source.md)」を参照してください。 そうでない場合は、 **[新しいサブスクリプション]** ボタンを使用できません。  
  
 この記事では、データ ドリブン サブスクリプションを作成する方法については説明しません。 データ ドリブン サブスクリプションを作成する方法については、「[データ ドリブン サブスクリプションの作成 &#40;SSRS チュートリアル&#41;](../../reporting-services/create-a-data-driven-subscription-ssrs-tutorial.md)」をご覧ください。  
  
###  <a name="bkmk_create_fileshare_subscription"></a> ファイル共有サブスクリプションを作成するには  
  
1. [レポート サーバーの Web ポータル (SSRS ネイティブ モード)](../../reporting-services/web-portal-ssrs-native-mode.md) に移動します。  
  
2.  目的のレポートに移動します。 レポートを右クリックして、 **[サブスクライブ]** を選択します。  
  
3.  **[説明]** : レポートのサブスクリプションの説明を入力します (512 文字まで)。  
  
4.  **[所有者]** : [所有者] フィールドには、既定で現在のユーザーが表示され、サブスクリプションの作成時には編集できません。 ただし、サブスクリプションの保存後に、所有者や説明など、サブスクリプションのプロパティは変更できます。  

5. **[サブスクリプションの種類]** の下の **[標準サブスクリプション]** ラジオ ボタンを選択します。

6. **[スケジュール]** セクションの下で、次のいずれかを選択します。  
   - **[共有スケジュール]** 。  
   - **[レポート固有のスケジュール]** 。  

    スケジュール設定の詳細については、「[スケジュール](../../reporting-services/subscriptions/schedules.md)」をご覧ください。
  
7. **[転送先]** の下で、 **[Windows ファイル共有]** を選択します。  
  
8. **[Delivery options (Windows File Share)]\(配信オプション (Windows ファイル共有)\)** の下で、以下を指定します。  
   - **[ファイル名]** : レポートのファイル名を入力します。
   - **[ファイルの作成時にファイルの拡張子を追加]** : このオプションを選択すると、ファイル名に 3 文字のファイル拡張子が追加されます。 ファイルの拡張子は、選択したレポート出力形式によって決まります。  
   - **[パス]** : レポートを配信する既存フォルダーの汎用名前付け規則 (UNC) パスを入力します (たとえば、\\<servername\>\<myreports>)。 パスの先頭には円記号 (\) を 2 つ含めます。 末尾には円記号を指定しないでください。  
  
     ![ファイル共有サブスクリプション](../../reporting-services/subscriptions/media/create-and-manage-subscriptions-for-native-mode-report-servers/subscription-file-share-delivery-option.png "ファイル共有サブスクリプション")  
  
   - **[表示形式]** : ファイル配信に使用するレポートの出力形式を選択します。 レポートを開くために使用するデスクトップ アプリケーションに対応する形式を選択します。 単一のストリームでレポートを表示しない形式、または静的ファイルでサポートできない対話機能が導入された形式 (HTML 4.0 など) は選択しないでください。  
  
   - **[資格情報]** : ファイル共有アカウントまたは特定の Windows ユーザーの資格情報を選択します。 レポート管理者がファイル共有アカウントを構成していない場合、 **[ファイル共有アカウントを使用する]** は無効です。 詳細については、「[サブスクリプション設定とファイル共有アカウント (構成マネージャー)](../../reporting-services/install-windows/subscription-settings-and-a-file-share-account-configuration-manager.md)」を参照してください。 **[ユーザー名]** および **[パスワード]** テキスト ボックスに、ファイル共有のアクセスに必要な資格情報を、ユーザー名に対応する *\<domain>* \\ *\<user name>* の形式で指定します。  
  
   - **[上書きのオプション]** :  
     - **[既存のファイルを新しいバージョンで上書きする]** 。  
     - **[以前のバージョンがある場合はファイルを上書きしない]** : オンにすると、既存のファイルが検出された場合に配信されません。  
     - **[自動増分のファイル名を新しいバージョンとして追加します]** : レポート サーバーによってファイル名に番号が付加され、同じ名前の既存のファイルとそのファイルが区別されます。  

9. パラメーター化されたレポートの場合は、このサブスクリプションのレポートで使用するパラメーターを指定します。 要求時または他のスケジュールされた操作でレポートを実行するときに使用されるパラメーターとは別のパラメーターにすることができます。  
  
レポートが静的ファイルとして配信されます。 レポートに対話機能 (たとえば、追加の行と列へのリンク) を含める場合でも、これらの機能は使用できません。  
  
###  <a name="bkmk_create_email_subscription"></a> 電子メール サブスクリプションを作成するには  
  
1. [レポート サーバーの Web ポータル (SSRS ネイティブ モード)](../../reporting-services/web-portal-ssrs-native-mode.md) に移動します。  
  
2. 目的のレポートに移動します。 レポートを右クリックして、 **[サブスクライブ]** を選択します。  
  
3. **[説明]** : レポートのサブスクリプションの説明を入力します (512 文字まで)。  
  
4.  **[所有者]** : [所有者] フィールドには、既定で現在のユーザーが表示され、サブスクリプションの作成時には編集できません。 ただし、サブスクリプションの保存後に、所有者や説明など、サブスクリプションのプロパティは変更できます。  

5. **[サブスクリプションの種類]** の下の **[標準サブスクリプション]** ラジオ ボタンを選択します。

6. **[スケジュール]** セクションの下で、次のいずれかを選択します。  
   - **[共有スケジュール]** 。  
   - **[レポート固有のスケジュール]** 。  

    スケジュール設定の詳細については、「[スケジュール](../../reporting-services/subscriptions/schedules.md)」をご覧ください。
  
7. **[転送先]** の下で、 **[電子メール]** を選択します。  **[電子メール]** オプションを選択できない場合、レポート サーバーが電子メール サブスクリプション用に構成されていません。 「[Reporting Services サービス アプリケーションの電子メールの構成](../../reporting-services/install-windows/configure-e-mail-for-a-reporting-services-service-application.md)」をご覧ください。
  
8. **[Delivery options (E-Mail)]\(配信オプション (電子メール)\)** の下で、以下を指定します。
   - **[宛先]** : [宛先] フィールドの受信者名は、ドメイン ユーザー アカウントを使用して自動的に指定されます。 [ユーザー名]@[domain.com] の形式になっていることを確認します。 **[宛先]** フィールドがご自分のユーザー アカウントで自動的に指定されるかどうかは、レポート サーバーの構成設定によって決まります。 構成設定の電子メール アドレスの変更について詳しくは、「[Reporting Services サービス アプリケーションの電子メールの構成](../../reporting-services/install-windows/configure-e-mail-for-a-reporting-services-service-application.md)」をご覧ください。

     >[!NOTE]  
     > 権限によっては、レポートの配信先の電子メール アドレスを入力できます。 電子メール アドレスを複数指定するには、セミコロン (;) で区切ります。 **[CC]** 、 **[BCC]** 、および **[返信先]** テキスト ボックスに、追加の電子メール アドレスを入力することもできます。 このためには、すべてのサブスクリプションを管理する権限が必要です。  
  
   - **[件名]** : 既定値は "@ExecutionTime に @ReportName が実行されました" です。 件名は編集できますが、@ReportName と @ExecutionTime は **[件名]** フィールドでサポートされている唯一のグローバル変数です。  
  
     ![電子メール サブスクリプション](../../reporting-services/subscriptions/media/create-and-manage-subscriptions-for-native-mode-report-servers/subscription-e-mail-delivery-option.png "電子メール サブスクリプション")  

   - **[レポートを含める]** : レポートのコピーを埋め込む、または添付する場合に選択します。 レポートの形式は、選択した表示形式によって決まります。 レポートのサイズが電子メール システムに定義された制限を超えると予想される場合は、このオプションを使用しないでください。  
  
   - **[リンクを含める]** : 電子メール メッセージの本文にレポートの URL リンクを含める場合は、このオプションを選択します。  
  
     >[!NOTE]  
     >これらのオプションのいずれも選択しない場合、件名行の通知テキストのみが送信されます。  
  
   - **[表示形式]** リスト ボックスから表示形式を選択します。 このオプションは、 **[レポートを含める]** を選択してレポートのコピーを埋め込むか添付する場合に使用できます。  
      - 電子メール メッセージの本文にレポートを埋め込むには、 **[MHTML (Web アーカイブ)]** を選択します。  
      - レポートを添付ファイルとして送信するには、他の表示形式を選択します。  
  
   - **[優先度]** リスト ボックスから優先度を選択します。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Exchange では、電子メール メッセージの重要度レベルを表すフラグをここで設定します。  
   - 必要な場合は **[コメント]** を入力します。
  
9. パラメーター化されたレポートの場合は、このサブスクリプションのレポートで使用するパラメーターを指定します。 要求時または他のスケジュールされた操作でレポートを実行するときに使用されるパラメーターとは別のパラメーターを指定できます。  
  
##  <a name="bkmk_modify_subscription"></a> サブスクリプションを変更するには  
 サブスクリプションは、いつでも変更できます。 サブスクリプションを処理中に変更する場合、配信拡張機能がサブスクリプション データを受け取る前に、更新された設定をレポート サーバーに保存すると、その設定が使用されます。 それ以外の場合は、既存の設定が使用されます。  
  
 サブスクリプションを作成するユーザーが、そのサブスクリプションを所有します。 各ユーザーは、自分が所有するサブスクリプションを変更または削除できます。 サブスクリプションのプロパティ ページからレポートの所有者を変更するか、所有者をプログラムで変更することができます。 詳細については、以下を参照してください。  
  
-   [Use PowerShell to Change and List Reporting Services Subscription Owners and Run a Subscription](../../reporting-services/subscriptions/manage-subscription-owners-and-run-subscription-powershell.md)  
  
-   <xref:ReportService2010.ReportingService2010.ChangeSubscriptionOwner%2A>  
  
 サブスクリプションを検索するには、 **[個人用サブスクリプション]** ページを使用するか、レポートに関連したサブスクリプション定義を表示します。 サブスクリプションを直接検索することはできません。また、所有者名、トリガー情報、状態情報を基にサブスクリプションを検索することもできません。  
  
 レポート サーバー管理者もサブスクリプションを変更または削除することができます。  
  
>[!NOTE]  
> レポート サーバー管理者は、特定のレポート サーバーで使用されている個別のサブスクリプションすべてを 1 か所から管理することはできません。 ただし、個別のサブスクリプションそれぞれにアクセスして、変更または削除することができます。  
  
##  <a name="bkmk_delete_subscription"></a> サブスクリプションを削除するには  
サブスクリプションを削除するには:  
  
1. [レポート サーバーの Web ポータル (SSRS ネイティブ モード)](../../reporting-services/web-portal-ssrs-native-mode.md) に移動します。  
  
2. Web ポータルで、ツール バーの **[個人用サブスクリプション]** を選択し、変更または削除するサブスクリプションに移動します。  
  
3. レポートを右クリックして、 **[削除]** を選択します。  
  
レポート サーバーで現在処理中のサブスクリプションを取り消す場合は、「 [実行中の処理を管理する](../../reporting-services/subscriptions/manage-a-running-process.md)」を参照してください。  
  
 サブスクリプションを終了するときに、そのサブスクリプションを検索できない場合は、受信中のレポートをメモして、名前を使用して検索します。 レポートにアクセスすると、サブスクリプションから自分を削除できます。 サブスクリプションを検索できない場合は、サブスクリプションがデータ ドリブン サブスクリプションである可能性があります。 詳細については、レポート サーバー管理者に問い合わせてください。  
  
 基になるレポートを削除すると、サブスクリプションは自動的に削除されます。 サブスクリプションを処理中に削除する場合、配信拡張機能がサブスクリプション データを受け取る前に削除操作を行うと、サブスクリプションは停止します。 それ以外の場合は、サブスクリプションの処理を続行します。  
  
## <a name="see-also"></a>参照  
 [SharePoint モード レポート サーバーのサブスクリプションの作成と管理](../../reporting-services/subscriptions/create-and-manage-subscriptions-for-sharepoint-mode-report-servers.md)  
 [Use PowerShell to Change and List Reporting Services Subscription Owners and Run a Subscription](../../reporting-services/subscriptions/manage-subscription-owners-and-run-subscription-powershell.md)  
 [データ ドリブン サブスクリプション](../../reporting-services/subscriptions/data-driven-subscriptions.md)  
 [サブスクリプションと配信 &#40;Reporting Services&#41;](../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)  
 [レポート サーバーの Web ポータル (SSRS ネイティブ モード)](../../reporting-services/web-portal-ssrs-native-mode.md)  
 [個人用サブスクリプションを使用する (ネイティブ モードのレポート サーバー)](../../reporting-services/subscriptions/use-my-subscriptions-native-mode-report-server.md)  
  