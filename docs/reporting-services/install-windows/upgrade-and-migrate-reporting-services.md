---
title: Reporting Services のアップグレードと移行 | Microsoft Docs
ms.prod: reporting-services
ms.prod_service: reporting-services-native
helpviewer_keywords:
- SSRS, upgrading
- Reporting Services, upgrades
- SQL Server Reporting Services, upgrading
- upgrading Reporting Services
author: maggiesMSFT
ms.author: maggies
ms.topic: conceptual
ms.date: 08/17/2017
ms.openlocfilehash: 9d0ff28e1e9c7784da2c1206f72573ba608797a1
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68264989"
---
# <a name="upgrade-and-migrate-reporting-services"></a>Upgrade and Migrate Reporting Services

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)]

  このトピックでは、SQL Server Reporting Services のアップグレードおよび移行オプションの概要を示します。 展開された SQL Server Reporting Services をアップグレードするには、次の 2 つの一般的な方法があります。  
 
-   **アップグレード:** サーバーと現在インストールされているインスタンスで [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] コンポーネントをアップグレードします。 これは一般に "インプレース" アップグレードと呼ばれます。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サーバーのモード間でのインプレース アップグレードはサポートされていません。 たとえば、ネイティブ モードのレポート サーバーを SharePoint モードのレポート サーバーにアップグレードすることはできません。 レポート アイテムはモード間で移行できます。 詳細については、このドキュメントの「ネイティブ モードから SharePoint モードへの移行のシナリオ」を参照してください。  
  
-   **移行**:新しい SharePoint 環境をインストールして構成し、レポート アイテムとリソースを新しい環境にコピーして、既存のコンテンツを使用するよう新しい環境を構成します。 下位レベルの移行形式では、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] データベース、構成ファイル、および SharePoint コンテンツ データベース (SharePoint モードを使用している場合) をコピーします。  
    
> **[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ネイティブ モード &#124; [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint モード

> [!NOTE]
> SharePoint と Reporting Services の統合は、SQL Server 2016 以降では使用できません。
   
##  <a name="bkmk_known_issues"></a> アップグレードに関する既知の問題とベスト プラクティス  
 アップグレード可能なサポートされるエディションとバージョンの詳細な一覧については、「 [Supported Version and Edition Upgrades](../../database-engine/install-windows/supported-version-and-edition-upgrades.md)」を参照してください。  
  
> [!TIP]  
>  SQL Server に関する問題の最新情報については、以下を参照してください。  
>   
>  -   [SQL Server 2016 リリース ノート](https://go.microsoft.com/fwlink/?LinkID=398124)をダウンロードする。  
  
  
##  <a name="bkmk_side_by_side"></a> サイド バイ サイド インストール  
 SQL Server Reporting Services のネイティブ モードは、[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] または [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] のネイティブ モードの展開とサイド バイ サイドでインストールできます。  
  
 SharePoint モードの SQL Server Reporting Services と以前のバージョンの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint モードのコンポーネントのサイド バイ サイド展開はサポートされていません。  
  
  
##  <a name="bkmk_inplace_upgrade"></a> インプレース アップグレード  
 アップグレードは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップで実行されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップを使用すると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を含む任意またはすべての [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]コンポーネントをアップグレードできます。 セットアップによって既存のインスタンスが検出され、アップグレードするように求められます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップには、コマンド ライン引数またはセットアップ ウィザードで指定できるアップグレード オプションが用意されています。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップを実行すると、次のいずれかのバージョンからアップグレードするオプションを選ぶか、既存のインストールと並行して実行する SQL Server Reporting Services の新しいインスタンスをインストールすることができます。  
  
-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
  
-   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
  
-   [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]  
  
-   [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の詳細については、次のトピックを参照してください。  

* [SQL Server 2016 へのアップグレード](../../database-engine/install-windows/upgrade-sql-server.md)
* [インストール ウィザードを使用した SQL Server 2016 へのアップグレード &#40;セットアップ&#41;](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)
* [コマンド プロンプトからの SQL Server 2016 のインストール](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)
  
  
##  <a name="bkmk_upgrade_checklist"></a> アップグレード前のチェック リスト  
 SQL Server Reporting Services にアップグレードする前に、次のトピックを確認してください。  
  
-   お使いのハードウェアおよびソフトウェアで [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)]をサポートできるかどうかを判断する要件を確認します。 詳細については、「 [SQL Server 2016 のインストールに必要なハードウェアおよびソフトウェア](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)」を参照してください。  
  
-   システム構成チェッカー (SCC) を使って、レポート サーバー コンピューターをスキャンし、SQL Server Reporting Services の正常なインストールを妨げる可能性のある状態をチェックします。 詳細については、「 [Check Parameters for the System Configuration Checker](../../database-engine/install-windows/check-parameters-for-the-system-configuration-checker.md)」を参照してください。  
  
-   セキュリティのベスト プラクティスと [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のためのガイダンスを確認します。 詳細については、「 [Security Considerations for a SQL Server Installation](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)」を参照してください。  
  
-   対称キーをバックアップします。 詳細については、「 [Back Up and Restore Reporting Services Encryption Keys](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)」を参照してください。  
  
-   レポート サーバーのデータベースと構成ファイルをバックアップします。 詳細については、「 [Backup and Restore Operations for Reporting Services](../../reporting-services/install-windows/backup-and-restore-operations-for-reporting-services.md)」を参照してください。  
  
-   IIS で既存の [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 仮想ディレクトリに任意のカスタマイズをバックアップします。  
  
-   無効な SSL 証明書を削除します。  これには、有効期限が切れており、Reporting Services をアップグレードする前に更新する予定のない証明書が含まれます。  無効な証明書はアップグレードが失敗する原因となり、" **Microsoft.ReportingServices.WmiProvider.WMIProviderException: Web サイトで Secure Sockets Layer (SSL) 証明書が構成されていません。** " のようなエラー メッセージが Reporting Services のログ ファイルに書き込まれます。  
  
 実稼働環境をアップグレードする前に、必ず実稼働環境と同じ構成をしている実稼動前の環境でアップグレード テストを実行してください。  
  
  
## <a name="overview-of-migration-scenarios"></a>移行シナリオの概要  
 サポートされているバージョンの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] から [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]にアップグレードする場合、通常は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップ ウィザードを実行することで、レポート サーバーのプログラム ファイル、データベース、およびすべてのアプリケーション データをアップグレードできます。  
  
 ただし、次の状況が生じた場合は、レポート サーバー インストールを手動で **移行** する必要があります。  
  
-   配置で使用されるレポート サーバーの種類を変更します。 たとえば、ネイティブ モードのレポート サーバーを SharePoint モードにアップグレードまたは変換することはできません。 詳細については、「[ネイティブ モードから SharePoint モードへの移行 &#40;SSRS&#41;](../../reporting-services/install-windows/native-to-sharepoint-migration-ssrs.md)」を参照してください。  
  
-   アップグレード プロセス中にレポート サーバーがオフラインになる時間を最小限に抑えることが求められている。 既存のレポート サーバーのインストールの状態を変更せずに、新しいレポート サーバー インスタンスにコンテンツ データをコピーし、インストールをテストする間、現在のインストールはオンライン状態で維持されます。  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] を配置した SharePoint 2010 を SharePoint 2013/2016 に移行することが求められている。 SharePoint 2013/2016 では、SharePoint 2010 からのインプレース アップグレードがサポートされていません。 詳細については、「[Reporting Services の移行 &#40;SharePoint Mode&#41;](../../reporting-services/install-windows/migrate-a-reporting-services-installation-sharepoint-mode.md)」を参照してください。  
  
  
##  <a name="bkmk_native_scenarios"></a> ネイティブ モードのアップグレードと移行のシナリオ  
 **アップグレード:** ネイティブ モードのインプレース アップグレード手順は、前述のサポートされている各バージョンで共通です。 SQL Server インストール ウィザードまたはコマンド ライン インストールを実行します。 インストールが完了すると、レポート サーバー データベースは自動的に新しいレポート サーバー データベース スキーマにアップグレードされます。 詳細については、このトピックの「 [インプレース アップグレード](#bkmk_inplace_upgrade) 」を参照してください。  
  
 アップグレード処理では、まずアップグレードする既存のレポート サーバー インスタンスを選択します。  
  
1.  レポート サーバー データベースがリモート コンピューター上に存在し、そのデータベースを更新する権限がない場合は、リモートのレポート サーバー データベースを更新するための資格情報を指定するように求められます。 **sysadmin** 権限またはデータベース更新権限を持つ資格情報を指定してください。  
  
2.  アップグレードの妨げになる条件または設定がないかどうかがチェックされ、構成設定が読み取られます。 たとえば、カスタム拡張機能がレポート サーバーに配置されていないかどうかがチェックされます。 アップグレードがブロックされた場合は、アップグレードがブロックされないようにインストールを変更するか、新しい SQL Server Reporting Services インスタンスに移行する必要があります。 詳細については、アップグレード アドバイザーのマニュアルを参照してください。  
  
3.  アップグレードを続行できる場合は、アップグレード処理を進めるように求められます。  
  
4.  SQL Server Reporting Services プログラム ファイルの新しいフォルダーが作成されます。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のインストール用のプログラム フォルダーには、MSRS13.\<*インスタンス名*> が含まれます。  
  
5.  SQL Server Reporting Services レポート サーバーのプログラム ファイル、構成ツール、およびレポート サーバー機能の一部であるコマンド ライン ユーティリティが追加されます。  
  
    1.  以前のバージョンのプログラム ファイルは削除されます。  
  
    2.  新しいバージョンにアップグレードされるレポート サーバーの構成ツールおよびユーティリティには、ネイティブ モードの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ツール、コマンド ライン ユーティリティ (RS.exe など)、およびレポート ビルダーがあります。  
  
    3.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] などの他のクライアント ツールは個別にダウンロードし、個別にアップグレードする必要があります。 詳細については、「 [Download SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/mt238290.aspx)」 (SQL Server Management Studio (SSMS) のダウンロード) を参照してください。
  
    4.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] は個別にダウンロードします。 詳細については、「 [SQL Server Data Tools in Visual Studio 2015](https://msdn.microsoft.com/mt186501)」 (Visual Studio 2015 の SQL Server Data Tools) を参照してください。  
  
6.  SQL Server Reporting Services レポート サーバー サービスのサービス コントロール マネージャーにあるサービス エントリが再利用されます。 このサービスのエントリには、レポート サーバー Windows サービス アカウントが含まれます。  
  
7.  IIS の既存の仮想ディレクトリ設定に基づいて新しい URL が予約されます。 IIS の仮想ディレクトリは削除されない場合があるので、アップグレードの完了後に手動で削除してください。  
  
8.  構成ファイル内の設定がマージされます。 現在のインストールの構成ファイルが基礎として使用され、新しいエントリが追加されます。 使用されなくなったエントリは削除されませんが、アップグレードの完了後はレポート サーバーによって読み取られなくなります。 アップグレードでは古いログ ファイル、使用されなくなった RSWebApplication.config ファイル、または IIS の仮想ディレクトリ設定は削除されません。 また、古いバージョンのレポート デザイナーや Management Studio などのクライアント ツールは削除されません。 これらのファイルやツールが不要になった場合は、アップグレードの完了後に削除してください。  
  
 **移行:** ネイティブ モード インストールの以前のバージョンを SQL Server Reporting Services に移行する手順は、前述のサポートされている各バージョンで共通です。 詳細については、「[Reporting Services のインストールの移行 &#40;ネイティブ モード&#41;](../../reporting-services/install-windows/migrate-a-reporting-services-installation-native-mode.md)」を参照してください。  
  
  
##  <a name="bkmk_native_scaleout"></a> Reporting Services ネイティブ モードのスケールアウト配置のアップグレード  
 複数のレポート サーバーにスケールアウトされる [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ネイティブ モードの配置をアップグレードする方法の概要を次に示します。 このプロセスでは、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置のダウンタイムが発生します。  
  
1.  レポート サーバー データベースと暗号化キーをバックアップします。 詳細については、「[Reporting Services のバックアップおよび復元操作](../../reporting-services/install-windows/backup-and-restore-operations-for-reporting-services.md)」および「[スケールアウト配置に関する暗号化キーの追加と削除 &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/add-and-remove-encryption-keys-for-scale-out-deployment.md)」を参照してください。  
  
2.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成マネージャーを使用して、スケールアウトした配置からすべてのレポート サーバーを削除します。 詳細については、「[ネイティブ モード レポート サーバーのスケールアウト配置の構成 &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/configure-a-native-mode-report-server-scale-out-deployment.md)」を参照してください。  
  
3.  いずれかのレポート サーバーを SQL Server Reporting Services にアップグレードします。  
  
4.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成マネージャーを使用して、スケールアウト配置にレポート サーバーを再度追加します。 詳細については、「[ネイティブ モード レポート サーバーのスケールアウト配置の構成 &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/configure-a-native-mode-report-server-scale-out-deployment.md)」を参照してください。  
  
     各サーバーで、アップグレードおよびスケールアウトの手順を繰り返します。  
  
##  <a name="bkmk_sharePoint_scenarios"></a> SharePoint モードのアップグレードと移行のシナリオ  
 以降のセクションでは、指定されたバージョンの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の SharePoint モードから SQL Server Reporting Services [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の SharePoint モードにアップグレードまたは移行するために必要な基本的な手順と問題について説明します。  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint モードの配置をアップグレードするためのインストール コンポーネントは 2 つあります。  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 共有サービス。  
  
    > [!TIP]  
    >  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint コマンドレット `Get-SPRSServiceApplicationServers` を使用して、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 共有サービスを現在実行しているためアップグレードが必要なサーバーを SharePoint ファームで特定します。  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 製品用アドイン。 詳細については、「 [SharePoint 用 Reporting Services アドインのインストールまたはアンインストール](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)」を参照してください。  
  
 SharePoint モードのインストールを移行する方法については、「[Reporting Services のインストールの移行 &#40;SharePoint Mode&#41;](../../reporting-services/install-windows/migrate-a-reporting-services-installation-sharepoint-mode.md)」を参照してください。  
  
> [!IMPORTANT]  
>  次のシナリオでは、異なるテクノロジをアップグレードする必要があるため、SharePoint 環境のダウンタイムが発生する場合があります。 ダウンタイムの発生を許容できない場合は、インプレース アップグレードではなく、移行操作を実行する必要があります。  
  
### <a name="includesssql14includessssql14-mdmd-to-sql-server-reporting-services"></a>[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] を SQL Server Reporting Services に  
 **開始環境:** [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] または [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP1、SharePoint 2010 または SharePoint 2013。  
  
 **終了環境:** SQL Server Reporting Services、SharePoint 2013、または SharePoint 2016。   
  
-   **SharePoint 2013/2016:** SharePoint 2013/2016 では、SharePoint 2010 からのインプレース アップグレードがサポートされていません。 ただし、 **データベース アタッチ アップグレード**  の手順はサポートされています。
  
     SharePoint 2010 と統合された [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のインストールを使用している場合は、SharePoint サーバーのインプレース アップグレードを行うことはできません。 ただし、SharePoint 2010 ファームから SharePoint 2013/2016 ファームにコンテンツ データベースとサービス アプリケーション データベースを移行することは可能です。  
  
### <a name="includesssql11includessssql11-mdmd-to-sql-server-reporting-services"></a>[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] を SQL Server Reporting Services に  
 **開始環境:** [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] または [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)]、SharePoint 2010。  
  
 **終了環境:** SQL Server Reporting Services、SharePoint 2013、または SharePoint 2016。   
  
-   **SharePoint 2013/2016:** SharePoint 2013/2016 では、SharePoint 2010 からのインプレース アップグレードがサポートされていません。 ただし、 **データベース アタッチ アップグレード**  の手順はサポートされています。
  
     SharePoint 2010 と統合された [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のインストールを使用している場合は、SharePoint サーバーのインプレース アップグレードを行うことはできません。 ただし、SharePoint 2010 ファームから SharePoint 2013/2016 ファームにコンテンツ データベースとサービス アプリケーション データベースを移行することは可能です。  
  
### <a name="includesskilimanjaroincludessskilimanjaro-mdmd-to-sql-server-reporting-services"></a>[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] を SQL Server Reporting Services に  
 **開始環境:** [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、SharePoint 2010。  
  
 **終了環境:** SQL Server Reporting Services、SharePoint 2013、または SharePoint 2016。  
 
-   **SharePoint 2013/2016:** SharePoint 2013/2016 では、SharePoint 2010 からのインプレース アップグレードがサポートされていません。 ただし、 **データベース アタッチ アップグレード**  の手順はサポートされています。

    Reporting Services をアップグレードする前に、まず、SharePoint を移行する必要があります。
  
-   ファーム内の各 Web フロントエンドに SQL Server Reporting Services バージョンの SharePoint 用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] アドインをインストールします。 アドインをインストールするには、SQL Server Reporting Services インストール ウィザードを使うか、またはアドインをダウンロードします。  
  
-   SQL Server Reporting Services のインストールを実行し、"レポート サーバー" ごとに SharePoint モードをアップグレードします。 SQL Server インストール ウィザードによって [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サービスがインストールされ、新しいサービスのアプリケーションが作成されます。 
  
  
##  <a name="bkmk_migration_considerations"></a> 移行に関する考慮事項  
 アプリケーション データを移動する際には、次の問題と制限事項に注意する必要があります。  
  
-   暗号化キーの保護には、コンピューターの ID を組み込んだハッシュが含まれます。  
  
-   レポート サーバー データベース名は固定であり、新しいコンピューターで名前を変更することはできません。  
  
### <a name="encryption-key-considerations"></a>暗号化キーに関する考慮事項  
 レポート サーバー データベースを新しいコンピューターに移動する場合は、必ず事前に暗号化キーをバックアップします。  
  
 レポート サーバー インストールを別のコンピューターに移動すると、レポート サーバー データベースに格納されている機微なデータを保護するために使用される暗号化キーを保護するハッシュが無効になります。 データベースを使用するレポート サーバー インスタンスは、それぞれに専用の暗号化キーのコピーを保持しています。これは、現在のコンピューターで定義されたサービス アカウントの ID で暗号化されています。 コンピューターを変更すると、新しいコンピューターで同じアカウント名を使用しても、サービスはそのキーにアクセスできなくなります。  
  
 新しいレポート サーバー コンピューターで元に戻せる暗号化を再設定するには、事前にバックアップしたキーを復元する必要があります。 レポート サーバー データベースに格納されている完全なキーのセットは、対称キーの値、およびキーを格納したレポート サーバー インスタンスのみが使用できるようにキーへのアクセスを制限するための ID 情報で構成されています。 キーを復元するときに、レポート サーバーによって、キーの既存のコピーが新しいバージョンで置き換えられます。 新しいバージョンには、現在のコンピューターで定義されたコンピューター ID とサービス ID の値が含まれています。 詳細については、次の各トピックを参照してください。  
  
-   SharePoint モード: 詳細については、「[Reporting Services SharePoint サービス アプリケーションの管理](../../reporting-services/report-server-sharepoint/manage-a-reporting-services-sharepoint-service-application.md)」の「キー管理」のセクションを参照してください。  
  
-   ネイティブ モード: 「 [Reporting Services の暗号化キーのバックアップと復元](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)」を参照してください。  
  
  
### <a name="fixed-database-name"></a>固定されたデータベース名  
 レポート サーバー データベースの名前は変更できません。 データベースの ID は、データベース作成時にレポート サーバーのストアド プロシージャで記録されます。 レポート サーバーのプライマリ データベースまたは一時データベースの名前を変更すると、プロシージャ実行時にエラーが発生し、レポート サーバー インストールが無効になります。  
  
 既存のインストールのデータベース名が新しいインストールに適さない場合は、適切な名前で新しいデータベースを作成し、以下の方法で既存のアプリケーション データを読み込むことを検討してください。  
  
-   レポート サーバー Web サービスの SOAP メソッドを呼び出してデータベース間でデータをコピーする [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] スクリプトを作成します。 スクリプトの実行には RS.exe ユーティリティを使用できます。 この方法の詳細については、「 [Reporting Services を使ったスクリプトの作成と PowerShell](../../reporting-services/tools/scripting-and-powershell-with-reporting-services.md)」を参照してください。  
  
-   WMI プロバイダーを呼び出してデータベース間でデータをコピーするコードを記述します。 このアプローチの詳細については、「 [Reporting Service WMI プロバイダーへのアクセス](../../reporting-services/tools/access-the-reporting-services-wmi-provider.md)」を参照してください。  
  
-   アイテム数が少ない場合は、レポート デザイナー、モデル デザイナー、およびレポート ビルダーから新しいレポート サーバーに、レポートおよび共有データ ソースを再パブリッシュできます。 ロールの割り当て、サブスクリプション、共有スケジュール、レポート スナップショット スケジュール、レポートやその他のアイテムに設定したカスタム プロパティ、モデル アイテム セキュリティ、およびレポート サーバーで設定したプロパティを再作成する必要があります。 レポート履歴およびレポート実行ログ データは失われます。  
  
  
##  <a name="bkmk_additional_resources"></a> その他のリソース  
  
> [!NOTE]  
>  SharePoint データベース アタッチ アップグレードの詳細については、以下を参照してください。  
  
-   [SharePoint 2016 へのアップグレード プロセスの概要](https://technet.microsoft.com/library/cc262483\(v=office.16\))

-   [SharePoint 2013 へのアップグレード プロセスの概要](https://go.microsoft.com/fwlink/p/?LinkId=256688)。
  
-   [SharePoint 2013 へのアップグレードの前に環境をクリーンアップする](https://go.microsoft.com/fwlink/p/?LinkId=256689)  
  
-   [SharePoint 2013 から SharePoint Server 2016 にデータベースをアップグレードする](https://technet.microsoft.com/library/cc303436\(v=office.16\))

-   [SharePoint 2010 から SharePoint 2013 にデータベースをアップグレードする](https://go.microsoft.com/fwlink/p/?LinkId=256690)。  

## <a name="next-steps"></a>次の手順

[レポートのアップグレード](../../reporting-services/install-windows/upgrade-reports.md)   
[インストール ウィザードを使用した SQL Server 2016 へのアップグレード &#40;セットアップ&#41;](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)  

その他の質問 [Reporting Services のフォーラムに質問してみてください](https://go.microsoft.com/fwlink/?LinkId=620231)
