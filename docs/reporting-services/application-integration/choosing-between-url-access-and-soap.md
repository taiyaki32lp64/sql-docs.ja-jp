---
title: Reporting Services での URL アクセスまたは SOAP の選択 | Microsoft Docs
ms.date: 10/19/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: application-integration
ms.topic: reference
author: maggiesMSFT
ms.author: maggies
monikerRange: = sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 8a9c28c2e0eeae14dbc25db3c78c3962ddebd89e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62704071"
---
# <a name="choosing-between-url-access-and-soap-in-reporting-services"></a>Reporting Services での URL アクセスまたは SOAP の選択

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-not-2017](../../includes/ssrs-appliesto-not-2017.md)] [!INCLUDE [ssrs-appliesto-not-pbirs](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] をカスタム アプリケーションへ統合するのは、必ずしも容易な作業ではありません。 ただし、その原因はプログラミング モデルや API が複雑なためではなく、統合方法が多数存在することです。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] はもともと開発者向けプラットフォームとして設計されているので、プログラミングを柔軟に行えるようになっています。 柔軟性を得るには、[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のレポート ナビゲーション機能と管理機能を既存ビジネス アプリケーションに統合することに関して重要な意思決定を行う必要があります。

> [!NOTE]
> SQL Server 2017 Reporting Services 以降では、ソリューションの開発に REST API アクセスを使用できます。 SOAP API アクセスは非推奨とされます。 詳細については、「[Develop with the REST APIs for Reporting Services](../developer/rest-api.md)」 (Reporting Services の REST API による開発) を参照してください。
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] をカスタム アプリケーションに統合するには、URL アクセスと Reporting Services SOAP API という 2 つの方法があります。 どちらの方法を使用するかは、いくつかの要因によって異なります。 状況によっては、[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] をカスタム ビジネス アプリケーションに統合する場合に URL アクセスと SOAP の両方が必要です。 決定に際して、次の事項を考慮する必要があります。  
  
-   自分自身、またはエンド ユーザーにとって、どのようなエンタープライズ レポート機能が必要か。 レポートの起動や操作はできるだけ簡単な方がよいのか、あるいは、カスタム ビジネス ソリューションの高度なレポート サーバー管理機能を使用する必要があるのか。  
  
-   一般的なユーザーの操作環境はどのようなものか。 ビジネス アプリケーションとして、Web アプリケーションを使用するのか、Windows アプリケーションを使用するのか。 エンド ユーザーは、Win32 環境から Web 環境へ簡単に切り替えることができるか。 レポートを実行および管理するうえで、どのような機能が必要か。  
  
 これらの事項を考慮したうえで、[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] を IT インフラストラクチャに統合する方法を決定してください。 通常、個別のレポートを表示およびナビゲートする場合は URL アクセスが適しています。 URL アクセスでは、Web サービスのオーバーヘッドなしにレポートを自由にすばやくナビゲートできます。 また、レポートのナビゲーションにレポートのツール バーを含む完全な HTML ビューアーを使用するプログラム技法は、現在のところ URL アクセスのみです。 URL アクセスでは、パフォーマンスも SOAP より向上します。サーバーからやり取りされる SOAP 要求のマーシャリングをバイパスするためです。 組み込まれたツールを使用してレポートを表示およびナビゲーションするために、すばやくかつ簡単なアクセスが必要な統合シナリオには、URL アクセスが適しています。  
  
> [!NOTE]  
> レポート サーバー URL アクセスは、HTML ビューアーとレポート ツール バーの拡張された機能をサポートします。 SOAP API は、この種の表示レポートをサポートしません。 SOAP API を使用してレポートを表示する場合は、独自のレポート ツール バーを設計および開発する必要があります。
  
 レポート ツール バーの詳細については、「[HTML Viewer and the Report Toolbar](../../reporting-services/html-viewer-and-the-report-toolbar.md)」(HTML ビューアーとレポート ツール バー) を参照してください。  
  
 URL アクセスの詳細については、「[URL Access](../../reporting-services/url-access-ssrs.md)」(URL アクセス) を参照してください。  
  
 URL アクセスはレポートの表示に便利ですが、エンタープライズ レポート機能に不可欠なレポートと名前空間の管理機能はありません。 このような場合は、Reporting Services SOAP API の幅広く豊富な機能をお勧めします。 SOAP API を使用すると、レポートの管理と配置、スケジュールの作成、サーバーのプロパティの構成、レポート サーバー名前空間の管理、サブスクリプションの作成などが可能です。 SOAP API は、[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の管理機能の完全なセットを提供します。 SOAP API では、API の <xref:ReportExecution2005.ReportExecutionService.Render%2A> メソッドを通してレポートを表示およびナビゲートすることもできます。 ただし、SOAP API を通してレポートを表示する場合は、レポート ツール バーの組み込み表示機能を使用できず、URL アクセスのようなレポート対話機能も自動的に処理されません。  
  
 Reporting Services SOAP API の詳細については、「[Report Server Web Service](../../reporting-services/report-server-web-service/report-server-web-service.md)」(Report Server Web サービス) を参照してください。  
  
 ほとんどの場合、レポート機能のニーズを満たすために URL アクセスと SOAP 呼び出しの両方が必要です。 SOAP を使用するのは、レポート サーバー データベースに最初に接続するときと、ユーザー インターフェイスに使用可能なレポートの一覧を表示するときです。URL アクセスを使用するのは、実際に個別のレポートにアクセスし、ナビゲートするときです。  
  
 URL アクセスと Web サービスを組み合わせて統合レポート機能を実現する例については、「[SQL Server Reporting Services Product Samples](https://go.microsoft.com/fwlink/?LinkId=177889)」(SQL Server Reporting Services 製品サンプル) を参照してください。

その他の質問 [Reporting Services のフォーラムに質問してみてください](https://go.microsoft.com/fwlink/?LinkId=620231)
