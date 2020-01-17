---
title: ユーザー定義関数の変更 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: 891c37b3-cb72-411f-9937-ee87e6d95f34
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 77fbdc3bf2f579d585a802d5ed137cfe2a149c2b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68196451"
---
# <a name="modify-user-defined-functions"></a>ユーザー定義関数の変更
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] では、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../includes/tsql-md.md)]を使用してユーザー定義関数を変更できます。 以下に示す方法でユーザー定義関数を変更しても、関数の権限は変更されません。また、従属する関数、ストアド プロシージャ、またはトリガーにも影響はありません。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [Security](#Security)  
  
-   **ユーザー定義関数を変更する方法:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
 ALTER FUNCTION を使用して次の操作を実行することはできません。  
  
-   スカラー値関数をテーブル値関数に変更したり、その逆の変更を行ったりする  
  
-   インライン関数を複数ステートメント関数に変更したり、その逆の変更を行ったりする  
  
-   Transact-SQL 関数を CLR 関数に変更したり、その逆の変更を行ったりする  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 関数またはスキーマに対する ALTER 権限が必要です。 関数でユーザー定義型が指定されている場合は、その型に対する EXECUTE 権限が必要です。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-modify-a-user-defined-function"></a>ユーザー定義関数を変更するには  
  
1.  変更する関数を含むデータベースの横にあるプラス記号をクリックします。  
  
2.  **Programmability** フォルダーの横にあるプラス記号をクリックします。  
  
3.  変更する次の関数を含むフォルダーの横にあるプラス記号をクリックします。  
  
    -   Table-valued Function  
  
    -   スカラー値関数  
  
    -   集計関数  
  
4.  変更する関数を右クリックし、 **[変更]** を選択します。  
  
5.  クエリ ウィンドウで、ALTER FUNCTION ステートメントに必要な変更を加えます。  
  
6.  **ファイル** メニューの **function_name**_の保存_をクリックします。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-modify-a-user-defined-function"></a>ユーザー定義関数を変更するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```  
    -- Scalar-Valued Function  
    USE [AdventureWorks2012]  
    GO  
    ALTER FUNCTION [dbo].[ufnGetAccountingEndDate]()  
    RETURNS [datetime]   
    AS   
    BEGIN  
        RETURN DATEADD(millisecond, -2, CONVERT(datetime, '20040701', 112));  
    END;  
    ```  
  
    ```  
    -- Table-Valued Function   
    USE [AdventureWorks2012]  
    GO  
    ALTER FUNCTION [dbo].[ufnGetContactInformation](@PersonID int)  
    RETURNS @retContactInformation TABLE   
    (  
        -- Columns returned by the function  
        [PersonID] int NOT NULL,   
        [FirstName] [nvarchar](50) NULL,   
        [LastName] [nvarchar](50) NULL,   
        [JobTitle] [nvarchar](50) NULL,  
        [BusinessEntityType] [nvarchar](50) NULL  
    )  
    AS   
    -- Returns the first name, last name, job title and business entity type for the specified contact.  
    -- Since a contact can serve multiple roles, more than one row may be returned.  
    BEGIN  
    IF @PersonID IS NOT NULL   
    BEGIN  
         IF EXISTS(SELECT * FROM [HumanResources].[Employee] e   
         WHERE e.[BusinessEntityID] = @PersonID)   
         INSERT INTO @retContactInformation  
              SELECT @PersonID, p.FirstName, p.LastName, e.[JobTitle], 'Employee'  
              FROM [HumanResources].[Employee] AS e  
              INNER JOIN [Person].[Person] p ON p.[BusinessEntityID] = e.[BusinessEntityID]  
              WHERE e.[BusinessEntityID] = @PersonID;  
  
         IF EXISTS(SELECT * FROM [Purchasing].[Vendor] AS v  
         INNER JOIN [Person].[BusinessEntityContact] bec ON bec.[BusinessEntityID] = v.[BusinessEntityID]  
         WHERE bec.[PersonID] = @PersonID)  
         INSERT INTO @retContactInformation  
              SELECT @PersonID, p.FirstName, p.LastName, ct.[Name], 'Vendor Contact'   
              FROM [Purchasing].[Vendor] AS v  
              INNER JOIN [Person].[BusinessEntityContact] bec ON bec.[BusinessEntityID] = v.[BusinessEntityID]  
              INNER JOIN [Person].ContactType ct ON ct.[ContactTypeID] = bec.[ContactTypeID]  
              INNER JOIN [Person].[Person] p ON p.[BusinessEntityID] = bec.[PersonID]  
              WHERE bec.[PersonID] = @PersonID;  
  
         IF EXISTS(SELECT * FROM [Sales].[Store] AS s  
         INNER JOIN [Person].[BusinessEntityContact] bec ON bec.[BusinessEntityID] = s.[BusinessEntityID]  
         WHERE bec.[PersonID] = @PersonID)  
         INSERT INTO @retContactInformation  
              SELECT @PersonID, p.FirstName, p.LastName, ct.[Name], 'Store Contact'   
              FROM [Sales].[Store] AS s  
              INNER JOIN [Person].[BusinessEntityContact] bec ON bec.[BusinessEntityID] = s.[BusinessEntityID]  
              INNER JOIN [Person].ContactType ct ON ct.[ContactTypeID] = bec.[ContactTypeID]  
              INNER JOIN [Person].[Person] p ON p.[BusinessEntityID] = bec.[PersonID]  
              WHERE bec.[PersonID] = @PersonID;  
  
         IF EXISTS(SELECT * FROM [Person].[Person] AS p  
         INNER JOIN [Sales].[Customer] AS c ON c.[PersonID] = p.[BusinessEntityID]  
         WHERE p.[BusinessEntityID] = @PersonID AND c.[StoreID] IS NULL)   
         INSERT INTO @retContactInformation  
              SELECT @PersonID, p.FirstName, p.LastName, NULL, 'Consumer'   
              FROM [Person].[Person] AS p  
              INNER JOIN [Sales].[Customer] AS c ON c.[PersonID] = p.[BusinessEntityID]  
              WHERE p.[BusinessEntityID] = @PersonID AND c.[StoreID] IS NULL;   
         END  
    RETURN;  
    END;  
    ```  
  
 詳細については、「[ALTER FUNCTION &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-function-transact-sql)」を参照してください。  
  
  
