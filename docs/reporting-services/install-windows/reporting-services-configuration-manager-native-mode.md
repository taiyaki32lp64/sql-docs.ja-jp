---
title: Reporting Services 構成マネージャー (ネイティブ モード) | Microsoft Docs
ms.date: 09/20/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Reporting Services Configuration tool
- configuration options [Reporting Services]
- report servers [Reporting Services], configuring
- components [Reporting Services], Reporting Services Configuration tool
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 3df5a4c27e5c916d5a2c803d7bd4d40110aabb27
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2019
ms.locfileid: "73593780"
---
# <a name="reporting-services-configuration-manager-native-mode"></a>Reporting Services 構成マネージャー (ネイティブ モード)

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のネイティブ モード インストールを構成するには、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成マネージャーを使用します。 ファイルのみのインストール オプションを使用してレポート サーバーをインストールした場合は、構成マネージャーを使用して、サーバーを使用するための構成を行う必要があります。 既定の構成のインストール オプションを使用してレポート サーバーをインストールした場合は、構成マネージャーを使用して、セットアップ時に指定した設定の確認や変更を行うことができます。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成マネージャーでは、ローカルまたはリモートのレポート サーバー インスタンスを構成できます。

> [!NOTE]
> SharePoint と Reporting Services の統合は、SQL Server 2016 以降では使用できません。 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] リリース以降の [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成マネージャーは、SharePoint モードのレポート サーバーを管理できるように設計されていません。 SharePoint モードの管理や構成は、SharePoint サーバーの全体管理および PowerShell スクリプトを使用して行います。  
  
##  <a name="bkmk_scenarios"></a> Reporting Services 構成マネージャーを使用するシナリオ  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成マネージャーを使用すると、次のタスクを実行できます。  
  
-   レポート サーバー サービス アカウントの構成。 アカウントは最初にセットアップ時に構成されますが、パスワードの更新や使用するアカウントの変更を行う場合は、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成マネージャーで変更できます。  
  
-   URL の作成および構成。 レポート サーバーおよび [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)] は、URL でアクセスされる [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] アプリケーションです。 レポート サーバーの URL からは、レポート サーバーの SOAP エンドポイントにアクセスできます。 [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)] の URL は、 [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)] を開くために使用されます。また、1 つの URL を構成することも、アプリケーションごとに複数の URL を構成することもできます。  
  
-   レポート サーバー データベースの作成および構成。 レポート サーバーは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースを内部ストレージとして必要とする、ステートレス サーバーです。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成マネージャーを使用すると、レポート サーバー データベースを作成し、そのレポート サーバー データベースへの接続を構成できます。 必要なコンテンツが格納されている既存のレポート サーバー データベースを選択することもできます。  
  
-   ネイティブ モードのスケールアウト配置の構成。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] では、複数のレポート サーバー インスタンスで 1 つの共有レポート サーバー データベースを使用できるようにする配置トポロジをサポートします。 レポート サーバーをスケールアウト配置するには、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成マネージャーを使用して各レポート サーバーを共有レポート サーバー データベースに接続します。  
  
-   保存されている接続文字列や資格情報を暗号化する対称キーのバックアップ、復元、または置き換え。 サービス アカウントを変更する場合や、レポート サーバー データベースを別のコンピューターに移動する場合は、対称キーのバックアップが必要となります。  
  
-   自動実行アカウントを構成する。 このアカウントは、スケジュールされた操作でのリモート接続や、ユーザーの資格情報が利用できない場合に使用します。  
  
-   レポート サーバーの電子メールの構成。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] は、簡易メール転送プロトコル (SMTP) を使用してレポートまたはレポート処理通知を電子メールボックスに配信する、レポート サーバーの電子メール配信拡張機能を備えています。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成マネージャーでは、電子メール配信に使用する、ネットワーク上の SMTP サーバーまたはゲートウェイを指定できます。  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成マネージャーには、レポート サーバー コンテンツの管理、拡張機能の有効化、サーバーに対するアクセス権の付与を支援する機能はありません。 これには完全な配置が必要であり、拡張機能の有効化や既定値の変更には [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] を使用し、サーバーへのユーザー アクセス権の付与には Web ポータルを使用します。

##  <a name="bkmk_requirements"></a> 必要条件

[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成マネージャーはバージョン固有です。 このバージョンの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] と共にインストールされる [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーは、以前のバージョンの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]の構成には使用できません。 同じコンピューター上で古いバージョンと新しいバージョンの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] をサイド バイ サイドで実行している場合は、各バージョンに付属する Reporting Services 構成マネージャーを使用して、各インスタンスを構成する必要があります。  

[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成マネージャーを使用するには、次の準備が必要です。

- 構成対象のレポート サーバーをホストするコンピューターに対し、ローカルのシステム管理者権限が必要です。 リモート コンピューターを構成する場合、そのリモート コンピューターに対するローカルのシステム管理者権限も必要です。

- レポート サーバー データベースをホストするために使用される [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] に対し、データベースを作成する権限が必要です。

- 構成対象のレポート サーバー上で、Windows Management Instrumentation (WMI) サービスが有効化および実行されている必要があります。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成マネージャーは、レポート サーバーの WMI プロバイダーを使用して、ローカルおよびリモートのレポート サーバーに接続します。 リモートのレポート サーバーを構成する場合は、そのコンピューターでリモートの WMI アクセスが許可されている必要があります。 詳細については、「 [リモート管理用のレポート サーバーの構成](../../reporting-services/report-server/configure-a-report-server-for-remote-administration.md)」を参照してください。  

- リモートのレポート サーバー インスタンスに接続して構成するには、リモートの WMI (Windows Management Instrumentation) 呼び出しを有効にして Windows ファイアウォールを通過できるようにしておく必要があります。 詳細については、「 [リモート管理用のレポート サーバーの構成](../../reporting-services/report-server/configure-a-report-server-for-remote-administration.md)」を参照してください。

Reporting Services 構成マネージャーは、SQL Server Reporting Services をインストールするときに自動的にインストールされます。

##  <a name="bkmk_start_configuration_manager"></a> Reporting Services 構成マネージャーを起動するには

1.  使用している Microsoft Windows のバージョンに合わせて次の手順を使用します。

    - Windows のスタート画面から「 **Reporting** 」と入力し、検索結果から " **Reporting Services 構成マネージャー** " を選択します。

    - **[スタート]** を選択し、 **[すべてのプログラム]** 、 [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]、 **[構成ツール]** の順にポイントします。

         以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]からレポート サーバー インスタンスを構成する場合は、そのバージョンのプログラム フォルダーを開きます。 たとえば、 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] サーバー コンポーネントの構成ツールを開くには、[ [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)] ] ではなく [ [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ] をポイントします。

         **Reporting Services 構成マネージャー**を選択します。

2. **[Reporting Services 構成の接続]** ダイアログ ボックスが表示されたら、構成するレポート サーバー インスタンスを選択できます。 **[接続]** を選択します。

3. **[サーバー名]** ボックスに、レポート サーバー インスタンスがインストールされているコンピューターの名前を指定します。 ローカル コンピューターの名前が既定で表示されますが、リモート コンピューターにインストールされているレポート サーバーに接続する場合は、リモートの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスの名前を入力できます。

4. リモート コンピューターを指定する場合は、 **[検索]** を選択して接続を確立します。

5. **Report Server stance**で、構成する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] インスタンスを選択します。 この一覧には、このバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のレポート サーバー インスタンスのみが表示されます。 以前のバージョンの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]を構成することはできません。

6. **[接続]** を選択します。

## <a name="next-steps"></a>次の手順

[Web ポータル](../../reporting-services/web-portal-ssrs-native-mode.md)   
[Reporting Services ツール](../../reporting-services/tools/reporting-services-tools.md)   
[レポート サーバー データベース接続の構成](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md)   
[SQL Server 構成マネージャー](../../relational-databases/sql-server-configuration-manager.md)   
[レポート サーバーを構成および管理する](../../reporting-services/report-server/configure-and-administer-a-report-server-ssrs-native-mode.md)  

その他の質問 [Reporting Services のフォーラムに質問してみてください](https://go.microsoft.com/fwlink/?LinkId=620231)
