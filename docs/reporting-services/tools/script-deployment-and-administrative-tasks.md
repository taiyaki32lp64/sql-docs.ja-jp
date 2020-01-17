---
title: 配置タスクおよび管理タスクのスクリプト作成 | Microsoft Docs
ms.date: 05/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: tools
ms.topic: conceptual
helpviewer_keywords:
- scripts [Reporting Services]
- moving reports
- report servers [Reporting Services], duplicating settings
- deploying [Reporting Services], scripts
- copying report server settings
- administrative tasks [Reporting Services]
- duplicating report server environment
- migrating reports [Reporting Services]
- scripts [Reporting Services], deployments
- transferrng reports
- reports [Reporting Services], migrating
ms.assetid: d0416c9e-e3f9-456d-9870-2cfd2c49039b
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 694a2c4c14564a1d3d57322e1300beddd8bfab98
ms.sourcegitcommit: 1800fc15075bb17b50d0c18b089d8a64d87ae726
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2019
ms.locfileid: "66500568"
---
# <a name="script-deployment-and-administrative-tasks"></a>配置タスクおよび管理タスクのスクリプト作成

  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] は、スクリプトを使用した日常的なインストール、配置、および管理タスクの自動化をサポートします。 レポート サーバーの配置は複数の段階を伴うプロセスです。 配置を構成するためには複数のツールとプロセスを使用する必要があります。すべての作業を自動化する単一のプログラムやアプローチは存在しません。  
  
 すべての手順を自動化することが必ずしも有効な手段ではありません。 場合によっては、手作業またはグラフィカルなツールで作業することが、最も効率的かつシンプルな手段になる場合もあります。 たとえば、大量のレポートやモデルを配置する必要がある場合、レポート サーバー環境を再構築するようなコードを作成するよりも、レポート サーバー データベースをコピーした方が効率的です。  
  
 中には、カスタム コードを必要とする手順もあります。 たとえば、Web サービスとレポート マネージャーの URL の構成は自動化できますが、そのためには、レポート サーバーの Windows Management Instrumentation (WMI) プロバイダーを呼び出すカスタム コードを作成しなければなりません。 なんらかの理由でコードを作成したくない場合は、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ツールを使用して、この手順を実行する必要があります。  
  
 レポート サーバーを構成するスクリプトを実行するには、構成するコンピューターのローカル管理者である必要があります。 詳細については、「 [リモート管理用のレポート サーバーの構成](../../reporting-services/report-server/configure-a-report-server-for-remote-administration.md)」を参照してください。  
  
 このトピックでは、特定の手順を自動化する際に推奨されるアプローチについて説明します。 いくつかのプログラムやプログラム インターフェイスに触れ、このトピックでそれぞれについて後述します。  
  
## <a name="deployment-tasks-and-how-to-automate-them"></a>配置タスクと自動化の方法  
 次の表は、レポート サーバーを配置するために必要なインストール タスクおよび構成タスクをまとめたものです。 特定のタスクと、それを自動化するためのアプローチがひとめでわかるように記載されています。  
  
|タスク|アプローチ|  
|----------|--------------|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]をインストールする。|コマンド ラインからセットアップを実行することによって自動インストールが可能です。<br /><br /> セットアップ プログラムを使用すると、レポート サーバーのインストールと構成の両方を行うことができます。ただし、この場合は、既定の構成オプションを指定すること、システムが自動インストール要件をすべて満たしていることが条件となります。 既定の構成でインストールすることができない場合は、ファイルのみのインストールを実行する必要があります。|  
|サービス アカウントを構成する。|サービス アカウントは、最初にセットアップを使用して構成されます。 サービス アカウントに対する変更をセットアップ後のタスクとして自動化するには、レポート サーバー WMI プロバイダーを呼び出すカスタム コードを作成する必要があります。 サービス アカウントをプログラムによって構成するためのコマンド プロンプト ユーティリティやスクリプト テンプレートはありません。<br /><br /> コードを作成するのが困難であるなど、なんらかの理由でこの手順を自動化できない場合は、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ツールを実行することにより、アカウントを手動で簡単に構成できます。 詳細については、「[サービス アカウントの構成 (SSRS 構成マネージャー)](../install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)」を参照してください。|  
|レポート サーバー Web サービスとレポート マネージャーの URL を構成する。|レポート サーバー WMI プロバイダーを呼び出すカスタム コードを作成する必要があります。 URL を構成するためのコマンド ライン ユーティリティやスクリプト テンプレートはありません。<br /><br /> [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ツールを実行して URL を手動で構成した場合、コードを作成する必要はありません。 詳細については、「[URL の構成 &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)」をご覧ください。|  
|レポート サーバー データベースを作成する。|レポート サーバー WMI プロバイダーを呼び出すカスタム コードを作成する必要があります。 レポート サーバー データベースと RSExecRole を作成するためのコマンド プロンプト ユーティリティやスクリプト テンプレートはありません。<br /><br /> [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ツールを実行してデータベースを手動で作成した場合、コードを作成する必要はありません。 詳細については、「[ネイティブ モードのレポート サーバー データベースの作成 (SSRS 構成マネージャー)](../../reporting-services/install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md)」を参照してください。|  
|レポート サーバー データベース接続を構成する。|接続文字列、アカウントまたはパスワード、認証の種類を変更する場合は、 **rsconfig** ユーティリティを実行して接続を構成します。 詳細については、「[レポート サーバー データベース接続の構成 &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md)」および「[rsconfig ユーティリティ &#40;SSRS&#41;](../../reporting-services/tools/rsconfig-utility-ssrs.md)」を参照してください。<br /><br /> データベースの作成またはアップグレードに rsconfig.exe を使用することはできません。 データベースと RSExecRole が既に存在している必要があります。|  
|スケールアウト配置を構成する。|スケールアウト配置を自動化するには、次のいずれかのアプローチを使用します。<br /><br /> -   rskeymgmt.exe ユーティリティを実行して、レポート サーバー インスタンスを既存の環境に追加する。 詳細については、「[スケールアウト配置に関する暗号化キーの追加と削除 &#40;SSRS構成マネージャー&#41;](../../reporting-services/install-windows/add-and-remove-encryption-keys-for-scale-out-deployment.md)」を参照してください。<br />-   レポート サーバー WMI プロバイダーに対して実行するカスタム コードを作成する。|  
|暗号化キーをバックアップする。|暗号化キーのバックアップを自動化するには、次のいずれかのアプローチを使用します。<br /><br /> -   rskeymgmt.exe ユーティリティを実行してキーをバックアップする。 詳細については、「 [Back Up and Restore Reporting Services Encryption Keys](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)」を参照してください。<br />-   レポート サーバー WMI プロバイダーに対して実行するカスタム コードを作成する。|  
|レポート サーバーの電子メールを構成する。|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] WMI プロバイダーに対して実行するカスタム コードを作成します。 プロバイダーでは、電子メールの構成設定のサブセットがサポートされています。<br /><br /> RSReportServer.config ファイルにはすべての設定が含まれていますが、このファイルの使用を自動化しないようにしてください。 特に、ファイルを別のレポート サーバーにコピーする場合は、バッチ ファイルを使用しないでください。 各構成ファイルには、現在のインスタンスに固有の値が含まれています。 これらの値は、別のレポート サーバー インスタンスでは無効になります。<br /><br /> 設定の詳細については、次を参照してください。[電子メールの設定 - Reporting Services ネイティブ モード (構成マネージャー)](../install-windows/e-mail-settings-reporting-services-native-mode-configuration-manager.md)します。|  
|自動実行アカウントを構成する。|自動実行アカウントの構成を自動化するには、次のいずれかのアプローチを使用します。<br /><br /> -   rsconfig.exe ユーティリティを実行してアカウントを構成する。 詳細については、「[自動実行アカウントを構成する &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)」を参照してください。<br />-   レポート サーバー WMI プロバイダーを呼び出すカスタム コードを作成する。|  
|既存のコンテンツを別のレポート サーバー上に配置する (フォルダー階層、ロールの割り当て、レポート、サブスクリプション、スケジュール、データ ソース、リソースなど)。|既存のレポート サーバー環境を再構築する最善の方法は、レポート サーバー データベースを新しいレポート サーバー インスタンスにコピーすることです。<br /><br /> カスタム コードを作成して、既存のレポート サーバーのコンテンツをプログラムによって再構築する方法もあります。 ただし、サブスクリプション、レポート スナップショット、レポート履歴は、プログラムによって再作成できないことに注意してください。<br /><br /> 場合によっては両者を組み合わせた方法も効果的です (つまり、レポート サーバー データベースを復元してから、カスタム コードによって、特定の環境に合わせてレポート サーバー データベースを更新します)。<br /><br /> 詳細な例については、「 [レポート サーバー間でコンテンツをコピーするサンプル Reporting Services rs.exe スクリプト](../../reporting-services/tools/sample-reporting-services-rs-exe-script-to-copy-content-between-report-servers.md)」を参照してください。<br /><br /> レポート サーバー データベースの再配置の詳細については、「[別のコンピューターへのレポート サーバー データベースの移動 &#40;SSRS ネイティブ モード&#41;](../../reporting-services/report-server/moving-the-report-server-databases-to-another-computer-ssrs-native-mode.md)」を参照してください。 レポート サーバー環境をプログラムによって構築する方法の詳細については、このトピックの「スクリプトを使用したレポート サーバー コンテンツとフォルダーの移行」を参照してください。|  
  
## <a name="tools-and-technologies-for-automating-server-deployment"></a>サーバー配置を自動化するためのツールと技法  
 配置タスクとメンテナンス タスクを自動化するためのプログラムおよびインターフェイスを次に示します。  
  
-   セットアップ プログラムを自動モードで実行して、レポート サーバー コンポーネントのインストールから、場合によっては構成までを行うことができます。 ファイルのみのインストール オプションを使用して、セットアップ時にレポート サーバー インスタンスが構成されるようにする必要があります。  
  
-   ローカル サーバーとリモート サーバーの構成には、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] WMI プロバイダーおよび [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のコマンド ライン ユーティリティを使用できます。  
  
     [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] WMI プロバイダーは、サービス アカウントの指定、URL の構成、レポート サーバー データベースの作成と構成、電子メール配信用のレポート サーバーの構成など、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のインストールのあらゆる機能を構成するための、クラス、プロパティ、およびメソッドを公開します。 WMI プロバイダーを使用するには、カスタム コードまたはスクリプトを作成する必要があります。 詳細については、「 [Reporting Service WMI プロバイダーへのアクセス](../../reporting-services/tools/access-the-reporting-services-wmi-provider.md)」を参照してください。  
  
     コードを作成する代わりに、コマンド ライン ユーティリティ (rsconfig.exe および rskeymgmt.exe) を使用することもできます。 これらのユーティリティを実行するバッチ ファイルを作成できます。 構成タスクの一部は、これらのユーティリティを使って自動化できます。  
  
-   既存のコンテンツを再構築したり、レポート サーバーからレポート サーバーに移動したりするためのカスタム コードを [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] で作成し、レポート サーバーのスクリプト ホスト ツール (rs.exe) で実行できます。 このアプローチでは、 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]でスクリプトを作成して .rss ファイルとして保存し、そのスクリプトを rs.exe を使用して、対象レポート サーバー上で実行します。 作成するスクリプトでは、レポート サーバー Web サービスに対する SOAP インターフェイスを呼び出すことができます。 配置スクリプトは、レポート サーバー フォルダーの名前空間および内容の再作成や、ロールベースのセキュリティの再作成を可能にするため、このアプローチで作成します。  
  
-   SQL Server 2012 リリースでは、SharePoint 統合モード用の PowerShell コマンドレットが導入されました。 PowerShell を使用して、SharePoint 統合を構成および管理することができます。  詳細については、「 [Reporting Services SharePoint モード用の PowerShell コマンドレット](../../reporting-services/report-server-sharepoint/powershell-cmdlets-for-reporting-services-sharepoint-mode.md)」をご覧ください。  
  
## <a name="use-scripts-to-migrate-report-server-content-and-folders"></a>スクリプトを使用したレポート サーバー コンテンツとフォルダーの移行  
 レポート サーバー環境を別のレポート サーバー インスタンスに複製するためのスクリプトを作成できます。 配置スクリプトは、一般的には [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] で作成し、レポート サーバーのスクリプト ホスト ユーティリティで処理します。  
  
 詳細な例については、「 [レポート サーバー間でコンテンツをコピーするサンプル Reporting Services rs.exe スクリプト](../../reporting-services/tools/sample-reporting-services-rs-exe-script-to-copy-content-between-report-servers.md)」を参照してください。  
  
 スクリプトを使用して、フォルダー、共有データ ソース、リソース、レポート、ロールの割り当て、および設定を、あるサーバーから別のサーバーにコピーします。 1 つのレポート サーバー インスタンス用のスクリプトを作成してから、そのスクリプトを別のサーバーで実行して、レポート サーバー名前空間を再作成します。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] で、複数のレポート サーバーを配置している場合は、各サーバーで個別にスクリプトを実行して、すべてのサーバーを同様に構成できます。  
  
 次の一覧で、あるサーバーから別のサーバーにレポートを移行する手順を示します。  
  
1.  スクリプト変数を移行元レポート サーバーの URL に設定します。  
  
2.  <xref:ReportService2010.ReportingService2010.GetItemDefinition%2A> メソッドおよび <xref:ReportService2010.ReportingService2010.GetProperties%2A> メソッドを使用して、レポートのレポート定義およびプロパティを取得します。  
  
3.  移行先サーバーを指すように URL を設定します。  
  
4.  <xref:ReportService2010.ReportingService2010.CreateCatalogItem%2A> メソッドを使用し、<xref:ReportService2010.ReportingService2010.GetProperties%2A> から返されたプロパティと <xref:ReportService2010.ReportingService2010.GetItemDefinition%2A> から返されたレポート定義を渡します。  
  
 get メソッドと create メソッドを組み合わせて使用することで、設定、フォルダー、共有データ ソース、およびリソースの移行と同様の手順を実行できます。 使用可能なメソッドの詳細については、「[テクニカル リファレンス (SSRS)](../../reporting-services/technical-reference-ssrs.md)」を参照してください。  
  
> [!NOTE]  
>  スクリプトは、資格情報を明示的に設定しない限り、スクリプトを実行しているユーザーの [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 資格情報を使用して実行されます。  
  
 スクリプト ファイルのフォーマットおよび実行方法の詳細については、「 [rs.exe ユーティリティと Web サービスを使用したスクリプト](../../reporting-services/tools/script-with-the-rs-exe-utility-and-the-web-service.md)」を参照してください。  
  
## <a name="using-scripts-to-set-server-properties"></a>スクリプトを使用したサーバー プロパティの設定  
 レポート サーバーのシステム プロパティを設定するスクリプトを作成できます。 次の [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] .NET スクリプトは、プロパティを設定する 1 つの方法を示しています。 この例では RSClientPrint ActiveX コントロールを無効にしていますが、 **EnableClientPrinting** および **False** を有効なプロパティ名と値に置き換えることができます。 サーバーのプロパティの完全な一覧については、「 [レポート サーバーのシステム プロパティ](../../reporting-services/report-server-web-service/net-framework/reporting-services-properties-report-server-system-properties.md)」を参照してください。  
  
 スクリプトを使用するには、.rss 拡張子を持つファイルにスクリプトを保存し、rs.exe コマンド プロンプト ユーティリティを使用してレポート サーバー上でファイルを実行します。 スクリプトはコンパイルされないので [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]のインストールは不要です。 この例では、レポート サーバーをホストするローカル コンピューターに対する権限を持っていることを前提としています。 権限があるアカウントでログオンしていない場合は、追加のコマンド ライン引数を使用してアカウント情報を指定する必要があります。 詳細については、「[RS.exe ユーティリティ (SSRS)](../../reporting-services/tools/rs-exe-utility-ssrs.md)」を参照してください。  
  
> [!TIP]  
>  詳細な例については、「 [レポート サーバー間でコンテンツをコピーするサンプル Reporting Services rs.exe スクリプト](../../reporting-services/tools/sample-reporting-services-rs-exe-script-to-copy-content-between-report-servers.md)」を参照してください。  
  
```  
Public Sub Main()  
        Dim props(0) As [Property]  
        Dim setProp As New [Property]  
        setProp.Name = "EnableClientPrinting"  
        setProp.Value = "False"   
        props(0) = setProp  
        Try  
            rs.SetSystemProperties(props)  
        Catch ex As System.Web.Services.Protocols.SoapException  
            Console.Write(ex.Detail.InnerXml)  
        Catch e as Exception  
            Console.Write(e.Message)  
        End Try  
End Sub  
```

## <a name="next-steps"></a>次の手順

[GenerateDatabaseCreationScript メソッド &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-generatedatabasecreationscript.md)   
[GenerateDatabaseRightsScript メソッド &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-generatedatabaserightsscript.md)   
[GenerateDatabaseUpgradeScript メソッド &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-generatedatabaseupgradescript.md)   
[コマンド プロンプトからの SQL Server のインストール](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)   
[Reporting Services ネイティブ モードのレポート サーバーのインストール](~/reporting-services/install-windows/install-reporting-services-native-mode-report-server.md)   
[Reporting Services レポート サーバー (ネイティブ モード)](../../reporting-services/report-server/reporting-services-report-server-native-mode.md)   
[レポート サーバーのコマンド プロンプト ユーティリティ &#40;SSRS&#41;](../../reporting-services/tools/report-server-command-prompt-utilities-ssrs.md)   
[Reporting Services と Power View のブラウザー サポート](../../reporting-services/browser-support-for-reporting-services-and-power-view.md)   
[Reporting Services ツール](../../reporting-services/tools/reporting-services-tools.md)  

その他の質問 [Reporting Services のフォーラムに質問してみてください](https://go.microsoft.com/fwlink/?LinkId=620231)
