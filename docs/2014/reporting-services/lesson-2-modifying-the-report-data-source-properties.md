---
title: レッスン 2:ソースのプロパティのレポート データの変更 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: c962b0ff-ce8a-4742-8262-dc730901afcf
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 619d35c084884aa72de63ff221d5a6f61ea86196
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66108487"
---
# <a name="lesson-2-modifying-the-report-data-source-properties"></a>レッスン 2:レポート データ ソースのプロパティの変更
  このレッスンでは、受信者に配信されるレポートを、レポート マネージャーを使って選択します。 ここで定義するデータ ドリブン サブスクリプションによって、チュートリアル「 **基本的なテーブル レポートの作成 (SSRS チュートリアル)** 」で作成されたレポート [基本的なテーブル レポートの作成 (SSRS チュートリアル)](../reporting-services/create-a-basic-table-report-ssrs-tutorial.md)が配信されます。 この後の手順では、レポートがデータの取得に使用するデータ ソースの接続情報を変更します。 データ ドリブン サブスクリプションを介して配信できるのは、 **保存されている資格情報** を使用してレポート データ ソースにアクセスするレポートのみです。 保存されている資格情報は、レポートの自動処理に必要となります。  
  
 また、データセットとレポートを変更し、パラメーターを使用して `[Order]` のレポートをフィルター処理します。これによってサブスクリプションが特定の注文と表示形式で、レポートのさまざまなインスタンスを出力できるようになります。  
  
 **このトピックの内容:**  
  
-   [データ ソースのプロパティを変更するには](#bkmk_modify_datasource)  
  
-   [AdventureWorksDataset を変更するには](#bkmk_modify_dataset)  
  
-   [レポート パラメーターを追加し、レポートを再パブリッシュ](#bkmk_add_reportparameter)  
  
-   [レポートを再配置するには](#bkmk_redeploy)  
  
##  <a name="bkmk_modify_datasource"></a> データ ソースのプロパティを変更するには  
  
1.  開始[レポート マネージャー &#40;SSRS ネイティブ モード&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)管理者特権を持つなど、Internet Explorer のアイコンを右クリックし をクリックして**管理者として実行**します。  
  
2.  **Sales Orders** レポートを含むフォルダーを参照して、ショートカット メニューの **[管理]** をクリックします。  
  
     ![レポートのコンテキスト メニューを開き、管理](../../2014/tutorials/media/ssrs-tutorial-datadriven-manage-report.gif "レポートのコンテキスト メニューを開き、管理 の選択")  
  
3.  **[データ ソース]** タブをクリックします。  
  
4.  **[接続の種類]** で **[Microsoft SQL Server]** を選択します。  
  
5.  カスタム データ ソースの接続文字列は次のようになります。この文字列は、サンプル データベースがローカルのデータベース サーバーに存在することを想定しています。  
  
    ```  
    Data source=localhost; initial catalog=AdventureWorks2012  
    ```  
  
6.  **[レポート サーバーに保存され、セキュリティで保護された資格情報]** をクリックします。  
  
7.  ユーザー名とパスワードを入力します。ユーザー名は、 *domain\user*の形式で入力してください。 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] データベースにアクセスする権限がない場合は、このデータベースへの権限があるログイン情報を指定します。  
  
8.  **[データ ソースへの接続時に Windows 資格情報として使用する]** をクリックし、 **[OK]** をクリックします。 ドメイン アカウントを使用していない場合 ([!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ログインを使用している場合など) は、このチェック ボックスをオンにしないでください。  
  
9. **[接続テスト]** をクリックして、データ ソースに接続できることを確認します。  
  
10. **[適用]** をクリックします。  
  
11. レポートを表示し、指定した資格情報を使用してレポートが実行されていることを確認します。 レポートを表示するには、 **[表示]** タブをクリックします。レポートが開いたら、従業員名を選択してから **[レポートの表示]** をクリックする必要があります。  
  
##  <a name="bkmk_modify_dataset"></a> AdventureWorksDataset を変更するには  
  
1.  [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] で Sales Orders レポートを開きます。  
  
2.  データセット `AdventureWorksDataset` を右クリックし、 **[データセットのプロパティ]** をクリックします。  
  
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
  
##  <a name="bkmk_add_reportparameter"></a> レポート パラメーターを追加し、レポートを再パブリッシュ  
  
1.  **レポート データ** ペインで、 **[新規作成]** をクリックし、 **[パラメーター]** をクリックします。  
  
2.  **[名前]** に「 `OrderNumber`」と入力します。  
  
3.  **[プロンプト]** で、「 `OrderNumber`」と入力します。  
  
4.  **[空白の値 (" " ) を許可]** を選択します。  
  
5.  **[NULL 値を許可]** を選択します。  
  
6.  **[OK]** をクリックします。 次の図のように、パラメーターが **レポート データ ペイン** に追加されます。  
  
     ![レポート データ ペインに新しいパラメーターを追加](../../2014/tutorials/media/ssrs-tutorial-datadriven-parameter.gif "新しいパラメーター、レポート データ ペインに追加されます")  
  
7.  **[プレビュー]** タブをクリックしてレポートを実行します。レポート最上部のパラメーター入力ボックスに注意してください。 次のいずれかを実行できます。  
  
    -   [レポートの表示] をクリックして、パラメーターを使用しない完全なレポートを表示する。  
  
    -   Null オプションの選択を解除して注文番号を入力する。たとえば「so71949」と入力すると、レポートに注文が 1 つだけ表示されます。  
  
         ![パラメーター領域を表示、レポート ビューアー](../../2014/tutorials/media/ssrs-tutorial-datadriven-reportviewer-parameter.gif "パラメーター領域を表示、レポート ビューアー")  
  
8.  レポートを再配置して、このレッスンで適用した変更を、次のレッスンのサブスクリプション構成で利用できるようにします。 テーブルのチュートリアルで使用されるプロジェクト プロパティの詳細については、レポート サーバー (省略可能) に、レポートをパブリッシュ' するセクションを参照してください。 の[レッスン 6。グループと合計の追加 &#40;Reporting Services&#41;](../reporting-services/lesson-6-adding-grouping-and-totals-reporting-services.md)」を参照してください。  
  
##  <a name="bkmk_redeploy"></a> レポートを再配置するには  
  
1.  レポートを再配置して、このレッスンで適用した変更を、次のレッスンのサブスクリプション構成で利用できるようにします。 テーブルのチュートリアルで使用されるプロジェクト プロパティの詳細については、レポート サーバー (省略可能) に、レポートをパブリッシュ' するセクションを参照してください。 の[レッスン 6。グループと合計の追加 &#40;Reporting Services&#41;](../reporting-services/lesson-6-adding-grouping-and-totals-reporting-services.md)」を参照してください。  
  
2.  ツール バーの **[ビルド]** をクリックし、 **[Tutorial の配置]** をクリックします。  
  
## <a name="next-steps"></a>次の手順  
 保存されている資格情報を使用してデータを取得するレポートを構成しました。 次に、レポート マネージャーの [データ ドリブン サブスクリプション] ページを使用してサブスクリプションを指定します。 「[レッスン 3:データ ドリブン サブスクリプションを定義する](../reporting-services/lesson-3-defining-a-data-driven-subscription.md)します。  
  
## <a name="see-also"></a>参照  
 [レポート データ ソースを管理する](report-data/manage-report-data-sources.md)   
 [レポート データ ソースに関する資格情報と接続情報を指定する](report-data/specify-credential-and-connection-information-for-report-data-sources.md)   
 [データ ドリブン サブスクリプションの作成 &#40;SSRS チュートリアル&#41;](../reporting-services/create-a-data-driven-subscription-ssrs-tutorial.md)   
 [基本的なテーブル レポートの作成 (SSRS チュートリアル)](../reporting-services/create-a-basic-table-report-ssrs-tutorial.md)  
  
  
