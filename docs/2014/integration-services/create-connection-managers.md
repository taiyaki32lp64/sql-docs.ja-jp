---
title: 接続マネージャーを作成する |Microsoft Docs
ms.custom: ''
ms.date: 08/22/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.connectionmanager.f1
helpviewer_keywords:
- Integration Services packages, connections
- SSIS packages, connections
- packages [Integration Services], connections
- connection managers [Integration Services], creating
- SQL Server Integration Services packages, connections
ms.assetid: 6ca317b8-0061-4d9d-b830-ee8c21268345
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: a82ef5c249dd1bc15bc91e9ccc502ebffe3f1728
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66060121"
---
# <a name="create-connection-managers"></a>接続マネージャーを作成する
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] には、さまざまな種類のサーバーやデータ ソースに接続するタスクのニーズに合わせるため、さまざまな接続マネージャーが用意されています。 接続マネージャーは、データを抽出してさまざまな種類のデータ ストアに読み込むデータ フロー コンポーネントや、ログをサーバー、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] テーブル、またはファイルに書き込むログ プロバイダーによって使用されます。 たとえば、メール送信タスクが含まれるパッケージには、簡易メール転送プロトコル (SMTP) サーバーに接続するタイプの SMTP 接続マネージャーを使用します。 SQL 実行タスクが含まれるパッケージでは、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] データベースに接続する OLE DB 接続マネージャーを使用できます。 詳細については、「[Integration Services (SSIS) の接続](connection-manager/integration-services-ssis-connections.md)」を参照してください。  
  
 新しいパッケージを作成する際に接続マネージャーを自動的に作成して構成する場合は、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] インポートおよびエクスポート ウィザードを使用できます。 このウィザードは、接続マネージャーを使用する変換元および変換先の作成と構成を行う場合に役立ちます。 詳細については、「 [SQL Server データ ツールでのパッケージの作成](create-packages-in-sql-server-data-tools.md)」を参照してください。  
  
 手動で新しい接続マネージャーを作成して既存のパッケージに追加するには、[!INCLUDE[ssIS](../includes/ssis-md.md)] デザイナーの **[制御フロー]** タブ、 **[データ フロー]** タブ、および **[イベント ハンドラー]** タブに表示される **[接続マネージャー]** 領域を使用します。 **[接続マネージャー]** 領域で、作成する接続マネージャーの種類を選択し、[!INCLUDE[ssIS](../includes/ssis-md.md)] デザイナーで用意されているダイアログ ボックスを使用して、接続マネージャーのプロパティを設定します。 詳細については、後の「[接続マネージャー] 領域の使用」を参照してください。  
  
 パッケージに接続マネージャーを追加すると、タスク、Foreach ループ コンテナー、変換元、変換、および変換先で使用できます。 詳細については、「[Integration Services タスク](control-flow/integration-services-tasks.md)」、「[Foreach ループ コンテナー](control-flow/foreach-loop-container.md)」、および「[データ フロー](data-flow/data-flow.md)」を参照してください。  
  
## <a name="using-the-connection-managers-area"></a>[接続マネージャー] 領域の使用  
 接続マネージャーは、[!INCLUDE[ssIS](../includes/ssis-md.md)] デザイナーの **[制御フロー]** タブ、 **[データ フロー]** タブ、または **[イベント ハンドラー]** タブがアクティブなときに作成できます。  
  
 次の図は、[!INCLUDE[ssIS](../includes/ssis-md.md)] デザイナーの **[制御フロー]** タブ上にある **[接続マネージャー]** 領域を示しています。  
  
 ![パッケージの制御フロー デザイナーのスクリーンショット](media/samplecontrolflow.gif "パッケージの制御フロー デザイナーのスクリーンショット")  
  
#### <a name="to-add-configure-or-delete-a-connection-manager-in-ssis-designer"></a>SSIS デザイナーで接続マネージャーを追加、構成、または削除するには  
  
-   [パッケージの接続マネージャーを追加、削除、または共有する](../../2014/integration-services/add-delete-or-share-a-connection-manager-in-a-package.md)  
  
-   [接続マネージャーのプロパティを設定する](../../2014/integration-services/set-the-properties-of-a-connection-manager.md)  
  
## <a name="32-bit-and-64-bit-providers-for-connection-managers"></a>接続マネージャーの 32 ビット プロバイダーと 64 ビット プロバイダー  
 接続マネージャーが使用する多くのプロバイダーには、32 ビット バージョンと 64 ビット バージョンがあります。 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] のデザイン環境は 32 ビット環境であり、パッケージのデザイン時には 32 ビット プロバイダーのみが表示されます。 したがって、接続マネージャーで特定の 64 ビット プロバイダーが使用されるように構成できるのは、同じプロバイダーの 32 ビット バージョンがインストールされている場合のみです。  
  
 デザイン時に 32 ビット バージョンのプロバイダーを指定したかどうかにかかわらず、実行時には適切なバージョンが使用されます。 パッケージが [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] で実行されている場合でも、64 ビット バージョンのプロバイダーを実行できます。  
  
 どちらのバージョンのプロバイダーも ID は同じです。 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] ランタイムで使用可能な 64 ビット バージョンのプロバイダーを使用するかどうかを指定するには、[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトの Run64BitRuntime プロパティを設定します。 Run64BitRuntime プロパティ設定されている場合`true`、ランタイムが見つけて Run64BitRuntime がある場合は 64 ビット プロバイダーを使用して`false`ランタイムが検索し、32 ビット プロバイダーを使用します。 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトで設定できるプロパティの詳細については、「[Integration Services (SSIS) と Studio の環境](integration-services-ssis-development-and-management-tools.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [[制御フロー]](control-flow/control-flow.md)   
 [データ フロー](data-flow/data-flow.md)   
 [Integration Services (SSIS) のイベント ハンドラー](integration-services-ssis-event-handlers.md)  
  
  
