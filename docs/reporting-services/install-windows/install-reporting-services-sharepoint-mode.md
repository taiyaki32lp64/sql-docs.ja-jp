---
title: SharePoint モードで Reporting Services 2016 をインストールする | Microsoft Docs
ms.date: 12/20/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint
ms.topic: conceptual
helpviewer_keywords:
- default configuration [Reporting Services]
- installing Reporting Services, SharePoint integrated mode
- installation options [Reporting Services]
ms.assetid: ac6cba68-2665-4a39-8fa3-cb7d7e6723c0
author: maggiesMSFT
ms.author: maggies
monikerRange: '>=sql-server-2016 <=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: c0ffb0df6ee5e64e79cd232e07f8ab124dfee530
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62514477"
---
# <a name="install-reporting-services-2016-in-sharepoint-mode"></a>SharePoint モードで Reporting Services 2016 をインストールする

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE [ssrs-appliesto-not-2017](../../includes/ssrs-appliesto-not-2017.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE [ssrs-appliesto-not-pbirs](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

SharePoint の SQL Server Reporting Services では、レポートの作成とドキュメント ライブラリでの表示、[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サブスクリプションの電子メールを使用したレポートの配信、[!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]、データ アラート、レポート管理機能をすべて、[!INCLUDE[msCoName](../../includes/msconame-md.md)] SharePoint ベースの配置で使用できます。 SharePoint モードの機能の詳細については、「[Reporting Services レポート サーバー](../../reporting-services/report-server-sharepoint/reporting-services-report-server.md)」のサーバー モードごとの機能サポートと動作の違いに関するセクションを参照してください。

> [!NOTE]
> SharePoint と Reporting Services の統合は、SQL Server 2016 以降では使用できません。

SharePoint モードでの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] には、インストールする2 つの主な [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のコンポーネントがあります。  

|インストール|[説明]|  
|------------------|-----------------|  
|**レポート サーバー:** SharePoint モードでインストールされる [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] レポート サーバー|レポート サーバーは、データとレポートの処理と表示に加え、サブスクリプションとデータ警告処理も処理します。 SharePoint モードのレポート サーバーは、SharePoint 共有サービスとして設計およびインストールされています。<br /><br /> **方法:** レポート サーバーをインストールするには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインストール メディアを使用します。|  
|**アドイン:** SharePoint モードでインストールされる [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] アドイン ( **rssharepoint.msi**)。|アドインでは、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ユーザー インターフェイス (UI) ページと機能を SharePoint Web フロントエンド サーバーにインストールします。 UI 機能には、 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]、SharePoint サーバーの全体管理の管理ページ、SharePoint ドキュメント ライブラリ内で使用される機能ページ、および [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] データ警告ページが含まれます。<br /><br /> **方法:**  アドインは、Web ダウンロードまたは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインストール メディアからインストールできます。 詳細については、「 [SharePoint 製品用 Reporting Services アドインの検索場所](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)」を参照してください。|  
  
## <a name="in-this-section"></a>このセクションの内容

 [SharePoint、Reporting Services サーバー、Reporting Services アドインのサポートされる組み合わせ &#40;SQL Server 2016&#41;](../../reporting-services/install-windows/supported-combinations-of-sharepoint-and-reporting-services-server.md)  
  
 [SharePoint 製品用 Reporting Services アドインの検索場所](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)  
  
 [SharePoint モードでの最初のレポート サーバーのインストール](../../reporting-services/install-windows/install-the-first-report-server-in-sharepoint-mode.md)  
  
 [SharePoint 用 Reporting Services アドインのインストールまたはアンインストール](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)  
  
 [ファームへのレポート サーバーの追加 &#40;SSRS スケールアウト&#41;](../../reporting-services/install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md)  
  
 [ファームへの Reporting Services Web フロントエンドの追加](../../reporting-services/install-windows/add-an-additional-reporting-services-web-front-end-to-a-farm.md)  
  
 [Reporting Services サービス アプリケーションの電子メールの構成 &#40;SharePoint 2013 および SharePoint 2016&#41;](https://msdn.microsoft.com/38fc34a6-aae7-4dde-9ad2-f1eee0c42a9f)  
  
 [SSRS サービス アプリケーションを使用するためのサブスクリプションと警告の準備](../../reporting-services/install-windows/provision-subscriptions-and-alerts-for-ssrs-service-applications.md)  
  
 [Claims to Windows Token Service &#40;c2WTS&#41; と Reporting Services](../../reporting-services/install-windows/claims-to-windows-token-service-c2wts-and-reporting-services.md)  

## <a name="next-steps"></a>次の手順

 [データ警告のアーキテクチャとワークフロー](../../reporting-services/reporting-services-data-alerts.md#AlertingWF)   
 [警告管理者用のデータ警告マネージャー](../../reporting-services/data-alert-manager-for-alerting-administrators.md)  

その他の質問 [Reporting Services のフォーラムに質問してみてください](https://go.microsoft.com/fwlink/?LinkId=620231)
