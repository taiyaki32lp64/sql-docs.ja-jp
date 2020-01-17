---
title: Integration Services (SSIS) の開発と管理ツール |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
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
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 6ef390245e632b3e2c39bcc9ab27450839dcab2e
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71284367"
---
# <a name="integration-services-ssis-development-and-management-tools"></a>Integration Services (SSIS) の開発と管理ツール

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] には、パッケージと組み合わせて活用できる 2 つの Studio が含まれています。  
  
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
