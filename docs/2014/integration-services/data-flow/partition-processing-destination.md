---
title: パーティション処理変換先 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.partitionprocessingdest.f1
helpviewer_keywords:
- partitions [Analysis Services], processing
- Partition Processing destination [Integration Services]
- destinations [Integration Services], Partition Processing
ms.assetid: 36c592ff-3f78-4a58-b496-31c1c8eee131
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 53ef09d19b62c0e6ce7742c41581d3cdefdfc374
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68890561"
---
# <a name="partition-processing-destination"></a>パーティション処理変換先
  パーティション処理変換先は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] のパーティションを読み込んで処理します。 パーティションの詳細については、「[パーティション (Analysis Services - 多次元データ)](https://docs.microsoft.com/analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data)」を参照してください。  
  
 パーティション処理変換先には、次の機能が含まれます。  
  
-   増分処理、完全処理、または更新処理を実行するオプション。  
  
-   エラー構成。処理中のエラーを無視するか、またはエラーが指定した回数に達した場合、処理を停止するかを指定します。  
  
-   パーティション分割列への入力列のマッピング。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] オブジェクトの処理に関する詳細については、「[処理オプションと設定 (Analysis Services)](https://docs.microsoft.com/analysis-services/multidimensional-models/processing-options-and-settings-analysis-services)」を参照してください。  
  
> [!NOTE]  
>  ここで説明されているタスクは、Analysis Services テーブル モデルには適用されません。  テーブル モデルで入力列をパーティション列にマップすることはできません。 代わりに Analysis Services DDL 実行タスク [Analysis Services Execute DDL Task](../control-flow/analysis-services-execute-ddl-task.md) を使用してパーティションを処理することができます。  
  
## <a name="configuration-of-the-partition-processing-destination"></a>パーティション処理変換先の構成  
 パーティション処理変換先は、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 接続マネージャーを接続して、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクト、または変換先が処理するキューブとパーティションを含む [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] のインスタンスに接続します。 詳細については、「 [Analysis Services 接続マネージャー](../connection-manager/analysis-services-connection-manager.md)」を参照してください。  
  
 この変換先は 1 つの入力をとります。 エラー出力はサポートされていません。  
  
 プロパティを設定するには [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 **[パーティション処理変換先エディター]** ダイアログ ボックスで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [パーティション処理変換先エディター ([接続マネージャー] ページ)](../partition-processing-destination-editor-connection-manager-page.md)  
  
-   [パーティション処理変換先エディター ([マッピング] ページ)](../partition-processing-destination-editor-mappings-page.md)  
  
-   [パーティション処理変換先エディター ([詳細設定] ページ)](../partition-processing-destination-editor-advanced-page.md)  
  
 **[詳細エディター]** ダイアログ ボックスには、プログラムによって設定できるプロパティが反映されます。 **[詳細エディター]** ダイアログ ボックスまたはプログラムで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [共通プロパティ](../common-properties.md)  
  
-   [パーティション処理変換先のカスタム プロパティ](partition-processing-destination-custom-properties.md)  
  
 データ フロー コンポーネントのプロパティの設定方法については、「 [データ フロー コンポーネントのプロパティを設定する](set-the-properties-of-a-data-flow-component.md)」を参照してください。  
  
  
