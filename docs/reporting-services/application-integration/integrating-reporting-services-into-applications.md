---
title: アプリケーションへの Reporting Services の統合 | Microsoft Docs
ms.date: 05/14/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: application-integration
ms.topic: reference
author: maggiesMSFT
ms.author: maggies
monikerRange: = sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 64f4e77a943f1d71fc7655a4a1d36dffafe7afcf
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66175138"
---
# <a name="integrating-reporting-services-into-applications"></a>アプリケーションへの Reporting Services の統合

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-not-2017](../../includes/ssrs-appliesto-not-2017.md)] [!INCLUDE [ssrs-appliesto-not-pbirs](../../includes/ssrs-appliesto-not-pbirs.md)]

  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] は、拡張性のあるオープンなレポート プラットフォームであり、ソリューションを開発するための API の包括的なセットを開発者に提供するように設計されています。

> [!NOTE]
> SQL Server 2017 Reporting Services 以降では、ソリューションの開発に REST API アクセスを使用できます。 SOAP API アクセスは非推奨とされます。 詳細については、「[Develop with the REST APIs for Reporting Services](../developer/rest-api.md)」 (Reporting Services の REST API による開発) を参照してください。
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] をカスタム アプリケーションに統合するには、レポート サーバー Web サービス ([!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SOAP API ともいう)、[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] のレポート ビューアー コントロール、および URL アクセスの 3 つのオプションがあります。 アプリケーションに [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] を統合する方法は、オプションごとに異なります。
  
## <a name="report-server-web-service"></a>レポート サーバー Web サービス

 レポート サーバー Web サービスは、[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] に対して開発を行うための主要なインターフェイスです。 レポート カタログを管理するためのコードを開発する場合でも、サポートされている形式でレポートを表示するためのコードを開発する場合でも、Web サービスでは [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] をアプリケーションに統合するために必要なすべての方法が公開されています。 そのようなアプリケーションの一例が、[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] に含まれている Web ポータルです。これは Web サービスを使用してレポート サーバー データベースを管理します。  
  
## <a name="report-viewer-controls-for-visual-studio"></a>Visual Studio のレポート ビューアー コントロール

 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] で使用可能なレポート ビューアー コントロールは、レポート表示機能をアプリケーションに統合するために使用されます。 コントロールには、Windows フォームベースのアプリケーション用と Web フォームのアプリケーション用の 2 つがあります。 どちらのコントロールにも、レポート サーバーに配置されたレポートを表示する機能と、レポート サーバーがインストールされていない環境にあるレポートを表示する機能があります。  
  
## <a name="url-access"></a>URL アクセス  
 URL アクセスは、レポート ビューアー コントロールがオプションでない場合にレポート表示機能をアプリケーションに統合するためのもう 1 つのオプションです。 さらに、電子メールを介してユーザーにレポートへのリンクを送信するためにも使用できます。  
  
## <a name="in-this-section"></a>このセクションの内容

 [SOAP を使用した Reporting Services の統合](../../reporting-services/application-integration/integrating-reporting-services-using-soap.md)  
 レポート サーバー Web サービスを使用して、[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のレポート ナビゲーションおよび管理を既存のビジネス アプリケーションに統合する方法について説明します。  
  
 [レポート ビューアー コントロールを使用した Reporting Services の統合](../../reporting-services/application-integration/integrating-reporting-services-using-reportviewer-controls.md)  
 レポート ビューアー コントロールを使用して、レポート表示機能を既存のアプリケーションに統合する方法について説明します。  
  
 [URL アクセスを使用した Reporting Services の統合](../../reporting-services/application-integration/integrating-reporting-services-using-url-access.md)  
 URL アクセスを使用して、[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のレポート ナビゲーションを既存のビジネス アプリケーションに統合する方法について説明します。  
  
## <a name="next-steps"></a>次の手順

URL アクセスと SOAP API のどちらを使用するかを決定する際には、「[Choosing between URL access and SOAP in Reporting Services](choosing-between-url-access-and-soap.md)」 (Reporting Services での URL アクセスと SOAP の選択) を参照してください。

SQL Server 2017 Reporting Services の REST API については、「[Develop with the REST APIs for Reporting Services](../developer/rest-api.md)」 (Reporting Services の REST API による開発) を参照してください。

その他の質問 [Reporting Services のフォーラムに質問してみてください](https://go.microsoft.com/fwlink/?LinkId=620231)
