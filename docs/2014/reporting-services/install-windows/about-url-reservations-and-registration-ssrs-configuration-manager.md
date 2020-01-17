---
title: URL の予約と登録について (SSRS 構成マネージャー) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- URL reservations
- URL registration
- Report Server service, URL reservations
ms.assetid: c2c460c3-e749-4efd-aa02-0f8a98ddbc76
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 6b72d0a263010cc82abab38ea2d6149d3492ed7b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66108940"
---
# <a name="about-url-reservations-and-registration--ssrs-configuration-manager"></a>URL の予約と登録について (SSRS 構成マネージャー)
  Reporting Services アプリケーションの URL は、HTTP.SYS の URL 予約として定義されます。 URL 予約は、Web アプリケーションへの URL エンドポイントの構文を定義します。 レポート サーバーでアプリケーションを構成する際には、レポート サーバー Web サービスとレポート マネージャーの両方に対して URL 予約を定義します。 セットアップまたは [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ツールで URL を構成すると、自動的に URL 予約が作成されます。  
  
-   セットアップでは、既定値を使用して URL 予約が作成されます。 既定の構成でインストールすると、レポート サーバー Web サービスの URL とレポート マネージャーの URL の 2 つの URL が予約されます。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ツールを使用すると、URL をさらに追加したり、セットアップによって作成された既定の URL を変更したりできます。  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ツールでは、ツールの **[Web サービス URL]** ページまたは **[レポート マネージャー URL]** ページで指定した URL に基づいて URL 予約が作成されます。  
  
 いずれの場合も、さらに、レポート サーバー サービスへの URL に対する権限の割り当て、重複するインスタンスのチェック、および HTTP.SYS への URL 予約の追加が行われます。 HttpCfg.exe やその他のツールを使用して直接 Reporting Services の URL 予約を作成したり変更したりしないでください。 手順を省略したり無効な値を設定したりすると、診断や修正が困難な問題が発生する可能性があります。  
  
> [!NOTE]  
>  HTTP.SYS は、ネットワーク要求をリッスンして要求キューにルーティングするオペレーティング システム コンポーネントです。 このリリースの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]では、HTTP.SYS によって、レポート サーバー Web サービスとレポート マネージャーの要求キューが作成され、管理されます。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] アプリケーションのホスティングやアクセスにインターネット インフォメーション サービス (IIS) は使用されなくなりました。 HTTP.SYS 機能の詳細については、MSDN の「 [HTTP サーバー API](https://go.microsoft.com/fwlink/?LinkId=92652) 」を参照してください。  
  
##  <a name="ReportingServicesURLs"></a> Reporting Services の URL  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] では、以下のツール、アプリケーション、およびアイテムに URL を通じてアクセスできます。  
  
-   レポート サーバー Web サービス  
  
-   レポート マネージャー  
  
-   レポート ビルダー  
  
-   レポート サーバーにパブリッシュされたレポート  
  
 URL を指定できるその他のパブリッシュされるアイテム (モデルや共有データ ソースなど) には、URL を通じてスタンドアロンのアイテムとしてアクセスしないようにしてください。 これらのアイテムは、ブラウザー ウィンドウで表示しても意味のある形式で表示されません。  
  
> [!NOTE]  
>  レポート ビルダーへの URL アクセスや、レポート サーバーに保存されている特定のレポートへの URL アクセスについては説明しません。 これらのアイテムへの URL アクセスの詳細については、 [オンライン ブックの「](../access-report-server-items-using-url-access.md) URL アクセスを使用したレポート サーバー アイテムへのアクセス [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 」を参照してください。  
  
##  <a name="URLreservation"></a> URL の予約と登録  
 URL 予約は、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] アプリケーションへのアクセスに使用できる URL を定義します。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] では、レポート サーバー Web サービスとレポート マネージャーの URL を HTTP.SYS で 1 つ以上予約して、サービスの起動時に登録します。 レポート ビルダーとレポートの URL は、レポート サーバー Web サービスの URL 予約に基づいています。 URL にパラメーターを追加することにより、Web サービスを通じてそれらを開くことができます。 予約と登録は、HTTP.SYS によって行われます。 詳細については、MSDN の「 [名前空間の予約、登録、およびルーティング](https://go.microsoft.com/fwlink/?LinkId=92653) 」を参照してください。  
  
 *URL 予約* とは、Web アプリケーションへの URL エンドポイントを作成して HTTP.SYS に格納するプロセスです。 HTTP.SYS は、コンピューターで定義されているすべての URL 予約の共通リポジトリであり、URL 予約が一意であることを保証する一連の共通規則を定義します。  
  
 *URL の登録* は、サービスの起動時に行われます。 サービスが起動すると、要求キューが作成され、HTTP.SYS がそのキューへの要求のルーティングを開始します。 URL エンドポイントは、そのエンドポイントに転送される要求がキューに追加される前に登録される必要があります。 レポート サーバー サービスの起動時には、有効化されているすべてのアプリケーションに対して予約されているすべての URL が登録されます。 したがって、登録が行われるためには Web サービスが有効化されている必要があります。 ポリシー ベースの管理の Reporting Services のセキュリティ構成ファセットで **WebServiceAndHTTPAccessEnabled** プロパティを **False** に設定すると、Web サービスの URL がサービスの起動時に登録されません。  
  
 サービスを停止したり、Web サービスやレポート マネージャーのアプリケーション ドメインの再利用を行うと、URL の登録が解除されます。 サービスの実行中に URL 予約を変更すると、古い URL の登録を解除して新しい URL を使用できるようにするために、アプリケーション ドメインの再利用処理が直ちに行われます。  
  
 次の例は、URL 予約の概念と、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] アプリケーション用に使用される URL アドレスと URL 予約の関連付けを示しています。 URL 予約の構文が、アプリケーションへのアクセスに使用する URL とは異なる点に注目してください。  
  
|HTTP.SYS の URL 予約|[URL]|説明|  
|---------------------------------|---------|-----------------|  
|http://+:80/reportserver|http://\<computername>/reportserver<br /><br /> http://\<IPAddress>/reportserver<br /><br /> http://localhost/reportserver|この URL 予約では、ポート 80 でワイルドカード (+) を指定しています。 これにより、ポート 80 のレポート サーバー コンピューターに解決されるホストが指定されているすべての受信要求がレポート サーバー キューに送られます。 この URL 予約を使用すると、任意の数の URL を使用してレポート サーバーにアクセスできます。<br /><br /> ほとんどのオペレーティング システムでは、これが [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] レポート サーバーの既定の URL 予約です。|  
|http://123.45.67.0:80/reportserver|http://123.45.67.0/reportserver|この URL 予約では IP アドレスを指定しています。これは、ワイルドカードの URL 予約よりはるかに制限の厳しい URL 予約です。 レポート サーバーへの接続に使用できるのは、この IP アドレスを含む URL だけです。 この URL の予約 http:// でレポート サーバーへの要求\<computername >/reportserver または http://localhost/reportserver は失敗します。|  
  
##  <a name="DefaultURLs"></a> 既定の URL  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] を既定の構成でインストールすると、レポート サーバー Web サービスとレポート マネージャーの URL が自動的に予約されます。 これらの既定値は、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ツールで URL 予約を定義するときにも使用できます。 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] をインストールした場合や、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] を名前付きインスタンスとしてインストールした場合は、既定の URL にインスタンス名が含まれます。  
  
> [!IMPORTANT]  
>  インスタンスの文字はアンダースコア文字 (`_`) です。  
  
 URL 予約にはポート番号が含まれます。 以下のオペレーティング システムでは、複数の Web アプリケーションで 1 つのポートを共有できます。  
  
1.  [!INCLUDE[win8srv](../../includes/win8srv-md.md)]  
  
2.  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]  
  
3.  [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)]  
  
4.  [!INCLUDE[win7](../../includes/win7-md.md)]  
  
5.  [!INCLUDE[wiprlhlong](../../includes/wiprlhlong-md.md)]  
  
|インスタンスの種類|アプリケーション|既定の URL|HTTP.SYS の実際の URL 予約|  
|-------------------|-----------------|-----------------|----------------------------------------|  
|[既定のインスタンス]|レポート サーバー Web サービス|http://\<servername>/reportserver|http://\<servername>:80/reportserver|  
|[既定のインスタンス]|レポート マネージャー|http://\<servername>/reportserver|http://\<servername>:80/reportserver|  
|[名前付きインスタンス]|レポート サーバー Web サービス|http://\<servername>/reportserver_\<instancename>|http://\<servername>:80/reportserver_\<instancename>|  
|[名前付きインスタンス]|レポート マネージャー|http://\<servername>/reports_\<instancename>|http://\<servername >: 80/reports _\<instancename >|  
|SQL Server Express|レポート サーバー Web サービス|http://\<servername>/reportserver_SQLExpress|http://\<servername>:80/reportserver_SQLExpress|  
|SQL Server Express|レポート マネージャー|http://\<servername>/reports_SQLExpress|http://\<servername>:80/reports_SQLExpress|  
  
##  <a name="URLPermissionsAccounts"></a> Reporting Services の URL の認証とサービス ID  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の URL 予約では、レポート サーバー サービスのサービス アカウントが指定されます。 サービスが実行されているアカウントが、同じインスタンスで実行される [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] アプリケーションに対して作成されるすべての URL に対して使用されます。 レポート サーバー インスタンスのサービス ID は、RSReportServer.config ファイルに格納されます。  
  
 サービス アカウントには既定値はありません。 ただし、セットアップ時には (ファイルのみのモードでサーバーをインストールする場合でも) サービス アカウントを指定する必要があります。サービス アカウントは、RSReportServer.config の `URLReservation` に指定されます。 サービス アカウントの有効な値は、ドメイン ユーザー アカウント、`LocalSystem`、および `NetworkService` です。  
  
 既定のセキュリティが `RSWindowsNegotiate` であるため、匿名アクセスは無効になっています。 イントラネット アクセスの場合、レポート サーバーの URL ではネットワーク コンピューターの名前が使用されます。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] をインターネット接続用に構成する場合は、別の設定を使用する必要があります。 認証の詳細については、 [オンライン ブックで「](../security/authentication-with-the-report-server.md) レポート サーバーでの認証 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 」を参照してください。  
  
##  <a name="URLlocalAdmin"></a> ローカル管理用の URL  
 URL 予約に強いワイルドカードまたは弱いワイルドカードを指定した場合、 http://localhost/reportserver または http://localhost/reports を使用できます。  
  
 http://localhost URL は、 http://127.0.0.1 として解釈されます。 URL 予約をコンピューター名や 1 つの IP アドレスに設定した場合は、ローカル コンピューターの 127.0.0.1 に対して追加の予約を作成しないと localhost を使用できません。 同様に、localhost や 127.0.0.1 がコンピューターで無効になっている場合も、その URL を使用できません。  
  
 [!INCLUDE[wiprlhlong](../../includes/wiprlhlong-md.md)] と [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] には、誤ってプログラムが高度な特権で実行されるリスクを最小限に抑える新しいセキュリティ機能が含まれています。 これらのオペレーティング システムでローカル管理を有効にするには、追加の手順が必要です。 詳細については、「 [ローカル管理用のネイティブ モードのレポート サーバー &#40;SSRS&#41; の構成](../report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md)」を参照してください。  
  
##  <a name="URLSharePoint"></a> SharePoint 統合モードでレポート サーバーの Url  
 スタンドアロンのレポート サーバーを、大規模に配置された SharePoint 製品またはテクノロジの内部で実行するように構成すると、URL と仮想ディレクトリの構成が次のような影響を受けます。  
  
-   レポートやその他のアイテムの URL が、SharePoint Web アプリケーションの URL を通じて指定されます。 特定のレポートに URL でアクセスする場合は、常に完全修飾 URL を使用します。完全修飾 URL は、サイト パス、ドキュメント ライブラリ、アイテム名、およびファイル名拡張子 (レポートの場合は .rdl) で構成されます。 レポートで共有データ ソースとモデルを参照するとき、およびレポート サーバーへのパブリッシュ操作のためにターゲット サーバーとフォルダーを指定するときに、完全修飾 URL を指定する必要があります。  
  
-   さまざまな種類のレポート サーバー アイテムを区別するためにファイル名拡張子が使用されます。 有効な拡張子は、.rdl (レポート定義)、.smdl (レポート モデル)、および .rsds (SharePoint サイトに対して作成された共有データ ソース) です。  
  
-   SharePoint 製品およびテクノロジでも URL 予約が定義されていますが、サーバーへのパブリッシュの際にはそれらを無視できます。 SharePoint Web アプリケーションの URL 予約は内部操作です。  
  
-   使用することはできません、統合レポート サーバーと SharePoint テクノロジのインスタンスが同じコンピューターにインストールされている 1 台のサーバー展開の場合、 http://localhost/reportserver します。 場合 http://localhost は、SharePoint Web アプリケーションにアクセスするために使用する必要がありますまたは使用する既定以外の Web サイトの一意のポートの割り当てをレポート サーバーにアクセスします。 さらに、レポート サーバーが SharePoint ファームと統合されている場合は、リモート コンピューターにインストールされている配置内のノードではレポート サーバーへの localhost アクセスは解決されません。  
  
-   レポート マネージャーの URL 予約と URL エンドポイントは、SharePoint 統合モードで実行されているレポート サーバーに対しては構成できません。 構成した場合、SharePoint 統合モードでレポート サーバーを配置した後で機能しなくなります。 レポート マネージャーは SharePoint 統合モードではサポートされません。  
  
 大規模に配置された SharePoint 製品またはテクノロジの内部で実行するためにレポート サーバーのスケールアウト配置を統合した場合は、レポート サーバー ノードの負荷を分散して、スケールアウト配置への 1 つの仮想サーバー URL を定義します。 レポート サーバーの統合設定で指定できるレポート サーバーの URL は 1 つだけです。 スケールアウト配置の場合は、スケールアウト配置のサーバー ノードのアクセス ポイントをその URL に指定する必要があります。  
  
## <a name="see-also"></a>参照  
 [URL の構成 &#40;SSRS 構成マネージャー&#41;](configure-a-url-ssrs-configuration-manager.md)   
 [URL 予約の構文 &#40;SSRS 構成マネージャー&#41;](url-reservation-syntax-ssrs-configuration-manager.md)  
  
  
