---
title: レポート サーバー URL の構成 (SSRS 構成マネージャー) | Microsoft Docs
ms.date: 05/18/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Report Server Windows service, virtual directories
- report servers [Reporting Services], virtual directories
- virtual directories [Reporting Services]
ms.assetid: a0134ef0-086c-443e-93b9-7213a3d76393
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 823df0704b07657b5f7493c03fb14158b73263a2
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2019
ms.locfileid: "73594075"
---
# <a name="configure-report-server-urls--ssrs-configuration-manager"></a>レポート サーバー URL の構成 (SSRS 構成マネージャー)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]では、レポート サーバー Web サービスと [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)]へのアクセスに URL が使用されます。 どちらのアプリケーションを使用する場合も、事前に Web サービスと [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)]それぞれに 1 つ以上の URL を構成する必要があります。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] では、両方のアプリケーションの URL に既定値が用意されています。この既定値は、他の Web サービスや Web アプリケーションとのサイド バイ サイドの配置をはじめとするほとんどの配置シナリオに有効です。  
  
-   既定の構成をインストールした場合は、既定値を使用して自動的に URL が作成されます。  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ツールを使用して URL を作成または変更する場合は、URL の既定値をそのまま使用するか、カスタム値を指定できます。 URL を定義すると URL のテスト リンクがページに表示されるので、指定した設定が有効な接続であるかどうかを即座に確認できます。 URL の構成とテストの手順については、「 [URL の構成 &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)へのアクセスに URL が使用されます。  
  
## <a name="defining-a-report-server-url"></a>レポート サーバーの URL の定義  
 URL は、ネットワーク上のレポート サーバー アプリケーション インスタンスの場所を厳密に特定します。 レポート サーバーの URL を作成するときは、次の要素を指定する必要があります。  
  
|要素|[説明]|  
|----------|-----------------|  
|ホスト名|TCP/IP ネットワークでは、IP アドレスを使用してネットワーク上のデバイスを一意に識別します。 コンピューターにインストールされているネットワーク アダプター カードごとに、物理 IP アドレスが存在します。 IP アドレスがホスト ヘッダーに解決される場合、ホスト ヘッダーを指定できます。 レポート サーバーを企業ネットワークに配置している場合は、コンピューターのネットワーク名を使用できます。|  
|Port|TCP ポートはデバイス上のエンドポイントです。 レポート サーバーは、指定されたポートで要求をリッスンします。|  
|仮想ディレクトリ|1 つのポートが複数の Web サービスまたはアプリケーションで共有されていることがよくあります。 このため、レポート サーバーの URL には、要求を受け取るアプリケーションに対応する仮想ディレクトリが必ず含まれています。 同じ IP アドレスとポートでリッスンする [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] アプリケーションごとに、一意の仮想ディレクトリ名を指定する必要があります。|  
|SSL 設定|コンピューターに以前にインストールした既存の SSL 証明書を使用するように、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の URL を構成できます。 詳細については、「 [ネイティブ モードのレポート サーバーでの SSL 接続の構成](../../reporting-services/security/configure-ssl-connections-on-a-native-mode-report-server.md)」を参照してください。|  
  
## <a name="default-urls"></a>既定の URL  
 レポート サーバーまたは [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] に URL を通じてアクセスする場合は、URL に IP アドレスではなくホスト名を指定します。 TCP/IP ネットワークでは、IP アドレスがホスト名 (またはコンピューターのネットワーク名) に解決されます。 既定値を使用して URL を構成した場合は、コンピューター名または localhost をホスト名として指定する URL を使用して、レポート サーバー Web サービスにアクセスできます。  
  
-   `https://<computername>/reportserver`  
  
-   `https://localhost/reportserver`  
  
 上記の URL の使用を可能にする設定を次の表に示します。 この表の既定値を使用することで、ホスト名を含んだ URL を通じてレポート サーバーに接続できるようになります。  
  
|要素|[値]|説明|  
|----------|-----------|-----------------|  
|IP アドレス (IP address)|すべて割り当て|ネットワーク上のドメイン ネーム サービスによって、URL のホスト名がコンピューターの IP アドレスに解決されます。 定義した URL に IP アドレスが指定されていれば、特定のホストに送られる要求は目的の宛先に届きます。|  
|Port|80|ポート 80 は、コンピューターにおける TCP/IP 接続の既定のポートです。 レポート サーバーはポート 80 でリッスンしているため、URL ではポート番号を省略できます。 別のポートを指定する場合は、URL 内でそのポートを指定する必要があります。|  
|仮想ディレクトリ|ReportServer|どちらの URL 例にも仮想ディレクトリ名が含まれていることに注目してください。 URL 定義をカスタマイズしない限り、アプリケーションの仮想ディレクトリ名を必ず URL 内に指定する必要があります。|  
  
> [!NOTE]  
>  基になる URL 予約により、任意の有効なホスト名を URL で使用できるようになります。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ツールでは、複数種類のホスト名を特定のレポート サーバー インスタンスに解決できるようにする構文を使用して、HTTP.SYS に URL 予約が作成されます。 URL 予約の詳細については、「 [URL の予約と登録について &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/about-url-reservations-and-registration-ssrs-configuration-manager.md)へのアクセスに URL が使用されます。  
  
## <a name="server-side-permissions-on-a-report-server-url"></a>レポート サーバーの URL に対するサーバー側の権限  
 各 URL エンドポイントに対する権限は、レポート サーバー サービス アカウントに排他的に付与されます。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の URL に送信された要求を受け付ける権限を持つのはこのアカウントのみです。 セットアップまたは [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ツールでサービス ID を構成すると、アカウントに対してアクセス制限付きの随意アクセス制御リスト (DACL) が作成され、管理されます。 サービス アカウントを変更した場合は、作成済みの URL 予約が [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ツールによってすべて更新され、新しいアカウント情報が反映されます。 詳細については、 [URL 予約構文 &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/url-reservation-syntax-ssrs-configuration-manager.md)へのアクセスに URL が使用されます。  
  
## <a name="authenticating-client-requests-sent-to-a-report-server-url"></a>レポート サーバーの URL に送信されたクライアント要求の認証  
 URL エンドポイントで既定でサポートされる認証の種類は Windows 認証です。 これは既定のセキュリティ拡張機能です。 カスタムまたはフォーム認証プロバイダーを実装している場合は、レポート サーバーの認証設定を変更する必要があります。 必要に応じて、Windows 認証の設定を、ネットワークで使用されている認証サブシステムに合わせて変更することもできます。 詳細については、「 [レポート サーバーでの認証](../../reporting-services/security/authentication-with-the-report-server.md)」を参照してください。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [URL の構成 &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)  
 このトピックでは、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ツールで URL 予約を設定および変更する方法について説明します。  
  
 [URL の予約と登録について &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/about-url-reservations-and-registration-ssrs-configuration-manager.md)  
 アプリケーションおよびレポートへのアクセスには URL が使用されます。 このトピックでは、アプリケーションの URL、既定の URL、および [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]での URL 予約と登録のしくみについて説明します。  
  
 [URL 予約構文 &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/url-reservation-syntax-ssrs-configuration-manager.md)  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] で使用される既定の URL 予約は、ほとんどのシナリオに有効です。 ただし、アクセスを制限する場合や、インターネットまたはエクストラネットにアクセスできるように配置を拡張する場合は、要件に合わせて設定をカスタマイズする必要があります。 このトピックでは、URL 予約の構文について説明し、各自の配置に合わせてカスタムの予約を作成する場合の推奨事項を示します。  
  
 [構成ファイル内の URL &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/urls-in-configuration-files-ssrs-configuration-manager.md)  
 RSReportServer.config ファイルには、URL 予約の複数のエントリと、 [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] およびレポート サーバーの電子メール配信で使用される URL が含まれています。 このトピックでは、URL 構成設定の違いを理解できるように、それらの設定について概要を説明します。  
  
 [レポート サーバーの複数インスタンス配置における URL 予約 &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/url-reservations-for-multi-instance-report-server-deployments.md)  
 1 台のコンピューターに複数の [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] インスタンスをインストールすると、URL 登録時に URL の重複が発生する可能性が高くなります。 このエラーを回避するには、このトピックの推奨事項に従ってインスタンス固有の URL 予約を作成します。  
  
## <a name="see-also"></a>参照  
 [URL の構成 &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md) 
