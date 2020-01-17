---
title: レポート サーバー Web サービスのエンドポイント | Microsoft Docs
ms.date: 03/03/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-web-service
ms.topic: reference
helpviewer_keywords:
- management endpoints [Reporting Services]
- Web service [Reporting Services], endpoints
- endpoints [Reporting Services]
- execution endpoints [Reporting Services]
- Report Server Web service, endpoints
ms.assetid: f3f5d85f-9359-4508-bc5a-7f78a3cf7421
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 19daac65c808691be20621d6718b4b71e33b83f9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63284630"
---
# <a name="report-server-web-service-endpoints"></a>レポート サーバー Web サービスのエンドポイント
  レポート サーバー Web サービスでは、レポートの実行およびナビゲーションに加えて、レポート サーバーの管理に利用できる複数のエンドポイントが提供されます。  
  
## <a name="the-management-endpoints"></a>管理エンドポイント  
 <xref:ReportService2005>、<xref:ReportService2006>、<xref:ReportService2010> という 3 つのエンドポイントを利用して、レポート サーバーでオブジェクトを管理できます。 <xref:ReportService2005> エンドポイントは、ネイティブ モード用に構成されたレポート サーバーのオブジェクトを管理するために使用できます。 <xref:ReportService2006> エンドポイントは、SharePoint 統合モード用に構成されたレポート サーバーのオブジェクトを管理するために使用できます。 <xref:ReportService2010> エンドポイントは、<xref:ReportService2005> と <xref:ReportService2006> の機能をまとめたものであり、ネイティブ モード用または SharePoint 統合モード用に構成されているレポート サーバー上のオブジェクトを管理できます。  
  
> [!IMPORTANT]  
>  レポート サーバーが SharePoint 統合モード用に構成されている場合、<xref:ReportService2005> API は **rsOperationNotSupportedSharePointMode** エラーを返します。 レポート サーバーがネイティブ モード用に構成されている場合、<xref:ReportService2006> API は **rsOperationNotSupportedNativeMode** エラーを返します。 同様に、<xref:ReportService2010> のモード固有 API を不適切なモードで使用した場合も、それぞれエラーが返されます。  
  
> [!NOTE]  
>  [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] では、<xref:ReportService2005> エンドポイントと <xref:ReportService2006> エンドポイントは非推奨です。 <xref:ReportService2010> エンドポイントには、両方のエンドポイントの機能と追加の管理機能が含まれています。  
  
 レポート サーバーがネイティブ モード用または SharePoint 統合モード用に構成されている場合、管理エンドポイントの WSDL には次の URL を使用してアクセスできます。  
  
```  
https://<Server Name>/ReportServer/ReportService2010.asmx?wsdl  
```  
  
 詳細については、「[SOAP API へのアクセス](../../../reporting-services/report-server-web-service/accessing-the-soap-api.md)」を参照してください。  
  
## <a name="the-execution-endpoint"></a>実行エンドポイント  
 <xref:ReportExecution2005> エンドポイントを使用すると、開発者はネイティブ モードと SharePoint 統合モードの両方でレポート サーバーによるレポートの処理と表示を容易にカスタマイズできるようになります。 このエンドポイントには、以前のバージョンのレポート サーバー Web サービスに存在していたクラスとメソッドが含まれています。 さらに、実行エンドポイントにより公開される多くの新しいクラスとメソッドがレポート サーバー Web サービスに追加されました。  
  
 管理エンドポイントの WSDL には、次の URL を使用してアクセスできます。  
  
```  
https://<Server Name>/ReportServer/ReportExecution2005.asmx?wsdl  
```  
  
 レポート サーバーが SharePoint 統合モード用に構成されている場合、WSDL には次の URL を使用してアクセスできます。  
  
```  
https://<Server Name>/<Site Name>/_vti_bin/ReportServer/ReportExecution2005.asmx?wsdl  
```  
  
 詳細については、「[SOAP API へのアクセス](../../../reporting-services/report-server-web-service/accessing-the-soap-api.md)」を参照してください。  
  
## <a name="sharepoint-proxy-endpoints"></a>SharePoint プロキシ エンドポイント  
 レポート サーバーが SharePoint 統合モード用に構成されていて、[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] アドインがインストールされている場合、SharePoint サーバーにプロキシ エンドポイントのセットがインストールされています。 プロキシ エンドポイントは、レポート サーバーが SharePoint 統合モード用に構成されている場合に、レポート ソリューションを開発するための主要な API として利用できます。 プロキシ エンドポイントに対して開発を行う場合、[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] アドインは、信頼されたアカウント認証モードを使用して SharePoint サーバーとレポート サーバーの間で資格情報の交換を管理します。 レポート サーバー エンドポイントに対して開発を行う場合、呼び出し元のアプリケーションは、信頼されたアカウント認証モードを使用して資格情報の交換を管理する必要があります。 次の表は、[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] アドインと共にインストールされるエンドポイントの一覧です。  
  
|プロキシ エンドポイント|Description|  
|--------------------|-----------------|  
|<xref:ReportService2006>|SharePoint 統合モード用に構成されたレポート サーバーを管理するための API を提供します。<br /><br /> 注: [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] では、このエンドポイントは非推奨です。|  
|<xref:ReportService2010>|ネイティブ モード用または SharePoint 統合モード用に構成されたレポート サーバーを管理するための API を提供します。|  
|<xref:ReportExecution2005>|レポートの実行とナビゲーションのための API を提供します。|  
|<xref:ReportServiceAuthentication>|SharePoint Web アプリケーションがフォーム認証用に構成されている場合にレポート サーバーに対してユーザーを認証するための API を提供します。|  
  
 次の URL の例は、SharePoint サイトのプロキシ エンドポイントを参照しています。  
  
```  
https://<Server Name>/<Site Name>/_vti_bin/ReportServer/ReportService2010.asmx  
```  
  
```  
https://<Server Name>/<Site Name>/_vti_bin/ReportServer/ReportExecution2005.asmx  
```  
  
```  
https://<Server Name>/<Site Name>/_vti_bin/ReportServer/ReportServiceAuthentication.asmx  
```  
  
## <a name="see-also"></a>参照  
 [Web サービスと .NET Framework を使用してのアプリケーションの構築](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)  
  
  
