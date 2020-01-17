---
title: Reporting Services のプロパティ | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-web-service
ms.topic: reference
helpviewer_keywords:
- report servers [Reporting Services], properties
- properties [Reporting Services], about properties
- reports [Reporting Services], properties
- Report Server Web service, properties
- report properties [Reporting Services]
- XML Web service [Reporting Services], properties
- Web service [Reporting Services], properties
- properties [Reporting Services]
ms.assetid: 8c855194-4c20-4ecc-a328-5137d54b560c
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 36a105d3220755dd03ff05a50dd403d4bac25d3a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62703850"
---
# <a name="reporting-services-properties"></a>Reporting Services のプロパティ
  レポート サーバーは、レポート サーバーにグローバルなシステム プロパティのセット、およびレポート サーバー データベースに格納された個別のアイテムに関連付けられているアイテム プロパティのセットを定義します。 レポート サーバーによって定義されたプロパティは削除できず、場合によっては読み取り専用です。 アプリケーションでシステム プロパティとアイテム プロパティを拡張するには、ユーザー定義プロパティをシステム プロパティとアイテム プロパティに追加します。  
  
 次の Web サービス メソッドは、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] のプロパティを取得および設定します。  
  
|方法|操作|  
|------------|------------|  
|<xref:ReportService2010.ReportingService2010.GetProperties%2A>|レポート サーバー データベースのアイテムに関する 1 つ以上のプロパティ値を返します。|  
|<xref:ReportService2010.ReportingService2010.GetSystemProperties%2A>|1 つ以上のシステム プロパティを返します。|  
|<xref:ReportService2010.ReportingService2010.SetProperties%2A>|レポート サーバー データベースのアイテムの 1 つ以上のプロパティを設定します。|  
|<xref:ReportService2010.ReportingService2010.SetSystemProperties%2A>|1 つ以上のシステム プロパティを設定します。|  
  
## <a name="in-this-section"></a>このセクションの内容  
  
|トピック|[説明]|  
|-----------|-----------------|  
|[レポート サーバー アイテムのプロパティ](../../../reporting-services/report-server-web-service/net-framework/reporting-services-properties-report-server-item-properties.md)|[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] のアイテム固有のプロパティについて説明します。|  
|[レポート サーバーのシステム プロパティ](../../../reporting-services/report-server-web-service/net-framework/reporting-services-properties-report-server-system-properties.md)|[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] のシステム固有のプロパティについて説明します。|  
  
## <a name="see-also"></a>参照  
 [Web サービスと .NET Framework を使用してのアプリケーションの構築](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [レポート サーバー Web サービス](../../../reporting-services/report-server-web-service/report-server-web-service.md)   
 [テクニカル リファレンス (SSRS)](../../../reporting-services/technical-reference-ssrs.md)  
  
  
