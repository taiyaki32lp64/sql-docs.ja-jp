---
title: レポート サーバーを構成および管理する (SSRS ネイティブ モード) | Microsoft Docs
ms.date: 05/15/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- Reporting Services, components
- deploying [Reporting Services], component options
- report servers [Reporting Services], component options
- configuration options [Reporting Services]
- administering Reporting Services
- components [Reporting Services], configuring
- configuring servers [Reporting Services]
ms.assetid: cfec012b-56f1-4346-9814-247acf22351c
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: f605121be80ecef94f5a4412d23869cfd17c6ca6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66500308"
---
# <a name="configure-and-administer-a-report-server-ssrs-native-mode"></a>レポート サーバーを構成および管理する (SSRS ネイティブ モード)
  この記事では、[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] を構成するための方法について説明します。 また、特定のコンポーネント、機能、サーバー機能の構成方法について説明しているトピックへのリストも記載されています。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]は次の方法で構成できます。  
  
-   Reporting Services 構成マネージャーを使用します。 このセクションの多くのトピックでは、このツールを使用して特定の機能を構成する方法について説明しています。  
  
-   [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] を使用して、サーバーのプロパティのカスタマイズ、個人用レポートの有効化、トレース ログの有効化、および、サイト全体に対する既定値の設定を行います。 サイト設定の詳細については、Management Studio の「 [Reporting Services レポート サーバー &#40;ネイティブ モード&#41;](../../reporting-services/report-server/reporting-services-report-server-native-mode.md) 」を参照してください。 サーバーのプロパティをプログラムから設定するスクリプトを作成して実行できます。 詳細については、「 [配置タスクおよび管理タスクのスクリプト作成](../../reporting-services/tools/script-deployment-and-administrative-tasks.md) 」および「 [レポート サーバーのシステム プロパティ](../../reporting-services/report-server-web-service/net-framework/reporting-services-properties-report-server-system-properties.md)」を参照してください。  
  
-   Web ポータルを使用して、レポート サーバーにアクセスするための権限を与えます。 権限は、各ユーザーまたはグループ アカウントに対して定義したロールの割り当てを通じて付与されます。 詳細については、「[ロールと権限 (Reporting Services)](../../reporting-services/security/roles-and-permissions-reporting-services.md)」を参照してください。  
  
-   必要に応じて、構成ファイルを修正し、アプリケーションの設定を変更します。 各ファイルの詳細およびそれらの修正のガイドラインについては、「 [Reporting Services 構成ファイル](../../reporting-services/report-server/reporting-services-configuration-files.md)」を参照してください。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [レポート サーバー URL の構成 &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)  
 レポート サーバーおよび Web ポータルへのアクセスに使用する URL の定義方法について説明します。  
  
 [レポート サーバー サービス アカウントの構成 &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)  
 サービスのアカウントとパスワードを変更する方法の推奨事項と手順について説明します。  
  
 [レポート サーバー データベースの作成 &#40;SSRS構成マネージャー&#41;](../../reporting-services/install-windows/ssrs-report-server-create-a-report-server-database.md)  
 サーバーのメタデータやオブジェクトの格納に必要なレポート サーバー データベースを作成する方法について説明します。  
  
 [レポート サーバー データベース接続の構成 &#40;SSRS構成マネージャー&#41;](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md)  
 レポート サーバーからレポート サーバー データベースへの接続に使用する接続文字列を変更する方法について説明します。  
  
 [Reporting Services の電子メール配信](../install-windows/e-mail-settings-reporting-services-native-mode-configuration-manager.md)  
 電子メールによるレポートの配信をサポートするようにレポート サーバーを構成する方法について説明します。  
  
 [自動実行アカウントの構成 &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)  
 自動実行モードでレポートを処理するようにユーザー アカウントを構成する方法について説明します。  
  
## <a name="see-also"></a>参照  
 [Reporting Services 構成ファイル](../../reporting-services/report-server/reporting-services-configuration-files.md)   
 [Reporting Services 構成マネージャー &#40;ネイティブ モード&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)   
 [Reporting Services のセキュリティと保護](../../reporting-services/security/reporting-services-security-and-protection.md)   
 [Reporting Services レポート サーバー &#40;ネイティブ モード&#41;](../../reporting-services/report-server/reporting-services-report-server-native-mode.md)  
  
  
