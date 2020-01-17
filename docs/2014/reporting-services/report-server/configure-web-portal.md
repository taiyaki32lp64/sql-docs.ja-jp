---
title: レポート マネージャー (ネイティブ モード) の構成 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Report Manager [Reporting Services], configuring
ms.assetid: e918986c-af15-48f6-8178-256aed829c6a
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: aff33ad5722ad4b08c1429b795607d1217b95e39
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66103936"
---
# <a name="configure-report-manager-native-mode"></a>レポート マネージャーの構成 (ネイティブ モード)
  レポート マネージャーは、Web フロント エンド アプリケーションであり、レポートの表示、レポート サーバー コンテンツの管理、およびネイティブ モードのレポート サーバーへのアクセス権の付与に使用されます。 レポート マネージャーは、レポート サーバー Web サービスと共に、同じレポート サーバー インスタンス内にインストールされます。また、セットアップ時に **[ネイティブ モードの既存の構成をインストールする]** を選択した場合は、必要に応じて構成できます。 レポート マネージャーはインストール後のタスクとしても構成できます。 このトピックでは、次のレポート マネージャーの構成シナリオについて説明します。  
  
-   [既定の URL を使用するレポート マネージャーの構成](#ConfigureRMURL)  
  
     レポート マネージャーは、ユーザーが Web ブラウザーでアクセスする Web アプリケーションです。 少なくとも、ブラウザー ウィンドウでアプリケーションを開く際に使用する URL を定義する必要があります。 URL はホスト名、ポート、および仮想ディレクトリで構成されます。 この URL の既定値には、レポート サーバー Web サービスの URL 用に定義したホスト名とポートの値に加えて、 **レポート** の仮想ディレクトリ名が含まれます。 名前付きインスタンスを使用している場合、仮想ディレクトリは **reports_instance**になります ( **instance** の箇所には、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] インスタンスの名前が入ります)。  
  
-   **リモート コンピューターからのレポート マネージャーの実行**。 ネットワークの構成によっては、コンピューターのポート 80 を有効にして、レポート マネージャーによる要求を許可する必要があります。  
  
    > [!TIP]  
    >  リモート コンピューター上のレポート マネージャーにアクセスしようとして、ブラウザーに接続エラー メッセージが返される場合、一般的な原因はファイアウォールの設定です。 詳細については、「 [レポート サーバー アクセスに対するファイアウォールの構成](configure-a-firewall-for-report-server-access.md)」をご覧ください。  
  
     必要に応じて、両方のコンピューターでポート 80 を有効にし、そのポートを経由する要求を許可します。 詳細については、「 [レポート サーバー アクセスに対するファイアウォールの構成](configure-a-firewall-for-report-server-access.md)」をご覧ください。  
  
-   [特定のレポート サーバーの URL を使用するレポート マネージャーの構成](#ConfigureSpecificURL)  
  
     既定では、レポート マネージャーは、同じレポート サーバー インスタンスで実行されているレポート サーバー Web サービスに接続します。 レポート マネージャーは、レポート サーバー Web サービスの URL を使用して接続を確立します。 レポート サーバー Web サービス用に複数の URL を定義している場合、レポート マネージャーは最後に定義した URL を使用します。 ただし配置によっては、レポート マネージャーが Web サービスに接続する際に、常に静的 URL を使用しなければならない場合があります。 このような接続が必要になる状況として、特定のポートや IP アドレスに対してパケット フィルターを構成しており、レポート サーバーへ接続するときは必ず定義したフィルター ルールを適用する場合などが例として挙げられます。  
  
-   [リモート レポート サーバーを使用するレポート マネージャーの構成](#ConfigureRemoteRS)  
  
     既定では、レポート マネージャーは、同じレポート サーバー インスタンス内で実行されるレポート サーバー Web サービスへのフロント エンド アクセスを提供します。ただし、Web サービスとレポート マネージャーを個別のプロセスで実行する場合、または各サーバーにサーバー アクセスを個別に構成する場合 (たとえば、レポート マネージャーをエクストラネット接続またはインターネット接続でユーザーに配置し、レポート サーバーとレポート マネージャーの間にファイアウォールを設定する場合) は、リモートのレポート サーバー Web サービスにレポート マネージャーを接続するよう構成することができます。  
  
-   [スタイルのカスタマイズおよびアプリケーションのタイトルのカスタマイズ](#ModifyTitle)  
  
     レポート マネージャー、HTML レポート ビューアー、およびレポート ツール バーは、スタイルを変更したり、レポート マネージャーに表示されるアプリケーションのタイトルを編集したりすることにより、限られた範囲でカスタマイズできます。  
  
-   [レポート マネージャーの無効化](#DisableRM)  
  
     ネイティブ モードを使用する [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] インスタンスをインストールする場合、レポート マネージャーは既定で有効になっています。 ただし、同等の機能を備えたカスタムのフロント エンド アプリケーションがある場合、SOAP インターフェイスまたは URL アクセス インターフェイスのみを使用してレポート サーバーにアクセスする場合、あるいは別のレポート サーバー インスタンスのレポート マネージャーを使用する場合は、レポート マネージャーを無効にすることができます。  
  
## <a name="prerequisites"></a>前提条件  
 レポート マネージャーを使用するには、次の条件を満たす必要があります。  
  
-   最小限の構成が行われているレポート サーバーが必要です。 レポート サーバーの最小限の構成の詳細については、「[レポート サーバーの構成 &#40;Reporting Services ネイティブ モード&#41;](configure-a-report-server-reporting-services-native-mode.md)」を参照してください。  
  
-   レポート サーバーはネイティブ モードで動作する必要があります。 レポート マネージャーは、SharePoint 統合モード用に構成されているレポート サーバーと併用できません。 SQL Server 2012 では、レポート サーバーを別のモードに切り替えることはできません。 環境で使用しているレポート サーバーの種類を変更するには、目的のモードのレポート サーバーをインストールした後、新しいレポート サーバーにレポート アイテムをコピーまたは移動する必要があります。 このプロセスは、一般的には "移行" と呼ばれます。 移行に必要な手順は、移行先のモードと移行元のバージョンによって異なります。 詳細については、「 [Upgrade and Migrate Reporting Services](../install-windows/upgrade-and-migrate-reporting-services.md)」を参照してください。  
  
-   また、Internet Explorer 7.0 以降 (スクリプト機能オン) も必要です。 詳細については、次を参照してください。 [Reporting Services と Power View のブラウザー サポートの計画&#40;Reporting Services 2014&#41;](../browser-support-for-reporting-services-and-power-view.md)します。  
  
##  <a name="ConfigureRMURL"></a> 既定の URL を使用するレポート マネージャーの構成  
 既定では、レポート マネージャーの URL は一意の仮想ディレクトリ名に加えて、同じインスタンスで実行されているレポート サーバー Web サービス用に定義されているポートとホスト名で構成されます。 ほとんどの場合、ホスト名はレポート サーバー コンピューターのネットワーク名ですが、そのコンピューターを解決する IP アドレスまたはホスト ヘッダーである場合もあります。 既定の URL を使用するようにレポート マネージャーを構成するには、 **構成ツールの** [レポート マネージャー URL] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ページを使用します。  
  
#### <a name="to-configure-the-default-report-manager-url-and-virtual-directory"></a>既定のレポート マネージャー URL と仮想ディレクトリを構成するには  
  
1.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ツールを起動して、レポート サーバー インスタンスに接続します。  
  
2.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ツールで、 **[レポート マネージャー URL]** をクリックして、URL を構成するページを開きます。  
  
3.  レポート マネージャーの一意の仮想ディレクトリ名を入力します。  
  
4.  **[適用]** をクリックします。  
  
5.  [!INCLUDE[wiprlhlong](../../includes/wiprlhlong-md.md)] または Windows Server 2008 を使用している場合は、レポート マネージャーを使用する前に追加の手順が必要になることがあります。 詳細については、「 [ローカル管理用のネイティブ モードのレポート サーバー &#40;SSRS&#41; の構成](configure-a-native-mode-report-server-for-local-administration-ssrs.md)。  
  
##  <a name="ConfigureSpecificURL"></a> 特定のレポート サーバーの URL を使用するレポート マネージャーの構成  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ツールで URL を構成すると、レポート マネージャーは、同じサーバー インスタンス内で実行されるレポート サーバー用の新しい URL や更新された URL を自動的に検出し、これを使用します。 すべてのレポート サーバー要求に 1 つの静的 URL を使用することが必要な配置では、RSReportServer.config ファイルでその URL を指定できます。  
  
#### <a name="to-configure-a-static-report-server-url"></a>レポート サーバーの静的 URL を構成するには  
  
1.  テキスト エディターで **RSReportServer.config** ファイルを開きます。 既定では、\Program Files\Microsoft SQL Server\MSRS12.\<*instancename*>\Reporting Services\ReportServer にあります。  
  
2.  `ReportServerURL` を探します。  
  
3.  レポート サーバー インスタンスの URL に置き換えます。  
  
4.  変更を保存してファイルを閉じます。  
  
 構成ファイルの詳細については、次を参照してください。 [Reporting Services の構成ファイルを変更&#40;RSreportserver.config&#41; ](modify-a-reporting-services-configuration-file-rsreportserver-config.md)と[RSReportServer Configuration File](rsreportserver-config-configuration-file.md)します。  
  
##  <a name="ConfigureRemoteRS"></a> リモート レポート サーバーを使用するレポート マネージャーの構成  
 レポート マネージャーとレポート サーバーを異なるコンピューターに配置する配置構成では、2 つの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]を個別にインストールする必要があります。 レポート マネージャーは、レポート サーバー サービスに組み込まれているため、単独でインストールすることはできません。 レポート マネージャーを別のコンピューター上で独自のプロセス内で実行する場合は、2 番目のレポート サーバーをインストールする必要があります。 両方のサーバー インスタンスは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] レポート サーバーであることが必要です。  
  
#### <a name="to-connect-report-manager-to-a-remote-report-server-instance"></a>レポート マネージャーをリモート レポート サーバー インスタンスに接続するには  
  
1.  2 つのレポート サーバー インスタンスをインストールします。  
  
2.  レポート サーバーをホストする最初のインストールを構成します。  
  
    1.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ツールを起動します。  
  
    2.  **[Web サービス URL]** をクリックし、レポート サーバーのホスト名、ポート、および仮想ディレクトリを構成します。  
  
    3.  **[データベース]** をクリックし、レポート サーバー データベースを構成します。  
  
3.  レポート マネージャーをホストする 2 番目のインストールを構成します。  
  
    1.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ツールを起動します。  
  
    2.  **[レポート マネージャー URL]** をクリックし、レポート マネージャーの仮想ディレクトリ名を入力します。  
  
     データベースは構成しないでください。 また、URL のテストも行わないでください。  
  
4.  レポート マネージャーのコンピューター上で、リモート レポート サーバー インスタンスを指すように RSReportServer.config 内の構成設定を変更します。 起動時に、レポート マネージャーは構成ファイルを読み取り、レポート サーバーの URL を取得します。  
  
    1.  テキスト エディターで RSReportServer.config を開きます。 既定では、SQL Server\MSRS11 \Program Files\Microsoft になります。\< *instancename*> \reporting します。  
  
    2.  `ReportServerURL` を探します。  
  
    3.  リモート レポート サーバー インスタンスの URL に置き換えます。  
  
    4.  変更を保存してファイルを閉じます。  
  
5.  > [!TIP]  
    >  必要に応じて、両方のコンピューターでポート 80 を有効にし、そのポートを経由する要求を許可します。 詳細については、「 [レポート サーバー アクセスに対するファイアウォールの構成](configure-a-firewall-for-report-server-access.md)」をご覧ください。  
  
6.  レポート サーバーを再起動します。  
  
7.  ブラウザー ウィンドウでレポート マネージャーを開きます。 レポート マネージャーが既に開いている場合は、ブラウザーを更新して、レポート マネージャーがリモート サーバーに接続されていることを確認します。 ターゲット サーバーの内容を確認してください。  
  
8.  使用していないサーバー機能を無効にします。  
  
    -   レポート マネージャーのコンピューターで、`WebServiceAndHTTPAccessEnabled` および `ScheduleEventsAndReportDeliveryEnabled` を無効にします。  
  
    -   レポート サーバーのコンピューターで、`ReportManagerEnabled` を無効にします。  
  
 機能を無効にするには、「 [Reporting Services 機能の有効化と無効化](turn-reporting-services-features-on-or-off.md)」を参照してください。  
  
##  <a name="ModifyTitle"></a> スタイルのカスタマイズまたはアプリケーションのタイトルのカスタマイズ  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] では、レポート マネージャーのスタイル シートのカスタマイズをサポートしていません。 ただし、Web 開発に関する専門知識を持つユーザーであれば、各自の責任でスタイルを変更することができます。 スタイル情報を含むファイルの詳細については、「 [HTML ビューアーとレポート マネージャーのスタイル シートのカスタマイズに関する記事 (ページ、サイトなどの場合もあります)](../customize-style-sheets-for-html-viewer-and-report-manager.md)」を参照してください。  
  
 レポート マネージャーでは、アプリケーションのタイトルがページの上部に表示されます。 既定では、タイトルは **SQL Server Reporting Services**です。 このタイトルはカスタマイズできます。 タイトルを変更するには、レポート マネージャーの [サイトの設定] ページを使用します。 レポート マネージャーでアプリケーションの設定を変更する場合、[サイトの設定] ページでプロパティを設定するために、 **システム管理者** ロールが割り当てられている必要があります。 アプリケーションのタイトルを表示する場合は、 **システム ユーザー** ロールが割り当てられている必要があります。  
  
#### <a name="to-modify-application-title"></a>アプリケーションのタイトルを変更するには  
  
1.  レポート サーバーに対する **システム管理者** 権限が割り当てられたアカウントを使用してログオンします。  
  
2.  Internet Explorer を開きます。  
  
3.  レポート マネージャーの URL を入力します。 既定では、 http://\<**your-server-name**>/reports ですが、Reporting Services を名前付きインスタンスとしてインストールした場合、既定の URL は http://\<**your-server-name**>/reports\< **_instancename**> になります。  
  
4.  **[サイトの設定]** をクリックします。  
  
5.  **[全般]** タブの **[名前]** で、 **SQL Server Reporting Services** を別の名前に置き換えます。  
  
6.  **[適用]** をクリックします。  
  
##  <a name="DisableRM"></a> Turn Off Report Manager  
 レポート マネージャーを無効にできるのは、同等の機能を備えたカスタム アプリケーションがある場合、または別のサービス インスタンスのレポート マネージャー アプリケーションを使用している場合です。 レポート マネージャーを無効にするには、RSReportServer.config ファイルを変更します。  
  
#### <a name="to-turn-off-report-manager"></a>レポート マネージャーを無効にするには  
  
1.  テキスト エディターで RSReportServer.config ファイルを開きます。 既定では、SQL Server\MSRS11 \Program Files\Microsoft になります。\< *instancename*> \reporting します。  
  
2.  **IsReportManagerEnabled**を探します。  
  
3.  値を **False**に設定します。  
  
4.  変更を保存してファイルを閉じます。  
  
 構成ファイルの編集の詳細については、「[Reporting Services の構成ファイル &#40;RSreportserver.config&#41; の変更](modify-a-reporting-services-configuration-file-rsreportserver-config.md)」を参照してください。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の機能を無効にするには、「[Reporting Services 機能の有効化と無効化](turn-reporting-services-features-on-or-off.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [レポート マネージャー &#40;SSRS ネイティブ モード&#41;](../report-manager-ssrs-native-mode.md)   
 [Reporting Services と Power View のブラウザー サポートの計画&#40;Reporting Services 2014&#41;](../browser-support-for-reporting-services-and-power-view.md)   
 [URL の構成 &#40;SSRS 構成マネージャー&#41;](../install-windows/configure-a-url-ssrs-configuration-manager.md)   
 [Reporting Services のインストール状態の検証](../install-windows/verify-a-reporting-services-installation.md)   
 [HTML ビューアーとレポート マネージャーのスタイル シートのカスタマイズに関する記事 (ページ、サイトなどの場合もあります)](../customize-style-sheets-for-html-viewer-and-report-manager.md)   
 [Reporting Services 機能の有効化と無効化](turn-reporting-services-features-on-or-off.md)   
 [Reporting Services ネイティブ モードのレポート サーバーの管理](manage-a-reporting-services-native-mode-report-server.md)   
 [RSReportServer 構成ファイル](rsreportserver-config-configuration-file.md)   
 [ローカル管理用のネイティブ モードのレポート サーバー (SSRS) の構成](configure-a-native-mode-report-server-for-local-administration-ssrs.md)  
  
  
