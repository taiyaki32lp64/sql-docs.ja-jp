---
title: ストアド プロシージャの作成 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.technology: stored-procedures
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- new stored procedures
- stored procedures [SQL Server], creating
- creating stored procedures
ms.assetid: 76e8a6ba-1381-4620-b356-4311e1331ca7
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9aa5518ee9ebcaca287b76636d6eeea8af2f4ea5
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/23/2019
ms.locfileid: "72796424"
---
# <a name="create-a-stored-procedure"></a>ストアド プロシージャの作成
  このトピックでは、 [!INCLUDE[tsql](../../includes/tsql-md.md)] および [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] の CREATE PROCEDURE ステートメントを使用して、 [!INCLUDE[tsql](../../includes/tsql-md.md)] ストアド プロシージャを作成する方法について説明します。  
  
##  <a name="Top"></a>   
-   **作業を開始する準備:**  [アクセス許可](#Permissions)  
  
-   **プロシージャの作成に使用するもの:**  [SQL Server Management Studio](#SSMSProcedure)、 [Transact-SQL](#TsqlProcedure)  
  
##  <a name="Permissions"></a> アクセス許可  
 データベースの CREATE PROCEDURE 権限と、プロシージャを作成するスキーマに対する ALTER 権限が必要です。  
  
##  <a name="Procedures"></a> ストアド プロシージャを作成する方法  
 次のいずれかを使用します。  
  
-   [SQL Server Management Studio](#SSMSProcedure)  
  
-   [Transact-SQL](#TsqlProcedure)  
  
###  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
 **オブジェクト エクスプローラーでプロシージャを作成するには**  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンスに接続し、そのインスタンスを展開します。  
  
2.  **[データベース]** を展開し、 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベースを展開して、 **[プログラミング]** を展開します。  
  
3.  **[ストアド プロシージャ]** を右クリックし、 **[新しいストアド プロシージャ]** をクリックします。  
  
4.  **[クエリ]** メニューの **[テンプレート パラメーターの値の指定]** をクリックします。  
  
5.  **[テンプレート パラメーターの値の指定]** ダイアログ ボックスで、各パラメーターに次の値を入力します。  
  
    |パラメーター|の値|  
    |---------------|-----------|  
    |Author|*名前*|  
    |Create Date|*今日の日付*|  
    |Description|従業員のデータが返されます。|  
    |[Procedure_name]|HumanResources.uspGetEmployeesTest|  
    |@Param1|@LastName|  
    |@Datatype_For_Param1|`nvarchar`(50)|  
    |[Default_Value_For_Param1]|NULL|  
    |@Param2|@FirstName|  
    |@Datatype_For_Param2|`nvarchar`(50)|  
    |[Default_Value_For_Param2]|NULL|  
  
6.  クリックして **OK**です。  
  
7.  **クエリ エディター**で、SELECT ステートメントを次のステートメントに置き換えます。  
  
    ```sql  
    SELECT FirstName, LastName, Department  
    FROM HumanResources.vEmployeeDepartmentHistory  
    WHERE FirstName = @FirstName AND LastName = @LastName  
        AND EndDate IS NULL;  
    ```  
  
8.  構文をテストするには、 **[クエリ]** メニューの **[解析]** をクリックします。 エラー メッセージが返された場合は、ステートメントと上記の情報を比較し、必要に応じて修正します。  
  
9. ストアド プロシージャを作成するには、 **[クエリ]** メニューの **[実行]** をクリックします。 プロシージャがデータベース内のオブジェクトとして作成されます。  
  
10. オブジェクト エクスプローラーにリストされたプロシージャを確認するには、 **[ストアド プロシージャ]** を右クリックして **[更新]** を選択します。  
  
11. プロシージャを実行するには、オブジェクト エクスプローラーでストアド プロシージャ名 **HumanResources.uspGetEmployeesTest** を右クリックし、 **[ストアド プロシージャの実行]** を選択します。  
  
12. **[プロシージャの実行]** ウィンドウでパラメーター @LastName の値に「Margheim」を、パラメーター @FirstName の値に「Diane」を入力します。  
  
> [!WARNING]  
>  すべてのユーザー入力を検証します。 ユーザー入力は検証するまで連結しないでください。 検証していないユーザー入力から作成されたコマンドは、絶対に実行しないでください。  
  
###  <a name="TsqlProcedure"></a> Transact-SQL の使用  
 **クエリ エディターでプロシージャを作成するには**  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  **[ファイル]** メニューの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。 この例では、上と同じストアド プロシージャを別のプロシージャ名で作成します。  
  
    ```sql
    USE AdventureWorks2012;  
    GO  
    CREATE PROCEDURE HumanResources.uspGetEmployeesTest2   
        @LastName nvarchar(50),   
        @FirstName nvarchar(50)   
    AS
  
        SET NOCOUNT ON;  
        SELECT FirstName, LastName, Department  
        FROM HumanResources.vEmployeeDepartmentHistory  
        WHERE FirstName = @FirstName AND LastName = @LastName  
        AND EndDate IS NULL;  
    GO
    ```  
  
4.  プロシージャを実行するには、次の例をコピーして新しいクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。 パラメーター値を指定するときに別の方法が表示されることに注意してください。  
  
    ```sql
    EXECUTE HumanResources.uspGetEmployeesTest2 N'Ackerman', N'Pilar';  
    -- Or  
    EXEC HumanResources.uspGetEmployeesTest2 @LastName = N'Ackerman', @FirstName = N'Pilar';  
    GO  
    -- Or  
    EXECUTE HumanResources.uspGetEmployeesTest2 @FirstName = N'Pilar', @LastName = N'Ackerman';  
    GO
    ```  
  
## <a name="see-also"></a>「  
 [CREATE PROCEDURE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-procedure-transact-sql)  
  