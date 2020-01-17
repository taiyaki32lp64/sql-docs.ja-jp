---
title: ストアド プロシージャの再コンパイル| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.technology: stored-procedures
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- sp_recompile
- WITH RECOMPILE clause
- recompiling stored procedures
- stored procedures [SQL Server], recompiling
ms.assetid: b90deb27-0099-4fe7-ba60-726af78f7c18
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 43ae01b9173693370d5e422d4f26b6175101ff12
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62721037"
---
# <a name="recompile-a-stored-procedure"></a>ストアド プロシージャの再コンパイル
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] を使用して、 [!INCLUDE[tsql](../../includes/tsql-md.md)]でストアド プロシージャを再コンパイルする方法について説明します。 これを行う 3 つの方法:`WITH RECOMPILE`プロシージャ定義内またはプロシージャが呼び出されると、オプション、`RECOMPILE`を使用して個々 のステートメントでクエリ ヒント、`sp_recompile`システム ストアド プロシージャ。 このトピックでは、プロシージャ定義の作成時および既存のプロシージャの実行時に WITH RECOMPILE オプションを使用する方法について説明します。 さらに、sp_recompile システム ストアド プロシージャを使用して既存のプロシージャを再コンパイルする方法についても説明します。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [推奨事項](#Recommendations)  
  
     [Security](#Security)  
  
-   **ストアド プロシージャを再コンパイルするために使用するもの:**  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 作業を開始する準備  
  
###  <a name="Recommendations"></a> 推奨事項  
  
-   プロシージャを初めてコンパイルするときや再コンパイルするとき、データベースおよびそのオブジェクトの現在の状態に合わせてプロシージャのクエリ プランが最適化されます。 データベースのデータまたは構造に大きな変更が加えられた場合、プロシージャを再コンパイルすることにより、その変更に合わせてプロシージャのクエリ プランが更新され、最適化されます。 これにより、プロシージャの処理パフォーマンスが向上します。  
  
-   プロシージャの再コンパイルは、強制的に実行する必要がある場合もあれば、自動的に実行される場合もあります。 自動再コンパイルは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が再起動されるたびに発生します。 また、自動再コンパイルは、プロシージャによって参照されている基になるテーブルの物理デザインが変更された場合にも発生します。  
  
-   プロシージャの再コンパイルを強制的に行うもう 1 つの理由は、プロシージャのコンパイル時に "パラメーターを見つけ出す" 動作の影響を少なくすることです。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でプロシージャが実行されるとき、コンパイル時にプロシージャによって使用されるパラメーター値は、クエリ プランの生成の一部に含まれます。 これらの値が、その後呼び出されるプロシージャの標準的な値を表す場合は、プロシージャのコンパイルや実行のたびに、そのクエリ プランからメリットを得ることができます。 プロシージャのパラメーター値が非定型の値である場合は、プロシージャを強制的に再コンパイルし、異なるパラメーター値に基づく新しいプランを生成することにより、パフォーマンスを向上させることができます。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] には、プロシージャをステートメント レベルで再コンパイルする機能が備わっています。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でストアド プロシージャを再コンパイルすると、プロシージャ全体ではなく、再コンパイルが必要なステートメントだけがコンパイルされます。  
  
-   プロシージャの特定のクエリで通常使用される値が非定型の値や一時的な値である場合は、それらのクエリ内で RECOMPILE クエリ ヒントを使用することにより、プロシージャのパフォーマンスを向上させることができます。 再コンパイルされるのは、プロシージャ全体ではなく、クエリ ヒントを使用したクエリのみであるため、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のステートメント レベルの再コンパイル動作を模倣できます。 ただし、RECOMPILE クエリ ヒントを使用した場合、ステートメントをコンパイルするときに、プロシージャの現在のパラメーター値に加えてストアド プロシージャ内の任意のローカル変数の値も使用されます。 詳細については、「 [クエリ ヒント (Transact-SQL)](/sql/t-sql/queries/hints-transact-sql-query)」を参照してください。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 `WITH RECOMPILE` オプション  
 プロシージャ定義を作成するときにこのオプションを使用する場合、データベースの CREATE PROCEDURE 権限とプロシージャが作成されるスキーマに対する ALTER 権限が必要です。  
  
 EXECUTE ステートメントでこのオプションを使用する場合、プロシージャに対する EXECUTE 権限が必要です。 EXECUTE ステートメント自体に対する権限は必要がありませんが、EXECUTE ステートメント内で参照されているプロシージャに対する実行権限が必要です。 詳細については、「 [EXECUTE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/execute-transact-sql)」を参照してください。  
  
 `RECOMPILE` クエリ ヒント  
 この機能は、プロシージャが作成され、ヒントがプロシージャの [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントに含まれている場合に使用されます。 したがって、データベースの CREATE PROCEDURE 権限と、プロシージャを作成するスキーマに対する ALTER 権限が必要です。  
  
 `sp_recompile` システム ストアド プロシージャ  
 指定したプロシージャに対する ALTER 権限が必要です。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-recompile-a-stored-procedure-by-using-the-with-recompile-option"></a>WITH RECOMPILE オプションを使用してストアド プロシージャを実行するには  
  
1.  [!INCLUDE[ssDE](../../../includes/ssde-md.md)]に接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。 この例では、プロシージャ定義を作成します。  
  
```  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID ( 'dbo.uspProductByVendor', 'P' ) IS NOT NULL   
    DROP PROCEDURE dbo.uspProductByVendor;  
GO  
CREATE PROCEDURE dbo.uspProductByVendor @Name varchar(30) = '%'  
WITH RECOMPILE  
AS  
    SET NOCOUNT ON;  
    SELECT v.Name AS 'Vendor name', p.Name AS 'Product name'  
    FROM Purchasing.Vendor AS v   
    JOIN Purchasing.ProductVendor AS pv   
      ON v.BusinessEntityID = pv.BusinessEntityID   
    JOIN Production.Product AS p   
      ON pv.ProductID = p.ProductID  
    WHERE v.Name LIKE @Name;  
  
```  
  
#### <a name="to-recompile-a-stored-procedure-by-using-the-with-recompile-option"></a>WITH RECOMPILE オプションを使用してストアド プロシージャを実行するには  
  
1.  [!INCLUDE[ssDE](../../../includes/ssde-md.md)]に接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。 この例では、全従業員 (フルネーム) とその役職および部署名をビューから返す単純なプロシージャを作成します。  
  
     次に、2 番目のコード例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。 これにより、プロシージャが実行され、プロシージャのクエリ プランが再コンパイルされます。  
  
```sql  
USE AdventureWorks2012;  
GO  
EXECUTE HumanResources.uspGetAllEmployees WITH RECOMPILE;  
GO  
  
```  
  
#### <a name="to-recompile-a-stored-procedure-by-using-sprecompile"></a>sp_recompile を使用してストアド プロシージャを実行するには  
  
1.  [!INCLUDE[ssDE](../../../includes/ssde-md.md)]に接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。 この例では、全従業員 (フルネーム) とその役職および部署名をビューから返す単純なプロシージャを作成します。  
  
     次に、次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。 この場合、プロシージャは実行されません。代わりに、プロシージャが次回実行されるときにクエリ プランが更新されるように、再コンパイルの対象としてマークされます。  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_recompile N'HumanResources.uspGetAllEmployees';  
GO  
  
```  
  
## <a name="see-also"></a>参照  
 [ストアド プロシージャの作成](../stored-procedures/create-a-stored-procedure.md)   
 [ストアド プロシージャの変更](../stored-procedures/modify-a-stored-procedure.md)   
 [ストアド プロシージャの名前の変更](rename-a-stored-procedure.md)   
 [ストアド プロシージャの定義の表示](view-the-definition-of-a-stored-procedure.md)   
 [ストアド プロシージャの依存関係の表示](view-the-dependencies-of-a-stored-procedure.md)   
 [DROP PROCEDURE &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-procedure-transact-sql)  
  
  
