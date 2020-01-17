---
title: ディメンションの属性の追加 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- adding attributes
- automatic attribute creation
- attributes [Analysis Services], creating
- attributes [Analysis Services], adding
- manual attribute creation [Analysis Services]
ms.assetid: 25826ba1-2b38-4b34-bd3a-7eba116093ae
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 70817c567b77af2bfdb7d715683ae6081fda442b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66077428"
---
# <a name="add-an--attribute-to-a-dimension"></a>ディメンションへの属性の追加
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] では、自動または手動で、属性をディメンションに追加できます。  
  
 属性を自動的に作成するには、 **のディメンション デザイナーの** [ディメンション構造] [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]タブで、属性にマッピングする列を選択し、その列を **[データ ソース ビュー]** ペインから **[属性]** ペインにドラッグします。 これにより、列にマッピングされる属性が作成され、列の名前と同じ名前が属性に割り当てられます。 その名前を使用している属性が既に存在する場合は、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] では序数サフィックスを追加して、最初の重複する名前を "1" から始めます。  
  
 属性を手動で作成するには、 **[属性]** ペインをグリッド ビューに設定します。 グリッドの最後の行の名前の列で、 **\<新しい属性 >** 項目。 新しい属性の名前を入力します。 これにより、列にマッピングされない、すべてのプロパティが既定に設定されている属性が作成されます。 新しい属性の **KeyColumns** プロパティを構成して、 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] の **[プロパティ]** ウィンドウでマッピングを設定できます。  
  
 詳細については、「 [新しい属性の自動定義](attribute-properties-define-a-new-attribute-automatically.md)」、「 [新しい属性の手動による定義](../define-a-new-attribute-manually.md)」、「 [名前列への属性のバインド](attribute-properties-bind-an-attribute-to-a-name-column.md)」、「 [属性の KeyColumns プロパティの変更](attribute-properties-modify-the-keycolumn-property.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [ディメンションの属性のプロパティの参照](dimension-attribute-properties-reference.md)  
  
  
