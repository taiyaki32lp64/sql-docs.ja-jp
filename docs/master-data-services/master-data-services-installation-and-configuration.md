---
title: インストールと構成
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: quickstart
ms.assetid: f6cd850f-b01b-491f-972c-f966b9fe4190
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 60ee313b41a3882c07c98dce08382a98fec9c962
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73728069"
---
# <a name="master-data-services-installation-and-configuration"></a>マスター データ サービスのイントールと構成

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  この記事では、Windows Server 2012 R2 コンピューターへの [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] のインストール方法、MDS データベースと Web サイトの設定方法、およびサンプル モデルとデータの配置方法について説明します。 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] (MDS) では、組織が信頼されたバージョンのデータを管理できるようにします。   
  
> [!NOTE] 
> [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] をサポートするようになった Developer Edition を使用しているときに Windows 10 マシン上に [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] をインストールすることができます。 
>>さまざまな [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)] エディションのオペレーティング システムのサポートの詳細については、「[SQL Server 2016 のインストールに必要なハードウェアおよびソフトウェア](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)」を参照してください。 

[!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] のデータを整理する方法の概要については、「[マスター データ サービスの概要 (MDS)](../master-data-services/master-data-services-overview-mds.md)」を参照してください。     
  
 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] の新機能については、「[マスター データ サービス (MDS) の新機能](../master-data-services/what-s-new-in-master-data-services-mds.md)」を参照してください。  
 
[!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]を学習するためのビデオと他のトレーニング リソースへのリンクについては、「 [マスター データ サービスについて学習する](../master-data-services/learn-sql-server-master-data-services.md)」をご覧ください。 
  
> **ダウンロード**  
> -   [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]をダウンロードするには、  **[Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-sql-server-2017-ctp/)** にアクセスしてください。  
> -   Azure アカウントをすでにお持ちですか?  **[こちら](https://azure.microsoft.com/services/virtual-machines/sql-server/?wt.mc_id=sqL16_vm)** にアクセスして、SQL Server がインストール済みの仮想マシンをすぐにご利用いただけます。  
> 
> **MDS Web サイトを作成できませんか?**
> >この問題を解決する方法については、この Microsoft サポートの記事を参照してください。
> [SQL Server 2016 の低い特権のアカウントでは、MDS Web サイトを作成することはできません。](https://aka.ms/mdssupport) 

## <a name="internet-explorer-and-silverlight"></a>Internet Explorer と Silverlight
- Windows Server 2012 マシンに [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] をインストールするときに、Web アプリケーション サイトでスクリプトを許可するように Internet Explorer セキュリティ強化を構成しなければならない場合があります。 そうしないと、サーバー コンピューター上のサイトの参照が失敗します。
- Web アプリケーションで作業するには、Silverlight 5 をクライアント コンピューターにインストールする必要があります。 Silverlight の必要なバージョンがない場合、Web アプリケーションで Silverlight を使用する部分に移動したときに、Silverlight をインストールするよう要求されます。 Silverlight 5 は **[ここ](https://www.microsoft.com/silverlight/)** からインストールできます。

## <a name="includessmdsshort_mdincludesssmdsshort-mdmd-on-an-azure-virtual-machine"></a>Azure 仮想マシン上の [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]
既定では、[!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)] が既にインストールされている Azure 仮想マシンを起動すると、[!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] もインストールされます。 

次の手順として、インターネット インフォメーション サービス (IIS) をインストールします。 「[IIS のインストールと構成](#InstallIIS)」を参照してください。 

[!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)] のインストールを変更する場合は、既定の場所 (`<drive>`: \SQLServer_13.0_Full) にある setup.exe ファイルを見つけます。
  
## <a name="InstallMDS"></a> Master Data Services のインストール  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のセットアップ インストール ウィザードまたはコマンド プロンプトを使用して、[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] をインストールします。  
  
 **Windows Server 2012 R2 コンピューター上で [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] セットアップを使用して [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] をインストールするには**  
  
1.  Setup.exe をダブルクリックして、インストール ウィザードの手順を実行します。  
  
2.  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] [機能の選択] **ページで、** [共有機能] **の [** ] を選択します。  
  
     これは [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]、アセンブリ、Windows PowerShell スナップインのほか、Web アプリケーションおよび Web サービス用のフォルダーおよびファイルがインストールされます。  
  
     ![mds_SQLServer2016Setup_FeatureSelection](../master-data-services/media/mds-sqlserver2016setup-featureselection.png "mds_SQLServer2016Setup_FeatureSelection")  
  
3.  ウィザードの指示に従って操作します。  

## <a name="InstallIIS"></a> IIS のインストールと構成
  
1.  [!INCLUDE[winblue_server_2](../includes/winblue-server-2-md.md)]で、 **デスクトップ** のタスクバーにある **[サーバー マネージャー]** アイコンをクリックします。  
  
     ![Windows Server 2012 タスクバーのサーバーマネージャーのアイコン](../master-data-services/media/mds-windowsservertaskbar-servermanagericon.png "Windows Server 2012 タスクバーのサーバーマネージャーのアイコン")  
  
5.  **サーバー マネージャー**で、 **[管理]** メニューの **[役割と機能の追加]** をクリックします。  
   
     ![[サーバー管理] の [役割と機能の追加] メニューコマンド](../master-data-services/media/mds-servermanagerdashboard-addrolesfeaturesmenu.png "[サーバー管理] の [役割と機能の追加] メニューコマンド")  
  
6.  **役割と機能の追加ウィザード** の **[インストールの種類]** ページで、既定値 (**役割ベースまたは機能ベースのインストール**) を承諾して、 **[次へ]** をクリックします。  
  
7.  **[サーバー プールからサーバーを選択]** をクリックして、 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]をインストールしたサーバーをクリックします。  
  
     ![mds_AddRolesFeaturesWizard_ServerSelectionPage](../master-data-services/media/mds-addrolesfeatureswizard-serverselectionpage.png) 
  
8. **[サーバーの役割]** ページで、 **[Web サーバー]** をクリックし、 **[次へ]** をクリックします。 

   ![mds_AddRolesFeaturesWizard_ServerRolesPage](../master-data-services/media/mds-addrolesfeatureswizard-serverrolespage.png)
   
9. **[機能]** ページで、次の機能が選択されていることを確認し、 **[次へ]** をクリックします。 これらの機能は、[!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] の [!INCLUDE[winblue_server_2_md](../includes/winblue-server-2-md.md)] に必要です。
  
    |機能のインストール|機能のインストール|  
    |--------------|--------------|  
    |![mds_AddRolesFeaturesWizard_FeaturesPage](../master-data-services/media/mds-addrolesfeatureswizard-featurespage.png)|![mds_AddRolesFeaturesWizard_FeaturesPage_WindowsProcActive](../master-data-services/media/mds-addrolesfeatureswizard-featurespage-windowsprocactive.png)|  

10. 左側のウィンドウで **[Web サーバーの役割 (IIS)]** をクリックし、 **[役割サービス]** をクリックします。
11. **[役割サービス]** ページで、次の機能が選択されていることを確認し、 **[次へ]** をクリックします。 これらのサービスは、[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] の [!INCLUDE[winblue_server_2](../includes/winblue-server-2-md.md)] に必要です。

    > [!WARNING]  
    >  [WebDAV 発行] 役割サービスをインストールしないでください。 WebDAV 発行は、 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]と互換性がありません。  
  
     |役割サービス|役割サービス|  
    |-----------------------------|-----------------------------|  
    |![mds_AddRolesFeaturesWizard_RoleServicesPage](../master-data-services/media/mds-addrolesfeatureswizard-roleservicespage.png)|![mds_AddRolesFeaturesWizard_RoleServicesPage_PerformSecurity](../master-data-services/media/mds-addrolesfeatureswizard-roleservicespage-performsecurity.png)|  
    |![mds_AddRolesFeaturesWizard_RoleServicesPage_AppDevsection](../master-data-services/media/mds-addrolesfeatureswizard-roleservicespage-appdevsection.png)|![mds_AddRolesFeaturesWizard_RoleServicesPage_ManageToolssection](../master-data-services/media/mds-addrolesfeatureswizard-roleservicespage-managetoolssection.png)|  
    |||  
  
     他のオペレーティング システムで必須の機能と役割サービスの一覧は、「[Web アプリケーションの要件 &#40;マスター データ サービス&#41;](../master-data-services/install-windows/web-application-requirements-master-data-services.md)」を参照してください。   
  
 セットアップを使用した [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のインストールの詳細については、「[インストール ウィザードからの SQL Server 2016 のインストール (セットアップ)](../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)」を参照してください。  
  
 コマンド プロンプトを使用した [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のインストールの詳細については、「 [コマンド プロンプトから SQL Server 2016 をインストール](../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)」を参照してください。 コマンド プロンプトを使用する場合、 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] は機能パラメーターとして使用できるようになります。  
  
 インストール前のタスクに関する追加情報へのリンクの簡単な説明については、「[マスター データ サービスをインストールする](../master-data-services/install-windows/install-master-data-services.md)」を参照してください。  
  
##  <a name="SetUpWeb"></a> データベースと Web サイトを設定する  
 **[!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] を使って、データベースと Web サイトを設定するには**  

 
> [!WARNING]
>  [ Configuration Manager を起動する前に ](#InstallIIS)IIS をインストール[!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]する必要があります。 それ以外の場合、Configuration Manager にインターネット インフォメーション サービス エラーが表示され、[!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] Web アプリケーションを作成できなくなります。  
> 
> **ブラウザーの要件**
> >[!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] Web アプリケーションは、Internet Explorer (IE) 9 以降でのみ動作します。 IE 8 以前のバージョン、Microsoft Edge、Chrome はサポートされていません。    
  
1.  [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] を起動して、 **[データベース構成]** をクリックします。  
  
2.  **[データベースの作成]** をクリックして、 **データベースの作成ウィザード** で **[次へ]** をクリックします。  
  
3.  **[データベースサーバー]** ページで、SQL Server インスタンスを指定します。 

    >  [!INCLUDE[sqlv15](../includes/sssqlv15-md.md)] では SQL Server Managed Instance のサポートが追加されます。 **SQL Server インスタンス**の値を、Azure SQL Database マネージインスタンスのホストに設定します。 たとえば、 `xxxxxx.xxxxxx.database.windows.net`のようにします。

4. 認証の**種類**を選択し、 **[接続のテスト]** をクリックして、選択した認証の種類の資格情報を使用してデータベースに接続できることを確認します。 **[次へ]** をクリックします。

    >[!INCLUDE[sqlv15](../includes/sssqlv15-md.md)]の場合、Azure SQL Database マネージインスタンスに接続するには、次のいずれかの認証の種類を使用します。
    >
    >- Azure Active Directory 統合認証:**現在のユーザー– Active Directory 統合**
    >- SQL Server 認証: **SQL Server アカウント**。
    >
    >Azure SQL Database マネージインスタンスでは、ユーザーは `sysadmin` 固定サーバーロールのメンバーである必要があります。

    > [!NOTE]  
    >  認証の種類に **[現在のユーザー - 統合セキュリティ]** を選択すると、 **[ユーザー名]** ボックスは読み取り専用で、コンピューターにログオンした Windows ユーザー アカウント名が表示されます。 Azure 仮想マシン (VM) 上で [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)] [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] が実行されている場合、 **[ユーザー名]** ボックスに、VM の名前と、VM 上のローカル管理者アカウントのユーザー名が表示されます。 

    ![mds_2016ConfigManager_CreateDatabaseWizard_ServerPage](../master-data-services/media/mds-2016configmanager-createdatabasewizard-serverpage.png)  
  
4.  **[データベース名]** フィールドに名前を入力します。 必要に応じて、Windows 照合順序を選択して、 **[SQL Server の既定の照合順序]** チェック ボックスをオフにし、 **[大文字小文字を区別する]** などの利用可能なオプションを 1 つ以上クリックします。 **[次へ]** をクリックします。

    ![mds_2016ConfigManager_CreateDatabaseWizard_DatabasePage](../master-data-services/media/mds-2016configmanager-createdatabasewizard-databasepage.png)  
  
     Windows 照合順序の詳細については、「 [Windows 照合順序名 (Transact-SQL)](../t-sql/statements/windows-collation-name-transact-sql.md)」を参照してください。  
  
5.  **[ユーザー名]** フィールドで、マスター データ サービスの既定のスーパー ユーザーになるユーザーの Windows アカウントを指定します。 スーパー ユーザーには、すべての機能領域へのアクセス権があり、すべてのモデルを追加、削除、および更新できます。  

    ![mds_2016ConfigManager_CreateDatabaseWizard_AdminPage](../master-data-services/media/mds-2016configmanager-createdatabasewizard-adminpage.png)  
  
6.  **[次へ]** をクリックして、 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] データベースの設定の概要を表示し、 **[次へ]** をもう一度クリックしてデータベースを作成します。 **[続行して完了する]** ページが表示されます。

7. データベースが作成され、構成されたら、 **[完了]** をクリックします。  
  
     **データベースの作成ウィザード**の設定の詳細については、「[データベースの作成ウィザード (マスター データ サービス構成マネージャー)](../master-data-services/create-database-wizard-master-data-services-configuration-manager.md)」を参照してください。  
  
7.  **の** [データベース構成][!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] ページで、 **[データベースの選択]** をクリックします。  
  
8.  **[接続]** をクリックして、手順 7 で作成した [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] データベースを選択し、 **[OK]** をクリックします。 

    ![mds_2016ConfigManager_SelectDatabaseButton_ConnectToDatabaseDialog](../master-data-services/media/mds-2016configmanager-selectdatabasebutton-connecttodatabasedialog.png)  
  
     データベースの設定が完了しました。 **[データベース構成]** ページには、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 用に接続している [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]インスタンス、作成したデータベース、および現在のデータベース バージョンが表示されます。  

    ![mds_2016ConfigManager_DatabaseConfig_Completed](../master-data-services/media/mds-2016configmanager-databaseconfig-completed.png)   
  
9. [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]の左ペインで、 **[Web の構成]** をクリックします。  
  
10. **[Web サイト]** リスト ボックスで、 **[既定の Web サイト]** **[作成]** の順にクリックして、Web アプリケーションを作成します。  
  
    > [!NOTE]  
    >  **[既定の Web サイト]** を選択した場合、Web アプリケーションを作成する必要があります。 リスト ボックスで **[新しい Web サイトの作成]** を選択した場合、アプリケーションが自動的に作成されます。  

     ![mds_2016ConfigManager_WebConfig](../master-data-services/media/mds-2016configmanager-webconfig.png)  
  
11. **[アプリケーション プール]** セクションで、次のいずれかを実行します。  
  
    -   **管理者アカウント** データベースに対して、手順 5 で入力したのと同じユーザー名を入力し、パスワードを入力して、 **[OK]** をクリックします。  
  
         **- または -**  
  
    -   別のユーザー名とパスワードを入力し、[OK] をクリックします。  
  
         データベースと Web アプリケーションを作成する場合、同じアカウントを使用する必要はありません。  

        ![mds_2016ConfigManager_WebConfig_CreateWebApplication](../master-data-services/media/mds-2016configmanager-webconfig-createwebapplication.png)   
  
     **[Web アプリケーションの作成]** ダイアログ ボックスの詳細については、「[[Web アプリケーションの作成] ダイアログ ボックス (マスター データ サービス構成マネージャー)](../master-data-services/create-web-application-dialog-box-master-data-services-configuration-manager.md)」を参照してください。  
  
12. **[Web アプリケーション]** ボックスの **[Web 構成]** ページで、作成したアプリケーションをクリックして、 **[アプリケーションとデータベースの関連付け]** セクションで  **[選択]** をクリックします。  
  
13. **[接続]** をクリックして、Web アプリケーションと関連付けする必要がある [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] データベースを選択し、 **[OK]** をクリックします。  
  
     Web サイトの設定が完了しました。 **[Web の構成]** ページには、選択した Web サイト、作成した Web アプリケーション、およびアプリケーションに関連付けられた [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] データベースが表示されます。  

     ![mds_2016ConfigManager_WebConfig_Completed](../master-data-services/media/mds-2016configmanager-webconfig-completed.png)  
 
     
15. **[適用]** をクリックします。 **[構成の完了]** メッセージ ボックスが表示されます。 メッセージ ボックスで **[OK]** をクリックして、Web アプリケーションを起動します。 Web サイトのアドレスは、 https://*server name*/*web application*/ です。 


![mds_2016ConfigurationComplete_MessageBox](../master-data-services/media/mds-2016configurationcomplete-messagebox.png) 
  
     For more information about the settings on the Web Configuration page, see [Web Configuration Page &#40;Master Data Services Configuration Manager&#41;](../master-data-services/web-configuration-page-master-data-services-configuration-manager.md)  
  
 また、 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] を使って、 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] データベースに関連付けられている Web アプリケーションとサービスのその他の設定値も指定できます。 たとえば、データの読み込み頻度や検証メールの送信頻度を指定できます。 詳細については、「[システム設定 &#40;マスター データ サービス&#41;](../master-data-services/system-settings-master-data-services.md)」を参照してください。  
  
##  <a name="deploySample"></a> サンプル モデルとデータを配置する  
 次の 3 つのサンプル モデル パッケージは、[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] に付属しています。   これらのサンプル モデルには、データが含まれます。 **サンプル モデル パッケージの既定の場所は、%programfiles%\Microsoft SQL Server\140\Master Data Services\Samples\Packages です。**
  
-   chartofaccounts_en.pkg  
  
-   customer_en.pkg  
  
-   product_en.pkg  
  
 このパッケージは、MDSModelDeploy ツールを使用して配置します。 MDSModelDeploy ツールの既定の場所は、 *drive*\Program Files\Microsoft SQL Server\ 140\Master Data Services\Configuration にあります。  
  
 このツールを実行するための前提条件については、「[MDSModelDeploy を使用したモデルの配置パッケージの配置](../master-data-services/deploy-a-model-deployment-package-by-using-mdsmodeldeploy.md)」を参照してください。  
  
 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)][!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] の新機能をサポートするためにデータに加えられた更新については、「[SQL Server のサンプル: モデル配置パッケージ(MDS)](../master-data-services/sql-server-samples-model-deployment-packages-mds.md)」を参照してください。  
  
 **サンプル モデルを配置するには**  
  
1.  サンプル モデル パッケージを *drive*\Program Files\Microsoft SQL Server\140\Master Data Services\Configuration にコピーします。  
  
2.  管理者のコマンド プロンプトを開き、次のコマンドを実行して、MDSModelDeploy.exe のある場所に移動します。  
  
    ```  
    cd c:\Program Files\Microsoft SQL Server\140\Master Data Services\Configuration  
    ```  
  
3.  次の各コマンドを実行して、各サンプル モデルを [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] に配置します。  
  
    > [!IMPORTANT]  
    >  次の例では、サービスの値に `MDS1` が指定されます。 **Web サイトの設定時に、** [既定の Web サイト] [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] を選択した場合、この値を使用します。  「 [データベースと Web サイトを設定する](#SetUpWeb) 」セクションを参照してください。  
    >   
    >  新しい Web サイトを作成したか、または別の既存の Web サイトを選択した場合、適切なサービス値を特定するために、まず次のコマンドを実行します。  
    >   
    >  `MDSModelDeploy listservices`  
    >   
    >  戻り値のリスト内の最初のサービス値は、モデルを配置するために指定する値です。  
    >
    > [!NOTE]
    > サンプル モデルのメタデータ情報に関する詳細については、"c:\Program Files\Microsoft SQL Server\140\Master Data Services\Configuration" の場所にある使用可能な readme ファイルを参照してください。
    >
   
     **chartofaccounts_en.pkg サンプル モデルを配置するには**  
  
    ```  
    MDSModelDeploy deploynew -package chartofaccounts_en.pkg -model ChartofAccounts -service MDS1  
    ```  
  
     **customer_en.pkg サンプル モデルを配置するには**  
  
    ```  
    MDSModelDeploy deploynew -package customer_en.pkg -model Customer -service MDS1  
    ```  
  
     **product_en.pkg サンプル モデルを配置するには**  
  
    ```  
    MDSModelDeploy deploynew -package product_en.pkg -model Product -service MDS1  
  
    ```  
  
     モデルが正常に配置されると、"**MDSModelDeploy 操作は完了しました**" というメッセージが表示されます。  
  
     次の図は、product_en.pkg サンプル モデルを配置するためのコマンドを示します。  
  
     ![製品サンプルモデルを配置するためのコマンドライン](../master-data-services/media/mds-commandprompt-deployingsamplemodel-product.png "製品サンプルモデルを配置するためのコマンドライン")  
  
4.  サンプル モデルを表示するには、次を実行します。  
  
    1.  設定する [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] Web サイトに移動します。 「 [データベースと Web サイトを設定する](#SetUpWeb) 」セクションを参照してください。  
  
         Web サイトのアドレスは、 https://*server name*/*web application*/ です。  
  
    2.  **[モデル]** リスト ボックスからモデルを選択して、 **[エクスプローラー]** をクリックします。  
  
         ![MDS Web サイト、ホームページ。](../master-data-services/media/mds-mdswebsite-homepage-selectsamplemodel.png "MDS Web サイト、ホームページ。")  
  
## <a name="next-step"></a>次の手順  
 自分のデータ用に新しいモデルとエンティティを作成します。 「[モデルを作成する (マスター データ サービス)](../master-data-services/create-a-model-master-data-services.md)」と「[エンティティを作成する (マスター データ サービス)](../master-data-services/create-an-entity-master-data-services.md)」を参照してください。  
  
 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] のデータの構造を構築するモデルとエンティティを使用する方法の概要については、「[マスター データ サービスの概要 (MDS)](../master-data-services/master-data-services-overview-mds.md)」を参照してください。  
    
## <a name="see-also"></a>参照  
 [マスター データ サービス データベース](../master-data-services/master-data-services-database.md)   
 [マスター データ マネージャー Web アプリケーション](../master-data-services/master-data-manager-web-application.md)   
 [[データベース構成] ページ (マスター データ サービス構成マネージャー)](../master-data-services/database-configuration-page-master-data-services-configuration-manager.md)   
 [マスター データ サービス &#40;MDS&#41; の新機能](../master-data-services/what-s-new-in-master-data-services-mds.md)  
  
  
