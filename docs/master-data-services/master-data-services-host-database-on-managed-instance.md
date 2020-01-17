---
title: マネージインスタンスでデータベースをホストする
description: この記事では、マネージインスタンスでマスターデータサービス (MDS) データベースを構成する方法について説明します。
ms.custom: ''
ms.date: 07/01/2019
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 19519697-c219-44a8-9339-ee1b02545445
author: v-redu
ms.author: lle
manager: craigg
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: b4bb1a89e997486e88b6d4ca48a9a550d1c552b8
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73729021"
---
# <a name="host-an-mds-database-on-a-managed-instance"></a>マネージインスタンスで MDS データベースをホストする

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  この記事では、マネージインスタンスでマスターデータサービス (MDS) データベースを構成する方法について説明します。
  
## <a name="preparation"></a>準備

準備を行うには、Azure SQL Database マネージインスタンスを作成して構成し、web アプリケーションコンピューターを構成する必要があります。

### <a name="create-and-configure-the-database"></a>データベースを作成し、構成する

1. 仮想ネットワークを使用して Azure SQL Database マネージインスタンスを作成します。 詳細については[、「クイックスタート: Azure SQL Database マネージインスタンスを作成](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-get-started)する」を参照してください。

1. ポイント対サイト接続を構成します。 手順については、「[ネイティブ Azure 証明書 Azure portal 認証を使用して VNet へのポイント対サイト接続を構成](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal)する」を参照してください。

1. SQL Database マネージインスタンスを使用して Azure Active Directory 認証を構成します。 詳細については[、「SQL での Azure Active Directory 認証の構成と管理](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication-configure)」を参照してください。

### <a name="configure-web-application-machine"></a>Web アプリケーションコンピューターの構成

1. コンピューターが SQL Database マネージインスタンスにアクセスできることを確認するには、ポイント対サイト接続証明書と VPN をインストールします。 手順については、 [Azure portal 「ネイティブ Azure 証明書認証を使用した VNet へのポイント対サイト接続の構成](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal)」を参照してください。

1. 次の役割と機能をインストールします。
   - ロール
     - [インターネット インフォメーション サービス]
     - Web 管理ツール
     - IIS 管理コンソール
     - World Wide Web サービス
     - アプリケーション開発
     - .NET Extensibility 3.5
     - .NET Extensibility 4.5
     - ASP.NET 3.5
     - ASP.NET 4.5
     - ISAPI 拡張
     - ISAPI フィルター
     - HTTP 基本機能
     - 既定のドキュメント
     - ディレクトリの参照
     - HTTP エラー
     - 静的なコンテンツ
     - 状態と診断
     - HTTP ログ
     - 要求の監視
     - パフォーマンス
     - 静的なコンテンツの圧縮
     - セキュリティ
     - 要求フィルター
     - [Windows 認証]
       > [!NOTE]
       > WebDAV 発行をインストールしない

   - 機能
     - .NET Framework 3.5 (.NET 2.0 および 3.0 を含む)
     - .NET Framework 4.5 Advanced Services
     - ASP.NET 4.5
     - WCF サービス
     - HTTP アクティブ化 (必須)
     - TCP ポート共有
     - Windows プロセス アクティブ化サービス
     - プロセス モデル
     - .NET 環境
     - 構成 API
     - 動的なコンテンツ圧縮

## <a name="install-and-configure-an-mds-web-application"></a>MDS web アプリケーションのインストールと構成

次に、[!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]をインストールして構成します。

### <a name="install-sql-server-2019"></a>SQL Server 2019 をインストールする

SQL Server セットアップインストールウィザードまたはコマンドプロンプトを使用して [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]をインストールします。

1. `Setup.exe`を開き、インストールウィザードの手順に従います。

2. [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] [機能の選択] **ページで、** [共有機能] **の [** ] を選択します。
この操作は次のようにインストールされます。
   - [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]
   - アセンブリ
   - Windows PowerShell スナップイン
   - Web アプリケーションとサービスのフォルダーとファイル。

   ![SQLServer2019--Config-MI-SQLFeatureSelection](../master-data-services/media/mds-sqlserver2019-config-mi-sqlfeatureselection.png "SQLServer2019-Config-MI_SQLFeatureSelection")  

### <a name="set-up-the-database-and-website"></a>データベースと web サイトを設定する

1. Azure Virtual Network に接続して、マネージインスタンスに接続できることを確認します。

   ![mds-SQLServer2019-P2SVPNConnect](../master-data-services/media/mds-sqlserver2019-config-mi-p2svpnconnect.png "SQLServer2019-Config-MI_P2SVPNConnect")

1. [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] を開き、左側のウィンドウで **[データベースの構成]** を選択します。

1. **[データベースの作成]** を選択して、**データベースの作成ウィザード**を開きます。 **[次へ]** を選択します。

1. **[データベースサーバー]** ページで、 **[SQL Server インスタンス]** フィールドに入力し、**認証の種類**を選択します。 **[テスト接続]** を選択して、資格情報を使用して、選択した認証の種類を使用してデータベースに接続できることを確認します。 **[次へ]** を選択します。

   > [!NOTE]
   > - SQL Server インスタンスは `xxxxxxx.xxxxxxx.database.windows.net`のようになります。
   > - マネージインスタンスの場合は、 **"SQL Server Account"** と **"Current User – Active Directory Integrated"** 認証の種類のいずれかを選択します。
   > - 認証の種類として **[現在のユーザー-Active Directory 統合]** を選択した場合、 **[ユーザー名]** フィールドは読み取り専用になり、現在サインオンされている Windows ユーザーアカウントが表示されます。 Azure 仮想マシン (VM) で SQL Server 2019 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] を実行している場合、 **[ユーザー名]** フィールドには vm の名前と、vm 上のローカル管理者アカウントのユーザー名が表示されます。

   認証には、マネージインスタンスの **"sysadmin"** 規則が含まれている必要があります。

   ![SQLServer2019-MI-CreateDBConnect](../master-data-services/media/mds-sqlserver2019-config-mi-createdbconnect.png "SQLServer2019-Config-MI_CreateDBConnect")  

1. **[データベース名]** フィールドに名前を入力します。 必要に応じて、Windows 照合順序を選択するには、[**既定の照合順序を SQL Server**する] チェックボックスをオフにし、使用可能なオプションを1つ以上選択します。 たとえば、**大文字と小文字を区別**します。 **[次へ]** を選択します。

   ![SQLServer2019---//](../master-data-services/media/mds-sqlserver2019-config-mi-createddbname.png "SQLServer2019-Config-MI_CreatedDBName")

1. **[ユーザー名]** フィールドで、[!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]の既定のスーパーユーザーの Windows アカウントを指定します。 スーパーユーザーは、すべての機能領域にアクセスでき、すべてのモデルの追加、削除、および更新を行うことができます。

   ![SQLServer2019------//](../master-data-services/media/mds-sqlserver2019-config-mi-createdbusername.png "SQLServer2019-Config-MI_createDBUserName")

1. [**次**へ] を選択すると、[!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] データベースの設定の概要が表示されます。 もう一度 **[次へ]** を選択して、データベースを作成します。 **[進行状況と完了]** ページが表示されます。

1. データベースの作成と構成が完了したら、 **[完了]** を選択します。

   **データベースの作成ウィザード**の設定の詳細については、「[データベースの&#40;作成ウィザード&#41;[!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] Configuration Manager](../master-data-services/create-database-wizard-master-data-services-configuration-manager.md)」を参照してください。

1. [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]の **[データベースの構成]** ページで、データベースの **[選択]** を選択します。

1. **[接続]** を選択し、[!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] データベースを選択して、[ **OK]** を選択します。

   ![SQLServer2019-MI-connectDBName](../master-data-services/media/mds-sqlserver2019-config-mi-connectdbname.png "SQLServer2019-Config-MI_connectDBName")

1. [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]の左側のウィンドウで、 **[Web 構成]** を選択します。

1. [Web**サイト] ボックスの一覧で** **[既定の web サイト]** を選択し、 **[作成]** を選択して web アプリケーションを作成します。

   ![mds-SQLServer2019-WebConfiguration](../master-data-services/media/mds-sqlserver2019-config-mi-webconfiguration.png "SQLServer2019-Config-MI_WebConfiguration")

   > [!NOTE]
   > [既定の**Web サイト**] を選択した場合は、個別に web アプリケーションを作成する必要があります。 リストボックスで [**新しい web サイトを作成**する] を選択すると、アプリケーションが自動的に作成されます。

1. **[アプリケーションプール]** セクションで、別のユーザー名を入力し、パスワードを入力して、[ **OK]** を選択します。

   ![SQLServer2019--Config-MI-CreateWebApplication](../master-data-services/media/mds-sqlserver2019-config-mi-createwebapplication.png "SQLServer2019-Config-MI_CreateWebApplication")

   > [!NOTE]
   > ユーザーが、最近作成した Active Directory 統合認証を使用してデータベースにアクセスできることを確認します。 または、`web.config` 後で接続を変更することもできます。

   **[Web アプリケーションの作成]** ダイアログボックスの詳細については、「[ [Web アプリケーションの作成] ダイアログ&#40;ボックス[!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] Configuration Manager&#41;](../master-data-services/create-web-application-dialog-box-master-data-services-configuration-manager.md)」を参照してください。

1. **Web アプリケーション**ウィンドウの **[web 構成]** ウィンドウで、作成したアプリケーションを選択し、 **[アプリケーションとデータベースの関連付け]** セクションで **[選択]** を選択します。

1. **[接続]** を選択し、web アプリケーションに関連付ける [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] データベースを選択します。 **[OK]** を選択します。

   Web サイトのセットアップが完了しました。 **[Web 構成]** ページに、選択した web サイト、作成した web アプリケーション、およびアプリケーションに関連付けられている [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] データベースが表示されるようになります。

   ![mds-SQLServer2019-WebConfigSelectDB](../master-data-services/media/mds-sqlserver2019-config-mi-webconfigselectdb.png "SQLServer2019-Config-MI_WebConfigSelectDB")

1. **[適用]** を選択します。 **構成が完了**したことを確認するメッセージが表示されます。 メッセージボックスで [ **OK]** を選択して、web アプリケーションを起動します。 Web サイトのアドレスは `http://server name/web application/`。

## <a name="configure-authentication"></a>認証の構成

マネージインスタンスデータベースを web アプリケーションに接続するには、他の認証の種類を変更する必要があります。

[`C:\Program Files\Microsoft SQL Server\150\Master Data Services\WebApplication`] で `web.config` ファイルを見つけます。 ConnectionString を変更して、マネージインスタンスデータベースに接続するための他の認証の種類を変更します。

既定の認証の種類は、次の接続文字列の例に示すように `Active Directory Integrated` ます。

   ```xml
   <add name="MDS1" connectionString="Data Source=*****.*****.database.windows.net;Initial Catalog=MasterDataServices;Integrated Security=False;Connect Timeout=60;Authentication=&quot;Active Directory Integrated&quot;" />
   ```

MDS では、次の接続文字列の例に示すように、Active Directory パスワード認証と SQL Server 認証もサポートしています。

- パスワード認証の Active Directory

   ```xml
   <add name="MDS1" connectionString="Data Source=*****.*****.database.windows.net;Initial Catalog=MasterDataServices;Integrated Security=False;Connect Timeout=60;Authentication=&quot;Active Directory Password&quot; ; UID=bob@contoso.onmicrosoft.com; PWD=MyPassWord!" />
   ```

- SQL Server 認証

   ```xml
   <add name="MDS1" connectionString="Data Source=*****.*****.database.windows.net;Initial Catalog=MasterDataServices;Integrated Security=False;Connect Timeout=60;User ID=UserName;Password=MyPassword!;" />
   ```

## <a name="upgrade-includessmdsshort_mdincludesssmdsshort-mdmd-and-sql-database-version"></a>アップグレード [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] と SQL Database バージョン

### <a name="upgrade-includessmdsshort_mdincludesssmdsshort-mdmd"></a>[!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] のアップグレード

**SQL Server 2019 の累積的な更新プログラム**をインストールします。 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] は自動的に更新されます。

### <a name="upgrade-sql-server"></a>SQL Server をアップグレードする

**SQL Server 2019 の累積的な更新プログラム**をインストールした後に `The client version is incompatible with the database version` エラーが発生することがあります。
![SQLServer2019--Config-MI-UpgradeDBPage](../master-data-services/media/mds-sqlserver2019-config-mi-upgradedbpage.png "mSQLServer2019-Config-MI_UpgradeDBPage ")

この問題を解決するには、データベースのバージョンをアップグレードする必要があります。

1. [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]を開き、左側のウィンドウで **[データベースの構成]** を選択します。

1. [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]の **[データベースの構成]** ページで、データベースの **[選択]** を選択します。

1. Web アプリケーションに関連付けた [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] データベースを選択します。 **[接続]** を選択し、[ **OK]** を選択します。

   ![SQLServer2019-MI-ConnectDBName](../master-data-services/media/mds-sqlserver2019-config-mi-connectdbname.png "SQLServer2019-Config-MI_ConnectDBName")

1. **[データベースのアップグレード]** を選択します。 」を参照してください。

   ![SQLServer2019--Config-MI-SelectUpgradeDB](../master-data-services/media/mds-sqlserver2019-config-mi-selectupgradedb.png "SQLServer2019-Config-MI_SelectUpgradeDB")

1. データベースのアップグレードウィザードの **[ようこそ]** ページで **[次へ]** を選択し、 **[アップグレードの確認]** ページをクリックします。

   ![SQLServer2019--MI-UpgradeDBWizard](../master-data-services/media/mds-sqlserver2019-config-mi-upgradedbwizard.png "SQLServer2019-Config-MI_UpgradeDBWizard")

1. すべてのタスクが完了したら、 **[完了]** を選択します。

## <a name="see-also"></a>参照

- [マスター データ サービス データベース](../master-data-services/master-data-services-database.md)
- [マスター データ マネージャー Web アプリケーション](../master-data-services/master-data-manager-web-application.md)
- [[データベース構成] ページ (マスター データ サービス構成マネージャー)](../master-data-services/database-configuration-page-master-data-services-configuration-manager.md)
- [マスター データ サービス &#40;MDS&#41; の新機能](../master-data-services/what-s-new-in-master-data-services-mds.md)
