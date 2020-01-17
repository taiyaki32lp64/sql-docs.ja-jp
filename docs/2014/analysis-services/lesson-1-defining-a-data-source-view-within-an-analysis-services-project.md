---
title: レッスン 1:Services プロジェクト内での分析データ ソース ビューの定義 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 7d3ffabd-78ae-4204-8323-29949d030c16
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 08d4d24f9049c2fd68e827664ecb07393262d8bf
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66079209"
---
# <a name="lesson-1-defining-a-data-source-view-within-an-analysis-services-project"></a>レッスン 1:Analysis Services プロジェクト内でのデータ ソース ビューの定義
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] でビジネス インテリジェンス アプリケーションを設計するには、まず、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] で [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]プロジェクトを作成します。 このプロジェクト内で、ソリューションに必要なすべての要素を定義します。最初に定義するのはデータ ソース ビューです。  
  
 このレッスンの内容は次のとおりです。  
  
 [Analysis Services プロジェクトの作成](lesson-1-1-creating-an-analysis-services-project.md)  
 この実習では、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 多次元モデル テンプレートに基づいて [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial プロジェクトを作成します。  
  
 [データ ソースの定義](lesson-1-2-defining-a-data-source.md)  
 この実習では、この後のレッスンで定義する **ディメンションおよびキューブのデータ ソースとして、** AdventureWorksDW2012 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] データベースを指定します。  
  
 [データ ソース ビューの定義](lesson-1-3-defining-a-data-source-view.md)  
 この実習では、 **AdventureWorksDW2012** データベースの選択したテーブルに格納されているメタデータを 1 つにまとめた統合ビューを定義します。  
  
 [既定のテーブル名の変更](lesson-1-4-modifying-default-table-names.md)  
 この実習では、この後で定義する [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] オブジェクトを識別しやすくするために、データ ソース ビューのテーブル名をわかりやすい名前に変更します。  
  
 結果を、このレッスン用にビルドされたサンプル プロジェクト ファイルと比較してください。 このチュートリアルのサンプル プロジェクトのダウンロードの詳細については、CodePlex の製品サンプル ページで「[SSAS Multidimensional Model Projects for SQL Server 2012](https://go.microsoft.com/fwlink/p/?LinkID=221866)」を参照してください。  
  
## <a name="next-lesson"></a>次のレッスン  
 [レッスン 2:定義と、キューブの配置](lesson-2-defining-and-deploying-a-cube.md)  
  
## <a name="see-also"></a>参照  
 [Analysis Services プロジェクトの作成 (SSDT)](multidimensional-models/create-an-analysis-services-project-ssdt.md)   
 [サポートされるデータ ソース&#40;SSAS 多次元&#41;](multidimensional-models/supported-data-sources-ssas-multidimensional.md)   
 [多次元モデルのデータ ソース ビュー](multidimensional-models/data-source-views-in-multidimensional-models.md)   
 [Analysis Services のチュートリアル シナリオ](analysis-services-tutorial-scenario.md)   
 [多次元モデリング (Adventure Works チュートリアル)](multidimensional-modeling-adventure-works-tutorial.md)  
  
  
