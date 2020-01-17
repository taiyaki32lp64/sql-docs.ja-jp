---
title: SOAP API へのアクセス | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-web-service
ms.topic: reference
helpviewer_keywords:
- XML Web service [Reporting Services], WSDL
- Web service [Reporting Services], SOAP
- calling Web service
- SOAP [Reporting Services], accessing
- Report Server Web service, SOAP
- Web service [Reporting Services], WSDL
- WSDL [Reporting Services]
- XML Web service [Reporting Services], SOAP
- Report Server Web service, WSDL
- referencing WSDL
ms.assetid: 63bb870a-4dbf-46bd-8921-78f8ebe5fd75
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: c78f160e51265e4ce87a191aa3076dc4464c31d2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63026174"
---
# <a name="accessing-the-soap-api"></a>SOAP API へのアクセス
  レポート サーバー Web サービスは、SOAP (Simple Object Access Protocol) over HTTP を使用し、クライアント プログラムとレポート サーバー間の通信インターフェイスとして機能します。 Web サービスには、レポート実行用とレポート管理用の 2 つのエンドポイントがあり、[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の完全な機能にアクセスするために使用できるメソッドと複合型オブジェクトのセットで構成されます。 Web サービスを呼び出すには、Reporting Services Web サービス記述言語 (WSDL) を参照する必要があります。  
  
## <a name="referencing-the-reporting-services-wsdl"></a>Reporting Services WSDL の参照  
 Web サービスを正常に呼び出すには、サービスへのアクセス方法、サービスがサポートする操作、サービスが想定するパラメーター、およびサービスが返すものを知っておく必要があります。 WSDL は、コンピューターで読み取り、処理できる XML ドキュメントでこのような情報を提供します。  
  
 レポート サーバー Web サービスは、3 つの異なるエンドポイントで公開されます。 WSDL ファイルの名前は、エンドポイントごとに異なります。 <xref:ReportService2010> エンドポイントには、ネイティブ モードまたは SharePoint 統合モードでレポート サーバーのオブジェクトを管理するためのメソッドが含まれています。 このエンドポイントの WSDL には、`ReportService2010.asmx?wsdl.` を通してアクセスします。  
  
> [!NOTE]  
>  [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] では、<xref:ReportService2005> エンドポイントと <xref:ReportService2006> エンドポイントは非推奨です。 <xref:ReportService2010> エンドポイントには、両方のエンドポイントの機能と追加の管理機能が含まれています。  
  
-   <xref:ReportExecution2005> エンドポイントでは、開発者がレポート サーバーのレポートをプログラムによって処理および表示できます。 このエンドポイントの WSDL には、`ReportExecution2005.asmx?wsdl` を通してアクセスします。  
  
 WSDL は、SOAP と Web サービスをサポートする、[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK などの開発キットによって使用できます。  
  
 次の例は、[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 管理 WSDL ファイルへの URL の書式を示しています。  
  
```  
https://server/reportserver/ReportService2010.asmx?wsdl  
```  
  
 次の表では、URL の各要素を説明します。  
  
|URL の要素|[説明]|  
|-----------------|-----------------|  
|*server*|レポート サーバーが配置されているサーバーの名前。|  
|*reportserver*|XML Web サービスを含むフォルダーの名前。 これはセットアップ中に構成されます。|  
|*\<endpoint name>.asmx*|Web サービス エンドポイントの名前。|  
  
 WSDL フォーマットの詳細については、 http://www.w3.org/TR/wsdl の W3C (World Wide Web Consortium) WSDL 仕様を参照してください。  
  
## <a name="see-also"></a>参照  
 [Web サービスと .NET Framework を使用してのアプリケーションの構築](../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [レポート サーバー web サービス](../../reporting-services/report-server-web-service/report-server-web-service.md)  
  
  
