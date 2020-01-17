---
title: データ ソース ビュー デザイナー (Analysis Services - 多次元データ) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dsvdesigner.f1
helpviewer_keywords:
- Data Source View Designer
ms.assetid: 6f40a074-761f-440b-a999-09b755bd86ce
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9153a2d07653872ca6ce1f90e39c90f32da21fba
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66082522"
---
# <a name="data-source-view-designer-analysis-services---multidimensional-data"></a>データ ソース ビュー デザイナー (Analysis Services - 多次元データ)
  データ ソース ビュー (DSV) は、多次元モデル内でキューブやディメンションを作成するために使用される外部リレーショナル データ ソースの論理ビューです。  
  
 DSV を生成した後、 **内で** データ ソース ビュー デザイナー [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] を使用して DSV を直接操作することができます。基になるデータ ソースで、多次元モデルで必要とされるデータ要素が欠落している場合に、この方法が役に立つことがあります。  
  
 **データ ソース ビュー デザイナー** を開くには:  
  
-   **ソリューション エクスプローラー**でデータ ソース ビューをダブルクリックします。  
  
-   **ソリューション エクスプローラー** のデータ ソース ビューを右クリックし、 **[開く]** または **[デザイナーの表示]** を選択します。  
  
 **データ ソース ビュー デザイナー** には、ツール バー、DSV 内のオブジェクトとリレーションシップを示すダイアグラム、テーブルと名前付きクエリをアルファベット順に示すテーブル ペイン、および DSV の特定のダイアグラムを作成および表示するために使用する [ダイアグラム オーガナイザー] ペインがあります。 テーブルまたはリレーションシップを右クリックして、状況に依存するコマンドにアクセスすることができます。  
  
 ![データ ソース ビュー デザイナー](media/ssas-dsvdesigner.PNG "データ ソース ビュー デザイナー")  
  
 少なくとも DSV には、処理中にモデル オブジェクトを設定するために使用されるリレーショナル データベース テーブルが表示されます。 DSV は通常、データ ソース ビュー ウィザードを使用して生成します。 DSV 内のテーブル、列、およびリレーションシップが、キューブ内にあるディメンションとメジャーの基準になります。 DSV を作成した後、データ ソース ビュー デザイナーを使用して変更を加えることができます。  
  
 ほとんどの Analysis Services 開発者は、生成された DSV をほぼそのまま使用し、多少のカスタマイズを加えます。 特に SQL Server データベース内のビューからソース データを生成する場合は、この方法が一般的に使用されます。 その場合、Analysis Services DSV の代わりに、T-SQL ビュー内でデータのリレーションシップと計算を管理したいと考えることがあります。 ただし、基になるデータベースの所有者でない場合は、Analysis Services 内で DSV を変更し、モデル内で使用するデータ構造の開発をさらに進めることができます。  
  
## <a name="tasks-in-data-source-view-designer"></a>データ ソース ビュー デザイナー内のタスク  
 データ ソース ビュー デザイナーを使用して、DSV に対して次の編集を行うことができます。  
  
|||  
|-|-|  
|列またはテーブルの名前を変更するか、新しい計算列を作成する。 たとえば、名と姓を結合して、新しフル ネーム列を作成します。|[データ ソース ビューでの名前付き計算の定義 (Analysis Services)](multidimensional-models/define-named-calculations-in-a-data-source-view-analysis-services.md)|  
|テーブルのリレーションシップの手動での追加|[データ ソース ビューでの論理リレーションシップの定義 (Analysis Services)](multidimensional-models/define-logical-relationships-in-a-data-source-view-analysis-services.md)|  
|T-SQL クエリに基づいて新しいオブジェクトを定義する、名前付きクエリを作成します。|[データ ソース ビューでの名前付きクエリの定義 (Analysis Services)](multidimensional-models/define-named-queries-in-a-data-source-view-analysis-services.md)|  
|基になるデータを探索し、モデル オブジェクトによって表される実際のデータ値を表示します。<br /><br /> データ探索では、基になるディメンション テーブルやクエリから返されるデータを視覚的に検査し、コピーすることができます。 既定では、データ探索には上から順に取得するサンプリング方法が使用され、サンプル数は 5,000 ですが、これらの設定は変更できます。|[データ ソース ビューでのデータの検索 (Analysis Services)](multidimensional-models/explore-data-in-a-data-source-view-analysis-services.md)|  
|DSV のテーブルとリレーションシップのすべてまたは一部の図示|[データ ソース ビュー デザイナーでのダイアグラムの操作 &#40;Analysis Services&#41;](multidimensional-models/work-with-diagrams-in-data-source-view-designer-analysis-services.md)|  
  
## <a name="see-also"></a>関連項目  
 [多次元モデルのデータ ソース ビュー](multidimensional-models/data-source-views-in-multidimensional-models.md)   
 [データ ソース ビューでのテーブルまたはビューの追加または削除 (Analysis Services)](multidimensional-models/adding-or-removing-tables-or-views-in-a-data-source-view-analysis-services.md)  
  
  
