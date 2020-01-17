---
title: 計算ツール (キューブ デザイナーの [Kpi] タブ) (Analysis Services - 多次元データ) |Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.kpisview.calculationtoolspane.f1
ms.assetid: c030c725-7763-4c23-9988-4b274a88fc31
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ecd16965c81ccb091d70320bd91c56112d3c15a0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66088269"
---
# <a name="calculation-tools-kpis-tab-cube-designer-analysis-services---multidimensional-data"></a>[計算ツール] (キューブ デザイナーの [KPI] タブ) (Analysis Services - 多次元データ)
  キューブ デザイナーの **[KPI]** タブの **[計算ツール]** ペインを使用すると、主要業績評価指標 (KPI) で使用可能なメタデータ、関数、およびテンプレートを検索できます。  
  
> [!NOTE]  
>  このペインはフォーム ビューでのみ表示されます。  
  
## <a name="options"></a>および  
 **メタデータ**  
 選択したキューブのメタデータを表示します。  
  
 選択した要素を **KPI フォーム エディター** ペインにドラッグし、ペイン内の選択した場所にその要素の多次元式 (MDX) の構文を含めます。  
  
 **関数**  
 式および条件で使用可能な関数を表示します。  
  
 選択した要素を **KPI フォーム エディター** ペインにドラッグし、ペイン内の選択した場所にその要素の MDX の構文を含めます。  
  
> [!NOTE]  
>  プロジェクト モードでは、 **[計算ツール]** ダイアログ ボックスは [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]に付属している MDXFunctions.xml という名前の XML ファイルから、このオプションについての情報を読み取ります。 オンライン モードでは、このオプションについての情報は、このインスタンスの MDSCHEMA_FUNCTIONS スキーマ行セットから取得します。  
  
 **[テンプレート]**  
 KPI で使用可能な事前定義テンプレートを表示します。  
  
 選択した要素を **KPI フォーム エディター** ペインにドラッグし、ペイン内の選択した場所にその要素の MDX の構文を含めます。  
  
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
 選択されたテンプレートに基づいて、新しく計算されるメンバー、名前付きセット、またはスクリプト コマンドをキューブ スクリプトに追加し、 **KPI フォーム エディター** をフォーム ビューで表示します。  
  
> [!NOTE]  
>  このオプションは、 **[メタデータ]** が選択されている場合にのみ表示されます。  
  
## <a name="see-also"></a>関連項目  
 [キューブ デザイナー &#40;Analysis Services - 多次元データ&#41;](cube-designer-analysis-services-multidimensional-data.md)   
 [Kpi&#40;キューブ デザイナー&#41; &#40;Analysis Services - 多次元データ&#41;](kpis-cube-designer-analysis-services-multidimensional-data.md)   
 [ツールバー &#40;[Kpi] タブ、キューブ デザイナー&#41; &#40;Analysis Services - 多次元データ&#41;](toolbar-kpis-tab-cube-designer-analysis-services-multidimensional-data.md)   
 [KPI オーガナイザー &#40;[Kpi] タブ、キューブ デザイナー&#41; &#40;Analysis Services - 多次元データ&#41;](kpi-organizer-kpis-tab-cube-designer-analysis-services-multidimensional-data.md)   
 [KPI フォーム エディター &#40;[Kpi] タブ、キューブ デザイナー&#41; &#40;Analysis Services - 多次元データ&#41;](kpi-form-editor-kpis-tab-cube-designer-analysis-services-multidimensional-data.md)   
 [KPI ブラウザー &#40;[Kpi] タブ、キューブ デザイナー&#41; &#40;Analysis Services - 多次元データ&#41;](kpi-browser-kpis-tab-cube-designer-analysis-services-multidimensional-data.md)  
  
  
