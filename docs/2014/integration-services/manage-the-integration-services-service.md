---
title: Integration Services サービスの管理 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services service, configuring
- services [Integration Services], configuring
ms.assetid: 45554117-a0df-4830-b41c-5ebb33b764a5
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: fc3b1eb4e73b3d77b49cc9f485e0a6fc456a8875
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66057789"
---
# <a name="manage-the-integration-services-service"></a>Integration Services サービスを管理する
    
> [!IMPORTANT]  
>  このトピックでは、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] パッケージを管理するための Windows サービスである [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] サービスについて説明します。 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] では、以前のリリースの [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]との互換性を維持するために、このサービスをサポートしています。 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]以降では、Integration Services サーバー上のパッケージなどのオブジェクトを管理できます。  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] の [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] コンポーネントのインストール時に、[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] サービスもインストールされます。 既定では、[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] サービスが起動され、スタートアップの種類が自動に設定されます。 ただし、サービスを使用して [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] の格納されたパッケージおよび実行中のパッケージを管理するには、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] をインストールする必要があります。  
  
> [!NOTE]  
>  インスタンスに接続することはできません、 [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]からサービス、[!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]版[!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]します。 で、**サーバーへの接続**ダイアログ ボックスで、サーバーの名前をのみを入力することはできません、[!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]のバージョン、[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]サービスが実行されています。 ただし、サービスの構成ファイルを編集することで、[!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] バージョンの [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] から、[!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] のインスタンスに格納されているパッケージを管理できます。 詳細については、「 [Integration Services サービスの構成 (SSIS サービス)](service/integration-services-service-ssis-service.md)との互換性を維持するために、このサービスをサポートしています。  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] サービスのインスタンスは 1 台のコンピューターに 1 つだけインストールできます。 このサービスは、[!INCLUDE[ssDE](../includes/ssde-md.md)] の特定のインスタンスに固有ではありません。 サービスに接続するには、サービスが実行されているコンピューターの名前を使用します。  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] サービスは、次の Microsoft 管理コンソール (MMC) スナップインのいずれかを使用して管理できます: SQL Server 構成マネージャーまたはサービス。 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]でパッケージを管理するには、事前にサービスを起動しておく必要があります。  
  
 既定では、[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] サービスは、[!INCLUDE[ssDE](../includes/ssde-md.md)] と同時にインストールされる[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]のインスタンスの msdb データベース内にあるパッケージを管理するように構成されます。 [!INCLUDE[ssDE](../includes/ssde-md.md)]のインスタンスが同時にインストールされない場合、[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] サービスは、[!INCLUDE[ssDE](../includes/ssde-md.md)]のローカルの既定インスタンスの msdb データベース内にあるパッケージを管理するように構成されます。 [!INCLUDE[ssDE](../includes/ssde-md.md)] の名前付きインスタンスまたはリモート インスタンス、あるいは [!INCLUDE[ssDE](../includes/ssde-md.md)] の複数のインスタンスに格納されているパッケージを管理するには、サービスの構成ファイルを変更する必要があります。 詳細については、「 [Integration Services サービスの構成 (SSIS サービス)](service/integration-services-service-ssis-service.md)との互換性を維持するために、このサービスをサポートしています。  
  
 既定では、[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] サービスが停止すると、パッケージの実行も停止するように設定されています。 ただし、[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] サービスはパッケージが停止するまで待機しないため、[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] サービスの停止後に実行を続けるパッケージもあります。  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] サービスが停止した場合、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] インポートおよびエクスポート ウィザード、[!INCLUDE[ssIS](../includes/ssis-md.md)] デザイナー、パッケージ実行ユーティリティ、および **dtexec** コマンド プロンプト ユーティリティ (dtexec.exe) を使用してパッケージを実行し続けることができます。 ただし、実行中のパッケージを監視することはできません。  
  
 既定では、[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] サービスは NETWORK SERVICE アカウントのコンテキスト内で実行されます。  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] サービスは Windows のイベント ログに書き込みを行います。 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] でサービス イベントを表示できます。 Windows イベント ビューアーを使用してサービス イベントを表示することもできます。  
  
### <a name="to-set-properties-of-integration-services-service-using-the-services-snap-in"></a>サービス スナップインを使用して Integration Services サービスのプロパティを設定するには  
  
-   [Integration Services サービスのプロパティを設定する](../../2014/integration-services/set-the-properties-of-the-integration-services-service.md)  
  
### <a name="to-view-service-events-for-integration-services-service"></a>Integration Services のサービス イベントを表示するには  
  
-   [Integration Services サービスのイベントを表示する](../../2014/integration-services/view-events-for-the-integration-services-service.md)  
  
## <a name="see-also"></a>関連項目  
 [Integration Services サービス (SSIS サービス)](service/integration-services-service-ssis-service.md)   
 [Integration Services サービスの構成 (SSIS サービス)](configuring-the-integration-services-service-ssis-service.md)   
 [SQL Server インポートおよびエクスポート ウィザード](import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md)   
 [dtexec ユーティリティ](packages/dtexec-utility.md)   
 [プロジェクトとパッケージの実行](packages/run-integration-services-ssis-packages.md)  
  
  
