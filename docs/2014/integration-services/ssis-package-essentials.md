---
title: SSIS パッケージの Essentials |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- package requirements
ms.assetid: b0c86c35-e3d3-4724-9a96-4087e9d74bf3
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8cba1fb860d884b568fe132fc2b38ff50fbd480d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66055417"
---
# <a name="ssis-package-essentials"></a>SSIS パッケージの基本事項
  パッケージは、データの抽出、変換、および読み込みを行うための [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 機能が実装されているオブジェクトです。 パッケージは [!INCLUDE[ssIS](../includes/ssis-md.md)] で [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] デザイナーを使用して作成します。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] インポートおよびエクスポート ウィザード、または [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 接続プロジェクト ウィザードを使用してもパッケージを作成できます。 詳細については、 [SQL Server Data Tools でパッケージの作成](create-packages-in-sql-server-data-tools.md)SSIS デザイナーで、[プロジェクトのインポート ウィザード](../../2014/integration-services/import-project-wizard.md)します。  
  
 基本的なパッケージには次の要素が含まれます。  
  
 **制御フロー要素**  
 制御フロー要素は必須要素で、さまざまな関数を実行し、構造を提供し、要素が実行される順序を制御します。 主な制御フロー要素は、タスク、コンテナー、および優先順位制約です。 パッケージには、制御フロー要素が少なくとも 1 つ必要です。  
  
 詳細については、「 [Control Flow](control-flow/control-flow.md)」を参照してください。  
  
 **データ フロー要素**  
 データ フロー要素は省略可能な要素で、データの抽出、変更、およびデータ ソースへの読み込みを行います。 主なデータ フロー要素は、変換元、変換、および変換先です。 データ フロー要素はパッケージに含まれていなくてもかまいません。  
  
 詳細については、「 [Data Flow](data-flow/data-flow.md)」を参照してください。  
  
 基本的なパッケージを作成する方法の例は、次を参照してください。[レッスン 1。プロジェクトと基本パッケージ作成](lesson-1-create-a-project-and-basic-package-with-ssis.md)です。  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [SQL Server データ ツールでのパッケージの作成](create-packages-in-sql-server-data-tools.md)  
  
-   [制御フローのタスクまたはコンテナーを追加または削除する](control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)  
  
-   [タスクまたはコンテナーのプロパティを設定する](../../2014/integration-services/set-the-properties-of-a-task-or-container.md)  
  
-   [データ フローでコンポーネントを追加または削除する](data-flow/add-or-delete-a-component-in-a-data-flow.md)  
  
## <a name="related-content"></a>関連コンテンツ  
  
1.  MSDN.Microsoft.com のビデオ「[基本パッケージの作成 (SQL Server ビデオ)](https://go.microsoft.com/fwlink/?LinkId=131023)」  
  
## <a name="see-also"></a>参照  
 [Integration Services &#40;SSIS&#41; パッケージ](../../2014/integration-services/integration-services-ssis-packages.md)   
 [優先順位制約](control-flow/precedence-constraints.md)  
  
  
