---
title: データ ソース ビュー ([キューブ構造] タブ、キューブ デザイナー) (Analysis Services - 多次元データ) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.cubebuilder.datasourcepane.f1
ms.assetid: 1e39c910-5c10-4624-be27-ca02a461b46b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b5c5f1389e0761ba0665e37e842b23b58c70cfe2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66082527"
---
# <a name="data-source-view-cube-structure-tab-cube-designer-analysis-services---multidimensional-data"></a>[データ ソース ビュー] (キューブ デザイナーの [キューブ構造] タブ) (Analysis Services - 多次元データ)
  **[データ ソース ビュー]** ペインを使用すると、選択されたキューブに関連付けられているデータ ソース ビューのテーブルおよび列を表示できます。 このペインを使用すると、 **[データ ソース ビュー]** ペインから **[メジャー]** ペインに列をドラッグすることで、メジャー グループおよびメジャーを作成できます。  
  
## <a name="options"></a>および  
 **データ ソース ビュー**  
 選択されたキューブに関連付けられているデータ ソース ビューを表示します。  
  
 **(表示領域の移動)**  
 ペインの右下隅のスクロール バーの間をクリックすると、表示する **[データ ソース ビュー]** ペインの領域を選択します。  
  
## <a name="diagram-context-menu"></a>ダイアグラムのショートカット メニュー  
 **[データ ソース ビュー]** ペインのダイアグラムの背景を右クリックすると表示されるショートカット メニューでは、次のオプションを使用できます。  
  
 **テーブルを表示します。**  
 **[テーブルの表示]** ダイアログ ボックスを表示します。 **[テーブルの表示]** ダイアログ ボックスの詳細については、「[[テーブルの表示] ダイアログ ボックス (Analysis Services - 多次元データ)](show-table-dialog-box-analysis-services-multidimensional-data.md)」を参照してください。  
  
 **すべてのテーブルを表示します。**  
 キューブに関連付けられているデータ ソース ビューに含まれるすべてのテーブルをペインに表示します。  
  
 **使用されるテーブルのみを表示します。**  
 関連付けられているデータ ソース ビューのキューブによって使用されているテーブルだけをペインに表示します。  
  
 **フレンドリ名を表示します。**  
 選択すると、オブジェクトの表示名がペインに表示されます。  
  
 **[すべて選択]**  
 ペイン内のすべてのオブジェクトが選択されます。  
  
 **[テーブルの検索]**  
 **[テーブルの検索]** ダイアログ ボックスを表示します。 **[テーブルの検索]** ダイアログ ボックスの詳細については、「[[テーブルの検索] ダイアログ ボックス (Analysis Services - 多次元データ)](find-table-dialog-box-analysis-services-multidimensional-data.md)」を参照してください。  
  
 **テーブルを並べ替え**  
 **[斜線レイアウトに切り替え]** または **[四角形レイアウトに切り替え]** を選択して指定したレイアウトに従って、ペイン内のオブジェクトを並べ替えます。  
  
 **斜線レイアウトに切り替え**  
 オブジェクトを斜線パターンで整列できます。  
  
> [!NOTE]  
>  このオプションは、 **[四角形レイアウトに切り替え]** が選択されている場合にのみ表示されます。  
  
 **四角形レイアウトに切り替え**  
 オブジェクトを四角形パターンで整列できます。  
  
> [!NOTE]  
>  このオプションは、 **[斜線レイアウトに切り替え]** が選択されている場合にのみ表示されます。  
  
 **データ ソース ビューを編集します。**  
 オブジェクトに関連付けられているデータ ソース ビューのデータ ソース ビュー デザイナーを表示します。 データ ソース ビュー デザイナーの詳細については、「[データ ソース ビュー デザイナー (Analysis Services - 多次元データ)](data-source-view-designer-analysis-services-multidimensional-data.md)」を参照してください。  
  
 **データ ソース ビューを表示します。**  
 **[データ ソース ビュー]** ペインの表示モードとして、次のオプションのいずれかのオプションを選択します。  
  
-   ダイアグラム  
  
     現在のキューブに関連付けられているテーブルおよび列のダイアグラムを表示します。  
  
-   ツリー  
  
     現在のキューブに関連付けられているテーブルおよび列を含むツリー ビューを表示します。  
  
 **ダイアグラムのコピー元**  
 **[データ ソース ビュー]** ペインに表示する、キューブに関連付けられたデータ ソース ビューに含まれているいずれかのダイアグラムを選択します。  
  
 **[ズーム]**  
 利用可能なズーム オプションを選択します。  
  
 **Properties**  
 キューブに関連付けられたデータ ソース ビューのために、 **の** [プロパティ] [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] ウィンドウを表示します。  
  
## <a name="table-context-menu"></a>テーブルのショートカット メニュー  
 **[データ ソース ビュー]** ペインのテーブルまたはビューの名前を右クリックすると表示されるショートカット メニューでは、次のオプションを使用できます。  
  
 **関連テーブルを表示します。**  
 データ ソース ビューで選択されたテーブルに関連するテーブルをペインに表示します。  
  
 **テーブルの非表示します。**  
 ペインからテーブルを削除します。  
  
 **データの探索**  
 選択されているテーブルの **[データの探索]** ダイアログ ボックスを表示します。  
  
 **データ ソース ビューを編集します。**  
 選択したテーブルを含むデータ ソース ビューのデータ ソース ビュー デザイナーを表示します。 データ ソース ビュー デザイナーの詳細については、「[データ ソース ビュー デザイナー (Analysis Services - 多次元データ)](data-source-view-designer-analysis-services-multidimensional-data.md)」を参照してください。  
  
 **テーブルから新しいメジャー グループ**  
 選択されているテーブルに基づいて、 **[メジャー]** ペインに新しいメジャー グループを定義します。  
  
> [!NOTE]  
>  このオプションは、テーブルがまだ **[メジャー]** ペインのメジャー グループによって参照されていない場合にだけ有効になります。  
  
 **Properties**  
 **で選択されているテーブルの** [プロパティ] [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] ウィンドウを表示します。  
  
## <a name="column-context-menu"></a>列のショートカット メニュー  
 **[データ ソース ビュー]** ペインのテーブルまたはビューの列の名前を右クリックすると表示されるショートカット メニューでは、次のオプションを使用できます。  
  
 **列から新しいメジャー**  
 選択されている列に基づいて、 **[メジャー]** ペインに新しいメジャーを定義します。  
  
 **データの探索**  
 選択した列が含まれるテーブルの **[データの探索]** ダイアログ ボックスが表示されます。  
  
 **データ ソース ビューを編集します。**  
 選択した列を含むデータ ソース ビューのデータ ソース ビュー デザイナーを表示します。 データ ソース ビュー デザイナーの詳細については、「[データ ソース ビュー デザイナー (Analysis Services - 多次元データ)](data-source-view-designer-analysis-services-multidimensional-data.md)」を参照してください。  
  
 **Properties**  
 **で選択されている列の** [プロパティ] [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] ウィンドウを表示します。  
  
## <a name="relationship-context-menu"></a>リレーションシップのショートカット メニュー  
 **[データ ソース ビュー]** ペインのリレーションシップを右クリックすると表示されるショートカット メニューでは、次のオプションを使用できます。  
  
 **データ ソース ビューを編集します。**  
 選択されているリレーションシップを含むデータ ソース ビューのデータ ソース ビュー デザイナーを表示します。 データ ソース ビュー デザイナーの詳細については、「[データ ソース ビュー デザイナー (Analysis Services - 多次元データ)](data-source-view-designer-analysis-services-multidimensional-data.md)」を参照してください。  
  
 **Properties**  
 選択したリレーションシップの **[プロパティ]** ウィンドウを [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] に表示します。  
  
## <a name="see-also"></a>関連項目  
 [ツールバー&#40;キューブ構造 タブ、キューブ デザイナー&#41; &#40;Analysis Services - 多次元データ&#41;](toolbar-cube-structure-cube-designer-analysis-services-multidimensional-data.md)   
 [メジャー&#40;キューブ構造 タブ、キューブ デザイナー&#41; &#40;Analysis Services - 多次元データ&#41;](measures-cube-structure-cube-designer-analysis-services-multidimensional-data.md)   
 [ディメンション&#40;キューブ構造 タブ、キューブ デザイナー&#41; &#40;Analysis Services - 多次元データ&#41;](dimensions-cube-structure-cube-designer-analysis-services-multidimensional-data.md)   
 [キューブ構造&#40;キューブ デザイナー&#41; &#40;Analysis Services - 多次元データ&#41;](cube-structure-cube-designer-analysis-services-multidimensional-data.md)  
  
  
