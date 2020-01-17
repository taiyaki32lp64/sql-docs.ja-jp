---
title: 属性をディメンション デザイナーの表示 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- displaying attributes
- attributes [Analysis Services], viewing
- viewing attributes
ms.assetid: 855bef07-b72d-4ce3-bf02-de77abeee71a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ec86d5e7a910b7fb17397b1601fcc912b46c4d7f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66077129"
---
# <a name="view-attributes-in-dimension-designer"></a>ディメンション デザイナーでの属性の表示
  属性はディメンション オブジェクトで作成されます。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]のディメンション デザイナーを使用して、属性を表示したり構成したりできます。 ディメンション デザイナーの **[ディメンション構造]** タブの **[属性]** ペインには、ディメンションの属性が一覧表示されます。 このペインを使用して、属性の追加、削除、または構成を行います。 また、新しい階層でレベルとして使用する属性や、既存の階層にレベルとして追加する属性を選択できます。  
  
 ディメンションの属性を表示するには、そのディメンションのディメンション デザイナーを開きます。 ディメンション デザイナーの **[ディメンション構造]** タブの **[属性]**  ペインに、ディメンションの属性が表示されます。 ポイントして、リスト、ツリー、またはグリッド ビューを切り替えることができます**属性を表示**上、**ディメンション**のメニュー[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]次の表に示したコマンドのいずれかの をクリックします。  
  
|属性を表示|説明|  
|------------------------|-----------------|  
|**一覧**|属性を一覧形式で表示します。<br /><br /> 一覧から属性を削除したり、属性の名前を変更したり、属性の使用法を変更したりするには、その属性を右クリックします。<br /><br /> このビューは階層の構築に使用します。 属性の情報とメンバーのプロパティは表示されません。|  
|**ツリー**|ディメンションをツリーのトップレベル ノードとして、属性をツリー形式で表示します。 このビューは、メンバー プロパティの表示と作成に使用します。 また、階層の構築にも使用できます。 属性の属性リレーションシップを表示したり、新しい属性リレーションシップを作成したりするには、次の操作を実行して、その属性を展開します。<br /><br /> ディメンション、属性、またはメンバー プロパティをクリックして、 **[プロパティ]** ウィンドウにそのプロパティを表示します。<br /><br /> 属性またはメンバー プロパティを右クリックして、一覧から削除したり、名前を変更したり、その使用法を変更したりします。|  
|**グリッド**|属性をグリッド形式で表示します。 その属性のプロパティを表示するには、グリッドのいずれかの行をクリックします。  このビューは、属性の作成と構成に使用します。 グリッドには次の列が表示されます。<br /><br /> **名前**: の値が表示されます、**名前**プロパティ。 設定を変更するには、別の名前を入力します。<br /><br /> **使用状況**: これは通常、キー、親、または AccountType 属性であるかどうかを指定します。 別の設定を選択するには、この列の値をクリックします。<br /><br /> **型**: 属性のビジネス インテリジェンス カテゴリを指定します。 別の設定を選択するには、このセルをクリックします。<br /><br /> **キー列**: の OLE DB データ型を示しています、 **KeyColumn**属性のプロパティ。 この列は変更できません。<br /><br /> **列の名前を**: を示すかどうか、 **NameColumn**属性プロパティの設定は、設定と同じ列、 **KeyColumn**プロパティ。 この列は変更できません。|  
  
 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]では、属性の使用法に応じて、次の表のアイコンが属性に付いています。  
  
|アイコン|属性の使用法|  
|----------|---------------------|  
|![属性アイコン](../media/as-icon-attribute.gif "属性アイコン")|Regular または AccountType|  
|![キー属性アイコン](../media/as-icon-key-attribute.gif "キー属性アイコン")|キー|  
|![親属性アイコン](../media/as-icon-parent-attribute.gif "親属性アイコン")|Parent|  
  
## <a name="see-also"></a>参照  
 [ディメンションの属性のプロパティの参照](dimension-attribute-properties-reference.md)  
  
  
