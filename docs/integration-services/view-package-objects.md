---
title: パッケージ オブジェクトを表示する | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services packages, properties
- properties [Integration Services]
- Package Explorer window [Integration Services]
- packages [Integration Services], properties
- explorer view [Integration Services]
- SSIS packages, properties
- viewing package objects
- SQL Server Integration Services packages, properties
ms.assetid: a85c0245-0a68-4eb0-83b1-9b11df80bd10
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 28393d15ade12562dbcaa4af457bf0de0e51948b
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71295020"
---
# <a name="view-package-objects"></a>パッケージ オブジェクトを表示する

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  [!INCLUDE[ssIS](../includes/ssis-md.md)] デザイナーでは、 **[パッケージ エクスプローラー]** タブで、パッケージをエクスプローラー表示できます。 この表示には、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] アーキテクチャのコンテナー階層が反映されます。 パッケージ コンテナーはこの階層の最上層にあり、パッケージを展開すると、そのパッケージ内にある接続、実行可能ファイル、イベント ハンドラー、ログ プロバイダー、優先順位制約、および変数が表示されます。  
  
 実行可能ファイルとは、パッケージ内のコンテナーおよびタスクのことで、イベント ハンドラー、優先順位制約、および変数を含めることができます。 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] では、入れ子構造の階層のコンテナーがサポートされているため、For ループ コンテナー、Foreach ループ コンテナー、およびシーケンス コンテナーは他の実行可能ファイルを含めることができます。  
  
 パッケージにデータ フローが含まれる場合、 **パッケージ エクスプローラー** にはデータ フロー タスクが一覧表示され、データ フロー コンポーネントを一覧表示する **[コンポーネント]** フォルダーが含まれます。  
  
 **[パッケージ エクスプローラー]** タブでは、パッケージ内のオブジェクトを削除したり、 **[プロパティ]** ウィンドウにアクセスしてオブジェクトのプロパティを表示できます。  
  
 次の図は、簡単なパッケージのツリー ビューを示しています。  
  
 ![[パッケージ エクスプローラー] タブのスクリーンショット](../integration-services/media/packageexplorer.gif "[パッケージ エクスプローラー] タブのスクリーンショット")  
  
## <a name="view-the-package-structure-and-content"></a>パッケージの構造と内容を表示する  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]で、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] パッケージ エクスプローラー **で表示するパッケージが含まれている**プロジェクトを開きます。  
  
2.  **[パッケージ エクスプローラー]** タブをクリックします。  
  
3.  **[変数]** 、 **[優先順位制約]** 、 **[イベント ハンドラー]** 、 **[接続マネージャー]** 、 **[ログ プロバイダー]** 、または **[実行可能ファイル]** フォルダーの内容を表示するには、各フォルダーを展開します。  
  
4.  パッケージの構造に基づき、次の任意のレベルのフォルダーを展開します。  
  
## <a name="view-the-properties-of-a-package-object"></a>パッケージ オブジェクトのプロパティを表示する
  
-   オブジェクトを右クリックして **[プロパティ]** をクリックし、 **[プロパティ]** ウィンドウを開きます。  
  
## <a name="delete-an-object-in-a-package"></a>パッケージのオブジェクトを削除する  
  
-   オブジェクトを右クリックし、 **[削除]** をクリックします。 
 
## <a name="see-also"></a>参照  
 [Integration Services タスク](../integration-services/control-flow/integration-services-tasks.md)   
 [Integration Services コンテナー](../integration-services/control-flow/integration-services-containers.md)   
 [優先順位制約](../integration-services/control-flow/precedence-constraints.md)   
 [Integration Services (SSIS) の変数](../integration-services/integration-services-ssis-variables.md)   
 [Integration Services (SSIS) のイベント ハンドラー](../integration-services/integration-services-ssis-event-handlers.md)   
 [Integration Services &#40;SSIS&#41; のログ記録](../integration-services/performance/integration-services-ssis-logging.md)  
  
  
