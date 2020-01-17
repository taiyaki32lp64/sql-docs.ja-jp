---
title: レポートサーバーの Reporting Services |Microsoft Docs
ms.custom: ''
ms.date: 08/12/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- security [Reporting Services], extensions
- report servers [Reporting Services], about report server
- rendering extensions [Reporting Services], about extensions
- extensions [Reporting Services], about extensions
- storing data [Reporting Services]
- report servers [Reporting Services]
- data processing extensions [Reporting Services], about extensions
- delivery extensions [Reporting Services], about extensions
- data storage [Reporting Services]
- components [Reporting Services], report server
- report processing [Reporting Services], extensions
- Web service [Reporting Services], report server
- storage [Reporting Services]
ms.assetid: 88ed5b97-1d28-4980-80e4-b36761f3c03a
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 42ede73866c45662cf653d538f59be48684c5a45
ms.sourcegitcommit: 3b1f873f02af8f4e89facc7b25f8993f535061c9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/30/2019
ms.locfileid: "70176188"
---
# <a name="reporting-services-report-server"></a>Reporting Services Report Server
  このトピックでは、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] インストールの中心となるコンポーネントである [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] レポート サーバーの概要を説明します。 処理エンジンのペアと、認証、データ処理、表示、配信の各操作を行う用途別拡張機能の集合で構成されます。 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] レポート サーバーは、ネイティブ モードと SharePoint モードという 2 種類の配置モードのいずれかで動作します。 機能の比較については、「 [Feature Comparison of SharePoint and Native Mode](#bkmk_featuresupport) 」セクションを参照してください。  
  
 **インストール:** [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] のインストールの詳細については、以下を参照してください。  
  
-   [Reporting Services ネイティブ モードのレポート サーバーのインストール](install-windows/install-reporting-services-native-mode-report-server.md)  
  
-   [SharePoint &#40;PowerPivot と Reporting Services を使用した SQL Server BI 機能のインストール&#41;](../../2014/sql-server/install/install-sql-server-bi-features-sharepoint-powerpivot-reporting-services.md)  
  
 **Azure**: azure Virtual Machines で [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] を使用する方法の詳細については、次を参照してください。  
  
-   [Azure Virtual Machines のビジネスインテリジェンスを SQL Server](https://msdn.microsoft.com//library/windowsazure/jj992719.aspx)します。  
  
-   [PowerShell を使用したネイティブ モードのレポート サーバーを含む Azure VM の作成](https://msdn.microsoft.com/library/windowsazure/dn449661.aspx)。  
  
##  <a name="bkmk_top"></a> このトピックの内容  
  
-   [レポートサーバーモードの概要](#bkmk_overview)  
  
-   [SharePoint モードとネイティブモードの機能の比較](#bkmk_featuresupport)  
  
-   [Native Mode](#bkmk_nativemode)  
  
-   [SharePoint Web パーツでのネイティブモード](#bkmk_nativewithwebparts)  
  
-   [SharePoint モード](#bkmk_sharepointmode)  
  
-   [レポートプロセスとスケジュールおよび配信のプロセス](#bkmk_reportprocessor)  
  
-   [レポート サーバー データベース](#bkmk_reportdatabase)  
  
-   [認証、表示、データ、配信の各拡張機能](#bkmk_authentication)  
  
-   [関連タスク](#bkmk_relatedtasks)  
  
##  <a name="bkmk_overview"></a>レポートサーバーモードの概要  
 処理エンジン (プロセッサ) はレポート サーバーの中核となります。 プロセッサはレポート システムの整合性をサポートし、変更したり拡張したりすることはできません。 拡張機能もプロセッサですが、これらはきわめて限られた機能を実行します。 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] には、サポートされる拡張機能の種類ごとに、1 つ以上の既定の拡張機能が含まれます。 レポート サーバーにはカスタム拡張機能を追加できます。 これにより、レポート サーバーを拡張し、もともとサポートされていなかった機能を使用できるようにすることができます。たとえば、シングル サインオン テクノロジのサポート、既定の表示拡張機能では処理できないアプリケーション形式でのレポート出力、プリンターやアプリケーションへのレポート配信などのカスタム機能が考えられます。  
  
 レポート サーバーの個々のインスタンスは、プロセッサと拡張機能の完全な集合によって定義されます。この集合によって、最初の要求の処理から完成したレポートの表示まで、エンド ツー エンドの処理が行われます。 レポート サーバーは、サブコンポーネントを利用してレポート要求を処理し、要求時アクセスまたはスケジュールされた配布でレポートを利用できるようにします。  
  
 機能的には、レポート サーバーはさまざまなデータ ソースのレポート作成作業、レポート表示、およびレポート配信作業と、拡張可能な認証および承認スキームを可能にします。 また、レポート サーバーには、パブリッシュされたレポート、共有データ ソース、共有データセット、レポート パーツ、共有スケジュール、サブスクリプション、レポート定義ソース ファイル、モデル定義、コンパイル済みレポート、スナップショット、パラメーター、およびその他のリソースが格納される、レポート サーバー データベースが含まれています。 さらに、レポート サーバーでは、レポート要求を処理するようにレポート サーバーを構成する、スナップショット履歴を保持する、レポート、データ ソース、データセット、およびサブスクリプションに対する権限を管理する、などの管理作業を行うことができます。  
  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] レポート サーバーでは、レポート サーバー インスタンス用に次の 2 つの配置モードがサポートされています。  
  
-   **ネイティブ モード**(SharePoint Web パーツ対応ネイティブ モードを含む)。レポート サーバーはアプリケーション サーバーとして実行され、 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] コンポーネントのみを通じてすべての処理機能と管理機能が提供されます。 ネイティブ モードのレポート サーバーは、 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 構成マネージャーと SQL Server Management Studio を使って構成します。  
  
-   **SharePoint モード**。レポート サーバーは SharePoint サーバー ファームの一部としてインストールされます。  SharePoint モードの配置と構成には、PowerShell コマンドまたは SharePoint コンテンツ管理ページを使用します。  
  
 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] では、レポート サーバーを別のモードに切り替えることはできません。 環境で使用しているレポート サーバーの種類を変更するには、目的のモードのレポート サーバーをインストールした後、古いバージョンのレポート サーバーから新しいレポート サーバーにレポート アイテムまたはレポート サーバー データベースをコピーまたは移動する必要があります。 このプロセスは、一般的には "移行" と呼ばれます。 移行に必要な手順は、移行先のモードと移行元のバージョンによって異なります。 詳細については、「 [Upgrade and Migrate Reporting Services](install-windows/upgrade-and-migrate-reporting-services.md)」をご覧ください。  
  
##  <a name="bkmk_featuresupport"></a>SharePoint モードとネイティブモードの機能の比較  
  
|機能またはコンポーネント|ネイティブ モード|SharePoint モード|  
|--------------------------|-----------------|---------------------|  
|**URL アドレス指定**|はい|SharePoint 統合モードでは URL アドレスの利用が異なります。 レポート、レポート モデル、共有データ ソース、およびリソースの参照には SharePoint URL が使用されます。 レポート サーバーのフォルダー階層は使用されません。 ネイティブ モードのレポート サーバー上でサポートされる URL アクセスに依存するカスタム アプリケーションでは、レポート サーバーが SharePoint 統合用に構成されると、この機能が動作しなくなります。<br /><br /> URL アクセスの詳細については、「 [URL アクセス パラメーター リファレンス](url-access-parameter-reference.md)」を参照してください。|  
|**カスタム セキュリティ拡張機能**|はい|[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] のカスタム セキュリティ拡張機能は、レポート サーバーに配置したり使用することはできません。 レポート サーバーには特別な用途のセキュリティ拡張機能が用意されており、SharePoint 統合モードで動作するようにレポート サーバーを構成するときは常に使用されます。 このセキュリティ拡張機能は内部コンポーネントで、統合操作に必要です。|  
|**構成マネージャー**|はい|**\*\* 重要 \*\*** 構成マネージャーは、SharePoint モードのレポート サーバーの管理には使用できません。 代わりに、SharePoint サーバーの全体管理を使用してください。|  
|**レポート マネージャー**|はい|レポート マネージャーは、SharePoint モードの管理には使用できません。 SharePoint アプリケーション ページを使用してください。 詳細については、「 [Reporting Services の SharePoint サービスとサービス アプリケーション](../../2014/reporting-services/reporting-services-sharepoint-service-and-service-applications.md)｣を参照してください。|  
|**リンク レポート**|はい|不可。|  
|**個人用レポート**|はい|[いいえ]|  
|**個人用サブスクリプション** とバッチ処理方式|はい|[いいえ]|  
|**データ警告**|[いいえ]|はい|  
|**Power View**|[いいえ]|はい<br /><br /> クライアント ブラウザーに Silverlight が必要です。 ブラウザーの要件の詳細については、「 [Planning for Reporting Services and &#40;Power View browser&#41; Support Reporting Services 2014](../../2014/reporting-services/browser-support-for-reporting-services-and-power-view.md) 」を参照してください。|  
|**.RDL レポート**|はい|はい<br /><br /> .RDL レポートは、ネイティブ モードまたは SharePoint モードの [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] レポート サーバーで実行できます。|  
|**.RDLX レポート**|[いいえ]|はい<br /><br /> Power View .RDLX レポートは、SharePoint モードの [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] レポート サーバーでのみ実行できます。|  
|**SharePoint リストの拡張機能用の SharePoint ユーザー トークン資格情報**|[いいえ]|はい|  
|**インターネットに直接つながっている配置の AAM 領域**|[いいえ]|はい|  
|**SharePoint のバックアップと回復**|[いいえ]|はい|  
|**ULS ログのサポート**|[いいえ]|はい|  
  
##  <a name="bkmk_nativemode"></a>ネイティブモード  
 ネイティブ モードでは、レポート サーバーはスタンドアロンのアプリケーション サーバーとして、レポートとレポート モデルの表示、管理、処理、配信の機能をすべて提供します。 これはレポート サーバー インスタンスの既定のモードです。 セットアップ時にネイティブ モードのレポート サーバーを構成してインストールすることも、セットアップの完了後にレポート サーバーを構成してネイティブ モードで操作できるようにすることもできます。  
  
 次の図は、 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] ネイティブ モードの配置の 3 層アーキテクチャを示しています。 ここでは、データ層のレポート サーバー データベースとデータ ソース、中間層のレポート サーバー コンポーネント、およびプレゼンテーション層のクライアント アプリケーションと組み込みツールまたはカスタム ツールを示しています。 また、サーバー コンポーネント間での要求およびデータの流れと、データ ストアからコンテンツを送信および取得するコンポーネントも示しています。  
  
 ![Reporting Services のアーキテクチャ](media/reporting-serv-arch.gif "Reporting Services のアーキテクチャ")  
  
 Web サービス、バックグラウンド処理、およびその他の操作をホストする、"レポート サーバー サービス" と呼ばれる [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows サービスとして、レポート サーバーは実装されます。 Services コンソール アプリケーションでは、このサービスは SQL Server Reporting Services (MSSQLSERVER) として表示されます。  
  
 サード パーティの開発者は、追加の拡張機能を作成して、レポート サーバーの処理能力を置き換えたり、拡張したりできます。 アプリケーション開発者が利用できるプログラマティック インターフェイスの詳細については、「 [テクニカル リファレンス](../../2014/reporting-services/technical-reference-ssrs.md)」を参照してください。  
  
###  <a name="bkmk_nativewithwebparts"></a>SharePoint Web パーツでのネイティブモード  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] には、2.0 以降、または SharePoint Portal Server 2003 以降 [!INCLUDE[winSPServ](../includes/winspserv-md.md)] のインスタンスにインストールして登録できる Web パーツが2つ用意されています。 SharePoint サイトからは、Web パーツを使用して、ネイティブ モードで動作するレポート サーバーに格納され処理されているレポートを検索し表示できます。 これらの Web パーツは、 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]の前のリリースで導入されたものです。  
  
##  <a name="bkmk_sharepointmode"></a> SharePoint モード  
 SharePoint モードでは、レポート サーバーが SharePoint サーバー ファーム内で実行される必要があります。 レポート サーバーの処理、表示、および管理機能は、 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 共有サービスを実行する SharePoint アプリケーション サーバーおよび 1 つ以上の [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] サービス アプリケーションから提供されます。 レポート サーバーのコンテンツや操作へのフロントエンド アクセスを、SharePoint サイトが提供します。  
  
 SharePoint モードでは次のものが必要です。  
  
-   [!INCLUDE[SPF2010](../includes/spf2010-md.md)] または [!INCLUDE[SPS2010](../includes/sps2010-md.md)]。  
  
-   SharePoint 2010 製品用の適切なバージョンの [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] アドイン。  
  
-   [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 共有サービスがインストールされている SharePoint アプリケーション サーバーと、少なくとも 1 つの [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] サービス アプリケーション。  
  
 次の図は、SharePoint モードの [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 環境を示しています。  
  
 ![SSRS SharePoint の機能のアーキテクチャ](media/rs-sharepoint-architecture.gif "SSRS SharePoint の機能のアーキテクチャ")  
  
||[説明]|  
|-|-----------------|  
|**(1)**|Web サーバーまたは Web フロントエンド (WFE)。 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] アドインは、レポートや [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 管理ページの表示などの Web アプリケーション機能を使用してデータ ソースやサブスクリプションの管理などのタスクを実行する場合に、それらの機能を使用する各 Web サーバーにインストールする必要があります。|  
|**(2)**|アドインによってインストールされる URL と SOAP エンドポイントによって、クライアントが [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] サービス プロキシ経由でアプリケーション サーバーと通信できるようになります。|  
|**(3)**|[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 共有サービスを実行しているアプリケーション サーバー。 レポート処理のスケールアウトは SharePoint ファームの一部として管理され、 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] サービスを追加のアプリケーション サーバーに追加することによって実行されます。|  
|**(4)**|権限、電子メール、プロキシ、サブスクリプションを含むさまざまな構成を持つ、1 つ以上の [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] サービス アプリケーションを作成できます。|  
|**(5)**|レポート、データ ソース、および他のアイテムが SharePoint コンテンツ データベースに格納されます。|  
|**(6)**|[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] サービス アプリケーションは、レポート サーバー、一時、およびデータ警告の各機能のために 3 つのデータベースを作成します。 すべての SSRS サービス アプリケーションに適用される構成設定は **RSReportserver.config** ファイルに格納されます。|  
  
##  <a name="bkmk_reportprocessor"></a>レポートプロセスとスケジュールおよび配信のプロセス  
 レポート サーバーには 2 つの処理エンジンがあります。これらは、事前および中間のレポート処理と、スケジュールおよび配信の処理を行います。 レポート プロセッサは、レポートの定義またはモデルを取得し、データ処理拡張機能からのデータにレイアウト情報を結合して、それを要求された形式で表示します。 スケジュールおよび配信プロセスでは、スケジュールによって起動されたレポートを処理し、目的の配信先にレポートを配信します。  
  
##  <a name="bkmk_reportdatabase"></a>レポートサーバーデータベース  
 レポート サーバーは、すべてのプロパティ、オブジェクト、およびメタデータを [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] データベースに格納する、ステートレス サーバーです。 格納されるデータには、パブリッシュされたレポート、コンパイル済みレポート、レポート モデル、およびレポート サーバーが管理するすべてのアイテムへのアクセスを提供するフォルダー階層が含まれます。 レポート サーバー データベースは、 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] の単一のインストール用、またはスケールアウト配置に含まれる複数のレポート サーバー用の内部記憶域を提供します。 SharePoint 製品またはテクノロジの大規模な配置内で実行されるようにレポート サーバーを構成すると、レポート サーバーでは、レポート サーバー データベースに加えて SharePoint データベースも使用されます。 Reporting Services インストールで使用されるデータ ストアの詳細については、「 [レポート サーバー データベース &#40;SSRS ネイティブ モード&#41;](report-server/report-server-database-ssrs-native-mode.md)。  
  
##  <a name="bkmk_authentication"></a>認証、表示、データ、配信の各拡張機能  
 レポート サーバーでサポートされる拡張機能の種類は、認証拡張機能、データ処理拡張機能、レポート処理拡張機能、表示拡張機能、および配信拡張機能です。 レポート サーバーには、少なくとも 1 つの認証拡張機能、データ処理拡張機能、および表示拡張機能が必要です。 配信拡張機能とカスタム レポート処理拡張機能は省略可能ですが、レポートの配信またはカスタム コントロールをサポートする場合は必須です。  
  
 Reporting Services が提供する既定の拡張機能を使用すると、カスタム コンポーネントを開発することなく、すべてのサーバー機能を使用できます。 次の表に示す既定の拡張機能は、完全なレポート サーバー インスタンスの一部であり、すぐに使用できる機能を提供します。  
  
|[型]|既定値|  
|----------|-------------|  
|[認証]|既定のレポート サーバー インスタンスでは、Windows 認証がサポートされます。ドメインで有効になっていれば、権限の借用機能や委任機能もサポートされます。|  
|データ処理|既定のレポート サーバー インスタンスには、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]、Oracle、Hyperion Essbase、SAPBW、OLE DB、並列データ ウェアハウス、ODBC の各データ ソース用のデータ処理拡張機能があります。|  
|表示|既定のレポート サーバー インスタンスには、HTML、Excel、CSV、XML、Image、Word、SharePoint リスト、および PDF 用の表示拡張機能があります。|  
|Delivery|既定のレポート サーバー インスタンスには、電子メールの配信拡張機能とファイル共有の配信拡張機能があります。 レポート サーバーが SharePoint 統合用に構成されている場合は、レポートを SharePoint ライブラリに保存する配信拡張機能を使用できます。|  
  
> [!NOTE]  
>  Reporting Services に含まれているツールとアプリケーションの完全なセットを使用すると、サーバーを管理したり、コンテンツを作成したり、組織内のユーザーがそのコンテンツを使用できるようにしたりすることができます。  
  
##  <a name="bkmk_relatedtasks"></a> 関連タスク  
 次の各トピックでは、レポート サーバーのインストール、使用、およびメンテナンスについて詳しく説明します。  
  
|タスク|リンク|  
|----------|----------|  
|ハードウェアおよびソフトウェアの要件を確認します。|「[Hardware and Software Requirements for Reporting Services in SharePoint Mode](../../2014/sql-server/install/hardware-and-software-requirements-for-reporting-services-in-sharepoint-mode.md)」を参照してください。|  
|[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] を SharePoint モードでインストールします。|[SharePoint 2010 用 Reporting Services の SharePoint モードのインストール](../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)|  
|Web 開発者、またはカスケード スタイル シート作成に関する専門知識を持つユーザーであれば、各自の責任で既定のスタイルを変更し、色、フォント、およびツール バーやレポート マネージャーのレイアウトを変えることができます。 このリリースでは、既定のスタイル シートについても、そのスタイル シートの変更手順についても説明していません。|[HTML ビューアーおよびレポート マネージャーのスタイル シートをカスタマイズする](../../2014/reporting-services/customize-style-sheets-for-html-viewer-and-report-manager.md)|  
|HTML のスタイルやカスケード スタイル シート (CSS) の知識があれば、このトピックの情報を利用して、どのファイルを変更するとレポート マネージャーの外観をカスタマイズできるのかを判断できます。|[カスタム認証クッキーを送信するようにレポート マネージャーを構成する](security/configure-the-web-portal-to-pass-custom-authentication-cookies.md)|  
|レポート サーバー Web サービスおよび Windows サービスに対するメモリ設定を調整する方法について説明します。|[レポート サーバー アプリケーションで利用可能なメモリの構成](report-server/configure-available-memory-for-report-server-applications.md)|  
|リモート管理用にレポート サーバーを構成するための推奨されている手順について説明します。|[リモート管理用のレポート サーバーの構成](report-server/configure-a-report-server-for-remote-administration.md)|  
|ネイティブのレポート サーバー インスタンスで **個人用レポート** を使用できるかどうかを構成する方法について説明します。|[個人用レポートの有効化と無効化](report-server/enable-and-disable-my-reports.md)|  
|サポートされているブラウザーから、印刷機能を実現する RSClientPrint コントロールを設定する方法について説明します。 ブラウザーの要件の詳細については、「 [Planning for Reporting Services」 &#40;および「&#41;Power View browser Support Reporting Services 2014](../../2014/reporting-services/browser-support-for-reporting-services-and-power-view.md)」を参照してください。|[Reporting Services のクライアント側印刷機能の有効化と無効化](report-server/enable-and-disable-client-side-printing-for-reporting-services.md)|  
  
## <a name="see-also"></a>参照  
 [Reporting Services の拡張機能](extensions/reporting-services-extensions.md)   
 [Reporting Services ツール](tools/reporting-services-tools.md)   
 [サブスクリプションと配信 &#40;Reporting Services&#41;](subscriptions/subscriptions-and-delivery-reporting-services.md)   
 [レポート サーバー データベース &#40;SSRS ネイティブ モード&#41;](report-server/report-server-database-ssrs-native-mode.md)   
 [セキュリティ拡張機能の実装](extensions/security-extension/implementing-a-security-extension.md)   
 [データ処理拡張機能の実装](extensions/data-processing/implementing-a-data-processing-extension.md)   
 [Reporting Services でサポートされるデータ ソース (SSRS)](create-deploy-and-manage-mobile-and-paginated-reports.md)   
 [PowerShell を使用して SSRS を管理する方法](https://sqlbelle.wordpress.com/2015/08/17/automate-ssrs-report-generation-using-powershell/)  
  
  
