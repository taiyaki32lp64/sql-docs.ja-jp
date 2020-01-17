---
title: '[ブラウザー] (キューブ デザイナー) (Analysis Services - 多次元データ) |Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.browsecube.view.f1
ms.assetid: efb5ee1c-de50-4bfc-83ff-08a4f03c3ece
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4415fedb492eb32c2929c50999cad1542b41ca78
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66064619"
---
# <a name="browser-cube-designer-analysis-services---multidimensional-data"></a>[ブラウザー] (キューブ デザイナー) (Analysis Services - 多次元データ)
  キューブ内のディメンション、メジャー、および KPI を探索するには、キューブ デザイナーの **[ブラウザー]** タブを使用します。 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]では、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] キューブ ブラウザーが MDX クエリ デザイナーに統合され、MDX クエリの作成、キューブのフィルター処理とスライス、階層のドリル ダウンをグラフィカル ユーザー インターフェイスによって行うことができます。  
  
 **ブラウザー**タブには 2 つのモード。**デザイン モード**と**クエリ モード**します。 どちらのモードも、 **[メタデータ]** ペインのオブジェクトを使用してキューブを探索することができ、 **[メタデータ]** ペインからクエリ領域にメンバーをドラッグすることによって、必要なデータを取得するための MDX クエリを構築することができます。  
  
 **参照し、グラフィック デザイン モードを使用したクエリ**  
  
 次の図は、グラフィカル **デザイン モード** の **[ブラウザー]** インターフェイスです。  
  
 ![Analysis Services MDX クエリ デザイナー、デザイン ビュー](media/rsqd-dsawas-mdx-designmode.gif "Analysis Services MDX クエリ デザイナー、デザイン ビュー")  
  
 場合は、グラフィック デザイン モードで作業しているときに、**自動**(![クエリの自動実行](media/rsqdicon-autoexecute.gif "クエリの自動実行"))、ツールバーのトグル ボタンが選択されている、**ブラウザー**は、データ ペインにメタデータ オブジェクトをドロップするたびにクエリを実行します。 使用してクエリを実行することができますも手動で、**クエリの実行**(![クエリを実行](media/rsqdicon-run.gif "クエリを実行"))、ツールバーのボタンをクリックします。  
  
 グラフィカル クエリ デザイナーを **クエリ** モードに変更して、MDX ステートメントのテキストを編集するには、ツール バーの **[デザイン モード]** ボタンをクリックします。  
  
 **参照および MDX テキスト モードを使用してクエリ**  
  
 MDX テスト デザイン モードでは、MDX を直接編集することができます。 クエリ デザイン領域にオブジェクトを追加できるように **[メタデータ]** ペインは引き続き利用できます。また、MDX の関数や演算子を **[関数]** ペインの一覧からドラッグ アンド ドロップすることもできます。  
  
 次の図は、クエリ モードの **[ブラウザー]** インターフェイスを示しています。  
  
 ![Analysis Services MDX クエリ デザイナー、クエリ ビュー](media/rsqd-dsawas-mdx-querymode.gif "Analysis Services MDX クエリ デザイナー、クエリ ビュー")  
  
 最初はグラフィカル デザイン モードで必要なオブジェクトを追加し、キューブをスライスするためのフィルターを追加してからテキスト モードに切り替え、メンバーのプロパティやセルのプロパティを追加しながら、生成された既定の MDX クエリに対して必要部分を補う、という使い方ができます。  
  
 **[メタデータ]** ペインには、 **[メタデータ]** と **[関数]** のタブが表示されます。 **[メタデータ]** タブからは、ディメンション、階層、KPI、およびメジャーをクエリ デザイン領域にドラッグできます。 **[関数]** タブからは、関数をクエリ デザイン領域にドラッグできます。 クエリを実行すると、クエリ デザイン領域に MDX クエリの結果が表示されます。 また、 **ツール バー** にある **[Excel で分析]** をクリックし、Microsoft Office Excel にデータをエクスポートすることによって、ユーザーに表示される結果をピボットテーブルで確認することもできます。次のセクションでは、 **[ブラウザー]** のモードごとに、ツール バーとすべてのペインについて詳しく説明します。  
  
 テキスト モードで作業中に、注意してください、**自動**(![クエリの自動実行](media/rsqdicon-autoexecute.gif "クエリの自動実行"))、ツールバーのトグル ボタンは使用できません。 使用してクエリを手動で実行するただし、**クエリの実行**(![クエリを実行](media/rsqdicon-run.gif "クエリを実行"))、ツールバーのボタンをクリックします。  
  
## <a name="sections"></a>セクション  
 **[ツール バー]**  
 ツール バーには、デザイン ビューまたはクエリ ビューで使用できるツールが表示されます。 ツール バーとその機能の使用方法の詳細については、「[ツール バー &#40;キューブ デザイナーの [アクション] タブ&#41; &#40;Analysis Services - 多次元データ&#41;](toolbar-browser-tab-cube-designer-analysis-services-multidimensional-data.md)」を参照してください。  
  
 **Excel で分析**  
 **[Excel で分析]** 機能を使用すると、現在選択されているキューブ データを Excel に送り、ピボットテーブルでデータをプレビューすることができます。 "現在選択されているデータ" は、 **[メタデータ]** ペインから追加した項目と、フィルターとクエリ作成機能を使用して定義したフィルターとに基づいて決まります。 詳細については、「[[Excel で分析] (キューブ デザイナーの [ブラウザー] タブ) (Analysis Services - 多次元データ)](analyze-in-excel-browser-cube-designer-analysis-services-multidimensional-data.md)」を参照してください。  
  
 **メタデータ**  
 キューブに含まれるオブジェクトを表示したり、階層をドリル ダウンしたり、メジャーを探索して使用したりするには、 **[メタデータ]** ペインを使用します。 それらを選択した後で、関連したデータを **[レポート]** ペインで閲覧します。 このペインの詳細については、「[[メタデータ] &#40;キューブ デザイナーの [ブラウザー] タブ&#41; &#40;Analysis Services - 多次元データ&#41;](metadata-browser-tab-cube-designer-analysis-services-multidimensional-data.md)」を参照してください。  
  
 **フィルターとクエリ**  
 デザイン画面のこの領域を使用して、 **[メタデータ]** ペインからオブジェクトをドラッグ アンド ドロップしたり、ソース キューブやディメンションに対してフィルターの条件を指定したりすることによって MDX クエリを作成します。 詳細については、「[クエリとフィルター &#40;キューブ デザイナーの [ブラウザー] タブ&#41; &#40;Analysis Services - 多次元データ&#41;](query-filter-browser-cube-designer-analysis-services-multidimensional-data.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [キューブ オブジェクト&#40;Analysis Services - 多次元データ&#41;](multidimensional-models-olap-logical-cube-objects/cube-objects-analysis-services-multidimensional-data.md)   
 [多次元モデルのキューブ](multidimensional-models/cubes-in-multidimensional-models.md)   
 [キューブ デザイナー &#40;Analysis Services - 多次元データ&#41;](cube-designer-analysis-services-multidimensional-data.md)  
  
  
