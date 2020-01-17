---
title: キューブとディメンションのプロパティの確認 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: dda922b8-6d75-4662-b09e-8a317c6a1c70
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c95d241d136f290110ac8a2b72540011a3922e24
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66078999"
---
# <a name="reviewing-cube-and-dimension-properties"></a>キューブとディメンションのプロパティの確認
  キューブを定義した後は、その結果をキューブ デザイナーで確認できます。 この実習では、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial プロジェクトのキューブの構造を確認します。  
  
### <a name="to-review-cube-and-dimension-properties-in-cube-designer"></a>キューブ デザイナーでキューブとディメンションのプロパティを確認するには  
  
1.  キューブ デザイナーを開くには、ソリューション エクスプローラーの **[キューブ]** ノードで **[Analysis Services Tutorial]** キューブをダブルクリックします。  
  
2.  キューブ デザイナーで **[キューブ構造]** タブをクリックし、 **[メジャー]** ペインの **[Internet Sales]** メジャー グループを展開して、定義されているメジャーを表示します。  
  
     目的の場所 (順序) にドラッグすることによって、メジャーの順序を変更できます。 ここで作成した順序は、クライアント アプリケーションでのこれらのメジャーの順序に反映されます。 メジャー グループとその中のメジャーにはそれぞれプロパティが割り当てられます。これらのプロパティは [プロパティ] ウィンドウで編集できます。  
  
3.  キューブ デザイナーの **[キューブ構造]** タブの **[ディメンション]** ペインで、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial キューブのキューブ ディメンションを確認してください。  
  
     ソリューション エクスプローラーに表示されているように、データベース レベルで作成したディメンションは 3 つだけですが、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial キューブには 5 つのキューブ ディメンションがあります。 データベース ディメンションよりキューブ ディメンションの方が多いのは、Date データベース ディメンションを使用して、日付関連のキューブ ディメンションを 3 つ作成したためです。これらは、ファクト テーブル内のそれぞれ異なる日付関連ファクトに基づいています。 日付関連のこうしたディメンションは、" *多様ディメンション*" とも呼ばれます。 日付に関連する 3 つのキューブ ディメンションにより、製品売上に関する 3 種類のファクト (製品の受注日、納品期日、出荷日) を使用してキューブを生成できます。 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] では、複数のキューブ ディメンションに対して 1 つのデータベース ディメンションを繰り返し利用することにより、ディメンションの管理が容易になり、ディスク容量を節約でき、全体的な処理時間が短くなります。  
  
4.  **[キューブ構造]** タブの **[ディメンション]** ペインで **[Customer]** を展開し、 **[Customer の編集]** をクリックしてディメンション デザイナーでディメンションを開きます。  
  
     ディメンション デザイナーには、これらのタブが含まれています。**ディメンション構造**、**属性リレーションシップ**、**翻訳**、および**ブラウザー**します。 注意、**ディメンション構造** タブには、3 つのペインが含まれています。**属性**、**階層**、および**データ ソース ビュー**します。 ディメンションに含まれている属性は **[属性]** ペインに表示されます。 詳細については、次を参照してください。 [Dimension Attribute Properties Reference](multidimensional-models/dimension-attribute-properties-reference.md)、[ユーザー定義階層の](multidimensional-models/user-defined-hierarchies-create.md)します。  
  
5.  キューブ デザイナーに切り替えるには、ソリューション エクスプローラーの **[キューブ]** ノードで **[Analysis Services Tutorial]** キューブを右クリックし、 **[ビュー デザイナー]** をクリックします。  
  
6.  キューブ デザイナーで、 **[ディメンションの使用法]** タブをクリックします。  
  
     [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial キューブのこのビューには、Internet Sales メジャー グループで使用されているキューブ ディメンションが表示されます。 また、ここでは、各ディメンションと、そのディメンションが使用されているメジャー グループとのリレーションシップの種類を指定できます。  
  
7.  **[パーティション]** タブをクリックします。  
  
     キューブ ウィザードは、集計なしの MOLAP (multidimensional online analytical processing) ストレージ モードを使用して、1 つのパーティションをキューブに定義します。 MOLAP では、パフォーマンスを最適化するため、すべてのリーフレベル データと集計がキューブに格納されます。 集計とは、事前に計算された要約データです。質問の答えをあらかじめ用意しておくことで、クエリの応答時間が短くなります。 **[パーティション]** タブでは、新しいパーティション、ストレージ設定、および書き戻し設定を定義できます。パーティションの詳細については、「[パーティション (Analysis Services - 多次元データ)](multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md)」、「[集計と集計デザイン](multidimensional-models-olap-logical-cube-objects/aggregations-and-aggregation-designs.md)」を参照してください。  
  
8.  **[ブラウザー]** タブをクリックします。  
  
     [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]のインスタンスにまだキューブを配置していないので、キューブは表示されません。 この時点では、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial プロジェクトのキューブは、キューブの定義でしかありません。したがって、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]のどのインスタンスにも配置できます。 キューブを配置して処理するときに、定義済みオブジェクトを [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] のインスタンスに作成し、基のデータ ソースのデータをオブジェクトに取り込みます。  
  
9. ソリューション エクスプローラーで、 **[キューブ]** ノード内にある **[Analysis Services Tutorial]** を右クリックし、 **[コードの表示]** をクリックします。 場合によっては、しばらく待つ必要があります。  
  
     [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial キューブの XML コードが、 **[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial.cube [XML]** タブに表示されます。ディメンションの配置時には、実際にはこのコードによってキューブが [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] のインスタンスに作成されます。 詳細については、「[Analysis Services のプロジェクトでの XML の表示 (SSDT)](multidimensional-models/view-the-xml-for-an-analysis-services-project-ssdt.md)」を参照してください。  
  
10. XML コードのタブを閉じます。  
  
## <a name="next-task-in-lesson"></a>このレッスンの次の作業  
 [Analysis Services プロジェクトの配置](lesson-2-5-deploying-an-analysis-services-project.md)  
  
## <a name="see-also"></a>参照  
 [ディメンション デザイナーでのディメンション データの参照](multidimensional-models/database-dimensions-browse-dimension-data-in-dimension-designer.md)  
  
  
