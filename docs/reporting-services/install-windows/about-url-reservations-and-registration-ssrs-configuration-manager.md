---
title: URL の予約と登録について (SSRS 構成マネージャー) | Microsoft Docs
ms.date: 06/20/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- URL reservations
- URL registration
- Report Server service, URL reservations
ms.assetid: c2c460c3-e749-4efd-aa02-0f8a98ddbc76
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: dba8913c5aa5fa0aa8d93dd1c4dd639f85ac3081
ms.sourcegitcommit: 3f2936e727cf8e63f38e5f77b33442993ee99890
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/21/2019
ms.locfileid: "67314038"
---
# <a name="about-url-reservations-and-registration--ssrs-configuration-manager"></a>URL の予約と登録について (SSRS 構成マネージャー)
  Reporting Services アプリケーションの URL は、HTTP.SYS の URL 予約として定義されます。 URL 予約は、Web アプリケーションへの URL エンドポイントの構文を定義します。 レポート サーバー上でアプリケーションを構成する際には、レポート サーバー Web サービスと Web ポータルの両方に対して URL 予約を定義します。 セットアップまたは [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ツールで URL を構成すると、自動的に URL 予約が作成されます。  
  
-   セットアップでは、既定値を使用して URL 予約が作成されます。 セットアップで既定の構成をインストールすると、2 つの URL が予約されます: レポート サーバー Web サービス用に 1 つと、Web ポータル用に 1 つです。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ツールを使用すると、URL をさらに追加したり、セットアップによって作成された既定の URL を変更したりできます。  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ツールでは、ツールの **[Web サービス URL]** ページまたは **[Web ポータル URL]** ページで指定した URL に基づいて URL 予約が作成されます。  
  
 いずれの場合も、さらに、レポート サーバー サービスへの URL に対する権限の割り当て、重複するインスタンスのチェック、および HTTP.SYS への URL 予約の追加が行われます。 HttpCfg.exe やその他のツールを使用して直接 Reporting Services の URL 予約を作成したり変更したりしないでください。 手順を省略したり無効な値を設定したりすると、診断や修正が困難な問題が発生する可能性があります。  
  
> [!NOTE]  
> HTTP.SYS は、ネットワーク要求をリッスンして要求キューにルーティングするオペレーティング システム コンポーネントです。 このリリースの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] では、HTTP.SYS によって、レポート サーバー Web サービスと Web ポータルの要求キューが作成され、管理されます。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] アプリケーションのホスティングやアクセスにインターネット インフォメーション サービス (IIS) は使用されなくなりました。 HTTP.SYS 機能の詳細については、「[HTTP Server API (HTTP サーバー API)](https://go.microsoft.com/fwlink/?LinkId=92652)」をご覧ください。  
  
##  <a name="ReportingServicesURLs"></a> Reporting Services の URL  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] では、以下のツール、アプリケーション、およびアイテムに URL を通じてアクセスできます。  
  
-   レポート サーバー Web サービス  
  
-   Web ポータル  
  
-   レポート サーバーにパブリッシュされたレポート  
  
 URL を指定できるその他のパブリッシュされるアイテム (共有データ ソースなど) には、URL を通じてスタンドアロンのアイテムとしてアクセスしないようにしてください。 これらのアイテムは、ブラウザー ウィンドウで表示しても意味のある形式で表示されません。  
  
> [!NOTE]  
> この記事では、レポート サーバーに保存されている特定のレポートへの URL アクセスについては説明していません。 これらのアイテムへの URL アクセスについて詳しくは、「[URL アクセスを使用したレポート サーバー アイテムへのアクセス](../../reporting-services/access-report-server-items-using-url-access.md)」をご覧ください。  
  
##  <a name="URLreservation"></a> URL の予約と登録  
 URL 予約は、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] アプリケーションへのアクセスに使用できる URL を定義します。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] では、レポート サーバー Web サービスと [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] の URL を HTTP.SYS で 1 つ以上予約して、サービスの起動時に登録します。 URL にパラメーターを追加することにより、Web サービスを通じてレポートを開くことができます。 予約と登録は、HTTP.SYS によって行われます。 詳細については、「[Namespace Reservations, Registration, and Routing (名前空間の予約、登録、およびルーティング)](https://go.microsoft.com/fwlink/?LinkId=92653)」をご覧ください。  
  
 *URL 予約* とは、Web アプリケーションへの URL エンドポイントを作成して HTTP.SYS に格納するプロセスです。 HTTP.SYS は、コンピューターで定義されているすべての URL 予約の共通リポジトリであり、URL 予約が一意であることを保証する一連の共通規則を定義します。  
  
 *URL の登録* は、サービスの起動時に行われます。 サービスが起動すると、要求キューが作成され、HTTP.SYS がそのキューへの要求のルーティングを開始します。 URL エンドポイントは、そのエンドポイントに転送される要求がキューに追加される前に登録される必要があります。 レポート サーバー サービスの起動時には、有効化されているすべてのアプリケーションに対して予約されているすべての URL が登録されます。 したがって、登録が行われるためには Web サービスが有効化されている必要があります。 ポリシー ベースの管理の Reporting Services のセキュリティ構成ファセットで **WebServiceAndHTTPAccessEnabled** プロパティを **False** に設定すると、Web サービスの URL がサービスの起動時に登録されません。  
  
 サービスを停止するか、Web サービスや [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] アプリケーション ドメインの再利用を行うと、URL の登録が解除されます。 サービスの実行中に URL 予約を変更すると、古い URL の登録を解除して新しい URL を使用できるようにするために、アプリケーション ドメインの再利用処理が直ちに行われます。  
  
 次の例は、URL 予約の概念と、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] アプリケーション用に使用される URL アドレスと URL 予約の関連付けを示しています。 URL 予約の構文が、アプリケーションへのアクセスに使用する URL とは異なる点に注目してください。  
  
|HTTP.SYS の URL 予約|[URL]|説明|  
|---------------------------------|---------|-----------------|  
|`https://+:80/reportserver`|`https://<computername>/reportserver`<br /><br /> `https://<IPAddress>/reportserver`<br /><br /> `https://localhost/reportserver`|この URL 予約では、ポート 80 でワイルドカード (+) を指定しています。 これにより、ポート 80 のレポート サーバー コンピューターに解決されるホストが指定されているすべての受信要求がレポート サーバー キューに送られます。 この URL 予約を使用すると、任意の数の URL を使用してレポート サーバーにアクセスできます。<br /><br /> ほとんどのオペレーティング システムでは、これが [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] レポート サーバーの既定の URL 予約です。|  
|`https://123.45.67.0:80/reportserver`|`https://123.45.67.0/reportserver`|この URL 予約では IP アドレスを指定しています。これは、ワイルドカードの URL 予約よりはるかに制限の厳しい URL 予約です。 レポート サーバーへの接続に使用できるのは、この IP アドレスを含む URL だけです。 この URL 予約を指定すると、`https://<computername>/reportserver` または `https://localhost/reportserver` でのレポート サーバーへの要求は失敗します。|  
  
##  <a name="DefaultURLs"></a> 既定の URL  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] を既定の構成でインストールすると、レポート サーバー Web サービスと [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)]の URL が自動的に予約されます。 これらの既定値は、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ツールで URL 予約を定義するときにも使用できます。 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] をインストールした場合や、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] を名前付きインスタンスとしてインストールした場合は、既定の URL にインスタンス名が含まれます。  
  
> [!IMPORTANT]  
> インスタンスの文字はアンダースコア文字 ( **_** ) です。  
  
 URL 予約にはポート番号が含まれます。 以下のオペレーティング システムでは、複数の Web アプリケーションで 1 つのポートを共有できます。  
  
-   [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2  
  
-   [!INCLUDE[win8srv](../../includes/win8srv-md.md)]  
  
-   [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]  
  
-   [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)]  
  
-   [!INCLUDE[win7](../../includes/win7-md.md)]  
  
-   [!INCLUDE[wiprlhlong](../../includes/wiprlhlong-md.md)]  
  
|インスタンスの種類|アプリケーション|既定の URL|HTTP.SYS の実際の URL 予約|  
|-------------------|-----------------|-----------------|----------------------------------------|  
|[既定のインスタンス]|レポート サーバー Web サービス|`https://\<servername>/reportserver`|`https://<servername>:80/reportserver`|  
|[既定のインスタンス]|Web ポータル|`https://<servername>/reportserver`|`https://<servername>:80/reportserver`|  
|[名前付きインスタンス]|レポート サーバー Web サービス|`https://<servername>/reportserver_<instancename>`|`https://<servername>:80/reportserver_<instancename>`|  
|[名前付きインスタンス]|Web ポータル|`https://<servername>/reports_<instancename>`|`https://<servername>:80/reports_<instancename>`|  
|SQL Server Express|レポート サーバー Web サービス|`https://<servername>/reportserver_SQLExpress`|`https://<servername>:80/reportserver_SQLExpress`|  
|SQL Server Express|Web ポータル|`https://<servername>/reports_SQLExpress`|`https://<servername>:80/reports_SQLExpress`|  
  
##  <a name="URLPermissionsAccounts"></a> Reporting Services の URL の認証とサービス ID  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の URL 予約では、URL 予約のアカウントが表示されます。 仮想サービス アカウントが、同じインスタンスで実行される [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] アプリケーション用に作成されるすべての URL に対して使用されます。
  
 
 既定のセキュリティが **RSWindowsNegotiate**であるため、匿名アクセスは無効になっています。 イントラネット アクセスの場合、レポート サーバーの URL ではネットワーク コンピューターの名前が使用されます。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] をインターネット接続用に構成する場合は、別の設定を使用する必要があります。 認証の詳細については、「[レポート サーバーでの認証](../../reporting-services/security/authentication-with-the-report-server.md)」をご覧ください。  
  
##  <a name="URLlocalAdmin"></a> ローカル管理用の URL  
 URL 予約に強いワイルドカードまたは弱いワイルドカードを指定した場合、`https://localhost/reportserver` または `https://localhost/reports` を使用できます。  
  
 `https://localhost` URL は、`https://127.0.0.1` として解釈されます。 URL 予約をコンピューター名や 1 つの IP アドレスに設定した場合は、ローカル コンピューターの 127.0.0.1 に対して追加の予約を作成しないと localhost を使用できません。 同様に、localhost や 127.0.0.1 がコンピューターで無効になっている場合も、その URL を使用できません。  
  
 [!INCLUDE[wiprlhlong](../../includes/wiprlhlong-md.md)]と [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] 以降には、誤ってプログラムが高度な特権で実行されるリスクを最小限に抑える新しいセキュリティ機能が含まれています。 これらのオペレーティング システムでローカル管理を有効にするには、追加の手順が必要です。 詳細については、「 [ローカル管理用のネイティブ モードのレポート サーバー &#40;SSRS&#41; の構成](../../reporting-services/report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [URL の構成 &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)   
 [URL 予約の構文 &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/url-reservation-syntax-ssrs-configuration-manager.md)  
  