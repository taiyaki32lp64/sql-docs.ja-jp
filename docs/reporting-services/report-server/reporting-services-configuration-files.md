---
title: Reporting Services 構成ファイル | Microsoft Docs
ms.date: 05/30/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- deploying [Reporting Services], configuration files
- configuration options [Reporting Services]
- modifying configuration files
- configuration files [Reporting Services]
ms.assetid: 21e5c32f-ad67-4917-b55a-8e21bd64f5a6
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: b0bd7ad95fcda039c6fd5a9299f4339d35b8a619
ms.sourcegitcommit: e4b241fd92689c2aa6e1f5e625874bd0b807dd01
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/04/2019
ms.locfileid: "67564129"
---
# <a name="reporting-services-configuration-files"></a>Reporting Services 構成ファイル
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] では、レジストリと構成ファイルにコンポーネント情報が格納されます。この構成ファイルは、セットアップ時にファイル システムへコピーされます。 構成ファイルには、内部専用値とユーザー定義値を組み合わせたものが含まれています。 ユーザー定義値は、セットアップ、構成ツール、コマンド ライン ユーティリティを通じて指定するか、構成ファイルを手動で編集して指定します。  
  
 構成ファイルの変更が必要になるのは、詳細設定を追加したり構成したりする場合だけです。 構成設定は、XML 要素または XML 属性のいずれかとして指定されます。 XML ファイルおよび構成ファイルを理解している場合は、テキスト エディターまたはコード エディターを使用して、ユーザーが定義可能な設定を変更できます。 構成ファイルをどのように変更するか、または、レポート サーバーが最新の構成設定をどのように読み取るかの詳細については、「[Reporting Services の構成ファイル (rsreportserver.config) の変更](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)」を参照してください。  
  
> [!NOTE]  
> 以前のリリースでは、RSWebApplication.config という名前の独自の構成ファイルが使用されていました。今後、このファイルは使用されません。 以前の環境からアップグレードした場合、このファイルは削除されませんが、レポート サーバーは、このファイルから一切設定を読み取りません。 このファイルがコンピューターに存在する場合は、削除してください。 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降のバージョンでは、レポート マネージャーと Web ポータルの構成設定はすべて RSReportServer.config ファイルに格納され、このファイルから読み取られます。 設定が削除または移動された一覧を確認する方法については、「 [SQL Server 2016 における SQL Server Reporting Services の重大な変更](../../reporting-services/breaking-changes-in-sql-server-reporting-services-in-sql-server-2016.md)」を参照してください。  
  
 この記事の内容は次のとおりです。  
  
-   [構成ファイルの概要 (ネイティブ モード)](#bkmk_config_file_Summary_native_mode)  
  
-   [構成ファイルの概要 (SharePoint モード)](#bkmk_config_file_Summary_sharepoint_mode)  
  
##  <a name="bkmk_config_file_Summary_native_mode"></a> 構成ファイルの概要 (ネイティブ モード)  
 次の表は、構成設定の格納先とその説明を一覧にしたものです。 ほとんどの構成設定は [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]に含まれている構成ファイルに格納されます。 既定では、インストール ディレクトリは次の場所にあります。  
  
```
Install Paths  
C:\Program Files\Microsoft SQL Server\MSRSxx.MSSQLSERVER  (where xx is the MS SQL version number)
  or  
C:\Program Files\Microsoft SQL Server Reporting Services\SSRS  
  depending on the SSRS version
```  
  
|格納先|[説明]|場所|  
|----------------|-----------------|--------------|  
|RSReportServer.config|レポート サーバー サービスの機能領域 (レポート マネージャーまたは Web ポータル、レポート サーバー Web サービス、バックグラウンド処理) の構成設定が格納されます。 各設定の詳細については、「 [RsReportServer.config 構成ファイル](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)」を参照してください。|\<インストール ディレクトリ> \Reporting Services \ReportServer|  
|RSSrvPolicy.config|サーバー拡張機能のコード アクセス セキュリティ ポリシーが格納されます。 このファイルの詳細については、「 [Using Reporting Services Security Policy Files](../../reporting-services/extensions/secure-development/using-reporting-services-security-policy-files.md)」を参照してください。|\<インストール ディレクトリ> \Reporting Services \ReportServer|  
|RSMgrPolicy.config|Web ポータルのコード アクセス セキュリティ ポリシーが格納されます。 このファイルの詳細については、「 [Using Reporting Services Security Policy Files](../../reporting-services/extensions/secure-development/using-reporting-services-security-policy-files.md)」を参照してください。|\<インストール ディレクトリ> \Reporting Services \ReportManager|  
|レポート サーバー Web サービスの Web.config|ASP.NET に必要な設定のみが含まれています。|\<インストール ディレクトリ> \Reporting Services \ReportServer|  
|レポート マネージャーの Web.config|SSRS のバージョンについては該当する場合、ASP.NET の必要な設定のみが含まれています。|\<インストール ディレクトリ> \Reporting Services \ReportManager|  
|ReportingServicesService.exe.config|レポート サーバー サービスのトレース レベルおよびログ オプションを指定する構成設定が格納されます。 このファイルに含まれる要素の詳細については、「 [ReportingServicesService Configuration File](../../reporting-services/report-server/reportingservicesservice-configuration-file.md)」を参照してください。|\<インストール ディレクトリ> \Reporting Services \ReportServer \Bin|  
|レジストリ設定|構成状態のほか、Reporting Services をアンインストールするための設定が格納されます。 インストールまたは構成上の問題をトラブルシューティングする際は、これらの設定を参照することで、レポート サーバーがどのように構成されているかの情報を得ることができます。<br /><br /> これらの設定を直接変更することは避けてください。環境に不具合が生じる可能性があります。|HKEY_LOCAL_MACHINE \SOFTWARE \Microsoft \Microsoft SQL Server \\<InstanceID\> \Setup<br /><br /> **- および -**<br /><br /> HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\Services\ReportServer|  
|RSReportDesigner.config|レポート デザイナーの構成設定が格納されます。 詳細については、「 [RSReportDesigner Configuration File](../../reporting-services/report-server/rsreportdesigner-configuration-file.md)」をご覧ください。|\<ドライブ>:\Program Files \Microsoft Visual Studio 10 \Common7 \IDE \PrivateAssemblies|  
|RSPreviewPolicy.config|レポートのプレビュー時に使用されるサーバー拡張機能のコード アクセス セキュリティ ポリシーが格納されます。 このファイルの詳細については、「 [Using Reporting Services Security Policy Files](../../reporting-services/extensions/secure-development/using-reporting-services-security-policy-files.md)」を参照してください。|C:\Program Files\Microsoft Visual Studio 10.0\Common7\IDE\PrivateAssembliesr|  
  
##  <a name="bkmk_config_file_Summary_sharepoint_mode"></a> 構成ファイルの概要 (SharePoint モード)  
 次の表は、SharePoint モードのレポート サーバーに使用する構成ファイルの説明を一覧にしたものです。 ほとんどの構成設定は、SharePoint サービス アプリケーション データベースに格納されます。 詳細については、「 [Reporting Services の SharePoint サービスとサービス アプリケーション](../../reporting-services/report-server-sharepoint/reporting-services-sharepoint-service-and-service-applications.md)｣を参照してください  
  
 既定では、SharePoint モードのインストール ディレクトリは次の場所にあります。  
  
```
Install path
C:\Program Files\Common Files\Microsoft Shared\Web Server Extensions\15\WebServices\Reporting  
```  
  
|格納先|[説明]|場所|  
|----------------|-----------------|--------------|  
|RSReportServer.config|レポート サーバー サービスの機能領域 (レポート マネージャーまたは Web ポータル、レポート サーバー Web サービス、バックグラウンド処理) の構成設定が格納されます。 各設定の詳細については、「 [RsReportServer.config 構成ファイル](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)」を参照してください。|\<インストール ディレクトリ> \Reporting Services \ReportServer|  
|RSSrvPolicy.config|サーバー拡張機能のコード アクセス セキュリティ ポリシーが格納されます。 このファイルの詳細については、「 [Using Reporting Services Security Policy Files](../../reporting-services/extensions/secure-development/using-reporting-services-security-policy-files.md)」を参照してください。|\<インストール ディレクトリ> \Reporting Services \ReportServer|  
|レポート サーバー Web サービスの Web.config|SSRS のバージョンについては該当する場合、ASP.NET の必要な設定のみが含まれています。|\<インストール ディレクトリ> \Reporting Services \ReportServer|  
|レジストリ設定|構成状態のほか、Reporting Services をアンインストールするための設定が格納されます。 各 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サービス アプリケーションに関する情報も格納されます。<br /><br /> これらの設定を直接変更することは避けてください。環境に不具合が生じる可能性があります。|HKEY_LOCAL_MACHINE \SOFTWARE \Microsoft \Microsoft SQL Server \\<InstanceID\> \Setup<br /><br /> インスタンス ID の例: MSSQL13.MSSQLSERVER<br /><br /> **- および -**<br /><br /> HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\Reporting Services\Service Applications|  
|RSReportDesigner.config|レポート デザイナーの構成設定が格納されます。 詳細については、「 [RSReportDesigner Configuration File](../../reporting-services/report-server/rsreportdesigner-configuration-file.md)」をご覧ください。|\<ドライブ>:\Program Files \Microsoft Visual Studio 10 \Common7 \IDE \PrivateAssemblies|  
  
## <a name="see-also"></a>参照  
 [Reporting Services レポート サーバー (ネイティブ モード)](../../reporting-services/report-server/reporting-services-report-server-native-mode.md)   
 [Reporting Services の拡張機能](../../reporting-services/extensions/reporting-services-extensions.md)   
 [rsconfig ユーティリティ &#40;SSRS&#41;](../../reporting-services/tools/rsconfig-utility-ssrs.md)   
 [レポート サーバー サービスの開始と停止](../../reporting-services/report-server/start-and-stop-the-report-server-service.md)  
  
  
