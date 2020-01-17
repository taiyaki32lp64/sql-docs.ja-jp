---
title: Integration Services (SSIS) と Studio 環境 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- studio environments [Integration Services]
- tools [Integration Services], Business Intelligence Development Studio
- Business Intelligence Development Studio, Integration Services in
- SQL Server Management Studio [Integration Services]
- SSIS, studio environments
- SQL Server Integration Services, studio environments
- tools [Integration Services], SQL Server Management Studio
ms.assetid: 4eb73e65-d9f3-4ac6-a408-abfa85afc537
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 7c8f05c1b822cc3cad81ed910b71cb46621554eb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62892455"
---
# <a name="integration-services-ssis-and-studio-environments"></a>Integration Services (SSIS) と Studio の環境
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] には、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]と組み合わせて活用できる 2 つの "Studio" が含まれています。  
  
-   1 つは、ビジネス ソリューションに必要な[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] パッケージを開発するための [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] です。 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] の [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトを使ってパッケージを作成します。  
  
-   もう 1 つは、運用環境でパッケージを管理するための[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] です。  
  
## <a name="sql-server-data-tools"></a>SQL Server Data Tools  
 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]を使用すると、次のタスクを実行できます。  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] インポートおよびエクスポート ウィザードを実行し、変換元のデータを変換先にコピーする基本パッケージを作成します。  
  
-   複雑な制御フロー、データ フロー、イベント ドリブン手法、およびログ記録が含まれるパッケージを作成します。  
  
-   [!INCLUDE[ssIS](../includes/ssis-md.md)] デザイナーのトラブルシューティングと監視機能、および [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]のデバック機能を使用して、パッケージをテストおよびデバッグします。  
  
-   パッケージとパッケージ オブジェクトのプロパティを、実行時に更新する構成を作成します。  
  
-   パッケージとその依存関係を別のコンピューターにインストールする、配置ユーティリティを作成します。  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の msdb データベース、[!INCLUDE[ssIS](../includes/ssis-md.md)] パッケージ ストア、およびファイル システムに、パッケージのコピーを保存します。  
  
 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]の詳細については、「 [SQL Server Data Tools](https://msdn.microsoft.com/library/hh272686.aspx)」を参照してください。  
  
## <a name="sql-server-management-studio"></a>SQL Server Management Studio  
 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] の [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] サービスを利用して、パッケージの管理、実行中のパッケージの監視、および [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] オブジェクトと [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] オブジェクトの影響とデータ系列の決定を行います。  
  
 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]を使用すると、次のタスクを実行できます。  
  
-   わかりやすい方法でパッケージを整理するために、フォルダーを作成します。  
  
-   パッケージ実行ユーティリティを使用して、ローカル コンピューター上に格納されているパッケージを実行します。  
  
-   パッケージ実行ユーティリティを実行して、 **dtexec** コマンド プロンプト ユーティリティ (dtexec.exe) の実行時に使用するコマンド ラインを生成します。  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の msdb データベース、[!INCLUDE[ssIS](../includes/ssis-md.md)] パッケージ ストア、およびファイル システムのパッケージをインポートおよびエクスポートします。  
  
