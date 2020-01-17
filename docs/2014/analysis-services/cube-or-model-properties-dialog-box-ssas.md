---
title: キューブまたはモデルのプロパティ ダイアログ ボックス (SSAS) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.sqlserverstudio.cubeproperties.f1
ms.assetid: 97e367f9-f95a-4163-add1-c74fd22db249
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6857ece2f81ffdba839ec1a7f0ef420ec5d0acdf
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66086599"
---
# <a name="cube-or-model-properties-dialog-box-ssas"></a>[キューブのプロパティ] または [モデルのプロパティ] ダイアログ ボックス (SSAS)
  キューブまたはモデル データベースのプロパティを設定するには、 **の** [データベースのプロパティ] [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] ダイアログ ボックスを使用します。 ダイアログ ボックスを表示するには、 **オブジェクト エクスプローラー** でキューブまたはモデルを右クリックして、 **[プロパティ]** をクリックします。  
  
 このダイアログ ボックスには、次のプロパティに対応するタブが含まれています。  
  
-   [レポート アクション フォーム エディター&#40;アクション タブ、キューブ デザイナー&#41; &#40;Analysis Services - 多次元データ&#41;](report-action-form-editor-cube-designer-analysis-services-multidimensional-data.md)  
  
-   [キューブ、パーティション、およびディメンションの処理のエラー構成&#40;SSAS - 多次元&#41;](multidimensional-models/error-configuration-for-cube-partition-and-dimension-processing.md)  
  
-   [プロアクティブ キャッシュ&#40;プロパティ ダイアログ ボックスをパーティション分割&#41; &#40;SSMS&#41;](proactive-caching-partition-properties-dialog-box-ssms.md)  
  
## <a name="options"></a>および  
  
|項目|定義|  
|----------|----------------|  
|**名前**|キューブまたはモデルの名前が表示されます。|  
|**ID**|キューブまたはモデルの識別子が表示されます。|  
|**[説明]**|キューブまたはモデルの説明が表示されます。|  
|**[タイムスタンプの作成]**|キューブまたはモデルが作成された日時が表示されます。|  
|**[スキーマの最終更新]**|キューブまたはモデルのメタデータが最後に更新された日時が表示されます。|  
|**スクリプト キャッシュ処理モード**|キューブまたはモデルのスクリプト キャッシュに使用する処理モードを選択します。 このプロパティの値の詳細については、「<xref:Microsoft.AnalysisServices.Cube.ScriptCacheProcessingMode%2A>」を参照してください。|  
|**処理モード**|キューブまたはモデルに対して使用する処理モードを選択します。 このプロパティの値の詳細については、「<xref:Microsoft.AnalysisServices.Cube.ProcessingMode%2A>」を参照してください。|  
|**記憶域の場所**|キューブまたはモデルに関連付けられたメジャー グループおよびパーティションで使用する既定のストレージの場所を入力します。または、参照ボタン ( **[...]** ) をクリックして、 **[リモート フォルダーの参照]** ダイアログ ボックスを開いてフォルダーを選択します。 **[リモート フォルダーの参照]** ダイアログ ボックスの詳細については、「[[リモート フォルダーの参照] ダイアログ ボックス &#40;Analysis Services - 多次元データ&#41;](browse-for-remote-folder-dialog-box-analysis-services-multidimensional-data.md)」を参照してください。<br /><br /> このプロパティの値の詳細については、「<xref:Microsoft.AnalysisServices.Cube.StorageLocation%2A>」を参照してください。|  
|**State**|キューブまたはモデルの処理状態が表示されます。 このプロパティの値の詳細については、「<xref:Microsoft.AnalysisServices.ProcessableMajorObject.State%2A>」を参照してください。|  
|**LastProcessed**|キューブまたはモデルが最後に処理された日時が表示されます。|  
  
## <a name="see-also"></a>参照  
 [Analysis Services のデザイナーおよびダイアログ ボックス&#40;多次元データ&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [キューブ オブジェクト&#40;Analysis Services - 多次元データ&#41;](multidimensional-models-olap-logical-cube-objects/cube-objects-analysis-services-multidimensional-data.md)  
  
  
