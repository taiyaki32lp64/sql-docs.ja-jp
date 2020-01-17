---
title: 表示拡張機能にデバイス情報設定を渡す | Microsoft Docs
ms.date: 03/16/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-web-service
ms.topic: reference
helpviewer_keywords:
- device information settings [Reporting Services]
- Render method
- Report Server Web service, device information settings
- Web service [Reporting Services], device information settings
- XML Web service [Reporting Services], device information settings
- passing device information [Reporting Services]
- rendering extensions [Reporting Services], device information settings
- rendering [Reporting Services], settings
- device information settings [Reporting Services], about device information settings
- extensions [Reporting Services], device information settings
ms.assetid: fe718939-7efe-4c7f-87cb-5f5b09caeff4
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 4171fcbc01b7dfd36003bef6c4fa5d90c74600d3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63128886"
---
# <a name="passing-device-information-settings-to-rendering-extensions"></a>表示拡張機能にデバイス情報設定を渡す
  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]では、デバイス情報設定を使用して、表示パラメーターを表示拡張機能に渡します。 レポート サーバー Web サービスの設定は **DeviceInfo** XML 要素として渡し、レポート サーバーで処理されます。 デバイス情報設定には既定値があるため、表示プロセスでは省略可能な引数と見なされます。 しかし、デバイス情報設定を使用して、表示をカスタマイズし、サーバーで提供される既定値をオーバーライドできます。  
  
 デバイス情報設定はさまざまな方法で指定できます。 プログラムでは Render メソッドを使用できます。 URL によりレポートにアクセスする場合、URL パラメーターとしてデバイス情報を指定できます。 また、 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 構成ファイルのデバイス情報設定を編集し、表示パラメーターをグローバルに指定することもできます。 表示パラメーターをグローバルで指定する方法については、「[RSReportServer.Config で表示拡張機能パラメーターをカスタマイズする](../../../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md)」を参照してください。  
  
## <a name="passing-device-information-using-the-render-method"></a>Render メソッドを使用してデバイス情報を渡す  
 表示拡張機能にデバイス情報設定を渡すには、**M:Microsoft.WSSUX.ReportingServicesWebService.RSExecutionService2005.ReportExecutionService.Render(System.String,System.String,System.String@,System.String@,System.String@,Microsoft.WSSUX.ReportingServicesWebService.RSExecutionService2005.Warning[]@,System.String[]@)** メソッドを使用します。 たとえば、HTML に表示するときに HTML 断片を作成するには、次の XML 文字列を <xref:ReportExecution2005.ReportExecutionService.Render%2A> メソッドに渡すことができます。  
  
```  
<DeviceInfo>  
   <HTMLFragment>True</HTMLFragment>  
</DeviceInfo>  
```  
  
 レポートが HTML 断片として表示される場合、レポートの内容は TABLE 要素内に含まれ、HTML または BODY 要素は使用されません。 HTML 断片を使用して、既存の HTML ドキュメントにレポートを組み込むことができます。 HTML 出力のデバイス情報設定の詳細については、「 [HTML Device Information Settings](../../../reporting-services/html-device-information-settings.md)」をご覧ください。  
  
## <a name="passing-device-information-using-url-access"></a>URL アクセスを使用してデバイス情報を渡す  
 URL アクセスを使用してデバイス情報設定を渡すこともできます。 デバイス情報設定は URL パラメーターとして渡されます。 次の URL アクセス文字列をレポート サーバーに渡すと、HTML ビューアー ツール バーなしで表示するレポートを生成できます。  
  
```  
https://<Server Name>/reportserver?/SampleReports/Sales Order Detail&rs:Command=Render&rs:Format=HTML4.0&rc:Toolbar=False  
```  
  
 詳細については、「[URL でデバイス情報設定を指定する](../../../reporting-services/specify-device-information-settings-in-a-url.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [表示拡張機能のデバイス情報設定 &#40;Reporting Services&#41;](../../../reporting-services/device-information-settings-for-rendering-extensions-reporting-services.md)   
 [RSReportServer.Config で表示拡張機能パラメーターをカスタマイズする](../../../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [Web サービスと .NET Framework を使用してのアプリケーションの構築](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)  
  
  
