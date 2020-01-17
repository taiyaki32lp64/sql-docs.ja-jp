---
title: メタデータ ([ブラウザー] タブ、キューブ デザイナー) (Analysis Services - 多次元データ) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.browsecube.metadatapane.f1
ms.assetid: a1ace545-488d-4645-8330-56408a5e8abd
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3e4aade575cdcb8260865d4a1fe9ab6f4b7941fe
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66077851"
---
# <a name="metadata-browser-tab-cube-designer-analysis-services---multidimensional-data"></a>[メタデータ] (キューブ デザイナーの [ブラウザー] タブ) (Analysis Services - 多次元データ)
  キューブ構造の参照、関連するメジャーの確認、ディメンションの閲覧と作成には、キューブ デザイナーの **[ブラウザー]** タブの **[メタデータ]** ペインを使用します。 階層のドリル ダウン、使用できるメジャーと KPI の一覧表示、オブジェクトの完全修飾名のコピーなどを実行できます。  
  
 **[メタデータ]** ペインからクエリ作成領域にオブジェクトや階層をドラッグして新しいクエリを作成したり、データをエクスポートして Excel で参照したりすることもできます。  
  
## <a name="options"></a>および  
 **メタデータ**  
 現在のビューで使用可能なメタデータを表示します。 キューブ アイコンをクリックしてビュー (現在選択されているパースペクティブまたはキューブ) を変更した後、 **[キューブの選択]** ダイアログ ボックスを使用して新しいキューブまたはパースペクティブを選択できます。 **[メジャー グループ]** をクリックして、ドロップダウン リストから新しいメジャー グループを選択し、 **[メタデータ]** ペインで利用可能なオブジェクトをフィルター選択することもできます。  
  
 選択した項目を、 [!INCLUDE[msCoName](../includes/msconame-md.md)] [レポート] **ペインの** Office 11.0 PivotTable コントロールのフィルター、データ、行、または列の領域にドラッグして、選択した項目のデータを表示します。  
  
 **関数**  
 **[ブラウザー]** でクエリまたはデータ ビューの作成に使用できるすべての関数、演算子、および定数を一覧表示します。 関数を使用するには、目的の関数を探して、クエリ領域にドラッグします。 対応する構文の定義がテキストに追加されます。  
  
> [!WARNING]  
>  グラフィカル デザイン ビューで作業している場合、 **[関数]** の一覧は利用できません。  
  
 テーブル モデルで作業している場合は、関数の一覧に MDX 関数と DAX 関数の両方が含まれます。 そうでない場合は、一覧に MDX だけが含まれます。 多次元モデルは、オブジェクトの定義の一部として DAX 式を組み込むことはできますが、直接 DAX 関数を使用することはできません。  
  
 ヒント:DAX 関数が含まれているフォルダーは、すべて大文字で表示されます。 その他すべてのフォルダーには、MDX 関数が格納されています。 たとえば、これには統計関数の 2 つのフォルダーがあります。**統計**関連する DAX 関数が含まれています。  
  
## <a name="context-menu"></a>コンテキスト メニュー  
 **[メタデータ]** ペインで表示される要素を右クリックして表示されるショートカット メニューでは、次のオプションを使用できます。  
  
|オプション|説明|  
|------------|-----------------|  
|**クエリに追加します。**|選択したオブジェクトをクエリ作成領域の下のペインに追加します。|  
|**フィルターに追加します。**|選択したディメンション、属性、階層、またはレベルを **[ブラウザー]** のフィルター領域に追加します。<br /><br /> 注:レベルが選択されているまたはディメンション、属性、階層場合にのみ、このオプションは有効です。|  
|**コピー**|選択した項目をクリップボードに追加します。<br /><br /> 注:このオプションは、オブジェクトの完全修飾名をコピーします。|  
  
## <a name="see-also"></a>参照  
 [ツールバー&#40;ブラウザー タブ、キューブ デザイナー&#41; &#40;Analysis Services - 多次元データ&#41;](toolbar-browser-tab-cube-designer-analysis-services-multidimensional-data.md)   
 [Excel で分析&#40;ブラウザー タブ、キューブ デザイナー&#41; &#40;Analysis Services - 多次元データ&#41;](analyze-in-excel-browser-cube-designer-analysis-services-multidimensional-data.md)   
 [クエリおよびフィルター&#40;ブラウザー タブ、キューブ デザイナー&#41; &#40;Analysis Services - 多次元データ&#41;](query-filter-browser-cube-designer-analysis-services-multidimensional-data.md)   
 [ブラウザー&#40;キューブ デザイナー&#41; &#40;Analysis Services - 多次元データ&#41;](browser-cube-designer-analysis-services-multidimensional-data.md)  
  
  
