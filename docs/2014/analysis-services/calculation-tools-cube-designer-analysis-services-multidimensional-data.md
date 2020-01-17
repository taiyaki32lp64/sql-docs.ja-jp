---
title: 計算ツール (計算 タブ、キューブ デザイナー) (Analysis Services - 多次元データ) |Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.calculationsview.calculationtoolspane.f1
ms.assetid: b1aa8a1a-6532-45d2-8f53-d3e211d7197a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ff0f13ec91ef1e8796ed5ebd5ccf3cc37ff2f354
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66088279"
---
# <a name="calculation-tools-calculations-tab-cube-designer-analysis-services---multidimensional-data"></a>計算ツール (キューブ デザイナーの [計算] タブ) (Analysis Services - 多次元データ)
  キューブ デザイナーの **[計算]** タブの **[計算ツール]** ペインを使用すると、計算に使用するメタデータ、関数、およびテンプレートを検索できます。  
  
## <a name="options"></a>および  
 **メタデータ**  
 選択したキューブのメタデータを表示します。  
  
 選択した要素をスクリプト エディター ペイン、計算されるメンバー フォーム エディター ペイン、または名前付きセット フォーム エディター ペインにドラッグし、ペイン内の選択した場所にその要素の多次元式 (MDX) 構文を含めます。  
  
 **関数**  
 式および条件で使用可能な関数を表示します。  
  
 選択した要素を **スクリプト エディター**ペイン、 **計算されるメンバー フォーム エディター**ペインまたは **名前付きセット フォーム エディター** ペインにドラッグし、ペイン内の選択した場所にその要素の多次元式 (MDX) 構文を含めます。  
  
> [!NOTE]  
>  プロジェクト モードでは、 **[計算ツール]** ダイアログ ボックスは [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]に付属している MDXFunctions.xml という名前の XML ファイルから、このオプションについての情報を読み取ります。 オンライン モードでは、このオプションについての情報は、このインスタンスの MDSCHEMA_FUNCTIONS スキーマ行セットから取得します。  
  
 **[テンプレート]**  
 計算されるメンバー、名前付きセット、およびスクリプト コマンドで使用可能な定義済みのテンプレートを表示します。  
  
 選択した要素を **スクリプト エディター**ペイン、 **計算されるメンバー フォーム エディター**ペインまたは **名前付きセット フォーム エディター** ペインにドラッグし、ペイン内の選択した場所にその要素の多次元式 (MDX) 構文を含めます。  
  
## <a name="context-menu"></a>コンテキスト メニュー  
 **[計算ツール]** ペインで要素を右クリックして表示されるショートカット メニューでは、次のオプションを使用できます。  
  
 **コピー**  
 **[メタデータ]** または **[関数]** で選択した要素をクリップボードにコピーします。  
  
> [!NOTE]  
>  **[テンプレート]** が選択されている場合は、このオプションは表示されません。  
  
> [!NOTE]  
>  このオプションは、 **[メタデータ]** に表示されるディメンションの **[セット]** フォルダーや、 **[関数]** に表示される関数の関数グループ フォルダーなど、選択されたメンバーがコピーできない場合には無効になります。  
  
 **メンバーのフィルター選択します。**  
 **[メンバーのフィルター選択]** ダイアログ ボックスを表示し、 **[メタデータ]** で選択した要素について表示されたメンバーをフィルター処理します。 **[メンバーのフィルター選択]** ダイアログ ボックスの詳細については、「[[メンバーのフィルター選択] ダイアログ ボックス &#40;Analysis Services - 多次元データ&#41;](filter-members-dialog-box-analysis-services-multidimensional-data.md)」を参照してください。  
  
> [!NOTE]  
>  このオプションは、 **[メタデータ]** が選択されている場合にのみ表示されます。  
  
> [!NOTE]  
>  このオプションは、属性のレベルが **[メタデータ]** で選択されている場合にのみ有効です。  
  
 **テンプレートを追加します。**  
 選択されたテンプレートに基づいて、新しく計算されるメンバー、名前付きセット、またはスクリプト コマンドをキューブ スクリプトに追加し、そのコマンドに適する **スクリプト エディター**、 **計算されるメンバー フォーム エディター**、または **名前付きセット フォーム エディター** を表示するか、 **スクリプト エディター** ペインの内容を、(スクリプト ビューの) キューブ スクリプト内のコマンドの場所へスクロールします。  
  
> [!NOTE]  
>  このオプションは、 **[メタデータ]** が選択されている場合にのみ表示されます。  
  
## <a name="see-also"></a>関連項目  
 [キューブ デザイナー &#40;Analysis Services - 多次元データ&#41;](cube-designer-analysis-services-multidimensional-data.md)   
 [ツールバー&#40;計算 タブ、キューブ デザイナー&#41; &#40;Analysis Services - 多次元データ&#41;](toolbar-calculations-tab-cube-designer-analysis-services-multidimensional-data.md)   
 [スクリプト オーガナイザー&#40;計算 タブ、キューブ デザイナー&#41; &#40;Analysis Services - 多次元データ&#41;](script-organizer-cube-designer-analysis-services-multidimensional-data.md)   
 [計算されるメンバー フォーム エディター&#40;計算 タブ、キューブ デザイナー&#41; &#40;Analysis Services - 多次元データ&#41;](calculated-member-form-editor-cube-designer-analysis-services-multidimensional-data.md)   
 [名前付きセット フォーム エディター&#40;計算 タブ、キューブ デザイナー&#41; &#40;Analysis Services - 多次元データ&#41;](named-set-form-editor-cube-designer-analysis-services-multidimensional-data.md)   
 [スクリプト エディター&#40;計算 タブ、キューブ デザイナー&#41; &#40;Analysis Services - 多次元データ&#41;](script-editor-calculations-cube-designer-analysis-services-multidimensional-data.md)   
 [計算&#40;キューブ デザイナー&#41; &#40;Analysis Services - 多次元データ&#41;](calculations-cube-designer-analysis-services-multidimensional-data.md)  
  
  
