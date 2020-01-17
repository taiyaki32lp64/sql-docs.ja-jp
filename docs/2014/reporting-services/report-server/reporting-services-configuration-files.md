---
title: Reporting Services 構成ファイル | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- deploying [Reporting Services], configuration files
- configuration options [Reporting Services]
- modifying configuration files
- configuration files [Reporting Services]
ms.assetid: 21e5c32f-ad67-4917-b55a-8e21bd64f5a6
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f527b192af330f300f37102e00b010f44c82eaab
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66103347"
---
# <a name="reporting-services-configuration-files"></a>Reporting Services 構成ファイル
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] では、レジストリと構成ファイルにコンポーネント情報が格納されます。この構成ファイルは、セットアップ時にファイル システムへコピーされます。 構成ファイルには、内部専用値とユーザー定義値を組み合わせたものが含まれています。 ユーザー定義値は、セットアップ、構成ツール、コマンド ライン ユーティリティを通じて指定するか、構成ファイルを手動で編集して指定します。  
  
 構成ファイルの変更が必要になるのは、詳細設定を追加したり構成したりする場合だけです。 構成設定は、XML 要素または XML 属性のいずれかとして指定されます。 XML ファイルおよび構成ファイルを理解している場合は、テキスト エディターまたはコード エディターを使用して、ユーザーが定義可能な設定を変更できます。 構成ファイルをどのように変更するか、または、レポート サーバーが最新の構成設定をどのように読み取るかの詳細については、「[Reporting Services の構成ファイル (rsreportserver.config) の変更](modify-a-reporting-services-configuration-file-rsreportserver-config.md)」を参照してください。  
  
> [!NOTE]  
>  以前のリリースでは、RSWebApplication.config という名前の独自の構成ファイルが使用されていました。今後、このファイルは使用されません。 以前の環境からアップグレードした場合、このファイルは削除されませんが、レポート サーバーは、このファイルから一切設定を読み取りません。 このファイルがコンピューターに存在する場合は、削除してください。 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降のバージョンでは、レポート マネージャーのすべての構成設定は RSReportServer.config ファイルに格納され、このファイルから読み取られます。 これの設定が削除または移動された一覧を確認するには、次を参照してください。 [SQL Server 2014 における SQL Server Reporting Services における重大な変更](../breaking-changes-in-sql-server-reporting-services-in-sql-server-2016.md)します。  
  
 このトピックの内容  
  
-   [構成ファイルの概要 (ネイティブ モード)](#bkmk_config_file_Summary_native_mode)  
  
-   [構成ファイルの概要 (SharePoint モード)](#bkmk_config_file_Summary_sharepoint_mode)  
  
##  <a name="bkmk_config_file_Summary_native_mode"></a> 構成ファイルの概要 (ネイティブ モード)  
 次の表は、構成設定の格納先とその説明を一覧にしたものです。 ほとんどの構成設定は [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]に含まれている構成ファイルに格納されます。 既定では、インストール ディレクトリは次の場所にあります。  
  
```  
C:\Program Files\Microsoft SQL Server\MSRS12.MSSQLSERVER  
```  
  
|格納先|説明|場所|  
|----------------|-----------------|--------------|  
|RSReportServer.config|レポート サーバー サービスの機能領域の構成設定を格納します。レポート マネージャー、レポート サーバー Web サービス、およびバック グラウンド処理します。 各設定の詳細については、「 [RSReportServer Configuration File](rsreportserver-config-configuration-file.md)」を参照してください。|\<インストール ディレクトリ> \Reporting Services \ReportServer|  
|RSSrvPolicy.config|サーバー拡張機能のコード アクセス セキュリティ ポリシーが格納されます。 このファイルの詳細については、「 [Using Reporting Services Security Policy Files](../extensions/secure-development/using-reporting-services-security-policy-files.md)」を参照してください。|\<インストール ディレクトリ> \Reporting Services \ReportServer|  
|RSMgrPolicy.config|レポート マネージャーのコード アクセス セキュリティ ポリシーが格納されます。 このファイルの詳細については、「 [Using Reporting Services Security Policy Files](../extensions/secure-development/using-reporting-services-security-policy-files.md)」を参照してください。|\<インストール ディレクトリ> \Reporting Services \ReportManager|  
|レポート サーバー Web サービスの Web.config|ASP.NET に必要な設定のみが含まれています。|\<インストール ディレクトリ> \Reporting Services \ReportServer|  
|レポート マネージャーの Web.config|ASP.NET に必要な設定のみが含まれています。|\<インストール ディレクトリ> \Reporting Services \ReportManager|  
|ReportingServicesService.exe.config|レポート サーバー サービスのトレース レベルおよびログ オプションを指定する構成設定が格納されます。 このファイルに含まれる要素の詳細については、「 [ReportingServicesService Configuration File](reportingservicesservice-configuration-file.md)」を参照してください。|\<インストール ディレクトリ> \Reporting Services \ReportServer \Bin|  
|レジストリ設定|構成状態のほか、Reporting Services をアンインストールするための設定が格納されます。 インストールまたは構成上の問題をトラブルシューティングする際は、これらの設定を参照することで、レポート サーバーがどのように構成されているかの情報を得ることができます。<br /><br /> これらの設定を直接変更することは避けてください。環境に不具合が生じる可能性があります。|HKEY_LOCAL_MACHINE \SOFTWARE \Microsoft \Microsoft SQL Server \\<InstanceID\> \Setup<br /><br /> **- および -**<br /><br /> HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\Services\ReportServer|  
|RSReportDesigner.config|レポート デザイナーの構成設定が格納されます。 詳細については、「 [RSReportDesigner Configuration File](rsreportdesigner-configuration-file.md)」をご覧ください。|\<ドライブ>:\Program Files \Microsoft Visual Studio 10 \Common7 \IDE \PrivateAssemblies|  
|RSPreviewPolicy.config|レポートのプレビュー時に使用されるサーバー拡張機能のコード アクセス セキュリティ ポリシーが格納されます。 このファイルの詳細については、「 [Using Reporting Services Security Policy Files](../extensions/secure-development/using-reporting-services-security-policy-files.md)」を参照してください。|C:\Program Files\Microsoft Visual Studio 10.0\Common7\IDE\PrivateAssembliesr|  
  
##  <a name="bkmk_config_file_Summary_sharepoint_mode"></a> 構成ファイルの概要 (SharePoint モード)  
 次の表は、SharePoint モードのレポート サーバーに使用する構成ファイルの説明を一覧にしたものです。 ほとんどの構成設定は、SharePoint サービス アプリケーション データベースに格納されます。 詳細については、「 [Reporting Services の SharePoint サービスとサービス アプリケーション](../reporting-services-sharepoint-service-and-service-applications.md)｣を参照してください  
  
 既定では、SharePoint モードのインストール ディレクトリは次の場所にあります。  
  
```  
C:\Program Files\Common Files\Microsoft Shared\Web Server Extensions\15\WebServices\Reporting  
```  
  
|格納先|説明|場所|  
|----------------|-----------------|--------------|  
|RSReportServer.config|レポート サーバー サービスの機能領域の構成設定を格納します。レポート マネージャー、レポート サーバー Web サービス、およびバック グラウンド処理します。 各設定の詳細については、「 [RSReportServer Configuration File](rsreportserver-config-configuration-file.md)」を参照してください。|\<インストール ディレクトリ> \Reporting Services \ReportServer|  
|RSSrvPolicy.config|サーバー拡張機能のコード アクセス セキュリティ ポリシーが格納されます。 このファイルの詳細については、「 [Using Reporting Services Security Policy Files](../extensions/secure-development/using-reporting-services-security-policy-files.md)」を参照してください。|\<インストール ディレクトリ> \Reporting Services \ReportServer|  
|レポート サーバー Web サービスの Web.config|ASP.NET に必要な設定のみが含まれています。|\<インストール ディレクトリ> \Reporting Services \ReportServer|  
|レジストリ設定|構成状態のほか、Reporting Services をアンインストールするための設定が格納されます。 各 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サービス アプリケーションに関する情報も格納されます。<br /><br /> これらの設定を直接変更することは避けてください。環境に不具合が生じる可能性があります。|HKEY_LOCAL_MACHINE \SOFTWARE \Microsoft \Microsoft SQL Server \\<InstanceID\> \Setup<br /><br /> インスタンス ID の例:MSSQL12.MSSQLSERVER<br /><br /> **- および -**<br /><br /> HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\Reporting Services\Service Applications|  
|RSReportDesigner.config|レポート デザイナーの構成設定が格納されます。 詳細については、「 [RSReportDesigner Configuration File](rsreportdesigner-configuration-file.md)」をご覧ください。|\<ドライブ>:\Program Files \Microsoft Visual Studio 10 \Common7 \IDE \PrivateAssemblies|  
  
## <a name="see-also"></a>参照  
 [Reporting Services レポート サーバー (ネイティブ モード)](reporting-services-report-server-native-mode.md)   
 [Reporting Services の拡張機能](../extensions/reporting-services-extensions.md)   
 [rsconfig ユーティリティ &#40;SSRS&#41;](../tools/rsconfig-utility-ssrs.md)   
 [レポート サーバー サービスの開始と停止](start-and-stop-the-report-server-service.md)  
  
  
