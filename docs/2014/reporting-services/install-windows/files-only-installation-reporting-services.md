---
title: ファイルのみのインストール (Reporting Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- files-only installation [Reporting Services]
- installation options [Reporting Services]
ms.assetid: bdc74a8f-046c-4aa0-bfbd-4f1711dfb9ce
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: a854de693bce88fcba0de2f1c08e4b0fe296b512
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66108841"
---
# <a name="files-only-installation-reporting-services"></a>ファイルのみのインストール (Reporting Services)
  *ファイルのみのインストール* とは、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のインストール形態の 1 つです。このインストールでは、セットアップで、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] プログラム ファイルのフォルダー構造の作成、ディスクへのファイルのコピー、ローカル コンピューターへのレポート サーバー サービスの登録、サービス アカウントの構成、サービス アカウントへのファイル権限の付与、および [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] WMI プロバイダーの登録を行います。  
  
 ファイルのみのインストールには、次が含まれています。[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]機能。レポート サーバー サービス (バック グラウンド処理アプリケーション、およびレポート マネージャー、レポート サーバー Web サービスのホスト) をレポート ビルダーで、[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]構成ツール、および[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]コマンド ライン ユーティリティ (rsconfig.exe、rskeymgmt.exe とrs.exe)。 このオプションは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] or [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], which must be specified as separate items if you want to install them.  
  
 他のインストール モードとは異なり、ファイルのみのモードでインストールされたレポート サーバーは、セットアップの終了時点ではまだ使用できません。 [Reporting Services 構成マネージャー &#40;ネイティブ モード&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md) を使用してレポート サーバーをオンラインにするには、追加の構成が必要です。  
  
## <a name="when-to-select-files-only-installation-mode"></a>ファイルのみのインストール モードを選択する場合  
 次のような場合、ファイルのみのインストールを実行する必要があります。  
  
-   リモートのレポート サーバー データベースにレポート サーバーを接続する場合。  
  
-   レポート サーバーを名前付きインスタンスとしてインストールする場合。  
  
-   カスタムの設定や機能の使用が配置要件に含まれており、サーバー構成のタイミングと方法を完全に制御する必要がある場合。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を含む [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]フェールオーバー クラスターをインストールする場合。  
  
## <a name="how-to-perform-a-files-only-installation"></a>ファイルのみのインストールを実行する方法  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]では、ファイルのみのインストールが既定値です。  
  
 ファイルのみのインストールを、コマンド ラインまたはインストール ウィザードで指定できます。 手順については次のトピックを参照してください。  
  
-   [SQL Server 2014 インストール ウィザードからインストール&#40;セットアップ&#41;](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)します。  
  
-   [コマンド プロンプトから SQL Server 2014 インストール](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)します。  
  
#### <a name="example-command-line-script"></a>コマンド ライン スクリプトの例  
 わかりやすくするため、この例では /RSINSTALLMODE ="FilesOnlyMode" を指定しています。 実際には、ファイルのみのモードが既定値であるため、これを省略してもファイルのみのモードでインストールされます。  
  
```  
setup /q /ACTION=install /FEATURES=RS /InstanceName=MSSQLSERVER /RSSVCACCOUNT="NT AUTHORITY\NETWORK SERVICE" /RSINSTALLMODE="FilesOnlyMode"  
```  
  
#### <a name="installation-wizard"></a>インストール ウィザード  
 [機能の選択] ページで [ [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ] を選択すると、[ [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成] ページでインストール モードを指定できるようになります。 ファイルのみのインストールを指定するには、 **[構成] ページで** [レポート サーバーを構成せずにインストールする] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] をクリックします。  
  
## <a name="see-also"></a>関連項目  
 [Reporting Services のインストール状態の検証](verify-a-reporting-services-installation.md)   
 [レポート サーバー サービス アカウントの構成 &#40;SSRS 構成マネージャー&#41;](configure-the-report-server-service-account-ssrs-configuration-manager.md)   
 [レポート サーバー URL の構成 &#40;SSRS 構成マネージャー&#41;](configure-report-server-urls-ssrs-configuration-manager.md)   
 [レポート サーバー データベース接続の構成 &#40;SSRS構成マネージャー&#41;](../../sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)   
 [Reporting Services の SharePoint モード インストール&#40;SharePoint 2010 および SharePoint 2013&#41;](install-reporting-services-sharepoint-mode.md)   
 [Reporting Services ネイティブ モードのレポート サーバーのインストール](install-reporting-services-native-mode-report-server.md)   
 [Reporting Services ツール](../tools/reporting-services-tools.md)  
  
  
