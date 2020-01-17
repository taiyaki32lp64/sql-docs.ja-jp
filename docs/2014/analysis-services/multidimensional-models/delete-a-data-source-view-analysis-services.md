---
title: データ ソース ビュー (Analysis Services) の削除 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- deleting data source views
- data source views [Analysis Services], deleting
- removing data source views
ms.assetid: ae3f5ca0-ecbf-4b52-8386-eb457719d854
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9750751a23e4322a4a48ec0c1c227cf2df16f1c7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66075434"
---
# <a name="delete-a-data-source-view-analysis-services"></a>データ ソース ビューの削除 (Analysis Services)
  OLAP プロジェクトでデータ ソース ビュー (DSV) を使用していない場合、[!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] でプロジェクトから DSV を削除できます。  
  
 DSV は、削除すると完全に失われます。 削除した DSV を、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] のプロジェクトまたはデータベースに復元することはできません。  
  
 他のオブジェクトが依存している DSV は、オンライン モードの [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] によって開かれた [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] データベースから削除できません。 サーバーで実行中のデータベースに接続されているプロジェクトから DSV を削除するには、DSV 自体を削除する前に、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベース内でその DSV に依存しているすべてのオブジェクトを削除する必要があります。  
  
 DSV を削除すると、依存している他の [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] オブジェクトが無効になります。そのため、DSV を削除する前に、DSV を削除すると無効になるオブジェクトの一覧が表示されます。 使用する予定のあるオブジェクトが含まれていないか、この一覧で確認します。  
  
 ![ダイアログ ボックスのオブジェクトを削除する](../media/ssas-olapdsv-deleteobjects.gif "オブジェクトの削除 ダイアログ ボックス")  
  
## <a name="see-also"></a>参照  
 [多次元モデルのデータ ソース ビュー](data-source-views-in-multidimensional-models.md)   
 [データ ソース ビューのプロパティの変更 &#40;Analysis Services&#41;](change-properties-in-a-data-source-view-analysis-services.md)  
  
  
