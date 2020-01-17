---
title: ファームへのレポート サーバーの追加 (SSRS スケールアウト) | Microsoft Docs
ms.date: 05/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint
ms.topic: conceptual
ms.assetid: c1a6b683-15cf-44ae-ac60-ceee63a60aaf
author: maggiesMSFT
ms.author: maggies
monikerRange: '>=sql-server-2016 <=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 17cffe2f1eaf94174301212c6bb926528c56c7d3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63225698"
---
# <a name="add-an-additional-report-server-to-a-farm-ssrs-scale-out"></a>ファームへのレポート サーバーの追加 (SSRS スケールアウト)

  2 台目以降の SharePoint モードのレポート サーバーを SharePoint ファームに追加すると、レポート サーバーのパフォーマンスと応答時間を向上させることができます。 ユーザー、レポート、またはその他のアプリケーションをレポート サーバーに追加したときにパフォーマンスが低下する場合は、レポート サーバーを追加することでパフォーマンスを向上できます。 ハードウェアに問題がある場合、または環境内の個々のサーバーに対して全般的なメンテナンスを行う場合も、2 台目のレポート サーバーを追加してレポート サーバーの可用性を向上させることをお勧めします。 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降のリリースでの SharePoint モードの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 環境をスケールアウトする手順では、標準の SharePoint ファーム配置に従い、SharePoint の負荷分散機能を活用します。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の一部のエディションでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のスケールアウトがサポートされません。 詳しくは、[SQL Server の各エディションでサポートされている機能](~/sql-server/editions-and-components-of-sql-server-2017.md#SSRS)に関するページの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のセクションをご覧ください。  
  
> [!TIP]  
>  [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降では、サーバーの追加およびレポート サーバーのスケールアウトに [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成マネージャーを使用しません。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サービスを使用する SharePoint サーバーがファームに追加されると、SharePoint 製品では Reporting Services のスケールアウトを管理します。  
  
 ネイティブ モードのレポート サーバーをスケールアウトする方法の詳細については、「[ネイティブ モード レポート サーバーのスケールアウト配置の構成 &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/configure-a-native-mode-report-server-scale-out-deployment.md)」を参照してください。  
  
##  <a name="bkmk_loadbalancing"></a> 負荷分散  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サービス アプリケーションの負荷分散は、カスタムまたはサードパーティの負荷分散ソリューションが環境に含まれていない限り、SharePoint によって自動的に管理されます。 SharePoint の既定の負荷分散動作では、各 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] アプリケーション サービスは、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サービスを開始したすべてのアプリケーション サーバー間で分散されます。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サービスがインストールされていて開始されていることを確認するには、SharePoint サーバーの全体管理で **[サーバーのサービスの管理]** をクリックします。  
  
##  <a name="bkmk_prerequisites"></a> 前提条件  
  
-   SQL Server セットアップを実行するには、ローカル管理者である必要があります。  
  
-   コンピューターがドメインに参加する必要があります。  
  
-   SharePoint の構成データベースとコンテンツ データベースをホストしている既存のデータベース サーバーの名前を把握しておく必要があります。  
  
-   データベース サーバーは、リモート データベース接続を許可するように構成されている必要があります。  構成されていない場合は、新しいサーバーが SharePoint 構成データベースに接続できないため、新しいサーバーをファームに参加させることができません。  
  
-   新しいサーバーのバージョンは、現在のファーム サーバーが実行されているインストール済みの SharePoint のバージョンと同じである必要があります。 たとえば、SharePoint 2013 Service Pack 1 (SP1) が既にファームにインストールされている場合は、新しいサーバーをファームに参加させる前に、新しいサーバーにも SP1 をインストールする必要があります。  
  
##  <a name="bkmk_steps"></a> 手順  
 このトピックの手順では、SharePoint ファームの管理者がサーバーをインストールして構成すると想定しています。 この図は標準的な 3 層環境を示しています。次に、図の番号付き項目の説明を示します。  
  
-   (1) 複数の Web フロントエンド (WFE) サーバー。 WFE サーバーには、SharePoint 2016 用の [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] アドインが必要です。  
  
-   (2) [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] と Web サイトを実行している単一のアプリケーション サーバー。たとえば、サーバーの全体管理などです。 次の手順では、この層に 2 つ目のアプリケーション サーバーを追加します。  
  
-   (3) 2 つの SQL Server データベース サーバー。  
  
-   (4) ソフトウェアまたはハードウェアのネットワーク負荷分散ソリューション (NLB) を表します。  
  
 ![Reporting Services アプリケーション サーバーを追加する](../../reporting-services/install-windows/media/rs-sharepointscale.gif "Reporting Services アプリケーション サーバーを追加する")  
  
 次の手順では、管理者がサーバーをインストールして構成すると想定しています。 サーバーは、新しいアプリケーション サーバーとしてファームにセットアップされ、Web フロントエンド (WFE) としては使用されません。  
  
|手順|説明とリンク|  
|----------|--------------------------|  
|SharePoint サーバーをファームに追加します。|別の Reporting Services アプリケーションをデプロイするには、SharePoint をインストールする必要があります。<br/><br/>SharePoint 2013 の場合は、 [SharePoint Server 2013 での SharePoint サーバーのファームへの追加](https://technet.microsoft.com/library/cc261752(v=office.15).aspx)に関する記事を参照してください。<br/><br/>SharePoint 2016 の場合は、 [SharePoint Server 2016 での SharePoint サーバーのファームへの追加](https://technet.microsoft.com/library/cc261752(v=office.16).aspx)に関する記事を参照してください。|  
|Reporting Services SharePoint モードをインストールして構成します。|SQL Server のインストールを実行します。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint モードのインストールの詳細については、「[SharePoint モードでの最初のレポート サーバーのインストール](install-the-first-report-server-in-sharepoint-mode.md)」を参照してください。<br /><br /> サーバーをアプリケーション サーバーとしてのみ使用し、WFE として使用しない場合は、 **[SharePoint 製品用 Reporting Services アドイン]** を選択する必要はありません。<br /><br /> 1) **[セットアップ ロール]** ページで、 **[SQL Server 機能のインストール]** を選択します。<br /><br /> 2) **[機能の選択]** ページで、 **[Reporting Services - SharePoint]** を選択します。<br /><br /> 3) **[Reporting Services 構成]**  ページで、 **[Reporting Services SharePoint モード]** に **[インストールのみ]** オプションが選択されていることを確認します。|  
|Reporting Services が動作することを確認します。|1) SharePoint サーバーの全体管理で、 **[システム設定]** の **[このファームのサーバーの管理]** をクリックします。<br /><br /> 2) **SQL Server Reporting Services サービス**を確認します。<br /><br />詳細については、「 [Verify a Reporting Services Installation](../../reporting-services/install-windows/verify-a-reporting-services-installation.md)」をご覧ください。|  
  
##  <a name="bkmk_additional"></a> その他の構成  
 スケールアウト配置では、個々の [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サーバーを最適化して、バックグラウンド処理のみを実行できます。そのため、リソースの確保を求めて対話型のレポート実行との競合が発生することはありません。 バックグラウンド処理には、スケジュール、サブスクリプション、およびデータ警告が含まれます。  
  
 個々のレポート サーバーの動作を変更するには、**RSreportServer.config** 構成ファイルで **\<IsWebServiceEnable>** を false に設定します。  
  
 既定では、\<IsWebServiceEnable> を TRUE に設定してレポート サーバーが構成されます。 TRUE の設定を使用してすべてのサーバーが構成されている場合は、対話型処理とバックグラウンド処理がファーム内のすべてのノード間で負荷分散されます。  
  
 \<IsWebServiceEnable> を False に設定してすべてのレポート サーバーを構成した場合は、[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の機能を使用しようとすると、次のようなエラー メッセージが表示されます。  
  
      The Reporting Services Web Service is not enabled. Configure at least one instance of the Reporting Services SharePoint Service to have <IsWebServiceEnable> set to true. 
 
 詳細については、「[Reporting Services の構成ファイルの変更 &#40;RSreportserver.config&#41;](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)」を参照してください。  

## <a name="next-steps"></a>次の手順

[SharePoint Server 2016 での SharePoint サーバーのファームへの追加](https://technet.microsoft.com/library/cc261752(v=office.16).aspx)  
[SharePoint Server 2013 での SharePoint サーバーのファームへの追加](https://technet.microsoft.com/library/cc261752(v=office.15).aspx)

その他の質問 [Reporting Services のフォーラムに質問してみてください](https://go.microsoft.com/fwlink/?LinkId=620231)
