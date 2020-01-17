---
title: 翻訳の詳細 ([翻訳] タブ、ディメンション デザイナー) (Analysis Services - 多次元データ) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dimensiondesigner.translations.translationpane.tranlationdetails.f1
ms.assetid: 0aa61df3-f2b0-4703-a63b-124da672dcc3
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9f8debb50a798ba46457942e0e79a9d45ab392c1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66065852"
---
# <a name="translation-details-translations-tab-dimension-designer-analysis-services---multidimensional-data"></a>[翻訳の詳細] ([翻訳] タブ、ディメンション デザイナー) (Analysis Services - 多次元データ)
  ディメンション デザイナーの **[翻訳]** タブの **[翻訳の詳細]** ペインを使用すると、現在選択しているディメンションの翻訳を定義および管理できます。  
  
 **翻訳の詳細ウィンドウを表示するには**  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]で [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] プロジェクトを開き、目的のディメンションを開きます。  
  
2.  **[翻訳]** タブをクリックします。  
  
## <a name="options"></a>および  
 **[既定の言語]**  
 既定の言語におけるディメンション オブジェクトの名前を設定します。  
  
 **オブジェクトの種類**  
 翻訳されるプロパティを表示します。 値が指定されているオブジェクトとプロパティのみが翻訳できます。 次のプロパティが翻訳されます。  
  
-   [ディメンション]  
  
     `Caption` プロパティと `AttributeAllMember` プロパティ  
  
-   属性  
  
     `Caption`、`AttributeHierarchyDisplayFolder`、および `NamingTemplate` プロパティ  
  
    > [!NOTE]  
    >  `NamingTemplate` プロパティは、親属性でのみ使用できます。  
  
-   Hieararchy  
  
     `Caption` プロパティと `AllMemberName` プロパティ  
  
-   Level  
  
     `Caption` プロパティ  
  
 **\<言語 >**  
 選択した言語でディメンション オブジェクトのプロパティ値を入力、または選択します。 参照ボタン ( **[...]** ) をクリックすると、編集中のプロパティに応じて次のダイアログ ボックスが表示されます。  
  
-   `NamingTemplate` プロパティ  
  
     [&#91;レベル名前付けテンプレート&#93; ダイアログ ボックス &#40;Analysis Services - 多次元データ&#41;](level-naming-template-dialog-box-analysis-services-multidimensional-data.md) を表示します。  
  
-   `Caption` プロパティ (属性の場合)  
  
     [&#91;属性データの翻訳&#93; ダイアログ ボックス &#40;Analysis Services - 多次元データ&#41;](attribute-data-translation-dialog-box-analysis-services-multidimensional-data.md) を表示します。  
  
## <a name="shortcut-menu"></a>ショートカット メニュー  
 **[翻訳の詳細]** ペインで翻訳を右クリックして表示されるショートカット メニューでは、次のオプションを使用できます。  
  
 **新しい翻訳**  
 **[言語の選択]** ダイアログ ボックスを表示して、新しい翻訳を作成します。 翻訳は、 **[翻訳の詳細]** グリッドに新しい列として表示されます。  
  
 **翻訳を削除します。**  
 選択された翻訳を削除します。  
  
> [!NOTE]  
>  このオプションは、翻訳を削除するためにセルを右クリックした場合にのみ有効になります。  
  
 **新しいキャプション列**  
 **[翻訳の詳細]** グリッドで属性を変更するときに選択すると、 **[属性データの翻訳]** ダイアログ ボックスが表示され、新しいキャプション列を定義できます。 このオプションを有効にするには、属性の翻訳列のセルが **翻訳の詳細** グリッドで選択されている必要があります。  
  
> [!NOTE]  
>  このオプションは、属性の翻訳列を削除するためにセルを右クリックした場合にのみ有効になります。  
  
 **キャプション列を編集します。**  
 **[翻訳の詳細]** グリッドで属性を変更するときに選択すると、 **[属性データの翻訳]** ダイアログ ボックスが表示され、既存のキャプション列を変更できます。  
  
> [!NOTE]  
>  このオプションは、属性のキャプション列を含む翻訳列のセルが **[翻訳の詳細]** グリッドで選択されている場合のみ有効です。  
  
 **キャプション列を削除します。**  
 選択すると、 **[翻訳の詳細]** グリッドで選択している属性のキャプション列が削除されます。  
  
> [!NOTE]  
>  このオプションは、属性のキャプション列を含む翻訳列のセルを右クリックした場合にのみ有効になります。  
  
 **すべての属性を表示します。**  
 属性階層が無効になっている属性を含め、選択したディメンションに定義されている全属性が表示されます。  
  
## <a name="see-also"></a>参照  
 [翻訳&#40;ディメンション デザイナー&#41; &#40;Analysis Services - 多次元データ&#41;](translations-dimension-designer-analysis-services-multidimensional-data.md)  
  
  
