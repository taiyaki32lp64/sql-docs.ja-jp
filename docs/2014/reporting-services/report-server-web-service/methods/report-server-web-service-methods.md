---
title: レポート サーバー Web サービスのメソッド | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- Report Server Web service, methods
- Web service [Reporting Services], methods
- XML Web service [Reporting Services], features
- Web service [Reporting Services], features
- Report Server Web service, features
- XML Web service [Reporting Services], methods
ms.assetid: ce5afa27-e90c-44a7-b204-098a065b3665
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 37d0031ebfb4ec6d31da6aad9a8842c0623cb75b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63283480"
---
# <a name="report-server-web-service-methods"></a>レポート サーバー Web サービスのメソッド
  レポート サーバー Web サービスには、コンポーネントの機能に基づいた、複数のカテゴリのメソッドが含まれています。 これらのメソッドは、Web サービスのいくつかのエンドポイントを介して (レポート管理用に 3 つ、レポート実行用に 1 つ)、<xref:ReportService2010.ReportingService2010> クラスおよび <xref:ReportExecution2005.ReportExecutionService> クラスのメンバーとして提供されます。 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] SDK に含まれる wsdl.exe などのプロキシ クラス ツールを使用して、これらのクラスを生成できます。 Report Server Web サービスと [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] の詳細については、「[Web サービスと、.NET Framework を使用してのアプリケーションの構築](../net-framework/building-applications-using-the-web-service-and-the-net-framework.md)」を参照してください。  
  
## <a name="endpoints-and-methods"></a>エンドポイントおよびメソッド  
 次の表に、レポート サーバー Web サービスのエンドポイントと、<xref:ReportService2010.ReportingService2010> エンドポイントにより提供されるメソッドのカテゴリを示します。 他のエンドポイントで利用可能なメソッドの詳細については、「[テクニカル リファレンス (SSRS)](../../technical-reference-ssrs.md)」を参照してください。  
  
|トピック|説明|  
|-----------|-----------------|  
|[レポート サーバー Web サービス, エンドポイント](report-server-web-service-endpoints.md)|レポート サーバー Web サービスの管理用エンドポイントと実行用エンドポイントについて説明します。|  
|[レポート サーバー名前空間管理メソッド](report-server-namespace-management-methods.md)|レポート サーバー データベースの管理に使用できるメソッドについて説明します。 フォルダーとリソースの管理、アイテム プロパティの設定を行えます。|  
|[Authorization メソッド](authorization-methods.md)|タスク、ロール、およびポリシーの管理に使用できるメソッドについて説明します。|  
|[データ ソースと接続のメソッド](data-sources-and-connection-methods.md)|レポートのデータ ソース接続や資格情報の設定および管理に使用できるメソッドについて説明します。|  
|[レポート パラメーターのメソッド](report-parameters-methods.md)|レポートのパラメーターを設定および取得するためのメソッドについて説明します。|  
|[モデルのメソッド](../report-server-web-service.md)|モデルの管理に使用できるメソッドについて説明します。|  
|[Rendering メソッドと Execution メソッド](rendering-and-execution-methods.md)|レポートの実行、表示、およびキャッシュを管理するためのメソッドについて説明します。|  
|[レポート履歴メソッド](report-history-methods.md)|レポート履歴スナップショットを作成および管理するためのメソッドについて説明します。|  
|[メソッドのスケジュール設定](scheduling-methods.md)|レポート サーバーが使用する共有スケジュールとキャッシュ更新計画を作成および管理するためのメソッドについて説明します。|  
|[サブスクリプション メソッドおよび配信メソッド](subscription-and-delivery-methods.md)|サブスクリプションとレポート配信を作成および管理するためのメソッドについて説明します。|  
|[リンク レポートのメソッド](linked-reports-methods.md)|リンク レポートを作成および管理するためのメソッドについて説明します。|  
  
## <a name="see-also"></a>参照  
 [SOAP API へのアクセス](../accessing-the-soap-api.md)   
 [Web サービスと .NET Framework を使用してのアプリケーションの構築](../net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [レポート サーバー Web サービス](../report-server-web-service.md)   
 [テクニカル リファレンス (SSRS)](../../technical-reference-ssrs.md)  
  
  
