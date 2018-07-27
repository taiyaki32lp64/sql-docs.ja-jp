---
title: 処理およびストレージの場所 (パーティション ウィザード) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.asvs.partitionwizard.specifyprocessingandstorage.f1
ms.assetid: dda2dc57-923d-4db9-93a7-38e95770f3df
caps.latest.revision: 24
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: eae2e7c380b7b0de69047079edac87d273f07d52
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2018
ms.locfileid: "37286058"
---
# <a name="processing-and-storage-locations-partition-wizard"></a>[処理およびストレージの場所] (パーティション ウィザード)
  **[処理およびストレージの場所]** ページを使用すると、パーティションを所有するキューブの [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] インスタンスや、パーティションのデータを格納する [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] インスタンスを指定できます。 リモートの [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] インスタンス、または既定のストレージの場所とは異なるストレージの場所の、どちらかを指定することにより、リモート パーティションとしてパーティションを定義することができます。 リモート パーティションの詳細については、「 [リモート パーティション](multidimensional-models-olap-logical-cube-objects/partitions-remote-partitions.md)」をご覧ください。  
  
## <a name="processing-location-options"></a>[処理場所] オプション  
 **現在のサーバー インスタンス**  
 現在の [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] インスタンスがパーティションを処理します。  
  
 **リモートの Analysis Services データ ソース**  
 リモート [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] インスタンスがこのパーティションを処理します。  
  
 ドロップダウン リストから、パーティションの処理を行うリモート [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] インスタンスを表すデータ ソースを選択します。  
  
> [!NOTE]  
>  `Initial Catalog` 接続文字列プロパティで選択したデータ ソースに有効な [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] データベースが設定されていない場合や、`Initial Catalog` 接続文字列プロパティに指定されたデータベースがリモート パーティションをサポートしていない (つまり、指定されたデータベースの `MasterDatasourceID` プロパティが有効な値に設定されていない) 場合は、エラーが発生します。  
  
 **[新規作成]**  
 パーティションを処理するリモート [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] インスタンスを表す、新しいデータ ソースを作成します。  
  
## <a name="storage-location-options"></a>[ストレージの場所] オプション  
 **既定のサーバーの場所**  
 現在の [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] インスタンスのデータ フォルダーを、パーティションの集計データとインデックス付きデータの格納場所にします。  
  
 **指定されたフォルダー**  
 パーティションの集計データとインデックス付きデータの格納場所を指定します。  
  
 **[...]**  
 **[指定のフォルダー]** のフォルダーを選択する、 **[リモート フォルダーの参照]** ダイアログ ボックスを表示します。  
  
## <a name="see-also"></a>参照  
 [パーティション ウィザードの F1 ヘルプ&#40;Analysis Services - 多次元データ&#41;](partition-wizard-f1-help-analysis-services-multidimensional-data.md)   
 [パーティション&#40;Analysis Services - 多次元データ&#41;](multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md)   
 [リモート フォルダ] ダイアログ ボックスの [参照] &#40;Analysis Services - 多次元データ&#41;](browse-for-remote-folder-dialog-box-analysis-services-multidimensional-data.md)  
  
  