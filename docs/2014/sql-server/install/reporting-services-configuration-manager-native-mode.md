---
title: Reporting Services 構成マネージャー (ネイティブ モード) | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Reporting Services Configuration tool
- configuration options [Reporting Services]
- report servers [Reporting Services], configuring
- components [Reporting Services], Reporting Services Configuration tool
ms.assetid: 379eab68-7f13-4997-8d64-38810240756e
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: e7b5e46b90702bf39bf2902eed3e5a6c609757e0
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952491"
---
# <a name="reporting-services-configuration-manager-native-mode"></a>Reporting Services 構成マネージャー (ネイティブ モード)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のネイティブ モード インストールを構成するには、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成マネージャーを使用します。 ファイルのみのインストール オプションを使用してレポート サーバーをインストールした場合は、構成マネージャーを使用して、サーバーを使用するための構成を行う必要があります。 既定の構成のインストール オプションを使用してレポート サーバーをインストールした場合は、構成マネージャーを使用して、セットアップ時に指定した設定の確認や変更を行うことができます。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成マネージャーでは、ローカルまたはリモートのレポート サーバー インスタンスを構成できます。  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ネイティブ モード。  
  
> [!NOTE]  
>  [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] リリース以降の [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成マネージャーは、SharePoint モードのレポート サーバーを管理できるように設計されていません。 SharePoint モードの管理や構成は、SharePoint サーバーの全体管理および PowerShell スクリプトを使用して行います。 詳細については、「sharepoint[モードのインストール&#40;Reporting Services SharePoint&#41;2010 および sharepoint 2013](../../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md)」を参照してください。  
  
 **このセクションの内容:**  
  
 [レポート サーバー サービス アカウントの構成 &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)  
 サービスのアカウントとパスワードを変更する方法の推奨事項と手順について説明します。  
  
 [レポート サーバー URL の構成 &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)  
 レポート サーバー Web サービスおよびレポート マネージャーへのアクセスに使用する URL を構成する方法について説明します。  
  
 [レポート サーバー データベースの作成 &#40;SSRS 構成マネージャー&#41;](../../../2014/sql-server/install/create-a-report-server-database-ssrs-configuration-manager.md)  
 サーバーのメタデータやオブジェクトの格納に必要なレポート サーバー データベースを作成する方法について説明します。  
  
 [レポート サーバー データベース接続の構成 &#40;SSRS構成マネージャー&#41;](../../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)  
 レポート サーバーからレポート サーバー データベースへの接続に使用する接続文字列を変更する方法について説明します。  
  
 [自動実行アカウントの構成 &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)  
 自動実行モードでレポートを処理するようにユーザー アカウントを構成する方法について説明します。  
  
 [電子メール配信&#40;SSRS 用にレポートサーバーを構成する Configuration Manager&#41;](../../../2014/sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md)  
 電子メールによるレポートの配信をサポートするようにレポート サーバーを構成する方法について説明します。  
  
 [ネイティブ モード レポート サーバーのスケールアウト配置の構成 (SSRS 構成マネージャー)](../../reporting-services/install-windows/configure-a-native-mode-report-server-scale-out-deployment.md)  
 複数のレポート サーバー インスタンスで共有レポート サーバー データベースを使用する構成についての情報を提供します。  
  
 [暗号化キーの構成と管理 &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md)  
 機微なデータの保存時に使用する暗号化キーを使用および管理する方法について説明します。  
  
 [Reporting Services ネイティブ モードのレポート サーバーの管理](../../reporting-services/report-server/manage-a-reporting-services-native-mode-report-server.md)  
 一般的な作業の実行手順について説明します。  
  
 [Reporting Services Configuration Manager の F1 ヘルプ&#40;トピック SSRS ネイティブモード&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-f1-help-topics-ssrs-native-mode.md)  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ツールの各ページに関するヘルプ トピックを提供します。  
  
 **このトピックの内容:**  
  
-   [Reporting Services Configuration Manager を使用するシナリオ](#bkmk_scenarios)  
  
-   [要件](#bkmk_requirements)  
  
-   [Reporting Services Configuration Manager を開始するには](#bkmk_start_configuration_manager)  
  
##  <a name="bkmk_scenarios"></a> Reporting Services 構成マネージャーを使用するシナリオ  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成マネージャーを使用すると、次のタスクを実行できます。  
  
-   レポート サーバー サービス アカウントの構成。 アカウントは最初にセットアップ時に構成されますが、パスワードの更新や使用するアカウントの変更を行う場合は、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成マネージャーで変更できます。  
  
-   URL の作成および構成。 レポート サーバーおよびレポート マネージャーは、URL でアクセスされる [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] アプリケーションです。 レポート サーバーの URL からは、レポート サーバーの SOAP エンドポイントにアクセスできます。 レポート マネージャーの URL は、レポート マネージャーを起動するために使用されます。 1 つの URL を構成することも、アプリケーションごとに複数の URL を構成することもできます。  
  
-   レポート サーバー データベースの作成および構成。 レポート サーバーは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースを内部ストレージとして必要とする、ステートレス サーバーです。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成マネージャーを使用すると、レポート サーバー データベースを作成し、そのレポート サーバー データベースへの接続を構成できます。 必要なコンテンツが格納されている既存のレポート サーバー データベースを選択することもできます。  
  
-   ネイティブ モードのスケールアウト配置の構成。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] では、複数のレポート サーバー インスタンスで 1 つの共有レポート サーバー データベースを使用できるようにする配置トポロジをサポートします。 レポート サーバーをスケールアウト配置するには、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成マネージャーを使用して各レポート サーバーを共有レポート サーバー データベースに接続します。  
  
-   保存されている接続文字列や資格情報を暗号化する対称キーのバックアップ、復元、または置き換え。 サービス アカウントを変更する場合や、レポート サーバー データベースを別のコンピューターに移動する場合は、対称キーのバックアップが必要となります。  
  
-   自動実行アカウントを構成する。 このアカウントは、スケジュールされた操作でのリモート接続や、ユーザーの資格情報が利用できない場合に使用します。  
  
-   レポート サーバーの電子メールの構成。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] は、簡易メール転送プロトコル (SMTP) を使用してレポートまたはレポート処理通知を電子メールボックスに配信する、レポート サーバーの電子メール配信拡張機能を備えています。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成マネージャーでは、電子メール配信に使用する、ネットワーク上の SMTP サーバーまたはゲートウェイを指定できます。  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成マネージャーには、レポート サーバー コンテンツの管理、拡張機能の有効化、サーバーに対するアクセス権の付与を支援する機能はありません。 これには完全な配置が必要であり、拡張機能の有効化や既定値の変更には [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] を使用し、サーバーへのユーザー アクセス権の付与にはレポート マネージャーを使用します。  
  
##  <a name="bkmk_requirements"></a> 必要条件  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成マネージャーはバージョン固有です。 このバージョンの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] と共にインストールされる [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーは、以前のバージョンの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]の構成には使用できません。 同じコンピューター上で古いバージョンと新しいバージョンの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] をサイド バイ サイドで実行している場合は、各バージョンに付属する Reporting Services 構成マネージャーを使用して、各インスタンスを構成する必要があります。  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成マネージャーを使用するには、次の準備が必要です。  
  
-   構成対象のレポート サーバーをホストするコンピューターに対し、ローカルのシステム管理者権限が必要です。 リモート コンピューターを構成する場合、そのリモート コンピューターに対するローカルのシステム管理者権限も必要です。  
  
-   レポート サーバー データベースをホストするために使用される [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] に対し、データベースを作成する権限が必要です。  
  
-   構成対象のレポート サーバー上で、Windows Management Instrumentation (WMI) サービスが有効化および実行されている必要があります。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成マネージャーは、レポート サーバーの WMI プロバイダーを使用して、ローカルおよびリモートのレポート サーバーに接続します。 リモートのレポート サーバーを構成する場合は、そのコンピューターでリモートの WMI アクセスが許可されている必要があります。 詳細については、「 [リモート管理用のレポート サーバーの構成](../../reporting-services/report-server/configure-a-report-server-for-remote-administration.md)」を参照してください。  
  
-   リモートのレポート サーバー インスタンスに接続して構成するには、リモートの WMI (Windows Management Instrumentation) 呼び出しを有効にして Windows ファイアウォールを通過できるようにしておく必要があります。 詳細については、 [オンライン ブックの「](../../reporting-services/report-server/configure-a-report-server-for-remote-administration.md) リモート管理用のレポート サーバーの構成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 」を参照してください。  
  
 このバージョンの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成マネージャーは [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
##  <a name="bkmk_start_configuration_manager"></a> Reporting Services 構成マネージャーを起動するには  
  
#### <a name="to-start-reporting-services-configuration"></a>Reporting Services 構成を開始するには  
  
1.  使用している Microsoft Windows のバージョンに合わせて次の手順を使用します。  
  
    -   Windows のスタート画面から「 **Reporting** 」と入力し、検索結果から " **Reporting Services 構成マネージャー** " を選択します。  
  
    -   **[スタート]** ボタンをクリックし、 **[すべてのプログラム]** 、[ [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]]、 **[構成ツール]** の順にポイントします。  
  
         以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]からレポート サーバー インスタンスを構成する場合は、そのバージョンのプログラム フォルダーを開きます。 たとえば、 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] サーバー コンポーネントの構成ツールを開くには、[ [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)] ] ではなく [ [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] ] をポイントします。  
  
         **[Reporting Services 構成マネージャー]** をクリックします。  
  
2.  **[Reporting Services 構成の接続]** ダイアログ ボックスが表示されたら、構成するレポート サーバー インスタンスを選択できます。 **[接続]** をクリックします。  
  
3.  **[サーバー名]** ボックスに、レポート サーバー インスタンスがインストールされているコンピューターの名前を指定します。 ローカル コンピューターの名前が既定で表示されますが、リモート コンピューターにインストールされているレポート サーバーに接続する場合は、リモートの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスの名前を入力できます。  
  
4.  リモート コンピューターを指定する場合は、 **[検索]** をクリックして接続を確立します。  
  
5.  **Report Server stance**で、構成する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] インスタンスを選択します。 この一覧には、このバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のレポート サーバー インスタンスのみが表示されます。 以前のバージョンの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]を構成することはできません。  
  
6.  **[接続]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [レポート マネージャー &#40;SSRS ネイティブ モード&#41;](../../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [Reporting Services ツール](../../reporting-services/tools/reporting-services-tools.md)   
 [レポート サーバー データベース接続の構成 &#40;SSRS 構成マネージャー&#41;](../../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)   
 [SQL Server 構成マネージャー](../../relational-databases/sql-server-configuration-manager.md)   
 [レポート サーバーを構成および管理する &#40;SSRSネイティブ モード&#41;](../../reporting-services/report-server/configure-and-administer-a-report-server-ssrs-native-mode.md)  
  
  
