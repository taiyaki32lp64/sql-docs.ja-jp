---
title: Reporting Services の移行 (SharePoint モード) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 61290949-690a-4e19-b078-57c99b6b30fa
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c1f23dad22e1d748f39b1dd390b5874806193276
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75253188"
---
# <a name="migrate-a-reporting-services-installation-sharepoint-mode"></a>Reporting Services の移行 (SharePoint モード)
  このトピックでは、SharePoint モードで配置した [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] を SharePoint 環境間で移行するために必要な手順の概要について説明します。 具体的な手順は、以降元の SharePoint のバージョンによって異なる場合があります。 SharePoint モードのアップグレードと移行のシナリオの詳細については、「 [Upgrade and Migrate Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)」を参照してください。 1 つのサーバーから別のサーバーにのみレポート アイテムをコピーする場合は、「 [Sample Reporting Services rs.exe Script to Migrate Content between Report Servers](../tools/sample-reporting-services-rs-exe-script-to-copy-content-between-report-servers.md)」を参照してください。  
  
 
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ネイティブ モードの配置の移行の詳細については、「[Reporting Services のインストールの移行 &#40;ネイティブ モード&#41;](../../reporting-services/install-windows/migrate-a-reporting-services-installation-native-mode.md)」を参照してください。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]** SharePoint 2010 および SharePoint 2013|  
  
 移行を実行する一般的な理由として、配置した SharePoint 2010 を SharePoint 2013 にアップグレードする場合があります。 SharePoint 2013 では、SharePoint 2010 からのインプレース アップグレードがサポートされていないため、 **データベース アタッチ アップグレード** またはコンテンツのみの移行の手順を完了する必要があります。  
  
 SharePoint 2013 のアップグレードの詳細については、以下を参照してください。  
  
-   [SharePoint 2013 へのアップグレードプロセスの概要](https://go.microsoft.com/fwlink/p/?LinkId=256688)。  
  
-   [Sharepoint 2010 から sharepoint 2013 にデータベースをアップグレード](https://go.microsoft.com/fwlink/p/?LinkId=256690)します。  
  
-   [SharePoint 2013 でコンテンツデータベースを移動](https://technet.microsoft.com/library/cc262792.aspx)します。  
  
 
  
##  <a name="bkmk_prior_versions"></a>SQL Server 2012 より前の Reporting Services の SharePoint モードバージョンからの移行  
 
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint モード アーキテクチャは、サービス アプリケーション データベース スキーマを含め、 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]で変更されました。 より前のバージョンから sharepoint [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)]モードに移行する場合は[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]、最初に sharepoint と[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] sharepoint モードをインストールして、新しい sharepoint 環境を作成します。 詳細については、「sharepoint [2010 および sharepoint 2013&#41;の Reporting Services Sharepoint モードの &#40;インストール](../../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md)」を参照してください。  
  
 新しい SharePoint 環境が実行されていると、コンテンツ データベースを含むデータベース レベルで、コンテンツのみの移行またはすべてのコンテンツの移行を選択できます。  
  
###  <a name="bkmk_content_only_migration"></a>コンテンツのみの移行  
 **Reporting Services コンテンツのみの移行:**[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]コンテンツを新しいファームにコピーする場合は、 **rs**などのツールを使用して、コンテンツを新しい SharePoint インストールにコピーする必要があります。 コンテンツのみの移行の詳細については、以下を参照してください。  
  
-   ** [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] RSS スクリプト:** スクリプトでは、ネイティブモードと SharePoint モードのレポートサーバー間でコンテンツとリソースを移行できます。 詳細については、「[レポートサーバー間でコンテンツを移行するサンプル Reporting Services rs .Exe スクリプト](../tools/sample-reporting-services-rs-exe-script-to-copy-content-between-report-servers.md)」および「 [Reporting Services のレポートサーバーから別のレポートサーバーにコンテンツを移行する rs .exe スクリプト](https://azuresql.codeplex.com/releases/view/115207)」を参照してください。  
  
-   **Reporting Services 移行ツール:** このツールでは、ネイティブモードサーバーから SharePoint モードサーバーにレポートアイテムをコピーできます。 詳細については、「 [Reporting Services 移行ツール](https://www.microsoft.com/download/details.aspx?id=29560)」を参照してください。  
  
###  <a name="bkmk_full_migration"></a>完全な移行  
 **完全な移行:** SharePoint コンテンツデータベースを[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]カタログデータベースと共に新しいファームに移行する場合は、このトピックで説明するバックアップと復元の一連のオプションに従うことができます。 場合によっては、バックアップ時に使用したツールとは異なるツールを復元時に使用する必要があります。 たとえば、Configuration Manager を使用[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]すると、以前のバージョンのから暗号化キー [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]をバックアップできますが、sharepoint モードのインストールに[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]暗号化キーを復元するには、sharepoint サーバーの全体管理または PowerShell を使用する必要があります。  
  
####  <a name="bkmk_databases"></a>移行が完了したときに表示されるデータベース  
 次の表に、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint を正常に移行した後に存在する [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 関連の SQL Server データベースを示します。  
  
|データベース|名前の例||  
|--------------|------------------|-|  
|カタログ データベース|ReportingService_ [サービスアプリケーション GUID] **(\*)**|ユーザーが移行。|  
|一時データベース|ReportingService_ [service application GUID] TempDB **(\*)**|ユーザーが移行。|  
|警告データベース|ReportingService_[service application GUID]_Alerting|
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サービス アプリケーションの作成時に作成。|  
  
 **(\*)** 表に示した名前の例は、新しい ssrs サービスアプリケーションを作成するときに ssrs が使用する名前付け規則に従っています。 別のサーバーから移行する場合、カタログ データベースと一時データベースの名前は元のインストールと同じになります。  
  
####  <a name="bkmk_backup_operations"></a>バックアップ操作  
 ここでは、移行に必要な情報の種類と、バックアップの実行に使用するツールやプロセスについて説明します。  
  
 ![SSRS SharePoint 移行の基本図](../../../2014/sql-server/install/media/rs-sharepoint-migration.gif "SSRS SharePoint 移行の基本図")  
  
||Objects|方法|メモ|  
|-|-------------|------------|-----------|  
|**1 で保護されたプロセスとして起動されました**|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]暗号化キー。|**Rskeymgmt**または[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager。 「 [Reporting Services の暗号化キーのバックアップと復元](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)」を参照してください。|このツールはバックアップ操作だけでなく、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サービス アプリケーションの管理ページまたは PowerShell を使用した復元操作にも使用できます。|  
|**3**|SharePoint コンテンツ データベース||データベースをバックアップし、デタッチします。<br /><br /> 「[アップグレード方法を決定する (SharePoint Server 2010)」 (https://technet.microsoft.com/library/cc263447.aspx)](https://technet.microsoft.com/library/cc263447.aspx)「」の「データベースのアタッチアップグレード」を参照してください。|  
|**番**|
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]カタログ データベースである SQL Server データベース。|SQL Server データベースのバックアップと復元<br /><br /> または<br /><br /> SQL Server データベースのデタッチとアタッチ。||  
|**4/4**|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]構成ファイル。|単純なファイル コピー。|ファイルをカスタマイズしていた場合に、単純に rsreportserver.config をコピーします。 ファイルの既定の場所の例:C:\Program Files\Common Files\Microsoft Shared\Web Server Extensions\15\WebServices\Reporting<br /><br /> RSReportServer.config<br /><br /> Rssvrpolicy.config<br /><br /> レポート サーバーの ASP.NET アプリケーション用の Web.config<br /><br /> ASP.NET 用の Machine.config|  
  
####  <a name="bkmk_restore_operations"></a>復元操作  
 ここでは、移行に必要な情報の種類と、復元の実行に使用するツールやプロセスについて説明します。 復元に使用するツールは、バックアップ時に使用するツールと異なる場合があります。  
  
 復元の手順を実行する前に、新しい SharePoint ファームと [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint モードをインストールして構成しておく必要があります。 Sharepoint モードの基本的なインストールの詳細[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]については、「sharepoint [2010 および sharepoint 2013&#41;の Sharepoint モードのインストール &#40;Reporting Services ](../../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md)」を参照してください。  
  
||Objects|方法|メモ|  
|-|-------------|------------|-----------|  
|**1 で保護されたプロセスとして起動されました**|SharePoint コンテンツ データベースを新しいファームに復元する。|SharePoint の "データベース アタッチ アップグレード" の手法。|基本的な手順:<br /><br /> 1) データベースを新しいサーバーに復元します。<br /><br /> 2) URL を指定して、コンテンツ データベースを Web アプリケーションにアタッチします。<br /><br /> 3) Get-SPWebapplication を実行して、すべての Web アプリケーションと URL を一覧表示します。<br /><br /> 「[アップグレード方法を決定する (sharepoint server 2010)https://technet.microsoft.com/library/cc263447.aspx)](https://technet.microsoft.com/library/cc263447.aspx)」の「データベース接続アップグレード」、および「[データベースをアタッチして sharepoint server 2010 にアップグレードする」 (https://technet.microsoft.com/library/cc263299.aspx)](https://technet.microsoft.com/library/cc263299.aspx)「」を参照してください。|  
|**3**|
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] カタログ データベースである SQL データベースを復元する (ReportServer)。|SQL データベースのバックアップと復元。<br /><br /> **または**<br /><br /> SQL Server データベースのデタッチとアタッチ。|データベースを最初に使用するときに、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] によってデータベース スキーマが必要に応じて更新され、データベース スキーマが [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 環境で正常に動作できるようになります。|  
|**番**|新しい [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サービス アプリケーションを作成する。|SharePoint サーバーの全体管理。|新しいサービス アプリケーションを作成するときに、コピーしたレポート サーバー データベースを使用するように構成します。<br /><br /> SharePoint サーバーの全体管理の使用方法の詳細については、「sharepoint [2013 用 Reporting Services Sharepoint モードのインストール](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2013.md)」の「手順 3: Reporting Services サービスアプリケーションを作成する」セクションを参照してください。<br /><br /> PowerShell の使用例については、「[Reporting Services の SharePoint サービスとサービス アプリケーション](../../../2014/reporting-services/reporting-services-sharepoint-service-and-service-applications.md)」の「PowerShell を使用して Reporting Services サービス アプリケーションを作成するには」をご覧ください。|  
|**4/4**|
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ファイルを復元する。|単純なファイル コピー。|このファイルの既定の場所の例: C:\Program Files\Common Files\Microsoft Shared\Web Server Extensions\15\WebServices\Reporting|  
|**5/5**|
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 暗号化キーを復元します。|
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サービス アプリケーションの "SystemSettings" ページを使用して、キー バックアップ ファイルを復元します。<br /><br /> **または**<br /><br /> PowerShell。|「 [Reporting Services SharePoint サービスアプリケーションの管理](../../../2014/reporting-services/manage-a-reporting-services-sharepoint-service-application.md)」の「キー管理」を参照してください。|  
  
#####  <a name="bkmk_additional_configuration"></a>追加の構成  
 以前の SharePoint 環境の構成方法によっては、次の手順のどちらか、またはこの両方を実行する必要がある場合があります。  
  
1.  
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サービス アプリケーションの NTLM 認証を構成する。 詳細については、「[Reporting Services サービス アプリケーションの電子メールの構成 &#40;SharePoint 2010 および SharePoint 2013&#41;](../../reporting-services/install-windows/configure-e-mail-for-a-reporting-services-service-application.md)」を参照してください。  
  
##  <a name="bkmk_migrate_from_ctp"></a>SQL Server 2012 デプロイからの移行  
 マルチサーバー ファームでは、コンテンツ データベースとカタログ データベースが別々のコンピューターに置かれていることが多い場合があります。そのような場合は、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サービスがインストールされた新しいサーバーを SharePoint ファームに追加した後で、古いサーバーを削除するだけでかまいません。 データベースをコピーする必要はありません。  
  
### <a name="backup-operations"></a>バックアップ操作  
  
1.  
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 暗号化キーをバックアップします。  
  
2.  SharePoint サーバーの全体管理で (または PowerShell を使用して)、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サービス アプリケーションをバックアップします。 これによって、SharePoint のサービス アプリケーション データベースもバックアップされます。 「  [Reporting Services SharePoint サービス アプリケーションのバックアップと復元](../../../2014/reporting-services/backup-and-restore-reporting-services-sharepoint-service-applications.md)」を参照してください。  
  
3.  自動実行アカウント (UEA) と Windows 認証を使用している場合、その資格情報を記録しておき、復元プロセスでも使用できるようにしてください。  
  
4.  詳細については、「 [SharePoint 2013 でサービス アプリケーションをバックアップする](https://technet.microsoft.com/library/ee428318.aspx)」を参照してください。  
  
### <a name="restore-operations"></a>復元操作  
  
1.  SharePoint サーバーの全体管理を使用して、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サービス アプリケーションを復元します。 PowerShell を使用することもできます。  
  
2.  
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 暗号化キーを復元します。  
  
     「 [Reporting Services SharePoint サービスアプリケーションの管理](../../../2014/reporting-services/manage-a-reporting-services-sharepoint-service-application.md)」の「キー管理」を参照してください。  
  
3.  サービス アプリケーションに、UEA と Windows 資格情報を構成します。  
  
4.  詳細については、「 [SharePoint 2013 でサービス アプリケーションを復元する](https://technet.microsoft.com/library/ee428305.aspx)」を参照してください。  
  
##  <a name="bkmk_additional_resources"></a>その他のリソース  
  
-   [SharePoint 2013 へのアップグレードの概要 (https://technet.microsoft.com/library/ee833948.aspx)をご覧](https://technet.microsoft.com/library/ee833948.aspx)ください。  
  
-   [SharePoint 2013 へのアップグレードプロセスの概要 (https://technet.microsoft.com/library/cc262483.aspx)](https://technet.microsoft.com/library/cc262483.aspx).  
  
## <a name="see-also"></a>参照  
 [Reporting Services のアップグレードと移行](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)   
 [Reporting Services インストール &#40;ネイティブモードに移行する&#41;](../../reporting-services/install-windows/migrate-a-reporting-services-installation-native-mode.md)  
  
