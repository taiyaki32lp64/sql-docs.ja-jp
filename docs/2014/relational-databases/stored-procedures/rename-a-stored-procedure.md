---
title: ストアド プロシージャの名前の変更 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.technology: stored-procedures
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- stored procedures [SQL Server], renaming
- renaming stored procedures
ms.assetid: 5d2e4c68-7e0b-4405-8919-f5b203e46770
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b85a6a5e79c004eb3ed2c7c40c6e3b62d526e95a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62721014"
---
# <a name="rename-a-stored-procedure"></a>ストアド プロシージャの名前の変更
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] または [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用して、 [!INCLUDE[tsql](../../includes/tsql-md.md)]でストアド プロシージャの名前を変更する方法について説明します。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [Security](#Security)  
  
-   **ストアド プロシージャの名前を変更するために使用するもの:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   プロシージャ名は、 [識別子](../databases/database-identifiers.md)のルールに従っている必要があります。  
  
-   ストアド プロシージャの名前を変更しても、 **sys.sql_modules** カタログ ビューの定義列にある、対応するオブジェクトの名前は変更されません。 したがって、このオブジェクトの種類の名前を変更しないことをお勧めします。 代わりに、ストアド プロシージャを削除して新しい名前で再作成してください。  
  
-   プロシージャの名前または定義を変更すると、依存オブジェクトを更新してプロシージャに加えられた変更を反映しなければ、その依存オブジェクトが失敗する可能性があります。 詳細については、「 [ストアド プロシージャの依存関係の表示](view-the-dependencies-of-a-stored-procedure.md)」を参照してください。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 CREATE PROCEDURE  
 データベースの CREATE PROCEDURE 権限およびプロシージャの作成先となるスキーマの ALTER 権限、または、 **db_ddladmin** 固定データベース ロールのメンバーシップが必要です。  
  
 ALTER PROCEDURE  
 プロシージャの ALTER 権限、または **db_ddladmin** 固定データベース ロールのメンバーシップが必要です。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-rename-a-stored-procedure"></a>ストアド プロシージャの名前を変更するには  
  
1.  オブジェクト エクスプローラーで、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] に接続し、そのインスタンスを展開します。  
  
2.  **[データベース]** を展開し、プロシージャが属するデータベースを展開し、 **[プログラミング]** を展開します。  
  
3.  [ストアド プロシージャの依存関係を確認します](view-the-dependencies-of-a-stored-procedure.md)。  
  
4.  **[ストアド プロシージャ]** を展開し、名前を変更するプロシージャを右クリックして、 **[名前の変更]** をクリックします。  
  
5.  プロシージャ名を変更します。  
  
6.  依存オブジェクトまたはスクリプトで参照しているプロシージャ名を変更します。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-rename-a-stored-procedure"></a>ストアド プロシージャの名前を変更するには  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]に接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。 この例では、プロシージャを削除した後、新しい名前でプロシージャを再作成することによってプロシージャの名前を変更する方法を示します。 最初の例では、 `'HumanResources.uspGetAllEmployeesTest`という名前のストアド プロシージャを作成します。 2 番目の例では、ストアド プロシージャの名前を `HumanResources.uspEveryEmployeeTest`に変更します。  
  
```sql  
--Create the stored procedure.  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID ( 'HumanResources.uspGetAllEmployeesTest', 'P' ) IS NOT NULL   
    DROP PROCEDURE HumanResources.uspGetAllEmployeesTest;  
GO  
CREATE PROCEDURE HumanResources.uspGetAllEmployeesTest  
AS  
    SET NOCOUNT ON;  
    SELECT LastName, FirstName, Department  
    FROM HumanResources.vEmployeeDepartmentHistory;  
GO  
  
--Rename the stored procedure.  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID ( 'HumanResources.uspGetAllEmployeesTest', 'P' ) IS NOT NULL   
    DROP PROCEDURE HumanResources.uspGetAllEmployeesTest;  
GO  
CREATE PROCEDURE HumanResources.uspEveryEmployeeTest  
AS  
    SET NOCOUNT ON;  
    SELECT LastName, FirstName, Department  
    FROM HumanResources.vEmployeeDepartmentHistory;  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [ALTER PROCEDURE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-procedure-transact-sql)   
 [CREATE PROCEDURE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-procedure-transact-sql)   
 [ストアド プロシージャの作成](../stored-procedures/create-a-stored-procedure.md)   
 [ストアド プロシージャの変更](../stored-procedures/modify-a-stored-procedure.md)   
 [ストアド プロシージャの削除](../stored-procedures/delete-a-stored-procedure.md)   
 [ストアド プロシージャの定義の表示](view-the-definition-of-a-stored-procedure.md)   
 [ストアド プロシージャの依存関係の表示](view-the-dependencies-of-a-stored-procedure.md)  
  
  
