---
title: 属性 (ディメンション構造 タブ、ディメンション デザイナー) (Analysis Services - 多次元データ) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql.asvs.dimensiondesigner.dbv.attributespane.f1
ms.assetid: 627eaa08-7638-4edd-bdfa-0d8175a7cde5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a9eab7de49abaf06446fbd03f7b80c381d102f20
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66064400"
---
# <a name="attributes-dimension-structure-tab-dimension-designer-analysis-services---multidimensional-data"></a>[属性] ([ディメンション構造] タブ、ディメンション デザイナー) (Analysis Services - 多次元データ)
  このペインを使用すると、選択したディメンションに関連付けられている属性を管理できます。 属性をこのペインから **[階層]** ペインにドラッグすると、階層およびレベルを作成できます。 詳細については、次を参照してください。[階層&#40;ディメンション構造 タブ、ディメンション デザイナー&#41; &#40;Analysis Services - 多次元データ&#41;](hierarchies-dimension-designer-analysis-services-multidimensional-data.md)します。  
  
 属性を作成するには、一覧モード、ツリー モード、またはビュー モードで、 **[データ ソース ビュー]** ペインから **[属性]** ペインに列をドラッグします。 属性を削除するには、ショートカット メニューの **[削除]** をクリックします。  
  
 **[属性] ペインを表示するには**  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]で [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] プロジェクトを開き、目的のディメンションを開きます。  
  
2.  選択されていない場合は、 **[ディメンション構造]** タブをクリックします。  
  
## <a name="options"></a>および  
 **Attributes**  
 選択したディメンションで使用できる属性が表示されます。 このオプションは、次のモードのときに表示されます。  
  
-   一覧モード  
  
     このモードを使用して、階層を作成したり、変更したりします。 属性を一覧モードで表示するには、ショートカット メニューの **[属性を表示]** をクリックした後、 **[一覧]** をクリックします。  
  
-   ツリー モード  
  
     このモードを使用して、階層を作成したり、変更したりします。 属性をツリー モードで表示するには、ショートカット メニューの **[属性を表示]** をクリックした後、 **[ツリー]** をクリックします。  
  
-   グリッド モード  
  
     このモードを使用して、ディメンションを手動で作成したり、属性のプロパティを変更したりします。 属性をグリッド モードで表示するには、ショートカット メニューの **[属性を表示]** をクリックした後、 **[グリッド]** をクリックします。  
  
## <a name="grid-mode-options"></a>グリッド モードのオプション  
 グリッド モードで属性を表示すると、次に示す列にアクセスできます。  
  
 **名前**  
 属性の名前を表示します。  
  
 **使用方法**  
 選択した属性の使用法を設定します。 下向きの矢印をクリックして、次のいずれかを選択します。  
  
|値|説明|  
|-----------|-----------------|  
|Regular|標準属性を表します。|  
|Key|ディメンションのキー属性を表します。 これは、ディメンションのリーフ メンバーに対応しています。 キー属性は 1 つのディメンションにつき 1 つのみ存在します。 変更するには、 **[プロパティ]** ペインで **[KeyColumns]** プロパティの横にある **[...]** ボタンをクリックします。|  
|Parent|親子リレーションシップにおける親属性を表します。 このリレーションシップの子属性は、常にキー属性である必要があります。|  
|[AccountType]|勘定科目の種類の属性を表します。 これは、メジャーの集計関数が "ByAccount" に設定されているときに、サーバーまたはエンジンにより使用されます。|  
  
 **型**  
 属性の型を設定します。 下向きの矢印をクリックして、選択します。  
  
 **キー列**  
 基となる列のデータ型が表示されます。 新しい属性を作成する場合は、下向きの矢印をクリックして選択します。  
  
 **[名前] 列**  
 基となる列の場所が表示されます。 新しい属性を作成する場合は、下向きの矢印をクリックし、 **[キーと同一]** または **[分割列]** を選択します。 **[分割列]** を選択した場合、 **[プロパティ]** ペインの **[NameColumn]** プロパティによって、属性に使用する名前を格納する列が設定されます。  
  
## <a name="see-also"></a>参照  
 [ディメンション構造&#40;ディメンション デザイナー&#41; &#40;Analysis Services - 多次元データ&#41;](dimension-structure-dimension-designer-analysis-services-multidimensional-data.md)   
 [階層&#40;ディメンション構造 タブ、ディメンション デザイナー&#41; &#40;Analysis Services - 多次元データ&#41;](hierarchies-dimension-designer-analysis-services-multidimensional-data.md)   
 [ツールバー&#40;ディメンション構造 タブ、ディメンション デザイナー&#41; &#40;Analysis Services - 多次元データ&#41;](toolbar-dimension-structure-designer-analysis-services-multidimensional-data.md)  
  
  
