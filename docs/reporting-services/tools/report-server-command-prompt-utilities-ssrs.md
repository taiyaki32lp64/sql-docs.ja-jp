---
title: "レポート サーバーのコマンド プロンプト ユーティリティ (SSRS) |Microsoft ドキュメント"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- rsconfig utility
- components [Reporting Services], command line utilities
- rs utility
- command prompt utilities [Reporting Services]
- rskeymgmt utility
ms.assetid: 68f2f9f4-f894-40ff-a71c-f9756bf4b68c
caps.latest.revision: 48
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: eb04937fc5c68bf2efb82ece9914c56409b7f325
ms.contentlocale: ja-jp
ms.lasthandoff: 08/09/2017

---
# <a name="report-server-command-prompt-utilities-ssrs"></a>レポート サーバーのコマンド プロンプト ユーティリティ (SSRS)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]レポート サーバーの管理に使用できるいくつかのコマンド ライン ユーティリティが含まれています。 これらのユーティリティは、レポート サーバーをインストールする際に自動的にインストールされます。  
  
|名前|コマンド ファイル|サポートされる配置モード|Description|  
|----------|------------------|-------------------------------|-----------------|  
|RSS ユーティリティ|rs.exe (rs.exe)|ネイティブ モードと SharePoint モード。 SharePoint モードのサポートは [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] リリースで導入されました。|[rs ユーティリティ](../../reporting-services/tools/rs-exe-utility-ssrs.md) は、スクリプト操作の実行に使用できるスクリプト ホストです。 このツールを使用して実行[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]レポート サーバー データベース間でデータをコピーするスクリプトは、レポートをパブリッシュ、データベース、および複数のレポート サーバーで項目を作成します。 スクリプトを使用してサーバーを管理する方法の詳細については、「 [配置タスクおよび管理タスクのスクリプト作成](../../reporting-services/tools/script-deployment-and-administrative-tasks.md)」を参照してください。|  
|PowerShell コマンドレット||SharePoint のみ|PowerShell コマンドレットの一覧については、「 [Reporting Services SharePoint モードの PowerShell コマンドレット](../../reporting-services/report-server-sharepoint/powershell-cmdlets-for-reporting-services-sharepoint-mode.md)」を参照してください。|  
|rsconfig ユーティリティ (rsconfig utility)|rsconfig.exe (rsconfig.exe)|ネイティブのみ|[rsconfig ユーティリティ](../../reporting-services/tools/rsconfig-utility-ssrs.md) は、レポート サーバー データベースへのレポート サーバー接続を構成および管理する場合に使用します。 これを使用して、自動レポート処理に使用するユーザー アカウントを指定することもできます。 詳細については、「[Reporting Services レポート サーバー (ネイティブ モード)](../../reporting-services/report-server/reporting-services-report-server-native-mode.md)」を参照してください。 接続の構成の詳細については、「[レポート サーバー データベース接続の構成 (SSRS 構成マネージャー)](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md)」を参照してください。|  
|Rskeymgmt ユーティリティ|rskeymgmt.exe|ネイティブのみ|[rskeymgmt ユーティリティ](../../reporting-services/tools/rskeymgmt-utility-ssrs.md) は、暗号化キー管理ツールです。 このツールを使用して、対称キーのバックアップ、適用、再作成、および削除を行うことができます。 このツールを使用して、レポート サーバー インスタンスを共有レポート サーバー データベースにアタッチすることもできます。 Rskeymgmt は、データベース復旧操作で使用できます。 対称キーのバックアップ コピーを適用すると、新しいインストールで既存のデータベースを再利用できます。 キーを復元できない場合、使用しなくなった暗号化された内容を削除できます。 キーの管理と機密データの保存に関する詳細については、「[暗号化されたレポート サーバー データの格納 (SSRS 構成マネージャー)](../../reporting-services/install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md)」と「[暗号化キーの構成と管理 (SSRS 構成マネージャー)](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md)」を参照してください。|  
  
> [!NOTE]  
>  グラフィカル ユーザー インターフェイスのあるツールを使用する場合は、 **rsconfig** や **rskeymgmt**ではなく、Reporting Services 構成マネージャーを使用できます。  
  
## <a name="see-also"></a>参照  
 [Reporting Services 構成マネージャー & #40 です。ネイティブ モード &#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)   
 [Reporting Services ツール](../../reporting-services/tools/reporting-services-tools.md)   
 [Reporting Services レポート サーバー & #40 です。ネイティブ モード &#41;](../../reporting-services/report-server/reporting-services-report-server-native-mode.md)  
  
  