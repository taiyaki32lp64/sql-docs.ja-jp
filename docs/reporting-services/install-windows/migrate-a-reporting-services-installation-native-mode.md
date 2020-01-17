---
title: Reporting Services のインストールの移行 (ネイティブ モード) | Microsoft Docs
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
ms.date: 11/06/2018
ms.openlocfilehash: 5db33f22ffd5143d88c5654c753f1b08811c0c8a
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68262899"
---
# <a name="migrate-a-reporting-services-installation-native-mode"></a>Reporting Services のインストールの移行 (ネイティブ モード)

ここでは、[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のネイティブ モード配置でサポートされている次のいずれかのバージョンを新しい SQL Server Reporting Services インスタンスに移行する手順について説明します。  
  
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
* [!INCLUDE[ssSQL16](../../includes/sssql16-md.md)]

* [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
  
* [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
  
* [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]  
  
* [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]
::: moniker-end

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
* [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
  
* [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
  
* [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]  
  
* [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]

[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint モード配置を移行する方法については、「[Reporting Services の移行 &#40; SharePoint モード&#41;](../../reporting-services/install-windows/migrate-a-reporting-services-installation-sharepoint-mode.md)」をご覧ください。  

::: moniker-end
  
 移行とは、新しい SQL Server インスタンスにアプリケーション データ ファイルを移動することを指します。 以下は、インストールを移行する必要がある一般的な理由です。  
  
* 大規模な配置や稼働時間の要件がある。  
  
* インストールのハードウェアやトポロジを変更している。  
  
* アップグレードを妨げる問題が発生している。

## <a name="bkmk_nativemode_migration_overview"></a> ネイティブ モードの移行の概要

 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の移行プロセスには、手動による手順と自動化された手順があります。 レポート サーバーの移行の一環として、次の作業を実行します。  
  
* データベース、アプリケーション、および構成ファイルをバックアップします。  
  
* 暗号化キーをバックアップします。  
  
* SQL Server の新しいインスタンスをインストールします。 同じハードウェアを使用する場合、SQL Server は、インストールされているバージョン (サポートされているバージョンのいずれかの場合) とサイド バイ サイドでインストールできます。  
  
    > [!TIP]  
    >  サイド バイ サイド インストールを実行するには、SQL Server を名前付きインスタンスとしてインストールする必要があります。
  
* レポート サーバー データベースおよびその他のアプリケーション ファイルを、既にインストールされている SQL Server から、新しくインストールした SQL Server に移動します。  
  
* 任意のカスタム アプリケーション ファイルを新しいインストールに移動します。  
  
* レポート サーバーを構成します。  
  
* **RSReportServer.config** を編集して、以前のインストールからすべてのカスタム設定を含めます。  
  
* 必要に応じて、新しい [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Windows サービス グループについて、カスタムのアクセス制御リスト (ACL) を構成します。  
  
* 新しいインスタンスが完全に動作することを確認してから、使用しないアプリケーションおよびツールを削除します。  
  
 レポート サーバー データベースをホストする [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のエディションによっては制限があります。 以前のインストールで作成したレポート サーバー データベースを再利用する場合は、次のトピックを確認してください。  
  
* [レポート サーバー データベースの作成](../../reporting-services/install-windows/ssrs-report-server-create-a-report-server-database.md)  
  
## <a name="bkmk_fixed_database_name"></a> 固定されたデータベース名

 レポート サーバー データベースの名前は変更できません。 データベースの ID は、データベース作成時にレポート サーバーのストアド プロシージャで記録されます。 レポート サーバーのプライマリ データベースまたは一時データベースの名前を変更すると、プロシージャ実行時にエラーが発生し、レポート サーバー インストールが無効になります。  
  
 既存のインストールのデータベース名が新しいインストールに適さない場合は、適切な名前で新しいデータベースを作成し、以下の方法で既存のアプリケーション データを読み込むことを検討してください。  
  
* レポート サーバー Web サービスの SOAP メソッドを呼び出してデータベース間でデータをコピーする [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] スクリプトを作成します。 スクリプトの実行には RS.exe ユーティリティを使用できます。 この方法の詳細については、「 [Reporting Services を使ったスクリプトの作成と PowerShell](../../reporting-services/tools/scripting-and-powershell-with-reporting-services.md)」を参照してください。  
  
* WMI プロバイダーを呼び出してデータベース間でデータをコピーするコードを記述します。 このアプローチの詳細については、「 [Reporting Service WMI プロバイダーへのアクセス](../../reporting-services/tools/access-the-reporting-services-wmi-provider.md)」を参照してください。  
  
* アイテム数が少ない場合は、レポート デザイナー、モデル デザイナー、およびレポート ビルダーから新しいレポート サーバーに、レポートおよび共有データ ソースを再パブリッシュできます。 ロールの割り当て、サブスクリプション、共有スケジュール、レポート スナップショット スケジュール、レポートやその他のアイテムに設定したカスタム プロパティ、モデル アイテム セキュリティ、およびレポート サーバーで設定したプロパティを再作成します。 これらのアクションを行う場合は、レポート履歴やレポートの実行ログ データの損失に備えてください。
  
## <a name="bkmk_before_you_start"></a> 開始前の準備

 アップグレードではなく移行を行う場合でも、既存のインストールでアップグレード アドバイザーの実行を検討してください。移行に影響する問題を識別できる場合があります。 この手順は、インストールまたは構成していないレポート サーバーを移行する場合に特に役立ちます。 アップグレード アドバイザーを実行すると、新しくインストールする SQL Server でサポートされない可能性があるカスタム設定を確認できます。  
  
 また、インストールの移行方法に影響する SQL Server Reporting Services での以下の重要な変更点に注意してください。

* 新しい [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] でレポート マネージャーは置き換えられました。
  
* [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]以降、IIS は必須ではなくなりました。 インストールされているレポート サーバーを新しいコンピューターに移行する場合、Web サーバーの役割を追加する必要はありません。 また、URL および認証を構成する手順が以前のリリースとは異なり、問題の診断およびトラブルシューティングの手法やツールも変更になっています。  
  
* レポート サーバー Web サービス、 [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)]、およびレポート サーバー Windows サービスは、同じアカウントで実行されます。 3 つのアプリケーションはいずれも RSReportServer.config ファイルから構成設定を読み取ります。
  
* [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] および SQL Server Management Studio の設計が変更され、重複する機能が削除されました。 各ツールは、それぞれ別のタスクをサポートします。
  
* ISAPI フィルターは、 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 以降のバージョンではサポートされません。 ISAPI フィルターを使用する場合、移行を実行する前にレポート ソリューションを設計し直す必要があります。  
  
* IP アドレス制限は、 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 以降のバージョンではサポートされません。 IP アドレス制限を使用する場合、移行を実行する前にレポート ソリューションを設計し直すか、ファイアウォール、ルーター、ネットワーク アドレス変換 (NAT) などのテクノロジを使用して、レポート サーバーへのアクセスが制限されるアドレスを構成する必要があります。  
  
* クライアント SSL (Secure Sockets Layer) 証明書は、 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 以降のバージョンではサポートされません。 クライアント SSL 証明書を使用する場合、移行を実行する前にレポート ソリューションを設計し直す必要があります。  
  
* Windows 統合認証以外の認証の種類を使用する場合、サポートされている認証の種類で **RSReportServer.config** ファイルの`<AuthenticationTypes>` 要素を更新する必要があります。 サポートされている認証の種類は、NTLM、Kerberos、Negotiate、および Basic です。 匿名認証、.NET パスポート認証、およびダイジェスト認証は、 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 以降のバージョンではサポートされません。  
  
* カスタムのカスケード スタイル シートをレポート環境で使用している場合、そのスタイル シートは移行できません。 移行後に手動で移動します。
  
SQL Server Reporting Services の変更点の詳細については、アップグレード アドバイザーのマニュアルおよび「[Reporting Services の新機能](../../reporting-services/what-s-new-in-sql-server-reporting-services-ssrs.md)」をご覧ください。  

## <a name="bkmk_backup"></a> ファイルおよびデータのバックアップ

 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]の新しいインスタンスをインストールする前に、現在インストールされているすべてのファイルを必ずバックアップしてください。  
  
1. レポート サーバー データベースの暗号化キーをバックアップします。 これは、移行を正しく行うための重要な手順です。 移行プロセスの後の方で、暗号化されたデータへのレポート サーバーからのアクセスを復旧するために、このキーを復元する必要があります。 キーをバックアップするには、Reporting Services 構成マネージャーを使用してください。  
  
2. サポートされている任意の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベース バックアップ方法で、レポート サーバー データベースをバックアップします。 詳細については、「[別のコンピューターへのレポート サーバー データベースの移動 &#40;SSRS ネイティブ モード&#41;](../../reporting-services/report-server/moving-the-report-server-databases-to-another-computer-ssrs-native-mode.md)」にあるレポート サーバー データベースのバックアップ方法に関する指示をご覧ください。  
  
3. レポート サーバーの構成ファイルをバックアップします。 バックアップするのは次のファイルです。  
  
    1. RSReportServer.config  
  
    2. Rswebapplication.config  
  
    3. Rssvrpolicy.config  
  
    4. Rsmgrpolicy.config  
  
    5. Reportingservicesservice.exe.config  
  
    6. レポート サーバーの [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] アプリケーション用の Web.config  
  
    7. [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 用の Machine.config (レポート サーバー操作用に変更している場合)  

## <a name="bkmk_install_ssrs"></a> SQL Server Reporting Services のインストール

 新しいレポート サーバー インスタンスを、既定値以外の値で構成できるように、ファイルのみのモードでインストールします。 コマンド ラインからインストールする場合は、**FilesOnly** 引数を使用します。 インストール ウィザードでは、 **[サーバーを構成せずにインストールする]** を選択します。  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]の新しいインスタンスのインストール手順については、次のいずれかのリンクをクリックして参照してください。  
  
* [SQL Server をインストール ウィザードからインストールする &#40;セットアップ&#41;](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)  
  
* [コマンド プロンプトからの SQL Server のインストール](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)  

## <a name="bkmk_move_database"></a> レポート サーバー データベースの移動

 レポート サーバー データベースには、パブリッシュされたレポート、モデル、共有データ ソース、スケジュール、リソース、サブスクリプション、およびフォルダーが格納されます。 また、システム プロパティとアイテム プロパティ、およびレポート サーバー コンテンツにアクセスするための権限も格納されています。  
  
 移行に伴い、使用する [!INCLUDE[ssDE](../../includes/ssde-md.md)] インスタンスの変更も行う場合は、レポート サーバー データベースを新しい [!INCLUDE[ssDE](../../includes/ssde-md.md)] インスタンスに移動する必要があります。 同じ [!INCLUDE[ssDE](../../includes/ssde-md.md)] インスタンスを使っている場合は、「 [カスタム アセンブリや拡張機能の移動](#bkmk_move_custom)」セクションに進んでください。  
  
 レポート サーバー データベースを移動するには、次の手順を行います。
  
1. 使用する [!INCLUDE[ssDE](../../includes/ssde-md.md)] インスタンスを選択します。 SQL Server Reporting Services レポート サーバー データベースをホストするために次のいずれかのバージョンを使用する必要があります。  
  
    ::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
    * [!INCLUDE[ssSQL16](../../includes/sssql16-md.md)]

    * [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
  
    * [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
  
    * [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]  
  
    * [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]
    ::: moniker-end

    ::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
    * [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  

    * [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  

    * [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]  

    * [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]
    ::: moniker-end
  
2. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を起動し、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]に接続します。  
  
3. その **でレポート サーバー データベースをホストしたことがない場合は、システム データベースで** RSExecRole [!INCLUDE[ssDE](../../includes/ssde-md.md)] を作成します。 詳細については、「 [RSExecRole の作成](../../reporting-services/security/create-the-rsexecrole.md)」をご覧ください。  
  
4. 「[別のコンピューターへのレポート サーバー データベースの移動 &#40;SSRS ネイティブ モード&#41;](../../reporting-services/report-server/moving-the-report-server-databases-to-another-computer-ssrs-native-mode.md)」の指示に従います。  
  
 レポート サーバー データベースと一時データベースは相互に依存するため、一緒に移動する必要があることに注意してください。 データベースをコピーしても新しいインストールにセキュリティ設定がすべて移行されるわけではないため、コピーは使用しないでください。 スケジュールされたレポート サーバー操作の SQL Server エージェント ジョブは移動しないでください。 これらのジョブは、レポート サーバーで自動的に再作成されます。  

## <a name="bkmk_move_custom"></a> カスタム アセンブリや拡張機能の移動

 インストールにカスタム レポート アイテム、アセンブリ、または拡張機能が含まれている場合、それらのカスタム コンポーネントを再配置する必要があります。 カスタム コンポーネントを使用していない場合は、「 [レポート サーバーの構成](#bkmk_configure_reportserver)」に進んでください。  
  
 カスタム コンポーネントを再配置するには、次の手順を行います。  
  
1. アセンブリがサポートされているか、または再コンパイルが必要かを確認します。

    * カスタム セキュリティ拡張機能は、[IAuthenticationExtension2](https://msdn.microsoft.com/library/microsoft.reportingservices.interfaces.iauthenticationextension2.aspx) インターフェイスを使用して記述し直す必要があります。
  
    * [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のカスタム表示拡張機能は、表示オブジェクト モデル (ROM) を使用して記述し直す必要があります。  
  
    * HTML 3.2 レンダラーおよび HTML OWC レンダラーは、 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 以降のバージョンではサポートされません。  
  
    * それ以外のカスタム アセンブリを再コンパイルする必要はありません。  
  
2. アセンブリを新しいレポート サーバーの \bin フォルダーに移動します。 SQL Server では、既定のレポート サーバー インスタンスにおけるレポート サーバーのバイナリは次の場所にあります。  
  
     `\Program files\Microsoft SQL Server\MSRS13.MSSQLSERVER\Reporting Services\ReportServer\bin`  
  
3. 構成ファイルを変更してカスタム コンポーネントのエントリを追加します。 エントリは、使用するアセンブリの種類によって異なります。 ファイルの配置場所および構成エントリの追加位置については、以下を参照してください。  
  
    1. [カスタム アセンブリの配置](../../reporting-services/custom-assemblies/deploying-a-custom-assembly.md)  
  
    2. [カスタム レポート アイテムを配置する方法](../../reporting-services/custom-report-items/how-to-deploy-a-custom-report-item.md)  
  
    3. [データ処理拡張機能の配置](../../reporting-services/extensions/data-processing/deploying-a-data-processing-extension.md)  
  
    4. [配信拡張機能の配置](../../reporting-services/extensions/delivery-extension/deploying-a-delivery-extension.md)  
  
    5. [表示拡張機能の配置](../../reporting-services/extensions/rendering-extension/deploying-a-rendering-extension.md)  
  
    6. [セキュリティ拡張機能の実装](../../reporting-services/extensions/security-extension/implementing-a-security-extension.md)  

## <a name="bkmk_configure_reportserver"></a> レポート サーバーの構成

 レポート サーバー Web サービスと Web ポータルの URL を構成し、レポート サーバー データベースへの接続を構成します。  
  
 スケールアウト配置を移行する場合、すべてのレポート サーバー ノードをオフラインにし、一度に 1 つずつサーバーを移行します。 最初のレポート サーバーを移行し、レポート サーバー データベースに正常に接続すると、レポート サーバー データベースのバージョンは自動的に SQL Server データベースのバージョンにアップグレードされます。  
  
> [!IMPORTANT]
>  スケールアウト配置内にオンラインで、移行されていないレポート サーバーがある場合、アップグレードされたデータベースへの接続時に古いスキーマが使用されるため、*rsInvalidReportServerDatabase* 例外が発生する場合があります。  

移行したレポート サーバーがスケールアウト配置用の共有データベースとして構成されていた場合、**ReportServer** データベースの **Keys** テーブルから古い暗号化キーをすべて削除した後で、レポート サーバー サービスを構成する必要があります。 このキーが削除されていない場合、移行したレポート サーバーでは、スケールアウト配置モードで初期化が試行されます。 詳細については、「[スケールアウト配置に関する暗号化キーの追加と削除 &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/add-and-remove-encryption-keys-for-scale-out-deployment.md)」と「[暗号化キーの構成と管理 &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md)」をご覧ください。  

このスケールアウト キーは、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成マネージャーでは削除できません。 SQL Server Management Studio を使用して、 **ReportServer** データベースの **Keys** テーブルから古いキーを削除する必要があります。 Keys テーブル内のすべての行を削除します。 このアクションによってテーブルがクリアされ、以降の手順に示すように、対称キーのみを復元できるように準備されます。  

キーを削除する前に、対称暗号化キーをバックアップしておくことをお勧めします。 キーのバックアップには、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成マネージャーを使用できます。 Configuration Manager を開き、[暗号化キー] タブをクリックし、 **[バックアップ]** ボタンをクリックします。 スクリプト WMI コマンドを使用して暗号化キーをバックアップすることもできます。 WMI の詳細については、「[BackupEncryptionKey メソッド &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-backupencryptionkey.md)」をご覧ください。  
  
1. Reporting Services Configuration Manager を起動し、インストールした [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] インスタンスに接続します。 詳細については、「 [Reporting Services 構成マネージャー &#40;ネイティブ モード&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)」を参照してください。  
  
2. レポート サーバーと Web ポータルの URL を構成します。 詳細については、「[URL の構成 &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)」をご覧ください。  
  
3. 以前のインストールから既存のレポート サーバー データベースを選択して、レポート サーバー データベースを構成します。 正常に構成された後、レポート サーバー サービスが再開されます。また、レポート サーバー データベースへの接続が確立されると、データベースが自動的に SQL Server Reporting Services にアップグレードされます。 データベースの変更ウィザードを使用してレポート サーバー データベースを作成または選択する方法の詳細については、「[ネイティブ モード レポート サーバー データベースの作成](../../reporting-services/install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md)」をご覧ください。  
  
4. 暗号化キーを復元します。 この手順は、レポート サーバー データベースの既存の接続文字列および資格情報の暗号化を解除できるようにするために実行する必要があります。 詳細については、「 [Back Up and Restore Reporting Services Encryption Keys](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)」を参照してください。  
  
5. レポート サーバーを新しいコンピューターにインストールし、Windows ファイアウォールを使用している場合は、レポート サーバーがリッスンする TCP ポートが開いていることを確認します。 既定のポート番号は 80 です。 詳細については、「 [レポート サーバー アクセスに対するファイアウォールの構成](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md)」をご覧ください。  
  
6. ネイティブ モードのレポート サーバーをローカルで管理する場合は、Web ポータルによるローカル管理を許可するようにオペレーティング システムを構成する必要があります。 詳細については、「[ローカル管理用のネイティブ モードのレポート サーバーの構成](../../reporting-services/report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md)」を参照してください。  

## <a name="bkmk_copy_custom_config"></a> RSReportServer.config ファイルへのカスタム構成設定のコピー

以前のインストールで RSReportServer.config ファイルまたは RSWebApplication.config ファイルを変更していた場合、新しい RSReportServer.config ファイルで同じ変更を行います。 以前の構成ファイルで変更された可能性があるいくつかの項目と、SQL Server 2016 で同じ設定を構成するための方法に関する追加情報へのリンクを次に示します。  
  
|カスタマイズ|[情報]|  
|-------------------|-----------------|  
|カスタム設定を使用したレポート サーバーの電子メール配信|[電子メールの設定 * Reporting Services のネイティブ モード](../../reporting-services/install-windows/e-mail-settings-reporting-services-native-mode-configuration-manager.md)|  
|デバイス情報設定|[RSReportServer.Config で表示拡張機能パラメーターをカスタマイズする](../../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md)|

## <a name="bkmk_windowsservice_group"></a> Windows サービス グループとセキュリティ ACL

 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] には、[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Windows サービス グループという 1 つのサービス グループがあります。このサービス グループは、SQL Server Reporting Services と共にインストールされたすべてのレジストリ キー、ファイル、およびフォルダーのセキュリティ ACL を作成するために使用されます。 この Windows グループ名は SQLServerReportServerUser$\<*computer_name*>$\<*instance_name*> という形式で表示されます。  

## <a name="bkmk_verify"></a> 配置の確認

1. ブラウザーを開き、URL アドレスを入力して、レポート サーバーおよび [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] の仮想ディレクトリをテストします。 詳細については、「 [Reporting Services のインストール状態の検証](../../reporting-services/install-windows/verify-a-reporting-services-installation.md)」をご覧ください。  
  
2. レポートをテストし、レポートに意図したデータが含まれることを確認します。 データ ソース情報で、データ ソース接続情報が指定されたままになっているかどうかを確認します。 レポート サーバーでは、レポートを処理および表示する際にレポート オブジェクト モデルが使用されますが、[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]、[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]、または [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] の構造は新しいレポート定義言語要素には置き換えられません。 新しいバージョンのレポート サーバーで既存のレポートが実行される方法の詳細については、「[レポートのアップグレード](../../reporting-services/install-windows/upgrade-reports.md)」をご覧ください。  

## <a name="bkmk_remove_unused"></a> 使用しないプログラムおよびファイルの削除

レポート サーバーを新しいインスタンスに正常に移行したら、次の手順に従って、不要になったプログラムとファイルを削除できます。  
  
1. 以前のバージョンの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] が不要になった場合はアンインストールします。 この手順を実行しても、次の項目は削除されません。ただし、これらの項目が不要な場合は、手動で削除できます。  
  
    * 古いレポート サーバー データベース  
  
    * RsExec ロール  
  
    * レポート サーバーのサービス アカウント  
  
    * レポート サーバー Web サービスに使用するアプリケーション プール  
  
    * レポート マネージャーおよびレポート サーバー用の仮想ディレクトリ  
  
    * レポート サーバーのログ ファイル  
  
2. このコンピューター上で IIS が不要になった場合は削除します。

## <a name="next-steps"></a>次の手順

* [Reporting Services のインストールを移行する](../../reporting-services/install-windows/migrate-a-reporting-services-installation-sharepoint-mode.md)  
* [レポート サーバー データベース](../../reporting-services/report-server/report-server-database-ssrs-native-mode.md)   
* [Reporting Services のアップグレードと移行](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)   
* [Reporting Services の旧バージョンとの互換性](../../reporting-services/reporting-services-backward-compatibility.md)   
* [Reporting Services 構成マネージャー](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)  

その他の質問 [Reporting Services のフォーラムに質問してみてください](https://go.microsoft.com/fwlink/?LinkId=620231)
