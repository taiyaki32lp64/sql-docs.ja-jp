---
title: プラン ガイドの有効化または無効化 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- plan guides [SQL Server], disabling
- enabling plan guides
- plan guides [SQL Server], enabling
- disabling plan guides
ms.assetid: b00ab550-5308-4cb8-8330-483cd1d25654
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 7c64bf641a6519c42ad0d3a8cdfd578458f84439
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63150921"
---
# <a name="enable-or-disable-a-plan-guide"></a>プラン ガイドの有効化または無効化
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] では、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../includes/tsql-md.md)]を使用して、プラン ガイドを無効化および有効化できます。 データベース内の 1 つのプラン ガイドまたはすべてのプラン ガイドを有効化または無効化できます。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [Security](#Security)  
  
-   **プラン ガイドの無効化または有効化に使用するもの:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   有効、無効にする場合のどちらでも、そのプラン ガイドで参照されている関数、ストアド プロシージャ、または DML トリガーを削除または変更しようとすると、エラーが発生します。 上記のいずれかのオブジェクトの削除または変更の前に、常に依存関係を確認してください。  
  
-   無効なプラン ガイドを無効にする場合や、有効なプラン ガイドを有効にする場合は影響は生じず、エラーなしで実行できます。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 OBJECT プラン ガイドの無効化または有効化には、プラン ガイドによって参照されるオブジェクト (関数、ストアド プロシージャなど) に対する ALTER 権限が必要です。 その他すべてのプラン ガイドでは、ALTER DATABASE 権限が必要です。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-disable-or-enable-a-plan-guide"></a>プラン ガイドを無効化または有効化するには  
  
1.  プラス記号をクリックして、無効化または有効化するプラン ガイドのあるデータベースを展開し、プラス記号をクリックして **[プログラミング]** フォルダーを展開します。  
  
2.  プラス記号をクリックして **[プラン ガイド]** フォルダーを展開します。  
  
3.  無効化または有効化するプラン ガイドを右クリックし、 **[無効化]** または **[有効化]** を選択します。  
  
4.  **[プラン ガイドの無効化]** または **[プラン ガイドの有効化]** ダイアログ ボックスで、選択した動作が成功したことを確認し、 **[閉じる]** をクリックします。  
  
#### <a name="to-disable-or-enable-all-plan-guides-in-a-database"></a>データベース内のすべてのプラン ガイドを無効化または有効化するには  
  
1.  プラス記号をクリックして、無効化または有効化するプラン ガイドのあるデータベースを展開し、プラス記号をクリックして **[プログラミング]** フォルダーを展開します。  
  
2.  **[プラン ガイド]** フォルダーを右クリックし、 **[すべて有効化]** または **[すべて無効化]** を選択します。  
  
3.  **[すべてのプラン ガイドを無効化]** または **[すべてのプラン ガイドを有効化]** ダイアログ ボックスで、選択した動作が成功したことを確認し、 **[閉じる]** をクリックします。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-disable-or-enable-a-plan-guide"></a>プラン ガイドを無効化または有効化するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```  
    --Create a procedure on which to define the plan guide.  
    IF OBJECT_ID(N'Sales.GetSalesOrderByCountry', N'P') IS NOT NULL  
        DROP PROCEDURE Sales.GetSalesOrderByCountry;  
    GO  
    CREATE PROCEDURE Sales.GetSalesOrderByCountry   
        (@Country nvarchar(60))  
    AS  
    BEGIN  
        SELECT *  
        FROM Sales.SalesOrderHeader AS h   
        INNER JOIN Sales.Customer AS c ON h.CustomerID = c.CustomerID  
        INNER JOIN Sales.SalesTerritory AS t ON c.TerritoryID = t.TerritoryID  
        WHERE t.CountryRegionCode = @Country;  
    END  
    GO  
    --Create the plan guide.  
    EXEC sp_create_plan_guide N'Guide3',  
        N'SELECT *  
        FROM Sales.SalesOrderHeader AS h   
        INNER JOIN Sales.Customer AS c ON h.CustomerID = c.CustomerID  
        INNER JOIN Sales.SalesTerritory AS t ON c.TerritoryID = t.TerritoryID  
        WHERE t.CountryRegionCode = @Country',  
        N'OBJECT',  
        N'Sales.GetSalesOrderByCountry',  
        NULL,  
        N'OPTION (OPTIMIZE FOR (@Country = N''US''))';  
    --Disable the plan guide.  
    EXEC sp_control_plan_guide N'DISABLE', N'Guide3';  
    GO  
    --Enable the plan guide.  
    EXEC sp_control_plan_guide N'ENABLE', N'Guide3';  
    GO  
  
    ```  
  
#### <a name="to-disable-or-enable-all-plan-guides-in-a-database"></a>データベース内のすべてのプラン ガイドを無効化または有効化するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```  
    --Disable all plan guides in the database.  
    EXEC sp_control_plan_guide N'DISABLE ALL';  
    GO  
    --Enable all plan guides in the database.  
    EXEC sp_control_plan_guide N'ENABLE ALL';  
    GO  
  
    ```  
  
 詳細については、「[sp_control_plan_guide &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-control-plan-guide-transact-sql)」を参照してください。  
  
  
