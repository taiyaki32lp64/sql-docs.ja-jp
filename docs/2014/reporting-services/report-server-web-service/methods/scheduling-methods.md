---
title: メソッドのスケジュール設定 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- schedules [Reporting Services], methods
- reports [Reporting Services], scheduling
- shared schedules [Reporting Services], methods
- methods [Reporting Services], scheduling
ms.assetid: 68ae13f9-d91e-4572-a82a-8fa42001569e
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 99dac71ba0be4f4c3f3ff669f838b0409b996f06
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63283454"
---
# <a name="scheduling-methods"></a>メソッドのスケジュール設定
  これらのメソッドを使用して、レポート サーバーが利用する、レポートの実行と配信のための共有スケジュールとキャッシュ更新計画を作成および管理できます。  
  
|方法|操作|  
|------------|------------|  
|<xref:ReportService2010.ReportingService2010.CreateCacheRefreshPlan%2A>|アイテムのキャッシュ更新プランを作成します。|  
|<xref:ReportService2010.ReportingService2010.CreateSchedule%2A>|新しい共有スケジュールを作成します。|  
|<xref:ReportService2010.ReportingService2010.DeleteCacheRefreshPlan%2A>|キャッシュ更新プランを削除します。|  
|<xref:ReportService2010.ReportingService2010.DeleteSchedule%2A>|特定のスケジュール ID に基づいて共有スケジュールを削除します。|  
|<xref:ReportService2010.ReportingService2010.GetCacheRefreshPlanProperties%2A>|指定したキャッシュ更新プランのプロパティを返します。|  
|<xref:ReportService2010.ReportingService2010.GetScheduleProperties%2A>|共有スケジュールのプロパティ値を返します。|  
|<xref:ReportService2010.ReportingService2010.ListCacheRefreshPlans%2A>|カタログ アイテムに関連付けられたキャッシュ更新プランの一覧を返します。|  
|<xref:ReportService2010.ReportingService2010.ListScheduledItems%2A>|共有スケジュールに関連付けられたアイテムの一覧を返します。|  
|<xref:ReportService2010.ReportingService2010.ListSchedules%2A>|レポート サーバーまたは SharePoint サイトにおけるすべての共有スケジュールの一覧を返します。|  
|<xref:ReportService2010.ReportingService2010.ListScheduleStates%2A>|サポートされているスケジュールの状態の一覧を返します。|  
|<xref:ReportService2010.ReportingService2010.PauseSchedule%2A>|指定したスケジュールの実行を一時停止します。|  
|<xref:ReportService2010.ReportingService2010.ResumeSchedule%2A>|一時停止している共有スケジュールを再開します。|  
|<xref:ReportService2010.ReportingService2010.SetCacheRefreshPlanProperties%2A>|キャッシュ更新計画のプロパティを設定します。|  
|<xref:ReportService2010.ReportingService2010.SetScheduleProperties%2A>|共有スケジュールのプロパティ値を設定します。|  
  
## <a name="see-also"></a>関連項目  
 [Web サービスと .NET Framework を使用してのアプリケーションの構築](../net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [レポート サーバー Web サービス](../report-server-web-service.md)   
 [レポート サーバー Web サービス メソッド](report-server-web-service-methods.md)   
 [テクニカル リファレンス (SSRS)](../../technical-reference-ssrs.md)  
  
  
