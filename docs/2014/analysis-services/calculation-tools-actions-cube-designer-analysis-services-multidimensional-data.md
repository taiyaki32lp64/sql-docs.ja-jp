---
title: 計算ツール (キューブ デザイナーの [操作] タブ) (Analysis Services - 多次元データ) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.actionsview.calculationtoolspane.f1
ms.assetid: a3370370-43cd-4cc2-bb9f-c0d988b96f05
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 087f5f5e3383fd66244541fea35160946936bc1c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66088337"
---
# <a name="calculation-tools-actions-tab-cube-designer-analysis-services---multidimensional-data"></a>[計算ツール] (キューブ デザイナーの [アクション] タブ) (Analysis Services - 多次元データ)
  キューブ デザイナーの **[アクション]** タブの **[計算ツール]** ペインを使用すると、アクション、ドリルスルー アクション、およびレポート アクションで使用可能なメタデータ、関数、およびテンプレートを調査できます。  
  
## <a name="options"></a>および  
 **メタデータ**  
 選択したキューブのメタデータを表示します。  
  
 選択した要素を **アクション フォーム エディター**ペイン、 **ドリルスルー アクション フォーム エディター**ペイン、または **レポート アクション フォーム エディター** ペインにドラッグし、ペイン内の選択した場所にその要素の多次元式 (MDX) 構文を含めます。  
  
 **関数**  
 式および条件で使用可能な関数を表示します。  
  
 選択した要素を **アクション フォーム エディター**ペイン、 **ドリルスルー アクション フォーム エディター**ペイン、または **レポート アクション フォーム エディター** ペインにドラッグし、ペイン内の選択した場所にその要素の MDX 構文を含めます。  
  
> [!NOTE]  
>  プロジェクト モードでは、 **[計算ツール]** ダイアログ ボックスは [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]に付属している MDXFunctions.xml という名前の XML ファイルから、このオプションについての情報を読み取ります。 オンライン モードでは、このオプションについての情報は、このインスタンスの MDSCHEMA_FUNCTIONS スキーマ行セットから取得します。  
  
 **[テンプレート]**  
 アクションで使用可能な定義済みテンプレートを表示します。  
  
 選択した要素を **アクション フォーム エディター**ペイン、 **ドリルスルー アクション フォーム エディター**ペイン、または **レポート アクション フォーム エディター** ペインにドラッグし、ペイン内の選択した場所にその要素の MDX 構文を含めます。  
  
## <a name="context-menu"></a>コンテキスト メニュー  
 **[計算ツール]** ペインで要素を右クリックして表示されるコンテキスト メニューでは、次のオプションを使用できます。  
  
|オプション|定義|  
|------------|----------------|  
|**コピー**|**[メタデータ]** または **[関数]** で選択した要素をクリップボードにコピーします。<br /><br /> 場合に、このオプションが表示されないことに注意してください。**テンプレート**が選択されています。 なお、このオプションが選択されているメンバーがコピーできない場合などを無効になっている、**セット**フォルダーに表示されるディメンションの**メタデータ**またはに表示される関数の関数グループフォルダー**関数**します。|  
|**メンバーのフィルター選択します。**|**[メンバーのフィルター選択]** ダイアログ ボックスを表示し、 **[メタデータ]** で選択した要素について表示されたメンバーをフィルター処理します。 **[メンバーのフィルター選択]** ダイアログ ボックスの詳細については、「[[メンバーのフィルター選択] ダイアログ ボックス &#40;Analysis Services - 多次元データ&#41;](filter-members-dialog-box-analysis-services-multidimensional-data.md)」を参照してください。<br /><br /> 場合にのみ、このオプションが表示されることに注意してください。**メタデータ**が選択されています。 なお、属性のレベルを選択した場合にのみこのオプションが有効になっている**メタデータ**します。|  
|**テンプレートを追加します。**|選択したテンプレートに基づいて新しいアクション、ドリルスルー アクション、またはレポート アクションをキューブに追加し、それぞれ、 **アクション フォーム エディター**、 **ドリルスルー アクション フォーム エディター**、または **レポート アクション フォーム エディター**を表示します。<br /><br /> 注:このオプションは、 **[メタデータ]** が選択されている場合にのみ表示されます。|  
  
## <a name="see-also"></a>参照  
 [MDX スクリプティングの基礎 &#40;Analysis Services&#41;](multidimensional-models/mdx/mdx-scripting-fundamentals-analysis-services.md)   
 [アクション&#40;キューブ デザイナー&#41; &#40;Analysis Services - 多次元データ&#41;](actions-cube-designer-analysis-services-multidimensional-data.md)   
 [ツールバー&#40;アクションタブ、キューブ デザイナー&#41; &#40;Analysis Services - 多次元データ&#41;](toolbar-actions-tab-cube-designer-analysis-services-multidimensional-data.md)   
 [アクション オーガナイザー&#40;アクション タブ、キューブ デザイナー&#41; &#40;Analysis Services - 多次元データ&#41;](action-organizer-cube-designer-analysis-services-multidimensional-data.md)   
 [アクション フォーム エディター&#40;アクション タブ、キューブ デザイナー&#41; &#40;Analysis Services - 多次元データ&#41;](action-form-editor-cube-designer-analysis-services-multidimensional-data.md)   
 [ドリルスルー アクション フォーム エディター&#40;アクション タブ、キューブ デザイナー&#41; &#40;Analysis Services - 多次元データ&#41;](drillthrough-action-form-editor-cube-designer-analysis-services-multidimensional-data.md)   
 [レポート アクション フォーム エディター&#40;アクション タブ、キューブ デザイナー&#41; &#40;Analysis Services - 多次元データ&#41;](report-action-form-editor-cube-designer-analysis-services-multidimensional-data.md)  
  
  
