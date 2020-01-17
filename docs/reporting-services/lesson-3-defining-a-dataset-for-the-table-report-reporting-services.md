---
title: 'レッスン 3 : テーブル レポートのデータセットの定義 (Reporting Services) | Microsoft Docs'
ms.date: 05/01/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: ee93dfcb-8f52-4d63-b4f6-0d38e00fd350
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: eaa2af570ae363e6a48c8d14e5b73c70e6790b5c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65106021"
---
# <a name="lesson-3-defining-a-dataset-for-the-table-report-reporting-services"></a>レッスン 3 : テーブル レポートのデータセットの定義 (Reporting Services)

データ ソースを定義した後、データセットを定義する必要があります。 [!INCLUDE[ssrsnoversion](../includes/ssrsnoversion-md.md)]では、レポートで使用するデータは *データセット*に格納されます。 データセットには、データ ソースへのポインターと、レポートで使用されるクエリ、計算フィールド、変数が含まれています。

レポート デザイナーでクエリ デザイナーを使用して、データセットを定義します。 このチュートリアルでは、AdventureWorks2016 データベースから販売注文情報を取得するクエリを作成します。

## <a name="define-a-transact-sql-query-for-report-data"></a>レポート データ用に Transact-SQL クエリを定義する  

1. **[レポート データ]** ウィンドウで、 **[新規作成]**  >  **[データセット]** の順にクリックします。 **[データセットのプロパティ]** ダイアログ ボックスが開き、 **[クエリ]** セクションが表示されます。

    ![vs-data_set_properties_dialog](media/lesson-3-defining-a-dataset-for-the-table-report-reporting-services/vs-dataset-properties-dialog.png)

2. **[名前]** ボックスに「AdventureWorksDataset」と入力します。

3. その下の **[レポートに埋め込まれたデータセットを使用します]** を選択します。

4. **[データ ソース]** ボックスで、AdventureWorks2016 を選択します。

5. **[クエリの種類]** として **[テキスト]** を選択します。

6. **[クエリ]** ボックスに次の Transact-SQL クエリを入力するか、コピーして貼り付けます。

    ```T-SQL
    SELECT
       soh.OrderDate AS [Date],
       soh.SalesOrderNumber AS [Order],
       pps.Name AS [Subcat],
       pp.Name as [Product],
       SUM(sd.OrderQty) AS [Qty],
       SUM(sd.LineTotal) AS [LineTotal]
    FROM Sales.SalesPerson sp
    INNER JOIN Sales.SalesOrderHeader AS soh
          ON sp.BusinessEntityID = soh.SalesPersonID
       INNER JOIN Sales.SalesOrderDetail AS sd
          ON sd.SalesOrderID = soh.SalesOrderID
       INNER JOIN Production.Product AS pp
          ON sd.ProductID = pp.ProductID
       INNER JOIN Production.ProductSubcategory AS pps
          ON pp.ProductSubcategoryID = pps.ProductSubcategoryID
       INNER JOIN Production.ProductCategory AS ppc
          ON ppc.ProductCategoryID = pps.ProductCategoryID
    GROUP BY ppc.Name, soh.OrderDate, soh.SalesOrderNumber, pps.Name, pp.Name,soh.SalesPersonID  
    HAVING ppc.Name = 'Clothing'
    ```

7. (省略可能) **[クエリ デザイナー]** ボタンを選択します。 クエリは、テキスト ベースの*クエリ デザイナー*に表示されます。 クエリの結果を表示するには、**クエリ デザイナー** ツール バーの**実行** (![ssrs_querydesigner_run](media/ssrs-querydesigner-run.png)) ボタンをクリックします。 表示されるデータセットには、AdventureWorks2016 データベースの 4 つのテーブルからの 6 個のフィールドが含まれています。 クエリでは、エイリアスなど Transact-SQL の機能が利用されます。 たとえば、SalesOrderHeader テーブルは *soh*と呼ばれます。

8. **[OK]** を選択して**クエリ デザイナー**を終了します。

9. **[OK]** を選択して **[データセットのプロパティ]** ダイアログ ボックスを閉じます。

**[レポート データ]** ウィンドウに AdventureWorksDataset データセットとフィールドが表示されます。

   ![ssrs_adventureworksdataset](media/ssrs-adventureworksdataset.png)

## <a name="next-steps"></a>次の手順

これで、レポートのデータを取得するクエリを指定できました。 次に、レポートのレイアウトを作成します。 「[レッスン 4: レポートへのテーブルの追加 &#40;Reporting Services&#41;](lesson-4-adding-a-table-to-the-report-reporting-services.md)」に進みます。

## <a name="see-also"></a>参照

[クエリ デザイン ツール &#40;SSRS&#41;](../reporting-services/report-data/query-design-tools-ssrs.md)
[SQL Server の接続の種類 &#40;SSRS&#41;](../reporting-services/report-data/sql-server-connection-type-ssrs.md)
[チュートリアル: Transact-SQL ステートメントの作成](../t-sql/tutorial-writing-transact-sql-statements.md)
