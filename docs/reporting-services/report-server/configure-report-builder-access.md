---
title: レポート ビルダーへのアクセスの構成 | Microsoft Docs
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
ms.date: 06/06/2019
ms.openlocfilehash: 724fac17abf7f5da45101a6ff22d3185a7ade93b
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68255174"
---
# <a name="configure-report-builder-access"></a>レポート ビルダーへのアクセスの構成
レポート ビルダーは、ネイティブ モードまたは SharePoint 統合モード用に構成される [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] レポート サーバーに付属しているカスタム レポート ツールです。  

レポート ビルダーへのアクセスは、次の要素により決定されます。  

- レポート サーバーでレポート ビルダーを使用できるかどうかを指定するサーバー プロパティ。  

- 個々のユーザーやグループがレポート ビルダーを使用できるようにするためのロール割り当てまたは権限。  

- ユーザーの資格情報をレポート サーバーに渡せるか、アプリケーション ファイルで匿名アクセスを構成するかを指定する認証設定。

## <a name="prerequisites"></a>Prerequisites

レポート ビルダーは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のすべてのエディションで使用できるわけではありません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の各エディションでサポートされる機能の一覧については、「[SQL Server 2017 の各エディションとサポートされている機能](../../sql-server/editions-and-components-of-sql-server-2017.md)」をご覧ください。  

クライアントコンピューターには、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SSRS 2016 と2017用に4.6 または4.6.1 がインストールされている必要があります。 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] は、 [!INCLUDE[ndptecclick](../../includes/ndptecclick-md.md)] アプリケーションを実行するためのインフラストラクチャを提供します。  

Internet Explorer 11 [!INCLUDE[msCoName](../../includes/msconame-md.md)]以降、または他の最新のブラウザーを使用する必要があります。  

レポート ビルダーは、常に完全信頼モードで実行されます。部分信頼モードで実行されるように構成することはできません。 以前のリリースでは、レポート ビルダーを部分信頼モードで実行できましたが、 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降のバージョンではこのオプションはサポートされていません。  

## <a name="enabling-and-disabling-report-builder"></a>レポート ビルダーの有効化と無効化  

レポート ビルダーは既定で有効になっています。 レポート サーバー管理者は、レポート サーバーのシステム プロパティ **ShowDownloadMenu** を **false** に設定することで、レポート ビルダー機能を無効にすることができます。 このプロパティを設定すると、そのレポートサーバーのレポートビルダー、Mobile Report Publisher、および Power BI Mobile のダウンロードが無効になります。  

 レポート サーバーのシステム プロパティを設定するには、Management Studio またはスクリプトを使用します。   

 - Management Studio を使用するには、レポート サーバーに接続し、[詳細なサーバー プロパティ] ページを使用して **ShowDownloadMenu** を **false** に設定します。 このページを開く方法の詳細については、「[レポート サーバーのプロパティを設定する &#40;Management Studio&#41;](../../reporting-services/tools/set-report-server-properties-management-studio.md)」を参照してください。      

 - レポート サーバーのプロパティを設定するサンプル スクリプトを表示する方法は、「 [Script Deployment and Administrative Tasks](../../reporting-services/tools/script-deployment-and-administrative-tasks.md)」(配置タスクおよび管理タスクのスクリプト作成) を参照してください。  

## <a name="role-assignments-granting-report-builder-access-on-a-native-mode-report-server"></a>ネイティブ モードのレポート サーバーにおけるレポート ビルダーへのアクセスを許可するロールの割り当て  

ネイティブ モードのレポート サーバーでは、レポート ビルダーを使用するためのタスクを含むユーザー ロールの割り当てを作成します。 アイテムおよびサイト レベルでのロールの定義およびロールの割り当てを作成または変更できるのは、コンテンツ マネージャーとシステム管理者だけです。  

次に示す手順では、定義済みロールを使用しているものとします。 ロールの定義を変更した場合や SQL Server 2000 からアップグレードした場合は、ロールに必要なタスクが含まれていることを確認してください。 ロール割り当ての作成について詳しくは、「[レポート サーバーへのユーザー アクセスを許可する](../../reporting-services/security/grant-user-access-to-a-report-server.md)」をご覧ください。

ロールの割り当てを作成すると、次の操作を行う権限がユーザーに許可されます。  

- システム ユーザー ロールおよび閲覧者ロールに割り当てられたユーザーは、レポート ビルダーを起動せずに、レポート サーバーでパブリッシュされたレポート ビルダーのレポートを表示できます。  

- システム ユーザー ロールおよびレポート ビルダー ロールに割り当てられたユーザーは、モデルを生成したり、レポート ビルダーを起動してレポートを作成したり、レポートをレポート サーバーに保存したりすることができます。  

- システム ユーザー ロールおよびパブリッシャー ロールに割り当てられたユーザーは、モデル デザイナーからレポート サーバーにモデルをパブリッシュできます。 モデルは、レポート ビルダーではデータ ソースとして使用されます。  

- システム管理者ロールおよびコンテンツ マネージャー ロールに割り当てられたユーザーは、レポート ビルダーのレポートを作成、表示、および管理するための完全な権限を持ちます。  

### <a name="to-verify-required-tasks-are-in-the-role-definitions"></a>必要なタスクがロールの定義に含まれていることを確認するには  

1. Management Studio を開いてレポート サーバーに接続します。  

2. **[セキュリティ]** フォルダーを開きます。  

3. **[システム ロール]** フォルダーを開きます。  

4. **[システム管理者]** を右クリックし、 **[プロパティ]** をクリックします。  

5. **[レポート定義の実行]** を選択し、 **[OK]** をクリックします。  

6. **[システム ユーザー]** を右クリックし、 **[プロパティ]** をクリックします。  

7. **[レポート定義の実行]** を選択し、 **[OK]** をクリックします。  

8. **[ロール]** フォルダーを開きます。  

9. **[ブラウザー]** を右クリックし、 **[プロパティ]** をクリックします。  

10. **[モデルの表示]** を選択し、 **[OK]** をクリックします。  

11. **[コンテンツ マネージャー]** を右クリックし、 **[プロパティ]** をクリックします。  

12. **[モデルの表示]** 、 **[モデルの管理]** 、および **[レポートの使用]** を選択し、 **[OK]** をクリックします。  

13. **[パブリッシャー]** を右クリックし、 **[プロパティ]** をクリックします。  

14. **[モデルの管理]** を選択し、 **[OK]** をクリックします。  

15. レポート ビルダー ロールが存在しない場合は作成します。  

    1. **[セキュリティ]** フォルダーを開きます。  

    2. **[ロール]** を右クリックし、 **[新しいロール]** をクリックします。  

    3. [名前] に「 **レポート ビルダー**」と入力します。  

    4. [説明] に、Web ポータルのユーザーがロールの目的を把握できるようにするためのロールの説明を入力します。  

    5. **[レポートの使用]** 、 **[レポートの表示]** 、 **[モデルの表示]** 、 **[リソースの表示]** 、 **[フォルダーの表示]** 、 **[個別のサブスクリプションを管理]** の各タスクを追加します。  

    6. **[OK]** をクリックして、ロールを保存します。  

#### <a name="to-create-role-assignments-that-grant-access-to-report-builder"></a>レポート ビルダーへのアクセスを許可するロールの割り当てを作成するには  

1. Web ポータルを起動します。  

2. Web ポータルのホームページの右上にある歯車アイコンをクリックし、ドロップダウンメニューから **[サイトの設定]** を選択します。  
![web ポータルの歯車アイコンとメニュー](../../reporting-services/report-builder/media/configure-report-builder-access/ssrswebportal-site-settings-gear-icon-and-menu.png)

3. **[セキュリティ]** をクリックします。  

4. レポート ビルダーへのアクセスを構成するユーザーまたはグループのロールの割り当てが既に存在する場合は、 **[編集]** をクリックします。  
存在しない場合は、 **[新しいロールの割り当て]** をクリックします。 [グループまたはユーザー] で、Windows ドメインのユーザー アカウントまたはグループ アカウントを \<ドメイン>\\<アカウント\> の形式で入力します。 フォーム認証やカスタム セキュリティを使用している場合は、その環境に合った適切な形式でユーザー アカウントまたはグループ アカウントを指定します。  

5. **[システム ユーザー]** を選択し、 **[OK]** をクリックします。  

6. **[ホーム]** をクリックします。  

7. **[フォルダー設定]** タブをクリックします。  

8. **[セキュリティ]** タブをクリックします。  

9. レポート ビルダーへのアクセスを構成するユーザーまたはグループのロールの割り当てが既に存在する場合は、 **[編集]** をクリックします。  

    存在しない場合は、 **[新しいロールの割り当て]** をクリックします。 [グループまたはユーザー] で、Windows ドメインのユーザー アカウントまたはグループ アカウントを \<ドメイン>\\<アカウント\> の形式で入力します。 フォーム認証やカスタム セキュリティを使用している場合は、その環境に合った適切な形式でユーザー アカウントまたはグループ アカウントを指定します。  

10. **[レポート ビルダー]** を選択し、 **[適用]** をクリックします。  

11. ロールの割り当てを作成または変更するユーザーまたはグループが他にもある場合は、以上の手順を繰り返します。  

## <a name="permissions-granting-report-builder-access-on-a-sharepoint-integrated-mode-report-server"></a>SharePoint 統合モードのレポート サーバーにおけるレポート ビルダーへのアクセスを許可する権限  

SharePoint 統合モードのレポート サーバーでは、レポート ビルダーへのアクセスは、投稿またはフル コントロールの権限レベルの SharePoint ユーザーに許可されます。  

カスタム権限レベルを使用する場合は、権限レベルにアイテムの追加とアイテムの編集を含める必要があります。 組み込みアクセス許可レベルでのレポート ビルダーへのアクセスの詳細については、「 [Use Built-in Security in Windows SharePoint Services for Report Server Items](../../reporting-services/security/use-built-in-security-in-windows-sharepoint-services-for-report-server-items.md)」(レポート サーバー アイテムに対して Windows SharePoint Services の組み込みのセキュリティを使用する) を参照してください。 カスタム アクセス許可レベルのアクセス許可要件の詳細については、「 [Set Permissions for Report Server Operations in a SharePoint Web Application](../../reporting-services/security/set-permissions-for-report-server-operations-in-a-sharepoint-web-application.md)」(SharePoint Web アプリケーションのレポート サーバー操作に対する権限を設定する) を参照してください。  

## <a name="authentication-considerations-and-credential-reuse"></a>認証に関する注意点と資格情報の再利用  

- レポート ビルダーは、レポート サーバーに対する専用の接続を確立します。 シングル サインオンを有効にした Windows 統合セキュリティを使用していない場合、ユーザーは、レポート ビルダーからレポート サーバーに接続するために資格情報を再入力する必要があります。  

次の表に、レポート サーバーでサポートされている認証の種類、およびレポート ビルダーへのアクセスに追加の構成が必要かどうかを示します。  

## <a name="see-also"></a>参照  

- [レポート サーバーでの認証](../../reporting-services/security/authentication-with-the-report-server.md)
- [Reporting Services と Power View のブラウザー サポート](../../reporting-services/browser-support-for-reporting-services-and-power-view.md)
- [レポート ビルダーの起動](../../reporting-services/report-builder/start-report-builder.md)
- [レポート サーバーの Web ポータル (SSRS ネイティブ モード)](../web-portal-ssrs-native-mode.md)
- [Management Studio でレポート サーバーに接続する](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)
- [レポート サーバーのシステム プロパティ](../../reporting-services/report-server-web-service/net-framework/reporting-services-properties-report-server-system-properties.md)
