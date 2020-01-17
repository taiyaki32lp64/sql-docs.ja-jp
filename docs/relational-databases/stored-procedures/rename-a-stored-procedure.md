---
title: ストアド プロシージャの名前の変更 | Microsoft Docs
ms.custom: ''
ms.date: 07/06/2017
ms.prod: sql
ms.technology: stored-procedures
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- stored procedures [SQL Server], renaming
- renaming stored procedures
ms.assetid: 5d2e4c68-7e0b-4405-8919-f5b203e46770
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 177886f6b43e90a094ae69945a1deee7adcab61d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68136687"
---
# <a name="rename-a-stored-procedure"></a>ストアド プロシージャの名前の変更
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] または [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用して、 [!INCLUDE[tsql](../../includes/tsql-md.md)]でストアド プロシージャの名前を変更する方法について説明します。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [セキュリティ](#Security)  
  
-   **ストアド プロシージャの名前を変更するために使用するもの:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   プロシージャ名は、 [識別子](../../relational-databases/databases/database-identifiers.md)のルールに従っている必要があります。  
  
-   ストアド プロシージャの名前を変更しても、`object_id` およびそのプロシージャに明示的に割り当てられているすべてのアクセス許可は保持されます。 オブジェクトを削除し再作成すると、新しい `object_id` を作成し、そのプロシージャに明示的に割り当てられているすべてのアクセス許可を削除します。

-   ストアド プロシージャの名前を変更しても、**sys.sql_modules** カタログ ビューの定義列にある、対応するオブジェクトの名前は変更されません。 そうするには、ストアド プロシージャを削除して新しい名前で再作成してください。  

-   プロシージャの名前または定義を変更すると、依存オブジェクトを更新してプロシージャに加えられた変更を反映しなければ、その依存オブジェクトが失敗する可能性があります。 詳細については、「 [ストアド プロシージャの依存関係の表示](../../relational-databases/stored-procedures/view-the-dependencies-of-a-stored-procedure.md)」を参照してください。  
  
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
3.  [ストアド プロシージャの依存関係を確認します](../../relational-databases/stored-procedures/view-the-dependencies-of-a-stored-procedure.md)。  
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

CREATE PROCEDURE HumanResources.uspGetAllEmployeesTest  
AS  
    SET NOCOUNT ON;  
    SELECT LastName, FirstName, Department  
    FROM HumanResources.vEmployeeDepartmentHistory;  
GO  
  
--Rename the stored procedure.  
EXEC sp_rename 'HumanResources.uspGetAllEmployeesTest', 'uspEveryEmployeeTest'; 
```  
  
## <a name="see-also"></a>参照  
 [ALTER PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-procedure-transact-sql.md)   
 [CREATE PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)   
 [ストアド プロシージャの作成](../../relational-databases/stored-procedures/create-a-stored-procedure.md)   
 [ストアド プロシージャの変更](../../relational-databases/stored-procedures/modify-a-stored-procedure.md)   
 [ストアド プロシージャの削除](../../relational-databases/stored-procedures/delete-a-stored-procedure.md)   
 [ストアド プロシージャの定義の表示](../../relational-databases/stored-procedures/view-the-definition-of-a-stored-procedure.md)   
 [ストアド プロシージャの依存関係の表示](../../relational-databases/stored-procedures/view-the-dependencies-of-a-stored-procedure.md)  
  
  
