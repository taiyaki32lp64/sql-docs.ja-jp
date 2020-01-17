---
title: Rendering メソッドと Execution メソッド | Microsoft Docs
ms.date: 03/06/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-web-service
ms.topic: reference
helpviewer_keywords:
- rendered reports [Reporting Services]
- reports [Reporting Services], execution options
- methods [Reporting Services], execution options
- methods [Reporting Services], rendering
ms.assetid: 12626aad-f0be-4653-87d0-60eb3a3fff78
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 244541348f583ab5384a0ebfe7321509a421fe1b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63284537"
---
# <a name="rendering-and-execution-methods"></a>Rendering メソッドと Execution メソッド
  これらのメソッドを使用して、アイテムの実行とキャッシュ、およびレポートの表示を管理します。  
  
|方法|操作|  
|------------|------------|  
|<xref:ReportService2010.ReportingService2010.FlushCache%2A>|アイテムのキャッシュを無効にします。|  
|<xref:ReportService2010.ReportingService2010.GetCacheOptions%2A>|アイテムのキャッシュ構成と、キャッシュされたコピーの有効期限がいつ切れるかを表す設定を返します。|  
|<xref:ReportService2010.ReportingService2010.GetExecutionOptions%2A>|個々のアイテムの実行オプションおよび関連付けられている設定を返します。|  
|<xref:ReportService2010.ReportingService2010.ListExecutionSettings%2A>|サポートされている実行設定の一覧を返します。|  
|<xref:ReportExecution2005.ReportExecutionService.Render%2A>|指定されたレポートを処理し、指定された書式でレポートを表示します。|  
|<xref:ReportService2010.ReportingService2010.SetCacheOptions%2A>|アイテムをキャッシュ用に構成し、キャッシュ内のアイテムの有効期限を示す設定を提供します。|  
|<xref:ReportService2010.ReportingService2010.SetExecutionOptions%2A>|指定したアイテムの実行オプションおよび関連付けられた実行プロパティを設定します。|  
|<xref:ReportService2010.ReportingService2010.UpdateItemExecutionSnapshot%2A>|指定したアイテムのアイテム実行スナップショットを生成します。|  
  
## <a name="see-also"></a>参照  
 [Web サービスと .NET Framework を使用してのアプリケーションの構築](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [レポート サーバー Web サービス](../../../reporting-services/report-server-web-service/report-server-web-service.md)   
 [レポート サーバー Web サービス メソッド](../../../reporting-services/report-server-web-service/methods/report-server-web-service-methods.md)   
 [テクニカル リファレンス (SSRS)](../../../reporting-services/technical-reference-ssrs.md)  
  
  
