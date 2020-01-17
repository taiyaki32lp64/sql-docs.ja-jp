---
title: Reporting Services ネイティブ モード レポート サーバーのインストール |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- default configuration [Reporting Services]
- report servers [Reporting Services], default configurations
- installation options [Reporting Services]
ms.assetid: 8f25e6dc-b753-400e-9e9a-50f4f35bf6c4
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f3a54650403458eec09826b51f1528a844e48791
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66108811"
---
# <a name="install-reporting-services-native-mode-report-server"></a>Reporting Services ネイティブ モードのレポート サーバーのインストール
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ネイティブ モード レポート サーバーは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インストール ウィザードまたはコマンド ラインからインストールできます。 セットアップ ウィザードで、1) ファイルをインストールして既定の設定でサーバーを構成する、または 1) ファイルのインストールのみを行いインストール ウィザードではサーバーを構成しない、のいずれかを選択できます。 このトピックでは *ネイティブ モードの既定の構成* について確認します。このインストールでは、セットアップでレポート サーバー インスタンスのインストールと構成の両方が行われます。 セットアップが完了すると、レポート サーバーが実行され、使用できる状態になります。 ネイティブ モードのレポート サーバーは、スタンドアロンのアプリケーション サーバーとして実行されます。 ネイティブ モードは既定のサーバー モードです。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ネイティブ モード|  
  
##  <a name="bkmk_top"></a> このトピックの内容  
  
-   [既定の構成とは何ですか。](#bkmk_whatisdefaultconfiguration)  
  
-   [ネイティブ モードの既定の構成をインストールします。](#bkmk_whentoinstalldefaultconfig)  
  
-   [必要条件](#bkmk_requirements)  
  
-   [既定の URL 予約](#bkmk_defaultURLreservations)  
  
-   [SQL Server のインストール ウィザードによるネイティブ モードをインストールします。](#bkmk_installwithwizard)  
  
-   [コマンドラインを使用したネイティブ モードをインストールします。](#bkmk_commandline)  
  
##  <a name="bkmk_whatisdefaultconfiguration"></a> 既定の構成とは何ですか。  
 ネイティブ モードの既定の構成オプションを選択すると、セットアップで次の [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 機能がインストールされます。  
  
-   レポート サーバー サービス (レポート サーバー Web サービス、バックグラウンド処理アプリケーション、およびレポート マネージャーを含む)  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成マネージャー  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] コマンド ライン ユーティリティ (rsconfig.exe、rskeymgmt.exe、rs.exe)  
  
 このオプションは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] や [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]などの共有機能には適用されません。これらの機能をインストールする場合は、別のアイテムとして指定する必要があります。  
  
 ネイティブ モードのレポート サーバーのインストールの場合は、セットアップで以下が構成されます。  
  
-   レポート サーバー サービスのサービス アカウント  
  
-   レポート サーバー Web サービスの URL  
  
-   レポート マネージャーの URL  
  
-   レポート サーバー データベース  
  
-   レポート サーバー データベースへのサービス アカウント アクセス  
  
-   レポート サーバー データベース用の DSN 接続  
  
 セットアップでは、自動実行用アカウント、レポート サーバーの電子メール、暗号化キーのバックアップ、およびスケールアウト配置が構成されません。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成マネージャーを使用して、これらのプロパティを構成できます。 詳細については、「 [Reporting Services 構成マネージャー &#40;ネイティブ モード&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md)」を参照してください。  
  
##  <a name="bkmk_whentoinstalldefaultconfig"></a> ネイティブ モードの既定の構成をインストールします。  
 既定の構成では、セットアップの完了後すぐにレポート サーバーを使用できるように、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] が操作可能な状態でインストールされます。 このモードは、他のモードであれば [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ツールで実行すべき必須の構成タスクを省いて手順を省略する場合に指定します。  
  
 既定の構成をインストールしても、セットアップの完了後にレポート サーバーが動作するかどうかは保証されません。 サービスの起動時に既定の URL が登録されない可能性があります。 必ずインストールをテストして、サービスが予期したとおりに起動して実行されるかどうかを確認してください。  
  
##  <a name="bkmk_requirements"></a> 必要条件  
 既定の構成オプションでは、レポート サーバーを稼働させるために必要な中核となる設定の構成に既定値が使用されます。 これには次の要件があります。  
  
-   Microsoft SQL Server を実行するには、最低限のハードウェア要件とソフトウェア要件をハードウェアが満たしている必要があります。 詳細については、「 [Hardware and Software Requirements for Installing SQL Server 2014](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)」をご参照ください。  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] および [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] を、同じインスタンスに一緒にインストールする必要があります。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] インスタンスは、セットアップで作成されて構成されるレポート サーバー データベースをホストします。  
  
-   セットアップの実行に使用するユーザー アカウントは、ローカルの Administrators グループのメンバーである必要があります。また、レポート サーバー データベースをホストする [!INCLUDE[ssDE](../../includes/ssde-md.md)] インスタンス上のデータベースにアクセスする権限と、そのデータベースを作成する権限が必要です。  
  
-   セットアップでは、既定値を使用して、レポート サーバーとレポート マネージャーにアクセスするための URL を予約できる必要があります。 ここでの既定値とは、ポート 80、強いワイルドカード、および **ReportServer_\<***instance_name***>** と **Reports_\<***instance_name***>** の形式の仮想ディレクトリ名です。  
  
-   セットアップでは、既定値を使用してレポート サーバー データベースを作成できる必要があります。 ここでの既定値とは、 **ReportServer** と **ReportServerTempDB**です。 以前のインストールのデータベースが既に存在する場合は、ネイティブ モードの既定の構成のセットアップでレポート サーバーを構成できないため、セットアップはブロックされます。 セットアップのブロックを解除するには、データベースの名前を変更するか、データベースを移動または削除する必要があります。  
  
 コンピューターで、既定インストールの要件のうち満たされていないものがある場合は、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] をファイルのみのモードでインストールし、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成マネージャーを使用してセットアップの完了後に構成する必要があります。  
  
 既定のインストールを続行できるようにするためだけにコンピューターを再構成しないでください。 再構成の作業には数時間かかる可能性があり、時間を節約できるというこのインストール オプションの利点が実質的に失われます。 このような場合は、ファイルのみのモードで [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] をインストールし、特定の値を使用するようにレポート サーバーを構成することをお勧めします。  
  
##  <a name="bkmk_defaultURLreservations"></a> 既定の URL 予約  
 URL 予約は、プレフィックス、ホスト名、ポート、および仮想ディレクトリで構成されます。  
  
|要素|説明|  
|----------|-----------------|  
|Prefix|既定のプレフィックスは HTTP です。 以前に SSL (Secure Sockets Layer) 証明書をインストールした場合は、HTTPS プレフィックスを使用する URL 予約がセットアップで作成されます。|  
|ホスト名|既定のホスト名は、強いワイルドカード (+) です。 レポート サーバーが、 http:// を含め、コンピューターに解決されるあらゆるホスト名の指定のポートですべての HTTP 要求を受け入れることを指定します\<computername >/reportserver、 http://localhost/reportserver 、または http://\< IPAddress >/reportserver です。|  
|Port|既定のポートは 80 です。 80 以外のポートを使用する場合は、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Web アプリケーションをブラウザー ウィンドウで開くときに、そのポートを URL に明示的に追加する必要があるので注意してください。|  
|仮想ディレクトリ|既定では、reportserver _ の形式で仮想ディレクトリが作成\<*instance_name*> レポート サーバー Web サービスの場合は reports _\<*instance_name*>レポート マネージャー。 レポート サーバー Web サービスの既定の仮想ディレクトリは、 **reportserver**です。 レポート マネージャーの既定の仮想ディレクトリは、 **reports**です。|  
  
 完全な URL 文字列の例を次に示します。  
  
-   http://+:80/reportserver は、レポート サーバーへのアクセスを提供します。  
  
-   http://+:80/reports 、レポート マネージャーへのアクセスを提供します。  
  
##  <a name="bkmk_installwithwizard"></a> SQL Server のインストール ウィザードによるネイティブ モードをインストールします。  
 次に示すのは、SQL Server インストール ウィザードで選択する  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 固有の手順とオプションです。 ここでは、インストール ウィザードに表示されるそれぞれのページではなく、ネイティブ モードのインストールに含まれる [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 関連のページについてのみ説明します。  
  
1.  **[セットアップ ロール]** ページで、 **[SQL Server 機能のインストール]** を選択します。  
  
     ![セットアップ ロールの SQL Server 機能のインストール](../../../2014/sql-server/install/media/rs-setuprole.gif "セットアップ ロールの SQL Server 機能のインストール")  
  
2.  **[機能の選択]** ページで、次のオプションを選択します。  
  
    -   **[データベース エンジン サービス]** (データベース エンジンのインスタンスがまだインストールされていない場合)。  
  
    -   **Reporting Services-ネイティブ**します。  
  
    -   **管理ツール - 基本**します。 管理ツールは必須ではありませんが、その他の管理ツールがインストールされていない場合に推奨されています。 既定の構成オプションが機能しているレポート サーバーになりますが、構成オプションを変更したい場合があります。 [個人用レポート] などのいくつかのオプションで管理します。 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]  
  
     ![機能の選択での SSRS ネイティブ モードの選択](../../../2014/sql-server/install/media/rs-setupfeatureselection-native-withcircles.gif "機能の選択での SSRS ネイティブ モードの選択")  
  
3.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のサブスクリプション機能を使用する場合は、 **[サーバーの構成]** ページで、SQL Server エージェントのスタートアップの種類が **[自動]** に構成されていることを確認する必要があります。  
  
4.  **[Reporting Services の構成]** ページで、 **[インストールと構成]** を選択します。  
  
     ![SSRS ネイティブ モードの構成](../../../2014/sql-server/install/media/rs-setupconfiguration-native-with-circles.gif "SSRS ネイティブ モードの構成")  
  
5.  SQL Server インストール ウィザードの完了後、次の基本的な手順を使用して、既定のネイティブ モードのインストールを確認します。  
  
    -   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成マネージャーを開いて、レポート サーバーに接続できることを確認します。  
  
    -   管理者特権を使用してブラウザーを開き、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] レポート マネージャーに接続します。たとえば、「 `http://loclahost/Reports`」と入力します。  
  
    -   管理者特権を使用してブラウザーを開き、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] レポート サーバー ページにアクセスします。 例:  `http://loclahost/ReportServer`  
  
 詳細については、次の 2 つのトピックのネイティブ モードに関する説明を参照してください。  
  
 [Verify a Reporting Services Installation](../../reporting-services/install-windows/verify-a-reporting-services-installation.md)  
  
 [Reporting Services インストール時の問題解決](../../reporting-services/install-windows/troubleshoot-a-reporting-services-installation.md)  
  
##  <a name="bkmk_commandline"></a> コマンドラインを使用したネイティブ モードをインストールします。  
 次の例には、既定の構成に必要な [!INCLUDE[ssDE](../../includes/ssde-md.md)] サービスが示されています。  
  
```  
setup /q /ACTION=install /FEATURES=SQL,RS,TOOLS /INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="BUILTIN\ADMINISTRATORS"   
/RSSVCACCOUNT="NT AUTHORITY\NETWORK SERVICE" /SQLSVCACCOUNT="NT AUTHORITY\NETWORK SERVICE" /AGTSVCACCOUNT="NT AUTHORITY\NETWORK   
SERVICE" /RSSVCSTARTUPTYPE="Manual" /RSINSTALLMODE="DefaultNativeMode"  
```  
  
 詳細と例については、次を参照してください[コマンド プロンプト インストールの Reporting Services SharePoint モードとネイティブ モード](../../reporting-services/install-windows/install-reporting-services-at-the-command-prompt.md)と[コマンド プロンプトから SQL Server 2014 のインストール。](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)  
  
## <a name="see-also"></a>参照  
 [Reporting Services インストール時の問題解決](../../reporting-services/install-windows/troubleshoot-a-reporting-services-installation.md)   
 [Verify a Reporting Services Installation](../../reporting-services/install-windows/verify-a-reporting-services-installation.md)   
 [レポート サーバー サービス アカウントの構成 &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)   
 [レポート サーバー URL の構成 &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)   
 [レポート サーバー データベース接続の構成 &#40;SSRS 構成マネージャー&#41;](../../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)   
 [ファイルのみのインストール &#40;Reporting Services&#41;](../../reporting-services/install-windows/files-only-installation-reporting-services.md)   
 [レポート サーバーの初期化 &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md)   
 [ネイティブ モードのレポート サーバーでの SSL 接続の構成](../security/configure-ssl-connections-on-a-native-mode-report-server.md)   
 [レポート サーバー URL の構成 &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)   
 [を含めて、すべての](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)   
 [SQL Server 2014 のクイックスタート インストール](../../../2014/getting-started/quick-start-installation-of-sql-server-2014.md)  
  
  
