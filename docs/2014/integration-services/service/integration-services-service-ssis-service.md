---
title: Integration Services サービス (SSIS サービス) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services service, about Integration Services service
- SQL Server Integration Services service
- service [Integration Services],about Integration Services service
- service [Integration Services]
- SQL Server Integration Services, service
ms.assetid: 2c785b3b-4a0c-4df7-b5cd-23756dc87842
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 7eb8f74e271b9d5c19cedab4fd25069eb5a0e2b1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62766694"
---
# <a name="integration-services-service-ssis-service"></a>Integration Services サービス (SSIS サービス)
  このセクションのトピックでは、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージを管理するための Windows サービスである [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスについて説明します。 Integration Service パッケージの作成、保存、および実行には、このサービスは不要です。 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以前のリリースの [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] との互換性を維持するために、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]サービスをサポートしています。  
  
 以降では[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]オブジェクト、設定、および業務データを格納、`SSISDB`に配置したプロジェクト用のデータベース、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]プロジェクト配置モデルを使用してサーバー。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] データベース エンジンのインスタンスである [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サーバーは、データベースをホストします。 データベースの詳細については、「 [SSIS カタログ](../catalog/ssis-catalog.md)」を参照してください。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サーバーへのプロジェクトの配置の詳細については、「 [Integration Services サーバーへのプロジェクトの配置](../deploy-projects-to-integration-services-server.md)」を参照してください。  
  
## <a name="management-capabilities"></a>管理機能  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスは、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージを管理するための Windows サービスです。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスは [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]でのみ使用できます。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスを実行すると、以下の管理機能が使用できます。  
  
-   リモートまたはローカルに格納されたパッケージの開始  
  
-   リモートまたはローカルで実行中のパッケージの停止  
  
-   リモートまたはローカルで実行中のパッケージの監視  
  
-   パッケージのインポートおよびエクスポート  
  
-   パッケージ ストレージの管理  
  
-   ストレージ フォルダーのカスタマイズ  
  
-   サービス停止時の実行中のパッケージの停止  
  
-   Windows のイベント ログの表示  
  
-   複数の [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サーバーへの接続  
  
## <a name="startup-type-for-integration-services-service"></a>Integration Services サービスのスタートアップの種類  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスは [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]コンポーネントのインストール時にインストールされます。 既定では、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスが起動され、スタートアップの種類が自動に設定されます。 [!INCLUDE[ssIS](../../includes/ssis-md.md)] パッケージ ストアに格納されているパッケージを監視するには、サービスが実行されている必要があります。 [!INCLUDE[ssIS](../../includes/ssis-md.md)] パッケージ ストアは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンス内の msdb データベース、またはファイル システム内の指定されたフォルダーのいずれかです。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージの設計と実行だけを行う場合は、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスは必要ありません。 ただし、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]を使用してパッケージを一覧表示し、監視する場合はサービスが必要です。  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [Integration Services サービスのプロパティを設定する](../set-the-properties-of-the-integration-services-service.md)  
  
-   [Integration Services サービスのイベントを表示する](../view-events-for-the-integration-services-service.md)  
  
  
