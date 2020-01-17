---
title: ストアド プロシージャの変更 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: conceptual
helpviewer_keywords:
- modifying stored procedures
- editing stored procedures
- stored procedures [SQL Server], modifying
ms.assetid: 13396239-6100-48ce-aa34-461358d99c92
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 810dfbc7230171f59cb8f1df04ab1c7f4774e044
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72907243"
---
# <a name="modify-a-stored-procedure"></a>ストアド プロシージャの変更
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
    
##  <a name="Top"></a> このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] または [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用して、 [!INCLUDE[tsql](../../includes/tsql-md.md)]でストアド プロシージャを変更する方法について説明します。  
  
-   **作業を開始する準備:** [制限事項と制約事項](#Restrictions)、[セキュリティ](#Security)  
  
-   **プロシージャを変更するには次を使用します:** [SQL Server Management Studio](#SSMSProcedure)、[Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] ストアド プロシージャを CLR ストアド プロシージャに変更したり、その逆に変更することはできません。  
  
 以前のプロシージャ定義が WITH ENCRYPTION または WITH RECOMPILE を使用して作成されている場合、これらのオプションは、ALTER PROCEDURE ステートメントに指定されるときだけ有効になります。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 プロシージャに対する ALTER PROCEDURE 権限が必要です。  
  
##  <a name="Procedures"></a> ストアド プロシージャを変更する方法  
 次のいずれかを使用します。  
  
-   [SQL Server Management Studio](#SSMSProcedure)  
  
-   [Transact-SQL](#TsqlProcedure)  
  
###  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
 **Management Studio でプロシージャを変更するには**  
  
1.  オブジェクト エクスプローラーで、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンスに接続し、そのインスタンスを展開します。  
  
2.  **[データベース]** を展開し、プロシージャが属するデータベースを展開し、 **[プログラミング]** を展開します。  
  
3.  **[ストアド プロシージャ]** を展開し、変更するプロシージャを右クリックして、 **[変更]** をクリックします。  
  
4.  ストアド プロシージャのテキストを変更します。  
  
5.  構文をテストするには、 **[クエリ]** メニューの **[解析]** をクリックします。  
  
6.  変更をプロシージャの定義に保存するには、 **[クエリ]** メニューの **[実行]** をクリックします。  
  
7.  更新されたプロシージャの定義を [!INCLUDE[tsql](../../includes/tsql-md.md)] スクリプトとして保存するには、 **[ファイル]** メニューの **[名前を付けて保存]** をクリックします。 ファイル名をそのまま使用するか、または別の名前を入力し、 **[保存]** をクリックします。  

> [!IMPORTANT]  
>  すべてのユーザー入力を検証します。 ユーザー入力は検証するまで連結しないでください。 検証していないユーザー入力から作成されたコマンドは、絶対に実行しないでください。  
  
###  <a name="TsqlProcedure"></a> Transact-SQL の使用  
 **クエリ エディターでプロシージャを変更するには**  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンスに接続し、そのインスタンスを展開します。  
  
2.  **[データベース]** を展開し、プロシージャが属するデータベースを展開します。 または、ツール バーの利用可能なデータベースの一覧からデータベースを選択します。 この例では [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベースを選択します。  
  
3.  **[ファイル]** メニューの **[新しいクエリ]** をクリックします。  
  
4.  次の例をコピーし、クエリ エディターに貼り付けます。 この例では、 `uspVendorAllInfo` データベース内のすべてのベンダーの名前と、そのベンダーの提供製品、信用格付け、およびベンダーが現時点で製品を提供できるかどうかを返す [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] プロシージャが作成されます。  
  
    ```  
  
    IF OBJECT_ID ( 'Purchasing.uspVendorAllInfo', 'P' ) IS NOT NULL   
        DROP PROCEDURE Purchasing.uspVendorAllInfo;  
    GO  
    CREATE PROCEDURE Purchasing.uspVendorAllInfo  
    WITH EXECUTE AS CALLER  
    AS  
        SET NOCOUNT ON;  
        SELECT v.Name AS Vendor, p.Name AS 'Product name',   
          v.CreditRating AS 'Rating',   
          v.ActiveFlag AS Availability  
        FROM Purchasing.Vendor v   
        INNER JOIN Purchasing.ProductVendor pv  
          ON v.BusinessEntityID = pv.BusinessEntityID   
        INNER JOIN Production.Product p  
          ON pv.ProductID = p.ProductID   
        ORDER BY v.Name ASC;  
    GO  
  
    ```  
  
5.  **[ファイル]** メニューの **[新しいクエリ]** をクリックします。  
  
6.  次の例をコピーし、クエリ エディターに貼り付けます。 この例では、 `uspVendorAllInfo` プロシージャが変更されます。 EXECUTE AS CALLER 句が削除され、指定した製品を供給するベンダーだけを返すようにプロシージャの本体が変更されます。 ここでは、 `LEFT` 関数および `CASE` 関数を使用して、結果セットの表示をカスタマイズします。  
  
    ```  
    ALTER PROCEDURE Purchasing.uspVendorAllInfo  
        @Product varchar(25)   
    AS  
        SET NOCOUNT ON;  
        SELECT LEFT(v.Name, 25) AS Vendor, LEFT(p.Name, 25) AS 'Product name',   
        'Rating' = CASE v.CreditRating   
            WHEN 1 THEN 'Superior'  
            WHEN 2 THEN 'Excellent'  
            WHEN 3 THEN 'Above average'  
            WHEN 4 THEN 'Average'  
            WHEN 5 THEN 'Below average'  
            ELSE 'No rating'  
            END  
        , Availability = CASE v.ActiveFlag  
            WHEN 1 THEN 'Yes'  
            ELSE 'No'  
            END  
        FROM Purchasing.Vendor AS v   
        INNER JOIN Purchasing.ProductVendor AS pv  
          ON v.BusinessEntityID = pv.BusinessEntityID   
        INNER JOIN Production.Product AS p   
          ON pv.ProductID = p.ProductID   
        WHERE p.Name LIKE @Product  
        ORDER BY v.Name ASC;  
    GO  
  
    ```  
  
7.  変更をプロシージャの定義に保存するには、 **[クエリ]** メニューの **[実行]** をクリックします。  
  
8.  更新されたプロシージャの定義を [!INCLUDE[tsql](../../includes/tsql-md.md)] スクリプトとして保存するには、 **[ファイル]** メニューの **[名前を付けて保存]** をクリックします。 ファイル名をそのまま使用するか、または別の名前を入力し、 **[保存]** をクリックします。  
  
9. 変更したストアド プロシージャを実行するには、次の例を実行します。  
  
    ```  
    EXEC Purchasing.uspVendorAllInfo N'LL Crankarm';  
    GO  
  
    ```  
  
## <a name="see-also"></a>参照  
 [ALTER PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-procedure-transact-sql.md)  
  
  
