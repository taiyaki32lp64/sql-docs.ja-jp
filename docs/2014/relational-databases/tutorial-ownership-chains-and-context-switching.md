---
title: チュートリアル:所有権の継承とコンテキストの切り替え |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- context switching [SQL Server], tutorials
- ownership chains [SQL Server]
ms.assetid: db5d4cc3-5fc5-4cf5-afc1-8d4edc1d512b
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 1ae566345f722399982c909244e77c564abb7b53
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62524368"
---
# <a name="tutorial-ownership-chains-and-context-switching"></a>チュートリアル:所有権の継承とコンテキストの切り替え
  このチュートリアルでは、1 つのシナリオを使用して、所有権の継承とユーザー コンテキストの切り替えに関係する [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のセキュリティ概念について説明します。  
  
> [!NOTE]  
>  このチュートリアルのコードを実行するには、混合モードのセキュリティが構成されていることと、 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] データベースがインストールされていることが条件となります。 混合モードのセキュリティの詳細については、「 [認証モードの選択](security/choose-an-authentication-mode.md)」を参照してください。  
  
## <a name="scenario"></a>シナリオ  
 このシナリオでは、2 人のユーザーが、 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] データベースに格納されている購買発注データにアクセスするためのアカウントを必要としていることを想定します。 要件は次のとおりです。  
  
-   最初のアカウント (TestManagerUser) では、すべての購買注文のすべての詳細を確認できる必要があります。  
  
-   2 番目のアカウント (TestEmployeeUser) では、配送の一部が受領された場合の品目に関して、発注番号、発注日、出荷日、製品 ID 番号、発注品目数と受領品目数を、購買注文ごとに発注番号で確認できる必要があります。  
  
-   他のすべてのアカウントでは、各自の現在の権限を保持する必要があります。  
  
 このシナリオの要件を満たすため、ここでは例を次のように 4 分割して、所有権の継承とコンテキストの切り替えの各概念を示します。  
  
1.  環境を構成する。  
  
2.  購買注文によってデータにアクセスするストアド プロシージャを作成する。  
  
3.  ストアド プロシージャからデータにアクセスする。  
  
4.  環境をリセットする。  
  
 以下で、この例の各コード ブロックについて説明します。 完全なサンプル コードをコピーするには、このチュートリアルの最後の「 [完全なサンプル コード](#CompleteExample) 」を参照してください。  
  
## <a name="1-configure-the-environment"></a>1.環境を構成する  
 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] と次のコードを使用して `AdventureWorks2012` データベースを開き、`CURRENT_USER` [!INCLUDE[tsql](../includes/tsql-md.md)] ステートメントを使用して、dbo ユーザーがコンテキストとして表示されていることを確認します。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT CURRENT_USER AS 'Current User Name';  
GO  
```  
  
 CURRENT_USER ステートメントの詳細については、「[CURRENT_USER (Transact-SQL)](/sql/t-sql/functions/current-user-transact-sql)」を参照してください。  
  
 次のコードを dbo ユーザーとして実行し、サーバー上と [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] データベース内に 2 ユーザーを作成します。  
  
```  
CREATE LOGIN TestManagerUser   
    WITH PASSWORD = '340$Uuxwp7Mcxo7Khx';  
GO  
CREATE USER TestManagerUser   
   FOR LOGIN TestManagerUser  
   WITH DEFAULT_SCHEMA = Purchasing;  
GO   
  
CREATE LOGIN TestEmployeeUser  
    WITH PASSWORD = '340$Uuxwp7Mcxo7Khy';  
GO  
CREATE USER TestEmployeeUser   
   FOR LOGIN TestEmployeeUser;  
GO   
```  
  
 CREATE_USER ステートメントの詳細については、「[CREATE USER (Transact-SQL)](/sql/t-sql/statements/create-user-transact-sql)」を参照してください。 CREATE_LOGIN ステートメントの詳細については、「[CREATE LOGIN (Transact-SQL)](/sql/t-sql/statements/create-login-transact-sql)」を参照してください。  
  
 次のコードを実行し、 `Purchasing` スキーマの所有権を `TestManagerUser` アカウントに変更します。 所有権を与えられたアカウントでは、 `SELECT` 権限や `INSERT` 権限などすべてのデータ操作言語 (DML) のアクセス権限を、中のオブジェクトに対し使用できます。 `TestManagerUser` にもストアド プロシージャを作成する権限が付与されます。  
  
```  
/* Change owner of the Purchasing Schema to TestManagerUser */  
ALTER AUTHORIZATION   
   ON SCHEMA::Purchasing   
   TO TestManagerUser;  
GO  
  
GRANT CREATE PROCEDURE   
   TO TestManagerUser   
   WITH GRANT OPTION;  
GO  
```  
  
 GRANT ステートメントの詳細については、「[GRANT (Transact-SQL)](/sql/t-sql/statements/grant-transact-sql)」を参照してください。 ストアド プロシージャの詳細については、「[ストアド プロシージャ (データベース エンジン)](stored-procedures/stored-procedures-database-engine.md)」を参照してください。 [!INCLUDE[ssDE](../includes/ssde-md.md)] のすべてのアクセス許可を示したポスターについては、[https://go.microsoft.com/fwlink/?LinkId=229142](https://go.microsoft.com/fwlink/?LinkId=229142) を参照してください。  
  
## <a name="2-create-a-stored-procedure-to-access-data"></a>2.データにアクセスするストアド プロシージャを作成する  
 データベース内でコンテキストを切り替えるには、EXECUTE AS ステートメントを使用します。 EXECUTE AS を使用するには IMPERSONATE 権限が必要です。  
  
 次のコードでは、 `EXECUTE AS` ステートメントによりコンテキストを `TestManagerUser` に変更し、 `TestEmployeeUser`に必要とされるデータのみを表示するストアド プロシージャを作成します。 要件を満たすには、ストアド プロシージャでは発注番号を表す変数を 1 つ受け取ります。財務情報は表示せず、WHERE 句によって結果を一部配送のみに限定します。  
  
```  
EXECUTE AS LOGIN = 'TestManagerUser'  
GO  
SELECT CURRENT_USER AS 'Current User Name';  
GO  
  
/* Note: The user that calls the EXECUTE AS statement must have IMPERSONATE permissions on the target principal */  
CREATE PROCEDURE usp_ShowWaitingItems @ProductID int  
AS  
BEGIN   
   SELECT a.PurchaseOrderID, a.OrderDate, a.ShipDate  
      , b.ProductID, b.OrderQty, b.ReceivedQty  
   FROM Purchasing.PurchaseOrderHeader a  
      INNER JOIN Purchasing.PurchaseOrderDetail b  
         ON a.PurchaseOrderID = b.PurchaseOrderID  
   WHERE b.OrderQty > b.ReceivedQty  
      AND @ProductID = b.ProductID  
   ORDER BY b.ProductID ASC  
END  
GO  
```  
  
 この時点では、 `TestEmployeeUser` はどのデータベース オブジェクトにもアクセスできません。 コンテキストは引き続き `TestManagerUser` です。次のコードを実行し、ストアド プロシージャを介して  ユーザー アカウントがベース テーブル情報をクエリできるようにします。  
  
```  
GRANT EXECUTE  
   ON OBJECT::Purchasing.usp_ShowWaitingItems  
   TO TestEmployeeUser;  
GO  
```  
  
 `Purchasing` は既定では `TestManagerUser` スキーマに割り当てられるため、スキーマが明示的に指定されていない場合でも、ストアド プロシージャは `Purchasing` スキーマの一部です。 次のコードに示すように、システム カタログ情報を使用してオブジェクトを特定できます。  
  
```  
SELECT a.name AS 'Schema'  
   , b.name AS 'Object Name'  
   , b.type AS 'Object Type'  
FROM sys.schemas a  
   INNER JOIN sys.objects b  
      ON a.schema_id = b.schema_id   
WHERE b.name = 'usp_ShowWaitingItems';  
GO  
```  
  
 例のこの部分が完了すると、コードでは `REVERT` ステートメントによってコンテキストが切り替えられ、コンテキストは dbo に戻ります。  
  
```  
REVERT;  
GO  
```  
  
 REVERT ステートメントの詳細については、「[REVERT (Transact-SQL)](/sql/t-sql/statements/revert-transact-sql)」 を参照してください。  
  
## <a name="3-access-data-through-the-stored-procedure"></a>3.ストアド プロシージャからデータにアクセスする  
 `TestEmployeeUser` は、 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] データベースのオブジェクトに対し、ログイン権限と public データベース ロールに割り当てられた権限だけを持ちます。 `TestEmployeeUser` がベース テーブルにアクセスしようとすると、次のコードによりエラーが返されます。  
  
```  
EXECUTE AS LOGIN = 'TestEmployeeUser'  
GO  
SELECT CURRENT_USER AS 'Current User Name';  
GO  
/* This won't work */  
SELECT *  
FROM Purchasing.PurchaseOrderHeader;  
GO  
SELECT *  
FROM Purchasing.PurchaseOrderDetail;  
GO  
```  
  
 前のセクションで作成したストアド プロシージャで参照されるオブジェクトは、 `TestManagerUser` スキーマの所有権により `Purchasing` の所有となります。したがって、 `TestEmployeeUser` はストアド プロシージャを介してベース テーブルにアクセスできます。 次のコードでは、引き続き `TestEmployeeUser` をコンテキストとし、購買注文 952 をパラメーターとして渡します。  
  
```  
EXEC Purchasing.usp_ShowWaitingItems 952  
GO  
```  
  
## <a name="4-reset-the-environment"></a>4.環境をリセットする  
 次のコードでは、 `REVERT` コマンドにより現在のアカウントのコンテキストを `dbo`に戻し、環境をリセットします。  
  
```  
REVERT;  
GO  
ALTER AUTHORIZATION   
ON SCHEMA::Purchasing TO dbo;  
GO  
DROP PROCEDURE Purchasing.usp_ShowWaitingItems;  
GO  
DROP USER TestEmployeeUser;  
GO  
DROP USER TestManagerUser;  
GO  
DROP LOGIN TestEmployeeUser;  
GO  
DROP LOGIN TestManagerUser;  
GO  
```  
  
##  <a name="CompleteExample"></a> 完全な例  
 次に、完全なサンプル コードを示します。  
  
> [!NOTE]  
>  `TestEmployeeUser` はベース テーブルから選択することができないため、2 つのエラーが発生することが予測されますが、このコードには含まれていません。  
  
```  
/*   
Script:       UserContextTutorial.sql  
Author:       Microsoft  
Last Updated: Books Online  
Conditions:   Execute as DBO or sysadmin in the AdventureWorks database  
Section 1:    Configure the Environment   
*/  
USE AdventureWorks2012;  
GO  
SELECT CURRENT_USER AS 'Current User Name';  
GO  
/* Create server and database users */  
CREATE LOGIN TestManagerUser   
    WITH PASSWORD = '340$Uuxwp7Mcxo7Khx';  
  
GO  
  
CREATE USER TestManagerUser   
   FOR LOGIN TestManagerUser  
   WITH DEFAULT_SCHEMA = Purchasing;  
GO   
  
CREATE LOGIN TestEmployeeUser  
    WITH PASSWORD = '340$Uuxwp7Mcxo7Khy';  
GO  
CREATE USER TestEmployeeUser   
   FOR LOGIN TestEmployeeUser;  
GO   
  
/* Change owner of the Purchasing Schema to TestManagerUser */  
ALTER AUTHORIZATION   
   ON SCHEMA::Purchasing   
   TO TestManagerUser;  
GO  
  
GRANT CREATE PROCEDURE   
   TO TestManagerUser   
   WITH GRANT OPTION;  
GO  
  
/*   
Section 2: Switch Context and Create Objects  
*/  
EXECUTE AS LOGIN = 'TestManagerUser';  
GO  
SELECT CURRENT_USER AS 'Current User Name';  
GO  
  
/* Note: The user that calls the EXECUTE AS statement must have IMPERSONATE permissions on the target principal */  
CREATE PROCEDURE usp_ShowWaitingItems @ProductID int  
AS  
BEGIN   
   SELECT a.PurchaseOrderID, a.OrderDate, a.ShipDate  
      , b.ProductID, b.OrderQty, b.ReceivedQty  
   FROM Purchasing.PurchaseOrderHeader AS a  
      INNER JOIN Purchasing.PurchaseOrderDetail AS b  
         ON a.PurchaseOrderID = b.PurchaseOrderID  
   WHERE b.OrderQty > b.ReceivedQty  
      AND @ProductID = b.ProductID  
   ORDER BY b.ProductID ASC  
END;  
GO  
  
/* Give the employee the ability to run the procedure */  
GRANT EXECUTE   
   ON OBJECT::Purchasing.usp_ShowWaitingItems  
   TO TestEmployeeUser;  
GO   
  
/* Notice that the stored procedure is located in the Purchasing   
schema. This also demonstrates system catalogs */  
SELECT a.name AS 'Schema'  
   , b.name AS 'Object Name'  
   , b.type AS 'Object Type'  
FROM sys.schemas AS a  
   INNER JOIN sys.objects AS b  
      ON a.schema_id = b.schema_id   
WHERE b.name = 'usp_ShowWaitingItems';  
GO  
  
/* Go back to being the dbo user */  
REVERT;  
GO  
  
/*  
Section 3: Switch Context and Observe Security   
*/  
EXECUTE AS LOGIN = 'TestEmployeeUser';  
GO  
SELECT CURRENT_USER AS 'Current User Name';  
GO  
EXEC Purchasing.usp_ShowWaitingItems 952;  
GO  
  
/*   
Section 4: Clean Up Example  
*/  
REVERT;  
GO  
ALTER AUTHORIZATION   
ON SCHEMA::Purchasing TO dbo;  
GO  
DROP PROCEDURE Purchasing.usp_ShowWaitingItems;  
GO  
DROP USER TestEmployeeUser;  
GO  
DROP USER TestManagerUser;  
GO  
DROP LOGIN TestEmployeeUser;  
GO  
DROP LOGIN TestManagerUser;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [SQL Server データベース エンジンと Azure SQL Database のセキュリティ センター](security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)  
  
  
