---
title: 'レッスン 2: レポート データ ソースのプロパティの変更 | Microsoft Docs'
ms.date: 05/23/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: c962b0ff-ce8a-4742-8262-dc730901afcf
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 466415ebd4075afd5dda83e95a498a32b50af453
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62651727"
---
# <a name="lesson-2-modifying-the-report-data-source-properties"></a>レッスン 2: レポート データ ソースのプロパティの変更
この [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] レッスンでは、受信者に配信されるレポートを、Web ポータルを使って選択します。 ここで定義するデータ ドリブン サブスクリプションによって、チュートリアル「 **基本的なテーブル レポートの作成 (SSRS チュートリアル)** 」で作成されたレポート [基本的なテーブル レポートの作成 (SSRS チュートリアル)](../reporting-services/create-a-basic-table-report-ssrs-tutorial.md)が配信されます。  この後の手順では、レポートがデータの取得に使用するデータ ソースの接続情報を変更します。 データ ドリブン サブスクリプションを介して配信できるのは、 **保存されている資格情報** を使用してレポート データ ソースにアクセスするレポートのみです。 保存されている資格情報は、レポートの自動処理に必要となります。  
  
また、データセットとレポートを変更し、パラメーターを使用して `[Order]` のレポートをフィルター処理します。これによってサブスクリプションが特定の注文と表示形式で、レポートのさまざまなインスタンスを出力できるようになります。  
  
## <a name="bkmk_modify_datasource"></a>保存された資格情報を使用するようにデータソースを変更するには  
  
1.  管理者特権を使用して [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] Web ポータルを参照します。たとえば、Internet Explorer アイコンを右クリックして **[管理者として実行]** をクリックします。  
 
2.    Web ポータルの URL を参照します。  例:   
    `https://<server name>/reports`が配信されます。  
    `https://localhost/reports`
 **注:** Web *ポータル* URL は "Reports" です。Report *Server* の URL "Reportserver" ではありません。  
3.  **Sales Orders** レポートを含むフォルダーを参照して、ショートカット メニューの **[管理]** をクリックします。  
 
 ![ssrs_tutorial_datadriven_manage_report](../reporting-services/media/ssrs-tutorial-datadriven-manage-report.png)
  
3.  左側のウィンドウの **[データソース]** をクリックします。  
  
4.  **[接続の種類]** が **[Microsoft SQL Server]** であることを確認します。  
  
5.  接続文字列が次のようになっていることを確認します。この文字列は、サンプル データベースがローカルのデータベース サーバーに存在することを想定しています。  
  
    ```  
    Data source=localhost; initial catalog=AdventureWorks2014  
    ```  
  
6.  **[次の資格情報を使用する]** をクリックします。  
  
7. **[資格情報の種類]** で **[Windows ユーザー名とパスワード]** を選択します。
8. ユーザー名とパスワードを入力します。ユーザー名は、 *domain\user*の形式で入力してください。 AdventureWorks2014 データベースにアクセスする権限がない場合は、このデータベースへの権限があるログイン情報を指定します。  
    
9. **[接続テスト]** をクリックして、データ ソースに接続できることを確認します。  
  
10. **[保存]** をクリックします。
11. **[キャンセル]** をクリックします。  
  
11. レポートを表示し、指定した資格情報を使用してレポートが実行されていることを確認します。 。  
  
## <a name="bkmk_modify_dataset"></a>AdventureWorksDataset を変更するには  
 次の手順では、パラメーターを使用して注文番号でデータ セットをフィルター処理できるよう、データセットを変更します。
1.  で **Sales Orders** レポートを開きます。 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]  
  
2.  データセット `AdventureWorksDataset` を右クリックし、 **[データセットのプロパティ]** をクリックします。  
    ![ssrs_tutorial_datadriven_datasetproperties](../reporting-services/media/ssrs-tutorial-datadriven-datasetproperties.png)  
3.  `WHERE (UPPER(SalesOrderNumber) =UPPER(@OrderNumber) or  @OrderNumber IS NULL)` ステートメントを `Group By` ステートメントの前に追加します。 完全なクエリ構文は次のとおりです。  
  
    ```  
    SELECT soh.OrderDate AS Date, soh.SalesOrderNumber AS [Order], pps.Name AS Subcat, pp.Name AS Product, SUM(sd.OrderQty) AS Qty, SUM(sd.LineTotal)  AS LineTotal  
    FROM Sales.SalesPerson AS sp INNER JOIN  
      Sales.SalesOrderHeader AS soh ON sp.BusinessEntityID = soh.SalesPersonID INNER JOIN  
       Sales.SalesOrderDetail AS sd ON sd.SalesOrderID = soh.SalesOrderID INNER JOIN  
       Production.Product AS pp ON sd.ProductID = pp.ProductID  
    INNER JOIN  
       Production.ProductSubcategory AS pps ON pp.ProductSubcategoryID = pps.ProductSubcategoryID   
    INNER JOIN  
        Production.ProductCategory AS ppc ON ppc.ProductCategoryID = pps.ProductCategoryID  
  
    WHERE (UPPER(SalesOrderNumber) =UPPER(@OrderNumber) or  @OrderNumber IS NULL)  
  
    GROUP BY ppc.Name, soh.OrderDate, soh.SalesOrderNumber, pps.Name, pp.Name, soh.SalesPersonID  
    HAVING (ppc.Name = 'Clothing')  
    ```  
  
4.  **[OK]** をクリックします。  
 次の手順では、レポートにパラメーターを追加します。  データセット パラメーターは、レポート パラメーターにフィードされます。 
## <a name="bkmk_add_reportparameter"></a>レポート パラメーターを追加し、レポートを再パブリッシュするには  
  
1.  **[レポート データ]** ペインで、[パラメーター] フォルダーを展開し、 **[Ordernumber]** パラメーターをダブルクリックします。  これは、データセットにパラメーターを追加した前の手順で自動的に作成されています。 **[新規]** そして **[パラメーター]** をクリックします。  
 ![ssrs_tutorial_datadriven_parameter](../reporting-services/media/ssrs-tutorial-datadriven-parameter.png) 
2.  **[名前]** が `OrderNumber`であることを確認します。  
  
3.  **[プロンプト]** が `OrderNumber`であることを確認します。  
  
4.  **[空白の値 (" " ) を許可]** を選択します。  
  
5.  **[NULL 値を許可]** を選択します。  
  
6.  **[OK]** をクリックします。  
  
7.  **[プレビュー]** タブをクリックして、レポートを実行します。 レポートの先頭にパラメーター入力領域が表示されます。 次のいずれかを実行できます。  
  
    -   [レポートの表示] をクリックして、パラメーターを使用しない完全なレポートを表示する。  
  
    -   **Null** オプションを選択解除し、たとえば注文番号を「 *so71949*」と入力し、レポートにこの 1 つの注文のみが表示されるよう **[レポートの表示]** をクリックします。  
    ![ssrs_tutorial_datadriven_reportviewer_parameter](../reporting-services/media/ssrs-tutorial-datadriven-reportviewer-parameter.png) 
 
  
## <a name="bkmk_redeploy"></a>レポートを再配置する  
  
1.  レポートを再配置して、このレッスンで適用した変更を、次のレッスンのサブスクリプション構成で利用できるようにします。 テーブルのチュートリアルで使用されるプロジェクト プロパティの詳細については、「[レッスン 6: グループと合計の追加 (Reporting Services)](../reporting-services/lesson-6-adding-grouping-and-totals-reporting-services.md)」の「レポートをレポート サーバーにパブリッシュするには (オプション)」セクションを参照してください。  
  
2.  ツール バーの **[ビルド]** をクリックし、 **[Tutorial の配置]** をクリックします。  
  
## <a name="next-steps"></a>Next Steps  
+ 保存されている資格情報を使用してデータを取得するレポートを構成したので、パラメーターを使用してデータをフィルター処理できます。 
+ 次のレッスンでは、Web ポータルのデータ ドリブン サブスクリプション ページを使用してサブスクリプションを構成します。 「 [レッスン 3: データ ドリブン サブスクリプションの定義](../reporting-services/lesson-3-defining-a-data-driven-subscription.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
[レポート データ ソースを管理する](../reporting-services/report-data/manage-report-data-sources.md)  
[レポート データ ソースに関する資格情報と接続情報を指定する](../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md)  
[データ ドリブン サブスクリプションの作成 &#40;SSRS チュートリアル&#41;](../reporting-services/create-a-data-driven-subscription-ssrs-tutorial.md)  
[基本的なテーブル レポートの作成 (SSRS チュートリアル)](../reporting-services/create-a-basic-table-report-ssrs-tutorial.md)  
  
  
  

