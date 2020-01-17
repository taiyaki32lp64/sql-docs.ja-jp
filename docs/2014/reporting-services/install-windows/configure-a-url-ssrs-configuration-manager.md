---
title: URL の構成 (SSRS 構成マネージャー) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- URL access [Reporting Services], syntax
ms.assetid: 851e163a-ad2a-491e-bc1e-4df92327092f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 617a4e01b3fd4f8dcbc6d929c2a26d483f2fa1ec
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66108861"
---
# <a name="configure-a-url--ssrs-configuration-manager"></a>URL の構成 (SSRS 構成マネージャー)
  レポート マネージャーやレポート サーバー Web サービスを使用するには、まず、各アプリケーションに対して少なくとも 1 つの URL を構成する必要があります。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] を "ファイルのみ" モードでインストールした場合 (インストール ウィザードの [レポート サーバー インストール オプション] ページで **[サーバーを構成せずにインストールする]** オプションを選択した場合) は、URL の構成は必須です。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] を既定の構成でインストールした場合は、各アプリケーションの URL が既に構成されています。 SharePoint 統合モードを使用するように構成されているレポート サーバーを利用している場合に [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ツールを使用してレポート サーバー Web サービスの URL を変更するには、SharePoint サーバーの全体管理でも URL を更新する必要があります。  
  
 URL を構成するには、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ツールを使用します。 URL のすべての部分をこのツールで定義します。 以前のリリースとは異なり、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 以降のバージョンの [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] アプリケーションへのアクセスにインターネット インフォメーション サービス (IIS) Web サイトは使用されません。  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] には、他の Web サービスや Web アプリケーションとのサイド バイ サイドの配置を含むほとんどの配置シナリオに対応する既定値が用意されています。 同じコンピューターで複数のレポート サーバー インスタンスを実行する場合に URL が競合するリスクを最小限に抑えられるように、既定の URL にはインスタンス名が組み込まれます。  
  
 このトピックでは、次のタスクの手順について説明します。  
  
-   レポート サーバー Web サービスの URL を作成する。  
  
-   レポート マネージャーの URL を作成する。  
  
-   URL の詳細プロパティを設定して追加の URL を定義する。  
  
 や相互運用性の問題の詳細 Url を格納して管理する方法の詳細については、次を参照してください[についての URL 予約と登録&#40;SSRS 構成マネージャー&#41; ](about-url-reservations-and-registration-ssrs-configuration-manager.md)と[レポートのインストール。サービスとインターネット インフォメーション サービスのサイド バイ サイドで&#40;SSRS ネイティブ モード&#41;](install-reporting-and-internet-information-services-side-by-side.md)で[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]オンライン ブックの「します。 Reporting Services でよく使用される URL の例については、このトピックの「 [URL の構成の例](#URLExamples) 」を参照してください。  
  
## <a name="prerequisites"></a>前提条件  
 URL の作成や変更を行う前に、次の点を確認してください。  
  
-   レポート サーバー コンピューターのローカル Administrators グループのメンバーとしてログインする必要があります。  
  
-   同じコンピューターに IIS 6.0 または 7.0 がインストールされている場合は、ポート 80 を使用する Web サイトの仮想ディレクトリの名前を確認してください。 Reporting Services の既定の仮想ディレクトリ名 ("Reports" および "ReportServer") を使用している仮想ディレクトリがあった場合は、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の URL を構成する際に別の仮想ディレクトリ名を選択します。  
  
-   URL は、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ツールを使用して構成する必要があります。 システム ユーティリティを使用したり、 RSReportServer.config ファイルの `URLReservations` セクションで直接 URL 予約を変更したりしないでください。 内部に格納されている基になる URL 予約と、RSReportServer.config ファイルに格納されている URL 設定の両方を更新し、同期を維持するためには、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ツールを使用する必要があります。  
  
-   レポートがあまり使用されない時間に行うようにしてください。 URL 予約を変更するたびに、レポート サーバー Web サービスとレポート マネージャーのアプリケーション ドメインの再利用が行われる可能性があります。  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]の URL の構成の概要については、「[レポート サーバー URL の構成 &#40;SSRS 構成マネージャー&#41;](configure-report-server-urls-ssrs-configuration-manager.md)」を参照してください。  
  
### <a name="to-configure-a-url-for-the-report-server-web-service"></a>レポート サーバー Web サービスの URL を構成するには  
  
1.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ツールを起動して、ローカル レポート サーバー インスタンスに接続します。  
  
2.  **[Web サービス URL]** をクリックします。  
  
3.  仮想ディレクトリを指定します。 仮想ディレクトリ名によって、要求を受信するアプリケーションが識別されます。 IP アドレスとポートは複数のアプリケーションで共有される可能性があるため、どのアプリケーションが要求を受信するのかを仮想ディレクトリ名で指定します。  
  
     要求が確実に目的の宛先に届くように、仮想ディレクトリ名には一意の値を指定する必要があります。 この値は必須です。 大文字と小文字は区別されません。 仮想ディレクトリ名と [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] アプリケーションのインスタンスは一対一に対応しています。 同じアプリケーション インスタンスへの URL を複数作成する場合は、すべての URL で同じ仮想ディレクトリ名を使用する必要があります。  
  
     レポート サーバー Web サービスの既定の仮想ディレクトリ名は、 **ReportServer**です。  
  
4.  ネットワーク上のレポート サーバー コンピューターを一意に識別する IP アドレスを指定します。 ホスト ヘッダーを指定したり、同じアプリケーション インスタンスに対して追加の URL を定義したりする場合は、 **[詳細設定]** をクリックする必要があります。 URL の詳細プロパティを設定する方法については、このトピックで後ほど説明します。 詳細プロパティを設定しない場合は、 **[Web サービス URL]** ページを使用して値を次の中から選択します。  
  
    -   **[すべて割り当て]** は、レポート サーバー アプリケーションを指す URL に、コンピューターに割り当てられている IP アドレスをどれでも使用できることを示します。 コンピューターに割り当てられている IP アドレスに対してドメイン ネーム サーバーによって解決されるわかりやすいホスト名 (コンピューター名など) も、この値の対象に含まれます。 これは、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] URL の既定値です。  
  
    -   **[すべて未割り当て]** は、他のアプリケーションによって処理されていない要求をレポート サーバーがすべて受信することを示します。 このオプションは選択しないことをお勧めします。 このオプションを選択すると、レポート サーバーに送信した要求が、より強力な URL 予約を持つ別のアプリケーションによって受信されてしまう可能性があります。  
  
    -   **[127.0.0.1]** は、localhost にアクセスする場合に使用する IPv4 アドレスです。 この値は、レポート サーバー コンピューターでのローカル管理をサポートします。 この値のみを選択すると、レポート サーバー コンピューターにローカルにログオンしているユーザーだけがアプリケーションにアクセスできるようになります。  
  
    -   **[::1]** は、IPv6 形式のループバック アドレスです。  
  
    -   特定の IP アドレスもこの一覧に表示されます。 IP アドレスは、IPv4 形式および IPv6 形式で指定できます。 "*nnn.nnn.nnn.nnn* " は、コンピューターのネットワーク アダプター カードの 32 ビット IPv4 アドレスです。 IPv6 アドレスは、コロンで区切られた 8 つの 4 バイト フィールドから成る 128 ビットのアドレスです \<prefix>:*nnnn:nnnn:nnnn:nnnn:nnnn:nnnn*。  
  
         複数のカードがある場合や、ネットワークで IPv4 と IPv6 の両方のアドレスがサポートされている場合は、複数の IP アドレスが表示されます。 1 つの IP アドレスのみを選択すると、アプリケーション アクセスがその IP アドレス (およびドメイン ネーム サーバーによってそのアドレスにマップされるホスト名) に限定されます。 localhost を使用してレポート サーバーにアクセスすることはできません。また、レポート サーバー コンピューターにインストールされている他のネットワーク アダプター カードの IP アドレスは使用できません。 通常、この値を選択するのは、明確な IP アドレスやホスト名を指定する複数の URL 予約 (イントラネット接続に使用するネットワーク アダプター カード用と外部接続に使用するネットワーク アダプター カード用など) を構成する場合です。  
  
5.  ポートを指定します。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] および Windows Server 2008 の [!INCLUDE[wiprlhlong](../../includes/wiprlhlong-md.md)] では、ポート 80 が既定のポートになっています。これは、他のアプリケーションとポートを共有できるためです。 カスタム ポート番号を使用する場合は、レポート サーバーへのアクセスに使用する URL で常にその番号を指定する必要があることに注意してください。 使用可能なポートを見つけるには、次の方法を使用できます。  
  
    -   コマンド プロンプトで次のコマンドを入力し、使用されている TCP ポートの一覧を取得します。  
  
         `netstat -a -n -p tcp`  
  
    -   Microsoft サポート技術情報の「 [TCP/IP ポートの割り当てについて](https://support.microsoft.com/kb/174904)」を読んで、TCP ポートの割り当てと、Well Known ポート (0 ～ 1023)、予約済みポート (1024 ～ 49151)、および動的/プライベート ポート (49152 ～ 65535) の違いについて確認します。  
  
    -   Windows ファイアウォールを使用している場合はポートを開く必要があります。 手順については、「 [Configure a Firewall for Report Server Access](../report-server/configure-a-firewall-for-report-server-access.md)」を参照してください。  
  
6.  まだ確認していない場合は、使用する予定の名前と同じ名前の仮想ディレクトリが IIS にないことを確認します (IIS がインストールされている場合)。  
  
7.  コンピューターに SSL 証明書がインストールされている場合は、ここでその証明書を選択して URL をバインドすることができます。  
  
8.  SSL 証明書を選択する場合は、必要に応じてカスタム ポートを指定できます。 既定のポートは 443 ですが、使用可能なポートをどれでも使用できます。  
  
9. **[適用]** をクリックして URL を作成します。  
  
10. ページの **[URL]** セクションでリンクをクリックして URL をテストします。 URL をテストするには、先にレポート サーバー データベースを作成して構成する必要があります。 手順については、「[ネイティブ モード レポート サーバー データベースの作成 &#40;SSRS 構成マネージャー&#41;](ssrs-report-server-create-a-native-mode-report-server-database.md)」を参照してください。  
  
11. さらに、SharePoint 統合モードを使用するようにレポート サーバーが構成されている場合は、SharePoint サーバーの全体管理でレポート サーバー Web サービスの URL を構成します。 SharePoint サーバーの全体管理でレポート サーバー Web サービスの URL を更新する方法の詳細については、次を参照してください[レポート サーバーの構成と管理&#40;Reporting Services SharePoint モード&#41;](../configure-administer-report-server-reporting-services-sharepoint-mode.md)と。[Reporting Services レポート サーバー &#40;SharePoint モード&#41;](../reporting-services-report-server-sharepoint-mode.md)します。  
  
### <a name="to-create-a-url-reservation-for-report-manager"></a>レポート マネージャーの URL 予約を作成するには  
  
1.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ツールを起動して、レポート サーバー インスタンスに接続します。  
  
2.  **[レポート マネージャー URL]** をクリックします。  
  
3.  仮想ディレクトリを指定します。 レポート マネージャーは、レポート サーバー Web サービスと同じ IP アドレスとポートでリッスンします。 別のレポート サーバー Web サービスを指すようにレポート マネージャーを構成した場合は、RSReportServer.config ファイルでレポート マネージャーの URL 設定を変更する必要があります。 手順については、次を参照してください。[レポート マネージャーの構成&#40;ネイティブ モード&#41;](../report-server/configure-web-portal.md)で[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]オンライン ブックの「します。  
  
4.  SSL 証明書がインストールされている場合は、その証明書を選択して、レポート マネージャーへの要求をすべて HTTPS でルーティングするように指定できます。  
  
     SSL 証明書を選択する場合は、必要に応じてカスタム ポートを指定できます。 既定のポートは 443 ですが、使用可能なポートをどれでも使用できます。  
  
5.  **[適用]** をクリックして URL を作成します。  
  
6.  ページの **[URL]** セクションでリンクをクリックして URL をテストします。  
  
## <a name="setting-advanced-properties-to-specify-additional-urls"></a>追加の URL を指定するための詳細プロパティの設定  
 別のポートやホスト名 (IP アドレスか、コンピューターに割り当てられている IP アドレスに対してドメイン ネーム サーバーによって解決されるホスト ヘッダー名) を指定して、レポート サーバー Web サービスやレポート マネージャーに対して複数の URL を予約することができます。 複数の URL を作成すると、同じレポート サーバー インスタンスへの異なるアクセス パスを設定できます。 たとえば、レポート サーバーへのイントラネット アクセスとエクストラネット アクセスを有効にする場合は、既定の URL をイントラネット アクセス用に使用して、追加の完全修飾ホスト名をエクストラネット アクセス用に使用することができます。  
  
-   http://myserver01/reportserver  
  
-   http://www.adventure-works.com/reportserver  
  
 同じアプリケーション インスタンスに対して複数の仮想ディレクトリ名を設定することはできません。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] アプリケーションの各インスタンスはそれぞれ 1 つの仮想ディレクトリ名にマップされます。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の複数のインスタンスが同じコンピューター上にある場合は、アプリケーションの仮想ディレクトリ名にインスタンス名を含めて、各要求が確実に目的の宛先に届くようにする必要があります。  
  
#### <a name="to-set-advanced-properties-on-a-url"></a>URL の詳細プロパティを設定するには  
  
1.  いずれかで、 **Web サービスの URL**または**レポート マネージャー URL** ] ページで [ **[詳細設定]** します。  
  
2.  **[追加]** をクリックします。  
  
3.  [IP アドレス] または [ホスト ヘッダー名] をクリックします。 ホスト ヘッダーを指定する場合は、DNS サービスで解決できる名前を指定してください。 公のドメイン名を指定する場合は、 http://www を含む URL 全体を指定します。  
  
4.  ポートを指定します。 カスタム ポートを指定する場合は、アプリケーションの URL に常にポート番号を含める必要があります。  
  
5.  **[OK]** をクリックします。  
  
6.  ブラウザー ウィンドウを開き、URL を入力して、URL をテストします。  
  
## <a name="urls-for-multiple-report-server-instances-on-the-same-computer"></a>同じコンピューター上の複数のレポート サーバー インスタンスの URL  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]の複数のインスタンスの URL を予約する場合は、名前の競合が発生しないように名前付け規則に従う必要があります。 詳細については、「[レポート サーバーの複数インスタンス配置における URL 予約 &#40;SSRS 構成マネージャー&#41;](url-reservations-for-multi-instance-report-server-deployments.md)」を参照してください。  
  
##  <a name="URLExamples"></a> URL の構成の例  
 レポート サーバーの URL の具体例を次に示します。  
  
-   http://localhost/reportserver  
  
-   http://localhost/reportserver_SQLEXPRESS  
  
-   http://sales01/reportserver  
  
-   http://sales01:8080/reportserver  
  
-   https://sales.adventure-works.com/reportserver  
  
-   https://www.adventure-works.com:8080/reportserver01  
  
 レポート マネージャーへアクセスするための URL では、上記と類似した形式が使用されます。通常この URL は、レポート サーバーをホストする Web サイトで作成されます。 レポート サーバーの URL と異なる点は仮想ディレクトリ名です。この例では **reports** が使用されますが、別の名前を使用することもできます。  
  
-   http://localhost/reports  
  
-   http://localhost/reports_SQLEXPRESS  
  
-   http://sales01/reports  
  
-   http://sales01:8080/reports  
  
-   https://sales.adventure-works.com/reports  
  
-   https://www.adventure-works.com:8080/reports  
  
## <a name="see-also"></a>参照  
 [Reporting Services 構成マネージャー &#40;ネイティブ モード&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md)   
 [レポート サーバー URL の構成 &#40;SSRS 構成マネージャー&#41;](configure-report-server-urls-ssrs-configuration-manager.md)  
  
  
