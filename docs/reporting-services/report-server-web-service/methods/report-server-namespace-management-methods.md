---
title: レポート サーバー名前空間管理メソッド | Microsoft Docs
ms.date: 03/06/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-web-service
ms.topic: reference
helpviewer_keywords:
- reports [Reporting Services], managing
- management methods [Reporting Services]
- methods [Reporting Services], about methods
- methods [Reporting Services]
ms.assetid: 2aa43ce9-f51e-408a-8ce0-b40d3dd62561
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 7639cd7ce7cd33f59fbc65116264a8b887879b77
ms.sourcegitcommit: 710d60e7974e2c4c52aebe36fceb6e2bbd52727c
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 10/11/2019
ms.locfileid: "72278296"
---
# <a name="report-server-namespace-management-methods"></a>レポート サーバー名前空間管理メソッド
  レポート サーバー管理 Web サービスには、レポート サーバー データベースのレポート、フォルダー、およびリソースの管理に使用できるメソッドが含まれています。  
  
|方法|操作|  
|------------|------------|  
|<xref:ReportService2010.ReportingService2010.CancelJob%2A>|ジョブの実行を取り消します。|  
|<xref:ReportService2010.ReportingService2010.CreateFolder%2A>|レポート サーバー データベースまたは SharePoint ライブラリにフォルダーを追加します。|  
|<xref:ReportService2010.ReportingService2010.CreateCatalogItem%2A>|レポート サーバー データベースまたは SharePoint ライブラリに新しいアイテムを追加します。 このメソッドが適用されるアイテムの種類は、**Report**、**Model**、**Dataset**、**Component**、**Resource**、**DataSource** です。|  
|M:ReportService2010.ReportingService2010.CreateReportEditSession (System.string, system.string, System.string [], ReportService2010 [] @) を指定します。|新しいレポート編集セッションを作成します。|  
|<xref:ReportService2010.ReportingService2010.DeleteItem%2A>|レポート サーバー データベースまたは SharePoint ライブラリからアイテムを削除します。|  
|<xref:ReportService2010.ReportingService2010.FindItems%2A>|指定した検索条件に一致する、レポート サーバー データベースまたは SharePoint ライブラリのアイテムを返します。|  
|<xref:ReportService2010.ReportingService2010.FireEvent%2A>|指定したパラメーターに基づいてイベントをトリガーします。|  
|<xref:ReportService2010.ReportingService2010.GetExtensionSettings%2A>|指定した拡張機能の設定の一覧を返します。|  
|<xref:ReportService2010.ReportingService2010.GetItemType%2A>|レポート サーバー データベースまたは SharePoint ライブラリにアイテムが存在する場合に、アイテムの種類を取得します。|  
|<xref:ReportService2010.ReportingService2010.GetProperties%2A>|レポート サーバー データベースまたは SharePoint ライブラリのアイテムに関する 1 つ以上のプロパティ値を返します。|  
|<xref:ReportService2010.ReportingService2010.GetItemDefinition%2A>|アイテムの定義またはコンテンツを取得します。 このメソッドが適用されるアイテムの種類は、**Report**、**Model**、**Dataset**、**Component**、**Resource**、**DataSource** です。|  
|<xref:ReportService2010.ReportingService2010.GetItemReferences%2A>|アイテムに関連付けられたカタログ アイテム参照の一覧を返します。|  
|<xref:ReportService2010.ReportingService2010.GetReportServerConfigInfo%2A>|接続しているレポート サーバー インスタンス、またはスケールアウト配置内のすべてのレポート サーバー インスタンスに関する情報を返します。|  
|<xref:ReportService2010.ReportingService2010.GetSystemProperties%2A>|1 つ以上のシステム プロパティを返します。|  
|<xref:ReportService2010.ReportingService2010.ListChildren%2A>|指定したフォルダーの子の一覧を取得します。|  
|<xref:ReportService2010.ReportingService2010.ListDatabaseCredentialRetrievalOptions%2A>|サポートされている資格情報取得オプションの一覧を返します。|  
|<xref:ReportService2010.ReportingService2010.ListEvents%2A>|レポート サーバー構成ファイルに表示されるイベント拡張機能の一覧を返します。|  
|<xref:ReportService2010.ReportingService2010.ListJobs%2A>|レポート サーバーで実行中のジョブの一覧を返します。|  
|<xref:ReportService2010.ReportingService2010.ListExtensions%2A>|指定した拡張機能の種類に対して構成された拡張機能の一覧を返します。|  
|<xref:ReportService2010.ReportingService2010.ListExtensionTypes%2A>|サポートされている拡張機能の種類の一覧を返します。|  
|<xref:ReportService2010.ReportingService2010.ListItemTypes%2A>|サポートされているカタログ アイテムの種類の一覧を返します。|  
|<xref:ReportService2010.ReportingService2010.ListJobActions%2A>|サポートされているジョブの操作の一覧を返します。|  
|<xref:ReportService2010.ReportingService2010.ListJobStates%2A>|サポートされているジョブの状態の一覧を返します。|  
|<xref:ReportService2010.ReportingService2010.ListJobTypes%2A>|サポートされているジョブの種類の一覧を返します。|  
|<xref:ReportService2010.ReportingService2010.ListParents%2A>|指定したアイテムの親アイテムを取得します。|  
|<xref:ReportService2010.ReportingService2010.ListSecurityScopes%2A>|サポートされているセキュリティ スコープの一覧を返します。|  
|<xref:ReportService2010.ReportingService2010.Logoff%2A>|Web サービス要求を行っている現在のユーザーをログアウトします。 このメソッドは、ネイティブ モードにのみ適用されます。|  
|<xref:ReportService2010.ReportingService2010.LogonUser%2A>|ユーザーのログオンを処理し、レポート サーバー Web サービスへのユーザーの要求を認証します。 このメソッドは、ネイティブ モードにのみ適用されます。|  
|<xref:ReportService2010.ReportingService2010.SetItemReferences%2A>|アイテムに関連付けられたカタログ アイテムを設定します。|  
|<xref:ReportService2010.ReportingService2010.MoveItem%2A>|アイテムの移動や名前の変更を行います。|  
|<xref:ReportService2010.ReportingService2010.SetProperties%2A>|アイテムの 1 つ以上のプロパティを設定します。|  
|<xref:ReportService2010.ReportingService2010.SetItemDefinition%2A>|指定したアイテムの定義またはコンテンツを設定します。 このメソッドが適用されるアイテムの種類は、**Report**、**Model**、**Dataset**、**Component**、**Resource**、**DataSource** です。|  
|<xref:ReportService2010.ReportingService2010.SetSystemProperties%2A>|レポート サーバーまたは SharePoint ファームの 1 つ以上のシステム プロパティを設定します。|  
|<xref:ReportService2010.ReportingService2010.ValidateExtensionSettings%2A>|[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 拡張機能の設定を検証します。|  
  
## <a name="see-also"></a>参照  
 [Web サービスと .NET Framework を使用してのアプリケーションの構築](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [レポート サーバー Web サービス](../../../reporting-services/report-server-web-service/report-server-web-service.md)   
 [レポート サーバー Web サービス メソッド](../../../reporting-services/report-server-web-service/methods/report-server-web-service-methods.md)   
 [テクニカル リファレンス (SSRS)](../../../reporting-services/technical-reference-ssrs.md)  
  
  
