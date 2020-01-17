---
title: レッスン 11:パーティションの作成 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 92eb21a8-5fc4-4999-ad37-1332ce26431d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 06ffe60802e52bd0ae141435628fc3812dc2c7c6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66079200"
---
# <a name="lesson-11-create-partitions"></a>レッスン 11:パーティションの作成
  このレッスンでは、パーティションを作成して Internet Sales テーブルをより小さな論理部分に分割し、他のパーティションと分離して処理 (更新) できるようにします。 既定では、すべてのテーブル モデルに含めることは、すべてのテーブルの列と行が含まれる 1 つのパーティションを持っています。 Internet Sales テーブルの年間でデータを分割します。各テーブルの 5 年間の 1 つのパーティション。  これにより、各パーティションを個別に処理できるようにします。 詳細については、「[パーティション (SSAS テーブル)](tabular-models/partitions-ssas-tabular.md)」を参照してください。  
  
 このレッスンを完了するまでに時間を推定するには。**15 分**  
  
## <a name="prerequisites"></a>前提条件  
 このトピックはテーブル モデリング チュートリアルの一部であり、チュートリアルでの順番に従って実行する必要があります。 このレッスンでは、タスクを実行する前に、前のレッスンを完了が必要があります。[レッスン 10:階層を作成する](lesson-9-create-hierarchies.md)します。  
  
## <a name="create-partitions"></a>パーティションの作成  
  
#### <a name="to-create-partitions-in-the-internet-sales-table"></a>Internet Sales テーブル内にパーティションを作成するには  
  
1.  モデル デザイナーで **[Internet Sales]** テーブルをクリックし、 **[テーブル]** メニュー、 **[パーティション]** の順にクリックします。  
  
     **[パーティション マネージャー]** ダイアログ ボックスが表示されます。  
  
2.  **Partition Manager**  ダイアログ ボックスで**パーティション**、クリックして、 **Internet Sales**パーティション。  
  
3.  **パーティション名**、名を変更して`Internet Sales 2005`します。  
  
    > [!TIP]  
    >  次の手順に進む前に、[テーブルのプレビュー] ウィンドウの列名が、モデル テーブル (チェックされている) に含まれている列を、ソースの列名で表示していることに注意してください。 これは、[テーブルのプレビュー] ウィンドウでは、モデル テーブルからではなく、ソース テーブルから取得された列が表示されるためです。  
  
4.  プレビュー ウィンドウの右上にある **[クエリ エディター]** ボタンを選択します。  
  
     特定の期間内の行だけをパーティションに含めたいので、WHERE 句を含める必要があります。 WHERE 句は、SQL ステートメントによってのみ作成できます。  
  
5.  **[SQL ステートメント]** フィールドで、次のステートメントを貼り付けて既存のステートメントを置き換えます。  
  
    ```  
    SELECT   
    [dbo].[FactInternetSales].[ProductKey],  
    [dbo].[FactInternetSales].[CustomerKey],  
    [dbo].[FactInternetSales].[PromotionKey],  
    [dbo].[FactInternetSales].[CurrencyKey],  
    [dbo].[FactInternetSales].[SalesTerritoryKey],  
    [dbo].[FactInternetSales].[SalesOrderNumber],  
    [dbo].[FactInternetSales].[SalesOrderLineNumber],  
    [dbo].[FactInternetSales].[RevisionNumber],  
    [dbo].[FactInternetSales].[OrderQuantity],  
    [dbo].[FactInternetSales].[UnitPrice],  
    [dbo].[FactInternetSales].[ExtendedAmount],  
    [dbo].[FactInternetSales].[UnitPriceDiscountPct],  
    [dbo].[FactInternetSales].[DiscountAmount],  
    [dbo].[FactInternetSales].[ProductStandardCost],  
    [dbo].[FactInternetSales].[TotalProductCost],  
    [dbo].[FactInternetSales].[SalesAmount],  
    [dbo].[FactInternetSales].[TaxAmt],  
    [dbo].[FactInternetSales].[Freight],  
    [dbo].[FactInternetSales].[CarrierTrackingNumber],  
    [dbo].[FactInternetSales].[CustomerPONumber],  
    [dbo].[FactInternetSales].[OrderDate],  
    [dbo].[FactInternetSales].[DueDate],  
    [dbo].[FactInternetSales].[ShipDate]   
    FROM [dbo].[FactInternetSales]  
    WHERE (([OrderDate] >= N'2005-01-01 00:00:00') AND ([OrderDate] < N'2006-01-01 00:00:00'))  
    ```  
  
     このステートメントは、WHERE 句で指定されているように、OrderDate が 2005 年度に該当する行のすべてのデータをパーティションに含めるよう指定しています。  
  
6.  **[検証]** をクリックします。  
  
     特定の列がソースに存在しないことを示す警告が表示されます。 これは、ために[レッスン 3。列名の変更](rename-columns.md)ソースにある同じ列に異なるモデルでの Internet Sales テーブル内のそれらの列の名前を変更します。  
  
#### <a name="to-create-a-partition-for-the-2006-year-in-the-internet-sales-table"></a>Internet Sales テーブル内に、2006 年のパーティションを作成するには  
  
1.  **Partition Manager**  ダイアログ ボックスで**パーティション**、 をクリックして、`Internet Sales 2005`パーティションを作成したし**コピー**します。  
  
2.  **パーティション名**、型`Internet Sales 2006`します。  
  
3.  SQL ステートメントを同じ順序がパーティションに、2006 年の行だけを含めるには、次のように WHERE 句を置き換えます。  
  
    ```  
    WHERE (([OrderDate] >= N'2006-01-01 00:00:00') AND ([OrderDate] < N'2007-01-01 00:00:00'))  
    ```  
  
#### <a name="to-create-a-partition-for-the-2007-year-in-the-internet-sales-table"></a>Internet Sales テーブル内に、2007 年のパーティションを作成するには  
  
1.  **[パーティション マネージャー]** ダイアログ ボックスで **[コピー]** をクリックします。  
  
2.  **パーティション名**、型`Internet Sales 2007`します。  
  
3.  **切り替え先**、**クエリ エディター**します。  
  
4.  SQL ステートメントを同じ順序がパーティションに、2007 年の行だけを含めるには、次のように WHERE 句を置き換えます。  
  
    ```  
    WHERE (([OrderDate] >= N'2007-01-01 00:00:00') AND ([OrderDate] < N'2008-01-01 00:00:00'))  
    ```  
  
#### <a name="to-create-a-partition-for-the-2008-year-in-the-internet-sales-table"></a>Internet Sales テーブル内に、2008 年のパーティションを作成するには  
  
1.  **[パーティション マネージャー]** ダイアログ ボックスで **[新規]** をクリックします。  
  
2.  **パーティション名**、型`Internet Sales 2008`します。  
  
3.  **切り替え先**、**クエリ エディター**します。  
  
4.  SQL ステートメントを同じ順序がパーティションに、2008 年の行だけを含めるには、次のように WHERE 句を置き換えます。  
  
    ```  
    WHERE (([OrderDate] >= N'2008-01-01 00:00:00') AND ([OrderDate] < N'2009-01-01 00:00:00'))  
    ```  
  
#### <a name="to-create-a-partition-for-the-2009-year-in-the-internet-sales-table"></a>Internet Sales テーブル内に 2009 年用のパーティションを作成するには  
  
1.  **[パーティション マネージャー]** ダイアログ ボックスで **[新規]** をクリックします。  
  
2.  **パーティション名**、型`Internet Sales 2009`します。  
  
3.  **切り替え先**、**クエリ エディター**します。  
  
4.  SQL ステートメントで、WHERE 句を次の内容に置き換えて、2009 年の行だけがパーティションに含まれるようにします。  
  
    ```  
    WHERE (([OrderDate] >= N'2009-01-01 00:00:00') AND ([OrderDate] < N'2010-01-01 00:00:00'))  
    ```  
  
## <a name="process-partitions"></a>パーティションの処理  
 **[パーティション マネージャー]** ダイアログ ボックスで、新たに作成した各パーティションのパーティション名の隣にアスタリスク ( **\*** ) が表示されます。 これは、パーティションがまだ処理 (更新) されていないことを示します。 新しいパーティションを作成したら、"パーティションの処理" または "テーブルの処理" 操作を実行して、それらのパーティション内のデータを更新する必要があります。  
  
#### <a name="to-process-internet-sales-partitions"></a>Internet Sales パーティションを処理するには  
  
1.  **[OK]** をクリックし、 **[パーティション マネージャー]** ダイアログ ボックスを閉じます。  
  
2.  モデル デザイナーで **[Internet Sales]** テーブルをクリックし、 **[モデル]** メニューをクリックした後、 **[処理]** (更新) をポイントし、 **[パーティションの処理]** をクリックします。  
  
3.  **[パーティションの処理]** ダイアログ ボックスで、 **[モード]** が **[既定の処理]** に設定されていることを確認します。  
  
4.  作成した 5 つのパーティションのそれぞれについて、 **[処理]** 列のチェック ボックスをオンにし、 **[OK]** をクリックします。  
  
     権限借用資格情報の入力を求められた場合は、レッスン 2 の手順 6. で指定した、Windows のユーザー名とパスワードを入力します。  
  
     **データ プロセス** ダイアログ ボックスが表示され、各パーティションのプロセスの詳細が表示されます。 転送される行数はパーティションごとに異なります。 これは、各パーティションに、SQL ステートメントの WHERE 句で指定された年の行が含められるためです。 2010 年についてはデータがありません。  
  
## <a name="next-steps"></a>次の手順  
 このチュートリアルを続行するには、次のレッスンに移動します。レッスン:[レッスン 12:ロールを作成](lesson-11-create-roles.md)です。  
  
  
