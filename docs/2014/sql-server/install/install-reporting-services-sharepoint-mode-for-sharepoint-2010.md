---
title: SharePoint 2010 用の SharePoint モードのインストール Reporting Services |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 47efa72e-1735-4387-8485-f8994fb08c8c
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 758c76bf243af66157aa06f761df010a1e086a91
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/23/2019
ms.locfileid: "72798349"
---
# <a name="install-reporting-services-sharepoint-mode-for-sharepoint-2010"></a>SharePoint 2010 用 Reporting Services の SharePoint モードのインストール
  このトピックでは、SharePoint モードでの Reporting Services レポート サーバーのシングル サーバー インストールの手順について説明します。 手順には、SQL Server インストール ウィザードの実行と、SharePoint 2010 サーバーの全体管理を使用する追加構成タスクが含まれます。 また、既存のインストールについての個々の手順 ([!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サービス アプリケーションの作成など) をこのトピックで確認することもできます。 既存のファームに [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サーバーを追加する方法については、「追加の[レポートサーバーを&#40;ファームに追加する&#41; SSRS スケールアウト](../../reporting-services/install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md)」と「[ファームに追加の Reporting Services Web フロントエンドを追加](../../reporting-services/install-windows/add-an-additional-reporting-services-web-front-end-to-a-farm.md)する」を参照してください。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  SharePoint 2010|  
  
 シングルサーバーインストールは、開発およびテストのシナリオには便利ですが、運用環境では推奨されません。  
  
> [!NOTE]  
>  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]への SharePoint モードのアップグレードと既存の [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のインストールの詳細については、「 [Reporting Services のアップグレードと移行](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)」を参照してください。  
  

  
##  <a name="bkmk_prereq"></a> の前提条件  
  
-   > [!IMPORTANT]  
    >  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint モードを構成および管理するために、[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成マネージャーを使用するまたはサポートする必要はなくなりました。 SharePoint モードでレポート サーバーを構成するには、SharePoint サーバーの全体管理を使用します。 詳細については、「 [Reporting Services SharePoint サービスアプリケーションの管理](../../../2014/reporting-services/manage-a-reporting-services-sharepoint-service-application.md)」を参照してください。  
  
-   SharePoint 2010 製品を含む要件については、次のトピックを参照してください。  
  
    -   [オンラインリリースノート](https://msdn.microsoft.com/library/dn169381.aspx)
  
    -   [SharePoint 2010 ファームで SQL Server BI 機能を使用するためのガイド](../../../2014/sql-server/install/guidance-for-using-sql-server-bi-features-in-a-sharepoint-2010-farm.md)  
  
-   このトピックでは、SharePoint 2010 製品のインストールについては説明しません。 詳細については、「 [SharePoint 2010 ファームで SQL SERVER BI 機能を使用するためのガイダンス](../../../2014/sql-server/install/guidance-for-using-sql-server-bi-features-in-a-sharepoint-2010-farm.md)」を参照してください。  
  
-   ここで説明する手順は、[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] レポート サーバーを構成するためのものであり、以前のバージョンのレポート サーバーには使用できません。 以前のバージョンのレポート サーバーでは、SharePoint 共有サービス アーキテクチャが使用されていませんでした。 たとえば、SQL Server 2008 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] レポート サーバーや、SQL Server 2008 R2 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] レポート サーバーなどです。  
  
-   Windows サーバーマネージャーで**SharePoint 2010 管理**サービスが開始されていることを確認します。  
  
 ![1台のサーバーにインストールされる SSRS コンポーネント](../../../2014/sql-server/install/media/rs-deployment-1-server.gif "1台のサーバーにインストールされる SSRS コンポーネント")  
  
### <a name="database-considerations-for-a-single-server-configuration"></a>単一のサーバー構成に関するデータベースの注意事項  
  
-   Reporting Services および SharePoint 製品とテクノロジはどちらも、SQL Server のリレーショナル データベースを使用して、アプリケーション データを格納します。  
  
-   [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] には、SQL エンジンの互換性のある SQL Server 評価版インスタンスが必要です。  
  
-   SharePoint 製品では、既存のデータベース インスタンスを使用できます。 データベースエンジンのインスタンスがインストールされていない場合は、sharepoint 製品のセットアッププログラムによって、SharePoint アプリケーションデータベースの SQL Server Express エディションがインストールされます。  
  
-   レポート サーバー インスタンスの場合、データベースに SQL Server Express Edition を使用することはできません。 ただし、SharePoint 製品によってインストールされる SQL Server Express Edition インスタンスは、他のデータベース エンジン エディションと共存できます。  
  

  
##  <a name="bkmk_install_SSRS"></a>SharePoint モードで Reporting Services レポートサーバーをインストールする  
  
1.  SQL Server インストール ウィザードを実行します。  
  
2.  ウィザードの左側の **[インストール]** をクリックし、 **[SQL Server の新規スタンドアロン インストールを実行するか、既存のインストールに機能を追加します]** をクリックします。  
  
3.  **[セットアップ サポート ルール]** ページで、すべてのルールに合格したら、 **[OK]** をクリックします。  
  
4.  **[セットアップ サポート ファイル]** ページで、 **[インストール]** をクリックします。  
  
5.  サポートファイルのインストールが完了し、サポートルールの状態が **[成功]** と表示されたら、 **[次へ]** をクリックします。 警告やインストールの障害となる問題を確認します。  
  
6.  **[プロダクトキー]** ページで、キーを入力するか、"Enterprise 評価版" エディションの既定値をそのまま使用します。  
  
     **[次へ]** をクリックします。  
  
7.  使用許諾条件を確認して同意します。 マイクロソフトでは、機能使用状況に関するデータを送信することに同意して、製品の機能やサポートの改善にご協力いただき感謝しております。  
  
     **[次へ]** をクリックします。  
  
8.  **[セットアップロール]** ページで、 **[SQL Server 機能のインストール]** を選択します。  
  
     **[次へ]** をクリックします。  
  
     ![セットアップロールの SQL Server 機能のインストール](../../../2014/sql-server/install/media/rs-setuprole.gif "セットアップロールの SQL Server 機能のインストール")  
  
9. **[機能の選択]** ページで、次のオプションを選択します。  
  
    -   **Reporting Services - SharePoint**  
  
    -   **SharePoint 2010 製品用の Reporting Services アドイン**。 ![メモ](../../../2014/reporting-services/media/rs-fyinote.png "n注")アドインをインストールするためのインストールウィザードオプションは、[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] リリースで新しく追加されました。  
  
    -   SQL Server [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスがまだインストールされていない場合は、 **[データベース エンジン サービス]** および **[管理ツール - 完全]** をクリックして完全な環境をインストールすることもできます。  
  
     **[次へ]** をクリックします。  
  
     ![SharePoint モードの SSRS 機能の選択](../../../2014/sql-server/install/media/rs-setupfeatureselection-sharepoint-with-circles.gif "SharePoint モードの SSRS 機能の選択")  
  
10. **[インストールルール]** ページで **[次へ]** をクリックします。 警告やインストールの障害となる問題を確認します。  
  
11. データベース エンジン サービスを選択した場合は、 **[インスタンスの構成]** ページで **MSSQLSERVER** の既定のインスタンスを受け入れて、 **[次へ]** をクリックします。 Reporting Services 共有サービス アーキテクチャは、以前の Reporting Services アーキテクチャとは異なり、SQL Server "インスタンス" に基づいていません。  
  
12. **[必要なディスク領域]** ページを確認し、 **[次へ]** をクリックします。  
  
13. **[サーバーの構成]** ページで、適切な資格情報を入力します。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のデータ警告機能またはサブスクリプション機能を使用する場合は、SQL Server エージェントの **[スタートアップの種類]** を **[自動]** に変更する必要があります。  
  
     **[次へ]** をクリックします。  
  
14. データベース エンジン サービスを選択した場合は、 **[データベース エンジンの構成]** ページが表示されるので、SQL 管理者の一覧に適切なアカウントを追加して、 **[次へ]** をクリックします。  
  
15. **[Reporting Services の構成]** ページで、 **[インストールのみ]** オプションをクリックします。 このオプションを選択すると、レポートサーバーファイルがインストールされますが、[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]の SharePoint 環境は構成されません。SQL Server のインストールが完了したら、このトピックの他のセクションに従って SharePoint 環境を構成します。 これには、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 共有サービスのインストールと、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サービス アプリケーションの作成が含まれます。  
  
     ![rs_SQL11_SETUP_SSRS_configpage_withcircles](../../../2014/sql-server/install/media/rs-kj-setup-ssrs-configpage-withcircles.gif "rs_SQL11_SETUP_SSRS_configpage_withcircles")  
  
16. **[エラー レポート]** ページでエラー レポートを送信するためのチェック ボックスをオンにすると、マイクロソフトが SQL Server の機能とサービスを改善するのに役立ちます。  
  
     **[次へ]** をクリックします。  
  
17. **[インストール構成ルール]** ページで警告を確認して、 **[次へ]** をクリックします。  
  
18. **[インストールの準備完了]** ページで、インストールの概要を確認して **[次へ]** をクリックします。 この概要には、 **Sharepointfilesonlymode**のインストールモードの値とアカウント情報を含む**Reporting Services**ノードが含まれます。  
  

  
##  <a name="bkmk_install_SSRS_sharedservice"></a>Reporting Services SharePoint サービスをインストールして起動する  
 ![PowerShell 関連コンテンツ](../../../2014/reporting-services/media/rs-powershellicon.jpg "PowerShell 関連コンテンツ")  
  
> [!NOTE]  
>  を既存の SharePoint ファームにインストールする場合は、このセクションの手順を実行**する必要はありません**。 前のセクションで SQL Server インストールウィザードを実行したときに、[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint サービスがインストールされ、開始されました。  
  
 必要なファイルは SQL Server インストール ウィザードの中でインストールされていますが、サービスを SharePoint ファームに登録する必要があります。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] リリースでは、SharePoint モードの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] に対する PowerShell が新たにサポートされました。 以下では、SharePoint 管理シェルを開いてコマンドレットを実行する手順を説明します。  
  
1.  **[スタート]** ボタンをクリックします。  
  
2.  **[Microsoft SharePoint 2010 製品]** グループをクリックします。  
  
3.  **[SharePoint 2010 管理シェル]** を右クリックし、 **[管理者として実行]** をクリックします。  
  
4.  次の PowerShell コマンドを実行して、SharePoint サービスをインストールします。 コマンドが正常に完了すると、管理シェルの表示が改行されます。 コマンドが正常に完了しても、管理シェルにメッセージは表示されません。  
  
    ```powershell
    Install-SPRSService  
    ```  
  
5.  次の PowerShell コマンドを実行して、サービスプロキシをインストールします。  
  
    ```powershell
    Install-SPRSServiceProxy  
    ```  
  
6.  次の PowerShell コマンドを実行してサービスを開始します。または、SharePoint サーバーの全体管理からサービスを開始する手順については、次のメモを参照してください。  
  
    ```powershell
    Get-SPServiceInstance -All | Where {$_.TypeName -like "SQL Server Reporting*"} | Start-SPServiceInstance  
    ```  
  
 3 番目の PowerShell コマンドを実行する代わりに、SharePoint サーバーの全体管理からサービスを開始することもできます。 次の手順を使用すると、サービスが実行していることを確認することもできます。  
  
1.  SharePoint サーバーの全体管理で、 **[システム設定]** の **[サーバーのサービスの管理]** をクリックします。  
  
2.  **[SQL Server Reporting Services サービス]** を探して、[アクション] 列の **[開始]** をクリックします。  
  
3.  Reporting Services サービスのステータスが **[停止]** から **[開始]** に変わります。 Reporting Services サービスが一覧にない場合は、PowerShell を使用してサービスをインストールします。  
  
    > [!NOTE]  
    >  Reporting Services サービスが **[開始]** 中 ステータスのままで、 **[開始]** に変わらない場合は、Windows サーバーマネージャーで "SharePoint 2010 Administration" サービスが開始されていることを確認します。  

##  <a name="bkmk_create_serrviceapplication"></a>Reporting Services サービスアプリケーションを作成する  
 ここでは、既存のサービス アプリケーションを確認している場合に、サービス アプリケーションおよびプロパティの説明を作成する手順について説明します。  
  
1.  SharePoint サーバーの全体管理で、 **[アプリケーション構成の管理]** の **[サービス アプリケーションの管理]** をクリックします。  
  
2.  SharePoint リボンで、 **[新規作成]** ボタンをクリックします。  
  
3.  [新規作成] メニューで、 **[SQL Server Reporting Services サービス アプリケーション]** をクリックします。  
  
    > [!WARNING]  
    >  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] オプションが一覧に表示されない場合は、 **[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 共有サービスがインストールされていない**ことを示しています。 前のセクションの、PowerShell コマンドレットを使用して [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サービスをインストールする方法を確認してください。  
  
4.  **[SQL Server Reporting Services サービス アプリケーションの作成]** ページで、アプリケーションの名前を入力します。 複数の Reporting Services サービスアプリケーションを作成する場合は、わかりやすい名前または名前付け規則を使用して、管理操作と管理操作を整理することができます。  
  
5.  **[アプリケーション プール]** セクションで、このアプリケーションのための新しいアプリケーション プールを作成します (推奨)。 新しいアプリケーションプールにサービスアプリケーションと同じ名前を使用すると、継続的な管理が容易になります。  
  
     そのアプリケーション プールの管理アカウントを選択または作成します。 必ずドメイン ユーザー アカウントを指定してください。 ドメイン ユーザー アカウントにより、パスワードやアカウント情報をまとめて更新できる SharePoint の管理アカウント機能を使用できるようになります。 ドメイン アカウントは、配置をスケールアウトして、同じ ID で実行されるサービス インスタンスを追加する場合にも必要です。  
  
6.  **[データベース サーバー]** で、現在のサーバーを使用するか、または別の SQL Server を選択することができます。  
  
7.  **[データベース名]** の既定値は " `ReportingService_<guid>`" で、これは一意のデータベース名です。 新しい値を入力する場合は、一意の値を入力します。  
  
8.  **[データベース認証]** の既定値は、"Windows 認証" です。 **[SQL 認証]** を選択する場合は、SharePoint 管理者ガイドを参照して、SharePoint 配置でその認証の種類を使用するためのベスト プラクティスを確認してください。  
  
9. **[Web アプリケーションの関連付け]** セクションで、現在の Reporting Services サービス アプリケーションによるアクセス用に準備する Web アプリケーションを選択します。 1 つの Reporting Services サービス アプリケーションを 1 つの Web アプリケーションに関連付けることができます。 現在のすべての Web アプリケーションが既に Reporting Services サービス アプリケーションと関連付けられている場合は、警告メッセージが表示されます。  
  
10. クリックして **OK**です。  
  
11. サービス アプリケーションの作成処理には数分かかることがあります。 完了すると、確認メッセージと、 **[サブスクリプションと警告の準備]** ページへのリンクが表示されます。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のサブスクリプション機能と警告機能を使用する場合は、準備手順を行います。 詳細については、「[SSRS サービス アプリケーションを使用するためのサブスクリプションと警告の準備](../../reporting-services/install-windows/provision-subscriptions-and-alerts-for-ssrs-service-applications.md)」を参照してください。  
  
 ![PowerShell 関連コンテンツ](../../../2014/reporting-services/media/rs-powershellicon.jpg "PowerShell 関連コンテンツ")PowerShell を使用して [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サービスアプリケーションを作成する方法の詳細については、「 [powershell を使用して Reporting Services サービスアプリケーションを作成するに](../../../2014/reporting-services/reporting-services-sharepoint-service-and-service-applications.md#bkmk_powershell_create_ssrs_serviceapp)は」を参照してください。  
  

  
##  <a name="bkmk_powerview"></a>Power View サイトコレクション機能をアクティブにします。  
 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]は、[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[SPS2010](../../includes/sps2010-md.md)] Enterprise Edition 用の [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] アドインの機能であり、サイトコレクション機能です。 この機能は、ルート サイト コレクションと、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] アドインのインストール後に作成されたサイト コレクションで自動的にアクティブ化されます。 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]を使用する場合は、この機能がアクティブ化されていることを確認してください。  
  
 SharePoint 2010 製品のインストール後に SharePoint 2010 製品用の [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] アドインをインストールした場合、レポート サーバーの統合機能と Power View の統合機能はルート サイト コレクションでのみアクティブ化されます。 他のサイト コレクションについては、この機能を手動でアクティブ化します。  
  
#### <a name="to-activate-the-power-view-feature"></a>Power View 機能をアクティブ化するには  
  
1.  ブラウザーで目的の SharePoint サイトを開きます。  
  
2.  **[サイトの操作]** をクリックします。  
  
3.  **[サイトの設定]** をクリックします。  
  
4.  [サイト コレクションの管理] グループで **[サイト コレクションの機能]** をクリックします。  
  
5.  一覧で **[Power View 統合機能]** を探します。  
  
6.  **[アクティブ化]** をクリックします。  
  
 この手順は、サイト コレクションごとに実行します。 詳細については、「[レポートサーバーのアクティブ化」および「SharePoint の Power View 統合機能](../../reporting-services/activate-the-report-server-and-power-view-integration-features-in-sharepoint.md)」を参照してください。  
  
##  <a name="bkmk_additional_config"></a> その他の構成  
 このセクションでは、SharePoint のほとんどの配置で重要になる追加の構成手順について説明します。  
  
###  <a name="bkmk_provision_agent"></a> サブスクリプションと警告の準備  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のサブスクリプションとデータ警告の機能を利用するには、SQL Server エージェントの権限の構成が必要になる場合があります。 SQL Server エージェントが実行中であるにもかかわらず、SQL Server エージェントが必要であることを示すエラー メッセージが表示された場合は、権限を更新します。 サービス アプリケーション作成成功ページの **[サブスクリプションと警告の準備]** リンクをクリックして、SQL Server エージェントを準備するための別のページに移動します。 配置がコンピューターの境界をまたいでいる場合は (たとえば、SQL Server データベース インスタンスが異なるコンピューターにある場合)、準備手順を行う必要があります。 詳細については、「 [SSRS サービス アプリケーションを使用するためのサブスクリプションと警告の準備](../../reporting-services/install-windows/provision-subscriptions-and-alerts-for-ssrs-service-applications.md)」をご覧ください  
  

  
### <a name="configure-e-mail-for-a-service-application"></a>サービスアプリケーションの電子メールを構成する  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のデータ警告機能は、電子メール メッセージで警告を送信します。 電子メールを送信するには、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サービス アプリケーションを構成して、このサービス アプリケーションの電子メール配信拡張機能を変更しなければならない場合があります。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サブスクリプション機能の電子メール配信拡張機能を使用する場合は、電子メールの設定が必要です。 詳細については、「[Reporting Services サービス アプリケーションの電子メールの構成 &#40;SharePoint 2010 および SharePoint 2013&#41;](../../reporting-services/install-windows/configure-e-mail-for-a-reporting-services-service-application.md)」を参照してください。  
  

  
### <a name="add-reporting-services-content-types"></a>Reporting Services のコンテンツの種類を追加  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] では、共有データ ソース (.rsds) ファイル、レポート モデル (.smdl)、レポート ビルダーのレポート定義 (.rdl) ファイルを管理する際に使用されるコンテンツの種類が、あらかじめ定義されています。 コンテンツの種類として、 **[レポート ビルダー レポート]** 、 **[レポート モデル]** 、および **[レポート データ ソース]** をライブラリに追加すると、 **[新規作成]** コマンドが有効になり、その種類のドキュメントを新規作成できるようになります。 詳細については、「 [SharePoint 統合モード&#40;&#41;のライブラリ Reporting Services にレポートサーバーコンテンツの種類を追加する](../../../2014/reporting-services/add-reporting-services-content-types-to-a-sharepoint-library.md)」を参照してください。  
  

  
### <a name="activate-the-file-sync-feature"></a>ファイル同期機能のアクティブ化  
 ユーザーがパブリッシュ済みレポート アイテムを SharePoint ドキュメント ライブラリに頻繁に直接アップロードする場合は、レポート サーバーのファイル同期機能が役立ちます。 ファイル同期機能では、レポート サーバー カタログとドキュメント ライブラリのアイテムの同期が、より頻繁に行われます。 詳しくは、「 [SharePoint サーバーの全体管理でレポート サーバーのファイル同期機能をアクティブにする](../../../2014/reporting-services/activate-report-server-file-sync-feature-sharepoint-central-administration.md)」をご覧ください。  
  
## <a name="see-also"></a>参照  
 [Reporting Services SharePoint モード用の PowerShell コマンドレット](../../../2014/reporting-services/powershell-cmdlets-for-reporting-services-sharepoint-mode.md)   
 [SQL Server 2012  の各エディションがサポートする機能](https://go.microsoft.com/fwlink/?linkid=232473)  
 [Reporting Services の SharePoint サービスとサービス アプリケーション](../../../2014/reporting-services/reporting-services-sharepoint-service-and-service-applications.md)  
