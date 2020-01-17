---
title: SQL Server Reporting Services のツリー マップとサンバースト グラフ | Microsoft Docs
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
ms.reviewer: ''
ms.custom: ''
ms.date: 04/26/2019
ms.openlocfilehash: fd9ac9ccd0906ee34a66b7144fdd964d05e5f050
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68259364"
---
# <a name="treemap-and-sunburst-charts-in-reporting-services"></a>Reporting Services のツリー マップとサンバースト グラフ 

SQL Server [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ツリー マップおよびサンバースト視覚エフェクトは、階層データを視覚的に表現する上で非常に効果的です。 この記事では、ツリー マップまたはサンバースト グラフを [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] レポートに追加する方法の概要を説明します。 この記事には、開始するための AdventureWorks サンプル クエリも含まれています。  
  
##  <a name="bkmk_treemap_chart"></a> ツリー マップ グラフ  

ツリー マップ グラフでは、グラフ領域がデータ階層のさまざまなレベルと相対サイズを表す複数の四角形に分割されます。 マップは、幹から次第に小さな枝へと分かれていく、木の枝に似ています。 各四角形は、階層内の次のレベルを表す、より小さな四角形に分割されます。 最上位レベルのツリー マップ四角形は、最も大きな四角形がグラフの左上隅に、最も小さな四角形が右下隅にという並びで順々に配置されます。  四角形内では、次のレベルの四角形が同様に左上から右下へ大きい順に配置されます。  

たとえば、次のサンプル ツリー マップの図では、南西区域が最も大きく、ドイツが最も小さくなっています。 南西区域内では、ロード バイクがマウンテン バイクよりも大きくなっています。  

![ssrs_treemap_example](../../reporting-services/report-design/media/ssrs-treemap-example.png "ssrs_treemap_example")  
  
### <a name="to-insert-a-treemap-chart-and-set-up-the-sample-adventureworks-data"></a>ツリー マップ グラフを挿入し、Adventureworks のサンプル データに対して設定するには  

> [!NOTE]
> レポートにグラフを追加する前に、データ ソースとデータセットを作成します。  サンプル データとサンプル クエリについては、「[AdventureWorks データのサンプル](#bkmk_sample_data)」を参照してください。  
  
1. デザイン サーフェイスを右クリックし **[挿入]**  >  **[グラフ]** を選択します。 **ツリーマップ** アイコンを選択します。

    ![ssrs_treemap_icon](../../reporting-services/media/ssrs-treemap-icon.png "ssrs_treemap_icon")  

2. グラフの位置の変更およびサイズの変更を行います。 サンプル データを使用する場合は、5 インチ幅のグラフで始めることをお勧めします。  
  
3. サンプル データから、次のフィールドを追加します。  
  
    * **値:** LineTotal
    * **カテゴリ グループ** (次の順序を使用):
        1. CategoryName
        2. SubcategoryName
    * **系列グループ:** TerritoryName  

    ![ssrs_treemap_example_properties](../../reporting-services/report-design/media/ssrs-treemap-example-properties.png "ssrs_treemap_example_properties")
  
4. ツリーマップの全般的な形式に合わせてページ サイズを最適化するには、凡例を下部に配置します。  
  
5. サブカテゴリと行の合計を表示するツールヒントを追加するには、 **[LineTotal]** を右クリックし、 **[系列のプロパティ]** を選択します。  
  
     ![ssrs_visualization_seriesproperties](../../reporting-services/report-design/media/ssrs-visualization-seriesproperties.png "ssrs_visualization_seriesproperties")  
  
     **[ツールヒント]** プロパティを次の値に設定します。  
  
    ```
    =Fields!SubcategoryName.Value &": " &Format(Sum(Fields!LineTotal.Value),"C")  
    ```  
  
    詳細については、「[系列へのツールヒントの表示 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/show-tooltips-on-a-series-report-builder-and-ssrs.md)」を参照してください。  
  
6. 既定のグラフ タイトルを **区域別の売上**に変更します。  
  
7. 表示されるラベル値の数は、フォントのサイズ、グラフ領域全体のサイズ、および特定の四角形のサイズにより変わります。 より多くのラベルを表示するには、**LineTotal** の **[ラベル フォント]** プロパティを既定の **8pt** から **10pt** に変更します。  

##  <a name="bkmk_sunburst_chart"></a> サンバースト グラフ  

サンバースト グラフでは、階層は一連の円で表されます。 階層の最上位レベルは中心であり、階層の下位レベルは中心の外側の輪です。  最下位レベルの階層は、最も外側のリングとなります。  
  
![ssrs_sunburst_example](../../reporting-services/report-design/media/ssrs-sunburst-example.png "ssrs_sunburst_example")  
  
### <a name="to-insert-a-sunburst-chart-and-set-up-the-sample-adventureworks-data"></a>サンバースト グラフを挿入し、Adventureworks のサンプル データに対して設定するには

> [!NOTE]
> レポートにグラフを追加する前に、データ ソースとデータセットを作成します。 サンプル データとサンプル クエリについては、「[AdventureWorks データのサンプル](#bkmk_sample_data)」を参照してください。  
  
1. デザイン サーフェイスを右クリックし **[挿入]**  >  **[グラフ]** を選択します。 **[サンバースト]** アイコンを選択します。

     ![ssrs_sunburst_icon](../../reporting-services/media/ssrs-sunburst-icon.png "ssrs_sunburst_icon")  
  
2. グラフの位置の変更およびサイズの変更を行います。 サンプル データを使用する場合は、5 インチ幅のグラフで始めることをお勧めします。  
  
3. サンプル データから、次のフィールドを追加します。  

    * **値:** LineTotal
    * **カテゴリ グループ** (次の順序を使用):
        1. CategoryName
        2. SubcategoryName
        3. SalesReasonName
    * **系列グループ:** TerritoryName  

    ![ssrs_treemap_example_properties](../../reporting-services/report-design/media/ssrs-treemap-example-properties.png "ssrs_treemap_example_properties")
  
4. サンバースト グラフの全般的な形式に合わせてページ サイズを最適化するには、凡例を下部に配置します。  
  
5. 既定のグラフ タイトルを **区域別の売上と販売理由** に変更します。  
  
6. サンバーストにラベルとしてカテゴリ グループの値を追加するには、ラベルのプロパティ **[Visible]** を true に設定し、 **[UseValueAsLabel]** を false に設定します。<br /><br /> 表示されるラベル値は、フォントのサイズ、グラフ領域全体のサイズ、および特定の四角形のサイズに影響されます。  より多くのラベルを表示するには、**LineTotal** の **[ラベル フォント]** プロパティを既定の **8pt** から **10pt** に変更します。

    ![ssrs_sunburst_linetotalproperties](../../reporting-services/report-design/media/ssrs-sunburst-linetotalproperties.png "ssrs_sunburst_linetotalproperties")
  
7. 色の範囲を変更する場合は、グラフの **[パレット]** プロパティを変更します。  

     ![ssrs_visualization_palette](../../reporting-services/report-design/media/ssrs-visualization-palette.png "ssrs_visualization_palette")  

##  <a name="bkmk_sample_data"></a> AdventureWorks データのサンプル

このセクションでは、サンプル クエリを紹介すると共に、[!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] でデータ ソースとデータセットを作成するための基本的な手順について説明します。 レポートにデータ ソースとデータセットが既に存在する場合、このセクションは省略できます。  
  
クエリでは、AdventureWorks の販売注文の詳細なデータを返します。これには販売区域、製品カテゴリ、製品サブカテゴリ、および販売理由のデータが含まれます。  
  
1. **データを取得します**。  
  
     このセクションのクエリは、「[Adventure Works 2016 Full Database Backup](https://github.com/Microsoft/sql-server-samples/releases)」 (Adventure Works 2016: データベースの完全なバックアップ) からダウンロードできる AdventureWorks データベースに基づいています。  

2. **データ ソースを作成します**。  
  
    1. **[レポート データ]** で、 **[データ ソース]** を右クリックし、 **[データ ソースの追加]** を選択します。  
  
    2. **[レポートに埋め込まれた接続を使用する]** を選択します。  
  
    3. [接続の種類] で **[Microsoft SQL Server]** を選択します。  
  
    4. サーバーとデータベースに接続文字列を入力します。 例:  
  
        ```
        Data Source=[server name];Initial Catalog=AdventureWorks2016  
        ```  
  
    5. 接続を確認するには、 **[テスト接続]** ボタンを選択し、 **[OK]** をクリックします。  
  
     データ ソースの作成の詳細については、「[データ接続を追加および確認する &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)」を参照してください。  
  
3. **データセットを作成します**。  
  
    1. **[レポート データ]** で、 **[データセット]** を右クリックし、 **[データセットの追加]** を選択します。  
  
    2. **[レポートに埋め込まれたデータセットを使用します]** を選択します。  
  
    3. 作成したデータ ソースを選択します。  
  
    4. **[テキスト]** クエリ タイプを選択し、次のクエリをコピーして **[クエリ]** ボックスに貼り付けます。  
  
        ```sql
        SELECT    Sales.SalesOrderHeader.SalesOrderID, Sales.SalesOrderHeader.OrderDate, Sales.SalesOrderDetail.SalesOrderDetailID, Sales.SalesOrderDetail.ProductID, Sales.SalesOrderDetail.LineTotal,   
                                 Sales.SalesOrderDetail.UnitPrice, Sales.SalesOrderDetail.OrderQty, Production.Product.Name, Production.Product.ProductNumber, Sales.SalesTerritory.TerritoryID, lower(Sales.SalesTerritory.Name) AS TerritoryName,   
                                 Production.ProductSubcategory.Name AS SubcategoryName, Production.ProductCategory.Name AS CategoryName, Sales.SalesReason.SalesReasonID, Sales.SalesReason.Name AS SalesReasonName  
        FROM            Sales.SalesOrderDetail INNER JOIN  
                                 Sales.SalesOrderHeader ON Sales.SalesOrderDetail.SalesOrderID = Sales.SalesOrderHeader.SalesOrderID INNER JOIN  
                                 Production.Product ON Sales.SalesOrderDetail.ProductID = Production.Product.ProductID INNER JOIN  
                                 Sales.SalesTerritory ON Sales.SalesOrderHeader.TerritoryID = Sales.SalesTerritory.TerritoryID AND Sales.SalesOrderHeader.TerritoryID = Sales.SalesTerritory.TerritoryID AND   
                                 Sales.SalesOrderHeader.TerritoryID = Sales.SalesTerritory.TerritoryID INNER JOIN  
                                 Production.ProductSubcategory ON Production.Product.ProductSubcategoryID = Production.ProductSubcategory.ProductSubcategoryID AND   
                                 Production.Product.ProductSubcategoryID = Production.ProductSubcategory.ProductSubcategoryID AND   
                                 Production.Product.ProductSubcategoryID = Production.ProductSubcategory.ProductSubcategoryID INNER JOIN  
                                 Production.ProductCategory ON Production.ProductSubcategory.ProductCategoryID = Production.ProductCategory.ProductCategoryID AND   
                                 Production.ProductSubcategory.ProductCategoryID = Production.ProductCategory.ProductCategoryID AND   
                                 Production.ProductSubcategory.ProductCategoryID = Production.ProductCategory.ProductCategoryID INNER JOIN  
                                 Sales.SalesOrderHeaderSalesReason ON Sales.SalesOrderHeader.SalesOrderID = Sales.SalesOrderHeaderSalesReason.SalesOrderID AND   
                                 Sales.SalesOrderHeader.SalesOrderID = Sales.SalesOrderHeaderSalesReason.SalesOrderID AND Sales.SalesOrderHeader.SalesOrderID = Sales.SalesOrderHeaderSalesReason.SalesOrderID AND   
                                 Sales.SalesOrderHeader.SalesOrderID = Sales.SalesOrderHeaderSalesReason.SalesOrderID INNER JOIN  
                                 Sales.SalesReason ON Sales.SalesOrderHeaderSalesReason.SalesReasonID = Sales.SalesReason.SalesReasonID AND   
                                 Sales.SalesOrderHeaderSalesReason.SalesReasonID = Sales.SalesReason.SalesReasonID AND Sales.SalesOrderHeaderSalesReason.SalesReasonID = Sales.SalesReason.SalesReasonID AND   
                                 Sales.SalesOrderHeaderSalesReason.SalesReasonID = Sales.SalesReason.SalesReasonID  
        ```  
  
    5. **[OK]** を選択します。  
  
     データセットの作成の詳細については、「[共有データセットまたは埋め込みデータセットの作成 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)」を参照してください。  
  
## <a name="see-also"></a>参照

* [共有データセット デザイン ビュー &#40;レポート ビルダー&#41;](../../reporting-services/report-builder/shared-dataset-design-view-report-builder.md)

* [系列へのツールヒントの表示 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/show-tooltips-on-a-series-report-builder-and-ssrs.md)

* [チュートリアル: Power BI でのツリー マップ](https://support.powerbi.com/knowledgebase/articles/556200-tutorial-treemaps-in-power-bi)

* [ツリー マップ: Microsoft Research Data Visualization Apps for Office](https://research.microsoft.com/projects/msrdatavis/treemap.aspx)