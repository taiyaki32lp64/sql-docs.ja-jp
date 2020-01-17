---
title: MSSQLSERVER_4186 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 4186 (Database Engine error)
ms.assetid: 1ae88554-f291-45bc-a186-6f41d9cd0fca
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 53a8e0ab728c1fee0033ef86dbf6b7dfc22bdc8c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62867846"
---
# <a name="mssqlserver4186"></a>MSSQLSERVER_4186
    
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|4186|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名||  
|メッセージ テキスト|列 '%ls.%.*ls' は、OUTPUT 句で参照できません。列定義にサブクエリが含まれているか、列定義でユーザー データまたはシステム データにアクセスする関数を参照しています。 関数は、スキーマ バインドされていない場合、既定でデータ アクセスを実行すると想定されます。 列定義からサブクエリまたは関数を削除するか、OUTPUT 句から列を削除することを検討してください。|  
  
## <a name="explanation"></a>説明  
 非決定的な動作を防ぐために、ビューまたはインライン テーブル値関数から返される列が次のいずれかの方法で定義されている場合、OUTPUT 句ではその列を参照できません。  
  
-   サブクエリ。  
  
-   ユーザー データやシステム データにアクセスするユーザー定義関数、またはそのようなアクセスを行うと想定されるユーザー定義関数  
  
-   ユーザー データやシステム データにアクセスするユーザー定義関数を定義に含む計算列  
  
### <a name="examples"></a>使用例  
 **サブクエリで定義されたビュー列**  
  
 次の例では、選択リストでサブクエリを使用して `State` 列を定義するビューを作成します。 次に、UPDATE ステートメントで OUTPUT 句の `State` 列を参照すると、選択リストのサブクエリが原因でエラーが発生します。  
  
```  
USE AdventureWorks2012;  
GO  
CREATE VIEW dbo.V1  
AS  
    SELECT City,  
-- subquery to return the State name  
           (SELECT Name FROM Person.StateProvince AS sp   
            WHERE sp.StateProvinceID = a.StateProvinceID) AS State  
    FROM Person.Address AS a;  
GO  
--Reference the State column in the OUTPUT clause of an UPDATE statement  
UPDATE dbo.V1   
SET City = City + 'Test'   
OUTPUT deleted.City, deleted.State, inserted.City, inserted.State  
WHERE State = 'Texas';  
GO  
```  
  
 **関数で定義されたビュー列**  
  
 次の例では、データにアクセスするスカラー関数 `dbo.ufnGetStock`を選択リストで使用して `CurrentInventory` 列を定義するビューを作成します。 次に、UPDATE ステートメントで OUTPUT 句の `CurrentInventory` 列を参照します。  
  
```  
USE AdventureWorks2012;  
GO  
CREATE VIEW Production.ReorderLevels  
AS  
    SELECT ProductID, ProductModelID, ReorderPoint,  
           dbo.ufnGetStock(ProductID) AS CurrentInventory  
    FROM Production.Product;  
GO  
  
UPDATE Production.ReorderLevels  
SET ReorderPoint += CurrentInventory  
OUTPUT deleted.ReorderPoint, deleted.CurrentInventory,  
       inserted.ReorderPoint, inserted.CurrentInventory  
WHERE ProductModelID BETWEEN 75 and 80;  
```  
  
## <a name="user-action"></a>ユーザーの操作  
 エラー 4186 は、次のいずれかの方法で解決できます。  
  
-   サブクエリの代わりに結合を使用して、ビューまたは関数の列を定義します。 たとえば、`dbo.V1` ビューは次のように作成し直すことができます。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    CREATE VIEW dbo.V1  
    AS  
        SELECT City, sp.Name AS State  
        FROM Person.Address AS a   
        JOIN Person.StateProvince AS sp   
        ON sp.StateProvinceID = a.StateProvinceID;  
    ```  
  
-   ユーザー定義関数の定義を調べます。 関数でユーザー データまたはシステム データにアクセスしない場合は、WITH SCHEMABINDING 句を含めるように関数を変更します。  
  
-   OUTPUT 句から列を削除します。  
  
## <a name="see-also"></a>参照  
 [OUTPUT 句 &#40;Transact-SQL&#41;](/sql/t-sql/queries/output-clause-transact-sql)  
  
  
