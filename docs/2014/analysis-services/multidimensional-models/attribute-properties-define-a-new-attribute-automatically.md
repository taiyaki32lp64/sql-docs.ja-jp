---
title: 自動的に新しい属性の定義 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- automatic attribute creation
- attributes [Analysis Services], creating
ms.assetid: 208a050a-5e2f-470c-b645-8d835e123db7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5f77148e039e61c080d0eae4e4ab7cad06ef050d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66077304"
---
# <a name="define-a-new-attribute-automatically"></a>新しい属性の自動定義
  ディメンション デザイナーでは、ドラッグ アンド ドロップ編集を使用して、ディメンションに新しい属性を作成することができます。  
  
### <a name="to-create-a-new-attribute-automatically"></a>新しい属性を自動的に作成するには  
  
1.  ディメンション デザイナーで、属性を作成するディメンションを開きます。  
  
2.  **[ディメンション構造]** タブの **[データ ソース ビュー]** ペインで、属性をバインドするテーブルの列を選択し、その列を **[属性]** ペインにドラッグします。  
  
     [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] バインド先の列と同じ名前の新しい属性が作成されます。 同じ列を使用する複数の属性がある場合は、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] により、属性名に番号が追加されます。  
  
## <a name="see-also"></a>関連項目  
 [多次元モデル内のディメンション](dimensions-in-multidimensional-models.md)   
 [ディメンションの属性のプロパティの参照](dimension-attribute-properties-reference.md)  
  
  
