---
title: ユーザー定義関数の削除 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: db1d668a-23b7-4757-a9c5-1bd848ba7f6d
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: aa54440c5b1a506ce9c218dc7213383e0ff43ca0
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72906866"
---
# <a name="delete-user-defined-functions"></a>ユーザー定義関数の削除
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] では、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または  を使用してユーザー定義関数を削除できます。 [!INCLUDE[tsql](../../includes/tsql-md.md)]  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [セキュリティ](#Security)  
  
-   **ユーザー定義関数を削除するために使用するもの:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   データベース内に、この関数を参照し SCHEMABINDING を使って作成された Transact-SQL 関数またはビューがある場合、または、この関数を参照する計算列、CHECK 制約、DEFAULT 制約がある場合、関数は削除できません。  
  
-   この関数を参照し、インデックスが作成された計算列がある場合、関数の削除はできません。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 関数が属しているスキーマに対する ALTER 権限、または関数に対する CONTROL 権限が必要です。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-delete-a-user-defined-function"></a>ユーザー定義関数を削除するには  
  
1.  変更する関数を含むデータベースの横にあるプラス記号をクリックします。  
  
2.  **Programmability** フォルダーの横にあるプラス記号をクリックします。  
  
3.  変更する次の関数を含むフォルダーの横にあるプラス記号をクリックします。  
  
    -   Table-valued Function  
  
    -   スカラー値関数  
  
    -   集計関数  
  
4.  削除する関数を右クリックして、 **[削除]** をクリックします。  
  
5.  **[オブジェクトの削除]** ダイアログ ボックスで **[OK]** をクリックします。  

    > [!IMPORTANT]  
    >  **[オブジェクトの削除]** ダイアログ ボックスの **[依存関係の表示]** をクリックして **[_function\_name_ の依存関係]** ダイアログ ボックスを開きます。 関数に依存するすべてのオブジェクトと、関数が依存するすべてのオブジェクトが表示されます。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-delete-a-user-defined-function"></a>ユーザー定義関数を削除するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```  
    -- creates function called "Sales.ufn_SalesByStore"  
    USE AdventureWorks2012;  
    GO  
    CREATE FUNCTION Sales.ufn_SalesByStore (@storeid int)  
    RETURNS TABLE  
    AS  
    RETURN   
    (  
        SELECT P.ProductID, P.Name, SUM(SD.LineTotal) AS 'Total'  
        FROM Production.Product AS P   
        JOIN Sales.SalesOrderDetail AS SD ON SD.ProductID = P.ProductID  
        JOIN Sales.SalesOrderHeader AS SH ON SH.SalesOrderID = SD.SalesOrderID  
        JOIN Sales.Customer AS C ON SH.CustomerID = C.CustomerID  
        WHERE C.StoreID = @storeid  
        GROUP BY P.ProductID, P.Name  
    );  
    GO  
    ```  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- determines if function exists in database  
    IF OBJECT_ID (N'Sales.fn_SalesByStore', N'IF') IS NOT NULL  
    -- deletes function  
        DROP FUNCTION Sales.fn_SalesByStore;  
    GO  
    ```  
  
 詳細については、「[DROP FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-function-transact-sql.md)」を参照してください。  
  
  
