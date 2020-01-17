---
title: ストアド プロシージャの依存関係の表示 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: stored-procedures
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- stored procedures [SQL Server], dependencies
- displaying stored procedure dependencies
- viewing stored procedure dependencies
ms.assetid: 6ae0a369-1bc7-4ae4-be89-2b483697cd1f
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 027373f9ff65d02c6bc2fb49079be3e1eda817bb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68050914"
---
# <a name="view-the-dependencies-of-a-stored-procedure"></a>ストアド プロシージャの依存関係の表示
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] または [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用して、 [!INCLUDE[tsql](../../includes/tsql-md.md)]でストアド プロシージャの依存関係を表示する方法について説明します。  
  
##  <a name="Top"></a>   
-   **作業を開始する準備:** [制限事項と制約事項](#Restrictions)、[セキュリティ](#Security)  
  
-   **プロシージャの依存関係の表示に使用するもの:** [SQL Server Management Studio](#SSMSProcedure)、[Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 システム関数: **sys.dm_sql_referencing_entities**  
 参照先エンティティに対する CONTROL 権限および sys.dm_sql_referencing_entities に対する SELECT 権限が必要です。 参照先エンティティがパーティション関数である場合、データベースに対する CONTROL 権限が必要です。 既定では、SELECT 権限が public に与えられます。  
  
 システム関数: **sys.dm_sql_referenced_entities**  
 sys.dm_sql_referenced_entities に対する SELECT 権限および参照元エンティティに対する VIEW DEFINITION 権限が必要です。 既定では、SELECT 権限が public に与えられます。 参照元エンティティがデータベース レベルの DDL トリガーである場合は、データベースに対する VIEW DEFINITION 権限またはデータベースに対する ALTER DATABASE DDL TRIGGER 権限が必要です。 参照元エンティティがサーバー レベルの DDL トリガーである場合は、サーバーに対する VIEW ANY DEFINITION 権限が必要です。  
  
 オブジェクト カタログ ビュー: **sys.sql_expression_dependencies**  
 データベースに対する VIEW DEFINITION 権限およびデータベースの sys.sql_expression_dependencies に対する SELECT 権限が必要です。 既定では、SELECT 権限は db_owner 固定データベース ロールのメンバーだけに与えられます。 SELECT 権限と VIEW DEFINITION 権限が別のユーザーに与えられている場合、権限が許可されているユーザーはデータベース内のすべての依存関係を表示できます。  
  
##  <a name="Procedures"></a> ストアド プロシージャの依存関係を表示する方法  
 次のいずれかを使用します。  
  
-   [SQL Server Management Studio](#SSMSProcedure)  
  
-   [Transact-SQL](#TsqlProcedure)  
  
###  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
 **オブジェクト エクスプローラーでプロシージャの依存関係を表示するには**  
  
1.  オブジェクト エクスプローラーで、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] に接続し、そのインスタンスを展開します。  
  
2.  **[データベース]** を展開し、プロシージャが属するデータベースを展開し、 **[プログラミング]** を展開します。  
  
3.  **[ストアド プロシージャ]** を展開し、プロシージャを右クリックして、 **[依存関係の表示]** をクリックします。  
  
4.  プロシージャに依存しているオブジェクトの一覧を表示します。  
  
5.  プロシージャが依存しているオブジェクトの一覧を表示します。  
  
6.  **[OK]** をクリックします。  
  
###  <a name="TsqlProcedure"></a> Transact-SQL の使用  
 **クエリ エディターでプロシージャの依存関係を表示するには**  
  
 システム関数: **sys.dm_sql_referencing_entities**  
 この関数は、プロシージャに依存しているオブジェクトを表示するために使用します。  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンスに接続し、そのインスタンスを展開します。  
  
2.  **[データベース]** を展開し、プロシージャが属するデータベースを展開します。  
  
3.  **[ファイル]** メニューの **[新しいクエリ]** をクリックします。  
  
4.  次の例をコピーし、クエリ エディターに貼り付けます。 最初の例では、 `uspVendorAllInfo` データベース内のすべてのベンダーの名前と、そのベンダーの提供製品、信用格付け、およびベンダーが現時点で製品を提供できるかどうかを返す [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] プロシージャが作成されます。  
  
    ```  
    USE AdventureWorks2008R2;  
    GO  
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
  
5.  このプロシージャの作成後、2 番目の例では、sys.dm_sql_referencing_entities 関数を使用して、プロシージャに依存しているオブジェクトを表示します。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT referencing_schema_name, referencing_entity_name, referencing_id, referencing_class_desc, is_caller_dependent  
    FROM sys.dm_sql_referencing_entities ('Purchasing.uspVendorAllInfo', 'OBJECT');   
    GO  
  
    ```  
  
 システム関数: **sys.dm_sql_referenced_entities**  
 この関数は、プロシージャが依存しているオブジェクトを表示するために使用します。  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンスに接続し、そのインスタンスを展開します。  
  
2.  **[データベース]** を展開し、プロシージャが属するデータベースを展開します。  
  
3.  **[ファイル]** メニューの **[新しいクエリ]** をクリックします。  
  
4.  次の例をコピーし、クエリ エディターに貼り付けます。 最初の例では、 `uspVendorAllInfo` データベース内のすべてのベンダーの名前と、そのベンダーの提供製品、信用格付け、およびベンダーが現時点で製品を提供できるかどうかを返す [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] プロシージャが作成されます。  
  
    ```  
    USE AdventureWorks2008R2;  
    GO  
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
  
5.  このプロシージャの作成後、2 番目の例では、sys.dm_sql_referenced_entities 関数を使用して、プロシージャが依存しているオブジェクトを表示します。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT referenced_schema_name, referenced_entity_name,  
    referenced_minor_name,referenced_minor_id, referenced_class_desc,  
    is_caller_dependent, is_ambiguous  
    FROM sys.dm_sql_referenced_entities ('Purchasing.uspVendorAllInfo', 'OBJECT');  
    GO  
    ```  
  
 オブジェクト カタログ ビュー: **sys.sql_expression_dependencies**  
 このビューを使用すると、プロシージャが依存しているオブジェクトまたはプロシージャに依存しているオブジェクトを表示できます。  
  
 プロシージャに依存しているオブジェクトを表示します。  
 1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンスに接続し、そのインスタンスを展開します。  
  
2.  **[データベース]** を展開し、プロシージャが属するデータベースを展開します。  
  
3.  **[ファイル]** メニューの **[新しいクエリ]** をクリックします。  
  
4.  次の例をコピーし、クエリ エディターに貼り付けます。 最初の例では、 `uspVendorAllInfo` データベース内のすべてのベンダーの名前と、そのベンダーの提供製品、信用格付け、およびベンダーが現時点で製品を提供できるかどうかを返す [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] プロシージャが作成されます。  
  
    ```  
    USE AdventureWorks2008R2;  
    GO  
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
  
5.  このプロシージャの作成後、2 番目の例では、sys.sql_expression_dependencies ビューを使用して、プロシージャに依存しているオブジェクトを表示します。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT OBJECT_SCHEMA_NAME ( referencing_id ) AS referencing_schema_name,  
        OBJECT_NAME(referencing_id) AS referencing_entity_name,   
        o.type_desc AS referencing_desciption,   
        COALESCE(COL_NAME(referencing_id, referencing_minor_id), '(n/a)') AS referencing_minor_id,   
        referencing_class_desc, referenced_class_desc,  
        referenced_server_name, referenced_database_name, referenced_schema_name,  
        referenced_entity_name,   
        COALESCE(COL_NAME(referenced_id, referenced_minor_id), '(n/a)') AS referenced_column_name,  
        is_caller_dependent, is_ambiguous  
    FROM sys.sql_expression_dependencies AS sed  
    INNER JOIN sys.objects AS o ON sed.referencing_id = o.object_id  
    WHERE referenced_id = OBJECT_ID(N'Purchasing.uspVendorAllInfo')  
    GO  
    ```  
  
 プロシージャが依存しているオブジェクトを表示します。  
 1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンスに接続し、そのインスタンスを展開します。  
  
2.  **[データベース]** を展開し、プロシージャが属するデータベースを展開します。  
  
3.  **[ファイル]** メニューの **[新しいクエリ]** をクリックします。  
  
4.  次の例をコピーし、クエリ エディターに貼り付けます。 最初の例では、 `uspVendorAllInfo` データベース内のすべてのベンダーの名前と、そのベンダーの提供製品、信用格付け、およびベンダーが現時点で製品を提供できるかどうかを返す [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] プロシージャが作成されます。  
  
    ```  
    USE AdventureWorks2008R2;  
    GO  
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
  
5.  このプロシージャの作成後、2 番目の例では、sys.sql_expression_dependencies ビューを使用して、プロシージャが依存しているオブジェクトを表示します。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT OBJECT_NAME(referencing_id) AS referencing_entity_name,   
        o.type_desc AS referencing_desciption,   
        COALESCE(COL_NAME(referencing_id, referencing_minor_id), '(n/a)') AS referencing_minor_id,   
        referencing_class_desc, referenced_class_desc,  
        referenced_server_name, referenced_database_name, referenced_schema_name,  
        referenced_entity_name,   
        COALESCE(COL_NAME(referenced_id, referenced_minor_id), '(n/a)') AS referenced_column_name,  
        is_caller_dependent, is_ambiguous  
    FROM sys.sql_expression_dependencies AS sed  
    INNER JOIN sys.objects AS o ON sed.referencing_id = o.object_id  
    WHERE referencing_id = OBJECT_ID(N'Purchasing.uspVendorAllInfo');  
    GO  
    ```  
  
## <a name="see-also"></a>参照  
 [ストアド プロシージャの名前の変更](../../relational-databases/stored-procedures/rename-a-stored-procedure.md)   
 [sys.dm_sql_referencing_entities &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referencing-entities-transact-sql.md)   
 [sys.dm_sql_referenced_entities &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql.md)   
 [sys.sql_expression_dependencies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)  
  
  
