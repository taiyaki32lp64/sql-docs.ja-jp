---
title: ディメンション処理変換先 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.dimensionprocessingdest.f1
helpviewer_keywords:
- Dimension Processing destination
- loading dimensions
- destinations [Integration Services], Dimension Processing
- dimensions [Analysis Services], processing
ms.assetid: 4c49bb95-7259-42f4-a785-bb6aaf5f8566
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 3f4aaaef619e0f8ae5810e70e9a6707c6213268d
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68890564"
---
# <a name="dimension-processing-destination"></a>ディメンション処理変換先
  ディメンション処理変換先は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] のディメンションを読み込んで処理します。 ディメンションの詳細については、「[ディメンション (Analysis Services - 多次元データ)](https://docs.microsoft.com/analysis-services/multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data)」を参照してください。  
  
 ディメンション処理変換先には、次の機能が含まれます。  
  
-   増分処理、完全処理、または更新処理を実行するオプション。  
  
-   エラー構成。ディメンション処理がエラーを無視するか、または指定した数のエラー発生後に停止するかどうかを指定します。  
  
-   ディメンション テーブルの列への入力列のマッピング  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] オブジェクトの処理に関する詳細については、「[処理オプションと設定 (Analysis Services)](https://docs.microsoft.com/analysis-services/multidimensional-models/processing-options-and-settings-analysis-services)」を参照してください。  
  
## <a name="configuration-of-the-dimension-processing-destination"></a>ディメンション処理変換先の構成  
 ディメンション処理変換先は、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 接続マネージャーを接続して、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクト、または、変換先が処理するディメンションを含む [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] のインスタンスに接続します。 詳細については、「 [Analysis Services 接続マネージャー](../connection-manager/analysis-services-connection-manager.md)」を参照してください。  
  
 この変換先は 1 つの入力をとります。 エラー出力はサポートされていません。  
  
 プロパティを設定するには [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 **[ディメンション処理変換先エディター]** ダイアログ ボックスで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [ディメンション処理変換先エディター ([接続マネージャー] ページ)](../dimension-processing-destination-editor-connection-manager-page.md)  
  
-   [ディメンション処理変換先エディター ([マッピング] ページ)](../dimension-processing-destination-editor-mappings-page.md)  
  
-   [ディメンション処理変換先エディター ([詳細設定] ページ)](../dimension-processing-destination-editor-advanced-page.md)  
  
 **[詳細エディター]** ダイアログ ボックスには、プログラムによって設定できるプロパティが反映されます。 **[詳細エディター]** ダイアログ ボックスまたはプログラムで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [共通プロパティ](../common-properties.md)  
  
 データ フロー コンポーネントのプロパティの設定方法については、「 [データ フロー コンポーネントのプロパティを設定する](set-the-properties-of-a-data-flow-component.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [データ フロー](data-flow.md)   
 [Integration Services の変換](transformations/integration-services-transformations.md)  
  
  
